---
title: Deploy web challenge Flask
summary: "Bài viết này dùng để ghi lại các bước cơ bản để dễ dàng deploy một thử thách web Flask cho team nghiên cứu."
sidebar: mydoc_sidebar
permalink: ctfd_deploy_web_challenge_flask.html
folder: CTFd
---

Chuẩn bị folder với cấu trúc sau:

```
web-flask
  ├── templates/
  │   ├── vuln.html
  ├── docker-compose.yml
  ├── Dockerfile
  ├── app.py
  └── requirements.txt
```

## 1. vuln.html

```
<html>
     <body>
   
      <h1>This site is vulnerable</h1>
      
   </body>
</html>
```

## 2. app.py

```
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/')
def vuln():
   return render_template('vuln.html')

if __name__ == '__main__':
   app.run()
```

## 3. requirements.txt

```
Flask
```

## 4. Dockerfile

```
FROM python:3.7-alpine

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD [ "python", "./app.py" ]
```

Giải thích thì:

|        | ý nghĩa 
| ------ | ------ 
| FROM python:3.7-alpine | Lấy image từ docker hub làm môi trường chạy web. |
| WORKDIR | Trỏ vào thư mục làm việc. |
| COPY | Copy file từ source vào destination (source là thư mục hiện tại, destination là thư mục bên trong docker) |
| RUN | Chạy lệnh khi build image. |
| CMD | Chỉ cho Docker biết lệnh nào sẽ được chạy khi container bắt đầu được chạy. |

## 3. docker-compose.yml

```
version: "3.9"
services:
    web-flask:
        build: .
        ports:
            - "19062:5000"
        volumes:
            - .:/usr/src/app
```

Giải thích thì:

|        | ý nghĩa 
| ------ | ------ 
| version: "3.9" | Version của file docker-compose (cái này giữ nguyên).  |
| services | Chứa các container. Với mỗi service là tên của một container (tên container chọn tùy ý). |
| build | Chỉ ra vị trị đường dẫn đặt Dockerfile (như trên là trỏ về thư mục hiện tại). |
| ports | Kết nối port của máy host đến port của container (như trên thì 19062 là port của máy chủ, 5000 là port mặc định của dịch vụ flask). |
| volumes | Gắn đường dẫn trên host machine được sử dụng trên container. |

## 4. Run docker-composer

`sudo docker-composer up`

Test lại bằng cách truy cập `localhost:19062`.
