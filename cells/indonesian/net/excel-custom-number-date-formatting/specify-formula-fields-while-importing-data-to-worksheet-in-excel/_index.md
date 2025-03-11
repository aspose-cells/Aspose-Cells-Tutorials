---
title: Tentukan Bidang Rumus Saat Mengimpor Data ke Lembar Excel
linktitle: Tentukan Bidang Rumus Saat Mengimpor Data ke Lembar Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara mengimpor data ke dalam lembar Excel dengan bidang rumus tertentu menggunakan Aspose.Cells untuk .NET dalam tutorial terperinci ini.
weight: 11
url: /id/net/excel-custom-number-date-formatting/specify-formula-fields-while-importing-data-to-worksheet-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tentukan Bidang Rumus Saat Mengimpor Data ke Lembar Excel

## Perkenalan

Jika berbicara tentang penanganan berkas Excel secara terprogram, Aspose.Cells for .NET merupakan alat yang sangat berharga. Alat ini menyediakan fungsionalitas yang tangguh untuk membuat, memodifikasi, dan memanipulasi lembar kerja Excel dengan mudah. Salah satu fitur menarik yang ditawarkannya adalah kemampuan untuk menentukan bidang rumus saat mengimpor data ke dalam lembar Excel. Bayangkan Anda sedang mengerjakan laporan keuangan dan perlu menghitung total secara otomatis berdasarkan masukan pengguna. Tutorial ini akan memandu Anda langkah demi langkah untuk mencapainya dengan pendekatan yang jelas dan lugas.

## Prasyarat

Sebelum masuk ke kode, mari pastikan Anda memiliki semua yang dibutuhkan. 

1. Visual Studio atau lingkungan pengembangan terpadu (IDE) .NET apa pun: Pastikan Anda memiliki IDE yang sesuai untuk menulis dan menjalankan kode C# Anda.
2.  Aspose.Cells untuk .NET: Anda perlu mengunduh dan merujuk pustaka Aspose.Cells di proyek Anda. Anda dapat mengunduhnya dari[Aspose merilis](https://releases.aspose.com/cells/net/).
3. Pengetahuan dasar C#: Keakraban dengan C# dan konsep pemrograman berorientasi objek akan membantu Anda memahami contoh-contoh dengan lebih baik.
4. .NET Framework: Tutorial ini mengasumsikan Anda menggunakan .NET Framework 4.5 atau yang lebih tinggi.

Setelah Anda menyelesaikan prasyarat, mari lanjutkan untuk mengimpor beberapa data ke dalam lembar Excel dengan bidang rumus yang ditentukan.

## Paket Impor

Sebelum Anda mulai menulis kode, Anda perlu mengimpor namespace Aspose.Cells yang diperlukan. Hal ini biasanya dilakukan di bagian atas berkas C# Anda:

```csharp
using Aspose.Cells;
using System;
using System.Collections.Generic;
```

Hal ini memungkinkan Anda untuk menggunakan kelas dan metode yang disediakan oleh pustaka Aspose.Cells tanpa perlu menambahkan awalan namespace setiap saat.

Mari kita uraikan keseluruhan proses menjadi langkah-langkah yang dapat dikelola:

## Langkah 1: Tentukan Direktori Output

Pertama, Anda perlu menentukan di mana Anda ingin menyimpan berkas Excel Anda. Berikut cara melakukannya:

```csharp
static string outputDir = "Your Document Directory"; // tentukan direktori dokumen Anda di sini
```

 Mengganti`"Your Document Directory"` dengan jalur berkas Anda yang sebenarnya. Di sinilah berkas Excel yang dihasilkan akan disimpan.

## Langkah 2: Buat Kelas yang Ditentukan Pengguna untuk Item Data

Berikutnya, kita akan mendefinisikan kelas untuk menyusun data yang rencananya akan kita impor.

```csharp
class DataItems
{
    public int Number1 { get; set; }
    public int Number2 { get; set; }
    public string Formula1 { get; set; }
    public string Formula2 { get; set; }
}
```

 Ini`DataItems` Kelas akan menampung bilangan bulat mentah dan rumus yang akan kita tulis pada lembar Excel. 

## Langkah 3: Inisialisasi Daftar untuk Menampung Item Data

 Kami akan menggunakan daftar untuk menampung beberapa contoh`DataItems` kelas.

```csharp
List<DataItems> dis = new List<DataItems>();
```

## Langkah 4: Tambahkan Item Data ke Daftar

Sekarang, mari tambahkan beberapa entri ke daftar kita. Setiap entri akan berisi dua angka dan dua rumus.

```csharp
// Tentukan dan tambahkan setiap item data
DataItems di = new DataItems();
di.Number1 = 2002;
di.Number2 = 3502;
di.Formula1 = "=SUM(A2,B2)";
di.Formula2 = "=HYPERLINK(\"https://www.aspose.com\",\"Situs Web Aspose\")";
dis.Add(di);

// Ulangi untuk item data tambahan
```

 Pastikan untuk menyesuaikan masing-masing`DataItems` contoh dengan nilai dan rumus yang unik.

## Langkah 5: Buat Buku Kerja dan Akses Lembar Kerja

Berikutnya, buat buku kerja dan akses lembar kerja pertama tempat kita nantinya akan mengimpor data.

```csharp
Workbook wb = new Workbook(); // membuat buku kerja baru
Worksheet ws = wb.Worksheets[0]; // akses lembar kerja pertama
```

## Langkah 6: Tentukan Opsi Tabel Impor

Di sinilah keajaiban terjadi. Anda perlu menentukan kolom mana dalam data Anda yang sesuai dengan rumus. 

```csharp
ImportTableOptions opts = new ImportTableOptions();
opts.IsFormulas = new bool[] { false, false, true, true };
```

 Dalam contoh ini, dua bidang terakhir berisi rumus, yang ditunjukkan oleh`true` , sedangkan dua bidang pertama diatur ke`false`.

## Langkah 7: Impor Objek Kustom

Sekarang semuanya sudah disiapkan, mari impor daftar item data kita ke dalam lembar kerja.

```csharp
ws.Cells.ImportCustomObjects(dis, 0, 0, opts);
```

Baris ini secara efektif mengimpor data yang dimulai pada sel A1.

## Langkah 8: Hitung Rumus

Karena kami telah mengimpor beberapa rumus, penting untuk menghitungnya.

```csharp
wb.CalculateFormula();
```

Metode ini memastikan bahwa rumus Anda dievaluasi berdasarkan dependensinya.

## Langkah 9: Sesuaikan Kolom Secara Otomatis

Untuk memastikan data Anda ramah untuk ditampilkan, Anda dapat menyesuaikan kolom secara otomatis berdasarkan konten.

```csharp
ws.AutoFitColumns();
```

Langkah ini mengoptimalkan tata letak berkas Excel. 

## Langkah 10: Simpan File Excel Anda

Akhirnya, saatnya untuk menyimpan file Excel yang baru Anda buat. 

```csharp
wb.Save(outputDir + "outputSpecifyFormulaFieldsWhileImportingDataToWorksheet.xlsx");
```

Pastikan nama file keluaran Anda relevan dan deskriptif!

## Langkah 11: Memeriksa Eksekusi

Sebagai cara sederhana untuk mengonfirmasi bahwa semuanya berjalan dengan benar, Anda mungkin ingin mencetak pesan.

```csharp
Console.WriteLine("SpecifyFormulaFieldsWhileImportingDataToWorksheet executed successfully.");
```

Ini memberi Anda umpan balik langsung bahwa kode telah berfungsi tanpa masalah.

## Kesimpulan

Nah, itu dia! Anda telah berhasil mengimpor data ke dalam lembar Excel menggunakan Aspose.Cells for .NET dan menentukan bidang rumus. Dengan mengikuti langkah-langkah ini, Anda dapat menerapkan teknik serupa untuk mengotomatiskan tugas pemrosesan data yang disesuaikan dengan kebutuhan Anda. Baik Anda mengolah angka untuk laporan atau sekadar mengelola data, menguasai seni manipulasi Excel dengan Aspose adalah keterampilan yang layak dimiliki.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET yang dirancang untuk membuat, memanipulasi, dan mengonversi file Excel secara terprogram.

### Bagaimana cara menginstal Aspose.Cells untuk .NET?
 Anda dapat mengunduhnya dari[Aspose merilis](https://releases.aspose.com/cells/net/) dan merujuknya dalam proyek Anda.

### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya, Aspose menawarkan uji coba gratis yang tersedia di[tautan ini](https://releases.aspose.com/).

### Di mana saya dapat menemukan lebih banyak contoh?
 Contoh dan dokumentasi tambahan dapat ditemukan di[Halaman dokumentasi Aspose](https://reference.aspose.com/cells/net/).

### Bagaimana jika saya mengalami masalah saat menggunakan Aspose?
 Anda dapat mencari bantuan dari forum dukungan Aspose[Di Sini](https://forum.aspose.com/c/cells/9).
 
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
