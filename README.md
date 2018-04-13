由于公司的项目比较多，而且总更新不同的版本，测试人员有的时候会拿来一个不知n月前安装的App告诉你，这个App有问题，然后这个问题你会发现是早就修改过的，但是测试者不知你App的具体信息，你也不知是什么时候给安装过的。因此就想到了这个方法，把程序的信息直接放到了App的图标上，让测试人员和你都能快速定位问题，我是把版本号，SVN上对应代码的版本，打包的时间显示在图标上了(这个根据自己的情况来显示，你就放你的名字都是可以的)，只是用来内部测试使用。

实现的效果图：



下边介绍下整个安装流程：

实现上边效果需要执行一个脚本，在ios中使用脚本真的很方便，最近已经迷上用脚本做一些事情了，比如打包项目、显示SVN版本号到Build中、清除项目中的没有使用的图片等等等。

首先需要在Xcode中Target的Build Phases中，添加一个Run Script的Build Phase来执行一些脚本做一些操作，这里的脚本会在每次build的时候执行，然后我们就可以通过脚本给App图标添加版本信息了。



编辑Shell 把脚本的位置放上就可以了



在这里再说下怎么在iOS中使用Shell语句吧

你可以先输入echo "Hello World" （第一个想起的就是输出这个） 


然后Command + B 构建工程，可以通过下边的方式或者快捷键Command + 8 查看构建日志，测试脚本已经成功执行。



 输出的结果






下边就开始将版本信息填充到App 图标上

将版本信息填充到图标上，这里需要安装2个工具：ImageMagick和ghostscript，ImageMagicK的convert命令可以将文字写到图片上。

步骤1：下载XQuartz-2.7.11.dmg
下载地址：https://www.xquartz.org/ 

步骤2：安装homebrew （我理解 就相当于AppStore）
shell中执行如下命令 
/usr/bin/ruby -e “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)” 

步骤3：执行命令
brew install imagemagick

imagemagick已经成功安装。 

homebrew方式安装的imagemagick路径默认在/usr/local/Cellar路径下

步骤4：安装ghostscript

ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)" < /dev/null 2> /dev/null
brew install ghostscript
ghostscript已经成功安装。 

至此，安装完毕 ，现在开始讲解下脚本中的配置

根据自己图标的位置来修改对应地址（icons_path指现地址 icons_dest_path指生成后的地址）



显示的内容  我这里是根据需要进行修改的  这块可以根据自己的需要来修改


caption="version:${version}\build:${build_num}\ntime:${Timer}"


以上就是按照和使用的方式，在运行成功之后 会生成一个新图标的类 进行选择再次运行就可以了




文章的地址：
https://blog.csdn.net/wangxinxu521/article/details/79911213
