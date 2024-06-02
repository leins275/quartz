---
title: Скрипты автоматизации работы с wireguard
draft: false
tags: 
aliases:
---
# Введение

Сейчас vpn актуален как никогда. В этой статье я хочу вставить свои 5 копеек в дополнение к статье `devpew`, предложив несколько
полезных скриптов по утилизации установки вайргарда на сервер с ubuntu и созданием клиентов.

# Как пользоваться

[Ссылка](https://devpew.com/blog/wireguard/) на сайт с описанием вайргарда и как его настраивать. Ниже приведу выжимки и практические кейсы.

# Автоматизированный скрипт для установки

Этот скрипт настроит wireguard за вас на чистом сервере с ubuntu 20.04, и вам останется только добавить клиентов при помощи 
следующего скрипта.

```bash
#!/usr/bin/env bash

apt update -y
apt upgrade -y
apt install -y wireguard qrencode

echo "net.ipv4.ip_forward=1" >> /etc/sysctl.conf
sysctl -p

wg genkey | tee /etc/wireguard/privatekey | wg pubkey | tee /etc/wireguard/publickey
server_priv_key=`cat "/etc/wireguard/privatekey"`

echo "[Interface]
Address = 10.0.0.1/24
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
ListenPort = 51820
PrivateKey = $server_priv_key
" > /etc/wireguard/wg0.conf

systemctl enable --now wg-quick@wg0

echo "2" > /etc/wireguard/.loc
```

# Скрипт по автоматизации создания клиентов

Этот скрипт вас спасет, если вы хотите создавать много клиентов "для всей семьи", друзей и знакомых.
Использовать так: `./useradd.sh vasja_pupkin_0`
Скрипт сделает за вас всю работу по созданию нового клиента, создаст ему конфиг и покажет qr код.


```bash
#!/usr/bin/env bash

username=$1
serverip=`curl -s https://icanhazip.com`
serverpubkey=`cat "/etc/wireguard/publickey"`

wg genkey | tee "/etc/wireguard/$username" | wg pubkey | tee "/etc/wireguard/$username""_pub"

pubkey=`cat "/etc/wireguard/$username""_pub"`
privatekey=`cat "/etc/wireguard/$username"`

ip_last=`cat /etc/wireguard/.loc`
echo "$(($ip_last+1))" > /etc/wireguard/.loc

echo "# $username
[Peer]
PublicKey = $pubkey
AllowedIPs = 10.0.0.$ip_last/32" >> /etc/wireguard/wg0.conf

systemctl restart wg-quick@wg0

echo "[Interface]
PrivateKey = $privatekey
Address = 10.0.0.$ip_last/32
DNS = 8.8.8.8

[Peer]
PublicKey = $serverpubkey
Endpoint = $serverip:51820
AllowedIPs = 0.0.0.0/0
PersistentKeepalive = 20" > "/etc/wireguard/$username.conf"

qrencode -t ansiutf8 < "/etc/wireguard/$username.conf"
```

# Автоподключение vpn gnome3

Это должно вам помочь, если вы используете третий гном и хотите, чтобы после включения или разблокировки компьютера 
он подключался к vpn автоматически.

```bash
nmcli connections show
# then just copy ID of vpn connection
nmcli connection edit "<Name of your internet connection>"
print connection.secondaries
set connection.secondaries <ID of vpn connection>
save
quit
```


