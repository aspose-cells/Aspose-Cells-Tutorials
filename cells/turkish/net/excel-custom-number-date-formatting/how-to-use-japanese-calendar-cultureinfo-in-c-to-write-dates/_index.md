---
category: general
date: 2026-10-26
description: C#'de dönem tarihlerini ayrıştırırken ve NPOI ile bir Excel çalışma sayfasına
  eklerken Japon takvimi CultureInfo'ını nasıl kullanacağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: tr
lastmod: 2026-10-26
og_description: C#'de Japon takvimi CultureInfo'i kullanarak Reiwa dönemi tarihlerini
  ayrıştırın ve bir Excel çalışma sayfasına yazın. Açıklamalı, çalıştırılabilir tam
  kod.
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: C#'ta Japon takvim CultureInfo kullanımı – tam Excel örneği
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: C#'ta Japon takvim CultureInfo'ı kullanarak tarihleri Excel'e yazma
url: /tr/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Japon takvim CultureInfo kullanarak tarihleri Excel'e yazma

If you need to **use Japanese calendar CultureInfo** while working with dates in C#, this guide shows you exactly how. You’ll learn to parse a date string that contains a Japanese era name (for example, *Reiwa 2/5/1*) and then write the resulting `DateTime` into the first cell of an Excel worksheet using the NPOI library.

Parsing era‑based dates without the correct `CultureInfo` leads to `FormatException` or incorrect month/day values. By configuring `CultureInfo` to the Japanese calendar, you guarantee that the .NET runtime interprets the era correctly and that the value you store in Excel matches the original Japanese notation.

In this tutorial you will:

* Create a `CultureInfo` object that uses the Japanese calendar.
* Parse a Japanese era date string with `DateTime.Parse`.
* Insert the parsed `DateTime` into an NPOI worksheet cell.
* See the complete, runnable program and expected output.

> **Prerequisites** – .NET 6.0+ (or .NET Core 3.1+), the **NPOI** NuGet package, and a basic understanding of C# and Excel file handling.

---

## Gereksinimler

| Item | Reason |
|------|--------|
| **.NET SDK** (6.0 veya daha yeni) | `CultureInfo` için çalışma zamanı ve kütüphaneleri sağlar. |
| **NPOI** (`NPOI` NuGet package) | Office yüklü olmadan Excel dosyaları oluşturmanıza ve manipüle etmenize olanak tanır. |
| **Visual Studio Code**, **Visual Studio**, or any C# IDE | Örneği derlemek ve çalıştırmak için. |
| **Japanese era date string** (e.g., `"Reiwa 2/5/1"`) | Japon takviminin kullanımını gösterir. |

## Adım 1: NPOI'yi Kurun

Open a terminal in your project folder and run:

```bash
dotnet add package NPOI --version 2.6.1
```

The package supplies `IWorkbook`, `ISheet`, and `ICell` types used later.

## Adım 2: Japon takvimini kullanan bir CultureInfo oluşturun

The Japanese calendar is an era‑based calendar. You must request the *Japanese* variant of the `ja-JP` locale and explicitly set the calendar to `JapaneseCalendar`.

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – The default `ja-JP` culture uses the Gregorian calendar. Reassigning the `Calendar` property ensures that era names such as *Reiwa* are recognized during parsing.

## Adım 3: Japon era tarih dizesini ayrıştırın

Now that the `CultureInfo` is configured, you can safely parse a string that contains an era name.

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Çıktı**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

The `Parse` method interprets *Reiwa 2* as the Gregorian year 2020, month 5, day 1.

### Kenar durumu: geçersiz era'ları işleme

If a user supplies an unsupported era (e.g., `"Heisei 31/4/30"` after the Heisei era ended), `DateTime.Parse` throws a `FormatException`. Wrap the call in a try‑catch block to provide a friendly error message:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

## Adım 4: Ayrıştırılan DateTime'ı bir Excel çalışma sayfasına yazın

With the `DateTime` object ready, you can store it in an Excel cell. NPOI automatically formats `DateTime` values as Excel dates.

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Sonuç** – Opening *JapaneseEraDate.xlsx* shows the date **2020‑05‑01** in cell A1.

### Neden NPOI kullanmalı?

*Her platformda çalışır* (Windows, Linux, macOS) ve **Microsoft Office** gerektirmez. Bu, çözümü CI boru hatları, Docker konteynerleri veya sunucu‑tarafı işleme için uygun kılar.

## Adım 5: Tam, çalıştırılabilir program

Putting everything together, here is a complete console application that demonstrates the entire flow:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**Nasıl çalıştırılır**

```bash
dotnet run
```

After execution, you’ll find `JapaneseEraDate.xlsx` in the project folder with the correctly parsed date.

## Yaygın tuzaklar ve en iyi uygulama ipuçları

| Pitfall | Fix / Recommendation |
|---------|----------------------|
| `japaneseCulture.DateTimeFormat.Calendar` ayarlamayı unutmak | Her zaman bir `JapaneseCalendar` örneği atayın; aksi takdirde era adı tanınmaz. |
| Özel `CultureInfo` olmadan `DateTime.TryParse` kullanmak | Davranışı tutarlı tutmak için aynı `japaneseCulture`'ı `TryParse`'a geçirin. |
| Excel'in era adını göstermesini beklemek | Excel'in yerleşik tarih formatları yalnızca Gregorian'dir. Era adının gösterilmesi gerekiyorsa, orijinal dizeyi ayrı bir sütunda saklayın veya özel bir metin formatı oluşturun. |
| `FileStream`'i serbest bırakmamak | Dosya tutamacının hızlıca serbest bırakılmasını sağlamak için (gösterildiği gibi) bir `using` bloğu kullanın. |
| `CultureInfo` nesnelerini farklı thread'lerde karıştırmak | `CultureInfo` yalnızca okuma‑yazma olmayan işlemler için thread‑güvenlidir, ancak ilk kurulumdan sonra `Calendar` özelliğini değiştirmekten kaçının. |

## Sonuç

You now know how to **use Japanese calendar CultureInfo** in C# to accurately parse Japanese era dates and write the resulting `DateTime` into an Excel worksheet with NPOI. The complete example covers configuration, parsing, error handling, and Excel output, giving you a solid foundation for any internationalized reporting or data‑exchange scenario.

Next, you might explore:

* **Özel metinle tarih biçimlendirme**: Excel içinde era adını korumak için.  
* **Excel'den tarih okuma**: `cell.DateCellValue` kullanarak Japon takvimine saygı göstererek.  
* **Aynı tekniği uygulama**: `JapaneseCalendar`'ı uygun `Calendar` alt sınıfı ile değiştirerek diğer era‑tabanlı takvimler (ör. Tay Budist takvimi) için.

Feel free to experiment with different era strings, larger data sets, or integrating this logic into ASP.NET Core APIs that generate Excel reports on the fly. Happy coding!

## Sonra Ne Öğrenmelisiniz?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Japon Takvim Tarihleriyle Excel Çalışma Kitabı Oluşturma – Tam Kılavuz](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Excel'de Japon Era Tarihlerini Ayrıştırma – C# Geliştiricileri için Tam Kılavuz](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [C#'ta Excel çalışma kitabı oluşturma ve Japon tarihlerini ayrıştırma](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}