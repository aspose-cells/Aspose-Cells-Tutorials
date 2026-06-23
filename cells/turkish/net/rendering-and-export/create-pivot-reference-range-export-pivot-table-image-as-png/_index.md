---
category: general
date: 2026-02-09
description: C#'ta pivot referans aralığı oluşturun ve pivot tablo görüntüsünü dışa
  aktarın. Aspose.Cells kullanarak Excel aralığını png olarak kaydetmeyi öğrenin –
  hızlı ve kapsamlı rehber.
draft: false
keywords:
- create pivot reference range
- export pivot table image
- save excel range as png
- Aspose.Cells C#
- Excel automation C#
language: tr
og_description: C#'ta pivot referans aralığı oluşturun ve pivot tablo görüntüsünü
  PNG olarak dışa aktarın. Excel aralığını PNG olarak kaydetmek için eksiksiz adım
  adım rehber.
og_title: Pivot Referans Aralığını Oluştur – Pivot Tablo Görüntüsünü PNG Olarak Dışa
  Aktar
tags:
- Aspose.Cells
- C#
- Excel
title: Pivot Referans Aralığını Oluştur – Pivot Tablo Görüntüsünü PNG Olarak Dışa
  Aktar
url: /tr/net/rendering-and-export/create-pivot-reference-range-export-pivot-table-image-as-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot Referans Aralığını Oluştur – Pivot Tablo Görüntüsünü PNG Olarak Dışa Aktar

Bir Excel çalışma kitabında **pivot referans aralığını** C# ile oluşturmak mı istiyorsunuz? Sadece birkaç satır kodla **pivot tablo görüntüsünü dışa aktarabilir** ve **Excel aralığını png olarak kaydedebilirsiniz**. Deneyimlerime göre, canlı bir pivotu statik bir görüntüye dönüştürmek, analizleri raporlara, e‑postalara veya panolara bütün çalışma kitabını getirmeden eklemenin pratik bir yoludur.

Bu öğreticide ihtiyacınız olan her şeyi adım adım inceleyeceğiz: gerekli kütüphaneler, tam kod, her çağrının önemi ve karşılaşabileceğiniz bazı tuzaklar. Sonunda, herhangi bir pivot tablonun PNG dosyasını güvenle üretebilecek ve bu deseni birden çok çalışma sayfası veya özel görüntü formatları için nasıl uyarlayacağınızı anlayacaksınız.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- **Aspose.Cells for .NET** (ücretsiz deneme sürümü test için yeterlidir).  
- **.NET 6.0** veya üzeri – kullandığımız API, .NET Standard 2.0+ ile tamamen uyumludur, bu yüzden daha eski framework’ler de derlenebilir.  
- Temel bir C# projesi (Console App, WinForms veya ASP.NET – NuGet paketi referanslayabilen herhangi bir proje).  

Aspose.Cells’ı henüz kurmadıysanız, şu komutu çalıştırın:

```bash
dotnet add package Aspose.Cells
```

Hepsi bu – COM interop yok, sunucuda Excel kurulumu da gerekmez.

## Adım 1: Çalışma Kitabını Açın ve İlk Çalışma Sayfasına Erişin

İlk olarak çalışma kitabı dosyasını yükleyip pivot tablonun bulunduğu çalışma sayfasını alın. Demo dosyalarının çoğu pivotu **ilk çalışma sayfasına** (`Worksheets[0]`) koyduğu için bu örnekte onu seçiyoruz; isterseniz indeks yerine isim de verebilirsiniz.

```csharp
using Aspose.Cells;
using System;

// Load an existing Excel file (replace with your own path)
Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

// Access the first worksheet – this is where our pivot lives
Worksheet worksheet = wb.Worksheets[0];
```

*Neden önemli:* `Worksheet`, tüm aralık‑tabanlı işlemlerin giriş noktasıdır. Yanlış sayfayı işaret ederseniz, sonraki `PivotTables[0]` çağrısı `IndexOutOfRangeException` fırlatır.

## Adım 2: Pivot Referans Aralığını Oluşturun

Şimdi pivot tablonun kendisinden **referans aralığını** isteyelim. Bu aralık, pivotun tam hücrelerini – başlıkları, veri satırlarını ve toplamları – temsil eder. `CreateReferenceRange()` metodu, birleştirilmiş hücreleri ve gizli satırları sizin için halleder.

```csharp
// Grab the first pivot table on the worksheet
PivotTable pivot = worksheet.PivotTables[0];

// Build a reference range that covers the whole pivot
Range pivotReferenceRange = pivot.CreateReferenceRange();
```

> **İpucu:** Çalışma kitabınızda birden fazla pivot varsa, `worksheet.PivotTables` koleksiyonunu döngüye alıp `Name` özelliğine göre ihtiyacınız olanı seçebilirsiniz.

## Adım 3: Referans Aralığını Görüntü Olarak Render Edin

Aspose.Cells, herhangi bir `Range`’i görüntüye dönüştürebilir. Dönen nesne raster (PNG, JPEG) ve vektör (SVG) formatlarını destekler. Burada varsayılan raster görüntüyü istiyoruz; bu, `System.Drawing.Image`‑uyumlu bir nesnedir.

```csharp
// Convert the pivot reference range into an image object
ImageOrVector pivotImage = pivotReferenceRange.ToImage();
```

*Arka planda ne oluyor?* API, hücre stillerini, yazı tiplerini ve koşullu biçimlendirmeyi dikkate alarak aralığın görsel düzenini anlık olarak yakalar. Temelde bir ekran görüntüsü almak gibi, ancak programatik ve UI olmadan.

## Adım 4: Oluşturulan Görüntüyü Dosyaya Kaydedin

Son olarak görüntüyü kalıcı hale getirin. `Save` metodu, uzantı “.png” olduğunda otomatik olarak PNG seçer. DPI kontrolü veya farklı bir format isterseniz bir `SaveOptions` nesnesi de geçirebilirsiniz.

```csharp
// Save the image as PNG – the extension drives the format
pivotImage.Save("YOUR_DIRECTORY/pivot.png");
```

Bu satır çalıştıktan sonra `pivot.png` dosyasını açın; pivot tablonun pikselleşmiş bir anlık görüntüsü, istediğiniz yere yerleştirilmeye hazır olacaktır.

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, kopyalayıp çalıştırabileceğiniz bağımsız bir konsol programı aşağıdadır:

```csharp
using Aspose.Cells;
using System;

namespace PivotExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/source.xlsx");

            // 2️⃣ Access first worksheet
            Worksheet worksheet = wb.Worksheets[0];

            // 3️⃣ Get first pivot table
            if (worksheet.PivotTables.Count == 0)
            {
                Console.WriteLine("No pivot tables found on the first sheet.");
                return;
            }
            PivotTable pivot = worksheet.PivotTables[0];

            // 4️⃣ Create a reference range that covers the whole pivot
            Range pivotReferenceRange = pivot.CreateReferenceRange();

            // 5️⃣ Render the range to an image
            ImageOrVector pivotImage = pivotReferenceRange.ToImage();

            // 6️⃣ Save as PNG
            string outputPath = "YOUR_DIRECTORY/pivot.png";
            pivotImage.Save(outputPath);

            Console.WriteLine($"Pivot table image saved to {outputPath}");
        }
    }
}
```

**Beklenen çıktı:** `YOUR_DIRECTORY` içinde `pivot.png` adlı bir dosya. Herhangi bir görüntü görüntüleyicide açın – orijinal pivotun tam düzenini, sütun başlıkları, veri satırları ve toplam satırlarıyla birlikte görmelisiniz.

## Pivot Tablo Görüntüsünü Dışa Aktar – Boyut ve DPI Özelleştirme

Varsayılan görüntü bazen bir sunum slaytı için çok küçük olur. Çözünürlüğü bir `ImageOrVectorSaveOptions` nesnesi geçirerek kontrol edebilirsiniz:

```csharp
using Aspose.Cells.Drawing;

// Define PNG options – 300 DPI for high‑quality print
ImageOrVectorSaveOptions options = new ImageOrVectorSaveOptions
{
    ImageFormat = ImageFormat.Png,
    Resolution = 300 // DPI
};

pivotImage.Save("YOUR_DIRECTORY/pivot_highres.png", options);
```

*Neden DPI ayarlamalısınız?* Daha yüksek DPI, özellikle PNG PowerPoint ya da PDF içinde ölçeklendirildiğinde kenarların daha keskin olmasını sağlar.

## Excel Aralığını PNG Olarak Kaydet – Birden Çok Çalışma Sayfası İşleme

Birden fazla sayfadan pivotları dışa aktarmanız gerekiyorsa, `Workbook.Worksheets` üzerinden döngü kurup adımları tekrarlayın. Kısa bir snippet:

```csharp
foreach (Worksheet ws in wb.Worksheets)
{
    foreach (PivotTable pt in ws.PivotTables)
    {
        Range refRange = pt.CreateReferenceRange();
        ImageOrVector img = refRange.ToImage();
        string fileName = $"pivot_{ws.Name}_{pt.Name}.png";
        img.Save($"YOUR_DIRECTORY/{fileName}");
        Console.WriteLine($"Saved {fileName}");
    }
}
```

Bu desen, çalışma kitabındaki **her pivot için pivot tablo görüntüsü dışa aktarır** ve dosya adını sayfa ve pivot adıyla oluşturur – toplu işlem için idealdir.

## Yaygın Tuzaklar ve Çözüm Önerileri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| `IndexOutOfRangeException` on `PivotTables[0]` | Çalışma sayfasında pivot tablo yok. | `worksheet.PivotTables.Count` değerini kontrol edip ardından erişin. |
| Boş görüntü çıktısı | Pivot, tüm satırları gizleyecek şekilde filtrelenmiş. | Pivotun görünür veri içerdiğinden emin olun veya `pivot.RefreshData();` metodunu `CreateReferenceRange()` öncesinde çağırın. |
| Düşük çözünürlüklü PNG | Varsayılan DPI 96. | Yukarıda gösterildiği gibi `ImageOrVectorSaveOptions.Resolution` ayarlayın. |
| Dosya yolu hataları | `YOUR_DIRECTORY` içinde geçersiz karakterler. | `Path.Combine` ve `Path.GetInvalidPathChars()` kullanarak yolu temizleyin. |

## Doğrulama – Hızlı Test

Tam örneği çalıştırdıktan sonra:

1. `pivot.png` dosyasını Windows Photo Viewer’da açın.  
2. Sütun başlıkları, veri satırları ve toplam satırların Excel görünümüyle eşleştiğini doğrulayın.  
3. Eksik satırlar görürseniz, `CreateReferenceRange()` öncesinde pivotun **RefreshData** metodunun çağrıldığını tekrar kontrol edin.

## Bonus: PNG’yi Word Belgesine Gömme

Görüntü zaten PNG olduğundan, doğrudan Aspose.Words’e besleyebilirsiniz:

```csharp
using Aspose.Words;
Document doc = new Document();
DocumentBuilder builder = new DocumentBuilder(doc);
builder.InsertImage("YOUR_DIRECTORY/pivot.png");
doc.Save("YOUR_DIRECTORY/report.docx");
```

Artık pivotun tam anlık görüntüsünü içeren bir Word raporunuz var – manuel kopyala‑yapıştıra gerek kalmadı.

## Sonuç

Aspose.Cells ile C#’ta **pivot referans aralığını oluşturmayı**, **pivot tablo görüntüsünü dışa aktarmayı** ve **Excel aralığını png olarak kaydetmeyi** öğrendiniz. Özetle:

- Görsel alanı izole etmek için `PivotTable.CreateReferenceRange()` kullanın.  
- Bu aralığı `Range.ToImage()` ile görüntüye dönüştürün.  
- PNG olarak kaydedin; isterseniz baskı kalitesi için DPI’yi ayarlayın.  

Bundan sonra toplu dışa aktarma, farklı görüntü formatları (SVG, JPEG) veya PNG’yi PDF/Word belgelerine gömme gibi konuları keşfedebilirsiniz. Pivotu statik bir grafik olarak yakaladığınızda olanaklar sınırsızdır.

Sorularınız veya zor bir senaryonuz mu var? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}