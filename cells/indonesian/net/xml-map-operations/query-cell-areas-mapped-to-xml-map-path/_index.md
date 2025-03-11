---
title: Kueri Area Sel yang Dipetakan ke Jalur Peta XML menggunakan Aspose.Cells
linktitle: Kueri Area Sel yang Dipetakan ke Jalur Peta XML menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengkueri area sel yang dipetakan XML di Excel menggunakan Aspose.Cells untuk .NET. Panduan langkah demi langkah ini membantu Anda mengekstrak data XML terstruktur dengan lancar.
weight: 12
url: /id/net/xml-map-operations/query-cell-areas-mapped-to-xml-map-path/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kueri Area Sel yang Dipetakan ke Jalur Peta XML menggunakan Aspose.Cells

## Perkenalan
Pernahkah Anda bertanya-tanya bagaimana cara bekerja dengan data XML di Excel menggunakan .NET? Dengan Aspose.Cells untuk .NET, pustaka yang hebat untuk manipulasi spreadsheet, Anda dapat dengan mudah berinteraksi dengan peta XML dalam file Excel Anda. Bayangkan Anda memiliki file Excel yang diisi dengan data terstruktur, dan Anda perlu mengkueri area tertentu yang dipetakan ke jalur XML—di sinilah Aspose.Cells bersinar. Dalam tutorial ini, kita akan menyelami kueri area sel yang dipetakan ke jalur peta XML dalam file Excel menggunakan Aspose.Cells untuk .NET. Apakah Anda ingin membuat laporan dinamis atau mengotomatiskan ekstraksi data, panduan ini akan membantu Anda dengan petunjuk langkah demi langkah.
## Prasyarat
Sebelum kita mulai membuat kode, ada beberapa hal yang Anda perlukan:
1.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka ini. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/) atau dapatkan melalui NuGet.
2. File Excel yang dipetakan XML: Untuk tutorial ini, Anda memerlukan file Excel (.xlsx) yang berisi peta XML.
3. Lingkungan Pengembangan: Panduan ini mengasumsikan Anda menggunakan Visual Studio, tetapi editor C# apa pun seharusnya berfungsi dengan baik.
4.  Lisensi Aspose: Anda dapat menggunakan lisensi sementara jika diperlukan, yang bisa Anda dapatkan[Di Sini](https://purchase.aspose.com/temporary-license/).
## Paket Impor
Untuk memulai, pastikan untuk mengimpor namespace yang diperlukan dalam berkas kode Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Diagnostics;
using System.Collections;
```
Dengan paket ini, Anda akan siap mengakses buku kerja, memanipulasi lembar kerja, dan menanyakan peta XML dalam lembar kerja.
## Langkah 1: Muat File Excel yang Berisi Peta XML
Pertama, Anda perlu memuat berkas Excel yang sudah berisi pemetaan XML. Berkas ini berfungsi sebagai sumber data.
```csharp
// Tentukan jalur direktori untuk sumber dan keluaran
string sourceDir = "Your Document Directory";
// Memuat file Excel
Workbook wb = new Workbook(sourceDir + "sampleXmlMapQuery.xlsx");
```
 Di Sini,`Workbook` adalah kelas yang mewakili seluruh file Excel, yang Anda muat menggunakan jalur file. Ganti`"Your Document Directory"` dengan jalur direktori sebenarnya tempat berkas Anda berada.
## Langkah 2: Akses Peta XML di Buku Kerja
Setelah berkas dimuat, langkah berikutnya adalah mengakses peta XML dalam buku kerja. Peta ini berfungsi sebagai jembatan antara lembar kerja dan data XML Anda.
```csharp
//Akses peta XML pertama di buku kerja
XmlMap xmap = wb.Worksheets.XmlMaps[0];
```
 Di sini, kami mengambil peta XML pertama di buku kerja dengan mengakses`XmlMaps[0]` dari`Worksheets` koleksi. Anda dapat memiliki beberapa peta XML dalam satu buku kerja, dan tutorial ini berfokus pada yang pertama.
## Langkah 3: Akses Lembar Kerja untuk Menanyakan
Setelah peta XML siap, sekarang Anda perlu memilih lembar kerja tertentu tempat data yang dipetakan berada. Ini biasanya lembar kerja pertama, tetapi tergantung pada pengaturan berkas Anda.
```csharp
// Akses lembar kerja pertama di buku kerja
Worksheet ws = wb.Worksheets[0];
```
Mengakses lembar kerja tempat data yang dipetakan XML berada memungkinkan Anda menargetkan sel tertentu. Di sini, kami menggunakan lembar kerja pertama, tetapi Anda dapat memilih lembar kerja lain dengan mengubah indeks atau menentukan nama.
## Langkah 4: Kueri Peta XML Menggunakan Jalur
Sekarang tibalah bagian inti: meminta peta XML. Di sini, Anda akan menentukan jalur XML dan mengambil data yang dipetakan ke jalur tersebut dalam lembar kerja.
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData");
ArrayList ret = ws.XmlMapQuery("/MiscData", xmap);
```
 Itu`XmlMapQuery`metode ini mengambil dua parameter—jalur XML dan peta XML yang Anda ambil sebelumnya. Dalam contoh ini, kami akan meminta jalur`/MiscData` , yang merupakan jalur tingkat atas dalam struktur XML. Hasilnya disimpan dalam`ArrayList`, membuatnya mudah untuk diulang.
## Langkah 5: Menampilkan Hasil Kueri
 Setelah data di-query, langkah selanjutnya adalah menampilkan hasilnya. Mari kita cetak setiap item dari`ArrayList` ke konsol untuk melihat dengan jelas data apa yang diekstraksi.
```csharp
// Cetak hasil kueri
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
 Loop ini melewati setiap item di`ArrayList` dan mencetaknya ke konsol. Anda akan melihat data yang diekstrak dari jalur peta XML`/MiscData`.
## Langkah 6: Menanyakan Jalur XML Bersarang
 Untuk menyempurnakan kueri Anda, mari kita telusuri jalur bersarang dalam struktur XML, seperti`/MiscData/row/Color`.
```csharp
Console.WriteLine("Query Xml Map from Path - /MiscData/row/Color");
ret = ws.XmlMapQuery("/MiscData/row/Color", xmap);
```
 Di sini, kami meminta jalur yang lebih spesifik dalam data XML. Dengan mempersempit ke`/MiscData/row/Color` , Anda hanya menargetkan informasi warna di bawah`row` simpul dalam struktur XML.
## Langkah 7: Menampilkan Hasil Kueri Jalur Bersarang
Terakhir, Anda ingin mencetak hasil kueri yang disempurnakan ini untuk melihat nilai spesifik yang dipetakan ke`/MiscData/row/Color`.
```csharp
// Cetak hasil kueri jalur bersarang
for (int i = 0; i < ret.Count; i++)
{
    Console.WriteLine(ret[i]);
}
```
Sama seperti sebelumnya, loop ini mengeluarkan hasil kueri ke konsol, yang memungkinkan Anda meninjau data spesifik yang diambil dari jalur XML bersarang.
## Kesimpulan
Nah, itu dia! Dengan Aspose.Cells untuk .NET, kueri area sel yang dipetakan ke jalur peta XML menjadi mudah dan sangat efektif. Fitur hebat ini mengubah permainan bagi pengembang yang perlu mengekstrak data XML tertentu dari spreadsheet. Kini Anda memiliki dasar untuk mengimplementasikan kueri XML yang lebih kompleks dan bahkan menggabungkan beberapa pemetaan XML dalam alur kerja Excel Anda. Siap untuk mengembangkannya lebih jauh? Jelajahi dokumentasi Aspose.Cells untuk fungsi peta XML tambahan guna menyempurnakan aplikasi Anda!
## Pertanyaan yang Sering Diajukan
### Bisakah saya memetakan beberapa file XML dalam satu buku kerja Excel?  
Ya, Aspose.Cells memungkinkan Anda mengelola beberapa peta XML dalam buku kerja, yang memungkinkan interaksi data yang kompleks.
### Apa yang terjadi jika jalur XML tidak ada di peta?  
 Jika jalur tidak valid atau tidak ada,`XmlMapQuery` metode akan mengembalikan kosong`ArrayList`.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells untuk .NET?  
 Ya, lisensi diperlukan untuk fungsionalitas penuh. Anda dapat mencoba[uji coba gratis](https://releases.aspose.com/)atau dapatkan[lisensi sementara](https://purchase.aspose.com/temporary-license/).
### Bisakah saya menyimpan data yang ditanyakan ke file Excel baru?  
Tentu saja! Anda dapat mengekstrak data yang diminta dan menuliskannya ke file Excel lain atau format lain yang didukung oleh Aspose.Cells.
### Apakah mungkin untuk menanyakan peta XML dalam format selain Excel (.xlsx)?  
Pemetaan XML didukung dalam file .xlsx. Untuk format lain, fungsionalitasnya mungkin terbatas atau tidak didukung.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
