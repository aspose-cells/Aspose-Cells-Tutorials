---
category: general
date: 2026-06-21
description: เรียนรู้วิธีสร้างอิมเมจ Docker และรันคอนเทนเนอร์ Docker ด้วยการแมปพอร์ตที่เหมาะสม
  รวมถึงการแมปพอร์ตด้วยคำสั่ง docker run และการเปิดเผยพอร์ตใน Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: th
og_description: สร้างอิมเมจ Docker และรันคอนเทนเนอร์ Docker ด้วยการแมปพอร์ตที่ถูกต้อง
  เชี่ยวชาญการแมปพอร์ตเมื่อรัน Docker และเปิดเผยพอร์ตใน Docker ภายในไม่กี่นาที.
og_title: สร้าง Docker Image และรัน Docker Container – คู่มือฉบับสมบูรณ์
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
title: สร้างภาพ Docker และรันคอนเทนเนอร์ Docker – คู่มือฉบับสมบูรณ์
url: /th/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง Docker Image และรัน Docker Container – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่าจะ **สร้าง docker image** สำหรับเว็บแอปง่าย ๆ แล้วทำให้มันทำงานได้โดยไม่มีปัญหา? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจออุปสรรคเดียวกันเมื่อลองใช้ containerization ครั้งแรก ในบทเรียนนี้เราจะเดินผ่านกระบวนการทั้งหมด ตั้งแต่การเขียน Dockerfile ไปจนถึงการเปิดพอร์ตที่ถูกต้องและสุดท้ายใช้ `docker run` เพื่อแมปพอร์ตนั้นไปยังโฮสต์ของคุณ เมื่อจบคุณจะรู้วิธี **run docker container** พร้อมการแมปพอร์ตที่เหมาะสม และจะเข้าใจว่าการเปิดพอร์ตใน Docker มีความสำคัญอย่างไร

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: คำสั่ง `docker build` ที่แม่นยำ, วิธี **docker build from Dockerfile**, รายละเอียดของ `docker run port mapping`, และแม้กระทั่งการตรวจสอบอย่างเร็วเพื่อให้แน่ใจว่าคอนเทนเนอร์กำลังฟังที่พอร์ตที่คุณคาดหวัง ไม่มีเนื้อหาเกินความจำเป็น เพียงแค่คู่มือแบบทำตามขั้นตอนที่คุณสามารถคัดลอก‑วางลงในเทอร์มินัลของคุณได้

## สิ่งที่คุณจะได้เรียนรู้

- เขียน Dockerfile ขั้นต่ำสำหรับแอป Node.js (หรือแอปอื่น)  
- **Build docker image** ด้วยไวยากรณ์ CLI อย่างเป็นทางการ  
- เข้าใจความแตกต่างระหว่าง `EXPOSE` ใน Dockerfile กับแฟล็ก `-p` ใน `docker run`  
- **Run docker container** ด้วย `docker run port mapping` เพื่อให้บริการที่ `http://localhost:5000` สามารถเข้าถึงได้  
- วินิจฉัยปัญหาที่พบบ่อย เช่น พอร์ตที่ลืมเปิดหรือพอร์ตโฮสต์‑คอนเทนเนอร์ไม่ตรงกัน  

### ข้อกำหนดเบื้องต้น

- ติดตั้ง Docker Engine (Desktop หรือ Engine 20.10+)  
- มีความคุ้นเคยพื้นฐานกับ command line  
- มีเว็บแอปขนาดเล็ก (เราจะใช้เซิร์ฟเวอร์ Python Flask หนึ่งบรรทัด, แต่คุณสามารถเปลี่ยนเป็นอะไรก็ได้)  

ถ้าคุณมีทั้งหมดนี้แล้ว, ไปต่อกันเลย

---

## ขั้นตอนที่ 1: สร้างแอปพลิเคชันง่าย ๆ

ก่อนอื่นเราต้องมีสิ่งที่จะแพคเกจไว้ในคอนเทนเนอร์ สร้างโฟลเดอร์ชื่อ `myapp` แล้ววางไฟล์เดียว `app.py` ไว้ด้านใน:

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

> **เคล็ดลับ:** บรรทัด `host="0.0.0.0"` บอก Flask ให้ฟังบนทุกอินเทอร์เฟซ ซึ่งจำเป็นสำหรับ Docker เพื่อส่งต่อทราฟฟิกจากโฮสต์

ตอนนี้คุณมีเว็บเซอร์วิสขนาดเล็กที่ฟังบนพอร์ต 5000 ภายในคอนเทนเนอร์แล้ว

## ขั้นตอนที่ 2: เขียน Dockerfile (Docker Build from Dockerfile)

ต่อไปเราต้องมี **Dockerfile** ที่บอก Docker ว่าจะประกอบ Image อย่างไร วางไฟล์นี้ไว้ข้าง `app.py`:

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

สิ่งที่ควรสังเกต:

- `FROM python:3.11-slim` ให้เรามี base image ที่มีน้ำหนักเบา  
- `EXPOSE 5000` **expose port in docker** – เป็นคำแนะนำให้ผู้ที่อ่าน Dockerfile รู้ว่าแอปจะฟังที่พอร์ตใด, แต่ไม่ได้เปิดพอร์ตบนโฮสต์จริง ๆ  
- บรรทัด `CMD` จะรัน Flask server เมื่อคอนเทนเนอร์เริ่มทำงาน  

## ขั้นตอนที่ 3: **Build Docker Image** จาก Dockerfile

เปิดเทอร์มินัล, `cd` ไปยังโฟลเดอร์ที่มี Dockerfile, แล้วรัน:

```bash
docker build -t myflaskapp .
```

มาดูรายละเอียดของคำสั่งนี้:

- `docker build` คือคำสั่งที่ **builds docker image** ชั้นต่าง ๆ ตามคำสั่งใน Dockerfile  
- `-t myflaskapp` ตั้งชื่อ (tag) ให้ Image ที่สร้างขึ้น เพื่อให้คุณอ้างอิงได้ง่ายในภายหลัง  
- จุด `.` สุดท้ายบอก Docker ให้ใช้ไดเรกทอรีปัจจุบันเป็น build context (ที่ Docker จะมองหา Dockerfile และไฟล์ใด ๆ ที่คุณ `COPY`)  

คุณควรเห็นผลลัพธ์คล้ายกับ:

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

หากเจอข้อผิดพลาดใด ๆ ให้ตรวจสอบไวยากรณ์ของ Dockerfile อีกครั้งและตรวจว่าไฟล์ `app.py` อยู่ในโฟลเดอร์เดียวกันหรือไม่

### ตรวจสอบว่า Image มีอยู่จริง

รัน `docker images` แล้วมองหา `myflaskapp`:

```bash
docker images | grep myflaskapp
```

คุณจะเห็นบางอย่างเช่น:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

ยินดีด้วย—คุณเพิ่ง **built docker image** สำเร็จ!

## ขั้นตอนที่ 4: **Run Docker Container** ด้วย Port Mapping

ตอนนี้ Image พร้อมแล้ว, ถึงเวลาที่จะ **run docker container** และทำให้ Flask app สามารถเข้าถึงจากเครื่องโฮสต์ของคุณ ใช้แฟล็ก `-p` เพื่อทำ **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

คำอธิบาย:

- ตัวเลข `5000` ด้านซ้ายคือ **host port**  
- ตัวเลข `5000` ด้านขวาคือ **container port** ที่เราได้ `EXPOSE` ไว้ก่อนหน้านี้  
- Docker จะส่งต่อทราฟฟิกจาก `localhost:5000` บนเครื่องของคุณไปยังพอร์ต 5000 ภายในคอนเทนเนอร์  

คุณควรเห็นล็อกการเริ่มต้นของ Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

เปิดเบราว์เซอร์และไปที่ `http://localhost:5000` คุณจะเห็นข้อความ “Hello from Docker!” — คอนเทนเนอร์กำลังให้บริการตามที่คาดหวัง

### แยกคอนเทนเนอร์ออก (Optional)

หากคุณไม่ต้องการให้เทอร์มินัลถูกบล็อก, เพิ่ม `-d` เพื่อรันในพื้นหลัง:

```bash
docker run -d -p 5000:5000 myflaskapp
```

คุณสามารถหยุดคอนเทนเนอร์ภายหลังด้วย `docker stop <container-id>`  

## ขั้นตอนที่ 5: เจาะลึก – **Expose Port in Docker** vs. **Docker Run Port Mapping**

หลายคนมักสับสนระหว่างคำสั่ง `EXPOSE` กับแฟล็ก `-p`, แต่สองอย่างนี้ทำหน้าที่ต่างกัน:

| Concept | What it does | Does it open the port on the host? |
|---------|--------------|------------------------------------|
| `EXPOSE` (in Dockerfile) | เอกสารบอกว่าคอนเทนเนอร์ *ตั้งใจ* ฟังที่พอร์ตใด | **No** – เพียง metadata |
| `-p host:container` (docker run) | สร้างกฎ NAT ที่ส่งต่อทราฟฟิกจากพอร์ตโฮสต์ไปยังพอร์ตคอนเทนเนอร์ | **Yes** – การส่งต่อพอร์ตจริง |

หากคุณลืมใส่ `EXPOSE`, คำสั่ง `docker run -p` ยังทำงานได้, แต่คุณจะสูญเสียเอกสารอธิบายสำหรับผู้ใช้ต่อไป หากคุณเพียง `EXPOSE` แล้วไม่ใช้ `-p`, เซอร์วิสจะไม่สามารถเข้าถึงจากโฮสต์ได้

### ใช้ `docker run` กับพอร์ตโฮสต์ที่ต่างกัน

บางครั้งคุณอาจมีบริการอื่นกำลังฟังที่พอร์ต 5000 อยู่ ไม่เป็นไร—ให้แมปไปยังพอร์ตโฮสต์อื่น:

```bash
docker run -p 8080:5000 myflaskapp
```

ตอนนี้แอปจะเข้าถึงได้ที่ `http://localhost:8080` ในขณะที่ยังฟังที่ 5000 ภายในคอนเทนเนอร์ ความยืดหยุ่นนี้เป็นหนึ่งในจุดแข็งหลักของ **docker run port mapping**

## ขั้นตอนที่ 6: ปัญหาที่พบบ่อย & กรณีขอบ

| Issue | Symptom | Fix |
|-------|---------|-----|
| Forgetting `EXPOSE` | นักพัฒนามือใหม่ไม่รู้ว่าจะแมปพอร์ตไหน | เพิ่ม `EXPOSE 5000` (หรือพอร์ตที่แอปของคุณใช้) |
| Using the wrong host port | เบราว์เซอร์แสดง “connection refused” | ตรวจสอบให้แน่ใจว่าด้านซ้ายของ `-p` ตรงกับพอร์ตที่คุณพยายามเข้าถึง |
| Container crashes on start | ไม่มีล็อก, คอนเทนเนอร์ออกทันที | รัน `docker logs <container-id>` เพื่อดูข้อความ error; ส่วนใหญ่เกิดจาก dependency หายหรือ `CMD` ผิด |
| Port already in use on host | Docker แสดง “bind: address already in use” | เลือกพอร์ตโฮสต์อื่น (`-p 8080:5000`) |
| Not binding to `0.0.0.0` | เซอร์วิสเข้าถึงได้เฉพาะจากภายในคอนเทนเนอร์ | ใน Flask ตั้ง `host="0.0.0.0"`; เฟรมเวิร์กอื่นมีการตั้งค่าแบบเดียวกัน |

### สร้าง Multi‑Stage Images (ขั้นสูง)

หากต้องการ Image ที่เล็กลง, คุณสามารถ **build docker image** ด้วย Dockerfile แบบหลายขั้นตอน:

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

เทคนิคนี้จะลบเลเยอร์ที่ใช้ในขั้นตอนการสร้างออก, ทำให้ได้ Image ที่บางเบา—เหมาะสำหรับ production

## ขั้นตอนที่ 7: ทำความสะอาด

เมื่อคุณทดลองเสร็จแล้ว, ทำความสะอาดเพื่อไม่ให้ดิสก์เต็ม:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

การทำความสะอาดช่วยป้องกันการบวมของดิสก์และทำให้สภาพแวดล้อม Docker ของคุณเป็นระเบียบ

---

## สรุป

ตอนนี้คุณมีเวิร์กโฟลว์ครบวงจรสำหรับ **build docker image** และ **run docker container** พร้อมการ **docker run port mapping** ที่ถูกต้อง ด้วยความเข้าใจว่าการ **expose port in docker** ทำงานอย่างไรและแฟล็ก `-p` ส่งต่อทราฟฟิกอย่างไร คุณจึงสามารถคอนเทนเนอร์ไลเซอร์บริการใด ๆ และทำให้เข้าถึงได้จากโฮสต์หรือเครือข่ายภายนอกได้อย่างมั่นใจ

ต่อไปคุณจะทำอะไร? ลองเปลี่ยน Flask app เป็นไบนารี Go, เพิ่ม environment variables ด้วย `-e`, หรือผลักดัน Image ที่คุณสร้างใหม่ไปยัง Docker Hub ด้วย `docker push` โลกไม่มีขีดจำกัด, และคุณก็ได้พลังใหม่ในโลก DevOps แล้ว

Happy container


## สิ่งที่คุณควรเรียนต่อไป

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบต่าง ๆ ในโปรเจกต์ของคุณเอง

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step‑by‑Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}