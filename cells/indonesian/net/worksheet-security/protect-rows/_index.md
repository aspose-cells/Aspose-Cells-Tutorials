---
title: Melindungi Baris dalam Lembar Kerja menggunakan Aspose.Cells
linktitle: Melindungi Baris dalam Lembar Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara melindungi baris dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Amankan data Anda dengan perlindungan tingkat baris dan cegah perubahan yang tidak disengaja.
weight: 18
url: /id/net/worksheet-security/protect-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Melindungi Baris dalam Lembar Kerja menggunakan Aspose.Cells

## Perkenalan
Bekerja dengan file Excel secara terprogram sering kali merupakan tugas yang tidak hanya memerlukan manipulasi data tetapi juga perlindungan data. Apakah Anda perlu melindungi data sensitif atau mencegah penyuntingan yang tidak disengaja, melindungi baris dalam lembar kerja dapat menjadi langkah penting. Dalam tutorial ini, kita akan membahas cara melindungi baris tertentu dalam lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Kita akan membahas semua langkah yang diperlukan, mulai dari menyiapkan lingkungan Anda hingga menerapkan fitur perlindungan dengan cara yang sederhana dan mudah diikuti.
## Prasyarat
Sebelum Anda dapat mulai melindungi baris dalam lembar kerja, ada beberapa hal yang perlu Anda siapkan:
1.  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal Aspose.Cells untuk .NET di mesin pengembangan Anda. Jika Anda belum melakukannya, Anda dapat mengunduhnya dengan mudah dari[Halaman unduhan Aspose Cells](https://releases.aspose.com/cells/net/).
2. Visual Studio atau IDE .NET apa pun: Untuk menerapkan solusi, Anda perlu menyiapkan lingkungan pengembangan. Visual Studio adalah pilihan yang bagus, tetapi IDE apa pun yang kompatibel dengan .NET juga dapat digunakan.
3. Pengetahuan Dasar C#: Memahami dasar-dasar pemrograman C# akan membantu Anda mengikuti tutorial dan memodifikasi kode contoh agar sesuai dengan kebutuhan Anda.
4.  Dokumentasi API Aspose.Cells: Biasakan diri Anda dengan[Dokumentasi Aspose.Cells untuk .NET](https://reference.aspose.com/cells/net/) untuk mendapatkan gambaran umum tentang struktur kelas dan metode yang digunakan di perpustakaan.
Jika Anda sudah menyiapkan prasyaratnya, kita dapat langsung masuk ke implementasinya.
## Paket Impor
Untuk memulai, Anda perlu mengimpor paket-paket yang diperlukan. Pustaka-pustaka ini penting untuk berinteraksi dengan berkas Excel dalam proyek C# Anda.
```csharp
using System.IO;
using Aspose.Cells;
```
Setelah Anda mengimpor paket yang diperlukan, Anda dapat mulai membuat kode. 
Sekarang, mari kita bagi prosesnya menjadi beberapa langkah yang lebih kecil agar lebih mudah diikuti. Setiap langkah akan berfokus pada bagian tertentu dari penerapan, memastikan Anda dapat memahami dan menerapkannya dengan cepat. 
## Langkah 1: Buat Buku Kerja dan Lembar Kerja Baru
Sebelum Anda dapat menerapkan pengaturan proteksi, Anda perlu membuat buku kerja baru dan memilih lembar kerja yang ingin Anda gunakan. Ini akan menjadi dokumen kerja Anda.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Buat buku kerja baru.
Workbook wb = new Workbook();
// Buat objek lembar kerja dan dapatkan lembar pertama.
Worksheet sheet = wb.Worksheets[0];
```
Dalam contoh ini, kami membuat buku kerja baru dengan satu lembar kerja (yang merupakan pengaturan default saat Anda membuat buku kerja baru menggunakan Aspose.Cells). Kami kemudian mengambil lembar kerja pertama dalam buku kerja, yang akan menjadi target untuk perlindungan baris kami.
## Langkah 2: Tentukan Objek Style dan StyleFlag
Langkah selanjutnya adalah mendefinisikan objek style dan style flag. Objek-objek ini memungkinkan Anda untuk mengubah properti sel, seperti apakah sel terkunci atau tidak terkunci.
```csharp
// Tentukan objek gaya.
Style style;
// Tentukan objek styleflag.
StyleFlag flag;
```
Anda akan menggunakan objek ini pada langkah selanjutnya untuk menyesuaikan properti sel dan menerapkannya ke lembar kerja Anda.
## Langkah 3: Buka Kunci Semua Kolom di Lembar Kerja
Secara default, semua sel dalam lembar kerja Excel terkunci. Namun, saat Anda melindungi lembar kerja, status terkunci akan diberlakukan. Untuk memastikan bahwa hanya baris atau sel tertentu yang dilindungi, Anda dapat membuka kunci semua kolom terlebih dahulu. Langkah ini penting jika Anda ingin melindungi hanya baris tertentu.
```csharp
// Ulangi semua kolom pada lembar kerja dan buka kuncinya.
for (int i = 0; i <= 255; i++)
{
    style = sheet.Cells.Columns[(byte)i].Style;
    style.IsLocked = false;
    flag = new StyleFlag();
    flag.Locked = true;
    sheet.Cells.Columns[(byte)i].ApplyStyle(style, flag);
}
```
 Dalam kode ini, kita mengulang semua 256 kolom di lembar kerja (lembar kerja Excel memiliki maksimal 256 kolom, diindeks dari 0 hingga 255) dan mengaturnya`IsLocked` properti untuk`false`Tindakan ini memastikan bahwa semua kolom tidak terkunci, tetapi kami akan tetap mengunci baris tertentu nanti.
## Langkah 4: Kunci Baris Pertama
Setelah Anda membuka kunci kolom, langkah berikutnya adalah mengunci baris tertentu yang ingin Anda lindungi. Dalam contoh ini, kita akan mengunci baris pertama. Ini memastikan bahwa pengguna tidak dapat mengubahnya sementara baris lainnya dibiarkan tidak terkunci.
```csharp
//Dapatkan gaya baris pertama.
style = sheet.Cells.Rows[0].Style;
// Kunci itu.
style.IsLocked = true;
//Buatlah contoh bendera.
flag = new StyleFlag();
// Atur pengaturan kunci.
flag.Locked = true;
// Terapkan gaya ke baris pertama.
sheet.Cells.ApplyRowStyle(0, style, flag);
```
Di sini, kita mengakses gaya baris pertama dan mengaturnya`IsLocked` properti untuk`true` Setelah itu kita menggunakan`ApplyRowStyle()` metode untuk menerapkan gaya kunci ke seluruh baris. Anda dapat mengulangi langkah ini untuk mengunci baris lain yang ingin Anda lindungi.
## Langkah 5: Lindungi Lembaran
Setelah kita membuka dan mengunci baris yang diperlukan, saatnya untuk melindungi lembar kerja. Perlindungan ini memastikan bahwa tidak seorang pun dapat mengubah baris atau sel yang terkunci kecuali mereka menghapus kata sandi perlindungan (jika tersedia).
```csharp
// Lindungi lembaran itu.
sheet.Protect(ProtectionType.All);
```
 Pada langkah ini, kami menerapkan perlindungan ke seluruh lembar menggunakan`ProtectionType.All`Jenis perlindungan ini berarti semua aspek lembar, termasuk baris dan sel yang terkunci, dilindungi. Anda juga dapat menyesuaikan perlindungan ini dengan menentukan jenis perlindungan yang berbeda jika diperlukan.
## Langkah 6: Simpan Buku Kerja
Terakhir, kita perlu menyimpan buku kerja setelah menerapkan gaya dan proteksi yang diperlukan. Buku kerja dapat disimpan dalam berbagai format, seperti Excel 97-2003, Excel 2010, dst.
```csharp
// Simpan berkas Excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Baris kode ini menyimpan buku kerja dalam format Excel 97-2003 dengan perubahan yang diterapkan. Anda dapat mengubah format file sesuai kebutuhan Anda dengan memilih dari berbagai`SaveFormat` pilihan.
## Kesimpulan
Nah, itu dia! Anda telah berhasil mempelajari cara melindungi baris dalam lembar kerja menggunakan Aspose.Cells for .NET. Dengan mengikuti langkah-langkah di atas, Anda dapat membuka atau mengunci baris atau kolom sesuai kebutuhan, dan menerapkan perlindungan untuk memastikan integritas data Anda.
## Pertanyaan yang Sering Diajukan
### Bagaimana saya bisa melindungi beberapa baris sekaligus?  
 Anda dapat melakukan pengulangan melalui beberapa baris dan menerapkan gaya penguncian ke setiap baris secara individual. Cukup ganti`0` dengan indeks baris yang ingin Anda kunci.
### Bisakah saya mengatur kata sandi untuk perlindungan lembar?  
 Ya! Anda dapat memberikan kata sandi ke`sheet.Protect()` metode untuk menegakkan perlindungan kata sandi.
### Bisakah saya membuka kunci sel dan bukan seluruh kolom?  
Ya! Daripada membuka kolom, Anda dapat membuka sel individual dengan memodifikasi properti gayanya.
### Apa yang terjadi jika saya mencoba mengedit baris yang dilindungi?  
Bila suatu baris diproteksi, Excel akan mencegah dilakukannya penyuntingan apa pun terhadap sel yang terkunci kecuali Anda membuka proteksi pada lembar tersebut.
### Bisakah saya melindungi rentang tertentu dalam satu baris?  
 Ya! Anda dapat mengunci rentang individual dalam satu baris dengan mengatur`IsLocked` properti untuk sel tertentu dalam rentang.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
