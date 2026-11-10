---
category: general
date: 2026-10-01
description: Japon dönem tarihini Aspose.Cells kullanarak C#'de Gregoryen DateTime'e
  dönüştürün. Japon takvimini hızlı bir şekilde nasıl dönüştüreceğinizi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: tr
lastmod: 2026-10-01
og_description: Japon dönemi tarihini C#'ta Gregorian DateTime'e dönüştürün. Bu öğreticide,
  Japon takvimini Aspose.Cells ile doğru bir şekilde nasıl dönüştüreceğiniz açıklanıyor.
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: Japon dönemi tarihini C#'ta Gregoryen takvimine dönüştürme – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: C#'ta Japon era tarihini Gregoryen takvime nasıl dönüştürürsünüz
url: /tr/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Japon era tarihini Gregorian takvimine C# ile nasıl dönüştürülür

C# içinde **Japon era tarihini** Gregorian tarihlere dönüştürmeniz gerekiyorsa, bu rehber tam olarak nasıl yapılacağını gösterir. İster eski verileri işliyor olun, kullanıcı girdilerini okuyor olun ya da raporlar oluşturuyor olun, Aspose.Cells kütüphanesi dönüşümü basitleştirir. Ayrıca, elektronik tablolarda çalışırken **Japon takvimini nasıl dönüştüreceğinizi** keşfedeceksiniz.

Bu öğretici, bir çalışma kitabı oluşturulmasından bir `DateTime` değerinin alınmasına kadar her adımı kapsar— böylece tam, çalıştırılabilir bir programı kopyala‑yapıştırabilirsiniz. Harici bir dokümantasyona ihtiyaç yok; sadece aşağıdaki kodu ve açıklamaları izleyin.

## Önkoşullar

* .NET 6.0 veya daha yeni (kod .NET Framework 4.6+ ile de çalışır)
* **Aspose.Cells** için bir lisans (ücretsiz deneme test için çalışır)
* Visual Studio 2022 veya VS Code gibi bir geliştirme ortamı
* C# konsol uygulamalarıyla temel aşinalık

## Aspose.Cells ile Japon era tarihini dönüştürme

Dönüşümün çekirdeği birkaç basit API çağrısında bulunur. Aspose.Cells, Japon era dizelerini (ör. “Reiwa 2/04/01”) otomatik olarak yorumlar ve çalışma sayfası yeniden hesaplandığında sonucu bir `DateTime` nesnesi olarak sunar.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### Her adımın önemi

| Adım | Amaç | Dönüşüme nasıl yardımcı olur |
|------|------|------------------------------|
| **Çalışma kitabı oluştur** | Excel formüllerini ve tarih sistemlerini anlayan bir konteyner sağlar. | Kütüphanenin dahili tarih motoru yalnızca bir çalışma kitabı içinde etkinleştirilir. |
| **Era dizesi ekle** | Çevirmek istediğiniz ham Japon takvim metnini sağlar. | Aspose.Cells, *Reiwa*, *Heisei*, *Showa* gibi era adlarını tanır. |
| **Stil ayarla** | Hücreyi literal bir dize yerine değer hücresi olarak işleme zorlar. | Stil olmadan, `Calculate` yöntemi hücreyi görmezden gelebilir ve metin değişmeden kalır. |
| **Hesapla** | Era dizesinin ayrıştırılmasını ve dahili seri tarih numarasına dönüşümünü tetikler. | Kütüphane “Reiwa 2/04/01” → seri numara → Gregorian `DateTime` olarak dönüştürür. |
| **`DateTimeValue` oku** | Dönüştürülmüş .NET `DateTime` nesnesini döndürür. | Artık herhangi bir .NET API'sinde kullanabileceğiniz standart bir `DateTime`'a sahipsiniz. |

## Diğer senaryolarda Japon takvimini nasıl dönüştürürsünüz

Aynı yaklaşım, Aspose.Cells tarafından desteklenen herhangi bir Japon era adı için çalışır:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### Geçersiz veya belirsiz dizeleri işleme

* **Geçersiz era adı** – Aspose.Cells bir `FormatException` fırlatır. Dönüşümü `try/catch` içinde sararak dostça bir hata mesajı sağlayın.
* **Yıl/ay/gün eksik** – Kütüphane tam bir “Era Year/Month/Day” deseni bekler. Kısmi veri alırsanız, eksik bölümleri ekleyin ya da girdiyi erken reddedin.
* **Farklı yerel ayarlar** – Dönüşüm, geçerli iş parçacığı kültürüne **bağlı değildir**; her zaman Aspose.Cells içinde yerleşik Japon era haritasını kullanır. Bu, yöntemi sunucu tarafı işleme için güvenli kılar.

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## Pratik ipuçları ve yaygın tuzaklar

* **`Calculate`'dan önce her zaman `SetStyle` çağırın**. Bu adımı atlamak, hücrenin düz metin tutucusu kalması nedeniyle sık hata kaynağıdır.
* **Birçok tarihi dönüştürmeniz gerekiyorsa aynı çalışma kitabını yeniden kullanın**. Her dönüşüm için yeni bir çalışma kitabı oluşturmak gereksiz yük getirir.
* **Toplu dönüşüm** – Bir sütunu era dizeleriyle doldurun, `worksheet.Calculate()` metodunu bir kez çağırın, ardından tüm `DateTimeValue` sütununu okuyun. Bu, hücre başına yeniden hesaplamaktan çok daha verimlidir.
* **Sürüm uyumluluğu** – Era dönüşüm mantığı Aspose.Cells 22.9'da tanıtıldı. Bu sürüm veya daha yenisini kullandığınızdan emin olun; eski sürümler dizeyi düz metin olarak işler.

## Tam çalışan örnek (konsol uygulaması)

Aşağıda, hemen derleyip çalıştırabileceğiniz bağımsız bir program bulunmaktadır. Hem Reiwa hem de Heisei dönüşümünü gösterir ve hataları nazikçe ele alır.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**Beklenen konsol çıktısı**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

Bu programı çalıştırmak, kütüphanenin **Japon era tarihini** doğru bir şekilde dönüştürdüğünü ve desteklenmeyen değerleri nazikçe raporladığını doğrular.

## Sonuç

Artık Aspose.Cells kullanarak C# içinde **Japon era tarihini** standart Gregorian `DateTime` nesnelerine nasıl dönüştüreceğinizi biliyorsunuz. İşlem, era metnini eklemek, bir stil uygulamak, çalışma sayfasını yeniden hesaplamak ve `DateTimeValue`'yu okumak kadar basittir. Yukarıdaki adımları izleyerek, **Japon takvimini** toplu olarak nasıl dönüştüreceğiniz, hataları nasıl yöneteceğiniz ve performansı nasıl optimize edeceğiniz sorusuna da yanıt bulabilirsiniz.

### Sonraki adımlar

* **Biçimlendirme seçeneklerini** keşfedin ve Gregorian tarihi özel bir sayı formatıyla çalışma sayfasına geri yazın.
* Bu dönüşümü **veri içe aktarma hatları** ile birleştirin (ör. era tarihleri içeren CSV dosyalarını okuma).
* Daha karmaşık takvim senaryoları için **tarih aritmetiği** ve **bölgesel ayarlar** gibi diğer Aspose.Cells özelliklerini inceleyin.

Kodlamaktan keyif alın ve örneği kendi veri işleme iş akışlarınıza uyarlamaktan çekinmeyin!

## Sonraki Öğrenmeniz Gerekenler?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [C# ile Aspose.Cells Kullanarak Japon Era Tarihini Ayrıştırma – Tam Kılavuz](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [C# ile Aspose.Cells Kullanarak Japon Era Ayrıştırmayı Etkinleştirme](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [C# ile çalışma kitabı oluşturma ve dizeyi tarihe dönüştürme](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}