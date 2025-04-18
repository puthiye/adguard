# adguard

```
services:
  adguardhome: 
    image: adguard/adguardhome  
    container_name: adguardhome 
    restart: unless-stopped 
    environment:
            - TZ=Australia/Melbourne
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

     # Expose port 3000 on TCP for AdGuard Home's API
      - "3000:3000/tcp"   
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

# Block ad over WiFi
```
 In WiFi settings, configure manual DNS and point to the server where adguard service is running
```

# Block ad over cellular network
```
Login to tailscale.com -> DNS -> Global nameservers -> Raspberry Pi's unique Tailscale IP -> Enable Override DNS Servers

"Override DNS Servers" is a "global" setting that forces "all devices" in the Tailnet to use the globally configured Tailscale DNS servers, overriding their local DNS configurations. When enabled, devices ignore their existing DNS settings and always query the Tailscale-defined nameservers.

```

The iOS tailscale app will get the below DNS ip address which is the Raspberry Pi's unique Tailscale IP

![1ios_tailscale_dns](https://github.com/user-attachments/assets/48b59c02-e975-46d1-b26b-e411b13377df)



# Override blocking rules for certain domains

Adguard rules can block iOS app store and Amazon music service. To resolve this issue goto Adguard settings, add Custom Filtering
```
@@||apple.com^$important
@@||amazon.com^$important^

```


