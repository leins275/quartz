---
title: UFW firewall
date: 2024-10-02
---
# How to enable UFW firewall
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing

sudo ufw allow ssh
sudo ufw allow http
sudo ufw allow https

sudo ufw enable
```

- [[UFW rules for its outline]]
- [Source](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-ubuntu-20-04)