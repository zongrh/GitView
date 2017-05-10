###1、HTML简介
HTML = HyperText Markup Language = 超文本标记语言

HTML编辑器:DreamWaver,Frontpage,记事本(Notepad)

扩展名的规定.htm或者.html

###2、HTML基本标签
一个最简单的网页

    <html>
    <head>
    <title>Title of page</title>
    </head>
    <body>
    This is my first homepage. 
    <b>This text is bold</b>
    </body>
    </html> 

标记一般成对出现
与大小写无关（W3C推荐使用小写标签）

HTML是一个不严格的语言

1.显示粗体

    <b> </b>
2.标签的属性

    <body bgcolor="red">   bg=background=背景
3.单引号与双引号问题

    一般使用双引号
4.段落标签 paragraph=段落

    <p> </p>
5.标题

    <h1>到<h6>,<h1>最大，<h6>最小  
    headline=标题
    align属性：align=对齐 left, right,center,
6.换行

    break(line break)
7.注释

    <!-- This is a comment --> 
8.横线

    <hr>
###3、HTML格式化标签

1.加粗文字，两个标签

    <b></b>、<strong> </strong>
2.文字变大，变小

    <big></big>、<small></small>
3.倾斜字体

    <em> </em> <i> </i> em=emphasis=加强语气
4.下标字体

    <sub> </sub>
5.上标字体

    <sup> </sup>
6.下划线

    <u> </u>  underline=下划线
7.删除线

    <s> </s> 或者<strike> </strike>
8.预格式化的文本

    <pre> </pre>
9.可移动的文字

    marquee  direction属性，控制方向
10.图像标签

    img
11.HTML实体

    显示结果    描述            	实体名    	实体号 
            不可拆分的空格   	&nbsp;    	&#160; 
    < 		  小于			&lt; 		&#60; 
    > 		  大于 			&gt; 		&#62; 
    & 		  and符号 		&amp; 		&#38; 
    " 		  引号 		     &quot; 		&#34; 
    ' 		  单引号   					&#39; 


    显示结果  描述  			实体名  		实体号  
    ￠ 		分 				&cent; 		&#162; 
    ￡ 		英镑 			&pound; 		&#163; 
    ￥ 		人民币元 			&yen; 		&#165; 
    § 		章节 			&sect; 		&#167; 
    ? 		版权 			&copy; 		&#169; 
    ? 		注册 			&reg; 		&#174; 
    × 		乘号 			&times; 		&#215; 
    ÷ 		除号 			&divide; 		&#247; 》
###4、HTML链接标签

### 1.链接

    <a href=""> </a>
    文字链接和图片链接
    文字链接与图片链接
    target属性  （target=目标）
    _blank
    _self
    _parent
    _top
    framename

###2.锚标记
    <a name="定位标记名">
    <a href="#定位标记名"> 

    <a name="tips">Useful Tips Section</a>
    <a href="http://www.w3schools.com/html_links.asp#tips">Jump to the Useful Tips Section</a>

    <a href="#tips">Jump to the Useful Tips Section</a>

    <a href="mailto:someone@microsoft.com?subject=Hello%20again">
        "ftp://www.xinqushi.net/files/a.zip"

    <frameset cols="25%,50%,25%">
	   <frame src="frame_a.htm">
	   <frame src="frame_b.htm">
	   <frame src="frame_c.htm">
    </frameset>

    <frameset rows="25%,50%,25%">
        <frame src="frame_a.htm">
        <frame src="frame_b.htm">
        <frame src="frame_c.htm">
    </frameset>

    <frameset cols="25%,50%,25%">
    	<frame src="frame_a.htm">
    	<frame src="frame_b.htm">
    	<frame src="frame_c.htm">
    <noframes>
    <body>Your browser does not handle frames!</body>
    </noframes>
    </frameset>

###5、HTML框架标签

	frame=框架

	col = column = 列
	row = row    = 行

	frameborder

	不要把框架的定义放在body中，框架定义页不需要body。

	<frameset cols="25%,50%,25%">
		<frame src="frame_a.htm">
		<frame src="frame_b.htm">
		<frame src="frame_c.htm">
	</frameset>

	<frameset rows="25%,50%,25%">
		<frame src="frame_a.htm">
		<frame src="frame_b.htm">
		<frame src="frame_c.htm">
	</frameset>

	<frameset cols="25%,50%,25%">
		<frame src="frame_a.htm">
		<frame src="frame_b.htm">
	<frame src="frame_c.htm">
	<noframes>
	<body>Your browser does not handle frames!</body>
	</noframes>
	</frameset>

	2.内联框架

  	可以将一个页面嵌入进来

	<iframe src="intro.htm"></iframe>
###6、HTML表格标签
    <table>
    <tr>   r=row
    <td>   d=data
    <th>
    2.border属性

    3.caption属性

    4.cellpadding属性在表格内容和边框之间留出更多空白

    5.cellspacing属性来增加单元格间距

    6.bgcolor设置背景颜色，background设置背景图片 
    bg=background=背景这两个属性可以针对表，行，单元格设置

    7.align对齐

    8.colspan(跨列),rowspan(跨行) 

    9.表格中的空格
###7、HTML列表和表单标签

列表元素

1.无序列表

    <ul>                            ul=unsorted list=无序列表
    	<li>Coffee</li>            li=list item=列表项
    	<li>Tea</li>
    	<li>Milk</li>
    </ul>

    ul属性: type= disc / circle / square



2.有序列表

    ol=ordered list=有序列表
    <ol>
    	<li>Coffee</li>
    	<li>Tea</li>
    	<li>Milk</li>
    </ol>
    ol属性 type = A / a / I / i 


 3.列表嵌套

    案例1：
    <ul>
        <li>Coffee</li>
        <li>Tea
        <ul>
            <li>Black tea</li>
	        <li>Green tea</li>
	    </ul>
	    </li>
    	<li>Milk</li>
    </ul>

    案例2：
    <ul>
	   <li>Coffee</li>
	   <li>Tea
	      <ul>
	        <li>Black tea</li>
	        <li>Green tea
	            <ul>
		           <li>China</li>
	                <li>Africa</li>
		       </ul>
         </ul>
	  </li>
	  <li>Milk</li>
    </ul>

3.表单

    用一个案例讲解以下的表单对象
    个人信息
    用户名，密码，性别，兴趣爱好，所在城市，备注，提交按钮，重置按钮,提示按钮
    form：表单，一个表单包含的数据会一起被提交
    input type="text" type= text/password/radio(取一样的name表示一组)/checkbox/button/submit/reset

    select option
    textarea

----
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>input</title>
</head>
<body>
<form>
    用户名：<input type="text" name="username" size="50px">
    <p>
        密码： <input type="password" name="pass">
    <p>        <!-- name 都等于sex 表示是一组的只能选择一个   radio 选择框-->
        性别：男<input type="radio" name="sex">女<input type="radio" name="sex">
    <p><!--checkbox 代表多选-->
        兴趣爱好
    <p>
        看书<input type="checkbox" name="read">
        游泳<input type="checkbox" name="swim">
        爬山<input type="checkbox" name="climb">
    <p>
        <select name="city">
            <!--option 选项的意思-->
            <option value="1">北京</option>
            <option value="2">上海</option>
            <option value="3">天津</optionvalue>
            <option value="4">重庆</option>
        </select>
    <p>
        备注<textarea name="memo" rows="5" cols="20"></textarea>
    <p>
        <!--reset 重置 -->
        <input type="reset" value="重置">
        <input type="submit" value="保存">
        <input type="button" value="获取帮助">
</form>
</body>
</html>

###8、CSS概述及选择器优先级
    样式表
    CSS = Cascading Style Sheet = 层叠样式表
    用来控制网页上元素的颜色、外观、位置、大小等，让网页的样式更容易控制和管理，让网页变得更漂亮，美观的一种方法。
    作用：
    1.让网页变得漂亮
    2.让网页的格式更容易被控制
    DreamWeaver CS6
    DIV标记 ，层，一个矩形空间，中间可以放文字图片
    举一个小例子，来说明样式表出现的三种位置
    id => # class=>.
    id代表了唯一性。
     1.内嵌样式表
    style="font-size:26px"
     2.内部样式表
    <style type="text/css">
    .a
    {
    	font-size:16px;
    }
    </style>
     3.外部样式表
    <link rel="stylesheet" type="text/css" href="myfile.css"/>
    讲解两种基本的样式表选择器 
    选择器很多，暂时先讲两种
    selector:选中一个元素，对其进行样式设置的办法
     1.类选择器(样式表中用.命名，网页中用class指定样式表)
     2.ID选择器(样式表中用#命名，网页中用id指定样式表)

    CSS的优先级
    样式表优先级：就近原则，内嵌样式表>内部样式表>外部样式表
    选择器优先级：ID选择器>类选择器
###9、CSS样式分类及背景样式
    CSS属性的使用

    CSS属性分类

     1.背景
     2.文本
     3.边框
     4.外边距
     5.内边距
     6.列表

     背景样式

    background-color:颜色

    选择器：类选择器(class,.)、ID选择器(id,#),标签选择器
    body

    background-image:url(图片地址)
    image=图片

     background-repeat:no-repeat/repeat/repeat-x/repeat-y
     repeat=重复， 当图片覆盖不了整个区域的时候，是否需要重复，怎么重复的问题？

    background-attachment:fixed/scroll
    attachment：附着
    fixed:固定 scroll：滚动
    background-postion:X Y     
    X:left,center,right Y:top,center,bottom
    X,Y也可以设置左边距和右边距
###10、CSS文本样式

    CSS属性的使用

    文本样式

    字体颜色，文本间距，对齐方式

    1.字体颜色
     color

    2.字符间距
     letter-spacing

    3.行间距
     line-height

    4.文本对齐方式
     text-align:left/right/center,justify
     justify表示两端对齐

    5.修饰文本
      text-decoration
      包括下划线、上划线、删除线等
      text-decoration:underline/line-through/overline

    6.文本缩进
      text-indent

    7.转换大小写
     text-transform:capitalize/uppercase/lowercase
     其中capitalize表示第一个字母大写

    8.控制文本换行
     white-space：normal/pre/nowrap

    9.字体大小
     font-size

    10.选择字体
     font-family

###11、CSS边框样式

CSS属性的使用

    边框样式

    1.边框类型
     border-style:
 
     (1)solid	实线边框
     (2)double	双线边框，两条边框线的距离是：border-width

     以下边框根据border-color颜色值画出
     (3)groove	3D凹槽边框
     (4)ridge	菱形边框
     (5)inset	3D凹边
     (6)outset	3D凸边

    2.边框颜色
      border-color

      设置一个颜色：四个边框用一个颜色画出
      设置两个颜色：第一个颜色用于画出上下边框的颜色，第二个颜色用于画出左右边框的颜色
      设置四个颜色：按上右下左的顺时针顺序指定四个边框的颜色

    3.边框宽度
     border-width

    4.分别设置各个边框
      border-top,border-right,border-bottom,border-left
      例如：border-top:ridge 10px red;

    5.综合声明边框
     border
     例如：border:groove 2px blue;

###12、CSS内外边距样式
    CSS属性的使用

    外边距样式

    1.margin-top

    2.margin-right
     不能用来定义子块与父块的距离，只能定义子块与子块之间的距离。

    3.margin-bottom
     不能用来定义子块与父块的距离，只能定义子块与子块之间的距离。

    4.margin-left

    5.margin

     四个参数：上、右、下、左
     三个参数：上、左右、下
     两个参数  上下、左右


    内边距样式

    1.padding-top
    2.padding-right
    3.padding-bottom
    4.padding-left

    5.padding

    四个参数 上 右 下 左
    三个参数 上 左右 下
    两个参数 上下 左右
###13、后代选择器

    类(.),ID（#），标签选择器


    1.后代(派生)选择器

    h1 em  {color:red;}

    <h1>This is a <em>important</em> heading</h1>
    <p>This is a <em>important</em> paragraph.</p>

    div .a {background:blue;}

    <div>
    <p class="a">这是一段文字</p>
    <p>APEC会议在北京顺利闭幕!</p>
    </div>

    2.属性选择器

    什么叫属性
    <a href="test.jsp">测试</a>
    <hr width="50%">

    属性选择器可以根据元素的属性及属性值来选择元素。

    例子 1
    如果您希望把包含标题（title）的所有元素变为红色，可以写作：
    *[title] {color:red;}

    *=通配符

    例子 2
    与上面类似，可以只对有 href 属性的锚（a 元素）应用样式：
    a[href] {color:red;}

    例子 3
    还可以根据多个属性进行选择，只需将属性选择器链接在一起即可。
    例如，为了将同时有 href 和 title 属性的 HTML 超链接的文本设置为红色，可以这样写：
    a[href][title] {color:red;}

    <br/> = <br></br> = 自封闭标签


    根据具体属性值选择
    除了选择拥有某些属性的元素，还可以进一步缩小选择范围，只选择有特定属性值的元素。

    例子 1
    例如，假设希望将指向 Web 服务器上某个指定文档的超链接变成红色，可以这样写：
    a[href="http://www.w3school.com.cn/about_us.asp"] {color: red;}

    例子 2
    与简单属性选择器类似，可以把多个属性-值选择器链接在一起来选择一个文档。
    a[href="http://www.w3school.com.cn/"][title="W3School"] {color: red;}


    [attribute]	        用于选取带有指定属性的元素。
    [attribute=value]	用于选取带有指定属性和值的元素。

    [attribute~=value]	用于选取属性值中包含指定词汇的元素。

    p[title~="张"]

    [attribute|=value]	用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。

    p[title|="Test"] Test it

    [attribute^=value]	匹配属性值以指定值开头的每个元素。

    p[title^="Test"] Testit 或者是 Test it

    [attribute$=value]	匹配属性值以指定值结尾的每个元素。

    [attribute*=value]	匹配属性值中包含指定值的每个元素。


    根据元素的特殊状态来选取元素（伪类）
    根据元素中特别的内容（伪元素）

    伪类和伪元素的表示形式也使用“:”（英文冒号）与其它选择器相区分

    3.伪类
    根据元素的特殊状态来选取元素

    :link

    伪类将应用于未被访问过的链接，与:visited互斥。

    :hover

    伪类将应用于有鼠标指针悬停于其上的元素。

    :active

    伪类将应用于被激活的元素，如被点击的链接、被按下的按钮等。

    :visited

    伪类将应用于已经被访问过的链接，与:link互斥。

    需要注意的是在CSS的定义中，同一个元素的:hover必须位于:link、:visited之后才能生效，:active必须位于:hover之后才能生效。

    :link、:visited、:hover、:active


    :focus

    伪类将应用于拥有键盘输入焦点的元素。

    :first-child
    
    伪类将应用于元素在页面(或者在父容器)中第一次出现的时候。

    :lang

    伪类将应用于元素带有指定lang的情况。


    4.伪元素
    根据元素中特别的内容（伪元素）

    与伪类针对特殊状态的元素不同的是，伪元素是对元素中的特定内容进行操作，它所操作的层次比伪类更深了一层，也因此它的动态性比伪类要低得多。实际上，设计伪元素的目的就是去选取诸如元素内容第一个字（母）、第一行，选取某些内容前面或后面这种普通的选择器无法完成的工作。它控制的内容实际上和元素是相同的，但是它本身只是基于元素的抽象，并不存在于文档中，所以叫伪元素。

 

    :first-letter

    伪元素的样式将应用于元素文本的第一个字（母）。

    :first-line

    伪元素的样式将应用于元素文本的第一行。

    :before

    在元素内容的最前面添加新内容。

    举例

    在每个 <p> 元素的内容之前插入新内容：
    p:before
    { 
    content:"台词：";
    }


    p:before
    { 
    content:"台词：-";
    background-color:yellow;
    color:red;
    font-weight:bold;
    }
    :after

    在元素内容的最后面添加新内容。

    举例：与:before相同

###14、属性选择器
    类(.),ID（#），标签选择器


     1.后代(派生)选择器

     h1 em  {color:red;}

    <h1>This is a <em>important</em> heading</h1>
    <p>This is a <em>important</em> paragraph.</p>

    div .a {background:blue;}

    <div>
    <p class="a">这是一段文字</p>
    <p>APEC会议在北京顺利闭幕!</p>
    </div>

    2.属性选择器

    什么叫属性
    <a href="test.jsp">测试</a>
    <hr width="50%">
    属性选择器可以根据元素的属性及属性值来选择元素。

    例子 1
    如果您希望把包含标题（title）的所有元素变为红色，可以写作：
    *[title] {color:red;}

    *=通配符

    例子 2
    与上面类似，可以只对有 href 属性的锚（a 元素）应用样式：
    a[href] {color:red;}

    例子 3
    还可以根据多个属性进行选择，只需将属性选择器链接在一起即可。
    例如，为了将同时有 href 和 title 属性的 HTML 超链接的文本设置为红色，可以这样写：
    a[href][title] {color:red;}

    <br/> = <br></br> = 自封闭标签


    根据具体属性值选择
    除了选择拥有某些属性的元素，还可以进一步缩小选择范围，只选择有特定属性值的元素。

    例子 1
    例如，假设希望将指向 Web 服务器上某个指定文档的超链接变成红色，可以这样写：
    a[href="http://www.w3school.com.cn/about_us.asp"] {color: red;}

    例子 2
    与简单属性选择器类似，可以把多个属性-值选择器链接在一起来选择一个文档。
    a[href="http://www.w3school.com.cn/"][title="W3School"] {color: red;}


    [attribute]	        用于选取带有指定属性的元素。
    [attribute=value]	用于选取带有指定属性和值的元素。

    [attribute~=value]	用于选取属性值中包含指定词汇的元素。

    p[title~="张"]

    [attribute|=value]	用于选取带有以指定值开头的属性值的元素，该值必须是整个单词。

    p[title|="Test"] Test it

    [attribute^=value]	匹配属性值以指定值开头的每个元素。

    p[title^="Test"] Testit 或者是 Test it

    [attribute$=value]	匹配属性值以指定值结尾的每个元素。

    [attribute*=value]	匹配属性值中包含指定值的每个元素。


    根据元素的特殊状态来选取元素（伪类）
    根据元素中特别的内容（伪元素）

    伪类和伪元素的表示形式也使用“:”（英文冒号）与其它选择器相区分

    3.伪类
    根据元素的特殊状态来选取元素

    :link

    伪类将应用于未被访问过的链接，与:visited互斥。

    :hover

    伪类将应用于有鼠标指针悬停于其上的元素。

    :active

    伪类将应用于被激活的元素，如被点击的链接、被按下的按钮等。

    :visited

    伪类将应用于已经被访问过的链接，与:link互斥。

    需要注意的是在CSS的定义中，同一个元素的:hover必须位于:link、:visited之后才能生效，:active必须位于:hover之后才能生效。

    :link、:visited、:hover、:active


    :focus
    
    伪类将应用于拥有键盘输入焦点的元素。

    :first-child

    伪类将应用于元素在页面(或者在父容器)中第一次出现的时候。

    :lang

    伪类将应用于元素带有指定lang的情况。


    4.伪元素
    根据元素中特别的内容（伪元素）

    与伪类针对特殊状态的元素不同的是，伪元素是对元素中的特定内容进行操作，它所操作的层次比伪类更深了一层，也因此它的动态性比伪类要低得多。实际上，设计伪元素的目的就是去选取诸如元素内容第一个字（母）、第一行，选取某些内容前面或后面这种普通的选择器无法完成的工作。它控制的内容实际上和元素是相同的，但是它本身只是基于元素的抽象，并不存在于文档中，所以叫伪元素。

 

    :first-letter

    伪元素的样式将应用于元素文本的第一个字（母）。

    :first-line
    
    伪元素的样式将应用于元素文本的第一行。

    :before

    在元素内容的最前面添加新内容。

    举例

    在每个 <p> 元素的内容之前插入新内容：
    p:before
    { 
    content:"台词：";
    }


    p:before
    { 
    content:"台词：-";
    background-color:yellow;
    color:red;
    font-weight:bold;
    }
    :after

    在元素内容的最后面添加新内容。

    举例：与:before相同


















