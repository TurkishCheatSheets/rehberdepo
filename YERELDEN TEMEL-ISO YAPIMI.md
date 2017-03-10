//Gerekli Paketler:lzip,squashfs-tools(mksquashfs),syslinux-utils(isohybrid),genisoimage

//temel iso yapmak(minimal iso)

cd /sources/milis.git

mkdir -p /mnt/lfs

export LFS=/mnt/lfs

./lfs-mekanizma -ia

cd /paketler/temel/

sirali_kur /root/talimatname/temel/derleme.sira /mnt/lfs/

cd /paketler/temelek/

sirali_kur /root/talimatname/temel-ek/derleme.sira /mnt/lfs/

cd /sources/milis.git

./lfs-mekanizma -cg

cd /tmp

rm *.PRE

for i in *.POST; do bash "$i"; done

//sorunsuz calisirsa kur-kos betikleri

rm *.POST

//initrd yapmak için

cd /root

./lfs-mekanizma -bo

//exit ile dışarı çıkıp iso yapmak icin.

./lfs-mekanizma -so

./lfs-mekanizma -io

./qemu.sh
