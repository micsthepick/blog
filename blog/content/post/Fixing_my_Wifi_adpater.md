---
title: "Fixing my Wifi Adapter"
date: 2025-06-14
tags: ["hardware", "networking", "drivers", "troubleshooting"]
---

# Fixing my Wifi Adapter
I happen to have a TP Link Branded Adapter (T3U, but this fix should work on a variety of devices)  
It turns out that a common problem is that it doesn't use USB 3, and when I create a PAN (personal area network) - even if I set it to prefer 5GHz, the speed was abysmally slow.  

I searched for quite a while for a fix, and finally stumbled on this beta driver from this TP-LINK post: <a href="https://community.tp-link.com/en/home/forum/topic/653702">Archer T3U Plus is causing BSOD when using a hotspot on Windows 11.</a>  

The install is fairly simple, extract the zip, and run Setup.exe.

## DISCLAIMER:
The above driver is beta, I can't offer a warranty that everything will work, and you'd have to ask TP-LINK directly if you aren't sure about it, and also there may evntually be a driver update more recent (or perhaps there already is, as I stopped once I found a working solution).  

in case the link rots I've also saved a web archive capture:
```
/web/20250614112350/https://static.tp-link.com/upload/beta/2022/202206/20220601/Realtek_WLAN_1030.44.0531.2021_Win20H1_RS1_Archive3_DUA_0530_U2U3.zip
```
(web.archive.org)

## before / after
before:  

consistently less than 50mbps with iperf3 direct ip access and a 5GHz hotspot to my Quest 3 512Gb. (Even the home router beats it ~min100 ~max150 ~avg130 with the 5GHz network it provides if I use the internal ip of my PC on that router)  

after: 

<div class="text-center">
  <figure class="figure">
    <img src="../../usbtreeview_wifi_adapter.png" alt="USBTreeView depicts losing a HighSpeed device, and gaining a SuperSpeed device - which is the TP-LINK" style="max-height:400px;"/>
    <figcaption class="figure-caption" style="margin-bottom: 1em;">USBTreeview</figcaption>
  </figure> 
</div>
as pictured above, the device stays in USB 3 mode.  

Rates:
```
[  5]   0.00-1.01   sec  20.4 MBytes   169 Mbits/sec
[  5]   1.01-2.01   sec  15.1 MBytes   127 Mbits/sec
[  5]   2.01-3.01   sec  10.4 MBytes  87.1 Mbits/sec
[  5]   3.01-4.01   sec  11.1 MBytes  93.6 Mbits/sec
[  5]   4.01-5.01   sec  20.5 MBytes   173 Mbits/sec
[  5]   5.01-6.00   sec  15.5 MBytes   130 Mbits/sec
[  5]   6.00-7.00   sec  19.2 MBytes   161 Mbits/sec
[  5]   7.00-8.00   sec  16.1 MBytes   136 Mbits/sec
[  5]   8.00-9.00   sec  17.0 MBytes   143 Mbits/sec
[  5]   9.00-10.02  sec  23.1 MBytes   191 Mbits/sec
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-10.02  sec   168 MBytes   141 Mbits/sec                  receiver
```
whilst I didn't record the rates from before changing drivers except by memory, there is at least a 3x improvement over the non-updated version, however if I compare it to the hoem wireless network, it barely eeks out an extra 10 Mbits out of 140 on average - perhaps not insiginificant, but I would not call it statistically significant without doing further testing.  

However the one big benefit to using the Ad-hoc hotspot, is that I can Isolate my quest 3 from the home wifi plus it stays connected to my pc directly, and doesn't migrate to the satellite AP, which would mean horrible speed and latency.
