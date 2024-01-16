## BEGINNING
S3 filesystem in default is not supported yet by Linux OS, but we can add this capability by install s3fs-fuse driver.

These are many ways how the driver implemented in some Linux distors:
* Amazon Linux via EPEL:

  ```
  sudo amazon-linux-extras install epel
  sudo yum install s3fs-fuse
  ```

* Arch Linux:

  ```
  sudo pacman -S s3fs-fuse
  ```

* Debian 9 and Ubuntu 16.04 or newer:

  ```
  sudo apt install s3fs
  ```

* Fedora 27 or newer:

  ```
  sudo dnf install s3fs-fuse
  ```

* Gentoo:

  ```
  sudo emerge net-fs/s3fs
  ```

* RHEL and CentOS 7 or newer via EPEL:

  ```
  sudo yum install epel-release
  sudo yum install s3fs-fuse
  ```

* SUSE 12 and openSUSE 42.1 or newer:

  ```
  sudo zypper install s3fs
  ```

## EXAMPLE
How to implement s3fs-fuse in Debian. We need prepare some informations and credentials. (i.e. S3 provider from idcloudhost):

|                   |                                          |
|-------------------|------------------------------------------|
| S3 Service URL    | https://is3.cloudhost.id                 |
| Bucket name       | the-nagoya                               |
| ACCESS_KEY_ID     | 65TN7ZJBU3PGAU8CS01H                     |
| SECRET_ACCESS_KEY | LQZ2Y8S5oh7PR7P8rezhwPCr39MVDh6YSfLU3A9P |

1. Create a file to save credentials. Default location for the s3fs password file can be created:
    * using a .passwd-s3fs file in the users home directory (i.e. ${HOME}/.passwd-s3fs)
    * using the system-wide /etc/passwd-s3fs file
    ```sh
    # echo ACCESS_KEY_ID:SECRET_ACCESS_KEY > ${HOME}/.passwd-s3fs
    echo 65TN7ZJBU3PGAU8CS01H:LQZ2Y8S5oh7PR7P8rezhwPCr39MVDh6YSfLU3A9P > ${HOME}/.passwd-s3fs
    chmod 600 ${HOME}/.passwd-s3fs

    # or:
    # sudo echo ACCESS_KEY_ID:SECRET_ACCESS_KEY > /etc/passwd-s3fs
    sudo su -c "echo 65TN7ZJBU3PGAU8CS01H:LQZ2Y8S5oh7PR7P8rezhwPCr39MVDh6YSfLU3A9P > /etc/passwd-s3fs"
    ```
2. Create a file to save mounting instruction for auto mounting on reboot.
   ```sh
   sudo mkdir /mnt/S3-Nagoya
   sudo su -c "echo 'the-nagoya /mnt/S3-Nagoya fuse.s3fs _netdev,allow_other,use_path_request_style,url=https://is3.cloudhost.id,use_cache=/root/cache 0 0' >> /etc/fstab"
   ```
3. Manualy mount and umount
   ```sh
   # mount
   mount /mnt/S3-Nagoya

   # umount
   umount /mnt/S3-Nagoya
   ```

## REFFERENCES
* https://github.com/s3fs-fuse/s3fs-fuse/blob/master/README.md




