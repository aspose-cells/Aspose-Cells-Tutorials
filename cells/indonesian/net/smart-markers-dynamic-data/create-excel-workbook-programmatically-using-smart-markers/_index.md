---
category: general
date: 2026-09-24
description: Buat workbook Excel secara programatis dan pelajari cara membuat beberapa
  lembar detail, kemudian simpan workbook sebagai file xlsx dengan contoh C# yang
  jelas.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook programmatically
- how to create multiple detail sheets
- save workbook as xlsx file
language: id
lastmod: 2026-09-24
og_description: Buat workbook Excel secara programatik, lihat cara membuat beberapa
  lembar detail dan menyimpan workbook sebagai file xlsx dalam satu contoh yang dapat
  dijalankan.
og_image_alt: Screenshot of an Excel workbook created programmatically in C#
og_title: Buat workbook Excel secara programatis – panduan lengkap C#
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Create Excel workbook programmatically and learn how to create multiple
    detail sheets, then save workbook as xlsx file with a clear C# example.
  headline: Create Excel workbook programmatically using Smart Markers
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
title: Buat workbook Excel secara programatis menggunakan Smart Markers
url: /id/net/smart-markers-dynamic-data/create-excel-workbook-programmatically-using-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat workbook Excel secara programatis menggunakan Smart Markers

Jika Anda perlu **membuat workbook Excel secara programatis**, panduan ini menunjukkan secara tepat cara melakukannya dengan Aspose.Cells .NET. Anda juga akan menemukan **cara membuat beberapa lembar detail** dari satu sumber data dan akhirnya **menyimpan workbook sebagai file xlsx** tanpa langkah manual apa pun.  

Solusinya lengkap: kami akan menelusuri setiap baris kode, menjelaskan mengapa setiap pengaturan penting, dan membahas jebakan umum seperti nama lembar yang duplikat. Pada akhir tutorial, Anda akan memiliki aplikasi konsol yang siap dijalankan yang menghasilkan workbook dengan lembar master dan sekumpulan lembar detail.

## Apa yang Anda butuhkan

| Prasyarat | Alasan |
|--------------|--------|
| .NET 6.0 SDK atau yang lebih baru | Menyediakan runtime untuk aplikasi konsol C# |
| Aspose.Cells untuk .NET (paket NuGet `Aspose.Cells`) | Menyediakan kelas `Workbook`, `SmartMarkerProcessor`, dan `SmartMarkerOptions` |
| Sumber data sederhana (mis., `DataTable` atau daftar objek) | Menyediakan nilai yang akan diperluas oleh Smart Markers |
| Visual Studio 2022 atau editor apa pun yang mendukung .NET | Memudahkan kompilasi dan menjalankan kode |

> **Pro tip:** Instal paket Aspose.Cells melalui CLI sebelum Anda memulai:  
> `dotnet add package Aspose.Cells`

## Langkah 1: Siapkan proyek dan impor namespace

Buat proyek konsol baru dan bawa namespace yang diperlukan ke dalam ruang lingkup.

```csharp
using System;
using System.Data;               // For DataTable (sample data source)
using Aspose.Cells;              // Core Excel API
using Aspose.Cells.SmartMarkers; // Smart Marker processing
```

*Mengapa ini penting*: `Aspose.Cells` menangani siklus hidup workbook, sementara `Aspose.Cells.SmartMarkers` memberikan Anda mesin Smart Marker yang kuat yang dapat menghasilkan banyak lembar dari satu templat.

## Langkah 2: Buat workbook Excel secara programatis

Tindakan konkret pertama adalah menginstansiasi sebuah `Workbook`. Objek ini mewakili seluruh file Excel dalam memori.

```csharp
// Step 2: Create a new workbook (or load an existing template)
Workbook workbook = new Workbook(); // an empty workbook with one default sheet
```

Jika Anda lebih suka memulai dari templat yang sudah berisi baris header atau pemformatan, ganti `new Workbook()` dengan `new Workbook("Template.xlsx")`. Sisanya proses berjalan identik.

## Langkah 3: Siapkan templat Smart Marker

Smart Markers bekerja pada isi sel yang berisi placeholder seperti `&=Employees.Name`. Untuk tutorial ini kami akan menambahkan templat sederhana langsung melalui kode, tetapi Anda juga dapat mengedit lembar secara manual di Excel.

```csharp
// Access the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];

// Write a header row
sheet.Cells["A1"].PutValue("Employee Report");

// Insert a Smart Marker that will generate a detail sheet for each employee
sheet.Cells["A3"].PutValue("&=Employees.Name");

// Optional: add column titles for the detail sheet
sheet.Cells["A4"].PutValue("Name");
sheet.Cells["B4"].PutValue("Department");
sheet.Cells["C4"].PutValue("Salary");
```

*Mengapa ini penting*: Placeholder `&=Employees.Name` memberi tahu processor Smart Marker untuk mengiterasi koleksi `Employees`. Setiap iterasi akan membuat worksheet baru karena kami akan mengonfigurasi processor untuk membuat **lembar detail** untuk setiap baris.

## Langkah 4: Bangun sumber data yang berisi beberapa baris

Kami akan menggunakan `DataTable` sebagai cara cepat untuk mensimulasikan koleksi catatan karyawan.

```csharp
// Step 4: Create a DataTable with sample employee data
DataTable employees = new DataTable("Employees");
employees.Columns.Add("Name", typeof(string));
employees.Columns.Add("Department", typeof(string));
employees.Columns.Add("Salary", typeof(decimal));

employees.Rows.Add("Alice Johnson", "Finance", 72000);
employees.Rows.Add("Bob Smith", "Engineering", 95000);
employees.Rows.Add("Carol Lee", "Marketing", 63000);
```

Anda dapat mengganti ini dengan `IEnumerable` apa pun (mis., `List<Employee>`) – Smart Markers menerima sumber data apa pun yang mengimplementasikan `IEnumerable`.

## Langkah 5: Konfigurasikan opsi Smart Marker – cara membuat beberapa lembar detail

Secara default, Smart Markers menulis data kembali ke lembar yang sama. Untuk menghasilkan **beberapa lembar detail**, Anda harus mengatur properti `DetailSheetNewName`. Ini juga menunjukkan **cara membuat beberapa lembar detail** tanpa konflik penamaan.

```csharp
// Step 5: Configure Smart Marker options
SmartMarkerOptions smOptions = new SmartMarkerOptions
{
    // Each iteration will create a new sheet named "Detail"
    DetailSheetNewName = "Detail"
};
```

Jika sumber data berisi nama duplikat, processor secara otomatis menambahkan sufiks numerik (mis., `Detail_1`, `Detail_2`). Ini mencegah kesalahan runtime dan memastikan semua lembar detail disimpan.

## Langkah 6: Proses Smart Markers

Sekarang kami memanggil processor, melewatkan sumber data dan opsi yang baru saja kami definisikan.

```csharp
// Step 6: Process Smart Markers
workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);
```

*Mengapa ini penting*: Processor membaca placeholder `&=Employees.Name`, mengiterasi setiap baris `employees`, membuat lembar baru bernama “Detail”, dan menulis data baris ke lembar tersebut. Lembar asli tetap sebagai lembar ringkasan atau master.

## Langkah 7: Simpan workbook sebagai file xlsx

Akhirnya, simpan workbook ke disk menggunakan pola **save workbook as xlsx file**.

```csharp
// Step 7: Save the resulting workbook
string outputPath = @"./output/detail.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}");
```

Enum `SaveFormat.Xlsx` menjamin bahwa file disimpan dalam format Office Open XML modern, yang kompatibel dengan Excel 2007+ dan sebagian besar layanan cloud.

## Contoh lengkap yang dapat dijalankan

Salin kode berikut ke dalam `Program.cs` dari proyek konsol .NET dan jalankan. Program akan menghasilkan `detail.xlsx` di folder `output`, berisi satu lembar master dan tiga lembar detail (satu per karyawan).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace ExcelSmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create an empty workbook
            Workbook workbook = new Workbook();

            // 2️⃣ Build a simple template with a Smart Marker
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells["A1"].PutValue("Employee Report");
            sheet.Cells["A3"].PutValue("&=Employees.Name");
            sheet.Cells["A4"].PutValue("Name");
            sheet.Cells["B4"].PutValue("Department");
            sheet.Cells["C4"].PutValue("Salary");

            // 3️⃣ Prepare the data source
            DataTable employees = new DataTable("Employees");
            employees.Columns.Add("Name", typeof(string));
            employees.Columns.Add("Department", typeof(string));
            employees.Columns.Add("Salary", typeof(decimal));

            employees.Rows.Add("Alice Johnson", "Finance", 72000);
            employees.Rows.Add("Bob Smith", "Engineering", 95000);
            employees.Rows.Add("Carol Lee", "Marketing", 63000);

            // 4️⃣ Configure Smart Marker options (how to create multiple detail sheets)
            SmartMarkerOptions smOptions = new SmartMarkerOptions
            {
                DetailSheetNewName = "Detail"
            };

            // 5️⃣ Process the markers
            workbook.Worksheets[0].SmartMarkerProcessor.Process(employees, smOptions);

            // 6️⃣ Save workbook as xlsx file
            string outPath = "./output/detail.xlsx";
            workbook.Save(outPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outPath}");
        }
    }
}
```

**Output yang diharapkan**

- `output/detail.xlsx` berisi:
  - **Sheet1** – templat asli dengan header “Employee Report”.
  - **Detail** – lembar detail pertama dengan catatan Alice.
  - **Detail_1** – lembar detail kedua dengan catatan Bob.
  - **Detail_2** – lembar detail ketiga dengan catatan Carol.

Buka file di Excel dan Anda akan melihat setiap karyawan pada lembarnya masing-masing, membuktikan bahwa kami berhasil **membuat beberapa lembar detail** dan **menyimpan workbook sebagai file xlsx**.

## Pertanyaan umum & penanganan kasus tepi

| Pertanyaan | Jawaban |
|----------|--------|
| *Bagaimana jika saya memerlukan nama khusus untuk setiap lembar detail?* | Atur `DetailSheetNewName = "Employee_"` dan sertakan kolom bernama `SheetName` dalam sumber data. Processor akan menambahkan nilai `SheetName` ke nama dasar. |
| *Apakah saya dapat mempertahankan lembar asli sebagai ringkasan semua detail?* | Ya. Lembar master tetap tidak tersentuh; Anda dapat menambahkan formula yang merujuk ke lembar detail yang dihasilkan. |
| *Apa yang terjadi ketika sumber data kosong?* | Tidak ada lembar detail yang dibuat, tetapi workbook tetap disimpan. Pertimbangkan memeriksa `employees.Rows.Count` sebelum memproses jika Anda memerlukan penanganan khusus. |
| *Apakah memungkinkan menggunakan file templat yang sudah ada?* | Ganti `new Workbook()` dengan `new Workbook("Template.xlsx")`. Semua logika Smart Marker berfungsi dengan cara yang sama. |

## Kesimpulan

Anda sekarang tahu **cara membuat workbook Excel secara programatis**, cara **membuat beberapa lembar detail** menggunakan Smart Markers, dan cara **menyimpan workbook sebagai file xlsx** dengan Aspose.Cells. Contoh lengkap dapat disesuaikan untuk faktur, laporan, atau skenario apa pun yang memerlukan output Excel master‑detail.

### Langkah selanjutnya

- Jelajahi fitur Smart Marker lainnya seperti **group markers** dan **conditional formatting**.
- Ganti `DataTable` dengan kueri basis data nyata untuk menghasilkan laporan berskala besar.
- Gunakan `Workbook.Save("output.pdf", SaveFormat.Pdf)` untuk mengekspor data yang sama ke PDF untuk distribusi.

Silakan bereksperimen dengan skema penamaan, gaya, atau lembar kerja tambahan—keterampilan generasi Excel programatis baru Anda siap untuk penggunaan produksi. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang sangat terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber daya menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Buat Workbook Excel C# – Tambahkan Komentar & Simpan sebagai XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [Buat Workbook Baru di C# – Tambahkan Rumus dan Simpan File Excel](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Buat Workbook Excel C# – Sisipkan JSON dan Simpan sebagai XLSX](/cells/english/net/excel-data-import-export/create-excel-workbook-c-insert-json-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}