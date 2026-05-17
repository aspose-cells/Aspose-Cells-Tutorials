---
category: general
date: 2026-03-22
description: Excel'de yazdırma alanını ayarlayın ve düzenlenebilir şekillerle Excel'i
  PowerPoint'e dönüştürün. Başlık satırını nasıl tekrarlayacağınızı, Excel'den PowerPoint
  oluşturmayı ve Excel'i pptx olarak dışa aktarmayı öğrenin.
draft: false
keywords:
- set print area
- convert excel to powerpoint
- repeat title row
- create powerpoint from excel
- export excel to pptx
language: tr
og_description: Excel'de yazdırma alanını ayarlayın ve düzenlenebilir şekiller içeren
  bir PowerPoint slaytına dönüştürün. Başlık satırını tekrarlamak ve Excel'i pptx
  olarak dışa aktarmak için bu kapsamlı rehberi izleyin.
og_title: Excel'de Yazdırma Alanını Ayarlama – PowerPoint'e Aktarma Öğreticisi
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint generation
title: Excel'de Yazdırma Alanını Ayarlayın ve PowerPoint'e Aktarın – Adım Adım Rehber
url: /tr/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Yazdırma Alanını Ayarlama ve PowerPoint'e Aktarma – Tam Programlama Öğreticisi

Hiç Excel çalışma sayfasında **set print area** ihtiyacı duydunuz ve ardından bu bölümü bir PowerPoint slaytına dönüştürmek istediniz mi? Tek başınıza değilsiniz. Birçok raporlama sürecinde güzel bir şekilde yazdırılan aynı verilerin bir sunumda da görünmesi gerekir; genellikle ilk satır başlık olarak tekrarlanır. İyi haber? Birkaç C# satırıyla **convert excel to powerpoint** yapabilir, tüm metin kutularını düzenlenebilir tutabilir ve hatta **repeat title row** otomatik olarak gerçekleştirebilirsiniz.

Bu rehberde, bilmeniz gereken her şeyi adım adım ele alacağız: yazdırma alanını yapılandırmaktan PowerPoint içinde doğrudan düzenleyebileceğiniz bir PPTX dosyası oluşturmaya kadar. Sonunda **create powerpoint from excel** yapabilecek, sonucu **export excel to pptx** olarak dışa aktarabilecek ve aynı kodu herhangi bir .NET projesinde yeniden kullanabileceksiniz. Sihir yok, sadece net adımlar ve tam, çalıştırılabilir bir örnek.

## Gereksinimler

- **.NET 6.0** veya daha yenisi (API, .NET Framework ile de çalışır)
- **Aspose.Cells for .NET** (`Workbook`, `ImageOrPrintOptions` vb. sağlayan kütüphane)
- Temel bir C# IDE (Visual Studio, Rider veya C# uzantılı VS Code)
- Dışa aktarmak istediğiniz verileri içeren bir Excel dosyası (`input.xlsx`)

Hepsi bu—Aspose.Cells dışında ekstra NuGet paketi yok. Kütüphaneyi henüz eklemediyseniz, şu komutu çalıştırın:

```bash
dotnet add package Aspose.Cells
```

Şimdi başlayabiliriz.

## Adım 1: Çalışma Kitabını Yükleme – Dışa Aktarmanın Başlangıç Noktası

İlk yapmanız gereken, slayta dönüştürmek istediğiniz sayfayı içeren çalışma kitabını yüklemektir. Çalışma kitabını kaynak belge olarak düşünün; onsuz başka bir şey önemsizdir.

```csharp
using Aspose.Cells;

// Load the workbook that contains the shapes and data
Workbook workbook = new Workbook(@"C:\MyProjects\ExcelToPpt\input.xlsx");
```

**Neden önemli:** Çalışma kitabını yüklemek, çalışma sayfası koleksiyonuna, sayfa‑ayarları seçeneklerine ve dışa aktarma motoruna erişim sağlar. Bu adımı atlayarsanız **print area** ayarlayamaz veya satırları tekrarlayamazsınız.

> **Pro ipucu:** Test ederken mutlak bir yol kullanın, ardından üretim için göreli bir yol ya da yapılandırma‑tabanlı bir yol ile değiştirin.

## Adım 2: Dışa Aktarma Seçeneklerini Yapılandırma – Metin Kutularını ve Şekilleri Düzenlenebilir Tutma

PowerPoint'e dışa aktarırken muhtemelen ortaya çıkan slaytın düzenlenebilir olmasını istersiniz. Aspose.Cells, bunu `ImageOrPrintOptions` ile kontrol etmenizi sağlar. `ExportTextBoxes` ve `ExportShapeObjects` değerlerini `true` olarak ayarlamak, kütüphaneye bu nesneleri bir görüntüye dönüştürmek yerine yerel PowerPoint öğeleri olarak korumasını söyler.

```csharp
// Configure export options for a PPTX slide
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    SaveFormat = SaveFormat.Pptx,      // The target format – crucial for PowerPoint
    ExportTextBoxes = true,            // Keep text boxes editable
    ExportShapeObjects = true          // Keep shape objects editable
};
```

**Neden önemli:** Eğer bir zaman **convert excel to powerpoint** yapıp ardından slaytı manuel olarak ayarlamanız gerekirse, bu ayar metin kutularını baştan oluşturmanızı engeller. Ayrıca oklar veya grafikler gibi şekillerin yeniden boyutlandırabileceğiniz vektör nesneleri olarak kalmasını sağlar.

## Adım 3: Yazdırma Alanını Ayarlama ve Başlık Satırını Tekrarlama

Şimdi öğreticinin özüne geliyoruz: **set print area** ve ilk satırın her sayfada (veya bizim durumumuzda dışa aktarılan slaytta) tekrarlanmasını sağlamak. Yazdırma alanı, Excel'e hangi hücrelerin yazdırılacağını—ya da bizim senaryomuzda dışa aktarılacağını—söyler.

```csharp
// Define the area of the sheet to export (A1:G20)
Worksheet sheet = workbook.Worksheets[0];
sheet.PageSetup.PrintArea = "A1:G20";

// Repeat the first row as a title on each printed page
sheet.PageSetup.PrintTitleRows = "$1:$1";
```

**Neden önemli:** Dışa aktarmayı `A1:G20` ile sınırlayarak büyük boş aralıkların çekilmesini önlersiniz; bu dönüşümü hızlandırır ve slaytı düzenli tutar. `PrintTitleRows` satırı, ilk satırı bir başlık gibi davranır—sunumda **repeat title row** istediğinizde tam olarak ihtiyacınız olan şey.

> **Köşe durum:** Verileriniz 2. satırda başlıyorsa, aralığı buna göre ayarlayın (ör. `PrintTitleRows = "$2:$2"`).

## Adım 4: Çalışma Sayfasını PowerPoint Dosyası Olarak Kaydetme

Son olarak, slaytı diske yazıyoruz. `Save` yöntemi hedef dosya adını ve daha önce yapılandırdığımız seçenekleri alır. Sonuç, düzenlenebilir metin kutuları ve şekiller içeren, PowerPoint'te açılmaya hazır bir PPTX dosyasıdır.

```csharp
// Save the selected sheet as a PPTX file using the configured options
string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
workbook.Save(outputPath, exportOptions);
```

**Gördükleriniz:** PowerPoint'te `SheetWithEditableShapes.pptx` dosyasını açın. İlk satır bir başlık olarak görünür, `A1:G20` aralığındaki tüm hücreler işlenir ve Excel'de eklediğiniz şekiller hâlâ hareket ettirilebilir ve düzenlenebilir. Rasterleştirilmiş görüntüler yok—sadece yerel PowerPoint nesneleri.

## Tam Çalışan Örnek – Tüm Adımlar Birleştirildi

Aşağıda, tamamen kopyala‑yapıştır hazır program bulunmaktadır. Bir konsol uygulaması olarak çalıştırabilir veya daha büyük bir çözüme gömebilirsiniz.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the workbook
            string inputPath = @"C:\MyProjects\ExcelToPpt\input.xlsx";
            Workbook workbook = new Workbook(inputPath);

            // Step 2: Set export options for editable PPTX
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportTextBoxes = true,
                ExportShapeObjects = true
            };

            // Step 3: Define print area and repeat title row
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G20";
            sheet.PageSetup.PrintTitleRows = "$1:$1";

            // Step 4: Save as PowerPoint
            string outputPath = @"C:\MyProjects\ExcelToPpt\SheetWithEditableShapes.pptx";
            workbook.Save(outputPath, exportOptions);

            Console.WriteLine($"Successfully exported to {outputPath}");
        }
    }
}
```

**Beklenen çıktı:** Programı çalıştırdıktan sonra, konsol başarı mesajını yazdırır ve PPTX dosyası belirtilen konumda ortaya çıkar. Dosyayı açtığınızda seçilen aralıkla tek bir slayt, düzenlenebilir metin kutuları ve orijinal şekiller gösterilir.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

| Soru | Cevap |
|------|-------|
| **Bu birden fazla çalışma sayfası ile çalışır mı?** | Evet. `workbook.Worksheets` üzerinden döngü yapın ve her sayfa için aynı adımları tekrarlayın, her seferinde çıktı dosya adını değiştirin. |
| **Birden fazla slayt dışa aktarmam gerekirse ne yapmalıyım?** | `workbook.Save` metodunu farklı `ImageOrPrintOptions` nesneleriyle birden çok kez çağırın; gerektiğinde her biri farklı bir `PageSetup` ile yapılandırılmış olur. |
| **Slayt boyutunu değiştirebilir miyim?** | DPI ayarlamak için `exportOptions.ImageFormat` kullanın veya kaydetmeden önce `sheet.PageSetup.PaperSize` değerini değiştirin. |
| **Aspose.Cells ücretsiz mi?** | Su işaretli ücretsiz bir değerlendirme sunar. Üretim için lisans gereklidir. |
| **Excel formülleri ne olacak?** | Dışa aktarılan değerler, dışa aktarma anındaki **hesaplanmış sonuçlardır**. PowerPoint'te canlı formüllere ihtiyacınız varsa, farklı bir yaklaşım gerekecektir. |

## Sorunsuz Bir İş Akışı İçin İpuçları

- **Pro ipucu:** Dışa aktarmadan önce tüm formüllerin güncel olmasını sağlamak için `Workbook.Settings.CalcMode = CalculationModeType.Automatic` ayarlayın.
- **Dikkat:** Çok büyük aralıklar bellek baskısına neden olabilir. Yazdırma alanını en küçük gerekli aralığa indirgeyin.
- **Performans ipucu:** Birçok sayfa dışa aktarıyorsanız tek bir `ImageOrPrintOptions` örneğini yeniden kullanın; her seferinde yeni bir tane oluşturmak ek yük getirir.
- **Sürüm notu:** Yukarıdaki kod, Aspose.Cells 23.10 (Kasım 2023'te yayınlandı) sürümünü hedeflemektedir. Daha sonraki sürümler aynı API'yi korur, ancak kırılma değişiklikleri için her zaman sürüm notlarını kontrol edin.

## Sonuç

Excel çalışma sayfasında **set print area** nasıl yapılır, ilk satırın başlık olarak nasıl tekrarlanır ve ardından **export excel to pptx** nasıl yapılır, düzenlenebilir metin kutuları ve şekiller korunarak ele alındı. Kısacası, sadece birkaç C# satırıyla **convert excel to powerpoint**, **repeat title row** ve **create powerpoint from excel** yapmanın güvenilir bir yolunu artık biliyorsunuz.

Bir sonraki adıma hazır mısınız? Onlarca raporu toplu olarak dönüştürmeyi otomatikleştirmeyi deneyin ya da dışa aktarmadan sonra PowerPoint SDK'sını kullanarak özel slayt düzenleri ekleyin. Sınır yok—deneyin, hatalar yapın ve programatik belge oluşturmanın gücünün tadını çıkarın.

Bu öğreticiyi faydalı bulduysanız, paylaşın, kendi düzenlemelerinizle bir yorum bırakın veya **export excel to pptx** ve ilgili otomasyon konularındaki diğer rehberlerimize göz atın. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}