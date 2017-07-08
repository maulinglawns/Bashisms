# Bashisms

**A bunch of settings and config files that I always use upon new installs.<br>
Plus some hacks/bug fixes**

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
set showmatch

" Disable auto-comments
autocmd FileType * setlocal formatoptions-=c formatoptions-=r formatoptions-=o
</pre>

<h1>Debian GNOME</h1>

<h3>Change system font in Gnome:</h3>

Edit `/usr/share/gnome-shell/theme/gnome-shell.css`
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

Add the below to `~/.fonts.conf`

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

Run `dconf-editor`

Browse to:

`org/gnome/desktop/sound`

Untick **event-sounds**

Done!


<h1>iwlwifi hacks</h1>
<pre>
magnus@debian-probook:~$ cat /etc/modprobe.d/iwlwifi.conf 
# Below line is to stop wifi disconnecting at random intervals
options iwlwifi 11n_disable=1
# Below line is to stop the d*mn wifi led from blinking whenever there is
# traffic over the wifi network!!!
options iwlwifi led_mode=1
</pre>


<h1>Debian Stretch</h1>
On older (~2010) laptops screen goes black and is completely unresponsive.

`journalctl` reports:

`drm:ironlake_irq_handler [i915]] *ERROR* CPU pipe A FIFO underrun` 

See this bug report: https://bugs.debian.org/cgi-bin/bugreport.cgi?bug=859639

My (and original bug reporter's, thanks Uwe!) solution/workaround is:
- Add this content to `/etc/X11/xorg.conf.d/20-intel.conf`:
```
Section "Device"
        Identifier      "Intel Graphics"
        Driver          "intel"
EndSection
```
- Reboot
