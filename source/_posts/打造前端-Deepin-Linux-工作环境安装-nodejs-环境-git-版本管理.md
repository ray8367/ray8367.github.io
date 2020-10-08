---
title: "打造前端 Deepin Linux 工作环境安装 nodejs 环境,git 版本管理"
date: 2020-10-08 23:54:52
tags: Linux
---

<div id="article_content" class="article_content clearfix">
        <link rel="stylesheet" href="https://csdnimg.cn/release/blogv2/dist/mdeditor/css/editerView/ck_htmledit_views-a405391f94.css">
                <div id="content_views" class="markdown_views">
                     
<p>好的，前面我们已经对系统进行了基本的设置，然后我们从这一篇博文开始，就要非常认真的开始配置我们的工作环境了。</p> 
<p>对了，我们要理解，我们的 <code>deepin linux</code> 系统是基于 <code>Debian</code> 系统开发的，所以，我们在找资料的时候，以 <code>Debian</code> 系统为准。</p> 
<h2 id="安装-nodejs"><a name="t1"></a><a name="t1"></a>安装 nodejs</h2> 
<p>首先，我们打开 <code>nodejs</code> 官方网站 <a href="https://nodejs.org/en/" target="_blank" rel="noopener noreferrer">https://nodejs.org/en/</a> 点击菜单栏的 <strong>Download</strong> 链接，进入下载界面</p> 
<p><img src="https://img-blog.csdn.net/20171103131234544?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="nodejs" title=""></p> 
<p>滚动页面到下面，点击 <code>Installing Node.js via package manager</code> 链接，进入用包管理安装软件的页面。</p> 
<p><img src="https://img-blog.csdn.net/20171103131423598?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="Installing Node.js via package manager" title=""></p> 
<p>点击 <code>Debian and Ubuntu based Linux distributions</code> 跳转到安装指导内容区域</p> 
<p><img src="https://img-blog.csdn.net/20171103131737778?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="Debian and Ubuntu based Linux distributions" title=""></p> 
<p>我们可以看到，执行命令 <code>sudo apt-get install -y nodejs</code> 来进行安装 <code>nodejs</code>，然后我们就打开终端，输入这个命令，然后盲输入密码，就可以安装我们需要的 <code>nodejs</code> 了。</p> 
<blockquote> 
 <p>我大可以直接给出命令，让大家直接执行就好，通过这段在网站的查找资料，是为了告诉大家，如何在网上找我们的需要的资料。</p> 
</blockquote> 
<p><img src="https://img-blog.csdn.net/20171103132310809?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="install nodejs" title=""></p> 
<p>另外，我们还需要安装 <code>npm</code> 包管理器。同样，我们执行命令 </p> 
<pre class="prettyprint" name="code"><code class="language-# hljs lasso has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;">sudo apt<span class="hljs-attribute">-get</span> install <span class="hljs-attribute">-y</span> npm<div class="hljs-button {2}" data-title="复制" data-report-click="{&quot;spm&quot;:&quot;1001.2101.3001.4259&quot;}"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre> 
<p>进行安装。</p> 
<p><img src="https://img-blog.csdn.net/20171103132504234?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="install npm" title=""></p> 
<p>如上图所示，我们输入 <code>npm -v</code> 可看到输出了我们安装的版本号，说明安装已经成功了。</p> 
<p>但是我发现，输入 <code>node</code> 不能进入到 <code>node</code> 环境，而要输入 <code>nodejs</code> 才可以进入环境，这多多少少让我感觉有点不爽。所以我决定做一个命令映射，让我的输入和 <code>mac</code>平台一样。</p> 
<p>首先，我在 <code>~</code> 家目录中，用 <code>ls -a</code> 命令，看是否存在 <code>.bash_profile</code> 文件。看来系统默认是没有这个文件的。</p> 
<p>于是，我用 <code>vim .bash_profile</code> 创建这个文件，录入以下内容：</p> 
<pre class="prettyprint" name="code"><code class="language-# hljs ruby has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;"><span class="hljs-keyword">alias</span> node=<span class="hljs-string">"nodejs"</span><div class="hljs-button {2}" data-title="复制" data-report-click="{&quot;spm&quot;:&quot;1001.2101.3001.4259&quot;}"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre> 
<p><code>:wq</code> 保存退出之后，在终端里输入</p> 
<pre class="prettyprint" name="code"><code class="language-# hljs avrasm has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;">. ~/<span class="hljs-preprocessor">.bash</span>_profile<div class="hljs-button {2}" data-title="复制" data-report-click="{&quot;spm&quot;:&quot;1001.2101.3001.4259&quot;}"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre> 
<p>命令，使我们刚刚输入的内容生效，然后我们输入</p> 
<pre class="prettyprint" name="code"><code class="language-# hljs lasso has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;">node <span class="hljs-attribute">-v</span><div class="hljs-button {2}" data-title="复制" data-report-click="{&quot;spm&quot;:&quot;1001.2101.3001.4259&quot;}"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre> 
<p>看是否能够输出我们的版本号</p> 
<p><img src="https://img-blog.csdn.net/20171103134300194?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="node -v" title=""></p> 
<p>如上图所示，已经和我设想的是一样一样的了。</p> 
<blockquote> 
 <p>其实我们大可以使用 <code>nodejs</code> 来启动 <code>node</code> 环境，我补充这一段内容是为了告诉大家，如何将一个较长的命令，通过我们的 <code>~/.bash_profile</code> 的配置变成一个较短的命令，这样便于我们更好的使用我们的命令行工具。</p> 
</blockquote> 
<h2 id="安装-git-版本工具"><a name="t2"></a><a name="t2"></a>安装 git 版本工具</h2> 
<p>我们在终端中输入</p> 
<pre class="prettyprint" name="code"><code class="language-# hljs 1c has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;">apt-cache search git <span class="hljs-string">| grep ^git</span><div class="hljs-button {2}" data-title="复制" data-report-click="{&quot;spm&quot;:&quot;1001.2101.3001.4259&quot;}"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre> 
<p>来搜索我们的 <code>git</code> 安装包，为什么我后面增加了一个<code>| grep ^git</code> 这样的东西？这是为了过滤我们的信息，默认信息会非常的多，我们可以通过 <code>grep</code> 工具来对各种信息进行过滤。更多内容请参考 <a href="http://blog.csdn.net/fungleo/article/details/76588993" target="_blank" rel="noopener noreferrer">http://blog.csdn.net/fungleo/article/details/76588993</a></p> 
<p><img src="https://img-blog.csdn.net/20171103135220717?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="apt-cache search git" title=""></p> 
<p>我们可以看到，我们要安装的，就叫 <code>git</code>。于是，我们输入</p> 
<pre class="prettyprint" name="code"><code class="language-# hljs lasso has-numbering" onclick="mdcp.copyCode(event)" style="position: unset;">sudo apt<span class="hljs-attribute">-get</span> install git <span class="hljs-attribute">-y</span><div class="hljs-button {2}" data-title="复制" data-report-click="{&quot;spm&quot;:&quot;1001.2101.3001.4259&quot;}"></div></code><ul class="pre-numbering" style=""><li style="color: rgb(153, 153, 153);">1</li></ul></pre> 
<p>安装 <code>git</code> 版本管理工具</p> 
<p><img src="https://img-blog.csdn.net/20171103135424432?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvRnVuZ0xlbw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast" alt="sudo apt-get install git -y" title=""></p> 
<p>如上图所示，我们输入 <code>git --version</code> 可以看到输出了正确的 <code>git</code> 版本号。说明我们的 <code>git</code> 已经安装完成了。</p> 
<blockquote> 
 <p>我在博文中会穿插更多的内容，引申出来一些东西，是为了让大家更好的思考一些东西。我建议大家收藏我的博客，因为我的博客里面干货满满哦！</p> 
</blockquote> 
<p>本文由 FungLeo 原创，原文地址为：<a href="https://blog.csdn.net/FungLeo/article/details/78434813" target="_blank" rel="noopener noreferrer">https://blog.csdn.net/FungLeo/article/details/78434813</a> </p>
                </div><div><div></div></div>
                <link href="https://csdnimg.cn/release/blogv2/dist/mdeditor/css/editerView/markdown_views-10218d227c.css" rel="stylesheet">
                <link href="https://csdnimg.cn/release/blogv2/dist/mdeditor/css/style-57471a2b6e.css" rel="stylesheet">
        </div>
