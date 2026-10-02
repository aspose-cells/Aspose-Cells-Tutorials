---
category: general
date: 2026-01-14
description: Cara menyalin tabel pivot menggunakan Aspose.Cells dan juga belajar mengonversi
  Excel ke PPTX, menyalin rentang ke buku kerja lain, serta membuat kotak teks dapat
  diedit di PPTX dalam satu tutorial.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: id
og_description: Bagaimana menyalin tabel pivot dan kemudian mengonversi Excel ke PPTX,
  menyalin rentang ke buku kerja lain, serta membuat kotak teks dapat diedit di PPTX—semua
  dengan Aspose.Cells.
og_title: Cara Menyalin Pivot Table di C# – Panduan Lengkap Excel ke PPTX
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Cara Menyalin Pivot Table di C# – Mengonversi Excel ke PPTX, Menyalin Rentang
  & Membuat Kotak Teks Dapat Diedit
url: /id/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyalin Pivot Table di C# – Panduan Lengkap Excel ke PPTX

Menyalin pivot table dari satu workbook ke workbook lain adalah pertanyaan yang sering muncul saat Anda mengotomatisasi laporan berbasis Excel. Dalam tutorial ini kami akan membahas tiga skenario dunia nyata menggunakan **Aspose.Cells for .NET**: menyalin rentang pivot‑table, mengekspor worksheet ke file PPTX dengan textbox yang dapat diedit, dan mengisi satu sel dengan array JSON melalui Smart Markers.  

Anda juga akan melihat cara **mengonversi Excel ke PPTX**, **menyalin rentang ke workbook lain**, dan **membuat textbox PPTX dapat diedit** tanpa merusak format apa pun. Pada akhir tutorial Anda akan memiliki basis kode siap‑jalankan yang dapat Anda masukkan ke proyek .NET mana pun.

> **Pro tip:** Semua contoh menargetkan Aspose.Cells 23.12, tetapi konsep yang sama berlaku untuk versi sebelumnya dengan sedikit penyesuaian API.

![Diagram showing how a pivot table is copied, a worksheet exported to PPTX, and a JSON array inserted – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## Apa yang Anda Butuhkan

- Visual Studio 2022 (atau IDE C# apa pun)
- .NET 6.0 atau runtime yang lebih baru
- Paket NuGet Aspose.Cells for .NET  
  ```bash
  dotnet add package Aspose.Cells
  ```
- Dua file Excel contoh (`source.xlsx`, `chartWithTextbox.xlsx`) yang ditempatkan di folder yang Anda kontrol (ganti `YOUR_DIRECTORY` dengan path aktual Anda).

Tidak ada pustaka tambahan yang diperlukan; assembly `Aspose.Cells` yang sama menangani Excel, PPTX, dan Smart Markers.

---

## Cara Menyalin Pivot Table dan Mempertahankan Datanya

Saat Anda menyalin rentang yang berisi pivot table, perilaku default adalah menempel hanya **nilai**. Untuk mempertahankan definisi pivot tetap utuh, Anda harus mengaktifkan flag `CopyPivotTable`.

### Langkah‑per‑Langkah

1. **Muat workbook sumber** yang berisi pivot table.  
2. **Buat workbook tujuan kosong** – ini akan menerima rentang yang disalin.  
3. **Gunakan `CopyRange` dengan `CopyPivotTable = true`** sehingga definisi pivot ikut disalin bersama data.  
4. **Simpan file tujuan** di lokasi yang Anda inginkan.

#### Contoh Kode Lengkap

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Mengapa ini berhasil:**  
`CopyOptions.CopyPivotTable` memberi tahu Aspose.Cells untuk menggandakan objek `PivotTable` yang mendasarinya, bukan hanya nilai yang sudah dirender. Workbook tujuan kini berisi pivot yang sepenuhnya berfungsi dan dapat Anda refresh atau modifikasi secara programatis.

**Edge case:** Jika workbook sumber menggunakan sumber data eksternal, Anda mungkin perlu menyematkan data atau menyesuaikan string koneksi setelah menyalin, jika tidak pivot akan menampilkan “#REF!”.

---

## Konversi Excel ke PPTX dan Buat Textbox Dapat Diedit

Mengekspor worksheet ke PowerPoint sangat berguna untuk membuat deck slide langsung dari data. Secara default textbox yang diekspor menjadi bentuk statis, tetapi mengatur `IsTextBoxEditable` mengubah perilaku tersebut.

### Langkah‑per‑Langkah

1. **Buka workbook** yang berisi chart dan textbox yang ingin Anda ekspor.  
2. **Konfigurasikan `ImageOrPrintOptions`** dengan `SaveFormat = SaveFormat.Pptx`.  
3. **Tentukan area cetak** yang mencakup textbox.  
4. **Aktifkan `IsTextBoxEditable`** sehingga teks dapat diedit setelah PPTX dibuka.  
5. **Simpan file PPTX**.

#### Contoh Kode Lengkap

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Result:** Buka `result.pptx` di PowerPoint – textbox yang Anda tempatkan di Excel kini menjadi textbox biasa yang dapat Anda ketik di dalamnya. Tidak perlu membuatnya kembali secara manual.

**Common pitfall:** Jika worksheet berisi sel yang digabung dan area cetak memotongnya, slide yang dihasilkan dapat bergeser. Sesuaikan area cetak atau pisahkan sel sebelum mengekspor.

---

## Salin Rentang ke Workbook Lain dengan Smart Markers (JSON → Sel Tunggal)

Terkadang Anda perlu menyematkan array JSON ke dalam satu sel Excel, misalnya saat mengirim data ke sistem downstream yang mengharapkan string JSON. Smart Markers Aspose.Cells dapat menyerialisasi array sebagai satu sel ketika Anda mengatur `ArrayAsSingle = true`.

### Langkah‑per‑Langkah

1. **Muat workbook template** yang berisi placeholder Smart Marker (misalnya `&=Items.Name`).  
2. **Siapkan objek data** – tipe anonim dengan array `Items`.  
3. **Buat `SmartMarkerProcessor`** dan terapkan data dengan `ArrayAsSingle`.  
4. **Simpan workbook yang telah terisi**.

#### Contoh Kode Lengkap

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Explanation:**  
Ketika `ArrayAsSingle` bernilai true, Aspose.Cells menggabungkan setiap elemen `Items.Name` menjadi string bergaya JSON (`["A","B"]`) dan menuliskannya ke sel yang memuat smart marker. Ini menghindari pembuatan baris terpisah untuk setiap elemen array.

**When to use:** Ideal untuk mengekspor tabel konfigurasi, payload API, atau skenario apa pun di mana konsumen mengharapkan string JSON yang kompak daripada tata letak tabular.

---

## Tips Tambahan & Penanganan Edge‑Case

| Scenario | What to Watch For | Suggested Fix |
|----------|-------------------|---------------|
| **Large Pivot Tables** | Memory usage spikes when copying huge pivot caches. | Use `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` before loading. |
| **Exporting to PPTX with Images** | Images may be rasterized at low DPI. | Set `pptxOptions.ImageResolution = 300` for sharper slides. |
| **Smart Marker JSON Formatting** | Special characters (`"` , `\`) break JSON. | Escape them manually or use `JsonSerializer` to pre‑serialize before feeding Smart Markers. |
| **Copy Range across Different Excel Versions** | Older `.xls` files may lose formatting. | Save the destination as `.xlsx` to preserve modern features. |

---

## Ringkasan – Cara Menyalin Pivot Table dan Lebih Banyak Lagi

Kami memulai dengan menjawab **cara menyalin pivot table** sambil mempertahankan fungsionalitasnya, kemudian menunjukkan **cara mengonversi Excel ke PPTX**, **membuat textbox PPTX dapat diedit**, dan akhirnya **cara menyalin rentang ke workbook lain** menggunakan Smart Markers untuk menyematkan array JSON sebagai satu sel.  

Ketiga potongan kode tersebut berdiri sendiri; Anda dapat menempelkannya ke aplikasi console baru, menyesuaikan path file, dan menjalankannya hari ini.

---

## Apa Selanjutnya?

- **Jelajahi format ekspor lain** – Aspose.Cells juga mendukung PDF, XPS, dan HTML.  
- **Refresh pivot table secara programatis** menggunakan `PivotTable.RefreshData()` setelah menyalin.  
- **Gabungkan Smart Markers dengan chart** untuk menghasilkan dashboard dinamis yang memperbarui secara otomatis.  

Jika Anda tertarik pada **menyimpan workbook sebagai PPTX** dengan tata letak slide khusus, lihat dokumentasi Aspose.Cells tentang `SlideOptions`.  

Silakan bereksperimen—ganti area cetak, coba `CopyOptions` yang berbeda, atau berikan payload JSON yang lebih kompleks. API cukup fleksibel untuk sebagian besar pipeline pelaporan.

---

### Pertanyaan yang Sering Diajukan

**Q: Apakah `CopyPivotTable` juga menyalin slicer?**  
A: Tidak secara langsung. Slicer adalah objek terpisah; setelah menyalin Anda perlu membuatnya kembali atau menyalinnya melalui koleksi `Worksheet.Shapes`.

**Q: Bisakah saya mengekspor beberapa worksheet ke satu deck PPTX?**  
A: Ya. Lakukan loop pada setiap worksheet, panggil `Save` dengan `ImageOrPrintOptions` yang sama, dan atur `pptxOptions.StartSlideNumber` untuk melanjutkan penomoran.

**Q: Bagaimana jika array JSON saya berisi objek bersarang?**  
A: Atur `ArrayAsSingle = false` dan gunakan template khusus yang melakukan iterasi pada

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}