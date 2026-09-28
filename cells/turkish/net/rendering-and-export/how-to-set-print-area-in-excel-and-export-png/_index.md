---
category: general
date: 2026-09-27
description: Excel'de yazdırma alanını ayarlayın ve seçili hücrelerin PNG görüntülerini
  nasıl dışa aktaracağınızı öğrenin. Bu kılavuz ayrıca aralığı görüntü olarak kaydetmeyi
  ve çalışma sayfasına resim eklemeyi kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: tr
lastmod: 2026-09-27
og_description: Excel'de yazdırma alanını ayarlayın ve Aspose.Cells ile PNG olarak
  dışa aktarın. Aralığı görüntü olarak kaydetmek ve çalışma sayfasına resim eklemek
  için bu adım adım rehberi izleyin.
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Excel'de yazdırma alanını ayarla – C#'ta PNG dışa aktar
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Excel'de yazdırma alanını nasıl ayarlayıp PNG olarak dışa aktarılır?
url: /tr/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Yazdırma Alanını Nasıl Ayarlarsınız ve PNG Olarak Dışa Aktarırsınız

Bir görüntü oluşturmadan önce **set print area excel** yapmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Ayrıca belirli bir aralıktan **how to export png** dosyalarını, **save range as image** ve **add picture to worksheet** tek bir tekrarlanabilir iş akışında nasıl yapacağınızı öğreneceksiniz.

Programatik olarak Excel ile çalışmak, genellikle hücrelerin yalnızca bir alt kümesini—örneğin bir pivot tablo veya bir grafik—görüntüye dönüştürmek istediğiniz anlamına gelir. Önce bir yazdırma alanı tanımlayarak, dışa aktarılan PNG'nin tam olarak beklediğiniz hücreleri içerdiğinden, daha fazla ve daha az olmadığından emin olursunuz. Bu öğretici, çalışma kitabını yüklemekten son PNG dosyasını kaydetmeye kadar her adımı size gösterir ve her ayarın neden önemli olduğunu açıklar.

## Önkoşullar

Başlamadan önce aşağıdakilerin yüklü olduğundan emin olun:

* .NET 6.0 veya daha yeni bir sürüm yüklü  
* Visual Studio 2022 (veya herhangi bir C# IDE)  
* **Aspose.Cells for .NET** NuGet paketi (`Install-Package Aspose.Cells`)  
* Bilinen bir dizinde bulunan bir Excel dosyası (`input.xlsx`)  

Bu gereksinimler, kodun ek yapılandırma olmadan çalışmasını sağlar.

## Adım 1: Çalışmak istediğiniz çalışma kitabını yükleyin

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

`Workbook` sınıfı, tüm Excel dosyasını temsil eder. İlk olarak onu yüklemek, çalışma sayfalarına, hücrelere ve sayfa‑ayarları seçeneklerine erişim sağlar.

## Adım 2: Hedef aralık için **Set print area excel**

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

**Print area**'yı ayarlamak, Excel'e (ve Aspose.Cells'e) hangi hücrelerin yazdırılabilir sayfaya ait olduğunu söyler. Daha sonra sayfayı bir görüntü olarak dışa aktardığınızda, yalnızca bu alan işlenir; bu, temiz bir **export selected cells image** için esastır.

## Adım 3: Görüntü dışa aktarma seçeneklerini yapılandırın – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` çıktının formatını kontrol eder. `ImageFormat.Png` seçerek, web ve masaüstü ortamlarında iyi çalışan yüksek çözünürlüklü, şeffaf arka planlı bir görüntü garantilersiniz.

## Adım 4: Tanımlı aralıktan bir resim oluşturun ve **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

`Pictures.Add` yöntemi, çalışma sayfasına yeni bir resim ekler. Adım 2'de oluşturulan aralığı geçirerek, **save range as image** işlemini doğrudan sayfaya koyarsınız; bu, daha sonra resmi çalışma kitabının diğer bölümlerinde referans göstermeniz gerektiğinde faydalıdır.

## Adım 5: **Save the picture as an image file** – **export selected cells image** iş akışını tamamlayarak

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

`Save` çağrısı, resmi Adım 3'te tanımlanan seçenekleri kullanarak dosya sistemine yazar. Ortaya çıkan `selected_range.png`, **set print area excel** komutuyla tanımlanan hücreleri tam olarak içerir.

## Tam, çalıştırılabilir örnek

Tüm parçaları bir araya getirdiğinizde, herhangi bir konsol uygulamasına bırakabileceğiniz kompakt bir program elde edersiniz:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### Beklenen çıktı

Programı çalıştırdığınızda şunu görürsünüz:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

Ve `selected_range.png` dosyasının, `input.xlsx` dosyasındaki yalnızca A1‑G20 hücrelerini gösterdiğini göreceksiniz.

## Yaygın tuzaklar ve nasıl kaçınılır

| Sorun | Neden olur | Çözüm |
|-------|------------|------|
| Dışa aktarılan görüntü tüm sayfayı içeriyor | Yazdırma alanı tanımlanmadı | Resmi oluşturmadan önce **set print area excel** yaptığınızdan emin olun |
| PNG bulanık | Varsayılan DPI düşük | `imageOptions.DpiX` ve `imageOptions.DpiY` değerlerini daha yüksek bir değere (ör. 300) ayarlayın |
| Dosya bulunamadı hatası | Yanlış dizin yolu | `Path.Combine` kullanın veya klasörün varlığını iki kez kontrol edin |
| Resim kaymış görünüyor | Yanlış satır/sütun indeksleri | `Pictures.Add` metodunun ilk iki parametresi, resmin yerleştirildiği sol‑üst hücredir; temiz bir dışa aktarma için bunları `0,0` olarak tutun |

## Pro ipucu: Tek çalıştırmada birden fazla aralığı dışa aktar

Birden fazla alan için **export selected cells image** yapmanız gerekiyorsa, Adım 2‑5'i bir döngü içinde tekrarlayın ve her yinelemede `printArea`'yı değiştirin. Her resme benzersiz bir dosya adı verin; aksi takdirde sonraki kaydetme önceki dosyanın üzerine yazar.

## Sonuç

Artık **set print area excel**, **how to export png** yapılandırma, **save range as image** ve **add picture to worksheet** işlemlerini Aspose.Cells kullanarak nasıl yapacağınızı biliyorsunuz. Bu uçtan uca çözüm, herhangi bir hücre bloğunu sadece birkaç C# satırıyla yüksek kaliteli bir PNG'ye dönüştürmenizi sağlar.

Sonraki adımda şunları keşfedebilirsiniz:

* Dışa aktarılan PNG'ye kenarlıklar veya filigranlar eklemek (*add picture to worksheet* stil ile arama yapın)  
* Baskı raporları için doğrudan PDF'ye dışa aktarmak (*export selected cells image* → PDF iş akışı)  
* Toplu işte birden fazla çalışma kitabı için süreci otomatikleştirmek  

Farklı aralıklar, DPI ayarları veya görüntü formatlarıyla denemeler yapmaktan çekinmeyin; projenizin ihtiyaçlarına uygun hale getirin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Excel'de Yazdırma Alanını Ayarlayın ve PowerPoint'e Dışa Aktarın – Adım Adım Kılavuz](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Aspose.Cells Java ile Excel Yazdırma Alanını HTML'e Dışa Aktarın](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Aspose.Cells for .NET Kullanarak Excel'de Yazdırma Alanı Nasıl Ayarlanır](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}