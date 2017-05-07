# viewbook-2110-archlinux
## Archlinux install ISO for the Viewbook 2110 
This is based on the ISO from 2017-04
- EFI 
Is the contents of the EFI partition on the USB key
- arch32 
Has the files needed to create bootia32.efi:
$ grub-mkstandalone -d /usr/lib/grub/i386-efi/ -O i386-efi --modules="part_gpt part_msdos" --fonts="unicode" --locales="uk" --themes="" -o  "YOUR_PATH/arch32/bootia32.efi" "boot/grub/grub.cfg=YOUR_PATH/arch32/grub.cfg" -v
- arch-custom.iso
Is the install CD,created with:
$ iso_label="ARCH_201704"
$ xorriso -as mkisofs -iso-level 3 -full-iso9660-filenames -volid "${iso_label}" -eltorito-boot isolinux/isolinux.bin -eltorito-catalog isolinux/boot.cat -no-emul-boot -boot-load-size 4 -boot-info-table  -isohybrid-mbr SQUASHFS_DIR/isolinux/isohdpfx.bin  -output arch-custom.iso SQUASHFS_DIR/
