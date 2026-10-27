---
category: general
date: 2026-09-24
description: Aspose.Cells kullanarak C#'de Japon İmparatorluk Dönemi ile DateTime
  ayrıştırın. Japon era takvimini etkinleştirin, era dizgilerini yazın ve doğru DateTime
  değerlerini alın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: tr
lastmod: 2026-09-24
og_description: C#'ta Aspose.Cells kullanarak Japon İmparatorluk Dönemi ile DateTime'ı
  ayrıştırın. Bu öğreticide Japon era takvimini nasıl etkinleştireceğiniz, era metinlerini
  nasıl yazacağınız ve doğru bir DateTime'ı nasıl geri okuyacağınız gösterilmektedir.
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Aspose.Cells kullanarak Japon İmparatorluk Dönemi ile DateTime ayrıştırma
  – C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Aspose.Cells kullanarak Japon İmparatorluk Dönemi ile DateTime'ı ayrıştır
url: /tr/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japon İmparatoru Dönemi ile DateTime Ayrıştırma – Aspose.Cells

Bir .NET uygulamasında **Japon İmparatoru Dönemi ile DateTime ayrıştırma** ihtiyacınız varsa, bu rehber Aspose.Cells ile bunu nasıl yapacağınızı adım adım gösterir. Japon era takvimini etkinleştirerek, era‑bazlı bir dize yazarak ve ortaya çıkan `DateTime` değerini okuyarak, manuel dize işleme ihtiyacını ortadan kaldıran güvenilir, kültüre duyarlı tarihler elde edersiniz.

Japon era tarihleriyle çalışmak, “令和3年5月10日” gibi tarihlerin hâlâ saklandığı finans, devlet ve eski sistemlerde yaygındır. Bu öğretici, proje kurulumundan hesaplamalar, günlük kaydı veya UI gösterimi için kullanabileceğiniz bir `DateTime` nesnesi elde etmeye kadar tam süreci kapsar.

## Öğrenecekleriniz

- Bir C# projesine Aspose.Cells NuGet paketini nasıl ekleyeceğinizi.  
- `Workbook.Settings` üzerinden **Japon era takvimini** nasıl etkinleştireceğinizi.  
- Japon era tarih dizesini bir hücreye yazarak Aspose.Cells’in otomatik olarak ayrıştırmasını nasıl sağlayacağınızı.  
- Ayrıştırılan `DateTime` değerini `DateTimeValue` özelliğiyle nasıl okuyacağınızı.  

**Önkoşullar**  
- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır).  
- C# ve Visual Studio (veya herhangi bir IDE) konusunda temel bilgi.  
- Aspose.Cells paketini indirmek için internet erişimi.

---

## Adım 1: Aspose.Cells’i Yükleyin

Proje klasörünüzü bir terminalde ya da NuGet Package Manager Console’da açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.Cells
```

Ya da Visual Studio’da projeye sağ‑tıklayın → **Manage NuGet Packages** → **Aspose.Cells** aratın ve **Install**’a tıklayın.  
Bu, `Workbook`, `Worksheet` ve ihtiyacımız olan ayrıştırma yeteneklerini sağlayan `Aspose.Cells` derlemesini ekler.

## Adım 2: Japon era takvimini etkinleştirin

Aspose.Cells, Japon era ayrıştırmasını varsayılan olarak devre dışı bırakır. `Workbook.Settings.UseJapaneseEraCalendar` bayrağıyla bunu açmanız gerekir.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

`UseJapaneseEraCalendar` değerini `true` yapmak, kütüphaneye era adlarını (`令和`, `平成`, `昭和` vb.) resmi Japon takvim kurallarına göre yorumlamasını söyler.

## Adım 3: Bir hücreye Japon era tarih dizesi yazın

Şimdi, ilk çalışma sayfasını alın ve Japon era tarih dizesini **A1** hücresine yerleştirin.

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**Neden çalışır:**  
`UseJapaneseEraCalendar` aktif olduğunda, `PutValue` dizeyi inceler, era ön ekini (`令和`) algılar ve dahili olarak karşılık gelen Gregoryen yıla (2021) dönüştürür. Kütüphane değeri yalnızca metin olarak değil, gerçek bir `DateTime` nesnesi olarak saklar.

## Adım 4: Ayrıştırılan `DateTime` değerini alın

Şimdi hücrenin `DateTimeValue` özelliğini okuyun. Aspose.Cells otomatik olarak Gregoryen tarihi döndürür.

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Programı çalıştırdığınızda şu çıktı elde edilir:

```
Parsed Gregorian date: 2021-05-10
```

Çıktı, **Japon İmparatoru Dönemi ile DateTime Ayrıştırma** işleminin “令和3年5月10日” tarihini 10 Mayıs 2021 olarak doğru bir şekilde dönüştürdüğünü doğrular.

## Adım 5: Kenar durumları ve yaygın varyasyonları ele alın

### Birden çok era formatı
Aspose.Cells, çeşitli era temsillerini tanır:

| Dönem (Japonca) | Gregoryen yıl aralığı |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑günümüz         |

Kaynak veriniz tam‑geniş karakterler, boşluklar veya “年”, “月”, “日” kanjileri içeriyorsa, ayrıştırıcı yine başarılı olur. Örneğin, `"平成31年4月30日"` `2019-04-30` olur.

### Geçersiz dizeler
Dize ayrıştırılamadığında (ör. `"令和99年13月40日"`), `DateTimeValue` `DateTime.MinValue` döndürür. Bu durumu kontrol edebilirsiniz:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### Özelliği devre dışı bırakma
Daha sonra dönüştürülmemiş era dizelerini saklamanız gerekirse, bayrağı tekrar `false` yapın:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### Performans ipucu
Era takvimini etkinleştirmek, dize içeren her `PutValue` çağrısına küçük bir ek yük getirir. Sadece birkaç hücreyi ayrıştırıyorsanız, işlemin hemen öncesinde bayrağı açıp sonrasında kapatarak etkisini en aza indirebilirsiniz.

## Tam, çalıştırılabilir örnek

Aşağıda, kopyalayıp anında çalıştırabileceğiniz tam program yer alıyor.

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**Beklenen çıktı**

```
Parsed Gregorian date: 2021-05-10
```

Program, **Japon İmparatoru Dönemi ile DateTime Ayrıştırma** sürecini Aspose.Cells kullanarak, çalışma kitabı oluşturulmasından kullanılabilir bir `DateTime` nesnesi elde edilmesine kadar uçtan uca gösterir.

---

## Sonuç

Artık C# içinde **Japon İmparatoru Dönemi ile DateTime Ayrıştırma** işlemini şu adımlarla yapabilirsiniz:

1. **Aspose.Cells**’i kurun.  
2. `Workbook.Settings` üzerinden **Japon era takvimini** etkinleştirin.  
3. Era‑bazlı dizeleri hücrelere yazın.  
4. Ortaya çıkan `DateTimeValue`’yu okuyun.  

Bu yaklaşım, manuel ayrıştırma mantığını ortadan kaldırır, resmi era sınırlarına saygı gösterir ve mevcut .NET tarih‑işleme kodlarıyla sorunsuz bütünleşir.  

**Sonraki adımlar**  
- Aspose.Cells’in **Hijri** veya **Thai Buddhist** takvimleri gibi diğer kültüre özgü özelliklerini keşfedin.  
- Bu tekniği, era tarihlerine referans veren formülleri değerlendirmek için `CalcEngine` gibi **Workbook Settings** ile birleştirin.  
- Ayrıştırılan `DateTime` değerini raporlama, veritabanı depolama veya Gregorian tarih gerektiren UI bileşenlerinde kullanın.

Farklı era dizelerini deneyin, geçersiz girdileri yönetin ve çözümü daha büyük veri‑import hatlarına entegre edin. Kodlamanın tadını çıkarın!


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak ilgili konuları ayrıntılı bir şekilde ele alır. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to Parse Japanese Dates in C# – Complete Guide](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [How to Implement Date Validation in .NET Using Aspose.Cells: A Comprehensive Guide](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}