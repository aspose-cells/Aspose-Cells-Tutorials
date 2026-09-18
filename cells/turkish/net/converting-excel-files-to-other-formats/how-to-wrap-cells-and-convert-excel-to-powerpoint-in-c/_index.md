---
category: general
date: 2026-09-18
description: Excel çalışma kitabındaki hücreleri nasıl sarar ve PowerPoint dosyası
  olarak kaydedersiniz. WRAPCOLS kullanımını öğrenin, çalışma kitabı sayfası oluşturun
  ve PPTX olarak dışa aktarın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to wrap cells
- convert excel to powerpoint
- save excel as powerpoint
- how to use wrapcols
- create workbook worksheet
language: tr
lastmod: 2026-09-18
og_description: C# kullanarak Excel’de hücreleri nasıl kaydırır ve çalışma kitabını
  düzenlenebilir bir PowerPoint dosyası olarak dışa aktarabilirsiniz. WRAPCOLS ve
  çalışma sayfası oluşturmayı öğrenmek için adım adım rehberi izleyin.
og_image_alt: Diagram showing how to wrap cells in Excel before exporting to PowerPoint
og_title: C#'ta hücreleri kaydırma ve Excel'i PowerPoint'e dönüştürme
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: How to wrap cells in an Excel workbook and save it as a PowerPoint
    file. Learn to use WRAPCOLS, create workbook worksheet, and export to PPTX.
  headline: How to wrap cells and convert Excel to PowerPoint in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: C#'ta hücreleri kaydırma ve Excel'i PowerPoint'e dönüştürme
url: /tr/net/converting-excel-files-to-other-formats/how-to-wrap-cells-and-convert-excel-to-powerpoint-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hücreleri nasıl sarar ve Excel'i PowerPoint'e C# ile dönüştürürsünüz

Bir Excel sayfasında **hücreleri nasıl sarılır** yapmanız ve ardından o sayfayı bir PowerPoint sunumuna dönüştürmeniz gerekiyorsa, bu kılavuz size eksiksiz, çalıştırmaya hazır bir çözüm gösterir. İlk iki cümlenin sonunda, sarma işlemini gerçekleştiren API çağrılarının ve dosyayı PPTX olarak kaydeden yöntemin tam olarak hangileri olduğunu bileceksiniz.

Microsoft Office yüklü olmadan Excel çalışma kitaplarını manipüle etmenizi sağlayan bir kütüphane olan Aspose.Cells for .NET'i kullanacağız. Eğitim **convert Excel to PowerPoint** konusunu kapsar, **how to use WRAPCOLS** gösterir ve **create workbook worksheet** en iyi uygulamalarını açıklar. Harici bir araç gerekmez—sadece bir .NET geliştirme ortamı.

## Önkoşullar

- .NET 6.0 ve üzeri (kod .NET Framework 4.6+ ile de çalışır)
- Aspose.Cells for .NET NuGet paketi (`Install-Package Aspose.Cells`)
- C# ve çalışma sayfaları kavramına temel aşinalık
- Visual Studio veya VS Code gibi bir IDE

> **Pro ipucu:** Deneme sırasında Aspose.Cells'in ücretsiz değerlendirme lisansını kullanın; üretime geçmeden önce tam lisansla değiştirin.

## Adım 1: Bir çalışma kitabı oluşturun ve bir çalışma sayfası ekleyin

İlk olarak **create workbook worksheet** yapmanız gereken, bir `Workbook` nesnesi örneklemektir. Varsayılan olarak Aspose.Cells bir çalışma sayfası (indeks 0) oluşturur; bunu demo için kullanacağız.

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Step 1: Initialize a new workbook (creates one worksheet automatically)
        Workbook workbook = new Workbook();

        // Reference the first worksheet for later operations
        Worksheet ws = workbook.Worksheets[0];
```

**Neden önemli:** Çalışma kitabını başlatmak size temiz bir tuval sağlar. Varsayılan çalışma sayfası zaten `Worksheets` koleksiyonunun bir parçasıdır, bu yüzden ekstra sayfa istemediğiniz sürece `Add()` çağırmanıza gerek yoktur.

## Adım 2: Kaynak aralığını doldurun (A2:A10)

**how to wrap cells** yapmadan önce, saracak veri gerekir. Bu adım A2'den A10'a kadar hücreleri örnek metinle doldurur.

```csharp
        // Fill cells A2:A10 with a long string to demonstrate wrapping
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }
```

**Köşe durum:** Kaynak aralık boş ise, `WRAPCOLS` `#VALUE!` döndürür. Aralığın en az bir boş olmayan hücre içerdiğinden emin olun.

## Adım 3: WRAPCOLS formülünü uygulayın

Şimdi temel soru **how to use WRAPCOLS**'a yanıt veriyoruz. Formül dikey bir aralığı alır ve belirli sayıda sütuna dağıtır. Formülü `A1` hücresine yazarız; ortaya çıkan dizi otomatik olarak komşu hücrelere yayılır.

```csharp
        // Step 3: Apply WRAPCOLS to wrap A2:A10 into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";
```

**Arka planda ne olur:** `WRAPCOLS` kaynak aralığı değerlendirir, öğeleri hedef sütunlar arasında eşit (veya mümkün olduğunca yakın) şekilde böler ve değerleri dikdörtgen bir blok içine yazar. Blok boyutu dinamiktir, bu yüzden hedef aralığı önceden tanımlamanıza gerek yoktur.

## Adım 4: Çalışma kitabını düzenlenebilir bir PowerPoint dosyası olarak kaydedin

Son olarak **convert Excel to PowerPoint** ve **save Excel as PowerPoint** konularına değiniyoruz. Aspose.Cells bir çalışma sayfasını doğrudan PPTX'e aktarabilir, düzenlenebilir bir şekil olarak düzeni korur.

```csharp
        // Step 4: Export the worksheet to an editable PPTX presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

**Neden PPTX?** Oluşturulan PowerPoint, sarılmış hücrelerin tablo olarak gösterildiği tek bir slayt içerir. Dosyayı Microsoft PowerPoint'te açabilir, metni düzenleyebilir, stilleri değiştirebilir veya ek slaytlar ekleyebilirsiniz—her şey tamamen düzenlenebilir kalır.

### Beklenen çıktı

- **Excel tarafı:** `A1` hücresi, orijinal uzun dizelerin 3 sütunlu bir dizisini gösterir, her sütun yaklaşık aynı sayıda satır içerir.
- **PowerPoint tarafı:** `ChartEditable.pptx` dosyasını açmak, sarılmış düzeni yansıtan bir tablo içeren bir slayt gösterir. Tablo, yerel bir PowerPoint nesnesi gibi seçilebilir, yeniden boyutlandırılabilir veya düzenlenebilir.

## Yaygın varyasyonlar ve dikkat edilmesi gerekenler

| Senaryo | Ayarlama |
|----------|------------|
| **Wrap into more columns** | `WRAPCOLS`'in ikinci argümanını değiştirin, ör. `=WRAPCOLS(A2:A10,5)`. |
| **Wrap a different range** | Formül referansını güncelleyin, ör. `=WRAPCOLS(B2:B15,2)`. |
| **Export only a portion of the sheet** | `Worksheet.ExportDataTable` kullanarak bir `DataTable` çıkarın ve ardından özel PPTX oluşturmak için `Presentation` API'lerini kullanın. |
| **Large worksheets ( > 10 000 rows )** | Performans darboğazlarını önlemek için dışa aktarmayı birden fazla slayta bölmeyi düşünün. |

> **Dikkat edin:** Çalışma kitabı grafik içerdiğinde varsayılan PPTX dışa aktarımı çalışma sayfasını tek bir görüntü olarak render eder. `WRAPCOLS` kullanmak, verinin tablo olarak kalmasını sağlar ve bu da düzenlenebilir olur.

## Hızlı kopyala‑yapıştır için tam kaynak kodu

```csharp
using System;
using Aspose.Cells;

class WrapAndExport
{
    static void Main()
    {
        // Create a new workbook (contains one default worksheet)
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // Populate A2:A10 with sample long text
        for (int i = 2; i <= 10; i++)
        {
            ws.Cells[$"A{i}"].PutValue(
                "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                "Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
        }

        // Apply WRAPCOLS to wrap the range into 3 columns, result starts at A1
        ws.Cells["A1"].Formula = "=WRAPCOLS(A2:A10,3)";

        // Save as an editable PowerPoint presentation
        string outputPath = @"YOUR_DIRECTORY\ChartEditable.pptx";
        workbook.Save(outputPath, SaveFormat.Pptx);

        Console.WriteLine($"Workbook exported successfully to {outputPath}");
    }
}
```

Dosyayı `Program.cs` olarak kaydedin, NuGet paketini geri yükleyin ve çalıştırın:

```bash
dotnet run
```

Konsolda dışa aktarımı onaylayan mesajı görmelisiniz ve PPTX dosyası belirtilen klasörde görünecektir.

## Sonuç

Artık bir Excel çalışma sayfasında **how to wrap cells** yapmayı, **how to use WRAPCOLS**'ı ve Aspose.Cells kullanarak **save excel as powerpoint** ile **convert Excel to PowerPoint** için tam adımları biliyorsunuz. Tam çözüm **create workbook worksheet**'i gösterir, sarma formülünü uygular ve sunum ayarlamaları için hazır, düzenlenebilir bir PPTX dosyası üretir.

### Sonraki adımlar

- Dışa aktarmadan önce diğer Excel işlevlerini (ör. `TRANSPOSE`, `FILTER`) keşfedin.
- Bir döngü kullanarak birden fazla çalışma sayfasını çok‑slaytlı bir PowerPoint sunumuna birleştirin.
- Dışa aktarmadan sonra Aspose.Slides'i entegre ederek özel slayt başlıkları veya marka öğeleri ekleyin.

Farklı sütun sayıları, kaynak aralıklar veya aynı PPTX içinde grafik ve tablo kombinasyonlarıyla denemeler yapmaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki eğitimler, bu kılavuzda gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET ile Excel'i PowerPoint'e Dönüştürme: Tam Kılavuz](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Aspose.Cells for .NET ile Excel'de Metni Sarma | Biçimlendirme Eğitimi](/cells/english/net/formatting/wrap-text-excel-aspose-cells-net/)
- [Aspose.Cells for .NET ile Excel Çalışma Kitabı ve Çalışma Sayfası Özelliklerini HTML'e Dışa Aktarma](/cells/english/net/workbook-operations/export-excel-properties-to-html-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}