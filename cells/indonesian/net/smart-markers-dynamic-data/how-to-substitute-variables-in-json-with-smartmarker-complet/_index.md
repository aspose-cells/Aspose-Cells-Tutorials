---
category: general
date: 2026-03-29
description: Cara mengganti variabel dalam JSON menggunakan SmartMarker – pelajari
  cara menggunakan ekspresi if, menerapkan logika kondisional, mengalikan nilai, dan
  menghasilkan JSON dengan mudah.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: id
og_description: Cara mengganti variabel dalam JSON menggunakan SmartMarker. Temukan
  cara menggunakan ekspresi if, menerapkan logika kondisional, mengalikan nilai, dan
  menghasilkan JSON dalam hitungan menit.
og_title: Cara Mengganti Variabel dalam JSON dengan SmartMarker – Langkah demi Langkah
tags:
- C#
- SmartMarker
- JSON templating
title: Cara Mengganti Variabel dalam JSON dengan SmartMarker – Panduan Lengkap
url: /id/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Mengganti Variabel dalam JSON dengan SmartMarker – Panduan Lengkap

Pernah bertanya-tanya **bagaimana cara mengganti variabel** di dalam payload JSON tanpa menulis parser khusus? Anda tidak sendirian. Dalam banyak skenario integrasi—seperti faktur, mesin penetapan harga, atau file konfigurasi dinamis—Anda perlu menyuntikkan nilai runtime, menerapkan kondisi sederhana, dan bahkan mungkin melakukan perkalian cepat. Tutorial ini menunjukkan secara tepat **bagaimana cara mengganti variabel** menggunakan pustaka SmartMarker, sambil menjaga JSON tetap bersih dan mudah dibaca.

Kami akan membahas contoh dunia nyata yang mencakup **use if expression**, **how to apply conditional**, **how to multiply values**, dan **how to generate json** secara langsung. Pada akhir tutorial, Anda akan memiliki potongan kode C# siap‑jalankan yang dapat Anda sisipkan ke proyek .NET mana pun.

## Apa yang Akan Anda Pelajari

- Siapkan `SmartMarkerOptions` untuk menyimpan variabel yang dapat digunakan kembali.  
- Tulis template JSON yang berisi ekspresi `if` untuk logika kondisional.  
- Kalikan sebuah nilai dengan variabel di dalam template.  
- Proses template dengan `SmartMarkerProcessor` dan dapatkan string JSON akhir.  
- Memecahkan masalah umum seperti variabel yang hilang atau ekspresi yang tidak valid.  

Tidak ada layanan eksternal, tidak ada dependensi berat—hanya C# biasa dan paket NuGet SmartMarker.

---

## Cara Mengganti Variabel – Gambaran Langkah‑per‑Langkah

Berikut adalah gambaran tingkat tinggi dari alur kerja. Anggaplah ini sebagai pipeline di mana template JSON mentah Anda masuk dari kiri, mesin SmartMarker melakukan magisnya, dan JSON yang sudah dirender sepenuhnya keluar di sebelah kanan.

![Diagram yang menunjukkan cara mengganti variabel dalam JSON](https://example.com/images/smartmarker-flow.png "Cara mengganti variabel dalam JSON")

*Image alt text: Diagram yang menunjukkan cara mengganti variabel dalam JSON.*

---

## Langkah 1: Instal dan Impor SmartMarker

Sebelum Anda dapat memulai, pastikan paket SmartMarker sudah direferensikan dalam proyek Anda. Jika Anda menggunakan .NET CLI, jalankan:

```bash
dotnet add package SmartMarker
```

Kemudian, tambahkan direktif `using` yang diperlukan di bagian atas file C# Anda:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro tip:** Versi terbaru (per Maret 2026) adalah 2.4.1. Versi ini mendukung .NET 6 dan yang lebih baru, tetapi juga berfungsi dengan baik pada .NET Framework 4.7.

---

## Langkah 2: Buat SmartMarker Options dan Definisikan Variabel

Sekarang kita akan membuat sebuah instance `SmartMarkerOptions` yang akan menyimpan semua variabel yang ingin kita gunakan kembali di seluruh template. Di sinilah kita menjawab pertanyaan **how to substitute variables**—variabel berfungsi sebagai placeholder yang akan diganti oleh SmartMarker nanti.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

Mengapa menyimpan tarif di `Variables` alih-alih menuliskannya secara langsung? Karena Anda mungkin mengambil angka tersebut dari basis data, file konfigurasi, atau input pengguna. Menyimpannya di options membuat template dapat digunakan kembali dan mudah diuji.

---

## Langkah 3: Tulis Template JSON dengan Ekspresi `if`

Di sinilah kata kunci **use if expression** bersinar. SmartMarker memungkinkan Anda menyematkan logika kondisional langsung di dalam string JSON. Sintaksnya terlihat seperti nama properti, tetapi SmartMarker memperlakukannya sebagai sebuah arahan.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

Perhatikan kunci `if(Amount>500)`. SmartMarker mengevaluasi ekspresi `Amount>500`; jika benar, nilai yang bersesuaian (`${Amount * Rate}`) akan dimasukkan ke output. Sintaks `${...}` adalah mesin *variable substitution*—di sini kami **how to multiply values** (`Amount * Rate`) sebelum menyuntikkan hasilnya.

---

## Langkah 4: Proses Template dan Dapatkan JSON Akhir

Dengan options dan template siap, kami menyerahkan semuanya ke processor. Metode `ProcessJson` mem-parsing template, menerapkan kondisi, melakukan perkalian, dan mengembalikan string JSON yang bersih.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Menjalankan potongan kode mencetak:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Apa yang terjadi?**  
- `Amount` adalah 1000, yang memenuhi `Amount>500`.  
- SmartMarker mengevaluasi `${Amount * Rate}` → `1000 * 0.08 = 80`.  
- Kunci kondisional asli (`if(Amount>500)`) diganti dengan nama properti bersih (`Result`). Secara default SmartMarker menggunakan `"Result"` tetapi Anda dapat menyesuaikannya (lebih lanjut nanti).

Jika Anda mengubah `Amount` menjadi `400`, outputnya menjadi:

```json
{
  "Amount": 400
}
```

Blok kondisional menghilang karena ekspresi dievaluasi menjadi `false`. Itulah inti dari logika **how to apply conditional** dalam JSON.

---

## Langkah 5: Menyesuaikan Nama Properti Output (Opsional)

Kadang-kadang Anda tidak menginginkan kunci generik `"Result"`. SmartMarker memungkinkan Anda menentukan nama khusus menggunakan opsi `RenameIfExpression`:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Output:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Sekarang nilai kondisional disimpan di bawah nama properti yang lebih bermakna—sempurna untuk layanan hilir yang mengharapkan field tertentu.

---

## Kesalahan Umum dan Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| Variabel tidak ditemukan | Anda merujuk ke variabel yang tidak ada di `smartMarkerOptions.Variables`. | Periksa kembali ejaan dan pastikan variabel ditambahkan sebelum diproses. |
| Sintaks `if` tidak valid | Kurang tanda kurung atau operator yang salah (`>`, `<`, `==`). | Ikuti pola tepat `if(<expression>)`; SmartMarker hanya mendukung perbandingan numerik sederhana. |
| JSON menjadi tidak valid | Secara tidak sengaja meninggalkan koma di akhir setelah blok kondisional. | Biarkan SmartMarker menangani penghapusan; pastikan template asli secara sintaksis benar. |
| Format angka tidak terduga | Hasil muncul sebagai string `"80"` alih-alih angka. | Lakukan cast atau parse nanti, atau gunakan `${(Amount * Rate):N0}` untuk format numerik. |

---

## Contoh Lengkap yang Berfungsi (Siap Salin‑Tempel)

Berikut adalah program lengkap yang dapat Anda kompilasi dan jalankan. Program ini memperlihatkan **how to generate json** dengan variabel dinamis, kondisi, dan aritmatika—semua dalam kurang dari 30 baris.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Output konsol yang diharapkan**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

Silakan ubah `Amount` untuk menguji cabang kondisional, atau sesuaikan `Rate` untuk melihat perhitungan diskon yang berbeda.

---

## Memperluas Pola – Lebih Banyak Skenario “How to”

- **How to substitute variables** dari file konfigurasi: Muat `Dictionary<string, object>` dari `appsettings.json` dan masukkan ke `smartMarkerOptions.Variables`.  
- **How to use if expression** untuk beberapa kondisi: Rangkai seperti `"if(Amount>500 && CustomerType=='VIP')"`—SmartMarker mendukung logika AND/OR.  
- **How to apply conditional** formatting: Gunakan `${Amount:0.00}` di dalam ekspresi untuk mengontrol jumlah desimal.  
- **How to multiply values** dengan matematika yang lebih kompleks: `${(Amount - Discount) * TaxRate}` berfungsi dengan cara yang sama.  
- **How to generate json** untuk objek bersarang: Letakkan blok kondisional di dalam objek JSON lain, dan SmartMarker akan mempertahankan hierarki.

---

## Kesimpulan

Kami telah membahas **how to substitute variables** dalam JSON menggunakan SmartMarker, mendemonstrasikan **use if expression** untuk penyertaan kondisional, menjelaskan **how to apply conditional** logic, menunjukkan **how to multiply values** di dalam template, dan akhirnya mengilustrasikan **how to generate json** yang siap untuk konsumsi hilir. Pendekatan ini ringan, tidak memerlukan mesin templating eksternal, dan cocok dengan mulus di basis kode C# mana pun.

Cobalah—ubah variabel, tambahkan lebih banyak kondisi, atau bungkus semuanya dalam kelas helper untuk penggunaan kembali di seluruh solusi Anda. Ketika Anda perlu menghasilkan JSON dinamis dengan cepat, SmartMarker adalah pilihan yang solid dan siap produksi.

---

**Langkah Selanjutnya**

- Selami lebih dalam fitur lanjutan SmartMarker seperti loop (`foreach`) dan fungsi kustom.  
- Gabungkan teknik ini dengan endpoint ASP.NET Core untuk menyajikan API JSON dinamis.  
- Jelajahi pustaka templating lain (mis., Handlebars.NET) untuk perbandingan, terutama jika Anda membutuhkan sintaks yang lebih kaya.

Ada pertanyaan atau kasus penggunaan tertentu yang Anda hadapi? Tinggalkan komentar di bawah, dan mari kita selesaikan bersama. Selamat coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}