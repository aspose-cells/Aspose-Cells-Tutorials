---
category: general
date: 2026-06-21
description: Mở cổng container trong Docker đồng thời thiết lập thư mục làm việc và
  sao chép mã nguồn ứng dụng của bạn. Tìm hiểu cách docker hoá một API Python từng
  bước.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: vi
og_description: Mở cổng container trong Docker, đặt thư mục làm việc và sao chép mã
  nguồn của bạn vào container. Hướng dẫn này cho thấy cách docker hoá một API Python.
og_title: Mở Cổng Container trong Docker – Hướng Dẫn Toàn Diện
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  headline: Expose Container Port in Docker – Full Dockerfile Guide
  type: TechArticle
- description: Expose container port in Docker while setting the working directory
    and copying your app source. Learn how to dockerize a Python API step‑by‑step.
  name: Expose Container Port in Docker – Full Dockerfile Guide
  steps:
  - name: 1. Changing the Host Port
    text: 'Sometimes port 5000 is already in use on your machine. No problem—just
      change the host side of the mapping:'
  - name: 2. Multi‑Stage Builds for Smaller Images
    text: If you don’t need the full Aspose.Cells runtime in production, you can create
      a multi‑stage build that compiles assets in a heavy image then copies only the
      runtime bits into a lightweight `python:3.11-slim` final stage. This reduces
      the final image size dramatically.
  - name: 3. Using Docker Compose
    text: 'For more complex setups (e.g., a database alongside the API), put the same
      instructions into a `docker-compose.yml`:'
  - name: 4. Environment Variables
    text: 'If your API needs configuration (like a secret key), pass them at runtime:'
  type: HowTo
- questions:
  - answer: Check the logs with `docker logs api_container`. A common mistake is forgetting
      `host="0.0.0.0"` in Flask.
    question: Container exits immediately?
  - answer: Verify with `docker ps` and `netstat -tulpn`. Use a different host port
      as shown above.
    question: Port already in use?
  - answer: Ensure your `requirements.txt` is present before the `RUN pip install`
      step, or add the packages directly in the Dockerfile.
    question: Missing dependencies?
  type: FAQPage
tags:
- Docker
- Python
- API
title: Mở Cổng Container trong Docker – Hướng Dẫn Dockerfile Toàn Diện
url: /vi/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mở Cổng Container trong Docker – Hướng Dẫn Dockerfile Đầy Đủ

Bạn đã bao giờ tự hỏi làm thế nào để **expose container port** khi đang container hoá một Python API chưa? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển đều gặp phải vấn đề này: ứng dụng chạy tốt trên máy local, nhưng khi chạy trong Docker, bên ngoài không thể truy cập được. Trong tutorial này, chúng ta sẽ đi qua một Dockerfile hoàn chỉnh không chỉ **expose container port** mà còn **set working directory docker**, **dockerfile copy app**, và **copy source into container**—tất cả những gì bạn cần để **dockerize python api** mà không gặp khó khăn.

Chúng ta sẽ bắt đầu với một ứng dụng Flask siêu nhẹ, sau đó xây dựng một image Docker từ đầu, giải thích từng lệnh, và cuối cùng chạy container để bạn có thể truy cập `http://localhost:5000/health`. Khi kết thúc, bạn sẽ có một Docker image sẵn sàng cho môi trường production và có thể đẩy lên bất kỳ registry nào.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- Docker Engine ≥ 20.10 được cài đặt (Docker Desktop hoạt động tốt trên Windows/macOS, Docker Engine trên Linux).
- Kiến thức cơ bản về Python và Flask (hoặc bất kỳ framework WSGI‑compatible nào).
- Một trình soạn thảo văn bản hoặc IDE (VS Code, PyCharm, v.v.) để chỉnh sửa Dockerfile và code Python.

Không cần thêm bất kỳ thư viện nào ngoài những gì image **Aspose.Cells Python.NET base** chính thức cung cấp.

## Step 1: Create a Minimal Python API

Đầu tiên, hãy viết một dịch vụ Flask siêu nhỏ mà chúng ta sẽ **dockerize python api** sau này. Lưu file này dưới tên `api_server.py` trong một thư mục trống.

```python
# api_server.py
from flask import Flask, jsonify

app = Flask(__name__)

@app.route("/health")
def health():
    return jsonify(status="OK", message="API is running")

if __name__ == "__main__":
    # Listen on all interfaces so Docker can forward the port
    app.run(host="0.0.0.0", port=5000)
```

Tại sao lại dùng `host="0.0.0.0"`? Trong container, `localhost` chỉ đề cập tới chính container. Gán địa chỉ `0.0.0.0` sẽ khiến Flask chấp nhận kết nối từ bất kỳ giao diện mạng nào, điều này rất quan trọng cho bước **expose container port** sau này.

## Step 2: Choose the Right Base Image

Trong ví dụ này, chúng ta sẽ sử dụng **Aspose.Cells Python.NET base image** chính thức của Aspose (`aspose/cells-pythonnet:6.22`). Image này đã bao gồm .NET runtime, Python 3.9 và thư viện Aspose.Cells—rất phù hợp nếu API của bạn cần thao tác với Excel.

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

Nếu bạn không cần Aspose, có thể thay thế bằng `python:3.11-slim`. Các phần còn lại của Dockerfile vẫn giữ nguyên.

## Step 3: **Dockerfile Copy App** – Copy Your Source Into the Container

Tiếp theo, chúng ta cần đưa mã nguồn vào image. Đây là nơi lệnh **dockerfile copy app** tỏa sáng.

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

Dấu `.` đại diện cho build context—thư mục nơi bạn chạy `docker build`. Khi sao chép toàn bộ, bạn cũng đưa vào `requirements.txt` (nếu có) và bất kỳ tài nguyên tĩnh nào. Nếu muốn image gọn hơn, bạn có thể liệt kê chỉ những file thực sự cần thiết.

## Step 4: **Set Working Directory Docker** – Define the Working Directory

Sau khi sao chép, chúng ta chỉ định cho Docker nơi thực thi các lệnh tiếp theo. Đây là bước **set working directory docker**.

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

Tại sao lại làm như vậy? Nó giúp bạn tránh việc phải gõ đường dẫn đầy đủ sau này (ví dụ `python api_server.py` thay vì `python /app/api_server.py`). Đồng thời, nó làm cho cấu trúc hệ thống file trong container trở nên rõ ràng hơn cho bất kỳ ai đọc image sau này.

## Step 5: Install Python Dependencies (Optional but Recommended)

Nếu API của bạn phụ thuộc vào các package bên ngoài, hãy tạo một file `requirements.txt` và cài đặt chúng trong một layer riêng. Điều này cải thiện khả năng cache.

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

Câu lệnh có điều kiện đảm bảo quá trình build sẽ không thất bại nếu bạn không có `requirements.txt`—rất tiện cho ví dụ tối thiểu ở trên.

## Step 6: **Expose Container Port** – Make the API Reachable from Outside

Bây giờ chúng ta đến phần quan trọng nhất: **expose container port**. Lệnh này thông báo cho Docker biết container sẽ lắng nghe cổng nào, cho phép ánh xạ cổng khi chạy.

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

Lưu ý rằng `EXPOSE` chỉ là một gợi ý tài liệu; việc ánh xạ thực tế diễn ra khi bạn chạy `docker run -p`. Tuy nhiên, việc khai báo cổng là một best practice và giúp các công cụ như Docker Compose tự động chuyển tiếp cổng đúng.

## Step 7: Define the Startup Command

Cuối cùng, chúng ta chỉ định cho Docker cách khởi chạy API. Đây là lệnh `CMD`.

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

Sử dụng dạng mảng JSON tránh các vấn đề khi Docker thực thi qua shell và làm cho lệnh trở nên di động hơn.

## Full Dockerfile Recap

Kết hợp tất cả các phần lại, đây là Dockerfile hoàn chỉnh mà bạn có thể sao chép‑dán:

```dockerfile
# Step 1: Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22

# Step 2: Copy your application source code into the container
COPY . /app

# Step 3: Set the working directory to the application folder
WORKDIR /app

# Optional: Install Python dependencies if you have a requirements file
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi

# Step 4: Expose the port your API server will listen on
EXPOSE 5000

# Step 5: Define the command to start the API server
CMD ["python", "api_server.py"]
```

> **Pro tip:** Đặt dòng `COPY` *trước* dòng `RUN pip install` nếu bạn có nhiều dependencies. Docker sẽ cache layer chứa các package đã cài, vì vậy khi rebuild sau khi thay đổi code, Docker sẽ không phải cài lại toàn bộ.

## Step 8: Build the Docker Image

Mở terminal trong thư mục chứa `Dockerfile` và `api_server.py`, sau đó chạy:

```bash
docker build -t my-python-api .
```

Docker sẽ stream từng bước, hiển thị các layer được cache nếu có. Nếu mọi thứ diễn ra suôn sẻ, bạn sẽ thấy `Successfully tagged my-python-api:latest`.

## Step 9: Run the Container and Verify the Port Mapping

Bây giờ khởi chạy container, ánh xạ cổng nội bộ `5000` tới cổng `5000` trên host (hoặc bất kỳ cổng host nào bạn muốn):

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` chạy ở chế độ detached.
- `-p 5000:5000` yêu cầu Docker chuyển tiếp cổng host 5000 tới cổng container 5000—đúng như chỉ thị **expose container port** đã chuẩn bị.

Bạn có thể kiểm tra endpoint bằng `curl`:

```bash
curl http://localhost:5000/health
```

Kết quả mong đợi:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

Nếu bạn nhận được JSON này, chúc mừng—bạn đã **dockerize python api** thành công và mở được cổng truy cập.

## Common Edge Cases & How to Handle Them

### 1. Changing the Host Port

Đôi khi cổng 5000 đã được sử dụng trên máy của bạn. Không sao—chỉ cần thay đổi phần cổng phía host:

```bash
docker run -d -p 8080:5000 my-python-api
```

Bây giờ `http://localhost:8080/health` sẽ hoạt động trong khi container vẫn lắng nghe trên `5000`.

### 2. Multi‑Stage Builds for Smaller Images

Nếu bạn không cần toàn bộ runtime Aspose.Cells trong môi trường production, có thể tạo một multi‑stage build: biên dịch tài nguyên trong một image nặng, sau đó sao chép chỉ các phần runtime cần thiết vào stage cuối cùng sử dụng `python:3.11-slim`. Cách này giảm đáng kể kích thước image cuối cùng.

### 3. Using Docker Compose

Đối với các cấu hình phức tạp hơn (ví dụ: một database chạy cùng API), hãy đưa cùng các lệnh vào file `docker-compose.yml`:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose sẽ tự động tôn trọng chỉ thị `EXPOSE`, vì vậy bạn không cần lặp lại ánh xạ cổng.

### 4. Environment Variables

Nếu API của bạn cần cấu hình (như secret key), hãy truyền chúng khi chạy container:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

Trong Python, bạn có thể đọc bằng `os.getenv("SECRET_KEY")`.

## Debugging Tips

- **Container exits immediately?** Kiểm tra log bằng `docker logs api_container`. Một lỗi phổ biến là quên `host="0.0.0.0"` trong Flask.
- **Port already in use?** Kiểm tra bằng `docker ps` và `netstat -tulpn`. Dùng cổng host khác như hướng dẫn ở trên.
- **Missing dependencies?** Đảm bảo `requirements.txt` tồn tại trước bước `RUN pip install`, hoặc thêm các package trực tiếp trong Dockerfile.

## Recap

Chúng ta đã bắt đầu với một Flask app đơn giản, chọn một base image mạnh mẽ, **dockerfile copy app** để đưa code vào, **set working directory docker** để thực thi gọn gàng, khai báo `EXPOSE 5000` để **expose container port**, và kết thúc bằng `CMD` để khởi chạy dịch vụ. Việc build và run image đã cho chúng ta một **dockerize python api** hoàn chỉnh, sẵn sàng để ai cũng có thể pull và chạy.

## What’s Next?

- **Thêm health‑check** vào Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`).
- **Triển khai logging** tới stdout để Docker có thể thu thập.
- **Bảo mật API** bằng HTTPS


## What Should You Learn Next?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, giúp bạn mở rộng các kỹ thuật đã học trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã nguồn đầy đủ và giải thích chi tiết từng bước để bạn có thể nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Copy Sheets Within Workbook Using Aspose.Cells for .NET - Step-by-Step Guide](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [Copy Data in Excel Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}