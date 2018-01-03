# vim
**Ubuntu vim安装、配置指南**

## vim源码编译
编译Vim之前，需要下载编译的相关工具和一些库

	sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev libgtk2.0-dev libatk1.0-dev libbonoboui2-dev libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev ruby-dev mercurial
	git clone git@github.com:vim/vim.git
	cd vim/
	./configure --with-features=huge --enable-rubyinterp --enable-pythoninterp --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu/ --enable-perlinterp --enable-gui=gtk2 --enable-cscope --enable-luainterp --enable-perlinterp --enable-multibyte --prefix=/usr
	make
	make install

说明：

1. –with-features=huge：支持最大特性 
1. –enable-rubyinterp：启用Vim对ruby编写的插件的支持 
1. –enable-pythoninterp：启用Vim对python编写的插件的支持 
1. –enable-luainterp：启用Vim对lua编写的插件的支持 
1. –enable-perlinterp：启用Vim对perl编写的插件的支持 
1. –enable-multibyte：多字节支持 可以在Vim中输入中文 
1. –enable-cscope：Vim对cscope支持 
1. –enable-gui=gtk2：gtk2支持,也可以使用gnome，表示生成gvim 
1. –with-python-config-dir=/usr/lib/python2.7/config-i386-linux-gnu/ 指定 python 路径 
1. –prefix=/usr：编译安装路径

## 插件管理
vundle 会接管 .vim/ 下的所有原生目录

	git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

## .vimrc文件配置


	"===========================
	" 设置leader为;
	"===========================
	let mapleader=";"
	let maplocalleader=";" 

	"===========================
	" vim系统环境
	"===========================
	" 让配置变更立即生效
	autocmd BufWritePost $MYVIMRC source $MYVIMRC

	set nocompatible              " 去除VI一致性,必须

	" 打开文件类型的检测
	" 为特定的文件类型允许插件文件的载入
	" 为特定的文件类型载入缩进文件
	filetype plugin indent on

	"===========================
	" 编码格式
	"===========================
	set encoding=utf-8
	set termencoding=utf-8
	set fileencoding=utf-8
	set fileencodings=ucs-bom,utf-8,chinese,cp936

	"===========================
	" 文本编辑
	"===========================
	" 配色方案
	colorscheme desert

	set tabstop=4		"设置tab的跳数
	set expandtab
	set backspace=2 	"设置退格键可用
	"set nu! 		"设置显示行号
	set wrap 		"设置自动换行
	"set nowrap 		"设置不自动换行
	set linebreak 		"整词换行，与自动换行搭配使用
	"set list 		"显示制表符
	set autochdir 		"自动设置当前目录为正在编辑的目录
	set hidden 		"自动隐藏没有保存的缓冲区，切换buffer时不给出保存当前buffer的提示
	set scrolloff=5 	"在光标接近底端或顶端时，自动下滚或上滚
	"Toggle Menu and Toolbar 	"隐藏菜单栏和工具栏
	"set guioptions-=m
	"set guioptions-=T
	set showtabline=2 	"设置显是显示标签栏
	set autoread 		"设置当文件在外部被修改，自动更新该文件
	set mouse=a 		"设置在任何模式下鼠标都可用
	set nobackup 		"设置不生成备份文件
	"set go=				"不要图形按钮
	set guioptions-=T           " 隐藏工具栏
	"set guioptions-=m           " 隐藏菜单栏

	map <F11> <Esc>:call libcallnr("gvimfullscreen.dll", "ToggleFullScreen", 0)<CR>

	" 查找/替换相关的设置
	set hlsearch "高亮显示查找结果
	set incsearch "增量查找
	" 全文搜索选中的文字
	nnoremap <silent> <Leader>f y/<c-r>=escape(@", "\\/.*$^~[]")<cr><cr>
	nnoremap <silent> <Leader>F y?<c-r>=escape(@", "\\/.*$^~[]")<cr><cr>
	" 普通模式下 Shift+W 切换自动换行
	nnoremap <s-w> :exe &wrap==1 ? 'set nowrap' : 'set wrap'<cr>
	" 普通模式下 Ctrl+c 复制文件路径
	nnoremap <c-c> :let @* = expand('%:p')<cr>

	"===========================
	"代码设置
	"===========================
	syntax enable "打开语法高亮
	syntax on "打开语法高亮
	set showmatch "设置匹配模式，相当于括号匹配
	set smartindent "智能对齐
	set shiftwidth=4 "换行时，交错使用4个空格
	set autoindent "设置自动对齐
	set ai! "设置自动缩进
	" set cursorcolumn "启用光标列
	set cursorline	"启用光标行
	set guicursor+=a:blinkon0 "设置光标不闪烁
	" set fdm=indent "设置成marker折叠方式
	set colorcolumn=100
	
	" Style
	set number   " 显示行号
	set wildmenu " 开启命令行补全
	" set nocursorline  " 不突出显示当前行
	" set shortmess=atl  "启动时不显示 捐赠提示
	set helplang=cn
	
	" Display extra whitespace
	set list listchars=tab:\|\ ,trail:.,extends:>,precedes:<
	
	" Tab
	set softtabstop=4 " 设置按BackSpace的时候可以一次删除掉4个空格
	"set smarttab
	
	" 定义快捷键到行首和行尾
	nmap LB 0
	nmap LE $
	" 设置快捷键将选中文本块复制至系统剪贴板
	vnoremap <Leader>y "+y
	" 设置快捷键将系统剪贴板内容粘贴至 vim
	nmap <Leader>p "+p
	" 定义快捷键关闭当前分割窗口
	nmap <Leader>q :q<CR>
	" 定义快捷键保存当前窗口内容
	nmap <Leader>w :w<CR>
	" 定义快捷键保存所有窗口内容并退出 vim
	nmap <Leader>WQ :wa<CR>:q<CR>
	" 不做任何保存，直接退出 vim
	nmap <Leader>Q :qa!<CR>
	" 依次遍历子窗口
	nnoremap nw <C-W><C-W>
	" 跳转至右方的窗口
	nnoremap <Leader>lw <C-W>l
	" 跳转至左方的窗口
	nnoremap <Leader>hw <C-W>h
	" 跳转至上方的子窗口
	nnoremap <Leader>kw <C-W>k
	" 跳转至下方的子窗口
	nnoremap <Leader>jw <C-W>j
	" 定义快捷键在结对符之间跳转
	nmap <Leader>M %

	" <F4> 格式化文件
	map <F4> :call FormatFile()<CR>
	"map <leader>d :call FormatFile()<CR>
	func! FormatFile()
	:%retab!
	:set encoding=utf-8
	:%s/\s\+$//
	:set ff=unix
	endfunc
	
	" 替换函数。参数说明：
	" confirm：是否替换前逐一确认
	" wholeword：是否整词匹配
	" replace：被替换字符串
	function! Replace(confirm, wholeword, replace)
	    wa
	    let flag = ''
	    if a:confirm
	        let flag .= 'gec'
	    else
	        let flag .= 'ge'
	    endif
	    let search = ''
	    if a:wholeword
	        let search .= '\<' . escape(expand('<cword>'), '/\.*$^~[') . '\>'
	    else
	        let search .= expand('<cword>')
	    endif
	    let replace = escape(a:replace, '/\&~')
	    execute '%s/' . search . '/' . replace . '/' . flag . '| update'
	endfunction
	" 不确认、非整词
	nnoremap <Leader>R :call Replace(0, 0, input('Replace '.expand('<cword>').' with: '))<CR>
	" 不确认、整词
	nnoremap <Leader>rw :call Replace(0, 1, input('Replace '.expand('<cword>').' with: '))<CR>
	" 确认、非整词
	nnoremap <Leader>rc :call Replace(1, 0, input('Replace '.expand('<cword>').' with: '))<CR>
	" 确认、整词
	nnoremap <Leader>rcw :call Replace(1, 1, input('Replace '.expand('<cword>').' with: '))<CR>
	nnoremap <Leader>rwc :call Replace(1, 1, input('Replace '.expand('<cword>').' with: '))<CR>

	" vundle 环境设置
	set rtp+=~/.vim/bundle/Vundle.vim
	" vundle 管理的插件列表必须位于 vundle#begin() 和 vundle#end() 之间
	call vundle#begin()
	Plugin 'VundleVim/Vundle.vim'
	Plugin 'altercation/vim-colors-solarized'
	Plugin 'tomasr/molokai'
	Plugin 'vim-scripts/phd'
	Plugin 'Mark'
	Plugin 'Lokaltog/vim-powerline'
	Plugin 'scrooloose/nerdtree'
	Plugin 'fholgado/minibufexpl.vim'
	Plugin 'Valloric/YouCompleteMe'
	Plugin 'majutsushi/tagbar'
	Plugin 'vim-scripts/indexer.tar.gz'
	Plugin 'vim-scripts/DfrankUtil'
	Plugin 'vim-scripts/vimprj'
	Plugin 'ctrlpvim/ctrlp.vim'
	Plugin 'dyng/ctrlsf.vim'
	" 插件列表结束
	call vundle#end()

	" {{{ Mark 给各种tags标记不同的颜色，便于观看调式的插件。
	" 在运行source后Mark会被覆盖
	hi MarkWord1  ctermbg=Cyan     ctermfg=Black  guibg=#8CCBEA    guifg=Black
	hi MarkWord2  ctermbg=Green    ctermfg=Black  guibg=#A4E57E    guifg=Black
	hi MarkWord3  ctermbg=Yellow   ctermfg=Black  guibg=#FFDB72    guifg=Black
	hi MarkWord4  ctermbg=Red      ctermfg=Black  guibg=#FF7272    guifg=Black
	hi MarkWord5  ctermbg=Magenta  ctermfg=Black  guibg=#FFB3FF    guifg=Black
	hi MarkWord6  ctermbg=Blue     ctermfg=Black  guibg=#9999FF    guifg=Black
	
	nmap <silent> <Leader>hl <plug>MarkSet
	vmap <silent> <Leader>hl <plug>MarkSet
	nmap <silent> <Leader>hh <plug>MarkClear
	nmap <silent> <Leader>hr <plug>MarkRegex
	vmap <silent> <Leader>hr <plug>MarkRegex
	" }}}

	" 设置状态栏主题风格
	let g:Powerline_colorscheme='solarized256'
	set guifont=PowerlineSymbols\ for\ Powerline
	let g:Powerline_symbols = 'fancy'

	" 使用 NERDTree 插件查看工程文件。设置快捷键，速记：file list
	nmap <Leader>fl :NERDTreeToggle<CR>
	" 设置NERDTree子窗口宽度
	let NERDTreeWinSize=32
	" 设置NERDTree子窗口位置
	let NERDTreeWinPos="right"
	" 显示隐藏文件
	let NERDTreeShowHidden=0
	" NERDTree 子窗口中不显示冗余帮助信息
	let NERDTreeMinimalUI=1
	" 删除文件时自动删除文件对应 buffer
	let NERDTreeAutoDeleteBuffer=1
	
	" 显示/隐藏 MiniBufExplorer 窗口
	map <Leader>bl :MBEToggle<cr>
	" buffer 切换快捷键
	map <C-Tab> :MBEbn<cr>
	map <C-S-Tab> :MBEbp<cr>

	" 设置 tagbar 子窗口的位置出现在主编辑区的左边 
	let tagbar_left=1 
	" 设置显示／隐藏标签列表子窗口的快捷键。速记：identifier list by tag
	nnoremap <F8> :TagbarToggle<CR> 
	" 设置标签子窗口的宽度 
	let tagbar_width=32 
	" tagbar 子窗口中不显示冗余帮助信息 
	let g:tagbar_compact=1
	" 设置 ctags 对哪些代码标识符生成标签
	let g:tagbar_type_cpp = {
	    \ 'ctagstype' : 'c',
	    \ 'kinds' : [
	         \ 'c:classes:0:1',
	         \ 'd:macros:0:1',
	         \ 'e:enumerators:0:0', 
	         \ 'f:functions:0:1',
	         \ 'g:enumeration:0:1',
	         \ 'l:local:0:1',
	         \ 'm:members:0:1',
	         \ 'n:namespaces:0:1',
	         \ 'p:functions_prototypes:0:1',
	         \ 's:structs:0:1',
	         \ 't:typedefs:0:1',
	         \ 'u:unions:0:1',
	         \ 'v:global:0:1',
	         \ 'x:external:0:1'
	     \ ],
	     \ 'sro'        : '::',
	     \ 'kind2scope' : {
	         \ 'g' : 'enum',
	         \ 'n' : 'namespace',
	         \ 'c' : 'class',
	         \ 's' : 'struct',
	         \ 'u' : 'union'
	     \ },
	     \ 'scope2kind' : {
	         \ 'enum'      : 'g',
	         \ 'namespace' : 'n',
	         \ 'class'     : 'c',
	         \ 'struct'    : 's',
	         \ 'union'     : 'u'
	     \ }
	     \ }

	" << ctrlp
	let g:ctrlp_map = '<Leader>p'
	let g:ctrlp_cmd = 'CtrlP'
	"<Leader>f搜索MRU文件
	nmap <Leader>pf :CtrlPMRUFiles<CR>
	"<Leader>b显示缓冲区文件，并可通过序号进行跳转
	nmap <Leader>pb :CtrlPBuffer<CR>
	set wildignore+=*/tmp/*,*.so,*.swp,*.zip,*.d,*.o,*.txt,*/build/*,*~
	let g:ctrlp_custom_ignore = {
	    \ 'dir':  '\v[\/]\.(git|hg|svn|rvm)$',
	    \ 'file': '\v\.(exe|so|dll|zip|tar|tar.gz|pyc)$',
	    \ }
	let g:ctrlp_working_path_mode=0
	let g:ctrlp_match_window_bottom=1
	let g:ctrlp_max_height=15
	let g:ctrlp_match_window_reversed=0
	let g:ctrlp_mruf_max=500
	let g:ctrlp_follow_symlinks=1
	" <<

	" 设置插件 indexer 调用 ctags 的参数
	" 默认 --c++-kinds=+p+l，重新设置为 --c++-kinds=+p+l+x+c+d+e+f+g+m+n+s+t+u+v
	" 默认 --fields=+iaS 不满足 YCM 要求，需改为 --fields=+iaSl
	let g:indexer_ctagsCommandLineOptions="--c++-kinds=+p+l+x+c+d+e+f+g+m+n+s+t+u+v --fields=+iaSl --extra=+q"

	" YCM 补全菜单配色
	" 菜单
	highlight Pmenu ctermfg=2 ctermbg=3 guifg=#005f87 guibg=#EEE8D5
	" 选中项
	highlight PmenuSel ctermfg=2 ctermbg=3 guifg=#AFD700 guibg=#106900
	" 补全功能在注释中同样有效
	let g:ycm_complete_in_comments=0
	" 允许 vim 加载 .ycm_extra_conf.py 文件，不再提示
	let g:ycm_confirm_extra_conf=0
	" 开启 YCM 标签补全引擎
	let g:ycm_collect_identifiers_from_tags_files=1
	" 引入 C++ 标准库tags
	"set tags+=/data/misc/software/misc./vim/stdcpp.tags
	" YCM 集成 OmniCppComplete 补全引擎，设置其快捷键
	"inoremap <leader>; <C-x><C-o>
	" 补全内容不以分割子窗口形式出现，只显示补全列表
	set completeopt-=preview
	" 从第一个键入字符就开始罗列匹配项
	let g:ycm_min_num_of_chars_for_completion=2
	" 禁止缓存匹配项，每次都重新生成匹配项
	let g:ycm_cache_omnifunc=0
	" 语法关键字补全          
	let g:ycm_seed_identifiers_with_syntax=0
	" 开启 YCM 标签引擎
	let g:ycm_collect_identifiers_from_tags_files=1
	nnoremap <leader>jc :YcmCompleter GoToDeclaration<CR>
	" 只能是 #include 或已打开的文件
	nnoremap <leader>jd :YcmCompleter GoToDefinition<CR>
	" 重新编译
	nnoremap <F5> :YcmForceCompileAndDiagnostics<CR>
	
	" 使用 ctrlsf.vim
	" 插件在工程内全局查找光标所在关键字，设置快捷键。快捷键速记法：search in project
	nnoremap <Leader>sp :CtrlSF<CR>




