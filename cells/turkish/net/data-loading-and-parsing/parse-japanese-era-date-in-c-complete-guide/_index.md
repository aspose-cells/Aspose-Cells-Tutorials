---
category: general
date: 2026-06-27
description: C#'ta Japon era tarihini nasıl ayrıştıracağınızı ve ardından datetime'ı
  yyyy-aa-gg formatında ISO çıktısı için nasıl biçimlendireceğinizi öğrenin. Adım
  adım kod, kenar durumları ve ipuçları.
draft: false
keywords:
- parse japanese era date
- format datetime yyyy-mm-dd
- C# JapaneseCalendar
- CultureInfo date parsing
- .NET DateTime era handling
language: tr
og_description: C#'de Japon dönemi tarihini ayrıştırın ve datetime'ı yyyy‑mm‑dd biçiminde
  zahmetsizce formatlayın. Açıklamalar ve dikkat edilmesi gereken noktalarla tam örnek.
og_title: C#'ta Japon dönem tarihini ayrıştır – Tam Programlama Rehberi
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
title: C#'ta Japon dönemi tarihini ayrıştırma – Tam Rehber
url: /tr/net/data-loading-and-parsing/parse-japanese-era-date-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Japon Dönemi Tarihini Ayrıştırma – Tam Kılavuz

Hiç .NET uygulamasında **Japon dönemi tarihini ayrıştırmanız** gerekti ve sonucun neden yanlış göründüğünü merak ettiniz mi? Yalnız değilsiniz. Birçok eski sistemde tarihler “R3‑04‑01” biçiminde gelir ve bunları API'ler veya veritabanları için temiz bir **format datetime yyyy-mm-dd** dizesine dönüştürmeniz gerekir.  

Bu öğreticide bunu başarmak için tam adımları gösterecek, her parçanın neden önemli olduğunu açıklayacak ve geliştiricileri sık sık zorlayan zor kenar durumlarını nasıl ele alacağınızı göstereceğiz.

> **Not:** Tüm kod, .NET 6 veya daha yeni bir sürümü hedefleyen bir konsol uygulamasına kopyala‑yapıştır yapmaya hazırdır.

## Gerekenler

- .NET 6 SDK (veya herhangi bir yeni sürüm)
- C# ve `System.Globalization` ad alanına temel aşinalık
- Bir IDE veya editör – Visual Studio, VS Code, Rider, neyi tercih ederseniz

Harici NuGet paketlerine gerek yok; her şey BCL içinde bulunur.

## Adım 1: Japon Kültürünü İmparatorluk Takvimiyle Ayarlama

İlk olarak, Japon imparatorluk takvimini bilen bir `CultureInfo`'a ihtiyacımız var. Varsayılan olarak `ja-JP` Gregoryen takvimini kullanır, bu yüzden `DateTimeFormat.Calendar` özelliğini bir `JapaneseCalendar` örneğiyle değiştiriyoruz.

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

> **Neden önemli:** `JapaneseCalendar`, “R” (Reiwa) gibi dönem sembollerini doğru Gregoryen yıla çevirir. Olmasaydı, `DateTime.Parse` bir `FormatException` fırlatırdı.

## Adım 2: Döneme Dayalı Tarih Dizesini Ayrıştırma

Şimdi `"R3-04-01"` gibi bir dizeyi `DateTime.Parse`'a verebiliriz. Az önce yapılandırdığımız kültür, “R3” kısmını nasıl yorumlayacağını parser'a söyler.

```csharp
        // Step 2: Parse a date string that uses the Japanese era format (e.g., "R3-04-01")
        string eraDate = "R3-04-01";
        DateTime parsedDate = DateTime.Parse(eraDate, japaneseCulture);
```

Eğer hatalı girişlerde istisna atılmasını önlemek isterseniz, `Parse` yerine `TryParseExact` kullanın:

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

> **İpucu:** Özel format dizesi `"ggy-MM-dd"` parser'a tam olarak ne beklediğini söyler. “gg” dönem tasvircisi, “y” ise o dönemdeki yılı temsil eder.

## Adım 3: Sonucu ISO 8601'e Dönüştürme (`format datetime yyyy-mm-dd`)

Son olarak, `DateTime`'ı standart bir ISO formatında çıktılarız. `"yyyy-MM-dd"` format belirteci tam olarak bunu yapar.

```csharp
        // Step 3: Display the parsed date in a standard ISO format
        string isoDate = parsedDate.ToString("yyyy-MM-dd", CultureInfo.InvariantCulture);
        Console.WriteLine(isoDate); // Expected output: 2021-04-01
    }
}
```

Programı çalıştırdığınızda şu çıktı alınır:

```
2021-04-01
```

Bu, **format datetime yyyy-mm-dd** istediğiniz ve JSON yükleri, SQL eklemeleri veya herhangi bir downstream sistem için hazır olan formattır.

![Japon dönem tarihini ayrıştırma örneği](placeholder.png){alt="Japon dönem tarihini ayrıştırma örneği"}

## Diğer Dönemler ve Kenar Durumlarını Ele Alma

### Birden Çok Dönem

Japonya birçok dönemi (Meiji, Taishō, Shōwa, Heisei, Reiwa) yaşamıştır. `JapaneseCalendar` bunları otomatik olarak eşler, bu yüzden `"H30-12-31"` (Heisei 30) `2018-12-31` olur. Aynı ayrıştırma mantığını tutun; takvim ağır işi yapar.

### Geçersiz Girdi

Bir dize beklenen desenle eşleşmezse `Parse` bir istisna fırlatır. Daha önce gösterildiği gibi `TryParseExact` kullanın veya bir düzenli ifadeyle ön‑doğrulama yapın:

```csharp
bool IsValidEraDate(string input) =>
    System.Text.RegularExpressions.Regex.IsMatch(
        input, @"^[RHS][0-9]+-\d{2}-\d{2}$", System.Text.RegularExpressions.RegexOptions.IgnoreCase);
```

### Zaman Dilimleri

`DateTime` nesneleri varsayılan olarak “kind‑agnostic”tir. UTC zaman damgasına ihtiyacınız varsa şu çağrıyı yapın:

```csharp
DateTime utc = DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc);
```

Ya da tam bölge farkı için `DateTimeOffset` kullanın.

## Tam Çalışan Örnek

Yeni bir konsol projesine yapıştırabileceğiniz tüm kod parçacığı aşağıdadır:

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

**Beklenen konsol çıktısı**

```
Original era date: R3-04-01
Converted ISO date: 2021-04-01
```

## Özet

**Japon dönemi tarih** dizelerini şu adımlarla **parse** ettik:

1. `ja-JP` için bir `CultureInfo` oluşturup `JapaneseCalendar` ile değiştirdik.
2. `DateTime.Parse` ya da daha dayanıklı `TryParseExact` ile özel bir format kullandık.
3. Sonuç `DateTime`'ı `"yyyy-MM-dd"` ile biçimlendirerek istediğiniz **format datetime yyyy-mm-dd** elde ettik.

Bu, eski Japon dönemi verilerini modern ISO‑uyumlu sistemlere bağlamak için ihtiyacınız olan her şey.

## Sıradaki Adımlar

- **Toplu işleme:** Bir CSV dosyasındaki dönem tarihlerini döngüyle okuyup ISO dizelerini veritabanına yazın.
- **Yerelleştirme:** ISO tarihlerini UI gösterimi için tekrar dönem formatına çevirin (`ToString("ggyy年MM月dd日", japaneseCulture)`).
- **Özel takvimler:** Diğer bölgesel ihtiyaçlar için `TaiwanCalendar` veya `HijriCalendar` keşfedin.

Denemeler yapın—dönem dizesini değiştirin, kenar durumlarını test edin veya bu mantığı ASP.NET Core uç noktalarına entegre edin. Bir sorunla karşılaşırsanız, aşağıya yorum bırakın; iyi kodlamalar!

## Sonra Ne Öğrenmeli?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, projelerinizde ek API özelliklerini ustalaşmanız ve alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalar ve tam çalışan kod örnekleri içerir.

- [Aspose.Cells Kullanarak .NET'te Tarih Doğrulamasını Nasıl Uygularsınız: Kapsamlı Bir Kılavuz](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)
- [Aspose.Cells .NET ile Excel Tarih Sistemini 1904'e Değiştirme](/cells/english/net/calculation-engine/change-excel-date-system-aspose-cells-net/)
- [Aspose.Cells for .NET Kullanarak Excel Yorumlarını Uygulama ve Biçimlendirme: Adım Adım Kılavuz](/cells/english/net/comments-annotations/implement-format-excel-comments-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}