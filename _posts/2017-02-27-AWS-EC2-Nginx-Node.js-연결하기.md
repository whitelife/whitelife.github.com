---
layout: post
title: AWS EC2 Nginx Node.js 연결하기
date: 2017-02-27 00:00:00
categories: AWS
---

Nginx, Node.js가 설치되어 있어야합니다.

## Nginx location 설정

~/nginx/conf 추가, server 영역 안에 추가해야합니다.

```
location /nodejs {
    proxy_pass  http://127.0.0.1:3000;
    proxy_set_header Host       $host;
    proxy_set_header X-Real-IP  $remote_addr;
}
```

## Node.js Application 추가

~/projects/helloworld/helloworld.js

```javascript
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World\n');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
```

## Node.js Application 실행

```
node ~/projects/helloworld/helloworld.js
```

## Http 요청하기

- [http://whitelife.co.kr/nodejs](http://whitelife.co.kr/nodejs)


