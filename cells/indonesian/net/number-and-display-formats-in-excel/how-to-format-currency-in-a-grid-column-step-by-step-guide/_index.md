---
category: general
date: 2026-02-15
description: cara memformat mata uang dengan cepat menggunakan set column number format
  dan menerapkan format numerik khusus di C#. pelajari cara mengambil kolom berdasarkan
  nama dan mengatur perataan kolom grid.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: id
og_description: cara memformat mata uang di kolom grid menggunakan C#. tutorial ini
  menunjukkan cara mengambil kolom berdasarkan nama, mengatur format angka kolom,
  menerapkan format numerik khusus, dan mengatur perataan kolom grid.
og_title: Cara memformat mata uang di Kolom Grid – Panduan Lengkap
tags:
- C#
- GridFormatting
- UI
title: Cara memformat mata uang di Kolom Grid – Panduan Langkah demi Langkah
url: /id/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cara memformat mata uang di Kolom Grid – Tutorial Pemrograman Lengkap

Pernah bertanya-tanya **bagaimana cara memformat mata uang** di kolom grid tanpa membuat rambut Anda rontok? Anda bukan satu-satunya. Ketika Anda melihat angka biasa seperti `1234.5` dan berharap angka tersebut secara ajaib muncul sebagai `$1,234.50`, jawabannya biasanya hanya beberapa baris konfigurasi.  

Dalam panduan ini kami akan **mengambil kolom berdasarkan nama**, **mengatur format angka kolom**, dan **menerapkan format numerik khusus** yang menghormati tata letak akuntansi standar. Sepanjang jalan kami juga akan **mengatur perataan kolom grid** dan menambahkan border halus agar UI terlihat rapi.

> **TL;DR** – Pada akhirnya Anda akan memiliki potongan kode siap‑jalankan yang mengubah desimal mentah menjadi nilai mata uang yang diformat indah di dalam kontrol bergaya `GridJs` apa pun.

---

## Apa yang Anda Butuhkan

- Proyek .NET (versi apa pun yang mendukung C# 8.0+ – Visual Studio 2022 bekerja dengan baik).  
- Komponen grid yang menyediakan koleksi `Columns` (contoh ini menggunakan kelas fiktif `GridJs`, tetapi konsepnya dapat diterapkan pada grid DevExpress, Telerik, atau Syncfusion).  
- Familiaritas dasar dengan sintaks C# – tidak memerlukan trik lanjutan.

Jika Anda sudah memiliki semuanya, bagus. Jika belum, cukup buat aplikasi console; grid dapat dimock untuk ilustrasi.

---

## Implementasi Langkah‑per‑Langkah

Di bawah setiap langkah Anda akan melihat blok kode ringkas, penjelasan singkat tentang **mengapa** baris tersebut penting, dan tip untuk menghindari jebakan umum.

### ## Langkah 1 – Mengambil kolom “Amount” berdasarkan nama

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Mengapa ini penting:**  
Sebagian besar API grid mengekspor kolom melalui indeks mirip kamus. Mengambil kolom berdasarkan nama headernya (`"Amount"`) memungkinkan Anda memanipulasi tampilannya tanpa menyentuh sumber data yang mendasarinya.  

**Tip Pro:** Selalu lindungi terhadap pengembalian `null` – kesalahan pengetikan pada nama kolom atau perubahan skema dinamis dapat menyebabkan `NullReferenceException` pada runtime.

---

### ## Langkah 2 – Mengatur format angka kolom menggunakan mask mata uang khusus

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Mengapa ini penting:**  
String format mengikuti konvensi format akuntansi Excel:

- `_(* #,##0.00_)` → Angka positif, rata kanan dengan spasi di depan untuk simbol mata uang.  
- `_(* (#,##0.00)` → Angka negatif dibungkus dalam tanda kurung.  
- `_(* \"-\"??_)` → Nilai nol ditampilkan sebagai tanda hubung.  
- `_(@_)` → Nilai teks tetap tidak berubah.

Menggunakan **apply custom numeric format** memberi Anda kontrol penuh atas pemisah ribuan, tempat desimal, dan penempatan simbol mata uang.  

**Kasus khusus:** Jika aplikasi Anda perlu menghormati locale yang berbeda (mis., Euro alih-alih USD), ganti spasi di depan dengan simbol yang sesuai atau gunakan format yang memperhatikan `CultureInfo` di sumber data.

---

### ## Langkah 3 – Menyelaraskan isi kolom ke kanan untuk keterbacaan

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Mengapa ini penting:**  
Nilai mata uang lebih mudah dipindai ketika mereka berbaris pada pemisah desimal. Mengatur **set grid column alignment** ke `Right` meniru cara spreadsheet menampilkan data keuangan.  

**Catatan:** Beberapa grid mengabaikan perataan pada sel yang berisi templat khusus. Jika Anda melihat perataan tidak berpengaruh, periksa kembali bahwa kolom tidak menggunakan renderer sel khusus.

---

### ## Langkah 4 – Menambahkan border abu-abu tipis di sekitar sel kolom

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Mengapa ini penting:**  
Border halus memisahkan kolom “Amount” dari tetangganya, terutama ketika grid memiliki warna baris bergantian. Ini menjadi petunjuk visual bahwa data tersebut mewakili angka keuangan yang terpisah.  

**Tip:** Jika Anda memerlukan garis yang lebih tebal untuk keperluan pencetakan, ubah `BorderLineStyle` menjadi `Medium` atau ubah `Color` menjadi `Color.Black`.

---

## Contoh Lengkap yang Berfungsi

Berikut seluruh potongan kode yang dapat Anda sisipkan ke dalam proyek WinForms atau WPF yang menggunakan kontrol bergaya `GridJs`. Contoh ini juga mencetak nilai yang diformat ke konsol sehingga Anda dapat memverifikasi output tanpa UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Output konsol yang diharapkan**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Perhatikan bagaimana angka positif rata kanan, angka negatif muncul dalam tanda kurung, dan nol ditampilkan sebagai tanda hubung – persis seperti yang ditentukan oleh string format khusus.

---

## Pertanyaan yang Sering Diajukan & Kasus Khusus

| Pertanyaan | Jawaban |
|----------|--------|
| *Bagaimana jika grid menggunakan budaya yang berbeda (mis., € alih-alih $)?* | Ganti spasi di depan dalam string format dengan simbol yang diinginkan atau biarkan sumber data menghasilkan string yang sudah diformat menggunakan `CultureInfo.CurrentCulture`. |
| *Apakah saya dapat menggunakan kembali format yang sama untuk beberapa kolom?* | Tentu saja. Simpan string format dalam sebuah konstanta (`const string CurrencyMask = "...";`) dan tetapkan di mana pun Anda membutuhkan mata uang. |
| *Apa yang terjadi jika kolom berisi nilai string?* | String format hanya memengaruhi tipe numerik. String melewati tanpa perubahan, itulah mengapa bagian terakhir dari mask (`_(@_)`) ada – ia mempertahankan konten non‑numerik. |
| *Apakah ada dampak kinerja?* | Sangat kecil. Format diterapkan pada saat render, bukan saat pengambilan data. Kecuali Anda merender ribuan baris per frame, Anda tidak akan merasakan perlambatan. |
| *Bagaimana cara membuat border lebih tebal untuk laporan cetak?* | Ganti `BorderLineStyle.Thin` dengan `BorderLineStyle.Medium` atau `BorderLineStyle.Thick`. Beberapa pustaka juga memungkinkan Anda menentukan lebar piksel secara langsung. |

---

## Kesimpulan

Kami telah membahas **cara memformat mata uang** di kolom grid dari awal hingga akhir: mengambil kolom berdasarkan nama, mengatur format angka kolom, menerapkan format numerik khusus, meratakan sel, dan menambahkan border yang elegan. Contoh lengkap dapat dijalankan langsung dan menunjukkan hasil visual yang tepat yang dapat Anda harapkan.

Jika Anda siap melanjutkannya, coba:

- **Dynamic cultures** – ubah string format berdasarkan locale pengguna.  
- **Conditional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}