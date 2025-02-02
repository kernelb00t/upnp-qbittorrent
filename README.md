# upnp-qbittorrent
A Dockerfile to keep Qbittorrent up to date with reverse proxy ports. Keep in mind that this project is specially targeted at Proton VPN; though I can accept other services if no big 

## How it is working
Proton VPN has a port forwarding service. Using Wireguard, you have a command to run each 60s to renew the forwarded port. The problem is, when restarting the VPN or the Docker host, you will lose the port because you didn't renew the port. 

This script aims to solve this problem by:
1. Get the old port set on the Qbittorrent panel
2. Ask for renewal. The output of the command throws the port with too much info. That need to be parsed.
3. Parse the output to get the new port.
4. If the port changed, call the Qbittorrent API to change it and store the new port.
5. Sleep 45s (15s of safety, this can be adjusted) and restart at step 2.

## Requirements
1. A Docker host
2. A VPN service like Proton VPN
3. A Docker VPN client like [linuxserver/wireguard](https://docs.linuxserver.io/images/docker-wireguard/)

## Get it installed
1. Get the Dockerfile and the update.sh script. Those 2 files are the only necessary ones. If you have a Docker Compose config, it is recommended to put these in a folder to keep it tidy.
