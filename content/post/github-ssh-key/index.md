---
title: "Github SSH Key"
date: 2021-08-01T21:49:19+07:00
draft: false
tags:
    - Github
    - SSH
categories:
    - Tutorials
image: 2021-08-02_064106.png
---

## Tạo SSH key

```
mkdir sshforgithub
ssh-keygen -t rsa -f id_rsa
ls -la sshforgithub
```

## Thêm SSH key vào trong Github

Truy cập https://github.com/settings/keys

![](2021-08-02_064106.png)

Thêm public key vào trong Github
![](2021-08-02_064132.png)

Nhập mật khẩu của Github để xác thực.
![](2021-08-02_064155.png)

## Thiết lập SSH trên máy tính

Di chuyển key vào trong thư mục SSH, cụ thể là `.ssh`
```
mv id_rsa ~/.ssh
```

Thêm dòng sau vào ~/.ssh/config
```
# My Github
Host github.com
        User git
        Hostname github.com
        Port 22
        PreferredAuthentications publickey
        IdentityFile    ~/.ssh/id_rsa
```

Thêm repo remote vào trong project
```
git remote -v
git remote add github git@github.com:tribuivant/tribuivant.github.io.git
git push github master
```