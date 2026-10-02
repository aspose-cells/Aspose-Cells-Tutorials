---
category: general
date: 2026-05-30
description: Aspose.Cells kullanarak C#'de Japon dönemi ayrıştırmasını etkinleştirin.
  Çalışma kitabı kültürünü ayarlamayı, dönem tarihlerini ayrıştırmayı ve Excel çalışma
  sayfalarında Japon takvimini yönetmeyi öğrenin.
draft: false
keywords:
- enable japanese era parsing
- Aspose.Cells Japanese era
- set workbook culture
- parse era dates
- c# excel date parsing
language: tr
og_description: C#'ta Aspose.Cells ile Japon dönemi ayrıştırmasını etkinleştirin.
  Bu kılavuz, çalışma kitabı kültürünü nasıl ayarlayacağınızı, dönem desteğini nasıl
  etkinleştireceğinizi ve Japon tarihleriyle nasıl çalışacağınızı gösterir.
og_title: C#'de Japon Dönemi Ayrıştırmayı Etkinleştirme – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Enable Japanese era parsing in C# using Aspose.Cells. Learn to set
    workbook culture, parse era dates, and handle Japanese calendar in Excel worksheets.
  headline: Enable Japanese Era Parsing in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Aspose.Cells ile C#'de Japon Dönemi Ayrıştırmayı Etkinleştir
url: /tr/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.Cells'ta Japanese Era Parsing'i Etkinleştirme

Japon bir müşteri için Excel dosyaları oluştururken **enable japanese era parsing** gerektiğinde hiç oldu mu? Tek başınıza değilsiniz—birçok geliştirici, eski Japon takvimi (令和, 平成, vb.) verilerde göründüğünde bir duvara çarpıyor. İyi haber, Aspose.Cells bu dönem tarihlerini tanımasını ve standart Gregoryen değerlere dönüştürmesini çok kolay hâle getiriyor.

Bu öğreticide, Aspose.Cells kullanarak **enable japanese era parsing** adımlarını, çalışma kitabının kültürünü Japonca olarak ayarlamayı ve bir hücreye dönem‑formatlı tarih eklemeyi göstereceğiz. Sonunda, “令和3年5月1日” ifadesini doğru `2021‑05‑01` tarih nesnesine dönüştüren çalıştırılabilir bir C# kod parçacığına sahip olacaksınız. Harici belgeye gerek yok—sadece kopyalayıp yapıştırın ve çalıştırın.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Core, .NET Framework ve .NET 5+ ile çalışır)
- Aspose.Cells for .NET (NuGet paketi `Aspose.Cells`)
- Temel C# bilgisi—eğer bir `Console.WriteLine` yazabiliyorsanız yeterlidir
- Tercih ettiğiniz bir IDE (Visual Studio, VS Code, Rider…)

> **Pro ipucu:** Aspose.Cells sürümünüzü güncel tutun; sürüm 24.10+ en son Japon dönemi tanımlarını içerir.

## Neden **enable japanese era parsing**'i Etkinleştirmelisiniz?

Japon takvimleri, imparatorluk dönemlerine bağlı dönemleri kullanır. Çoğu modern uygulama için tarihleri tanıdık Gregorian formatında saklamak istersiniz, ancak kaynak veri hâlâ “令和3年5月1日” şeklinde gelebilir. **enable japanese era parsing**'i atladığınızda, dize düz metin olarak kabul edilir ve hesaplamalar, sıralama ve grafik oluşturma bozulur. Dönem desteğini açarak, Aspose.Cells bu dizeleri otomatik olarak doğru `DateTime` değerlerine dönüştürür, hem Japon kullanıcılar için okunabilirliği hem de sonraki işlemler için sayısal doğruluğu korur.

## Adım 1: Çalışma Kitabının Kültürünü Japonca Olarak Ayarlama

İlk yapmanız gereken, Aspose.Cells'e çalışma kitabının varsayılan yerel ayarının Japonca (`ja-JP`) olduğunu söylemektir. Bu, kültüre özgü tüm ayrıştırmaların (dönem adları dahil) Japon kurallarına göre yapılmasını sağlar.

```csharp
using Aspose.Cells;
using System.Globalization;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Set the workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");
```

> **Neden önemli:** `CultureInfo` nesnesi sayı formatlarını, tarih ayırıcılarını ve bizim için en önemlisi, dize ayrıştırılırken kullanılan takvim sistemini kontrol eder.

## Adım 2: Japanese Era Parsing'i Etkinleştirme

Kültür ayarlandıktan sonra, Aspose.Cells'in dönem tarihlerini tanımasını sağlayan anahtarı açmanız gerekir. Bu, **enable japanese era parsing**'in özüdür.

```csharp
        // Enable parsing of Japanese era dates (令和, 平成, 昭和, etc.)
        workbook.Settings.UseJapaneseEra = true;
```

> **Yaygın tuzak:** Bu bayrağı unutmak, “令和3年5月1日” ifadesinin düz metin olarak kalmasına neden olur. Açık olduğunda, Aspose.Cells dönemi otomatik olarak doğru Gregorian yıla eşler.

## Adım 3: Bir Hücreye Dönem‑Formatlı Tarih Eklemek

Kültür ve dönem desteği hazır olduğunda, Japon dönem dizesi eklemek oldukça basittir. Kütüphane bunu ayrıştırır ve gerçek bir `DateTime` değeri olarak saklar.

```csharp
        // Grab the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Insert a Japanese era date string into cell A1
        // The string "令和3年5月1日" becomes 2021‑05‑01 internally
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Save the workbook to verify the result
        workbook.Save("JapaneseEraDemo.xlsx");
    }
}
```

### Beklenen Çıktı

- Oluşturulan `JapaneseEraDemo.xlsx` dosyasındaki **A1 hücresi** **2021‑05‑01** tarihini (veya Excel'i Japon yerel ayarıyla açarsanız yerelleştirilmiş Japon tarih formatını) gösterecek.
- Temel değer gerçek bir `DateTime` olduğundan, formüllerde, pivot tablolarında veya daha ileri C# hesaplamalarında güvenle kullanılabilir.

## Adım 4: Ayrıştırılan Tarihi Programatik Olarak Doğrulama (İsteğe Bağlı)

Kaydetmeden önce ayrıştırmanın başarılı olduğunu iki kez kontrol etmek isterseniz, hücreyi tekrar okuyabilirsiniz:

```csharp
        // Retrieve the value as a DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        Console.WriteLine($"Parsed date: {parsedDate:yyyy-MM-dd}");
        // Output: Parsed date: 2021-05-01
```

Bu küçük doğrulama adımı, birim testlerinde veya kullanıcı tarafından sağlanan Excel dosyalarını işlerken kullanışlıdır.

## Kenar Durumları ve Varyasyonlar

| Senaryo | Ne Yapmalı |
|----------|------------|
| **Bir çalışma kitabında birden fazla dönem** | `UseJapaneseEra = true` tutun; Aspose.Cells tüm desteklenen dönemleri (令和, 平成, 昭和, 大正, 明治) tanıyacaktır. |
| **Karışık Gregorian ve dönem dizeleri** | Ayrıştırıcı otomatik olarak ayırır; Gregorian dizeler değişmeden kalır. |
| **Özel takvim gereksinimleri** | `Workbook.Settings.Calendar`'ı belirli bir `Calendar` örneğine ayarlayarak daha fazla kontrol sağlayabilirsiniz. |
| **Eski .NET sürümleri** | Aynı kod .NET Framework 4.6+ üzerinde çalışır; sadece `System.Globalization.CultureInfo` yapıcısının mevcut olduğundan emin olun. |

## Gerçek‑Dünya Projeleri İçin Pratik İpuçları

- Bir döngü içinde birçok çalışma kitabı oluşturuyorsanız **CultureInfo'yi önbelleğe alın**; tekrar tekrar oluşturmak ek yük getirir.
- `PutValue` çağırmadan önce **girişi doğrulayın**; hatalı dönem dizeleri bir istisna fırlatır.
- Verinin kesinlikle dönem tarihi içermediğinden emin olduğunuzda **dönem ayrıştırmayı kapatın** (`UseJapaneseEra = false`)—bu performansı biraz artırabilir.
- Ayrıştırılan tarihi korurken çıktı formatını (XLSX, XLS, CSV) kontrol etmek için **`Workbook.SaveOptions`'ı kullanın**.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class EnableJapaneseEraParsingDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Set workbook culture to Japanese (ja-JP)
        workbook.Settings.Culture = new CultureInfo("ja-JP");

        // 3️⃣ Enable Japanese era parsing
        workbook.Settings.UseJapaneseEra = true;

        // 4️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 5️⃣ Insert an era‑formatted date
        sheet.Cells["A1"].PutValue("令和3年5月1日");

        // Optional: read back the parsed value
        DateTime dt = sheet.Cells["A1"].GetDateTime();
        Console.WriteLine($"Parsed date: {dt:yyyy-MM-dd}");

        // Save the workbook
        workbook.Save("EnableJapaneseEraParsing.xlsx");
    }
}
```

Programı çalıştırın, oluşturulan dosyayı açın ve A1 hücresinde **2021‑05‑01** göreceksiniz—bu, **enable japanese era parsing**'i başarıyla yaptığımızın kanıtıdır.

## Sonuç

Az önce, Aspose.Cells kullanarak C#'ta **enable japanese era parsing**'i nasıl yapacağınızı, çalışma kitabının kültürünü nasıl ayarlayacağınızı ve “令和3年5月1日” gibi dönem tarihlerini sorunsuzca standart Gregorian değerlere nasıl dönüştüreceğinizi gösterdik. Adımlar azdır, kod bağımsızdır ve sonuç Excel'de sorunsuz çalışır.

Bir sonraki zorluğa hazır mısınız? **set workbook culture**'i Japon Yen'i için sayı biçimlendirmesiyle birleştirmeyi deneyin ya da Gregorian ve dönem tarihlerini karıştıran çok sayfalı bir rapor oluşturun. Artık .NET Excel otomasyon projelerinizde Japon takvimiyle ilgili tüm tuhaflıkları ele alacak temele sahipsiniz.

---

*Bu rehber size yardımcı olduysa, Aspose.Cells GitHub deposunu yıldızlamayı veya yorumlarda kendi ipuçlarınızı paylaşmayı düşünün. Kodlamanın keyfini çıkarın!*

## Sonra Ne Öğrenmelisiniz?

- [Aspose.Cells for .NET ile Kültüre Özel Tarihler İçeren Excel Çalışma Kitaplarını Yükleme](/cells/english/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)
- [Aspose.Cells .NET ile Excel Dosyalarında Çok Dilli Destek İçin Dil Nasıl Ayarlanır](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Aspose Cells Net ile Çalışma Kitabı Kültürüne Özel Tarihleri Yükleme](/cells/chinese/net/formatting/load-workbook-culture-specific-dates-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}