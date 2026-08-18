---
category: general
date: 2026-08-17
description: C# ile Excel'i PowerPoint olarak kaydedin – XLSX dosyalarını dönüştürmek,
  metin kutularını düzenlenebilir hâle getirmek ve PPTX çıktısı oluşturmak için adım
  adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as powerpoint
- convert excel to powerpoint
- how to convert xlsx
- make textbox editable
- how to edit textboxes
language: tr
lastmod: 2026-08-17
og_description: C# ile Excel'i PowerPoint olarak kaydedin, tam kod örneğiyle. XLSX'i
  nasıl dönüştüreceğinizi, metin kutularını düzenlenebilir hale getirmeyi ve PPTX'e
  dışa aktarmayı öğrenin.
og_image_alt: Screenshot showing Excel data saved as a PowerPoint slide
og_title: Excel'i C#'ta PowerPoint olarak Kaydet – Tam Dönüştürme Rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Save Excel as PowerPoint with C# – step‑by‑step guide to convert XLSX
    files, make textboxes editable, and generate PPTX output.
  headline: How to save Excel as PowerPoint using C# and Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel-to-PowerPoint
title: C# ve Aspose.Cells kullanarak Excel'i PowerPoint olarak kaydetme
url: /tr/net/converting-excel-files-to-other-formats/how-to-save-excel-as-powerpoint-using-c-and-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ve Aspose.Cells ile Excel’i PowerPoint Olarak Kaydetme

Bir .NET projesinde **Excel’i PowerPoint olarak kaydetmeniz** gerekiyorsa, bu kılavuz size tamamen çalışır bir çözüm sunar. XLSX çalışma kitabını nasıl yükleyeceğinizi, sayfadaki her metin kutusunu düzenlenebilir hale getireceğinizi ve sonucu bir PPTX dosyasına dışa aktaracağınızı sadece birkaç C# satırıyla göreceksiniz.

Excel’i PowerPoint’e dönüştürmek, raporlama panoları, slayt desteleri veya otomatik sunum oluşturma gibi senaryolar için yaygın bir gereksinimdir. Bu öğreticide ayrıca **metin kutularını programlı olarak nasıl düzenleyeceğinizi** de ele alıyoruz, böylece kaydetmeden önce slayt içeriğini özelleştirebilirsiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 (veya daha yeni) SDK  
* Visual Studio 2022 veya VS Code gibi bir geliştirme ortamı  
* Aspose.Cells for .NET lisansı (veya ücretsiz deneme anahtarı) – [Aspose web sitesinden](https://products.aspose.com/cells/net/) indirin  
* Dönüştürmek istediğiniz `input.xlsx` dosyası  

> **Pro ipucu:** Ücretsiz deneme sürümünü kullanırsanız, oluşturulan PPTX bir filigran içerir. Lisanslı bir sürüm bunu kaldırır.

## Adım 1: Aspose.Cells NuGet paketini yükleyin

Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.Cells
```

Bu, dönüşüm için gerekli `Workbook`, `Worksheet` ve `Shape` sınıflarını sağlayan `Aspose.Cells` derlemesini ekler.

## Adım 2: Bir konsol uygulaması iskeleti oluşturun

Yeni bir konsol projesi oluşturun (halihazırda bir projeniz yoksa):

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
```

Oluşturulan `Program.cs` dosyasını sonraki adımlarda gösterilen kodla değiştirin.

## Adım 3: Çalışma kitabını yükleyin ve ilk çalışma sayfasını seçin

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Load the workbook from a file – adjust the path to your environment
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];
```

**Neden önemli:**  
`Workbook`, Excel dosyasını belleğe okur, `Worksheet` ise sayfanın hücrelerine, grafiklerine ve şekillerine erişim sağlar. İlk çalışma sayfası genellikle sunmak istediğiniz varsayılan rapordur.

## Adım 4: Sayfadaki her metin kutusunu düzenlenebilir hâle getirin

```csharp
        // Iterate through all shapes on the worksheet
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            // Check if the shape is a textbox (ShapeType.TextBox)
            if (shapeItem.Type == ShapeType.TextBox)
            {
                // The IsEditable property was added in Aspose.Cells 25.11
                shapeItem.TextBox.IsEditable = true;
            }
        }
```

**Neden buna ihtiyacınız var:**  
Excel’den içe aktarılan metin kutuları PowerPoint’te varsayılan olarak salt okunurdur. `IsEditable = true` ayarı, siz ya da daha sonra PowerPoint kullanıcıları metni doğrudan slaytta değiştirebilmenizi sağlar.

## Adım 5: Çalışma kitabını PowerPoint sunumu olarak kaydedin

```csharp
        // Define the output path for the PPTX file
        string outputPath = @"YOUR_DIRECTORY\output.pptx";

        // Save the workbook as a PowerPoint presentation
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

**Arka planda neler oluyor:**  
`Workbook.Save`, `SaveFormat.Pptx` enum değerini algılar ve Excel sayfa düzenini—satırlar, sütunlar, grafikler ve artık düzenlenebilir metin kutuları dahil—PowerPoint slayt nesnelerine dönüştürür.

## Tam kaynak kodu (çalıştırılabilir)

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Load the workbook from a file
        string inputPath = @"YOUR_DIRECTORY\input.xlsx";
        Workbook workbook = new Workbook(inputPath);

        // Step 2: Get the first worksheet in the workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Make every textbox on the sheet editable (property added in version 25.11)
        foreach (Shape shapeItem in worksheet.Shapes)
        {
            if (shapeItem.Type == ShapeType.TextBox)
            {
                shapeItem.TextBox.IsEditable = true;
            }
        }

        // Step 4: Save the workbook as a PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\output.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Conversion complete. PPTX saved to: {outputPath}");
    }
}
```

### Beklenen çıktı

Programı (`dotnet run`) çalıştırdığınızda şu çıktıyı görmelisiniz:

```
Conversion complete. PPTX saved to: YOUR_DIRECTORY\output.pptx
```

`output.pptx` dosyasını Microsoft PowerPoint’te açtığınızda, orijinal Excel sayfasını yansıtan bir slayt görüntülenir. Tüm metin kutuları çift tıklanarak doğrudan düzenlenebilir.

## Yaygın sorular ve kenar durumları

| Soru | Cevap |
|------|-------|
| **İlk sayfa yerine belirli bir çalışma sayfasını dönüştürebilir miyim?** | Evet. `workbook.Worksheets[0]` yerine `workbook.Worksheets["SheetName"]` veya ihtiyacınız olan herhangi bir indeks kullanın. |
| **Çalışma kitabı birden fazla sayfa içeriyorsa ne yapmalıyım?** | Her çalışma sayfası için ayrı bir PPTX dosyası oluşturmak üzere `workbook.Save`’i birden çok kez çağırın, ya da Aspose.Slides’ten `Presentation` nesnelerini kullanarak tek bir sunumda birleştirin. |
| **Grafikler korunacak mı?** | Aspose.Cells, Excel grafiklerini otomatik olarak PowerPoint grafik nesnelerine dönüştürür. Ek bir kod gerekmez. |
| **Slayt boyutunu nasıl değiştiririm?** | `workbook.Save` işleminden sonra oluşturulan PPTX’i Aspose.Slides ile yükleyip `Presentation.SlideSize` özelliğini ayarlayabilirsiniz. |
| **Kaydetmeden önce metin kutusunun metnini değiştirmek istiyorum, nasıl yaparım?** | Döngü içinde `shapeItem.TextBox.Text`’e erişin, değiştirin ve ardından `IsEditable = true` ayarlayın. Örnek: `shapeItem.TextBox.Text = "Yeni başlık";` |

## Sorun giderme ipuçları

* **“ShapeType.TextBox” bulunamadı** – Aspose.Cells 25.11 veya daha yeni bir sürüm kullandığınızdan emin olun; eski sürümlerde `IsEditable` özelliği yoktur.  
* **Dosya bulunamadı hataları** – `YOUR_DIRECTORY`’nin mutlak bir yol olduğundan veya göreli yolun doğru konuma işaret ettiğinden emin olun.  
* **Lisans uygulanmadı** – Değerlendirme filigranlarını kaldırmak için çalışma kitabını yüklemeden önce `License license = new License(); license.SetLicense("Aspose.Total.NET.lic");` kodunu çalıştırın.

## Sonuç

Artık bir XLSX çalışma kitabını yükleyerek, sayfadaki her metin kutusunu düzenlenebilir hâle getirerek ve PPTX olarak dışa aktararak **Excel’i PowerPoint olarak kaydetmeyi** C# ile biliyorsunuz. Bu yöntem grafikler, resimler ve hücre biçimlendirmesini otomatik olarak işler ve size sunuma hazır bir slayt destesi sunar.

Sonraki adımda **Aspose.Slides ile Excel’i PowerPoint’e dönüştürme**, **dönüştürmeden sonra metin kutularını programlı olarak düzenleme** veya **birden çok çalışma kitabını toplu işleme** gibi konuları keşfedebilirsiniz. Bu konular, burada ele aldığımız temel adımları genişleterek raporlama iş akışınızı daha da otomatikleştirmenize yardımcı olur.

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak daha yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [How to Save Excel Files in Multiple Formats Using Aspose.Cells .NET (2023 Guide)](/cells/english/net/workbook-operations/aspose-cells-net-save-excel-formats/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}