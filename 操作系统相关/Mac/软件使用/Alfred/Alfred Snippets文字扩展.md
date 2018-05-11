## Mac效率神器Alfred系列教程---Snippets文字扩展

Alfred文字片段和自动扩展

每天我们都要用Mac进行很多文字的输入，包括邮件、写作、通讯等等。在输入文字的过程中，往往有很多内容是需要经常重复输入的，比如一些常用用语、个人Email地址、邮件页面底端的公司个人信息等等。每次遇到要输入这些内容的时候，都需要重复输入相同的文本，不免有些浪费时间。Alfred的文字片段和自动扩展功能（Snippets and Text Expansion）就是为完美解决这个问题而设计的，让你仅仅只需输入某几个设定好的特定字符，就能扩展出完整的、冗长的常用字符串。 

Mac上有不少解决文字扩展之类问题的软件，比如TextExpander、Typinatord等，但这些都是付费软件，而且功能繁多，Alfred的文字自动扩展功能可以帮助很多非重度用户脱离这些付费软件的束缚。而且可以在Alfred中对每个Snippet进行分类，插入时间日期等等，并且可以很方便的与其他用户进行分享。

Snippet的创建

关于如何创建自定义的Snippet，有两种方法：

1.通过Snippet设置面板创建

打开Alfred的Snippet设置面板，可以看到下方分为左右两个区域，左边为Snippet的分组，右边为每个分组下的具体文字Snippet。

![img](https://t12.baidu.com/it/u=544584920,2402969766&fm=173&s=6418E83B51DF41CE52CD7CDE0100C0B2&w=640&h=438&img.JPEG)

每个文字Snippet都要属于某一个分组，因此如果左边还没有建立分组的话，可以点击左侧面板下方的“+”按钮进行添加。点击后会弹出添加对话框， 

![img](https://t10.baidu.com/it/u=81238647,1577618303&fm=173&s=64986C3B11DF51CC4C68F8DE0100C0B1&w=640&h=438&img.JPEG)

Name:分组名字Affix：Snippet前缀。与后面描述的单独条目的Snippet Keyword一起组合成Snippet关键字；keyword：分组关键字，为可选项，如果输入了keyword，则会在单独条目关键字后面自动添加这个keyword；图标：分组的图标。这里最重要的是Affix选项，为Snippet的前缀，这个分组下的每个条目之前都会附加上这个前缀进行匹配。 分组创建成功之后，就可以在这个分组之下添加Snippet了。点击右下角的“+”进行条目的添加： 

![img](https://t12.baidu.com/it/u=3957054551,3200224211&fm=173&s=648C7C33031B446F1AF5A4DA0100C0B1&w=640&h=438&img.JPEG)

Name:条目名称Keyword：Snippet条目关键字Collection：条目所在的分组Snippet：需要进行对其进行扩展的完整文本内容Auto expansion allowed：允许自动扩展在这里输入Keyword关键字后，这个Snippet的缩略语就会变成“分组Affix + 条目Keyword + 分组keyword”。只要在任何地方输入这个组合，就能扩展出Snippet中定义的文本内容。

2.通过Clipboard创建

如果熟悉使用Clipboard剪切板历史记录，则可以通过Clipboard直接进行Snippet的创建。按下Clipboard的热键（默认为Command + Option + C）打开剪切板历史记录的面板，里面列出了所有进行过复制动作的文本条目。选中一个条目后，按下Command + S，就能弹出添加Snippet条目的对话框，重复上一步骤即可。

对Snippet关键字的建议

如前所述，只要定义好了Snippet条目，则在任何文本输入的地方输入“分组Affix + 条目Keyword + 分组keyword”，就能自动展开相应的文本片段。但是这个“Affix + Keyword”组合的定义最好也遵循一定的规则，要容易记忆、方便输入，但同时也不能与其他热键冲突。以下是关于怎样定义Affix和Keyword的几个建议：

在Keyword中不要使用正常词汇，以避免有些不期望的展开。比如如果你将Keyword定义为“apple”，则在任何输入“apple”的地方都会扩展成为定义好的文本片段，即使你想进行输入的就是“apple”这个单词本身。因此，最好能用一些特殊记法，比如将关键字每个单词的首字母捡出来连在一起等等；所有的snippet都要以非字母数字开头，比如感叹号，分号，冒号等等（类似于!!office，::coffee这样的）；使用不常用的大写形式，比如“officE”；使用双重字母，比如“ttime”。动态占位符（Dynamic Placeholders）

什么是动态占位符

很多时候，你想在文本中插入一些特定的内容，但这些内容在每一次输入的时候都会有所不同，比如日期、时间、剪切板中的文本等等。使用动态占位符，就能在输入Snippets的时候，扩展出的文字根据具体的情况而变化。只需在编辑Snippets的时候，将相应的关键字放在{}内，比如{date}，{time}，{clipboard}。则当输入Snippets的时候，{}中的内容会自动转变为相应的动态内容，比如日期、时间、剪切板文本。 

![img](https://t11.baidu.com/it/u=852218548,4110111246&fm=173&s=64887C33110F514D1EFDE5DA0100C0B1&w=640&h=438&img.JPEG)

显示日期时间

显示日期时间的占位符关键字有三个：

{date}：显示当前日期{time}：显示当前时间{datetime}：显示当前日期和时间日期和时间都有short、medium、long和full这几种显示方式，Alfred默认的为midium。要想改变显示方式，只需在关键字后面接上相应的方式名称即可，例如“{date:long}”。这些显示方式的具体格式可以在Mac设置面板中的“时间&区域”中查看： 

![img](https://t11.baidu.com/it/u=202026661,1793646108&fm=173&s=29087032519FE1C85C7DC0DC0100C0B3&w=640&h=495&img.JPEG)

不仅能显示当前时间，利用加减算数符号进行计算之后，还能显示过去或者未来的日期时间，比如{date +1D}会显示明天的日期，{time -3h -30m}会显示3个半小时之前的时间等等。支持的算子有以下几种：

1Y：年1M：月1D：天1h：小时1m：分钟1s：秒在用算式计算时间时，同时也能接上显示方式，按照需要的格式显示相应的日期时间，比如“{time -2h -20m:long}”，“{date -2m:short}”。

剪切板内容

Mac剪切板历史功能可以记录下之前所有的复制功能，按下热键Command + Option + C就能打开历史记录面板。利用Snippet的“{clipboard}”这个占位符，可以动态获取剪切板中的内容，而且可以按照需要更改对应剪切文本的格式，在某些场合下使用会非常方便。

比如新建一个Snippet，关键字设为“!!testcp”，然后利用{clipboard}的位移功能来选择不同顺序的剪切板文本，需要注意的是，这里的位移首先是从数字0开始，而不是1，“{clipboard:0}”代表剪切板第一项内容，“{clipboard:1}”为第二项内容，“{clipboard:2}”为第三项，以此类推。{clipboard}和{clipboard:0}的意义相同。首先建立一个Snippet， 

![img](https://t11.baidu.com/it/u=2574213061,1935674226&fm=173&s=648C7C330B0B444D0A7DA0DB0100C0B1&w=640&h=438&img.JPEG)

然后对下面几行文本分别按顺序进行复制（括号中的内容不要进行复制）

（第一行文本）小明（第二行文本）（第三行文本）18（第四行文本）华中科技大学之后按下Command + Option + C打开剪切板历史记录面板，你会看到刚刚复制过的几项文本都保存在其中了， 

![img](https://t10.baidu.com/it/u=4220417580,2765799868&fm=173&s=609E55321F0E754D5C7958DA000080B1&w=640&h=485&img.JPEG)

现在按下刚才新建Snippet时设定好的关键字“!!testcp”，就会自动呈现以下内容：

用户信息： 名字： 小明 邮箱： 年龄： 18 毕业学校： 华中科技大学还可以加上一些转换命令，对剪切板中的文本进行格式转换：

{clipboard:uppercase}：将文本全部转换为大写；{clipboard:lowercase}：将文本全部转换为小写；{clipboard:capitals}：将文本中每个单词的首字母变为大写。光标位置

利用{cursor}占位符，可以在输入Snippet扩展为对应文字后，光标自动定位到{cursor}在文本中的位置，方便之后对某些内容的输入。比如新建以下Snippet： 

![img](https://t11.baidu.com/it/u=2372756233,1679310632&fm=173&s=648C7C330B0B444D1A75A0DB0100C0B1&w=640&h=438&img.JPEG)

当输入!!cursortest之后，Snippet中的文本会自动展开，之后光标位置会自动定位到{cursor}所在的位置，方便信息的输入，省去了还要再次操作鼠标进行光标定位的麻烦。

查看所有的Snippets

当你熟悉了Snippets的用法之后，会在工作学习中建立很多方便自己使用的Snippet关键字。当你记不清某些关键字的时候，可以用Snippet Viewer来进行查看和查询。启动Snippet View的方法有两种：

利用热键，可以在Snippet的设置面板中，对Viewer Hotkey进行设置；按下Command + Option + C打开剪切板历史记录面板，选择最上方的“All Snippets”。之后你就会看到所有的Snippet分组以及每个分组下的条目，在输入框中输入字符串可以进行过滤。 

![img](https://t12.baidu.com/it/u=18265214,1788121734&fm=173&s=6E28A50B1D1E75CE5C795DDB0000C0B0&w=640&h=485&img.JPEG)

更方便的是，打开Alfred输入框，利用“snip”关键字也能快捷的对Snippet进行查询，只需输入名字或者某些字符串即可。 

![img](https://t11.baidu.com/it/u=1755197437,596304937&fm=173&s=0F38A50B3EAA570968F8ADCE0300F0B7&w=640&h=361&img.JPEG)

分享Snippet

当你创建了一个非常方便快捷的Snippet分组，也能将其分享出去，给其他Alfred用户使用。方法是右键单击某个Snippet分组，然后选择Export，就会将其导出成一个文件。其他用户只要双击这个Snippet文件就能将这个Snippet集合导入到自己的Alfred中。 

![img](https://t12.baidu.com/it/u=1914915377,4065399887&fm=173&s=CC10ED1A399FC4CE5AE1A0DB000090B3&w=640&h=534&img.JPEG)

Alfred也很贴心的为我们准备了一些很实用的Snippet集合，点击Snippet设置面板中的“Get Collections”按钮就能跳转到相应网页， 

![img](https://t12.baidu.com/it/u=4037304980,2131470376&fm=173&s=4906EC1A190E46CE1EF035D3000010B0&w=640&h=529&img.JPEG)

其中包含了以下几个Snippet分组：

Mac Symbols：集合了很多常用的Mac符号，比如输入“!!cmd”对应“”符号，“!!shift”对应“”符号等等。有了这个集合，就再也不用在符号表中辛辛苦苦去找某个Mac标志符号了；ASCII Art：集合了一些好玩的火星文字表情；Currency Symbols：集合了一些常用的货币符号，比如“::cny”代表“”，“::usd”代表“$”等等；Dynamic Content examples：一些关于动态占位符的例子，可以学习一下使用方法；Emoji Pack：很强大的Emoji表情包。有海量的Emoji符号，输入对应的关键字就能自动插入想要的Emoji表情，简直不要太方便，再也不用一个个翻页的去找了 

![img](https://t10.baidu.com/it/u=2634289539,1322585108&fm=173&s=701EEC3B150C50E8166580D60000D0B3&w=640&h=349&img.JPEG)