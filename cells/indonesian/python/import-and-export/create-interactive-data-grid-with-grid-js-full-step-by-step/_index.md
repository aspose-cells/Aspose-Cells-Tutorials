---
category: general
date: 2026-06-21
description: Buat grid data interaktif menggunakan Grid.js dan pelajari cara menampilkan
  tabel data JSON dengan penyortiran, paginasi, dan pencarian. Sempurna untuk dasbor
  web.
draft: false
keywords:
- create interactive data grid
- display json data table
- how to use gridjs
language: id
og_description: Buat grid data interaktif dalam hitungan menit. Pelajari cara menggunakan
  Grid.js untuk menampilkan tabel data JSON dengan paginasi, penyortiran, dan pencarian.
og_title: Buat Grid Data Interaktif dengan Grid.js – Tutorial Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  headline: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create interactive data grid using Grid.js and learn how to display
    JSON data table with sorting, pagination, and search. Perfect for web dashboards.
  name: Create Interactive Data Grid with Grid.js – Full Step‑by‑Step Guide
  steps:
  - name: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
    text: A modern browser (Chrome, Edge, or Firefox) – Grid.js relies on ES6 features.
  - name: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
    text: A local or remote folder containing a `grid_data.json` file (we’ll show
      the format).
  - name: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
    text: Basic familiarity with HTML and JavaScript – nothing fancy, just the ability
      to open a `.html` file in a browser.
  type: HowTo
tags:
- JavaScript
- Grid.js
- Data Visualization
title: Buat Grid Data Interaktif dengan Grid.js – Panduan Lengkap Langkah demi Langkah
url: /id/python/import-and-export/create-interactive-data-grid-with-grid-js-full-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Grid Data Interaktif dengan Grid.js – Panduan Langkah‑per‑Langkah Lengkap

Pernah bertanya-tanya bagaimana cara **membuat grid data interaktif** yang memungkinkan pengguna mengurutkan, mencari, dan menelusuri baris tanpa menulis backend? Anda tidak sendirian. Di banyak dasbor, titik sakit terbesar adalah mengubah dump JSON statis menjadi tabel yang halus dan dapat dicari—sesuatu yang terasa semulus spreadsheet tetapi berjalan sepenuhnya di browser.

Dalam tutorial ini kami akan menjelaskan **cara menggunakan Grid.js** untuk **menampilkan tabel data JSON** pada halaman HTML sederhana. Pada akhir tutorial Anda akan memiliki contoh yang berfungsi yang dapat Anda masukkan ke dalam proyek apa pun, serta tips untuk menyesuaikan toolbar, menangani set data besar, dan menghindari masalah umum.

## Apa yang Akan Anda Pelajari

- Cara mengambil file JSON yang mendefinisikan kolom dan baris.
- Cara menginisialisasi **Grid.js** dengan pagination, sorting, searching, dan toolbar kustom.
- Cara merender grid ke dalam kontainer target.
- Penyesuaian opsional: format sel kustom, penggantian tema, dan penanganan error.
- Contoh kode lengkap yang siap disalin‑tempel.

### Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. Browser modern (Chrome, Edge, atau Firefox) – Grid.js bergantung pada fitur ES6.
2. Folder lokal atau remote yang berisi file `grid_data.json` (kami akan menunjukkan formatnya).
3. Pemahaman dasar tentang HTML dan JavaScript – tidak perlu hal rumit, hanya kemampuan membuka file `.html` di browser.

Tidak ada alat build, tidak ada npm install, tidak ada kode sisi server. Itulah keindahan **membuat grid data interaktif** dengan Grid.js: ia bekerja langsung dari CDN.

---

## Langkah 1: Siapkan JSON yang Mendefinisikan Tabel Anda

Hal pertama yang Anda butuhkan adalah payload JSON yang memberi tahu Grid.js kolom apa yang ada dan baris apa yang akan ditampilkan. Anggaplah ini sebagai cetak biru untuk **menampilkan tabel data JSON** Anda. Berikut contoh minimal yang dapat Anda simpan sebagai `grid_data.json` di direktori yang sama dengan file HTML Anda:

```json
{
  "columns": ["ID", "Name", "Email", "Country"],
  "rows": [
    [1, "Alice Johnson", "alice@example.com", "USA"],
    [2, "Bob Smith", "bob@example.com", "Canada"],
    [3, "Carlos Ruiz", "carlos@example.com", "Mexico"],
    [4, "Diana Lee", "diana@example.com", "UK"]
  ]
}
```

*Mengapa format ini?* Grid.js mengharapkan `columns` menjadi array string (atau objek untuk konfigurasi lanjutan) dan `rows` menjadi array of arrays di mana setiap array dalamnya sesuai dengan urutan kolom. Tentu saja Anda dapat menambahkan lebih banyak kolom atau objek bersarang – Grid.js akan merendernya selama bentuknya cocok.

> **Tip Pro:** Jika Anda mengambil data dari API, cukup ganti `fetch('grid_data.json')` statis dengan URL endpoint Anda. Sisanya tetap sama.

---

## Langkah 2: Inisialisasi Grid.js – Inti dari **cara menggunakan gridjs**

Sekarang sumber data siap, kita perlu menambahkan Grid.js ke halaman dan memberi tahu cara kerjanya. Di sinilah kita benar-benar **membuat grid data interaktif** dengan fungsionalitas seperti pagination, sorting, dan tombol toolbar yang berguna.

```html
<!-- Load Grid.js from the CDN -->
<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
```

CDN memberikan versi stabil terbaru, dan tema Meri­maid menambahkan tampilan bersih dan modern secara langsung. Anda dapat menggantinya dengan `gridjs.min.css` jika lebih suka gaya default.

Selanjutnya, di dalam tag `<script>`, ambil JSON dan inisialisasi grid:

```javascript
// Step 2: Initialise Grid.js with pagination, sorting, searching, and a toolbar
fetch('grid_data.json')
  .then(response => response.json())
  .then(data => {
    const grid = new gridjs.Grid({
      columns: data.columns,      // Pull column headers from JSON
      data: data.rows,            // Pull row data from JSON
      pagination: { enabled: true, limit: 10 }, // Show 10 rows per page
      sort: true,                 // Enable column sorting
      search: true,               // Add a search box above the grid
      toolbar: {
        enabled: true,
        items: [
          {
            type: 'button',
            text: 'Help',
            onClick: () => alert('Use the search box to filter rows or click column headers to sort.')
          }
        ]
      },
      // Optional: custom cell formatter for the Email column
      // This demonstrates a deeper dive into how to use Grid.js
      // and shows you can embed HTML inside cells.
      columns: data.columns.map(col => {
        if (col === 'Email') {
          return {
            name: col,
            formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
          };
        }
        return col; // Simple string for other columns
      })
    });

    // Step 3: Render the grid into the target container
    grid.render(document.getElementById('grid-container'));
  })
  .catch(err => console.error('Failed to load grid data:', err));
```

### Menjabarkan Opsi‑opsi

| Opsi | Apa Fungsinya | Mengapa Penting |
|------|---------------|-----------------|
| `pagination` | Membagi baris menjadi halaman (default 10 per halaman) | Menjaga tabel besar tetap dapat digunakan tanpa membebani UI. |
| `sort` | Header kolom yang dapat diklik mengubah urutan naik/turun | Pengguna dapat dengan cepat menemukan baris dengan nilai tertinggi. |
| `search` | Menambahkan input teks yang menyaring baris secara langsung | Bagus untuk pencarian ad‑hoc tanpa memuat ulang data. |
| `toolbar` | Menambahkan tombol atau dropdown kustom di atas grid | Sempurna untuk aksi “Help”, “Export”, atau “Refresh”. |
| `formatter` | Memungkinkan Anda mengembalikan HTML mentah untuk sebuah sel | Di sini kami mengubah string email menjadi tautan mailto yang dapat diklik. |

> **Mengapa pendekatan ini?** Dengan menjaga konfigurasi grid secara deklaratif, Anda dapat dengan mudah menyesuaikan perilaku tanpa menyentuh logika rendering inti. Ini adalah cara yang direkomendasikan untuk **cara menggunakan Grid.js** pada kebanyakan proyek.

---

## Langkah 3: Render Grid ke dalam Halaman Anda

Baris terakhir skrip—`grid.render(document.getElementById('grid-container'))`—menyuntikkan tabel yang sepenuhnya berfungsi ke dalam `<div>` yang Anda letakkan di suatu tempat dalam body HTML Anda:

```html
<div id="grid-container"></div>
```

Itu saja. Saat halaman dimuat, browser mengambil JSON, membangun instance Grid.js, dan menampilkan tabel interaktif di layar. Tidak ada penyegaran, tidak ada panggilan server setelah pemuatan awal.

---

## Opsional: Penyesuaian Styling dan Tema

Jika tema Meri­maid default bukan selera Anda, Anda dapat menggantinya dengan tema bawaan lainnya (`gridjs.min.css`) atau menulis CSS Anda sendiri. Misalnya, untuk membuat latar belakang header berwarna abu‑abu lembut:

```css
.gridjs-th {
  background-color: #f5f5f5;
}
```

Tambahkan potongan kode di dalam tag `<style>` atau stylesheet eksternal. Grid.js menghormati selector CSS standar, sehingga Anda memiliki kontrol penuh atas font, warna, dan spasi.

---

## Masalah Umum & Cara Menghindarinya

| Masalah | Gejala | Solusi |
|---------|--------|--------|
| **CORS errors** saat mengambil JSON dari domain lain | Konsol browser menampilkan “Blocked by CORS policy” | Host JSON pada origin yang sama atau aktifkan CORS di server. |
| **Large data sets cause lag** | Scroll menjadi patah‑patah, pagination lambat | Gunakan pagination `server` (`pagination: { server: { url: (prev, page, limit) => … } }`) atau lazy‑load baris. |
| **Toolbar button doesn’t appear** | Tidak ada tombol yang terlihat meskipun `toolbar.enabled: true` | Pastikan Anda menggunakan Grid.js versi 2.0+; versi lama memiliki API toolbar yang berbeda. |
| **Email links not clickable** | Formatter mengembalikan teks biasa | Kembalikan `gridjs.html(...)` alih-alih string biasa, seperti yang ditunjukkan pada contoh. |

Menangani masalah ini sejak awal menghemat Anda berjam‑jam debugging di kemudian hari.

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah file HTML lengkap yang dapat Anda simpan sebagai `index.html`. Buka di browser, dan Anda akan melihat demo **membuat grid data interaktif** yang **menampilkan tabel data JSON** dengan sorting, searching, dan tombol bantuan.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Create Interactive Data Grid with Grid.js</title>
  <!-- Grid.js core library -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Optional theme – Meri­maid -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Simple custom styling */
    body { font-family: Arial, sans-serif; margin: 20px; }
    .gridjs-container { max-width: 900px; margin: auto; }
    .gridjs-th { background-color: #f0f8ff; }
  </style>
</head>
<body>
  <h1>Create Interactive Data Grid with Grid.js</h1>
  <p>This page demonstrates how to <strong>display JSON data table</strong> using Grid.js. Feel free to edit <code>grid_data.json</code> and refresh.</p>

  <!-- Grid will be rendered here -->
  <div id="grid-container"></div>

  <script>
    // Load JSON data and initialise Grid.js
    fetch('grid_data.json')
      .then(r => r.json())
      .then(data => {
        const grid = new gridjs.Grid({
          columns: data.columns.map(col => {
            // Custom formatter for Email column
            if (col === 'Email') {
              return {
                name: col,
                formatter: cell => gridjs.html(`<a href="mailto:${cell}">${cell}</a>`)
              };
            }
            return col;
          }),
          data: data.rows,
          pagination: { enabled: true, limit: 5 },
          sort: true,
          search: true,
          toolbar: {
            enabled: true,
            items: [
              {
                type: 'button',
                text: 'Formula Help',
                onClick: () => alert('Hover over a cell to see its formula description.')
              }
            ]
          }
        });

        // Render the grid
        grid.render(document.getElementById('grid-container'));
      })
      .catch(err => console.error('Error loading grid data:', err));
  </script>
</body>
</html


## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan menjelajahi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Membuat Daftar Validasi Data Excel dengan Aspose.Cells untuk Java: Panduan Langkah‑per‑Langkah](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)
- [Cara Membuat Kotak Centang di Excel menggunakan Aspose.Cells untuk .NET | Tutorial Validasi Data](/cells/english/net/data-validation/create-checkboxes-net-excel-aspose-cells/)
- [Buat & Impor Data XML ke Excel Menggunakan Aspose.Cells untuk Java](/cells/english/java/import-export/create-import-xml-data-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}