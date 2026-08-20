---
category: general
date: 2026-02-14
description: İndirim şablonunu hızlıca oluşturun ve elektronik tabloda indirim uygulamayı,
  şablona veri eklemeyi ve akıllı işaretçiler için değişken önek tanımlamayı öğrenin.
draft: false
keywords:
- create discount template
- apply discount in spreadsheet
- inject data into template
- define variable prefix
language: tr
og_description: C# ile indirim şablonu oluşturun. Elektronik tabloda indirimi uygulamayı,
  şablona veri enjekte etmeyi ve akıllı işaretçiler için değişken önek tanımlamayı
  öğrenin.
og_title: İndirim Şablonu Oluştur – Tam C# Kılavuzu
tags:
- C#
- SmartMarker
- Spreadsheet Automation
title: C#'ta İndirim Şablonu Oluşturma – Adım Adım Rehber
url: /tr/net/smart-markers-dynamic-data/create-discount-template-in-c-step-by-step-guide/
---

ablonu oluştur**, ardından **tablodaki hücrelerde indirimi uygula**, **verileri şablona enjekte et** ve hatta akıllı işaretçileriniz için **değişken önekini tanımla** nasıl yapacağınızı temiz C# kodu ile göstereceğiz."

Continue.

We must keep bold formatting.

Proceed.

Will produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# İndirim Şablonu Oluştur – Tam C# Kılavuzu

Satış raporu için **indirim şablonu oluştur**manız gerektiğinde, sayıları otomatik olarak bir tabloya nasıl aktaracağınızdan emin olmadınız mı? Yalnız değilsiniz. Bu öğreticide tam olarak **indirim şablonu oluştur**, ardından **tablodaki hücrelerde indirimi uygula**, **verileri şablona enjekte et** ve hatta akıllı işaretçileriniz için **değişken önekini tanımla** nasıl yapacağınızı temiz C# kodu ile göstereceğiz.

Problemi tanımlayarak başlayacağız, ardından kopyala‑yapıştır yapabileceğiniz çalışan bir çözüme geçeceğiz. Sonunda, fatura, fiyat listesi ya da dinamik indirim gerektiren herhangi bir tablo oluştururken kullanabileceğiniz yeniden kullanılabilir bir desen elde edeceksiniz.

---

## Öğrenecekleriniz

- İndirim‑duyarlı bir tablo şablonu nasıl tasarlanır.
- İşaretçilerin kolay fark edilmesi için özel bir `VariablePrefix` / `VariableSuffix` nasıl yapılandırılır.
- Anonim bir nesne (`discountData`) `SmartMarkerProcessor` içine nasıl geçirilir.
- Oluşan formül (`=IF(#Discount#>0, A1*(1-#Discount#), A1)`) son fiyatı otomatik olarak nasıl hesaplar.
- Sıfır‑indirim satırları ya da birden fazla indirim katmanı gibi kenar durumlarıyla başa çıkma ipuçları.

**Önkoşullar** – .NET 6 veya üzeri bir .NET çalışma zamanı, `SmartMarkerProcessor` sağlayan `Aspose.Cells` (veya benzeri) kütüphanesine bir referans ve temel C# sözdizimi bilgisi. Karmaşık bir şey yok.

---

## Adım 1: Tablo Şablonunuzda Bir İndirim Şablonu Oluşturun

Yeni bir çalışma kitabı açın (veya mevcut birini kullanın) ve indirimin uygulanacağı bir yer tutucu yerleştirin. Şablonu, işlemcinin değiştireceği “akıllı işaretçiler” içeren sade bir Excel dosyası olarak düşünün.

```csharp
using Aspose.Cells;          // SmartMarkerProcessor lives here
using System;

// Step 1: Load or create a workbook
Workbook wb = new Workbook();               // creates an empty .xlsx in memory
Worksheet ws = wb.Worksheets[0];
ws.Name = "Pricing";

// Put a header
ws.Cells["A1"].PutValue("Original Price");
ws.Cells["B1"].PutValue("Discounted Price");

// Sample data row – the formula will be injected later
ws.Cells["A2"].PutValue(100);               // original price = 100
ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";
```

**Neden önemli:** Formül içine `#Discount#` gömerek, işlemciye indirim değerinin tam olarak nerede bulunması gerektiğini söylüyoruz. `SmartMarkerProcessor` daha sonra `#Discount#` ifadesini siz sonrada sağlayacağınız sayı ile değiştirir, formülün geri kalanını dokunulmaz bırakır.

---

## Adım 2: Akıllı İşaretçiler İçin Değişken Önekini Tanımlayın

Kutudan çıkar çıkmaz, birçok kütüphane `${Variable}` ya da `{{Variable}}` biçiminde işaretçiler arar. Bizim senaryomuzda temiz, insan‑okunur bir işaretçi istiyoruz, bu yüzden **değişken önekini** ve son ekini açıkça **tanımlıyoruz**.

```csharp
// Step 2: Configure how markers are identified
var smartMarkerOptions = new SmartMarkerOptions
{
    VariablePrefix = "#",   // start marker
    VariableSuffix = "#"    // end marker
};
```

**Pro ipucu:** `#` kullanmak işaretçileri kısa ve Excel’in formül çubuğunda kolayca fark edilebilir kılar. Mevcut Excel fonksiyonlarıyla çakışmaları önlemek isterseniz farklı bir çift seçin (ör. `[[` ve `]]`).

---

## Adım 3: SmartMarkerProcessor ile Verileri Şablona Enjekte Edin

Şimdi gerçek indirim değerini veriyoruz. İşlemci çalışma sayfasını tarar, her `#Discount#` işaretçisini bulur ve anonim nesneden aldığımız değerle değiştirir.

```csharp
// Step 3: Prepare the data that will be injected
var discountData = new { Discount = 0.10, Total = 100 };

// Run the processor – it mutates the workbook in‑place
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);
```

Bu çağrıdan sonra `B2` hücresindeki formül şu hâle gelir:

```
=IF(0.1>0, A2*(1-0.1), A2)
```

Çalışma kitabı hesaplandığında `B2` **90** gösterir; yani 100’lük orijinal fiyata %10 indirim uygulanmıştır.

**Neden çalışıyor:** `StartSmartMarkerProcessing` her hücreyi dolaşır, `#Discount#` tokenını arar ve sayısal değeri yerleştirir. Token bir `IF` ifadesi içinde olduğundan, indirim sıfır olduğunda bile tablo bu durumu sorunsuz yönetir.

---

## Adım 4: Tablo’da İndirimi Uygula – Sonucu Doğrula

Hesaplamayı tetikleyelim ve son fiyatı konsola yazdıralım. Bu adım, **tablodaki hücrelerde indirimi uygula** iş akışının başarılı olduğunu kanıtlar.

```csharp
// Step 4: Force calculation and read the result
wb.CalculateFormula();                     // ensures all formulas are up‑to‑date
double discountedPrice = ws.Cells["B2"].DoubleValue;

Console.WriteLine($"Original: {ws.Cells["A2"].DoubleValue}");
Console.WriteLine($"Discounted (10%): {discountedPrice}");
```

**Beklenen çıktı**

```
Original: 100
Discounted (10%): 90
```

`discountData.Discount` değerini `0.25` olarak değiştirip işlemciyi yeniden çalıştırırsanız, çıktı otomatik olarak %25 indirim gösterecektir—ek bir kod eklemenize gerek yok.

---

## Adım 5: Kenar Durumları ve Birden Fazla İndirimle Baş Etme

### Sıfır‑İndirim Satırları

Bazen bir ürün indirimde değildir. Formülü dayanıklı tutmak için daha önce eklediğiniz `IF` zaten bu senaryoyu kapsar: `#Discount#` `0` olduğunda, orijinal fiyat değişmeden geçer.

```csharp
var noDiscountData = new { Discount = 0.0 };
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(noDiscountData, smartMarkerOptions);
wb.CalculateFormula();
Console.WriteLine($"No discount applied: {ws.Cells["B2"].DoubleValue}");
```

### Birden Fazla İndirim Sütunu

Satır başına ayrı indirimler gerekiyorsa, her satıra kendi işaretçisini verin; ör. `#Discount1#`, `#Discount2#` ve bir koleksiyon geçirin:

```csharp
var multiDiscountData = new[]
{
    new { Discount = 0.05 },   // row 2
    new { Discount = 0.15 }    // row 3
};

ws.SmartMarkerProcessor.StartSmartMarkerProcessing(multiDiscountData, smartMarkerOptions);
```

İşlemci işaretçileri sırasıyla eşleştirir, böylece her satır doğru değeri alır.

---

## Tam Çalışan Örnek

Aşağıda, yukarıdaki tüm adımları içeren, kopyala‑yapıştır hazır program yer alıyor. `Program.cs` olarak kaydedin, `Aspose.Cells` referansını ekleyin ve çalıştırın.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook & template
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];
        ws.Name = "Pricing";
        ws.Cells["A1"].PutValue("Original Price");
        ws.Cells["B1"].PutValue("Discounted Price");
        ws.Cells["A2"].PutValue(100);
        ws.Cells["B2"].Formula = "=IF(#Discount#>0, A2*(1-#Discount#), A2)";

        // 2️⃣ Define marker delimiters
        var smartMarkerOptions = new SmartMarkerOptions
        {
            VariablePrefix = "#",
            VariableSuffix = "#"
        };

        // 3️⃣ Inject a 10 % discount
        var discountData = new { Discount = 0.10 };
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(discountData, smartMarkerOptions);

        // 4️⃣ Calculate and display result
        wb.CalculateFormula();
        double original = ws.Cells["A2"].DoubleValue;
        double discounted = ws.Cells["B2"].DoubleValue;

        Console.WriteLine($"Original: {original}");
        Console.WriteLine($"Discounted (10%): {discounted}");

        // Optional: Save the workbook to verify manually
        wb.Save("DiscountedPricing.xlsx");
    }
}
```

Çalıştırdığınızda beklenen sayılar ekrana basılır ve `DiscountedPricing.xlsx` adlı bir dosya oluşturulur; bu dosyayı Excel’de açtığınızda formülün zaten çözülmüş olduğunu görebilirsiniz.

---

## Sonuç

Artık **indirim şablonu oluştur**, **tablodaki hücrelerde indirimi uygula**, **verileri şablona enjekte et** ve **akıllı işaretçiler için değişken önekini tanımla** konularını birkaç özlü C# satırıyla nasıl yapacağınızı biliyorsunuz. Desen ölçeklenebilir—anonim nesneyi değiştirin ya da toplu güncellemeler için bir koleksiyon besleyin, aynı şablon her türlü indirim senaryosunu idare eder.

Bir sonraki seviyeye hazır mısınız? Şunları deneyin:

- İndirimlerin yanında vergi hesaplamaları eklemek.
- İndirim yüzdelerini sabit kodlamak yerine bir veritabanından çekmek.
- Yüksek indirimli satırları vurgulamak için koşullu biçimlendirme kullanmak.

Bu eklemeler temel fikri korurken indirim şablonunuzun faydasını genişletir.

Sorularınız veya ilginç bir kullanım senaryonuz mu var? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}