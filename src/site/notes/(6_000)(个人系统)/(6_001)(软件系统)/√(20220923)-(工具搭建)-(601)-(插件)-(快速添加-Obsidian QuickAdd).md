---
{"dg-publish":true,"permalink":"/6-000/6-001/20220923-601-obsidian-quick-add/","dgHomeLink":true,"dgPassFrontmatter":false}
---


# <font color=#DC143C>(20220923)-(工具搭建)-(601)-(插件)-(Obsidian QuickAdd)</font>
URL:: [Obsidian 插件之 QuickAdd](https://zhuanlan.zhihu.com/p/386885976)
URL:: [Obsidian最强插件：QuickAdd - 少数派](https://sspai.com/post/69375)

```
dataview
table without id 入榜亮点, 入榜输出
where contains(TITLES, "")
```

```dataview
table without id 萃取重点
where contains(TITLES, "Obsidian QuickAdd")
```

```toc
```

![](https://pic1.zhimg.com/v2-3b3d6e8aee4565cf3970768627777ea2_1440w.jpg?source=172ae18b)

>[!background] 背景介绍
>在过去几个月中，我一直将<strong><font color=#E6E022>Workbench</font></strong>视作是我此生不弃的插件，自从遇到Quickadd后我动摇了。
>2021-07-26更新：我将开发者制作的视频教程搬运到了B站，注意目前还没有任何字幕，所以仅是方便各位参考：[Obsidian插件之QuickAdd使用教程](https://link.zhihu.com/?target=https%3A//www.bilibili.com/video/bv1CA411A71P)

## 01.前言
此前，我在Obsidian中<strong><font color=#9966CC>最主要的需求是将写好的大段文字拆分成一个个小文章、将别人写好的文章拆分成一个个小笔记</font></strong>，<strong><font color=#E6E022>而Workbench以及Note-refactor解决了这两个需求</font></strong>，但是有一个一直无法完全解决的痛点——我就单纯想要选中其中的一部分来发送到自己的Workbench中，由于Workbench作者过去几个月都没有更新过Workbench，我就一直忍着这个来安慰自己这是个伪需求，直至遇到了Quickadd才明白这其实不是伪需求（如果有伪需求能过去几个月都困扰着我那也不是伪需求了）。

## 02.QuickAdd插件简介
>[!summary] 插件介绍
>QuickAdd插件，不如说是Obsidian的小Quicker插件——作者一开始就赋予了QuickAdd<strong><font color=#E6E022>按顺序执行Obsidian内命令的动作序列功能</font></strong>，而其又有<strong><font color=#E6E022>基本的快速编辑文本的功能</font></strong>，甚至还有<strong><font color=#E6E022>执行脚本</font></strong>以及让这些成为一个<strong><font color=#E6E022>多选选择窗口的功能</font></strong>。

其中QuickAdd的<strong><font color=#FF0000>Macro功能</font></strong>(也就是上文说到的动作序列功能)除了成为单独的动作序列功能，也可以<strong><font color=#E6E022>在上文提到的选中文本或者弹出窗口输入文本后执行相应的动作序列功能</font></strong>，也就是<strong><font color=#FF0000>你可以选中文本后再使用Obsidian相关功能将其输入到自己的模板中</font></strong>。

没错，它可以作为参数输入到你的模板文件中。显然这些用法还是脱离大众太远，这里就说我最常用的功能——<strong><font color=#FF4500>裁剪</font></strong>以及<strong><font color=#FF4500>快速插入画板</font></strong>，希望各位可以从这两个小用法上找到自己可能能解决掉的工作流需求。(2021.07.11注：Capture是捕获的意思，此处是错误的翻译，但愿没有引起误会)

## 03.QuickAdd插件用法
### 0301.关于裁剪
>[!attention] 用法总结
><strong><font color=#FF0000>选中文本后插入笔记</font></strong>，目前QuickAdd插件已经更新到0.3.4(截至笔者写作日期)，支持了以下的选项：

![|L](https://pic2.zhimg.com/80/v2-bd3181cf6ba5da477f13108433bb8f8d_1440w.jpg)
+ 裁剪到当前的文档
+ 裁剪到指定的文档，支持日期格式
+ 当文件不存在的时候新建文件
+ 输出的内容为任务格式，也就是附带"`-[]`"
+ 输入到文档的结尾(开启该功能后将覆盖下边的功能)
+ 将此处更改成你所裁剪到的文档的链接
+ 插入到指定文本后
+ 裁剪后输入到文档中的格式

而捕获格式中包含以下的替代符：
+ {{DATE}}：作为<strong><font color=#E6E022>日期</font></strong>的替代符
+ {{VDATE}}：作为<strong><font color=#E6E022>日期</font></strong>的另一种替代符
+ {{NAME}}：作为<strong><font color=#E6E022>文件名</font></strong>的替代符
+ {{VALUE}}：则<strong><font color=#E6E022>充当为你输入或者选择的文本的替代符</font></strong>，即当你没有选择内容的时候，会弹窗让你输入内容
    + {{VALUE:ABC}}：指的是<strong><font color=#E6E022>弹窗会是ABC作为标题</font></strong>
+ {{LINKCURRENT}}：作为<strong><font color=#E6E022>当前笔记的文件链接</font></strong>的替代符
+ {{TEMPLATE}}：则是对应的<strong><font color=#E6E022>模板</font></strong>(也就是你放过去以后要不要再插入个模板)
    + 其中{{TEMPLATE:ABC}}：则<strong><font color=#E6E022>直接插入名为ABC的模板</font></strong>，而如果你不设置这个，就会出现菜单让你选择
+ {{MACRO}}：则是执行对应的Macro序列其中
    + {{MACRO:ABC}}：则指定直接执行名为ABC的序列，而如果你不设置这个，就会出现菜单让你选择
    + 例如，你如果设置了{{DATE:HH:MM}}{{VALUE}}就会在你裁剪的时候生成12:00裁剪内容到此为止，想必大家都能想到这个究竟能不能在自己的工作流中占据一定的地位，对我来说，这个功能极大地丰富了某些插件互动的功能，这个将会在下方的特殊用法中提及，接下来说一下它的序列功能

### 0302.关于序列
>[!example] 步骤1
序列功能的使用方法可能有点绕，首先你需要：
![创建序列](https://pic3.zhimg.com/80/v2-1ba927ef34d0092564730524145e109a_1440w.jpg)

>[!example] 步骤2
然后就会得到一个能够用于执行的序列，然后点击左下角的ManageMacro来到这个界面：
![|L](https://pic1.zhimg.com/80/v2-e64bfa30324b319d79d77c8c60d9cc94_1440w.jpg)

>[!example] 步骤3
点一下Config，可以获得
![|L](https://pic3.zhimg.com/80/v2-6b627055c3b18af189bed07ef1d952fe_1440w.jpg)
然后就按步骤选择或者添加你要的命令、脚本以及序列即可，其中那个时钟按钮是添加暂停多久，用于防止一些命令没有启动完毕就执行下一个命令。这样如图中，我就可以获得一个快速插入画板且快速更改对应文件名的序列，最后在你最开始建立的画图序列中选择齿轮后，再选择你上方选择的Macro。
![|L](https://pic1.zhimg.com/80/v2-28654608ab2cb78823f7e73c7dfe7658_1440w.jpg)

如上你就可以构建一个可以在所有平台的Obsidian中执行的QuickAdd脚本了。

## 04.QuickAdd特殊用法
>[!attention] 明确需求
>之前在想法中提到过，<strong><font color=#E6E022>用QuickAdd配合Kanban可以实现快速添加项目到自己的Kanban文件中</font></strong>，例如在写作的时候将想到的其它的点子快速添加到自己的想法Board上。
>也可以基于这个来<strong><font color=#E6E022>实现快速添加内容到自己的日记中</font></strong>，例如如果你同时用Logseq和Obsidian的话，那么这个功能就是急需的了。

>[!summary] 延伸应用
>此外上文未提到的是，你在序列中采用的脚本所得到的<strong><font color=#FF0000>参数</font></strong>，以及使用模板所得到的参数，都可以在同一个序列的后续模板或者脚本中使用，即传参。

## 05.总结
通过利用QuickAdd，你<strong><font color=#E6E022>在写作中或者在使用Obsidian的过程中可以降低一些重复操作的工作</font></strong>，而且也可以<strong><font color=#E6E022>避免频繁打断自己的工作的情况</font></strong>，你选中一些自己文章中的文本，然后发送到Kanban中提醒自己要扩展这些文本，这个过程在QuickAdd的加持下十分方便，谢谢阅读。

<hr style="border:3px solid ForestGreen"> </hr>

# 少数派——Obsidian最强插件：QuickAdd
>[!background] 前言
>嗨大家！今天介绍Obsidian(一款本地化笔记软件)最强的插件：QuickAdd。
>从我开始用quickadd这个插件开始，它就越来越融入到我的<strong><font color=#E6E022>日常笔记流程</font></strong>中，而且随着使用的越习惯、越平淡，还开发出了一开始没有想过的用法(虽然就是很简单)。如果现在让我只能留一个第三方插件，毫无疑问，我会选择quickadd。

QuickAdd，有人称呼它为“<strong><font color=#FF0000>快加</font></strong>”，虽然有点不那么优美，可是也很贴切了。`萃取重点`:: <strong><font color=#E6E022>插件的官方介绍是：快速地添加笔记(Notes)或内容(Content)到你的库(Vault)</font></strong>。（P.S.作者英文水平有限，担心翻译不准确才加上英文原单词，不是为了凑字数，不是！）

如果你的英文水平很好，那么可以去看插件在github里的readme，不仅有视频介绍，还有一些工作流的例子(虽然是国外的)，可以说非常有用了。对于高阶用户来说，官方的文档应该会比我的教程更有用。

本文依然延续往期教程风格，适合新手用户。如果你想尝试QuickAdd，或者正在用QuickAdd，但是在使用上有疑惑，希望这篇文章能够给你一些参考和启发。

## 01.QuickAdd的4种类型
>[!summary] QuickAdd的4种类型
>+ Capture：捕捉。捕捉输入内容到某个文件。
>+ Template：模板。用模板新建文件。
>+ Multi：多(菜单)。用于把quickadd命令做成可选菜单的形式。
>+ Macro：宏。执行一系列命令组合。(本篇暂不涉及)

我没有按照官方的顺序来列这4种类型，而是按照我认为的使用的难易程度排列，或者说这是我认为对于新接触这个插件的用户来说比较容易上手的渐进式的使用过程。之前在介绍工作流的时候，简单介绍过这个插件，所以基础的怎么创建命令，以及每个设置的释义就不再重复介绍了。本次重点在于这4个快加类型的应用，让我们来看看它们能做到什么，以及如何操作。

### 0101.CAPTURE捕捉
>[!attention] 用途说明
>`萃取重点`:: <strong><font color=#9966CC>介绍：捕捉你输入的文本，插入到指定的文件。</font></strong>捕捉，可以捕捉内容到指定文件的指定地方。根据这个特性，我们可以实现一些简单又实用的用法。

>[!example] 010101.记录闪念/间歇日记
![](https://i.loli.net/2021/10/16/CYiB2EAfWGqVwor.gif)

+ 下面我们就开始吧！添加一个capture类型的快加，打开设置。
+ ![](https://i.loli.net/2021/10/16/iZynxCzjql9GrFd.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)
+ <strong><font color=#FF4500>step1:在FileName项，填写上你想要捕捉内容保存到的文件。</font></strong>
    + 比如我们现在是要记闪念日记，那么我要保存到当天的日记笔记里。文件名称支持格式语法，比如{{DATE}}，会输出日期，和我们默认的模板日期几乎是一样的，但是有一个重要的不同，快加的DATE是大写。
    + 下图是我的快加闪念设置，可以看到我的日记保存目录，以及动态的日记笔记名，这里你可以直接复制日记插件里设置的格式，粘贴进来。
    + `萃取重点`:: 这样我每次调用快加:闪念命令，写入的内容就会插入到当天的日记里。下面附上快加支持的format，供参考：
    + ![快加支持的FORMAT](https://i.loli.net/2021/10/16/JKybpOWqhiU48j2.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)
+ <strong><font color=#FF4500>step2:指定插入到指定位置(非必要)</font></strong>
    + ![配置详情](https://i.loli.net/2021/10/16/HEnIRr4Uq9vKoj5.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)
    + 在Insert after项，你可以<strong><font color=#E6E022>指定把内容插入到文件的某个位置</font></strong>，比如我想要插入到二级标题闪念下面。下图是我的配置：
    + 首先，打开Insert after项右边的开关，然后在下方的输入框输入`## 闪念`。<strong><font color=#E6E022>注意由于是二级标题，所以井号后面有空格。只有字符一模一样，快加命令才能找到指定行，并且把内容插入到对应的位置。</font></strong><strong><font color=#FF0000>提示：Insertafter项同样支持格式语法。</font></strong>
    + 上图中可以看到还有一个设置项，<strong><font color=#9966CC>Insert at end of section</font></strong>。section是章节、一段的意思，比如我的二级标题「闪念」，那么这一整个二级标题的范围，都作为一个块。当该选项不打开时，每次的捕捉内容会插入在二级标题「闪念」的最上方。那么我多次插入日记的内容，呈现出来其实是倒序排列的，后插入的内容显示在最上方。当打开该选项时，最后插入的内容就会在二级标题「闪念」的末尾位置。
+ <strong><font color=#FF4500>step3:给闪念日记加上时间戳</font></strong>
    + ![加上时间戳](https://i.loli.net/2021/10/16/46F8m1DqXVkeI9r.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)
    + 下图中，有2个设置我用红色字体标注了翻译（粗翻，不保证准确），就不再展开讲了，请按需使用。这里讲一下经常被问到的，给闪念日记加上时间戳。我们在记闪念笔记的时候，往往需要带上时间戳，以便于以后查看。这时候可以使用Capture format设置项。
        + 1-打开Capture format的开关。
        + 2-在文本框里写格式语法。下面做一下简单的解释。
            + <strong><font color=#E6E022>{{DATE:YYYY-MM-DDHH:mm}}就是时间的写法，DATE语法可以从官方的日记插件设置页找到：</font></strong>
            + <strong><font color=#E6E022>{{VALUE}}</font></strong>就是捕捉的内容。
            + 最前面有一个`\n`，这是换行语法，在md中不会原样输出，而是会自动换行一样，再插入相应的内容。
            + `-`，是列表语法，因为我喜欢使用列表输入内容而已，没有特别的含义，如果你不想要列表，去掉上图事例中的短横杠-就可以了。

上面只是一个例子，希望大致能让你明白怎么写capture format。`萃取重点`:: 总结一下，就是<strong><font color=#E6E022>非格式语法会原样输出</font></strong>，<strong><font color=#E6E022>格式语法会动态输出</font></strong>，你可以自己定需要插入什么时间格式，也可以自己给你的闪念加点花样，比如前面加上emoji之类的。

>[!example] 010102.头脑风暴
虽然上面介绍的是插入闪念日记，但这个例子是想介绍捕捉内容到指定位置的这个使用场景。你可以用这个方法做一系列和插入日记相关的命令，比如：

>[!example] 使用场景
>你可以在一个标题下面，用不同的emoji区分不同的内容类型(快加设置时capture format加上emoji)。也可以将不同类型的内容插入到不同的标题下(即设置Insert after项)。
![](https://i.loli.net/2021/10/16/FNshl1tozj5JHcx.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

>[!example] 010103.快速添加一个任务

这个很简单，有两种方法：
+ 第一种是和上面的设置一样，在capture format里，写`- [ ] {{VALUE}}`；
+ 第二种就是在设置快加命令的时候，勾选Task项。
    + ![](https://i.loli.net/2021/10/16/q8buFlgyaYcAo7s.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

>[!example] 010104.延伸使用：快速添加到看板
>这是一个和看板的联动使用。由于<strong><font color=#E6E022>实际上看板里的Item(一条，但出于习惯后文均称作一列)对应的是md语法的二级标题</font></strong>，一个看板卡片对应的是md的任务语法`- [ ]`，所以我们可以利用这个关系来给看板快速添加卡片。

>[!summary] 案例说明
例如：我有一个「<strong><font color=#70f3ff>灵感看板</font></strong>」用来收集写作灵感，这个看板里面有一个列是「<strong><font color=#70f3ff>Inbox</font></strong>」，用来作为<strong><font color=#70f3ff>灵感的收集箱</font></strong>。现在我想要快速添加一个新灵感到「灵感看板」的「Inbox」。快速添加到看板的QUICKADD设置是：
+ FileName项写上「灵感看板」的文件位置
+ 打开Task项的开关
+ 打开Insert after项的开关，并写上`##Inbox`
+ 如果你想要每次新添加的卡片都放在列的最下面，就打开Insert at end of section项的开关。如果不打开，默认卡片会放在列的最上方。

>[!example] 010105.玩点好玩的，插入admonition的框

从一开始为了不污染MARKDOWN文件，到实在无法抵抗admonition的高颜值，我终于还是开始使用admonition了。但是每次都要写那么长的代码块，真的很累啊，而且总是想不起来自己的设定(我为自己的笔记设置了一套ADMONITION卡片，每一个都有不同的用途)。就在我为此而烦心的时候，忽然想起了QUICKADD，OMG，为什么我没有早点想起来？！希望我不是最后一个知道的。

>[!summary] 案例说明
>同样使用QUICKADD的捕捉，打开捕捉内容到当前文件的当前位置的选项开关，然后在CAPTUREFORMAT里面粘贴进那一长串ADMONITION语法。完美！
>![](https://i.loli.net/2021/10/16/p7L5tjruNMGvDxU.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)
>
>注意，我这是为了实现在当前文件的当前位置插入一段admonition，才使用了capture to active file，如果你想要添加到指定文件的指定位置，请仍然参考前文闪念日记的设置。

>[!example] 010106.进阶用法：做问答式笔记
>仍然是capture format这个设置项，我们可以玩点花样。你可以用这节介绍的方法来做问答日记，或者用来写晨间日记，或者为自己做一些简单的心理/情绪引导。

先来看一下效果：
+ ![效果演示](https://i.loli.net/2021/10/16/K7ebfmXD8EIG9sJ.gif)
+ 上面演示的capture format设置内容如下：

```md
### 行为疗法{{DATE:YYYYMMDDHHmm}}
- 你有什么感觉？
  - {{VALUE:你有什么感觉？}}

- 现在你脑海中在想什么？
  - {{VALUE:现在你脑海中在想什么？}}

- 它真实吗？
  - {{VALUE:它真实吗？}}
  > 我在思考，不一定意味着这是事实。
```

接下来说说原理：
+ 当使用{{VALUE:你有什么感觉？}}的时候，弹出的捕捉框会以“你有什么感觉？”作为输入提示文字。
+ capture format支持多个{{VALUE}}，也就是你可以一次捕捉多个内容。

### 0102.Template模板
>[!attention] 用途说明
>介绍：快加文件，<strong><font color=#E6E022>即用指定模板新建一个文件</font></strong>。
>关于QUICKADD模板类型的用法，我在我的OBSIDIAN工作流：模板+QUICKADD+DATAVIEW快速创建和自动索引中有写过，而且用法也比较简单，在此就不再复述了。(工作流那篇文章中对每个设置项做了翻译，基本上看完翻译就都懂了)。

简单说下重点：
+ 可以指定使用的模板。
+ 可以指定新文件保存的位置。
+ 模板文件中支持<strong><font color=#FF0000>格式语法</font></strong>。

对，又是格式语法，我们上面有演示怎么写日期时间的格式语法，现在可以把它用在你的模板文件中，就可以做到自动记录创建时间。下面是我的提案模板中yaml的写法。

```md

--title: {{NAME}}
--UID: {{DATE:YYYYMMDDHHmmss}}
--aliases: []
--tags: []
--项目状态: 提案
--主题: {{VALUE:主题是什么？}}
--date: {{DATE:YYYY-MM-DD HH:mm:ss}}

```
+ {{NAME}}是文件名的写法
+ {{VALUE:主题是什么？}}<strong><font color=#E6E022>这种写法会作为一个提示输入弹窗，让我录入</font></strong>。
+ {{DATE:YYYY-MM-DDHH:mm:ss}}在创建文件时会变成当前的年月日时分秒
+ {{VALUE:值1,值2,值3}}，在使用快加Template类型的命令新建文件时，会作为一个下拉选项让你选择。
    + 来源:{{VALUE:微信读书,纸书,bilibili,网络}}
    + 特殊格式语法：<strong><font color=#E6E022>在模板中这样写，可以在新建时出现选择框</font></strong>。(该方法为@简睿提供)

### 0103.multi多(菜单)
>[!attention] 用途说明
>介绍：将已经做好的快加命令做成组合菜单。如果把创建的一个个快加捕捉命令和快加模板命令比作是文件的话，multi就是文件夹。创建一个multi，把单个快加命令拖拽进multi，就像将文件拖拽进文件夹。`萃取重点`:: <strong><font color=#FF0000>这个拖拽，需要点小技巧，就是往右侧框外拖，不然拖不进去。</font></strong>
![案例所示拖拽操作](https://i.loli.net/2021/10/17/EpyYLTS4XHa6VlN.gif)<br/>
然后你就可以得到：
![案例所示最终效果](https://i.loli.net/2021/10/17/UYKebyanxwlmWDE.gif)

>[!summary] 结语
>本篇以几个应用场景展开，并没有很全面的介绍quickadd的每一个设置，希望这有限的信息能够在你使用quickadd的路上助你一臂之力。
>如果有用，欢迎留言告诉我，你的反馈，是我最大的动力。谢谢你看到这里，我们下期见！如果没有了下期，那就祝你，上午好，下午好，晚上好，再见！
>P.S.本文首发于博客