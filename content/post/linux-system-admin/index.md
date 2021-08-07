---
title: "Linux System Admin"
date: 2021-08-02T20:40:48+07:00
draft: false
image: linux.jpg
tags:
    - Linux
categories:
    - Sharing
    - Learn
---

## Kiểm tra thông tin phần cứng

Kiểm tra `RAM`
```bash
free -h
```

Kiểm tra `CPU`
```bash
lscpu
```

Kiểm tra thông tin ổ đĩa
```bash
lsblk
df -hT
```

## Kiểm tra thông tin phần mềm

Kiểm tra các dịch vụ đang chạy
```bash
systemctl
```

## Kiểm tra kết nối

Dùng lệnh `curl`
```
curl
curl -Iv https://google.com
```

Dùng lệnh `wget`
```
wget
```

Dùng lệnh `netstat`
```
netstat -tlpn
```

Dùng lệnh `telnet`
```
telnet 127.0.0.0 80
```

Dùng lệnh `ping`
```
ping google.com
ping 8.8.8.8
```

## Công cụ cần thiết

Dùng tmux
```
tmux new -s section-name
```