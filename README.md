# cmake_learning
这是一个学习CMake的项目
CMake概述
CMake是一个项目的构建工具，并且是跨平台的，关于项目的构建我们所熟知的还有Makefile（通过make命令进行项目的构建），大多数IDE软件都集成了make。比如VS的nmake、Linux的GNU make、qt的qmake。如果自己手动的编写makefile，会发现，makefile通常依赖于当前的平台，而且编写makefile的工作量比较大，解决依赖关系时也容易出错。
而CMake可以解决makefile的问题。CMake可以根据开发平台自动的生成makefile文件和工程文件夹，最后用户只需要用make编译即可。
综上所述，CMake可以看作一个自动编写Makefile文件的工具。
 -------------------编写-------------》
 |                                   |
项目-->CMakeLists.txt-->cmake-->Makefile->make->目标文件
一般的C/C++程序是通过工具链（tool chain）进行预处理，然后通过编译和汇编生成中间文件，中间文件之间通过链接来生成可执行文件。
CMake的使用
注释
cmake的注释有两种一种是以 ‘#’ 开头的单行注释，以下是一个示例
# 这是一个CMakeLists.txt文件
cmake_minimum_required(VERSION 3.0.0)
以上是一个最小的cmake的文件其中有一个单行注释和一个约束，来告诉cmake可以运行的最小版本。
多行注释就是在 ‘#’ 后面添上’[[]]‘,在两个中括号之间写多汗注释
#[[这个

是一个

多行

注释]]
cmake_minimum_required(VERSION 3.0.0)
project
project：定义工程名称，并可以指定工程的版本、工程描述、web主页地址、支持的语言，如果不需要这些都是可以忽略的，只需要制定出工程名字即可。
project(<ProjectName> 
    [VERSION <major>[.<minor>[.<patch>[.<tweak>]]]] 
    [LANGUAGES languages...] 
    [HOMEPAGE_URL url] 
    [DESCRIPTION description] 
    [COMPONENTS components...])
其中，<ProjectName>是项目的名称，它是一个必需的参数。可以选择一个可选的VERSION参数来指定项目的版本号，版本号可以包含主版本号、次版本号、补丁版本号和调整版本号。
此外，还可以选择使用LANGUAGES参数指定项目使用的编程语言，HOMEPAGE_URL参数指定项目的主页URL，DESCRIPTION参数用于提供项目的描述信息。
另外，还可以使用COMPONENTS参数来定义项目的组件。组件是项目中的独立部分，可以用于模块化构建和安装。
add_executable
add_executable定义工程会生成一个可执行程序，语法如下：
add_executable(可执行程序名 源文件名称)
这里的可执行程序名和工程的项目名称没有任何关系，可以随意指定。源文件名称可以是一个也可以是多个，如果有多个可以用空格或者‘；’间隔。
# 样式1
add_executable(app add.cpp div.cpp main.cpp sub.cpp)
# 样式2
add_executable(app add.cpp;div.cpp;main.cpp;sub.cpp)
set
set是用来自定义值的一个函数它的用法如下：
set(变量名 值)
注意在CMakeLists.txt文件中所有的量都是字符串类型，如果需要使用其他类型需要转换。
当要使用变量的时候，要将变量名称用“${变量名}”。
示例：
# 这是一个CMakeLists.txt文件
cmake_minimum_required(VERSION 3.0.0)
project(APP)
set(SRC_LIST add.cpp div.cpp main.cpp mul.cpp sub.cpp)
add_executable(app ${SRC_LIST})
