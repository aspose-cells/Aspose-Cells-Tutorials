---
title: Tambahkan Kotak Kombo ke Lembar Kerja di Excel
linktitle: Tambahkan Kotak Kombo ke Lembar Kerja di Excel
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menambahkan kotak kombo ke lembar kerja Excel secara terprogram menggunakan Aspose.Cells for .NET. Panduan langkah demi langkah ini memandu Anda melalui setiap detail.
weight: 21
url: /id/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Kotak Kombo ke Lembar Kerja di Excel

## Perkenalan
Membuat lembar kerja Excel yang interaktif dapat meningkatkan pengalaman pengguna secara signifikan, terutama saat Anda menambahkan elemen formulir seperti kotak kombo. Kotak kombo memungkinkan pengguna untuk memilih opsi dari daftar yang telah ditetapkan, sehingga memudahkan dan mengefisienkan input data. Dengan Aspose.Cells for .NET, Anda dapat membuat kotak kombo secara terprogram di lembar Excel tanpa menggunakan Excel secara langsung. Pustaka yang canggih ini memungkinkan pengembang untuk memanipulasi file Excel dengan berbagai cara, termasuk kemampuan untuk mengotomatiskan kontrol formulir.
Dalam tutorial ini, kami akan memandu Anda melalui proses penambahan kotak kombo ke lembar kerja di Excel menggunakan Aspose.Cells for .NET. Jika Anda ingin membuat lembar kerja yang dinamis dan mudah digunakan, panduan ini akan membantu Anda memulai.
## Prasyarat
Sebelum kita masuk ke kode, mari pastikan Anda memiliki semua yang Anda butuhkan:
- Aspose.Cells untuk .NET: Unduh dan instal pustaka Aspose.Cells untuk .NET dari[halaman unduhan](https://releases.aspose.com/cells/net/).
- .NET Framework: Pastikan Anda telah menginstal .NET Framework di komputer Anda. Versi apa pun yang didukung oleh Aspose.Cells dapat digunakan.
- Lingkungan Pengembangan: Gunakan IDE seperti Visual Studio untuk mengelola proyek Anda dan menulis kode.
-  Lisensi Aspose: Anda dapat bekerja tanpa lisensi dalam mode evaluasi, tetapi untuk versi lengkap, Anda perlu menerapkan lisensi. Dapatkan lisensi[lisensi sementara](https://purchase.aspose.com/temporary-license/) jika diperlukan.
## Paket Impor
Untuk memulai, Anda perlu mengimpor namespace yang diperlukan ke dalam proyek Anda. Berikut ini yang Anda perlukan:
```csharp
using System.IO;
using Aspose.Cells;
```
Ini penting untuk berinteraksi dengan file Excel dan memanipulasi elemen formulir seperti kotak kombo dalam buku kerja.
Mari kita uraikan proses penambahan kotak kombo menjadi beberapa langkah sederhana agar mudah dipahami.
## Langkah 1: Siapkan Direktori Dokumen
Langkah pertama adalah membuat direktori tempat file Excel Anda akan disimpan. Anda dapat membuat folder baru jika belum ada.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Menentukan lokasi penyimpanan berkas keluaran.
- System.IO.Directory.Exists: Memeriksa apakah direktori sudah ada.
- System.IO.Directory.CreateDirectory: Membuat direktori jika hilang.
## Langkah 2: Buat Buku Kerja Baru
Sekarang, buat buku kerja Excel baru tempat Anda akan menambahkan kotak kombo.

```csharp
// Buat Buku Kerja baru.
Workbook workbook = new Workbook();
```

- Buku kerja buku kerja: Menginisialisasi contoh baru kelas Buku Kerja, yang merepresentasikan berkas Excel.
## Langkah 3: Dapatkan Lembar Kerja dan Sel
Berikutnya, akses lembar kerja pertama dari buku kerja dan ambil kumpulan sel tempat Anda akan memasukkan data.

```csharp
// Dapatkan lembar kerja pertama.
Worksheet sheet = workbook.Worksheets[0];
// Dapatkan koleksi sel lembar kerja.
Cells cells = sheet.Cells;
```

- Lembar kerja: Mengambil lembar kerja pertama dari buku kerja.
- Sel sel: Mendapatkan kumpulan sel dari lembar kerja.
## Langkah 4: Masukkan Nilai untuk Kotak Kombo
Sekarang, kita perlu memasukkan beberapa nilai ke dalam sel. Nilai-nilai ini akan berfungsi sebagai opsi untuk kotak kombo.

```csharp
// Masukkan nilai.
cells["B3"].PutValue("Employee:");
// Tebalkan.
cells["B3"].GetStyle().Font.IsBold = true;
// Masukkan beberapa nilai yang menunjukkan rentang input untuk kotak kombo.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- sel["B3"].PutValue: Menempatkan label "Karyawan" di sel B3.
- Font.IsBold = true: Mengatur teks menjadi tebal untuk membuatnya menonjol.
- Rentang masukan: Memasukkan beberapa ID karyawan di sel A2 hingga A7. ID ini akan muncul di kotak dropdown kombo.
## Langkah 5: Tambahkan Kotak Kombo ke Lembar Kerja
Langkah selanjutnya adalah menambahkan kontrol kotak kombo ke lembar kerja Anda. Kotak kombo ini akan memungkinkan pengguna memilih salah satu ID karyawan yang Anda masukkan sebelumnya.

```csharp
// Tambahkan kotak kombo baru.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Menambahkan kotak kombo baru ke lembar kerja. Angka (2, 0, 2, 0, 22, 100) mewakili posisi dan dimensi kotak kombo.
## Langkah 6: Hubungkan Kotak Kombo ke Sel dan Atur Rentang Input
Untuk membuat kotak kombo berfungsi, kita perlu menautkannya ke sel tertentu dan menentukan rentang sel tempat opsi akan diambil.

```csharp
// Mengatur sel yang ditautkan.
comboBox.LinkedCell = "A1";
// Mengatur rentang masukan.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Menghubungkan pilihan kotak kombo ke sel A1. Nilai yang dipilih dari kotak kombo akan muncul di sel ini.
- InputRange: Menentukan rentang sel (A2:A7) yang berisi nilai-nilai yang akan mengisi opsi kotak kombo.
## Langkah 7: Sesuaikan Tampilan Kotak Kombo
Anda dapat menyesuaikan kotak kombo lebih lanjut dengan menentukan jumlah baris dropdown dan mengaktifkan bayangan 3D untuk estetika yang lebih baik.

```csharp
// Tetapkan jumlah baris daftar yang ditampilkan di bagian daftar kotak kombo.
comboBox.DropDownLines = 5;
// Atur kotak kombo dengan bayangan 3-D.
comboBox.Shadow = true;
```

- DropDownLines: Mengontrol berapa banyak opsi yang akan terlihat dalam kotak kombo dropdown sekaligus.
- Bayangan: Menambahkan efek bayangan 3D ke kotak kombo.
## Langkah 8: Sesuaikan Kolom Secara Otomatis dan Simpan Buku Kerja
Terakhir, mari sesuaikan kolom secara otomatis untuk tata letak yang bersih dan simpan buku kerja.

```csharp
// Kolom Penyesuaian Otomatis
sheet.AutoFitColumns();
// Menyimpan berkas.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: Secara otomatis menyesuaikan lebar kolom agar sesuai dengan konten.
- Simpan: Menyimpan buku kerja sebagai file Excel di direktori yang ditentukan.

## Kesimpulan
Menambahkan kotak kombo ke lembar kerja Excel Anda menggunakan Aspose.Cells untuk .NET merupakan proses mudah yang sangat meningkatkan fleksibilitas input data. Dengan membuat kontrol formulir secara terprogram, Anda dapat membuat lembar kerja interaktif dengan mudah. Tutorial ini menunjukkan kepada Anda cara menambahkan kotak kombo, menautkannya ke sel, dan mengonfigurasi rentang inputnya, semuanya menggunakan Aspose.Cells.
 Aspose.Cells menyediakan berbagai fitur untuk manipulasi file Excel, menjadikannya pilihan ideal bagi pengembang yang ingin mengotomatiskan tugas spreadsheet. Cobalah dengan[uji coba gratis](https://releases.aspose.com/).
## Pertanyaan yang Sering Diajukan
### Bisakah saya menggunakan Aspose.Cells tanpa menginstal Excel?
Ya, Aspose.Cells bekerja secara independen dari Excel dan tidak memerlukan Excel untuk diinstal.
### Bagaimana cara menerapkan lisensi di Aspose.Cells?
 Anda dapat mengajukan lisensi dengan mendapatkannya dari[Di Sini](https://purchase.aspose.com/buy) dan memanggil`License.SetLicense()` dalam kode Anda.
### Format apa yang didukung Aspose.Cells untuk menyimpan file?
Aspose.Cells mendukung penyimpanan file dalam berbagai format seperti XLSX, XLS, CSV, PDF, dan banyak lagi.
### Apakah ada batasan jumlah kotak kombo yang dapat saya tambahkan?
Tidak, tidak ada batasan yang ketat; Anda dapat menambahkan kotak kombo sebanyak yang dibutuhkan proyek Anda.
### Bagaimana cara mendapatkan dukungan untuk Aspose.Cells?
 Anda bisa mendapatkan dukungan dari[Forum Aspose](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
