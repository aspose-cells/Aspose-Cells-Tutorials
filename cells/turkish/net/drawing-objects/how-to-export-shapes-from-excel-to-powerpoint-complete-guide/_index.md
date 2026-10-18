---
category: general
date: 2026-07-26
description: Excel çalışma sayfasındaki şekilleri sadece birkaç adımda PowerPoint'e
  nasıl aktarılır – geliştiriciler için hızlı bir Excel'den PPTX'e dışa aktarma öğreticisi.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: tr
lastmod: 2026-07-26
og_description: Excel'den PowerPoint'e şekilleri adım adım nasıl dışa aktarılır. Bu
  Excel'den PPTX'e dışa aktarma öğreticisini izleyin ve çalışma sayfalarınızın düzenlenebilir
  slaytlara dönüşümünü görün.
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Excel'den PowerPoint'e Şekilleri Nasıl Dışa Aktarırsınız – Hızlı ve Kolay
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Excel'den PowerPoint'e Şekilleri Nasıl Dışa Aktarılır – Tam Rehber
url: /tr/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'den PowerPoint'e Şekilleri Dışa Aktarma – Tam Kılavuz

Hiç **şekilleri dışa aktarmanın** bir Excel dosyasından nasıl yapılacağını ve PowerPoint sunumunda düzenlenebilir kalmasını merak ettiniz mi? Tek başınıza değilsiniz. Raporlama hattı oluşturuyor olun ya da sadece bir elektronik tabloyu sunuma hızlıca dönüştürmeniz gerekiyor olsun, **çalışma sayfasını PowerPoint'e dönüştürme** yeteneği, şekil düzenlenebilirliğini kaybetmeden saatlerce manuel işi tasarruf ettirebilir.

Bu **excel to powerpoint tutorial** içinde, bir çalışma kitabını yükleyen, doğru dışa aktarma seçeneklerini yapılandıran ve metin kutuları ile diğer çizim nesnelerinin düzenlenebilir kaldığı bir PPTX dosyası yazan tam çalışan bir C# örneğini adım adım inceleyeceğiz. Belirsiz referanslar yok—sadece bugün kopyalayıp yapıştırıp çalıştırabileceğiniz kod.

## Öğrenecekleriniz

- Şekil düzenlenebilirliğini koruyarak **export excel to pptx** için tam adımlar.  
- `Aspose.Cells` kütüphanesinin `PptxSaveOptions` öğesinin dışa aktarma davranışını nasıl kontrol ettiğini.  
- Birden fazla çalışma sayfasını, eksik dosyaları ve özel şekil ayarlarını yönetmek için ipuçları.  
- Herhangi bir .NET projesine ekleyebileceğiniz tam, çalıştırılabilir bir program.

### Ön Koşullar

- .NET 6.0 veya daha yeni bir sürüm (kod ayrıca .NET Framework 4.7+ üzerinde de çalışır).  
- **Aspose.Cells for .NET** için geçerli bir lisans (ücretsiz deneme test için çalışır).  
- En az bir metin kutusu veya şekil içeren bir Excel çalışma kitabı (ör. `ShapesDemo.xlsx`).  
- Bir geliştirme ortamı—Visual Studio, Rider veya VS Code yeterli.

Bunlara sahipseniz, başlayalım.

## Adım 1: Çalışma Kitabını Yükleme – Şekilleri Dışa Aktarmanın Başlangıç Noktası

İlk olarak, düzenlenebilir tutmak istediğimiz şekilleri içeren Excel dosyasını açmamız gerekiyor.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**Neden önemli:**  
`Workbook` nesnesi, dosya içindeki her hücre, grafik ve çizim nesnesine erişim sağlayan bir kapıdır. İlk çalışma sayfasını (`Worksheets[0]`) alarak bilinen bir sayfa üzerinde çalıştığımızı garantileriz, ancak belirli bir sekme gerekiyorsa indeksi bir isimle (`workbook.Worksheets["Sheet2"]`) değiştirebilirsiniz.

> **Pro ipucu:** Dosya yolu yanlış olduğunda dostça bir hata mesajı vermek için yükleme çağrısını bir `try / catch` bloğuna sarın.

## Adım 2: PPTX Dışa Aktarma Seçeneklerini Yapılandırma – Şekilleri Dışa Aktarmanın Çekirdeği

Şimdi Aspose.Cells'e, oluşturulan PPTX içinde şekillerin düzenlenebilir kalmasını söylüyoruz.

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**Bu bayraklar neden?**  
- `ExportEditableTextBoxes`, Excel metin kutularını çift tıklayıp düzenleyebileceğiniz PowerPoint metin yer tutucularına dönüştürür.  
- `ExportEditableShapes`, oklar, dikdörtgenler ve SmartArt gibi şekiller için aynı işlemi yapar. Bunlar olmadan nesneler statik görüntüler haline gelir ve **convert worksheet to powerpoint** iş akışının amacını bozar.

`PptxSaveOptions`'ı slayt boyutunu, temayı veya yazı tiplerinin gömülüp gömülmeyeceğini kontrol edecek şekilde ayarlayabilirsiniz—sunumunuzun kurumsal marka ile eşleşmesi gerektiğinde faydalıdır.

## Adım 3: Çalışma Sayfasını PPTX Olarak Kaydet – Excel Çalışma Kitabını PowerPoint'e Dışa Aktarmanın Son Parçası

Seçenekler ayarlandığında, kaydetmek basittir.

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**Arka planda ne olur?**  
Aspose.Cells, sayfadaki her çizim nesnesi üzerinde döner, onu karşılık gelen PowerPoint şekil sınıfına eşler ve PowerPoint'in okuduğu XML'i yazar. Düzenlenebilir bayrakları etkinleştirdiğimiz için XML, her şekli `Picture` yerine `Shape` olarak işaretler, böylece PowerPoint bunu canlı bir nesne olarak kabul eder.

## Adım 4: Dışa Aktarmayı Doğrulama – Kullanıcı için Hızlı Geri Bildirim

Küçük bir konsol mesajı, işlemin başarılı olduğunu bildirir.

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

Programı çalıştırıp mesajı görürseniz, PowerPoint'te `ShapesEditable.pptx` dosyasını açın. Herhangi bir metin kutusuna tıklayın—metni doğrudan düzenleyebilmelisiniz ve bir şekli sürüklemek, onu yerel bir PowerPoint nesnesi gibi hareket ettirmelidir.

## Adım 5: Gerçek Dünya Senaryolarını Ele Alma

Aşağıda bir **excel to powerpoint tutorial** üzerinde çalışırken karşılaşabileceğiniz yaygın varyasyonlar bulunmaktadır.

### Birden Çok Çalışma Sayfası

Birden fazla sayfayı tek bir PPTX'e dışa aktarmanız gerekiyorsa, `workbook.Worksheets` üzerinde döngü yapın ve aynı `pptxOptions` ile `worksheet.Save` çağırın. Aspose.Cells her sayfa için otomatik olarak yeni bir slayt ekleyecektir.

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### Özel Slayt Düzenleri

`pptxOptions.SlideSize` (ör. `SlideSizeType.Widescreen`) belirterek kurumsal sunum boyutlarınıza uyan bir slayt boyutu ayarlayabilirsiniz.

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### Eksik Dosyalar veya İzinler

Tüm `Main` metodunu bir `try` bloğuna sarın:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

Bu, **export excel workbook powerpoint** sürecini üretim hatları için sağlam hâle getirir.

## Tam Çalışan Örnek

İşte hemen derleyebileceğiniz tam program. `ExportEditableShapes.cs` olarak kaydedin, dosya yollarını ayarlayın ve `dotnet run` komutunu çalıştırın.

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**Beklenen çıktı** programı çalıştırdığınızda:

```
Exported worksheet with editable shapes.
```

Oluşturulan `ShapesEditable.pptx` dosyasını açın ve her Excel şeklinin tamamen düzenlenebilir bir PowerPoint nesnesi olarak göründüğünü göreceksiniz—**how to export shapes** aradığınız tam olarak bu.

## Sıkça Sorulan Sorular

- **Bu eski Excel formatlarıyla (.xls) çalışır mı?**  
  Evet. `Workbook` `.xls`, `.xlsx` ve hatta CSV dosyalarını açabilir. Şekil dışa aktarımı aynı şekilde çalışır.

- **Grafikleri düzenlenebilir tutmam gerekirse ne olur?**  
  Grafikler zaten yerel PowerPoint grafikleri olarak dışa aktarılır; ekstra bayraklara ihtiyacınız yok.

- **PDF yerine PPTX'e dışa aktarabilir miyim?**  
  Kesinlikle—sadece `SaveFormat.Pptx` yerine `SaveFormat.Pdf` koyun ve `PptxSaveOptions`'ı atlayın.

## Sonuç

Artık Excel'den düzenlenebilir bir PowerPoint sunumuna **how to export shapes** sorusunun sağlam, uçtan uca bir yanıtına sahipsiniz. `Aspose.Cells`'in `PptxSaveOptions` özelliğini kullanarak her metin kutusunu ve çizim nesnesini korur, statik bir elektronik tabloyu minimum çabayla dinamik bir sunuma dönüştürürsünüz.

Bir sonraki zorluğa hazır mısınız? Özel slayt ana temaları eklemeyi, programatik olarak resim eklemeyi deneyin ya da bu dışa aktarmayı haftalık satış sunumlarını otomatik olarak üreten bir CI/CD hattına bağlayın. **export excel workbook powerpoint** dünyası tamamen açık—keşfedin!

--- 

*Bu **excel to powerpoint tutorial**'ı faydalı bulduysanız, GitHub'da yıldız verin ya da hâlâ elektronik tabloları slaytlara kopyalayan bir meslektaşınızla paylaşın. İyi kodlamalar!*

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells Java Kullanarak Bir Excel Çalışma Sayfasını PNG Olarak Dışa Aktarma](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Aspose.Cells for Java Kullanarak Excel Hücrelerini Görüntü Olarak Dışa Aktarma](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [Aspose.Cells Java ile Ölçeklenebilir Vektör Grafikleri (SVG) Olarak Excel Grafiklerini Dışa Aktarma](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}