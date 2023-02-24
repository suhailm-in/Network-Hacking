# Network Hacking [![Link Status](https://github.com/cugu/awesome-forensics/workflows/CI/badge.svg)](https://github.com/suhailm-in/Network-Hacking)

**Network Hacking** and forensic analysis tools and resources.

- [Network Hacking ](#network-hacking-)

  - [Network Basics](#network-basics)
    - [MAC Address Changing](#mac-address-changing)
    - [Wireless Mode Changing](#wireless-mode-changing)
    - [Wireless Mode Changing ALFA](#wireless-mode-changing-alfa)
    - [Wireless Mode Changing Other Adapters](#wireless-mode-changing-other-adapters)
    

  - [Pre Connection Attacks](#pre-connection-attacks)
    - [WIFI Bands](#wifi-bands)
    - [Packet Sniffing](#packet-sniffing)
    - 
    


  - [Gaining Access](#gaining-access)
  - [Post Connection Attacks](#post-connection-attacks)
  
  

---
## Network Basics

### MAC Address Changing 

```
ifconfig
ifconfig wlan0 down
ifconfig wlan0 hw ether 00:11:22:33:44:55
ifconfig wlan0 up
ifconfig
```

- ifconfig - list all the network interfaces
- wlan0 - name of the network interfaces
- down - disable interface
- up - enable interfaces
- hw - hardware
- ether - mac address

### Wireless Mode Changing
Managed mode - Monitor mode
- To enable Monitor mode for test packet injection

> see all interface <br>
```
ifconfig
```
> desable interface <br>
> check for any conflicting process and kill them <br>
> monitore mode enable <br>
> enable interface
```
ifconfig wlan0 down
airmon-ng check kill
iwconfig wlan0 mode monitor
ifconfig wlan0 up
```
> see wireless interface only
```
iwconfig
```

### Wireless Mode Changing ALFA
ALFA - AWUS036NHA <br>
- To enable Monitor mode for test packet injection:


>see interface
```
ip addr
iwconfig
```
>check for any conflicting process and kill them <br>
>start monitor mode <br>
>verify that monitor mode is used <br>
```
sudo airmon-ng check kill
sudo airmon-ng start wlan0
sudo airmon-ng
```
>you could also use iwconfig to check that interface is in monitor mode
```
iwconfig
```


### Wireless Mode Changing Other Adapters
TP-Link - TL-WN722N V2/V1 OR Other Ineterfaces <br>
Managed mode - Monitor mode<br>



```
ifconfig wlan0 down
airmon-ng check kill
ifconfig wlan0 mode monitor
ifconfig wlan0mon up
iwconfig
```
> or
```
ifconfig wlan0 down
airmon-ng check kill
airmon-ng start wlan0
iwconfig
```
Driver Installing Processes <br>
> Use these commands to get the adapter working on Kali for packet injection and monitoring:
```
sudo apt update
sudo apt upgrade
sudo apt install bc
sudo apt-get install build-essential 
sudo apt-get install libelf-dev 
```
> Try either of these commands to see which works:
```
sudo apt-get install linux-headers-`uname -r`
```
> or
```
sudo apt-get install linux-headers-5.10.0-kali6-amd64
```
> Driver Installing
```
sudo apt install dkms
sudo rmmod r8188eu.ko
git clone https://github.com/aircrack-ng/rtl8188eus
cd rtl8188eus
sudo -i
echo "blacklist r8188eu" > "/etc/modprobe.d/realtek.conf"
exit
sudo reboot
sudo apt update
cd rtl8188eus
sudo make
sudo make install
sudo modprobe 8188eu
```
  
> To enable Monitor mode and test packet injection:
```
sudo ifconfig wlan0 down
sudo airmon-ng check kill
sudo iwconfig wlan0 mode monitor
sudo ifconfig wlan0mon up
iwconfig
```
```
sudo aireplay-ng --test wlan0mon
```


---
## Pre Connection Attacks


### WIFI Bands

- besides the frequency range that can be used
- determines the channel that can be used
- clients need to support band used by a router to communicate with it
- data can be sniffed from a certain band if the wireless adapter used supports that band

***a - uses 5Ghz Frequency only <br>***
***b,g - both use 2.4Ghz Frequency only <br>***
***n - uses 5Ghz and 2.4Ghz <br>***
***ac - uses Frequencies lower than 6Gzh***

> see all 2.4Ghz Frequencies wifi bands
```
airodump-ng wlan0mon
```
> see all 5Ghz Frequencies wifi bands
```
airodump-ng --band a wlan0mon
```
> see both 2.4Ghz and 5Ghz Frequencies wifi bands
```
airodump-ng --band abg wlan0mon
```


### Packet Sniffing
- **Using Airodump-ng**
- ***airodump-ng*** is part of the ***aircrack-ng***
- ***airodump-ng*** is a packet sinffer
> get the AP's MAC Address and channel
```
sudo airdump-ng wlan0mon
```





---
## Gaining Access

---

## Post Connection Attacks


## Collections

- [AboutDFIR – The Definitive Compendium Project](https://aboutdfir.com) - Collection of forensic resources for learning and research. Offers lists of certifications, books, blogs, challenges and more
- [DFIR.Training](https://www.dfir.training/) - Database of forensic resources focused on events, tools and more
- :star: [ForensicArtifacts.com Artifact Repository](https://github.com/ForensicArtifacts/artifacts) - Machine-readable knowledge base of forensic artifacts

## Tools

- [Forensics tools on Wikipedia](https://en.wikipedia.org/wiki/List_of_digital_forensics_tools)
- [Eric Zimmerman's Tools](https://ericzimmerman.github.io/#!index.md)

### Distributions

- [bitscout](https://github.com/vitaly-kamluk/bitscout) - LiveCD/LiveUSB for remote forensic acquisition and analysis
- [Remnux](https://remnux.org/) - Distro for reverse-engineering and analyzing malicious software
- [SANS Investigative Forensics Toolkit (sift)](https://github.com/teamdfir/sift) - Linux distribution for forensic analysis
- [Tsurugi Linux](https://tsurugi-linux.org/) - Linux distribution for forensic analysis
- [WinFE](https://www.winfe.net/home) - Windows Forensics enviroment

### Frameworks
