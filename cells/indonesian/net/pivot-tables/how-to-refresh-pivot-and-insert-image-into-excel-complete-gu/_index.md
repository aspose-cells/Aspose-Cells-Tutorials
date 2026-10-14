---
category: general
date: 2026-04-07
description: Pelajari cara menyegarkan pivot, menyisipkan gambar ke dalam Excel, dan
  menyimpan buku kerja Excel dengan placeholder gambar dalam beberapa langkah saja.
draft: false
keywords:
- how to refresh pivot
- insert image into excel
- save excel workbook
- add picture placeholder
- refresh pivot table
language: id
og_description: Cara menyegarkan pivot di Excel, menyisipkan gambar ke dalam Excel,
  dan menyimpan buku kerja Excel menggunakan C# dengan placeholder gambar. Contoh
  kode langkah demi langkah.
og_title: Cara menyegarkan pivot dan menyisipkan gambar ke Excel – Panduan Lengkap
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara menyegarkan pivot dan menyisipkan gambar ke dalam Excel – Panduan Lengkap
url: /id/net/pivot-tables/how-to-refresh-pivot-and-insert-image-into-excel-complete-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara menyegarkan pivot dan menyisipkan gambar ke Excel – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara menyegarkan pivot** ketika data sumber berubah, dan kemudian menempatkan gambar grafik atau tabel baru langsung ke lembar yang sama? Anda bukan satu-satunya. Dalam banyak alur pelaporan data berada di database, tabel pivot menariknya, dan file Excel akhir harus menampilkan angka terbaru sebagai gambar—agar pengguna downstream tidak sengaja mengedit sumber.  

Dalam tutorial ini kami akan membahas secara detail: **bagaimana cara menyegarkan pivot**, **menyisipkan gambar ke Excel**, dan akhirnya **menyimpan workbook Excel** sambil menggunakan **placeholder gambar**. Pada akhir tutorial Anda akan memiliki satu program C# yang dapat dijalankan yang melakukan semuanya, dan Anda akan memahami mengapa setiap baris kode penting.

> **Pro tip:** Pendekatan ini bekerja dengan Aspose.Cells 2024 atau yang lebih baru, yang berarti Anda tidak memerlukan Excel terpasang di server.

---

## Apa yang Anda Butuhkan

- **Aspose.Cells for .NET** (paket NuGet `Aspose.Cells`).  
- .NET 6.0 SDK atau yang lebih baru (kode juga dapat dikompilasi dengan .NET 8).  
- File Excel dasar (`input.xlsx`) yang sudah berisi tabel pivot dan placeholder gambar (objek gambar pertama pada lembar).  
- Sedikit rasa ingin tahu tentang model objek Excel.

Tidak ada interop COM tambahan, tidak perlu instalasi Office, hanya C# murni.

---

## Cara Menyegarkan Pivot dan Menangkap Data Terbaru

Hal pertama yang harus Anda lakukan adalah memberi tahu Excel (atau lebih tepatnya, Aspose.Cells) bahwa tabel pivot harus menghitung ulang berdasarkan rentang sumber terbaru. Melewatkan langkah ini akan membuat Anda mendapatkan angka yang usang, yang mengalahkan tujuan otomatisasi secara keseluruhan.

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// 1️⃣ Load the workbook and grab the first worksheet
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelDemo\input.xlsx");
Worksheet worksheet = workbook.Worksheets[0];

// 2️⃣ Refresh the first pivot table so it reflects the latest data
worksheet.PivotTables[0].Refresh();
```

**Mengapa ini penting:**  
Saat Anda memanggil `Refresh()`, mesin pivot menjalankan kembali logika agregasinya. Jika Anda kemudian mengekspor pivot sebagai gambar, gambar tersebut akan menampilkan *total saat ini*, bukan yang ada saat file terakhir disimpan.

---

## Menyisipkan Gambar ke Excel Menggunakan Placeholder Gambar

Setelah pivot segar, kita perlu mengubahnya menjadi gambar statis. Ini berguna ketika Anda ingin mengunci visual untuk distribusi atau menyematkannya ke slide PowerPoint nanti.

```csharp
// 3️⃣ Set up image options – we want a PNG image
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png
};

// 4️⃣ Render the refreshed pivot table to an image using the options
Image pivotImage = worksheet.PivotTables[0].ToImage(imageOptions);
```

Objek `ImageOrPrintOptions` memungkinkan Anda mengontrol resolusi, latar belakang, dan format. PNG bersifat loss‑less dan bekerja dengan baik untuk kebanyakan laporan bisnis.

---

## Menambahkan Placeholder Gambar ke Worksheet

Sebagian besar templat Excel sudah berisi bentuk atau gambar yang berfungsi sebagai “slot” untuk grafik dinamis. Jika Anda belum memilikinya, cukup sisipkan gambar kosong di Excel dan simpan templatnya—Aspose.Cells akan menampilkannya sebagai `Pictures[0]`.

```csharp
// 5️⃣ Place the rendered image into the first picture placeholder on the sheet
worksheet.Pictures[0].Image = pivotImage;
```

**Bagaimana jika Anda memiliki beberapa placeholder?**  
Cukup ubah indeks (`Pictures[1]`, `Pictures[2]`, …) atau lakukan loop melalui `worksheet.Pictures` untuk menemukan satu berdasarkan nama.

---

## Menyimpan Workbook Excel Setelah Modifikasi

Akhirnya, kami menyimpan perubahan. Workbook kini berisi pivot yang telah disegarkan, PNG yang baru dibuat, dan placeholder gambar yang telah diperbarui dengan gambar tersebut.

```csharp
// 6️⃣ Save the workbook to see the result
workbook.Save(@"C:\MyProjects\ExcelDemo\output.xlsx");
```

Saat Anda membuka `output.xlsx` Anda akan melihat slot gambar terisi dengan snapshot pivot terbaru. Tidak ada langkah manual yang diperlukan.

---

## Contoh Kerja Lengkap (Semua Langkah Bersama)

Berikut adalah program lengkap yang siap disalin‑tempel. Program ini mencakup pernyataan `using` yang diperlukan, penanganan error, dan komentar yang menjelaskan setiap baris yang tidak langsung terlihat.

```csharp
using Aspose.Cells;
using System;
using System.Drawing.Imaging;

namespace ExcelPivotImageDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\MyProjects\ExcelDemo\input.xlsx";
            string outputPath = @"C:\MyProjects\ExcelDemo\output.xlsx";

            try
            {
                // Load workbook
                Workbook workbook = new Workbook(inputPath);
                Worksheet sheet = workbook.Worksheets[0];

                // -------------------------------------------------
                // Refresh pivot table – this is the core of "how to refresh pivot"
                // -------------------------------------------------
                if (sheet.PivotTables.Count == 0)
                {
                    Console.WriteLine("No pivot tables found on the first worksheet.");
                    return;
                }
                sheet.PivotTables[0].Refresh();

                // -------------------------------------------------
                // Convert refreshed pivot to PNG image
                // -------------------------------------------------
                ImageOrPrintOptions imgOpts = new ImageOrPrintOptions
                {
                    ImageFormat = ImageFormat.Png,
                    // Optional: higher DPI for sharper images
                    HorizontalResolution = 150,
                    VerticalResolution = 150
                };
                Image pivotImg = sheet.PivotTables[0].ToImage(imgOpts);

                // -------------------------------------------------
                // Insert the image into the first picture placeholder
                // -------------------------------------------------
                if (sheet.Pictures.Count == 0)
                {
                    // If the template lacks a placeholder, we create one on the fly
                    int picIdx = sheet.Pictures.Add(0, 0, pivotImg);
                    sheet.Pictures[picIdx].Name = "PivotSnapshot";
                }
                else
                {
                    sheet.Pictures[0].Image = pivotImg;
                }

                // -------------------------------------------------
                // Save the updated workbook – this fulfills "save excel workbook"
                // -------------------------------------------------
                workbook.Save(outputPath);
                Console.WriteLine($"Workbook saved successfully to {outputPath}");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
                // In production you might log the stack trace or rethrow
            }
        }
    }
}
```

**Hasil yang diharapkan:**  
Buka `output.xlsx`. Objek gambar pertama kini menampilkan PNG dari tabel pivot yang telah disegarkan. Jika Anda mengubah data sumber di `input.xlsx` dan menjalankan program lagi, gambar akan otomatis terupdate—tanpa perlu menyalin‑tempel secara manual.

---

## Variasi Umum & Kasus Edge

| Situasi | Apa yang Perlu Diubah |
|-----------|----------------|
| **Multiple pivot tables** | Loop melalui `sheet.PivotTables` dan segarkan masing‑masing, kemudian pilih yang Anda butuhkan untuk gambar. |
| **Different image format** | Set `ImageFormat = ImageFormat.Jpeg` (atau `Bmp`) di `ImageOrPrintOptions`. |
| **Dynamic placeholder selection** | Gunakan `sheet.Pictures["MyPlaceholderName"]` alih‑alih indeks. |
| **Large workbooks** | Tingkatkan `Workbook.Settings.CalculateFormulaEngine` ke `EngineType.Fast` untuk refresh yang lebih cepat. |
| **Running on a headless server** | Aspose.Cells berfungsi penuh tanpa UI, jadi tidak ada konfigurasi tambahan yang diperlukan. |

---

## Pertanyaan yang Sering Diajukan

**Q: Apakah ini bekerja dengan workbook yang mendukung macro (`.xlsm`)?**  
A: Ya. Aspose.Cells memperlakukan mereka seperti workbook lainnya; macro tetap dipertahankan tetapi tidak dijalankan selama refresh.

**Q: Bagaimana jika pivot menggunakan sumber data eksternal?**  
A: Anda harus memastikan string koneksi valid pada mesin yang menjalankan kode. Panggil `pivotTable.CacheDefinition.ConnectionInfo` untuk menyesuaikannya secara programatik.

**Q: Bisakah saya menempatkan gambar ke rentang sel tertentu alih‑alih placeholder gambar?**  
A: Tentu saja. Gunakan `sheet.Pictures.Add(row, column, pivotImg)` dimana `row` dan `column` adalah indeks berbasis nol.

---

## Ringkasan

Kami telah membahas **bagaimana cara menyegarkan pivot**, **menyisipkan gambar ke Excel**, **menambahkan placeholder gambar**, dan akhirnya **menyimpan workbook Excel**—semuanya dalam potongan kode C# yang rapi. Dengan menyegarkan pivot terlebih dahulu, Anda menjamin bahwa gambar mencerminkan angka terbaru, dan dengan menggunakan placeholder Anda menjaga templat tetap bersih dan dapat digunakan kembali.

Selanjutnya, Anda dapat menjelajahi:

- Mengekspor gambar yang sama ke laporan PDF (`PdfSaveOptions`).  
- Mengotomatiskan batch file dengan data sumber yang berbeda.  
- Menggunakan Aspose.Slides untuk menempelkan PNG langsung ke slide PowerPoint.

Silakan bereksperimen—ganti PNG dengan JPEG, ubah DPI, atau tambahkan beberapa gambar. Ide dasarnya tetap sama: jaga data tetap segar, tangkap sebagai gambar, dan sematkan di tempat yang Anda butuhkan.

Selamat coding! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}