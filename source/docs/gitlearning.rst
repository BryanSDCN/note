.. _gitlearning:

======================
Git简单教程
======================

*这里简单讲解一下Git的使用方法*


本地仓库如何上传到GitHub仓库
======================================

方式一
-----------

1. 在GitHub新建仓库
#. 本地使用命令git clone，将空仓库复制到本地
#. 将工程文件copy到本地空仓库
#. 使用命令git add -> commit -> push，将代码上传到GitHub

.. note::

   该方式无法保留之前的本地commit


方式二
--------------------

1. 在GitHub创建新仓库，得到远程仓库链接
#. 进入本地仓库目录，增加远程仓库链接

   | 命令 ``git remote add origin https://github.com/yourgithubID/gitRepo.git``
   | 查看文件 ``.git\config`` 是否已经修改

#. 推送本地工程文件到远程仓库
   
   | 命令 ``git push -u origin master`` ，命令中的origin是上一步中的远程名


.. note::

   该方式可以保留本地之前的所有commit


Git文件介绍
=====================

介绍Git项目中的常见文件的作用

.gitattributes
----------------------

1. 用于统计GitHub文件统计

   Github中创建一个repository后会出现一个统计使用语言的颜色条。只需要在工程中加上一个.gitattributes，内容为：

   ::

      *.js linguist-language=Java
      *.css linguist-language=Java


   也就是把js、css后缀的文件都算作Java。也可以使用linguist-vendored属性来设置是否进行统计，例如：

   ::

      special-vendored-path/* linguist-vendored
      jquery.js linguist-vendored=false   

#. gitattributes文件以行为单位设置一个路径下所有文件的属性。在gitattributes文件的一行中，一个属性（以text属性为例）可能有4种状态：
   
   + 设置text
   + 不设置-text
   + 设置值text=string
   + 未声明，通常不出现该属性即可；但是为了覆盖其他文件中的声明，也可以!text

   gitattributes文件示例：

   ::

      
     *          text=auto
     *.txt      text
     *.jpg      -text
     *.vcproj   text eol=crlf
     *.sh       text eol=lf
     *.py       eol=lf


   说明：

   第1行，对任何文件，设置text=auto，表示文件的行尾自动转换。如果是文本文件，则在文件入Git库时，行尾自动转换为LF。如果已经在入Git库中的文件的行尾为CRLF，则该文件在入Git库时，不再转换为LF。
   第2行，对于txt文件，标记为文本文件，并进行行尾规范化。

   第3行，对于jpg文件，标记为非文本文件，不进行任何的行尾转换。

   第4行，对于vcproj文件，标记为文本文件，在文件入Git库时进行规范化，即行尾为LF。但是在检出到工作目录时，行尾自动转换为CRLF。

   第5行，对于sh文件，标记为文本文件，在文件入Git库时进行规范化，即行尾为LF。在检出到工作目录时，行尾也不会转换为CRLF（即保持LF）。

   第6行，对于py文件，只针对工作目录中的文件，行尾为LF。


