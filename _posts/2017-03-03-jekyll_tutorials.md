---
layout: post
title: Windows平台利用Jekyll搭建博客
date: 2017-03-03 
tags: 博客   
---
　本文修改自[leopard的教程](http://baixin.io/2016/10/jekyll_tutorials1/)，如为linux或Mac用户请直接查看原教程。
---
  原文博主是用Mac搭建的，而一部分想要尝试搭建博客的朋友可能使用的是windows平台。而windows平台与Mac，linux上搭建的过程有些小差异。本文在windows平台操作，添加了些原文未写的错误和解决方法，较原文流程更详细些。[博客模板效果](http://baixin.io/#blog)。


### 介绍

 　Jekyll 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过 Markdown （或者 Textile） 以及 Liquid 转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。Jekyll 也可以运行在 GitHub Page 上，也就是说，你可以使用 GitHub 的服务来搭建你的项目页面、博客或者网站，而且是完全免费的

　使用 Jekyll 搭建博客之前要确认下本机环境，Git 环境（用于部署到远端）、[Ruby](http://www.ruby-lang.org/en/downloads/) 环境（Jekyll 是基于 Ruby 开发的）、包管理器 [RubyGems](http://rubygems.org/pages/download) 。  
　　Jekyll 是一个免费的简单静态网页生成工具，可以配合第三方服务例如： Disqus（评论）、多说(评论) 以及分享 等等扩展功能，Jekyll 可以直接部署在 Github（国外） 或 Coding（国内） 上，可以绑定自己的域名。[Jekyll中文文档](http://jekyll.bootcss.com/)、[Jekyll英文文档](https://jekyllrb.com/)、[Jekyll主题列表](http://jekyllthemes.org/)。

### 第一步：安装Ruby
　[Ruby官网下载地址](http://rubyinstaller.org/downloads/)笔者使用的是2.33
　安装注意：
> 1.下载时选择正确版本（32/64位）
> 2.环境变量的设定：此电脑->右键属性->高级系统设置->如图

![](/images/posts/jekyll(2)/image2.png)
![](/images/posts/jekyll(2)/image3.png)
安装后，通过在命令行中输入以下命令来确保一切工作正常：
```
$ ruby -v
ruby 2.3.3
```
如果一切工作正常，将会输出所安装的 Ruby 解释器的版本.

### 第二步：安装RubyGems
[RubyGems下载地址](http://rubygems.org/pages/download)
随后进入安装位置shift+右键打开命令行运行以下代码（打开命令行的方法下文还将用到）：

```
ruby setup.rb
```

**安装Devkit**
　Windows下通过执行bundle     install命令来安装时（稍后讲提到），可能会提示错误信息，是一个叫Devkit的东西没有安装，需要安装它才行。　
　DevKit 是windows平台下编译和使用本地C/C++扩展包的工具。它就是用来模拟Linux平台下的make, gcc, sh来进行编译。下载的网址同上，往下翻便能看到。安装时自己选文件夹安装。
　然后Cmd运行以下代码：
```
$ ruby dk.rb init
$ ruby dk.rb install
```

### 第三步：Bundler

```
$ gem install bundler
```

将提示： 

```
Fetching: bundler-1.13.5.gem (100%)
Successfully installed bundler-1.13.5
Parsing documentation for bundler-1.13.5
Installing ri documentation for bundler-1.13.5
Done installing documentation for bundler after 5 seconds
1 gem installed

```
执行 $ jekyll server  时，提示

```

Could not find proper version of jekyll (3.1.1) in any of the sources
Run `bundle install` to install missing gems.

```

跟着提示运行命令

```
$ bundle install
```

这个时候你可能会发现 bundle install 运行卡主不动了。

如果很长时间都没任何提示的话，你可以尝试修改 gem 的 source

```
$ gem sources --remove https://rubygems.org/
$ gem sources -a http://ruby.taobao.org/
$ gem sources -l
*** CURRENT SOURCES ***

http://ruby.taobao.org

```

再次执行命令 $ bundle install，发现开始有动静了

```
Fetching gem metadata from https://rubygems.org/...........
Fetching version metadata from https://rubygems.org/..
Fetching dependency metadata from https://rubygems.org/.
。。。
Installing jekyll-watch 1.3.1
Installing jekyll 3.1.1
Bundle complete! 3 Gemfile dependencies, 17 gems now installed.
Use `bundle show [gemname]` to see where a bundled gem is installed.

```

bundler安装完成

### 第四步：Jekyll 环境配置

安装 jekyll

```     
$ gem install jekyll     
```    
创建博客操作

```    
$ jekyll new myBlog  //myBlog为自定义名  
```   

进入博客目录

```
$ cd myBlog  //进入该文件夹
```

启动本地服务

```
$ jekyll serve
```

在浏览器里输入： [http://localhost:4000](http://localhost:4000)，就可以看到你的博客效果了。

![](/images/posts/jekyll(2)/image1.png)

若现出错则查看后面     Q&A

### 五：目录结构
　
　Jekyll 的核心其实是一个文本转换引擎。它的概念其实就是： 你用你最喜欢的标记语言来写文章，可以是 Markdown，也可以是 Textile,或者就是简单的 HTML, 然后 Jekyll 就会帮你套入一个或一系列的布局中。在整个过程中你可以设置URL路径, 你的文本在布局中的显示样式等等。这些都可以通过纯文本编辑来实现，最终生成的静态页面就是你的成品了。

 一个基本的 Jekyll 网站的目录结构一般是像这样的：

```
.
├── _config.yml
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   ├── post.html
|   └── page.html
├── _posts
|   └── 2016-10-08-welcome-to-jekyll.markdown
├── _sass
|   ├── _base.scss
|   ├── _layout.scss
|   └── _syntax-highlighting.scss
├── about.md
├── css
|   └── main.scss
├── feed.xml
└── index.html

```

这些目录结构以及具体的作用可以参考 [官网文档](http://jekyll.com.cn/docs/structure/) 

进入 _config.yml 里面，修改成你想看到的信息，重新 jekyll server ，刷新浏览器就可以看到你刚刚修改的信息了。

到此，博客初步搭建算是完成了，

### 六：博客部署到远端 

　我这里讲的是部署到 Github Page 创建一个 github 账号，然后创建一个跟你账户名一样的仓库，如原作者的 github 账户名叫 [leopardpan](https://github.com/leopardpan)，原作者的 github 仓库名就叫 [leopardpan.github.io](https://github.com/leopardpan/leopardpan.github.io)，创建好了之后，把刚才建立的 myBlog 项目 push 到 username.github.io仓库里去（username指的是你的github用户名），检查你远端仓库已经跟你本地 myBlog 同步了，然后你在浏览器里输入 username.github.io ，就可以访问你的博客了。
**关于如何使用Github**
首先注册你的github账号并建立库
![](/images/posts/jekyll(2)/image4.png)
然后安装Git[Git下载](https://git-for-windows.github.io/)
在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，
随后输入：
```
$ git config –global user.name “Your Name”
$ git config –global user.email “email@example.com”　
```
**关于如何使用push**
进入你的文件夹目录里shift右键gitbash
```
$ git init
$ git add .
$ git commit -m " init blog "
$ git remote add origin https://github.com/username/username.github.io //自行修改username
$ git push origin master

```
然后进你的github库看看传上去没
推荐使用[SourseTree](https://www.sourcetreeapp.com/)
### 编写文章

　　所有的文章都是 _posts 目录下面，文章格式为 mardown 格式，文章文件名可以是 .mardown 或者 .md。

　　编写一篇新文章很简单，你可以直接从 _posts/ 目录下复制一份出来 `2016-10-16-welcome-to-jekyll副本.markdown` ，修改名字为 2016-10-16-article1.markdown ，注意：文章名的格式前面必须为 2016-10-16- ，日期可以修改，但必须为 年-月-日- 格式，后面的 article1 是整个文章的连接 URL，如果文章名为中文，那么文章的连接URL就会变成这样的：http://baixin.io/2015/08/%E6%90%AD%E5/ ， 所以建议文章名最好是英文的或者阿拉伯数字。 双击 2016-10-16-article1.markdown 打开

```

---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-10-16 11:29:08 +0800
categories: jekyll update
---

正文...

```


title: 显示的文章名， 如：title: 我的第一篇文章                    
date:  显示的文章发布日期，如：date: 2016-10-16                          
categories: tag标签的分类，如：categories: 随笔            

注意：文章头部格式必须为上面的，.... 就是文章的正文内容。

原作者：写文章使用的是 Sublime Text2 编辑器，如果你对 markdown 语法不熟悉的话，可以看看[作业部落的教程](https://www.zybuluo.com/) 
原作者的另一篇文章[Markdown工具](http://baixin.io/2016/11/markdownTool/)


### 使用原文作者的博客模板

虽然博客部署完成了，你会发现博客太简单不是你想要的，你可以查看[Jekyll的一些主题](http://jekyllthemes.org/)，此处安利一下原作者博客模板

首先你要获取博客，[Github项目地址](https://github.com/leopardpan/leopardpan.github.io.git)，你可以直接[点击下载博客](https://github.com/leopardpan/leopardpan.github.io/archive/master.zip)，进去leopardpan.github.io/ 目录下， 使用命令部署本地服务 

```
$ jekyll server   
```
在浏览器输入 [127.0.0.1:4000](127.0.0.1:4000) ， 就可以看到原作者[baixin.io](http://baixin.io)博客效果了

### 修改成你自己的博客

>* 如果你想使用原作者的模板请把 _posts/ 目录下的文章都去掉。
>* 修改 _config.yml 文件里面的内容为你自己的。
>* 如果想要自定义头像，请进images目录下，将用来替换的图片重命名为原来图片的名字 //建议使用[Notepad++](http://rj.baidu.com/soft/detail/13478.html?ald)来修改，下同
>* 进入主目录下找到about.md修改里面的信息改为自己的

然后使用 git push 到你自己的仓库里面去，检查你远端仓库，在浏览器输入 username.github.io 就会发现，你有一个漂亮的主题模板了。
（以上具体操作参考 六：部署到远端）


#### 【 Ps：如果想修改博客样式却不知道怎么修改，可以进原作者的[博客评论下联系](http://baixin.io/2016/10/jekyll_tutorials1/)（我也还在研究中，爱莫能助啊）】

### Q&A：**可能出现的错误**
**1.如果你本机没配置过任何jekyll的环境，可能会报错**
当运行
```
$ jekyll server

```

继续报错

```
Configuration file: /Users/tendcloud-Caroline/Desktop/leopardpan.github.io/_config.yml
  Dependency Error: Yikes! It looks like you don't have jekyll-sitemap or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- jekyll-sitemap' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/! 
jekyll 3.1.1 | Error:  jekyll-sitemap

```
表示 当前的 jekyll 版本是 3.1.1 ，无法使用 jekyll-sitemap 

解决方法有两个

> 1、打开当前目录下的 _config.yml 文件，把 gems: [jekyll-paginate,jekyll-sitemap] 换成 gems: [jekyll-paginate] ，也就是去掉jekyll-sitemap。（这样就可以解决了其实）

> 2、升级 jekyll 版本，原作者使用的是 jekyll 3.1.2 （笔者发现升级后其实还是一样）。

修改完成后保存配置，再次执行

```
$ jekyll server

```
提示

```
Configuration file: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_config.yml
            Source: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github
       Destination: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_site
 Incremental build: disabled. Enable with --incremental
      Generating... 
                    done in 0.901 seconds.
 Auto-regeneration: enabled for '/Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github'
Configuration file: /Users/baixinpan/Desktop/OpenSource/Mine/Page-Blog/leopardpan.github.io-github/_config.yml
    Server address: http://127.0.0.1:4000/
  Server running... press ctrl-c to stop.

```

表示本地服务部署成功。

**2.如果出现此问题**
```
/Library/Ruby/Gems/2.0.0/gems/bundler-1.13.6/lib/bundler/definition.rb:179:in `rescue in specs': Your bundle is **locked to colorator (0.1)**, but that version could not be found in any of the sources listed in your Gemfile. If you haven't changed sources, that means the author of colorator (0.1) has removed it. You'll need to update your bundle to a different version of colorator (0.1) that hasn't been removed in order to install. (Bundler::GemNotFound)
from /Library/Ruby/Gems/2.0.0/gems/bundler-1.13.6/lib/bundler/definition.rb:173:in `specs'
from /Library/Ruby/Gems/2.0.0/gems/bundler-1.13.6/lib/bundler/definition.rb:233:in `specs_for'
from /Library/Ruby/Gems/2.0.0/gems/bundler-1.13.6/lib/bundler/definition.rb:222:in `requested_specs'
from /Library/Ruby/Gems/2.0.0/gems/bundler-1.13.6/lib/bundler/runtime.rb:118:in `block in definition_method'
from /Library/Ruby/Gems/2.0.0/gems/bundler-1.13.6/lib/bundler/runtime.rb:19:in `setup'
from /Library/Ruby/Gems/2.0.0/gems/bundler-1.13.6/lib/bundler.rb:99:in `setup'
from /Library/Ruby/Gems/2.0.0/gems/jekyll-3.3.1/lib/jekyll/plugin_manager.rb:36:in `require_from_bundler'
from /Library/Ruby/Gems/2.0.0/gems/jekyll-3.3.1/exe/jekyll:9:in `'
from /usr/local/bin/jekyll:23:in `load'
from /usr/local/bin/jekyll:23:in `'
```
问题原因在于原作者使用的是colorator (0.1)，而我们使用的是更新的版本，这大概是兼容问题

　　根据原文评论下ID为吴赋的朋友所说“不能用github上clone下来的项目里的Gemfile.lock，而是要用jekyll new XXX生成的项目里的Gemfile.lock。这个文件里记录了本地依赖包的版本，不同电脑上可能存在差别”我们只要把第四步时myblog里的Gemfile.lock拿出来替换原作者的模板即可。
　　右键Gemfilm使用notepad++打开检查是否如下
```
GEM
  remote: https://rubygems.org/
  specs:
    addressable (2.5.0)
      public_suffix (~> 2.0, >= 2.0.2)
    colorator (1.1.0)
    ffi (1.9.17-x64-mingw32)
    forwardable-extended (2.6.0)
    jekyll (3.4.0)
      addressable (~> 2.4)
      colorator (~> 1.0)
      jekyll-sass-converter (~> 1.0)
      jekyll-watch (~> 1.1)
      kramdown (~> 1.3)
      liquid (~> 3.0)
      mercenary (~> 0.3.3)
      pathutil (~> 0.9)
      rouge (~> 1.7)
      safe_yaml (~> 1.0)
    jekyll-paginate (1.1.0)
    jekyll-sass-converter (1.5.0)
      sass (~> 3.4)
    jekyll-watch (1.5.0)
      listen (~> 3.0, < 3.1)
    kramdown (1.13.2)
    liquid (3.0.6)
    listen (3.0.8)
      rb-fsevent (~> 0.9, >= 0.9.4)
      rb-inotify (~> 0.9, >= 0.9.7)
    mercenary (0.3.6)
    pathutil (0.14.0)
      forwardable-extended (~> 2.6)
    public_suffix (2.0.5)
    rb-fsevent (0.9.8)
    rb-inotify (0.9.8)
      ffi (>= 0.5.0)
    redcarpet (3.4.0)
    rouge (1.11.1)
    safe_yaml (1.0.4)
    sass (3.4.23)

PLATFORMS
  x64-mingw32

DEPENDENCIES
  jekyll
  jekyll-paginate
  redcarpet

BUNDLED WITH
   1.14.5
```
在此状态下应该是不会再报错了
3.
> 问题：The CNAME `baixin.io` is already taken 
> 解决：把CNAME里面的baixin.io修改成你自己的域名，如果你暂时没有域名，CNAME里面就什么都不用写。

4.
> 问题： 如果进入setting时发现提示你cname出了什么错误
> 解决：把远端库里的CNAME改成你的github给你创建的默认域名（username.github.io）。

5.
> 问题：A file was included in `你的ID.github.io-master/about.md` that is a symlink or does not exist in your `_includes` directory. For more information, see https://help.github.com/articles/page-build-failed-file-is-a-symlink/.

> 解决：这说明你传上去时可能外面包了个文件夹。正确的上传姿势应该是你的远端仓库一进就是[一堆文件夹的那种样子](https://github.com/leopardpan/leopardpan.github.io/)

6.
> 问题：windows使用git时出现：warning: LF will be replaced by CRLF
> 解决：windows中的换行符为 CRLF， 而在Linux下的换行符为LF，所以在执行add . 时出现提示，gitbash里
```
$ rm -rf .git  // 删除.git  
$ git config --global core.autocrlf false  //禁用自动转换  
```

然后
然后重新执行：
```
$ git init
$ git add . 
```
### 为什么要是用 Jekyll

使用了 Jekyll 你会发现如果你想使用多台电脑发博客都很方便，只要把远端 github 仓库里的博客 clone 下来，写文章后再提交就可以了，Hexo 由于远端提交的是静态网页，所有无法直接写 Markdown 的文章。如果你想看 Hexo 搭建博客，可以看看原作者的另一篇[HEXO搭建个人博客](http://baixin.io/2015/08/HEXO%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)的教程。

如果你在搭建博客遇到问题，可以在[原文博客](http://baixin.io/2016/10/jekyll_tutorials1/)的评论里给原作者提问，也可以在本文下方向我评论（搭建问题应该还是能帮上忙的）。
