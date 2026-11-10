---
category: general
date: 2026-10-01
description: Pelajari cara menambahkan properti khusus ke buku kerja Excel menggunakan
  Aspose.Cells. Panduan ini juga menunjukkan cara menambahkan ID proyek dan membaca
  properti khusus.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: id
lastmod: 2026-10-01
og_description: Tambahkan properti khusus ke buku kerja Excel dengan Aspose.Cells.
  Ikuti tutorial lengkap ini untuk menambahkan ID proyek, mengatur info peninjau,
  dan membaca properti khusus secara programatis.
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Menambahkan properti khusus ke buku kerja Excel – panduan langkah demi langkah
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara menambahkan properti khusus ke buku kerja Excel
url: /id/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menambahkan properti khusus ke workbook Excel

Jika Anda perlu **menambahkan properti khusus** ke workbook Excel, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells untuk .NET. Anda juga akan belajar cara menambahkan ID proyek, mengatur nama reviewer, dan kemudian **membaca properti khusus** kembali dari file.

Bekerja dengan metadata khusus memungkinkan Anda menyematkan informasi spesifik bisnis langsung di dalam spreadsheet, memudahkan pelacakan kepemilikan, versi, atau konteks lain tanpa harus memelihara basis data terpisah. Langkah‑langkah di bawah ini mencakup alur kerja end‑to‑end lengkap, mulai dari membuat workbook hingga menyimpan properti baru.

## Prasyarat

* .NET 6.0 atau lebih baru terpasang  
* Lisensi Aspose.Cells untuk .NET yang valid (atau percobaan gratis)  
* Visual Studio 2022 (atau IDE C# apa pun)  

Tidak ada paket NuGet tambahan yang diperlukan selain `Aspose.Cells`.

## Langkah 1: Siapkan proyek dan impor namespace

Buat aplikasi console baru dan tambahkan referensi Aspose.Cells:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

Namespace `Aspose.Cells` berisi kelas `Workbook`, `Worksheet`, dan `CustomPropertyCollection` yang akan kita gunakan.

## Langkah 2: Muat workbook yang ada (atau buat yang baru)

Anda dapat memulai dengan file `.xlsb` yang sudah ada atau membuat workbook baru. Contoh di bawah memuat file bernama **Data.xlsb** yang berada di folder bernama `YOUR_DIRECTORY`.

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

Jika file tidak ada, ganti kode dengan `new Workbook();` untuk membuat workbook kosong.

## Langkah 3: Tambahkan properti khusus ke lembar kerja pertama

Operasi utama adalah **menambahkan properti khusus** ke sebuah worksheet. Aspose.Cells menyimpan properti khusus dalam sebuah koleksi yang berperilaku seperti kamus.

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

Alasan kami menggunakan `CustomProperties.Add` alih‑alih `CustomProperties["Name"] = value` adalah karena metode `Add` membuat entri jika belum ada dan menjamin tipe data yang benar disimpan. Pendekatan ini mencegah ketidaksesuaian tipe secara tidak sengaja yang dapat menyebabkan error runtime saat membaca nilai nanti.

## Langkah 4: Simpan workbook dengan properti baru

Setelah Anda menyuntikkan metadata, simpan perubahan ke file baru sehingga file asli tetap tidak tersentuh.

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Pada titik ini file Excel berisi metadata khusus yang Anda definisikan. Anda dapat memverifikasi properti tersebut menggunakan langkah‑langkah pada bagian berikutnya.

## Langkah 5: Baca properti khusus dari workbook

Membaca **properti khusus Excel** mengikuti pola koleksi yang sama. Potongan kode ini menunjukkan cara mengambil nilai yang baru saja disimpan.

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`Indexer` `CustomPropertyCollection` mengembalikan objek `CustomProperty`; mengakses properti `Value`‑nya memberikan data yang disimpan dalam tipe aslinya. Memeriksa `null` sebelum melakukan casting menghindari `NullReferenceException` jika properti tidak ada.

### Output konsol yang diharapkan

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

Timestamp akan mencerminkan momen tepat ketika Anda memanggil `Add` pada langkah 3.

## Tips profesional: Memperbarui properti khusus yang ada

Jika Anda perlu **menambahkan informasi khusus** nanti (misalnya, mengubah reviewer), gunakan setter `CustomPropertyCollection`:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

Pola ini memastikan bahwa properti akan diperbarui atau dibuat, yang berguna dalam alur kerja iteratif seperti pembuatan laporan otomatis.

## Langkah 6: Verifikasi properti di dalam Excel (opsional)

Anda juga dapat melihat properti khusus langsung di Excel:

1. Buka file `DataWithProps.xlsb` yang disimpan di Microsoft Excel.  
2. Pilih **File → Info → Properties → Advanced Properties**.  
3. Pilih tab **Custom**.  

Anda akan melihat entri `ProjectId`, `Reviewer`, dan `CreatedOn` terdaftar dengan nilai masing‑masing.

## Contoh kerja lengkap

Berikut adalah program lengkap yang berdiri sendiri yang menggabungkan semua potongan kode sebelumnya. Salin ke dalam `Program.cs` dan jalankan; konsol akan menampilkan nilai yang diambil.

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

Menjalankan program ini menghasilkan output konsol yang ditunjukkan sebelumnya dan membuat `DataWithProps.xlsb` yang berisi metadata yang disematkan.

## Pertanyaan umum dan kasus tepi

| Pertanyaan | Jawaban |
|---|---|
| **Apakah saya dapat menyimpan tipe non‑primitif?** | Aspose.Cells mendukung `string`, `int`, `double`, `DateTime`, dan `bool`. Untuk objek kompleks, serialisasikan terlebih dahulu ke JSON atau XML dan simpan sebagai string. |
| **Bagaimana jika workbook dilindungi kata sandi?** | Buka workbook dengan kata sandi (`new Workbook(path, password)`) sebelum mengakses `CustomProperties`. Properti tetap dapat diakses setelah dekripsi. |
| **Apakah properti khusus tetap ada setelah konversi format?** | Saat menyimpan ke format lain (misalnya, `.xlsx`), Aspose.Cells mempertahankan properti khusus selama format target mendukungnya. |
| **Bagaimana cara menghapus properti khusus?** | Gunakan `worksheet.CustomProperties.Remove("PropertyName");`. Ini menghapus entri dari koleksi. |

## Langkah selanjutnya

Sekarang Anda sudah tahu cara **menambahkan properti khusus**, Anda dapat menjelajahi topik terkait seperti:

* **excel custom properties** untuk versioning dokumen  
* **read custom properties** dari beberapa worksheet dalam satu workbook  
* Menggunakan **Aspose.Cells** untuk membuat pivot table yang merujuk ke metadata khusus  
* Mengekspor workbook ke PDF sambil mempertahankan properti khusus  

Bereksperimenlah dengan berbagai tipe data, gabungkan properti khusus dengan komentar sel, atau integrasikan metadata ke dalam sistem manajemen dokumen yang lebih besar.

---

**Siap mengotomatisasi pelaporan Excel Anda?** Tambahkan kode di atas ke proyek Anda, sesuaikan nama properti agar sesuai dengan kebutuhan bisnis Anda, dan Anda akan memiliki spreadsheet yang dapat menjelaskan dirinya sendiri siap untuk proses selanjutnya.

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Excel – Tambahkan Properti Khusus dan Simpan sebagai XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [Cara Mengakses Properti Dokumen Khusus di Excel Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Menguasai Properti Khusus Excel Menggunakan Aspose.Cells .NET untuk Manajemen Data yang Ditingkatkan](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}