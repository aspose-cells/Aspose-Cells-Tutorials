---
category: general
date: 2026-06-30
description: Pelajari cara mendapatkan alamat sel yang dipilih, memperbarui nilai
  sel grid, dan membaca nilai input dengan JavaScript menggunakan GridJs. Kode dan
  tips langkah demi langkah.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: id
og_description: Dapatkan alamat sel yang dipilih, perbarui nilai sel grid, dan baca
  nilai input dengan JavaScript. Ikuti panduan lengkap ini untuk integrasi GridJs
  yang mulus.
og_title: Dapatkan Alamat Sel yang Dipilih – Tutorial Lengkap GridJs JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Dapatkan Alamat Sel yang Dipilih di GridJs – Panduan JavaScript Lengkap
url: /id/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dapatkan Alamat Sel yang Dipilih – Tutorial Lengkap GridJs JavaScript

Pernahkah Anda perlu **mendapatkan alamat sel yang dipilih** dari tabel GridJs tetapi tidak yakin panggilan API mana yang harus digunakan? Anda bukan satu‑satunya. Di banyak panel admin, pengguna mengklik sebuah sel, mengedit nilai dalam modal, dan mengharapkan grid menampilkan perubahan secara langsung. Tutorial ini menunjukkan cara tepat untuk mengambil alamat tersebut, membaca harga baru dari bidang input, dan **memperbarui nilai sel grid** tanpa memuat ulang halaman.

Kami juga akan membahas **membaca nilai input dengan JavaScript** dengan cara yang benar, menangani kasus tepi, dan menutup modal setelah pembaruan selesai. Pada akhir tutorial Anda akan memiliki potongan kode mandiri yang dapat disisipkan ke proyek apa pun yang menggunakan GridJs.

## Apa yang Akan Anda Bangun

- Tabel HTML sederhana yang didukung oleh GridJs.  
- Modal penyuntingan yang muncul ketika sebuah sel diklik.  
- JavaScript yang **mendapatkan alamat sel yang dipilih**, mengambil harga yang diketik pengguna, **memperbarui nilai sel grid**, dan akhirnya menyembunyikan modal.

Tidak diperlukan pustaka eksternal selain GridJs, dan kode ini bekerja pada browser modern (Chrome 102+, Edge, Firefox). Jika Anda sudah memiliki instance GridJs di halaman, Anda dapat menyalin‑tempel bagian yang relevan secara langsung.

## Prasyarat

- Pengetahuan dasar tentang JavaScript dan DOM.  
- Pustaka GridJs sudah dimuat (melalui CDN atau npm).  
- Halaman yang sudah menampilkan grid GridJs (kami akan menunjukkan contoh minimal).

Jika ada yang terasa belum familiar, jangan khawatir—setiap langkah menyertakan rangkuman singkat.

---

## Langkah 1: Siapkan Kerangka HTML

Pertama, susun kontainer tabel, modal tersembunyi, dan input harga. Modal akan ditampilkan dengan kelas CSS sederhana.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Pro tip:** `#editModal` menggunakan trik CSS minimal—cukup tambahkan kelas `active` untuk menampilkannya. Anda dapat menggantinya dengan Bootstrap, Tailwind, atau komponen modal apa pun yang sudah Anda gunakan.

---

## Langkah 2: Inisialisasi GridJs dan Tangkap Klik Sel

Sekarang kita akan membuat grid dengan data contoh dan mendengarkan pemilihan sel. Ketika pengguna mengklik sebuah sel, kita akan **mendapatkan alamat sel yang dipilih** dan membuka modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Mengapa ini berhasil:** `GridJs.getSelectedCell()` mengembalikan string seperti `"C2"` (kolom C, baris 2). Menyimpannya dalam `lastSelectedCell` memungkinkan kita merujuk ke lokasi tepat ketika nanti **memperbarui nilai sel grid**.

---

## Langkah 3: Baca Harga Baru dari Bidang Input

Saat pengguna mengklik **Save**, kita perlu **membaca nilai input dengan JavaScript** secara aman. Langkah ini juga memvalidasi bahwa harga yang dimasukkan adalah angka positif.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Catatan:** Menggunakan `parseFloat` memastikan kita menerima desimal (misalnya `1.99`). Guard `isNaN` mencegah pengiriman kosong yang tidak sengaja.

---

## Langkah 4: Perbarui Nilai Sel yang Dipilih

Sekarang kita akhirnya **memperbarui nilai sel grid** menggunakan alamat yang telah kita tangkap sebelumnya. Metode `updateCell` milik GridJs mengembalikan sebuah promise, sehingga kita dapat menambahkan aksi menutup modal secara berantai.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **Mengapa menggunakan promise?** GridJs mungkin perlu merender ulang tabel atau menyinkronkan dengan backend. Dengan menunggu promise, kita menjamin UI hanya tersembunyi setelah grid menampilkan nilai baru.

---

## Langkah 5: Tangani Cancel dan Kasus Tepi

Solusi yang kuat selalu memberi pengguna jalan keluar. Tombol **Cancel** hanya menyembunyikan modal dan menghapus alamat yang tersimpan.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### Bagaimana Jika Tidak Ada Sel yang Dipilih?

Jika pengguna secara tidak sengaja menekan tombol **Save** tanpa mengklik sel terlebih dahulu (mungkin mereka membuka modal secara programatik), `lastSelectedCell` akan bernilai `null`. Pengembalian awal dalam `updateSelectedCell` mencegah error runtime dan mencatat peringatan yang membantu.

### Menghadapi Grid Besar

Untuk grid dengan pagination, `GridJs.getSelectedCell()` tetap mengembalikan alamat absolut (misalnya `"B12"`), bukan hanya baris yang terlihat. Ini berarti pembaruan tetap berfungsi meski baris yang diedit berada di halaman lain. Hanya perlu diingat bahwa UI tidak otomatis berpindah halaman setelah pembaruan—jika Anda memerlukannya, panggil `grid.forceUpdate()` atau navigasikan ke halaman yang sesuai secara manual.

---

## Contoh Kerja Lengkap

Berikut adalah kode lengkap yang dapat Anda salin‑tempel ke satu berkas HTML. Buka di browser, klik sel mana saja, ubah harga, dan saksikan grid memperbarui secara langsung.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Get Address, Cell Count, and Offset for Entire Excel Range](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Get Address Cell Count And Offset For Entire Excel Range](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}