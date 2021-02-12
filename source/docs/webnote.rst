.. _wetnote:

==================
创建网页笔记
==================

大家平时一定看过很多资料，查过很多资料，当时理解了，但是过后又忘了，等到需要用的时候又要重新去搜索，\
这浪费了很多时间，解决这个问题最好的办法就是有一个专属自己的笔记本，我自己也记过很多笔记，比如写个\
word、txt之类的，但是笔记多了之后就容易乱，而且有时候会觉得这些文档工具的排版不是很美观，这时候如果\
有一个专业排版的云端网页笔记本，那所有的问题就解决了，本文档就是教你如何创建属于自己的云端网页笔记。

所需工具
==================

创建网页笔记所需的工具有Sphinx、GitHub、Readthedocs。下面对这些工具做个简单的介绍：

- Sphinx 是一种文档工具，它可以令人轻松的撰写出清晰且优美的文档, 由 Georg Brandl 在BSD 许可证下开发.\
  新版的Python文档 就是由Sphinx生成的， 并且它已成为Python项目首选的文档工具,同时它对C/C++ 项目也有\
  很好的支持; 并计划对其它开发语言添加特殊支持。本站当然也是使用 Sphinx 生成的，它采用reStructuredText语言。
 
- GitHub是一个面向开源及私有软件项目的托管平台，因为只支持Git作为唯一的版本库格式进行托管，故名GitHub。
 
- Read the Docs是一个基于Sphinx的在线文档托管系统，接受一个Git Repository或SVN仓库作为文档来源。
 
为了帮助理解，打个比方，Sphinx就像是一个编译器，他可以将我们按照一定的reStructuredText语法编写的文档代码\
翻译成优美的可读的文档，就像LaTeX可以将代码翻译成PDF文档一样。我们写好的文档代码可以放在本地磁盘，也可以\
放在云端仓库，GitHub就是这个云端仓库。Readthedocs就是托管我们的文档，让它以网页的形式展示给我们。

Sphinx安装
=============

几篇教程:

- 这里是一个中文教程: sphinx使用手册_
- 这里是官方网站: Sphinx_
- 这里是一篇reStructuredText的教程: reStructuredText_


.. _reStructuredText: http://www.bary.com/doc/a/228277572381775842/
.. _Sphinx: http://www.sphinx-doc.org
.. _sphinx使用手册: http://zh-sphinx-doc.readthedocs.io


*TBD*

Git安装与GitHub的使用
=======================

GitHub的几篇教程:

+ 一篇GitHub教程: GitHub的使用_
+ 本地连接GitHub的两种方式对比: `ssh VS https`_，`signing failed`_


.. _`ssh VS https`: http://blog.csdn.net/oDeviloo/article/details/52654590
.. _GitHub的使用: http://blog.csdn.net/hcbbt/article/details/11651229/
.. _`signing failed`: https://www.cnblogs.com/ailhc/p/6586465.html

*TBD*

Readthedocs的使用
======================

*TBD*

Windows开发环境快速搭建
==========================

.. important::

    只针对Windows10系统，其他Windows系统可能有安装依赖问题

1. 安装python3。
#. 安装Vim for windows(GVim)。
#. 安装Git for windows。
#. 安装pip。
#. 使用pip安装sphinx。

   a. 打开cmd，运行安装命令： ``pip install -U sphinx``
   #. 检查是否安装成功： ``sphinx-build --version``
   #. 如果需要使用最新的开发版，则使用命令： ``pip install -U --pre sphinx``
   #. 安装Read the Docs主题库，运行命令： ``pip install sphinx_rtd_theme``

#. 获取实例，修改，编译。

   a. 在需要存放实例的路径打开CMD ``ALT+D`` 输入CMD回车
   #. 运行命令： ``git clone https://github.com/BryanSDCN/note.git``
   #. 使用Vim打开工程主文件index.rst： ``vim source\index.rst`` ，修改并保存

      + 如果遇到如下问题：

        .. image:: /images/vimbug1.png
         :alt: bug1

        vim的rst语法文件有中文码问题，打开vim\\vim82\\syntax\\rst.vim，修改第123行。
        
      + 如果vim打开中文是乱码：

        文件.vimrc中增加 ``set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936`` 。

   #. 编译工程： ``make html`` ，查看编译结果： ``.\build\html\index.html`` 。

      .. important::
         如果编译之后网页没有更改，运行 ``make clean`` ，清除缓存，重新全部编译



参考链接
======================

#. http://www.jianshu.com/p/78e9e1b8553a
#. http://wowubuntu.com/restructuredtext-sphinx.html
#. https://zhuanlan.zhihu.com/p/27544821








