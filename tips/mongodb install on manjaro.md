

Here is what I did to install.

As the package is not available in the official Arch repositories and can't be installed using packman, you need to follow a few steps to install it.

- First, you need to get the URL for the repo of prebuilt binaries for from AUR. It can be found here and by the time of writing this it was https://aur.archlinux.org/mongodb-bin.git

Simply clone the repo in your home directory or anywhere else. 

- Do git clone https://aur.archlinux.org/mongodb-bin.git, then head to the cloned directory, cd mongodb-bin.

- Now, all you need to do is to run makepkg -si command to make the package. the -s flag will handle the dependencies for you and the -i flag will install the package.

- After makepkg finishes its execution, don't forget to start mongodb.service. Run systemctl start mongodb and if needed enable it with systemctl enable mongodb.

- Type mongo in terminal and if the Mongo Shell runs you are all set.
