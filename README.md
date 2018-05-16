# environment-config
Set up a new Mac OS

## VIM configuration

Clone the Vundle.vim repository:
```
git clone https://github.com/VundleVim/Vundle.vim.git
```

Set up Vundle:
```
git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
```

Add the following content to your $HOME/.vimrc file:

```
" vim:foldmethod=marker:foldlevel=0

" Plugins {{{
set nocompatible              " be iMproved, required
filetype off                  " required

set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

Plugin 'VundleVim/Vundle.vim'
Plugin 'scrooloose/syntastic'
Plugin 'scrooloose/nerdtree'
Plugin 'scrooloose/nerdcommenter'
Plugin 'rodjek/vim-puppet'
Plugin 'godlygeek/tabular'
Plugin 'honza/vim-snippets'
Plugin 'vim-scripts/bash-support.vim'
Plugin 'airblade/vim-gitgutter'
Plugin 'Shougo/neocomplete.vim'
Plugin 'garbas/vim-snipmate'
Plugin 'MarcWeber/vim-addon-mw-utils'
Plugin 'tomtom/tlib_vim'
Plugin 'aperezdc/vim-template'
Plugin 'kien/ctrlp.vim'
Plugin 'skywind3000/quickmenu.vim'
Plugin 'altercation/vim-colors-solarized'
Plugin 'Lokaltog/vim-powerline'
Plugin 'junegunn/fzf.vim'
Plugin 'sjl/gundo.vim'
Plugin 'Xuyuanp/nerdtree-git-plugin'
Plugin 'chr4/nginx.vim'
Plugin 'SirVer/ultisnips'
Plugin 'tpope/vim-fugitive'
Plugin 'lepture/vim-jinja'
Plugin 'elzr/vim-json'
Plugin 'vim-scripts/groovy.vim'
Plugin 'martinda/Jenkinsfile-vim-syntax'
Plugin 'tpope/vim-pathogen'

call vundle#end()
filetype plugin indent on
" }}}

" General config {{{

set ai
set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab
set smartindent
set cm=blowfish
set nu
set colorcolumn=80
set number
set showcmd
set cursorline
set wildmenu
set lazyredraw
set showmatch
syntax on
set guifont=Terminus
set mouse=a " use mouse everywhere
set scrolloff=10 " Keep 10 lines (top/bottom) for scope
" turn off auto adding comments on next line
" so you can cut and paste reliably
" http://vimdoc.sourceforge.net/htmldoc/change.html#fo-table
set fo=tcq
set nocompatible
set modeline

" Enable global clipboard
if has('mac')
  set clipboard=unnamed
else
  set clipboard=unnamedplus
endif

" force sudo write
cmap w!! w !sudo tee > /dev/null %
" }}}

" Search {{{
set incsearch           " search as characters are entered
set hlsearch            " highlight matches
" Clear highlighting on escape in normal mode
nnoremap <esc> :noh<return><esc>
nnoremap <esc>^[ <esc>^[
" }}}

" Tabs and buffers {{{

" Tabs
nnoremap ,t <Esc>:tabnew<CR>
nnoremap ,<Tab> :tabnext<CR>
nnoremap ,n :tabnext<CR>
nnoremap ,p :tabprevious<CR>
nnoremap ,1 1gt
nnoremap ,2 2gt
nnoremap ,3 3gt
nnoremap ,4 4gt
nnoremap ,5 5gt
nnoremap ,6 6gt
nnoremap ,7 7gt
nnoremap ,8 8gt
nnoremap ,9 9gt
nnoremap ,0 10gt

" Buffers
nnoremap ;; :Buffers<CR>
nnoremap ;1 :b 1<CR>
nnoremap ;2 :b 2<CR>
nnoremap ;3 :b 3<CR>
nnoremap ;4 :b 4<CR>
nnoremap ;5 :b 5<CR>
nnoremap ;6 :b 6<CR>
nnoremap ;7 :b 7<CR>
nnoremap ;8 :b 8<CR>
nnoremap ;9 :b 9<CR>
nnoremap ;0 :b 10<CR>
" }}}

" Folding {{{
set foldenable          " enable folding
set foldlevelstart=10   " open most folds by default
set foldnestmax=10      " 10 nested fold max
" space open/closes folds
nnoremap <space> za
set foldmethod=indent   " fold based on indent level
" }}}

" Mark bad syntax {{{

"highlight LiteralTabs ctermbg=darkgreen guibg=darkgreen
"autocmd ColorScheme * highlight LiteralTabs ctermbg=darkgreen guibg=darkgreen
"call matchadd('LiteralTabs', '\s\  ')

highlight ExtraWhitespace ctermbg=darkgreen guibg=darkgreen
autocmd ColorScheme * highlight ExtraWhitespace ctermbg=darkgreen guibg=darkgreen
call matchadd('ExtraWhitespace', '\s\+$')

highlight BadWhitespace ctermbg=darkgreen guibg=darkgreen
autocmd ColorScheme * highlight BadWhitespace ctermbg=darkgreen guibg=darkgreen
call matchadd('BadWhitespace', '^\t\+')
" }}}

" Specific languages config {{{

" Puppet {{{
au BufRead,BufNewFile *.pp
  \ set filetype=puppet
  au BufRead,BufNewFile *_spec.rb
    \ nmap <F8> :!rspec --color %<CR>
filetype plugin indent on " Enable indentation matching for =>'s
" }}}

" Python {{{
au BufRead,BufNewFile *.py,*pyw set shiftwidth=4
au BufRead,BufNewFile *.py,*pyw set tabstop=4
au BufRead,BufNewFile *.py,*.pyw set expandtab
autocmd FileType python setlocal commentstring=#\ %s
" }}}

" Makefile {{{
autocmd BufEnter Makefile setlocal noexpandtab
" }}}

" Ruby {{{
autocmd FileType ruby setlocal commentstring=#\ %s
" }}}

" }}}

" Plugin Pathogen {{{
execute pathogen#infect()
" }}}

" Plugin NERDTree {{{
map <C-n> :NERDTreeToggle<CR>
" }}}

" Plugin vim-json {{{
" Map z and r to reset folding
autocmd FileType json map zr :syn sync fromstart<CR>
autocmd FileType json set foldmethod=syntax
autocmd FileType json set foldlevel=100
let g:vim_json_syntax_conceal = 0
" }}}

" Plugin powerline {{{
set t_Co=256
set nocompatible   " Disable vi-compatibility
set laststatus=2   " Always show the statusline
set encoding=utf-8 " Necessary to show Unicode glyphs
set showtabline=2 " Always display the tabline, even if there is only one tab
set noshowmode " Hide the default mode text (e.g. -- INSERT -- below the statusline)
if has('mac')
  set rtp+=~/Library/Python/2.7/lib/python/site-packages/powerline/bindings/vim/
else
  set rtp+=~/.local/lib/python2.7/site-packages/powerline/bindings/vim/
endif
" }}}

" Plugin solarized {{{
syntax enable
set background=dark
let g:solarized_termcolors=256
colorscheme solarized
let g:Powerline_symbols = 'fancy'
" }}}

" Plugin syntastic {{{
let g:syntastic_check_on_open = 0
let g:syntastic_check_on_wq = 0
let g:syntastic_puppet_puppetlint_args = '--no-80chars-check'
let g:syntastic_python_checkers = ['flake8']
"let g:syntastic_error_symbol = 'âœ–ï¸Ž'
"let g:syntastic_warning_symbol = 'âœ–ï¸Ž'
"let g:syntastic_style_error_symbol = 'âž¡'
"let g:syntastic_style_warning_symbol = 'âž¡'
" }}}

" Plugin neocomplete {{{
" Disable AutoComplPop.
let g:acp_enableAtStartup = 0
" Use neocomplete.
let g:neocomplete#enable_at_startup = 1
" Use smartcase.
let g:neocomplete#enable_smart_case = 1
" Set minimum syntax keyword length.
let g:neocomplete#sources#syntax#min_keyword_length = 3
let g:neocomplete#lock_buffer_name_pattern = '\*ku\*'

" Define dictionary.
let g:neocomplete#sources#dictionary#dictionaries = {
    \ 'default' : '',
    \ 'vimshell' : $HOME.'/.vimshell_hist',
    \ 'scheme' : $HOME.'/.gosh_completions'
        \ }

" Define keyword.
if !exists('g:neocomplete#keyword_patterns')
    let g:neocomplete#keyword_patterns = {}
endif
let g:neocomplete#keyword_patterns['default'] = '\h\w*'

" Plugin key-mappings.
inoremap <expr><C-g>     neocomplete#undo_completion()
inoremap <expr><C-l>     neocomplete#complete_common_string()

" Recommended key-mappings.
" <CR>: close popup and save indent.
inoremap <silent> <CR> <C-r>=<SID>my_cr_function()<CR>
function! s:my_cr_function()
  "return neocomplete#close_popup() . "\<CR>"
  " For no inserting <CR> key.
  return pumvisible() ? neocomplete#close_popup() : "\<CR>"
endfunction
" <TAB>: completion.
"inoremap <expr><TAB>  pumvisible() ? "\<C-n>" : "\<TAB>"
" <C-h>, <BS>: close popup and delete backword char.
inoremap <expr><C-h> neocomplete#smart_close_popup()."\<C-h>"
inoremap <expr><BS> neocomplete#smart_close_popup()."\<C-h>"
inoremap <expr><C-y>  neocomplete#close_popup()
inoremap <expr><C-e>  neocomplete#cancel_popup()
" Close popup by <Space>.
"inoremap <expr><Space> pumvisible() ? neocomplete#close_popup() : "\<Space>"

" For cursor moving in insert mode(Not recommended)
"inoremap <expr><Left>  neocomplete#close_popup() . "\<Left>"
"inoremap <expr><Right> neocomplete#close_popup() . "\<Right>"
"inoremap <expr><Up>    neocomplete#close_popup() . "\<Up>"
"inoremap <expr><Down>  neocomplete#close_popup() . "\<Down>"
" Or set this.
"let g:neocomplete#enable_cursor_hold_i = 1
" Or set this.
"let g:neocomplete#enable_insert_char_pre = 1

" AutoComplPop like behavior.
"let g:neocomplete#enable_auto_select = 1

" Shell like behavior(not recommended).
"set completeopt+=longest
"let g:neocomplete#enable_auto_select = 1
"let g:neocomplete#disable_auto_complete = 1
"inoremap <expr><TAB>  pumvisible() ? "\<Down>" : "\<C-x>\<C-u>"

" Enable omni completion.
autocmd FileType css setlocal omnifunc=csscomplete#CompleteCSS
autocmd FileType html,markdown setlocal omnifunc=htmlcomplete#CompleteTags
autocmd FileType javascript setlocal omnifunc=javascriptcomplete#CompleteJS
autocmd FileType python setlocal omnifunc=pythoncomplete#Complete
autocmd FileType xml setlocal omnifunc=xmlcomplete#CompleteTags

" Enable heavy omni completion.
if !exists('g:neocomplete#sources#omni#input_patterns')
  let g:neocomplete#sources#omni#input_patterns = {}
endif
"let g:neocomplete#sources#omni#input_patterns.php = '[^. \t]->\h\w*\|\h\w*::'
"let g:neocomplete#sources#omni#input_patterns.c = '[^.[:digit:] *\t]\%(\.\|->\)'
"let g:neocomplete#sources#omni#input_patterns.cpp = '[^.[:digit:] *\t]\%(\.\|->\)\|\h\w*::'

" For perlomni.vim setting.
" https://github.com/c9s/perlomni.vim
let g:neocomplete#sources#omni#input_patterns.perl = '\h\w*->\h\w*\|\h\w*::'
" }}}

" Plugin Vim templates {{{
let g:email = 'fr3nd@fr3nd.net'
let g:username = 'Carles AmigÃ³'
" }}}

" Plugin Vim gitgutter {{{
highlight clear SignColumn
"let g:gitgutter_sign_added = 'âœš'
"let g:gitgutter_sign_modified = 'âžœ'
"let g:gitgutter_sign_removed = 'âœ˜'
" }}}

" Plugin gundo {{{
let g:gundo_prefer_python3 = 1
nnoremap <F5> :GundoToggle<CR>
" }}}

" Plugin nerdcommenter {{{
" configuring leader key to ,
let mapleader=","
set timeout timeoutlen=1500
" Allow commenting and inverting empty lines (useful when commenting a region)
let g:NERDCommentEmptyLines = 1
" Enable trimming of trailing whitespace when uncommenting
let g:NERDTrimTrailingWhitespace = 1
" Align line-wise comment delimiters flush left instead of following code indentation
let g:NERDDefaultAlign = 'left'
" }}}

" Plugin CtrlP {{{
" Making CtrlP search MUCH faster
let g:ctrlp_user_command = 'ag %s -l --nocolor -g ""'
let g:ctrlp_match_window = 'bottom,order:ttb'
let g:ctrlp_switch_buffer = 0
let g:ctrlp_working_path_mode = 0
" }}}

" Plugin FZF {{{

" <C-p> or <C-t> to search files
nnoremap <silent> <C-t> :FZF -m<cr>
"nnoremap <silent> <C-p> :FZF -m<cr>

" This is the default extra key bindings
let g:fzf_action = {
  \ 'ctrl-t': 'tab split',
  \ 'ctrl-x': 'split',
  \ 'ctrl-v': 'vsplit' }

" Default fzf layout
" - down / up / left / right
let g:fzf_layout = { 'down': '~40%' }

" In Neovim, you can set up fzf window using a Vim command
"let g:fzf_layout = { 'window': 'enew' }
"let g:fzf_layout = { 'window': '-tabnew' }

" Customize fzf colors to match your color scheme
let g:fzf_colors =
\ { 'fg':      ['fg', 'Normal'],
  \ 'bg':      ['bg', 'Normal'],
  \ 'hl':      ['fg', 'Comment'],
  \ 'fg+':     ['fg', 'CursorLine', 'CursorColumn', 'Normal'],
  \ 'bg+':     ['bg', 'CursorLine', 'CursorColumn'],
  \ 'hl+':     ['fg', 'Statement'],
  \ 'info':    ['fg', 'PreProc'],
  \ 'prompt':  ['fg', 'Conditional'],
  \ 'pointer': ['fg', 'Exception'],
  \ 'marker':  ['fg', 'Keyword'],
  \ 'spinner': ['fg', 'Label'],
  \ 'header':  ['fg', 'Comment'] }

" Enable per-command history.
" CTRL-N and CTRL-P will be automatically bound to next-history and
" previous-history instead of down and up. If you don't like the change,
" explicitly bind the keys to down and up in your $FZF_DEFAULT_OPTS.
"let g:fzf_history_dir = '~/.local/share/fzf-history'
" }}}

" Plugin Quickmenu {{{
"
" choose a favorite key to show/hide quickmenu
noremap <silent><F12> :call quickmenu#toggle(0)<cr>

" enable cursorline (L) and cmdline help (H)
let g:quickmenu_options = "HL"

" To add options:
" function quickmenu#append(text, action [, help = ''])

" new section: empty action with text starts with "#" represent a new section
call quickmenu#append("# Debug", '')

" script between %{ and } will be evaluated before menu open
call quickmenu#append("Run %{expand('%:t')}", '!./%', "Run current file")

" Gundo
call quickmenu#append("# Gundo", '')
call quickmenu#append("Undo tree", 'GundoToggle', "View undo tree")

" new section
call quickmenu#append("# Git", '')

" use fugitive to show diff
call quickmenu#append("git diff", 'Gvdiff', "use fugitive's Gvdiff on current document")
call quickmenu#append("git status", 'Gstatus', "use fugitive's Gstatus on current document")
call quickmenu#append("git blame", 'Gblame', "use fugitive's Gblame on current document")

" new section
call quickmenu#append("# Misc", '')
call quickmenu#append("Turn paste %{&paste? 'off':'on'}", "set paste!", "enable/disable paste mode (:set paste!)")
call quickmenu#append("Turn spell %{&spell? 'off':'on'}", "set spell!", "enable/disable spell check (:set spell!)")
call quickmenu#append("Buffers", 'Buffers', "Show list of buffers")

" }}}

" Plugin utilsnips {{{

" Trigger configuration. Do not use <tab> if you use https://github.com/Valloric/YouCompleteMe.
let g:UltiSnipsExpandTrigger="<tab>"
let g:UltiSnipsJumpForwardTrigger="<c-b>"
let g:UltiSnipsJumpBackwardTrigger="<c-z>"
" }}}
```

Then, open a file or simply type vim:
```
vim
```

And type:
```
:VundleInstall
```

It will download and install the VIM plugins.

## iTerm configuration

Install Oh My Zsh:
```
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
