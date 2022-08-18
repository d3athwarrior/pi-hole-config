# pi-hole-config

The pi-hole.yml file captures the configuration that needs to be made in order to run pi-hole on a Ubuntu server 20.04.4 LTS release.

## Issues
1. The pi hole container fails to start in case I am using an IP address to bind the port 53 so that the host system's DNS service can keep on running as it did before. There is a conflict between the host's systemd-resolved configuration and the pi-hole wanting to bind to port 53 on the host for DNS services.  
   In order to solve this issue, the guide listed on [Dokcer github](https://github.com/pi-hole/docker-pi-hole#installing-on-ubuntu) needs to be followed.  
   The host server needs to stop using the stub resolve.conf and start to use the actual one which gets impacted by the netplan modifications. The symlink in `/etc/resolv.conf` should be changed to point to the actual configuration in `/run/systemd/resolve/resolv.conf`  
   The netplan needs to be updated with a static IP and DNS configuration so that the pi-hole can safely bind to the host on port 53 without conflict.
