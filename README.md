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
*   Add new user to video group to be able to access the camera:
    *   `usermod -a -G video bob`

## Node.js

*   Download installation script for Debian: `curl -sL https://deb.nodesource.com/setup_7.x | bash -`
    *   More installation scripts [here](https://github.com/nodesource/distributions)
    *   Note: if it does not work without sudo, use the following command: `sudo curl -sL https://deb.nodesource.com/setup_7.x | bash -`
*   `sudo su`
*   `apt-get install -y nodejs`

## WLAN

*   `sudo nano /etc/wpa_supplicant/wpa_supplicant.conf`
    *   Content:
    ```
    auto wlan0
    allow-hotplug wlan0
    iface wlan0 inet dhcp
    wpa-ap-scan 1
    wpa-scan-ssid 1
    network={
        ssid="<SSID>"
        psk="<KEY>"
    }
    gateway <IPROUTER>
    ```
*   `sudo nano /etc/network/interfaces`
    *   Content:
    ```
    source-directory /etc/network/interfaces.d
    auto lo
    iface lo inet loopback
    auto wlan0
    allow-hotplug wlan0
    iface wlan0 inet dhcp
    wpa-ap-scan 1
    wpa-scan-ssid 1
    wpa-ssid "<SSID>"
    wpa-psk "<KEY>"
    pre-up iw dev wlan0 set power_save off
    post-down iw dev wlan0 set power_save on
    ```
*   `sudo ifdown wlan0 && sudo ifup wlan0`