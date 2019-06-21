% Vim ++

Vim, short for Vi Improved, is one of the most popular command line text editor out in the world of Free and Open-Source Softwares. It's manual describes it as "vim - Vi IMproved, a programmer's text editor", and it surely is. A lot of people use it and they have their own reasons for choosing vim. While some are still using it just because they don't know how to exit after entering once, others have a more genuine reason. But if you ask any Vimmer (a word I just invented), you will surely hear this as one of the reasons: "Its very configurable". And that's exactly what we will do today. We are going to enhance our favourite text editor to make it literally vim++.

There are two way of improving vi improved:

## The Vimrc file

While you can set your preferences for each vim instance by using the commands ([top 50](https://www.shortcutfoo.com/blog/top-50-vim-configuration-options/) because there is literally no end to them), but the moment you open the next file in vim, every thing will be new and at factory reset. So how do you permanently save your preferences? Enter the [vimrc](https://vim.fandom.com/wiki/Open_vimrc_file) file. For every linux user, there is a vim configuration file in your home folder normally. Its hidden so you normally don't see it. But doing a ``ls -a | grep vim`` should reveal the file.

In that file, you put your prefrences and the key shortcuts that you want to use. As an example, here is one of the most common prefences that people use and that I have used too:

	set number	" see numbers of the line

So putting the above line in your vimrc file will make vim to show the line numbers. Now there are thousands of commands and preferences that you can use or set, so I am not going to discuss them over here. You can find some useful preferences on [this blog](https://spf13.com/post/perfect-vimrc-vim-config-file/), [this website](https://vimrcfu.com/) and this [this series of articles](https://gunpreetahuja.wordpress.com/2014/05/30/all-i-got-to-know-about-vim-1/). But hey, here is what I use, my vimrc:

	set spell spelllang=en_us	"Set spell-check to english us
	
	set spellfile=$HOME/vim/spell/en.utf-8.add	"Add spelling file
	" set ai
	set number	"Set line number
	
	set incsearch	"Highlight expressions
	set ignorecase	"Ignore case in searches
	set smartcase	"Make case-sensitive when all is caps
	set hlsearch	"Highlight searches
	nmap \q :nohlsearch<CR>		"Speacial key combination to undo highlight search
	nmap \e :NERDTreeToggle<CR>	"Key combination to toggle NERDTree
	
	set statusline+=%#warningmsg#	"Add warning messages in status line
	set statusline+=%{SyntasticStatuslineFlag()}	"Set Syntastic Status line flag
	set statusline+=%*
	let g:syntastic_always_populate_loc_list = 1
	let g:syntastic_auto_loc_list = 1
	let g:syntastic_check_on_open = 1
	let g:syntastic_check_on_wq = 0
	
	set nocompatible   " Disable vi-compatibility
	set laststatus=2   " Always show the statusline
	set encoding=utf-8 " Necessary to show Unicode glyphs
	
	execute pathogen#infect()	"Enable pathogen
	syntax on
	filetype plugin indent on
	autocmd BufWritePost *.py call flake8#Flake8()	"Enable flake 8 on saving python file

## The Plugins

Now my vimrc is not meant to work alone. It can but it's not meant to. My vimrc has some lines that are meant to support some plugins. Plugins as you know, are additional features that really enhance the vim. So let's have a look at one that I use and love:

1. [Pathogen](https://github.com/tpope/vim-pathogen): From its github description "pathogen.vim makes it super easy to install plugins and runtime files in their own private directories." And well, that's exactly what it does. Its a plugin that helps installing other plugins. After you have pathogen, you can just ``git clone`` the other plugins in ``~/.vim/bundle``.

2. [Fugitive](https://github.com/tpope/vim-fugitive): Another one from the [developer of Pathogen](https://github.com/tpope), this one is a killer. "A Git wrapper so awesome, it should be illegal". If you are an addict of [git](https://hacksd.wordpress.com/2019/02/28/using-git/) and vim, this right here is your drug. It just elegantly merges vim and git together. I personally love it.

3. [YouCompleteMe](https://github.com/Valloric/YouCompleteMe): A code-completion engine for Vim. This is what most developers would like to have in their vim. Now your vim is upgraded to an IDE.

4. [Syntastic](https://github.com/vim-syntastic/syntastic): Another developer friendly tool, this is a syntax checking tool that helps you  to write correct and proper code.

5. [Vim-Flake8](https://github.com/nvie/vim-flake8): Love python and its coding standards? Well here is the too to help you write the best python code. Currently syntastic and flake8 overlap in my system, but I will soon disable syntastic for python because I prefer flake8.

6. [NERDTree](https://github.com/scrooloose/nerdtree): This plugin lets to open a tree explorer of your current directory. Another step closer to getting your own IDE in the terminal. You can open the explorer with :Explore command in vim, but this one is seriously better.

7. [Powerline](https://github.com/Lokaltog/vim-powerline): And who doesn't like a good looking vim. Though deprecated, this plugin greatly enhances your status line and makes it a lot more informative.

Now these are just some of the plugins that I have explored and use currently. There are loads of them out there for you to enjoy!!!

## Extras

Just some extra stuff to makes your vim experience much more rewarding:

- Tabs: Yes, you heard it right! Vim has tabs and why not. Just run ``:tabe <filename>`` to open file in another tab and then navigate with ``:tabn`` and ``:tabp``. The best part is that tabs let you seamlessly copy and move info amongst various files in the same terminal.

- Window split: While tabs are more useful, sometimes you may just want to split the window so here you go. ``:split filename`` to split window horizontally and ``:vsplit file`` for vertical split. Use ``ctrl-w ctrl-w`` to navigate.

- Auto-correction: If you are using spellcheck, then reach the miss-spelled word by ``]s`` (forward) or ``[s`` (backward) and when on the word, press ``z=`` to get a list of possible correction.
Fun fact: I used auto-correction to auto-correct the Auto-Correction.

- Copy to graphic clipboard: Install vim-gnome in ubuntu  using ``sudo apt install vim-gnome`` and press ``"+y`` to copy selected content to the graphical clipboard to paste  it anywhere. ``"+p`` also pastes the copied content in vim.

So these are all that I currently use to enhance my vim. If in future I discover anything new, I will update here. 
And while I exit from here, think you can exit from vim? Well think again after reading [this](https://stackoverflow.blog/2017/05/23/stack-overflow-helping-one-million-developers-exit-vim/)

![](http://devhumor.com/content/uploads/images/May2017/exit-vim-2.jpg)

