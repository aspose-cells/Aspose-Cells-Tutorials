---
title: Menyisipkan Gambar dengan Penanda Gambar di Aspose.Cells
linktitle: Menyisipkan Gambar dengan Penanda Gambar di Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Temukan cara menyisipkan gambar menggunakan penanda gambar di Aspose.Cells untuk .NET dengan panduan langkah demi langkah kami! Sempurnakan laporan Excel Anda dengan visual secara efektif.
weight: 16
url: /id/net/smart-markers-dynamic-data/insert-images-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Menyisipkan Gambar dengan Penanda Gambar di Aspose.Cells

## Perkenalan
Apakah Anda ingin membumbui lembar kerja Excel Anda dengan beberapa gambar? Mungkin Anda ingin membuat laporan dinamis yang menyertakan gambar langsung dari sumber data Anda? Jika demikian, Anda berada di tempat yang tepat! Dalam panduan ini, kami akan memandu Anda melalui proses penyisipan gambar menggunakan penanda gambar di pustaka Aspose.Cells untuk .NET. Tutorial ini sangat cocok untuk pengembang .NET yang ingin menyempurnakan laporan Excel mereka dan meningkatkan keterlibatan pengguna secara keseluruhan.
## Prasyarat
Sebelum menyelami seluk-beluk pengkodean, penting untuk memastikan Anda telah menyiapkan beberapa hal:
1. Lingkungan .NET: Miliki lingkungan pengembangan .NET yang berfungsi. Anda dapat menggunakan Visual Studio atau IDE .NET lain pilihan Anda.
2.  Pustaka Aspose.Cells untuk .NET: Anda harus mengunduh dan memiliki akses ke pustaka Aspose.Cells. Anda bisa mendapatkan versi terbaru[Di Sini](https://releases.aspose.com/cells/net/).
3. Gambar yang Diperlukan: Pastikan Anda memiliki gambar yang ingin Anda gunakan yang tersimpan di direktori proyek Anda.
4. Pemahaman Dasar tentang C#: Pemahaman dasar tentang C# dan bekerja dengan DataTables akan membantu Anda mengikutinya dengan lancar.
Sekarang setelah kita menyiapkan semuanya, mari kita mulai dengan mengimpor paket yang diperlukan!
## Paket Impor
Sebelum kita menjalankan fungsi apa pun, kita perlu mengimpor namespace penting. Dalam berkas C# Anda, pastikan Anda telah menyertakan yang berikut ini:
```csharp
using System.IO;
using Aspose.Cells;
using System.Data;
```
Ruang nama ini akan memberi Anda kelas dan fungsi untuk memanipulasi file Excel dan menangani tabel data.
Sekarang, mari kita uraikan proses penyisipan gambar menggunakan Aspose.Cells menjadi beberapa langkah sederhana. Kita akan membahas langkah-langkah yang diperlukan untuk menyiapkan tabel data, memuat gambar, dan menyimpan berkas Excel akhir.
## Langkah 1: Tentukan Direktori Dokumen Anda
Pertama-tama, Anda perlu menentukan direktori dokumen tempat gambar dan berkas templat berada. Direktori ini akan berfungsi sebagai jalur dasar untuk semua operasi berkas Anda.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory"; // Ubah ini ke direktori Anda yang sebenarnya
```
 Mengganti`"Your Document Directory"` dengan jalur tempat gambar dan berkas templat Anda disimpan. Ini bisa berupa jalur relatif atau absolut.
## Langkah 2: Muat Gambar Anda ke dalam Array Byte
Selanjutnya, kita akan membaca gambar yang ingin Anda masukkan ke dalam berkas Excel. Anda perlu membuat DataTable yang menyimpan data gambar.
```csharp
// Dapatkan data gambar.
byte[] imageData = File.ReadAllBytes(dataDir + "aspose-logo.jpg");
```
 Itu`File.ReadAllBytes()` Metode ini digunakan untuk membaca berkas gambar ke dalam array byte. Anda dapat melakukannya untuk beberapa gambar dengan mengulang proses untuk setiap berkas.
## Langkah 3: Buat DataTable untuk Menampung Gambar
Sekarang kita akan membuat DataTable. Tabel ini akan memungkinkan kita untuk menyimpan data gambar secara terstruktur.
```csharp
// Membuat tabel data.
DataTable t = new DataTable("Table1");
// Tambahkan kolom untuk menyimpan gambar.
DataColumn dc = t.Columns.Add("Picture");
// Tetapkan tipe datanya.
dc.DataType = typeof(object);
```
 Di sini, kita membuat DataTable baru yang disebut "Table1" dan menambahkan kolom bernama "Gambar." Tipe data untuk kolom ini diatur ke`object`, yang diperlukan untuk menyimpan array byte.
## Langkah 4: Tambahkan Rekaman Gambar ke DataTable
Setelah DataTable disiapkan, kita dapat mulai menambahkan gambar ke dalamnya.
```csharp
// Tambahkan rekaman baru ke dalamnya.
DataRow row = t.NewRow();
row[0] = imageData;
t.Rows.Add(row);
// Tambahkan rekaman lain (yang berisi gambar) ke dalamnya.
imageData = File.ReadAllBytes(dataDir + "image2.jpg");
row = t.NewRow();
row[0] = imageData;
t.Rows.Add(row);
```
 Buat baris baru untuk setiap gambar dan tetapkan nilai kolom pertama ke data gambar. Gunakan`t.Rows.Add(row)` untuk menambahkan baris ke DataTable. Beginilah cara Anda membangun koleksi gambar secara dinamis.
## Langkah 5: Buat Objek WorkbookDesigner
 Selanjutnya, saatnya untuk membuat`WorkbookDesigner` objek, yang akan digunakan untuk memproses templat Excel.
```csharp
// Buat objek WorkbookDesigner.
WorkbookDesigner designer = new WorkbookDesigner();
```
 Itu`WorkbookDesigner`Kelas ini memungkinkan Anda bekerja lebih fleksibel dengan berkas Excel Anda dengan membantu merancang laporan kompleks menggunakan templat.
## Langkah 6: Buka File Excel Template Anda
 Anda harus memuat file templat Excel Anda ke dalam`WorkbookDesigner`Berfungsi sebagai dasar tempat penanda gambar Anda akan diproses.
```csharp
// Buka berkas Excel templat.
designer.Workbook = new Workbook(dataDir + "TestSmartMarkers.xlsx");
```
 Mengganti`"TestSmartMarkers.xlsx"` dengan nama templat Anda yang sebenarnya. Berkas ini harus berisi placeholder yang dikenal sebagai smart marker, yang memberi tahu Aspose.Cells tempat meletakkan data gambar.
## Langkah 7: Tetapkan Sumber Data untuk WorkbookDesigner Anda
Setelah membuka buku kerja, langkah berikutnya adalah menghubungkan DataTable Anda ke WorkbookDesigner.
```csharp
// Tetapkan sumber data.
designer.SetDataSource(t);
```
Baris ini memberi tahu desainer untuk menggunakan DataTable yang Anda buat sebagai sumber data. Baris ini membuat tautan antara data gambar dan templat.
## Langkah 8: Proses Penanda di Template Anda
Sekarang saatnya membiarkan keajaiban terjadi! Kami akan memproses penanda dalam templat, yang akan mengganti placeholder dengan data gambar sebenarnya.
```csharp
// Memproses penanda.
designer.Process();
```
 Itu`Process()` metode memindai templat untuk penanda pintar dan mengisinya menggunakan data dari DataTable.
## Langkah 9: Simpan File Excel Akhir
Langkah terakhir, tentu saja, menyimpan berkas Excel yang baru dibuat beserta gambar yang disertakan. Mari kita lakukan sekarang!
```csharp
// Simpan berkas Excel.
designer.Workbook.Save(dataDir + "output.xls");
```
Anda dapat memilih format yang Anda inginkan untuk berkas yang disimpan. Dalam kasus ini, kami menyimpannya sebagai "output.xls." Ubah nama berkas sesuai kebutuhan Anda.
## Kesimpulan
Nah, itu dia! Panduan yang disederhanakan untuk memasukkan gambar ke dalam lembar kerja Excel menggunakan Aspose.Cells dengan bantuan penanda gambar. Fitur ini sangat berguna untuk membuat laporan dinamis yang menyertakan gambar berdasarkan sumber data Anda. Baik Anda mengerjakan analisis bisnis atau materi pendidikan, metode ini dapat meningkatkan presentasi dokumen Anda secara signifikan.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka hebat untuk .NET yang memungkinkan pengguna membuat, memanipulasi, dan mengonversi file Excel secara terprogram.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
Ya! Anda bisa mendapatkan versi uji coba gratis Aspose.Cells[Di Sini](https://releases.aspose.com/).
### Di mana saya dapat mempelajari lebih lanjut tentang penggunaan Aspose.Cells?
 Anda bisa menyelami[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk panduan dan sumber daya yang lengkap.
### Apakah saya memerlukan lisensi untuk menerapkan Aspose.Cells dengan aplikasi saya?
 Ya, untuk penggunaan produksi, Anda memerlukan lisensi. Anda dapat memperoleh lisensi sementara[Di Sini](https://purchase.aspose.com/temporary-license/).
### Bagaimana cara mendapatkan dukungan teknis untuk Aspose.Cells?
 Untuk pertanyaan teknis, Anda dapat mengunjungi[Forum Dukungan Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
