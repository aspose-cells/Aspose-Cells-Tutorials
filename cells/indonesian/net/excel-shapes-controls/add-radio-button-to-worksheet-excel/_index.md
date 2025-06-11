---
"description": "Pelajari cara menambahkan tombol radio ke lembar kerja Excel menggunakan Aspose.Cells for .NET dengan panduan langkah demi langkah yang mudah ini. Sempurna untuk membuat formulir Excel yang interaktif."
"linktitle": "Tambahkan Tombol Radio ke Lembar Kerja di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Tambahkan Tombol Radio ke Lembar Kerja di Excel"
"url": "/id/net/excel-shapes-controls/add-radio-button-to-worksheet-excel/"
"weight": 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Tambahkan Tombol Radio ke Lembar Kerja di Excel

## Bevezetés
Pernahkah Anda bertanya-tanya bagaimana cara mempercantik lembar Excel Anda dengan elemen interaktif seperti tombol radio? Baik Anda sedang membuat survei, formulir, atau alat analisis, menambahkan tombol radio benar-benar dapat meningkatkan interaksi pengguna. Dalam tutorial ini, kami akan memandu Anda melalui proses penambahan tombol radio ke lembar Excel Anda menggunakan Aspose.Cells for .NET. Kami akan menguraikan semuanya menjadi langkah-langkah yang mudah diikuti, memastikan Anda akan menjadi ahli di akhir artikel ini. Siap untuk mencobanya? Mari kita mulai!
## Előfeltételek
Sebelum kita masuk ke bagian yang menyenangkan yaitu menambahkan tombol radio, mari pastikan Anda telah menyiapkan semuanya untuk memulai.
1. Aspose.Cells untuk .NET: Pertama, pastikan Anda telah mengunduh dan menginstal [Aspose.Cells .NET-hez](https://releases.aspose.com/cells/net/) pustaka. Anda dapat mengunduhnya melalui NuGet di Visual Studio atau dari halaman unduhan.
2. IDE (Integrated Development Environment): Anda memerlukan IDE seperti Visual Studio untuk menulis dan mengeksekusi kode C# Anda.
3. .NET Framework: Pastikan Anda telah menginstal .NET Framework 4.0 atau yang lebih baru di komputer Anda. Aspose.Cells memerlukan ini agar dapat berfungsi.
4. Pemahaman Dasar C#: Keakraban dengan sintaksis C# dan pemrograman .NET akan membuat segalanya lebih mudah saat Anda mengikutinya.
Setelah semuanya siap, kita siap berangkat!
## Csomagok importálása
Sebelum melakukan pengodean, penting untuk mengimpor namespace yang diperlukan guna menghindari kesalahan di kemudian hari. Tambahkan yang berikut ke kode Anda:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Drawing;
```
Impor ini penting untuk mengakses fungsionalitas buku kerja, menambahkan tombol radio, dan menangani operasi file.
## Langkah 1: Menyiapkan Buku Kerja
Hal pertama yang terpenting, mari buat buku kerja Excel baru.
Untuk memulai, Anda perlu membuat instance baru `Workbook` objek. Ini akan mewakili berkas Excel Anda dalam bentuk kode.
```csharp
// Hozz létre egy új munkafüzetet.
Workbook excelbook = new Workbook();
```
Pada langkah ini, Anda membuat buku kerja kosong. Bayangkan buku kerja tersebut sebagai kanvas kosong tempat Anda akan menambahkan tombol radio pada langkah berikutnya.
## Langkah 2: Menambahkan dan Memformat Nilai Sel
Selanjutnya, mari tambahkan judul ke lembar kerja. Kita akan menambahkan beberapa teks ke sel `C2` dan format agar menjadi tebal. Langkah ini menambahkan konteks ke tombol radio Anda.
### Sisipkan Teks di Sel
```csharp
// Masukkan nilai di sel C2.
excelbook.Worksheets[0].Cells["C2"].PutValue("Age Groups");
```
### Membuat Teks Tebal
```csharp
// Atur teks font di sel C2 menjadi tebal.
excelbook.Worksheets[0].Cells["C2"].GetStyle().Font.IsBold = true;
```
Di sini, kami telah menambahkan judul sederhana, “Kelompok Usia,” di sel `C2`, dan membuatnya tebal sehingga menonjol. Mudah, bukan?
## Langkah 3: Menambahkan Tombol Radio Pertama
Sekarang tibalah bagian yang menarik: menambahkan tombol radio pertama Anda ke lembar kerja!
### Tambahkan Tombol Radio
```csharp
// Tambahkan tombol radio ke lembar pertama.
Aspose.Cells.Drawing.RadioButton radio1 = excelbook.Worksheets[0].Shapes.AddRadioButton(3, 0, 2, 0, 30, 110);
```
Baris ini menambahkan tombol radio ke posisi tertentu pada lembar kerja Anda. Angka-angka tersebut mewakili penempatan dan ukurannya. Anggap saja seperti pengaturan koordinat X dan Y tombol.
### Mengatur Teks Tombol Radio
```csharp
// Tetapkan string teksnya.
radio1.Text = "20-29";
```
Di sini, kami memberi tombol radio label, “20-29,” yang mewakili kelompok usia.
### Hubungkan Tombol Radio ke Sel
```csharp
// Tetapkan sel A1 sebagai sel yang ditautkan untuk tombol radio.
radio1.LinkedCell = "A1";
```
Ini menghubungkan tombol radio ke sel `A1`, artinya hasil pemilihan tombol akan disimpan di sel tersebut.
### Tambahkan Efek 3D
```csharp
// Jadikan tombol radio 3-D.
radio1.Shadow = true;
```
Karena kami ingin tombol radio ini muncul, kami menambahkan efek 3D.
### Sesuaikan Garis Tombol Radio
```csharp
// Tetapkan bobot garis tombol radio.
radio1.Line.Weight = 4;
// Mengatur gaya tanda hubung pada garis tombol radio.
radio1.Line.DashStyle = MsoLineDashStyle.Solid;
```
Baris kode ini menyesuaikan ketebalan dan gaya tanda hubung pada batas tombol radio untuk membuatnya lebih menarik secara visual.
## Langkah 4: Menambahkan Tombol Radio Tambahan
Mari tambahkan dua tombol radio lagi untuk kelompok usia yang tersisa: "30-39" dan "40-49." Langkah-langkahnya sama, hanya dengan sedikit variasi pada koordinat dan label.
### Tambahkan Tombol Radio Kedua
```csharp
// Tambahkan tombol radio lain ke lembar pertama.
Aspose.Cells.Drawing.RadioButton radio2 = excelbook.Worksheets[0].Shapes.AddRadioButton(6, 0, 2, 0, 30, 110);
// Tetapkan string teksnya.
radio2.Text = "30-39";
// Tetapkan sel A1 sebagai sel yang ditautkan untuk tombol radio.
radio2.LinkedCell = "A1";
// Jadikan tombol radio 3-D.
radio2.Shadow = true;
// Tetapkan bobot tombol radio.
radio2.Line.Weight = 4;
// Mengatur gaya tanda hubung tombol radio.
radio2.Line.DashStyle = MsoLineDashStyle.Solid;
```
### Tambahkan Tombol Radio Ketiga
```csharp
// Tambahkan tombol radio lain ke lembar pertama.
Aspose.Cells.Drawing.RadioButton radio3 = excelbook.Worksheets[0].Shapes.AddRadioButton(9, 0, 2, 0, 30, 110);
// Tetapkan string teksnya.
radio3.Text = "40-49";
// Tetapkan sel A1 sebagai sel yang ditautkan untuk tombol radio.
radio3.LinkedCell = "A1";
// Jadikan tombol radio 3-D.
radio3.Shadow = true;
// Tetapkan bobot tombol radio.
radio3.Line.Weight = 4;
// Mengatur gaya tanda hubung tombol radio.
radio3.Line.DashStyle = MsoLineDashStyle.Solid;
```
## Langkah 5: Menyimpan File Excel
Setelah semua tombol radio ditambahkan dan diformat, saatnya menyimpan berkas.
```csharp
// Mentse el az excel fájlt.
string dataDir = "Your Document Directory";
excelbook.Save(dataDir + "book1.out.xls");
```
Pada langkah ini, buku kerja disimpan ke direktori yang Anda tentukan. Semudah itu—lembar kerja interaktif Anda kini siap!
## Következtetés
Nah, itu dia! Anda baru saja menambahkan tombol radio ke lembar kerja Excel menggunakan Aspose.Cells untuk .NET. Tutorial ini mencakup semuanya mulai dari menyiapkan buku kerja, memasukkan dan memformat nilai, menambahkan beberapa tombol radio, dan menautkannya ke sel. Sekarang, Anda siap membuat lembar Excel interaktif yang tidak hanya tampak hebat tetapi juga memberikan pengalaman pengguna yang lebih baik. Selamat menjelajahi lebih banyak kemungkinan dengan Aspose.Cells!
## GYIK
### Bisakah saya menambahkan lebih banyak tombol radio ke lembar yang berbeda?  
Tentu saja! Anda dapat mengulangi proses ini pada lembar mana pun dalam buku kerja dengan menentukan indeks lembar kerja yang benar.
### Bisakah saya menyesuaikan tampilan tombol radio lebih lanjut?  
Ya, Aspose.Cells menyediakan berbagai opsi penyesuaian, termasuk mengubah warna, ukuran, dan atribut pemformatan lainnya.
### Bagaimana saya dapat mendeteksi tombol radio mana yang dipilih?  
Sel yang ditautkan (misalnya, A1) akan menampilkan indeks tombol radio yang dipilih. Anda dapat memeriksa nilai sel yang ditautkan untuk mengetahui sel mana yang dipilih.
### Apakah ada batasan jumlah tombol radio yang dapat saya tambahkan?  
Tidak, tidak ada batasan pasti mengenai jumlah tombol radio yang dapat Anda tambahkan. Akan tetapi, sebaiknya antarmuka tetap ramah pengguna.
### Használhatom az Aspose.Cells-t más programozási nyelvekkel?  
Ya, Aspose.Cells mendukung banyak bahasa pemrograman, termasuk Java. Namun, tutorial ini secara khusus berfokus pada .NET.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}