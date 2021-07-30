# Arch-Installationation

The command I used to install arch in Virtual Box with XFCE4 and VirtualBox-Guest-Utils



`fdisk /dev/sda`

	n
	enter 
	enter
	enter 
	w


`mkfs.ext4 /dev/sda1`

`mount /dev/sda1 /mnt`


`pacstrap /mnt base linux linux-firmware`

`genfstab -U /mnt >> /mnt/etc/fstab`

`arch-chroot /mnt`

`timedatectl set-timezone Europe/Paris`


`pacman -S grub`

`grub-install /dev/sda`

`grub-mkconfig -o /boot/grub/grub.cfg`

# Fix Network 

`pacman -S networkmanager`

`systemctl enable NetworkManager`

`exit`

`reboot`

now boot in the existing os option 

---

In the os to install xfce4 desktop

`sudo pacman -S xorg xfce4 xfce4-goodies lightdm lightdm-gtk-greeter`
	enter 
	enter
	enter
	enter
  
`sudo systemctl enable lightdm`

---

Install VirtualBox guest utils

`sudo pacman -Sy virtualbox-guest-utils`

`sudo systemctl enable vboxservice.service`
