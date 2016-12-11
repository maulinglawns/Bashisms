# Bashisms

**A bunch of settings and config files that I always use upon new installs.**

Put in `~/.bash_aliases` or `~/.bashrc`
<pre>alias cp="cp -v" 
alias rm="rm -i" 
alias mv="mv -v" 
alias grep="grep --color=auto"
alias egrep="egrep --color=auto"</pre>

When as root, change prompt color to red.i Put this in root's `.bashrc`
<pre># Set prompt color to red when root
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '</pre>

My `~/.vimrc`
<pre>" Make tabs four spaces
set shiftwidth=4
set tabstop=4
set expandtab

" Enable syntax coloring
syntax enable

" Show line numbers
set number

" Show which mode (not mood!) we're in
set showmode

" Show matching brackets
set showmatch</pre>

