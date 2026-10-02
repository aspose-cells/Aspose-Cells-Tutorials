---
category: general
date: 2026-05-30
description: SmartMarkerProcessor'ı kullanarak mevcut sayfayı yeniden adlandırma ve
  Excel sayfa yeniden adlandırma görevlerini birkaç basit adımda otomatikleştirme.
draft: false
keywords:
- how to use smartmarkerprocessor
- rename existing sheet
- automate excel sheet rename
language: tr
og_description: How to use SmartMarkerProcessor to rename existing sheet and automate
  Excel sheet rename tasks in a concise, step‑by‑step guide.
og_title: SmartMarkerProcessor Nasıl Kullanılır – Excel'de Mevcut Sayfayı Yeniden
  Adlandırma
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  headline: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  type: TechArticle
- description: How to use SmartMarkerProcessor to rename existing sheet and automate
    Excel sheet rename tasks in a few simple steps.
  name: How to Use SmartMarkerProcessor – Rename Existing Sheet in Excel
  steps:
  - name: 1. Multiple Existing Detail Sheets
    text: If your template already contains **Detail**, **Detail_1**, and **Detail_2**,
      the processor will generate **Detail_3**. This behavior is deterministic, so
      you can rely on it for batch processing.
  - name: 2. Custom Prefixes or Suffixes
    text: You might want the new sheet to start with a date stamp, e.g., `"Detail_2023-09-01"`.
      Set `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"`. The processor
      will still add numeric suffixes if needed.
  - name: 3. Renaming Other Sheets
    text: '`SmartMarkerOptions` also provides `HeaderSheetNewName` and `SummarySheetNewName`.
      Use them the same way to **rename existing sheet** types beyond the detail sheet.'
  - name: 4. Performance Considerations
    text: When processing large workbooks (hundreds of sheets), instantiate **one**
      `SmartMarkerProcessor` and reuse it across files. This reduces memory churn
      and speeds up the **automate excel sheet rename** workflow.
  type: HowTo
tags:
- Excel automation
- GemBox
- SmartMarker
title: SmartMarkerProcessor Nasıl Kullanılır – Excel’de Mevcut Sayfayı Yeniden Adlandırma
url: /tr/net/worksheet-management/how-to-use-smartmarkerprocessor-rename-existing-sheet-in-exc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarkerProcessor Nasıl Kullanılır – Excel'de Mevcut Sayfayı Yeniden Adlandırma

Veri doldururken mevcut bir sayfayı yeniden adlandırmak için **SmartMarkerProcessor**'ı nasıl kullanacağınızı hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, şablonlarında zaten bir “Detail” çalışma sayfası bulunduğunda ve SmartMarker motoru aynı isimde başka bir sayfa oluşturmaya çalıştığında bir engelle karşılaşıyor. İyi haber? Birkaç satır kodla **Excel sayfa yeniden adlandırmayı otomatikleştirebilir** ve iş akışınızı bozmazsınız.

Bu öğreticide, işlemciyi nasıl yapılandıracağınızı, mevcut sayfaları nasıl yeniden adlandıracağınızı ve Excel dosyalarınızı düzenli tutacağınızı gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Tahmin yürütmeye gerek yok—sadece net kod, *neden* her satırın önemli olduğuna dair açıklamalar ve kaçınılmaz olarak karşılaşacağınız uç durumları ele almanız için ipuçları.

---

## Önkoşullar

- **GemBox.Spreadsheet** (veya `SmartMarkerProcessor` sağlayan herhangi bir kütüphane) 2024‑latest sürümü NuGet üzerinden yüklü.
- .NET geliştirme ortamı (Visual Studio, VS Code, Rider—seçiminiz).
- Temel bir Excel şablonu (`Template.xlsx`) ve içinde zaten **Detail** adlı bir çalışma sayfası bulunuyor.
- Şablona birleştirmek istediğiniz basit bir veri kaynağı (ör. `DataTable`, `List<T>` veya anonim bir nesne).

Hepsi bu kadar. Eğer bunlardan herhangi birine sahip değilseniz, hemen NuGet paketini edinin:

```bash
dotnet add package GemBox.Spreadsheet
```

---

![smartmarkerprocessor örneğini nasıl kullanılır](/images/smartmarkerprocessor-rename.png "smartmarkerprocessor örneğini nasıl kullanılır")

*Yukarıdaki görsel, yeniden adlandırma işleminden önce ve sonra çalışma sayfasını göstermektedir.*

---

## Adım 1: SmartMarkerProcessor Örneğini Oluşturma  

İlk olarak ihtiyacınız olan **SmartMarkerProcessor** nesnesidir. Bunu, şablonunuzu okuyan, Smart Marker'ları (ör. `{{Name}}`) arayan ve verileri uygun hücrelere yazan bir motor olarak düşünün.

```csharp
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

// Initialize the component (license key is optional for the free version)
SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

// Load the workbook that contains the template sheet.
var wb = ExcelFile.Load("Template.xlsx");

// Create the processor instance.
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

> **Neden önemli:** İşlemciyi **bir kez** örnekleyip uygulama boyunca yeniden kullanmak yükü azaltır. Ayrıca, çalışma kitabını önce yüklemek, sayfa koleksiyonuna bir referans sağlar; bu, sayfaları yeniden adlandırırken ihtiyacımız olacak.

---

## Adım 2: Mevcut Sayfayı Yeniden Adlandırma Seçeneklerini Yapılandırma  

Şimdi konunun özüne geliyoruz: SmartMarker'a bir sayfa adı çakışmasıyla karşılaştığında nasıl davranacağını söylemek. `SmartMarkerOptions` sınıfı `DetailSheetNewName` adlı bir özellik sunar. Eğer `"Detail"` adlı bir sayfa zaten varsa, işlemci çakışmayı önlemek için otomatik olarak bir ek (`_1`, `_2`, …) ekleyecektir.

```csharp
// Define processing options.
// The DetailSheetNewName property controls the base name for the detail sheet.
SmartMarkerOptions options = new SmartMarkerOptions
{
    // If "Detail" exists, the new sheet will become "Detail_1"
    DetailSheetNewName = "Detail"
};
```

> **Pro ipucu:** Özel bir ek tercih ediyorsanız (ör. `"Detail-Backup"`), sadece `DetailSheetNewName = "Detail-Backup"` olarak ayarlayın. İşlemci yine gerektiğinde sayılar ekleyecektir.

> **Neden önemli:** Bu seçenek olmadan, SmartMarker bir istisna fırlatır veya mevcut sayfayı sessizce üzerine yazar, bu da veri kaybına yol açar. Yeniden adlandırma davranışını açıkça yapılandırmak **Excel sayfa yeniden adlandırmayı otomatikleştirir** ve şablonlarınızı sağlam tutar.

---

## Adım 3: Veri Kaynağını Hazırlama  

SmartMarker, neredeyse her türlü enumerable veri kaynağıyla çalışabilir. Örnek olarak, fatura satırlarını temsil eden basit bir anonim nesne listesi kullanalım.

```csharp
var dataSource = new[]
{
    new { Item = "Widget A", Quantity = 5, Price = 9.99 },
    new { Item = "Widget B", Quantity = 2, Price = 19.95 },
    new { Item = "Widget C", Quantity = 1, Price = 49.50 }
};
```

Eğer zaten bir `DataTable` veya `IEnumerable<T>`'ınız varsa, sadece bağlayın—ek bir dönüşüm gerekmez.

---

## Adım 4: İlk Çalışma Sayfasına SmartMarker İşlemini Uygulama  

İşlemci, seçenekler ve veri hazır olduğunda, birleştirmeyi çalıştırma zamanı. Şablonumuzun bulunduğu **ilk çalışma sayfasını** (`wb.Worksheets[0]`) hedefleyeceğiz. `Process` metodu üç argüman alır: çalışma sayfası, veri kaynağı ve daha önce tanımladığımız seçenekler.

```csharp
// Apply SmartMarker processing.
// This will insert the data into the template and rename the detail sheet if needed.
processor.Process(wb.Worksheets[0], dataSource, options);
```

> **Arka planda ne olur?**  
> 1. SmartMarker, `{{Item}}`, `{{Quantity}}` gibi işaretleri bulmak için çalışma sayfasını tarar.  
> 2. `DetailSheetNewName` içinde tanımlanan adı kullanarak yeni bir detay sayfası oluşturur.  
> 3. Eğer “Detail” adlı bir sayfa zaten varsa, otomatik olarak “Detail_1” olur.  
> 4. Veri satırları yeni sayfaya, biçimlendirmeyi koruyarak yazılır.

---

## Adım 5: Sonucu Kaydetme ve Yeniden Adlandırmayı Doğrulama  

İşlemden sonra, çalışma kitabını diske kaydetmek ve sayfanın doğru şekilde yeniden adlandırıldığını iki kez kontrol etmek isteyeceksiniz.

```csharp
// Save the processed workbook.
wb.Save("Result.xlsx");

// Quick verification (optional console output)
Console.WriteLine("Worksheets in the resulting file:");
foreach (var sheet in wb.Worksheets)
    Console.WriteLine($"- {sheet.Name}");
```

`Result.xlsx` dosyasını açtığınızda, **Detail_1** adlı bir sayfa görmelisiniz (eğer “Detail_1” zaten varsa **Detail_2**). Veri satırları, şablonda yerleştirdiğiniz başlık satırının altında görünecek.

---

## Yaygın Uç Durumları Ele Alma  

### 1. Birden Fazla Mevcut Detail Sayfası  

Şablonunuz zaten **Detail**, **Detail_1** ve **Detail_2** içeriyorsa, işlemci **Detail_3** oluşturur. Bu davranış deterministiktir, bu yüzden toplu işleme için güvenebilirsiniz.

### 2. Özel Ön Ekler veya Son Ekler  

Yeni sayfanın tarih damgası ile başlamasını isteyebilirsiniz, ör. `"Detail_2023-09-01"`. `DetailSheetNewName = $"Detail_{DateTime.Today:yyyy-MM-dd}"` olarak ayarlayın. İşlemci yine gerektiğinde sayısal ekler ekleyecektir.

### 3. Diğer Sayfaları Yeniden Adlandırma  

`SmartMarkerOptions` ayrıca `HeaderSheetNewName` ve `SummarySheetNewName` sağlar. Bunları da aynı şekilde, detay sayfasının ötesindeki **mevcut sayfaları yeniden adlandırmak** için kullanın.

```csharp
options.HeaderSheetNewName = "Header";
options.SummarySheetNewName = "Summary";
```

### 4. Performans Düşünceleri  

Büyük çalışma kitaplarını (yüzlerce sayfa) işlerken, **tek** bir `SmartMarkerProcessor` örneği oluşturun ve dosyalar arasında yeniden kullanın. Bu, bellek tüketimini azaltır ve **excel sayfa yeniden adlandırmayı otomatikleştirme** iş akışını hızlandırır.

---

## Tam Çalışan Örnek  

Her şeyi bir araya getirerek, hemen bir konsol uygulamasına kopyalayıp çalıştırabileceğiniz bağımsız bir program burada:

```csharp
using System;
using GemBox.Spreadsheet;
using GemBox.Spreadsheet.SmartMarkers;

class Program
{
    static void Main()
    {
        // 1. License & load template.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");
        var wb = ExcelFile.Load("Template.xlsx");

        // 2. Create processor.
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 3. Define rename options.
        SmartMarkerOptions options = new SmartMarkerOptions
        {
            DetailSheetNewName = "Detail"
        };

        // 4. Prepare data source.
        var dataSource = new[]
        {
            new { Item = "Widget A", Quantity = 5, Price = 9.99 },
            new { Item = "Widget B", Quantity = 2, Price = 19.95 },
            new { Item = "Widget C", Quantity = 1, Price = 49.50 }
        };

        // 5. Process the first worksheet.
        processor.Process(wb.Worksheets[0], dataSource, options);

        // 6. Save the result.
        wb.Save("Result.xlsx");

        // 7. Verify sheet names.
        Console.WriteLine("Worksheets after processing:");
        foreach (var sheet in wb.Worksheets)
            Console.WriteLine($"- {sheet.Name}");
    }
}
```

**Beklenen çıktı** (konsol):

```
Worksheets after processing:
- Sheet1
- Detail_1
```

`Result.xlsx` dosyasını açın ve verilerin yeni **Detail_1** sekmesinin altında düzgün bir şekilde yer aldığını göreceksiniz.

---

## Özet  

**SmartMarkerProcessor**'ı mevcut bir sayfayı güvenli bir şekilde yeniden adlandırmak ve **Excel sayfa yeniden adlandırmayı** tamamen otomatikleştirmek için nasıl kullanacağınızı ele aldık. Önemli çıkarımlar şunlardır:

1. Tek bir `SmartMarkerProcessor` örneği oluşturun.  
2. Yeniden adlandırma mantığını kontrol etmek için `DetailSheetNewName` (veya diğer sayfa‑adı seçeneklerini) ayarlayın.  
3. Veri kaynağınızı ve seçeneklerinizi `Process` metoduna geçirin.  
4. Sayfanın beklendiği gibi yeniden adlandırıldığını kaydedin ve doğrulayın.

Bu adımlarla, SmartMarker'ı herhangi bir raporlama hattına entegre edebilirsiniz—faturalar, denetim günlükleri veya aylık panolar oluşturuyor olun. Yaklaşım ölçeklenebilir, ad çakışmalarını sorunsuz yönetir ve Excel şablonlarınızı yeniden kullanılabilir tutar.

Denemekten çekinmeyin—belki her çalıştırmada otomatik olarak bir sürüm numarası ekleyen bir “Report_2024_Q1” sayfası oluşturursunuz. Olasılıklar sonsuzdur ve artık **mevcut sayfayı yeniden adlandırma** otomasyonu için sağlam bir temele sahipsiniz.

Kodlamaktan keyif alın ve Excel dosyalarınız her zaman düzenli kalsın!

## Sıradaki Adım?

- **Diğer SmartMarkerOptions**'ı keşfedin: `HeaderSheetNewName`, `SummarySheetNewName` ve daha ince kontrol için `InsertBlankRows`.
- **Stil ile birleştirin**: Birleştirmeden sonra renkler, kenarlıklar veya koşullu biçimlendirme uygulamak için GemBox'ın zengin biçimlendirme API'sini kullanın.
- **Birden fazla çalışma kitabını toplu işleyin**: Şablonların bulunduğu bir dizini döngüye alın, maksimum verimlilik için aynı işlemci örneğini yeniden kullanın.

Denemekten çekinmeyin—belki her çalıştırmada otomatik olarak bir sürüm numarası ekleyen bir “Report_2024_Q1” sayfası oluşturursunuz. Olasılıklar sonsuzdur ve artık **mevcut sayfayı yeniden adlandırma** otomasyonu için sağlam bir temele sahipsiniz.

- [Aspose.Cells for .NET ile Excel Sayfalarını Birleştirme ve Yeniden Adlandırma: Adım Adım Kılavuz](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [Aspose.Cells ile .NET'te Excel Sayfa ID'lerini Değiştirme: Kapsamlı Rehber](/cells/english/net/worksheet-management/change-excel-sheet-id-net-aspose-cells/)
- [Aspose.Cells for .NET ile Excel'de Satır ve Sütunları Gruplama](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}