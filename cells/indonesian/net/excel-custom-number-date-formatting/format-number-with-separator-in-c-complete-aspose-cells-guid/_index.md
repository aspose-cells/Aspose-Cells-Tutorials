---
category: general
date: 2026-03-30
description: Pelajari cara memformat angka dengan pemisah menggunakan Aspose.Cells
  di C#. Termasuk mengatur format angka khusus, menambahkan pemisah ribuan, memformat
  tempat desimal, dan cara memformat sel.
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: id
og_description: Format angka dengan pemisah di C#. Panduan ini menunjukkan cara mengatur
  format angka khusus, menambahkan pemisah ribuan, memformat tempat desimal, dan cara
  memformat sel menggunakan Aspose.Cells.
og_title: Format Angka dengan Pemisah di C# – Tutorial Aspose.Cells
tags:
- C#
- Aspose.Cells
- Number Formatting
title: Format Angka dengan Pemisah di C# – Panduan Lengkap Aspose.Cells
url: /id/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memformat Angka dengan Pemisah di C# – Panduan Lengkap Aspose.Cells

Pernah perlu **memformat angka dengan pemisah** di spreadsheet tetapi tidak yakin panggilan API mana yang harus digunakan? Anda tidak sendirian—para pengembang terus bergulat dengan pemisah ribuan, tempat desimal, dan pola kustom saat mengekspor data.  

Kabar baik: Aspose.Cells membuatnya sangat mudah. Dalam tutorial ini kami akan menelusuri contoh dunia nyata yang **menetapkan format angka kustom**, **menambahkan pemisah ribuan**, **memformat tempat desimal**, dan menunjukkan **cara memformat sel** output sebagai string. Pada akhir tutorial Anda akan memiliki potongan kode siap‑jalankan yang dapat disisipkan ke proyek .NET mana pun.

## Apa yang Dibahas dalam Panduan Ini

* Paket NuGet yang tepat dan cara menginstalnya.  
* Kode langkah‑demi‑langkah yang membuat workbook, menulis nilai numerik, dan menerapkan format kustom.  
* Mengapa `ExportTableOptions.ExportAsString` adalah cara yang disarankan untuk mengambil nilai yang telah diformat.  
* Kesalahan umum—seperti lupa mengaktifkan `ExportAsString` atau menggunakan mask format yang salah.  
* Cara menyesuaikan mask format jika Anda memerlukan jumlah tempat desimal yang berbeda atau gaya pemisah yang lain.

Tidak ada tautan dokumentasi eksternal yang diperlukan; semua yang Anda butuhkan ada di sini. Mari kita mulai.

---

## Prasyarat

| Persyaratan | Alasan |
|-------------|--------|
| .NET 6.0 atau yang lebih baru | Aspose.Cells 23.10+ menargetkan .NET Standard 2.0+, jadi .NET 6 aman dan terkini. |
| Visual Studio 2022 (atau IDE C# apa pun) | Membuat debugging dan manajemen paket menjadi mudah. |
| Paket NuGet Aspose.Cells untuk .NET | Menyediakan kelas `Workbook`, `Worksheet`, dan `ExportTableOptions` yang akan kita gunakan. |

Anda dapat menginstal paket tersebut melalui Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

Itu saja—tidak ada DLL tambahan, tidak ada interop COM, hanya satu referensi NuGet.

---

## Langkah 1: Inisialisasi Workbook Baru (Cara Memformat Sel)

Hal pertama yang kami lakukan adalah membuat instance `Workbook` yang baru. Anggap saja ini sebagai file Excel kosong yang siap menerima data.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Mengapa ini penting:** `Workbook` adalah titik masuk untuk setiap operasi di Aspose.Cells. Dengan mengambil worksheet pertama (`Worksheets[0]`) kita mendapatkan kanvas bersih tanpa harus memberi nama sheet.

---

## Langkah 2: Tulis Nilai Numerik ke Sel Target

Selanjutnya, kami menaruh angka mentah ke sel **A1**. Nilainya belum diformat—hanya berupa double.

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **Tips profesional:** Gunakan `PutValue` alih‑alih `PutString` ketika Anda berencana menerapkan pemformatan numerik nanti. Ini mempertahankan tipe data dasar, memungkinkan perhitungan yang kompatibel dengan Excel.

---

## Langkah 3: Tetapkan Format Angka Kustom (Tambahkan Pemisah Ribuan & Format Tempat Desimal)

Sekarang masuk ke inti tutorial: mendefinisikan mask format yang memberi tahu Aspose.Cells cara menampilkan angka. Mask `#,##0.00` melakukan tiga hal:

1. **`#,##0`** – menambahkan pemisah ribuan (koma secara default).  
2. **`.00`** – memaksa tepat dua tempat desimal.  

Jika Anda memerlukan jumlah desimal yang berbeda, cukup ubah jumlah `0` setelah titik desimal.

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **Mengapa kami menggunakan `ExportAsString`**: Secara default, `ExportString` mengembalikan nilai mentah. Menetapkan `ExportAsString = true` memaksa API menerapkan mask `NumberFormat` sebelum mengonversi ke teks. Ini penting ketika Anda memerlukan representasi string yang tepat untuk laporan, payload JSON, atau tampilan UI.

---

## Langkah 4: Ekspor Teks yang Diformat (Cara Memformat Sel)

Dengan opsi yang sudah siap, kami memanggil `ExportString` pada sel yang sama. Metode ini menghormati mask yang baru saja kami definisikan dan mengembalikan string yang sudah diformat dengan rapi.

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

Menjalankan program mencetak **`12,345.68`** ke konsol—tepat seperti format yang kami minta.

> **Kasus tepi:** Jika angka sumber memiliki lebih dari dua tempat desimal, mask akan membulatkannya. Jika Anda memerlukan pemotongan alih‑alih pembulatan, Anda harus memproses nilai terlebih dahulu dengan `Math.Truncate` sebelum memanggil `PutValue`.

---

## Langkah 5: Menyesuaikan Format – Variasi Umum

### 5.1 Ubah Presisi Desimal

Ingin tiga tempat desimal? Ganti saja masknya:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 Gunakan Pemisah Ribuan yang Berbeda

Beberapa locale lebih suka spasi atau titik. Anda dapat menyisipkan karakter tersebut langsung:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

Atau mengandalkan pengaturan budaya workbook:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 Awalan atau Akhiran (Mata Uang, Persen)

Tambahkan tanda dolar atau persen langsung di dalam mask:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **Catatan:** Mask bersifat case‑sensitive. `$` dan `%` adalah simbol literal; mereka tidak memengaruhi nilai numerik dasar.

---

## Langkah 6: Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut adalah program lengkap yang dapat Anda salin ke aplikasi console baru. Program ini mencakup semua langkah, komentar, dan verifikasi output akhir.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

Jalankan program (`dotnet run` dari terminal atau tekan F5 di Visual Studio) dan Anda akan melihat angka yang diformat tercetak persis seperti yang ditunjukkan.

---

## Pertanyaan yang Sering Diajukan (FAQ)

**T: Apakah ini bekerja dengan versi Excel yang lebih lama?**  
J: Ya. Mask format mengikuti sintaks format angka native Excel, jadi versi apa pun yang memahami `#,##0.00` akan menampilkan string yang sama.

**T: Bagaimana jika saya perlu memformat rentang sel?**  
J: Lakukan iterasi pada rentang yang diinginkan dan terapkan `ExportTableOptions` yang sama pada setiap sel, atau set properti `Style.Custom` pada rentang tersebut dan kemudian panggil `ExportString` pada satu sel.

**T: Bisakah saya mengekspor langsung ke CSV dengan format ini diterapkan?**  
J: Tentu. Gunakan `Workbook.Save("output.csv", SaveFormat.CSV);` setelah mengatur format pada setiap sel. Aspose.Cells menghormati `Style` sel saat menghasilkan CSV.

---

## Kesimpulan

Kami baru saja menunjukkan cara **memformat angka dengan pemisah** di C# menggunakan Aspose.Cells, mencakup semuanya mulai dari **menetapkan format angka kustom** hingga **menambahkan pemisah ribuan**, **memformat tempat desimal**, dan cara **memformat sel** untuk ekspor string. Kode ini sepenuhnya mandiri, bekerja dengan .NET 6+, dan dapat disesuaikan untuk locale atau kebutuhan presisi apa pun.

Selanjutnya, Anda dapat menjelajahi:

* Menerapkan teknik yang sama pada tanggal dan waktu (`NumberFormat = "dd‑MMM‑yyyy"`).  
* Mengotomatiskan ekspor massal di mana setiap kolom memerlukan mask yang berbeda.  
* Mengintegrasikan string yang diformat ke dalam laporan PDF dengan Aspose.Words.

Cobalah, dan Anda akan cepat menjadi orang yang diandalkan untuk pemformatan spreadsheet di tim Anda. Selamat coding!   ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="Nomor yang diformat dengan pemisah ditampilkan di output Aspose.Cells"} 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}