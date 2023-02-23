# Network Hacking [![Link Status](https://github.com/cugu/awesome-forensics/workflows/CI/badge.svg)](https://github.com/suhailm-in/Network-Hacking)

**Network Hacking** and forensic analysis tools and resources.

- [Network Hacking ](#network-hacking-)

  - [Network Basics](#network-basics)
    - [MAC Address Changing](#mac-address-changing)
    - [Wireless Mode Changing](#wireless-mode-changing)

    
  - [Pre Connection Attacks](#pre-connection-attacks)
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
> Managed mode - Monitor mo
- see all interface
- desable interface
- check for any conflicting process and kill them
- monitore mode enable
- enable interface
- see wireless interface only

```
ifconfig
ifconfig wlan0 down
airmon-ng check kill
iwconfig wlan0 mode monitor
ifconfig wlan0 up
iwconfig
```


---
## Pre Connection Attacks

## Gaining Access

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
