---
category: general
date: 2026-06-21
description: Pelajari cara membuat image Docker dan menjalankan container Docker dengan
  pemetaan port yang tepat. Termasuk pemetaan port docker run dan mengekspos port
  di Docker.
draft: false
keywords:
- build docker image
- run docker container
- docker run port mapping
- expose port in docker
- docker build from dockerfile
language: id
og_description: Bangun image Docker dan jalankan container Docker dengan pemetaan
  port yang tepat. Kuasai pemetaan port docker run dan ekspos port di Docker dalam
  hitungan menit.
og_title: Membangun Image Docker dan Menjalankan Kontainer Docker – Panduan Lengkap
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
title: Membangun Image Docker dan Menjalankan Kontainer Docker – Panduan Lengkap
url: /id/python/import-and-export/build-docker-image-and-run-docker-container-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bangun Image Docker dan Jalankan Kontainer Docker – Panduan Lengkap

Pernah bertanya-tanya bagaimana cara **membangun image docker** untuk aplikasi web sederhana dan kemudian menjalankannya tanpa masalah? Anda tidak sendirian—banyak developer mengalami hal yang sama saat pertama kali mencoba containerization. Dalam tutorial ini kami akan membahas seluruh proses, mulai dari menulis Dockerfile hingga mengekspos port yang tepat dan akhirnya menggunakan `docker run` untuk memetakan port tersebut ke host Anda. Pada akhir tutorial Anda akan tahu persis cara **menjalankan kontainer docker** dengan pemetaan port yang benar, dan mengapa mengekspos port di Docker itu penting.

Kami akan membahas semua yang Anda butuhkan: perintah `docker build` yang tepat, cara **docker build from Dockerfile**, nuansa `docker run port mapping`, dan bahkan pemeriksaan cepat untuk memastikan kontainer benar‑benar mendengarkan di tempat yang Anda harapkan. Tanpa basa‑basi, hanya panduan langkah‑demi‑langkah yang dapat Anda salin‑tempel ke terminal.

## Apa yang Akan Anda Capai

- Menulis Dockerfile minimal untuk aplikasi Node.js (atau apa saja).  
- **Membangun image docker** menggunakan sintaks CLI resmi.  
- Memahami perbedaan antara `EXPOSE` di Dockerfile dan flag `-p` di `docker run`.  
- **Menjalankan kontainer docker** dengan `docker run port mapping` sehingga Anda dapat mengakses layanan di `http://localhost:5000`.  
- Mendiagnosa jebakan umum seperti port yang terlupakan atau port host‑container yang tidak cocok.

### Prasyarat

- Docker Engine terpasang (Desktop atau Engine 20.10+).  
- Familiaritas dasar dengan command line.  
- Sebuah aplikasi web kecil (kami akan menggunakan server Python Flask satu baris, tetapi Anda dapat menggantinya dengan apa saja).  

Jika Anda sudah memiliki semua itu, mari mulai.

---

## Langkah 1: Buat Aplikasi Sederhana

Pertama, kita membutuhkan sesuatu untuk dikontainerkan. Buat folder bernama `myapp` dan letakkan satu file `app.py` di dalamnya:

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

> **Tip pro:** Baris `host="0.0.0.0"` memberi tahu Flask untuk mendengarkan pada semua antarmuka, yang diperlukan agar Docker dapat meneruskan lalu lintas dari host.

Sekarang Anda memiliki layanan web kecil yang mendengarkan pada port 5000 di dalam kontainer.

## Langkah 2: Tulis Dockerfile (Docker Build from Dockerfile)

Selanjutnya, kita memerlukan **Dockerfile** yang memberi tahu Docker cara menyusun image. Letakkan file ini di samping `app.py`:

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

Beberapa hal yang perlu dicatat:

- `FROM python:3.11-slim` memberi kita image dasar yang ringan.  
- `EXPOSE 5000` **expose port in docker** – ini hanyalah petunjuk bagi siapa pun yang membaca Dockerfile, tetapi tidak secara otomatis membuka port di host.  
- Baris `CMD` menjalankan server Flask ketika kontainer dimulai.

## Langkah 3: **Membangun Image Docker** dari Dockerfile

Buka terminal, `cd` ke folder yang berisi Dockerfile, dan jalankan:

```bash
docker build -t myflaskapp .
```

Mari kita uraikan perintah itu:

- `docker build` adalah perintah yang **builds docker image** lapisan‑lapisan berdasarkan instruksi di Dockerfile.  
- `-t myflaskapp` memberi tag pada image yang dihasilkan dengan nama yang mudah diingat untuk referensi selanjutnya.  
- Titik `.` di akhir memberi tahu Docker untuk menggunakan direktori saat ini sebagai build context (tempat Docker mencari Dockerfile dan semua file yang Anda `COPY`).

Anda akan melihat output serupa dengan:

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

Jika ada error, periksa kembali sintaks Dockerfile dan pastikan file `app.py` berada di folder yang sama.

### Verifikasi Image Ada

Jalankan `docker images` dan cari `myflaskapp`:

```bash
docker images | grep myflaskapp
```

Anda akan melihat sesuatu seperti:

```
myflaskapp   latest   1c2d3e4f5g6h   2 minutes ago   120MB
```

Selamat—Anda baru saja **membangun image docker** dengan sukses!

## Langkah 4: **Menjalankan Kontainer Docker** dengan Pemetaan Port

Setelah image siap, saatnya **run docker container** dan membuat aplikasi Flask dapat diakses dari mesin host Anda. Gunakan flag `-p` untuk melakukan **docker run port mapping**:

```bash
docker run -p 5000:5000 myflaskapp
```

Penjelasan:

- Angka `5000` pertama (sisi kiri) adalah **host port**.  
- Angka `5000` kedua (sisi kanan) adalah **container port** yang sebelumnya kita ekspos.  
- Docker akan meneruskan lalu lintas dari `localhost:5000` pada mesin Anda ke port 5000 di dalam kontainer.

Anda akan melihat log startup Flask:

```
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)
```

Buka browser dan arahkan ke `http://localhost:5000`. Anda akan melihat “Hello from Docker!”—kontainer sedang melayani lalu lintas persis seperti yang diharapkan.

### Menjalankan Kontainer di Latar Belakang (Opsional)

Jika Anda tidak ingin terminal terblokir, tambahkan `-d` untuk menjalankannya di background:

```bash
docker run -d -p 5000:5000 myflaskapp
```

Anda dapat menghentikannya nanti dengan `docker stop <container-id>`.

## Langkah 5: Penjelasan Mendalam – **Expose Port in Docker** vs. **Docker Run Port Mapping**

Mudah untuk menganggap bahwa instruksi `EXPOSE` sama dengan flag `-p`, padahal keduanya memiliki tujuan berbeda:

| Konsep | Apa yang Dilakukan | Apakah Membuka Port di Host? |
|--------|--------------------|------------------------------|
| `EXPOSE` (di Dockerfile) | Mendokumentasikan port mana yang *diharapkan* kontainer untuk mendengarkan. | **Tidak** – hanya metadata. |
| `-p host:container` (docker run) | Membuat aturan NAT yang meneruskan lalu lintas dari port host ke port kontainer. | **Ya** – pemetaan port yang sebenarnya. |

Jika Anda lupa menambahkan `EXPOSE`, perintah `docker run -p` tetap berfungsi, tetapi Anda kehilangan dokumentasi yang membantu bagi pengguna downstream. Sebaliknya, jika Anda hanya `EXPOSE` tanpa pernah memakai `-p`, layanan tetap tidak dapat diakses dari host.

### Menggunakan `docker run` dengan Host Port Berbeda

Kadang‑kadang Anda sudah memiliki sesuatu yang mendengarkan pada host port 5000. Tidak masalah—cukup peta ke host port yang lain:

```bash
docker run -p 8080:5000 myflaskapp
```

Sekarang aplikasi dapat diakses di `http://localhost:8080`, sementara tetap mendengarkan pada 5000 di dalam kontainer. Fleksibilitas ini adalah salah satu kekuatan utama **docker run port mapping**.

## Langkah 6: Jebakan Umum & Kasus Edge

| Masalah | Gejala | Solusi |
|---------|--------|--------|
| Lupa menambahkan `EXPOSE` | Pengembang baru tidak tahu port mana yang harus dipetakan. | Tambahkan `EXPOSE 5000` (atau port yang digunakan aplikasi Anda). |
| Menggunakan host port yang salah | Browser menampilkan “connection refused”. | Pastikan sisi kiri `-p` cocok dengan port yang ingin Anda akses. |
| Kontainer crash saat start | Tidak ada log, kontainer keluar seketika. | Jalankan `docker logs <container-id>` untuk melihat pesan error; biasanya karena dependensi yang hilang atau `CMD` yang salah. |
| Port sudah dipakai di host | Docker menampilkan “bind: address already in use”. | Pilih host port yang berbeda (`-p 8080:5000`). |
| Tidak binding ke `0.0.0.0` | Layanan hanya dapat diakses dari dalam kontainer. | Pada Flask, set `host="0.0.0.0"`; framework lain memiliki pengaturan serupa. |

### Membangun Image Multi‑Stage (Lanjutan)

Jika Anda membutuhkan image akhir yang lebih kecil, Anda dapat **build docker image** dengan Dockerfile multi‑stage:

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

Teknik ini menghilangkan lapisan‑lapisan build‑time, menghasilkan image yang lebih ramping—ideal untuk produksi.

## Langkah 7: Bersihkan

Setelah selesai bereksperimen, bersihkan lingkungan Anda:

```bash
# Stop all running containers derived from the image
docker ps --filter "ancestor=myflaskapp" -q | xargs -r docker stop

# Remove the image
docker rmi myflaskapp
```

Membersihkan mencegah penumpukan disk dan menjaga lingkungan Docker tetap rapi.

---

## Kesimpulan

Anda kini memiliki alur kerja end‑to‑end yang solid untuk **build docker image** dan **run docker container** dengan **docker run port mapping** yang tepat. Dengan memahami cara **expose port in docker** dan bagaimana flag `-p` benar‑benar meneruskan lalu lintas, Anda dapat dengan percaya diri mengkontainerkan layanan apa pun dan membuatnya dapat diakses dari host atau jaringan yang lebih luas.

Apa selanjutnya? Coba ganti aplikasi Flask dengan binary Go, tambahkan variabel lingkungan dengan `-e`, atau push image yang baru Anda buat ke Docker Hub menggunakan `docker push`. Langit adalah batasnya, dan Anda baru saja memperoleh superpower baru di dunia DevOps.

Selamat berkontainer


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang dapat dijalankan dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Master Image Rendering in Excel Using Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/images-shapes/master-image-rendering-excel-aspose-cells-net/)
- [How to Add an Image to a Chart with Aspose.Cells for .NET: A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [How to Add Image Hyperlinks in .NET Workbooks Using Aspose.Cells for Enhanced Interactivity](/cells/english/net/images-shapes/adding-image-hyperlinks-net-workbooks-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}