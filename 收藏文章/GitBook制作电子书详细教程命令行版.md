<h1 class="csdn_top">GitBook制作电子书详细教程（命令行版）</h1>
                
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
<a target="_blank" href="https://github.com/GitbookIO/gitbook" style="color:rgb(166,36,37); outline:none">GitBook</a>&nbsp;是一款基于 Node.js 开发的开源的工具，可以通过命令行的方式创建电子书项目，再使用 MarkDown 编写电子书内容，然后生成 PDF、ePub、mobi 格式的电子书，或生成一个静态站点。</p>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
除此之外，还可以利用 Git 命令管理电子书版本。如果你是 GitHub 的重度使用者，还可以把你的 GitBook 帐户和 GitHub 帐户关联起来，这样不论在任何一方修改了内容，都可以互相同步。</p>
<h2 id="gb_1" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t0"></a>
一、安装 Node.js</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
由于 GitBook 是基于 Node.js 开发的，所以依赖 Node.js 环境。如果您的系统中还未安装 Node.js，请点击下面的链接，根据你所使用的系统下载对应的版本。如果已安装则略过本步骤。</p>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Node.js 下载页面</span>：<a target="_blank" href="https://nodejs.org/en/download/stable/" style="color:rgb(166,36,37); outline:none">https://nodejs.org/en/download/stable/</a></p>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
Windows 版和 Mac 版的 Node.js 都是常规的安装包，连续下一步安装即可。Lunix 版可以参照<a target="_blank" href="https://nodejs.org/en/download/package-manager/" style="color:rgb(166,36,37); outline:none">官方文档</a>通过 yum、apt-get 之类的工具安装，也可以通过源码包安装，如下所示：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">wget</span> https://nodejs.org/dist/v5.4.1/node-v5.4.1.tar.gz
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">tar</span> zxvf node-v5.4.1.tar.gz
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">cd</span> node-v5.4.1
$ ./configure
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">make</span>
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">make</span> <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">install</span></code></pre>
<h2 id="gb_2" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t1"></a>
二、安装 GitBook</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
打开“命令提示符”（Mac 系统打开“终端”）输入以下命令安装 GitBook：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ npm <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">install</span> gitbook-cli -g</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
由于网络的原因，安装的时间可能会较长一些，请耐心等待直到安装完成。安装完成后可以输入以下命令，以查看 GitBook 版本的方式检查是否安装成功：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ gitbook -V</code></pre>
<h2 id="gb_3" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t2"></a>
三、创建电子书项目</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
新建一个目录，并进入该目录使用 gitbook 命令初始化电子书项目。举个例子，现在要创建一个名为“MyFirstBook”的空白电子书项目，如下所示：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">mkdir</span> MyFirstBook
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">cd</span> MyFirstBook
$ gitbook init</code></pre>
<h2 id="gb_4" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t3"></a>
四、编辑电子书内容</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
初始化后的目录中会出现“README.md（电子书简介文件）”和“SUMMARY.md（导航目录文件）”两个基本文件。除此之外还可以手动新建其它“Glossary.md（书尾的词汇表）”、“book.json（电子书配置文件）”。电子书的正文内容可以根据自己的喜好创建新的后缀为 .md 文件，如“chapter01.md”，然后用 MarkDown 编写具体的文本内容即可。下面对这些文件分别做详细介绍。</p>
<h3 id="gb_4_1" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t4"></a>
1、README.md</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
此文件是简单的电子书介绍，可以把您所制作的电子书做一下简单的描述：</p>
<pre class=" language-markdown" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-markdown" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5"># 简介

这是我的第一本使用 GitBook 制作的电子书。</code></pre>
<h3 id="gb_4_2" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t5"></a>
2、SUMMARY.md</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
此为电子书的导航目录文件，每当新增一个章节文件就需要向此文件中添加一条记录。对于 Kindle 电子书来说，此文件所呈现的目录结构就是开头的目录内容和“前往”的目录导航。</p>
<pre class=" language-markdown" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-markdown" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5"># Summary

* [简介](README.md)
* [第一章](section1/README.md)
* [第二章](section2/README.md)</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
如果需要“子章节”可以使用&nbsp;<code style="font-family:Consolas,&quot;Courier New&quot;,monospace; font-size:14px">Tab</code>&nbsp;缩进来实现（最多支持三级标题），如下所示：</p>
<pre class=" language-markdown" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-markdown" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5"># Summary

* [第一章](section1/README.md)
    * [第一节](section1/example1.md)
    * [第二节](section1/example2.md)
* [第二章](section2/README.md)
    * [第一节](section2/example1.md)</code></pre>
<h3 id="gb_4_3" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t6"></a>
3、Glossary.md</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
对于电子书内容中需要解释的词汇可在此文件中定义。词汇表会被放在电子书末尾。其格式如下所示：</p>
<pre class=" break language-markdown" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:break-word; color:rgb(248,248,242); direction:ltr; white-space:pre-wrap; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-markdown" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:break-word; line-height:1.5"># 电子书
电子书是指将文字、图片、声音、影像等讯息内容数字化的出版物和植入或下载数字化文字、图片、声音、影像等讯息内容的集存储和显示终端于一体的手持阅读器。

# Kindle
Amazon Kindle 是由 Amazon 设计和销售的电子书阅读器（以及软件平台）。用户可以通过无线网络使用 Amazon Kindle 购买、下载和阅读电子书、报纸、杂志、博客及其他电子媒体。</code></pre>
<h3 id="gb_4_4" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t7"></a>
4、book.json</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
“book.json”是电子书的配置文件，可以看作是电子书的“原数据”，比如 title、description、isbn、language、direction、styles 等，更多<a target="_blank" href="http://help.gitbook.com/format/configuration.html" style="color:rgb(166,36,37); outline:none">点击这里</a>查看。它的基本结构如下所示：</p>
<pre class=" language-markdown" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-markdown" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">{
    "title": "我的第一本電子書",
    "description": "用 GitBook 制作的第一本電子書！",
    "isbn": "978-3-16-148410-0",
    "language": "zh-tw",
    "direction": "ltr"
}</code></pre>
<h3 id="gb_4_5" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t8"></a>
5、普通章节.md 文件</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
普通章节.md 文件可以使用您感觉顺手的文本编辑器编写。MarkDown 的写法可以<a target="_blank" href="http://help.gitbook.com/format/markdown.html" style="color:rgb(166,36,37); outline:none">点击这里</a>查看相关示例。每编写一个 .md 文件，不要忘了在“SUMMARY.md”文件中添加一条记录哦。</p>
<h3 id="gb_4_6" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t9"></a>
6、电子书封面图片</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
<a target="_blank" href="http://help.gitbook.com/format/cover.html" style="color:rgb(166,36,37); outline:none">GitBook 帮助文档</a>建议封面图片的尺寸为 1800*2360 像素并且遵循建议：</p>
<ul style="font-family:Lora,arial,serif; font-size:17px; line-height:28px; margin:0px 0px 28px 1.5em; padding:0px; border:0px; vertical-align:baseline">
<li style="margin:0px; padding:0px; border:0px; vertical-align:baseline">没有边框</li><li style="margin:3px 0px 0px; padding:0px; border:0px; vertical-align:baseline">
清晰可见的书本标题</li><li style="margin:3px 0px 0px; padding:0px; border:0px; vertical-align:baseline">
任何重要的文字在小版本中应该可见</li></ul>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
图片的格式为 jpg 格式。把图片重命名为“cover.jpg”放到电子书项目文件夹即可。</p>
<h2 id="gb_5" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t10"></a>
五、预览电子书内容</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
电子书内容编写完毕后可以使用浏览器预览一下。先输入下面的命令据 .md 文件生成 HTML 文档：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ gitbook build</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
生成完毕后，会在电子书项目目录中出现一个名为“_book”的文件夹。进入该文件夹，直接用浏览器打开“index.html”，或先输入下面的命令：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ gitbook serve</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
然后在浏览器中输入“<a target="_blank" href="http://localhost:4000/" style="color:rgb(166,36,37); outline:none">http://localhost:4000</a>”即可预览电子书内容，预览完毕后按&nbsp;<code style="font-family:Consolas,&quot;Courier New&quot;,monospace; font-size:14px">Ctrl + C</code>&nbsp;结束。</p>
<h2 id="gb_6" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t11"></a>
六、生成电子书文件</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
确定电子书没有问题后，可以通过输入以下命令生成 mobi 电子书：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ gitbook mobi ./ ./MyFirstBook.mobi</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
如果出现以下错误提示，说明您还未安装 Calibre。由于 GitBook 生成 mobi 格式电子书依赖 Calibre 的 ebook-convert，所以请先<a target="_blank" href="http://kindlefere.com/tools#calibre" style="color:rgb(166,36,37); outline:none">点击这里</a>下载安装 Calibre。</p>
<pre class=" language-markdown" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-markdown" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">Error: Need to install ebook-convert from Calibre</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
Calibre 安装完毕后，对于 Mac OS X 系统，还需要先设置一下软链接：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">ln</span> -s /Applications/calibre.app/Contents/MacOS/ebook-convert /usr/local/bin</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
再次运行转换命令，即可生成 mobi 格式电子书。</p>
<h2 id="gb_7" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t12"></a>
七、把项目托管到 GitBook.com</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
以上所有的步骤都是在本地进行的，如果需要实现电子书的版本管理，或者把电子书发布到网络上，还可以通过 Git 命令将本地的项目托管到 GitBook.com 上。</p>
<h3 id="gb_7_1" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t13"></a>
1、注册 GitHub.com 账号</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
首先进入&nbsp;<a target="_blank" href="https://www.gitbook.com/" style="color:rgb(166,36,37); outline:none">GitBook.com</a>&nbsp;注册一个账号，并新建一个项目。在“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Setting</span>（设置）”页面获取到“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Git
 URL</span>（Git 链接）”，链接的样子如下所示：</p>
<pre class=" language-markdown" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-markdown" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">https://git.gitbook.com/kindlefere/myfirstbook.git</code></pre>
<h3 id="gb_7_2" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t14"></a>
2、安装 Git 软件</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
在开始下面的步骤之前请先确保您的系统中已经安装了 Git。一般 Mac 和 Lunix 自带 Git 功能，可以在终端运行&nbsp;<code style="font-family:Consolas,&quot;Courier New&quot;,monospace; font-size:14px">git --version</code>&nbsp;查看 Git 版本。Windows 一般不会自带 Git 功能，请<a target="_blank" href="https://git-scm.com/downloads" style="color:rgb(166,36,37); outline:none">点击这里</a>下载先安装。</p>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
在安装 Windows 版的 Git 时，会看到“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Use Git from Git Bash only</span>”和“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Use Git from
 the Windows Command prompt</span>”两个选项。前者指的在程序自带的独立终端中使用 Git。后者是指可以通过系统自带的“命令提示符”使用 Git 命令。可以根据自己的喜好选择，个人推荐使用后者。</p>
<h3 id="gb_7_3" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t15"></a>
3、上传已有的电子书项目</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
在本地新建一个文件夹，并通过 Git 命令把刚才新建的远程项目抓取到本地，如下所示：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">mkdir</span> MyFirstBook-Git
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">cd</span> MyFirstBook-Git
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> init
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> pull https://git.gitbook.com/kindlefere/myfirstbook.git
</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
然后把本地项目“MyFirstBook”中的所有内容拷贝到刚才新建的文件夹中，如上面的“MyFirstBook-Git”。然后使用 Git 命令把本地的项目上传到远程，如下所示：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> add -A
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> commit -m <span class="token string" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(166,226,46)">"提交说明"</span>
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> remote add gitbook https://git.gitbook.com/kindlefere/myfirstbook.git
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> push -u gitbook master
</code></pre>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
期间需要输入你的 GitBook 注册邮箱和密码。今后修改内容后只需要输入以下 Git 命令即可：</p>
<pre class=" language-bash" style="margin-top:0.5em; margin-bottom:28px; word-spacing:normal; padding:1em; border:0px; font-size:14px; vertical-align:baseline; font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; max-width:100%; line-height:1.5; overflow:auto; word-wrap:normal; color:rgb(248,248,242); direction:ltr; word-break:normal; background:rgb(39,40,34)" name="code"><code class=" language-bash" style="font-family:Consolas,Monaco,&quot;Andale Mono&quot;,&quot;Ubuntu Mono&quot;,monospace; direction:ltr; word-spacing:normal; word-break:normal; word-wrap:normal; line-height:1.5">$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> add <span class="token punctuation" style="margin:0px; padding:0px; border:0px; vertical-align:baseline">[</span>修改的文件<span class="token punctuation" style="margin:0px; padding:0px; border:0px; vertical-align:baseline">]</span>
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> commit -m <span class="token string" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(166,226,46)">"提交说明"</span>
$ <span class="token function" style="margin:0px; padding:0px; border:0px; vertical-align:baseline; color:rgb(230,219,116)">git</span> push -u gitbook master
</code></pre>
<h2 id="gb_8" style="margin:56px 0px 28px; padding:0px; border:0px; font-size:28px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:36px"><a name="t16"></a>
八、把项目关联到 GitHub 帐户</h2>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
如果你喜欢使用 GitHub 管理项目。还可以把您的 GitBook 帐户和 GitHub 帐户关联起来，这样两者的修改内容就可以互相同步了。</p>
<h3 id="gb_8_1" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t17"></a>
1、关联 GitBook 和 GitHub 帐户</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
关联设置也很简单，首先进入 GitBook 的“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Account Settings</span>（帐户设置）”页面，在“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Profile</span>（个人资料）”标签页找到“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">GitHub</span>”选项卡，点击【Connect
 to GitHub】按钮会转向 GitHub 的“<span style="margin:0px; padding:0px; border:0px; vertical-align:baseline; font-weight:700">Authorize application</span>”页面，点击【Authorize application】按钮即可完成关联。</p>
<h3 id="gb_8_2" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t18"></a>
2、把 GitBook 项目导入到 GitHub</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
完成关联后即可设置同步电子书项目了。以电子书项目“MyFirstBook”为例，首先需要把项目导入到 GitHub 中一份。进入某个电子书项目的设置页面，切换到“GitHub”选项卡。在“GitHub Repository”中，点击【Export to GitHub】按钮，按照向导所示步骤将项目导入 GitHub 中。</p>
<h3 id="gb_8_3" style="margin:42px 0px 28px; padding:0px; border:0px; font-size:24px; vertical-align:baseline; clear:both; font-family:Bitter,STSong,SimSun,Georgia,serif; font-weight:400; letter-spacing:-0.01em; line-height:30px"><a name="t19"></a>
3、设置 GitBook 和 GitHuB 同步</h3>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
导出成功后，再回到 GitBook 项目设置页面的“GitHub”选项卡，在“GitHub Repository”中的输入框中填入 GitHub 的 Repository 名，如“GitHub用户名/myfirstbook”，点击【Save】按钮保存。</p>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
保存后当前页面会出现一个名为“Integration”的选项卡，点击里面的【Add webhook】按钮，允许 GitBook 接收 Github 的内容更新。这样就把 GitBook 上的项目和 GitHub 相对应的项目关联上了。</p>
<p style="margin-top:0px; margin-bottom:28px; padding-top:0px; padding-bottom:0px; font-family:Lora,arial,serif; font-size:17px; line-height:28px; border:0px; vertical-align:baseline">
此后即可用 GitHub 管理电子书项目，在 GitBook 上对电子书内容修改也会自动同步到 GitHub 中。</p>

