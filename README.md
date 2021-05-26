# SMBv1-Gateway
The SMBv1 Gateway provides a way to use a Raspberry Pi to confine SMBv1 access to legacy devices that do not support more recent versions such as SMBv3.
It was developped as a workaround for the lack of support for SMBv3 by the Sonos S1 and S2 ranges of products.

The SMBv1 version is notoriously weak and subject to exploits such as [ransomwares](https://stealthbits.com/blog/what-is-smbv1-and-why-you-should-disable-it/)

# Requirements

This is a Linux image based on Raspberry Pi OS 10 (buster) and Linux Kernel 5.4.51 and should be compatible with every current Raspberry Pi models (tested on Pi 2B and Pi 4B 2GB as of v0.0.1).
A Raspberry Pi using an Ethernet interface is recommended.

Here's what you need :
1. A Samba / Windows shared folder on a NAS device
2. Any Raspberry Pi, but I recommend a model with an Ethernet interface (100 mbs is enough)
3. A 4GB MicroSD card

# Credentials and environment

* Hostname: `smbgtw`
* IP Address: DHCP
* Root username: `pi`
* Password: `raspberry`

# Usage

1. Flash the image to a MicroSD card (4GB minimum) using any tool such as [BalenaEtcher](https://www.balena.io/etcher/)
2. Insert it into your Pi and start it. Default username is `pi` with password `raspberry`
3. Input your local (eg NAS) credentials in `/mnt/.smbcredentials`
4. Set up your local (eg NAS) shared folder in `/etc/fstab`: replace the `//server/share/` with your suitable info
5. Force mount the shared drive using `sudo mount -a`
6. Check the result with `ls /mnt/music`
7. Reset the Samba User Password (the one you will use to log via SMBv1) : `sudo smbpasswd music`
8. Map the new shared folder on your Legacy device `//smbgtw/music` using the following credentials
* Username : `music`
* Password : `<the one you provided at #7>`
