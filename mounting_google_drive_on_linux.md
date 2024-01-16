## A. INSTALLATION
### On Ubuntu
1. Install ocamlfuse using the following command:
   ```sh
   sudo add-apt-repository ppa:alessandro-strada/ppa
   sudo apt update && sudo apt install google-drive-ocamlfuse
   ```
3. Run ocamlfuse in the command line:
   ```sh
   google-drive-ocamlfuse
   ```
3. Authorize the ocamlfuse system to access files and folders on your google drive. A sign-in window will open in your browser automatically where the user needs to sign-in and provide required access.
4. Make a new directory named ‘googledrive’ where the Google drive will be mounted
   ```sh
   mkdir ~/googledrive
   ```
5. Mount the google drive on your Linux-based system by running the following command and you are done:
   ```sh
   google-drive-ocamlfuse ~/googledrive
   ```
6. Unmounting of the FUSE system can be done in case one wishes to disconnect the google drive with local system, by running the following command:
   ```sh
   fusermount -u ~/google-drive
   ```

### On Debian
1. There’s no official deb package for Debian. But we can easily compile it from source. First, install OPAM package manager.
   ```sh
   sudo apt install opam
   ```
2. Then install build dependencies.
   ```sh
   sudo apt install m4 libcurl4-gnutls-dev libfuse-dev libsqlite3-dev zlib1g-dev libncurses5-dev pkg-config
   ```
3. Initialize OPAM state.
   ```sh
   opam init
   ```
4. Update the list of available packages.
   ```sh
   opam update
   ```
5. Compile and install Google Drive Ocamlfuse.
   ```sh
   opam install google-drive-ocamlfuse
   ```

## B. SETUP
1. Create file */usr/bin/gdfuse* and copy these script into it:
   ```bash
    #!/bin/bash
    su $USER -l -c "google-drive-ocamlfuse -label $1 $*"
    exit 0 
   ```
2. Make it executable:
   ```sh
   sudo chmod 777 /usr/bin/gdfuse
   ```
3. Insert in */etc/fstab* file these config:
   ```sh
   gdfuse#default /mnt/gdrive fuse.google-drive-ocamlfuse  _netdev,defaults,uid=1000,gid=1000,allow_other 0 0
   ```

## C. COMMANDS
1. Manual mount
   ```sh
   sudo mount /mnt/gdrive
   ```
3. Manual umount
   ```sh
   sudo umount /mnt/gdrive
   ```


## Refferences:
1. https://medium.com/@enthu.cutlet/how-to-mount-google-drive-on-linux-windows-systems-5ef4bff24288
2. https://www.linuxbabe.com/cloud-storage/install-google-drive-ocamlfuse-ubuntu-linux-mint
