## Minimalistic rEFInd theme

[rEFInd](http://www.rodsbooks.com/refind/) is an easy to use boot manager for UEFI
based systems. This is a clean and minimal theme for it.

![rEFInd Minimalistic](http://i.imgur.com/3bMG6U7.png)

### rEFInd and theme install

1. Install **dependencies**
```sh
sudo pacman -S refind intel-ucode # or amd-ucode
```

2. Install rEFInd Boot Manager
```sh
sudo refind-install
git clone https://github.com/morynth/rEFInd-minimal.git
sudo cp rEFInd-minimal/refind.conf /boot/efi/refind
```

3. Copy Example Configuration
```sh
git clone --depth 1 https://github.com/morynth/rEFInd-minimal.git
sudo cp rEFInd-minimal/refind.conf /boot/efi/refind
```

4. Edit `refind.conf`

Modify the startup project configuration, including `volume` and `options`,volume specifies the partition where the kernel is located(EFI), and options="root=PARTUUID" specifies the root partition, `ls -l /dev/disk/by-label` and `ls -l /dev/disk/by-partuuid/` command can obtain partlabel and partuuid.

5. Btrfs Support(Optional)

make sure `btrfs_x64.efi driver` is installed, it can be installed manually by copying from `/usr/share/refind/drivers_x64/btrfs_x64.efi` to `esp/EFI/refind/drivers_x64/btrfs_x64.efi`, or you can install all drivers with the refind-install /dev/sdx --alldrivers option.

```sh
sudo mkdir -p /boot/EFI/refind/drivers_x64
sudo cp /usr/share/refind/drivers_x64/btrfs_x64.efi /boot/EFI/refind/drivers_x64/btrfs_x64.efi
```

6. Install theme
```sh
sudo mkdir -p /boot/EFI/refind/themes
```

7. Clone this repository into the `themes` directory.
```sh
sudo cp -r ./rEFInd-minimal /boot/EFI/refind/themes
```

Here's an example menuentry configuration (from the screenshot)

```nginx
menuentry "Arch Linux" {
	icon /EFI/refind/themes/rEFInd-minimal/icons/os_arch.png
	loader vmlinuz-linux
	initrd initramfs-linux.img
	options "rw root=UUID=dfb2919d-ff78-48db-a8a7-23f7542c343a loglevel=3"
}

menuentry "Windows" {
	icon /EFI/refind/themes/rEFInd-minimal/icons/os_win.png
	loader /EFI/Microsoft/Boot/bootmgfw.efi
}

menuentry "OSX" {
	icon /EFI/refind/themes/rEFInd-minimal/icons/os_mac.png
	loader /EFI/Apple/Boot/bootmgfw.efi
}
```

Entries that are autodetected should also show the proper icons.

### Background sizes

If you find the background looks blurry it may be due to the included wallpaper
being an incorrect resolution for your monitor. You can download the [original
high quality wallpaper][wallpaper], resize it as appropriate, and replace the
`background.png`.

You can of course also choose your own background!

### Attribution

The OS icons are from [Lightness for burg][icons] by [SWOriginal][icon-author].

The background is [Minimalist Wallpaper][wallpaper] by
[LeonardoAIanB][wallpaper-author]. Thank you to [Padster][padster] for locating
it!

[icons]: http://sworiginal.deviantart.com/art/Lightness-for-burg-181461810
[icon-author]: http://sworiginal.deviantart.com/

[padster]: https://github.com/theRealPadster
[wallpaper]: http://leonardoalanb.deviantart.com/art/Minimalist-wallpaper-295519786
[wallpaper-author]: http://leonardoalanb.deviantart.com/
