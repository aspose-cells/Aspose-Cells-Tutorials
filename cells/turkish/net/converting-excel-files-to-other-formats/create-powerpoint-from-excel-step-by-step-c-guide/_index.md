---
category: general
date: 2026-03-30
description: Aspose.Cells ve Aspose.Slides kullanarak Excel'den hızlıca PowerPoint
  oluşturun. Çalışma sayfasını görüntü olarak dışa aktarmayı ve sunumu C#'ta PPTX
  olarak kaydetmeyi öğrenin.
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: tr
og_description: Aspose ile C#'ta Excel'den PowerPoint oluşturun. Çalışma sayfasını
  resim olarak dışa aktarın, şekilleri düzenlenebilir tutun ve sonucu PPTX olarak
  kaydedin.
og_title: Excel'den PowerPoint Oluşturma – Tam C# Öğreticisi
tags:
- Aspose
- C#
- Office Automation
title: Excel'den PowerPoint Oluşturma – Adım Adım C# Rehberi
url: /tr/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'den PowerPoint Oluşturma – Tam C# Öğreticisi

Hiç **Excel'den PowerPoint oluşturma** ihtiyacı duydunuz mu ama grafikleri düzenlenebilir tutacak bir kütüphane bulamadınız mı? Yalnız değilsiniz. Birçok raporlama senaryosunda bir elektronik tabloyu slayt destesine dönüştürmek isteyeceksiniz, ancak metin kutularını sonradan düzenleme yeteneğini kaybetmek istemezsiniz. Bu rehber, **Excel'i PowerPoint'e dönüştürmeyi** Aspose.Cells ve Aspose.Slides kullanarak tam olarak nasıl yapacağınızı gösterirken, **çalışma sayfasını resim olarak dışa aktarma** ve sonunda **sunumu PPTX olarak kaydetme** konularını da kapsar.

Her satır kodu adım adım inceleyecek, *neden* her ayarın önemli olduğunu açıklayacak ve çalışma kitabınızda karmaşık grafikler varsa bunları resim olarak dışa aktarmak için ne yapmanız gerektiğini tartışacağız. Sonunda `ShapesDemo.xlsx` dosyasını alıp `Result.pptx` dosyasını üreten, çalıştırılmaya hazır bir C# konsol uygulamanız olacak – tüm metin kutuları düzenlenebilir ve net görüntülerle.

## Gereksinimler

- .NET 6.0 veya üzeri (API .NET Framework ile de çalışır, ancak .NET 6 en uygun sürümdür).  
- **Aspose.Cells** ve **Aspose.Slides** NuGet paketleri (ücretsiz deneme lisansları test için yeterlidir).  
- C# sözdizimine temel bir aşinalık – `Console.WriteLine` yazabiliyorsanız yeterli.  

Ek COM interop, sunucuda Office kurulumu veya manuel resim kopyala‑yapıştır gerekmez. Her şey programatik olarak halledilir.

---

## Excel'den PowerPoint Oluşturma – Çalışma Kitabını Yükleme ve Dışa Aktarım Seçeneklerini Ayarlama

İlk olarak Excel dosyasını açar ve Aspose.Cells'e sayfanın nasıl render edileceğini söyleriz. `ImageOrPrintOptions` nesnesi sihrin gerçekleştiği yerdir: `ExportShapes` ve `ExportEditableTextBoxes` özelliklerini etkinleştiririz, böylece tüm şekiller (grafikler dahil) slayt **içine** eklenir ve dönüşüm sonrası düzenlenebilir kalır.

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**Bu bayraklar neden?**  
- `OnePagePerSheet`, sayfanın birden fazla slayta bölünmesini engeller – tek bir tam‑boyutlu resim elde edersiniz.  
- `ExportShapes`, Aspose.Cells'in grafikleri *ve* vektör şekilleri rasterleştirerek görünümlerini korumasını sağlar.  
- `ExportEditableTextBoxes`, PowerPoint'te bir metin kutusuna çift tıklayıp Excel'i tekrar açmadan metni düzenleyebilmenizi sağlayan gizli sosdur.

> **İpucu:** Sadece statik bir grafik resmi ihtiyacınız varsa, `ExportShapes = false` yapın ve daha sonra `ExportExcelChartAsPicture` metodunu kullanın (son bölüme bakın).

---

## Excel'i PowerPoint'e Dönüştürme – Çalışma Sayfasından Resim Oluşturma

Seçenekler hazır olduğunda, çalışma sayfasını bir `System.Drawing.Image` nesnesine dönüştürürüz. `WorksheetToImageConverter` ağır işi yapar, az önce tanımladığımız ayarları uygular.

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

`0` argümanı ilk sayfayı gösterir (çünkü `OnePagePerSheet` sayesinde sadece bir sayfamız var). Ortaya çıkan `sheetImage`, orijinal DPI'yi korur, böylece slaytınız yüksek çözünürlüklü ekranlarda bile pikselleşmez.

---

## PPTX Olarak Kaydet – Resmi Bir Slayta Ekleme

Şimdi yeni bir PowerPoint dosyası oluşturur, bir slayt ekler ve bitmap'i üzerine bırakırız. Aspose.Slides resmi bir *picture frame* şekli olarak işler; bu şekli daha sonra yerel PowerPoint nesneleri gibi yeniden boyutlandırabilir veya taşıyabilirsiniz.

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **Resim slayt boyutundan büyük olsaydı ne olur?**  
> PowerPoint, slayt boyutlarını aşan her şeyi otomatik olarak kırpar. Hızlı bir çözüm, resmi eklemeden önce ölçeklendirmektir:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

Ardından `newWidth` ve `newHeight` değerlerini `AddPictureFrame` metoduna geçirebilirsiniz.

---

## Çalışma Sayfasını Resim Olarak Dışa Aktarma – PPTX Dosyasını Kaydetme

Son olarak sunumu diske kalıcı olarak yazarız. `SaveFormat.Pptx` bayrağı modern OpenXML formatını garantiler; bu format tüm yeni PowerPoint sürümleriyle uyumludur.

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

`Result.pptx` dosyasını açtığınızda, Excel sayfanızla tamamen aynı görünüme sahip tek bir slayt göreceksiniz, ancak yine de herhangi bir metin kutusuna tıklayıp içeriği doğrudan PowerPoint içinde düzenleyebileceksiniz.

---

## Excel Grafiğini Resim Olarak Dışa Aktarma – Raster Görüntüler Tercih Edildiğinde

Bazen düzenlenebilir şekillere ihtiyacınız olmaz; yüksek kaliteli bir PNG grafik yeterlidir. Aspose.Cells, tüm sayfayı dönüştürmeden belirli bir grafiği resim olarak dışa aktarabilir:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

Ardından `chart.png` dosyasını, `sheetImage` eklediğimiz aynı yöntemle bir slayta yerleştirebilirsiniz. Bu yaklaşım PPTX dosya boyutunu azaltır ve slaytta çevredeki verilere ihtiyaç duyulmadığında faydalıdır.

---

## Yaygın Tuzaklar ve Çözüm Önerileri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| **Metin bulanık görünüyor** | Düşük DPI (varsayılan 96) ile dışa aktarılıyor. | Dönüştürmeden önce `imageOptions.Dpi = 300;` ayarlayın. |
| **Şekiller kayboluyor** | `ExportShapes` `false` bırakılmış. | Düzenlenebilir grafiklere ihtiyacınız varsa `ExportShapes = true` olduğundan emin olun. |
| **Slayt boyutu uyuşmazlığı** | Resim slayt boyutlarından daha büyük. | Resmi ölçeklendirin (kod parçacığına bakın) veya `presentation.SlideSize` ile slayt boyutunu değiştirin. |
| **Lisans istisnası** | Deneme sürümü uygun şekilde etkinleştirilmemiş. | `License license = new License(); license.SetLicense("Aspose.Total.lic");` kodunu `Main` içinde erken çalıştırın. |

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda yeni bir konsol projesine yapıştırabileceğiniz tüm program yer alıyor. `YOUR_DIRECTORY` kısmını Excel dosyanızın bulunduğu klasörle değiştirin.

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Beklenen çıktı:**  
Program çalıştırıldığında `✅ PowerPoint successfully created at: YOUR_DIRECTORY/Result.pptx` mesajını verir. PPTX dosyasını açtığınızda, orijinal Excel sayfasını yansıtan tek bir slayt ve düzenlenebilir metin kutuları göreceksiniz.

---

## Özet ve Sonraki Adımlar

Artık Aspose'un güçlü API'lerini kullanarak **Excel'den PowerPoint oluşturma**, **çalışma sayfasını resim olarak dışa aktarma** ve **sunumu PPTX olarak kaydetme** işlemlerini, düzenlenebilirliği koruyarak nasıl yapacağınızı biliyorsunuz. Aynı desen çoklu‑sayfa çalışma kitapları için de geçerli — sadece `workbook.Worksheets` üzerinden döngü kurup her birine yeni bir slayt ekleyin.

**Bir sonraki keşifleriniz ne olabilir?**  

- **Toplu dönüşüm:** Bir klasördeki tüm Excel dosyalarını döngüyle işleyip her dosya için bir slayt destesi oluşturun.  
- **Dinamik düzenler:** `slide.LayoutSlide` kullanarak önceden tasarlanmış PowerPoint şablonlarını uygulayın.  
- **Sadece grafik dışa aktarımı:** “Excel grafiğini resim olarak dışa aktar” kod parçacığını slayt yer tutucularıyla birleştirerek daha hafif bir sunum hazırlayın.  
- **Gelişmiş stil:** Aspose.Slides ile özel slayt arka planları, geçişler veya animasyonlar ekleyin.

Denemeler yapmaktan çekinmeyin — DPI'yi değiştirin, `ShapeType.Ellipse` yerine dairesel bir picture frame kullanın ya da bir slayta birden fazla resim gömün. Programatik kontrol elinizde olduğunda sınır yoktur.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}