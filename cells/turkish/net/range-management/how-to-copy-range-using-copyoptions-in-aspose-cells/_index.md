---
category: general
date: 2026-11-19
description: Aspose.Cells'te CopyOptions kullanarak bir aralığı nasıl kopyalayacağınızı
  öğrenin; biçimlendirmeyi ve pivot tabloları koruyarak biçimlendirilmiş bir Excel
  aralığını kopyalayın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range using copyoptions
- copy excel range with formatting
- Aspose.Cells copy range
- preserve pivot tables Aspose
- Excel automation C#
language: tr
lastmod: 2026-11-19
og_description: Aspose.Cells'ta CopyOptions kullanarak aralığı kopyalamak, tam biçimlendirme
  ve özet tablolar korunarak Excel verilerini çoğaltmanıza olanak tanır ve güvenilir
  çalışma kitabı manipülasyonu sağlar.
og_image_alt: Screenshot of C# code that copies an Excel range using Aspose.Cells
  CopyOptions
og_title: Aspose.Cells'ta CopyOptions kullanarak aralığı kopyalama – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  headline: How to copy range using CopyOptions in Aspose.Cells
  type: TechArticle
- description: Learn how to copy range using CopyOptions in Aspose.Cells, preserving
    formatting and pivot tables while copying an Excel range with formatting.
  name: How to copy range using CopyOptions in Aspose.Cells
  steps:
  - name: Why `CopyOptions` matters
    text: '* **Performance** – The library performs a single internal operation rather
      than copying cells one‑by‑one. * **Accuracy** – All visual aspects (fonts, colors,
      borders) survive the move, which eliminates visual drift in generated reports.
      * **Reliability** – Pivot tables remain functional because the'
  - name: What if the destination area overlaps the source?
    text: 'Aspose.Cells throws an `ArgumentException`. To avoid this, calculate a
      destination that does not intersect the source, or copy to a different worksheet:'
  - name: How to copy between different workbooks?
    text: 'Create a second `Workbook` instance for the target file and use the same
      `CopyOptions` object:'
  - name: Does `CopyOptions` also copy merged cells?
    text: Yes. The `CopyStyle` flag includes merged‑cell information. If you need
      finer control, set `options.CopyMergedCells = true` (available in newer versions).
  - name: What about large ranges (thousands of rows)?
    text: The operation is memory‑efficient, but you may want to increase the `WorkbookSettings`
      `MemorySetting` to `MemorySetting.MemoryPreference` for very large files.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells'te CopyOptions kullanarak aralığı nasıl kopyalarım
url: /tr/net/range-management/how-to-copy-range-using-copyoptions-in-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells'ta CopyOptions Kullanarak Aralığı Kopyalama

Aspose.Cells'ta **copy range using CopyOptions**'a ihtiyacınız varsa, bu kılavuz hücre bloğunu nasıl çoğaltacağınızı ve tüm biçimlendirmeyi ve gömülü pivot tablolarını bozulmadan koruyacağınızı tam olarak gösterir. Birçok geliştirici, verileri çalışma sayfaları arasında taşırken biçimi korumakta zorlanır ve `CopyOptions` sınıfı bu sorunu ekstra manuel adımlar olmadan çözer.

Bu öğreticide şunları öğreneceksiniz:

* Excel çalışma kitabında kaynak ve hedef alanları tanımlama.  
* `CopyOptions` kullanarak hücre biçimlendirmesini, sütun genişliklerini ve pivot tablolarını koruma.  
* Sonucu, sonraki işleme hazır yeni bir dosyaya kaydetme.  

Örnek, herhangi bir `.xlsx` dosyasıyla çalışır ve yalnızca Aspose.Cells for .NET kütüphanesini gerektirir.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 veya daha yeni bir sürüm yüklü.  
* Geçerli bir Aspose.Cells for .NET lisansı (veya ücretsiz değerlendirme anahtarı).  
* Visual Studio 2022 veya tercih ettiğiniz herhangi bir C# IDE.  

`Aspose.Cells` dışındaki ek NuGet paketlerine gerek yok.

## Adım 1: Projeyi kurun ve ad alanlarını içe aktarın

Yeni bir konsol uygulaması oluşturun ve Aspose.Cells referansını ekleyin:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Your code will go here
        }
    }
}
```

`using Aspose.Cells;` yönergesi, `Workbook`, `CellArea` ve `CopyOptions` öğelerine erişmenizi sağlar.

## Adım 2: Değiştirmek istediğiniz çalışma kitabını yükleyin

```csharp
// Step 2: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`Workbook`, tüm Excel dosyasını temsil eder. `YOUR_DIRECTORY` ifadesini, kaynak dosyanızın bulunduğu klasörle değiştirin.

## Adım 3: Kaynak ve hedef aralıkları tanımlayın

```csharp
// Step 3: Define the source range (A1:H30)
CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");

// Step 3b: Define the destination range (A35:H64)
CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");
```

`CellArea.CreateCellArea`, sol‑üst ve sağ‑alt hücre adreslerine göre dikdörtgen bir alan oluşturur. Kopyalamanız gereken bloğun boyutuna uyması için koordinatları ayarlayabilirsiniz.

## Adım 4: Biçimlendirmeyi ve pivot tablolarını koruyarak aralığı kopyalayın

```csharp
// Step 4: Copy the range using CopyOptions
CopyOptions options = new CopyOptions
{
    // Preserve all cell styles, number formats, and column widths
    CopyStyle = true,
    // Keep formulas unchanged (they will still reference the original sheet)
    CopyFormula = true,
    // Preserve any pivot tables that intersect the copied area
    CopyPivotTables = true,
    // Retain data validation and conditional formatting
    CopyDataValidation = true,
    CopyConditionalFormatting = true
};

workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
```

`CopyOptions` nesnesi, Aspose.Cells'e tam olarak neyin korunacağını söyler. Kaynağınızda pivot tablolar bulunduğunda `CopyPivotTables = true` ayarı, **copy range using CopyOptions** için anahtardır. Diğer bayraklar ise **copy excel range with formatting** işleminin otomatik olarak gerçekleşmesini sağlar—kopyalama sonrası stilleri yeniden uygulamak için ekstra koda gerek kalmaz.

### `CopyOptions` neden önemlidir

- **Performance** – Kütüphane, hücreleri tek tek kopyalamak yerine tek bir iç işlem gerçekleştirir.  
- **Accuracy** – Tüm görsel öğeler (yazı tipleri, renkler, kenarlıklar) taşınma sırasında korunur, bu da oluşturulan raporlarda görsel kaymayı önler.  
- **Reliability** – Pivot tablolar, önbellekleri ve kaynak referansları kopyalandığı için işlevsel kalır.

## Adım 5: Değiştirilen çalışma kitabını kaydedin

```csharp
// Step 5: Save the workbook with the copied range
workbook.Save("YOUR_DIRECTORY/output.xlsx");
Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
```

`Save` çağrıldıktan sonra, `output.xlsx` dosyası orijinal verileri ve hedef konumda biçimlendirme ve pivot tabloları içeren kopyalanmış bloğu içerir.

## Referans için tam kaynak kodu

```csharp
using System;
using Aspose.Cells;

namespace ExcelCopyDemo
{
    class Program
    {
        static void Main()
        {
            // Load the source workbook
            Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // Define source and destination ranges
            CellArea sourceRange = CellArea.CreateCellArea("A1", "H30");
            CellArea destinationRange = CellArea.CreateCellArea("A35", "H64");

            // Configure copy options to preserve everything
            CopyOptions options = new CopyOptions
            {
                CopyStyle = true,
                CopyFormula = true,
                CopyPivotTables = true,
                CopyDataValidation = true,
                CopyConditionalFormatting = true
            };

            // Perform the copy operation
            workbook.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);

            // Save the result
            workbook.Save("YOUR_DIRECTORY/output.xlsx");
            Console.WriteLine("Range copied successfully. Output saved to output.xlsx");
        }
    }
}
```

Running this program prints:

```
Range copied successfully. Output saved to output.xlsx
```

`output.xlsx` dosyasını Excel'de açın – A1:H30 bloğunun A35:H64'te kopyalandığını, tüm hücre renkleri, kenarlıklar, sayı biçimleri ve pivot tablolarının bozulmadan olduğunu göreceksiniz.

## Yaygın sorular ve uç‑durum yönetimi

### Hedef alan kaynakla çakışırsa ne olur?

Aspose.Cells bir `ArgumentException` fırlatır. Bunu önlemek için, kaynakla kesişmeyen bir hedef konum hesaplayın veya farklı bir çalışma sayfasına kopyalayın:

```csharp
Worksheet destSheet = workbook.Worksheets.Add("CopySheet");
destSheet.Cells.CopyRange(sourceRange, CellArea.CreateCellArea("A1", "H30"), options);
```

### Farklı çalışma kitapları arasında nasıl kopyalanır?

Hedef dosya için ikinci bir `Workbook` örneği oluşturun ve aynı `CopyOptions` nesnesini kullanın:

```csharp
Workbook target = new Workbook();
target.Worksheets[0].Cells.CopyRange(sourceRange, destinationRange, options);
target.Save("target.xlsx");
```

### `CopyOptions` birleştirilmiş hücreleri de kopyalar mı?

Evet. `CopyStyle` bayrağı birleştirilmiş hücre bilgilerini içerir. Daha ince kontrol gerekiyorsa, `options.CopyMergedCells = true` olarak ayarlayın (daha yeni sürümlerde mevcuttur).

### Büyük aralıklar (binlerce satır) hakkında ne söyleyebiliriz?

İşlem bellek açısından verimlidir, ancak çok büyük dosyalar için `WorkbookSettings` `MemorySetting` değerini `MemorySetting.MemoryPreference` olarak artırmak isteyebilirsiniz.

## Profesyonel ipuçları

- **Reuse the same `CopyOptions`** örneğini birden fazla kopyalama işlemi için yeniden kullanın – nesne tahsis yükünü azaltır.  
- **Validate ranges** kopyalamadan önce: `if (!CellArea.IsValid(sourceRange) || !CellArea.IsValid(destinationRange))` yazım hatalarına bağlı hataları erken yakalamaya yardımcı olur.  
- **Turn off calculation** (`workbook.Settings.CalcMode = CalculationMode.Manual`) büyük veri setlerini kopyalarken süreci hızlandırmak için devre dışı bırakın, ardından kopyalama sonrası güncel sonuçlara ihtiyacınız varsa `workbook.CalculateFormula()` çağırın.

## Sonuç

Artık Aspose.Cells'ta **copy range using CopyOptions** nasıl yapılacağını biliyorsunuz; bu, **copy excel range with formatting** işlemini tam olarak gerçekleştirirken pivot tabloları ve diğer gelişmiş özellikleri korur. Bu yaklaşım manuel stil yeniden uygulamayı ortadan kaldırır ve Excel otomasyonunuzun sağlam ve sürdürülebilir olmasını sağlar.

İleride keşfedebileceğiniz adımlar:

* `CopyOptions` kullanarak tüm çalışma sayfalarını çoğaltın.  
* Kopyalama işlemini `WorksheetCollection.AddCopy` ile birleştirerek şablon‑tabanlı rapor oluşturun.  
* Kodu bir ASP.NET Core API'ye entegre ederek anlık Excel dönüşümleri sağlayın.

Farklı kaynak/hedef koordinatlarıyla denemeler yapmaktan çekinmeyin ve sonuçlarınızı yorumlarda paylaşın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Excel Aspose Cells Dotnet Copy Range Data](/cells/german/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/french/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)
- [Excel Aspose Cells Dotnet Copy Range Data](/cells/spanish/net/range-management/excel-aspose-cells-dotnet-copy-range-data/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}