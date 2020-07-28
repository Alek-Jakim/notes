## Package Management

Ubuntu is derived from Debian Linux. Debian uses the dpkg packaging system. A packaging system is a way to provide programs and applications for installation. This way, you don’t have to build a program from the source code.

APT (Advanced Package Tool) is the command line tool to interact with this packaging system. There are already dpkg commands to manage it, but apt is a more user-friendly way to handle packages. You can use it to find and install new packages, upgrade packages, clean your packages, etc.

`apt-get` and `apt-cache`. apt-get is for installing, upgrading, and cleaning packages, while apt-cache is used for finding new packages. 


```bash
#Updating the package database requires superuser privileges, so you’ll need to use sudo.
sudo apt-get update

#The most convenient way is to upgrade all the packages that have updates available. You can use the command below for this purpose
sudo apt-get upgrade

# To upgrade only a specific program, use the command below:
sudo apt-get upgrade <package_name>



# If you know the name of the package, you can easily install it using the command below:
sudo apt-get install <package_name>


# avoid using this command.
sudo apt-get dist-upgrade

#apt-cache command to search for packages - you don’t even need sudo here
apt-cache search <search term>


# for more info...
man apt-get
```

