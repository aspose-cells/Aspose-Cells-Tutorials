---
category: general
date: 2026-02-26
description: Terapkan format angka di Excel dengan cepat dan pelajari cara memformat
  kolom sebagai mata uang, mengatur format angka kolom, serta mengatur warna font
  kolom hanya dalam beberapa baris C#.
draft: false
keywords:
- apply number format excel
- format column as currency
- set column number format
- format currency column
- set column font color
language: id
og_description: Terapkan format angka Excel di C# dengan langkah mudah. Pelajari cara
  memformat kolom sebagai mata uang, mengatur format angka kolom, dan mengatur warna
  font kolom untuk spreadsheet profesional.
og_title: Menerapkan Format Angka di Excel – Panduan Lengkap untuk Styling Kolom
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: Menerapkan Format Angka di Excel – Panduan Langkah demi Langkah untuk Memformat
  Kolom
url: /id/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/
---

, Cherry) are product names; keep as is.

Also bullet list items after "Expected Output" are sentences; translate.

Also other bullet lists.

Make sure to keep markdown formatting.

Let's produce final translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# apply number format excel – Cara Mengatur Gaya Kolom Excel di C#

Pernah bertanya-tanya bagaimana cara **apply number format excel** saat Anda sudah melakukan looping melalui `DataTable`? Anda tidak sendirian. Kebanyakan pengembang menemui kendala ketika mereka membutuhkan header berwarna biru *dan* kolom dengan format mata uang dalam satu operasi impor yang sama. Kabar baiknya? Dengan beberapa baris C# dan objek style yang tepat, Anda dapat melakukannya tanpa harus memproses sheet setelahnya.

Dalam tutorial ini kita akan membahas contoh lengkap yang dapat dijalankan, yang menunjukkan cara **format column as currency**, **set column number format** untuk kolom lain, dan bahkan **set column font color** untuk header. Pada akhir tutorial Anda akan memiliki pola yang dapat dipakai ulang dan disisipkan ke proyek Aspose.Cells (atau serupa) mana pun.

## Apa yang Akan Anda Pelajari

- Cara mengambil `DataTable` dan memetakan setiap kolom ke `Style` tertentu.
- Langkah‑langkah tepat untuk **apply number format excel** menggunakan `Worksheet.Cells.ImportDataTable`.
- Mengapa membuat style di awal lebih efisien daripada memformat sel satu per satu.
- Penanganan kasus tepi ketika tabel sumber memiliki lebih banyak kolom daripada yang Anda beri style.
- Contoh kode lengkap yang siap disalin‑tempel dan dapat dijalankan hari ini.

> **Prasyarat:** Panduan ini mengasumsikan Anda memiliki Aspose.Cells untuk .NET (atau perpustakaan apa pun yang menyediakan API `Workbook`, `Worksheet`, `Style`) yang sudah direferensikan dalam proyek Anda. Jika Anda menggunakan perpustakaan lain, konsepnya tetap sama—cukup ganti nama tipe yang bersangkutan.

---

## Langkah 1: Ambil Data Sumber sebagai DataTable

Sebelum styling apa pun dapat dilakukan, Anda memerlukan data mentah. Pada kebanyakan skenario dunia nyata data berada di basis data, CSV, atau API. Untuk kejelasan kita akan membuat mock `DataTable` sederhana dengan dua kolom: *Product* (string) dan *Price* (decimal).

```csharp
using System;
using System.Data;
using Aspose.Cells;
using System.Drawing;

public static DataTable GetData()
{
    var dt = new DataTable();
    dt.Columns.Add("Product", typeof(string));
    dt.Columns.Add("Price", typeof(decimal));

    dt.Rows.Add("Apple", 1.25m);
    dt.Rows.Add("Banana", 0.75m);
    dt.Rows.Add("Cherry", 2.10m);

    return dt;
}
```

> **Mengapa ini penting:** Mengambil data ke dalam `DataTable` memberi Anda representasi tabel dalam memori yang dapat langsung dikonsumsi oleh `ImportDataTable`, menghilangkan kebutuhan untuk memasukkan sel satu per satu secara manual.

## Langkah 2: Buat Array Style – Satu untuk Setiap Kolom

Overload `ImportDataTable` yang akan kita gunakan menerima array objek `Style`. Setiap entri berkorespondensi dengan indeks kolom. Jika Anda membiarkan entri menjadi `null`, kolom tersebut akan mewarisi style default workbook.

```csharp
// Initialize the workbook (Aspose.Cells)
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Prepare the style array based on the number of columns
DataTable dataTable = GetData();
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

> **Tips pro:** Mendeklarasikan array *setelah* Anda memiliki `DataTable` memastikan ukuran array cocok persis, sehingga mencegah `IndexOutOfRangeException` nantinya.

## Langkah 3: Atur Warna Font Kolom (Biru) untuk Kolom Pertama

Permintaan umum adalah menyorot header atau kolom kunci dengan warna font yang berbeda. Di sini kita membuat teks kolom pertama berwarna biru.

```csharp
// Style for the first column – blue font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = Color.Blue;
```

> **Mengapa menggunakan objek style?** Style dapat dipakai ulang dan diterapkan secara massal, yang jauh lebih cepat dibanding iterasi setiap sel setelah impor. Workbook menyimpan cache style sekali, lalu menggunakan kembali untuk setiap sel di kolom tersebut.

## Langkah 4: Format Kolom Kedua sebagai Mata Uang

Format angka bawaan Excel diidentifikasi dengan indeks. `14` berkorespondensi dengan format mata uang default (misalnya `$1,234.00`). Jika Anda memerlukan format khusus, Anda dapat menetapkan string format sebagai gantinya.

```csharp
// Style for the second column – built‑in currency format (ID 14)
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].Number = 14; // 14 = built‑in currency format
```

> **Kasus tepi:** Jika workbook Anda menggunakan locale di mana simbol mata uang bukan `$`, indeks yang sama akan menyesuaikan secara otomatis (misalnya `€` untuk locale Jerman).

## Langkah 5: Impor DataTable dengan Style yang Sudah Didefinisikan

Sekarang kita gabungkan semuanya. Metode `ImportDataTable` akan menempelkan data mulai dari sel `A1` (baris 0, kolom 0) dan menerapkan style yang telah kita siapkan.

```csharp
// Import the DataTable into the worksheet, applying the column styles
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

- Parameter kedua `true` memberi tahu Aspose.Cells untuk memperlakukan baris pertama `DataTable` sebagai header kolom.
- Koordinat `0, 0` menentukan sudut kiri‑atas tempat impor dimulai.
- `columnStyles` memetakan setiap kolom ke style masing‑masing.

## Langkah 6: Simpan Workbook (Opsional, tapi Berguna untuk Verifikasi)

Jika Anda ingin melihat hasilnya di Excel, cukup simpan workbook ke disk. Langkah ini tidak diperlukan untuk logika styling, tetapi berguna untuk debugging.

```csharp
// Save the workbook to a file
workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved as StyledReport.xlsx");
```

### Output yang Diharapkan

| **Produk** (font biru) | **Harga** (mata uang) |
|------------------------|-----------------------|
| Apple                  | $1.25                 |
| Banana                 | $0.75                 |
| Cherry                 | $2.10                 |

- Kolom *Produk* muncul dengan font biru, sehingga menonjol.
- Kolom *Harga* menampilkan nilai dengan simbol mata uang default dan dua digit desimal.

---

## Pertanyaan yang Sering Diajukan & Variasi

### Bagaimana cara **set column number format** untuk lebih dari dua kolom?

Cukup perpanjang array `columnStyles`. Misalnya, untuk menampilkan persentase di kolom ketiga:

```csharp
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Number = 10; // 10 = built‑in percentage format
```

### Bagaimana jika saya membutuhkan format mata uang *kustom*, seperti “USD 1,234.00”?

Ganti properti `Number` dengan string format:

```csharp
columnStyles[1].Custom = "\"USD\" #,##0.00";
```

### Bisakah saya menerapkan **set column font color** ke kolom numerik tanpa memengaruhi format angkanya?

Tentu saja. Style dapat digabungkan. Anda dapat mengatur baik `Font.Color` maupun `Number` pada instance `Style` yang sama:

```csharp
columnStyles[3] = workbook.CreateStyle();
columnStyles[3].Font.Color = Color.Green;
columnStyles[3].Number = 2; // 2 = built‑in date format (just an example)
```

### Apa yang terjadi jika `DataTable` memiliki lebih banyak kolom daripada style?

Setiap kolom tanpa style eksplisit (`null`) akan mewarisi style default workbook. Untuk menghindari `null` yang tidak disengaja, Anda dapat menginisialisasi seluruh array dengan style dasar terlebih dahulu:

```csharp
Style defaultStyle = workbook.CreateStyle();
defaultStyle.Font.Size = 11;
for (int i = 0; i < columnStyles.Length; i++)
    columnStyles[i] = defaultStyle;
```

Lalu timpa hanya kolom yang Anda perlukan.

### Apakah pendekatan ini bekerja dengan set data besar (10rb+ baris)?

Ya. Karena styling diterapkan *sekali per kolom* sebelum impor, operasi tetap O(N) terhadap baris, dan penggunaan memori tetap rendah. Hindari looping setiap sel setelah impor—di situlah performa menurun.

---

## Contoh Lengkap yang Dapat Dijalankan (Copy‑Paste Ready)

```csharp
using System;
using System.Data;
using System.Drawing;
using Aspose.Cells;

class ExcelStyler
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 3️⃣ Prepare style array (one per column)
        Style[] columnStyles = new Style[dataTable.Columns.Count];

        // 4️⃣ Style first column – blue font
        columnStyles[0] = workbook.CreateStyle();
        columnStyles[0].Font.Color = Color.Blue;

        // 5️⃣ Style second column – built‑in currency format (ID 14)
        columnStyles[1] = workbook.CreateStyle();
        columnStyles[1].Number = 14;

        // 6️⃣ (Optional) Add more styles here – e.g., percentage, custom formats

        // 7️⃣ Import the DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // 8️⃣ Save to file for verification
        workbook.Save("StyledReport.xlsx", SaveFormat.Xlsx);
        Console.WriteLine("Excel file created: StyledReport.xlsx");
    }

    // Helper method to mock data
    public static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Price", typeof(decimal));

        dt.Rows.Add("Apple", 1.25m);
        dt.Rows.Add("Banana", 0.75m);
        dt.Rows.Add("Cherry", 2.10m);
        return dt;
    }
}
```

Jalankan program, buka `StyledReport.xlsx`, dan Anda akan langsung melihat hasil **apply number format excel**.

---

## Kesimpulan

Kami baru saja mendemonstrasikan cara bersih dan efisien untuk **apply number format excel** pada `DataTable` yang diimpor. Dengan menyiapkan array `Style[]` di awal, Anda dapat **format column as currency**, **set column number format**, dan **set column font color** dalam satu pemanggilan—tanpa perlu pemrosesan pasca‑impor.

Silakan kembangkan pola ini: tambahkan styling kondisional, gabungkan sel untuk heading, atau bahkan sisipkan formula. Prinsip yang sama tetap berlaku, menjaga kode Anda tetap rapi dan spreadsheet terlihat profesional.

---

### Apa Selanjutnya?

- Jelajahi **conditional formatting** untuk menyorot nilai yang melebihi ambang tertentu.
- Gabungkan teknik ini dengan **pivot table generation** untuk pelaporan dinamis.
- Coba **set column number format** untuk tanggal, persentase, atau notasi ilmiah khusus.

Ada trik lain yang Anda coba? Bagikan di komentar—mari kita terus berbagi.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}