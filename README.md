# Arch-Installation

The command I used to install arch in Virtual Box with XFCE4 and VirtualBox-Guest-Utils on a Non-UEFI systems



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

`timedatectl set-timezone Asia/Kolkata`


`pacman -S grub`

`grub-install /dev/sda`

`grub-mkconfig -o /boot/grub/grub.cfg`

Fix Network

`pacman -S networkmanager`

`systemctl enable NetworkManager`

To install XFCE desktop environment

`sudo pacman -S xorg xfce4 xfce4-goodies lightdm lightdm-gtk-greeter`
	enter 
	enter
	enter
	enter
  
`sudo systemctl enable lightdm`

`exit`

`reboot`

---

Now boot into the existing OS

Install VirtualBox guest utils

`sudo pacman -Sy virtualbox-guest-utils`

`sudo systemctl enable vboxservice.service`

`reboot`

Boot in the OS. Now you can have full screen.

---

# Creating Users and adding it in sudoers list.

Following this guide https://www.vultr.com/docs/create-a-sudo-user-on-arch-linux

Be in the root shell (root user) in the installed OS. I will be using the username `aksheet` (username to be all lowercaps). You can use the username you like.

`useradd --create-home aksheet`

![image](https://user-images.githubusercontent.com/71016915/127640975-11319040-676c-4a39-97d6-6d7fa0598759.png)

Set a password for the user by the `passwd aksheet` (aksheet being the username in my case)

![image](https://user-images.githubusercontent.com/71016915/127641805-c49b9de8-d78c-452b-83ab-b3d05c6409f3.png)

`usermod --append --groups wheel aksheet`

![image](https://user-images.githubusercontent.com/71016915/127641165-f3f3e011-75cf-41de-94d0-0121ebb5ea28.png)

`nano /etc/sudoers` 

Scroll down until you find this line in the file
```
## Uncomment to allow members of group wheel to execute any command
# %wheel ALL=(ALL) ALL
```
And uncomment (remove the #) the `# %whell ALL=(ALL) ALL` so it looks like this

![image](https://user-images.githubusercontent.com/71016915/127641615-a74f2bca-cd26-488f-8bd5-a632d626f166.png)

Now you can `su user` and do `sudo -l` and enter your user password.

![image](https://user-images.githubusercontent.com/71016915/127642067-d3ecebd6-0675-4e08-b7f0-32c71d7bbe5d.png)

To delete a user

`userdel -r username` - To delete the user including the /home/username directory

To remove the sudoers right

`nano /etc/sudoers` 

Scroll down until you find this line in the file you previously uncommented.

```
## Uncomment to allow members of group wheel to execute any command
 %wheel ALL=(ALL) ALL
```

And comment (add the #) the `%whell ALL=(ALL) ALL` so it looks like this

![image](https://user-images.githubusercontent.com/71016915/127642291-acefcf23-d6ef-46ff-a016-ae57398aff54.png)
