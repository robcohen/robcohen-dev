+++ 
draft = true
date = "2018-01-14T12:28:00+11:00"
title = "Setting up a Wireguard Server on Centos 7"
slug = "Setting up Wireguard on Centos 7"
tags = ["linux", "wireguard", "vpn", "centos"]
categories = ["guides", "how-to", ]
+++

## Overview
This guide will describe how to  configure Wireguard on a Centos 7 server. The configuration will be targeted towards utilizing Wireguard as a VPN service.

NOTE: This guide is not yet complete. I am going to add firewall configuration soon.

## Installing Wireguard

Up-to-date installation instructions for Wireguard is available on the official [WireGuard Installat Instructions Site](https://www.wireguard.com/install/)

## Server Setup

### Make wireguard configuration
As root:

```bash
$ mkdir /etc/wireguard
$ touch /etc/wireguard/wg0-vpn-server.conf
$ chmod 700 /etc/wireguard/wg0-vpn-server.conf
```

### Generate WireGuard keys
```bash
$ wg genkey | tee /dev/tty | wg pubkey
```

### Edit wireguard configuration

```
[Interface]
PrivateKey = <PASTE PRIVATE KEY HERE>
Address = 192.168.2.1/30
ListenPort = 51820

[Peer]
PublicKey = <PASTE PEER PUBLIC KEY HERE>
AllowedIPs = 172.16.0.0/30, 10.0.1.0/24, 10.0.2.0/24
Endpoint = x.x.x.x:51820
```

## Client Setup

### Installing Wireguard

Up-to-date installation instructions for Wireguard is available on the official [WireGuard Installat Instructions Site](https://www.wireguard.com/install/)

### Make wireguard configuration
As root:

```bash
$ mkdir /etc/wireguard
$ touch /etc/wireguard/wg0-vpn-server.conf
$ chmod 700 /etc/wireguard/wg0-vpn-server.conf
```

### Generate WireGuard keys
```bash
$ wg genkey | tee /dev/tty | wg pubkey
```


### Edit wireguard configuration

```
$ sudo wg showconf wg0 | sudo tee /etc/wireguard/wg0.conf
[Interface]
ListenPort = 51280
PrivateKey = Secret1
[Peer]
PublicKey = Wire3
AllowedIPs = 172.16.0.0/24
Endpoint = 203.0.113.30:71200
```