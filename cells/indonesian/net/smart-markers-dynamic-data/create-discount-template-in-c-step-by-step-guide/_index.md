---
category: general
date: 2026-02-14
description: Buat templat diskon dengan cepat dan pelajari cara menerapkan diskon
  di spreadsheet, menyuntikkan data ke dalam templat, serta mendefinisikan awalan
  variabel untuk penanda pintar.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: id
og_description: Buat templat diskon dengan C#. Pelajari cara menerapkan diskon di
  spreadsheet, menyuntikkan data ke dalam templat, dan mendefinisikan awalan variabel
  untuk smart marker.
og_title: Buat Template Diskon – Panduan Lengkap C#
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: Buat Template Diskon di C# – Panduan Langkah demi Langkah
url: /id/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

0}}. The original had code block placeholders but not fenced. The instruction says preserve all code blocks: fenced code blocks. Since there are none, fine.

Make sure we didn't translate any code snippets inside backticks.

Everything else fine.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Template Diskon – Panduan Lengkap C#

Pernah membutuhkan **create discount template** untuk laporan penjualan tetapi tidak yakin bagaimana cara memasukkan angka-angka secara otomatis ke dalam spreadsheet? Anda tidak sendirian. Dalam tutorial ini kami akan menunjukkan secara tepat cara **create discount template**, kemudian **apply discount in spreadsheet** pada sel, **inject data into template**, dan bahkan **define variable prefix** untuk smart marker Anda—semua dengan kode C# yang bersih.

Kami akan mulai dengan menjelaskan masalahnya, lalu langsung melompat ke solusi yang dapat Anda salin‑tempel. Pada akhir tutorial, Anda akan memiliki pola yang dapat digunakan kembali yang berfungsi baik saat Anda membuat faktur, daftar harga, atau spreadsheet apa pun yang memerlukan diskon dinamis.

---

## Apa yang Akan Anda Pelajari

- Cara merancang template spreadsheet yang memperhatikan diskon.
- Cara mengonfigurasi `VariablePrefix` / `VariableSuffix` khusus sehingga marker mudah terlihat.
- Cara mengirim objek anonim (`discountData`) ke dalam `SmartMarkerProcessor`.
- Cara formula yang dihasilkan (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) secara otomatis menghitung harga akhir.
- Tips menangani kasus tepi seperti baris tanpa diskon atau beberapa tingkat diskon.

**Prerequisites** – runtime .NET terbaru (≥ .NET 6), referensi ke pustaka `Aspose.Cells` (atau serupa) yang menyediakan `SmartMarkerProcessor`, dan pemahaman dasar tentang sintaks C#. Tidak ada yang rumit.

---

## Langkah 1: Buat Template Diskon di Spreadsheet Anda

Pertama, buka workbook baru (atau gunakan yang sudah ada) dan tempatkan placeholder di mana diskon akan diterapkan. Anggaplah template sebagai file Excel sederhana dengan “smart markers” yang akan digantikan oleh processor.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Why this matters:** Dengan menyisipkan `#Discount#` di dalam formula, kami memberi tahu processor tepat di mana nilai diskon harus ditempatkan. `SmartMarkerProcessor` akan menggantikan `#Discount#` dengan angka yang Anda berikan nanti, meninggalkan sisanya dari formula tidak berubah.

---

## Langkah 2: Tentukan Variable Prefix untuk Smart Markers

Secara default, banyak pustaka mencari `${Variable}` atau `{{Variable}}`. Dalam kasus kami, kami menginginkan marker yang bersih dan mudah dibaca manusia, jadi kami **define variable prefix** dan suffix secara eksplisit.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro tip:** Menggunakan `#` membuat marker pendek dan mudah terlihat di bar formula Excel. Jika Anda perlu menghindari benturan dengan fungsi Excel yang ada, pilih pasangan lain (misalnya, `[[` dan `]]`).

---

## Langkah 3: Inject Data ke Template Menggunakan SmartMarkerProcessor

Sekarang kami memasukkan nilai diskon yang sebenarnya. Processor akan memindai worksheet, menemukan setiap `#Discount#`, dan menggantinya dengan nilai dari objek anonim yang kami berikan.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Setelah pemanggilan ini, formula di `B2` menjadi:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Saat workbook menghitung, `B2` menampilkan **90**, yaitu diskon 10 % yang diterapkan pada harga asli 100.

**Why it works:** `StartSmartMarkerProcessing` memeriksa setiap sel, mencari token `#Discount#`, dan menggantinya dengan nilai numerik. Karena token berada di dalam pernyataan `IF`, spreadsheet tetap menangani kasus di mana diskon mungkin nol.

---

## Langkah 4: Apply Discount in Spreadsheet – Verifikasi Hasil

Mari jalankan perhitungan dan keluarkan harga akhir ke konsol. Langkah ini membuktikan bahwa alur kerja **apply discount in spreadsheet** berhasil.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Expected output**

```
Original: 100
Discounted (10%): 90
```

Jika Anda mengubah `discountData.Discount` menjadi `0.25` dan menjalankan kembali processor, output akan otomatis mencerminkan diskon 25 %—tanpa kode tambahan.

---

## Langkah 5: Menangani Edge Cases & Multiple Discounts

### Baris Tanpa Diskon

Kadang sebuah produk tidak sedang diskon. Untuk menjaga formula tetap kuat, `IF` yang Anda tempatkan sebelumnya sudah mencakup skenario ini: ketika `#Discount#` adalah `0`, harga asli tetap diteruskan tanpa perubahan.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Kolom Diskon Ganda

Jika Anda memerlukan diskon terpisah per baris, beri setiap baris markernya masing‑masing, misalnya `#Discount1#`, `#Discount2#`, dan kirimkan sebuah koleksi:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

Processor mencocokkan marker secara berurutan, sehingga setiap baris mendapatkan nilai yang tepat.

---

## Contoh Lengkap yang Berfungsi

Berikut adalah program lengkap yang siap disalin yang menggabungkan semua langkah di atas. Simpan sebagai `Program.cs`, tambahkan referensi ke `Aspose.Cells`, dan jalankan.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Menjalankan program ini akan mencetak angka yang diharapkan dan menghasilkan file `DiscountedPricing.xlsx` yang dapat Anda buka di Excel untuk melihat formula yang sudah terhitung.

---

## Kesimpulan

Anda kini tahu cara **create discount template**, **apply discount in spreadsheet**, **inject data into template**, dan **define variable prefix** untuk smart marker—semua dengan beberapa baris C# yang singkat. Pola ini dapat diskalakan—cukup ubah objek anonim atau berikan koleksi untuk pembaruan massal, dan template yang sama akan menangani semua skenario diskon yang Anda berikan.

Siap ke level berikutnya? Coba:

- Menambahkan perhitungan pajak bersama diskon.
- Mengambil persentase diskon dari basis data alih-alih menuliskannya secara hard‑code.
- Menggunakan pemformatan bersyarat untuk menyoroti baris dengan diskon tinggi.

Ekstensi tersebut mempertahankan gagasan inti sambil memperluas kegunaan template diskon Anda.

Ada pertanyaan atau contoh penggunaan yang menarik? Tinggalkan komentar di bawah, dan selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}