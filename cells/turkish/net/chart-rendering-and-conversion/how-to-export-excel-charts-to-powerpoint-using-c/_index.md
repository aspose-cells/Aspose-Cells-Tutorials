---
category: general
date: 2026-10-26
description: C# ile Excel grafiklerini PowerPoint’e nasıl dışa aktaracağınızı öğrenin.
  Şekil düzenlenebilirliğini koruyun ve birkaç satır kodla PPTX olarak kaydedin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel charts to powerpoint
- Aspose.Cells export
- C# Excel to PowerPoint conversion
- preserve shape editability
- SaveFormat.Pptx
- Workbook.Save method
language: tr
lastmod: 2026-10-26
og_description: C# ile Excel grafiklerini PowerPoint'e aktarın. Bu kılavuz, şekilleri
  düzenlenebilir tutmayı ve Aspose.Cells kullanarak PPTX olarak kaydetmeyi gösterir.
og_image_alt: Export Excel charts to PowerPoint example showing a chart transferred
  from Excel to a slide
og_title: C# ile Excel grafiklerini PowerPoint'e aktar – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  headline: How to export Excel charts to PowerPoint using C#
  type: TechArticle
- description: Learn how to export Excel charts to PowerPoint with C#. Preserve shape
    editability and save as PPTX in a few lines of code.
  name: How to export Excel charts to PowerPoint using C#
  steps:
  - name: Load the Excel workbook
    text: '```csharp using Aspose.Cells;'
  - name: (Optional) Adjust workbook settings
    text: In most cases the default settings are sufficient for a clean export. However,
      if you need to change the calculation mode, page setup, or hide certain sheets,
      you can do it here.
  - name: Save the workbook as a PowerPoint file
    text: '```csharp // Export the workbook to PPTX while keeping chart shapes editable
      workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx); ```'
  - name: Verify the result
    text: 'Open `Shapes.pptx` in PowerPoint and:'
  - name: 'Edge case: Exporting multiple worksheets with separate charts'
    text: If your Excel file contains several worksheets, each with its own chart,
      Aspose.Cells creates a separate slide for each chart automatically. You can
      control slide order by rearranging worksheets before the save operation.
  - name: 'Performance tip: Stream the output instead of writing to disk'
    text: When generating PowerPoint files in a web API, avoid temporary files by
      writing to a `MemoryStream`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- PowerPoint
title: C# kullanarak Excel grafiklerini PowerPoint'e nasıl aktarılır
url: /tr/net/chart-rendering-and-conversion/how-to-export-excel-charts-to-powerpoint-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel grafiklerini PowerPoint'e C# ile nasıl dışa aktarılır

Eğer **Excel grafiklerini PowerPoint'e dışa aktarmanız** gerekiyorsa, bu kılavuz size tamamen çalışır bir çözümü adım adım gösterir. Raporlama panosu oluşturuyor ya da slayt destelerini otomatikleştiriyor olun, birkaç satır C# kodu ile grafik şekillerinizin dönüşüm sonrası tamamen düzenlenebilir kalmasını sağlayacaksınız.

Bu öğreticide şunları öğreneceksiniz:

* Grafikler içeren mevcut bir Excel çalışma kitabını yükleme.  
* (İsteğe bağlı) Dönüştürmeden önce çalışma kitabı ayarlarını ayarlama.  
* Çalışma kitabını, şekil düzenlenebilirliğini koruyarak bir PowerPoint dosyası olarak kaydetme.  

Tüm bunlar **Aspose.Cells for .NET** ile yapılır; bu kütüphane, sunucuda Microsoft Office gerektirmeden Excel‑to‑PowerPoint dönüşümünü yönetir.

## Gereksinimler

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 veya üzeri | Modern çalışma zamanı ve tam dil özellikleri |
| Visual Studio 2022 (veya herhangi bir IDE) | Kullanışlı editör ve hata ayıklayıcı |
| **Aspose.Cells for .NET** NuGet paketi | `Workbook` sınıfını ve `SaveFormat.Pptx` desteğini sağlar |
| Grafik içeren bir Excel dosyası (`ChartAndShapes.xlsx`) | Dışa aktarmak istediğiniz grafiklerin kaynağı |

> **Pro tip:** Kodu test etmek için ücretsiz **Aspose.Cells Evaluation** sürümünü kullanın; bir lisans anahtarı değerlendirme filigranını kaldırır.

```bash
dotnet add package Aspose.Cells
```

## Excel grafiklerini PowerPoint'e dışa aktarma – tam iş akışı

Aşağıda, **şekil düzenlenebilirliğini koruyarak** dışa aktarmayı gerçekleştiren uçtan uca kod yer almaktadır. Her adım ayrıntılı olarak açıklanmıştır.

### Adım 1: Excel çalışma kitabını yükleyin

```csharp
using Aspose.Cells;

// Load the workbook that holds the charts you want to export
Workbook workbook = new Workbook(@"C:\Projects\ChartAndShapes.xlsx");
```

*`Workbook` sınıfı, tüm Excel dosyasını temsil eder. Dosyanın yüklenmesi, tüm çalışma sayfalarını, grafikleri ve şekilleri belleğe okur; bu da sonraki tüm işlemler için gereklidir.*

### Adım 2: (İsteğe bağlı) Çalışma kitabı ayarlarını düzenleyin

Çoğu durumda varsayılan ayarlar temiz bir dışa aktarım için yeterlidir. Ancak hesaplama modunu, sayfa düzenini değiştirmek ya da belirli sayfaları gizlemek istiyorsanız, bunu burada yapabilirsiniz.

```csharp
// Example: ensure all formulas are calculated before export
workbook.CalculateFormula();

// Example: hide a sheet that you don’t want in the PowerPoint
workbook.Worksheets["SecretData"].IsVisible = false;
```

> **Neden önemli:** Dönüştürmeden önce ayarları düzenlemek, oluşturulan slaytların tam olarak istediğiniz durumu yansıtmasını sağlar; özellikle formüller ya da gizli sayfalar grafik verilerini etkileyebildiğinde.

### Adım 3: Çalışma kitabını PowerPoint dosyası olarak kaydedin

```csharp
// Export the workbook to PPTX while keeping chart shapes editable
workbook.Save(@"C:\Projects\Shapes.pptx", SaveFormat.Pptx);
```

*`SaveFormat.Pptx` sabiti, Aspose.Cells’e bir PowerPoint sunumu yazmasını söyler. Kütüphane, her Excel grafiğini Microsoft PowerPoint’te tamamen düzenlenebilir bir şekle dönüştürür.*

### Adım 4: Sonucu doğrulayın

`Shapes.pptx` dosyasını PowerPoint’te açın ve:

1. Herhangi bir slayttaki grafiği seçin.  
2. Sağ‑tıklayın → **Edit Data**.  
3. Grafik veri tablosunun göründüğünden ve değerleri değiştirebildiğinizden emin olun.

Grafik **Edit Data** panelini açıyorsa, dönüşüm başarılı olmuş ve **şekil düzenlenebilirliği** korunmuş demektir.

![Excel grafiklerini PowerPoint'e dışa aktarma örneği](export-excel-charts-to-powerpoint.png){.img-fluid alt="Excel grafiklerini PowerPoint'e dışa aktarma örneği"}

## Yaygın tuzaklar ve nasıl önlenir

| Issue | Cause | Fix |
|-------|-------|-----|
| Grafikler statik görüntü olarak görünür | PPTX dışa aktarımını desteklemeyen eski bir Aspose.Cells sürümü kullanılıyor | Aspose.Cells 23.x veya daha yeni bir sürüme yükseltin |
| PowerPoint grafiğinde veri eksik | Dışa aktarmadan önce çalışma kitabı tam olarak hesaplanmamış | `workbook.CalculateFormula()` metodunu `Save` öncesinde çağırın |
| Şekiller düzenlenebilir değil | `SaveFormat.Xlsx` ile kaydediliyor, `SaveFormat.Pptx` yerine | `Workbook.Save` çağrısında `SaveFormat.Pptx` kullandığınızdan emin olun |
| Çalışma zamanı lisans istisnası | Kayıtlı lisans olmadan değerlendirme sürümü | Lisansınızı şu şekilde kaydedin: `License license = new License(); license.SetLicense("Aspose.Cells.lic");` |

### Kenar durumu: Birden fazla çalışma sayfası ve ayrı grafikler

Excel dosyanızda her bir çalışma sayfasında ayrı bir grafik varsa, Aspose.Cells her grafik için otomatik olarak ayrı bir slayt oluşturur. Kaydetme işleminden önce çalışma sayfalarını yeniden düzenleyerek slayt sırasını kontrol edebilirsiniz.

```csharp
// Move the worksheet that should appear first in the slide deck
workbook.Worksheets.MoveTo(2, 0); // move sheet index 2 to position 0
```

### Performans ipucu: Çıktıyı diske yazmak yerine akışa (stream) yönlendirin

Web API içinde PowerPoint dosyaları üretirken, geçici dosyalardan kaçınmak için bir `MemoryStream`’e yazın.

```csharp
using (MemoryStream pptStream = new MemoryStream())
{
    workbook.Save(pptStream, SaveFormat.Pptx);
    // Return the stream as a file download
    FileContentResult result = new FileContentResult(pptStream.ToArray(),
        "application/vnd.openxmlformats-officedocument.presentationml.presentation")
    {
        FileDownloadName = "Charts.pptx"
    };
    return result;
}
```

## Tam, çalıştırılabilir örnek

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1. Load the workbook containing charts
            string excelPath = @"C:\Projects\ChartAndShapes.xlsx";
            Workbook workbook = new Workbook(excelPath);

            // 2. (Optional) Ensure formulas are up‑to‑date
            workbook.CalculateFormula();

            // 3. Export to PowerPoint while preserving shape editability
            string pptxPath = @"C:\Projects\Shapes.pptx";
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export complete. PowerPoint saved to: {pptxPath}");
        }
    }
}
```

**Beklenen çıktı:** Konsol onay mesajını yazdırır ve `Shapes.pptx` PowerPoint’te açıldığında her Excel grafiği kendi slaytında görünür. Bir grafiği seçtiğinizde verileri düzenleyebildiğinizi göreceksiniz; bu da **şekil düzenlenebilirliğinin** korunduğunu kanıtlar.

## Özet ve sonraki adımlar

Artık **Excel grafiklerini PowerPoint'e C# ile dışa aktarırken** grafiklerin tamamen düzenlenebilir kalmasını biliyorsunuz. Çözümün kalbi, **Aspose.Cells export** özelliği olan `Workbook.Save` metodunun `SaveFormat.Pptx` parametresidir; bu, karmaşık Open XML işlemlerini soyutlar.

İleride şunları keşfedebilirsiniz:

* **Aspose.Slides** API’si ile özel slayt başlıkları veya notlar ekleme.  
* Grafiklerin yanında tablolar, resimler gibi diğer Excel nesnelerini dönüştürme.  
* Bir arka plan hizmetinde birden çok çalışma kitabını toplu işleme otomasyonu.

Yukarıda gösterilen isteğe bağlı ayarlarla deneyler yapın ve bu deseni raporlama hatlarınızda hızlı, güvenilir PowerPoint üretimi için entegre edin.


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve ilgili konuları ayrıntılı olarak ele alan tam çalışan kod örnekleri içerir. Her biri adım adım açıklamalarla API özelliklerini daha iyi kavramanızı ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenizi sağlar.

- [Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide](/cells/english/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/)
- [How to Export Excel to PowerPoint with C# – Complete Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-with-c-complete-guide/)
- [How to Export Shapes from Excel to PowerPoint – Complete Guide](/cells/english/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}