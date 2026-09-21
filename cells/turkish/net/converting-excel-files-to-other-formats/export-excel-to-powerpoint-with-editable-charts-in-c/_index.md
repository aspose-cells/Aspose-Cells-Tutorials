---
category: general
date: 2026-09-21
description: Aspose.Cells kullanarak düzenlenebilir grafiklerle Excel'i PowerPoint'e
  aktarın. Grafiklerin düzenlenebilir kalmasını sağlarken bir çalışma sayfasını PPTX'e
  dönüştürmek için bu adım adım kılavuzu izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- worksheet to powerpoint
- export excel chart pptx
- editable charts pptx
language: tr
lastmod: 2026-09-21
og_description: Aspose.Cells kullanarak düzenlenebilir grafiklerle Excel'i PowerPoint'e
  aktarın. Grafiklerin tam düzenlenebilirliğini koruyarak bir çalışma sayfasını PPTX'e
  nasıl dönüştüreceğinizi öğrenin.
og_image_alt: Screenshot of a PowerPoint slide showing an editable Excel chart after
  export
og_title: Düzenlenebilir grafiklerle Excel'i PowerPoint'e aktar – C# öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  headline: Export Excel to PowerPoint with editable charts in C#
  type: TechArticle
- description: Export Excel to PowerPoint with editable charts using Aspose.Cells.
    Follow this step‑by‑step guide to convert a worksheet to PPTX while keeping charts
    editable.
  name: Export Excel to PowerPoint with editable charts in C#
  steps:
  - name: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
    text: '**Preserve chart data ranges** – Ensure the chart data source resides in
      the same worksheet you are exporting. Cross‑sheet references are converted to
      static values in the PPTX.'
  - name: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
    text: '**Use the latest Aspose.Cells version** – New releases improve support
      for additional chart features and fix edge‑case bugs related to PPTX export.'
  - name: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
    text: '**Validate the output** – After conversion, open the generated PPTX in
      PowerPoint and verify that you can edit the chart title, series, and axis labels.
      If any element appears as an image, double‑check that `ExportChartAsEditableText`
      is enabled and that the chart type is supported.'
  - name: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
    text: '**Batch processing** – For automation scenarios (e.g., generating a slide
      deck from many Excel reports), wrap the conversion logic in a method that accepts
      `Workbook`, `int worksheetIndex`, and `string outputPath`. This isolates the
      **export excel to powerpoint** workflow and makes it reusable.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- PPTX export
title: C#'ta düzenlenebilir grafiklerle Excel'i PowerPoint'e aktar
url: /tr/net/converting-excel-files-to-other-formats/export-excel-to-powerpoint-with-editable-charts-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i PowerPoint'e Düzenlenebilir Grafiklerle C# ile Dışa Aktarma

Excel'i PowerPoint'e düzenlenebilir grafiklerle dışa aktarmak, tablo görsellerini sunumlarda yeniden kullanmanız gerektiğinde yaygın bir gereksinimdir. Bu kılavuz, Aspose.Cells for .NET kullanarak **export Excel to PowerPoint** işlemini grafik düzenlenebilirliğini koruyarak nasıl yapacağınızı gösterir.

Şunları öğreneceksiniz:

* Grafikler ve metin kutuları içeren mevcut bir çalışma kitabını yükleyin.  
* Grafiklerin ve şekillerin düzenlenebilir kalması için PPTX dışa aktarma seçeneklerini yapılandırın.  
* Belirli bir çalışma sayfasını, Microsoft PowerPoint'te açılıp düzenlenebilen bir PowerPoint dosyasına dönüştürün.

Bu öğretici, temel C# bilgisine ve .NET’in (≥ .NET 6) son sürümüne sahip olduğunuzu varsayar. Aspose.Cells ile ilgili önceden bir deneyim gerekmez.

---

## Excel'i PowerPoint'e Dışa Aktarma – Genel Bakış

**export Excel to PowerPoint** arkasındaki temel fikir, her çalışma sayfasını bir PPTX slaytına render edilebilen bir görüntü kaynağı olarak ele almaktır. `ExportChartAsEditableText` ve `ExportShapeAsEditableText` bayraklarını değiştirerek, Aspose.Cells grafik verilerini düz bir bitmap yerine PowerPoint çizim nesneleri olarak yazar. Bu sayede ortaya çıkan slayt tamamen düzenlenebilir olur—tıpkı PowerPoint içinde doğrudan oluşturulmuş bir grafik gibi.

> **Neden düzenlenebilir grafikler kullanılmalı?**  
> Düzenlenebilir grafikler, sunum sahiplerinin verileri, renkleri veya etiketleri orijinal Excel dosyasına geri dönmeden ayarlamasına olanak tanır, son dakika değişikliklerini hızlandırır ve sunum iş akışını sorunsuz tutar.

## Bir Çalışma Sayfasını PowerPoint'e Dönüştürme (worksheet to PowerPoint)

Aşağıda, **worksheet to PowerPoint** dönüşümünü gösteren tam, çalıştırılabilir bir örnek bulunmaktadır.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the chart and textbox
            // Replace YOUR_DIRECTORY with the actual folder path on your machine.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Configure PPTX export options to keep charts and shapes editable
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,               // Target format: PPTX
                ExportChartAsEditableText = true,           // Enable editable charts
                ExportShapeAsEditableText = true            // Enable editable shapes/textboxes
            };

            // Step 3: Export the first worksheet (index 0) to a PowerPoint file
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";
            workbook.Worksheets[0].ConvertToImage(exportOptions, outputPath);

            Console.WriteLine($"Worksheet successfully exported to {outputPath}");
        }
    }
}
```

### Her Adımın Açıklaması

| Adım | Kodun yaptığı şey | Neden **export excel chart pptx** için önemlidir |
|------|-------------------|----------------------------------------------|
| 1️⃣   | `input.xlsx` dosyasını bir `Aspose.Cells.Workbook` nesnesine yükler. | Çalışma kitabı, dışa aktarmak istediğiniz grafiklere erişim sağlar. |
| 2️⃣   | `ExportType` değerini `Pptx` olarak ayarlar ve `ExportChartAsEditableText` ve `ExportShapeAsEditableText` seçeneklerini etkinleştirir. | Bu bayraklar **editable charts pptx** için anahtardır – kütüphaneye grafik geometrisini raster görüntüler yerine PowerPoint çizim nesneleri olarak yazmasını söyler. |
| 3️⃣   | İlk çalışma sayfasında `ConvertToImage` metodunu çağırır ve `Worksheet.pptx` dosyasını üretir. | Metod, **export excel to powerpoint** işlemini gerçekleştirir ve doğrudan PowerPoint'te açılabilecek bir PPTX dosyası yazar. |

> **Pro tip:** *Birden fazla* çalışma sayfasını dışa aktarmanız gerekiyorsa, `workbook.Worksheets` üzerinde döngü kurup her biri için `ConvertToImage` çağırın; isteğe bağlı olarak çıktı dosyalarını `Sheet1.pptx`, `Sheet2.pptx` gibi adlandırabilirsiniz.

## PPTX'te Düzenlenebilir Grafikleri Etkinleştirme (export excel chart pptx)

`ExportChartAsEditableText` **true** olarak ayarlandığında, Aspose.Cells her grafiği PPTX XML içinde bir `<a:graphic>` öğeleri koleksiyonu olarak yazar. PowerPoint bu öğeleri yerel grafik nesneleri olarak algılar ve grafiğe çift‑tıklayarak grafik düzenleyicisini açabilirsiniz.

**Yaygın tuzaklar**

* **Missing Aspose.Cells license** – Lisans olmadan kütüphane çıktıya bir filigran ekler. Programınızda erken bir aşamada lisans kaydedin (`License license = new License(); license.SetLicense("Aspose.Cells.lic");`).  
* **Unsupported chart types** – Çoğu 2‑D grafik (sütun, çizgi, pasta) tamamen düzenlenebilirken, bazı karmaşık 3‑D veya kombinasyon grafikleri görüntülere geri dönebilir. Tam düzenlenebilirliğe güveniyorsanız grafik tiplerinizi test edin.  
* **Large worksheets** – Çok büyük çalışma sayfalarını dışa aktarmak önemli bellek tüketimine yol açabilir. Dönüştürülen alanı sınırlamak için `ImageOrPrintOptions` içinde `ExportMaxRows` veya `ExportMaxColumns` kullanmayı düşünün.

## Grafiklerin Düzenlenebilir Kalmasını Sağlama İpuçları (editable charts pptx)

1. **Preserve chart data ranges** – Grafik veri kaynağının dışa aktardığınız aynı çalışma sayfasında bulunduğundan emin olun. Sayfa dışı referanslar PPTX içinde statik değerlere dönüştürülür.  
2. **Use the latest Aspose.Cells version** – Yeni sürümler, ek grafik özellikleri desteğini artırır ve PPTX dışa aktarımıyla ilgili uç durum hatalarını giderir.  
3. **Validate the output** – Dönüştürmeden sonra oluşturulan PPTX'i PowerPoint'te açın ve grafik başlığını, serileri ve eksen etiketlerini düzenleyebildiğinizi doğrulayın. Herhangi bir öğe görüntü olarak görünüyorsa, `ExportChartAsEditableText`'in etkin olduğundan ve grafik tipinin desteklendiğinden emin olun.  
4. **Batch processing** – Otomasyon senaryoları (ör. birçok Excel raporundan bir slayt destesi oluşturma) için dönüşüm mantığını `Workbook`, `int worksheetIndex` ve `string outputPath` parametrelerini kabul eden bir metoda sarın. Bu, **export excel to powerpoint** iş akışını izole eder ve yeniden kullanılabilir hâle getirir.

## Tam Çalışan Örnek Özeti

Her şeyi bir araya getirerek, yeni bir .NET konsol projesine kopyalayıp yapıştırabileceğiniz minimal program aşağıdadır:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Register license (optional but removes evaluation watermark)
            // var license = new License();
            // license.SetLicense("Aspose.Cells.lic");

            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            string outputPath = @"YOUR_DIRECTORY\Worksheet.pptx";

            Workbook workbook = new Workbook(inputPath);

            ImageOrPrintOptions options = new ImageOrPrintOptions
            {
                ExportType = ExportType.Pptx,
                ExportChartAsEditableText = true,
                ExportShapeAsEditableText = true
            };

            workbook.Worksheets[0].ConvertToImage(options, outputPath);

            Console.WriteLine($"Export complete: {outputPath}");
        }
    }
}
```

**Beklenen Sonuç**

* `Worksheet.pptx` adlı bir dosya `YOUR_DIRECTORY` içinde görünür.  
* Dosyayı Microsoft PowerPoint'te açtığınızda, orijinal grafik ve metin kutularını içeren bir slayt gösterir.  
* Grafiğe çift tıkladığınızda PowerPoint'in grafik düzenleyicisi açılır ve seri değerlerini, renkleri veya eksen başlıklarını değiştirmenize izin verir—bu da **editable charts pptx** özelliğinin amaçlandığı gibi çalıştığını doğrular.

## Sonuç

Artık **export Excel to PowerPoint** işlemini grafiklerin düzenlenebilir kalmasını sağlayarak tam bir çözüme sahipsiniz. `ImageOrPrintOptions` içinde `ExportChartAsEditableText` ve `ExportShapeAsEditableText` ayarlarını yapılandırarak, dönüşüm süreci grafiklerin doğrudan PowerPoint'te oluşturulmuş gibi davrandığı yerel bir PPTX dosyası üretir.  

Bundan sonra şunları yapabilirsiniz:

* Kodunuzu birden fazla çalışma sayfasını işleyebilecek şekilde genişletin (**worksheet to PowerPoint** her biri için).  
* Dışa aktarmayı, slayt başlıkları ekleme veya resim yerleştirme gibi diğer Aspose.Cells özellikleriyle birleştirin.  
* Özel temalarla **export Excel chart PPTX** gibi ilgili konuları keşfedin veya tüm slayt paketi oluşturma sürecini otomatikleştirin.

Farklı grafik tipleriyle denemeler yapın, veri etiketleri ekleyin veya bu iş akışını daha büyük bir raporlama sistemine entegre edin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanıza ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Aspose.Cells for .NET Kullanarak Excel'i PowerPoint'e Dönüştürme: Tam Kılavuz](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}