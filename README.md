# HowToUseModerncv
使用Latec+moderncv编写简历
* 前言
  这事还得从2016年年末说起，因为当时不想在医疗这边干了，就想换个工作，正
  好有一个朋友在金山，我想去北京看看也是可以的，于是就直接从某人才市场
  的网站上填了一份简历，保存成Word格式发给了她，发给了她。金山和微软也
  算是冤家了吧，至少在字处理软件这块。后来我就转了手pdf格式。但是那真叫一个难看，low的不要不
  要的。正愁没有着，天上掉下个粘豆包，让我知道了还有Latex这么个东西，
  想想也真是汗颜，做为计算机科班出身，又工作多年，竟然不知道Latex，难
  怪挣钱少，不愿天，不愿地，只愿自己没多学习。虽然最后没有去金山，但是
  因为找到了Latex这么好玩的东西，我就在东软又这么混了一年，今天和大家
  分享一下使用Latex+moderncv编写简历的方法，希望大家从我软走出去都能找
  到好工作，也显得我软出去的人不那么low，因为使用Latex生成的简历，面试
  官会高看一眼(除非面试官太水了)。
  
* Tex, Latex, TexLive, tex编译器之间的关系
  Tex就是一种宏语言，它的作者是Donald E. Knuth，这里顺便向这位神一样的前
  辈表示敬意。Tex只定义了最基本操作，类似于编程语言，只是它只用来排版。
  
  Tex就只有一种Tex, 但是基于Tex出现了很多Tex的封装，这种封装完的东西
  叫做宏集，这种宏集更像是一组函数库，使用宏集就可以更轻松的对文档进行排版了，
  其中最常用的，也是最著名的就是由Leslie Lamport开发的Latex。
  
  那有了编程语言了，也有了基础的函数库了，我们还需要编译器或解释器才能
  把我们的程序变为计算机可以执行的程序。这种排版系统的编译器也像编程语
  言一样有很多种编译器，常用的有TexLive, CTex等。
  
  有了语言，有了函数库，又有了编译器，我们当然还需要编辑器。
  与我们日常写程序一样，我们可以使用IDE，也可以使用Emacs/Vi编辑器，
  甚至可以使用记事本。但我们选择工具的目的一定是最能提高生产效率的工具。
  记事本肯定不会最高效，IDE工具比较适合非计算机专业人士使用。
  对于程序员，我还是推荐大家使用Emacs或Vi, 我本人更推荐使用Emacs，因为我就用
  Emacs。
  明白了以上内容，我们就开始准备我们的环境了。
  
* 安装Tex发行版
  因为我使用的是Ubuntu，所以就直接安装TexLive。
  TexLive可以到阿里云上下载安装iso文件。
  http://mirrors.aliyun.com/CTAN/systems/texlive/Images/
  下载后，挂载iso文件。
  sudo mount -t iso9660 -o ro,loop,noauto /yourISOFileDictory/texlive.iso
  /mnt"
  mount后，进入/mnt目录，使用下面命令安装
  sudo ./install-tl
  也可以使用参数--gui进入图形界面安装方式。
  安装完成后，卸载镜像
  sudo unmount /mnt
  增加环境变量并加入到
  PATH中。注意PATH中各路径要有:分隔。
  完成以上步骤，我们可以在任意目录下输入latex --version看看是否安装成
  功，如果提示latex找不到，可能是安装出了问题或是没有把latex路径加入到
  PATH中。
  
* 安装Emacs+AUCTex插件
  对于使用其它编辑器的同学可以跳过此步。
  Emacs的安装与使用还是比较麻烦的，初学者需要经过很多折腾才能正常使用，
  为了节约篇幅，在此略过，另外我再写文章专门介绍Emacs。
  AUCTex插件因为在Emacs插件服务器上有，与其它插件安装相同，所以折腾过
  Emacs后，也就自然知道如何安装插件了。
  这里也不再赘述。
  
* 安装moderncv
** 为什么使用moderncv  
   有了Tex发行版与Tex编辑器，我们就可以编写tex文件并生成pdf了。
   但是自已手动编写简历还是有点力不从心，所以我们要使用moderncv制作好的
   模板来编写简历。
   在CTAN网站上可以下载moderncv，并解压到本地任意目录。
   
** moderncv简介
   moderncv的目录下，主要是一些sty文件与一个cls文件及examples目录。
   其中cls是class文件，它规范了某一类型的文件排版格式，如article就是论
   文，book就是书。不同类型文件共通的东西就是由cls来规范的，因为我们要使
   用moderncv来制作简历，所以moderncv中的cls提供的就是简历的基本格式，但
   这种基本格式比较笼统，还需要由sty文件进行补充，sty文件就是style
   文件。同一个cls文件与不同的sty文件组合就呈现出整体相似，但细节有差
   别的效果。所以cls文件类似于我们是编写一个动态库还是编写一个应用程序
   的模板，而sty文件类似于我们所使用的库或者叫做包(package)。
   examples目录中是一些tex例子及这些tex生成的pdf文件。大家可以先看看这
   种pdf简历是不是比Word做出来的简历更漂亮。
   这里的tex有英文的，有中文的，还有一个好像是法文，我不认识，但是感觉
   很多单词可以当英文看。
   因为我们要修改一些文件，所以在这之前，最好把moderncv目录备份一下。
   
** 制作简历
   我们可以先将examples目录中的中文tex文件生成pdf，如果没有错误，
   那么我们就可以使用这个tex文件做为基础，加以修改就可以了。如果不能正
   确的生成pdf，应该是对于中文字符的处理出现了问题，找一个适合自已Tex
   发行版的中文解决方法替换文件中的中文处理方法。
   这个tex文件中，有一些是可选的，有一些是必选的，可选的内容我们可以随
   意注释，不会影响简历的排版效果，但是当有必选的内容是我们不需要的时
   候，
   删除这些内容就会导致排版错误。
   先把这个tex文件浏览一遍，看看都是由什么内容构成的。
   注意%开头的行是注释，在这里主要是说明作用。
   有效内容第一行就是
   \documentclass[11pt,a4paper,sans]{moderncv}
   这句话说的是这个文件的类型是moderncv即简历，使用的默认字体是sans,
   字号11pt，纸张大小是A4.
   第二行是
   \moderncvstyle{casual}
   这句的意思是我们简历的风格是casual风格，可选的风格还有classic,
   oldstyle, banking三种。这里有注意一下，当使用casual风格时，某些
   section(注：section是文章的内容的一种分级，如章，节，段)是不能删除
   的，一但删除，后面的地址，电话等信息就显示不出来了。
   建议大家把这里修改成classic风格，确实也是比较经典。
   下面的一些信息大家一看就懂的，我就不多说了。
   在个人信息中，文件里没有列出\social这个命令，这个命令还是很好的，可
   以显示一些社交信息，如\social[linkedin]{lostinternet}显示领英信息，
   \social[github]{lostinternet}显示GitHub信息，加上GitHub信息还是能让
   你的简历加分不少的。
   之后就是各个section, 有你的教育背影，工作经历，语言技能，计算机技能，个人兴趣等等。
   自已想填就填，不想填就注释掉或删掉。
   这里的例子中不同section中使用的排版命令是不同的，
   \cventry代表一个工作或学习经历
   \cvitem就是一个条目加一个说明。
   \cvitemwithcomment就是比cvitem多一个注解。
   \cvdoubleitem就是每一行有两个条目。
   可以把某个命令复制需要的位置使用。
   有了这些内容，就开始动手做一个让你自已満意的简历吧。
   
* 最后
  使用latex做的简历，是很容易一眼就看出来的，对于一个软件行业的面试官
  来说，一份latex简历，必然给你加分不少，如果你再使用Emacs，那又加分不
  少，如果你还是在linux系统下写的，那么这样的员工谁会不想要呢。
  如果你还有一个好的学历，很牛X的能力，很漂亮的履历，必然会要到丰厚的蔪水
  的。
  
