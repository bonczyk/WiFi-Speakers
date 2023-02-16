# WiFi-Speakers
Play Windows audio on your Linux PC (DD-WRT) with USB speakers


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

