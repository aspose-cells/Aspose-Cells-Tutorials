---
category: general
date: 2026-02-15
description: Mengurai JSON bersarang dengan C# menggunakan SmartMarkers dan pelajari
  cara membuat payload JSON C# untuk pesanan kompleks. Panduan langkah demi langkah
  dengan kode lengkap dan penjelasan.
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: id
og_description: Mengurai JSON bersarang C# secara instan. Pelajari cara membuat payload
  JSON C# dan memprosesnya dengan SmartMarkers dalam contoh lengkap yang dapat dijalankan.
og_title: Mengurai JSON Bersarang C# – Membuat Payload JSON C#
tags:
- json
- csharp
- smartmarkers
title: Mengurai JSON Bersarang C# – Membuat Payload JSON C#
url: /id/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai JSON Bersarang C# – Membuat Payload JSON C#  

Pernah perlu **mengurai JSON bersarang C#** tetapi tidak yakin harus mulai dari mana? Anda tidak sendirian—banyak pengembang menemui kebuntuan ketika data mereka berisi array di dalam objek. Kabar baiknya, dengan beberapa baris kode Anda dapat **membuat payload JSON C#** dan membiarkan SmartMarkers menelusuri struktur bersarang untuk Anda.  

Dalam tutorial ini kita akan membangun string JSON yang mewakili pesanan dengan item‑baris, mengaktifkan processor SmartMarkers agar memahami rentang bersarang, dan akhirnya memverifikasi bahwa data telah diurai dengan benar. Pada akhir tutorial Anda akan memiliki program mandiri yang siap disalin‑tempel dan dapat disesuaikan dengan JSON hierarkis apa pun yang Anda temui.

## Apa yang Anda Butuhkan  

- .NET 6 atau lebih baru (kode ini juga dapat dikompilasi dengan .NET Core 3.1)  
- Referensi ke pustaka SmartMarkers (atau pemroses serupa yang mendukung rentang bersarang)  
- Pengetahuan dasar C#—tidak ada yang eksotis, hanya pernyataan `using` biasa dan metode `Main`  

Itu saja. Tidak ada paket NuGet tambahan selain pustaka penanda, dan tidak ada layanan eksternal.

## Langkah 1: Membuat Payload JSON C# – Membangun Data  

Pertama kita susun string JSON yang berisi array pesanan, masing‑masing pesanan memiliki array `Lines`‑nya sendiri. Anggap saja ini sebagai cuplikan mini‑manajemen pesanan.

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

Mengapa membuat payload sebagai string verbatim? Karena ia mempertahankan jeda baris dan memungkinkan Anda melihat struktur sekilas—sangat berguna saat men-debug JSON bersarang.  

> **Tip profesional:** Jika JSON Anda berasal dari basis data atau API, Anda dapat mengganti literal tersebut dengan `File.ReadAllText` atau permintaan web—tidak ada bagian dalam tutorial ini yang bergantung pada sumbernya.

## Langkah 2: Mengaktifkan Rentang Bersarang dengan SmartMarkerOptions  

SmartMarkers memerlukan sedikit isyarat agar memahami bahwa sebuah array dapat berisi array lain. Itulah fungsi `EnableNestedRanges`.

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

Menetapkan `EnableNestedRanges` ke `true` memberi tahu processor untuk memperlakukan setiap koleksi `Lines` sebagai sub‑rentang dari rentang induk `Orders`. Tanpa flag ini, loop dalam akan diabaikan, dan Anda hanya akan melihat objek tingkat atas.

## Langkah 3: Memproses JSON dengan SmartMarkersProcessor  

Sekarang kita serahkan string JSON dan opsi ke processor. Pemanggilan bersifat sinkron dan tidak mengembalikan apa‑apa—SmartMarkers menulis hasilnya ke konteks internal, yang dapat Anda ambil nanti.

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

Jika Anda menggunakan pustaka lain, ganti `ws.SmartMarkersProcessor.Process` dengan nama metode yang sesuai; prinsipnya tetap sama—lewatkan JSON dan konfigurasi yang mengaktifkan penanganan bersarang.

## Langkah 4: Memverifikasi Hasil Penguraian  

Setelah diproses, biasanya Anda ingin memastikan setiap pesanan dan item‑barisnya telah dikunjungi. Di bawah ini cara sederhana untuk menampilkan data kembali ke konsol menggunakan metode hipotetik `GetProcessedData` (ganti dengan accessor aktual pustaka Anda).

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**Output konsol yang diharapkan**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

Melihat hierarki yang direproduksi mengonfirmasi bahwa **parse nested json c#** berhasil seperti yang diharapkan.

## Langkah 5: Kasus Tepi & Kesalahan Umum  

### Koleksi Kosong  
Jika sebuah pesanan tidak memiliki `Lines`, processor tetap akan membuat rentang kosong. Pastikan kode hilir Anda dapat menangani daftar kosong tanpa melempar `NullReferenceException`.

### Struktur Sangat Bersarang  
`EnableNestedRanges` bekerja untuk dua tingkat nesting secara default. Untuk tiga tingkat atau lebih Anda mungkin perlu mengatur `MaxNestedDepth` (jika pustaka menyediakan) atau memanggil processor secara rekursif pada setiap sub‑objek.

### Karakter Khusus  
String JSON yang berisi kutipan, backslash, atau Unicode memerlukan pelolosan yang tepat. Menggunakan string verbatim (`@""`) seperti yang kami lakukan menghindari sebagian besar masalah, tetapi jika Anda membuat JSON secara programatik, biarkan `System.Text.Json.JsonSerializer` menangani pelolosannya untuk Anda.

### Kinerja  
Mengurai payload besar (megabyte) dapat memakan banyak memori. Pertimbangkan untuk streaming JSON dengan `Utf8JsonReader` dan memberi potongan ke processor jika Anda menemui kendala kinerja.

## Gambaran Visual  

![Diagram yang menggambarkan alur parse nested json c# melalui pemrosesan SmartMarkers](parse-nested-json-csharp-diagram.png "diagram parse nested json c#")

Gambar menunjukkan perjalanan dari JSON mentah → SmartMarkerOptions → Processor → Model objek yang diurai.

## Ringkasan  

Kami telah menelusuri contoh lengkap **parse nested json c#**, mulai dari **create json payload c#** hingga memverifikasi data bersarang setelah diproses. Poin penting yang dapat diambil:

1. Bangun string JSON yang terstruktur dengan baik dan mencerminkan objek domain Anda.  
2. Aktifkan `EnableNestedRanges` (atau yang setara) agar parser menghormati array dalam.  
3. Jalankan processor dan periksa hasilnya untuk memastikan setiap level telah dikunjungi.  

## Apa Selanjutnya?  

- **Payload dinamis:** Ganti string hard‑coded dengan objek yang diserialisasi melalui `System.Text.Json`.  
- **Penanda khusus:** Perluas SmartMarkers dengan tag Anda sendiri untuk menyisipkan bidang terhitung ke setiap item‑baris.  
- **Penanganan error:** Bungkus pemanggilan `Process` dalam try/catch dan log detail `SmartMarkerException` untuk pemecahan masalah.  

Silakan bereksperimen—ganti array `Orders` dengan pelanggan, faktur, atau data hierarkis apa pun yang perlu Anda **parse nested json c#**. Polanya tetap sama.

Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}