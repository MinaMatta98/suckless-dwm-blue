# Suckless-dwm-blue
This repo features a pre-patched version of the suckless desktop window manager - dwm. Dwm is lightweight and written in (you wont believe it)...  . This makes it extremely lightweight and responsive, which is made especially clear when you contrast the dwm top bar to something like polybar. While polybar is a good bar extension it compartively is cripplingly slow.

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

## Installation via scripts
This section will detail installing dwm via scripts.

Initially, git clone this repo into your home directory:
<pre>git clone https://github.com/MinaMatta98/suckless-dwm-blue</pre>
