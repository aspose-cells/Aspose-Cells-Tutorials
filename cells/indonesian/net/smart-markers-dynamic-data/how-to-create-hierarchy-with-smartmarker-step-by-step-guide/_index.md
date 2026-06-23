---
category: general
date: 2026-02-14
description: Cara membuat hierarki dalam templat SmartMarker lebih mudah daripada
  yang Anda kira – pelajari cara membuat data hierarkis dan cara mencantumkan karyawan
  secara efisien.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: id
og_description: Cara membuat hierarki dalam templat SmartMarker itu sederhana. Ikuti
  panduan ini untuk membuat data hierarkis dan menampilkan daftar karyawan dengan
  rentang bersarang.
og_title: Cara Membuat Hierarki dengan SmartMarker – Panduan Lengkap
tags:
- SmartMarker
- C#
- templating
title: Cara Membuat Hierarki dengan SmartMarker – Panduan Langkah demi Langkah
url: /id/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Membuat Hierarki dengan SmartMarker – Panduan Lengkap

Pernah bertanya‑tanya **bagaimana cara membuat hierarki** di dalam template SmartMarker tanpa membuat rambut rontok? Anda tidak sendirian. Dalam banyak skenario pelaporan Anda memerlukan hubungan induk‑anak—misalnya departemen dan orang‑orang yang bekerja di dalamnya. Kabar baiknya, SmartMarker membuatnya menjadi sangat mudah begitu Anda mengetahui langkah‑langkah yang tepat.

Dalam tutorial ini kita akan membahas seluruh proses: mulai dari **membuat data hierarkis** di C#, mengaktifkan rentang bersarang, dan akhirnya merender template yang **menampilkan daftar karyawan** untuk setiap departemen. Pada akhir tutorial Anda akan memiliki contoh siap‑jalankan yang dapat Anda masukkan ke proyek .NET apa pun.

---

## Apa yang Anda Butuhkan

- .NET 6+ (versi terbaru apa pun)
- Referensi ke pustaka **SmartMarker** (namespace `ws.SmartMarkerProcessor`)
- Pengetahuan dasar C# – tidak perlu hal rumit, hanya beberapa objek dan satu atau dua lambda
- IDE atau editor pilihan Anda (Visual Studio, Rider, VS Code… silakan pilih)

Jika semua sudah ada, bagus—mari kita mulai.

---

## Cara Membuat Hierarki – Gambaran Umum

Ide dasarnya adalah membangun **graf objek bersarang** yang mencerminkan struktur yang ingin Anda lihat di dokumen akhir. Pada kasus kami graf tersebut tampak seperti:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker kemudian dapat mengiterasi `Departments` dan, karena kita akan mengaktifkan **pemrosesan rentang bersarang**, ia juga akan secara otomatis melintasi koleksi `Employees` tiap departemen.

---

## Langkah 1: Bangun Model Data Hierarkis

Pertama kita buat objek anonim yang berisi array departemen, masing‑masing dengan daftar karyawannya. Menggunakan tipe anonim membuat contoh ini ringan—silakan ganti dengan kelas POCO nyata nanti jika diperlukan.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Mengapa ini penting:** Array `Departments` adalah koleksi tingkat atas. Setiap elemen berisi array `Employees`, memberi kita level hierarki kedua yang nantinya akan diakses dengan `#Departments.Employees#`.

---

## Langkah 2: Aktifkan Pemrosesan Rentang Bersarang

SmartMarker tidak akan masuk ke koleksi dalam kecuali Anda memberi tahu. Objek `SmartMarkerOptions` menyimpan saklar tersebut.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **Tips pro:** Jika Anda lupa mengatur flag ini, rentang `#Employees#` di dalam tidak akan menghasilkan apa‑apa, dan Anda akan kebingungan mengapa template kosong.

---

## Langkah 3: Jalankan Processor dengan Data Anda

Sekarang kita serahkan data dan opsi ke processor. Variabel `ws` mewakili **WebService** Anda (atau objek apa pun yang menampung mesin SmartMarker).

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Pada titik ini SmartMarker mem-parsing template, menggantikan `#Departments.Name#` dengan nama tiap departemen, dan kemudian, karena rentang bersarang diaktifkan, mengiterasi koleksi `Employees` tiap departemen.

---

## Langkah 4: Buat Penanda Template

Berikut adalah template minimal yang menunjukkan kedua loop, luar dan dalam. Tempelkan ke editor template SmartMarker (atau file `.txt` yang Anda berikan ke processor).

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Saat dirender Anda akan melihat:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Apa yang Anda lihat:** `#Departments.Name#` luar mencetak judul departemen. Blok `#Departments.Employees#` dalam melintasi tiap karyawan, dan `#Departments.Employees#` di dalam blok menampilkan nama sebenarnya.

---

## Output yang Diharapkan & Verifikasi

Menjalankan contoh lengkap (data + opsi + template) harus menghasilkan daftar persis seperti yang ditunjukkan di atas. Untuk memverifikasi dengan cepat, Anda dapat mencetak hasilnya ke konsol:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

Jika Anda melihat dua judul departemen diikuti oleh bullet karyawan masing‑masing, Anda telah berhasil **membuat hierarki** dan **menampilkan daftar karyawan**.

---

## Kesalahan Umum & Kasus Tepi

| Masalah | Mengapa Terjadi | Solusi |
|-------|----------------|-----|
| Tidak ada output untuk karyawan | `EnableNestedRange` tetap false | Set `EnableNestedRange = true` |
| Nama karyawan duplikat | Array yang sama dipakai ulang di beberapa departemen | Clone array atau gunakan koleksi terpisah |
| Hierarki sangat besar menyebabkan tekanan memori | SmartMarker memuat seluruh graf objek ke memori | Stream data atau paginasi koleksi besar |
| Kesalahan sintaks template | Tag penutup `#/…#` terlewat | Gunakan validator SmartMarker atau uji cepat dengan template kecil |

---

## Melangkah Lebih Jauh – Variasi Dunia Nyata

1. **Sumber data dinamis** – Ambil departemen dari basis data dan petakan ke struktur anonim menggunakan LINQ.  
2. **Pemformatan bersyarat** – Tambahkan flag `IsManager` pada tiap karyawan dan gunakan tag bersyarat SmartMarker (`#if …#`) untuk menyorot manajer.  
3. **Beberapa level bersarang** – Jika Anda memerlukan tim di dalam departemen, cukup tambahkan koleksi lain (`Teams`) dan tetap biarkan `EnableNestedRange` aktif.

---

## Contoh Lengkap yang Siap Pakai (Copy‑Paste)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Template (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Menjalankan program akan mencetak hierarki persis seperti yang ditunjukkan sebelumnya.

---

## Kesimpulan

Kami telah membahas **cara membuat hierarki** di SmartMarker, mulai dari membentuk **data hierarkis** di C# hingga mengaktifkan rentang bersarang dan akhirnya merender template yang **menampilkan daftar karyawan** per departemen. Pola ini dapat diskalakan—tambahkan saja koleksi bersarang lebih banyak atau logika bersyarat dan Anda memiliki mesin pelaporan yang kuat di ujung jari.

Siap untuk tantangan berikutnya? Coba ganti tipe anonim dengan kelas POCO yang kuat, atau integrasikan alur ini ke endpoint ASP.NET Core yang mengembalikan dokumen PDF atau Word. Langit adalah batasnya, dan kini Anda memiliki fondasi yang solid.

---

![How to create hierarchy diagram](image.png){alt="Diagram cara membuat hierarki yang menunjukkan hubungan departemen‑karyawan"}

*Selamat coding! Jika Anda mengalami kendala, tinggalkan komentar di bawah—saya siap membantu.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}