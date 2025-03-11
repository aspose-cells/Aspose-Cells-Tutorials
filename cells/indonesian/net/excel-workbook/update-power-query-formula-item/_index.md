---
title: Memperbarui Item Rumus Power Query
linktitle: Memperbarui Item Rumus Power Query
second_title: Referensi API Aspose.Cells untuk .NET
description: Memperbarui item rumus Power Query di Excel dengan mudah menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah untuk menyederhanakan proses manipulasi data Anda.
weight: 160
url: /id/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memperbarui Item Rumus Power Query

## Perkenalan

Jika Anda pernah bekerja dengan Excel, Anda tahu betapa hebatnya Excel—terutama saat Anda mulai mendalami Power Query. Ini adalah rahasia yang memungkinkan Anda mengubah, membersihkan, dan menganalisis data dengan mudah. Salah satu cara praktis untuk memanipulasi rumus Power Query di Excel adalah melalui Aspose.Cells for .NET. Hari ini, kami akan memandu Anda memperbarui item rumus Power Query langkah demi langkah. Jadi, ambil topi koding Anda, dan mari kita mulai!

## Prasyarat

Sebelum Anda masuk ke kode, ada beberapa hal yang perlu Anda siapkan:

1. Visual Studio: Anda memerlukan lingkungan pengembangan terpadu (IDE) untuk menulis dan menjalankan kode .NET. Visual Studio adalah pilihan terbaik.
2.  Pustaka Aspose.Cells: Pastikan Anda memiliki pustaka Aspose.Cells yang tersedia dalam proyek Anda. Anda dapat mengunduhnya dari[lokasi](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Saat kita membahas ini bersama-sama, memiliki pemahaman mendasar tentang C# tentu akan membantu, terutama saat menjelajahi berbagai kelas dan metode.
4. Contoh File Excel: Anda akan memerlukan file Excel yang disebutkan dalam cuplikan kode. Pastikan Anda memiliki:
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: Pastikan proyek Anda menargetkan versi .NET Framework yang kompatibel.

Sekarang perlengkapan kita sudah siap, kita dapat lanjut ke bagian yang menyenangkan: menulis kode!

## Paket Impor

Pertama-tama, Anda perlu mengimpor namespace yang diperlukan. Berikut cara melakukannya:

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

Dengan menambahkan namespace ini, Anda memberi tahu kompiler bahwa Anda bermaksud menggunakan kelas dan metode dari pustaka Aspose.Cells. Langkah ini penting karena meletakkan dasar bagi kode yang mengikutinya.

Mari kita bahas cuplikan kode yang Anda berikan. Tutorial ini akan memandu Anda melalui setiap bagian, memastikan Anda memahami apa yang sedang terjadi.

## Langkah 1: Siapkan Direktori Kerja

Pada langkah ini, kita akan menentukan di mana file sumber dan output kita berada. Ini memastikan bahwa Aspose tahu di mana mencari file Excel Anda.

```csharp
// Direktori kerja
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## Langkah 2: Muat Buku Kerja

Sekarang, mari muat berkas Excel tempat Power Query berada.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Itu`Workbook` class adalah titik masuk Anda ke berkas Excel. Dengan meneruskan jalur berkas sumber, kita menciptakan contoh yang memungkinkan kita untuk memanipulasinya. Anda dapat membayangkannya seperti membuka buku—Anda bersiap untuk membaca (atau mengedit) isinya.

## Langkah 3: Akses Data Mashup

Berikutnya, kita akan mengakses rumus Power Query yang disimpan dalam Data Mashup buku kerja.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Itu`DataMashup` kelas berisi semua rumus Power Query yang terkait dengan buku kerja Anda. Di sinilah kita akan melakukan pekerjaan berat, seperti saat Anda membuka kotak peralatan untuk perbaikan.

## Langkah 4: Ulangi Rumus Power Query

Sekarang tibalah saatnya kita mengulangi rumus Power Query untuk menemukan rumus spesifik yang ingin kita perbarui.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

-  Kami mengulang setiap`PowerQueryFormula` di dalam`mashupData`.
- Dalam lingkaran itu, kita menyelami masing-masing`PowerQueryFormulaItem`.
- Kami memeriksa apakah nama item tersebut cocok dengan "Sumber". Jika cocok, kami memperbarui nilainya untuk menautkan ke berkas sumber baru kami.

Ini mirip dengan menemukan halaman yang tepat dalam sebuah manual dan kemudian membuat pembaruan yang diperlukan—ini adalah proses yang mudah dan teliti.

## Langkah 5: Simpan Buku Kerja yang Diperbarui

Setelah melakukan pembaruan, waktunya menyimpan perubahan.

```csharp
// Simpan buku kerja keluaran.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 Itu`Save` metode menulis buku kerja yang diperbarui ke direktori keluaran yang ditentukan. Ini seperti menyegel suntingan Anda dalam versi baru manual, siap digunakan orang lain!

## Kesimpulan

Selamat! Anda telah berhasil memperbarui item rumus Power Query menggunakan Aspose.Cells for .NET. Dengan metode ini, Anda dapat mengotomatiskan modifikasi rumus Power Query dalam file Excel Anda, sehingga menghemat waktu dan tenaga Anda.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka yang hebat untuk memanipulasi file Excel dalam aplikasi .NET tanpa perlu menginstal Microsoft Excel.

### Apakah saya memerlukan Microsoft Excel untuk menjalankan Aspose.Cells?
Tidak, Aspose.Cells memungkinkan Anda membuat dan mengedit file Excel secara terprogram tanpa memerlukan Excel di server atau mesin pengembangan Anda.

### Jenis berkas Excel apa yang dapat saya gunakan menggunakan Aspose.Cells?
Anda dapat bekerja dengan .xlsx, .xls, .xlsm, dan beberapa format Excel lainnya menggunakan Aspose.Cells.

### Apakah ada versi uji coba yang tersedia untuk Aspose.Cells?
 Ya, Anda dapat mengunduh versi uji coba gratis dari[Halaman rilis Aspose Cells](https://releases.aspose.com/).

### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.Cells?
 Anda dapat mengakses dukungan melalui[Forum Aspose](https://forum.aspose.com/c/cells/9), tempat Anda dapat mengajukan pertanyaan dan mendapatkan jawaban dari komunitas dan tim Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
