# Raspberry Pi Setup

## Preparations

*   `sudo apt-get update`
*   `sudo apt-get dist-upgrade`

## Change hostname

*   Replace hostname here: `sudo nano /etc/hosts`
*   Replace hostname here: `sudo nano /etc/hostname`
*   Commit changes: `sudo /etc/init.d/hostname.sh`
*   Reboot: `sudo reboot`

## Users

*   Change password: `passwd`
*   New user: `sudo adduser bob`
*   Add user as sudoer:
    *   From a sudoer account: `sudo visudo`
    *   Insert `bob ALL=(ALL:ALL) ALL` into the file opened

## Node.js

*   Download installation script for Debian: `curl -sL https://deb.nodesource.com/setup_7.x | bash -`
    *   More installation scripts [here](https://github.com/nodesource/distributions)
    *   Note: if it does not work without sudo, use the following command: `sudo curl -sL https://deb.nodesource.com/setup_7.x | bash -`
*   `sudo su apt-get install -y nodejs`
