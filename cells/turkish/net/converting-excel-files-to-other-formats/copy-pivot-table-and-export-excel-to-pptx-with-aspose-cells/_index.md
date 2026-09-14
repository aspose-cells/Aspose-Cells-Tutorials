---
category: general
date: 2026-09-11
description: Aspose.Cells kullanarak özet tabloyu kopyalayın ve Excel'i PPTX'e dışa
  aktarın. Düzenlenebilir PPTX oluşturmayı ve çalışma kitabını C#'ta PPTX olarak kaydetmeyi
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- export excel to pptx
- generate editable pptx
- save workbook as pptx
- export excel sheet pptx
language: tr
lastmod: 2026-09-11
og_description: Aspose.Cells kullanarak C#'ta pivot tabloyu kopyalayın ve Excel'i
  PPTX'e aktarın. Birkaç satır kodla düzenlenebilir PPTX oluşturun ve çalışma kitabını
  PPTX olarak kaydedin.
og_image_alt: Screenshot of copy pivot table code and generated editable PPTX slide
og_title: Pivot tabloyu kopyala ve Excel'i PPTX'e dışa aktar – tam C# rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-11'
  description: Copy pivot table and export Excel to PPTX using Aspose.Cells. Learn
    to generate editable PPTX and save workbook as PPTX in C#.
  headline: Copy pivot table and export Excel to PPTX with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel
- PPTX
- Pivot Table
title: Pivot tabloyu kopyala ve Aspose.Cells ile Excel'i PPTX'e dışa aktar
url: /tr/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot tabloyu kopyala ve Excel'i PPTX olarak Aspose.Cells ile dışa aktar

Eğer bir pivot tabloyu bir çalışma sayfasından diğerine kopyalamanız ve ardından Excel dosyasını bir PowerPoint sunumuna dışa aktarmanız gerekiyorsa, bu kılavuz size nasıl yapılacağını gösterir. Aspose.Cells kullanarak birkaç satır C# kodu ile düzenlenebilir bir PPTX oluşturabilir ve çalışma kitabını PPTX olarak kaydedebilirsiniz.

Bu öğretici, bir pivot tabloyu taşımak, işlevselliğini korumak ve grafiğin ve şekillerin düzenlenebilir kaldığı bir PPTX dosyası üretmek için gereken tüm adımları kapsar. Harici araçlara gerek yok—sadece Aspose.Cells kütüphanesi ve bir .NET geliştirme ortamı yeterlidir.

## Neler Başaracaksınız

* **Copy pivot table** bir kaynak sayfadan hedef sayfaya, tüm veri bağlantılarını koruyarak kopyala.  
* **Export Excel to PPTX**'i, böylece ortaya çıkan slayt PowerPoint'te düzenlenebilir.  
* **Generate editable PPTX**'i, grafiklerin, tabloların ve şekillerin görüntülere dönüştürülmediği bir şekilde oluştur.  
* **Save workbook as PPTX**'i aynı Aspose.Cells API çağrısı ile kaydet.  

### Önkoşullar

* .NET 6.0 veya daha yenisi (kod ayrıca .NET Framework 4.6+ ile de çalışır).  
* Aspose.Cells for .NET (NuGet paketi `Aspose.Cells`).  
* C# konsol uygulamaları hakkında temel bir anlayış.  

> **Pro ipucu:** NuGet paketini CLI üzerinden kurarak en son sürüme sahip olduğunuzdan emin olun:  
> ```bash
> dotnet add package Aspose.Cells
> ```

## Çalışma sayfaları arasında pivot tabloyu nasıl kopyalarsınız

İlk işlem, pivot tabloyu tanımını koruyarak taşımaktır. Aspose.Cells, `CopyPivotTable` bayrağını içeren bir `CopyOptions` nesnesiyle birlikte bir `CopyRange` yöntemi sağlar.

```csharp
using Aspose.Cells;
using Aspose.Cells.Export;

// Load the workbook that contains the source and destination worksheets.
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Identify the worksheets by name.
Worksheet sourceSheet = workbook.Worksheets["Source"];
Worksheet destinationSheet = workbook.Worksheets["Destination"];

// Define the range that encloses the pivot table on the source sheet.
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

// Copy the range to the destination sheet, preserving the pivot table.
destinationSheet.Cells.CopyRange(
    sourceRange,
    0,                     // destination row index
    0,                     // destination column index
    new CopyOptions { CopyPivotTable = true });
```

**Why this works:**  
`CopyRange` hücre verilerini, biçimlendirmeyi ve `CopyPivotTable` true olduğunda pivot tablonun önbelleğini ve meta verilerini kopyalar. Hedef aralık `A1` hücresinde (satır 0, sütun 0) başlar ancak ofsetleri değiştirerek pivot tabloyu başka bir yere yerleştirebilirsiniz.

**Common edge case:** Hedef sayfa aynı ada sahip bir pivot tablo zaten içeriyorsa, Aspose.Cells gelen tabloyu otomatik olarak yeniden adlandırır ve isim çakışmasını önler.

## Excel'i PPTX olarak dışa aktar ve düzenlenebilir PPTX oluştur

Pivot tablo yerinde olduktan sonra, tüm çalışma kitabını bir PPTX dosyasına dışa aktarabilirsiniz. `ImageOrPrintOptions` sınıfı, `ExportImageFormat = ImageFormat.Pptx` ayarlamanıza izin verir; bu, Aspose.Cells'in çıktıyı bir raster görüntü yerine PowerPoint sunumu olarak ele almasını sağlar.

```csharp
// Configure export options to produce an editable PPTX.
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
{
    ExportImageFormat = ImageFormat.Pptx
};

// Save the workbook as an editable PPTX file.
workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);
```

**Why this works:**  
`ExportImageFormat` `Pptx` olarak ayarlandığında, Aspose.Cells her çalışma sayfasını bir slayta dönüştürür. Şekiller, grafikler ve pivot tablolar yerel PowerPoint nesneleri olarak yazılır, böylece PowerPoint'te çift tıklayarak temel verileri düzenleyebilirsiniz.

**Tip for large workbooks:** Yalnızca belirli bir sayfa alt kümesine ihtiyacınız varsa, `Save` çağrısına önce `workbook.Worksheets.RemoveAt(index)` ile dışa aktarmak istemediğiniz sayfaları kaldırın. Bu, PPTX dosya boyutunu azaltır.

## Tam, çalıştırılabilir örnek

Aşağıda önceki adımları birleştiren tam program yer almaktadır. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek yol ile değiştirin.

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Export;

class Example
{
    static void Main()
    {
        // 1. Load the workbook that contains the source and destination worksheets.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Identify the source and destination worksheets.
        Worksheet sourceSheet = workbook.Worksheets["Source"];
        Worksheet destinationSheet = workbook.Worksheets["Destination"];

        // 3. Define the range that holds the pivot table.
        Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

        // 4. Copy the range, preserving the pivot table.
        destinationSheet.Cells.CopyRange(
            sourceRange,
            0,
            0,
            new CopyOptions { CopyPivotTable = true });

        // 5. Set up export options to generate an editable PPTX.
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions
        {
            ExportImageFormat = ImageFormat.Pptx
        };

        // 6. Save the workbook as a PPTX document.
        workbook.Save("YOUR_DIRECTORY/output.pptx", SaveFormat.Pptx, exportOptions);

        Console.WriteLine("Pivot table copied and workbook exported to PPTX successfully.");
    }
}
```

### Beklenen çıktı

Programı çalıştırdığınızda şu çıktı verir:

```
Pivot table copied and workbook exported to PPTX successfully.
```

`output.pptx` dosyasını Microsoft PowerPoint'te açtığınızda, kopyalanan pivot tablonun düzenlenebilir bir grafik olarak bulunduğu bir slayt göreceksiniz. Grafiğe çift tıkladığınızda PowerPoint grafik düzenleyicisi açılır ve serileri, eksenleri ve veri etiketlerini Excel'e geri dönmeden değiştirebilirsiniz.

## Yaygın sorunları ele alma

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| Pivot tablo statik bir görüntü olarak görünüyor | `CopyPivotTable` bayrağı atlanmış veya `ExportImageFormat` `Png` olarak ayarlanmış | `CopyPivotTable = true` ve `ExportImageFormat = ImageFormat.Pptx` olduğundan emin olun. |
| Hedef sayfa boş hücreler gösteriyor | Kaynak aralık pivot tablonun tüm alanını kapsamıyor | Aralığı (ör. `"A1:H30"`) tüm pivot alanlarını içerecek şekilde genişletin. |
| Dışa aktarılan PPTX çok büyük | Gereksiz çalışma sayfaları dahil edilmiş | `Save` çağrısından önce istenmeyen sayfaları kaldırın. |
| PowerPoint grafiği düzenleyemiyor | PPTX desteği olmayan eski bir Aspose.Cells sürümü kullanılıyor | En son Aspose.Cells sürümüne yükseltin (sürüm notlarını kontrol edin). |

## Sonraki adımlar ve ilgili konular

* **Export Excel sheet to PPTX with custom slide layouts** – slayt görünümünü daha ince kontrol etmek için `WorksheetToPdfConverter`'ı keşfedin.  
* **Export Excel to PDF** – `ImageFormat.Pptx` yerine `ImageFormat.Pdf` kullanarak PDF oluşturun.  
* **Programmatically modify PPTX after export** – animasyonlar veya konuşmacı notları eklemek için `Aspose.Slides` kütüphanesini kullanın.  

**copy pivot table**, **export excel to pptx** ve **generate editable pptx** konularını ustalaşarak, elektronik tablolardan doğrudan sunum dosyalarına veri taşıyan, düzenlenebilirliği kaybetmeyen uçtan uca raporlama boru hatları oluşturabilirsiniz.

---


## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [C#'ta Pivot Tabloyu Nasıl Kopyalarsınız – Excel'i PPTX'e Dönüştür, Aralığı Kopyala ve Metin Kutusu Oluştur](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Yeni Excel Çalışma Kitabı Oluştur – Pivot Tabloyu Kopyala ve Çoğalt](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)
- [Aspose.Cells for .NET Kullanarak Excel'de Pivot Tablo Oluştur](/cells/english/net/pivot-tables/create-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}