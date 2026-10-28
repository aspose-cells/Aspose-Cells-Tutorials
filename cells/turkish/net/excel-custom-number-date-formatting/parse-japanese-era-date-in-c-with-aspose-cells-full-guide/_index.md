---
category: general
date: 2026-06-08
description: Aspose.Cells kullanarak C#'de Japon era tarihini ayrıştırın. CultureInfo
  ja-JP ve Japon era formatının doğru Excel tarih dönüşümünü nasıl sağladığını öğrenin.
draft: false
keywords:
- parse japanese era date
- Aspose.Cells
- CultureInfo ja-JP
- Japanese era format
- Excel date conversion
- C# DateTime parsing
language: tr
og_description: C#'ta Japon era tarihini hızlıca ayrıştırın. Bu öğreticide CultureInfo
  ja-JP ve Aspose.Cells'in era dizelerini doğru DateTime nesnelerine nasıl dönüştürdüğü
  gösterilmektedir.
og_title: C#'da Japon Dönemi Tarihini Ayrıştır – Aspose.Cells Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  headline: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  type: TechArticle
- description: Parse Japanese era date in C# using Aspose.Cells. Learn how CultureInfo
    ja-JP and Japanese era format enable accurate Excel date conversion.
  name: Parse Japanese Era Date in C# with Aspose.Cells – Full Guide
  steps:
  - name: 5.1 Invalid or Empty Strings
    text: '```csharp string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString();
      // could be empty if (string.IsNullOrWhiteSpace(maybeDate)) { Console.WriteLine("Cell
      B1 is empty – skipping."); } else { // Attempt to parse; catch format exceptions
      try { DateTime dt = DateTime.Parse(maybeDate, new Cultur'
  - name: 5.2 Older Eras (Showa, Taisho)
    text: 'The same `CultureInfo ja-JP` works for older eras automatically:'
  - name: 5.3 Using `DateTime.ParseExact` for Strict Validation
    text: 'If you want to enforce the exact Japanese era pattern, use a custom format
      string:'
  type: HowTo
- questions:
  - answer: Yes. As long as the workbook’s `Settings.CultureInfo` is set to `ja-JP`
      *before* you call `GetDateTime()`, Aspose.Cells will interpret the existing
      strings correctly.
    question: Does this work with .xlsx files that already contain era dates?
  - answer: The parsing returns a `DateTime` with `Kind = Unspecified`. If you need
      UTC or local time, apply `DateTime.SpecifyKind` or convert after parsing.
    question: What about time zones?
  - answer: Absolutely. Loop through the desired range and call `GetDateTime()` on
      each cell—just remember to handle exceptions for malformed entries.
    question: Can I parse multiple cells at once?
  type: FAQPage
tags:
- C#
- Excel
- DateTime
- Localization
title: Aspose.Cells ile C#'ta Japon Dönemi Tarihini Ayrıştırma – Tam Kılavuz
url: /tr/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.Cells Kullanarak Japon Dönemi Tarihini Ayrıştırma – Tam Kılavuz

Excel sayfasından doğrudan **parse japanese era date** dizelerini ayrıştırmanız gerektiği oldu mu? Belki hâlâ “令和3年5月12日” kullanan eski bir sistemden veri çekiyorsunuz ve raporları çalıştırmak için temiz bir `DateTime` istiyorsunuz. Bu öğreticide, bu dönem‑biçimli dizeleri doğru C# tarihlerine dönüştüren, tamamen hazır‑çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz—tahmine gerek yok.

Aspose.Cells ve Japon dönemlerini okuyabilen **CultureInfo ja-JP** ayarını birlikte kullanacağız. Sonunda “令和”, “平成” ve hatta daha eski dönemleri sorunsuz bir şekilde işleyen yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.6+ üzerinde de çalışır)  
- Aspose.Cells for .NET (ücretsiz deneme NuGet paketini alabilirsiniz: `Install-Package Aspose.Cells`)  
- Temel C# bilgisi—fanteziye gerek yok, sadece bir console uygulaması yeterli  
- Tercih ettiğiniz bir IDE (Visual Studio, Rider, VS Code, vb.)

Hepsi bu. Ekstra hizmet yok, gizli üçüncü‑taraf ayrıştırıcılar yok.

## Adım 1: Projeyi Kurun ve Aspose.Cells'i Ekleyin

İlk olarak, yeni bir console projesi oluşturun:

```bash
dotnet new console -n JapaneseEraParser
cd JapaneseEraParser
dotnet add package Aspose.Cells
```

Şimdi **Program.cs** dosyasını açın ve gerekli ad alanlarını ekleyin:

```csharp
using System;
using System.Globalization;
using Aspose.Cells;
```

> **Pro tip:** Visual Studio kullanıyorsanız, IDE sınıf adlarını yazdıktan sonra `using` ifadelerini otomatik olarak önerecektir.

## Adım 2: Bir Çalışma Kitabı Oluşturun ve Japon Kültürünü Uygulayın

**parse japanese era date**'i doğru bir şekilde ayrıştırmanın anahtarı, Aspose.Cells'e hangi kültürü kullanacağını söylemektir. `CultureInfo`'i `ja-JP` olarak ayarlamak, dönem‑bilgili ayrıştırmayı etkinleştirir.

```csharp
// Step 2: Initialize a new workbook and set Japanese culture
Workbook workbook = new Workbook();
workbook.Settings.CultureInfo = new CultureInfo("ja-JP");
```

Bu neden önemli? Japon takviminde birden fazla dönem vardır (ör. *Reiwa* (令和), *Heisei* (平成)). `CultureInfo` nesnesi, her dönemin başlangıç tarihlerini bilen bir `JapaneseCalendar` içerir, bu sayede Japon dönemi formatını izleyen herhangi bir dize doğru şekilde yorumlanabilir.

## Adım 3: Bir Hücreye Japon Dönemi Tarihi Dizesi Yazın

Örnek bir dönem tarihini **A1** hücresine ekleyelim. Farklı dönemleri test etmek için dizeyi istediğiniz gibi değiştirebilirsiniz.

```csharp
// Step 3: Put a Japanese era date string into A1
string japaneseDate = "令和3年5月12日"; // Reiwa 3, May 12, 2021
workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);
```

Mevcut bir çalışma kitabı ile çalışmayı tercih ediyorsanız, `new Workbook("path/to/file.xlsx")` ile yükleyebilir ve oluşturma adımını atlayabilirsiniz.

## Adım 4: Değeri C# DateTime Nesnesi Olarak Alın

Şimdi sihir gerçekleşir. `GetDateTime()` çağrısıyla, Aspose.Cells hücreyi önceden ayarlanmış `CultureInfo` ile okur ve uygun bir `DateTime` döndürür.

```csharp
// Step 4: Parse the cell value into a DateTime
DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
```

**Expected output**

```
Parsed DateTime: 2021-05-12
```

Bu, **parse japanese era date** akışının tamamı—dört özlü kod satırı.

## Adım 5: Kenar Durumlarını ve Alternatif Dönemleri Ele Alma

Gerçek dünyadaki veriler her zaman temiz değildir. İşte karşılaşabileceğiniz birkaç senaryo ve bunları nasıl ele alacağınız.

### 5.1 Geçersiz veya Boş Dizeler

```csharp
string maybeDate = workbook.Worksheets[0].Cells["B1"].GetString(); // could be empty
if (string.IsNullOrWhiteSpace(maybeDate))
{
    Console.WriteLine("Cell B1 is empty – skipping.");
}
else
{
    // Attempt to parse; catch format exceptions
    try
    {
        DateTime dt = DateTime.Parse(maybeDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"B1 parsed as {dt:yyyy-MM-dd}");
    }
    catch (FormatException)
    {
        Console.WriteLine($"Unable to parse '{maybeDate}' as a Japanese era date.");
    }
}
```

### 5.2 Daha Eski Dönemler (Showa, Taisho)

Aynı `CultureInfo ja-JP` eski dönemler için otomatik olarak çalışır:

```csharp
string showaDate = "昭和45年12月31日"; // Showa 45 = 1970-12-31
DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
Console.WriteLine(showaParsed.ToString("yyyy-MM-dd")); // 1970-12-31
```

### 5.3 Katı Doğrulama İçin `DateTime.ParseExact` Kullanımı

Tam Japon dönemi desenini zorlamak istiyorsanız, özel bir format dizesi kullanın:

```csharp
string pattern = "ggggy年M月d日"; // gggg = era name, y = year in era
DateTime strictDate = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
Console.WriteLine(strictDate); // 2021-05-12 00:00:00
```

Bu yaklaşım, dize farklılaştığında bir `FormatException` fırlatır; bu, veri kalitesi kontrolleri için faydalı olabilir.

## Tam Çalışan Örnek

Aşağıda, **Program.cs** dosyasına kopyalayıp yapıştırabileceğiniz ve çalıştırabileceğiniz tam program yer alıyor.

```csharp
using System;
using System.Globalization;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and set Japanese culture
        Workbook workbook = new Workbook();
        workbook.Settings.CultureInfo = new CultureInfo("ja-JP");

        // 2️⃣ Insert a Japanese era date string
        string japaneseDate = "令和3年5月12日";
        workbook.Worksheets[0].Cells["A1"].PutValue(japaneseDate);

        // 3️⃣ Parse the cell value into DateTime
        DateTime parsedDate = workbook.Worksheets[0].Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");

        // 4️⃣ Demonstrate handling an older era
        string showaDate = "昭和45年12月31日";
        DateTime showaParsed = DateTime.Parse(showaDate, new CultureInfo("ja-JP"));
        Console.WriteLine($"Showa parsed: {showaParsed:yyyy-MM-dd}");

        // 5️⃣ Strict parsing with ParseExact
        string pattern = "gggy年M月d日";
        try
        {
            DateTime strict = DateTime.ParseExact(japaneseDate, pattern, new CultureInfo("ja-JP"));
            Console.WriteLine($"Strict parse: {strict:yyyy-MM-dd}");
        }
        catch (FormatException ex)
        {
            Console.WriteLine($"Strict parse failed: {ex.Message}");
        }
    }
}
```

`dotnet run` ile çalıştırın ve şunu görmelisiniz:

```
Parsed DateTime: 2021-05-12
Showa parsed: 1970-12-31
Strict parse: 2021-05-12
```

Boom—**parse japanese era date** tamam, ve karşılaşabileceğiniz herhangi bir dönem için bir şablonunuz oldu.

![Japon Dönemi Tarihi Ayrıştırma iş akışı – çalışma kitabı oluşturulması, kültür ayarı, hücre yazımı ve GetDateTime çağrısını gösterir](parse-japanese-era-date.png "Aspose.Cells ve CultureInfo ja-JP kullanarak japon dönemi tarihini nasıl ayrıştıracağınızı gösteren diyagram")

## Sık Sorulan Sorulara Yanıtlar

- **Bu, zaten dönem tarihleri içeren .xlsx dosyalarıyla çalışır mı?**  
  Evet. Çalışma kitabının `Settings.CultureInfo` özelliği `GetDateTime()` çağırmadan *önce* `ja-JP` olarak ayarlandığı sürece, Aspose.Cells mevcut dizeleri doğru şekilde yorumlayacaktır.

- **Zaman dilimleri hakkında ne söyleyebiliriz?**  
  Ayrıştırma, `Kind = Unspecified` olan bir `DateTime` döndürür. UTC veya yerel zaman gerekiyorsa, `DateTime.SpecifyKind` uygulayın veya ayrıştırmadan sonra dönüştürün.

- **Birden fazla hücreyi aynı anda ayrıştırabilir miyim?**  
  Kesinlikle. İstediğiniz aralıkta döngü yapıp her hücrede `GetDateTime()` çağırabilirsiniz—yalnızca hatalı girişler için istisnaları yakalamayı unutmayın.

## Sonuç

Aspose.Cells ve yerleşik `CultureInfo ja-JP` kullanarak C# içinde **parse japanese era date** dizelerini ayrıştırmak için ihtiyacınız olan her şeyi ele aldık. Çalışma kitabını kurmaktan, dönem‑biçimli dizeleri yazmaya, temiz bir `DateTime` almaya, eski dönemler ve katı doğrulama gibi kenar durumlarını ele almaya kadar—bu kılavuz size üretim‑hazır bir çözüm sunar.

Sonraki adımda, sayısal seri tarihleri için **Excel date conversion**'ı keşfedebilir veya diğer yerel ayarlar için özel takvimlerle **C# DateTime parsing**'e dalabilirsiniz. Aynı desen Tay Budist takvimi, İbrani takvimi ve daha fazlası için de çalışır—sadece `CultureInfo`'i değiştirin.

Karşılaştığınız bir zorluk var mı? Yorum bırakın, birlikte çözümleyelim. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells Kullanarak .NET'te Tarih Doğrulamasını Nasıl Uygularsınız: Kapsamlı Rehber](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Aspose.Cells .NET ile Excel Tarih Sistemini 1904'e Değiştirme](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Aspose.Cells for Java Kullanarak Özel Tarih Formatlarıyla Excel'i PDF'e Verimli Şekilde Dönüştürme](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}