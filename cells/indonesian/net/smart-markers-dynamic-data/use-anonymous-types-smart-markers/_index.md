---
title: Gunakan Tipe Anonim dengan Penanda Cerdas Aspose.Cells
linktitle: Gunakan Tipe Anonim dengan Penanda Cerdas Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menggunakan tipe anonim dengan penanda cerdas di Aspose.Cells untuk pembuatan laporan Excel yang dinamis di .NET. Ikuti panduan mudah kami.
weight: 17
url: /id/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gunakan Tipe Anonim dengan Penanda Cerdas Aspose.Cells

## Perkenalan
Jika berbicara tentang pembuatan laporan Excel yang dinamis dalam aplikasi .NET, Aspose.Cells menonjol sebagai alat yang hebat. Salah satu fitur terbaiknya adalah kemampuan untuk bekerja dengan penanda cerdas dan tipe anonim. Jika Anda baru mengenal konsep ini, jangan khawatir! Panduan ini akan menguraikan semua yang perlu Anda ketahui, dari prasyarat hingga contoh praktis, sekaligus membuatnya menarik dan mudah diikuti.
## Prasyarat
Sebelum kita masuk ke kode, mari pastikan Anda memiliki semua yang dibutuhkan untuk menjalankan contoh dalam tutorial ini dengan lancar.
### 1. Lingkungan .NET
Pastikan Anda memiliki lingkungan .NET yang berfungsi pada komputer lokal Anda. Anda dapat menggunakan Visual Studio atau IDE lain pilihan Anda.
### 2. Pustaka Aspose.Cells
 Anda memerlukan pustaka Aspose.Cells. Jika Anda belum mengunduhnya, Anda dapat menemukannya dengan mudah[Di Sini](https://releases.aspose.com/cells/net/) Anda juga dapat mencobanya dengan uji coba gratis yang tersedia di[tautan ini](https://releases.aspose.com/).
### 3. Pengetahuan Dasar C#
Pemahaman mendasar tentang pemrograman C# akan membantu Anda menavigasi tutorial dengan lebih mudah. Jika istilah seperti kelas, objek, dan properti sudah familier bagi Anda, Anda siap untuk memulai!
## Paket Impor
Untuk menggunakan pustaka Aspose.Cells di proyek Anda, Anda harus mengimpor namespace terkait. Tambahkan perintah penggunaan berikut di bagian atas berkas C# Anda:
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
Ruang nama ini akan memberi Anda akses ke semua kelas dan metode yang diperlukan yang akan dibahas nanti.
Sekarang, mari kita masuk ke inti tutorial! Anda akan melihat cara membuat file Excel dengan penanda cerdas menggunakan kelas khusus. Jangan khawatir; kami akan menguraikan semuanya menjadi langkah-langkah yang mudah dikelola!
## Langkah 1: Buat Kelas Kustom
Pertama, kita perlu kelas sederhana untuk mewakili data yang ingin kita tambahkan ke berkas Excel. Kelas ini akan menyimpan informasi tentang seseorang.
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
 Di sini, kita mendefinisikan kelas yang disebut`Person` dengan dua properti,`Name` Dan`Age`Konstruktor menginisialisasi properti ini. 
## Langkah 2: Siapkan Desainer Buku Kerja
 Selanjutnya, mari kita buat sebuah instance dari`WorkbookDesigner`kelas, yang akan kita gunakan untuk mendesain berkas Excel kita dengan penanda pintar.
```csharp
// Jalur ke direktori dokumen.
string dataDir = "Your Document Directory";
// Membuat instance objek perancang buku kerja.
WorkbookDesigner report = new WorkbookDesigner();
```
 Mengganti`"Your Document Directory"` dengan jalur file aktual tempat Anda ingin menyimpan file Excel.`WorkbookDesigner` kelas adalah jantung operasi ini, tempat Anda menentukan templat Anda.
## Langkah 3: Tambahkan Penanda ke Sel
Sekarang, kita perlu menambahkan penanda cerdas ke lembar kerja. Penanda ini akan menjadi tempat penampung data yang akan kita masukkan nanti.
```csharp
// Dapatkan lembar kerja pertama dalam buku kerja.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// Masukkan beberapa penanda ke dalam sel.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
 Kami menunjuk lembar kerja pertama dan menetapkan nilai untuk sel header. Penanda pintar diawali dengan`&=` yang memberi tahu Aspose bahwa ini adalah tempat penampung data yang akan disisipkan nanti.
## Langkah 4: Buat Daftar Orang
 Sekarang mari kita membuat daftar orang menggunakan`Person` kelas yang akan kita gunakan untuk mengisi penanda pintar.
```csharp
// Buat contoh koleksi daftar berdasarkan kelas khusus.
IList<Person> list = new List<Person>();
// Berikan nilai untuk penanda menggunakan objek kelas kustom.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
 Kami membuat daftar dan menambahkan contoh`Person`Daftar ini berfungsi sebagai sumber data saat mengisi templat Excel.
## Langkah 5: Tetapkan Sumber Data dan Penanda Proses
 Setelah daftar kita siap, kita perlu mengaturnya sebagai sumber data untuk`WorkbookDesigner` misalnya dan kemudian memproses penandanya.
```csharp
// Tetapkan sumber data.
report.SetDataSource("MyProduct", list);
// Memproses penanda.
report.Process(false);
```
 Itu`SetDataSource` metode menghubungkan daftar yang telah kita definisikan sebelumnya ke penanda.`Process` metode mengganti penanda pintar dalam buku kerja dengan nilai aktual dari objek kita.
## Langkah 6: Simpan File Excel
Terakhir, kita akan menyimpan buku kerja yang dimodifikasi ke direktori yang telah ditentukan.
```csharp
// Simpan berkas excel.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
Baris ini menyimpan buku kerja ke jalur file yang ditentukan. Anda dapat membuka file ini menggunakan Excel untuk melihat data yang disisipkan.
## Kesimpulan
Nah, itu dia! Anda telah berhasil membuat file Excel menggunakan smart marker di Aspose.Cells dengan kelas kustom Anda sendiri. Metode ini tidak hanya membuat manajemen data Anda lebih dinamis, tetapi juga menjaga kode Anda tetap bersih dan teratur.
Jadi, apakah Anda membuat laporan untuk analitik, melacak informasi, atau tugas terkait data lainnya, penanda pintar adalah sekutu Anda dalam membuat laporan Excel lebih mudah dikelola dan fleksibel!
## Pertanyaan yang Sering Diajukan
### Apa itu penanda pintar di Aspose.Cells?
Penanda pintar adalah tempat penampung khusus dalam dokumen Excel yang memungkinkan Anda menyisipkan data secara dinamis saat runtime.
### Dapatkah saya menggunakan tipe anonim untuk penanda pintar?
Ya! Penanda pintar dapat digunakan dengan semua jenis objek, termasuk tipe anonim, selama sesuai dengan struktur data yang diharapkan.
### Apakah Aspose.Cells gratis untuk digunakan?
Aspose.Cells adalah produk berbayar, tetapi Anda dapat memulai dengan uji coba gratis untuk menjelajahi fitur-fiturnya.
### Format file apa yang didukung Aspose.Cells?
Mendukung berbagai format file, termasuk XLS, XLSX, CSV, dan banyak lagi.
### Di mana saya dapat menemukan informasi lebih lanjut tentang Aspose.Cells?
 Untuk detail lebih lanjut, silakan cek[dokumentasi](https://reference.aspose.com/cells/net/) atau kunjungi[forum dukungan](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
