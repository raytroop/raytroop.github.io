---
title: network connection using nmcli
date: 2022-04-01 01:05:40
tags:
- nmcli
categories:
- devops
---

#### Problem

There is no network connection and device is not managed


```
$ nmcli device status 
DEVICE  TYPE      STATE      CONNECTION            
eth0    ethernet  unmanaged  --  
lo      loopback  unmanaged  --  
```

![image-20220401011509900](rocky-nmcli-network/image-20220401011509900.png)

#### solution

```bash
sudo nmcli networking on
```

Then, **eth0** is connected

```
$ nmcli device status 
DEVICE  TYPE      STATE      CONNECTION            
eth0    ethernet  connected  Ethernet connection 1 
lo      loopback  unmanaged  --  
```

![image-20220401011543866](rocky-nmcli-network/image-20220401011543866.png)



