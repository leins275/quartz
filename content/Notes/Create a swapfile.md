---
title: Create a swapfile
date: 2026-02-22
draft: false
tags: []
aliases:
---
Чтобы рассчитать размер свопа нужно вычислить

```
X * 1024 * 1024
```

Где X - число гигабайт, достаточное для размера свопфайла.

```bash
swapon -s 
sudo swapoff /dev/sdXX 
sudo nano /etc/fstab 
sudo dd if=/dev/zero of=/swapfile bs=1024 count=4194304 # 4 Gib, 8 388 608 - 8gb change count to get more 
sudo chmod 600 /swapfile 
sudo mkswap /swapfile 
sudo swapon /swapfile 
swapon -s 

/swapfile none swap sw 0 0
```

