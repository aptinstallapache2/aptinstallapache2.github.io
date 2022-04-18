---
title: Deploy web challenge Php Apache
summary: "Bài viết này dùng để ghi lại các bước cơ bản để dễ dàng deploy một thử thách web Php Apache cho team nghiên cứu."
sidebar: mydoc_sidebar
permalink: ctfd_deploy_web_challenge_php_apache.html
folder: CTFd
---

Chuẩn bị folder với cấu trúc sau:

```
php-apache
   ├── docker-compose.yml
   ├── Dockerfile
   └── index.php
```

## 1. index.php

File này chứa source code trang web chứa lỗ hổng tự tạo.

```
<html>
 <head>
  <title>PHP APACHE</title>
 </head>
 <body>
 <?php echo '<p>This site is vulnerable</p>'; ?> 
 </body>
</html>
```

## 2. Dockerfile

```
FROM php:7.2-apache
COPY . /var/www/html/
```

Giải thích thì:

|        | ý nghĩa 
| ------ | ------ 
| FROM php:7.2-apache | Lấy image từ docker hub làm môi trường chạy web. |
| COPY . /var/www/html/ | Copy toàn bộ file ở thư mục hiện tại (là 3 file ở cấu trúc folder nằm đầu trang) vào thư mục mặc định của apache /var/www/html/ |

## 3. docker-compose.yml

```
version: "3.9"
services:
    web:
        build: .
        ports:
            - "19061:80"
        volumes:
            - .:/var/www/html
```

Giải thích thì:

|        | ý nghĩa 
| ------ | ------ 
| version: "3.9" | ersion của file docker-compose (cái này giữ nguyên).  |
| services | Chứa các container. Với mỗi service là tên của một container (tên container chọn tùy ý). |
| build | Chỉ ra vị trị đường dẫn đặt Dockerfile (như trên là trỏ về thư mục hiện tại). |
| ports | Kết nối port của máy host đến port của container (như trên thì 19061 là port của máy chủ, 80 là port mặc định của dịch vụ apache bcontainer). |
| volumes | Gắn đường dẫn trên host machine được sử dụng trên container. |

## 1. Run docker-composer

`sudo docker-composer up`

Test lại bằng cách truy cập `localhost:19061`.
