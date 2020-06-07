# vim-notes
#### vim 使用笔记

* 安装vim-plug插件管理器

* .vimrc 配置

```shell
" #################### Vim ###########################################
set t_Co=256 " necessary for AirlineTheme
set laststatus=2
set foldmethod=syntax
set statusline=%F%m%r%h
set tabstop=4
set relativenumber
set number
set fencs=utf-8,gbk
set cindent
set expandtab
set softtabstop=4
set showmatch
set smartcase
set autochdir
set autoread
set wildmenu
set wildmode=longest:list,full
set hlsearch
set tags=./.tags;,.tags
let mapleader = ';'

" set nocompatible              " be iMproved, required
" filetype off                  " required

" Specify a directory for plugins
" - For Neovim: stdpath('data') . '/plugged'
" - Avoid using standard Vim directory names like 'plugin'
call plug#begin('~/.vim/plugged')

" Make sure you use single quotes

Plug 'junegunn/vim-easy-align'

" let Vundle manage YouCompleteMe,auto complete word,goto definition
" or declaration
Plug 'ycm-core/YouCompleteMe'

" let Vundle manage airline,show status line at bottom and buffer at top of
" the window
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'

" let Vundle manage ctrlP,show status line at bottom and buffer at top of
" the window
Plug 'ctrlpvim/ctrlp.vim'

" let Vundle manage ctrlP,show status line at bottom and buffer at top of
" the window
Plug 'dyng/ctrlsf.vim'
"go 插件
Plug 'fatih/vim-go'

" vim-gutentags,manage ctags or gtags
Plug 'ludovicchabant/vim-gutentags'
Plug 'skywind3000/gutentags_plus'
" Shorthand notation; fetches https://github.com/junegunn/vim-easy-align
" Plug 'junegunn/vim-easy-align'

" Any valid git URL is allowed
" Plug 'https://github.com/junegunn/vim-github-dashboard.git'

" Multiple Plug commands can be written in a single line using | separators
" Plug 'SirVer/ultisnips' | Plug 'honza/vim-snippets'

" On-demand loading
" Plug 'scrooloose/nerdtree', { 'on':  'NERDTreeToggle' }
" Plug 'tpope/vim-fireplace', { 'for': 'clojure' }

" Using a non-master branch
" Plug 'rdnetto/YCM-Generator', { 'branch': 'stable' }

" Using a tagged release; wildcard allowed (requires git 1.9.2 or above)
" Plug 'fatih/vim-go', { 'tag': '*' }

" Plugin options
" Plug 'nsf/gocode', { 'tag': 'v.20150303', 'rtp': 'vim' }

" Plugin outside ~/.vim/plugged with post-update hook
" Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }

" Unmanaged plugin (manually installed and updated)
" Plug '~/my-prototype-plugin'

" Initialize plugin system
call plug#end()

" Put your non-Plugin stuff after this line

" #################### YouCompleteMe ################################
let g:ycm_server_python_interpreter='/usr/bin/python'
let g:ycm_global_ycm_extra_conf='~/.vim/.ycm_extra_conf.py'
let g:ycm_show_diagnostics_ui = 0                  "关闭语法提示
let g:ycm_complete_in_comments=1                   " 补全功能在注释中同样有效
let g:ycm_confirm_extra_conf=0                     " 允许 vim 加载 .ycm_extra_conf.py 文件，不再提示
let g:ycm_collect_identifiers_from_tags_files=1    " 开启 YCM 标签补全引擎
let g:ycm_min_num_of_chars_for_completion=1        " 从第一个键入字符就开始罗列匹配项
let g:ycm_cache_omnifunc=0                         " 禁止缓存匹配项，每次都重新生成匹配项
let g:ycm_seed_identifiers_with_syntax=1           " 语法关键字补全
" let g:ycm_goto_buffer_command = 'horizontal-split' " 跳转打开上下分屏
map <F12> :YcmCompleter GoToDefinitionElseDeclaration<CR>


" #################### Airline ######################################
" 使用powerline打过补丁的字体
" let g:airline_powerline_fonts = 1
" 开启tabline
let g:airline#extensions#tabline#enabled = 1
let g:airline#extensions#tabline#formatter = 'unique_tail'
let g:airline#extensions#default#layout = [ [ 'a', 'b', 'c' ], [ 'x', 'y', 'z', 'error' ] ]
" let g:airline#extensions#default#layout = [ [ 'a' ], [ 'error', 'warning' ] ]
" tabline中当前buffer两端的分隔字符
let g:airline#extensions#tabline#left_sep = ' '
" tabline中未激活buffer两端的分隔字符
let g:airline#extensions#tabline#left_alt_sep = ' '
" tabline中buffer显示编号
" let g:airline#extensions#tabline#buffer_nr_show = 1
let g:airline_theme='bubblegum'

" #################### CtrlP ################################
let g:ctrlp_map = '<c-p>'
" let g:ctrlp_map = '<leader>f'
let g:ctrlp_cmd = 'CtrlPMixed'
"let g:ctrlp_user_command = 'find %s -type f'        "指定一个用于列出文件的外部工具
let g:ctrlp_working_path_mode = 'ra'
let g:ctrlp_user_command = ['.git', 'cd %s && git ls-files -co --exclude-standard']
let g:ctrlp_custom_ignore = '\v[\/]\.(git|hg|svn)$'
let g:ctrlp_custom_ignore = {
    \ 'dir':  '\v[\/]\.(git|hg|svn)$',
    \ 'file': '\v\.(exe|so|dll)$',
    \ 'link': 'SOME_BAD_SYMBOLIC_LINKS',
    \ }


" #################### CtrlSF ################################
let g:ctrlsf_ackprg='ag'
" nnoremap <leader>f :CtrlSF
let g:ctrlsf_ignore_dir=[".git", ".svn"]
let g:ctrlsf_search_mode = 'async'
" let g:ctrlsf_mapping = '<leader>w'
" nnoremap <F10> :CtrlSF<space><CR>
nnoremap <Leader>w :CtrlSF<space><CR>
" let g:ctrlsf_cmd = 'CtrlSF'
let g:ctrlsf_default_root = 'project'
let g:ctrlsf_context = '-B 1 -A 1'
let g:ctrlsf_default_view_mode = 'compact'

" #################### gutentags ##############################
" gutentags 搜索工程目录的标志，当前文件路径向上递归直到碰到这些文件/目录名
let g:gutentags_project_root = ['.root', '.svn', '.git', '.hg', '.project']
" 所生成的数据文件的名称
let g:gutentags_ctags_tagfile = '.tags'
" 同时开启 ctags 和 gtags 支持：
let g:gutentags_modules = []
if executable('ctags')
        let g:gutentags_modules += ['ctags']
endif
if executable('gtags-cscope') && executable('gtags')
        let g:gutentags_modules += ['gtags_cscope']
endif
" 将自动生成的 ctags/gtags 文件全部放入 ~/.cache/tags 目录中，避免污染工程目录
let g:gutentags_cache_dir = expand('~/.cache/tags')
" 配置 ctags 的参数，老的 Exuberant-ctags 不能有 --extra=+q，注意
let g:gutentags_ctags_extra_args = ['--fields=+niazS', '--extra=+q']
let g:gutentags_ctags_extra_args += ['--c++-kinds=+px']
let g:gutentags_ctags_extra_args += ['--c-kinds=+px']
" 如果使用 universal ctags 需要增加下面一行，老的 Exuberant-ctags 不能加下一行
let g:gutentags_ctags_extra_args += ['--output-format=e-ctags']
" 禁用 gutentags 自动加载 gtags 数据库的行为
let g:gutentags_auto_add_gtags_cscope = 0

" #################### gutentags_plus #########################
" enable gtags module
let g:gutentags_modules = ['ctags', 'gtags_cscope']

" config project root markers.
let g:gutentags_project_root = ['.root']

" generate datebases in my cache directory, prevent gtags files polluting my project
let g:gutentags_cache_dir = expand('~/.cache/tags')

" change focus to quickfix window after search (optional).
let g:gutentags_plus_switch = 1
```

* 常用命令

1. 打开vim
2. `:PlugInstall` 安装插件 
3. `:PlugStatus` 查看插件状态
4. `:PlugList` 列出所有插件
5. `:set mouse=a` 鼠标操作

6. 光标移动：

   1. ctrl+w+(小写的 hjkl), "非线性"的跳转的: ctrl_w+t(top : 左上角, +b: bottom, 右下角), p: preview: 上一个子窗口. 

7. 窗口本身的位值的移动:：

   1. ctrl_w + r: 窗口本身, 不是鼠标指针顺时针 (向下, 向右 移动), R : 则是逆时针反方向(向上, 向左)移动.

      ctrl_w+x: 左右上下对应位置的窗口 对调. 要注意窗口必须是 对应的, 如果不对应将无法对换, 比如左边一个大窗口, 右边有两个小的 子窗口, 则左右不能互换.