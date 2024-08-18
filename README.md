# _VM_
I have the best of made from scratch FreeBsd on VirtualBox :
https://download.freebsd.org/snapshots/
http://ftp.freebsd.org/pub/FreeBSD/snapshots/	stable

![VirtualBox__OLDuSTy__18_08_2024_20_43_49](https://github.com/user-attachments/assets/93e4bd3b-fe3f-46ad-a153-7395482839cd)

make install clean BATCH=yes
After install:
% shutdown -p now
unmount iso
# pw groupmod video -m guestuser
# pw groupmod network -m network
% sysctl net.wlan.devices
/etc/wpa_supplicant.conf
network={
	ssid="myssid"
	psk="mypsk"
}

1-
# pkg install xorg-server       (1gb 214mb downloaded)
# pkg install xorg-drivers	(61mib 8mb) (mouse kbdvideo vesa...)
# pkg install xorg-fonts	 (53mib 34mib)
# pkg install webfonts     (6mib 2mib)
# pkg install xinit (15 kib)
# pkg install xauth (2mib 698kb)
# pkg install xorg-apps
-2 Vm
# virtualbox-ose-additions-legacy (vbox 32bit and 64bit guest)
# virtualbox-ose-additions not working on for clipboard

-2 Intel and amd Graphics
# pkg install drm-510-kmod (13mib 3mib - support Fbsd 13.1 ++ )
# pkg install xf86-intel-video


For Startup services:
# ee /etc/rc.conf
moused_enable="YES"
dbus_enable=yes 
sound_load=yes
linux_enable="YES"	Linux Binary Compatibility
wlans_ath0="run0"
ifconfig_run0="WPA SYNCDHCP"
kld_list="fuse"	
kld_list="vmwgfx"
hald_enable=yes
snd_hda_load=yes
kld_list="i915kms"  just for intel graphics
kld_list="/boot/modules/radeonkms.ko" just for radeon
If ntpd(8) or ntpdate(8) is used, disable host time synchronization:
vboxservice_flags="--disable-timesync"
vboxguest_enable="YES"
vboxservice_enable="YES"
kld_list="${kld_list} fuse coretemp cpuctl" just for monitor cpu
3-
# pkg install gxkb 392mb 69mib
# pkg install xvkbd		virtual keyboard
# ee /etc/login.conf on top of :umask=022:
 :charset=UTF-8:\
 :lang=en_US.UTF-8:\
# cap_mkdb /etc/login.conf 
to disable beep (bell):
# ee /etc/sysctl.conf :
 kern.vt.enable_bell=0
# ee ~/.login   
setenv XKB_DEFAULT_RULES xorg   (for csh/tcsh)
# pkg install setxkbmap 12mib 3mib (x64 11kib)
% mkdir ~/.config
% mkdir ~/.config/gxkb
% shutdown -r now
Configuration is done via config file: .config/gxkb/gxkb.cfg :
layouts=us,ar
toggle_option=grp:alt_shift_toggle,grp_led:scroll,terminate:ctrl_alt_bksp

# ee /boot/loader.conf
fuse_load="YES"
# ee /etc/fstab
/dev/da1s1 /mnt ntfs mountprog=/usr/local/bin/ntfs-3g,late,failok,rw 0 0
proc	/proc	procfs	rw	0	0

# shutdown -r now
# Xorg -configure : xorg.conf.new generated (drivers: scfb vboxvideo modesetting vesa)
# ee /root/xorg.conf.new
# mv /root/xorg.conf.new /usr/local/etc/X11/xorg.conf.d/xorg.conf
# pkg install openbox (13mib 69mib)

# pkg install obconf  1mib 213kib
# pkg install tint2    1mib 345kib
https://draculatheme.com/openbox

# pkg install rxvt-unicode    (4mib 922kib)
# pkg install xrdb 18kib
# pkg install xdpyinfo   (90 kib)
 xdpyinfo | grep dimensions for resolution
# pkg install numlockx 25kib
# pkg install figlet 188kib
# pkg install bash 9mib 2mib
bash ./script.sh
# pkg install psearch 20kib
Finlay we need to tell Xorg to use openbox:
% echo "exec openbox-session" >> ~/.xinitrc
% mkdir ~/.config/openbox
% cp /usr/local/etc/xdg/openbox/*.* ~/.config/openbox
% ee ~/.config/openbox/autostart :
VBoxClient-all 	start virtualbox modules
xrdb -merge ~/.Xresources & change app theme
tint2 &
numlockx &
setxkbmap -layout "us,ar" -option "grp:alt_shift_toggle" &
mount_msdosfs /dev/da0s1 /media/flash &
% touch ~/.config/openbox/autostart && chmod +x ~/.config/openbox/autostart
% echo "#!/bin/sh" >> ~/.config/openbox/autostart
#ee /etc/ttys :
ttyv8   "/usr/local/bin/xdm -nodaemon"  xterm   off to on secure
# mkdir /mnt/hgfs
# su - user
% ee ~/.xsession
ck-launch-session dbus-launch --exit-with-session /usr/local/bin/startlxde   (Lxde)	

% shutdown -r now

# pkg install xfe 	19mib 5mib file manager like MS
# pkg install git 	43mib 9mib
# pkg install xcalc 3mib 540k

# pkg install vim 37mib 8mib

# pkg install keepassxc 65mib 13mib
# pkg install git 40mib 8mib 
# pkg install gnumeric 360mib 72mib 
# pkg install abiword 40mib 9mib 
# firefox-esr 375mib 79mib
______________________________________________________________________
openvpn
https://gist.github.com/johnramsden/349581cb60acf9a4c61e0d551c55ddbf
bash ./openvpn-pia.sh

______________________________________________________________________
# pkg install vscode 507mib 116mib
Build dependencies:
        zip : archivers/zip
        electron19 : devel/electron19
        rg : textproc/ripgrep
        npm-node16>0 : www/npm-node16
        yarn-node16>0 : www/yarn-node16
        update-desktop-database : devel/desktop-file-utils
        gmake>=4.3 : devel/gmake
        pkgconf>=1.3.0_1 : devel/pkgconf
        python3.9 : lang/python39
        xorgproto>=0 : x11/xorgproto
        x11.pc : x11/libX11
        xcb.pc : x11/libxcb
        xcomposite.pc : x11/libXcomposite
        xcursor.pc : x11/libXcursor
        xdamage.pc : x11/libXdamage
        xext.pc : x11/libXext
        xfixes.pc : x11/libXfixes
        xi.pc : x11/libXi
        xkbfile.pc : x11/libxkbfile
        xrandr.pc : x11/libXrandr
        xrender.pc : x11/libXrender
        xscrnsaver.pc : x11/libXScrnSaver
        xtst.pc : x11/libXtst
____________________________Clean sys________________________________
rm -vfR /tmp/*
rm -vfR /var/tmp/*
rm -vfR  /usr/home/noname/.cache/*
pkg clean -a

