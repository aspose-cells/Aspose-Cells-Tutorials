---
category: general
date: 2026-10-26
description: C#'ta yazdırma alanını ayarlayın ve bir Excel sayfasını PNG olarak dışa
  aktarın. Görüntü dışa aktarma seçeneklerini öğrenin, PNG nasıl dışa aktarılır ve
  bir çalışma kitabından yazdırılabilir bir görüntü elde edin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area
- excel sheet to png
- how to export png
- export excel image
- image export options
language: tr
lastmod: 2026-10-26
og_description: Yazdırma alanını ayarlayın ve bir Excel sayfasını C# ile PNG olarak
  dışa aktarın. Bu adım adım öğretici, görüntü dışa aktarma seçeneklerini ve bir çalışma
  kitabından PNG nasıl dışa aktarılacağını kapsar.
og_image_alt: Screenshot showing an Excel worksheet with the print area set and exported
  as a PNG image
og_title: Yazdırma alanını ayarla ve Excel sayfasını PNG olarak dışa aktar – C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Set print area and export an Excel sheet to PNG in C#. Learn image
    export options, how to export PNG, and get a printable image from a workbook.
  headline: Set print area and export Excel sheet to PNG in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Yazdırma alanını ayarla ve Excel sayfasını C#'ta PNG olarak dışa aktar
url: /tr/net/rendering-and-export/set-print-area-and-export-excel-sheet-to-png-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yazdırma alanını ayarlama ve Excel sayfasını PNG olarak dışa aktarma C#'ta

Eğer bir Excel sayfasını PNG olarak dışa aktarmadan önce **set print area** yapmanız gerekiyorsa, bu rehber nasıl yapılacağını gösterir. Görüntü dışa aktarma seçeneklerini yapılandıran, çalışma sayfasının yazdırma alanını ayarlayan ve sonucu bir görüntü olarak kaydeden tam bir C# örneği göreceksiniz.

Excel sayfasını PNG olarak dışa aktarmak, bir rapor, e-posta veya web sayfasına çalışma sayfası anlık görüntüsü eklemek istediğinizde yaygın bir gereksinimdir. Aşağıdaki kod, bir pivot tablo içeren herhangi bir çalışma kitabı ile çalışır, ancak teknik normal veri aralıkları için de geçerlidir. Harici araçlara gerek yok—sadece Aspose.Cells for .NET kütüphanesi.

## Önkoşullar

- .NET 6.0 veya daha yeni (örnek .NET 6 hedefli, ancak herhangi bir yeni .NET sürümü çalışır)
- Aspose.Cells for .NET (NuGet üzerinden kurun: `Install-Package Aspose.Cells`)
- C# ve çalışma sayfaları ve yazdırma alanları gibi Excel kavramlarına temel aşinalık

## Adım 1: Görüntü dışa aktarma seçeneklerini yapılandırma

İlk olarak bir `ImageOrPrintOptions` örneği oluşturursunuz. Bu nesne, Aspose.Cells'e sayfayı nasıl bir görüntü olarak işleyebileceğini söyler.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

// Define image export options (PNG format)
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    // Export quality settings can be adjusted here
    ImageFormat = ImageFormat.Png,
    // Optional: set resolution (DPI) for higher‑quality PNGs
    HorizontalResolution = 300,
    VerticalResolution = 300
};
```

**Neden önemli:** `ImageOrPrintOptions` çıktı formatını, çözünürlüğü ve diğer işleme ayrıntılarını kontrol eder. PNG kullanmak kayıpsız kalite sağlar, bu da net metin ve grafik gerektiren raporlar için idealdir.

## Adım 2: Çalışma kitabını yükleyin ve hedef çalışma sayfasına erişin

```csharp
// Load an existing workbook (replace with your file path)
Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

// Access the first worksheet in the workbook
Worksheet worksheet = wb.Worksheets[0];
```

**Neden önemli:** Yazdırma alanı bir çalışma sayfası‑seviyesi ayar olduğu için belirli bir `Worksheet` nesnesiyle çalışmanız gerekir.

## Adım 3: Yazdırmak istediğiniz aralığı belirleyin

Birçok senaryoda ilgilendiğiniz veri bir pivot tablonun içinde yer alır. Aşağıdaki kod, sayfadaki ilk pivot tablonun veri aralığını çıkarır.

```csharp
// Get the data range of the first pivot table on the worksheet
CellArea pivotDataRange = worksheet.PivotTables[0].PivotDataRange;
```

Eğer çalışma sayfanız bir pivot tablo içermiyorsa, `pivotDataRange` yerine manuel olarak oluşturduğunuz herhangi bir `CellArea` kullanabilirsiniz, örneğin:

```csharp
CellArea customRange = new CellArea(0, 0, 20, 10); // A1:K21
```

## Adım 4: **Set print area** seçilen aralığa eşleyecek şekilde ayarlama

```csharp
// Set the worksheet's print area to match the pivot table's data range
worksheet.PageSetup.PrintArea = pivotDataRange.RefersTo;
```

**Neden önemli:** Yazdırma alanı, Excel'e (ve Aspose.Cells'e) sayfayı bir görüntüye işlerken hangi hücrelerin dahil edileceğini söyler. Yazdırma alanını pivot veri aralığıyla hizalayarak boş kenar boşluklarından kaçınır ve dışa aktarılan PNG'nin yalnızca ilgili verileri içermesini sağlarsınız.

## Adım 5: Çalışma sayfasını PNG görüntüsü olarak dışa aktar

```csharp
// Export the worksheet to an image using the defined options
// and assign the resulting image to the first picture shape on the sheet
worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);

// Optionally, save the image to a file for external use
worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);
```

**Neden önemli:** `worksheet.ToImage` daha önce ayarlanan yazdırma alanına saygı gösterir, bu yüzden PNG dosyası tam olarak tanımladığınız hücreleri içerir. Görüntüyü bir resim şekline atamak, gerektiğinde onu tekrar çalışma kitabına gömmeyi sağlar, diske kaydetmek ise bağımsız bir dosya elde etmenizi sağlar.

## Tam çalışan örnek

Tüm adımları bir araya getirerek hemen çalıştırabileceğiniz bağımsız bir program elde edersiniz.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Rendering;
using System.Drawing.Imaging;

class ExportExcelToPng
{
    static void Main()
    {
        // 1️⃣ Configure image export options (PNG format)
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            HorizontalResolution = 300,
            VerticalResolution = 300
        };

        // 2️⃣ Load the workbook
        Workbook wb = new Workbook(@"C:\Temp\SampleWorkbook.xlsx");

        // 3️⃣ Access the first worksheet
        Worksheet worksheet = wb.Worksheets[0];

        // 4️⃣ Get the data range of the first pivot table (or define your own)
        CellArea dataRange = worksheet.PivotTables[0].PivotDataRange;

        // 5️⃣ **Set print area** to the data range
        worksheet.PageSetup.PrintArea = dataRange.RefersTo;

        // 6️⃣ Export the worksheet as PNG
        worksheet.Pictures[0].Image = worksheet.ToImage(imageOptions);
        worksheet.Pictures[0].Image.Save(@"C:\Temp\WorksheetExport.png", ImageFormat.Png);

        Console.WriteLine("Export complete: WorksheetExport.png created.");
    }
}
```

### Beklenen çıktı

Programı çalıştırmak `C:\Temp\WorksheetExport.png` dosyasını oluşturur. Dosyayı açtığınızda **set print area** ile tanımlanan hücreleri (bu örnekte pivot tablo verileri) içeren net bir PNG görüntüsü görürsünüz. Görüntü, ek bir dönüşüm adımı gerektirmeden Word belgelerine, PowerPoint slaytlarına veya web sayfalarına eklenebilir.

## Birden fazla çalışma sayfası veya pivot tablo işleme

- **Multiple worksheets:** `wb.Worksheets` üzerinden döngü yapın ve dışa aktarmanız gereken her sayfa için adım 3‑5'i tekrarlayın.
- **Multiple pivot tables:** Uygun `PivotTables[index]` seçin veya `worksheet.PivotTables` üzerinde döngü yaparak her tabloyu ayrı ayrı dışa aktarın.
- **No pivot table:** `CellArea`'yı manuel olarak oluşturun (Adım 3'teki yoruma bakın) ve `PrintArea`'ya atayın.

## Pratik ipuçları (E‑E‑A‑T)

- **Pro tip:** Baskıya hazır PNG'ler için `HorizontalResolution` ve `VerticalResolution` değerlerini 300 DPI olarak ayarlayın; daha düşük değerler web kullanımı için dosya boyutunu azaltır.
- **Watch out for empty picture shapes:** Çalışma sayfasında resim şekli yoksa, görüntüyü atamadan önce bir tane ekleyin:

```csharp
if (worksheet.Pictures.Count == 0)
{
    worksheet.Pictures.Add(0, 0, 0, 0);
}
```

- **Performance:** Birden fazla çalışma sayfası için tek bir `ImageOrPrintOptions` örneği yeniden kullanmak gereksiz tahsisleri önler.
- **Compatibility:** Aspose.Cells 23.9+ .NET 6 ve sonrası ile tam uyumludur; daha eski sürümler API adlarında ayarlamalar gerektirebilir.

## Sonuç

Artık **set print area** nasıl yapılacağını ve bir Excel'i dışa aktarmayı biliyorsunuz

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Excel'i PNG olarak dışa aktarma – tam adım‑adım kılavuz](/cells/english/net/image-and-chart-operations/how-to-export-excel-to-png-full-step-by-step-guide/)
- [Excel aralığını C# ve Aspose.Cells ile görüntü olarak dışa aktarma](/cells/english/net/image-and-chart-operations/how-to-export-excel-range-as-image-with-c-and-aspose-cells/)
- [excel sayfasını png'ye – C#'ta bir Pivot Tabloyu PNG olarak dışa aktarma](/cells/english/net/conversion-and-rendering/excel-sheet-to-png-export-a-pivot-table-as-png-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}