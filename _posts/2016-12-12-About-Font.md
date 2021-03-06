---
layout: post
title: web网页中文字体应用指南
---

在 Web 上应用字体是一项基本技术，同时也是一门艺术。而真正的挑战在于中文字体，由于中文字体组成的特殊性导致其体积过于庞大，除了操作系统内置的字体之外，我们很难在网站上应用其他的字体。在可选性很差的前提之下，如何正确的使用中文字体呢?  
首先，以下的字体声明都是很糟糕的，切忌使用:  

font-family: "宋体";  
font-family: "宋体", Arial;   
font-family: Arial, "宋体", "微软雅黑";  
font-family: Helvetica, Arial, "华文细黑", "微软雅黑";  
...  

中文字体也有英文名称。尽管我们在操作系统中常常看到宋体、微软雅黑、华文细黑这样的字体名称，但实际上这只是字体的显示名称，而不是字体文件的名称。所以最好的方法是同时声明中文字体的字体名称（英文）和显示名称（中文），就像这样:  

font-family: SimSun, "宋体";  
font-family: "Microsoft YaHei", "微软雅黑";  
font-family: STXihei, "华文细黑", "Microsoft YaHei", "微软雅黑"; 

永远不要忘记声明英文字体，并且英文字体应该在中文字体之前。记住这个事实：绝大部分中文字体里包含英文字母（但是基本上都很丑），而英文字体里不包含中文字符.   

在网页里中/英文混排是很常见的，你绝对不会喜欢用中文字体显示英文的效果，所以一定不要忘了先声明英文字体：  
font-family: Georgia, SimSun, "宋体";   
font-family: Arial, "Microsoft YaHei", "微软雅黑";   
另外还有一个好习惯，就是在最后补充英文字体族的名称。字体族大体上分为两类：非衬线和衬线。一般来说，你应该这么做：   
font-family: Georgia, SimSun, "宋体", serif;   
font-family: Arial, "Microsoft YaHei", "微软雅黑", sans-serif;  

请注意：以上两句声明中的宋体和微软雅黑不应该调换（尽管调换了也不会发生错误），这是因为从字体的式样来看，微软雅黑是非衬线的，而宋体才是衬线的。然而中文并不像英文那样严格区分字体族，所以这一点在实际应用当中并不那么重要。  

别忘了照顾不同的操作系统   

作为一个 Web 开发者，你理应对 Windows, Mac OS, Linux   家族等常用操作系统里的系统字体有足够的了解，特别是中文。在这里，我们假设目标网站要同时给予 windows 用户和 mac 用户最好的字体体验，于是我们可以这样声明:   

font-family: Helvetica, Tahoma, Arial, STXihei, "华文细黑", "Microsoft YaHei", "微软雅黑", sans-serif;
这句声明都做到哪些事情呢？让我们一一说明（括号内代表其对应的目标操作系统）：  

对于英文字符，首先查找Helvetica(Mac)，然后查找Tahoma(Win)，都找不到就用Arial(Mac&Win)；若是以上三者都缺失，则使用当前默认的sans-serif字体(操作系统或浏览器指定)
对于中文字体，我们已经了解其规则了。华文细黑(Mac)，微软雅黑(Win)是这两个平台的默认中文字体。  

到此为止，我们的字体声明已经很不错了——如果你不必考虑还在使用旧版本操作系统的用户的话。遗憾地是，中文市场还有大量的用户在使用 Windows XP，宋体才是他们的主要中文字体。为了照顾到这些用户，你可以为微软雅黑增加一个 fallback：  

font-family: Helvetica, Tahoma, Arial, STXihei, "华文细黑", Heiti, "黑体", "Microsoft YaHei", "微软雅黑", SimSun, "宋体", sans-serif;   

同样地，你看到我们也为 Mac 系统使用了黑体作为 fallback。    

其他 

不加双引号可以吗？ 

可以。有些英文字体的名称多于两个单词，因为单词中间有空格所以需要用 "" 包裹起来。中文字体很特别，按照英文的角度来看，像微软雅黑究竟算是一个词还是四个词呢？没关系，好在中文字体的名称里没有空格，所以 "" 不加也没什么大碍。 

不过，谁都不能保证在任何操作系统/浏览器环境下都是如此，若是发生了奇怪的事情，不妨加上双引号试试看。  

可以默认显示某种字体吗？比如微软雅黑  

你可能注意到了，在我们最后的字体声明里，华文细黑是默认字体（如果你的系统上安装了声明里所有的中文字体的话），为什么我要先声明 Mac 系统的字体呢？  

按理来说，大多数网站的主要目标市场还是 Windows 用户的，所以理论上这个才是合理的声明：  

font-family: Helvetica, Tahoma, Arial, "Microsoft YaHei", "微软雅黑", SimSun, "宋体", STXihei, "华文细黑", Heiti, "黑体", sans-serif;   

但实际上却并非如此。在中文字体的用户群体里，很大一部分拥有 Mac 的人都同时安装了 Win 下常用的中文字体（这得归功于 Office for Mac）；但极少有 Win 用户去安装 Mac 下的中文字体。  

因此，把 Mac 用字体声明在前面几乎不会对 Win 用户产生什么影响（因为他们压根没有！），倒是用来做 fallback 的黑体可能会取代微软雅黑的位置，所以更保险的做法或许是这样：  

font-family: Helvetica, Tahoma, Arial, STXihei, "华文细黑", "Microsoft YaHei", "微软雅黑", SimSun, "宋体", Heiti, "黑体", sans-serif;  

但无论如何请不要把微软雅黑放在中文字体的最前面，作为史上最丑陋的中文字体之一，微软雅黑实在不是什么好的选择。  

本文摘抄自[ruby-china](https://ruby-china.org/topics/14005)   
