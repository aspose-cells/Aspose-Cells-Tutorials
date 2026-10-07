---
category: general
date: 2026-10-07
description: C#'ta Excel'i PPT olarak kaydedin ve metin kutuları ile şekilleri düzenlenebilir
  tutun. Aspose.Cells kullanarak Excel'i PowerPoint'e nasıl dönüştüreceğinizi adım
  adım öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as ppt
- convert excel to powerpoint
- how to export excel
- how to keep textboxes
- convert spreadsheet to presentation
language: tr
lastmod: 2026-10-07
og_description: C#'ta Excel'i PPT olarak kaydedin, metin kutularını ve şekilleri koruyarak.
  Excel'i PowerPoint'e tam düzenlenebilirlik ile dönüştürmek için bu eksiksiz öğreticiyi
  izleyin.
og_image_alt: Diagram of Excel workbook being saved as PPT with editable text boxes
og_title: Excel'i PPT olarak kaydet – düzenlenebilir dönüşüm rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  headline: How to save Excel as PPT with editable text boxes in C#
  type: TechArticle
- description: Save Excel as PPT in C# while keeping text boxes and shapes editable.
    Learn step‑by‑step how to convert Excel to PowerPoint using Aspose.Cells.
  name: How to save Excel as PPT with editable text boxes in C#
  steps:
  - name: Why each line matters
    text: 1. **Loading the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you full access to worksheets, charts, and embedded objects. 2. **Configuring
      `PptxSaveOptions`** – Setting `ExportTextBoxesAsEditable` and `ExportShapesAsEditable`
      tells Aspose.Cells to write those objects as native
  - name: Tips for large files
    text: '- **Memory management:** Call `GC.Collect()` after the conversion if you
      process many files in a batch. - **Image quality:** Use `opts.ImageResolution
      = 300` to increase chart clarity when the source contains high‑resolution graphics.
      - **Performance:** Set `opts.CompressionLevel = CompressionLevel.'
  - name: 'Edge case: Converting a macro‑enabled workbook (`.xlsm`)'
    text: Aspose.Cells can read `.xlsm` files, but macros are **not** transferred
      to the PPTX because PowerPoint does not support VBA macros from Excel. If you
      need the macro logic, consider exporting the relevant data first, then recreating
      the macro in PowerPoint VBA manually.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel‑to‑PowerPoint
- document‑conversion
title: C#'ta düzenlenebilir metin kutularıyla Excel'i PPT olarak kaydetme
url: /tr/net/converting-excel-files-to-other-formats/how-to-save-excel-as-ppt-with-editable-text-boxes-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i PPT olarak kaydetme ve düzenlenebilir metin kutularını C# ile koruma

Eğer **Excel'i PPT olarak kaydetmeniz** ve her metin kutusu ile şekli düzenlenebilir tutmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Aspose.Cells for .NET kullanarak birkaç satır kodla **Excel'i PowerPoint'e dönüştürebilir** ve özgün düzeni koruyarak ortaya çıkan sunumun PowerPoint'te nesneleri kaybetmeden düzenlenebilmesini sağlayabilirsiniz.

Dönüştürmenin yanı sıra, **Excel'i dışa aktarmayı** metin kutularını koruyarak nasıl yapacağınızı, metin kutularını düzenlenebilir tutmayı ve **çalışma sayfasını sunuma dönüştürmeyi** büyük çalışma kitapları ve karmaşık grafikler için nasıl çalıştıracağınızı öğreneceksiniz.

## What you’ll need

- .NET 6.0 veya üzeri (kod .NET Framework 4.6+ ile de çalışır)
- Aspose.Cells for .NET lisansı (ücretsiz deneme değerlendirme için çalışır)
- Visual Studio 2022 (veya C# destekleyen herhangi bir IDE)
- Metin kutuları, şekiller veya grafikler içeren örnek bir Excel dosyası (ör. `WithTextBoxes.xlsx`)

> **Pro ipucu:** Ücretsiz deneme sürümünü kullanıyorsanız, değerlendirme filigranlarından kaçınmak için programınızın başında `License.SetLicense("Aspose.Total.lic")` ayarlayın.

## How to save Excel as PPT while preserving text boxes

Bu bölüm doğrudan ana anahtar kelime **save Excel as PPT**'ye odaklanır. Aşağıdaki kod, yeni bir konsol projesine yapıştırabileceğiniz tam, çalıştırılabilir bir örnektir.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Presentation;

class Program
{
    static void Main()
    {
        // Step 1: Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBoxes.xlsx");

        // Step 2: Configure PPTX save options to keep text boxes and shapes editable
        PptxSaveOptions saveOptions = new PptxSaveOptions
        {
            ExportTextBoxesAsEditable = true,   // how to keep textboxes editable
            ExportShapesAsEditable = true       // also keep shapes editable
        };

        // Step 3: Save the workbook as an editable PowerPoint presentation
        workbook.Save("YOUR_DIRECTORY/ExportEditable.pptx", saveOptions);

        Console.WriteLine("Excel file has been successfully saved as PPT.");
    }
}
```

### Why each line matters

1. **Çalışma kitabını yükleme** – `Workbook`, `.xlsx` dosyasını belleğe okur ve çalışma sayfalarına, grafiklere ve gömülü nesnelere tam erişim sağlar.
2. **`PptxSaveOptions` yapılandırması** – `ExportTextBoxesAsEditable` ve `ExportShapesAsEditable` ayarları, Aspose.Cells'e bu nesneleri düzleştirilmiş görüntüler yerine yerel PowerPoint şekilleri olarak yazmasını söyler. Bu, dönüşüm sonrası **metin kutularını nasıl düzenlenebilir tutacağınız** anahtarıdır.
3. **PPTX olarak kaydetme** – `PptxSaveOptions` nesnesiyle birlikte `Save` yöntemi, gerçek **convert Excel to PowerPoint** işlemini gerçekleştirir. Çıktı dosyası (`ExportEditable.pptx`) Microsoft PowerPoint'te açılabilir ve yerel bir sunum gibi düzenlenebilir.

> **Not:** Çıktı, özgün sütun genişliklerini, satır yüksekliklerini ve hücre biçimlendirmesini korur, böylece görsel düzen kaynak Excel sayfasıyla aynı kalır.

![Başarılı dönüşümü onaylayan konsol çıktısının ekran görüntüsü](/images/save-excel-as-ppt-console.png "Excel'i PPT olarak kaydettikten sonra konsol çıktısı")

*Görsel alt metni: “Excel dosyası başarıyla PPT olarak kaydedildi.” mesajını gösteren konsol penceresi.*

## Convert Excel to PowerPoint – handling large workbooks

Birçok çalışma sayfası içeren bir **çalışma sayfasını sunuma dönüştürürken**, her sayfanın ayrı bir slayt olmasını isteyebilirsiniz. Aspose.Cells bunu otomatik olarak yapar, ancak davranışı ince ayar yapabilirsiniz:

```csharp
// Create save options with a custom slide layout
PptxSaveOptions opts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Each worksheet becomes a new slide (default behavior)
    // You can also set opts.OnePagePerSheet = false to merge sheets
};
workbook.Save("LargeExport.pptx", opts);
```

### Tips for large files

- **Bellek yönetimi:** Bir toplu işlemde birçok dosya işliyorsanız, dönüşümden sonra `GC.Collect()` çağırın.
- **Görüntü kalitesi:** Kaynak yüksek çözünürlüklü grafikler içeriyorsa, grafik netliğini artırmak için `opts.ImageResolution = 300` kullanın.
- **Performans:** Düzenlenebilirliği etkilemeden PPTX dosya boyutunu azaltmak için `opts.CompressionLevel = CompressionLevel.Maximum` ayarlayın.

## How to export Excel while preserving formulas and charts

Çalışma kitabınız formüller içeriyorsa, dönüşüm sırasında değerlendirilir ve ortaya çıkan değerler slaytlarda görünür. Orijinal formüller **aktarılamaz**, çünkü PowerPoint Excel formüllerini yerel olarak desteklemez. Ancak, kaynak çalışma kitabını sunuma bağlı tutabilirsiniz:

```csharp
PptxSaveOptions linkedOpts = new PptxSaveOptions
{
    ExportTextBoxesAsEditable = true,
    ExportShapesAsEditable = true,
    // Keep a link to the original Excel file for future updates
    LinkToSource = true
};
workbook.Save("LinkedExport.pptx", linkedOpts);
```

Kullanıcı PowerPoint'te PPTX dosyasını açtığında, bağlı verileri güncellemek isteyip istemediğini soran bir iletişim kutusu görünür. Bu, **how to export Excel** gereksinimini karşılar ve sonraki düzenlemelere izin verir.

## Common pitfalls and how to keep textboxes intact

| Symptom | Cause | Fix |
|---------|-------|-----|
| Metin kutuları görüntü olarak görünür | `ExportTextBoxesAsEditable` varsayılan `false` olarak bırakıldı | `ExportTextBoxesAsEditable = true` olarak ayarlayın |
| Şekiller PowerPoint'te taşınamıyor | `ExportShapesAsEditable` etkinleştirilmedi | `ExportShapesAsEditable = true` etkinleştirin |
| Grafik açıklamaları eksik | Grafik, dönüştürücü tarafından desteklenmeyen özel bir tema kullanıyor | Dönüştürmeden önce standart bir tema uygulayın |
| Sunum boş | Çalışma kitabı yolu yanlış veya dosya kilitli | Yolu doğrulayın ve dosyanın başka bir yerde açık olmadığından emin olun |

### Edge case: Converting a macro‑enabled workbook (`.xlsm`)

Aspose.Cells `.xlsm` dosyalarını okuyabilir, ancak makrolar **aktarılamaz** çünkü PowerPoint Excel'den VBA makrolarını desteklemez. Makro mantığına ihtiyacınız varsa, önce ilgili verileri dışa aktarmayı, ardından makroyu PowerPoint VBA'da manuel olarak yeniden oluşturmayı düşünün.

## Verify the output – convert spreadsheet to presentation correctly

Kodu çalıştırdıktan sonra, `ExportEditable.pptx` dosyasını PowerPoint'te açın:

1. **Bir metin kutusunu seçin** – nesnenin düzenlenebilir olduğunu doğrulayan tipik yeniden boyutlandırma tutamaçlarını görmelisiniz.
2. **Bir şekle sağ tıklayın** – bağlam menüsü PowerPoint şekil seçeneklerini (dolgu, çizgi vb.) gösterecektir.
3. **Slayt sırasını kontrol edin** – her çalışma sayfası bir slayta karşılık gelmeli ve özgün sekme sırasını korumalıdır.

Herhangi bir nesne düzenlenebilir değilse, `PptxSaveOptions` bayraklarını tekrar kontrol edin. Varsayılan değerler (`false`) dönüştürücünün nesneleri rasterleştirmesine neden olur; bu yüzden **metin kutularını nasıl tutacağınız** gereksinimi için bunları `true` olarak ayarlamak çok önemlidir.

## Best practices for production use

- **Lisansı erken ayarlayın:** `License license = new License(); license.SetLicense("Aspose.Total.lic");`
- **İstisna yönetimi:** Dönüşümü `try/catch` bloğu içinde sararak dosya erişim hatalarını ortaya çıkarın.
- **Günlükleme:** Denetim izleri için kaynak ve hedef yolları zaman damgalarıyla kaydedin.
- **Birim testi:** Sonuç PPTX'in beklenen düzenlenebilir şekil sayısını içerdiğini doğrulamak için bilinen nesnelere sahip küçük bir çalışma kitabı kullanın.

```csharp
try
{
    // Conversion code from earlier sections
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Conversion failed: {ex.Message}");
    // Optionally rethrow or handle according to your error policy
}
```

## Conclusion

Artık **Excel'i PPT olarak kaydetme** sırasında metin kutularını, şekilleri ve genel düzeni koruyan eksiksiz, üretim‑hazır bir çözüme sahipsiniz. `PptxSaveOptions` yapılandırmasıyla **metin kutularını nasıl tutacağınızı** düzenlenebilir hâle getirerek dönüşüm sonrası PowerPoint'te sorunsuz düzenlemeyi sağlarsınız. Aynı yaklaşım, **Excel'i PowerPoint'e dönüştürmenizi**, **Excel'i dışa aktarmanızı** ve **çalışma sayfasını sunuma dönüştürmenizi** her boyutta çalışma kitabı için mümkün kılar.

Sonraki adımda, **Excel grafiklerini yüksek çözünürlüklü görüntüler olarak dışa aktarma**, **birden fazla çalışma kitabını toplu dönüştürme** veya **oluşturulan PPTX'i bir web uygulamasına gömme** gibi ilgili konuları keşfedin. Bunların her biri burada ele alınan temeller üzerine inşa edilerek gerçek dünyadaki belge otomasyonu senaryolarında Aspose.Cells'in gücünü genişletir. Kodlamanın tadını çıkarın!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells for .NET Kullanarak Excel'i PowerPoint'e Dönüştürme: Tam Kılavuz](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells .NET ile Excel'de Metin Kutuları Ekleme ve Erişme | Adım Adım Kılavuz](/cells/english/net/images-shapes/aspose-cells-net-add-text-boxes-excel/)
- [Aspose.Cells .NET Kullanarak Excel Sayfalarını Görüntülere Dönüştürme (Adım Adım Kılavuz)](/cells/english/net/workbook-operations/convert-excel-sheets-images-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}