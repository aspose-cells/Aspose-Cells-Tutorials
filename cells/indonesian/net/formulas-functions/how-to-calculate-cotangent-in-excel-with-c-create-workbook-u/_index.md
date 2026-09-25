---
category: general
date: 2026-05-04
description: Cara menghitung kotangen saat membuat workbook Excel di C#. Pelajari
  cara menggunakan fungsi EXPAND, menyimpan workbook, dan mengotomatisasi perhitungan.
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: id
og_description: Cara menghitung kotangen di Excel menggunakan C#. Tutorial ini menunjukkan
  cara membuat buku kerja Excel, menggunakan EXPAND, dan menyimpan file.
og_title: Cara Menghitung Kotangen di Excel – Panduan Lengkap Buku Kerja C#
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Cara Menghitung Kotangen di Excel dengan C# – Buat Workbook, Gunakan EXPAND,
  dan Simpan
url: /id/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menghitung Cotangent di Excel dengan C# – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara menghitung cotangent** langsung di dalam file Excel yang dihasilkan oleh C#? Mungkin Anda sedang membangun model keuangan, laporan ilmiah, atau sekadar mengotomatisasi tugas spreadsheet yang membosankan. Kabar baiknya? Anda dapat melakukannya dalam beberapa baris kode—tanpa rumus manual, tanpa akrobatik copy‑paste.

Dalam tutorial ini kami akan memandu Anda membuat workbook Excel, memperluas array dengan fungsi **EXPAND**, menyisipkan rumus **COT** untuk menghitung cotangent 45°, dan akhirnya menyimpan file sehingga Anda dapat membukanya di Excel dan melihat hasilnya. Sepanjang jalan kami juga akan membahas **cara menggunakan expand**, **cara menyimpan workbook**, serta beberapa tip berguna yang sering terlewat.

> **Jawaban singkat:** Gunakan Aspose.Cells (atau Microsoft Interop) untuk membuat workbook, set `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"`, set `ws.Cells["B1"].Formula = "=COT(PI()/4)"`, lalu panggil `workbook.Save("output.xlsx")`.

---

## Apa yang Anda Butuhkan

- **.NET 6+** (atau runtime .NET terbaru apa pun).  
- **Aspose.Cells for .NET** (versi trial gratis atau berlisensi).  
- Pemahaman dasar tentang sintaks C#.  
- Visual Studio, Rider, atau editor apa pun yang Anda suka.

Tidak ada add‑in Excel tambahan yang diperlukan; semuanya berjalan di sisi server dan file yang dihasilkan dapat dibuka di versi Excel terbaru mana pun.

---

## Langkah 1: Buat Excel Workbook dari C#

Membuat workbook adalah fondasi. Anggap saja seperti membuka buku catatan baru sebelum Anda mulai menulis.

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**Mengapa ini penting:**  
`Workbook` mewakili seluruh paket `.xlsx`. Secara default ia berisi satu lembar, yang dapat diakses melalui `Worksheets[0]`. Jika Anda membutuhkan lebih banyak lembar nanti, Anda dapat menambahkannya dengan `workbook.Worksheets.Add()`.

> **Pro tip:** Jika Anda menargetkan .NET Core, pastikan paket NuGet Aspose.Cells cocok dengan runtime Anda agar tidak kehilangan dependensi native.

---

## Langkah 2: Gunakan Fungsi EXPAND untuk Mengisi Kolom

Fungsi **EXPAND** adalah cara Excel mengubah array statis menjadi rentang dinamis. Ini sempurna ketika Anda ingin menghasilkan kolom nilai tanpa menuliskan setiap sel secara manual.

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### Cara Kerjanya

- `{1,2,3}` adalah array sumber (tiga angka).  
- `5` memberi tahu Excel untuk menghasilkan **5 baris**.  
- `1` memberi tahu Excel untuk menghasilkan **1 kolom**.  

Saat Anda membuka file yang disimpan, sel A1 hingga A5 akan berisi `1, 2, 3, 0, 0` (baris tambahan diisi dengan nol).

**Kasus tepi:** Jika argumen `rows` lebih kecil daripada panjang array sumber, Excel memotong array. Jadi `=EXPAND({1,2,3},2,1)` hanya akan menampilkan `1` dan `2`.

---

## Langkah 3: Sisipkan Rumus COT untuk Menghitung Cotangent

Sekarang saatnya bintang utama: **cara menghitung cotangent** di Excel. Fungsi `COT` mengharapkan sudut dalam radian, jadi kami memberinya `PI()/4` (yang sama dengan 45°).

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### Mengapa Menggunakan COT Daripada Tan?

Cotangent adalah kebalikan dari tangent (`cot = 1 / tan`). Meskipun Anda bisa menulis `=1/TAN(PI()/4)`, menggunakan `COT` lebih bersih dan menghindari kesalahan pembagian‑nol ketika sudutnya 0° atau 180°.

**Output yang diharapkan:** Membuka `output.xlsx` akan menampilkan `1` di B1, karena cotangent 45° (π/4 radian) sama dengan 1.

**Bagaimana jika saya butuh derajat?**  
Fungsi trigonometri Excel bekerja dalam radian. Konversi derajat dengan `RADIANS(deg)`. Contoh: `=COT(RADIANS(60))`.

---

## Langkah 4: Simpan Workbook agar Anda Dapat Melihat Hasilnya

Menyimpan adalah langkah terakhir dari puzzle. Anda dapat menulis ke folder mana pun yang memiliki izin menulis.

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Cara Menyimpan dalam Berbagai Format

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

Jika Anda perlu men-stream file (misalnya untuk API web), gunakan `workbook.Save(stream, SaveFormat.Xlsx)` sebagai gantinya.

---

## Contoh Lengkap yang Berfungsi

Menggabungkan semuanya, berikut program mandiri yang dapat Anda salin‑tempel ke aplikasi console.

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**Verifikasi hasil:**  
- Buka `output.xlsx`.  
- Kolom A harus berisi `1, 2, 3, 0, 0`.  
- Sel B1 harus menampilkan `1`.  

Jika nilai‑nilai tersebut muncul, Anda telah berhasil mempelajari **cara menghitung cotangent** secara programatik serta **cara membuat excel workbook**, **menggunakan fungsi expand**, dan **menyimpan workbook**—semuanya dalam satu langkah.

---

## Pertanyaan Umum & Hal-hal yang Perlu Diwaspadai

### Apakah `COT` bekerja di versi Excel lama?

Ya, `COT` sudah ada sejak Excel 2007. Jika Anda menargetkan Excel 2003 (`.xls`), Anda harus menggantinya dengan `1/TAN(...)` karena `COT` tidak tersedia di sana.

### Bagaimana jika rumus tidak menghitung otomatis?

Aspose.Cells mengevaluasi rumus secara malas. Panggil `workbook.CalculateFormula()` sebelum menyimpan jika Anda memerlukan nilai yang sudah dihitung di dalam file.

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### Bisakah saya menulis hasil langsung tanpa rumus?

Tentu, Anda dapat menghitung nilai di C# (`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`) dan menetapkannya ke `ws.Cells["B1"].Value = result;`. Tutorial ini fokus pada rumus Excel karena tetap dinamis—mengubah sudut nanti akan memperbarui nilai secara otomatis.

---

## Pro Tips untuk Proyek Dunia Nyata

- **Operasi batch:** Jika Anda mengisi ribuan baris, nonaktifkan perhitungan (`workbook.Settings.CalculateFormulaOnOpen = false`) selama penulisan, lalu aktifkan kembali setelah selesai.  
- **Menamai rentang:** Gunakan `ws.Cells.CreateRange("MyArray", "A1:A5")` dan referensikan nama tersebut dalam rumus untuk spreadsheet yang lebih jelas.  
- **Penanganan error:** Bungkus `workbook.Save` dalam try/catch untuk menampilkan masalah izin (`UnauthorizedAccessException`).

---

## Kesimpulan

Kami telah membahas **cara menghitung cotangent** dalam lembar Excel yang dihasilkan oleh C#, mendemonstrasikan **cara menggunakan expand** untuk mengisi kolom, dan menunjukkan **cara menyimpan workbook** untuk inspeksi langsung. Contoh lengkap yang dapat dijalankan di atas memberi Anda fondasi kuat untuk mengotomatisasi spreadsheet apa pun yang menggabungkan data statis dengan perhitungan trigonometri.

Langkah selanjutnya? Coba ganti sudut dalam rumus `COT` dengan referensi sel (`=COT(PI()*A1/180)`) agar pengguna dapat memasukkan derajat. Atau jelajahi fungsi matematika lain seperti `SIN`, `COS`, dan `ATAN2`—semuanya berfungsi dengan cara yang sama di dalam workbook yang dihasilkan.

Selamat coding, semoga spreadsheet Anda selalu bebas error! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}