<body>
<h1 class="csdn_top">修改已提交的 git comments 的作者信息（Changing author info）</h1>
<p>最近想把本地的代码库上传到github上，结果上传完毕后才发现作者莫名其妙变成了其他人</p>
<p>
    <img src="http://img.blog.csdn.net/20170717172034138?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWRhbWxldmluZTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt=""></p>
<p>追究原因，发现我用的 smartgit 工具，当初在配置 Comment 信息时，填写了正确的 username，但却随便填写了一个
    useremail为“888888@qq.com”，于是上传到github后，就给我匹配成了github上使用“888888@qq.com”邮箱注册的用户“nuo503”了，当时就郁闷了...................</p>
<p>后来查看github的官方文档，发现有可以修改已提交更改的作者信息的方案，这里是官网的链接：<a target="_blank" href="https://help.github.com/articles/changing-author-info/">Changing
    author info</a></p>
<p>我将其实践了过后，发现可行，于是整理出以下几个步骤：</p>
<p>1.找到当初安装 git 软件时的目录，找到 git-bash.exe 并使用管理员方式运行。</p>
<p>2.从远程 github 上 clone 一个临时的库到本地，运行以下命令即可：</p>
<p><code>git clone --bare https://github.com/你的github账户/你的代码库名.git</code></p>
<p><code></code><img src="http://img.blog.csdn.net/20170717175541899?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWRhbWxldmluZTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt=""><br>
</p>
<p>3.运行上述命令后，会在 git-bash.exe 相对目录下新建 “<code>你的代码库名.git</code>” 的临时库根目录，运行以下命令进入临时库根目录：</p>
<p>cd&nbsp; <code>你的代码库名.git</code></p>
<p><code>4.修改以下命令中的对应参数，并运行该命令：</code></p>
<p><code></code></p>
<pre><code>git filter-branch --env-filter '  
an="$GIT_AUTHOR_NAME"  
am="$GIT_AUTHOR_EMAIL"  
cn="$GIT_COMMITTER_NAME"  
cm="$GIT_COMMITTER_EMAIL"  
if [ "$GIT_COMMITTER_EMAIL" = "[Your Old Email]" ]  
then  
    cn="[Your New Author Name]"  
    cm="[Your New Email]"  
fi  
if [ "$GIT_AUTHOR_EMAIL" = "[Your Old Email]" ]  
then  
    an="[Your New Author Name]"  
    am="[Your New Email]"  
fi  
export GIT_AUTHOR_NAME="$an"  
export GIT_AUTHOR_EMAIL="$am"  
export GIT_COMMITTER_NAME="$cn"  
export GIT_COMMITTER_EMAIL="$cm"  
'  
</code></pre>

<p>贴一个我已经修改好的</p>
<pre><code>git filter-branch --env-filter '  
an="$GIT_AUTHOR_NAME"  
am="$GIT_AUTHOR_EMAIL"  
cn="$GIT_COMMITTER_NAME"  
cm="$GIT_COMMITTER_EMAIL"  
if [ "$GIT_COMMITTER_EMAIL" = "old@163.com" ]  
then  
    cn="xxx123"  
    cm="xxx@qq.com"  
fi  
if [ "$GIT_AUTHOR_EMAIL" = "old@163.com" ]  
then  
    an="xxx123"  
    am="xxx@qq.com"  
fi  
export GIT_AUTHOR_NAME="$an"  
export GIT_AUTHOR_EMAIL="$am"  
export GIT_COMMITTER_NAME="$cn"  
export GIT_COMMITTER_EMAIL="$cm"  
'  
</code></pre>

<p>注意：不要遗漏掉 单引号<br>
<img src="http://img.blog.csdn.net/20170717175521135?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWRhbWxldmluZTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt=""><br></p>
<p></p>
<p><code>5.运行以下命令，强制将本地修改 push 到远程 github 上（建议事先备份代码库）：</code></p>
<p><code></code>git push --force --tags origin 'refs/heads/*'</p>
<p>
    <img src="http://img.blog.csdn.net/20170717175245525?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWRhbWxldmluZTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt=""><br>
</p>
<p>6.运行以下命令，清除本地临时库即可：<br>
    <code>cd ..</code><br>
    <code>rm -rf repo.git</code></p>
<p><code><br>
</code></p>
<p><code>最后，给大家看看我成功修改作者信息后的截图：</code></p>
<p><code><img src="http://img.blog.csdn.net/20170717175745444?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYWRhbWxldmluZTc=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center" alt=""></code><br>
</p>
<p></p><p>追加命令</p><p></p>
<pre><code>git config --list   可以查看配置的一些东西。可以看到user.name 和user.email  分别是什么。。
                    如果你没有初始化过。那么直接：
git config --global user.name "输入你的用户名"
git config --global user.email "输入你的邮箱"
                    这样就可以初始化了。
如果你已经初始化过了，但是不小心把邮箱和用户名输错了，那么就要修改了。
git config --global --replace-all user.email "输入你的邮箱" 
git config --global --replace-all user.name "输入你的用户名"
</code></pre>

<p><a href="http://blog.csdn.net/adamlevine7/article/details/75257766">感谢原作者</a></p>



<!-- This document was created with MarkdownPad, the Markdown editor for Windows (http://markdownpad.com) -->
</body>