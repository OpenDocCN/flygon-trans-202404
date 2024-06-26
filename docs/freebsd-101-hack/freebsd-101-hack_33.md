# 打印 PCI 设备信息

## 打印 PCI 设备信息

`FreeBSD` 提供了 `pciconf` 命令，可以列出 `PCI` 设备的信息：

```
# pciconf -lv
hostb0@pci0:0:0:0:  class=0x060000 card=0x197615ad chip=0x71908086 rev=0x01 hdr=0x00
vendor = 'Intel Corporation'
device = '440BX/ZX/DX - 82443BX/ZX/DX Host bridge'
class  = bridge
subclass   = HOST-PCI
pcib1@pci0:0:1:0:   class=0x060400 card=0x00000000 chip=0x71918086 rev=0x01 hdr=0x01
vendor = 'Intel Corporation'
device = '440BX/ZX/DX - 82443BX/ZX/DX AGP bridge'
class  = bridge
subclass   = PCI-PCI
isab0@pci0:0:7:0:   class=0x060100 card=0x197615ad chip=0x71108086 rev=0x08 hdr=0x00
vendor = 'Intel Corporation'
device = '82371AB/EB/MB PIIX4 ISA'
class  = bridge
subclass   = PCI-ISA
...... 
```

如果你习惯于使用在 `GNU/Linux` 上预装的 `lspci`，你可以自行安装它：

```
# pkg install pciutils
......
# lspci
00:00.0 Host bridge: Intel Corporation 440BX/ZX/DX - 82443BX/ZX/DX Host bridge (rev 01)
00:01.0 PCI bridge: Intel Corporation 440BX/ZX/DX - 82443BX/ZX/DX AGP bridge (rev 01)
00:07.0 ISA bridge: Intel Corporation 82371AB/EB/MB PIIX4 ISA (rev 08)
...... 
```

参考：

["lspci" & pciconf 命令在 FreeBSD 中](http://kazaonfreebsd.blogspot.com/2012/12/lspci-pciconf-commands-in-freebsd.html).
