---
category: general
date: 2026-07-03
description: Buat workbook Excel dalam C# dan atur formula sel, hitung formula pi,
  lalu ekspor Excel dengan formula. Ikuti tutorial singkat dan praktis ini.
draft: false
keywords:
- create excel workbook
- set cell formula
- calculate pi formula
- how to set formula
- export excel with formulas
language: id
og_description: Buat workbook Excel di C# dan atur formula sel, hitung formula pi,
  lalu ekspor Excel dengan formula. Pelajari seluruh proses dalam hitungan menit.
og_title: Buat Buku Kerja Excel dengan Rumus – Panduan Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Create Excel workbook in C# and set cell formula, calculate pi formula,
    then export Excel with formulas. Follow this quick, practical tutorial.
  headline: Create Excel Workbook with Formulas – Full Step‑by‑Step Guide
  type: TechArticle
- description: Create Excel workbook in C# and set cell formula, calculate pi formula,
    then export Excel with formulas. Follow this quick, practical tutorial.
  name: Create Excel Workbook with Formulas – Full Step‑by‑Step Guide
  steps:
  - name: Does the workbook keep the formulas after saving?
    text: Yes. Aspose.Cells writes both the formula string (`Formula`) and the evaluated
      value (`Value`). When you open the file, Excel will re‑evaluate the formulas
      on load, but the saved formula remains intact—perfect for later edits.
  - name: What if I need to set a formula that references another sheet?
    text: Just use the typical Excel notation, e.g., `=Sheet2!C3*2`. Aspose.Cells
      parses it correctly as long as the target sheet exists.
  - name: How to handle large data sets without blowing memory?
    text: Use `WorkbookDesigner` or stream the workbook directly to a `MemoryStream`
      and then to a response object. This avoids loading the entire file into RAM
      when you only need to push it to a client.
  - name: Can I protect the sheet while still allowing formula evaluation?
    text: 'Absolutely. After setting formulas, call:'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Buat Buku Kerja Excel dengan Rumus – Panduan Langkah demi Langkah Lengkap
url: /id/net/excel-formulas-and-calculation-options/create-excel-workbook-with-formulas-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Membuat Workbook Excel dengan Formula – Panduan Lengkap

Pernah bertanya-tanya bagaimana **membuat workbook excel** secara programatis dan menjaga formula tetap aktif saat Anda membuka file? Anda tidak sendirian. Baik Anda membangun mesin pelaporan, generator faktur, atau sekadar mengotomatiskan dump harian, kemampuan untuk mengatur formula sel, menghitung formula pi, dan kemudian **mengekspor excel dengan formula** menghemat berjam‑jam penyesuaian manual.

Dalam tutorial ini kami akan memandu Anda melalui contoh praktis menggunakan pustaka Aspose.Cells untuk .NET. Kami akan mulai dengan membuat workbook, kemudian menunjukkan **cara mengatur formula** untuk array dinamis, menghitung nilai trigonometri dengan π, menghitung ulang sheet, dan akhirnya menyimpan file sehingga Excel menampilkan hasil secara langsung.

## Apa yang Anda Butuhkan

- .NET 6 (atau runtime .NET terbaru) – kode juga dapat dikompilasi dengan .NET Core.  
- Aspose.Cells untuk .NET – paket NuGet kuat tanpa lisensi untuk demo kami (`Install-Package Aspose.Cells`).  
- IDE pilihan Anda (Visual Studio, Rider, VS Code – pilih yang paling nyaman).  

Tidak ada dependensi lain. Jika Anda belum pernah menyentuh Aspose.Cells sebelumnya, jangan khawatir; API‑nya sederhana dan cuplikan di bawah siap untuk disalin‑tempel.

## Membuat Workbook Excel – Penyiapan Awal

Langkah pertama. Kita memerlukan objek workbook baru yang akan menampung worksheet‑nya. Anggap saja sebagai file Excel kosong yang menunggu konten.

```csharp
using Aspose.Cells;

 // Step 1: Create a workbook and obtain the first worksheet
Workbook workbook = new Workbook();               // <-- creates a new .xlsx in memory
Worksheet ws = workbook.Worksheets[0];           // the default first sheet
```

*Mengapa ini penting:* Kelas `Workbook` adalah titik masuk untuk setiap operasi—tanpa itu Anda tidak dapat menambahkan sheet, mengatur formula, atau mengekspor apa pun. Dengan mengambil `Worksheets[0]` kita mendapatkan referensi ke tab default bernama “Sheet1”.

> **Pro tip:** Jika Anda membutuhkan beberapa sheet, cukup panggil `workbook.Worksheets.Add()` dan simpan referensi `Worksheet` yang dikembalikan.

## Mengatur Formula Sel – Ekspansi Array Dinamis

Sekarang mari **mengatur formula sel** yang memperluas rentang secara dinamis. Fungsi `EXPAND` adalah fitur baru Excel 365 yang menumpahkan array sumber ke ukuran yang ditentukan.

```csharp
// Step 2: Apply a dynamic array formula that expands A2:A5 to 4 rows, 1 column
ws.Cells["A1"].Formula = "=EXPAND(A2:A5,4,1)";
```

Apa yang terjadi di balik layar?  

- `A2:A5` adalah rentang sumber (empat sel).  
- Argumen kedua (`4`) memberi tahu Excel untuk membuat **4 baris**.  
- Argumen ketiga (`1`) memaksa **1 kolom**.  

Saat Anda membuka file yang disimpan, sel A1:A4 akan otomatis berisi nilai dari A2:A5. Jika Anda kemudian mengubah salah satu sel sumber, spill akan terupdate secara instan—tanpa makro.

> **Kasus tepi:** `EXPAND` hanya berfungsi pada versi Excel yang mendukung array dinamis (Office 365, Excel 2021+). Versi lama akan menampilkan error `#NAME?`.

## Menghitung Formula Pi – Contoh Trigonometri

Selanjutnya kami akan mendemonstrasikan **menghitung formula pi** dengan menggunakan fungsi bawaan `PI()` bersama `COT`. Ini memperlihatkan bagaimana ekspresi yang kompatibel dengan Excel dapat disuntikkan dari kode.

```csharp
// Step 3: Apply a trigonometric formula to compute the cotangent of π/4
ws.Cells["B1"].Formula = "=COT(PI()/4)";
```

Mengapa `COT(PI()/4)`? Cotangen dari 45° (π/4 radian) bernilai 1, sehingga sel harus menampilkan **1** setelah perhitungan. Ini merupakan pemeriksaan sanity yang bagus—jika Anda melihat nilai lain, kemungkinan langkah recalculation tidak dijalankan.

## Menghitung Ulang Worksheet – Memastikan Formula Terhitung

Aspose.Cells tidak secara otomatis mengevaluasi formula ketika Anda mengaturnya. Anda harus secara eksplisit memicu proses perhitungan.

```csharp
// Step 4: Recalculate the worksheet so the formulas are evaluated
ws.CalculateFormula();
```

Memanggil `CalculateFormula()` akan menelusuri setiap sel yang berisi formula, menghitung hasilnya, dan menyimpannya di properti `Value` sel tersebut. Langkah ini menjamin workbook yang Anda simpan sudah berisi angka yang dihitung, yang berguna ketika Anda membuka file di lingkungan tanpa UI (misalnya layanan pelaporan).

## Mengekspor Excel dengan Formula – Menyimpan File

Akhirnya, kami **mengekspor excel dengan formula** ke file fisik. Formatnya standar `.xlsx`, sepenuhnya kompatibel dengan program spreadsheet modern mana pun.

```csharp
// Step 5: Save the workbook to view the results
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
workbook.Save(outputPath);
```

Buka `output.xlsx` di Excel dan Anda akan melihat:

| A | B |
|---|---|
| (nilai dari A2) | 1 |
| (nilai dari A3) |   |
| (nilai dari A4) |   |
| (nilai dari A5) |   |

Sel **B1** menampilkan **1**, mengonfirmasi perhitungan `COT(PI()/4)` kami. Sel **A1:A4** menampilkan nilai yang tumpah dari **A2:A5** berkat formula `EXPAND`.

> **Verifikasi cepat:** Ubah nilai di `A2` menjadi `99`, jalankan kembali program, dan buka file lagi. Spill di kolom A seharusnya kini menampilkan `99` di bagian atas rentang.

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

### Apakah workbook tetap menyimpan formula setelah disimpan?

Ya. Aspose.Cells menulis baik string formula (`Formula`) maupun nilai yang sudah dihitung (`Value`). Saat Anda membuka file, Excel akan mengevaluasi ulang formula pada saat load, tetapi formula yang disimpan tetap utuh—sempurna untuk penyuntingan selanjutnya.

### Bagaimana jika saya perlu mengatur formula yang merujuk ke sheet lain?

Gunakan notasi Excel biasa, misalnya `=Sheet2!C3*2`. Aspose.Cells akan mem‑parsenya dengan benar selama sheet target memang ada.

### Bagaimana menangani kumpulan data besar tanpa menghabiskan memori?

Gunakan `WorkbookDesigner` atau alirkan workbook langsung ke `MemoryStream` lalu ke objek respons. Ini menghindari memuat seluruh file ke RAM ketika Anda hanya perlu mengirimnya ke klien.

### Bisakah saya melindungi sheet sambil tetap memperbolehkan evaluasi formula?

Tentu saja. Setelah mengatur formula, panggil:

```csharp
ws.Protect(ProtectionType.All);
```

Flag perlindungan tidak menghentikan perhitungan; ia hanya membatasi edit oleh pengguna.

## Contoh Lengkap yang Siap Dijalan

Berikut adalah program lengkap yang siap dijalankan. Tempelkan ke proyek konsol baru, tambahkan paket NuGet Aspose.Cells, dan tekan **F5**.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelFormulaDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create a new workbook and grab the first worksheet
            Workbook workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];

            // Populate source cells A2:A5 so the EXPAND formula has something to spill
            ws.Cells["A2"].PutValue(10);
            ws.Cells["A3"].PutValue(20);
            ws.Cells["A4"].PutValue(30);
            ws.Cells["A5"].PutValue(40);

            // 2️⃣ Set a dynamic array formula in A1
            ws.Cells["A1"].Formula = "=EXPAND(A2:A5,4,1)";

            // 3️⃣ Compute cotangent of π/4 in B1
            ws.Cells["B1"].Formula = "=COT(PI()/4)";

            // 4️⃣ Force calculation so values are stored
            ws.CalculateFormula();

            // 5️⃣ Save the workbook – this exports the Excel with formulas intact
            string outputPath = Path.Combine(Environment.CurrentDirectory, "output.xlsx");
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to: {outputPath}");
        }
    }
}
```

**Output yang diharapkan** (ketika Anda membuka `output.xlsx`):

- **A1:A4** berisi `10, 20, 30, 40` masing‑masing (spill dari A2:A5).  
- **B1** menampilkan `1` (hasil `COT(PI()/4)`).  

Semua sel lain tetap kosong, persis seperti yang kami programkan.

## Kesimpulan

Kami baru saja **membuat workbook excel**, **mengatur formula sel** untuk array dinamis, **menghitung formula pi** dengan fungsi trigonometri, memaksa perhitungan ulang, dan akhirnya **mengekspor excel dengan formula** ke disk. Seluruh alur ini dapat diselesaikan dalam beberapa baris kode, namun memperlihatkan kemampuan inti yang Anda perlukan untuk otomatisasi dunia nyata.

Apa selanjutnya? Coba ganti `EXPAND` dengan `FILTER`, sematkan gambar melalui objek `Picture`, atau hasilkan chart secara dinamis. API Aspose.Cells mencakup segala hal mulai dari penulisan sel sederhana hingga pivot table kompleks, jadi langit adalah batasnya.

Jangan ragu bereksperimen, memecahkan sesuatu, dan kembali dengan modifikasi Anda sendiri. Jika menemukan kendala, tinggalkan komentar di bawah—selamat coding! 

![Contoh pembuatan workbook Excel](excel-workbook-example.png "Contoh pembuatan workbook Excel yang menampilkan formula di A1 dan B1")


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Otomatisasi Excel dengan Aspose.Cells .NET&#58; Menguasai Workbook & Perhitungan Formula](/cells/english/net/formulas-functions/excel-automation-aspose-cells-net-workbook-formulas/)
- [Otomatisasi Excel dengan Aspose.Cells .NET&#58; Membuat Workbook & Menetapkan Tautan Eksternal](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Cara Membuat dan Menyimpan Workbook Excel sebagai ODS Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}