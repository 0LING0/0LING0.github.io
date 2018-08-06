---
layout: post
title: 如何用jekyll和github搭建一个博客
---

花了三四天的时间，终于将自己的博客搭建成功，虽然还是毛坯房，简陋了些，但感觉像有了自己的小窝一样，很开心。尽管如此，心里还是不敢太兴奋，因为实在不知道jekyll会不会突然又报出一个什么error，汗！！另外还要十分感谢计算机系高材生小其同学的指点与帮助，不然真是不知道还要花多长时间。

关于jekyll建博，网上有很多教程，写得也非常详细，但是我的搭建过程并不顺利，应该说是磕磕绊绊，因为遇到了很多教程中没有提到的问题，自然，因为大家用的电脑不同，系统不同，自然问题也是千奇百怪，就像每个人都有自己的独一无二的生命历程一样，遇到问题不要逃避，多搜索，多请教别人，总能够找到方法。下面我把自己的搭建过程记录下来，作为几天折腾的总结。

6月份的时候就有尝试过在github上搭建，但是当时心浮气躁，看了几天的教程更是云里雾里，遂放弃。最近是在知乎上了解到百度前端学院，顺藤摸瓜地看了好几位大牛的github和个人博客，便决心一定要好好搭建个博客。

如果不想买域名的话，那就先用github.io的个人博客页面。这里有两种方式搭建：1.fork 别人的模板，然后把github项目（repositories）名称改成 你的用户名.github.io, 在网址栏输入 username.github.io，就可以看到你的博客界面了。接下来你可以利用github 在线的markdown编辑工具prose（网址prose.io）编辑你想要的内容  2.利用jekyll本地搭建，上传到github,记得也把项目名称改成 username.github.io, 然后本地用你喜欢的编辑器来编辑，我是用的sublime；jekyll 服务默认4000端口，所以可以边修改边在浏览器上本地看效果，直到自己满意了，就可以在git bash 中输入命令提交到github上了（这里只要在本地打开控制台运行jekyll serve, 页面就是实时更新的，很好用）

第一种方法很简便快捷，我尝试过，可是在prose里面修改后，post文章在博客里面怎么都看不到，页面也刷新不了，无奈之下只好采取第二种办法。实践证明，如果你想有一个属于自己的DIY博客，本地安装jekll是首选。因为它允许你用喜欢的编辑器随心所欲地装扮你的博客，并且实时报错，多么地人性化。

好了，先理清一下思路，jekyll是用来本地写静态博客的，写好了之后你可以托管到github上，那么别人访问网址就可以看到了。

所以，第一步，先注册一个github账号吧，然后下载git,百度上搜索就可以，装好后打开git bash控制台，打开是下面这样的。
![1]({{ site.baseurl }}/images/cre-blog-1.png)

然后依次输入以下两行命令：     
ssh-keygen -t rsa -C "email address"          
cat ~/.ssh/id_rsa.pub   

email address就是你的注册邮箱。输入第二行命令的时候会出现一长串密钥一样的字母，我们要把它复制到github上。登录你的github,点开setting，再点击ssh,你会看到 New SSH key的按键，点击
![3]({{ site.baseurl }}/images/cre-blog-3.png)

这里注意git bash控制台好像是不能直接复制的，所以需要找到id_rsa.pub文件，用记事本打开，然后再复制。我的是在c盘下面，C:\Users\Administrator\.ssh 文件夹里面，如果实在找到不到，就直接搜索框搜吧。   

添加成功后在git bash中输入第三行命令   
ssh -T git@github.com

顺利的话，就会出现你的用户名，告诉你已经配置成功，如下图。
![2]({{ site.baseurl }}/images/cre-blog-2.png)

然后回到网站上看看刚刚添加的SSH key 有没有变绿。变成绿色的话说明已经配置成功了，以防万一，我们再试一下，在github中新建一个带readme的项目，然后在git bash中输入  git clone url    (这个url是刚刚新建的项目的url)    
打开刚刚操作的那个盘，会发现已经克隆完成，那么现在我们来做一些改动，随便在里面新建一个记事本吧。然后bash中输入下面三行命令：   
git add .    (如果出错的话输入git init后再输这个)   
git commit -m "xxxx"   (引号里面一定要写点什么，不然同步不了)   
git push origin master    (这里会弹出对话框让你输邮箱和密码，直接输吧)   

控制台没报错的话就到github网站上看看刚刚那个项目是不是更新了，到这里我们的git配置就算完成了。如果由于某种原因你需要重新操作这个步骤，配置SSH的话，记得删掉github上的ssh,同时删掉本地的.SSH文件夹。

另外摘录几个git常用命令：   
$ git init 在当前目录新建一个git代码库   
$ git status  显示有变更的文件   
$ git reset   重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
—————————————————————————————————————

OK，到现在我们已经成功了一半，接下来就是在本地安装jekyll,安装过程比较繁琐，也可能遇到很多问题，静下心来，多搜索，多请教，不要着急，慢慢来。O(∩_∩)O

Jekyll的工作原理就是把markdown文件编译处理生成HTML文件，我是根据这篇教程来安装的,[Run jekyll on windows](http://jekyll-windows.juthilo.com/), 共5步，一步一步跟着来，不要着急。   
1. 安装Ruby 和Ruby Devkit。 Ruby 里面有个gem安装包，安装成功后，就可以在控制台输入命令“gem install xxxx”来安装各种软件，jekyll就是其中一种   
2. 输入命令 gem install jekyll  安装jekyll 
3. 安装Rouge(gem install rouge),Python,以及pip。这里需要注意一下pip的安装，安装过程中你会遇到下面这个界面    

![4]({{ site.baseurl }}/images/cre-blog-4.png)

不要紧张，把它全部复制下来，然后文件名改为get-pip.py,接着在控制台运行 python get-pip.py就会进行安装了。

4.安装watch,这一步好像不装也可以，想装的话就按照它那个命令。   
5.到这里差不多已经安装成功了，输入Jekyll new myblog命令，会看到新建成功了一个myblog文件夹，把它上传到github上，并命名为 你的用户名.github.io。在命令行打开该文件，输入jekyll serve,于是在127端口就能看到博客啦，方便进行本地调试。
这里如果没有连上github并更改命名的话，本地4000端口是显示不出来的，具体原因我还不清楚，留待以后解决吧。

<br/>
<br/>
<hr>
git常见问题总结

1.如果提交时报错     

To git@git.oschina.net:yangzhi/hello.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@git.oschina.net:yangzhi/hello.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushin
hint: to the same ref. You may want to first merge the remote changes (e.g.
hint: 'git pull') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.   

可以输入：git push -f

——————2018/8/3更新
git 提交命令
~~~javascript
git init
git add .
git commit -m "commit名称"
git remote add origin https://github.com/0LING0/text.git
git push origin master  //如果不行的话，后面加-f
~~~
