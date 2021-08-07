---
title: "Docker Python Django"
date: 2021-08-02T10:42:35+07:00
draft: false
image: docker-django.jpg
tags:
    - Docker
    - Docker-Compose
    - Python
    - Django
    - SSH
categories:
    - Tutorials
---

## Cấu hình Ubuntu Server

```
ssh e.bui@13.76.175.68
sudo apt-get update
```

## Cài đặt môi trường

### Cài đặt Docker
Cài đặt Docker trên Ubuntu
```
curl -sSL https://get.docker.com | sudo -E sh
sudo systemctl enable --now docker.service docker.socket
sudo usermod -aG docker ebui
sudo reboot
```

Kiểm tra Docker
```
docker version
```

### Cài đặt Docker Compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```
Kiểm tra docker-compose
```
docker-compose version
```

### Thiếp lập components cho project

Tạo thư mục chứa project
```
mkdir dopydj && cd dopydj
```

Tạo `Dockerfile`
```
# syntax=docker/dockerfile:1
FROM python:3
ENV PYTHONUNBUFFERED=1
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/
```

Tạo file `requirements.txt`
```
Django>=3.0,<4.0
psycopg2-binary>=2.8
```

Tạo file `docker-compose.yml`
```yaml
version: "3.9"
   
services:
  db:
    image: postgres
    volumes:
      - ./data/db:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=postgres
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - ./code:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
```

Tạo Django project

```bash
docker-compose run web django-admin startproject mysite .

sudo chown -R $USER:$USER .
```

Kết nối Database
```python
# settings.py
   
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```
Chạy docker-compose trên Ubuntu
```
docker-compose up
```

> Chú ý nếu lỗi thì `ALLOWED_HOSTS = ['*']`

## Một số lỗi thường gặp

- Cài đặt Docker
  - Thiếu permision. Cần cấp permision cho user qua lệnh `usermod -aG docker USER`
- Cài đặt Django
  - Lỗi không kết nối được Database. Cần chú ý đến file `settings.py`
  - Lỗi không kết nối được tới Web. Cần chú ý đến `ALLOWED_HOSTS`

## Tham khảo

https://docs.docker.com/samples/django/

https://docs.docker.com/engine/install/ubuntu/

https://docs.docker.com/compose/install/
