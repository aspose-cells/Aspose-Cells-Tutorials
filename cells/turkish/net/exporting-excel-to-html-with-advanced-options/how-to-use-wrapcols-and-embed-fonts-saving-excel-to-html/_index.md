---
category: general
date: 2026-10-20
description: Aspose.Cells'ta wrapcols kullanımını, HTML'de fontları gömmeyi ve tam
  bir C# örneğiyle Excel'i HTML olarak kaydetmeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- embed fonts in html
- save excel as html
- convert workbook to html
- use wrapcols function
language: tr
lastmod: 2026-10-20
og_description: Aspose.Cells'ta wrapcols nasıl kullanılır, HTML'de fontlar nasıl gömülür
  ve çalışma kitabı HTML'ye nasıl dönüştürülür; geliştiriciler için net bir C# rehberi.
og_image_alt: Screenshot of an Excel workbook saved as HTML with embedded fonts using
  Aspose.Cells
og_title: Excel'i HTML'ye dışa aktarırken wrapcols ve gömülü yazı tiplerini nasıl
  kullanılır?
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to use wrapcols in Aspose.Cells, embed fonts in HTML, and
    save Excel as HTML with a complete C# example.
  headline: How to use wrapcols and embed fonts saving Excel to HTML
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel to HTML
- Smart Markers
title: Excel'i HTML'ye kaydederken wrapcols ve gömülü fontları nasıl kullanılır
url: /tr/net/exporting-excel-to-html-with-advanced-options/how-to-use-wrapcols-and-embed-fonts-saving-excel-to-html/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Wrapcols Kullanımı ve Excel'i HTML Olarak Kaydetme ve Yazı Tiplerini Gömme

Aspose.Cells formülünde **wrapcols nasıl kullanılır** ihtiyacınız varsa, bu kılavuz size tam adımları gösterir. Ayrıca **HTML'de yazı tiplerini gömmeyi** ve **Excel'i HTML olarak kaydetmeyi** öğrenecek ve çıktının tarayıcılar arasında aynı görünmesini sağlayacaksınız.  

Bu öğreticide üç pratik senaryo ele alınmaktadır: `WRAPCOLS` işlevini kullanmak, gömülü yazı tipleriyle bir çalışma kitabını dışa aktarmak ve Smart Markers ile bir ana‑detay raporu oluşturmak. Sonunda, bu özelliklerin tümünü gösteren tek bir çalıştırılabilir C# programına sahip olacaksınız.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 (veya daha yeni bir sürüm) yüklü.
* Projenize Aspose.Cells for .NET eklenmiş (`dotnet add package Aspose.Cells`).
* C# ve Excel formüllerine temel aşinalık.

Ek bir üçüncü‑taraf kütüphaneye gerek yok; Aspose.Cells HTML dönüşümünü ve yazı tipi gömmeyi dahili olarak yönetir.

## Adım 1: Formülde **wrapcols nasıl kullanılır** işlevini gösterin

`WRAPCOLS` işlevi tek‑boyutlu bir aralığı iki‑boyutlu bir diziye bölerek önce sütunları doldurur. Bu, raporlama veya grafik oluşturma için verileri yeniden şekillendirmeniz gerektiğinde faydalıdır.

```csharp
using Aspose.Cells;
using System;

class WrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Populate a vertical range A1:A3
        sheet.Cells["A1"].PutValue(1);
        sheet.Cells["A2"].PutValue(2);
        sheet.Cells["A3"].PutValue(3);

        // Apply WRAPCOLS(A1:A3, 2) – this creates a 2‑column array {1,2}
        sheet.Cells["B1"].Formula = "=WRAPCOLS(A1:A3, 2)";

        // Force calculation so the formula result is materialized
        workbook.CalculateFormula();

        // Output the result to verify the function works
        Console.WriteLine("Result of WRAPCOLS: " + sheet.Cells["B1"].Value);
        // Expected output: Result of WRAPCOLS: 1
    }
}
```

**Neden bu çalışıyor:**  
`WRAPCOLS` iki argüman alır – kaynak aralık ve sütun sayısı. İşlev diziye sütun‑bazlı doldurur ve fazla değerleri (örnekteki `3` gibi) atar. Sonuç, hedef aralığın sol‑üst hücresinde (`B1`) görünür ve tam diziye ihtiyacınız varsa aralığı manuel olarak genişletebilirsiniz.

> **Pro ipucu:** Formülü ayarladıktan sonra, hücre değerlerini okumadan önce sonucun güncel olduğundan emin olmak için `workbook.CalculateFormula()` metodunu çağırın.

## Adım 2: **Çalışma kitabını HTML'e dönüştür** ve **HTML'de yazı tiplerini göm**

Bir Excel dosyasını HTML'e dışa aktardığınızda, yazı tipleri genellikle tarayıcının varsayılanlarıyla değiştirilir ve bu da görsel düzeni bozabilir. Aspose.Cells, çalışma kitabında kullanılan tam yazı tiplerini doğrudan HTML dosyasına gömmenizi sağlar.

```csharp
using Aspose.Cells;
using Aspose.Cells.Rendering;   // Required for HtmlSaveOptions
using System;

class HtmlExportDemo
{
    static void Main()
    {
        // Re‑use the workbook from the previous step
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue("Hello");
        sheet.Cells["A2"].PutValue("World");

        // Configure HTML save options
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions
        {
            // Embedding fonts ensures the output looks the same on any device
            EmbedFonts = true,
            // Optional: specify a folder for supporting files (images, CSS)
            ExportEmbeddedImages = true
        };

        // Save the workbook as an HTML file with embedded fonts
        string outputPath = @"C:\Temp\WorkbookWithFonts.html";
        workbook.Save(outputPath, htmlOptions);

        Console.WriteLine($"Workbook saved to HTML with embedded fonts at: {outputPath}");
    }
}
```

**Yazı tiplerini gömmek neden önemlidir:**  
`EmbedFonts` `true` olduğunda, Aspose.Cells kullanılan her TrueType/OpenType yazı tipini oluşturulan HTML içinde Base64‑kodlu bir `@font-face` kuralına dönüştürür. Bu, istemci makinenin aynı yazı tiplerine sahip olma ihtiyacını ortadan kaldırır ve piksel‑tam bir render garantiler.

> **Köşe durum:** Kaynak çalışma kitabı, sunucuda yüklü olmayan bir yazı tipine referans veriyorsa, Aspose.Cells varsayılan bir yazı tipine geri döner ve bir uyarı verir. Gerekli yazı tiplerinin mevcut olduğundan emin olun.

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [C#'ta WRAPCOLS Kullanımı – Wrap Fonksiyonlarıyla Excel Çalışma Kitabı Oluşturma](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [HTML'de Yazı Tiplerini Gömme – C# ile Excel'i HTML'e Dönüştürme](/cells/english/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-convert-excel-to-html-with-c/)
- [Aspose.Cells for .NET Kullanarak Excel Dosyalarını HTML'e Dönüştürme: Üst Üste Gelen İçeriği Gizleme](/cells/english/net/workbook-operations/excel-to-html-hide-overlaid-content-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}