---
category: general
date: 2026-03-21
description: Buat buku kerja Excel dan impor tabel data ke Excel sambil mengatur gaya
  kolom, ekspor data ke Excel, dan format tanggal sel Excel dalam menit.
draft: false
keywords:
- create excel workbook
- import datatable to excel
- set column style
- export data to excel
- format excel cells date
language: id
og_description: Buat workbook Excel dengan cepat. Pelajari cara mengimpor datatable
  ke Excel, mengatur gaya kolom, mengekspor data ke Excel, dan memformat tanggal sel
  Excel dalam satu panduan.
og_title: Buat Workbook Excel – Tutorial Lengkap tentang Pemformatan dan Ekspor
tags:
- C#
- Aspose.Cells
- Excel automation
title: Buat Workbook Excel dengan Tabel Bergaya – Panduan Langkah demi Langkah
url: /id/net/excel-workbook/create-excel-workbook-with-styled-table-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Workbook Excel – Tutorial Pemrograman Lengkap

Pernahkah Anda perlu **create excel workbook** yang tampak rapi langsung dari kode? Mungkin Anda menarik data dari basis data, dan ingin tanggal‑tanggalnya muncul dalam format yang tepat tanpa harus mengutak‑atik di Excel nanti. Itu adalah titik sakit yang umum—terutama ketika outputnya dikirim ke kotak masuk klien dan mereka mengharapkan semuanya siap pakai.

Dalam panduan ini kami akan membahas solusi tunggal yang **imports datatable to excel**, menerapkan **set column style**, dan akhirnya **export data to excel** sebagai file yang diformat dengan baik. Anda akan melihat secara tepat cara **format excel cells date** sehingga spreadsheet terbaca seperti laporan profesional, dan Anda akan mendapatkan contoh lengkap yang dapat dijalankan di akhir. Tanpa bagian yang hilang, tanpa shortcut “lihat dokumen”—hanya kode murni yang dapat Anda masukkan ke proyek Anda hari ini.

---

## Apa yang Akan Anda Pelajari

- Cara **create excel workbook** menggunakan pustaka Aspose.Cells (atau API kompatibel lainnya).
- Cara tercepat untuk **import datatable to excel** tanpa loop sel‑per‑sel manual.
- Teknik untuk **set column style**, termasuk menerapkan format tanggal pada kolom tertentu.
- Cara **export data to excel** dengan satu panggilan `Save`.
- Kesalahan umum saat Anda mencoba **format excel cells date** dan cara menghindarinya.

### Prasyarat

- .NET 6+ (atau .NET Framework 4.6+).  
- Aspose.Cells untuk .NET terpasang (`Install-Package Aspose.Cells`).  
- Sebuah `DataTable` yang siap diekspor—sumber data Anda bisa berupa SQL, CSV, atau apa pun yang dapat diubah menjadi `DataTable`.

Jika Anda sudah nyaman dengan C# dan memiliki semua komponen tersebut, Anda siap melanjutkan. Jika tidak, bagian “Prasyarat” di atas memberikan daftar periksa singkat.

---

## Langkah 1 – Buat Instance Workbook Excel

Hal pertama yang Anda lakukan ketika ingin **create excel workbook** secara programatis adalah menginstansiasi objek workbook. Anggap ini sebagai membuka buku catatan kosong di mana Anda akan menuliskan data nanti.

```csharp
using Aspose.Cells;
using System.Data;

// Step 1: Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();
```

> **Mengapa ini penting:**  
> Kelas `Workbook` adalah titik masuk untuk setiap operasi di Aspose.Cells. Membuatnya di awal memberi Anda kanvas bersih, dan Anda dapat memuat file yang sudah ada nanti jika perlu menambahkan data alih‑alih memulai dari nol.

---

## Langkah 2 – Siapkan DataTable untuk Diimpor

Sebelum kita dapat **import datatable to excel**, kita memerlukan sebuah `DataTable`. Dalam proyek nyata ini biasanya berasal dari `SqlDataAdapter.Fill` atau `DataTable.Load`. Untuk kejelasan, kami akan menyiapkan metode stub yang mengembalikan tabel siap pakai.

```csharp
// Step 2: Obtain the data to be written – a DataTable with three columns
DataTable dataTable = GetData();   // assume GetData() returns the required table

// Example implementation (you can replace this with your own data source)
DataTable GetData()
{
    DataTable dt = new DataTable();
    dt.Columns.Add("OrderDate", typeof(DateTime));
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Quantity", typeof(int));

    dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
    dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
    dt.Rows.Add(DateTime.Today, "Cherries", 60);
    return dt;
}
```

> **Tip:** Jika tanggal Anda disimpan sebagai string, konversikan terlebih dahulu ke `DateTime`—jika tidak, langkah **format excel cells date** tidak akan berfungsi sebagaimana mestinya.

---

## Langkah 3 – Definisikan Gaya untuk Setiap Kolom (Set Column Style)

Sekarang tiba saatnya kita **set column style**. Kami akan membuat array objek `Style`—satu per kolom. Kolom pertama mendapatkan format tanggal bawaan (kode 14), sementara kolom lainnya tetap dengan format umum (kode 0).

```csharp
// Step 3: Define a style for each column; apply a date format to the first column
Style[] columnStyles = new Style[3];
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = workbook.CreateStyle();
    columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date format, 0 = general
}
```

> **Mengapa menggunakan objek style?**  
> Menerapkan style sekali dan menggunakannya kembali jauh lebih efisien daripada mengatur format pada setiap sel secara individual. Ini juga menjamin seluruh kolom mematuhi aturan **format excel cells date** yang sama, yang penting untuk konsistensi saat file dibuka di locale yang berbeda.

---

## Langkah 4 – Impor DataTable dengan Gaya ke Worksheet

Dengan workbook siap dan style telah didefinisikan, kini kita **import datatable to excel**. Metode `ImportDataTable` melakukan pekerjaan berat: menulis header kolom, baris‑baris, dan menerapkan style yang kami berikan.

```csharp
// Step 4: Access the first worksheet and import the DataTable using the styles
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

> **Apa yang terjadi di balik layar?**  
> - `true` memberi tahu Aspose.Cells untuk menyertakan nama kolom sebagai baris pertama.  
> - `0, 0` adalah indeks baris dan kolom awal (pojok kiri‑atas).  
> - `columnStyles` menyelaraskan setiap kolom dengan style yang kami siapkan, memastikan aturan **format excel cells date** diterapkan pada kolom tanggal.

---

## Langkah 5 – Simpan (Ekspor) Workbook ke File Fisik

Akhirnya, kami **export data to excel** dengan menyimpan workbook ke disk. Anda dapat mengubah jalur ke folder mana pun, atau bahkan mengalirkan file langsung ke respons HTTP untuk API web.

```csharp
// Step 5: Save the workbook with the styled table
workbook.Save("YOUR_DIRECTORY/StyledTable.xlsx");
```

> **Pro tip:** Gunakan `workbook.Save(Stream, SaveFormat.Xlsx)` ketika Anda perlu mengirim file melalui jaringan tanpa menulis ke disk.

---

## Contoh Kerja Penuh (Semua Langkah Digabung)

Berikut adalah program lengkap yang siap dijalankan. Salin‑tempel ke aplikasi console, sesuaikan jalur output, dan Anda akan memiliki file Excel yang diformat dengan baik dalam hitungan detik.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // 1️⃣ Create the workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Get the data (replace GetData with your own source if needed)
        DataTable dataTable = GetData();

        // 3️⃣ Prepare column styles – date format for the first column
        Style[] columnStyles = new Style[3];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            columnStyles[i] = workbook.CreateStyle();
            columnStyles[i].Number = (i == 0) ? 14 : 0;   // 14 = date, 0 = general
        }

        // 4️⃣ Import the DataTable with the styles
        Worksheet worksheet = workbook.Worksheets[0];
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 5️⃣ Save the file
        workbook.Save("StyledTable.xlsx");

        Console.WriteLine("Excel workbook created successfully!");
    }

    // Sample data generator – replace with real data source
    static DataTable GetData()
    {
        DataTable dt = new DataTable();
        dt.Columns.Add("OrderDate", typeof(DateTime));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(DateTime.Today.AddDays(-2), "Apples", 120);
        dt.Rows.Add(DateTime.Today.AddDays(-1), "Bananas", 85);
        dt.Rows.Add(DateTime.Today, "Cherries", 60);
        return dt;
    }
}
```

**Output yang Diharapkan:**  
Saat Anda membuka `StyledTable.xlsx`, kolom A menampilkan tanggal seperti `03/19/2026` (tergantung locale Anda), sementara kolom B dan C menampilkan nama produk dan kuantitas sebagai teks/angka biasa. Tidak ada langkah format tambahan yang diperlukan—proses **create excel workbook** Anda selesai.

---

## Pertanyaan yang Sering Diajukan & Kasus Tepi

### 1️⃣ Bagaimana jika DataTable saya memiliki lebih dari tiga kolom?
Tambahkan lebih banyak objek `Style` ke array `columnStyles`, dan sesuaikan properti `Number` untuk kolom mana pun yang memerlukan format khusus (misalnya, mata uang, persentase). Metode `ImportDataTable` akan mencocokkan setiap style berdasarkan posisi.

### 2️⃣ Bisakah saya menerapkan format tanggal khusus alih‑alih kode bawaan 14?
Tentu saja. Ganti `columnStyles[i].Number = 14;` dengan:

```csharp
columnStyles[i].Number = 22;               // built‑in custom format ID
columnStyles[i].Custom = "dd‑MMM‑yyyy";    // or any .NET date pattern you like
```

### 3️⃣ Bagaimana cara **export data to excel** dalam API web tanpa menulis ke disk?
Gunakan `MemoryStream`:

```csharp
using (var ms = new MemoryStream())
{
    workbook.Save(ms, SaveFormat.Xlsx);
    ms.Position = 0;
    // return File(ms.ToArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "Report.xlsx");
}
```

### 4️⃣ Bagaimana jika locale pengguna mengharapkan pemisah tanggal yang berbeda?
Format tanggal bawaan (ID 14) menghormati pengaturan locale workbook. Jika Anda memerlukan format tetap terlepas dari locale, gunakan properti `Custom` seperti yang ditunjukkan di atas.

### 5️⃣ Apakah ini bekerja dengan .NET Core?
Ya—Aspose.Cells mendukung .NET Standard 2.0 dan yang lebih baru, sehingga kode yang sama berjalan di .NET 6, .NET 7, atau runtime kompatibel lainnya.

---

## Tips Praktik Terbaik (Pro Tips)

- **Gunakan kembali style**: Membuat style per kolom memang murah, tetapi menggunakan kembali objek style yang sama untuk kolom identik menghemat memori.
- **Hindari loop sel‑per‑sel**: `ImportDataTable` sangat dioptimalkan; loop manual lebih lambat dan rawan kesalahan.
- **Setel budaya workbook lebih awal** jika Anda memerlukan pemisah angka/tanggal yang konsisten di semua lingkungan:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("en-US");
```

- **Validasi DataTable** sebelum impor—tanggal null akan menyebabkan pengecualian saat style tanggal diterapkan.
- **Aktifkan perhitungan** jika Anda menambahkan formula setelah impor:

```csharp
workbook.CalculateFormula();
```

---

## Kesimpulan

Anda kini memiliki resep lengkap, ujung‑ke‑ujung untuk **create excel workbook**, **import datatable to excel**, **set column style**, **export data to excel**, dan **format excel cells date**—semua dalam kurang dari selusin baris kode C#. Pendekatan ini cepat, dapat diandalkan, dan menempatkan urusan format di dalam kode, sehingga spreadsheet akhir siap untuk pengguna bisnis begitu mereka membukanya.

Siap untuk tantangan berikutnya? Coba tambahkan conditional formatting, sisipkan chart, atau konversi file…

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}