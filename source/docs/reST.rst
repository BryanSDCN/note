.. _reST:

========================
reStructuredText 简介
========================

reStructuredText是一种轻量级的文本标记语言，直译为：重构建的文本，为Python中Docutils项目的一部分。
其一般保存的文件以.rst为后缀。在必要的时候，.rst文件可以被转化成PDF或者HTML格式，
也可以有Sphinx转化为LaTex,man等格式，现在被广泛的用于程序的文档撰写。

参考链接：
 
| http://www.pythondoc.com/sphinx/index.html
| http://www.sphinx-doc.org/en/stable/markup/toctree.html


标题（Title）
==================

来看看标题的实例: ::

	=====================
	这是一个标题
	=====================
	
	---------------------
	这也是一个标题
	---------------------
	
	#####################
	这还是一个标题
	#####################

reStructuredText可用于作为标题修饰的字符有很多很多: ::

	! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~

只要你想，上面的任意一个都可以用来作为标题的修饰符，当然，reStructuredText也是有推荐的，它推荐下面这些字符: ::

	= - ` : . ' " ~ ^ _ * + #

这些字符是上面一堆字符中稍微看起来不会那么奇怪的一部分，当然，个人建议不要那么花哨，尽量用这两个中的一个: ::

	= -

上面实例的写法也许有点复杂，.rst文件中，你还可以只给出下半部分的字符即可: ::

	这和第一个标题一样
	========================

对于相同的符号，有上标是一级标题，没有上标是二级标题。
标题最多分六级，可以自由组合使用。
全加上上标或者是全不加上标，使用不同的 6 个符号的标题依次排列，则会依次生成的标题为H1-H6。 ::

	=========
	一级标题
	=========
	
	二级标题
	=========

	一级标题
	^^^^^^^^
	
	二级标题
	---------
	
	三级标题
	>>>>>>>>>
	
	四级标题
	:::::::::
	
	五级标题
	'''''''''
	
	六级标题
	""""""""

.. hint:: 作为修饰的字符长度要大于等于文字长度。另外，标题是能够嵌套的。

段落（Paragraphs）
====================
段落是reST文件的基本模块。段落一般隶属于某个章节中，是一块左对齐并且没有其他元素体标记的块。在.rst文件中，段落和
其他内容的分割是靠空行来完成，如果段落相较于其他的段落有缩进，reStructuredText会解析为引用段落，样式上有些不同。 ::

	这里是一段reStructuredText的内容，它可以很长很长。。。。最后，末尾留出空行表示是本段落的结束即可。

	这里是另外一段reStructuredText的内容，这段内容和上一段之间，乃至后面的其他内容之间都要留出空行进行分割。
	
		这个也是段落，当时由于缩进了，会变成引用段落。显示和直接的段落有点不同
		
列表(List)
=====================

列表在HTML中被分为两种，一个是有序列表（Enumerated Lists），一种是无序列表（Bullet Lists），在reStructuredText中，
我们也能找到这两种列表，还有一种称为定义列表（Definition Lists），这和HTML中的DL一样，在.rst文件中可以支持嵌套列表。

*无序列表* 要求文本块是以下面这些字符开始，并且后面紧跟空格，而后跟列表项的内容，其中列表项比趋势左对齐并且有与列表对应的缩进。 ::

	* + - •

还是那句话，用最常用的几个字符就好，不用那么花哨。下面是示例： ::

	- 这里是列表的第一个列表项
 
	- 这是第二个列表项
 
	- 这是第三个列表项
 
		- 这是缩进的第一个列表项
			注意，这里的缩进要和当前列表项的缩进同步。
 
	- 第一级的第四个列表项
 
	- 列表项之间要用个空格来分割。

*有序列表* 在格式上和无序列表差不多，但是在使用的前缀修饰符上，使用的不是无序列表那种字符，而是可排序的字符，可以识别的有下面这些： ::

	arabic numerals: 1, 2, 3, ... (no upper limit).
	uppercase alphabet characters: A, B, C, ..., Z.
	lower-case alphabet characters: a, b, c, ..., z.
	uppercase Roman numerals: I, II, III, IV, ..., MMMMCMXCIX (4999).
	lowercase Roman numerals: i, ii, iii, iv, ..., mmmmcmxcix (4999).

如果你不想使用这些，在你标明第一个条目的序号字符后，第二个开始你还可以使用"#"号来让reStructuredText自动生成需要的序号（Docutils >= 0.3.8）。 ::

	1. 第一项
		巴拉巴拉好多内容在这里。。。
 
	#. 第二项
 
		a. 第二项的第一小项
 
		#. 第二项的第二小项
 
	#. 第三项

*定义列表* ：每个定义列表项里面包含术语（term），分类器（classifiers，可选）， 定义（definition）。术语是一行文字或者短语，分类器跟在术语后面，
用“ ： ”(空格，冒号，空格）分隔。定义是相对于术语缩进后的一个块。定义中可以包含多个段落或者其他的内容元素。术语和定义之间可以没有空行，
但是在定义列表前后必须要有空行的存在。下面是示例： ::

	术语1
		术语1的定义
	 
	术语 2
		术语2的定义,这是第一段
	 
		术语2的定义，第二段
	 
	术语 3 : 分类器
		术语3的定义
	 
	 
	术语 4 : 分类器1 : 分类器2
		术语4的定义

.. hint:: 在reStructuredText中，还有两种列表，一种是字段列表（Field Lists），一种是选项列表（Option Lists）。由于是rst的语法入门教程，这里不做深入介绍

块（Blocks）
=====================

块在reStructuredText中的表现方式也有好几种，最常见的包括文本块、引用文本块、行块、引用块。

文本块(Literal Blocks)
-------------------------

这种块的表达非常简单，就是在前面内容结束之后，用两个冒号" :: "(空格[Optional]，冒号，冒号）来分割，
并在之后紧接着插入空行，而后放入块的内容，块内容要相对之前的内容有缩进。 ::

	这里是块之前的的内容。。。 ::

		这里是块的内容。前面有缩进，空行，和::分隔符。
		此处内容会被一直视为块内容

		空行也不能阻断块内容。。

	但是，当内容像这样，不再和块内容一样缩进时，块内容就自动的结束了。
	
这是块的最简单方式，一般我们编写的代码块就是用这种方式表现。

引用文本块(Quoted Literal Blocks)
---------------------------------------

引用文本块是非缩进的连续文本块，其每一行以相同的非字母可打印7位ASCII字符开始。引用文本快由
空行结束。引用文本快会在处理过的文档中保存。

以下是所有有效缩进字符: ::

	! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~

.. note:: 这与有效的章节标题装饰相同。

下面是引用文本块的例子： ::

! 这里是引用文本块的内容
! 这里是另一行
! 这是第三行
! 空行作为结束

行块（Line Blocks）
--------------------------------

行块对于地址块很有用。诗(诗歌、歌词)和无装饰列表等行结构有重要 意义。行块是一组由竖线(“|”)前缀开头的行。
每个竖线前缀表示一个新行，因此折行会被保留。初始缩进对于嵌套结构也很重要。支持行内标记。连续行被包装为
一个长的行，他们以一个空格代替竖线开始，左边必须对齐，但不需要与上面的文字的左边对齐。行块以空行结束。

这个例子展示了行块连续行:

| 这是一个行块的第一行，我需要打很多的字来填充
| 这一行，所以这些字可能没有什么意义，比如像这样的字，阿斯
| 蒂芬拉就是的房间辣豆腐机安检打发斯蒂芬，请你不要在意。。。
| 这是第二行，我真的没有时间打这么多字，所以我

	| 就复制粘贴了上一行的内容，所以这些字可能没有什么意义，
	| 比如像这样的字，阿斯蒂芬拉就是的房间辣豆腐机安检打发斯蒂芬，请你不要在意。。。
	| 这是第二行，我真的没有时间打这
	| 么多字，所以我就复制粘贴了上一行的内容，所以这些字可能没有什么意义，

| 比如像这样的字，阿斯蒂芬拉就是的房间辣豆腐机安检打发斯蒂芬，请你不要在意。。。
| 这是第二行，我真的没有时间打这么多字，所以我就复制粘贴了上一行的内容，所以这些
| 字可能没有什么意义，比如像这样的字，阿斯蒂芬拉就是的房间
| 辣豆腐机安检打发斯蒂芬，请你不要在意。。。

引用块（Block Quotes）
--------------------------------

一个以缩进与前面的文本关联的文本块，前面没有标记表示其为文被快或其他内容的，是引用块。
里面的所有标记会被连续处理（对于正文元素和行内标记)

这个例子展示了引用块：

	这是一个引用块的第一行，我需要打很多的字来填充
	这一行，所以这些字可能没有什么意义，比如像这样的字，阿斯
	蒂芬拉就是的房间辣豆腐机安检打发斯蒂芬，请你不要在意。。。
	这是第二行，我真的没有时间打这么多字，所以我
	
		就复制粘贴了上一行的内容，所以这些字可能没有什么意义，
		比如像这样的字，阿斯蒂芬拉就是的房间辣豆腐机安检打发斯蒂芬，请你不要在意。。。
		这是第二行，我真的没有时间打这
		么多字，所以我就复制粘贴了上一行的内容，所以这些字可能没有什么意义，

	比如像这样的字，阿斯蒂芬拉就是的房间辣豆腐机安检打发斯蒂芬，请你不要在意。。。
	这是第二行，我真的没有时间打这么多字，所以我就复制粘贴了上一行的内容，所以这些
	字可能没有什么意义，比如像这样的字，阿斯蒂芬拉就是的房间
	辣豆腐机安检打发斯蒂芬，请你不要在意。。。

样式(Style)
=====================

reStructuredText中支持对文本进行样式控制，比如：粗体(Strong)，斜体(Italic)，等宽字体(Monospace)，引用( interpreted text)。 ::

	.. Strong Emphasis

	This is **Strong Text**. HTML tag is strong.粗体

	.. Italic, Emphasis

	This is *Emphasis* Text.这个HTML使用em， 斜体

	.. Interpreted Text

	This is `Interpreted Text`. 注意，这个HTML一般用<cite>表示

	.. Inline Literals

	This is ``Inline Literals``. HTML tag is <tt>. 等宽字体.


超链接(Hyperlink)
==========================

介绍各类带有链接性质的超链接

参考链接： https://www.cnblogs.com/seayxu/p/5603876.html

自动超链接
----------------------------

reStructuredText会自动将网址生成超链接。 ::

	https://www.google.com

https://www.google.com

外部超链接(External Hyperlink)
---------------------------------------------

引用/参考(reference)，是简单的形式，只能是一个词语，引用的文字不能带有空格。 ::

	这篇文章来自我的Github,请参考 reference_。

	.. _reference: https://www.google.com

这篇文章来自我的Github,请参考 reference_。

.. _reference: https://www.google.com
	
引用/参考(reference)，行内形式，引用的文字可以带有空格或者符号。 ::

	这篇文章来自我的Github,请参考 `Google <https://www.google.com>`_。

这篇文章来自我的Github,请参考 `Google <https://www.google.com>`_。

内部超链接|锚点(Internal Hyperlink)
--------------------------------------------------------------
::

	更多信息参考 引用文档_

	这里是其他内容

	.. _引用文档:

	这是引用部分的内容

更多信息参考 引用文档_

这里是其他内容

.. _引用文档:

这是引用部分的内容

匿名超链接(Anonymous hyperlink)
-------------------------------------------------------------------

词组(短语)引用/参考(phrase reference)，引用的文字可以带有空格或者符号，需要使用反引号引起来。
::

	这篇文章参考的是：`Quick reStructuredText`__。

	.. __: http://docutils.sourceforge.net/docs/user/rst/quickref.html

这篇文章来自我的Github,请参考 `Quick reStructuredText`__。

.. __: http://docutils.sourceforge.net/docs/user/rst/quickref.html


间接超链接(Indirect Hyperlink)
---------------------------------------------------------------

间接超链接是基于匿名链接的基础上的，就是将匿名链接地址换成了外部引用名。
::

	SeayXu_ 是 `我的 GitHub 用户名`__。

	.. _SeayXu: https://github.com/SeayXu/

	__ SeayXu_

SeayXu_ 是 `我的 GitHub 用户名`__。

.. _SeayXu: https://github.com/SeayXu/

__ SeayXu_


隐式超链接(Implicit Hyperlink)
------------------------------------------------------

小节标题、脚注和引用参考会自动生成超链接地址，使用小节标题、脚注或引用参考名称作为超链接名称就可以生成隐式链接。 ::

	第一节 介绍
	===========

	其他内容...

	隐式链接到 `第一节 介绍`_，即可生成超链接。

替换引用(Substitution Reference)
-------------------------------------------------------

替换引用就是用定义的指令替换对应的文字或图片，和内置指令(inline directives)类似。 ::

	这是 |logo| github的Logo，我的github用户名是:|name|。

	.. |logo| image:: https://help.github.com/assets/images/site/favicon.ico
	.. |name| replace:: Google

这是 |logo| github的Logo，我的github用户名是:|name|。

.. |logo| image:: https://help.github.com/assets/images/site/favicon.ico
.. |name| replace:: Google

.. hint:: 我们会发现，两个处理连接的时候，都需要在链接文字前面要空格与前面进行分割，这个在英文当中比较好处理，
	因为单个词之间有空格，而在中文中，字之间没有空格，如果加入空格，在显示时会有空格，影响观感，为此，如果在中文中使用，需要考虑好。

指令(Directives )
=============================

指令是reStructuredText的扩展机制，一种添加支持新结构而不用添加新的语法（指令支持额外的本地语法）的方法。

如果reStructuredText的某种实现不能识别一个指令(如，指令处理器未安装 )，会生成一个3级(error)系统信息，
且整个指令块(包括指令本身)会被包含 为一个文本块。因为”::”是一个自然选择。

参考链接： http://docutils.sourceforge.net/docs/ref/rst/directives.html#code

主要的指令有以下几种：

警告指令
--------------------

警告类型有如下多种： ::

	attention, caution, danger, error, hint, important, note, tip, warning, admonition, title
	
警告被特别的标记为”topics”，可以呈现在任何原始正文元素呈现的位置。它们包含任意正文元素。通常，
警告被渲染为文档中的一个偏移块，有时是一个匹配警告类型的标题的概述或阴影。例如:

.. DANGER::
	| This is danger.
	| Beware killer rabbits!

.. attention::
	This is attention.

.. caution::
	This is caution.
	
.. important::
	This is important.

任何跟在指令指示器后的文本(在同一行和/或下一行缩进)都会被解释为一个指令块并被解析为普通的正文元素。
例如，下面的”note”警告指令包含一个段落和一个有两个列表项组成的无序列表:

.. note:: This is a note admonition.
   This is the second line of the first paragraph.

   - The note contains all indented body elements
     following.
   - It includes this bullet list.
   
图片指令
--------------------

常用的两个图片指令: “image”和”figure”

下面是一个图片指令和所需选项的例子： ::

	.. image:: picture.jpeg
		:height: 100px
		:width: 200 px
		:scale: 50 %
		:alt: alternate text
		:align: right

下列选项可以被识别:

	| **alt** : 替换文本: 当应用无法显示图片时，会显示图片的一个简短的描述或 由应用为视觉受损的用户读出。
	| **height** : 图片所需要的高。用于存储空间或比例尺图片的纵向。当”scale”也被 指定了，它们会组合到一起。例如，一个高位200px且比例尺为50等 价于高位100px且没有比例尺。
	| **width** : 图片的宽度。用于存储空间或比例尺图片的横向类似”height”，当指定 “scale”选项，则会被组合。
	| **scale** : 图片的统一缩放因子。默认”100%”，即无缩放。如果未指定高度和宽度选项，如果安装了 Python图片库 (PIL)且图片有效，则其会被会用于决定它们。
	| **align** : “top”, “middle”, “bottom”, “left”, “center”, or “right”图片的对齐方式，等价于HTML的 <img> 标签的”align”属性。 值”顶端”、”居中”、”底部”用于
		控制图片的纵向对齐(与文本基线关联)。它们只对行内图片(替代)有用。 值”左”、”中”、”右”用于控制图片的横向对齐，
		允许图片漂浮，文字围绕图片。具体的行为取决于浏览器或用于渲染的软件。
	| **target** : 文本(URI或引用名称)将图片变为超链接引用(“可点击”)。可选参数是一个URI(相对或绝对)，或一个包含下划线前缀的引用名称。
	| 以及通用选项 **:class:** and **:name:**.
	
代码指令
-----------------------
代码指令用于插入代码块，并可以实现语法高亮。

关于语法高亮： http://pygments.org/languages/

下面是例子：

::

	.. code:: python
		:name: bbbb

		def my_function():
			"just a test"
			print 8/2

下面是效果：

..	code:: python
	:name: bbbb
	
	def my_function():
	    "just a test"
	    print 8/2

rtd theme 配置
================================

rtd 主题由Read the Doc团队开发，主题美观大方。本小节将以此主题为例，说明主题如何自定义。

主题的配置文件在 ``sphinx_rtd_theme/theme.conf`` 文件中，默认配置如下：

::

    [theme]
    inherit = basic
    stylesheet = css/theme.css

    [options]
    typekit_id = hiw1hhg
    analytics_id =
    sticky_navigation = False
    logo_only =
    collapse_navigation = False
    display_version = True
    navigation_depth = 4
    prev_next_buttons_location = bottom
    canonical_url =


基本选项含义：

* ``analytics_id`` 字符串。配置 Google Analytics ID 可以追踪网站访问情况。
* ``display_version`` 布尔值。配置是否显示版本号。

导航栏选项：

* ``collapse_navigation`` 布尔值。启用后，不在导航栏中显示 +。
* ``navigation_depth`` 整数。最大深度为4层，设置为 -1 表示不限制深度。

更多说明，可见 `官方文档 <https://sphinx-rtd-theme.readthedocs.io/en/latest/configuring.html>`_


PDF输出：http://media.readthedocs.org/pdf/doclikecode/latest/doclikecode.pdf


其他例子
======================

该文本是 ``行内文本`` 的一个例子。

This is `interpreted text`.

See the `Python home page <http://www.python.org>`_ for info.

This `link <Python home page_>`_ is an alias to the link above.

See the `Python home page`_ for info.

This link_ is an alias to the link above.

.. _Python home page: http://www.python.org
.. _link: `Python home page`_