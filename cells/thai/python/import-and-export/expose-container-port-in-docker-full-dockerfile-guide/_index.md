---
category: general
date: 2026-06-21
description: เปิดพอร์ตคอนเทนเนอร์ใน Docker พร้อมตั้งค่าไดเรกทอรีทำงานและคัดลอกซอร์สโค้ดของแอปของคุณ
  เรียนรู้วิธีทำ Dockerize API ของ Python ทีละขั้นตอน.
draft: false
keywords:
- expose container port
- set working directory docker
- dockerfile copy app
- copy source into container
- dockerize python api
language: th
og_description: เปิดพอร์ตคอนเทนเนอร์ใน Docker ตั้งค่าไดเรกทอรีทำงาน และคัดลอกซอร์สโค้ดของคุณเข้าสู่คอนเทนเนอร์
  บทเรียนนี้แสดงวิธีการทำ Dockerize API ด้วย Python.
og_title: เปิดพอร์ตคอนเทนเนอร์ใน Docker – คู่มือฉบับสมบูรณ์
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
title: เปิดพอร์ตคอนเทนเนอร์ใน Docker – คู่มือ Dockerfile ฉบับเต็ม
url: /th/python/import-and-export/expose-container-port-in-docker-full-dockerfile-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เปิดพอร์ตคอนเทนเนอร์ใน Docker – คู่มือ Dockerfile ฉบับเต็ม

เคยสงสัยไหมว่าอย่างไรจึงจะ **expose container port** เมื่อคุณกำลังทำคอนเทนเนอร์ไอพีเอพี Python? คุณไม่ได้เป็นคนเดียว นักพัฒนาส่วนใหญ่เจอปัญหาเดียวกัน: แอปทำงานในเครื่องท้องถิ่น แต่เมื่ออยู่ใน Docker แล้วโลกภายนอกไม่สามารถเข้าถึงได้ ในบทแนะนำนี้เราจะพาเดินผ่าน Dockerfile ฉบับเต็มที่ไม่เพียงแต่ **expose container port** แต่ยังรวมถึง **set working directory docker**, **dockerfile copy app**, และ **copy source into container**—ทุกอย่างที่คุณต้องการเพื่อ **dockerize python api** อย่างง่ายดาย

เราจะเริ่มด้วย Flask แอปขนาดเล็ก จากนั้นสร้าง Docker image ตั้งแต่ต้น อธิบายแต่ละคำสั่ง และสุดท้ายรันคอนเทนเนอร์เพื่อให้คุณเข้าถึง `http://localhost:5000/health` เมื่อเสร็จคุณจะมี Docker image ที่พร้อมสำหรับการผลิตและสามารถพุชไปยังรีจิสทรีใดก็ได้

## ข้อกำหนดเบื้องต้น

- Docker Engine ≥ 20.10 installed (Docker Desktop works fine on Windows/macOS, Docker Engine on Linux).
- ความคุ้นเคยพื้นฐานกับ Python และ Flask (หรือเฟรมเวิร์กที่เข้ากันกับ WSGI)
- โปรแกรมแก้ไขข้อความหรือ IDE (VS Code, PyCharm, ฯลฯ) เพื่อแก้ไข Dockerfile และโค้ด Python

ไม่มีไลบรารีเพิ่มเติมที่จำเป็นนอกจากสิ่งที่ภาพฐาน Aspose.Cells Python.NET อย่างเป็นทางการให้มา

## ขั้นตอนที่ 1: สร้าง Python API ขั้นต่ำ

ก่อนอื่นให้เขียนบริการ Flask ขนาดเล็กที่เราจะ **dockerize python api** ต่อไป บันทึกไฟล์นี้เป็น `api_server.py` ในโฟลเดอร์ว่าง

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

ทำไมต้องใช้ `host="0.0.0.0"`? ภายในคอนเทนเนอร์ `localhost` หมายถึงคอนเทนเนอร์เอง การผูกกับ `0.0.0.0` บอก Flask ให้รับการเชื่อมต่อจากทุกอินเทอร์เฟซ ซึ่งจำเป็นสำหรับขั้นตอน **expose container port** ที่จะตามมา

## ขั้นตอนที่ 2: เลือก Base Image ที่เหมาะสม

สำหรับตัวอย่างนี้เราจะใช้ **Aspose.Cells Python.NET base image** อย่างเป็นทางการของ Aspose (`aspose/cells-pythonnet:6.22`) ซึ่งมาพร้อมกับ .NET runtime, Python 3.9, และไลบรารี Aspose.Cells—เหมาะอย่างยิ่งหาก API ของคุณต้องการจัดการ Excel

```dockerfile
# Use the official Aspose.Cells Python.NET base image
FROM aspose/cells-pythonnet:6.22
```

หากคุณไม่ต้องการ Aspose สามารถเปลี่ยนเป็น `python:3.11-slim` ได้ ส่วนที่เหลือของ Dockerfile ยังคงเหมือนเดิม

## ขั้นตอนที่ 3: **Dockerfile Copy App** – คัดลอกซอร์สของคุณเข้าสู่คอนเทนเนอร์

ต่อไปเราต้องนำโค้ดของเราเข้าไปในอิมเมจ นี่คือจุดที่คำสั่ง **dockerfile copy app** มีประโยชน์

```dockerfile
# Copy the entire current directory (your app) into /app inside the container
COPY . /app
```

เครื่องหมาย `.` แทนบริบทการสร้าง (build context) — โฟลเดอร์ที่คุณรัน `docker build` การคัดลอกทุกอย่างจะรวม `requirements.txt` (ถ้ามี) และไฟล์สถิติก็ด้วย หากต้องการอิมเมจที่แคบลงให้ระบุเฉพาะไฟล์ที่จำเป็นเท่านั้น

## ขั้นตอนที่ 4: **Set Working Directory Docker** – กำหนด Working Directory

หลังจากคัดลอก เราบอก Docker ว่าจะรันคำสั่งต่อไปที่ไหน นี่คือขั้นตอน **set working directory docker**

```dockerfile
# Set /app as the working directory for the rest of the build
WORKDIR /app
```

ทำไมต้องทำ? จะช่วยให้คุณไม่ต้องพิมพ์พาธเต็มในภายหลัง (เช่น `python api_server.py` แทน `python /app/api_server.py`) และทำให้โครงสร้างไฟล์ของคอนเทนเนอร์ดูชัดเจนสำหรับผู้ที่อ่านอิมเมจต่อไป

## ขั้นตอนที่ 5: ติดตั้ง Python Dependencies (ไม่บังคับแต่แนะนำ)

หาก API ของคุณต้องพึ่งพาแพคเกจภายนอก ให้สร้าง `requirements.txt` แล้วติดตั้งในเลเยอร์แยก เพื่อให้การแคชทำงานได้ดีขึ้น

```dockerfile
# Install Python dependencies (if requirements.txt exists)
RUN if [ -f requirements.txt ]; then pip install --no-cache-dir -r requirements.txt; fi
```

เงื่อนไขนี้ทำให้การสร้างไม่ล้มเหลวหากไม่มี `requirements.txt`—สะดวกสำหรับตัวอย่างขั้นต่ำด้านบน

## ขั้นตอนที่ 6: **Expose Container Port** – ทำให้ API สามารถเข้าถึงจากภายนอกได้

ตอนนี้เรามาถึงจุดสำคัญ: **expose container port** คำสั่งนี้บอก Docker ว่าคอนเทนเนอร์จะฟังที่พอร์ตใด เพื่อให้ทำการแมปพอร์ตที่รันไทม์ได้

```dockerfile
# Expose the Flask port (5000) so the host can forward traffic
EXPOSE 5000
```

ควรทราบว่า `EXPOSE` เป็นเพียงคำแนะนำในเอกสาร; การแมปจริงเกิดขึ้นเมื่อคุณรัน `docker run -p` อย่างไรก็ตาม การประกาศพอร์ตเป็นแนวปฏิบัติที่ดีและช่วยให้เครื่องมือเช่น Docker Compose ส่งต่อพอร์ตที่ถูกต้องอัตโนมัติ

## ขั้นตอนที่ 7: กำหนดคำสั่ง Startup

สุดท้ายเราบอก Docker ว่าจะเปิด API อย่างไร นี่คือคำสั่ง `CMD`

```dockerfile
# Start the Flask API when the container launches
CMD ["python", "api_server.py"]
```

การใช้รูปแบบอาร์เรย์ JSON จะหลีกเลี่ยงปัญหาการตีความของเชลล์และทำให้คำสั่งพกพาได้ดียิ่งขึ้น

## สรุป Dockerfile ฉบับเต็ม

รวมทุกส่วนเข้าด้วยกัน นี่คือ Dockerfile ฉบับเต็มที่คุณสามารถคัดลอก‑วางได้

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

> **Pro tip:** ให้วางบรรทัด `COPY` *ก่อน* บรรทัด `RUN pip install` หากคุณมี dependencies จำนวนมาก Docker จะเก็บแคชเลเยอร์ที่มีแพคเกจติดตั้งไว้ ดังนั้นการสร้างใหม่หลังจากเปลี่ยนโค้ดจะไม่ต้องติดตั้งซ้ำทั้งหมด

## ขั้นตอนที่ 8: สร้าง Docker Image

เปิดเทอร์มินัลในโฟลเดอร์ที่มี `Dockerfile` และ `api_server.py` แล้วรัน:

```bash
docker build -t my-python-api .
```

Docker จะสตรีมแต่ละขั้นตอน แสดงเลเยอร์ที่แคชได้ หากทุกอย่างราบรื่นคุณจะเห็น `Successfully tagged my-python-api:latest`

## ขั้นตอนที่ 9: รันคอนเทนเนอร์และตรวจสอบการแมปพอร์ต

ตอนนี้ให้เปิดคอนเทนเนอร์โดยแมปพอร์ตภายใน `5000` ไปยังพอร์ตโฮสต์ `5000` (หรือพอร์ตโฮสต์อื่นที่คุณต้องการ)

```bash
docker run -d -p 5000:5000 --name api_container my-python-api
```

- `-d` รันในโหมดแยก (detached)
- `-p 5000:5000` บอก Docker ให้ส่งต่อพอร์ตโฮสต์ 5000 ไปยังพอร์ตคอนเทนเนอร์ 5000—ตรงกับที่คำสั่ง **expose container port** เตรียมไว้

คุณสามารถทดสอบ endpoint ด้วย `curl`:

```bash
curl http://localhost:5000/health
```

ผลลัพธ์ที่คาดหวัง:

```json
{
  "status": "OK",
  "message": "API is running"
}
```

หากคุณเห็น JSON นี้ ยินดีด้วย—you’ve successfully **dockerized python api** and made the port accessible.

## กรณีขอบที่พบบ่อยและวิธีจัดการ

### 1. เปลี่ยนพอร์ตของโฮสต์

บางครั้งพอร์ต 5000 อาจถูกใช้งานอยู่บนเครื่องของคุณ ไม่เป็นไร—เพียงเปลี่ยนด้านโฮสต์ของการแมป:

```bash
docker run -d -p 8080:5000 my-python-api
```

ตอนนี้ `http://localhost:8080/health` จะทำงานได้ในขณะที่คอนเทนเนอร์ยังฟังที่ `5000`

### 2. Multi‑Stage Builds สำหรับภาพขนาดเล็ก

หากคุณไม่ต้องการรันไทม์ Aspose.Cells เต็มรูปแบบใน production สามารถสร้าง multi‑stage build ที่คอมไพล์ assets ในอิมเมจหนัก แล้วคัดลอกเฉพาะส่วนรันไทม์ไปยังขั้นสุดท้ายที่ใช้ `python:3.11-slim` ซึ่งทำให้ขนาดอิมเมจสุดท้ายลดลงอย่างมาก

### 3. ใช้ Docker Compose

สำหรับการตั้งค่าที่ซับซ้อนกว่า (เช่น ฐานข้อมูลร่วมกับ API) ให้ใส่คำสั่งเดียวกันลงใน `docker-compose.yml`:

```yaml
version: "3.9"
services:
  api:
    build: .
    ports:
      - "5000:5000"
    restart: unless-stopped
```

Compose จะเคารพคำสั่ง `EXPOSE` โดยอัตโนมัติ ดังนั้นคุณไม่จำเป็นต้องระบุการแมปพอร์ตซ้ำ

### 4. ตัวแปรสภาพแวดล้อม

หาก API ของคุณต้องการการตั้งค่า (เช่น secret key) ให้ส่งค่าที่ runtime:

```bash
docker run -d -p 5000:5000 -e SECRET_KEY=supersecret my-python-api
```

ใน Python คุณสามารถอ่านค่าได้ด้วย `os.getenv("SECRET_KEY")`

## เคล็ดลับการดีบัก

- **Container exits immediately?** ตรวจสอบล็อกด้วย `docker logs api_container`. ความผิดพลาดทั่วไปคือลืมใส่ `host="0.0.0.0"` ใน Flask
- **Port already in use?** ตรวจสอบด้วย `docker ps` และ `netstat -tulpn`. ใช้พอร์ตโฮสต์อื่นตามที่แสดงข้างต้น
- **Missing dependencies?** ตรวจสอบให้แน่ใจว่า `requirements.txt` อยู่ก่อนขั้นตอน `RUN pip install` หรือเพิ่มแพคเกจโดยตรงใน Dockerfile

## สรุป

เราเริ่มจาก Flask แอปง่าย ๆ เลือก base image ที่แข็งแรง, **dockerfile copy app** เพื่อนำโค้ดเข้า, **set working directory docker** เพื่อความสะอาด, ประกาศ `EXPOSE 5000` เพื่อ **expose container port**, และจบด้วย `CMD` ที่เปิดบริการ การสร้างและรันอิมเมจทำให้เราได้ **dockerize python api** ที่พร้อมใช้งานและใครก็สามารถดึงและรันได้

## ต่อไปคืออะไร?

- **Add a health‑check** ใน Dockerfile (`HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1`)
- **Implement logging** ไปยัง stdout เพื่อให้ Docker สามารถจับได้
- **Secure the API** ด้วย HTTPS

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณเอง

- [คัดลอกแผ่นงานภายในเวิร์กบุ๊กโดยใช้ Aspose.Cells สำหรับ .NET - คู่มือขั้นตอน](/cells/english/net/worksheet-management/copy-sheets-within-workbook-aspose-cells-net/)
- [คัดลอกข้อมูลใน Excel โดยใช้ Aspose.Cells สำหรับ .NET: คู่มือขั้นตอน](/cells/english/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [วิธีนำเข้า DataTable ไปยัง Excel โดยใช้ Aspose.Cells สำหรับ .NET (คู่มือขั้นตอน)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}