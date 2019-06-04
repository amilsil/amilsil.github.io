---
layout: post
title: How To Run A Script After Network Initialisation on Raspbian
tags:
- raspbian-lite
- bash
- systemctl
---

I have a raspberry pi configured to share my wifi internet through the ethernet port, so that I can turn my dump ethernet printer to a wifi accessible one.

I do this by using the setup guide at https://www.instructables.com/id/Share-WiFi-With-Ethernet-Port-on-a-Raspberry-Pi/.

There's a script that I have to run for internet sharing to kick off at https://raw.githubusercontent.com/arpitjindal97/raspbian-recipes/master/wifi-to-eth-route.sh.

But I also want to run this script after the network initialisation of raspbian lite. This is how I could do this.

## Create a Systemd Service

Go to **/etc/systemd/system/**.

Create a new service by the name **start-internet-sharing.service** and add the following in there.

```
[Unit]
Description=Start Sharing Internet
Wants=network-online.target
After=network-online.target

[Service]
ExecStart=/etc/init.d/wifi-to-eth-route.sh

[Install]
WantedBy=multi-user.target
```

Note: I have the above script downloaded at `/etc/init.d/wifi-to-eth-route.sh`
**Wants** and **After** above will declare the requirement and the event to run the script on.

That's it. Restart the rpi and whatever the script you want to run will run after network initialisation.
