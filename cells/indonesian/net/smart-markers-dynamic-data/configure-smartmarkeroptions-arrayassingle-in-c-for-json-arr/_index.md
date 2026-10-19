---
category: general
date: 2026-09-21
description: Konfigurasikan SmartMarkerOptions ArrayAsSingle di C# untuk mengekspor
  array JSON sebagai nilai sel tunggal dalam buku kerja Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: id
lastmod: 2026-09-21
og_description: Konfigurasikan SmartMarkerOptions ArrayAsSingle di C# untuk mengekspor
  array JSON sebagai nilai sel tunggal. Pelajari solusi lengkap langkah demi langkah.
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: Konfigurasikan SmartMarkerOptions ArrayAsSingle di C# – panduan lengkap
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Konfigurasikan SmartMarkerOptions ArrayAsSingle di C# untuk array JSON
url: /id/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Konfigurasi SmartMarkerOptions ArrayAsSingle di C# untuk array JSON

Jika Anda perlu **mengonfigurasi SmartMarkerOptions ArrayAsSingle** saat menghasilkan file Excel dengan Aspose.Cells, panduan ini menunjukkan secara tepat cara melakukannya. Anda akan melihat cara menjaga array JSON tetap utuh dalam satu sel alih‑alih menyebarkan elemennya ke beberapa baris.

Bekerja dengan data JSON dalam spreadsheet sering berarti memilih antara tampilan datar dan representasi yang kompak. Dalam banyak skenario pelaporan—seperti menyimpan daftar tag atau sekumpulan pengidentifikasi—Anda ingin seluruh string JSON tetap berada dalam satu sel. Flag **ArrayAsSingle** dalam `SmartMarkerOptions` memungkinkan hal itu.

Dalam tutorial ini Anda akan:

* Membuat sebuah `DataTable` yang menyimpan array JSON dalam sebuah kolom.  
* Menempatkan Smart Markers di lembar kerja Excel.  
* **Mengonfigurasi SmartMarkerOptions ArrayAsSingle** sehingga array JSON diperlakukan sebagai nilai sel tunggal.  
* Memproses marker dan menyimpan workbook.  
* Memverifikasi output.

> **Prasyarat** – Anda memerlukan pustaka Aspose.Cells untuk .NET (v23.12 atau lebih baru) dan lingkungan pengembangan .NET (Visual Studio 2022 disarankan). Pengetahuan dasar tentang C# dan DataTables diasumsikan.

---

## Langkah 1: Siapkan sumber data dengan array JSON

Pertama, bangun sebuah `DataTable` yang meniru data yang akan Anda terima dari layanan atau basis data. Kolom **Names** berisi string yang dienkode JSON yang mewakili sebuah array nama.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*Mengapa langkah ini?*  
Smart Markers membaca data langsung dari objek .NET. Dengan menempatkan array JSON dalam kolom string, Anda mempertahankan sintaks JSON yang tepat, yang kemudian dapat ditulis ke sel tanpa perubahan.

---

## Langkah 2: Sisipkan Smart Markers ke dalam workbook baru

Buat workbook baru, pilih lembar kerja pertama, dan tulis Smart Markers yang merujuk ke seluruh tabel serta kolom **Names** tertentu.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

Marker `&=dataTable.Names` memberi tahu Aspose.Cells untuk mengganti sel dengan nilai kolom **Names** untuk setiap baris dalam `dataTable`. Karena hanya ada satu baris, marker akan diproses satu kali.

---

## Langkah 3: **Konfigurasi SmartMarkerOptions ArrayAsSingle**

Secara default, Aspose.Cells memperluas string yang mirip array menjadi baris terpisah. Menetapkan `ArrayAsSingle` ke `true` menimpa perilaku tersebut, memaksa seluruh string JSON tetap berada dalam satu sel.

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*Mengapa mengaktifkan `ArrayAsSingle`?*  
Ketika `ArrayAsSingle` bernilai `false`, mesin menginterpretasikan `["Alice","Bob"]` sebagai dua nilai terpisah dan menuliskannya ke baris berdekatan. Menetapkannya ke `true` memperlakukan string sebagai nilai atomik, yang penting untuk mempertahankan format JSON di dalam Excel.

---

## Langkah 4: Proses Smart Markers dengan opsi yang dikonfigurasi

Sekarang jalankan mesin Smart Marker, dengan melewatkan objek opsi yang baru saja Anda konfigurasikan.

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

Selama pemrosesan, Aspose.Cells membaca `dataTable`, menerapkan marker, dan menghormati flag `ArrayAsSingle`, sehingga array JSON tidak diubah.

---

## Langkah 5: Simpan workbook dan verifikasi hasilnya

Akhirnya, tulis workbook ke disk. Buka file yang dihasilkan di Excel atau penampil spreadsheet apa pun untuk memastikan bahwa sel **A2** berisi string JSON yang tepat.

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Output yang Diharapkan

| A   |
|-----|
| **["Alice","Bob"]** |

Sel **A2** menampilkan array JSON sebagai nilai teks tunggal, persis seperti yang disimpan dalam `DataTable`. Tidak ada baris tambahan yang dibuat.

---

## Variasi umum dan penanganan kasus tepi

| Situasi | Cara menyesuaikan |
|-----------|--------------|
| **Multiple rows with JSON arrays** | Pengaturan `ArrayAsSingle` yang sama berfungsi; setiap array JSON pada baris tetap berada di selnya masing‑masing. |
| **Different JSON structures (objects, nested arrays)** | Selama JSON berupa string, `ArrayAsSingle` akan menjaga keutuhannya. Untuk objek kompleks Anda mungkin perlu meloloskan tanda kutip. |
| **Using a different data source (e.g., List\<T\>)** | Ganti `DataTable` dengan koleksi enumerable apa pun; sintaks marker (`&=myList.Property`) tetap sama. |
| **Exporting to CSV instead of XLSX** | `ArrayAsSingle` tetap berlaku, tetapi ingat bahwa CSV tidak mempertahankan format sel; Anda mungkin perlu membungkus JSON dalam tanda kutip. |

**Pro tip:** Selalu setel `ArrayAsSingle` *sebelum* memanggil `ProcessSmartMarkers`. Mengubah flag setelah pemrosesan tidak berpengaruh pada sel yang sudah dihasilkan.

---

## Contoh lengkap yang dapat dijalankan

Berikut adalah program lengkap yang dapat Anda salin‑tempel ke aplikasi konsol. Program ini mencakup semua direktif `using` dan komentar untuk kejelasan.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

Jalankan program, buka `SmartMarkerJson.xlsx`, dan Anda akan melihat array JSON tetap terjaga di sel **A2**.

---

## Kesimpulan

Anda kini tahu cara **mengonfigurasi SmartMarkerOptions ArrayAsSingle** di C# untuk menjaga array JSON tetap sebagai nilai sel tunggal saat menggunakan smart markers Aspose.Cells. Langkah‑langkah—menyiapkan `DataTable`, menyisipkan marker, mengatur flag `ArrayAsSingle`, memproses, dan menyimpan—membentuk pola berulang yang dapat Anda terapkan pada skenario apa pun yang memerlukan representasi JSON yang kompak di dalam Excel.

Selanjutnya, Anda mungkin ingin menjelajahi:

* **Smart markers Aspose.Cells** untuk melakukan iterasi pada koleksi.  
* Mengekspor **objek JSON bersarang** dengan menyesuaikan format sel.  
* Menggabungkan **format bersyarat** dengan smart markers untuk laporan yang lebih kaya.

Silakan bereksperimen dengan struktur data yang berbeda dan bagikan temuan Anda. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait dan membangun di atas teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Excel dari JSON – Panduan Lengkap Aspose.Cells](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Buat dan Konfigurasi Workbook Excel Aspose Cells .NET](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Buat dan Konfigurasi Workbook Excel Aspose Cells .NET](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}