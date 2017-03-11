# Bashisms

**A bunch of settings and config files that I always use upon new installs.**

--

Put in `~/.bash_aliases` or `~/.bashrc`
<pre>alias cp="cp -v" 
alias rm="rm -i" 
alias mv="mv -v" 
alias grep="grep --color=auto"
alias egrep="egrep --color=auto"</pre>

--

When `root`, change prompt color to red. Put this in `/root/.bashrc`
<pre># Set prompt color to red when root
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;31m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '</pre>

--

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

<h1>Debian GNOME</h1>

<h3>Change system font in Gnome:</h3>
Edit this file: `/usr/share/gnome-shell/theme/gnome-shell.css`
The value we are looking for is this:
<pre>/* default text style */
stage {
    font-family: <b>cantarell</b>, sans-serif;
    font-size: 11pt;
    color: white;
}</pre>

Change from `cantarell` to whatever font that is easier on the eyes.

<h2>Fix font issue(s) in Firefox:</h2>
(https://unix.stackexchange.com/a/226926)<br>
Add the below to `$HOME/.fonts.conf`:<br>

```xml
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
<fontconfig>
 <match target="font">
  <edit mode="assign" name="rgba">
   <const>rgb</const>
  </edit>
 </match>
 <match target="font">
  <edit mode="assign" name="hinting">
   <bool>true</bool>
  </edit>
 </match>
 <match target="font">
  <edit mode="assign" name="hintstyle">
   <const>hintslight</const>
  </edit>
 </match>
 <match target="font">
  <edit mode="assign" name="antialias">
   <bool>true</bool>
  </edit>
 </match>
  <match target="font">
  <edit mode="assign" name="lcdfilter">
    <const>lcddefault</const>
  </edit>
  </match>
</fontconfig>
```
<h2>Disable annoying sound events</h2>
Run `dconf-editor`<br />
Browse to:<br />
`org/gnome/desktop/sound`<br />
Untick **event-sounds**<br />
Done!
