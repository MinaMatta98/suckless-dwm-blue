# Suckless-dwm-blue
This repo features a pre-patched version of the suckless desktop window manager - dwm. Dwm is lightweight and written in (you wont believe it) ... C . This makes it extremely lightweight and responsive, which is made especially clear when you contrast the dwm top bar to something like polybar. While polybar is a good bar extension it compartively is cripplingly slow.

You can find the unpatched dwm window manager in the following link: https://dwm.suckless.org/ 

The suckless dwm window manager is known to be difficult to patch. Users are generally capable of integrating a few patches with ease, however, the patches may be difficult to merge and would sometimes conflict each other. Note that I am no expert in C code and am open to criticism.

**This is a patch of dwm featuring mainly barpadding, colorbar, fullgaps, hide vacant tags, status2d, systray and winicon patches.**

**All credit for the desktop background go to u/baron-digit**

Here is a demonstration of the display manager's "desktop environment":

# Dwm with Alacritty, Zsh and Powerlevel10k
![Arch-Desktop](/Images/Screenshot-1.png)
# Dwm demonstrating the master-stack tile layout
![Arch-Desktop](/Images/Screenshot-2.png)
# Dwm with dmenu as a launch helper
![Arch-Desktop](/Images/Screenshot-3.png)
# Dwm top bar with systray, dwmblocks, winicons and hidden vacant tags
![Arch-Desktop](/Images/Screenshot-4.png)
# Dwm with lf as the file manager
![Arch-Desktop](/Images/Screenshot-5.png)

# Directory
Due to the size of this project, the installation will be split amongst multiple sections:
* dwm
* dwmblocks-async & dwmblocks-scripts
* dmenu & dmenu-scripts
* lightdm
* grub
* picom
* alacritty
* zsh

# Dwm Installation
The dwm install, while needing quite a bit of tuning to get working does actually feature other people's patches. This installation features the integration of the following patches:

* dwm-activetagindicatorbar-6.2: https://dwm.suckless.org/patches/activetagindicatorbar/
* dwm-actualfullscreen-20211013-cb3f58a: https://dwm.suckless.org/patches/actualfullscreen/
* dwm-autostart-20210120-cb3f58a: https://dwm.suckless.org/patches/autostart/
* dwm-bar-height-6.2: https://dwm.suckless.org/patches/bar_height/
* dwm-barpadding-20211020-a786211: https://dwm.suckless.org/patches/barpadding/
* dwm-centeredmaster-6.1: https://dwm.suckless.org/patches/centeredmaster/
* dwm-colorbar-6.2: https://dwm.suckless.org/patches/colorbar/
* dwm-fullgaps-6.2: https://dwm.suckless.org/patches/fullgaps/
* dwm-hide_vacant_tags-6.2: https://dwm.suckless.org/patches/hide_vacant_tags/
* dwm-noborder-6.2: https://dwm.suckless.org/patches/noborder/
* dwm-pertag-20200914-61bb8b2: https://dwm.suckless.org/patches/pertag/
* dwm-status2d-6.3: https://dwm.suckless.org/patches/status2d/
* dwm-statuscmd-status2d-20210405-60bb3df: https://dwm.suckless.org/patches/statuscmd/
* dwm-swallow-20201211-61bb8b2: https://dwm.suckless.org/patches/swallow/
* dwm-systray-6.3: https://dwm.suckless.org/patches/systray/
* dwm-winicon-6.2-v2.1: https://dwm.suckless.org/patches/winicon/

These patches generally required a lot of configurations to get working together. Namely, the most complex to get working together would be barpadding, systray, winicon and status2d. This is due to them generally interfering with each others core functionality.

## Dependancies
The following dependancies are required for Dwm, installable through the following terminal commands:
* X (Xorg Server) :
<pre><span sytle="color:red">sudo </span>pacman -Sy xorg</pre>
You would also need your graphics card drivers. Please refer to the following link for Arch: https://wiki.archlinux.org/title/Hardware_video_acceleration. If you use an alternative distribution, please follow the distributions graphics driver installation guide.
* Libxcb:
<pre>sudo pacman -Sy libxcb</pre>
* Xdg-utils:
<pre>sudo pacman -Sy xdg-utils</pre>
* Nerd-Font-Icons (I will demonstrate with yay, but paru and other download managers can be used. Note that the complete package isn't needed):
<pre>yay -S nerd-fonts-complete</pre>
* Yahl-libs:
<pre>sudo pacman -Sy yahl</pre>
* Imlib2:
<pre>sudo pacman -Sy imlib2</pre>
* A Display Manager, I use lightdm, gdm can also be used but is slower: 
<pre>sudo pacman -Sy lightdm
sudo systemctl enable lightdm</pre>
* For volume control (non-essential, but will lead to a better top bar experience) via pulseaudio and tuning via pulsemixer:
<pre>sudo pacman -S pulseaudio pulsemixer</pre>
* GTK for general theming:
<pre>sudo pacman -S gtk2 gtk3 gtk4</pre>
* GTK theming tools (will be used in this guide), cli options available also:
<pre>sudo pacman -S lxappearance-gtk3</pre>
* **A desktop compositor such as picom or xcompmgr. You will realise that dwm hangs without one.**
<pre>sudo pacman -S picom</pre>
* feh for setting the background wallpaper
<pre>sudo pacman -S feh</pre>

## Startup Application Management ##
This installation of dwm allows for startup applications to be directly launched from $HOME/.dwm/autostart.sh

Prior to moving forward, execute the following script into your terminal of choice within the downloaded folder:
<pre>chmod +x install-bg.sh && ./install-bg.sh</pre>

A cat ~/.dwm/autostart.sh will reveal the following:
<pre>
#!/usr/bin/bash
numlockx on &
$HOME/.config/feh/.fehbg &
picom &
xbindkeys &
xset r rate 300 55
dwmblocks &
clipmenud &
kdeconnect-cli &
</pre>

Note the following:
* Picom or alternative desktop compositors are essential for a viable experience.
* The xset command can be ommited. It simply increases scroll speed.
* xbindkeys and clipmenud will be elaborated on in the dmenu section and dwmblocks will also have its own section. 


## Installation via scripts
This section will detail installing dwm via scripts.

Initially, git clone this repo into your home directory:
<pre>clone https://github.com/MinaMatta98/suckless-dwm-blue</pre>
Then install the patched version of dwm via the following terminal command:
<pre>sudo make clean install</pre>

## General Theming
This section involves the general theming and will allow for the installation of certain icons and modal colors that will help complete the end user experience. Note that none of these are my own and full credit go to the owners below:
* Layan-dark-solid theme: https://github.com/vinceliuice/Layan-gtk-the theme

**All credits for the theme go to the abovementioned author**
* Lyra-purple-dark icons: https://github.com/yeyushengfan258/Lyra-icon-theme

**All credits for the icons go to the abovementioned author**

### GTK theme installation
From the main folder ($HOME/suckless-dwm-blue/), install the GKT theme by inputting the following terminal command:
<pre>./Layan-gtk-theme/install.sh</pre>
If the command could not execute, then do the following:
<pre>chmod +rwx $HOME/suckless-dwm-blue/Layan-gtk-theme/install.sh && $HOME/suckless-dwm-blue/Layan-gtk-theme/install.sh</pre>

### Icon theme installation
From the main folder ($HOME/suckless-dwm-blue/), install the icon theme by inputting the following terminal command:
<pre>./Lyra-icon-theme/install.sh</pre>
If the command could not execute, then do the following:
<pre>chmod +rwx $HOME/suckless-dwm-blue/Lyra-icon-theme/install.sh && $HOME/suckless-dwm-blue/Lyra-icon-theme/install.sh</pre>

#### GTK and Icon theme activation ###
Now that the themes have been installed in the system, they must be selected for system use:
* Start lxappearance from your terminal or launcher of choice
* Under Widgets, select Layan-dark-solid
![themeing](/Images/Screenshot-6.png)
* Under Icons, select Lyra-dark-purple
![themeing](/Images/Screenshot-7.png)
* Under Font, select enable antialiasing and hinting
![themeing](/Images/Screenshot-8.png)
* Under Other, select enable accessibility in GTK+ applications
![themeing](/Images/Screenshot-9.png)
