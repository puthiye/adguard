# adguard

Port 53 port bind error

```

Edit /etc/systemd/resolved.conf - uncomment the line with DNSStubListener and change yes to no.

Restart systemd-resolved with sudo systemctl restart systemd-resolved.service

Fix local dns resolution by removing the symlink to the systemd stub-resolv.conf and replace it with a link to a full resolv.conf

sudo rm /etc/resolv.conf

sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf

```
