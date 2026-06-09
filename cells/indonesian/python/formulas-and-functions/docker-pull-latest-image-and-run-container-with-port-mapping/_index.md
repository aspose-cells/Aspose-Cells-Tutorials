---
category: general
date: 2026-06-08
description: Tarik gambar terbaru dengan Docker, lalu jalankan kontainer Docker secara
  terpisah (detached) sambil mengekspos port 8080 melalui pemetaan port kontainer
  Docker. Panduan langkah demi langkah untuk penyiapan cepat.
draft: false
keywords:
- docker pull latest image
- docker container port mapping
- run docker container detached
- docker expose port 8080
- map host port docker
language: id
og_description: Tarik gambar terbaru Docker dan jalankan kontainer Docker secara terpisah
  sambil mengekspos port 8080. Pelajari cara memetakan port host Docker dalam hitungan
  menit.
og_title: Tarik Gambar Terbaru Docker dan Jalankan Kontainer dengan Pemetaan Port
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Docker pull latest image, then run Docker container detached while
    exposing port 8080 via docker container port mapping. Step‑by‑step guide for quick
    setup.
  headline: Docker Pull Latest Image and Run Container with Port Mapping
  type: TechArticle
tags:
- Docker
- Containers
- DevOps
title: Tarik Gambar Terbaru Docker dan Jalankan Kontainer dengan Pemeta Port
url: /id/python/formulas-and-functions/docker-pull-latest-image-and-run-container-with-port-mapping/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Docker Pull Latest Image and Run Container with Port Mapping

Pernah bertanya-tanya bagaimana cara **docker pull latest image** dan langsung memiliki layanan yang mendengarkan di mesin Anda? Anda tidak sendirian—banyak pengembang mengalami hal ini saat pertama kali menjalankan sebuah container. Kabar baiknya? Ini sangat mudah setelah Anda mengetahui perintah yang tepat.

Dalam tutorial ini kita akan menelusuri cara menarik image Aspose.Cells Grid.js terbaru, memetakan port host 8080 ke container, dan menjalankan container dalam mode detached. Pada akhir tutorial Anda akan memiliki UI yang berfungsi penuh di `http://localhost:8080` tanpa menulis satu baris Dockerfile pun.

## What You’ll Achieve

- Menarik image Docker terbaru menggunakan **docker pull latest image**
- Memetakan port host 8080 ke port container 80 (`docker container port mapping`)
- Menjalankan container di latar belakang (`run docker container detached`)
- Memverifikasi bahwa layanan dapat diakses melalui `docker expose port 8080`

### Prerequisites

- Docker Engine ≥ 20.10 terpasang secara lokal  
- Familiaritas dasar dengan command‑line (kami akan membuatnya sederhana)  
- Koneksi internet untuk mengunduh image pertama kali  

Jika Anda belum memiliki salah satu dari hal tersebut, instal Docker terlebih dahulu—tidak perlu menciptakan kembali roda.

---

## Step 1: Docker Pull Latest Image

Hal pertama yang Anda butuhkan adalah salinan terbaru dari image Aspose.Cells Grid.js. Menarik image terbaru memastikan Anda mendapatkan perbaikan bug dan fitur terbaru.

```bash
# Pull the latest Aspose.Cells Grid.js image from Docker Hub
docker pull aspose/cells-gridjs:latest
```

> **Mengapa ini penting:** Docker menyimpan cache image secara lokal, jadi menarik **docker pull latest image** setiap kali memastikan Anda tidak terjebak dengan versi lama yang mungkin kehilangan patch keamanan penting.

> **Pro tip:** Jika Anda memerlukan versi tertentu, ganti `latest` dengan tag yang diinginkan, misalnya `aspose/cells-gridjs:2.1.0`.

---

## Step 2: Docker Container Port Mapping (Expose Port 8080)

Container secara default terisolasi, yang berarti port internalnya tidak dapat diakses dari host Anda. Di sinilah **docker container port mapping** berperan—Anda memberi tahu Docker untuk meneruskan lalu lintas dari port host (8080) ke port container (80).

```bash
# Map host port 8080 to container port 80 and run the container detached
docker run -d -p 8080:80 aspose/cells-gridjs:latest
```

**Penjelasan per bagian:**

- `-d` – menjalankan container **detached**, sehingga terminal Anda bebas untuk pekerjaan lain.
- `-p 8080:80` – **map host port docker** 8080 ke port internal container 80.  
  Sisi kiri (`8080`) adalah port host, sisi kanan (`80`) adalah port container.
- `aspose/cells-gridjs:latest` – image yang baru saja kita tarik.

> **Kasus khusus:** Jika port 8080 sudah digunakan, Docker akan menampilkan error. Anda dapat menghentikan layanan yang konflik atau memilih port host lain, misalnya `-p 9090:80`.

---

## Step 3: Verify the Service (Docker Expose Port 8080)

Setelah container berjalan, mari pastikan **docker expose port 8080** memang berfungsi.

```bash
# List running containers to confirm the one we just started
docker ps

# Quick curl test (optional)
curl http://localhost:8080
```

Anda seharusnya melihat halaman HTML atau respons JSON dari Grid.js. Jika mendapatkan *connection refused*, periksa kembali bahwa container masih berjalan (`docker ps`) dan tidak ada aturan firewall yang memblokir port 8080.

---

## Optional: Using Docker Compose for Reusability

Jika Anda berencana menjalankan container ini secara sering, file `docker‑compose.yml` kecil dapat menghemat beberapa ketukan tombol.

```yaml
version: "3.9"
services:
  gridjs:
    image: aspose/cells-gridjs:latest   # docker pull latest image handled automatically
    ports:
      - "8080:80"                       # map host port docker
    restart: unless-stopped
```

Jalankan dengan satu perintah:

```bash
docker compose up -d   # runs detached, same as run docker container detached
```

Compose secara otomatis menarik image terbaru jika belum ada, membuat alur kerja Anda semakin mulus.

---

## Common Pitfalls & How to Avoid Them

| Gejala | Penyebab Kemungkinan | Solusi |
|---------|----------------------|--------|
| `port is already allocated` | Port host 8080 sedang dipakai | Pilih port host lain (`-p 9090:80`) |
| Container exits immediately | Image memerlukan environment variables | Periksa README image untuk pengaturan `ENV` yang diperlukan |
| Tidak dapat mengakses UI dari perangkat lain | Hanya terikat pada localhost | Gunakan `-p 0.0.0.0:8080:80` atau konfigurasi firewall |
| Image usang meskipun sudah `docker pull` | Tag image masih di-cache secara lokal | Jalankan `docker pull --quiet aspose/cells-gridjs:latest` untuk memaksa refresh |

---

## Full Script for One‑Click Setup

Salin‑tempel blok di bawah ini ke dalam file bernama `run-gridjs.sh`, beri hak eksekusi (`chmod +x run-gridjs.sh`), dan jalankan. Skrip ini menangani penarikan, menjalankan, dan verifikasi dalam satu langkah.

```bash
#!/usr/bin/env bash
# -------------------------------------------------
# One‑click script: docker pull latest image + run
# -------------------------------------------------

# Pull the newest image (docker pull latest image)
docker pull aspose/cells-gridjs:latest

# Run detached with host port mapping (docker container port mapping)
docker run -d -p 8080:80 --name gridjs aspose/cells-gridjs:latest

# Wait a couple of seconds for the service to start
sleep 3

# Verify the UI is reachable (docker expose port 8080)
if curl -s http://localhost:8080 >/dev/null; then
  echo "✅ Grid.js UI is up at http://localhost:8080"
else
  echo "⚠️  Something went wrong – check docker ps and logs"
fi
```

Menjalankan skrip ini memberi Anda hasil yang sama dengan tiga langkah manual, tetapi dengan satu perintah saja. Praktis untuk pipeline CI atau demo cepat.

---

## Conclusion

Anda baru saja mempelajari cara **docker pull latest image**, menyiapkan **docker container port mapping**, dan **run docker container detached** sambil **docker expose port 8080**. Dengan beberapa perintah ini Anda dapat menjalankan layanan berbasis web apa pun dan membuatnya langsung dapat diakses di mesin Anda dengan **map host port docker** ke port internal container.

Apa selanjutnya? Coba ganti image Aspose.Cells Grid.js dengan aplikasi web lain, eksperimen dengan beberapa pemetaan port, atau integrasikan setup ini ke dalam stack Docker Compose untuk deployment berskala produksi. Konsep yang Anda kuasai di sini—menarik image terbaru, mengekspos port, dan menjalankan container di latar belakang—adalah blok bangunan dari alur kerja kontainer modern.

Jangan ragu meninggalkan komentar jika Anda menemukan kendala, atau bagikan bagaimana Anda menyesuaikan skrip untuk proyek Anda sendiri. Selamat ber‑container!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Add an Image to a Chart with Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/add-image-chart-aspose-cells-dotnet/)
- [Excel to Image Conversion in Java&#58; A Step-by-Step Guide Using Aspose.Cells](/cells/english/java/workbook-operations/excel-image-conversion-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}