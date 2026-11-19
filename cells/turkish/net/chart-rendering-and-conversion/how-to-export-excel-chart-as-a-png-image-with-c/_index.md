---
category: general
date: 2026-11-19
description: Aspose.Cells kullanarak Excel grafiğini PNG görüntüsü olarak nasıl dışa
  aktarılır. Excel grafik görüntüsünü kaydetmeyi ve görüntü formatını PNG olarak ayarlamayı
  sadece birkaç adımda öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel chart
- save excel chart image
- set image format png
- save excel picture file
language: tr
lastmod: 2026-11-19
og_description: Aspose.Cells ile Excel grafiğini PNG görüntüsü olarak nasıl dışa aktarılır.
  Excel grafik görüntüsünü kaydetmek ve görüntü formatını PNG olarak verimli bir şekilde
  ayarlamak için bu adım adım kılavuzu izleyin.
og_image_alt: How to export Excel chart as a PNG image
og_title: Excel grafiğini PNG görüntüsü olarak dışa aktarma – hızlı C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: How to export Excel chart as a PNG image using Aspose.Cells. Learn
    to save Excel chart image and set image format PNG in just a few steps.
  headline: How to export Excel chart as a PNG image with C#
  type: TechArticle
tags:
- Excel
- C#
- Aspose.Cells
- Chart export
title: C# ile Excel grafiğini PNG görüntüsü olarak dışa aktarma
url: /tr/net/chart-rendering-and-conversion/how-to-export-excel-chart-as-a-png-image-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel grafiğini C# ile PNG görüntüsü olarak dışa aktarma

Taşınabilir bir görüntüye **Excel grafiğini dışa aktarma** ihtiyacınız varsa, bu rehber eksiksiz, çalıştırmaya hazır bir çözüm sunar. Aspose.Cells kullanarak sadece üç satır kodla **Excel grafik görüntüsünü kaydet** PNG formatında, ayrıca öğreticide **image format png ayarla** ve **Excel resim dosyasını kaydet** nasıl yapılır da açıklanıyor.

Bu makaleyi, bir çalışma kitabını yükleyen, ilk grafiği işleyen ve bir `pivot.png` dosyasını diske yazan çalıştırılabilir bir programla tamamlayacaksınız. Ek bir araç gerekmez, manuel kopyala‑yapıştır yok—herhangi bir .NET projesine ekleyebileceğiniz temiz C# kodu.

## Önkoşullar

* .NET 6.0 SDK veya daha yeni bir sürüm (kod .NET Framework 4.6+ ile de çalışır)
* Visual Studio 2022 veya herhangi bir C# editörü
* Aspose.Cells for .NET lisansı (veya geçici bir değerlendirme anahtarı)
* İlk çalışma sayfasında en az bir grafik içeren bir Excel dosyası (`pivot.xlsx`)

Bu öğeler tek dış bağımlılıklardır; öğreticide makinede Office yüklü olmasına gerek yok.

## Adım 1: Aspose.Cells'i Yükleyin

Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.Cells
```

Paket, `Aspose.Cells` ad alanını ekler; bu ad alanı `Workbook`, `ImageOrPrintOptions` ve **Excel grafik görüntüsünü kaydet** için gereken diğer sınıfları sağlar.

## Adım 2: Minimal bir konsol programı oluşturun

Yeni bir konsol uygulaması oluşturun (`dotnet new console -n ExportChartDemo`) ve otomatik oluşturulan `Program.cs` dosyasını aşağıdaki kodla değiştirin. Program **Excel grafiğini dışa aktarma** nasıl yapılır gösterir ve her kararı açıklayan yorumlar içerir.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for ImageOrPrintOptions
using System.Drawing.Imaging;  // Provides ImageFormat enum

namespace ExportChartDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook that contains the pivot chart
            // -----------------------------------------------------------------
            // Replace the path with the actual location of your Excel file.
            string workbookPath = @"YOUR_DIRECTORY\pivot.xlsx";
            Workbook workbook = new Workbook(workbookPath);

            // -----------------------------------------------------------------
            // 2️⃣ Set up image export options (PNG format)
            // -----------------------------------------------------------------
            // This is where we **set image format png** for the exported picture.
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                // Optional: control the resolution (DPI) of the output image.
                // Higher DPI yields larger files but sharper charts.
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 3️⃣ Render the first picture (the chart) on the first worksheet
            // -----------------------------------------------------------------
            // Aspose.Cells stores charts as Picture objects inside the worksheet.
            // The index [0] refers to the first chart; adjust if you have multiple.
            Worksheet sheet = workbook.Worksheets[0];
            if (sheet.Pictures.Count == 0)
            {
                Console.WriteLine("No pictures found on the first worksheet.");
                return;
            }

            // Render the picture to a PNG file.
            string outputPath = @"YOUR_DIRECTORY\pivot.png";
            sheet.Pictures[0].RenderToImage(imageOptions, outputPath);

            Console.WriteLine($"Chart exported successfully to: {outputPath}");
        }
    }
}
```

### Her bölümün önemi

* **Loading the workbook** – `Workbook`, Microsoft Excel yüklü olmadan `.xlsx` dosyasını ayrıştırır.
* **ImageOrPrintOptions** – Bu nesne çıktı formatını kontrol eder. `ImageFormat = ImageFormat.Png` ayarını yaparak **image format png ayarla**, bu kayıpsız ve geniş çapta desteklenir.
* **RenderToImage** – `RenderToImage` yöntemi grafiği (`Picture` nesnesi) bir görüntü dosyasına dönüştürür. Yöntem aynı zamanda ölçekleme, DPI ve şeffaflığı otomatik olarak yönetir.
* **Error handling** – `sheet.Pictures.Count == 0` kontrolü, çalışma sayfasında grafik yoksa bir çalışma zamanı hatasını önler; bu, kullanıcıların yanlış sayfayı seçtiği yaygın bir durumdur.

## Adım 3: Programı çalıştırın ve sonucu doğrulayın

1. Projeyi derleyin: `dotnet build`.
2. Çalıştırın: `dotnet run --project ExportChartDemo`.

Her şey doğru yapılandırıldıysa, şunu göreceksiniz:

```
Chart exported successfully to: YOUR_DIRECTORY\pivot.png
```

`pivot.png` dosyasını herhangi bir görüntüleyicide açın. Excel grafiğinin tam görsel temsilini görmelisiniz; bu, **Excel resim dosyasını kaydet** başarıyla yaptığınızı doğrular.

### Beklenen çıktı

Aşağıda, dışa aktarılan PNG'nin nasıl görünebileceğine dair bir örnek (gerçek grafik, kaynak dosyanıza bağlıdır) yer almaktadır.

![Exported Excel chart saved as PNG image](images/exported-chart.png){: .center alt="Excel grafiğini PNG görüntüsü olarak kaydetme"}

## Adım 4: Gelişmiş seçenekler – birden fazla grafiği dışa aktarma

Çalışma kitabınız birden fazla grafik içeriyorsa, `Pictures` koleksiyonunda döngü oluşturabilirsiniz:

```csharp
for (int i = 0; i < sheet.Pictures.Count; i++)
{
    string chartPath = $@"YOUR_DIRECTORY\chart_{i + 1}.png";
    sheet.Pictures[i].RenderToImage(imageOptions, chartPath);
    Console.WriteLine($"Chart {i + 1} saved to {chartPath}");
}
```

Bu desen, sayfadaki her grafik için **Excel grafik görüntüsünü kaydet** sağlar; raporlama hatları için kullanışlıdır.

## Yaygın tuzaklar ve nasıl önlenir

| Semptom | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| `ArgumentOutOfRangeException` on `Pictures[0]` | Çalışma sayfasında grafik yok veya grafik farklı bir sayfada. | Sayfa indeksini (`Worksheets[0]`) doğrulayın ve grafiğin var olduğundan emin olun. Gerekirse `Worksheets["SheetName"]` kullanın. |
| Exported image is blurry | DPI çok düşük ayarlandı (varsayılan 96). | `ImageOrPrintOptions` içinde `HorizontalResolution` ve `VerticalResolution` değerlerini artırın. |
| PNG file is empty or corrupted | Lisans eksikliği nedeniyle değerlendirme kısıtlamaları. | Çalışma kitabını yüklemeden önce geçerli bir Aspose.Cells lisansı uygulayın (`License license = new License(); license.SetLicense("Aspose.Total.lic");`). |
| File path errors (`FileNotFoundException`) | `YOUR_DIRECTORY` yer tutucusu hatalı. | Mutlak yollar kullanın veya `Path.Combine(Environment.CurrentDirectory, "pivot.xlsx")` kullanın. |

Bu sorunları çözmek, sorunsuz bir **excel resim dosyasını kaydet** deneyimi sağlar.

## Pro ipucu: Görüntüyü doğrudan bellek akışına dışa aktar

Bazen görüntüyü diske yazmak yerine bellekte (ör. bir web API'sine yüklemek için) tutmanız gerekir:

```csharp
using (var ms = new MemoryStream())
{
    sheet.Pictures[0].RenderToImage(imageOptions, ms);
    // ms now contains the PNG bytes – you can send them over HTTP, store in DB, etc.
}
```

Aynı **image format png ayarla** mantığı geçerlidir; sadece dosya yolunu bir akışla değiştirirsiniz.

## Sonuç

Artık Aspose.Cells for .NET kullanarak Excel grafiğini PNG dosyası olarak **Excel grafiğini dışa aktarma** nasıl yapılacağını biliyorsunuz. Öğreticide şunlar ele alındı:

* Kütüphaneyi kurma
* Bir çalışma kitabı yükleme
* **image format png ayarla**
* **Excel grafik görüntüsünü kaydet** to disk
* Birden fazla grafiği işleme ve yaygın hataları ele alma

Bu temelle, grafik dışa aktarmayı otomatik raporlama, web servisleri veya masaüstü yardımcı programlarına entegre edebilirsiniz. Sonraki adımda, **excel resim dosyasını kaydet** gibi ilgili konuları JPEG (`ImageFormat.Jpeg`) olarak keşfedebilir veya grafiklerin PDF'ye dönüştürülmesini inceleyebilirsiniz.

Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalar içeren tam çalışan kod örnekleri sunar; böylece ek API özelliklerini öğrenebilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Aspose.Cells .NET Kullanarak Excel Pasta Grafiğini Görüntüye Dönüştürme: Adım Adım Kılavuz](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)
- [Grafiği PNG Olarak Dışa Aktar – Aspose.Cells ile Excel'i HTML'ye Dönüştürme Tam Kılavuzu](/cells/english/net/chart-rendering-and-conversion/export-chart-as-png-complete-guide-to-convert-excel-to-html/)
- [Aspose.Cells .NET Kullanarak Excel Hücrelerini Görüntüye Dışa Aktarma: Adım Adım Kılavuz](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}