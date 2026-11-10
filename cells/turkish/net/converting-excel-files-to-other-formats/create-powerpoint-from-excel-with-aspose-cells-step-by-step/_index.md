---
category: general
date: 2026-10-01
description: Aspose.Cells kullanarak C# ile Excel'den PowerPoint oluşturun. Excel'i
  PowerPoint'e dışa aktarın ve XLSX'i PPTX'e hızlıca tam bir kod örneğiyle dönüştürün.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create PowerPoint from Excel
- export Excel to PowerPoint
- convert Excel to PPTX
- convert XLSX to PPTX
- generate PowerPoint from Excel
language: tr
lastmod: 2026-10-01
og_description: C#'ta Aspose.Cells kullanarak Excel'den PowerPoint oluşturun. Excel'i
  PowerPoint'e dışa aktarmayı ve XLSX'i PPTX'e birkaç satır kodla dönüştürmeyi öğrenin.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel using Aspose.Cells
og_title: Aspose.Cells ile Excel'den PowerPoint Oluşturma – hızlı rehber
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Create PowerPoint from Excel using Aspose.Cells in C#. Export Excel
    to PowerPoint and convert XLSX to PPTX quickly with a complete code example.
  headline: Create PowerPoint from Excel with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Office automation
title: Aspose.Cells ile Excel'den PowerPoint Oluşturma – adım adım rehber
url: /tr/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Excel'den PowerPoint Oluşturma – adım adım kılavuz

Eğer **Excel'den PowerPoint oluşturmanız** gerekiyorsa, bu öğretici Aspose.Cells for .NET ile bunu nasıl yapacağınızı gösterir. **Excel'i PowerPoint'e dışa aktarmayı**, bir XLSX çalışma kitabını PPTX sunumuna dönüştürmeyi ve sonuç slaytlarını C# projenizden çıkmadan özelleştirmeyi öğreneceksiniz.

Bu kılavuz, .NET 6 veya daha yeni bir sürümde kodu çalıştırmak için gereken her şeyi kapsar; proje kurulumu, gerekli NuGet paketleri ve tam, çalıştırılabilir bir örnek dahil. Sonunda, orijinal Excel grafiğini çalışma kitabında göründüğü gibi tam olarak içeren bir PowerPoint dosyanız olacak.

## Gereksinimler

| Önkoşul | Sebep |
|---|---|
| .NET 6 SDK or newer | C# konsol uygulaması için çalışma zamanını sağlar |
| Visual Studio 2022 (or any IDE) | Kolay proje oluşturma ve hata ayıklamayı sağlar |
| Aspose.Cells for .NET NuGet package | `Workbook` sınıfını ve dışa aktarma API'lerini sağlar |
| An Excel file (`.xlsx`) that contains at least one chart | PowerPoint slaytı için kaynak veri |

> **Pro tip:** Aspose.Cells Windows, Linux ve macOS'ta çalışır, bu yüzden aynı kodu Docker konteynerlerinde veya CI pipeline'larında çalıştırabilirsiniz.

## Adım 1: Yeni bir konsol projesi oluşturun ve Aspose.Cells ekleyin

Bir terminal (veya Visual Studio Package Manager Console) açın ve şu komutu çalıştırın:

```bash
dotnet new console -n ExcelToPptxDemo
cd ExcelToPptxDemo
dotnet add package Aspose.Cells
```

`dotnet add package` komutu, daha sonra kullanılacak `ExportPptx` metodunu içeren **Aspose.Cells**'in en son kararlı sürümünü indirir.

## Adım 2: Kaynak Excel çalışma kitabını ekleyin

Dönüştürmek istediğiniz Excel dosyasını proje klasörüne yerleştirin. Bu öğreticide `ChartOle.xlsx` dosyasını kullanıyoruz; bu dosya ilk çalışma sayfasında tek bir grafik içerir.

```
/ExcelToPptxDemo
│   Program.cs
│   ChartOle.xlsx   ← your source workbook
```

## Adım 3: **Excel'den PowerPoint oluşturacak** kodu yazın

`Program.cs` dosyasını açın ve içeriğini aşağıdaki kodla değiştirin. Örnek, **temel dışa aktarma** işlemini gösterir ve ayrıca eksik dosyalar ve desteklenmeyen grafik türleri gibi yaygın kenar durumlarını nasıl ele alacağınızı gösterir.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelToPptxDemo
{
    class Program
    {
        static void Main()
        {
            // Define input and output paths
            string inputPath = Path.Combine(AppContext.BaseDirectory, "ChartOle.xlsx");
            string outputPath = Path.Combine(AppContext.BaseDirectory, "Exported.pptx");

            // Verify that the source workbook exists
            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: The file '{inputPath}' was not found.");
                return;
            }

            try
            {
                // Load the Excel workbook that contains the chart
                var workbook = new Workbook(inputPath);

                // Export the first worksheet as a PowerPoint presentation
                // This call performs the **convert Excel to PPTX** operation.
                workbook.Worksheets[0].ExportPptx(outputPath);

                Console.WriteLine($"Success: PowerPoint file created at '{outputPath}'.");
            }
            catch (Exception ex)
            {
                // Catch any errors thrown by Aspose.Cells (e.g., unsupported chart)
                Console.WriteLine($"Export failed: {ex.Message}");
            }
        }
    }
}
```

### Bunun neden çalıştığı

* `Workbook`, gömülü grafikler, tablolar ve biçimlendirme dahil olmak üzere tüm Excel dosyasını okur.  
* `ExportPptx`, aktif çalışma sayfasını bir PPTX slayt destesi haline dönüştürür. Metot, Excel grafiklerini otomatik olarak PowerPoint şekillerine çevirir ve görsel sadakati korur.  
* Kod, işlemi bir `try/catch` bloğuna sarar ve bozuk dosyalardan kaynaklanan **XLSX'i PPTX'e dönüştür** hataları gibi hataları ortaya çıkarır.

## Adım 4: Programı çalıştırın ve çıktıyı doğrulayın

Uygulamayı çalıştırın:

```bash
dotnet run
```

Aşağıdaki konsol mesajını görmelisiniz:

```
Success: PowerPoint file created at '.../Exported.pptx'.
```

`Exported.pptx` dosyasını Microsoft PowerPoint'te veya herhangi bir uyumlu görüntüleyicide açın. İlk slayt, `ChartOle.xlsx` içinde göründüğü gibi grafiği tam olarak gösterir. Bu, **Excel'den PowerPoint başarıyla oluşturduğunuzu** doğrular.

## Adım 5: İleri Seviye – birden fazla çalışma sayfasını dışa aktarma veya özel slayt düzenleri

Temel örnek yalnızca ilk çalışma sayfasını dışa aktarır. Gerçek dünyada şunlara ihtiyaç duyabilirsiniz:

* **Birden fazla çalışma sayfasını** ayrı slaytlara dışa aktarın.  
* **Slayt boyutunu kontrol edin** veya bir başlık yer tutucu ekleyin.  
* **Gizli çalışma sayfalarını** dönüşüme dahil edin.  

Aşağıda, tüm çalışma sayfalarını döngüye alıp her birini ayrı bir slayt olarak ekleyen kısa bir kod parçacığı bulunmaktadır:

```csharp
// Export each worksheet as a separate slide
var pptxPath = Path.Combine(AppContext.BaseDirectory, "FullExport.pptx");
var presentation = new Presentation(); // Aspose.Slides.Presentation, if you have the Slides library

foreach (Worksheet ws in workbook.Worksheets)
{
    // Convert worksheet to an image first (optional for custom layout)
    var imgStream = new MemoryStream();
    ws.PageSetup.PrintArea = ws.Cells.MaxDisplayRange; // ensure full content
    ws.Pictures[0].ToImage(imgStream, ImageFormat.Png);

    // Add a new slide and insert the image
    var slide = presentation.Slides.AddEmptySlide(presentation.SlideSize.Size);
    slide.Shapes.AddPictureFrame(ShapeType.Rectangle, 0, 0, presentation.SlideSize.Size.Width, presentation.SlideSize.Size.Height, imgStream);
}

// Save the final presentation
presentation.Save(pptxPath, SaveFormat.Pptx);
```

> **Not:** İleri seviye kod parçası **Aspose.Slides for .NET** kütüphanesini gerektirir. Eğer sadece basit tek sayfa dönüşümüne ihtiyacınız varsa, önceki `ExportPptx` çağrısı yeterlidir.

## Yaygın tuzaklar ve nasıl önlenir

| Sorun | Neden | Çözüm |
|---|---|---|
| Export sonrası boş slayt | Çalışma sayfasında görünür nesne yok | `ExportPptx` çağrısı yapılmadan önce en az bir grafik, tablo veya şekil olduğundan emin olun. |
| PowerPoint'te eksik fontlar | PPTX'in açıldığı makinede font yüklü değil | Gerekli fontları Excel çalışma kitabına gömün veya hedef sisteme kurun. |
| Beklenmeyen ölçekleme | Büyük grafik slayt boyutlarını aşıyor | Dışa aktarmadan önce çalışma sayfasının `PageSetup.Zoom` özelliğini ayarlayın. |
| `convert XLSX to PPTX` `NotSupportedException` hatası veriyor | Aspose.Cells tarafından desteklenmeyen grafik türü (ör. 3‑D haritalar) | Grafiği desteklenen bir türle değiştirin veya sayfayı önce bir görüntü olarak dışa aktarın. |

Bu kenar durumlarını ele almak, üretim ortamlarında güvenilir bir **Excel'den PowerPoint dışa aktarma** iş akışı sağlar.

## Sonuç

Artık Aspose.Cells for .NET kullanarak **Excel'den PowerPoint oluşturmayı** biliyorsunuz. Öğreticide şunlar ele alındı:

* Proje kurulumu ve NuGet kurulumu  
* Bir Excel çalışma kitabını yükleme ve `ExportPptx` çağırma  
* Kodu çalıştırma ve oluşturulan PPTX'i doğrulama  
* Çözümü birden fazla çalışma sayfasını ve özel düzenleri işleyebilecek şekilde genişletme  
* Yaygın dönüşüm sorunlarından kaçınmak için pratik ipuçları  

Bu bilgiyle rapor oluşturmayı otomatikleştirebilir, sunum hatları kurabilir veya Excel‑to‑PowerPoint dönüşümünü herhangi bir C# uygulamasına entegre edebilirsiniz. Farklı grafik türleriyle deney yapın, slayt başlıkları ekleyin veya tam özellikli sunum oluşturma için dışa aktarmayı Aspose.Slides ile birleştirin.

--- 

*Daha fazlasını keşfetmeye hazır mısınız? **Excel'i PDF'e dönüştür**, **Excel verilerini Word'e göm**, veya **Aspose.Slides ile programlı olarak PPTX dosyalarını düzenle** gibi ilgili konulara göz atın.*

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Excel'i PowerPoint'e Dönüştür Aspose Cells .NET](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Excel'i PowerPoint'e Dönüştür Aspose Cells .NET](/cells/french/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Excel'i PowerPoint'e Dönüştür Aspose Cells .NET](/cells/spanish/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}