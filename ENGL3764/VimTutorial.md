# Vim Tutorial: Composition <!--- Name in progress -->

<!---
Guide Starts with installing a plugin manager.
Provide useful plugins
explain text objects
-->

Vim is an extraordinarily powerful text editor despite its famously difficult
learning curve. Once you have an understanding of navigation, editing, and basic
regular expressions however, the editor begins to feel more natural and you can
perform many tasks with ease. To get the most out of Vim however, one must
master the concept of command composition. Once a user has mastered these
features they become capable of performing most any task with the minimal amount
of motion necessary.

## Configuration and Plugins

Before beginning, the examples in this tutorial will use the plugins and options
below. These features are extraordinarily useful and are enabled in many
proficient Vim users .vimrc files in one variation or another. To install these
plugins, use a plugin manager such as
[Plug](https://github.com/junegunn/vim-plug),
[Pathogen](https://github.com/tpope/vim-pathogen), or
[Vundle](https://github.com/VundleVim/Vundle.vim).

### Enabled Options

'''
" Show Line Numbers on the side 
set number 

" Show last command keystroke in the bottom right of the statusline.
set showcmd

" Highlight successful search matches
set hlsearch

" Update search matches as you type
set incsearch

" Bind a single spacebar keystroke to clear search highlighting in normal mode 
nnoremap <silent> <Space> :nohlsearch<Bar>:echo<CR>
'''

### Plugins
Plug 'tpope/vim-surround'
Plug 'tpope/vim-repeat'
Plug 'tpope/vim-abolish'
Plug 'tpope/vim-commentary'
Plug 'christoomey/vim-titlecase'
Plug 'christoomey/vim-sort-motion'
Plug 'godlygeek/tabular'

-
-
-
-

<!--- :%s/\s\+$// -->
<!--- :%s/\t/    /g -->
<!--- record with q, q to stop, @reg to play, <C-r>reg to insert commands -->
<!--- 
