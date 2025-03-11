---
title: Memperbarui Item Rumus Power Query di Buku Kerja
linktitle: Memperbarui Item Rumus Power Query di Buku Kerja
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara memperbarui rumus Power Query di Excel dengan Aspose.Cells untuk .NET dalam panduan langkah demi langkah yang komprehensif ini.
weight: 27
url: /id/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Memperbarui Item Rumus Power Query di Buku Kerja

## Perkenalan
Memahami cara mengelola data secara efisien menggunakan Power Query di Excel adalah hal yang sangat penting bagi setiap analis data atau penggemar Excel. Jika Anda pernah perlu memperbarui item rumus di buku kerja Power Query, Anda berada di tempat yang tepat. Panduan ini dirancang khusus untuk membantu Anda mempelajari cara menggunakan Aspose.Cells for .NET untuk memperbarui rumus Power Query di buku kerja Excel dengan lancar. Dengan beberapa langkah sederhana, Anda akan dapat memanipulasi dan menyederhanakan data, memastikan buku kerja Anda tetap dinamis dan terpusat.
## Prasyarat
Sebelum Anda mulai menyelami contoh kode dan langkah-langkahnya, mari kita bahas apa saja yang Anda perlukan:
1. Pemahaman Dasar tentang C# dan .NET: Keakraban dengan konsep pemrograman dalam C# akan bermanfaat saat kita akan menulis beberapa kode.
2.  Instal Aspose.Cells untuk .NET: Anda perlu mengintegrasikan pustaka Aspose.Cells ke dalam proyek .NET Anda. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
3. File Excel Siap untuk Dimodifikasi: Pastikan Anda memiliki file Excel yang berisi Power Query yang ingin Anda perbarui. Anda perlu memiliki contoh buku kerja seperti`SamplePowerQueryFormula.xlsx` sesuai keinginan Anda.
## Paket Impor
Untuk memulai, pastikan Anda telah menyertakan namespace berikut dalam file C# Anda:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Ini akan memungkinkan Anda mengakses fungsionalitas yang disediakan oleh pustaka Aspose.Cells, khususnya untuk bekerja dengan buku kerja dan data Power Query.
## Langkah 1: Siapkan Direktori Kerja Anda
Hal pertama yang paling utama, Anda perlu menentukan di mana file sumber dan keluaran Anda berada. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
 Pada langkah ini, Anda menentukan jalur direktori. Ganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Excel Anda disimpan. Ini memberi tahu program tempat mencari file sumber dan tempat menyimpan file yang diperbarui.
## Langkah 2: Muat Buku Kerja
Sekarang setelah Anda menetapkan direktori kerja, langkah berikutnya adalah memuat berkas Excel ke dalam program.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Di sini, Anda membuat`Workbook` objek yang memuat file Excel yang ditentukan.`Workbook`kelas adalah bagian dari pustaka Aspose.Cells dan penting untuk operasi apa pun yang akan Anda lakukan pada berkas Excel tersebut.
## Langkah 3: Mengakses Data Power Query
Setelah buku kerja dimuat, saatnya mengakses rumus Power Query yang tersimpan di dalamnya.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Pada baris ini,`DataMashup` Properti membantu mengakses struktur data Power Query dalam buku kerja. Properti ini memberi Anda kemampuan untuk berinteraksi dengan berbagai aspek data Power Query yang terdapat dalam file Excel Anda.
## Langkah 4: Ulangi Rumus Power Query
Setelah data Power Query dapat diakses, langkah berikutnya adalah mengulangi setiap rumus yang ada.
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
 Di sinilah keajaiban terjadi. Kami mengulang setiap`PowerQueryFormula` dan kemudian melalui masing-masing`PowerQueryFormulaItem` . Itu`if` pernyataan mencari item rumus bernama "Sumber" dan memperbarui nilainya menjadi jalur file sumber yang ingin Anda rujuk ke Power Query. Ini memungkinkan Anda untuk secara dinamis mengubah file mana Power Query menarik data.
## Langkah 5: Simpan Buku Kerja yang Diperbarui
Setelah memperbarui item rumus yang diperlukan, langkah terakhir Anda adalah menyimpan Buku Kerja.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Baris ini menyimpan buku kerja yang dimodifikasi ke berkas baru, dengan demikian mempertahankan versi asli sembari memungkinkan Anda bekerja dengan versi yang diperbarui.
## Langkah 6: Pesan Konfirmasi
Terakhir, ada baiknya Anda memeriksa apakah kode Anda telah dijalankan dengan benar.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Pesan sederhana ini akan mengonfirmasikan kepada Anda di konsol bahwa operasi Anda berhasil, memberikan akhir proses yang meyakinkan.
## Kesimpulan
Nah, itu dia! Memperbarui item rumus Power Query di Excel menggunakan Aspose.Cells untuk .NET dapat dilakukan hanya dalam beberapa langkah mudah. Dengan mengikuti panduan ini, Anda dapat mengelola koneksi data Excel secara efisien dan menjaga buku kerja Anda tetap berjalan lancar. Baik Anda seorang profesional berpengalaman atau baru mulai memanipulasi data, Aspose.Cells menyediakan cara yang hebat untuk mengotomatiskan dan menyempurnakan alur kerja Excel. 
## Pertanyaan yang Sering Diajukan
### Bisakah saya menggunakan Aspose.Cells dengan versi .NET mana pun?
Aspose.Cells kompatibel dengan beberapa versi .NET, termasuk .NET Framework dan .NET Core.
### Apakah Aspose.Cells gratis untuk digunakan?
 Aspose.Cells menawarkan uji coba gratis, tetapi untuk penggunaan berkelanjutan, diperlukan lisensi. Anda dapat memperoleh lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).
### Bagaimana jika file Excel saya yang ada tidak memiliki Power Query?
Proses yang dijelaskan berfokus pada pembaruan item Power Query, jadi jika file Anda tidak memilikinya, Anda perlu menyertakan Power Query terlebih dahulu.
### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells?
 Periksa dokumentasi untuk panduan dan contoh yang lengkap. Kunjungi[dokumentasi](https://reference.aspose.com/cells/net/).
### Bagaimana cara melaporkan bug atau masalah dengan Aspose.Cells?
Anda dapat menghubungi forum dukungan mereka untuk mendapatkan bantuan terkait masalah apa pun yang Anda hadapi.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
