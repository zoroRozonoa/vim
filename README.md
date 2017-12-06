# vim
Ubuntu vim安装、配置指南

vim源码编译
编译Vim之前，需要下载编译的相关工具和一些库
sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev libgtk2.0-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev ruby-dev mercurial

git clone git@github.com:vim/vim.git
cd vim/
./configure --with-features=huge --enable-rubyinterp --enable-pythoninterp --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu/ --enable-perlinterp --enable-gui=gtk2 --enable-cscope --enable-luainterp --enable-perlinterp --enable-multibyte --prefix=/usr
make
make install

说明：
–with-features=huge：支持最大特性 
–enable-rubyinterp：启用Vim对ruby编写的插件的支持 
–enable-pythoninterp：启用Vim对python编写的插件的支持 
–enable-luainterp：启用Vim对lua编写的插件的支持 
–enable-perlinterp：启用Vim对perl编写的插件的支持 
–enable-multibyte：多字节支持 可以在Vim中输入中文 
–enable-cscope：Vim对cscope支持 
–enable-gui=gtk2：gtk2支持,也可以使用gnome，表示生成gvim 
–with-python-config-dir=/usr/lib/python2.7/config-i386-linux-gnu/ 指定 python 路径 
–prefix=/usr：编译安装路径
