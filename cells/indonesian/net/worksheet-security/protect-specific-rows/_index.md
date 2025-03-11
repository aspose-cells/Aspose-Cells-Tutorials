---
title: Melindungi Baris Tertentu dalam Lembar Kerja menggunakan Aspose.Cells
linktitle: Melindungi Baris Tertentu dalam Lembar Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara melindungi baris tertentu dalam lembar kerja Excel menggunakan Aspose.Cells for .NET dengan panduan langkah demi langkah ini. Amankan data Anda secara efektif.
weight: 16
url: /id/net/worksheet-security/protect-specific-rows/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Melindungi Baris Tertentu dalam Lembar Kerja menggunakan Aspose.Cells

## Perkenalan
Dalam tutorial ini, kami akan memandu Anda melalui proses melindungi baris tertentu dalam lembar kerja Excel menggunakan Aspose.Cells for .NET. Kami akan membahas setiap langkah secara terperinci, meliputi prasyarat, mengimpor paket yang diperlukan, dan menguraikan kode menjadi instruksi yang mudah diikuti. Pada akhirnya, Anda akan dibekali dengan pengetahuan untuk menerapkan perlindungan baris dalam aplikasi Anda sendiri.
## Prasyarat
Sebelum terjun ke implementasi, ada beberapa prasyarat yang perlu Anda penuhi untuk mengikuti tutorial ini:
1. Aspose.Cells untuk .NET: Anda harus menginstal Aspose.Cells untuk .NET. Jika Anda belum menginstalnya, Anda bisa mendapatkan versi terbaru dengan mengunjungi situs web Aspose.
2. Pemahaman Dasar tentang C# dan .NET: Tutorial ini mengasumsikan bahwa Anda sudah familier dengan C# dan memiliki pengetahuan dasar tentang pemrograman .NET. Jika Anda belum familier dengan keduanya, sebaiknya Anda membaca beberapa sumber pengantar terlebih dahulu.
3. Visual Studio atau IDE .NET apa pun: Anda memerlukan lingkungan pengembangan terpadu (IDE) seperti Visual Studio untuk menjalankan kode. Ini menyediakan semua alat dan kemampuan debugging yang diperlukan.
4. Lisensi Aspose.Cells: Jika Anda ingin menghindari batasan versi evaluasi, pastikan Anda memiliki lisensi Aspose.Cells yang valid. Anda juga dapat menggunakan lisensi sementara jika Anda baru memulai.
 Untuk informasi lebih rinci tentang Aspose.Cells dan instalasinya, Anda dapat memeriksa[dokumentasi](https://reference.aspose.com/cells/net/).
## Paket Impor
Untuk mulai menggunakan Aspose.Cells, Anda perlu mengimpor namespace yang diperlukan dalam proyek C# Anda. Namespace ini memberi Anda akses ke kelas dan metode yang diperlukan untuk memanipulasi file Excel.
Berikut cara mengimpor namespace yang diperlukan:
```csharp
using System.IO;
using Aspose.Cells;
```
Impor ini penting karena menyediakan akses ke fungsionalitas Aspose.Cells dan memungkinkan Anda berinteraksi dengan file Excel di proyek .NET Anda.
Setelah Anda menyiapkan prasyarat dan melakukan impor yang diperlukan, saatnya untuk mulai menggunakan kode yang sebenarnya. Kami akan membagi proses ini menjadi beberapa langkah untuk memastikan kejelasan.
## Langkah 1: Siapkan Direktori Proyek Anda
Dalam program apa pun, mengatur berkas adalah kuncinya. Pertama, mari buat direktori tempat kita dapat menyimpan buku kerja. Kita periksa apakah direktori tersebut ada dan buat jika perlu.
```csharp
// Tentukan jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
// Buat direktori jika belum ada.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Di sini, Anda menentukan jalur tempat file Excel akan disimpan. Jika folder tersebut tidak ada, kami akan membuatnya. Langkah ini penting untuk memastikan buku kerja Anda memiliki tempat untuk menyimpan.
## Langkah 2: Buat Buku Kerja Baru
 Selanjutnya kita membuat workbook baru dengan menggunakan`Workbook` Kelas ini menyediakan semua fungsi yang dibutuhkan untuk bekerja dengan file Excel.
```csharp
// Buat buku kerja baru.
Workbook wb = new Workbook();
```
Pada titik ini, kita sekarang memiliki buku kerja baru untuk digunakan.
## Langkah 3: Akses Lembar Kerja
Sekarang kita mengakses lembar kerja pertama dari buku kerja yang baru dibuat. Sebuah buku kerja dapat berisi beberapa lembar kerja, tetapi dalam kasus ini, kita akan fokus pada lembar kerja pertama.
```csharp
// Buat objek lembar kerja dan dapatkan lembar pertama.
Worksheet sheet = wb.Worksheets[0];
```
 Di Sini,`Worksheets[0]` merujuk pada lembar kerja pertama dalam buku kerja (yang diindeks mulai dari 0).
## Langkah 4: Buka Kunci Semua Kolom
Di Excel, sel dikunci secara default saat lembar diproteksi. Jika Anda ingin memproteksi baris tertentu, Anda harus membuka kunci kolom terlebih dahulu. Pada langkah ini, kita akan mengulang semua kolom dan membuka kuncinya.
```csharp
// Tentukan objek gaya.
Style style;
// Tentukan objek styleflag.
StyleFlag flag;
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
Di sini, kita menelusuri kolom 0 hingga 255 (jumlah total kolom dalam lembar kerja Excel) dan membukanya. Ini memastikan bahwa baris yang ingin kita lindungi masih dapat berinteraksi, sementara yang lain tetap terkunci.
## Langkah 5: Kunci Baris Pertama
Sekarang setelah semua kolom tidak terkunci, kita dapat melanjutkan untuk melindungi baris. Pada langkah ini, kita mengunci baris pertama, yang akan membuatnya tidak dapat diedit setelah lembar tersebut dilindungi.
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
Kode ini mengunci baris pertama, memastikannya tetap terlindungi setelah kita menerapkan perlindungan pada lembar tersebut.
## Langkah 6: Lindungi Lembar Kerja
Pada titik ini, kita siap untuk melindungi lembar kerja. Langkah ini menerapkan pengaturan perlindungan ke seluruh lembar kerja, memastikan bahwa sel yang terkunci tidak dapat diedit.
```csharp
// Lindungi lembaran itu.
sheet.Protect(ProtectionType.All);
```
 Dengan menggunakan`ProtectionType.All`kami memastikan bahwa semua sel, kecuali yang tidak terkunci secara eksplisit (seperti kolom kami), terlindungi. Ini adalah langkah yang menerapkan perlindungan pada lembar kerja.
## Langkah 7: Simpan File Excel
Terakhir, setelah menerapkan proteksi, kita simpan buku kerja tersebut. Anda dapat menentukan format penyimpanan file tersebut. Dalam contoh ini, kita simpan buku kerja sebagai file Excel 97-2003.
```csharp
// Simpan berkas excel.
wb.Save(dataDir + "output.out.xls", SaveFormat.Excel97To2003);
```
Langkah ini menyimpan berkas ke jalur yang ditentukan, menyelesaikan tugas melindungi baris tertentu dalam lembar kerja.
## Kesimpulan
Melindungi baris tertentu dalam lembar kerja Excel menggunakan Aspose.Cells for .NET merupakan proses yang mudah setelah Anda menguraikannya langkah demi langkah. Dengan membuka kunci kolom, mengunci baris tertentu, dan menerapkan pengaturan perlindungan, Anda memastikan bahwa data Anda tetap aman dan hanya dapat diedit jika diperlukan. Tutorial ini mencakup semua langkah utama, mulai dari menyiapkan direktori proyek hingga menyimpan buku kerja akhir.
Baik Anda membuat templat, laporan, atau lembar kerja interaktif, menggunakan proteksi baris adalah cara yang sederhana namun efektif untuk mempertahankan kendali atas data Anda. Cobalah proses ini dalam proyek Anda sendiri dan jelajahi potensi penuh Aspose.Cells untuk .NET.
## Pertanyaan yang Sering Diajukan
### Bisakah saya melindungi beberapa baris dalam lembar kerja?  
Ya, Anda dapat menerapkan langkah perlindungan yang sama ke beberapa baris dengan memodifikasi loop atau menerapkan gaya ke baris lainnya.
### Apa yang terjadi jika saya tidak membuka kunci kolom apa pun sebelum melindungi lembar tersebut?  
Jika Anda tidak membuka kunci kolom, kolom tersebut akan terkunci saat lembar dilindungi, dan pengguna tidak akan dapat berinteraksi dengannya.
### Bagaimana saya bisa membuka kunci sel tertentu, bukan seluruh kolom?  
 Anda dapat membuka sel tertentu dengan mengakses gayanya dan mengaturnya`IsLocked` properti untuk`false`.
### Bisakah saya menggunakan metode ini untuk melindungi seluruh lembar kerja?  
Ya, Anda dapat melindungi seluruh lembar kerja dengan menerapkan perlindungan ke semua sel dan tidak membiarkan satu sel pun tidak terkunci.
### Bagaimana cara membuka proteksi lembar kerja?  
 Anda dapat menghapus perlindungan dengan menelepon`Unprotect`metode pada lembar kerja dan memberikan kata sandi proteksi (jika ada).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
