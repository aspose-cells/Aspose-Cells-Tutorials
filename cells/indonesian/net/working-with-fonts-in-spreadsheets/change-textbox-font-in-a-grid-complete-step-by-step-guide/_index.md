---
category: general
date: 2026-06-21
description: Pelajari cara mengubah font kotak teks, mengatur warna font secara programatis,
  dan menyesuaikan ukuran font sel dalam grid. Ikuti tutorial praktis ini untuk menata
  kotak teks.
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: id
og_description: Ubah font kotak teks dalam grid dengan cepat. Panduan ini menunjukkan
  cara menata kotak teks, mengatur warna font secara programatik, dan menyesuaikan
  ukuran sel dengan kode yang jelas.
og_title: Ubah Font Kotak Teks di Grid – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: Ubah Font Kotak Teks di Grid – Panduan Lengkap Langkah demi Langkah
url: /id/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengubah Font Kotak Teks dalam Grid – Panduan Lengkap Langkah‑per‑Langkah

Pernahkah Anda perlu **mengubah font kotak teks** di dalam data grid tetapi tidak yakin properti mana yang harus diubah? Anda tidak sendirian—banyak pengembang mengalami kendala ini saat membangun tabel yang dapat diedit atau dasbor. Dalam tutorial ini kami akan menjelaskan secara tepat cara mengubah font kotak teks, mengatur warnanya secara programatik, dan bahkan menyesuaikan ukuran font sel‑per‑sel.

Kami juga akan menambahkan tips tentang **cara menata kotak teks**, membahas skenario **mengubah ukuran font sel**, dan menunjukkan cara **mengatur warna font secara programatik** tanpa membuat Anda stres. Pada akhir tutorial Anda akan memiliki potongan kode yang dapat digunakan kembali dan bekerja dengan komponen grid apa pun yang menyediakan API `getCell`.

## Prerequisites

- Browser modern dengan dukungan ES6 (Chrome, Edge, Firefox, Safari)
- Library grid yang menyediakan `grid.getCell(row, col)` dan mengembalikan objek sel yang berisi referensi `textbox`
- Pengetahuan dasar tentang objek JavaScript dan properti CSS

Tidak ada paket tambahan yang diperlukan—hanya JavaScript biasa dan API grid itu sendiri.

## Overview of the Solution

Ide dasarnya sederhana: ambil sel target, dapatkan kotak teks yang tersemat, lalu tetapkan objek font baru yang mendefinisikan keluarga, ukuran, dan warna. Anggap saja Anda memberi kotak teks pakaian baru. Berikut alur tingkat tinggi:

1. **Akses sel target** – temukan baris/kolom yang Anda inginkan.
2. **Ambil kotak teks** – elemen UI yang menampung teks.
3. **Buat objek gaya font** – tentukan keluarga, ukuran, dan warna.
4. **Terapkan gaya** – tetapkan objek ke properti `font` pada kotak teks.

Itu saja. Mari selami tiap langkah, jelaskan mengapa penting, dan lihat kode dalam aksi.

![Screenshot sel grid dengan kotak teks yang ditata – mengubah font kotak teks](/images/change-textbox-font-example.png)

## Step 1: Access the Target Cell in the Grid

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **Mengapa ini penting:**  
> Grid biasanya menyimpan baris dan kolom sebagai indeks berbasis nol. Dengan memanggil `grid.getCell(2, 3)` kita mengambil sel pada **baris 2, kolom 3**. Jika Anda perlu **mengubah ukuran font sel** untuk lokasi lain, cukup ubah indeksnya.

**Pro tip:** Jika grid Anda mendukung kolom bernama, Anda dapat mengganti kolom numerik dengan kunci, misalnya `grid.getCell(2, "price")`.

## Step 2: Grab the Textbox Inside That Cell

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **Apa yang terjadi:**  
> Sebagian besar implementasi grid membungkus konten yang dapat diedit di dalam elemen `<input>` atau `<textarea>` dan mengekspornya sebagai `cell.textbox`. Mengambil referensi ini memungkinkan kita memanipulasi gaya visualnya secara langsung.

Jika grid menggunakan nama properti yang berbeda (seperti `cell.editor`), cukup sesuaikan kode—ini adalah variasi umum ketika Anda **cara menata kotak teks** untuk komponen kustom.

## Step 3: Define the Desired Font Properties

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Memecah Objek

| Properti | Tujuan | Contoh Nilai |
|----------|--------|--------------|
| `family` | Keluarga font – mengontrol jenis huruf. | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | Ukuran font dalam piksel (atau poin, tergantung grid). | `12`, `14`, `16` |
| `color`  | Warna teks dalam format CSS apa pun. | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **Mengapa kami menggunakan objek:**  
> Menggabungkan tiga atribut tersebut membuat kode lebih rapi dan mencerminkan cara banyak pustaka UI mengharapkan informasi gaya. Ini juga memungkinkan Anda **mengubah keluarga font grid** atau **mengatur warna font secara programatik** dengan satu penugasan.

## Step 4: Apply the Font Style to the Textbox

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **Di balik layar:**  
> Komponen kotak teks pada grid menafsirkan properti `font` dan memperbarui CSS‑nya sesuai. Satu baris ini menggantikan keluarga font, ukuran, dan warna sebelumnya sekaligus—tepat apa yang Anda butuhkan ketika **mengubah font kotak teks** di banyak sel.

Jika komponen menggunakan API yang berbeda (misalnya `textbox.style.fontFamily = ...`), sesuaikan penugasan tetapi pertahankan prinsip yang sama.

## Full Working Example

Berikut potongan kode mandiri yang dapat Anda tempel ke dalam file HTML yang menyertakan objek grid tiruan. Potongan ini mendemonstrasikan alur lengkap dari langkah 1 hingga langkah 4, plus verifikasi cepat bahwa gaya telah berubah.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Expected Output

- Kotak teks yang berada di **baris 2, kolom 3** kini menampilkan teks dengan **Arial**, **14 px**, dan warna biru **#0066CC**.
- Membuka konsol browser akan mencetak sesuatu seperti:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

Jika Anda membuka halaman, Anda akan melihat perubahan secara visual—tidak ada lagi font sistem default.

## Frequently Asked Questions (FAQ)

### Apakah saya dapat mengubah hanya ukuran font tanpa memengaruhi keluarga atau warna?
Tentu saja. Cukup hilangkan properti yang tidak ingin Anda ubah:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### Bagaimana jika grid saya menggunakan nama properti yang berbeda untuk kotak teks?
Periksa objek sel di konsol (`console.log(cell)`). Anda kemungkinan akan melihat sesuatu seperti `cell.editor` atau `cell.input`. Ganti `cell.textbox` dengan referensi yang tepat.

### Bagaimana cara menerapkan gaya yang sama ke seluruh kolom?
Lakukan iterasi pada baris dan tetapkan font untuk setiap sel di kolom tersebut:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### Apakah ada cara untuk mengembalikan ke font asli?
Simpan gaya asli sebelum menimpa:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Tips & Best Practices

- **Pembaruan batch:** Jika Anda perlu menata banyak sel, bungkus perubahan dalam `requestAnimationFrame` atau metode batch khusus grid untuk menghindari thrashing tata letak.
- **Font responsif:** Gunakan satuan relatif (`em`, `rem`) alih-alih piksel tetap jika UI Anda harus berskala.
- **Aksesibilitas:** Pastikan kontras yang cukup saat Anda **mengatur warna font secara programatik**—WCAG AA minimum adalah rasio 4.5:1 untuk teks normal.
- **Quirks lintas‑browser:** Beberapa grid lama mungkin memerlukan penetapan `style.fontFamily` langsung pada elemen `<input>` alih-alih menggunakan objek `font`.

## Conclusion

Kami baru saja membahas **cara mengubah font kotak teks** di dalam grid, mulai dari mengambil sel yang tepat hingga mendefinisikan objek `fontStyle` yang dapat digunakan kembali dan menerapkannya dalam satu baris. Sepanjang jalan kami juga belajar **mengubah ukuran font sel**, **mengatur warna font secara programatik**, dan bahkan menyesuaikan **mengubah keluarga font grid** untuk kolom tertentu.

Sekarang Anda dapat mengambil pola ini dan menyesuaikannya dengan pustaka UI apa pun—baik Anda membangun dasbor admin, editor ala spreadsheet, atau alat pelaporan kustom. Bereksperimenlah dengan keluarga, ukuran, dan warna yang berbeda; mungkin tambahkan efek hover atau penataan kondisional berdasarkan nilai data.

Punya tantangan penataan lain? Tinggalkan komentar, dan mari kita selesaikan bersama. Selamat coding!

## What Should You Learn Next?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑per‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Cara Mengubah Warna Font di Excel Menggunakan Aspose.Cells untuk Java: Panduan Lengkap](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Ubah Warna Font Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Ubah Warna Font Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}