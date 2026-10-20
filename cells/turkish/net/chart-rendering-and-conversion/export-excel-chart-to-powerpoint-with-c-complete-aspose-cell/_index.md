---
category: general
date: 2026-08-04
description: Aspose.Cells kullanarak C# ile Excel grafiğini PowerPoint'e aktarın.
  Bu adım adım Excel'den PowerPoint'e dönüşüm kılavuzunu izleyin ve şekilleri düzenlenebilir
  tutun.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel chart to powerpoint
- Aspose.Cells PPTX export
- editable shapes in PowerPoint
- Excel to PowerPoint conversion
- C# chart export
language: tr
lastmod: 2026-08-04
og_description: Aspose.Cells ile C#'ta Excel grafiğini PowerPoint'e aktarın. Düzenlenebilir
  bir PPTX nasıl oluşturulur, grafik verileri nasıl korunur ve Excel'den PowerPoint'e
  dönüşüm nasıl otomatikleştirilir öğrenin.
og_image_alt: Screenshot of an Excel chart rendered as an editable PowerPoint slide
og_title: C# ile Excel grafiğini PowerPoint'e aktar – tam Aspose.Cells öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  headline: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  type: TechArticle
- description: Export Excel chart to PowerPoint using Aspose.Cells in C#. Follow this
    step‑by‑step Excel to PowerPoint conversion guide and keep shapes editable.
  name: Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide
  steps:
  - name: Expected output
    text: '| File name | Content on slide | |--------------------------|------------------------------------------|
      | `ShapesExport.pptx` | The chart from `Shapes.xlsx` rendered as an editable
      PowerPoint chart, with axis labels, legends, and data series intact. |'
  - name: Exporting multiple worksheets
    text: If you need a slide for each worksheet, loop through `workbook.Worksheets`
      and call `Save` with a unique file name for each iteration.
  - name: Controlling slide layout
    text: Aspose.Slides lets you add a custom slide layout after the export. Create
      a new presentation, import the generated slide, and then apply a master theme.
  - name: Handling charts with external data sources
    text: If a chart references a data range outside the defined print area, extend
      the `PrintArea` to include those cells. Otherwise the chart may lose data series
      during export.
  - name: Licensing considerations
    text: 'Aspose libraries work in evaluation mode with a watermark. To remove the
      watermark, set the license before any API call:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- PowerPoint
title: C# ile Excel grafiğini PowerPoint'e aktar – kapsamlı Aspose.Cells rehberi
url: /tr/net/chart-rendering-and-conversion/export-excel-chart-to-powerpoint-with-c-complete-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel chart to PowerPoint with C# – complete Aspose.Cells guide

Eğer **export Excel chart to PowerPoint** ihtiyacınız varsa, bu öğretici Aspose.Cells ve Aspose.Slides kullanarak C# ile nasıl yapılacağını gösterir. Tamamen düzenlenebilir bir PPTX elde edeceksiniz; grafik verilerini ve şekillerini korur, böylece dönüşüm daha fazla tasarım çalışması için hazır olur.

Excel'den PowerPoint'e grafik dışa aktarmak, otomatik raporlama hatları, satış sunumları veya eğitim materyalleri oluştururken yaygın bir gereksinimdir. Bu rehberde, tüm grafik öğelerini düzenlenebilir tutan bir **Excel to PowerPoint conversion** işlemini adım adım öğreneceksiniz. Manuel kopyala‑yapıştır gerekmez ve kod .NET 6+ ile klasik .NET Framework'te de çalışır.

## Önkoşullar

- Geçerli bir Aspose.Cells lisansı (veya ücretsiz değerlendirme anahtarı)  
- Projeye eklenmiş Aspose.Slides for .NET (kütüphane PPTX çıktısını yönetir)  
- .NET 6 SDK veya daha yeni bir sürüm yüklü  
- En az bir grafik içeren bir Excel çalışma kitabı (bu örnek için `Shapes.xlsx` kullanıyoruz)  

NuGet paketlerini aşağıdaki komutlarla kurabilirsiniz:

```bash
dotnet add package Aspose.Cells
dotnet add package Aspose.Slides
```

## Adım 1: Excel çalışma kitabını yükleyin

İlk işlem, dışa aktarmak istediğiniz grafiği içeren çalışma kitabını açmaktır. `Workbook` sınıfı, tüm Excel dosyasını temsil eder.

```csharp
using Aspose.Cells;
using Aspose.Slides;   // required for PPTX output

// Load the Excel workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

**Neden bu önemli:** Çalışma kitabını yüklemek, sayfalarına, grafiklerine ve biçimlendirmesine erişmenizi sağlar. Aspose.Cells, dosyayı Microsoft Office yüklü olmadan okur; bu da çözümü hafif ve sunucu dostu tutar.

## Adım 2: Çalışma sayfasını seçin ve yazdırma alanını tanımlayın

Bir çalışma sayfası birçok grafik içerebilir, ancak genellikle belirli bir bölgeyi dışa aktarırsınız. `PrintArea` ayarlamak, Aspose.Cells'e hangi hücrelerin (grafikler dahil) işleneceğini söyler.

```csharp
// Choose the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Define the area that contains the chart and any supporting data
worksheet.PageSetup.PrintArea = "A1:G30";
```

**Neden bu önemli:** Dışa aktarmayı tanımlı bir yazdırma alanıyla sınırlayarak gereksiz boş slaytlardan kaçınılır ve PPTX dosya boyutu küçük tutulur. Alan, grafiğinizin tam aralığına göre ayarlanabilir.

## Adım 3: Düzenlenebilir bir PPTX için dışa aktarma seçeneklerini yapılandırın

Aspose.Cells, çıktı formatını ve düzenlenebilirliği kontrol etmek için `ImageOrPrintOptions` sınıfını kullanır. `ImageFormat`'i `ImageFormat.Pptx` olarak ayarlamak bir PowerPoint dosyası oluşturur, `ExportEditableShapes = true` ise grafik nesnelerini düzenlenebilir şekiller olarak korur.

```csharp
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Pptx,   // Target format
    ExportEditableShapes = true       // Keep shapes/textboxes editable
};

// Attach the options to the worksheet's print settings
worksheet.PageSetup.PrintOptions = exportOptions;
```

**Neden bu önemli:** `ExportEditableShapes` bayrağı, **editable shapes in PowerPoint** sonucunun anahtarıdır. Bu bayrak olmadan grafik bir görüntü olarak rasterleştirilir ve veri noktalarını ya da stilini daha sonra değiştirme imkanı kaybolur.

## Adım 4: Çalışma sayfasını PowerPoint sunumu olarak kaydedin

Son olarak, `Workbook` nesnesi üzerindeki `Save` metodunu çağırın. `SaveFormat.Pptx` enum'u Aspose.Cells'e bir PowerPoint dosyası üretmesini söyler.

```csharp
// Export the selected worksheet to a PPTX file
workbook.Save("YOUR_DIRECTORY/ShapesExport.pptx", SaveFormat.Pptx);
```

Kod tamamlandığında, `ShapesExport.pptx` dosyasını PowerPoint'te açın. Orijinal Excel grafiğini yerel bir PowerPoint grafik nesnesi olarak içeren bir slayt göreceksiniz. Verileri düzenlemek, renkleri değiştirmek veya animasyon eklemek için grafiğe çift tıklayın—tıpkı grafiği doğrudan PowerPoint'te oluşturmuş gibi.

### Beklenen çıktı

| Dosya adı                | Slayttaki içerik                         |
|--------------------------|------------------------------------------|
| `ShapesExport.pptx`      | `Shapes.xlsx` dosyasındaki grafik, düzenlenebilir bir PowerPoint grafik olarak işlenir; eksen etiketleri, lejandlar ve veri serileri korunur. |

## Tam, çalıştırılabilir örnek

Aşağıda, kopyalayıp yapıştırıp çalıştırabileceğiniz tam program yer alıyor. Gerekli tüm `using` ifadelerini, hata yönetimini ve yorumları içerir.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;   // Required for PPTX output

class ExcelToPowerPoint
{
    static void Main()
    {
        // Path to the source Excel file – adjust as needed
        const string excelPath = "YOUR_DIRECTORY/Shapes.xlsx";
        // Path for the generated PowerPoint file
        const string pptxPath = "YOUR_DIRECTORY/ShapesExport.pptx";

        try
        {
            // Load the workbook
            Workbook workbook = new Workbook(excelPath);

            // Use the first worksheet (you can change the index or name)
            Worksheet worksheet = workbook.Worksheets[0];

            // Define the area that contains the chart
            worksheet.PageSetup.PrintArea = "A1:G30";

            // Set export options for PPTX with editable shapes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Pptx,
                ExportEditableShapes = true
            };
            worksheet.PageSetup.PrintOptions = exportOptions;

            // Save as PPTX
            workbook.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine($"Export successful. PPTX saved to: {pptxPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during export: {ex.Message}");
        }
    }
}
```

**Her bloğun açıklaması**

| Blok | Amaç |
|------|------|
| `using` yönergeleri | Aspose.Cells ve Aspose.Slides ad alanlarını getirir. |
| `Workbook workbook = new Workbook(excelPath);` | Excel dosyasını Office yüklü olmadan yükler. |
| `worksheet.PageSetup.PrintArea = "A1:G30";` | Dışa aktarmayı grafiği içeren bölgeyle sınırlar. |
| `ImageOrPrintOptions` | PPTX çıktısını yapılandırır ve **Aspose.Cells PPTX export**'ı düzenlenebilir şekillerle etkinleştirir. |
| `workbook.Save(pptxPath, SaveFormat.Pptx);` | PowerPoint dosyasını diske yazar. |
| `try / catch` | Eksik dosyalar veya lisans sorunları için temel hata yönetimi sağlar. |

Bu programı çalıştırdığınızda, Microsoft PowerPoint, Google Slides (dönüştürme sonrası) veya herhangi bir uyumlu görüntüleyicide açabileceğiniz bir PowerPoint slaytı oluşturulur.

## Yaygın varyasyonlar ve uç durumlar

### Birden fazla çalışma sayfasını dışa aktarma

Her çalışma sayfası için bir slayt gerekiyorsa, `workbook.Worksheets` üzerinde döngü yapın ve her yineleme için benzersiz bir dosya adıyla `Save` metodunu çağırın.

```csharp
int index = 1;
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.PageSetup.PrintOptions = exportOptions;
    string fileName = $"Slide{index++}.pptx";
    workbook.Save(fileName, SaveFormat.Pptx);
}
```

### Slayt düzenini kontrol etme

Aspose.Slides, dışa aktarmadan sonra özel bir slayt düzeni eklemenize izin verir. Yeni bir sunum oluşturun, oluşturulan slaytı içe aktarın ve ardından bir ana tema uygulayın.

```csharp
using Aspose.Slides.Export;

// Load the PPTX created by Aspose.Cells
Presentation pres = new Presentation(pptxPath);

// Apply a built‑in layout (e.g., Title and Content)
pres.Slides[0].LayoutSlide = pres.LayoutSlides[(int)SlideLayoutType.TitleAndContent];

// Save the final presentation
pres.Save("FinalPresentation.pptx", SaveFormat.Pptx);
```

### Dış veri kaynaklı grafikleri işleme

Bir grafik, tanımlı yazdırma alanının dışındaki bir veri aralığını referans alıyorsa, `PrintArea`'yı bu hücreleri kapsayacak şekilde genişletin. Aksi takdirde grafik dışa aktarım sırasında veri serilerini kaybedebilir.

### Lisanslama hususları

Aspose kütüphaneleri, bir filigran ile değerlendirme modunda çalışır. Filigranı kaldırmak için herhangi bir API çağrısından önce lisansı ayarlayın:

```csharp
var license = new Aspose.Cells.License();
license.SetLicense("Aspose.Cells.lic");
```

Gelişmiş özelliklerini kullanıyorsanız Aspose.Slides için de aynı işlemi yapın.

## Profesyonel ipuçları

- **Export seçeneklerini yeniden kullanın:** Tek bir `ImageOrPrintOptions` örneği oluşturun ve kodun DRY kalması için her çalışma sayfasına atayın.  
- **Toplu işleme:** Büyük ölçekli raporlama için bu dışa aktarma mantığını bir arka plan çalışanı veya Azure Function ile birleştirerek isteğe bağlı PPTX dosyaları üretin.  
- **Performans:** Yalnızca grafik görüntüsüne (düzenlenebilir olmayan) ihtiyacınız varsa, `ExportEditableShapes = false` ayarlayın. Bu, bellek kullanımını azaltır ve dönüşümü hızlandırır.  
- **Test:** Oluşturulan PPTX'i hem Windows hem de macOS PowerPoint kurulumlarında doğrulayın; bazı render farklılıkları platformlar arasında değişebilir.

## Sonuç

Artık C# kullanarak **export Excel chart to PowerPoint** için tam, uçtan uca bir çözüme sahipsiniz. Öğreticide, çalışma kitabını yükleme, yazdırma alanını seçme, **Aspose.Cells PPTX export**'ı **editable shapes in PowerPoint** ile yapılandırma ve sonucu tamamen düzenlenebilir bir PPTX dosyası olarak kaydetme konuları ele alındı.

Buradan, toplu dışa aktarma, özel slayt düzenleri veya süreci bir web API'sine entegre etme gibi ek **Excel to PowerPoint conversion** senaryolarını keşfedebilirsiniz. Farklı grafik türleriyle deney yapın, görseller ekleyin veya birden fazla çalışma sayfasını tek bir sunumda birleştirerek çıktıyı iş ihtiyaçlarınıza göre özelleştirin.

Raporlama iş akışınızı otomatikleştirmeye hazır mısınız? Kaynak dosyayı değiştirin, yazdırma alanını ayarlayın ve kodu mevcut .NET hizmetlerinize entegre edin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells for .NET Kullanarak Excel'i PowerPoint'e Dönüştürme: Tam Bir Rehber](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells for .NET Kullanarak Excel Grafiklerini PDF'e Dışa Aktarma: Adım Adım Rehber](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [Aspose.Cells .NET Kullanarak Excel Hücrelerini Görsele Dışa Aktarma: Adım Adım Rehber](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}