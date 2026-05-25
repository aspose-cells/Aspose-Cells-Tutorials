---
category: general
date: 2026-02-23
description: Cara membuat workbook menggunakan Aspose.Cells dan menambahkan marker
  dengan array JSON. Pelajari cara menambahkan marker, menggunakan array JSON, dan
  smart marker Aspose.Cells dalam hitungan menit.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: id
og_description: Cara membuat workbook menggunakan Aspose.Cells, menambahkan penanda,
  dan menggunakan array JSON. Panduan langkah demi langkah ini menunjukkan semua yang
  Anda butuhkan.
og_title: Cara Membuat Workbook dengan Smart Markers – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cara Membuat Buku Kerja dengan Smart Markers – Panduan Aspose.Cells
url: /id/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Workbook dengan Smart Markers – Panduan Aspose.Cells

Pernah bertanya‑tanya **cara membuat workbook** yang secara otomatis mengisi data dari sumber JSON? Anda bukan satu‑satunya—para pengembang terus menanyakan cara menambahkan marker yang mengambil nilai dari array, terutama saat bekerja dengan Aspose.Cells. Kabar baik? Ini cukup sederhana setelah Anda memahami konsep smart‑marker. Dalam tutorial ini kami akan membahas cara membuat workbook, menambahkan marker, menggunakan array JSON, dan mengonfigurasi smart markers di Aspose.Cells sehingga Anda dapat menghasilkan file Excel secara dinamis.

Kami akan mencakup semua yang perlu Anda ketahui: menginisialisasi workbook, membangun `MarkerCollection`, memberi makan array JSON, mengaktifkan flag “ArrayAsSingle”, dan akhirnya menerapkan marker. Pada akhir tutorial Anda akan memiliki program C# yang berfungsi penuh dan menghasilkan file Excel dengan nilai **A**, **B**, dan **C** terisi secara otomatis. Tanpa layanan eksternal, hanya keajaiban Aspose.Cells murni.

## Prasyarat

- .NET 6.0 atau lebih baru (kode juga berfungsi dengan .NET Framework 4.6+)
- Paket NuGet Aspose.Cells untuk .NET (`Install-Package Aspose.Cells`)
- Pemahaman dasar tentang sintaks C# (jika Anda benar‑baru, potongan kode sangat banyak diberi komentar)
- Visual Studio atau IDE lain yang Anda sukai

Jika Anda sudah memiliki semua ini, bagus—mari kita mulai.

## Langkah 1: Cara Membuat Workbook (Inisialisasi File Excel)

Hal pertama yang Anda butuhkan adalah objek workbook kosong. Anggap saja ini sebagai kanvas kosong yang nanti akan diisi data oleh Aspose.Cells.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Mengapa ini penting:** `Workbook` adalah titik masuk untuk setiap operasi Excel. Tanpa itu Anda tidak dapat menempelkan smart markers atau menyimpan file. Membuat workbook terlebih dahulu juga memastikan Anda memiliki lingkungan bersih untuk langkah‑langkah selanjutnya.

## Langkah 2: Cara Menambahkan Marker – Inisialisasi Marker Collection

Smart markers berada di dalam `MarkerCollection`. Koleksi ini adalah tempat Anda mendefinisikan placeholder (marker) dan data yang akan menggantikannya.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Tips profesional:** Anda dapat menggunakan kembali `MarkerCollection` yang sama untuk beberapa worksheet, tetapi memiliki satu per sheet membuat proses debug lebih mudah.

## Langkah 3: Gunakan Array JSON – Tambahkan Marker dengan Data JSON

Sekarang kita benar‑benar menambahkan marker. Placeholder `{SmartMarker}` akan digantikan oleh array JSON yang kita berikan. JSON harus berupa stringified array, misalnya `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Penjelasan:** Metode `Add` menerima dua argumen: teks marker dan sumber data. Di sini sumber data adalah array JSON, yang dapat diparse secara otomatis oleh Aspose.Cells. Inilah inti **use json array** dengan smart markers.

## Langkah 4: Konfigurasi Marker – Perlakukan Array sebagai Nilai Tunggal

Secara default, Aspose.Cells memperluas array JSON menjadi baris‑baris terpisah. Jika Anda ingin seluruh array diperlakukan sebagai nilai sel tunggal (berguna untuk daftar dropdown atau string yang digabung), aktifkan flag `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Kapan menggunakannya:** Jika Anda menginginkan array muncul dalam satu sel (misalnya `"A,B,C"`), aktifkan flag ini. Jika tidak, Aspose.Cells akan menuliskan setiap elemen ke barisnya masing‑masing.

## Langkah 5: Tempelkan Marker ke Worksheet dan Terapkan

Akhirnya, hubungkan koleksi marker ke worksheet dan beri tahu Aspose.Cells untuk mengganti placeholder dengan data sebenarnya.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Hasil:** Setelah menjalankan program, `SmartMarkerResult.xlsx` berisi nilai **A** (atau seluruh array jika `ArrayAsSingle` bernilai true) di sel `A1`. Buka file tersebut untuk memverifikasi.

### Output yang Diharapkan

| A |
|---|
| A |   *(jika `ArrayAsSingle` bernilai false, elemen pertama mengisi sel)*

Jika Anda mengatur `ArrayAsSingle = true`, sel `A1` akan berisi string `["A","B","C"]`.

## Langkah 6: Cara Menambahkan Marker – Skenario Lanjutan (Opsional)

Anda mungkin bertanya, *bagaimana jika saya membutuhkan lebih dari satu marker?* Jawabannya sederhana: panggil `Add` lagi.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Mengapa ini berhasil:** Setiap marker beroperasi secara independen, sehingga Anda dapat mencampur “array as single” dan “expand into rows” dalam worksheet yang sama. Fleksibilitas ini menjadi ciri khas **smart markers aspose.cells**.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|---------|----------------|--------|
| Marker tidak diganti | Teks placeholder hilang atau typo | Pastikan sel berisi string marker yang tepat (`{SmartMarker}`) |
| JSON tidak ter‑parse | Sintaks JSON tidak valid (kurang tanda kutip) | Gunakan validator JSON atau escape tanda kutip ganda dalam string C# |
| Array memperluas secara tak terduga | `ArrayAsSingle` tetap pada nilai default `false` | Setel `["ArrayAsSingle"] = true` untuk marker tertentu |
| Workbook tersimpan kosong | `Apply()` tidak dipanggil sebelum `Save()` | Selalu panggil `worksheet.SmartMarkers.Apply()` sebelum menyimpan |

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

Berikut adalah program lengkap yang dapat Anda tempel ke aplikasi console. Tidak ada file tambahan yang diperlukan.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Jalankan program, buka `SmartMarkerResult.xlsx`, dan Anda akan melihat array JSON (atau elemen pertamanya) ditempatkan rapi di sel **A1**.

## Langkah Selanjutnya: Memperluas Solusi

Sekarang Anda sudah tahu **cara membuat workbook**, **cara menambahkan marker**, dan **use json array** dengan Aspose.Cells, pertimbangkan ide‑ide lanjutan berikut:

1. **Multiple Worksheets** – Loop melalui daftar worksheet dan tempelkan koleksi marker yang berbeda pada masing‑masing.
2. **Dynamic JSON** – Ambil JSON dari API web (`HttpClient`) dan beri langsung ke `smartMarkerCollection.Add`.
3. **Styling Output** – Setelah menerapkan marker, format sel (font, warna) agar laporan terlihat lebih profesional.
4. **Export Formats** – Simpan workbook sebagai PDF, CSV, atau HTML dengan mengubah `workbook.Save("file.pdf")`.

Masing‑masing topik ini secara alami melibatkan **smart markers aspose.cells**, sehingga Anda akan memperluas konsep inti yang baru saja dipelajari.

## Kesimpulan

Kami telah membahas **cara membuat workbook** dari awal, **cara menambahkan marker**, dan **use json array** dengan smart markers Aspose.Cells. Contoh lengkap yang dapat dijalankan memperlihatkan seluruh alur kerja, mulai dari inisialisasi `Workbook` hingga menyimpan file akhir. Dengan mengaktifkan flag `ArrayAsSingle` Anda mendapatkan kontrol detail tentang bagaimana data JSON muncul di Excel, menjadikan solusi ini dapat disesuaikan untuk berbagai skenario pelaporan.

Cobalah kode tersebut, ubah JSON‑nya, dan bereksperimen dengan marker tambahan. Setelah Anda menguasai blok‑blok bangunan ini, menghasilkan laporan Excel yang canggih menjadi sangat mudah. Ada pertanyaan atau ingin berbagi kasus penggunaan menarik? Tinggalkan komentar di bawah—selamat coding!

![Diagram yang menunjukkan cara membuat workbook dengan smart markers di Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "cara membuat workbook dengan smart markers di Aspose.Cells")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}