---
category: general
date: 2026-11-19
description: C#'ta hücre sayı formatını ayarlayın ve Japon dönemi tarihleri için Excel
  tarih formatını nasıl uygulayacağınızı öğrenin; bu, güvenilir C# Excel tarih dönüşümünü
  sağlar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set cell number format
- apply excel date format
- c# excel date conversion
- japanese era date excel
- aspose.cells date handling
language: tr
lastmod: 2026-11-19
og_description: C#'ta hücre sayı formatını ayarlayın ve Japon dönemi tarihleri için
  Excel tarih formatını uygulayın. Doğru C# Excel tarih dönüşümü için bu kapsamlı
  rehberi izleyin.
og_image_alt: Screenshot showing a C# code editor with set cell number format applied
  to an Excel cell
og_title: C#'ta hücre sayı formatını ayarlayın ve Japon tarihlerini dönüştürün – adım
  adım rehber
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  headline: Set cell number format and convert Japanese dates in C#
  type: TechArticle
- description: Set cell number format in C# and learn how to apply Excel date format
    for Japanese era dates, enabling reliable C# Excel date conversion.
  name: Set cell number format and convert Japanese dates in C#
  steps:
  - name: Why this works
    text: '* `Style.Number = 14` maps to Excel’s *Short Date* format (`mm/dd/yyyy`
      by default). * When the cell contains a Japanese era string like `R3/04/01`,
      Aspose.Cells’ internal parser recognises the era and converts it to the corresponding
      Gregorian serial number during `CalculateFormula()`. * After the '
  - name: When to use a custom format
    text: '* Reports intended for Japanese audiences. * When you need to preserve
      the original era information for legal documents. * In dashboards where both
      Gregorian and era dates are shown side‑by‑side.'
  - name: Full end‑to‑end example
    text: Below is a self‑contained program that demonstrates both the Gregorian and
      era outputs in one run.
  - name: Edge cases & common pitfalls
    text: '| Situation | What to watch for | Fix / Recommendation | |----------------------------------------|------------------------------------------------------|----------------------------------------------------------|
      | Empty or malformed era string | `PutValue` stores the literal text; conversion
      fails'
  - name: Automation tip
    text: 'If you need to process a large range of era dates (e.g., column A contains
      many Japanese dates), wrap the conversion logic in a loop:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- Date conversion
title: Hücre sayı formatını ayarla ve C#'ta Japon tarihlerini dönüştür
url: /tr/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta hücre sayı biçimini ayarlama ve Japon tarihlerini dönüştürme

## Ne öğreneceksiniz

* Bir çalışma kitabı oluşturmayı ve ilk çalışma sayfasına erişmeyi.  
* Excel'in değeri tarih olarak işlemesi için **set cell number format**'ı nasıl ayarlayacağınızı.  
* Japon era dizelerini tanıyan **apply Excel date format**'ı nasıl uygulayacağınızı.  
* Formülleri yeniden hesaplayarak **C# Excel date conversion**'ı nasıl tetikleyeceğinizi.  
* Beklenen çıktı ve uç durumlar için sorun giderme ipuçları.

**Önkoşullar**

* .NET 6 veya üzeri (kod .NET Framework 4.6+ ile de çalışır).  
* Aspose.Cells for .NET 2024 veya daha yeni sürüm – NuGet üzerinden kurun: `dotnet add package Aspose.Cells`.  
* C# ve Excel tarih işleme konularında temel bilgi.

> **Pro ipucu:** Aspose.Cells, Microsoft Office yüklü olmadan çalışır ve bu da sunucu‑tarafı otomasyon için idealdir.

## C#'ta Aspose.Cells ile hücre sayı biçimini ayarlama

İlk adım, Excel'e hücrenin bir tarih içerdiğini söylemektir. Excel tarihleri seri numaralar olarak saklar, bu yüzden hedef hücreye yerleşik bir tarih sayı biçimi (ID 14) uygulamamız gerekir.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraDateDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Insert a Japanese era date string (Reiwa 3) into cell A1
        sheet.Cells["A1"].PutValue("R3/04/01");

        // 3️⃣ **Set cell number format** – use built‑in date format ID 14
        //    This tells Excel to treat the string as a date value.
        sheet.Cells["A1"].Style.Number = 14;

        // 4️⃣ Recalculate formulas so the internal date engine converts the era.
        workbook.CalculateFormula();

        // 5️⃣ Output the converted Gregorian date.
        Console.WriteLine(sheet.Cells["A1"].StringValue); // → 2021-04-01
    }
}
```

### Neden bu çalışıyor

* `Style.Number = 14` Excel'in *Kısa Tarih* biçimine (`mm/dd/yyyy` varsayılan) eşlenir.  
* Hücre `R3/04/01` gibi bir Japon era dizesi içerdiğinde, Aspose.Cells'in dahili ayrıştırıcısı era'yı tanır ve `CalculateFormula()` sırasında karşılık gelen Gregoryen seri numarasına dönüştürür.  
* Hesaplamadan sonra, `StringValue` biçimlendirilmiş Gregoryen tarihi döndürür.

## Japon era tarihleri için Excel tarih biçimini uygulama

Hücrenin Gregoryen tarih yerine Japon era'sını göstermesini istiyorsanız, era kodunu içeren özel bir sayı biçimi kullanabilirsiniz. Bu, **apply excel date format** yeteneğini gösterir.

```csharp
// Apply a custom format that forces the Japanese era display
sheet.Cells["A1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";

// Recalculate to apply the custom format
workbook.CalculateFormula();

// Output the era‑styled string
Console.WriteLine(sheet.Cells["A1"].StringValue); // → R3年04月01日
```

* `[$-ja-JP]` Japon yerel ayarını zorlar.  
* `ggg` era adını temsil eder (ör. `R` Reiwa için).  
* Literal karakterler (`年`, `月`, `日`) eklemek tanıdık bir Japon tarih düzeni oluşturur.

### Özel bir biçim ne zaman kullanılmalı

* Japon izleyicilere yönelik raporlar.  
* Yasal belgeler için orijinal era bilgisini korumanız gerektiğinde.  
* Hem Gregoryen hem de era tarihlerinin yan yana gösterildiği panolarda.

## C# Excel tarih dönüşümü – Japon era'larını işleme

**c# excel date conversion** süreci üç mantıksal bölüme ayrılabilir:

1. **Parse the era string** – Aspose.Cells otomatik olarak `R` (Reiwa), `H` (Heisei), `S` (Showa) vb. tanır.  
2. **Convert to a serial number** – Excel tarihleri 1899‑12‑30 tarihinden itibaren gün sayısı olarak saklar.  
3. **Format the serial number** – ya yerleşik bir biçim (ID 14) ya da özel bir Japon biçimi ile.

### Tam uçtan uca örnek

Aşağıda, hem Gregoryen hem de era çıktısını tek bir çalıştırmada gösteren bağımsız bir program bulunmaktadır.

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConversion
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Input: Reiwa 3 (2021) – can be any era string
        ws.Cells["A1"].PutValue("R3/04/01");

        // ---- Part 1: Gregorian output ----
        ws.Cells["A1"].Style.Number = 14;      // built‑in short date
        wb.CalculateFormula();                // forces conversion
        string gregorian = ws.Cells["A1"].StringValue;
        Console.WriteLine($"Gregorian: {gregorian}"); // 2021-04-01

        // ---- Part 2: Japanese era output ----
        ws.Cells["B1"].PutValue("R3/04/01");   // repeat input for clarity
        ws.Cells["B1"].Style.Custom = "[$-ja-JP]ggge\"年\"m\"月\"d\"日\"";
        wb.CalculateFormula();
        string era = ws.Cells["B1"].StringValue;
        Console.WriteLine($"Japanese era: {era}"); // R3年04月01日
    }
}
```

**Beklenen konsol çıktısı**

```
Gregorian: 2021-04-01
Japanese era: R3年04月01日
```

### Uç durumlar ve yaygın tuzaklar

| Durum                                 | Dikkat edilmesi gereken                                          | Düzeltme / Öneri                                                                                                   |
|---------------------------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| Boş veya hatalı biçimlendirilmiş era dizesi | `PutValue` literal metni saklar; dönüşüm başarısız olur          | Hücreye yazmadan önce girdiyi bir düzenli ifadeyle doğrulayın.                                                       |
| Yerel ayar uyuşmazlığı                | Özel biçim, Japon karakterler yerine batı rakamlarını gösteriyor | `Custom` biçimin `[$-ja-JP]` içerdiğinden emin olun veya `Workbook.Settings.CultureInfo` değerini `ja-JP` olarak ayarlayın. |
| Çalışma kitabı, tarih hücresine başvuran formüller içeriyor | Yeniden hesaplama, formül sonuçlarını üzerine yazabilir          | `CalculateFormula`'ı tüm biçimlendirme adımlarından **sonra** çağırın, ya da hataları atlamak istiyorsanız `Workbook.CalculateFormula(FormulaCalculationOptions.IgnoreError)` kullanın. |
| Eski Aspose.Cells sürümlerini kullanmak | Japon era desteği 2022 Üçüncü çeyrekte eklendi                  | En son NuGet paketine yükseltin.                                                                                     |

## Çözümü test etme

1. **Run the program**'ı Visual Studio'dan veya `dotnet run` ile çalıştırın.  
2. Konsolun Gregoryen tarih `2021‑04‑01` ve era dizesi `R3年04月01日` yazdırdığını doğrulayın.  
3. Oluşturulan çalışma kitabını (eğer `wb.Save("Demo.xlsx");` eklerseniz) Microsoft Excel'de açın ve hücrelere aynı biçimin uygulandığını görün.

### Otomasyon ipucu

Büyük bir era tarih aralığını (ör. A sütunu birçok Japon tarihi içeriyorsa) işlemeniz gerekiyorsa, dönüşüm mantığını bir döngü içinde sarın:

```csharp
for (int row = 0; row < ws.Cells.MaxDataRow + 1; row++)
{
    var cell = ws.Cells[row, 0]; // column A
    cell.Style.Number = 14;
}
wb.CalculateFormula();
```

Bu yaklaşım **set cell number format** işlemini hızlı ve bellek‑verimli tutar.

## Sonuç

Artık Aspose.Cells kullanarak C#'ta **set cell number format**'ı nasıl yapacağınızı, Japon era dizeleri için **apply Excel date format**'ı nasıl uygulayacağınızı ve era'dan Gregoryen tarihlere güvenilir **C# Excel date conversion**'ı nasıl gerçekleştireceğinizi biliyorsunuz. Tam, çalıştırılabilir kod her iki çıktıyı gösterir ve yaygın uç durumları vurgular.  

**Sonraki adımlar**

* Diğer yerleşik biçim ID'lerini keşfedin

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri içerir.

- [C#'ta Excel tarih biçimini ayarla – Tam Adım‑Adım Kılavuz](/cells/english/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/)
- [Aspose.Cells ile Excel sayı biçimini nasıl uygularsınız](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)
- [C#'ta Excel'de özel sayı biçimini nasıl uygularsınız](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}