 安装强大的SublimeClang插件
   SublimeClang是Sublime Text中唯一的C/C++自动补全插件，功能强大，自带语法检查功能，不过最近作者已经停止更新了，目前只能在Sublime Text 2的Package Control中可以找到并自动安装，在SublimeText 3中只能手动通过源码安装，其代码线在https://github.com/quarnster/SublimeClang中。具体安装步骤如下：

    安装相关软件
        sudo apt-get install cmake build-essential clang git
        cd ~/.config/sublime-text-3/Packages
        git clone --recursive https://github.com/quarnster/SublimeClang SublimeClang
        cd SublimeClang
        cp /usr/lib/x86_64-linux-gnu/libclang-3.4.so.1 internals/libclang.so      #这一步很重要，如果你的clang库不是3.4版本的话，请将对应版本的库拷贝到internals中
        cd src
        mkdir build
        cd build
        cmake ..
        make

一切成功的话将会在SublimeClang/internals目录中生成libcache.so库文件。重启Sublime Text，然后按快捷键Ctrl + `(Esc下面那个键)打开自带的控制输出，看看有没有错误，如果没有错误就说明一切OK了。接下来就是配置自己的文件了，按下ctrl + shift + p快捷键，在弹出的输入框中输入 sublimeclang settings ，然后选择带User那一行，在打开的文件中输入如下信息：

    {
        "show_output_panel": false,
        "dont_prepend_clang_includes": true,
        "inhibit_sublime_completions": false,

        "options":
        [
            "-std=gnu++11",
            "-isystem", "/usr/include",
            "-isystem", "/usr/include/c++/*",
            "-isystem", "/usr/include/c++/4.8",
            "-isystem", "/usr/include/c++/4.8/*",
            "-isystem", "/usr/include/boost",
            "-isystem", "/usr/include/boost/**",
            "-isystem", "/usr/lib/gcc/x86_64-linux-gnu/4.8/include",
            "-isystem", "/usr/lib/gcc/x86_64-linux-gnu/4.8/include/*"
        ]
    }
    注释：我的gcc版本为4.8，如果你的不是请替换对应的版本，在#include相应的头文件后保存当前文件，在接下来的操作中将更快的提示所包含在头文件的函数或者变量。