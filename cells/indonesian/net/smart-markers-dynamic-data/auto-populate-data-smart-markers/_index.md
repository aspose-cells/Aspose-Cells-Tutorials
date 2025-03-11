---
title: Mengisi Data Secara Otomatis di Seluruh Lembar di Aspose.Cells
linktitle: Mengisi Data Secara Otomatis di Seluruh Lembar di Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara mengisi data secara otomatis di beberapa lembar kerja di Excel menggunakan pustaka Aspose.Cells for .NET. Pelajari proses langkah demi langkah untuk menyederhanakan tugas pengelolaan data Anda.
weight: 11
url: /id/net/smart-markers-dynamic-data/auto-populate-data-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengisi Data Secara Otomatis di Seluruh Lembar di Aspose.Cells

## Perkenalan
Dalam dunia manajemen dan otomatisasi data, kemampuan untuk mengisi data secara efisien di beberapa lembar kerja merupakan tugas yang krusial. Aspose.Cells untuk .NET menyediakan solusi yang ampuh untuk masalah ini, yang memungkinkan Anda mentransfer data dari sumber data ke beberapa lembar dalam buku kerja Excel dengan lancar. Dalam tutorial ini, kami akan memandu Anda melalui proses pengisian data otomatis di seluruh lembar kerja langkah demi langkah menggunakan pustaka Aspose.Cells.
## Prasyarat
Sebelum kita masuk ke tutorial, pastikan Anda memiliki prasyarat berikut:
1. [Bahasa Indonesia: Microsoft Visual Studio](https://visualstudio.microsoft.com/downloads/) - Ini adalah lingkungan pengembangan utama untuk bekerja dengan Aspose.Cells untuk .NET.
2. [Aspose.Cells untuk .NET](https://releases.aspose.com/cells/net/) - Anda dapat mengunduh versi terbaru pustaka dari situs web Aspose.
 Untuk memulai, Anda dapat menggunakan[uji coba gratis**](https://releases.aspose.com/) atau[**purchase a license](https://purchase.aspose.com/buy) dari Aspose.Cells untuk .NET.
## Paket Impor
Mulailah dengan mengimpor paket yang diperlukan dalam proyek C# Anda:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Data;
```
## Langkah 1: Buat Tabel Data
Langkah pertama adalah membuat tabel data yang akan berfungsi sebagai sumber data untuk lembar kerja Anda. Dalam contoh ini, kita akan membuat tabel data sederhana bernama "Karyawan" dengan satu kolom "IDKaryawan":
```csharp
//Direktori keluaran
string outputDir = "Your Document Directory";
//Buat tabel data karyawan
DataTable dt = new DataTable("Employees");
dt.Columns.Add("EmployeeID", typeof(int));
//Tambahkan baris di dalam tabel data
dt.Rows.Add(1230);
dt.Rows.Add(1231);
dt.Rows.Add(1232);
dt.Rows.Add(1233);
dt.Rows.Add(1234);
dt.Rows.Add(1235);
dt.Rows.Add(1236);
dt.Rows.Add(1237);
dt.Rows.Add(1238);
dt.Rows.Add(1239);
dt.Rows.Add(1240);
dt.Rows.Add(1241);
dt.Rows.Add(1242);
dt.Rows.Add(1243);
dt.Rows.Add(1244);
dt.Rows.Add(1245);
dt.Rows.Add(1246);
dt.Rows.Add(1247);
dt.Rows.Add(1248);
dt.Rows.Add(1249);
dt.Rows.Add(1250);
```
## Langkah 2: Buat Pembaca Data dari Tabel Data
 Selanjutnya, kita akan membuat`DataTableReader` dari tabel data yang baru saja kita buat. Ini akan memungkinkan kita untuk menggunakan tabel data sebagai sumber data untuk pustaka Aspose.Cells:
```csharp
//Buat pembaca data dari tabel data
DataTableReader dtReader = dt.CreateDataReader();
```
## Langkah 3: Buat Buku Kerja Baru
 Sekarang, kita akan membuat buku kerja baru menggunakan`Workbook` kelas yang disediakan oleh Aspose.Cells:
```csharp
//Buat buku kerja kosong
Workbook wb = new Workbook();
```
## Langkah 4: Tambahkan Penanda Cerdas ke Lembar Kerja
Pada langkah ini, kita akan menambahkan penanda pintar ke sel-sel di lembar kerja pertama dan kedua buku kerja. Penanda pintar ini akan digunakan untuk mengisi data dari tabel data:
```csharp
//Akses lembar kerja pertama dan tambahkan penanda pintar di sel A1
Worksheet ws = wb.Worksheets[0];
ws.Cells["A1"].PutValue("&=Employees.EmployeeID");
//Tambahkan lembar kerja kedua dan tambahkan penanda pintar di sel A1
wb.Worksheets.Add();
ws = wb.Worksheets[1];
ws.Cells["A1"].PutValue("&=Employees.EmployeeID");
```
## Langkah 5: Buat Desainer Buku Kerja
 Sekarang kita akan membuat`WorkbookDesigner` objek, yang akan membantu kita mengatur sumber data dan memproses penanda pintar:
```csharp
//Buat desainer buku kerja
WorkbookDesigner wd = new WorkbookDesigner(wb);
```
## Langkah 6: Tetapkan Sumber Data
 Selanjutnya, kita akan mengatur sumber data untuk perancang buku kerja. Kita akan menggunakan`DataTableReader` kita buat sebelumnya dan tentukan jumlah baris yang akan diproses:
```csharp
//Tetapkan sumber data dengan pembaca data
wd.SetDataSource("Employees", dtReader, 15);
```
## Langkah 7: Memproses Penanda Cerdas
Terakhir, kita akan memproses penanda pintar di lembar kerja pertama dan kedua:
```csharp
//Proses tag penanda pintar di lembar kerja pertama dan kedua
wd.Process(0, false);
wd.Process(1, false);
```
## Langkah 8: Simpan Buku Kerja
Langkah terakhir adalah menyimpan buku kerja ke direktori keluaran yang ditentukan:
```csharp
//Simpan buku kerja
wb.Save(outputDir + "outputAutoPopulateSmartMarkerDataToOtherWorksheets.xlsx");
Console.WriteLine("AutoPopulateSmartMarkerDataToOtherWorksheets executed successfully.");
```
Selesai! Anda telah berhasil menggunakan Aspose.Cells for .NET untuk mengisi data secara otomatis di beberapa lembar kerja dalam buku kerja Excel.
## Kesimpulan
Dalam tutorial ini, Anda telah mempelajari cara menggunakan pustaka Aspose.Cells for .NET untuk mengisi data secara otomatis di beberapa lembar kerja dalam buku kerja Excel. Dengan memanfaatkan kekuatan penanda pintar dan`WorkbookDesigner` kelas, Anda dapat secara efisien mentransfer data dari sumber data ke berbagai lembar dalam buku kerja Anda.
## Pertanyaan yang Sering Diajukan
### Dapatkah saya menggunakan Aspose.Cells untuk .NET untuk mengisi data secara otomatis di beberapa buku kerja, bukan hanya lembar kerja?
 Ya, Anda juga dapat menggunakan Aspose.Cells untuk mengisi data secara otomatis di beberapa buku kerja. Prosesnya mirip dengan apa yang telah kita bahas dalam tutorial ini, tetapi Anda harus bekerja dengan beberapa`Workbook` objek, bukan hanya satu.
### Bagaimana saya dapat menyesuaikan tampilan dan format data yang terisi otomatis?
Aspose.Cells menyediakan berbagai macam opsi pemformatan yang dapat Anda terapkan pada data yang terisi otomatis. Anda dapat mengatur font, ukuran, warna, batas, dan lainnya menggunakan berbagai properti dan metode yang tersedia di pustaka.
### Apakah ada cara untuk menangani kumpulan data besar secara efisien saat mengisi data secara otomatis?
 Ya, Aspose.Cells menawarkan fitur seperti lazy loading dan chunking yang dapat membantu Anda bekerja dengan kumpulan data besar secara lebih efisien. Anda dapat menjelajahi opsi ini di[dokumentasi](https://reference.aspose.com/cells/net/).
### Dapatkah saya menggunakan Aspose.Cells untuk mengisi data secara otomatis dari database, bukan dari tabel data?
 Tentu saja! Aspose.Cells dapat bekerja dengan berbagai sumber data, termasuk database. Anda dapat menggunakan`DataTableReader` atau`DataReader` kelas untuk terhubung ke basis data Anda dan menggunakan data untuk pengisian otomatis.
### Apakah ada cara untuk mengotomatiskan seluruh proses pengisian data otomatis di seluruh lembar?
Ya, Anda dapat membuat komponen atau metode yang dapat digunakan kembali yang merangkum langkah-langkah yang telah kita bahas dalam tutorial ini. Dengan cara ini, Anda dapat dengan mudah mengintegrasikan logika pengisian otomatis ke dalam aplikasi atau skrip Anda, menjadikannya proses yang lancar dan otomatis.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
