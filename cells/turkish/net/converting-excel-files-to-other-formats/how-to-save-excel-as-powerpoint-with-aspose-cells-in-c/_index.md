---
category: general
date: 2026-11-16
description: Excel'i PowerPoint olarak kaydetmeyi ve Excel'i programlı bir şekilde
  PowerPoint'e dönüştürmeyi öğrenin. Bu adım adım kılavuz, Excel'i PPTX olarak dışa
  aktarmayı ve bir çalışma kitabını PPTX olarak kaydetmeyi de kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- export excel to pptx
- how to convert excel slide
- save workbook as pptx
language: tr
lastmod: 2026-11-16
og_description: Aspose.Cells kullanarak Excel'i PowerPoint olarak kaydedin. Bu kılavuzu
  izleyerek Excel'i PowerPoint'e dönüştürün, Excel'i PPTX olarak dışa aktarın ve çalışma
  kitabını dakikalar içinde PPTX olarak kaydedin.
og_image_alt: Screenshot showing the result of saving Excel as PowerPoint with editable
  shapes
og_title: Excel'i PowerPoint olarak kaydet – Tam C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to save Excel as PowerPoint and convert Excel to PowerPoint
    programmatically. This step‑by‑step guide also covers export Excel to PPTX and
    saving a workbook as PPTX.
  headline: How to save Excel as PowerPoint with Aspose.Cells in C#
  type: TechArticle
tags:
- Excel
- PowerPoint
- Aspose.Cells
- C#
- Export
title: C#'ta Aspose.Cells kullanarak Excel'i PowerPoint olarak kaydetme
url: /tr/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-with-aspose-cells-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i PowerPoint olarak kaydetme Aspose.Cells ile C#'ta

Programlı olarak **Excel'i PowerPoint olarak kaydetmeniz** gerekiyorsa, bu öğretici size eksiksiz, çalıştırmaya hazır bir çözüm sunar. Raporlama motoru ya da otomatik slayt oluşturucu geliştiriyor olsanız da, aşağıdaki adımlar bir Excel çalışma sayfasını sadece birkaç kod satırıyla düzenlenebilir bir PPTX slaytına dönüştürmenizi sağlar.

Nasıl **Excel'i PowerPoint'e dönüştüreceğinizi**, sayfayı bir PPTX dosyasına dışa aktaracağınızı ve metin kutuları ile şekilleri düzenlenebilir tutacağınızı öğreneceksiniz – tüm bunlar .NET ortamından çıkmadan.

## Önkoşullar

* .NET 6.0 veya üzeri (kod .NET Framework 4.7.2+ ile de çalışır)
* Geçerli bir Aspose.Cells lisansı (ücretsiz deneme değerlendirme amaçlı çalışır)
* Visual Studio 2022 (veya herhangi bir C# IDE)
* Dışa aktarmak istediğiniz veri ve şekilleri içeren bir Excel çalışma kitabı

## Adım 1: Aspose.Cells'i Yükleyin

Add the Aspose.Cells NuGet package to your project:

```bash
dotnet add package Aspose.Cells
```

> **Pro ipucu:** Belirli bir sürümü hedeflemek için `-v` bayrağını kullanın, ör. `Aspose.Cells.24.5`.

## Adım 2: Dışa aktarmak istediğiniz çalışma kitabını yükleyin

The first operation in the **save Excel as PowerPoint** workflow is loading the source workbook.

```csharp
using Aspose.Cells;
using System;

// Load the workbook that contains the shapes
Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");
```

*Neden önemli:* Çalışma kitabını yüklemek, çalışma sayfalarına, sayfa ayarına ve düzenlenebilir PowerPoint şekillerine dönüşecek çizim nesnelerine erişim sağlar.

## Adım 3: Düzenlenebilir bir PPTX slaytı için dışa aktarma seçeneklerini yapılandırın

To **convert Excel to PowerPoint** while preserving editability, you must set a few properties on `ImageOrPrintOptions`.

```csharp
// Prepare export options to generate an editable PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // Export format
    ExportEditableText = true,        // Keep text boxes editable
    ExportEditableShapes = true       // Keep shapes editable
};
```

*Açıklama:*  
* `SaveFormat = SaveFormat.Pptx` Aspose.Cells'e bir PowerPoint dosyası üretmesini söyler.  
* `ExportEditableText` ve `ExportEditableShapes` oluşturulan slaytın yerel bir PowerPoint slaytı gibi davranmasını sağlar—metin kutusuna ya da şekle tıklayıp doğrudan PowerPoint içinde düzenleyebilirsiniz.

## Adım 4: Dışa aktarma alanını tanımlayın ve tek bir slayta sığdırın

When you **export Excel to PPTX**, you usually want a specific range to appear on the slide. Setting the print area and fitting options guarantees a clean, single‑slide output.

```csharp
// Define the area of the first worksheet to export
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G30";

// Fit the exported content to a single slide
sheet.PageSetup.FitToPagesTall = 1;
sheet.PageSetup.FitToPagesWide = 1;
```

*Neden önemli:* `PrintArea`, dışa aktarmayı A1 ile G30 arasındaki hücrelerle sınırlar, `FitToPagesTall` ve `FitToPagesWide` ise her şeyi tek bir slayta sıkıştırarak istenmeyen ekstra sayfaların oluşmasını önler.

## Adım 5: Çalışma sayfasını düzenlenebilir bir PPTX dosyası olarak kaydedin

Now you can finally **save workbook as PPTX** and complete the **save Excel as PowerPoint** process.

```csharp
// Save the worksheet as an editable PPTX file
workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
Console.WriteLine("Export completed: EditableShapes.pptx");
```

Programı çalıştırdıktan sonra `EditableShapes.pptx` dosyasını Microsoft PowerPoint'te açın. Seçilen Excel aralığını yansıtan bir slayt göreceksiniz ve tüm metin kutuları ile şekiller tamamen düzenlenebilir olacaktır.

### Beklenen çıktı

* `C:\Output\` içinde `EditableShapes.pptx` adlı bir dosya.
* A1:G30 aralığını içeren bir PowerPoint slaytı.
* PowerPoint içinde çift tıklayıp doğrudan düzenleyebileceğiniz metin kutuları, grafikler ve şekiller.

## Tam kaynak kodu (kopyalamaya hazır)

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Load the workbook that contains the shapes
            Workbook workbook = new Workbook(@"C:\Data\WithShapes.xlsx");

            // Step 2: Prepare export options to generate an editable PPTX slide
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportEditableText = true,   // keep text boxes editable
                ExportEditableShapes = true  // keep shapes editable
            };

            // Step 3: Define the area of the first worksheet to export
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";

            // Step 4: Fit the exported content to a single slide
            sheet.PageSetup.FitToPagesTall = 1;
            sheet.PageSetup.FitToPagesWide = 1;

            // Step 5: Save the worksheet as an editable PPTX file
            workbook.Save(@"C:\Output\EditableShapes.pptx", exportOptions);
            Console.WriteLine("Export completed: EditableShapes.pptx");
        }
    }
}
```

## Yaygın sorular ve uç‑durum yönetimi

| Question | Answer |
|----------|--------|
| **Birden fazla çalışma sayfam olsaydı ne olur?** | `workbook.Worksheets` üzerinde döngü yapın ve her sayfa için adım 3‑5'i tekrarlayın, çıktı dosya adını değiştirerek (ör. `Sheet1.pptx`, `Sheet2.pptx`). |
| **Tüm çalışma kitabını tek bir PowerPoint sunumuna dışa aktarabilir miyim?** | Evet. `ImageOrPrintOptions` üzerinde `ExportAllSheets = true` ayarlayın. Her çalışma sayfası ayrı bir slayt olur. |
| **Şekillerim resim olarak görünüyor, düzenlenebilir nesne değil.** | `ExportEditableShapes = true` olduğundan ve Aspose.Cells 24.5+ (daha eski sürümler bu özelliği desteklemez) kullandığınızdan emin olun. |
| **Oluşturulan PPTX çok büyük.** | Yazdırma alanını küçültün veya `exportOptions.ImageResolution` ile görüntü çözünürlüğünü düşürün. |
| **Üretim ortamında lisansa ihtiyacım var mı?** | Ücretli bir lisans değerlendirme filigranını kaldırır ve tam performansı açar. Ücretsiz deneme test amaçlı çalışır. |

## Sağlam üretim kodu için ipuçları

* **Dosya yollarını doğrulayın** `Workbook` veya `Save` çağırmadan önce `FileNotFoundException` oluşmasını önlemek için.  
* **Dışa aktarmayı bir try/catch bloğuna sarın** lisans hatalarını (`Aspose.Cells.LicenseException`) yakalamak için.  
* **Çalışma kitabını serbest bırakın** (`workbook.Dispose()`) işiniz bittiğinde yönetilmeyen kaynakları serbest bırakmak için.  
* **Async I/O kullanın** (`FileStream` ile `await`) çok sayıda büyük sayfayı bir web hizmetinde dışa aktarırken.  

## Sonraki adımlar

Artık **Excel'i PowerPoint olarak kaydetmeyi** bildiğinize göre ilgili konuları keşfedebilirsiniz:

* **Özel slayt düzenleriyle Excel'i PPTX'e dışa aktar** – `SlideSize` ayarlayın ve bir ana slayt ekleyin.  
* **Excel slaytını PDF'e dönüştür** – yazdırılabilir bir sürüm için `SaveFormat.Pdf` kullanın.  
* **Çalışma kitabı klasörünü toplu olarak dönüştür** – yukarıdaki döngüyü `Directory.GetFiles` ile birleştirin.

Farklı yazdırma alanları, ölçekleme seçenekleri ve PowerPoint temalarıyla deney yaparak çıktıyı kuruluşunuzun marka kimliğine göre özelleştirin.

---

*Kodlamanız keyifli olsun! Bu kılavuz **Excel'i PowerPoint'e dönüştürmenize** yardımcı olduysa, ekip arkadaşlarınızla paylaşın ya da daha fazla yardım için Aspose.Cells GitHub deposunda bir issue açın.*

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [C# ve Aspose.Cells kullanarak Excel'i PowerPoint olarak kaydetme](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/)
- [Excel'den PPTX Kaydetme – Excel Sayfasını PowerPoint'e Dışa Aktarma Tam Kılavuzu](/cells/english/java/integration-interoperability/how-to-save-pptx-from-excel-complete-guide-to-export-excel-s/)
- [Excel'i PowerPoint'e Dönüştür – Tam Adım Adım Kılavuz](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-full-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}