---
title: Muat Lembar Terlihat Hanya dari File Excel
linktitle: Muat Lembar Terlihat Hanya dari File Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara memuat hanya lembar yang terlihat dari file Excel menggunakan Aspose.Cells untuk .NET dalam panduan langkah demi langkah ini.
weight: 12
url: /id/net/excel-file-handling/load-visible-sheets-only/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Muat Lembar Terlihat Hanya dari File Excel

## Perkenalan
Saat Anda bekerja dengan file Excel di aplikasi .NET, tantangan dalam mengelola beberapa lembar kerja menjadi jelas, terutama saat beberapa lembar disembunyikan atau tidak relevan dengan operasi Anda. Aspose.Cells untuk .NET adalah pustaka canggih yang membantu Anda memanipulasi file Excel secara efisien. Dalam artikel ini, kita akan membahas cara memuat hanya lembar yang terlihat dari file Excel, dengan memfilter data tersembunyi. Jika Anda pernah merasa kewalahan saat menavigasi data Excel, panduan ini cocok untuk Anda!
## Prasyarat
Sebelum memulai tutorial, pastikan Anda memiliki semua yang perlu diikuti:
1. Pemahaman Dasar C#: Tutorial ini dirancang untuk pengembang yang terbiasa dengan bahasa pemrograman C#.
2.  Aspose.Cells untuk .NET: Anda harus mengunduh dan menyiapkan pustaka Aspose.Cells untuk .NET. Anda dapat[unduh perpustakaan di sini](https://releases.aspose.com/cells/net/).
3. Visual Studio atau IDE apa pun: Anda harus memiliki IDE tempat Anda dapat menulis dan menguji kode C# Anda.
4. .NET Framework: Pastikan Anda telah menginstal .NET Framework yang diperlukan untuk menjalankan aplikasi Anda.
5. Contoh File Excel: Untuk latihan, buatlah contoh file Excel atau ikuti kode yang diberikan.
Sudah siap semuanya? Keren! Mari kita mulai!
## Paket Impor
Salah satu langkah pertama dalam setiap proyek C# yang bekerja dengan Aspose.Cells adalah mengimpor paket yang dibutuhkan. Ini memungkinkan Anda untuk mengakses semua fungsi yang disediakan oleh pustaka. Berikut cara melakukannya:
1. Buka Proyek Anda: Mulailah dengan membuka proyek C# Anda di Visual Studio atau IDE pilihan lainnya.
2. Tambahkan Referensi: Klik kanan proyek Anda di Solution Explorer, pilih "Tambah," lalu "Referensi." 
3. Telusuri Aspose.Cells: Temukan file Aspose.Cells.dll yang Anda unduh sebelumnya dan tambahkan ke referensi proyek Anda.
Langkah ini penting karena menghubungkan fungsionalitas Aspose.Cells ke proyek Anda. 
```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Setelah Anda mengimpor paket yang diperlukan, kita akan membuat contoh buku kerja Excel. Dalam buku kerja ini, kita akan memiliki beberapa lembar, dan salah satunya akan disembunyikan untuk tutorial ini.
## Langkah 1: Siapkan Lingkungan Anda
Pertama, mari kita atur lingkungan dan tentukan jalur untuk file sampel.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
string sampleFile = "output.xlsx";
string samplePath = dataDir + sampleFile;
```
 Dalam potongan kode ini, ganti`"Your Document Directory"` dengan jalur sebenarnya tempat Anda ingin menyimpan buku kerja Anda. 
## Langkah 2: Buat Buku Kerja
Selanjutnya, mari buat buku kerja dan tambahkan beberapa data.
```csharp
// Buat contoh buku kerja
Workbook createWorkbook = new Workbook();
createWorkbook.Worksheets["Sheet1"].Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet2").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets.Add("Sheet3").Cells["A1"].Value = "Aspose";
createWorkbook.Worksheets["Sheet3"].IsVisible = false; // Jadikan Sheet3 tersembunyi
createWorkbook.Save(samplePath);
```
Berikut rincian kejadiannya:
- Kami membuat buku kerja baru dan menambahkan tiga lembar.
- “Sheet1” dan “Sheet2” akan terlihat, sedangkan “Sheet3” akan disembunyikan.
- Kami kemudian menyimpan buku kerja ke jalur yang ditentukan.
## Langkah 3: Muat Buku Kerja Contoh dengan Opsi Muat
Sekarang kita memiliki buku kerja dengan lembar yang terlihat dan tersembunyi, saatnya memuatnya sambil memastikan kita hanya mengakses lembar yang terlihat.
```csharp
LoadOptions loadOptions = new LoadOptions();
loadOptions.LoadFilter = new CustomLoad();
```
Potongan kode ini menyiapkan opsi pemuatan untuk buku kerja, yang akan kita sesuaikan untuk memfilter lembar tersembunyi.
## Langkah 4: Tentukan Filter Beban Kustom
Untuk memuat lembar yang terlihat saja, kita perlu membuat filter pemuatan khusus. Berikut cara mendefinisikannya:
```csharp
class CustomLoad : LoadFilter
{
    public override void StartSheet(Worksheet sheet)
    {
        if (sheet.IsVisible)
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.All;
        }
        else
        {
            this.LoadDataFilterOptions = LoadDataFilterOptions.Structure;
        }
    }
}
```
-  Itu`StartSheet` metode memeriksa apakah setiap lembar terlihat.
- Jika terlihat, ia memuat semua data dari lembar itu.
- Jika tidak terlihat, ia akan melewati pemuatan data apa pun dari lembar tersebut.
## Langkah 5: Muat Buku Kerja Menggunakan Opsi Muat
Sekarang mari memuat buku kerja dan menampilkan data dari lembar yang terlihat.
```csharp
Workbook loadWorkbook = new Workbook(samplePath, loadOptions);
Console.WriteLine("Sheet1: A1: {0}", loadWorkbook.Worksheets["Sheet1"].Cells["A1"].Value);
Console.WriteLine("Sheet2: A1: {0}", loadWorkbook.Worksheets["Sheet2"].Cells["A1"].Value);
```
 Potongan kode ini menggunakan`loadOptions` untuk hanya mengimpor data dari lembar yang terlihat dan menampilkan konten sel A1 dari “Sheet1” dan “Sheet2.” 
## Kesimpulan
Nah, itu dia! Anda telah berhasil mempelajari cara memuat hanya lembar kerja yang terlihat dari file Excel menggunakan Aspose.Cells for .NET. Mengelola lembar kerja Excel Anda dapat menjadi mudah jika Anda tahu cara membatasi data yang Anda ambil dan bekerja hanya dengan apa yang Anda perlukan. Hal ini tidak hanya meningkatkan efisiensi aplikasi Anda, tetapi juga membuat kode Anda lebih bersih dan mudah dikelola. 
## Pertanyaan yang Sering Diajukan
### Bisakah saya memuat lembar tersembunyi jika diperlukan?
Ya, Anda cukup menyesuaikan kondisi di filter beban khusus untuk menyertakan lembar tersembunyi.
### Untuk apa Aspose.Cells digunakan?
Aspose.Cells digunakan untuk memanipulasi file Excel tanpa memerlukan Microsoft Excel untuk diinstal, menawarkan fungsionalitas seperti membaca, menulis, dan mengelola lembar kerja Excel.
### Apakah ada versi uji coba Aspose.Cells?
 Ya kamu bisa[unduh uji coba gratis](https://releases.aspose.com/) untuk menguji fitur-fiturnya.
### Di mana saya dapat menemukan dokumentasi untuk Aspose.Cells?
 Itu[dokumentasi](https://reference.aspose.com/cells/net/) menyediakan informasi lengkap tentang semua fitur.
### Bagaimana cara membeli Aspose.Cells?
 Anda dapat dengan mudah[beli Aspose.Cells](https://purchase.aspose.com/buy) dari halaman pembelian mereka.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
