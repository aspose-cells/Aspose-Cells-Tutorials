---
category: general
date: 2026-07-14
description: Simpan Excel sebagai HTML dengan cepat dan pelajari cara mengonversi
  Excel ke HTML dengan format lengkap. Ekspor Excel dengan format menggunakan Aspose.Cells
  dalam hitungan menit.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: id
lastmod: 2026-07-14
og_description: Simpan Excel sebagai HTML secara instan. Panduan ini menunjukkan cara
  mengonversi Excel ke HTML sambil mempertahankan gaya dan mengaktifkan pemformatan
  angka Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Simpan Excel sebagai HTML – Ekspor Langkah demi Langkah dengan Format Lengkap
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Simpan Excel sebagai HTML – Panduan Lengkap Mengekspor Excel dengan Pemformatan
url: /id/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Save Excel as HTML – Panduan Lengkap untuk Mengekspor Excel dengan Pemformatan

Pernah bertanya-tanya bagaimana cara **menyimpan Excel sebagai HTML** tanpa kehilangan warna, batas, atau format angka? Anda bukan satu-satunya. Dalam banyak skenario pelaporan Anda memerlukan tampilan workbook yang siap untuk web, dan cara tercepat adalah mengekspor file langsung ke HTML.  

Dalam tutorial ini kami akan membahas langkah‑langkah tepat untuk **mengonversi Excel ke HTML** menggunakan Aspose.Cells, mengaktifkan pemformatan angka Grid.js, dan memastikan output terlihat persis seperti spreadsheet asli. Pada akhir tutorial Anda akan memiliki file HTML siap pakai yang dapat Anda sajikan dari server web mana pun.

## Apa yang Akan Anda Pelajari

- Prasyarat dan instalasi paket  
- Memuat workbook yang sudah ada (atau membuatnya secara dinamis)  
- Mengonfigurasi `HtmlSaveOptions` untuk kesetiaan visual yang sempurna  
- Mengaktifkan `GridJsOptions.EnableNumberFormat` untuk mempertahankan gaya numerik  
- Menyimpan file dan memverifikasi hasilnya  

Jika Anda pernah mencoba **mengekspor Excel dengan pemformatan** menggunakan dump CSV umum, Anda tahu betapa frustrasinya ketika angka berubah menjadi teks biasa. Panduan ini menghindari jebakan tersebut.

---

## Prasyarat – Siapkan Lingkungan Pengembangan Anda

Sebelum kita masuk ke kode, pastikan Anda memiliki:

| Persyaratan | Mengapa penting |
|-------------|-----------------|
| .NET 6.0 atau lebih baru (tutorial ini menggunakan .NET 6) | API modern dan kinerja yang lebih baik |
| Visual Studio 2022 (atau VS Code dengan ekstensi C#) | Pengeditan dan debugging yang nyaman |
| Paket NuGet Aspose.Cells untuk .NET | Pustaka yang menggerakkan `HtmlSaveOptions` dan `GridJsOptions` |
| File Excel contoh (`sample.xlsx`) atau workbook yang Anda buat dalam kode | Sumber yang akan Anda konversi |

Instal Aspose.Cells dengan perintah berikut di Package Manager Console:

```powershell
Install-Package Aspose.Cells
```

> **Tip Pro:** Jika Anda berada di pipeline CI, tambahkan baris `dotnet add package` yang sama ke skrip build Anda sehingga dependensi selalu ada.

## Langkah 1: Muat atau Buat Workbook

Anda dapat memuat file yang sudah ada atau membuatnya secara programatis. Berikut contoh minimal yang membuat workbook dengan beberapa sel bergaya sehingga Anda dapat melihat pemformatan tetap terjaga setelah ekspor.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Mengapa ini penting:** Dengan secara eksplisit mengatur format angka, Anda nanti akan melihat `GridJsOptions.EnableNumberFormat` mempertahankan format tersebut dalam output HTML.

## Langkah 2: Konfigurasikan Opsi Penyimpanan HTML

Sekarang kita membuat instance `HtmlSaveOptions`. Objek ini memberi tahu Aspose.Cells secara tepat bagaimana HTML harus dirender.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Mengaktifkan Pemformatan Angka Grid.js

Jika Anda berencana menyematkan HTML ke dalam halaman yang menggunakan **Grid.js** untuk tabel interaktif, Anda ingin angka tetap terformat (misalnya simbol mata uang, pemisah ribuan). Baris berikut melakukan hal itu secara tepat:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **Apa yang terjadi di balik layar?** `EnableNumberFormat` menyuntikkan potongan JavaScript kecil yang memberi tahu Grid.js untuk menginterpretasikan atribut `data-format` pada sel, mempertahankan pemformatan gaya Excel di browser.

## Langkah 3: Simpan Workbook sebagai File HTML

Dengan workbook siap dan opsi sudah disetel, baris terakhir menulis file HTML ke disk.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Menjalankan program menghasilkan file `gridjs.html` yang terlihat seperti ini (tampilan disederhanakan):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Buka file tersebut di browser apa pun dan Anda akan melihat tabel yang bergaya rapi, lengkap dengan latar belakang header abu‑abu muda dan pemformatan mata uang. Jika Anda menempatkan halaman ini ke situs yang sudah memuat Grid.js, angka akan otomatis ditampilkan dengan koma dan simbol yang tepat.

## Kesalahan Umum Saat Anda **Mengonversi Excel ke HTML**

| Masalah | Mengapa terjadi | Cara menghindarinya |
|---------|-----------------|---------------------|
| **Rumus hilang** | HTML bersifat statis; rumus menjadi nilai biasa. | Jika Anda memerlukan perhitungan langsung, simpan workbook di server dan gunakan pustaka JavaScript seperti SheetJS. |
| **Gambar hilang** | Gambar disimpan sebagai sumber terpisah. | Setel `HtmlSaveOptions.ExportImagesAsBase64 = true` untuk menyematkannya langsung. |
| **File besar** | Workbook besar menghasilkan HTML + JS yang sangat besar. | Gunakan `ExportOnlyVisibleSheets` atau bagi menjadi beberapa halaman melalui `HtmlSaveOptions.OnePagePerSheet`. |
| **Locale angka tidak tepat** | Excel menyimpan angka dalam budaya invarian, browser mungkin menerapkan pengaturan lokal. | Secara eksplisit setel `htmlOptions.Encoding = Encoding.UTF8` dan gunakan `GridJsOptions.EnableNumberFormat`. |

## Lanjutan: Mengekspor Beberapa Sheet dengan Instance Grid.js Individu

Jika workbook Anda berisi beberapa sheet dan Anda ingin masing‑masing menjadi tabel Grid.js sendiri, Anda dapat melakukan loop pada worksheet dan menyimpan masing‑masing secara terpisah:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Setiap file akan berisi elemen `<table class="gridjs-table">` masing‑masing, siap untuk manipulasi independen.

## Memverifikasi Output – Daftar Periksa Cepat

1. **Gaya tetap?** Bandingkan warna latar belakang sel dan batas dengan tampilan Excel asli.  
2. **Format angka terjaga?** Cari atribut `data-format` pada elemen `<td>`.  
3. **Gambar ditampilkan?** Jika Anda mengekspor gambar sebagai Base64, mereka harus muncul secara inline.  
4. **Konsol browser bersih?** Tidak ada error JavaScript terkait Grid.js.  

Jika salah satu pemeriksaan ini gagal, tinjau kembali properti `HtmlSaveOptions` yang bersangkutan—sebagian besar masalah berasal dari flag yang belum diaktifkan.

## Kesimpulan

Anda kini memiliki metode yang kuat dan siap produksi untuk **menyimpan Excel sebagai HTML** sambil mempertahankan setiap gaya, batas, dan representasi numerik. Dengan mengonfigurasi `HtmlSaveOptions` dan mengaktifkan `GridJsOptions.EnableNumberFormat`, Anda telah mengubah spreadsheet statis menjadi tabel yang ramah web dan berfungsi mulus dengan Grid.js.

Singkatnya, tutorial ini menunjukkan cara **mengonversi Excel ke HTML** dan **mengekspor Excel dengan pemformatan** menggunakan Aspose.Cells. Jangan ragu bereksperimen: coba tema berbeda, sematkan diagram, atau bahkan sajikan HTML melalui endpoint ASP.NET untuk konversi secara langsung.

## Apa Selanjutnya?

- **Jelajahi format ekspor lain**: PDF, PNG, atau CSV melalui `Workbook.Save`.  
- **Integrasikan dengan ASP.NET Core**: Kembalikan string HTML langsung dari aksi controller.  
- **Kombinasikan dengan SheetJS**: Muat kembali HTML yang dihasilkan ke dalam workbook JavaScript untuk penyuntingan sisi klien.  

Jika Anda mengalami kendala, tinggalkan komentar di bawah atau periksa dokumentasi Aspose.Cells untuk opsi konfigurasi yang lebih mendalam. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap yang berfungsi dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Export Excel to HTML with Grid Lines Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Export Excel to HTML Preserving Border Styles Using Aspose.Cells for Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Convert HTML to Excel Using Aspose.Cells .NET: A Comprehensive Guide](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}