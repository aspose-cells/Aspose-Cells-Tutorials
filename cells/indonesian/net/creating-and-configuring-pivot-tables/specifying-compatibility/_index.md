---
title: Tentukan Kompatibilitas File Excel Secara Terprogram di .NET
linktitle: Tentukan Kompatibilitas File Excel Secara Terprogram di .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara memanipulasi tabel pivot Excel dengan Aspose.Cells untuk .NET, termasuk pembaruan data, pengaturan kompatibilitas, dan pemformatan sel.
weight: 23
url: /id/net/creating-and-configuring-pivot-tables/specifying-compatibility/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tentukan Kompatibilitas File Excel Secara Terprogram di .NET

## Perkenalan

Dalam dunia yang digerakkan oleh data saat ini, mengelola dan memanipulasi file Excel secara terprogram telah menjadi hal yang penting bagi banyak pengembang. Jika Anda bekerja dengan Excel dalam .NET, Aspose.Cells adalah pustaka canggih yang memudahkan pembuatan, pembacaan, modifikasi, dan penyimpanan file Excel. Salah satu fitur penting dari pustaka ini memungkinkan Anda menentukan kompatibilitas file Excel secara terprogram. Dalam tutorial ini, kita akan menjelajahi cara memanipulasi file Excel, terutama berfokus pada pengelolaan kompatibilitas menggunakan Aspose.Cells untuk .NET. Pada akhirnya, Anda akan memahami cara mengatur kompatibilitas untuk file Excel, terutama untuk tabel pivot, sambil menyegarkan dan mengelola data.

## Prasyarat

Sebelum terjun ke fase pengkodean, pastikan Anda memiliki hal berikut:

1. Pengetahuan dasar C#: Karena kita akan menulis kode dalam C#, pemahaman yang mendalam tentang bahasa tersebut akan membantu Anda memahami tutorial ini dengan lebih baik.
2.  Aspose.Cells untuk pustaka .NET: Anda dapat mengunduhnya dari[Aspose Cells merilis halaman](https://releases.aspose.com/cells/net/)Jika Anda belum mencobanya, pertimbangkan untuk mencoba uji coba gratis terlebih dahulu untuk mencoba fitur-fiturnya.
3. Visual Studio: Sebuah IDE tempat Anda dapat menulis dan menguji kode C# secara efektif.
4.  Contoh File Excel: Pastikan Anda memiliki contoh file Excel, sebaiknya yang berisi tabel pivot untuk demo. Untuk contoh kita, kita akan menggunakan`sample-pivot-table.xlsx`.

Jika prasyarat ini terpenuhi, mari kita mulai proses pengkodean.

## Paket Impor

Sebelum Anda mulai menulis aplikasi, Anda perlu menyertakan namespace yang diperlukan dalam kode Anda untuk memanfaatkan pustaka Aspose.Cells secara efektif. Berikut cara melakukannya.

### Impor Ruang Nama Aspose.Cells

```csharp
using System.IO;
using System;
using Aspose.Cells;
using Aspose.Cells.Pivot;
using System.Drawing;
```

Baris kode ini memastikan bahwa Anda dapat mengakses semua kelas dan metode dalam pustaka Aspose.Cells.

Sekarang, mari kita uraikan prosesnya secara rinci untuk memastikan semuanya jelas dan mudah dipahami.

## Langkah 1: Siapkan Direktori Anda

Pertama-tama, siapkan direktori tempat file Excel Anda berada. Penting untuk menyediakan jalur file yang benar.

```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```

 Di sini, ganti`"Your Document Directory"`dengan jalur sebenarnya ke berkas Excel Anda. Di sinilah berkas tabel pivot contoh Anda seharusnya berada.

## Langkah 2: Muat File Excel Sumber

Berikutnya, kita perlu memuat berkas Excel yang berisi contoh tabel pivot. 

```csharp
// Muat file excel sumber yang berisi contoh tabel pivot
Workbook wb = new Workbook(dataDir + "sample-pivot-table.xlsx");
```

 Pada langkah ini, kita membuat sebuah instance dari`Workbook` kelas, yang memuat berkas Excel yang ditentukan. 

## Langkah 3: Akses Lembar Kerja

Sekarang buku kerja telah dimuat, Anda harus mengakses lembar kerja yang berisi data tabel pivot.

```csharp
// Akses lembar kerja pertama yang berisi data tabel pivot
Worksheet dataSheet = wb.Worksheets[0];
```

Di sini, kita mengakses lembar kerja pertama tempat tabel pivot berada. Anda juga dapat melakukan pengulangan atau menentukan lembar kerja lain berdasarkan struktur Excel Anda.

## Langkah 4: Memanipulasi Data Sel

Berikutnya, Anda akan mengubah beberapa nilai sel di lembar kerja. 

### Langkah 4.1: Ubah Sel A3

Mari kita mulai dengan mengakses sel A3 dan menetapkan nilainya.

```csharp
// Akses sel A3 dan atur datanya
Cells cells = dataSheet.Cells;
Cell cell = cells["A3"];
cell.PutValue("FooBar");
```

Potongan kode ini memperbarui sel A3 dengan nilai “FooBar”.

### Langkah 4.2: Ubah Sel B3 dengan String Panjang

Sekarang, mari kita tetapkan string panjang ke dalam sel B3, yang melebihi batas karakter standar Excel.

```csharp
// Akses sel B3, atur datanya
string longStr = "Very long text 1. very long text 2.... [continue your long string]";
cell = cells["B3"];
cell.PutValue(longStr);
```

Kode ini penting karena menetapkan ekspektasi Anda mengenai batasan data, terutama saat bekerja dengan pengaturan kompatibilitas di Excel.

## Langkah 5: Periksa Panjang Sel B3

Penting juga untuk mengonfirmasi panjang string yang kita masukkan.

```csharp
// Cetak panjang string sel B3
Console.WriteLine("Length of original data string: " + cell.StringValue.Length);
```

Ini hanya untuk verifikasi untuk menunjukkan berapa banyak karakter yang ada di sel Anda.

## Langkah 6: Tetapkan Nilai Sel Lainnya

Sekarang kita akan mengakses lebih banyak sel dan menetapkan beberapa nilai.

```csharp
// Akses sel C3 dan atur datanya
cell = cells["C3"];
cell.PutValue("closed");

// Akses sel D3 dan atur datanya
cell = cells["D3"];
cell.PutValue("2016/07/21");
```

Masing-masing potongan kode ini memperbarui beberapa sel tambahan dalam lembar kerja.

## Langkah 7: Akses Tabel Pivot

Berikutnya, Anda akan mengakses lembar kerja kedua, yang terdiri dari data tabel pivot.

```csharp
//Mengakses lembar kerja kedua yang berisi tabel pivot
Worksheet pivotSheet = wb.Worksheets[1];

// Akses tabel pivot
PivotTable pivotTable = pivotSheet.PivotTables[0];
```

Cuplikan ini memungkinkan Anda memanipulasi tabel pivot untuk pengaturan kompatibilitas.

## Langkah 8: Mengatur Kompatibilitas untuk Excel 2003

Sangat penting untuk menentukan apakah tabel pivot Anda kompatibel dengan Excel 2003 atau tidak. 

```csharp
// Properti IsExcel2003Compatible memberi tahu apakah PivotTable kompatibel untuk Excel2003 saat menyegarkan PivotTable
pivotTable.IsExcel2003Compatible = true;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

 Di sinilah transformasi yang sebenarnya dimulai. Dengan menetapkan`IsExcel2003Compatible` ke`true`, Anda membatasi panjang karakter hingga 255 saat menyegarkan.

## Langkah 9: Periksa Panjang Setelah Pengaturan Kompatibilitas

Setelah mengatur kompatibilitas, mari kita lihat bagaimana pengaruhnya terhadap data.

```csharp
// Periksa nilai sel B5 dari lembar pivot.
Cell b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to True: " + b5.StringValue.Length);
```

Anda mungkin akan melihat keluaran yang mengonfirmasi efek pemotongan jika data awal melebihi 255 karakter.

## Langkah 10: Ubah Pengaturan Kompatibilitas

Sekarang, mari kita ubah pengaturan kompatibilitas dan periksa lagi.

```csharp
//Sekarang atur properti IsExcel2003Compatible menjadi false dan segarkan lagi
pivotTable.IsExcel2003Compatible = false;
pivotTable.RefreshData();
pivotTable.CalculateData();
```

Ini memungkinkan data Anda mencerminkan panjang aslinya tanpa batasan sebelumnya.

## Langkah 11: Verifikasi Panjangnya Lagi 

Mari kita verifikasi bahwa data sekarang secara akurat mencerminkan panjang sebenarnya.

```csharp
// Sekarang akan mencetak panjang asli data sel. Data tersebut belum terpotong sekarang.
b5 = pivotSheet.Cells["B5"];
Console.WriteLine("Length of cell B5 after setting IsExcel2003Compatible property to False: " + b5.StringValue.Length);
```

Anda akan melihat bahwa output mengonfirmasi penghapusan pemotongan.

## Langkah 12: Format Sel

Untuk meningkatkan pengalaman visual, Anda mungkin ingin memformat sel. 

```csharp
// Atur tinggi baris dan lebar kolom sel B5 dan juga bungkus teksnya
pivotSheet.Cells.SetRowHeight(b5.Row, 100);
pivotSheet.Cells.SetColumnWidth(b5.Column, 65);
Style st = b5.GetStyle();
st.IsTextWrapped = true;
b5.SetStyle(st);
```

Baris kode ini membuat data lebih mudah dibaca dengan menyesuaikan dimensi sel dan mengaktifkan pembungkusan teks.

## Langkah 13: Simpan Buku Kerja

Terakhir, simpan buku kerja Anda dengan perubahan yang telah Anda buat.

```csharp
// Simpan buku kerja dalam format xlsx
wb.Save(dataDir + "SpecifyCompatibility_out.xlsx", SaveFormat.Xlsx);
```

 Memilih format file yang tepat sangat penting saat menyimpan file Excel.`Xlsx`Format ini digunakan secara luas dan kompatibel dengan banyak versi Excel.

## Kesimpulan

Selamat! Anda kini telah memprogram pengaturan kompatibilitas file Excel menggunakan Aspose.Cells untuk .NET. Tutorial ini menguraikan setiap langkah, mulai dari menyiapkan lingkungan hingga mengubah pengaturan kompatibilitas untuk tabel pivot. Jika Anda pernah bekerja dengan data yang memerlukan batasan atau kompatibilitas tertentu, ini adalah keterampilan yang tidak boleh Anda abaikan.

## Pertanyaan yang Sering Diajukan

### Apa itu Aspose.Cells?  
Aspose.Cells adalah pustaka .NET yang dirancang untuk membantu pengembang membuat, memanipulasi, dan mengonversi file Excel dengan mudah.

### Mengapa kompatibilitas Excel penting?  
Kompatibilitas Excel sangat penting untuk memastikan bahwa file dapat dibuka dan digunakan dalam versi Excel yang dimaksud, terutama jika file tersebut berisi fitur atau format yang tidak didukung dalam versi sebelumnya.

### Bisakah saya membuat Tabel Pivot secara terprogram dengan Aspose.Cells?  
Ya, Anda dapat membuat dan memanipulasi Tabel Pivot secara terprogram menggunakan Aspose.Cells. Pustaka ini menyediakan berbagai metode untuk menambahkan sumber data, kolom, dan fitur yang terkait dengan Tabel Pivot.

### Bagaimana cara memeriksa panjang string dalam sel Excel?  
Anda dapat menggunakan`StringValue` milik suatu`Cell` objek untuk mendapatkan isi sel dan kemudian memanggil`.Length` properti untuk mengetahui panjang string.

### Dapatkah saya menyesuaikan pemformatan sel melampaui tinggi dan lebar baris?  
 Tentu saja! Aspose.Cells memungkinkan pemformatan sel yang ekstensif. Anda dapat mengubah gaya font, warna, batas, format angka, dan banyak lagi melalui`Style` kelas.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
