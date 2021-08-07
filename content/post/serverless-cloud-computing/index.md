---
title: "Serverless Cloud Computing"
date: 2021-08-03T16:46:32+07:00
draft: false
tags:
    - Gitlab
    - Docker
    - Aliyun
    - Alibaba Cloud
    - Function Compute
    - Serverless
categories:
    - Logs
image: serverless.jpg
---

## Cài đặt môi trường

**Dưới máy tính (Local)**

### Cài đặt Git

```bash 
yum install git

git clone <project>
```

### Cài đặt Funcarft

Tải Funcraft mới nhất [ở đây](https://github.com/alibaba/funcraft/releases)
```
curl -o fun-linux.zip http://funcraft-release.oss-accelerate.aliyuncs.com/fun/fun-v3.6.20-linux.zip

sudo yum install unzip
sudo unzip fun-linux.zip

sudo mv fun-v3.6.20-linux /usr/local/bin/fun

fun --version
```

Cấu hình Funcraft
```
fun config
```

### Cài đặt Docker

```bash
curl -sSL https://get.docker.com | sudo -E sh
sudo usermod -aG docker $(whoami)

# if you have not permission
sudo su -
touch /etc/sudoers.d/client
user_name   ALL=(ALL)  ALL

# docker command
sudo systemctl enable --now docker
sudo systemctl start docker
```

## Cấu hình cho project

```
fun install

cp config.py.example config.py

fun local invoke

fun deploy
```

## Tham khảo

- [How to install Funcraft](https://www.alibabacloud.com/help/doc-detail/161136.htm)
- [Configure Funcraft](https://www.alibabacloud.com/help/doc-detail/146702.htm)
- [How to use Funcraft to create a function](https://www.alibabacloud.com/help/doc-detail/155100.htm)