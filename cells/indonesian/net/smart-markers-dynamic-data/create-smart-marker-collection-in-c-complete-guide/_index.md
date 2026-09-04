---
category: general
date: 2026-02-23
description: Buat koleksi smart marker dengan cepat dan pelajari cara mendefinisikan
  variabel diskon untuk formula dinamis. Contoh C# langkah demi langkah dengan kode
  lengkap.
draft: false
keywords:
- create smart marker collection
- define discount variable
- smart markers Aspose.Cells
- worksheet formulas C#
- dynamic discount calculation
language: id
og_description: Buat koleksi smart marker di C# dan definisikan variabel diskon untuk
  formula Excel yang dinamis. Pelajari solusi lengkap yang dapat dijalankan.
og_title: Buat Koleksi Penanda Pintar – Tutorial Lengkap C#
tags:
- C#
- Aspose.Cells
- Excel automation
title: Buat Koleksi Penanda Pintar di C# – Panduan Lengkap
url: /id/net/smart-markers-dynamic-data/create-smart-marker-collection-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat Koleksi Smart Marker – Tutorial Lengkap C#

Pernahkah Anda perlu **create smart marker collection** dalam spreadsheet tetapi tidak yakin harus mulai dari mana? Anda bukan satu-satunya—banyak pengembang mengalami hambatan yang sama ketika mereka mencoba menyisipkan variabel dan formula ke dalam lembar kerja Excel secara programatis.  

Berita baik? Dalam panduan ini kami akan menunjukkan secara tepat cara **create smart marker collection** dan juga **define discount variable** sehingga sel Anda menghitung diskon secara langsung. Pada akhir tutorial Anda akan memiliki contoh C# siap‑jalankan yang dapat Anda masukkan ke dalam proyek Aspose.Cells mana pun.

## Apa yang Dibahas dalam Tutorial Ini

Kami akan membahas setiap langkah—dari menginisialisasi `MarkerCollection` hingga menerapkannya pada sebuah worksheet. Anda akan melihat mengapa setiap baris penting, cara menangani kasus tepi seperti banyak variabel, dan seperti apa spreadsheet yang dihasilkan. Tidak diperlukan dokumen eksternal; semua yang Anda butuhkan ada di sini.  

Prasyaratnya minimal: runtime .NET terbaru (disarankan 5.0+) dan perpustakaan Aspose.Cells untuk .NET yang diinstal via NuGet. Jika Anda sudah pernah bekerja dengan C#, Anda akan merasa nyaman dalam hitungan menit.

---

## Langkah 1: Siapkan Proyek dan Tambahkan Aspose.Cells

### Mengapa langkah ini penting  
Sebelum Anda dapat **create smart marker collection**, Anda memerlukan objek workbook yang akan menjadi target marker. Aspose.Cells menyediakan kelas `Workbook` dan `Worksheet` yang membuat proses ini mudah.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Initialize a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
```

> **Tips Pro:** Jika Anda menggunakan .NET Core, tambahkan paket dengan  
> `dotnet add package Aspose.Cells` sebelum mengompilasi.

### Hasil yang Diharapkan  
Pada titik ini Anda memiliki worksheet kosong (`ws`) yang siap menerima marker.

---

## Langkah 2: Buat Koleksi Smart Marker

### Mengapa langkah ini penting  
`MarkerCollection` adalah wadah yang menyimpan setiap variabel dan marker formula. Anggaplah ini sebagai “tas placeholder” yang nanti akan digantikan Aspose.Cells dengan nilai sebenarnya.

```csharp
        // Step 2: Create a collection to hold smart markers
        MarkerCollection markerCollection = new MarkerCollection();
```

Sekarang Anda telah **created smart marker collection**—dasar bagi semua konten dinamis selanjutnya.

---

## Langkah 3: Definisikan Variabel Diskon

### Mengapa langkah ini penting  
Mendefinisikan variabel memungkinkan Anda menggunakan nilai yang sama di banyak formula. Di sini kami **define discount variable** sebagai `0.1` (yaitu 10 %). Jika diskon berubah, Anda hanya perlu memperbarui satu entri.

```csharp
        // Step 3: Define a variable marker for Discount (value 0.1)
        markerCollection.Add("var:Discount", "0.1");
```

> **Bagaimana jika diskon bersifat dinamis?**  
> Anda dapat mengganti `"0.1"` dengan representasi string apa pun dari desimal, atau bahkan mengambilnya dari basis data sebelum menambahkan marker.

---

## Langkah 4: Tambahkan Marker Formula yang Menggunakan Variabel

### Mengapa langkah ini penting  
Marker formula memungkinkan Anda menyisipkan formula Excel yang merujuk ke variabel Anda. Pada contoh ini sel `A1` akan menghitung `B1 * (1 - Discount)`.

```csharp
        // Step 4: Define a formula marker that uses the Discount variable
        markerCollection.Add("A1", "=B1*(1-{{var:Discount}})");
```

Ketika Aspose.Cells memproses koleksi, ia akan mengganti `{{var:Discount}}` dengan `0.1`, menghasilkan formula akhir `=B1*(1-0.1)`.

---

## Langkah 5: Lampirkan Koleksi ke Worksheet

### Mengapa langkah ini penting  
Melampirkan memberi tahu worksheet marker mana yang menjadi miliknya. Tanpa tautan ini, pemanggilan `Apply` tidak akan memiliki apa‑apa untuk diproses.

```csharp
        // Step 5: Attach the marker collection to the worksheet's SmartMarkers
        ws.SmartMarkers.Add(markerCollection);
```

---

## Langkah 6: Isi Worksheet dan Terapkan Marker

### Mengapa langkah ini penting  
Kita memerlukan setidaknya satu nilai input untuk `B1` agar formula dapat menghasilkan hasil. Setelah mengatur `B1`, kita memanggil `Apply()` agar Aspose.Cells mengganti marker dan mengevaluasi formula.

```csharp
        // Provide a base price in B1 (e.g., $100)
        ws.Cells["B1"].PutValue(100);

        // Step 6: Apply the smart markers to populate the worksheet cells
        ws.SmartMarkers.Apply();

        // Save the workbook to verify the outcome
        wb.Save("SmartMarkerResult.xlsx");
    }
}
```

### Hasil yang Diharapkan
- Sel **B1** berisi `100`.
- Sel **A1** berisi formula `=B1*(1-0.1)`.
- Nilai yang dihitung di **A1** adalah `90` (yaitu diskon 10 % diterapkan).

Buka `SmartMarkerResult.xlsx` dan Anda akan melihat diskon sudah diterapkan—tidak perlu penyuntingan manual.

---

## Menangani Banyak Variabel dan Kasus Tepi

### Menambahkan lebih banyak variabel
Jika Anda memerlukan parameter tambahan, cukup terus panggil `Add` dengan awalan `var:`:

```csharp
markerCollection.Add("var:TaxRate", "0.07"); // 7 % tax
markerCollection.Add("B2", "=A1*(1+{{var:TaxRate}})"); // Total with tax
```

### Aturan Penamaan Variabel
- Gunakan hanya karakter alfanumerik dan garis bawah.
- Awali dengan `var:` untuk memberi tahu Aspose.Cells bahwa itu adalah variabel, bukan referensi sel.

### Bagaimana jika sebuah variabel tidak ada?
Aspose.Cells akan membiarkan placeholder tidak berubah, yang dapat membantu Anda menemukan masalah konfigurasi selama proses debugging.

---

## Contoh Kerja Lengkap (Semua Langkah Digabung)

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Initialize workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Create the smart marker collection
        MarkerCollection markerCollection = new MarkerCollection();

        // Define discount variable (10 % discount)
        markerCollection.Add("var:Discount", "0.1");

        // Optional: define tax variable (7 % tax)
        markerCollection.Add("var:TaxRate", "0.07");

        // Formula for discounted price in A1
        markerCollection.Add("A1", "=B1*(1-{{var:Discount}})");

        // Formula for total price with tax in B2
        markerCollection.Add("B2", "=A1*(1+{{var:TaxRate}})");

        // Attach collection to worksheet
        ws.SmartMarkers.Add(markerCollection);

        // Input base price
        ws.Cells["B1"].PutValue(100); // $100

        // Apply markers and evaluate formulas
        ws.SmartMarkers.Apply();

        // Save the file
        wb.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook saved. Check SmartMarkerResult.xlsx.");
    }
}
```

Menjalankan program ini menghasilkan spreadsheet di mana:

| Sel | Nilai | Penjelasan |
|------|-------|-------------|
| B1   | 100   | Harga dasar |
| A1   | 90    | Diskon 10 % diterapkan |
| B2   | 96.3  | Harga setelah diskon + pajak 7 % |

---

## Pertanyaan Umum & Jawaban

**T: Apakah ini bekerja dengan worksheet yang sudah ada?**  
J: Tentu saja. Anda dapat memuat workbook yang ada (`new Workbook("template.xlsx")`) dan kemudian menerapkan koleksi marker yang sama ke sheet mana pun.

**T: Bisakah saya menggunakan fungsi Excel yang kompleks?**  
J: Ya. Apa pun yang didukung Excel—`VLOOKUP`, `IF`, `SUMIFS`—dapat ditempatkan di dalam string marker. Ingatlah untuk meng‑escape kurung kurawal bila diperlukan.

**T: Bagaimana jika saya perlu mengubah diskon saat runtime?**  
J: Perbarui variabel sebelum memanggil `Apply()`:  
```csharp
markerCollection["var:Discount"] = newDiscount.ToString();
ws.SmartMarkers.Apply();
```

**T: Apakah ada dampak kinerja dengan banyak marker?**  
J: Menerapkan marker bersifat O(N) dimana N adalah jumlah marker. Untuk ribuan entri, pembaruan batch atau streaming workbook dapat menjaga penggunaan memori tetap rendah.

---

## Kesimpulan

Anda kini tahu cara **create smart marker collection** dalam C# dan **define discount variable** untuk menggerakkan perhitungan dinamis di worksheet Excel. Contoh lengkap yang dapat dijalankan memperlihatkan seluruh alur kerja—dari menyiapkan workbook hingga menyimpan file akhir dengan formula yang sudah dievaluasi.  

Siap untuk langkah berikutnya? Cobalah menambahkan pemformatan bersyarat berdasarkan harga setelah diskon, atau ambil tarif diskon dari file konfigurasi JSON. Mengeksplorasi variasi tersebut akan memperdalam penguasaan Anda atas smart marker Aspose.Cells dan membuat otomasi Excel Anda benar‑benar fleksibel.

Selamat coding, dan jangan ragu bereksperimen—tidak ada batasan apa yang dapat Anda otomatisasi dengan smart marker!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}