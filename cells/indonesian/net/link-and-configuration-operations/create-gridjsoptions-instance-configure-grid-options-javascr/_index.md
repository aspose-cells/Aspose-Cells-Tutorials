---
category: general
date: 2026-05-30
description: Pelajari cara membuat instance GridJsOptions dan mengkonfigurasi opsi
  grid JavaScript untuk tabel dinamis. Panduan langkah demi langkah dengan kode lengkap.
draft: false
keywords:
- create gridjsoptions instance
- configure grid options javascript
- gridjs initialization
- javascript data grid settings
- dynamic table configuration
language: id
og_description: Buat instance GridJsOptions dan konfigurasikan opsi grid JavaScript
  dalam hitungan menit. Contoh lengkap, penjelasan, dan tips praktik terbaik.
og_title: Buat Instance GridJsOptions – Konfigurasikan Opsi Grid JavaScript
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  headline: Create GridJsOptions Instance – Configure Grid Options JavaScript
  type: TechArticle
- description: Learn how to create GridJsOptions instance and configure grid options
    JavaScript for dynamic tables. Step‑by‑step guide with full code.
  name: Create GridJsOptions Instance – Configure Grid Options JavaScript
  steps:
  - name: Prerequisites
    text: '- A modern browser (Chrome, Edge, Firefox) – no build tools required. -
      Basic familiarity with JavaScript (variables, objects, DOM). - The Grid.js library
      (we’ll pull it from a CDN).'
  - name: Why this matters
    text: Loading the library from a CDN ensures you always get the latest stable
      version without a local install. The `<div id="grid-wrapper">` is the placeholder
      that the Grid.js constructor will target once we **configure grid options JavaScript**.
  - name: What you’re configuring
    text: '- **NumberFormatAlignment** – aligns numeric strings automatically. - **Pagination**
      – controls page size and navigation. - **Sorting** – toggles column sorting.
      - **Columns** – defines headers, data types, and custom renderers.'
  - name: Edge‑case note
    text: If you later supply a custom data source that already returns paginated
      results, you’ll want to disable Grid.js’s built‑in pagination to avoid double‑paging.
      Simply set `gridOptions.Pagination.enabled = false;`.
  - name: Expected Output
    text: 'When you open the HTML file in a browser you should see:'
  type: HowTo
tags:
- gridjs
- javascript
- data‑grid
title: Buat Instance GridJsOptions – Konfigurasikan Opsi Grid JavaScript
url: /id/net/link-and-configuration-operations/create-gridjsoptions-instance-configure-grid-options-javascr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Instance GridJsOptions – Konfigurasikan Grid Options JavaScript

Pernah bertanya-tanya bagaimana cara **create GridJsOptions instance** tanpa harus mencari‑cari dokumen yang tersebar? Anda bukan satu‑satunya. Ketika Anda membutuhkan tabel yang halus dan dapat diurutkan di halaman web, menguasai cara mengkonfigurasi grid options JavaScript adalah langkah pertama menuju UI yang rapi.

Dalam tutorial ini kami akan menelusuri kode tepat yang Anda perlukan, menjelaskan mengapa setiap pengaturan penting, dan menunjukkan contoh lengkap yang dapat dijalankan. Pada akhir tutorial Anda akan nyaman membuat GridJsOptions instance, menyesuaikan perataan, pagination, dan bahkan renderer sel khusus—semua dengan JavaScript murni.

## Apa yang Akan Anda Pelajari

- Cara **create GridJsOptions instance** dari awal.
- Properti kunci yang memungkinkan Anda **configure grid options JavaScript** (sorting, pagination, number formatting, dll.).
- Kesalahan umum (misalnya mencampur tipe string dan numerik) dan cara menghindarinya.
- Halaman HTML lengkap yang dapat Anda copy‑paste ke proyek apa pun dan melihat hasilnya secara instan.

### Prasyarat

- Browser modern (Chrome, Edge, Firefox) – tidak memerlukan alat build.
- Familiaritas dasar dengan JavaScript (variabel, objek, DOM).
- Library Grid.js (kami akan mengambilnya dari CDN).

Jika ada yang terdengar tidak familiar, jangan panik—setiap langkah menyertakan penyegaran singkat.

---

## Langkah 1: Muat Grid.js dan Siapkan Kerangka HTML

Sebelum kita dapat **create GridJsOptions instance**, kita membutuhkan library itu sendiri. Cara termudah adalah menggunakan CDN resmi. Di bawah ini adalah kerangka HTML minimal yang juga menyisakan sebuah `<div>` tempat grid akan dirender.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid.js Demo – Configuring Options</title>
  <!-- Grid.js CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <h2>Simple Data Grid</h2>
  <div id="grid-wrapper"></div>

  <!-- Grid.js JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
  <!-- Our custom script will go here -->
  <script src="grid-config.js"></script>
</body>
</html>
```

> **Pro tip:** Letakkan tautan CSS sebelum gaya Anda sendiri sehingga tema default grid dimuat dengan benar.

### Mengapa ini penting

Memuat library dari CDN memastikan Anda selalu mendapatkan versi stabil terbaru tanpa instalasi lokal. `<div id="grid-wrapper">` adalah placeholder yang akan ditargetkan konstruktor Grid.js setelah kita **configure grid options JavaScript**.

---

## Langkah 2: Buat Instance GridJsOptions Baru

Sekarang masuk ke inti tutorial: baris yang sebenarnya **creates GridJsOptions instance**. Dalam file terpisah bernama `grid-config.js` (direferensikan di HTML di atas) kami akan menulis:

```javascript
// grid-config.js

// Step 2: Create a new GridJsOptions instance to configure grid behavior
const gridOptions = new GridJsOptions();
```

Baris tunggal itu memberi Anda objek bersih yang dapat Anda isi dengan pengaturan. Anggap `gridOptions` sebagai panel kontrol untuk setiap fitur yang nantinya akan Anda aktifkan.

### Apa yang Anda konfigurasi

- **NumberFormatAlignment** – secara otomatis meratakan string numerik.
- **Pagination** – mengontrol ukuran halaman dan navigasi.
- **Sorting** – mengaktifkan/menonaktifkan pengurutan kolom.
- **Columns** – mendefinisikan header, tipe data, dan renderer khusus.

Anda dapat menambahkan properti ini sebelum akhirnya menginstansiasi Grid itu sendiri.

---

## Langkah 3: Aktifkan Penjajaran Angka (Persyaratan Umum)

Sebagian besar tabel berisi campuran teks dan angka. Secara default Grid.js meratakan semuanya ke kiri, yang terlihat aneh untuk nilai moneter. Untuk **configure grid options JavaScript** agar perataan tepat, atur flag `NumberFormatAlignment`:

```javascript
// Enable left/right alignment for numeric strings
gridOptions.NumberFormatAlignment = true;
```

Mengapa mengaktifkannya? Ketika flag bernilai true, Grid.js memeriksa setiap sel; jika terlihat seperti angka (misalnya “1234”, “12.34%”), ia secara otomatis meratakannya ke kanan. Penyesuaian kecil ini membuat laporan jauh lebih mudah dibaca.

---

## Langkah 4: Tambahkan Pagination dan Sorting

Grid dunia nyata jarang muat dalam satu layar. Mari aktifkan pagination (10 baris per halaman) dan izinkan pengguna mengurutkan kolom apa pun.

```javascript
gridOptions.Pagination = {
  limit: 10,          // rows per page
  enabled: true
};

gridOptions.Sort = true;   // enables click‑to‑sort on all columns
```

### Catatan Edge‑case

Jika Anda kemudian menyediakan sumber data khusus yang sudah mengembalikan hasil ter‑pagination, Anda harus menonaktifkan pagination bawaan Grid.js untuk menghindari double‑paging. Cukup set `gridOptions.Pagination.enabled = false;`.

---

## Langkah 5: Definisikan Kolom dan Data Contoh

Sekarang kami akan memberi grid data tiruan dan memberi tahu apa yang masing‑masing kolom wakili. Inilah tempat pola **create gridjsoptions instance** benar‑benar bersinar—semua berada dalam satu objek rapi.

```javascript
// Sample data array of objects
const sampleData = [
  { id: 1, name: "Alice", salary: "54000", department: "Engineering" },
  { id: 2, name: "Bob",   salary: "47000", department: "Marketing" },
  { id: 3, name: "Cara",  salary: "62000", department: "Design" },
  // ...more rows as needed
];

// Column definitions
gridOptions.Columns = [
  { id: "id",   name: "ID",          width: "5%" },
  { id: "name", name: "Employee",    width: "35%" },
  { id: "salary", name: "Salary ($)", width: "20%" },
  { id: "department", name: "Dept.",  width: "40%" }
];

// Attach data source
gridOptions.Data = sampleData;
```

Perhatikan kami menjaga nilai `id` kolom tetap identik dengan kunci di setiap objek data. Konvensi ini memungkinkan Grid.js memetakan nilai secara otomatis, menghemat Anda dari menulis formatter khusus untuk setiap kolom.

---

## Langkah 6: Instansiasi Grid dengan Opsi Kita

Kami akhirnya **configure grid options javascript** dengan mengirimkan objek `gridOptions` ke konstruktor Grid. Grid akan dirender di dalam `<div id="grid-wrapper">` yang kami siapkan sebelumnya.

```javascript
// Create the Grid instance using the previously built options
const grid = new Grid(gridOptions);

// Render the grid into the page
grid.render(document.getElementById("grid-wrapper"));
```

Itu saja. Seluruh proses—dari **create gridjsoptions instance** hingga rendering—memakan waktu kurang dari satu menit penulisan kode.

### Output yang Diharapkan

Saat Anda membuka file HTML di browser, Anda akan melihat:

- Baris header dengan “ID”, “Employee”, “Salary ($)”, “Dept.”.
- Angka gaji diratakan kanan (berkat `NumberFormatAlignment`).
- Kontrol pagination di bagian bawah (jika Anda menambahkan lebih dari sepuluh baris).
- Header kolom yang dapat diklik untuk mengurutkan naik/turun.

Jika ada yang tampak tidak beres, buka konsol browser (F12) dan periksa pesan error—kebanyakan bug berasal dari ID kolom yang tidak cocok atau skrip library yang hilang.

---

## Langkah 7: Penyesuaian Lanjutan (Opsional)

Berikut beberapa ide cepat yang dapat Anda coba setelah grid dasar berfungsi.

| Fitur | Cara mengaktifkan | Mengapa berguna |
|-------|-------------------|-----------------|
| **Custom cell renderer** | `gridOptions.Columns[2].formatter = (cell) => \`<b>$${cell}</b>\`;` | Menyorot gaji dengan tebal. |
| **Search bar** | `gridOptions.Search = true;` | Memungkinkan pengguna menyaring baris secara instan. |
| **Server‑side data** | Set `gridOptions.Server = { url: "/api/employees", then: data => data.items };` | Dapat menangani ribuan baris. |
| **Theme switching** | Add `gridOptions.ClassName = "gridjs-theme-dark";` | Menyesuaikan dengan desain mode gelap. |

Silakan campur dan cocokkan—Grid.js memang sengaja fleksibel. Ingatlah untuk tetap mempertahankan baris **create gridjsoptions instance** di atas; semua penyesuaian selanjutnya bergantung pada objek tunggal itu.

## Kesimpulan

Kami baru saja menelusuri alur kerja lengkap untuk **create GridJsOptions instance** dan **configure grid options JavaScript** demi tabel data yang fungsional, dapat diurutkan, dan ber‑pagination. Dimulai dari halaman HTML sederhana, kami memuat library, membangun objek opsi, mengaktifkan perataan numerik, menambahkan pagination, mendefinisikan kolom, dan akhirnya merender grid.

Dari sini Anda dapat:

- Mengganti `sampleData` statis dengan panggilan AJAX.
- Menambahkan formatter khusus untuk tanggal, mata uang, atau ikon.
- Mengintegrasikan grid ke dalam kerangka kerja seperti React atau Vue (objek `gridOptions` yang sama berfungsi di sana juga).

Kemungkinannya hampir tak terbatas, dan pola yang kami gunakan—memusatkan semua pengaturan dalam satu instance `GridJsOptions`—menjaga kode Anda tetap bersih dan mudah dipelihara.

Punya kasus penggunaan yang belum pasti? Tinggalkan komentar, dan kami akan menjelajahinya bersama. Selamat coding, dan nikmati membangun tabel dinamis dengan Grid.js!

## Apa yang Harus Anda Pelajari Selanjutnya?

- [Cara Membuat dan Mengonfigurasi Workbook Excel dengan Aspose.Cells .NET: Panduan Langkah‑per‑Langkah](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Cara Membuat dan Menata Tabel Excel Menggunakan Aspose.Cells untuk .NET | Panduan Langkah‑per‑Langkah](/cells/english/net/tables-structured-references/aspose-cells-net-excel-tables-styling/)
- [Cara Membuat & Memformat Sel Excel Menggunakan Aspose.Cells untuk Java: Panduan Langkah‑per‑Langkah](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}