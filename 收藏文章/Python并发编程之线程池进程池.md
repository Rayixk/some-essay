<body>
<h2>Python并发编程之线程池/进程池</h2>
<h3>引言</h3>
<p>Python标准库为我们提供了threading和multiprocessing模块编写相应的多线程/多进程代码，但是当项目达到一定的规模，频繁创建/销毁进程或者线程是非常消耗资源的，这个时候我们就要编写自己的线程池/进程池，以空间换时间。但从Python3.2开始，标准库为我们提供了concurrent.futures模块，它提供了ThreadPoolExecutor和ProcessPoolExecutor两个类，实现了对threading和multiprocessing的进一步抽象，对编写线程池/进程池提供了直接的支持。</p>
<h3>Executor和Future</h3>
<p>concurrent.futures模块的基础是Exectuor，Executor是一个抽象类，它不能被直接使用。但是它提供的两个子类ThreadPoolExecutor和ProcessPoolExecutor却是非常有用，顾名思义两者分别被用来创建线程池和进程池的代码。我们可以将相应的tasks直接放入线程池/进程池，不需要维护Queue来操心死锁的问题，线程池/进程池会自动帮我们调度。</p>
<p>Future这个概念相信有java和nodejs下编程经验的朋友肯定不陌生了，你可以把它理解为一个在未来完成的操作，这是异步编程的基础，传统编程模式下比如我们操作queue.get的时候，在等待返回结果之前会产生阻塞，cpu不能让出来做其他事情，而Future的引入帮助我们在等待的这段时间可以完成其他的操作。关于在Python中进行异步IO可以阅读完本文之后参考我的Python并发编程之协程/异步IO。</p>
<p>p.s: 如果你依然在坚守Python2.x，请先安装futures模块。</p>
<h3>使用submit来操作线程池/进程池</h3>
<p>我们先通过下面这段代码来了解一下线程池的概念</p>
<pre><code># example1.py
from concurrent.futures import ThreadPoolExecutor
import time
def return_future_result(message):
time.sleep(2)
return message
pool = ThreadPoolExecutor(max_workers=2)  # 创建一个最大可容纳2个task的线程池
future1 = pool.submit(return_future_result, ("hello"))  # 往线程池里面加入一个task
future2 = pool.submit(return_future_result, ("world"))  # 往线程池里面加入一个task
print(future1.done())  # 判断task1是否结束
time.sleep(3)
print(future2.done())  # 判断task2是否结束
print(future1.result())  # 查看task1返回的结果
print(future2.result())  # 查看task2返回的结果
</code></pre>

<p>我们根据运行结果来分析一下。我们使用submit方法来往线程池中加入一个task，submit返回一个Future对象，对于Future对象可以简单地理解为一个在未来完成的操作。在第一个print语句中很明显因为time.sleep(2)的原因我们的future1没有完成，因为我们使用time.sleep(3)暂停了主线程，所以到第二个print语句的时候我们线程池里的任务都已经全部结束。</p>
<pre><code>ziwenxie :: ~ » python example1.py
False
True
hello
world
# 在上述程序执行的过程中，通过ps命令我们可以看到三个线程同时在后台运行
ziwenxie :: ~ » ps -eLf | grep python
ziwenxie      8361  7557  8361  3    3 19:45 pts/0    00:00:00 python example1.py
ziwenxie      8361  7557  8362  0    3 19:45 pts/0    00:00:00 python example1.py
ziwenxie      8361  7557  8363  0    3 19:45 pts/0    00:00:00 python example1.py
</code></pre>

<p>上面的代码我们也可以改写为进程池形式，api和线程池如出一辙，我就不罗嗦了。</p>
<pre><code># example2.py
from concurrent.futures import ProcessPoolExecutor
import time
def return_future_result(message):
    time.sleep(2)
    return message
pool = ProcessPoolExecutor(max_workers=2)
future1 = pool.submit(return_future_result, ("hello"))
future2 = pool.submit(return_future_result, ("world"))
print(future1.done())
time.sleep(3)
print(future2.done())
print(future1.result())
print(future2.result())
</code></pre>

<p>下面是运行结果</p>
<pre><code>ziwenxie :: ~ » python example2.py
False
True
hello
world
ziwenxie :: ~ » ps -eLf | grep python
ziwenxie      8560  7557  8560  3    3 19:53 pts/0    00:00:00 python example2.py
ziwenxie      8560  7557  8563  0    3 19:53 pts/0    00:00:00 python example2.py
ziwenxie      8560  7557  8564  0    3 19:53 pts/0    00:00:00 python example2.py
ziwenxie      8561  8560  8561  0    1 19:53 pts/0    00:00:00 python example2.py
ziwenxie      8562  8560  8562  0    1 19:53 pts/0    00:00:00 python example2.py
</code></pre>

<h3>使用map/wait来操作线程池/进程池</h3>
<p>除了submit，Exectuor还为我们提供了map方法，和内建的map用法类似，下面我们通过两个例子来比较一下两者的区别。</p>
<h4>使用submit操作回顾</h4>
<pre><code># example3.py
import concurrent.futures
import urllib.request
URLS = ['http://httpbin.org', 'http://example.com/', 'https://api.github.com/']
def load_url(url, timeout):
    with urllib.request.urlopen(url, timeout=timeout) as conn:
        return conn.read()
# We can use a with statement to ensure threads are cleaned up promptly
with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:
    # Start the load operations and mark each future with its URL
    future_to_url = {executor.submit(load_url, url, 60): url for url in URLS}
    for future in concurrent.futures.as_completed(future_to_url):
        url = future_to_url[future]
        try:
            data = future.result()
        except Exception as exc:
            print('%r generated an exception: %s' % (url, exc))
        else:
            print('%r page is %d bytes' % (url, len(data)))
</code></pre>

<p>从运行结果可以看出，<strong>as_completed不是按照URLS列表元素的顺序返回的</strong>。</p>
<pre><code>ziwenxie :: ~ » python example3.py
'http://example.com/' page is 1270 byte
'https://api.github.com/' page is 2039 bytes
'http://httpbin.org' page is 12150 bytes
</code></pre>

<h4>使用map</h4>
<pre><code># example4.py
import concurrent.futures
import urllib.request
URLS = ['http://httpbin.org', 'http://example.com/', 'https://api.github.com/']
def load_url(url):
    with urllib.request.urlopen(url, timeout=60) as conn:
        return conn.read()
# We can use a with statement to ensure threads are cleaned up promptly
with concurrent.futures.ThreadPoolExecutor(max_workers=3) as executor:
    for url, data in zip(URLS, executor.map(load_url, URLS)):
        print('%r page is %d bytes' % (url, len(data)))
</code></pre>

<p>从运行结果可以看出，<strong>map是按照URLS列表元素的顺序返回的</strong>，并且写出的代码更加简洁直观，我们可以根据具体的需求任选一种。</p>
<pre><code>ziwenxie :: ~ » python example4.py
'http://httpbin.org' page is 12150 bytes
'http://example.com/' page is 1270 bytes
'https://api.github.com/' page is 2039 bytes
</code></pre>

<h4>第三种选择wait</h4>
<p>wait方法接会返回一个tuple(元组)，tuple中包含两个set(集合)，一个是completed(已完成的)另外一个是uncompleted(未完成的)。使用wait方法的一个优势就是获得更大的自由度，它接收三个参数FIRST<em>COMPLETED, FIRST</em>EXCEPTION 和ALL<em>COMPLETE，默认设置为ALL</em>COMPLETED。</p>
<p>我们通过下面这个例子来看一下三个参数的区别</p>
<pre><code>from concurrent.futures import ThreadPoolExecutor, wait, as_completed
from time import sleep
from random import randint
def return_after_random_secs(num):
    sleep(randint(1, 5))
    return "Return of {}".format(num)
pool = ThreadPoolExecutor(5)
futures = []
for x in range(5):
    futures.append(pool.submit(return_after_random_secs, x))
print(wait(futures))
# print(wait(futures, timeout=None, return_when='FIRST_COMPLETED'))
</code></pre>

<p>如果采用默认的ALL_COMPLETED，程序会阻塞直到线程池里面的所有任务都完成。</p>
<pre><code>ziwenxie :: ~ » python example5.py
DoneAndNotDoneFutures(done={
&lt;Future at 0x7f0b06c9bc88 state=finished returned str&gt;,
&lt;Future at 0x7f0b06cbaa90 state=finished returned str&gt;,
&lt;Future at 0x7f0b06373898 state=finished returned str&gt;,
&lt;Future at 0x7f0b06352ba8 state=finished returned str&gt;,
&lt;Future at 0x7f0b06373b00 state=finished returned str&gt;}, not_done=set())
</code></pre>

<p>如果采用FIRST_COMPLETED参数，程序并不会等到线程池里面所有的任务都完成</p>
<pre><code>ziwenxie :: ~ » python example5.py
DoneAndNotDoneFutures(done={
&lt;Future at 0x7f84109edb00 state=finished returned str&gt;,
&lt;Future at 0x7f840e2e9320 state=finished returned str&gt;,
&lt;Future at 0x7f840f25ccc0 state=finished returned str&gt;},
not_done={&lt;Future at 0x7f840e2e9ba8 state=running&gt;,
&lt;Future at 0x7f840e2e9940 state=running&gt;})
</code></pre>

<h4>References</h4>
<p><a href="https://docs.python.org/3/library/concurrent.futures.html" target="_blank" rel="external">DOCUMENTATION OF CONCURRENT-FUTURES</a></p>
<p><a href="http://python.jobbole.com/87272/">感谢原作者</a></p>


<!-- This document was created with MarkdownPad, the Markdown editor for Windows (http://markdownpad.com) -->
</body>