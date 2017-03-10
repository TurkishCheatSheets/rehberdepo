//temel derleme ortamının kurulması(rootfs yapmak)

cd /sources/milis.git

mkdir -p /mnt/lfs

export LFS=/mnt/lfs

./lfs-mekanizma -ia

cd /paketler/temel/

sirali_kur /root/talimatname/temel/derleme.sira /mnt/lfs/

cd /paketler/temelek/

mps -k git#2.7.1-x86_64.mps.lz -kok /mnt/lfs

cd /sources/milis.git

./lfs-mekanizma -cg

cd /tmp

rm *.PRE

for i in *.POST; do bash "$i"; done

//sorunsuz calisirsa kur-kos betikleri silinebilir.

rm *.POST

mps -trot

//temek paket veritabanı yedeğini görmek için

mps -trl

//derleme ortamı hazırlanmış olur.istediğimiz zaman "./lfs-mekanizma -cg" komutu ile ortama girebiliriz.

exit

./lfs-mekanizma -ui

//yaptıktan sonra ortamı taşınabilir sıkıştırma yapabiliriz.

mksquashfs /mnt/lfs milis_derlemeortami.sfs -comp xz
