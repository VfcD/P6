# Arch Linux : encrypt an external USB drive

Howto encrypt an external USB drive

scenario:

    USB drive for backups. 
    connected usb drive is sdb with one partition sdb1.

1. create and open luks partition

        cryptsetup -c aes-xts-plain64 -y -s 512 luksFormat /dev/sdb1
        cryptsetup luksOpen /dev/sdb1 backup_drive

2. create filesystem on decrypted partition

        mkfs.ext4	/dev/mapper/backup_drive

	close the luks container:
  
    	cryptsetup luksClose /dev/mapper/backup_drive


3. Using the encrypted drive
3.1 Mount
	
	cryptsetup luksOpen /dev/sdb1 backup_drive
	mount /dev/mapper/backup_drive /mnt

3.1 Umount
	
	umount /mnt
	cryptsetup luksClose /dev/mapper/backup_drive
