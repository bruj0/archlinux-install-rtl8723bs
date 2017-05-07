# viewbook-2110-archlinux
## Archlinux install ISO for the Viewbook 2110
- Wireless driver for the RLT8723bs
- EFI32
- Download ISO from https://github.com/bruj0/archlinux-install-rtl8723bs/releases/download/1/arch-custom.iso

## Installation
- Clear the USB key

`$ dd if=/dev/zero of/dev/sdX`
- Choose "blank GPT" and create 2 partitions, 1 of 1GB and 2 of 500M type ef00

`$ gdisk /dev/sdX`
- Format the EFi partition to fat32

`$ mkfs.vfat -F 32 -n "EFI"  /dev/sdX2`

- Mount and Copy the EFI files

`$ mount /dev/sdX2 /mnt/usb`

`$ cp -a EFI /mnt/usb`

`$ sync && umount /mnt/usb`
- Copy the Install CD ISO

`$ dd bs=4M if=arch-custom.iso of=/dev/sdX1`
- Boot the Viewbook with the new CD and follow the install instruction.

## Contents
This is based on the ISO from 2017-04

- EFI 

Is the contents of the EFI partition on the USB key
- arch32 

Files needed to create bootia32.efi:

`$ grub-mkstandalone -d /usr/lib/grub/i386-efi/ -O i386-efi --modules="part_gpt part_msdos" --fonts="unicode" --locales="uk" --themes="" -o  "YOUR_PATH/arch32/bootia32.efi" "boot/grub/grub.cfg=YOUR_PATH/arch32/grub.cfg" -v`

- arch-custom.iso

Install CD,created with:

`$ iso_label="ARCH_201704"`

`$ xorriso -as mkisofs -iso-level 3 -full-iso9660-filenames -volid "${iso_label}" -eltorito-boot isolinux/isolinux.bin -eltorito-catalog isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table  -isohybrid-mbr SQUASHFS_DIR/isolinux/isohdpfx.bin  -output arch-custom.iso SQUASHFS_DIR/`

## More info

https://wiki.archlinux.org/index.php/Unified_Extensible_Firmware_Interface#Booting_64-bit_kernel_on_32-bit_UEFI

https://wiki.archlinux.org/index.php/Remastering_the_Install_ISO

https://aur.archlinux.org/packages/8723bs-git/

https://watchmysys.com/blog/2015/12/arch-linux-and-sdio-wifi-on-a-bay-trail-tablet/

