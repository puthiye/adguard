# adguard

```
services:
  adguardhome:
    image: adguard/adguardhome
    container_name: adguardhome
    restart: unless-stopped
    ports:
      # Expose port 53 on TCP and UDP for DNS queries
      - "53:53/tcp"
      - "53:53/udp"

      # Expose port 68 on UDP for DHCP client
      # - "68:68/udp"

      # Expose port 80 on TCP for HTTP web interface
      - "80:80/tcp"

      # Expose port 443 on TCP and UDP for HTTPS web interface
      - "443:443/tcp"
      - "443:443/udp"
    volumes:
      - /etc/adguard/work:/opt/adguardhome/work
      - /etc/adguard/confdir:/opt/adguardhome/conf
```

Port 53 port bind error

```

Edit /etc/systemd/resolved.conf - uncomment the line with DNSStubListener and change yes to no.

Restart systemd-resolved with sudo systemctl restart systemd-resolved.service

Fix local dns resolution by removing the symlink to the systemd stub-resolv.conf and replace it with a link to a full resolv.conf

sudo rm /etc/resolv.conf

sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

```
