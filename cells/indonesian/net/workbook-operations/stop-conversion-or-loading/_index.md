---
title: Hentikan Konversi atau Pemuatan menggunakan Monitor Interupsi
linktitle: Hentikan Konversi atau Pemuatan menggunakan Monitor Interupsi
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menghentikan konversi buku kerja di Aspose.Cells untuk .NET menggunakan Interrupt Monitor, dengan tutorial terperinci langkah demi langkah.
weight: 26
url: /id/net/workbook-operations/stop-conversion-or-loading/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hentikan Konversi atau Pemuatan menggunakan Monitor Interupsi

## Perkenalan
Bekerja dengan file Excel yang besar sering kali melibatkan proses yang panjang yang dapat menghabiskan waktu dan sumber daya. Namun, bagaimana jika Anda dapat menghentikan proses konversi di tengah jalan saat Anda menyadari ada sesuatu yang perlu diubah? Aspose.Cells untuk .NET memiliki fitur yang disebut Interrupt Monitor, yang memungkinkan Anda untuk menghentikan konversi buku kerja ke format lain seperti PDF. Ini dapat menjadi penyelamat, terutama saat bekerja dengan file data yang besar. Dalam panduan ini, kami akan membahas cara menghentikan proses konversi menggunakan Interrupt Monitor di Aspose.Cells untuk .NET.
## Prasyarat
Sebelum memulai, pastikan Anda telah menyiapkan hal-hal berikut:
1.  Aspose.Cells untuk .NET - Unduh[Di Sini](https://releases.aspose.com/cells/net/).
2. Lingkungan Pengembangan .NET - Seperti Visual Studio.
3. Pengetahuan Dasar Pemrograman C# - Keakraban dengan sintaksis C# akan membantu Anda mengikutinya.
## Paket Impor
Untuk memulai, mari impor paket-paket yang diperlukan. Paket-paket impor ini meliputi:
- Aspose.Cells: Pustaka utama untuk memanipulasi file Excel.
- System.Threading: Untuk mengelola thread, karena contoh ini akan menjalankan dua proses paralel.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.IO;
```
Mari kita uraikan prosesnya menjadi beberapa langkah terperinci. Setiap langkah akan membantu Anda memahami pentingnya menyiapkan dan menggunakan Interrupt Monitor untuk mengelola konversi buku kerja Excel.
## Langkah 1: Buat Kelas dan Tetapkan Direktori Output
Pertama, kita perlu sebuah kelas untuk merangkum fungsi-fungsi kita, beserta direktori tempat berkas keluaran akan disimpan.
```csharp
class StopConversionOrLoadingUsingInterruptMonitor
{
    static string outputDir = "Your Document Directory";
}
```
 Mengganti`"Your Document Directory"` dengan jalur sebenarnya tempat Anda ingin menyimpan berkas PDF.
## Langkah 2: Buat Instansi Pemantau Interupsi
Selanjutnya, buat objek InterruptMonitor. Monitor ini akan membantu mengendalikan proses dengan mengatur kemampuan untuk menghentikannya pada titik tertentu.
```csharp
InterruptMonitor im = new InterruptMonitor();
```
Pemantau interupsi ini akan dilampirkan ke buku kerja kita, sehingga memungkinkan kita mengelola proses konversi.
## Langkah 3: Siapkan Buku Kerja untuk Konversi
Sekarang, mari kita membuat objek buku kerja, tetapkan InterruptMonitor padanya, lalu akses lembar kerja pertama untuk menyisipkan beberapa contoh teks.
```csharp
void CreateWorkbookAndConvertItToPdfFormat()
{
    Workbook wb = new Workbook();
    wb.InterruptMonitor = im;
    Worksheet ws = wb.Worksheets[0];
    Cell cell = ws.Cells["J1000000"];
    cell.PutValue("This is text.");
}
```
Kode di atas membuat buku kerja, mengatur InterruptMonitor untuknya, dan menempatkan teks di sel jauh (`J1000000`). Menempatkan teks pada posisi sel ini memastikan bahwa pemrosesan buku kerja akan lebih memakan waktu, sehingga memberikan InterruptMonitor cukup waktu untuk melakukan intervensi.
## Langkah 4: Simpan Buku Kerja sebagai PDF dan Tangani Gangguan
 Sekarang, mari kita coba menyimpan buku kerja sebagai PDF. Kita akan menggunakan`try-catch` blok untuk menangani gangguan apa pun yang mungkin terjadi.
```csharp
try
{
    wb.Save(outputDir + "output_InterruptMonitor.pdf");
}
catch (Aspose.Cells.CellsException ex)
{
    Console.WriteLine("Process Interrupted - Message: " + ex.Message);
}
```
Jika proses terhenti, pengecualian akan mendeteksinya dan menampilkan pesan yang sesuai. Jika tidak, buku kerja akan disimpan sebagai PDF.
## Langkah 5: Hentikan Proses Konversi
 Fitur utama di sini adalah kemampuan untuk menghentikan proses. Kami akan menambahkan penundaan menggunakan`Thread.Sleep` dan kemudian menelepon`Interrupt()` metode untuk menghentikan konversi setelah 10 detik.
```csharp
void WaitForWhileAndThenInterrupt()
{
    Thread.Sleep(1000 * 10);
    im.Interrupt();
}
```
Penundaan ini memberi waktu pada buku kerja untuk mulai mengonversi ke PDF sebelum sinyal interupsi dikirim.
## Langkah 6: Jalankan Thread Secara Bersamaan
Untuk menyatukan semuanya, kita perlu memulai kedua fungsi di thread terpisah. Dengan cara ini, konversi buku kerja dan interupsi tunggu dapat terjadi secara bersamaan.
```csharp
public void TestRun()
{
    ThreadStart ts1 = new ThreadStart(this.CreateWorkbookAndConvertItToPdfFormat);
    Thread t1 = new Thread(ts1);
    t1.Start();
    ThreadStart ts2 = new ThreadStart(this.WaitForWhileAndThenInterrupt);
    Thread t2 = new Thread(ts2);
    t2.Start();
    t1.Join();
    t2.Join();
}
```
 Kode di atas berjalan`CreateWorkbookAndConvertItToPdfFormat` Dan`WaitForWhileAndThenInterrupt` dalam untaian paralel, menggabungkannya setelah kedua proses selesai.
## Langkah 7: Eksekusi Akhir
 Terakhir, kami akan menambahkan`Run()` metode untuk mengeksekusi kode.
```csharp
public static void Run()
{
    new StopConversionOrLoadingUsingInterruptMonitor().TestRun();
    Console.WriteLine("StopConversionOrLoadingUsingInterruptMonitor executed successfully.");
}
```
 Ini`Run` metode adalah titik masuk untuk memulai dan mengamati interupsi dalam tindakan.
## Kesimpulan
Dalam tutorial ini, kami mengeksplorasi cara menghentikan proses konversi di Aspose.Cells untuk .NET. Interrupt Monitor adalah alat yang berguna saat bekerja dengan file Excel yang besar, yang memungkinkan Anda menghentikan proses tanpa menunggunya selesai. Ini sangat berguna dalam skenario di mana waktu dan sumber daya sangat berharga, dan umpan balik cepat dibutuhkan.
## Pertanyaan yang Sering Diajukan
### Apa itu Interrupt Monitor di Aspose.Cells untuk .NET?  
Interrupt Monitor memungkinkan Anda menghentikan proses konversi atau pemuatan buku kerja di tengah jalan.
### Dapatkah saya menggunakan Interrupt Monitor untuk format lain selain PDF?  
Ya, Anda juga dapat menghentikan konversi ke format lain yang didukung.
### Bagaimana Thread.Sleep() mempengaruhi waktu interupsi?  
Thread.Sleep() menciptakan penundaan sebelum memicu interupsi, memberikan waktu untuk memulai konversi.
### Bisakah saya menghentikan proses sebelum 10 detik?  
 Ya, ubah penundaan di`WaitForWhileAndThenInterrupt()` ke waktu yang lebih singkat.
### Apakah proses interupsi akan memengaruhi kinerja?  
Dampaknya minimal, dan sangat bermanfaat untuk mengelola proses yang berjalan lama.
 Untuk informasi lebih lanjut, silakan lihat[Dokumentasi Aspose.Cells untuk .NET](https://reference.aspose.com/cells/net/) Jika Anda butuh bantuan, lihat[Forum Dukungan](https://forum.aspose.com/c/cells/9)atau dapatkan[Uji Coba Gratis](https://releases.aspose.com/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
