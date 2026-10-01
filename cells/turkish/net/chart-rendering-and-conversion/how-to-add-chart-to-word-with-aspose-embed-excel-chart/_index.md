---
category: general
date: 2026-10-01
description: Aspose ile sadece birkaç dakikada Word'e grafik ekleyin. Excel grafiğini
  Word'e gömmeyi, grafiği Excel'den Word'e aktarmayı, Aspose ile Word belgesi oluşturmayı
  ve grafiği Word belgesine kaydetmeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add chart to word
- embed excel chart word
- export chart excel word
- create word document aspose
- save chart word document
language: tr
lastmod: 2026-10-01
og_description: Aspose ile dakikalar içinde Word'e grafik ekleyin. Bu kılavuz, Excel
  grafiğini Word'e nasıl gömeceğinizi, grafiği Excel'den Word'e nasıl dışa aktaracağınızı,
  Aspose ile Word belgesi oluşturmayı ve grafiği Word belgesine kaydetmeyi gösterir.
og_image_alt: Screenshot illustrating how to add chart to Word using Aspose
og_title: Aspose ile Word’e Grafik Ekle – Excel Grafiği Göm
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  headline: How to add chart to Word with Aspose – embed Excel chart
  type: TechArticle
- description: Add chart to Word with Aspose in just minutes. Learn to embed Excel
    chart in Word, export chart Excel Word, create Word document Aspose, and save
    chart Word document.
  name: How to add chart to Word with Aspose – embed Excel chart
  steps:
  - name: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
    text: '**Loading the workbook** – `Workbook` parses the Excel file and gives you
      programmatic access to its worksheets and charts.'
  - name: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
    text: '**Creating the Word document** – `Document` is the Aspose.Words entry point
      for any Word‑processing task.'
  - name: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
    text: '**DocumentBuilder** – This helper class lets you insert content (text,
      images, charts) at the current cursor position.'
  - name: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
    text: '**InsertChart** – The overload that accepts an `Aspose.Cells.Chart` object
      copies the chart’s data, formatting, and series directly into the Word file.
      No intermediate image conversion is required, preserving vector quality.'
  - name: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
    text: '**Save** – `Save` writes the .docx package to disk, completing the **save
      chart word document** step.'
  type: HowTo
tags:
- Aspose
- C#
- Word automation
title: Aspose ile Word'e Grafik Ekleme – Excel Grafiğini Gömme
url: /tr/net/chart-rendering-and-conversion/how-to-add-chart-to-word-with-aspose-embed-excel-chart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Word'e Grafik Ekleme Aspose ile – Excel Grafiği Gömme

Eğer **Word'e grafik eklemeniz** gerekiyorsa, bu öğretici size tamamen çalışır bir çözüm sunar. Excel'den Word'e bir grafiği nasıl gömeceğinizi, grafiği Excel'den Word'e nasıl dışa aktaracağınızı ve sadece birkaç C# satırıyla **grafik Word belgesini kaydetme** işlemini göreceksiniz.

Grafik gömme, raporlar, faturalar veya panoları programlı olarak oluştururken sıkça ihtiyaç duyulan bir özelliktir. Bu rehberin sonunda, **Aspose ile Word belgesi oluşturma** konusunda, bir Excel çalışma kitabındaki herhangi bir grafiği manuel kopyala‑yapıştır yapmadan Word belgesine ekleyebileceksiniz.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ ile de çalışır)
- Aspose.Cells ve Aspose.Words NuGet paketleri (`dotnet add package Aspose.Cells` ve `dotnet add package Aspose.Words` komutlarıyla kurulur)
- En az bir grafik içeren mevcut bir Excel dosyası (`Chart.xlsx`)
- Visual Studio 2022 veya VS Code gibi bir geliştirme ortamı

## Aspose ile Word'e Grafik Ekleme

Aşağıda tam, bağımsız bir program örneği yer alıyor. Yeni bir konsol projesine kopyalayın, paketleri geri yükleyin ve çalıştırın. Program Excel çalışma kitabını yükler, bir Word belgesi oluşturur, ilk grafiği ekler ve sonucu kaydeder.

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

namespace AddChartToWordDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the Excel workbook that contains the chart
            var workbookPath = @"YOUR_DIRECTORY\Chart.xlsx";
            var workbook = new Workbook(workbookPath);

            // Step 2: Create a new Word document that will receive the chart
            var wordDoc = new Document();

            // Step 3: Initialise a DocumentBuilder for the Word document
            var builder = new DocumentBuilder(wordDoc);

            // Step 4: Insert the first chart from the first worksheet into the Word document
            // This uses Aspose.Words' InsertChart overload that accepts an Aspose.Cells chart object
            builder.InsertChart(workbook.Worksheets[0].Charts[0]);

            // Step 5: Save the resulting Word document
            var outputPath = @"YOUR_DIRECTORY\Chart.docx";
            wordDoc.Save(outputPath);

            Console.WriteLine($"Chart successfully added and saved to '{outputPath}'.");
        }
    }
}
```

### Her satırın önemi

1. **Çalışma kitabını yükleme** – `Workbook`, Excel dosyasını ayrıştırır ve çalışma sayfalarına ve grafiklere programatik erişim sağlar.  
2. **Word belgesi oluşturma** – `Document`, Aspose.Words'un herhangi bir Word‑işleme görevinde giriş noktasıdır.  
3. **DocumentBuilder** – Bu yardımcı sınıf, mevcut imleç konumunda içerik (metin, resim, grafik) eklemenizi sağlar.  
4. **InsertChart** – `Aspose.Cells.Chart` nesnesini kabul eden aşırı yükleme, grafiğin verilerini, biçimlendirmesini ve serilerini doğrudan Word dosyasına kopyalar. Ara bir görüntü dönüşümüne ihtiyaç duyulmaz, vektör kalitesi korunur.  
5. **Save** – `Save`, .docx paketini diske yazar ve **grafik Word belgesini kaydet** adımını tamamlar.

#### Beklenen çıktı

Programı çalıştırdıktan sonra `Chart.docx` dosyasını açın. `Chart.xlsx` içinde saklanan tam grafiği, builder'ın konumlandırıldığı yerde (belgenin başlangıcı) göreceksiniz. Grafik, Word içinde tamamen düzenlenebilir durumdadır (yeniden boyutlandırabilir, renkleri değiştirebilir veya veri kaynağını düzenleyebilirsiniz).

## Excel Grafiğini Word'e Gömme

Birden fazla grafik eklemeniz gerekiyorsa, her grafik nesnesi için `InsertChart` çağrısını tekrarlayın. Örneğin, ilk çalışma sayfasındaki tüm grafikleri gömmek için:

```csharp
var sheet = workbook.Worksheets[0];
foreach (Chart chart in sheet.Charts)
{
    builder.InsertChart(chart);
    builder.Writeln(); // add a line break between charts
}
```

**İpucu:** `builder.Writeln()` kullanarak bir paragraf sonu ekleyin; böylece her grafik yeni bir satırda başlar.

## Excel‑Word Grafik Dışa Aktarma – Birden Çok Çalışma Sayfası İşleme

Grafikler birden çok çalışma sayfasına yayılmışsa, çalışma kitabının `Worksheets` koleksiyonunda döngü oluşturun:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    foreach (Chart chart in ws.Charts)
    {
        builder.InsertChart(chart);
        builder.Writeln();
    }
}
```

Bu yaklaşım, herhangi bir çalışma kitabı düzeni için **grafik Excel Word dışa aktarma** sağlar ve karmaşık raporlar için çözümü dayanıklı kılar.

## Aspose ile Word Belgesi Oluşturma – Görünümü Özelleştirme

`InsertChart` tarafından döndürülen `Shape` nesnesini değiştirerek eklenen her grafiğin boyut ve konumunu kontrol edebilirsiniz:

```csharp
Shape chartShape = builder.InsertChart(chart);
chartShape.Width = 500;   // width in points
chartShape.Height = 300;  // height in points
chartShape.WrapType = WrapType.Inline; // make the chart flow with text
```

`WrapType` değerini `Inline` olarak ayarlamak, grafiğin normal bir paragraf gibi davranmasını sağlar; bu, otomatik belge üretiminde sıkça tercih edilir.

## Grafik Word Belgesini Kaydetme – En İyi Uygulamalar

- **Açıklayıcı bir dosya adı kullanın** (`Report_Q1_2026.docx`) böylece sürüm takibi kolaylaşır.  
- **Nesneleri serbest bırakın**; özellikle büyük toplu işlemlerde:

```csharp
wordDoc.Dispose();
workbook.Dispose();
```

- **Sonucu programatik olarak doğrulayın**; çok sayıda dosya üretirken:

```csharp
if (System.IO.File.Exists(outputPath))
{
    Console.WriteLine("File saved successfully.");
}
else
{
    Console.Error.WriteLine("Failed to save the document.");
}
```

## Yaygın sorular & uç durumlar

| Soru | Cevap |
|------|-------|
| *Sayfadaki ilk grafik olmayan bir grafiği ekleyebilir miyim?* | Evet. İndeksle erişin: `sheet.Charts[2]` üçüncü grafik için. |
| *Excel grafiği, çalışma kitabında bulunmayan bir veri kaynağı kullanıyorsa ne olur?* | Aspose.Cells, veriyi doğrudan grafik nesnesine gömer; kaynak aralık kaldırılsa bile grafik çalışmaya devam eder. |
| *Aspose için lisansa ihtiyacım var mı?* | Ücretsiz deneme sürümü çalışır, ancak lisanslı sürüm değerlendirme filigranını kaldırır ve tam özellikleri açar. |
| *Grafik, ekleme sonrası Word içinde düzenlenebilir mi?* | Grafik, yerel bir Word grafiği olarak eklenir; kullanıcılar serileri, başlıkları ve stilleri Word arayüzüyle düzenleyebilir. |
| *Grafiği yerel bir grafik yerine resim olarak eklemek istersem?* | `builder.InsertImage(chart.ToImage())` kullanarak raster bir görüntü gömebilirsiniz. Bu, Word‑düzeyinde düzenlenebilirlik gerekmiyorsa tam görsel eşleşme sağlar. |

## Tam çalışan örnek (kopyala‑yapıştır)

```csharp
using System;
using Aspose.Cells;
using Aspose.Words;
using Aspose.Words.Drawing;

class AddChartToWord
{
    static void Main()
    {
        // Load Excel workbook
        var wb = new Workbook(@"C:\Data\Chart.xlsx");

        // Create Word document
        var doc = new Document();
        var builder = new DocumentBuilder(doc);

        // Insert every chart from every worksheet
        foreach (Worksheet ws in wb.Worksheets)
        {
            foreach (Chart ch in ws.Charts)
            {
                Shape shape = builder.InsertChart(ch);
                shape.Width = 500;
                shape.Height = 300;
                builder.Writeln(); // separate charts
            }
        }

        // Save the document
        var outPath = @"C:\Data\ReportWithCharts.docx";
        doc.Save(outPath);
        Console.WriteLine($"Document saved to {outPath}");
    }
}
```

Kodu çalıştırdığınızda (`ReportWithCharts.docx`) kaynak çalışma kitabındaki her grafik için **Word'e grafik ekleme** sonuçlarını içeren bir Word dosyası oluşturulur.

## Sonuç

Artık **Aspose.Cells ve Aspose.Words** kullanarak **Word'e grafik ekleme**, **Excel grafiğini Word'e gömme**, **grafik Excel Word dışa aktarma**, **Aspose ile Word belgesi oluşturma** ve son olarak **grafik Word belgesini kaydetme** konularını biliyorsunuz. Bu yöntem tek‑grafik senaryoları için olduğu kadar, birden çok çalışma sayfasına yayılmış karmaşık çalışma kitapları için de uygundur.

İlerleyen adımlarda şunları keşfedebilirsiniz:

- `Chart` API'si aracılığıyla eklenen grafiklere özel stil (renk, yazı tipi) uygulama.  
- Metin üretimiyle grafiği birleştirerek tamamen otomatik raporlar oluşturma.  
- Gerektiğinde Aspose.Slides kullanma.

## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakın konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Save DOCX from Excel – Complete Guide to Export Charts to Word](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-docx-from-excel-complete-guide-to-export-charts/)
- [Create Excel Workbook with Pie Chart Using Aspose.Cells .NET - Comprehensive Guide](/cells/english/net/charts-graphs/create-excel-workbook-pie-chart-aspose-cells-net/)
- [Create a Bubble Chart in Excel Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/charts-graphs/create-bubble-chart-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}