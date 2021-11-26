# kernel-debug-bootstrap

## prequisite

1. make the rootfs image

```
mkinitramfs -o ramdisk.img # in arch linux, the command is mkinitcpio
```

2. auto load the vmlinu gdb script in the kernel source code

```
echo "add-auto-load-safe-path path/to/linux/scripts/gdb/vmlinux-gdb.py" >> ~/.gdbinit
```


## qemu & gdb

```bash
qemu-system-x86_64 \
  -kernel arch/x86_64/boot/bzImage \
  -nographic \
  -append "console=ttyS0 nokaslr" \
  -initrd ramdisk.img \
  -m 512 \
  --enable-kvm \
  -cpu host \
  -s -S
```

gdb attach remote target

```
$gdb vmlinux
(gdb) target remote :1234
(gdb) hbreak start_kernel
(gdb) c
(gdb) lx-dmesg
```

