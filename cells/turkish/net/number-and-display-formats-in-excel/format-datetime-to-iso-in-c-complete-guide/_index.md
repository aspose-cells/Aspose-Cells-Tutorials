---
category: general
date: 2026-03-22
description: Excel'den tarih çıkarırken datetime'ı ISO formatına nasıl dönüştüreceğinizi
  ve Aspose.Cells kullanarak C#'ta ISO tarihini nasıl görüntüleyeceğinizi öğrenin.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: tr
og_description: datetime'ı ISO formatına dönüştürmek kolaylaştı. Bu rehber, Excel'den
  tarihi nasıl çıkaracağınızı ve Aspose.Cells ile ISO tarihini nasıl görüntüleyeceğinizi
  gösterir.
og_title: C#'ta datetime'ı ISO formatına dönüştür – Adım Adım Öğretici
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: C#'ta datetime'ı ISO formatına dönüştürme – Tam Kılavuz
url: /tr/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# format datetime to iso in C# – Complete Guide

Hiç **format datetime to iso** yapmanız gerekti, ancak kaynak bir Excel çalışma kitabının içinde mi? Belki hücrede “令和3年5月1日” gibi bir Japon dönemi var ve bunu temiz bir `2021‑05‑01` dizesine nasıl dönüştüreceğinizi merak ediyorsunuz. Yalnız değilsiniz. Bu öğreticide **extract date from excel** yapmayı, Japon dönemini ayrıştırmayı ve ardından **display iso date**'i konsolda göstermeyi birkaç satır C# ve Aspose.Cells ile göstereceğiz.

İhtiyacınız olan her şeyi adım adım inceleyeceğiz: gerekli NuGet paketi, doğrudan kopyalayıp yapıştırabileceğiniz tam kod, her satırın neden önemli olduğu ve birkaç kenar‑durum ipucu. Sonunda, orijinal Excel değeri ne kadar garip olursa olsun datetime to iso formatlayan yeniden kullanılabilir bir snippet elde edeceksiniz.

## What You’ll Need

- .NET 6.0 veya daha yeni (kod .NET Framework 4.6+ üzerinde de derlenebilir)
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir editör)
- **Aspose.Cells for .NET** NuGet paketi – `Install-Package Aspose.Cells`
- Japon dönemi formatında tarih tutan bir Excel dosyası (veya yeni bir çalışma kitabı)

Hepsi bu. Başka kütüphane, COM interop yok, sadece tek, iyi belgelenmiş bir yöntem.

## Step 1: Create a Workbook and Write a Japanese Era Date  

İlk olarak üzerinde çalışacağımız bir çalışma kitabına ihtiyacımız var. Zaten bir Excel dosyanız varsa `new Workbook("path")` ile yükleyebilirsiniz. Bu örnek için bellekte yeni bir çalışma kitabı oluşturup **A1** hücresine bir Japon dönemi dizesi yerleştireceğiz.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Why we do this:** Aspose.Cells hücre değerlerini varsayılan olarak string olarak ele alır. Ham dönem metnini ekleyerek, bir Japon müşterisinin tarihleri yerel takviminde girdiği gerçek bir senaryoyu taklit ediyoruz.

## Step 2: Enable Japanese Era Parsing and Extract the Date  

Aspose.Cells, Japon dönemi dizelerini .NET `DateTime` nesnelerine otomatik olarak çevirebilir—tek yapmanız gereken bunu etkinleştirmektir. `DateTimeParseOptions.EnableJapaneseEra` bayrağı bu işi yapar.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Pro tip:** `EnableJapaneseEra` seçeneğini unutursanız, kütüphane orijinal stringi döndürür ve sonraki dönüşümünüz başarısız olur. Karışık içeriklerle çalışıyorsanız her zaman `parsed.Type` kontrol edin.

## Step 3: Convert the Parsed DateTime to ISO 8601  

Artık geçerli bir `DateTime`'ımız olduğuna göre, onu ISO‑formatlı bir stringe dönüştürmek çok kolay. `"yyyy-MM-dd"` deseni ISO 8601 tarih kısmına uygundur ve çoğu API bu formatı bekler.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Programı çalıştırdığınızda şu çıktı gelir:

```
ISO date: 2021-05-01
```

İşte aradığınız **display iso date**.

## Full, Runnable Example  

Aşağıda doğrudan bir console projesine yapıştırabileceğiniz tam kod bloğu yer alıyor. Gizli bağımlılık yok, ekstra yapılandırma yok.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Expected output:** `ISO date: 2021-05-01`

## Step‑by‑Step Breakdown (Why Each Piece Matters)

| Adım | Ne Olur | Neden Önemli |
|------|---------|--------------|
| **Create workbook** | Bellekte bir Excel konteyneri başlatır. | Dosya sistemine dokunmadan test edebileceğiniz bir sandbox sağlar. |
| **PutValue** | Ham Japon dönemi stringini **A1** hücresine yazar. | Gerçek veri girişini taklit eder; ayrıştırıcının tam metni görmesini sağlar. |
| **GetValue with `EnableJapaneseEra`** | Dönem stringini .NET `DateTime`'a çevirir. | Takvim dönüşümünü otomatik yapar—manuel lookup tablolarına gerek kalmaz. |
| **`ToString("yyyy-MM-dd")`** | `DateTime`'ı ISO 8601 formatına getirir. | REST API'leri, veritabanları vb. tarafından kabul edilen kültür‑bağımsız, sıralanabilir bir tarih stringi garantiler. |
| **Console.WriteLine** | Son ISO tarihi gösterir. | Bütün pipeline'ın uçtan uca çalıştığını doğrular. |

## Handling Common Variations  

### 1. Different Cell Locations  

Tarihiniz **B2** veya bir adlandırılmış aralıkta ise, sadece `"A1"` yerine uygun adresi koyun:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Multiple Dates in a Column  

Birçok satır için **extract date from excel** yapmanız gerektiğinde, kullanılan aralıkta döngü oluşturun:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Fallback for Non‑Era Dates  

Bir hücre zaten standart bir tarih stringi içeriyorsa, ayrıştırıcı yine çalışır, ancak bir güvenlik önlemi eklemek isteyebilirsiniz:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

`TryParse` bayrağı istisnaları önler ve dönüşüm başarısız olursa orijinal değeri döndürür.

### 4. Time Component  

Zaman kısmına da ihtiyacınız varsa, `"yyyy-MM-ddTHH:mm:ss"` kullanın:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Bu, tam bir ISO 8601 zaman damgası üretir (`2021-05-01T00:00:00`).

## Visual Aid  

![format datetime to iso example](image.png "C#'ta datetime'ı iso formatına örnek bir gösterim")

*Alt metin:* *format datetime to iso örneği, konsol çıktısını gösteriyor*

## Frequently Asked Questions  

- **Can I use this with .xls files?**  
  Evet. Aspose.Cells, `.xls`, `.xlsx`, `.csv` ve birçok diğer formatı kutudan çıkar çıkmaz destekler.

- **What if the workbook is password‑protected?**  
  `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })` ile yükleyin.

- **Is the ISO format locale‑dependent?**  
  Hayır. `"yyyy-MM-dd"` deseni kültür‑bağımsızdır ve herhangi bir makinede aynı stringi üretir.

- **Does this work on .NET Core?**  
  Kesinlikle—Aspose.Cells .NET Standard 2.0 uyumludur.

## Wrap‑Up  

**format datetime to iso** yapmayı, **extract date from excel** ile Japon dönemi stringlerini ayrıştırarak ve sonunda **display iso date**'i konsolda göstermeyi ele aldık. Temel adımlar—çalışma kitabı oluşturma, dönem metnini yazma veya yükleme, Japon dönemi ayrıştırmayı etkinleştirme ve `ToString("yyyy-MM-dd")` ile formatlama—çoğu senaryo için yeterlidir.

Sonraki adımlarınız şunlar olabilir:

- ISO tarihlerini başka bir sütuna yazarak sonraki işlemlere hazırlama.
- Dönüştürülmüş çalışma kitabını toplu içe aktarma için CSV'ye dışa aktarma.
- Excel yüklemelerini kabul eden ve JSON‑kodlu ISO tarihleri dönen bir web API ile bu mantığı birleştirme.

Farklı tarih formatları, saat dilimleri veya hatta özel takvimlerle denemeler yapmaktan çekinmeyin. Aspose.Cells'in esnekliği sayesinde nadiren bir duvara çarparsınız.

İyi kodlamalar, ve tüm tarihlerinizi mükemmel ISO‑uyumlu olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}