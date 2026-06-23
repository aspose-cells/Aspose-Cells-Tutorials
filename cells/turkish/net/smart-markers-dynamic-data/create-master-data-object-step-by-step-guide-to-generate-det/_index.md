---
category: general
date: 2026-02-14
description: C#'ta ana veri nesnesi oluşturun ve detay sayfasını zahmetsizce üretin.
  Pratik kod örnekleriyle tam SmartMarker iş akışını öğrenin.
draft: false
keywords:
- create master data object
- generate detail sheet
- smartmarker processing
- worksheet automation
- c# data binding
language: tr
og_description: C#'ta ana veri nesnesi oluşturun ve SmartMarker ile detay sayfası
  oluşturun. Hazır‑çalıştırılabilir bir çözüm için ayrıntılı öğreticimizi takip edin.
og_title: Ana Veri Nesnesi Oluşturma – Tam Rehber
tags:
- C#
- SmartMarker
- Excel Automation
title: Ana Veri Nesnesi Oluşturma – Detay Sayfası Oluşturmak İçin Adım Adım Kılavuz
url: /tr/net/smart-markers-dynamic-data/create-master-data-object-step-by-step-guide-to-generate-det/
---

Master Data Object – Complete Tutorial" => "# Master Veri Nesnesi Oluşturma – Tam Kılavuz"

But maybe keep "Master Data Object" as is? The instruction: keep technical terms in English. "master data object" is a technical term, maybe keep as is. The title includes both English and Turkish. Could translate but keep term. Let's translate as "# Master Data Object Oluşturma – Tam Kılavuz". Or "# Master Data Object – Tam Kılavuz". Might be better: "# Master Data Object – Tam Kılavuz". Keep "Master Data Object". We'll keep as "# Master Data Object – Tam Kılavuz".

Similarly "SmartMarker" keep.

Proceed.

Translate bullet lists.

Make sure to keep code block placeholders unchanged.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Master Data Object – Tam Kılavuz

Hiç **master data object** oluşturmanız gerektiğinde, bunu bir SmartMarker detay sayfasına nasıl bağlayacağınızdan emin olmadınız mı? Tek başınıza değilsiniz. Birçok raporlama senaryosunda master nesne, dinamik bir detay sayfasını yönlendirir ve bağlantıyı doğru kurmak, resmi olmayan bir bulmacayı birleştirmek gibi hissettirebilir.  

Bu rehberde tüm süreci adım adım inceleyeceğiz—master data object’i oluşturma, SmartMarker seçeneklerini **detail sheet oluştur** şekilde yapılandırma ve sonunda işlemciyi çalıştırma. Sonunda, GrapeCity Documents for Excel (GcExcel) kütüphanesini kullanan herhangi bir .NET projesine yapıştırabileceğiniz çalıştırılabilir bir kod parçacığı elde edeceksiniz.

## Gereksinimler

- .NET 6+ (veya .NET Framework 4.7.2) ve `GcExcel.dll` referansı
- Temel C# bilgisi (değişkenler, anonim tipler, nesne başlatıcıları)
- `{{OrderId}}` gibi SmartMarker etiketleri ve satır öğeleri için bir tablo içeren bir Excel çalışma kitabı
- Visual Studio, Rider veya tercih ettiğiniz herhangi bir editör

Hepsi bu—core GcExcel dağıtımının dışına çıkacak ekstra bir NuGet paketi yok.

## Adım 1: Master Data Object’i Oluşturma

İlk olarak **master data object** oluşturmalısınız; bu nesne SmartMarker etiketlerinin beklediği yapıyı yansıtmalıdır. Bunu, hafif bir bellek içi rapor modeli olarak düşünebilirsiniz.

```csharp
// Step 1: Build the master data object that feeds the SmartMarkers.
// It contains an OrderId and a collection of line items.
var orderData = new
{
    OrderId = 1,
    Items = new[]
    {
        new { Product = "A", Quantity = 2 },
        new { Product = "B", Quantity = 5 }
    }
};
```

Neden burada anonim tip kullanıyoruz? Çünkü tam bir sınıf tanımlamadan hafif bir kapsayıcı tanımlamanıza izin verir—hızlı demolar veya şeklin değişme ihtimalinin düşük olduğu durumlar için idealdir. Daha sonra yeniden kullanılabilir bir model isterseniz, `var` yerine uygun bir POCO ile değiştirebilirsiniz.

> **İpucu:** Özellik adlarını (`OrderId`, `Product`, `Quantity`) çalışma sayfanızdaki yer tutucularla birebir aynı tutun; SmartMarker bunları büyük/küçük harfe duyarsız olarak eşleştirir.

## Adım 2: Detay Sayfası Oluşturmak İçin SmartMarker Seçeneklerini Yapılandırma

Şimdi SmartMarker’a satır‑öğe tablosu için ayrı bir çalışma sayfası istediğimizi söylüyoruz. İşte **generate detail sheet** anahtar kelimesinin devreye girdiği yer.

```csharp
// Step 2: Set up SmartMarker options.
// Enabling DetailSheet creates a new sheet for each master record.
var smartMarkerOptions = new SmartMarkerOptions
{
    DetailSheet = true,
    // The new sheet will be named using the OrderId value.
    DetailSheetNewName = "Order_{OrderId}"
};
```

`DetailSheetNewName` deseni, çalışma zamanında değiştirilen süslü‑parantez yer tutucularını kullanır. Örneğimizde sayfa `Order_1` olarak adlandırılacak. Daha sonra birden fazla sipariş döngüsü yaparsanız, her biri kendi sekmesine sahip olur—çoğu muhasebecinin beklediği tam senaryo.

## Adım 3: SmartMarker İşlemcisini Çalıştırma

Veri ve seçenekler hazır olduğunda, son adım hedef çalışma sayfası üzerinde işlemciyi çağırmaktır.

```csharp
// Step 3: Execute SmartMarker processing on the worksheet.
// 'worksheet' is an IWorksheet instance that points to the template sheet.
worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);
```

Arka planda SmartMarker, çalışma sayfasını etiketler için tarar, `orderData` değerlerini enjekte eder ve `DetailSheet` `true` olduğu için şablonu `Order_1` adlı yeni bir sayfaya kopyalar. Tüm satır öğeleri detay alanında görünür ve şablonda uyguladığınız biçimlendirme korunur.

### Tam Çalışan Örnek

Aşağıda, bir şablon çalışma kitabını (`Template.xlsx`) açan, üç adımı çalıştıran ve sonucu `Result.xlsx` olarak kaydeden bağımsız bir konsol programı yer alıyor. Bunu yeni bir konsol projesine kopyalayıp **F5** tuşuna basabilirsiniz.

```csharp
using System;
using GrapeCity.Documents.Excel;

class Program
{
    static void Main()
    {
        // Load the Excel template that contains SmartMarker tags.
        var workbook = new Workbook();
        workbook.Open("Template.xlsx");

        // -------------------------------------------------
        // Step 1: Create the master data object.
        // -------------------------------------------------
        var orderData = new
        {
            OrderId = 1,
            Items = new[]
            {
                new { Product = "A", Quantity = 2 },
                new { Product = "B", Quantity = 5 }
            }
        };

        // -------------------------------------------------
        // Step 2: Configure SmartMarker options to generate detail sheet.
        // -------------------------------------------------
        var smartMarkerOptions = new SmartMarkerOptions
        {
            DetailSheet = true,
            DetailSheetNewName = "Order_{OrderId}"
        };

        // -------------------------------------------------
        // Step 3: Process the worksheet.
        // -------------------------------------------------
        // Assume the first sheet holds the master template.
        var worksheet = workbook.Worksheets[0];
        worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orderData, smartMarkerOptions);

        // Save the populated workbook.
        workbook.Save("Result.xlsx");
        Console.WriteLine("Done! Check Result.xlsx – a new sheet named Order_1 should exist.");
    }
}
```

#### Beklenen Çıktı

- **Result.xlsx** içinde `Order_1` adlı bir sayfa bulunur.
- `{{OrderId}}` yer tutucusunun bulunduğu hücre (ör. A1) artık `1` gösterir.
- SmartMarker bloğundan başlayan bir tablo iki satır listeler:
  | Product | Quantity |
  |---------|----------|
  | A       | 2        |
  | B       | 5        |

Dosyayı açtığınızda, şablondan gelen biçimlendirmelerin (kenarlıklar, yazı tipleri, koşullu biçimlendirme vb.) korunduğunu göreceksiniz.

## Yaygın Sorular & Kenar Durumları

### Birden fazla siparişim olursa ne olur?

Master nesneyi bir koleksiyon içinde tutun ve SmartMarker’ın otomatik olarak yinelemesine izin verin:

```csharp
var orders = new[]
{
    new {
        OrderId = 1,
        Items = new[] { new { Product = "A", Quantity = 2 } }
    },
    new {
        OrderId = 2,
        Items = new[] { new { Product = "C", Quantity = 3 } }
    }
};

worksheet.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);
```

Her sipariş kendi sayfasını (`Order_1`, `Order_2`, …) oluşturur. İşlemci dış diziye master koleksiyon olarak davranır.

### Sayfanın konumunu nasıl kontrol ederim?

`smartMarkerOptions.DetailSheetInsertIndex = 2;` ile yeni sayfayı ikinci sekmeden sonra yerleştirebilir veya `DetailSheetInsertAfter = "Summary"` ile adlandırılmış bir sayfanın ardından ekleyebilirsiniz.

### Belirli bir çalıştırma için detay sayfasını devre dışı bırakabilir miyim?

Sadece `DetailSheet = false;` olarak ayarlayın. SmartMarker, satır öğelerini master etiketlerinin bulunduğu aynı sayfaya yazar.

### Büyük veri setleriyle nasıl başa çıkılır?

SmartMarker veriyi verimli bir şekilde akıtar, ancak birkaç yüz bin satırı aşarsanız Excel’in 1.048.576‑satır limitine takılabilirsiniz. Bu durumda veriyi birden fazla master kayıta bölün veya CSV’ye dışa aktarmayı düşünün.

## Görsel Genel Bakış

![Diagram illustrating how to create master data object and generate detail sheet using SmartMarker](/images/smartmarker-flow.png)

*İllüstrasyon, C# master nesnesinden → SmartMarker seçeneklerine → çalışma sayfası işleme → yeni detay sayfasına akışı gösterir.*

## Sonuç

Artık C#’ta **master data object** oluşturmayı ve SmartMarker’ı **detail sheet oluştur** şekilde otomatik olarak yapılandırmayı biliyorsunuz. Veri, seçenekler, işlemci üç adımlı desen, GcExcel ile Excel otomasyonunun çoğu senaryosunu kapsar.  

Bundan sonra keşfedebilecekleriniz:

- Her detay sayfasına başlık/altbilgi verisi eklemek
- Sipariş durumuna göre koşullu biçimlendirme kullanmak
- Oluşturulan çalışma kitabını `workbook.SaveAsPdf(...)` ile PDF olarak dışa aktarmak

Deneyin, hatalar yapın ve ardından birleştirin. Bu, çalışma sayfası otomasyonunu en hızlı şekilde öğrenmenin yoludur. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}