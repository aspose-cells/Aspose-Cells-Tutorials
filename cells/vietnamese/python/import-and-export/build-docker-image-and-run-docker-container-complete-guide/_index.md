---
category: general
date: 2026-06-21
description: Tìm hiểu cách tạo image Docker và chạy container Docker với việc ánh
  xạ cổng phù hợp. Bao gồm ánh xạ cổng khi chạy docker và mở cổng trong Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: vi
og_description: Xây dựng image Docker và chạy container Docker với ánh xạ cổng chính
  xác. Thành thạo việc ánh xạ cổng khi chạy Docker và mở cổng trong Docker chỉ trong
  vài phút.
og_title: Xây dựng hình ảnh Docker và chạy container Docker – Hướng dẫn toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  headline: Build Docker Image and Run Docker Container – Complete Guide
  type: TechArticle
- description: Learn how to build docker image and run docker container with proper
    port mapping. Includes docker run port mapping and expose port in docker.
  name: Build Docker Image and Run Docker Container – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Docker Engine installed (Desktop or Engine 20.10+). - Basic familiarity
      with the command line. - A tiny web app (we’ll use a one‑line Python Flask server,
      but you can swap it for anything).'
  - name: Verify the Image Exists
    text: 'Run `docker images` and look for `myflaskapp`:'
  - name: Detaching the Container (Optional)
    text: 'If you don’t want the terminal to be blocked, add `-d` to run in the background:'
  - name: Using `docker run` with Different Host Ports
    text: 'Sometimes you might already have something listening on host port 5000.
      No problem—just map to a different host port:'
  - name: Building Multi‑Stage Images (Advanced)
    text: 'If you ever need a smaller final image, you can **build docker image**
      with a multi‑stage Dockerfile:'
  type: HowTo
tags:
- docker
- containers
- devops
title: Xây dựng Image Docker và chạy Container Docker – Hướng dẫn chi tiết
url: /vi/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Xây Dựng Docker Image và Chạy Docker Container – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi làm thế nào để **build docker image** cho một ứng dụng web đơn giản và sau đó chạy nó mà không gặp rắc rối? Bạn không đơn độc—nhiều lập trình viên gặp cùng một khó khăn khi mới bắt đầu với containerization. Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình, từ việc viết Dockerfile đến việc expose cổng đúng và cuối cùng sử dụng `docker run` để ánh xạ cổng đó tới máy chủ của bạn. Khi kết thúc, bạn sẽ biết chính xác cách **run docker container** với ánh xạ cổng hợp lý, và sẽ hiểu vì sao việc expose cổng trong Docker lại quan trọng.

Chúng ta sẽ bao phủ mọi thứ bạn cần: lệnh `docker build` chính xác, cách **docker build from Dockerfile**, các chi tiết của `docker run port mapping`, và thậm chí một kiểm tra nhanh để chắc chắn container thực sự đang lắng nghe ở nơi bạn mong đợi. Không có phần thừa, chỉ có hướng dẫn thực hành, từng bước mà bạn có thể sao chép‑dán vào terminal.

## Những Điều Bạn Sẽ Đạt Được

- Viết một Dockerfile tối thiểu cho một ứng dụng Node.js (hoặc bất kỳ) nào.  
- **Build docker image** bằng cú pháp CLI chính thức.  
- Hiểu sự khác biệt giữa `EXPOSE` trong Dockerfile và cờ `-p` trong `docker run`.  
- **Run docker container** với `docker run port mapping` để bạn có thể truy cập dịch vụ tại `http://localhost:5000`.  
- Chẩn đoán các lỗi phổ biến như quên expose cổng hoặc cổng host‑container không khớp.

### Yêu Cầu Trước

- Docker Engine đã được cài đặt (Desktop hoặc Engine 20.10+).  
- Có kiến thức cơ bản về dòng lệnh.  
- Một ứng dụng web siêu nhỏ (chúng ta sẽ dùng một server Flask Python một dòng, nhưng bạn có thể thay bằng bất cứ gì).  

Nếu đã có những thứ trên, hãy bắt đầu.

---

## Bước 1: Tạo Ứng Dụng Đơn Giản

Đầu tiên, chúng ta cần một thứ để container hoá. Tạo một thư mục tên `myapp` và đặt một file duy nhất `app.py` vào trong:

```python
# app.py
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello from Docker!"

if __name__ == "__main__":
    app.run(host="0.0.0.0", port=5000)
```

> **Mẹo:** Dòng `host="0.0.0.0"` báo cho Flask lắng nghe trên mọi giao diện, đây là yêu cầu để Docker chuyển lưu lượng từ host.

Bây giờ bạn đã có một dịch vụ web siêu nhỏ lắng nghe trên cổng 5000 bên trong container.

## Bước 2: Viết Dockerfile (Docker Build from Dockerfile)

Tiếp theo, chúng ta cần một **Dockerfile** để chỉ cho Docker cách xây dựng image. Đặt file này cạnh `app.py`:

```dockerfile
# Dockerfile
FROM python:3.11-slim

# Install Flask
RUN pip install flask

# Copy our app into the image
COPY app.py /app/app.py

WORKDIR /app

# Expose the internal port (does NOT publish it yet)
EXPOSE 5000

# Default command to run the app
CMD ["python", "app.py"]
```

Một vài điểm cần lưu ý:

- `FROM python:3.11-slim` cung cấp cho chúng ta một image nền nhẹ.  
- `EXPOSE 5000` **expose port in docker** – đây là một gợi ý cho bất kỳ ai đọc Dockerfile, nhưng nó không thực sự mở cổng trên host.  
- Dòng `CMD` chạy server Flask khi container khởi động.

## Bước 3: **Build Docker Image** từ Dockerfile

Mở terminal, `cd` vào thư mục chứa Dockerfile, và chạy:

```bash
docker build -t myflaskapp .
```

Giải thích lệnh này:

- `docker build` là động từ **builds docker image** các lớp dựa trên các chỉ thị trong Dockerfile.  
- `-t myflaskapp` gắn thẻ cho image kết quả bằng một tên thân thiện mà bạn có thể tham chiếu sau này.  
- Dấu `.` ở cuối báo cho Docker dùng thư mục hiện tại làm ngữ cảnh build (nơi Docker tìm Dockerfile và mọi file bạn `COPY`).

Bạn sẽ thấy đầu ra tương tự như:

```
Sending build context to Docker daemon  3.072kB
Step 1/6 : FROM python:3.11-slim
 ---> 3b6c0f...
Step 2/6 : RUN pip install flask
 ---> Using cache
 ---> 9e2b7a...
...
Successfully built 1c2d3e4f5g6h
Successfully tagged myflaskapp:latest
```

Nếu gặp lỗi, hãy kiểm tra lại cú pháp Dockerfile và chắc chắn file `app.py` nằm trong cùng thư mục.

### Xác Nhận Image Đã Tồn Tại

Chạy `docker images` và tìm `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Bạn sẽ thấy một kết quả giống như:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Chúc mừng—bạn vừa **built docker image** thành công!

## Bước 4: **Run Docker Container** với Ánh Xạ Cổng

Bây giờ image đã sẵn sàng, đã đến lúc **run docker container** và làm cho Flask app có thể truy cập từ máy host của bạn. Dùng cờ `-p` để thực hiện **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Giải thích:

- Số `5000` đầu tiên (bên trái) là **cổng host**.  
- Số `5000` thứ hai (bên phải) là **cổng container** mà chúng ta đã expose trước đó.  
- Docker sẽ chuyển lưu lượng từ `localhost:5000` trên máy của bạn tới cổng 5000 bên trong container.

Bạn sẽ thấy log khởi động của Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Mở trình duyệt và truy cập `http://localhost:5000`. Bạn sẽ thấy “Hello from Docker!”—container đang phục vụ lưu lượng đúng như mong đợi.

### Tách Container Ra (Tùy Chọn)

Nếu bạn không muốn terminal bị chiếm, thêm `-d` để chạy ở nền:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Bạn có thể dừng nó sau này bằng `docker stop <container-id>`.

## Bước 5: Đi Sâu – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Rất dễ nhầm lẫn giữa chỉ thị `EXPOSE` và cờ `-p`, nhưng chúng có mục đích khác nhau:

| Concept | What it does | Does it open the port on the host? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | Documents which ports the container *intends* to listen on. | **No** – just metadata. |
| `-p host:container` (docker run) | Creates a NAT rule that forwards traffic from the host port to the container port. | **Yes** – actual port forwarding. |

Nếu bạn quên `EXPOSE`, lệnh `docker run -p` vẫn hoạt động, nhưng bạn sẽ mất tài liệu hữu ích cho những người dùng sau. Ngược lại, nếu chỉ `EXPOSE` mà không bao giờ dùng `-p`, dịch vụ sẽ không thể truy cập từ host.

### Sử Dụng `docker run` với Các Cổng Host Khác Nhau

Đôi khi bạn đã có một dịch vụ đang lắng nghe trên cổng host 5000. Không sao—chỉ cần ánh xạ sang một cổng host khác:

```bash
docker run -p 8080:5000 myflaskapp
```

Bây giờ app có thể truy cập tại `http://localhost:8080`, trong khi vẫn lắng nghe trên 5000 bên trong container. Sự linh hoạt này là một trong những điểm mạnh cốt lõi của **docker run port mapping**.

## Bước 6: Các Vấn Đề Thường Gặp & Trường Hợp Cạnh

| Issue | Symptom | Fix |
|-------|---------|-----|
| Forgetting `EXPOSE` | New developers can’t tell which port to map. | Add `EXPOSE 5000` (or whatever your app uses). |
| Using the wrong host port | Browser returns “connection refused”. | Verify the left side of `-p` matches the port you’re trying to reach. |
| Container crashes on start | No logs, container exits instantly. | Run `docker logs <container-id>` to see error messages; often caused by missing dependencies or wrong `CMD`. |
| Port already in use on host | Docker prints “bind: address already in use”. | Choose a different host port (`-p 8080:5000`). |
| Not binding to `0.0.0.0` | Service only reachable from inside container. | In Flask, set `host="0.0.0.0"`; other frameworks have similar settings. |

### Xây Dựng Multi‑Stage Image (Nâng Cao)

Nếu bạn cần một image cuối cùng nhỏ hơn, bạn có thể **build docker image** bằng Dockerfile đa giai đoạn:

```dockerfile
# Stage 1: Build
FROM python:3.11-slim AS builder
RUN pip install --target=/app flask
COPY app.py /app/

# Stage 2: Runtime
FROM python:3.11-slim
COPY --from=builder /app /app
WORKDIR /app
EXPOSE 5000
CMD ["python", "app.py"]
```

Kỹ thuật này loại bỏ các lớp thời gian build, tạo ra một image gọn nhẹ hơn—rất phù hợp cho môi trường production.

## Bước 7: Dọn Dẹp

Khi bạn đã thử nghiệm xong, hãy dọn dẹp:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Việc dọn dẹp ngăn ngừa việc chiếm dụng đĩa và giữ môi trường Docker của bạn luôn gọn gàng.

---

## Kết Luận

Bạn giờ đã có một quy trình toàn diện từ **build docker image** tới **run docker container** với **docker run port mapping** đúng cách. Khi hiểu cách **expose port in docker** và cách cờ `-p` thực sự chuyển lưu lượng, bạn có thể tự tin container hoá bất kỳ dịch vụ nào và làm cho nó có thể truy cập từ host hoặc mạng rộng hơn.

Tiếp theo bạn muốn làm gì? Hãy thử thay Flask bằng một binary Go, thêm biến môi trường bằng `-e`, hoặc đẩy image mới xây dựng lên Docker Hub bằng `docker push`. Bầu trời là giới hạn, và bạn vừa sở hữu một siêu năng lực mới trong thế giới DevOps.

Happy container


## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}