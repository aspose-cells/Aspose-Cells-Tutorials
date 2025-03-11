---
title: Kelompokkan Data dengan Penanda Cerdas di Aspose.Cells .NET
linktitle: Kelompokkan Data dengan Penanda Cerdas di Aspose.Cells .NET
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Kelompokkan data dengan mudah menggunakan smart marker di Aspose.Cells for .NET. Ikuti panduan lengkap kami untuk petunjuk langkah demi langkah.
weight: 15
url: /id/net/smart-markers-dynamic-data/group-data-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kelompokkan Data dengan Penanda Cerdas di Aspose.Cells .NET

## Perkenalan
Apakah Anda ingin mengelola dan menyajikan data secara efisien di Microsoft Excel? Jika demikian, Anda mungkin menemukan Aspose.Cells for .NET. Alat canggih ini dapat membantu Anda mengotomatiskan tugas Excel sekaligus memungkinkan manipulasi data yang kuat. Salah satu fitur yang sangat berguna adalah penggunaan penanda cerdas. Dalam panduan ini, kami akan menguraikan cara mengelompokkan data menggunakan penanda cerdas di Aspose.Cells for .NET langkah demi langkah. Jadi, ambil minuman favorit Anda, buat diri Anda nyaman, dan mari kita mulai!
## Prasyarat
Sebelum kita mulai membuat kode, pastikan Anda telah menyiapkan semuanya. Anda memerlukan hal berikut:
1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Ini adalah alat terbaik untuk mengembangkan aplikasi .NET.
2.  Aspose.Cells untuk .NET: Unduh dan instal Aspose.Cells dari[Di Sini](https://releases.aspose.com/cells/net/).
3. Contoh Basis Data (Northwind.mdb): Anda memerlukan contoh basis data untuk digunakan. Anda dapat menemukan basis data Northwind secara online dengan mudah.
4. Pemahaman Dasar C#: Panduan ini mengasumsikan Anda memiliki pemahaman dasar tentang pemrograman C#, sehingga Anda dapat mengikutinya tanpa banyak kesulitan.
## Paket Impor
Mari kita mulai dengan mengimpor namespace yang diperlukan. Anda perlu menyertakan yang berikut ini dalam berkas kode Anda:
```csharp
using System.IO;
using Aspose.Cells;
using System.Data;
```
Ruang nama ini akan memberi Anda akses ke kelas-kelas yang Anda perlukan untuk terhubung ke basis data Anda dan memanipulasi berkas Excel.
Sekarang, mari kita uraikan proses pengelompokan data dengan penanda pintar ke dalam langkah-langkah yang mudah diikuti.
## Langkah 1: Tentukan Direktori untuk Dokumen Anda
Pertama-tama, Anda perlu menentukan di mana dokumen Anda akan disimpan. Di sinilah Anda akan mengarahkan sumber data dan berkas keluaran. Berikut cara melakukannya:
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya di komputer Anda tempat basis data dan berkas keluaran Anda berada.
## Langkah 2: Buat Koneksi Basis Data
Selanjutnya, Anda perlu membuat koneksi ke basis data Anda. Ini akan memungkinkan Anda untuk mengkueri data secara efektif. Mari kita aturnya:
```csharp
//Buat objek koneksi, tentukan info penyedia dan tetapkan sumber data.
OleDbConnection con = new OleDbConnection("provider=microsoft.jet.oledb.4.0;data source=" + dataDir + "Northwind.mdb");
```
String koneksi ini menetapkan bahwa kita menggunakan penyedia Jet OLE DB untuk terhubung ke basis data Access.
## Langkah 3: Buka Koneksi
Setelah Anda menentukan koneksi, sekarang saatnya untuk benar-benar membukanya. Berikut cara melakukannya:
```csharp
// Buka objek koneksi.
con.Open();
```
 Dengan menyebut`con.Open()`, Anda membuat koneksi dan bersiap menjalankan perintah Anda.
## Langkah 4: Buat Objek Perintah
Dengan koneksi yang aktif, Anda perlu membuat perintah untuk menjalankan kueri SQL. Perintah ini akan menentukan data apa yang ingin Anda ambil dari basis data Anda.
```csharp
// Buat objek perintah dan tentukan kueri SQL.
OleDbCommand cmd = new OleDbCommand("Select * from [Order Details]", con);
```
 Di sini, kami memilih semua rekaman dari`Order Details` tabel. Anda dapat mengubah kueri ini sesuai kebutuhan untuk memfilter atau mengelompokkan data Anda secara berbeda.
## Langkah 5: Buat Adaptor Data
Selanjutnya, Anda memerlukan adaptor data yang berfungsi sebagai jembatan antara basis data dan kumpulan data. Adaptor ini seperti penerjemah antara dua lingkungan.
```csharp
// Membuat objek adaptor data.
OleDbDataAdapter da = new OleDbDataAdapter();
    
// Tentukan perintahnya.
da.SelectCommand = cmd;
```
## Langkah 6: Buat DataSet
Sekarang, mari kita siapkan kumpulan data untuk menampung data yang diambil. Satu kumpulan data dapat berisi beberapa tabel, yang membuatnya sangat serbaguna.
```csharp
// Membuat objek kumpulan data.
DataSet ds = new DataSet();
    
// Isi dataset dengan catatan tabel.
da.Fill(ds, "Order Details");
```
 Dengan`da.Fill()`, Anda mengisi dataset dengan rekaman dari perintah SQL kami.
## Langkah 7: Buat Objek DataTable
Untuk bekerja dengan data kita secara lebih efektif, kita akan membuat DataTable khusus untuk data 'Detail Pesanan':
```csharp
// Buat tabel data berkenaan dengan tabel kumpulan data.
DataTable dt = ds.Tables["Order Details"];
```
Baris ini mengambil tabel bernama “Detail Pesanan” dari kumpulan data dan membuat DataTable untuk penanganan yang lebih mudah.
## Langkah 8: Inisialisasi WorkbookDesigner
Saatnya menggunakan Aspose.Cells untuk memanipulasi dokumen Excel kita. Kita akan mulai dengan menginisialisasi`WorkbookDesigner`.
```csharp
// Buat objek WorkbookDesigner.
WorkbookDesigner wd = new WorkbookDesigner();
```
## Langkah 9: Buka Template Excel
Untuk mengelola data Anda dengan penanda cerdas, Anda memerlukan file Excel templat. File ini harus berisi penanda cerdas tempat data Anda akan ditempatkan.
```csharp
// Buka berkas templat (yang berisi penanda pintar).
wd.Workbook = new Workbook(dataDir + "Designer.xlsx");
```
 Pastikan Anda memiliki`Designer.xlsx` berkas yang dibuat dengan penanda pintar yang ada sebelum ini.
## Langkah 10: Tetapkan Sumber Data
Sekarang setelah kita membuat buku kerja dan penanda pintar sudah tersedia, kita dapat mengatur sumber data ke DataTable yang kita buat sebelumnya:
```csharp
// Tetapkan datatable sebagai sumber data.
wd.SetDataSource(dt);
```
## Langkah 11: Proses Penanda Cerdas
Langkah ini adalah tempat keajaiban terjadi. Pemrosesan penanda pintar akan mengisi berkas Excel Anda dengan data aktual dari DataTable.
```csharp
// Memproses penanda pintar untuk mengisi data ke dalam lembar kerja.
wd.Process(true);
```
 Lewat`true` ke`wd.Process()`memberi tahu perancang bahwa kita ingin mengganti penanda pintar dengan data kita yang sebenarnya.
## Langkah 12: Simpan File Excel
Terakhir, kita perlu menyimpan berkas Excel yang baru kita buat ke dalam disk. Ini adalah langkah terakhir, dan caranya cukup mudah:
```csharp
// Simpan berkas excel.
wd.Workbook.Save(dataDir + "output.xlsx");
```
Selesai! Anda telah mengelompokkan data Anda menggunakan penanda cerdas Aspose.Cells.
## Kesimpulan
Menggunakan penanda cerdas di Aspose.Cells for .NET merupakan cara yang ampuh untuk mengelola dan memformat data Anda di Excel dengan mudah. Hanya dengan beberapa baris kode, Anda dapat terhubung ke database, mengambil data, dan mengisi dokumen Excel. Baik Anda melakukan ini untuk pelaporan, analisis, atau hanya untuk menjaga semuanya tetap teratur, metode ini dapat menghemat waktu dan mengurangi kerepotan Anda.
## Pertanyaan yang Sering Diajukan
### Apa itu Penanda Cerdas?
Penanda pintar adalah anotasi khusus dalam templat yang dikenali Aspose.Cells untuk diisi dengan data secara dinamis.
### Bisakah saya mengelompokkan data secara berbeda?
Ya! Anda dapat memodifikasi query SQL SELECT untuk melakukan operasi pengelompokan, tergantung pada apa yang Anda butuhkan.
### Di mana saya dapat menemukan dokumentasi Aspose.Cells?
 Anda dapat mengakses dokumentasi[Di Sini](https://reference.aspose.com/cells/net/).
### Apakah ada uji coba gratis yang tersedia untuk Aspose.Cells?
 Tentu saja! Anda dapat mengunduh versi uji coba gratis[Di Sini](https://releases.aspose.com/).
### Bagaimana saya bisa mendapatkan dukungan untuk Aspose.Cells?
Untuk pertanyaan atau masalah apa pun, Anda dapat mengunjungi forum dukungan[Di Sini](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
