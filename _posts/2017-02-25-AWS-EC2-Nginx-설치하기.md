---
layout: post
title: AWS EC2 Nginx 설치하기
date: 2017-02-25 00:00:00
categories: AWS
---

설치 하기에 앞서 AWS EC2 Instance가 준비되어야 합니다.

## 필수 패키지 설치

```
sudo yum install -y pcre-devel zlib-devel openssl-devel gcc gcc-c++ make
```

## Nginx 설치

```
wget http://nginx.org/download/nginx-1.10.3.tar.gz
tar zxvf nginx-1.10.3.tar.gz
cd nginx-1.10.3
./configure \
    --user=ec2-user \
    --group=ec2-user \
    --prefix=/home/ec2-user/nginx \
    --sbin-path=/home/ec2-user/nginx/sbin/nginx \
    --conf-path=/home/ec2-user/nginx/conf/nginx.conf \
    --pid-path=/home/ec2-user/nginx/pid/nginx.pid \
    --with-http_ssl_module \
    --with-pcre \
make
make install
```

## Nginx 시작

```
cd /home/ec2-user/nginx/sbin
./nginx
```

## AWS EC2 방화벽 추가 (Security Groups 설정)

1. EC2 Console 화면 진입
2. Create Security Group 클릭
3. Security Groups 한가지 선택 마우스 오른쪽 클릭 > Copy to new 클릭
4. Inbound에 http 추가 > Create 클릭

## AWS EC2 방화벽 활성화

1. EC2 Console 화면 진입
2. Instances 클릭
3. Instance 선택 마우스 오른쪽 클릭 > Networking > Change Security Groups 클릭
4. 위에서 만든 Security Group 선택
5. Assign Security Groups 클릭

## 접속 확인

Instance에 있는 IPv4 Public IP를 확인한 후 접속해보자.
Hello World가 나올 것이다.
