---
category: general
date: 2026-06-30
description: Cara membuat gridjs dengan mudah menggunakan contoh JavaScript lengkap,
  mencakup konfigurasi gridjs, penyiapan kontainer, dan proses render.
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: id
og_description: Cara membuat gridjs dengan mudah menggunakan contoh JavaScript lengkap,
  mencakup konfigurasi gridjs, penyiapan kontainer, dan proses render.
og_title: Cara Membuat Gridjs – Panduan Lengkap Grid JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Cara Membuat Gridjs – Panduan Lengkap Grid JavaScript
url: /id/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Gridjs – Panduan Lengkap JavaScript Grid

Pernah bertanya-tanya **how to create gridjs** dan langsung melihat tabel data yang keren di halaman Anda? Anda bukan satu-satunya. Banyak pengembang mengalami kebuntuan saat pertama kali mencoba menghubungkan Gridjs, terutama pada objek konfigurasi dan pemanggilan render. Kabar baiknya? Ini sebenarnya sangat mudah setelah Anda mengetahui langkah yang tepat.

Dalam tutorial ini kami akan membahas contoh dunia nyata yang menunjukkan **how to create gridjs** dari awal, cara membuat **gridjs configuration** yang tepat, cara mengikat grid ke **gridjs container**, dan akhirnya cara memicu **gridjs render**. Pada akhir tutorial Anda akan memiliki grid yang berfungsi penuh yang dapat Anda sisipkan ke proyek mana pun—tanpa misteri, hanya kode yang jelas.

## Apa yang Akan Anda Pelajari

- Siapkan halaman HTML minimal yang siap untuk Gridjs.
- Tulis objek **gridjs configuration** yang mendefinisikan kolom, data, dan opsi.
- Lampirkan instance Gridjs ke elemen **gridjs container**.
- Panggil **gridjs render** untuk menampilkan tabel.
- Sesuaikan pengaturan umum (pagination, sorting, styling) dan hindari jebakan umum.

Tidak diperlukan alat build eksternal; semuanya berjalan di browser dengan satu tag script. Mari kita mulai.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

1. Browser modern (Chrome, Edge, Firefox, Safari) – apa saja yang mendukung ES6.
2. Pengetahuan dasar tentang HTML dan JavaScript – Anda tidak memerlukan framework.
3. Akses ke pustaka Gridjs – kami akan mengambilnya dari CDN, jadi tidak perlu instalasi npm.

Itu saja. Jika Anda sudah memiliki halaman yang ingin ditingkatkan, Anda dapat menempelkan potongan kode langsung di dalamnya.

## Langkah 1: Tambahkan Aset Gridjs ke Halaman Anda

Pertama, kita perlu memuat file CSS dan JavaScript Gridjs. Versi CDN ringan dan sempurna untuk demo cepat.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro tip:** Tema Mermaid memberikan tabel tampilan bersih dan modern tanpa CSS tambahan. Silakan ganti dengan `classic.min.css` jika Anda lebih suka gaya lain.

## Langkah 2: Definisikan **gridjs container**

**gridjs container** hanyalah `<div>` biasa yang akan menampung tabel yang dirender. Pada markup di atas kami sudah membuat `<div id="grid"></div>`. Atribut `id` sangat penting karena nanti kami akan menggunakannya untuk mengikat instance Gridjs.

Jika Anda membutuhkan beberapa grid pada halaman yang sama, berikan setiap container ID unik (`grid1`, `grid2`, …) dan ulangi logika binding untuk masing‑masing.

## Langkah 3: Buat Objek **gridjs configuration** 

Sekarang tiba pada inti **how to create gridjs** – konfigurasi. Objek JavaScript sederhana ini memberi tahu Gridjs kolom apa yang ditampilkan, data apa yang diisi, dan fitur mana yang diaktifkan.

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Mengapa konfigurasi ini penting

- **Columns** – mendefinisikan teks header dan lebar opsional. Tanpa ini, Gridjs akan menebak nama kolom dari baris data pertama, yang sering kurang terbaca.
- **Data** – array baris, setiap baris berupa array nilai sel. Anda juga dapat menyediakan fungsi async yang mengambil data dari API; pustaka akan menangani promise secara otomatis.
- **Pagination** – membatasi jumlah baris per halaman, mencegah tabel besar membebani UI.
- **Search & Sort** – mengaktifkan fitur interaktif dengan satu boolean, menghemat Anda dari menulis handler khusus.
- **Language** – menyesuaikan string UI, sempurna untuk lokalisasi atau branding.

Silakan ganti array data statis dengan panggilan fetch nanti; langkah-langkah lainnya tetap sama persis.

## Langkah 4: Instansiasi Gridjs dan Bind ke **gridjs container**

Dengan konfigurasi siap, kami membuat `GridJs.Grid` baru (nama kelasnya adalah `gridjs.Grid` pada build UMD) dan menunjukannya ke elemen container kami.

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

Perhatikan kami menggunakan `document.getElementById('grid')`—itu adalah **gridjs container** yang kami definisikan sebelumnya. Jika Anda memiliki beberapa container, cukup ulangi baris ini dengan ID yang sesuai.

## Langkah 5: Panggil **gridjs render** 

Bagian akhir dari puzzle adalah metode **gridjs render**. Metode ini mengambil konfigurasi yang kami berikan sebelumnya dan menyuntikkan `<table>` yang sepenuhnya bergaya ke dalam container.

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

Itu saja! Saat Anda membuka halaman di browser, Anda akan melihat tabel yang dapat dicari dan dipaginasi dengan empat baris yang kami definisikan. Kotak pencarian muncul otomatis di atas, dan kontrol pagination berada di bagian bawah.

### Output yang Diharapkan

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

UI akan menyesuaikan ketika Anda mengetik di kotak pencarian atau mengklik header kolom untuk mengurutkan.

## Variasi Umum & Kasus Edge

### Memuat Data Secara Asinkron

Jika data Anda berada di server, ganti array `data` statis dengan fungsi yang mengembalikan Promise:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Gridjs akan menampilkan spinner loading hingga promise selesai, kemudian merender tabel secara otomatis.

### Rendering Sel Kustom

Terkadang Anda membutuhkan ikon, tombol, atau tanggal terformat di dalam sel. Gunakan properti `formatter` pada kolom:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

Helper `gridjs.h` membuat elemen virtual DOM tanpa harus mengimpor React.

### Beberapa Grid pada Satu Halaman

Cukup ulangi langkah 2‑5 dengan ID container yang berbeda:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

Setiap grid beroperasi secara independen, sehingga Anda dapat mencampur batas pagination, set kolom, bahkan tema.

## Tips Pro & Jebakan yang Harus Dihindari

- **Don’t forget the CSS** – tanpa stylesheet tabel akan muncul sebagai tabel HTML biasa, kehilangan semua styling cantik dan kontrol pagination.
- **Avoid duplicate IDs** – setiap **gridjs container** harus memiliki ID unik; jika tidak Gridjs akan menimpa instance pertama.
- **Watch the data shape** – jumlah kolom harus cocok dengan jumlah sel di setiap baris; array yang tidak cocok menyebabkan glitch layout yang tidak terlihat.
- **Use `gridjs.h` for complex cells** – mencoba menyuntikkan string HTML mentah dapat merusak algoritma diffing virtual DOM.
- **Mind the version** – tautan CDN di atas mengarah ke rilis 5.x terbaru (per Juni 2026). Jika Anda mengunci ke versi lama, beberapa opsi (seperti `language`) mungkin tidak ada.

## Contoh Lengkap yang Berfungsi (Copy‑Paste)

Berikut adalah file HTML lengkap yang dapat Anda simpan sebagai `gridjs-demo.html` dan buka langsung di browser.



## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Aspose.Cells for Java&#58; Cara Membuat dan Memformat Workbook Excel Secara Efisien](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Cara Membuat dan Mengekspor Excel ke HTML Menggunakan Aspose.Cells Java | Panduan Operasi Workbook](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Cara Membuat dan Menggabungkan Workbook Excel Menggunakan Aspose.Cells untuk Java | Panduan Lengkap](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}