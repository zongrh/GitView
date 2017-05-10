## 正则总结：JavaScript中的正则表达式
##定义
在javascript我们可以通过内建的类来定义一个正则表达式。

    var reName = new RegExp("nowamagic");

实际上RegExp类的构造函数可以接受两个参数，除了本身需要匹配的模式字符串外，还可以定义指定额外处理方式的第二个参数。

    var reName = new RegExp("nowamagic","i");//忽略大小写
我很好奇输出reName会得到什么结果呢？于是：

    document.write(reName);
得到结果：/nowamagic/i，于是我们得到javascript中正则表达式的第二种定义方法（perl风格）：

    var reName = /nowamagic/;
那第二个参数呢？当然，同样可以为其指定第二个参数：

    var reName = /nowamagic/i;
这两种定义方式都是可行的，完全可以根据个人习惯进行选择。就像可以使用var s = new String(“for a simple life”);定义字符串的同时还可以使用var s = “for a simple life”;来定义是完全相同的。建议使用perl风格的写法，除了简洁外，还省去了使用RegExp构造函数定义时需要对“\”转义的麻烦。

如果要匹配字符“\”，perl风格的写法是：

    var res = /\\/;
而构造函数的写法则需要对两个“\”都进行转义：

    var res = new RegExp("\\\\");
感觉上是不是就麻烦了很多？
记住，在一个完整的正则表达式中“\”后面总是跟着另外一个字符。

##javascript中的正则表达式
其实上面已经在开始讲了javascript对正则表达式的实现方式了，只定义了正则表达式，但是如何在javascript中真正使用正则表达式呢？在javascript中RegExp和String对象都有处理正则表达式的方法。

**test** -- RegExp的test方法用来测试字符串是否匹配给出的匹配模式，返回布尔值；

**exec** -- RegExp的exec方法返回包含第一个匹配的的数组或null；

**match** -- String的match方法返回包含所有匹配子字符串的数组；

**replace** -- String的replace方法完成string的替换操作，支持正则表达式；

**search** -- 与String的indexof方法类似，不同的是search支持正则表达式，而不仅仅是字符串；

**split** -- 按照一定规则拆分字符串并将子字符串存储到数组中的String方法。

关于这些函数的具体使用方法，可以参阅JS的相关函数手册。

一个实例对象除了方法当然还有属性，一个正则表达式有以下属性：

**global** -- 布尔值，若全局选项g已设置则返回true，否则返回false；

**ignoreCase** -- 布尔值，若忽略大小写选项i已设置则返回true，否则返回false；

**lastIndex** -- 整数，使用exec或test方法时被填入，表示下次匹配将会从哪个字符位置开始；

**multiline** -- 布尔值，表示多行模式选项m是否设置，若设置则返回true，否则返回false；

**source** -- 正则表达式的元字符串形式。/\\/的source将返回”\\“。

##元字符
在正则表达式中有一些特殊的字符符号我们是不能直接使用的，必须对其进行转义后才能使用。如“\”，因为这些字符在正则表达式中有特殊的语法含义，这类字符被称为元字符，正则表达式中的元字符有：

    .,\,/,*,?,+,[,(,),],{,},^,$,|

可能不太好记忆，当无法确定某个字符是否是元字符的时候就勇敢的对其进行转义是没有错的，对不是元字符的字符进行转义是不会出什么问题的，但是如果不对元字符转义就会有意想不到的错误产生了。

##分组匹配

一个简单的字符就可以是一个匹配模式，但是现实情况往往不会这么简单。比如我们要匹配一个0-9的数字：

    var i = 5;
    var j = 6;
这个正则表达式要如何书写才能同时匹配这两个数字呢？简单的字符表达式当然无法完成了，这个时候我们就可以为0-9十个数字来定义一个字符集合（字符类）来进行匹配。

    var reNum = /[0123456789]/;
    document.write(reNum.test(i));//true
    document.write(reNum.test(j));//true
使用test方法测试匹配结果都输出了true。
##范围匹配
上一个例子使用了分组匹配，但是如果要匹配所有26个英文字母，还要包括大小写，仍然可以使用分组匹配：

    var reLetter = /abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ/;
恩，这个正则表达式是完全正确的，但是是不是感觉太长了，有没有办法让它更为简洁一点？当然是有的，为字符或数字指定一个匹配范围就可以了。

    var reNum = /[0-9]/;
    var reLetter = /[a-zA-Z]/;
这样就可以了，“-”用来定义一个匹配区间，字符的具体顺序由ASCII字符表确定，所以不能写成/A-z/，因为Z-a之间还包含着其他字符。
##取非匹配
很多编程语言中都使用“！”取非操作，包括javascript。正则表达式中也有取非操作，比如/[^0-9]/就是一个取非操作的正则表达式了。

    var i = 5;
    var s = "o";
    var rec = /[^0-9]/;
    document.write(rec.test(i));//false
    document.write(rec.test(s));//true
符号^用来完成取非操作，同时^0-9也是必须包含在[]中的，因为^其实还有另外一种特殊用途。
##特殊字符

可能你觉得/[a-zA-Z]/，/[0-9]/还是不够简洁，的确，在正则表达式中一些特定的字符集合可以使用一些特殊的元字符来代替。这些特殊的字符并不是必不可少的，但是却可以给我们带来不少方便。/[0-9]/就完全可以写成这样：

    var reNum = /\d/;
那大小写字母字符类呢？很遗憾，除了POSIX字符类（javascript不支持POSIX字符类）中有支持大小写字母的特殊字符类外并没有专门替代方法。

常见的特殊字符有：

    \d　任何一个数字字符，等价于[0-9]
    \D　任何一个非数字字符，等价于[^0-9]
    \w　任何一个字母数字或下划线字符，等价于[a-zA-Z_]
    \W　任何一个非字母数字和下划线字符，等价于[^a-zA-Z_]
    \s　任何一个空白字符，包括换页符、换行符、回车符、制表符和垂直制表符，等价于[\f\n\r\t\v]
    \S　任何一个非空白字符，等价于[^\f\n\r\t\v]
    .　换行和回车以外的任何单个字符，等价于[^\n\r]
相同字母大小写总是进行取非操作的。

##十六进制和八进制字符

在正则表达式中使用十六进制或八进制字符也是完全可行的，他们所匹配的字符即是由其转换成十进制后的数值在ASCII中所对应的字符。

    var reAt = /\x40/;//十六进制字符\x40(64)对应字符“@”
    var reA = /\0101/;//八进制字符\0101(65)对应字符“A”
##重复匹配

以匹配一个email地址为例，mymail@mail.com这样的一个email地址必须包括一个合法的用户名mymail，@符号以及一个合法的域。其中用户名和域名的字符个数都是无法判断的，但是有一点是肯定的——用户名必须至少是一个字符，域名至少是两个字符中间还必须有一个点号。于是我们可以这样做：

    var reMail = /\w+@\w+\.\w+/i;
    var email = "mymail@mail.com";
    document.write(reMail.test(email));//true
“+”表示字符出现一次或多次，至少出现一次。这个正则表达式其实并不能匹配所有合法的email地址，后面我们继续完善。

除了“+”可以指定至少匹配一次外，还有很多其他的可以指定匹配次数的方式。

    ?　出现零次或一次，最多一次
    *　出现任意次（零次、一次、多次）
    +　出现一次或多次，至少一次
    {n}　能且只能出现n次
    {n,m}　至少出现n次，最多出现m次
www.gogle.com，www.google.com，www.gooogle.com这三个网址都能正确地打开google的首页，于是就可以用{n,m}匹配其中的1个，2个或3个字母”o”。

    var gogle = "www.gogle.com";
    var google = "www.google.com";
    var gooogle = "www.gooogle.com";
    var reGoogle = /w{3}\.go{1,3}gle\.com/i;
    document.write(reGoogle.test(gogle));//true
    document.write(reGoogle.test(google));//true
    document.write(reGoogle.test(gooogle));//true
在上面的正则表达式中，我们使用了{3}来制定字符“w”能且只
能出现3次，用{1,3}来制定字母“o”可以出现1到3次。

##防止过度匹配

有这样一段HTML文本：

    var html = "<em>nowamagic</em>for a simple life<em>http://nowamagic.net/</em>";
如果现在要讲<em></em>及其中间的文本匹配出来，正则表达式可以这样写：


    var reEm1 = /<em>.*<\/em>/gi;
    document.write(html.match(reEm1));//"<em>nowamagic</em>for a simple life<em>http://nowamagic.net/</em>"
    var reEm2 = /<em>.*?<\/em>/gi;
    document.write(html.match(reEm2));//<em>nowamagic</em>,<em>http://nowamagic.net/</em>
当使用贪婪模式的时候，”.*”会最大程度地进行字符匹配，所以输出了整个字符串。而在惰性模式中，”.*?”只进行最小限度的匹配，所以完整的输出了我们需要的字符串。

惰性模式的语法很简单，即是在贪婪模式后面加上一个“?”即可。

    * –> *?
    + –> +?
    {n,} –> {n,}?

##位置匹配
    var s = “_Don’t do it!”;
如何将单词“do”匹配出来？it’s easy!

    var reDo = /do/gi;
    document.write(s.match(reDo));//Do,do
但是这个简单的正则表达式/do/gi将“don’t”中的“do”也进行了匹配，可这并不是想要的结果。而在正则表达式中有专门用来进行单词边界匹配的限定符”\b“。

    var reDo = /\bdo\b/gi;
    document.write(s.match(reDo));//do
“\b”到底匹配的什么呢？”\b”匹配的是一个位置，一个位于”\w“（字母，数字，下划线）和”\W“之间的位置。

既然有”\b”，那有”\B”吗？当然，他和”\b“刚好相反，由来匹配一个不是单词边界的位置。比如上例中匹配”don’t”中的”do”时”\B”就可派上用场。

    var reDo = /\Bdo\B/gi;
    document.write(s.match(reDo));//Do
在介绍取非匹配的时候介绍^只用位于[]并紧跟[方能取非匹配，而^还有另外一种用途——字符串边界匹配。

    ^　用来匹配字符串开头
    $　用来匹配字符串结尾
比如我们要匹配一个http://nowamagic.net形式的net域名：

    var url = "http://nowamagic.net";
    var reUrl = /^(http):\/\/nowamagic\.(net)$/gi;
    document.write(reUrl.test(url));//true
正则表达式reUrl限制url必须以”http”开头，以”net”结尾。

又如经常被扩展的string方法trim：

    function trim(s){
    return s.replace(/(^\s*)|(\s*$)/g,"");
    }
同时我们可以在整个模式的最前面使用(?m)来启用分行匹配模式。这样，^不但匹配正常的字符串开头，还将匹配行分隔符（换行符）后面的开始位置；$不仅匹配正常的字符串结尾，还将匹配行分隔符（换行符）后面的结束位置。


###延伸阅读
http://www.nowamagic.net/librarys/veda/detail/1283







