---
category: general
date: 2026-02-14
description: 'Otomatisasi pembuatan faktur dengan SmartMarker: pelajari cara mengulang
  lembar kerja, memberi nama secara dinamis, dan menguasai penamaan lembar kerja dinamis
  dalam hitungan menit.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: id
og_description: Otomatisasi pembuatan faktur dengan SmartMarker. Panduan ini menunjukkan
  cara mengulang lembar kerja, menamainya secara dinamis, dan menguasai penamaan lembar
  kerja dinamis.
og_title: Otomatisasi Pembuatan Faktur – Penamaan Lembar Kerja Dinamis & Pengulangan
tags:
- C#
- SmartMarker
- Excel Automation
title: Otomatisasi Pembuatan Faktur – Penamaan Lembar Kerja Dinamis & Pengulangan
  di C#
url: /id/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengotomatiskan Pembuatan Faktur – Penamaan Worksheet Dinamis & Pengulangan di C#

Pernah bertanya-tanya bagaimana **mengotomatiskan pembuatan faktur** tanpa harus menyalin sheet secara manual untuk setiap pesanan? Anda tidak sendirian. Banyak pengembang menemui kendala ketika mereka membutuhkan worksheet terpisah per faktur namun juga menginginkan nama sheet mencerminkan nomor pesanan. Pada tutorial ini kita akan menyelesaikan masalah tersebut menggunakan `SmartMarkerProcessor` dari SmartMarker dan menunjukkan **cara menamai worksheet** secara dinamis sekaligus membahas **cara mengulang worksheet** untuk setiap record. Pada akhir tutorial Anda akan memiliki contoh C# yang siap dijalankan yang menghasilkan workbook di mana setiap faktur berada pada tab yang sudah dinamai dengan rapi.

Kami akan membahas setiap langkah—dari mengambil pesanan dari sumber data hingga mengonfigurasi `SmartMarkerOptions` untuk penamaan worksheet dinamis. Tidak diperlukan dokumen eksternal; semua yang Anda butuhkan ada di sini. Pengetahuan dasar tentang C# dan referensi ke pustaka Aspose.Cells (atau mesin kompatibel SmartMarker apa pun) sudah cukup.

---

## Apa yang Akan Anda Bangun

- Mengambil koleksi objek order.
- Mengonfigurasi SmartMarker untuk **mengulang worksheet** untuk setiap order.
- Menerapkan **penamaan worksheet dinamis** menggunakan placeholder `{OrderId}`.
- Menghasilkan file Excel di mana setiap tab dinamai `Invoice_12345`, `Invoice_67890`, dll.
- Memverifikasi output dengan membuka workbook.

---

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga dapat dikompilasi dengan .NET 5+).
- Aspose.Cells untuk .NET (atau pustaka apa pun yang mengimplementasikan SmartMarker). Instal melalui NuGet:

```bash
dotnet add package Aspose.Cells
```

- Kelas `Order` dasar (Anda dapat menggantinya dengan DTO Anda sendiri).

---

## Langkah 1: Siapkan Proyek dan Model

Pertama, buat aplikasi console baru dan definisikan model data yang mewakili sebuah order.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Pro tip:** Jaga model tetap ringan untuk demo; Anda dapat menambahkannya nanti dengan detail baris, pajak, dll.

---

## Langkah 2: Siapkan Template Excel

SmartMarker bekerja dengan workbook template. Buat file bernama `InvoiceTemplate.xlsx` dengan satu worksheet bernama `InvoiceTemplate`. Pada sel **A1** letakkan placeholder SmartMarker seperti:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

Anda dapat memformat sel sesuka hati—header tebal, format mata uang, dll. Simpan file di folder root proyek.

> **Mengapa template?** Ini memisahkan tata letak dari kode, memungkinkan desainer mengubah tampilan tanpa menyentuh logika.

---

## Langkah 3: Konfigurasi Opsi SmartMarker – Ulang & Nama Worksheet

Sekarang kita akan memberi tahu SmartMarker untuk *mengulang* worksheet template untuk setiap order dan memberi setiap salinan nama yang mencakup ID order. Inilah inti dari **penamaan worksheet dinamis**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Cara Kerjanya

- **`RepeatWorksheet = true`** memberi tahu engine untuk menduplikasi sheet sumber untuk setiap elemen dalam koleksi `orders`. Ini memenuhi kebutuhan **cara mengulang worksheet**.
- **`RepeatWorksheetName = "Invoice_{OrderId}"`** adalah string template di mana `{OrderId}` adalah placeholder yang digantikan SmartMarker dengan ID order saat ini. Ini menjawab **cara menamai worksheet** dan **penamaan worksheet dinamis**.
- Processor menggabungkan setiap field order (`{{OrderId}}`, `{{Customer}}`, dll.) ke dalam sheet yang diduplikasi, menghasilkan faktur yang lengkap.

---

## Langkah 4: Jalankan Aplikasi dan Verifikasi Output

Kompilasi dan jalankan aplikasi console:

```bash
dotnet run
```

Anda akan melihat pesan sukses di konsol. Buka `GeneratedInvoices.xlsx` dan Anda akan menemukan tiga tab:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Setiap sheet berisi data order yang telah menggantikan placeholder. Tata letak yang Anda rancang di template tetap terjaga, membuktikan bahwa **mengotomatiskan pembuatan faktur** berfungsi end‑to‑end.

### Screenshot yang Diharapkan (teks alt untuk SEO)

![contoh otomatisasi pembuatan faktur menampilkan tiga worksheet dengan nama dinamis](/images/invoice-automation.png)

> *Teks alt gambar mencakup kata kunci utama untuk memenuhi SEO.*

---

## Langkah 5: Kasus Pojok & Variasi Umum

### Bagaimana jika OrderId mengandung karakter ilegal?

Nama sheet Excel tidak boleh mengandung `\ / ? * [ ] :`. Jika ID Anda mungkin mengandung karakter tersebut, bersihkan dulu:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Tambahkan properti terhitung ke `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Perlu mempertahankan sheet template asli?

Setel `smartMarkerOptions.RemoveTemplate = false;` (defaultnya `true`). Ini akan meninggalkan `InvoiceTemplate` asli tidak tersentuh sebagai referensi.

### Ingin mengelompokkan faktur berdasarkan pelanggan?

Anda dapat menumpuk **grup pengulangan**. Pertama ulangi berdasarkan pelanggan, lalu ulangi order di dalam setiap worksheet pelanggan. Sintaksnya sedikit lebih rumit, tetapi prinsipnya tetap sama—gunakan `RepeatWorksheet` dan pola penamaan yang mencerminkan hierarki.

---

## Contoh Lengkap yang Berfungsi (Semua Kode dalam Satu Tempat)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Salin‑tempel kode ini ke `Program.cs`, letakkan `InvoiceTemplate.xlsx` di sampingnya, dan Anda siap menjalankan.

---

## Pertanyaan yang Sering Diajukan

**T: Apakah pendekatan ini bekerja dengan set data besar (ribuan faktur)?**  
J: Ya. SmartMarker memproses data secara streaming, namun tetap perhatikan penggunaan memori. Jika mencapai batas, pertimbangkan memproses dalam batch dan menulis tiap batch ke workbook terpisah.

**T: Bisakah saya menambahkan logo ke setiap faktur secara otomatis?**  
J: Tentu. Letakkan gambar logo pada sheet template. Karena sheet tersebut diduplikasi, logo akan muncul pada setiap faktur yang dihasilkan tanpa kode tambahan.

**T: Bagaimana jika saya perlu melindungi worksheet?**  
J: Setelah proses selesai, iterasi `wb.Worksheets` dan panggil `ws.Protect(Password, ProtectionType.All)`.

---

## Kesimpulan

Kita baru saja **mengotomatiskan pembuatan faktur** dengan memanfaatkan fitur repeat‑worksheet SmartMarker dan pola penamaan yang cerdas. Tutorial ini mencakup **cara menamai worksheet**, mendemonstrasikan **cara mengulang worksheet** untuk setiap order, serta menampilkan **penamaan worksheet dinamis** yang membuat workbook Anda rapi dan mudah dicari.  

Dari pengambilan data, penyiapan template, konfigurasi `SmartMarkerOptions`, hingga penanganan kasus pojok, kini Anda memiliki solusi lengkap yang dapat dijalankan. Selanjutnya, coba tambahkan tabel item, terapkan conditional formatting, atau ekspor data yang sama ke PDF untuk pipeline penagihan yang sepenuhnya otomatis.

Siap meningkatkan level? Jelajahi topik terkait seperti “ekspor massal Excel dengan Aspose.Cells”, “konversi PDF worksheet”, atau “mengirim faktur yang dihasilkan langsung dari C#”. Langit adalah batasnya—selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}