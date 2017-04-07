---
title: "Recuperando partição NTFS montada no Linux"
layout: post
#date: 2016-02-24 22:48
#image: /assets/images/jason-rosewell-60014.jpg
headerImage: false
#largeImage: true
tag:
- quick-tips
- linux
category: blog
author: vhbsouza
description: Recuperando partição NTFS montada no Linux
---

Estava acordando hoje pra fazer meu TCC, quando ligo meu pc e tento acessar a partição onde meus dados estão armazenados, vejo a seguinte mensagem:

```shell
"Error mounting /dev/sdb1 at /media/fuzzy27/My Book: Command-line `mount -t "ntfs" -o "uhelper=udisks2,nodev,nosuid,uid=1000,gid=1000,dmask=0077,fmask=0177" "/dev/sdb1" "/media/fuzzy27/My Book"' exited with non-zero exit status 13: $MFTMirr does not match $MFT (record 0).
Failed to mount '/dev/sdb1': Input/output error
NTFS is either inconsistent, or there is a hardware fault, or it's a
SoftRAID/FakeRAID hardware. In the first case run chkdsk /f on Windows
then reboot into Windows twice. The usage of the /f parameter is very
important! If the device is a SoftRAID/FakeRAID then first activate
it and mount a different device under the /dev/mapper/ directory, (e.g.
/dev/mapper/nvidia_eahaabcc1). Please see the 'dmraid' documentation
for more details."
```

O que pude entender é que aparentemente, a partição NTFS (do meu antigo HD externo) perdeu esse “MTF”. Pesquisando um pouco encontrei uma solução simples:

```shell
sudo apt-get install ntfs-3g
sudo ntfsfix /dev/sdb1
```

Até mais :D

Referências:

- [http://askubuntu.com/questions/500647/unable-to-mount-ntfs-external-hard-drive](http://askubuntu.com/questions/500647/unable-to-mount-ntfs-external-hard-drive)
- [http://askubuntu.com/questions/183970/mount-exited-with-exit-code-13](http://askubuntu.com/questions/183970/mount-exited-with-exit-code-13)
