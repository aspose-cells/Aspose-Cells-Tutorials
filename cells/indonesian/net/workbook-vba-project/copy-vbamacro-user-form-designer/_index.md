---
title: Salin Penyimpanan Desainer Formulir Pengguna VBAMacro ke Buku Kerja menggunakan Aspose.Cells
linktitle: Salin Penyimpanan Desainer Formulir Pengguna VBAMacro ke Buku Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menyalin VBA Macro User Form Designer secara efisien di Aspose.Cells untuk .NET dengan tutorial langkah demi langkah kami yang komprehensif! Manfaatkan potensi Excel.
weight: 11
url: /id/net/workbook-vba-project/copy-vbamacro-user-form-designer/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Salin Penyimpanan Desainer Formulir Pengguna VBAMacro ke Buku Kerja menggunakan Aspose.Cells

## Perkenalan
Selamat datang! Jika Anda ingin meningkatkan pengalaman Excel Anda dengan makro VBA dan formulir pengguna, Anda berada di tempat yang tepat! Dalam panduan ini, kami akan membahas cara menyalin Desainer UserForm Makro VBA dari satu buku kerja ke buku kerja lain menggunakan Aspose.Cells untuk .NET. Baik Anda pengembang berpengalaman atau baru memulai, kami akan memandu Anda melalui setiap langkah penting. Anggap ini sebagai buku pedoman Anda untuk menguasai seni menangani file Excel secara terprogram. Siap untuk mencobanya? Ayo!
## Prasyarat
Sebelum kita masuk ke inti pengkodean, mari pastikan Anda memiliki semua yang dibutuhkan:
1. Lingkungan Pengembangan C#: Anda harus memiliki lingkungan kerja yang siap untuk pengembangan C#. Visual Studio sangat direkomendasikan.
2.  Pustaka Aspose.Cells untuk .NET: Pastikan Anda telah mengintegrasikan pustaka Aspose.Cells ke dalam proyek Anda. Anda dapat dengan mudah[unduh disini](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar tentang VBA dan Makro Excel: Pemahaman yang baik tentang VBA dan cara kerja makro Excel akan membantu Anda menavigasi tutorial ini dengan mudah.
4. File Excel dengan Formulir Pengguna: Untuk bereksperimen, buat atau dapatkan buku kerja Excel yang berisi Formulir Pengguna, sebaiknya dengan makro yang diaktifkan (seperti`.xlsm` (berkas).
## Paket Impor
Dalam proyek C# Anda, Anda perlu mengimpor namespace tertentu di bagian atas berkas Anda untuk memanfaatkan fungsi Aspose.Cells. Berikut cara melakukannya:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells.Vba;
```
Menyertakan namespace ini memungkinkan Anda mengakses semua alat hebat yang tertanam dalam pustaka Aspose.Cells. 
Sekarang setelah prasyarat dan paket-paket telah terpenuhi, saatnya beralih ke bagian yang menyenangkan: pengodean! Mari kita uraikan langkah demi langkah.
## Langkah 1: Tentukan Direktori Sumber dan Output Anda
Pertama, Anda perlu menentukan di mana file Anda berada:
```csharp
// Direktori sumber
string sourceDir = "Your Document Directory";
// Direktori keluaran
string outputDir = "Your Document Directory";
```
 Di sini, ganti`"Your Document Directory"` dengan jalur sebenarnya tempat file Anda disimpan. Di sinilah buku kerja sumber kita (dengan UserForm) akan diambil dan tempat buku kerja baru akan disimpan.
## Langkah 2: Buat Buku Kerja Target Kosong
Berikutnya, mari buat buku kerja target tempat kita akan menyalin formulir pengguna dan makro kita:
```csharp
// Buat buku kerja target kosong
Workbook target = new Workbook();
```
Baris kode ini menginisialisasi buku kerja baru yang kosong untuk diisi dengan data. Anggap saja ini sebagai kanvas kosong untuk karya agung Anda!
## Langkah 3: Muat Buku Kerja Template Anda
Kita perlu memuat buku kerja yang berisi formulir pengguna dan makro Anda:
```csharp
// Muat file Excel yang berisi Formulir Pengguna VBA-Macro Designer
Workbook templateFile = new Workbook(sourceDir + "sampleDesignerForm.xlsm");
```
 Pastikan untuk berubah`"sampleDesignerForm.xlsm"` ke nama berkas Anda yang sebenarnya. Buku kerja ini seperti buku resep Anda—dari buku inilah kita akan mengambil bahan-bahan kita!
## Langkah 4: Salin Lembar Kerja ke Buku Kerja Target
Sekarang, mari mulai menyalin lembar kerja dari templat kita ke buku kerja target:
```csharp
// Salin semua lembar kerja templat ke buku kerja target
foreach (Worksheet ws in templateFile.Worksheets)
{
    if (ws.Type == SheetType.Worksheet)
    {
        Worksheet s = target.Worksheets.Add(ws.Name);
        s.Copy(ws);
        // Letakkan pesan di sel A2 lembar kerja target
        s.Cells["A2"].PutValue("VBA Macro and User Form copied from template to target.");
    }
}
```
Pada langkah ini, kita mengulang setiap lembar kerja dalam templat dan menyalinnya ke buku kerja target. Jika dipikir-pikir, ini seperti memindahkan resep terbaik Anda dari satu buku masak ke buku masak lainnya!
## Langkah 5: Salin Makro VBA dari Template
Berikutnya, kita akan menyalin makro VBA, termasuk modul UserForm Designer, ke buku kerja baru kita:
```csharp
// Salin UserForm Desainer VBA-Macro dari Template ke Target
foreach (VbaModule vbaItem in templateFile.VbaProject.Modules)
{
    if (vbaItem.Name == "ThisWorkbook")
    {
        // Salin kode modul ThisWorkbook
        target.VbaProject.Modules["ThisWorkbook"].Codes = vbaItem.Codes;
    }
    else
    {
        // Salin kode dan data modul lainnya
        System.Diagnostics.Debug.Print(vbaItem.Name);
        int vbaMod = 0;
        Worksheet sheet = target.Worksheets.GetSheetByCodeName(vbaItem.Name);
        if (sheet == null)
        {
            vbaMod = target.VbaProject.Modules.Add(vbaItem.Type, vbaItem.Name);
        }
        else
        {
            vbaMod = target.VbaProject.Modules.Add(sheet);
        }
        target.VbaProject.Modules[vbaMod].Codes = vbaItem.Codes;
        if ((vbaItem.Type == VbaModuleType.Designer))
        {
            // Dapatkan data dari penyimpanan desainer formulir pengguna
            byte[] designerStorage = templateFile.VbaProject.Modules.GetDesignerStorage(vbaItem.Name);
            // Tambahkan penyimpanan desainer ke Proyek Vba target
            target.VbaProject.Modules.AddDesignerStorage(vbaItem.Name, designerStorage);
        }
    }
}
```
Potongan kode yang besar ini menangani pengecekan setiap modul VBA dalam file template. Kami menyalin desain UserForm dan kode terkaitnya. Ini seperti memastikan Anda tidak hanya mendapatkan resep pai Nenek yang terkenal tetapi juga teknik memanggangnya yang tepat!
## Langkah 6: Simpan Buku Kerja Target
Setelah kita memperoleh semua salinan kita, saatnya menyimpan kerja keras kita:
```csharp
// Simpan buku kerja target
target.Save(outputDir + "outputDesignerForm.xlsm", SaveFormat.Xlsm);
```
Pastikan untuk mengubah nama berkas keluaran sesuai kebutuhan. Setelah Anda menyimpannya, Anda secara efektif membuat versi buku kerja yang disesuaikan sendiri yang penuh dengan makro dan formulir pengguna. Seberapa menarik itu?
## Langkah 7: Konfirmasikan Keberhasilan
Terakhir, mari kita cetak pesan sukses ke konsol:
```csharp
Console.WriteLine("CopyVBAMacroUserFormDesignerStorageToWorkbook executed successfully.\r\n");
```
Kalimat singkat ini meyakinkan Anda bahwa proses Anda berjalan lancar. Ini adalah pelengkap yang sempurna untuk coding Anda!
## Kesimpulan
Selamat! Anda telah menyelesaikan panduan langkah demi langkah untuk menyalin VBA Macro User Form Designer dari satu buku kerja ke buku kerja lain menggunakan Aspose.Cells untuk .NET. Awalnya mungkin tampak sedikit membingungkan, tetapi dengan latihan, Anda akan dapat menangani manipulasi buku kerja seperti seorang profesional. Ingat, pengodean adalah tentang latihan, jadi jangan ragu untuk mencoba berbagai hal berbeda di file Excel Anda. Jika Anda memiliki pertanyaan atau mengalami masalah, jangan ragu untuk memeriksa forum Aspose atau dokumentasi untuk mendapatkan dukungan!
## Pertanyaan yang Sering Diajukan
### Versi Excel apa yang didukung Aspose.Cells?
Aspose.Cells mendukung berbagai format Excel termasuk XLSX, XLSM, CSV, dan banyak lagi.
### Bisakah saya menggunakan Aspose.Cells secara gratis?
 Ya! Anda dapat memulai dengan uji coba gratis, yang memungkinkan Anda mengevaluasi pustaka:[Uji Coba Gratis](https://releases.aspose.com/).
### Apakah saya memerlukan Visual Studio untuk menjalankan kode ini?
Meskipun sangat direkomendasikan karena fitur-fiturnya yang mudah digunakan, IDE C# apa pun dapat digunakan asalkan mendukung pengembangan .NET.
### Di mana saya dapat menemukan lebih banyak contoh dan dokumentasi?
 Anda dapat menjelajahi[Dokumentasi Aspose.Cells](https://reference.aspose.com/cells/net/) untuk contoh lebih lanjut dan penjelasan lebih mendalam.
### Bagaimana cara mengatasi masalah saat menggunakan Aspose.Cells?
 Anda harus mengunjungi[Forum Dukungan Aspose](https://forum.aspose.com/c/cells/9) untuk bantuan dari komunitas dan staf dukungan Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
