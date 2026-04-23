---
category: general
date: 2026-01-14
description: Aspose.Cells kullanarak pivot tabloyu nasıl kopyalanır ve aynı zamanda
  tek bir öğreticide Excel'i PPTX'e dönüştürmeyi, bir aralığı başka bir çalışma kitabına
  kopyalamayı ve PPTX'te metin kutusunu düzenlenebilir hâle getirmeyi öğrenin.
draft: false
keywords:
- how to copy pivot table
- convert excel to pptx
- copy range to another workbook
- make textbox editable pptx
- save workbook as pptx
language: tr
og_description: Pivot tabloyu nasıl kopyalar ve ardından Excel’i PPTX’e dönüştürür,
  aralığı başka bir çalışma kitabına kopyalar ve metin kutusunu düzenlenebilir PPTX
  yapar—hepsi Aspose.Cells ile.
og_title: C#'ta Pivot Tablosunu Kopyalama – Excel'den PPTX'ye Tam Rehber
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: C#'da Pivot Tablosunu Kopyalama – Excel'i PPTX'e Dönüştürme, Aralığı Kopyalama
  ve Metin Kutusunu Düzenlenebilir Yapma
url: /tr/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Pivot Tablosunu Nasıl Kopyalarsınız – Tam Excel to PPTX Kılavuzu

Bir çalışma kitabından diğerine pivot tablosunu kopyalamak, Excel‑tabanlı raporları otomatikleştirirken sık sorulan bir sorudur. Bu öğreticide **Aspose.Cells for .NET** kullanarak üç gerçek dünya senaryosunu adım adım inceleyeceğiz: bir pivot‑tablo aralığını kopyalama, bir çalışma sayfasını düzenlenebilir bir metin kutusuna sahip bir PPTX dosyasına dışa aktarma ve Smart Markers aracılığıyla bir JSON dizisini tek bir hücreye doldurma.  

Ayrıca **Excel to PPTX** dönüştürmeyi, **range'i başka bir çalışma kitabına kopyalamayı** ve **textbox editable PPTX** yapmayı, biçimlendirmeyi bozmadan göreceksiniz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz, çalıştırmaya hazır bir kod tabanına sahip olacaksınız.

> **Pro tip:** Tüm örnekler Aspose.Cells 23.12 sürümünü hedeflemektedir, ancak aynı kavramlar küçük API ayarlamalarıyla önceki sürümlere de uygulanabilir.

![Diagram showing how a pivot table is copied, a worksheet exported to PPTX, and a JSON array inserted – how to copy pivot table workflow](how-to-copy-pivot-table-diagram.png)

---

## İhtiyacınız Olanlar

- Visual Studio 2022 (veya herhangi bir C# IDE)
- .NET 6.0 veya daha yeni bir çalışma zamanı
- Aspose.Cells for .NET NuGet paketi  
  ```bash
  dotnet add package Aspose.Cells
  ```
- İki örnek Excel dosyası (`source.xlsx`, `chartWithTextbox.xlsx`) kontrol ettiğiniz bir klasöre yerleştirin (`YOUR_DIRECTORY` ifadesini gerçek yolunuzla değiştirin).

Ek bir kütüphane gerekmez; aynı `Aspose.Cells` derlemesi Excel, PPTX ve Smart Markers'ı yönetir.

## Pivot Tablosunu Kopyalama ve Verilerini Korumak

Pivot tablo içeren bir aralığı kopyaladığınızda, varsayılan davranış yalnızca **değerleri** yapıştırmaktır. Pivot tanımını bozulmadan tutmak için `CopyPivotTable` bayrağını etkinleştirmeniz gerekir.

### Adım‑Adım

1. **Pivot tabloyu içeren kaynak çalışma kitabını yükleyin**.  
2. **Boş bir hedef çalışma kitabı oluşturun** – bu, kopyalanan aralığı alacak.  
3. **`CopyRange`'i `CopyPivotTable = true` ile kullanın** böylece pivot tanımı veriyle birlikte taşınır.  
4. **Hedef dosyayı istediğiniz yere kaydedin**.

#### Full Code Example

```csharp
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // Step 1: Load the source workbook and define the range to copy
        Workbook sourceWorkbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
        // Assuming the pivot table lives inside A1:G20
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // Step 2: Create a destination workbook (blank)
        Workbook destinationWorkbook = new Workbook();
        Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

        // Step 3: Copy the range, preserving the pivot table
        destinationSheet.Cells.CopyRange(
            sourceRange,
            "B2", // paste start cell
            new CopyOptions { CopyPivotTable = true });

        // Step 4: Save the result
        destinationWorkbook.Save(@"YOUR_DIRECTORY\copyWithPivot.xlsx");
    }
}
```

**Neden bu çalışır:** `CopyOptions.CopyPivotTable` Aspose.Cells'e yalnızca işlenmiş değerler yerine temel `PivotTable` nesnesini kopyalamasını söyler. Hedef çalışma kitabı artık programatik olarak yenileyebileceğiniz veya değiştirebileceğiniz tam işlevsel bir pivot içerir.

**Köşe durum:** Kaynak çalışma kitabı harici veri kaynakları kullanıyorsa, kopyaladıktan sonra verileri gömmeniz veya bağlantı dizesini ayarlamanız gerekebilir, aksi takdirde pivot “#REF!” hatası gösterir.

## Excel'i PPTX'e Dönüştürme ve Metin Kutusunu Düzenlenebilir Yapma

Bir çalışma sayfasını PowerPoint'e dışa aktarmak, verilerden doğrudan slayt desteleri oluşturmak için kullanışlıdır. Varsayılan olarak dışa aktarılan metin kutusu statik bir şekil olur, ancak `IsTextBoxEditable` ayarlandığında bu davranış tersine döner.

### Adım‑Adım

1. **Dışa aktarmak istediğiniz grafik ve metin kutusunu içeren çalışma kitabını açın**.  
2. **`ImageOrPrintOptions`'ı `SaveFormat = SaveFormat.Pptx` ile yapılandırın**.  
3. **Metin kutusunu içerecek bir yazdırma alanı tanımlayın**.  
4. **`IsTextBoxEditable`'i etkinleştirin** böylece PPTX açıldıktan sonra metin düzenlenebilir.  
5. **PPTX dosyasını kaydedin**.

#### Full Code Example

```csharp
using Aspose.Cells;

class ExcelToPptxDemo
{
    static void Main()
    {
        // Step 1: Load the workbook with chart and textbox
        Workbook chartWorkbook = new Workbook(@"YOUR_DIRECTORY\chartWithTextbox.xlsx");

        // Step 2: Set export options for PPTX
        ImageOrPrintOptions pptxOptions = new ImageOrPrintOptions
        {
            SaveFormat = SaveFormat.Pptx
        };

        // Step 3: Define the print area that captures the textbox (A1:D20)
        chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:D20";

        // Step 4: Make the textbox editable in the exported PPTX
        chartWorkbook.Worksheets[0].PageSetup.IsTextBoxEditable = true;

        // Step 5: Export the worksheet to a PPTX file
        chartWorkbook.Save(@"YOUR_DIRECTORY\result.pptx", pptxOptions);
    }
}
```

**Sonuç:** `result.pptx` dosyasını PowerPoint'te açın – Excel'de yerleştirdiğiniz metin kutusu artık içine yazabileceğiniz normal bir metin kutusu olur. Elle yeniden oluşturmanıza gerek yok.

**Yaygın tuzak:** Çalışma sayfası, yazdırma alanıyla kesişen birleştirilmiş hücreler içeriyorsa, ortaya çıkan slayt kayabilir. Dışa aktarmadan önce yazdırma alanını ayarlayın veya hücre birleştirmelerini kaldırın.

## Smart Markers ile Başka Bir Çalışma Kitabına Aralık Kopyalama (JSON → Tek Hücre)

Bazen bir JSON dizisini tek bir Excel hücresine gömmeniz gerekir; örneğin, aşağı akış sistemlerine JSON dizesi bekleyen veri gönderirken. Aspose.Cells'in Smart Markers'ı, `ArrayAsSingle = true` ayarlandığında bir diziyi tek hücre olarak serileştirebilir.

### Adım‑Adım

1. **Smart Marker yer tutucusunu (ör. `&=Items.Name`) içeren bir şablon çalışma kitabını yükleyin**.  
2. **Veri nesnesini hazırlayın** – `Items` dizisine sahip anonim bir tip.  
3. **`SmartMarkerProcessor` oluşturun** ve veriyi `ArrayAsSingle` ile uygulayın.  
4. **Doldurulmuş çalışma kitabını kaydedin**.

#### Full Code Example

```csharp
using Aspose.Cells;
using System;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Load the template workbook containing a smart marker like "&=Items.Name"
        Workbook templateWorkbook = new Workbook(@"YOUR_DIRECTORY\SmartMarkerTemplate.xlsx");

        // Step 2: Prepare the data object with an array of items
        var data = new
        {
            Items = new[]
            {
                new { Name = "A" },
                new { Name = "B" }
            }
        };

        // Step 3: Apply the SmartMarkerProcessor with ArrayAsSingle option
        SmartMarkerProcessor processor = new SmartMarkerProcessor(templateWorkbook);
        processor.Apply(data, new SmartMarkerOptions { ArrayAsSingle = true });

        // Step 4: Save the result – the JSON array will appear in a single cell
        templateWorkbook.Save(@"YOUR_DIRECTORY\jsonSingleCell.xlsx");
    }
}
```

**Açıklama:** `ArrayAsSingle` true olduğunda, Aspose.Cells `Items.Name` öğelerinin her birini JSON benzeri bir dize (`["A","B"]`) olarak birleştirir ve smart marker'ın bulunduğu hücreye yazar. Bu, her öğe için ayrı bir satır oluşturulmasını önler.

**Ne zaman kullanılmalı:** Yapılandırma tablolarını, API yüklerini dışa aktarmak veya tüketicinin tablo düzeni yerine sıkıştırılmış bir JSON dizesi beklediği herhangi bir senaryo için idealdir.

## Ek İpuçları ve Köşe Durumu Yönetimi

| Senaryo | Dikkat Edilmesi Gereken | Önerilen Çözüm |
|----------|-------------------|---------------|
| **Büyük Pivot Tabloları** | Büyük pivot önbelleklerini kopyalarken bellek kullanımı artar. | Yüklemeden önce `WorkbookSettings.MemorySetting = MemorySetting.MemoryPreference` kullanın. |
| **Görsellerle PPTX'e Dışa Aktarma** | Görseller düşük DPI'da rasterleştirilebilir. | Daha net slaytlar için `pptxOptions.ImageResolution = 300` ayarlayın. |
| **Smart Marker JSON Biçimlendirme** | Özel karakterler (`"` , `\`) JSON'i bozar. | Manuel olarak kaçış karakteri ekleyin veya Smart Markers'a vermeden önce `JsonSerializer` ile önceden serileştirin. |
| **Farklı Excel Sürümleri Arasında Aralık Kopyalama** | Eski `.xls` dosyaları biçimlendirmeyi kaybedebilir. | Modern özellikleri korumak için hedefi `.xlsx` olarak kaydedin. |

## Özet – Pivot Tablosunu Nasıl Kopyalarsınız ve Daha Fazlası

İlk olarak **pivot tabloyu nasıl kopyalayacağınızı** ve işlevselliğini koruyarak yanıtladık, ardından **Excel'i PPTX'e dönüştürmeyi**, **textbox editable PPTX** yapmayı ve son olarak **Smart Markers kullanarak bir JSON dizisini tek hücreye gömerek aralığı başka bir çalışma kitabına kopyalamayı** gösterdik.

Üç kod parçacığı da bağımsızdır; yeni bir konsol uygulamasına yapıştırabilir, dosya yollarını ayarlayabilir ve bugün çalıştırabilirsiniz.

## Sonraki Adımlar

- **Diğer dışa aktarma formatlarını keşfedin** – Aspose.Cells ayrıca PDF, XPS ve HTML'yi destekler.  
- **Kopyaladıktan sonra `PivotTable.RefreshData()` kullanarak pivot tablolarını programatik olarak yenileyin**.  
- **Smart Markers'ı grafiklerle birleştirerek otomatik güncellenen dinamik kontrol panelleri oluşturun**.  

Eğer **çalışma kitabını PPTX olarak kaydetmek** ve özel slayt düzenleri kullanmakla ilgileniyorsanız, `SlideOptions` üzerine Aspose.Cells belgelerine göz atın.

Deney yapmaktan çekinmeyin—yazdırma alanını değiştirin, farklı `CopyOptions` deneyin veya daha karmaşık bir JSON yükü sağlayın. API, çoğu raporlama hattı için yeterince esnektir.

### Sıkça Sorulan Sorular

**Q: `CopyPivotTable` dilimleyicileri de kopyalıyor mu?**  
A: Doğrudan değil. Dilimleyiciler ayrı nesnelerdir; kopyaladıktan sonra onları yeniden oluşturmanız ya da `Worksheet.Shapes` koleksiyonu aracılığıyla kopyalamanız gerekir.

**Q: Birden fazla çalışma sayfasını tek bir PPTX destesine dışa aktarabilir miyim?**  
A: Evet. Her çalışma sayfası üzerinde döngü kurun, aynı `ImageOrPrintOptions` ile `Save` çağırın ve numaralandırmayı sürdürmek için `pptxOptions.StartSlideNumber` ayarlayın.

**Q: JSON dizim iç içe nesneler içerirse ne olur?**  
A: `ArrayAsSingle = false` ayarlayın ve üzerinde yineleme yapan özel bir şablon kullanın

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}