---
category: general
date: 2026-03-27
description: Cara membuat pivot di C# menggunakan Aspose.Cells – pelajari cara menambahkan
  data, mengaktifkan penyegaran, dan menyimpan workbook sebagai xlsx dalam satu tutorial.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: id
og_description: Cara membuat pivot di C# dengan Aspose.Cells. Panduan ini menunjukkan
  cara menambahkan data, mengaktifkan penyegaran, dan menyimpan buku kerja sebagai
  xlsx.
og_title: Cara Membuat Pivot di C# – Tutorial Lengkap Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cara Membuat Pivot di C# – Panduan Lengkap dengan Aspose.Cells
url: /id/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Pivot di C# – Tutorial Lengkap Aspose.Cells

Pernah bertanya‑tanya **cara membuat pivot** di C# tanpa harus berurusan dengan COM interop? Anda tidak sendirian. Dalam banyak aplikasi berbasis data, kita membutuhkan cara cepat untuk mengubah data penjualan mentah menjadi rangkuman yang rapi, dan Aspose.Cells menjadikannya sangat mudah.  

Dalam tutorial ini kami akan membahas setiap langkah: menambahkan data, membangun tabel pivot, mengaktifkan penyegaran otomatis, dan akhirnya **menyimpan workbook sebagai xlsx** sehingga pengguna Anda dapat langsung membukanya di Excel. Pada akhir tutorial Anda akan memiliki file `PivotRefresh.xlsx` yang siap pakai dan pemahaman yang kuat mengapa setiap baris kode penting.

## Prasyarat

- .NET 6+ (atau .NET Framework 4.7.2 ke atas) – semua runtime terbaru dapat digunakan.  
- Aspose.Cells untuk .NET – dapat diunduh dari NuGet (`Install-Package Aspose.Cells`).  
- Familiaritas dasar dengan sintaks C# – tidak diperlukan pengetahuan mendalam tentang Excel.

> **Tips pro:** Jika Anda menggunakan mesin perusahaan, pastikan lisensi Aspose sudah diterapkan; jika tidak, file yang dihasilkan akan memiliki watermark.

## Langkah 1 – Cara Menambahkan Data ke Workbook Baru

Sebelum pivot dapat dibuat, harus ada tabel sumber. Kami akan membuat workbook baru, menamai lembar kerja pertama *SalesData*, dan menambahkan beberapa baris yang meniru data penjualan dunia nyata.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Mengapa ini penting:**  
- Menggunakan `PutValue` secara otomatis menetapkan tipe sel, sehingga Anda tidak perlu khawatir tentang ketidaksesuaian string vs numerik di kemudian hari.  
- Menetapkan header pada baris 1 memberi mesin pivot sesuatu untuk direferensikan ketika Anda memetakan bidang.

## Langkah 2 – Membuat Worksheet yang Akan Menampung Tabel Pivot

Tabel pivot berada di lembar terpisah, menjaga data sumber tetap bersih dan laporan tetap rapi.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **Bagaimana jika Anda sudah memiliki lembar?** Cukup referensikan dengan indeks (`workbook.Worksheets["MySheet"]`) alih‑alih menambahkan lembar baru.

## Langkah 3 – Menentukan Rentang Sumber (Cara Menambahkan Data → Menentukan Rentang)

Aspose.Cells membutuhkan `CellArea` atau string rentang yang mencakup header dan data. Di sini kami mengasumsikan maksimum 100 baris; sesuaikan sesuai kebutuhan.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Kasus tepi:** Jika kumpulan data Anda bersifat dinamis, Anda dapat menghitung baris terakhir yang digunakan dengan `salesDataSheet.Cells.MaxDataRow` dan membangun rentang secara otomatis.

## Langkah 4 – Cara Membuat Pivot – Menyisipkan Tabel Pivot

Sekarang bagian yang menyenangkan: kami memberi tahu Aspose.Cells untuk membuat pivot yang terhubung ke rentang yang baru saja kami tetapkan.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Perhatikan referensi gaya formula (`=SalesData!A1:D100`). Itu adalah sintaks yang sama seperti yang Anda ketik di Excel, sehingga API terasa intuitif.

## Langkah 5 – Mengonfigurasi Field Baris, Kolom, dan Data (Cara Menambahkan Data → Fields)

Kami akan menempatkan *Region* pada baris, *Product* pada kolom, dan menjumlahkan baik *Units* maupun *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**Mengapa indeks ini?**  
Aspose.Cells mengindeks kolom mulai dari 0, sehingga `0` mengacu pada *Region*. Metode `DataFields.Add` memungkinkan Anda memberi nama ulang field (misalnya “Sum of Units”) dan memilih tipe agregasi – `Sum` adalah yang paling umum untuk data numerik.

## Langkah 6 – Cara Mengaktifkan Penyegaran – Membuat Pivot Otomatis Diperbarui saat Dibuka

Jika data sumber berubah nanti, Anda mungkin ingin pivot mencerminkan perubahan tersebut secara otomatis. Di sinilah `RefreshDataOnOpen` berperan.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Catatan:** Flag ini hanya berfungsi ketika workbook dibuka di Excel; ia tidak akan menghitung ulang di dalam Aspose.Cells kecuali Anda memanggil `pivotTable.RefreshData()` secara manual.

## Langkah 7 – Menyimpan Workbook sebagai XLSX (Cara Menyimpan Workbook sebagai XLSX)

Akhirnya, kami menyimpan file ke disk. Format `.xlsx` adalah tipe file Excel modern berbasis zip yang dapat bekerja di mana saja.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Menjalankan program menghasilkan file bernama **PivotRefresh.xlsx** di folder eksekusi. Buka di Excel dan Anda akan melihat pivot yang tertata rapi dengan baris *Region*, kolom *Product*, serta nilai *Units* dan *Revenue* yang dijumlahkan. Karena kami mengaktifkan penyegaran, setiap perubahan yang Anda buat pada lembar *SalesData* akan otomatis memperbarui pivot pada saat berikutnya workbook dibuka.

### Output yang Diharapkan

| Region | Widget | Gadget | … |
|--------|--------|--------|---|
| East   | 120    | 0      |   |
| West   | 0      | 85     |   |
| **Grand Total** | **120** | **85** |   |

*(Angka akan bervariasi tergantung pada baris yang Anda tambahkan.)*

---

## Pertanyaan Umum & Variasi

### Bagaimana jika saya membutuhkan beberapa tabel pivot?

Anda dapat mengulangi **Langkah 4** dengan nama dan lokasi yang berbeda. Setiap pemanggilan `PivotTables.Add` mengembalikan indeks baru yang dapat Anda gunakan untuk mengambil objek tabel.

### Bagaimana cara mengubah agregasi menjadi *Average* alih‑alih *Sum*?

Ganti `PivotTableDataAggregationType.Sum` dengan `PivotTableDataAggregationType.Average` pada pemanggilan `DataFields.Add`.

### Bisakah saya menata pivot (font, warna)?

Ya. Setelah pivot dibuat, Anda dapat mengakses properti `Style`‑nya atau menerapkan pemformatan sel pada rentang yang berisi pivot. Contohnya:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### Apakah memungkinkan menambahkan baris lagi setelah workbook disimpan?

Tentu saja. Muat file dengan `new Workbook("PivotRefresh.xlsx")`, tambahkan baris ke lembar *SalesData*, dan panggil `pivotTable.RefreshData()` sebelum menyimpan kembali.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Simpan file, jalankan, dan buka **PivotRefresh.xlsx** yang dihasilkan – Anda baru saja menguasai **cara membuat pivot** di C#.

---

## Penutup

Kami telah membahas **cara membuat pivot** secara programatis, cara **menambahkan data**, cara **mengaktifkan penyegaran**, dan akhirnya cara **menyimpan workbook sebagai xlsx** menggunakan Aspose.Cells. Kode

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}