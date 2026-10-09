---
category: general
date: 2026-06-27
description: Pelajari cara mengurai tanggal era Jepang di C# dan kemudian memformat
  datetime yyyy‑mm‑dd untuk output ISO. Kode langkah demi langkah, kasus tepi, dan
  tips.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: id
og_description: Mengurai tanggal era Jepang di C# dan memformat datetime yyyy-mm-dd
  dengan mudah. Contoh lengkap dengan penjelasan dan jebakan.
og_title: Mengurai tanggal era Jepang di C# – Panduan Pemrograman Lengkap
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  headline: Parse Japanese era date in C# – Complete Guide
  type: TechArticle
- description: Learn how to parse Japanese era date in C# and then format datetime
    yyyy-mm-dd for ISO output. Step‑by‑step code, edge cases, and tips.
  name: Parse Japanese era date in C# – Complete Guide
  steps:
  - name: Multiple Eras
    text: Japan has gone through several eras (Meiji, Taishō, Shōwa, Heisei, Reiwa).
      The `JapaneseCalendar` automatically maps them, so `"H30-12-31"` (Heisei 30)
      becomes `2018-12-31`. Just keep the same parsing logic; the calendar does the
      heavy lifting.
  - name: Invalid Input
    text: 'If a string doesn’t match the expected pattern, `Parse` throws. Use `TryParseExact`
      as shown earlier, or pre‑validate with a regular expression:'
  - name: Time Zones
    text: '`DateTime` objects are “kind‑agnostic” by default. If you need a UTC timestamp,
      call:'
  type: HowTo
tags:
- C#
- .NET
- DateTime
- Localization
title: Mengurai tanggal era Jepang di C# – Panduan Lengkap
url: /id/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Mengurai tanggal era Jepang di C# – Panduan Lengkap

Pernah perlu **mengurai tanggal era Jepang** dalam aplikasi .NET dan bertanya-tanya mengapa hasilnya terlihat salah? Anda tidak sendirian. Di banyak sistem warisan, tanggal muncul dalam gaya “R3‑04‑01”, dan Anda perlu mengubahnya menjadi string **format datetime yyyy-mm-dd** yang bersih untuk API atau basis data.  

Dalam tutorial ini kami akan menjelaskan langkah‑langkah tepat untuk melakukannya, menjelaskan mengapa setiap bagian penting, dan menunjukkan cara menangani kasus tepi yang rumit yang sering menyulitkan pengembang.

> **Catatan:** Semua kode siap untuk disalin‑tempel ke aplikasi console yang menargetkan .NET 6 atau yang lebih baru.

## Apa yang Anda Butuhkan

- .NET 6 SDK (atau versi terbaru apa pun)
- Familiaritas dasar dengan C# dan namespace `System.Globalization`
- IDE atau editor – Visual Studio, VS Code, Rider, apa saja yang Anda suka

Tidak diperlukan paket NuGet eksternal; semuanya berada di BCL.

## Langkah 1: Siapkan Budaya Jepang dengan Kalender Kekaisaran

Pertama, kita memerlukan `CultureInfo` yang mengetahui kalender kekaisaran Jepang. Secara default, `ja-JP` menggunakan kalender Gregorian, jadi kita mengganti `DateTimeFormat.Calendar`‑nya dengan instance `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Step 1: Create a Japanese culture and switch to the Japanese imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // (The rest of the code follows...)
```

> **Mengapa ini penting:** `JapaneseCalendar` menerjemahkan simbol era (seperti “R” untuk Reiwa) ke tahun Gregorian yang tepat. Tanpanya, `DateTime.Parse` akan melempar `FormatException`.

## Langkah 2: Mengurai String Tanggal Berbasis Era

Sekarang kita dapat memberi string seperti `"R3-04-01"` ke `DateTime.Parse`. Budaya yang baru saja kita konfigurasikan memberi tahu parser cara menafsirkan bagian “R3”.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Jika Anda lebih suka pendekatan yang lebih aman yang menghindari pengecualian pada input yang buruk, ganti `Parse` dengan `TryParseExact`:

```csharp
        // Safer alternative with TryParseExact
        if (DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",               // ggy = era+year, MM = month, dd = day
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime safeDate))
        {
            parsedDate = safeDate;
        }
        else
        {
            Console.WriteLine("Unable to parse the Japanese era date.");
            return;
        }
```

> **Tips pro:** String format khusus `"ggy-MM-dd"` memberi tahu parser persis apa yang diharapkan. “gg” adalah penunjuk era, “y” adalah tahun dalam era tersebut.

## Langkah 3: Mengonversi Hasil ke ISO 8601 (`format datetime yyyy-mm-dd`)

Akhirnya, kami mengeluarkan `DateTime` dalam format ISO standar. Spesifikator format `"yyyy-MM-dd"` melakukan hal itu.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Menjalankan program akan mencetak:

```
2021-04-01
```

Itulah **format datetime yyyy-mm-dd** yang Anda cari, siap untuk payload JSON, penyisipan SQL, atau sistem hilir manapun.

![parse japanese era date example](placeholder.png){alt="contoh mengurai tanggal era Jepang"}

## Menangani Era Lain dan Kasus Tepi

### Beberapa Era

Jepang telah melewati beberapa era (Meiji, Taishō, Shōwa, Heisei, Reiwa). `JapaneseCalendar` secara otomatis memetakan mereka, sehingga `"H30-12-31"` (Heisei 30) menjadi `2018-12-31`. Cukup gunakan logika parsing yang sama; kalender melakukan pekerjaan berat.

### Input Tidak Valid

Jika string tidak cocok dengan pola yang diharapkan, `Parse` akan melempar. Gunakan `TryParseExact` seperti yang ditunjukkan sebelumnya, atau lakukan pra‑validasi dengan ekspresi reguler:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Zona Waktu

Objek `DateTime` bersifat “kind‑agnostic” secara default. Jika Anda membutuhkan cap waktu UTC, panggil:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Atau gunakan `DateTimeOffset` untuk kesadaran zona penuh.

## Contoh Kerja Penuh

Berikut seluruh potongan kode yang dapat Anda masukkan ke dalam proyek console baru:

```csharp
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Initialize Japanese culture with the imperial calendar
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // The era‑based date you want to convert
        string eraDate = "R3-04-01";

        // Try parsing – safer than Parse when input may be malformed
        if (!DateTime.TryParseExact(
                eraDate,
                "ggy-MM-dd",
                japaneseCulture,
                DateTimeStyles.None,
                out DateTime parsedDate))
        {
            Console.WriteLine("Failed to parse the Japanese era date.");
            return;
        }

        // Convert to ISO 8601 (format datetime yyyy-mm-dd)
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine($"Original era date: {eraDate}");
        Console.WriteLine($"Converted ISO date: {isoDate}");
    }
}
```

**Output console yang diharapkan**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Ringkasan

Kami telah membahas cara **mengurai tanggal era Jepang** dengan:

1. Membuat `CultureInfo` untuk `ja-JP` dan mengganti dengan `JapaneseCalendar`.
2. Menggunakan `DateTime.Parse` atau `TryParseExact` yang lebih kuat dengan format khusus.
3. Memformat `DateTime` yang dihasilkan dengan `"yyyy-MM-dd"` untuk mencapai **format datetime yyyy-mm-dd** yang diinginkan.

Itulah semua yang Anda butuhkan untuk menjembatani data era Jepang warisan ke sistem modern yang mematuhi ISO.

## Apa Selanjutnya?

- **Pemrosesan batch:** Loop melalui CSV berisi tanggal era dan tulis string ISO ke basis data.
- **Lokalisasi:** Konversi tanggal ISO kembali ke format era untuk tampilan UI (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Kalender khusus:** Jelajahi `TaiwanCalendar` atau `HijriCalendar` untuk kebutuhan regional lainnya.

Silakan bereksperimen—ganti string era, uji kasus tepi, atau integrasikan logika ini ke endpoint ASP.NET Core. Jika Anda menemukan masalah, tinggalkan komentar di bawah; selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap dengan penjelasan langkah demi langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Change Excel Date System to 1904 using Aspose.Cells .NET](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [How to Implement and Format Excel Comments Using Aspose.Cells for .NET: A Step‑By‑Step Guide](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}