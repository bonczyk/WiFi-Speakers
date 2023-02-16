# WiFi-Speakers
Play Windows audio on your Linux PC (DD-WRT) with USB speakers

<h1>Using the WL-500g as a wireless soundcard</h1>
With an external USB soundcard and <a href="http://wl500g.dyndns.org/">Oleg's
modified firmware</a>, an ASUS <a
 href="http://www.asus.com/products4.aspx?l1=12&amp;l2=43&amp;l3=0&amp;model=61&amp;modelmenu=1">WL-500g</a>
WLAN router can be used to
wirelessly play music on your stereo using Winamp or almost any Linux
sound player.<br>
<h2>Installing EsounD on the WL-500g</h2>
<p>For receiving sound streams on the router and playing them on the
USB
sound card, the well-kown <a
 href="http://www.tux.org/%7Ericdude/EsounD.html">EsounD</a> daemon is
used. You can either install it as an ipgk from Unslug or download the
binary file from this location: <br>
</p>
<div style="margin-left: 40px;">EsounD daemon binary: <a
 href="http://home.in.tum.de/%7Epustka/mipsel/esd">esd</a> <br>
</div>
<p>Before starting it, the default ASUS sound server (useable only from
Windows Media Player) needs to be killed, as it occupies the sound
card:
</p>
<div style="margin-left: 40px;"><code>killall waveservermain</code><br>
<code>killall waveserver</code><br>
</div>
<p>Then the ESD daemon can be started:<span
 style="font-family: monospace;"></span></p>
<div style="margin-left: 40px;"><span style="font-family: monospace;"></span><code>esd
-d /dev/sound/dsp -tcp -public &amp;</code><br>
</div>
<h2>Connecting to the soundcard from a client computer</h2>
<p>If you are running Linux, you can use an audio player like <a
 href="http://www.xmms.org/">XMMS</a> or <a
 href="http://amarok.kde.org/">amaroK</a>, choose an EsounD output
plugin (gstreamer in case of amaroK) and enter the server's IP address.
</p>
<p>In order to connect to the EsoundD server from Windows, Kasper
Laudrup
has a nice EsounD output plugin for <a href="http://www.winamp.com/">Winamp</a>
available at&nbsp; <a href="http://www.linuxfan.dk/index.php?page=code">his
site</a>. Note that for Winamp 5 you need to download the Winamp 2
version, not Winamp 3. At the bottom of this page, there also is a link
to an updated version, which includes better resampling.<br>
</p>

<br>
<br>
<br>
<br>
<br>
<br>

cd /usr/local/sbin
wget http://home.in.tum.de/%7Epustka/mipsel/esd
chmod +x esd 
echo "#!/bin/sh" >> /usr/local/sbin/post-boot
echo "insmod soundcore.o" >> /usr/local/sbin/post-boot
echo "insmod audio.o" >> /usr/local/sbin/post-boot
echo "esd -d /dev/sound/dsp -tcp -public &" >> /usr/local/sbin/post-boot
flashfs save && flashfs commit && flashfs enable
reboot



#/usr/sbin/esd -d /dev/sound/dsp -tcp -public &
#/opt/bin/mipsel-linux-esd -nobeeps -d /dev/sound/dsp -tcp -public &


insmod soundcore.ko
insmod snd.ko
insmod snd-hwdep.ko
insmod snd-page-alloc.ko
insmod snd-timer.ko
insmod snd-pcm.ko
insmod snd-rawmidi.ko
insmod snd-mixer-oss.ko
insmod snd-pcm-oss.ko
insmod snd-usb-lib.ko
insmod snd-usb-audio.ko

mp3blaster -s /dev/sound/dsp -l ocb

kmod-sched - 3.1.5-1
kmod-scsi-core - 3.1.5-1
kmod-scsi-generic - 3.1.5-1
kmod-sit - 3.1.5-1
kmod-sound-core - 3.2.5-1
kmod-tun - 3.1.5-1
kmod-usb-audio - 3.2.5-1
kmod-usb-core - 3.2.5-1



--== Linux setup part 1
mkdir -p /usr/local/etc/dropbear
dropbearkey -t dss -f /usr/local/etc/dropbear/dropbear_dss_host_key
dropbearkey -t rsa -f /usr/local/etc/dropbear/dropbear_rsa_host_key
mkdir -p /usr/local/sbin/
echo "#!/bin/sh" >> /usr/local/sbin/post-boot
chmod +x /usr/local/sbin/post-boot
echo "dropbear" >> /usr/local/sbin/post-boot

flashfs save && flashfs commit && flashfs enable
reboot


--== Linux setup part 2
umount /tmp/harddisk
umount /opt

fdisk

mkswap /dev/discs/disc0/part2
swapon /dev/discs/disc0/part2
mke2fs -j /dev/discs/disc0/part1

mount -o bind /tmp/harddisk/opt /opt
mkdir -p /opt/tmp/ipkg 
cd /opt/tmp/ipkg
ipkg.sh update
wget http://ipkg.nslu2-linux.org/feeds/optware/oleg/cross/stable/uclibc-opt_0.9.28-13_mipsel.ipk
ipkg.sh install uclibc-opt_0.9.28-13_mipsel.ipk
wget http://ipkg.nslu2-linux.org/feeds/optware/oleg/cross/stable/ipkg-opt_0.99.163-10_mipsel.ipk
ipkg.sh install ipkg-opt_0.99.163-10_mipsel.ipk

ipkg update
ipkg install nano
ipkg install mc
ipkg install coreutils
ipkg install findutils
ipkg install diffutils
ipkg install unzip



#mount -t ext3 /dev/scsi/host0/bus0/target0/lun0/part3 /mnt
#tar cvO -C / .version bin/ etc/ lib/ sbin/ usr/ www/ var/ | tar x -C /mnt
#mkdir -p /mnt/tmp && mkdir -p /mnt/dev && mkdir -p /mnt/proc && mkdir -p /mnt/mnt
#umount /mnt
#nvram set boot_dev="/dev/scsi/host0/bus0/target0/lun0/part3"
#nvram commit

