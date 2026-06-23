---
category: general
date: 2026-06-08
description: C# ve Aspose.Cells kullanarak Excel aralığını görüntü olarak dışa aktarın.
  Excel çalışma sayfasını sadece birkaç basit adımda görüntü olarak kaydetmeyi öğrenin.
draft: false
keywords:
- export excel range as image
- save excel worksheet as image
- Aspose.Cells image export
- C# Excel automation
- pivot table to image
language: tr
og_description: C# ile Excel aralığını resim olarak dışa aktar. Bu öğretici, Excel
  çalışma sayfasını hızlı ve güvenilir bir şekilde resim olarak kaydetmenizi gösterir.
og_title: Excel Aralığını Görüntü Olarak Dışa Aktar – Tam C# Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  headline: Export Excel Range as Image – Complete C# Guide
  type: TechArticle
- description: Export Excel range as image using C# and Aspose.Cells. Learn how to
    save Excel worksheet as image in just a few simple steps.
  name: Export Excel Range as Image – Complete C# Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - Aspose.Cells
      for .NET ≥ 23.9 (you can grab a free trial from the Aspose website). - A basic
      understanding of C# and file I/O.'
  - name: What the code does
    text: '- `exportRange.ToImage` captures only the cells inside the range (pivot
      table or custom block). - `worksheet.ToImage` captures the *entire* visible
      area of the worksheet, effectively **save excel worksheet as image**.'
  - name: Multiple Pivot Tables
    text: 'If your workbook contains more than one pivot table, you can loop through
      them:'
  - name: Very Large Ranges
    text: 'Exporting a massive range (e.g., thousands of rows) can consume a lot of
      memory. Mitigate this by:'
  - name: Transparent Backgrounds
    text: 'If you need a transparent background (useful for overlaying on web pages),
      set the background color to `Color.Transparent` before export:'
  - name: File Permissions
    text: Make sure the target directory exists and your process has write permission.
      Otherwise `ToImage` throws an `IOException`.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel
- ImageExport
title: Excel Aralığını Görüntü Olarak Dışa Aktarma – Tam C# Rehberi
url: /tr/net/image-and-chart-operations/export-excel-range-as-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Aralığını Görüntü Olarak Dışa Aktarma – Tam C# Rehberi

Hiç **export Excel range as image** yapmanız gerekti ama hangi API çağrısını kullanacağınızdan emin değildiniz mi? Yalnız değilsiniz. Raporlama panosu oluşturuyor olun ya da bir PowerPoint slaytı için pivot tablonun bir anlık görüntüsüne ihtiyacınız olsun, bir hücre bloğunu PNG'ye dönüştürmek kullanışlı bir hiledir.

Bu rehberde, yalnızca **export excel range as image** yapmakla kalmayıp aynı zamanda tüm sayfa için **save excel worksheet as image** nasıl yapılacağını gösteren bağımsız bir örnek üzerinden ilerleyeceğiz. Harici betikler yok, sadece saf C# ve Aspose.Cells, böylece kodu kopyalayıp yapıştırabilir ve anında çalıştığını görebilirsiniz.

## Öğrenecekleriniz

- Mevcut bir çalışma kitabını yükleyin ve belirli bir aralığı (pivot tablo veya herhangi bir hücre bloğu) bulun.  
- Format, çözünürlük ve ölçekleme gibi görüntü dışa aktarma seçeneklerini yapılandırın.  
- Tek bir aralığı PNG, JPEG veya BMP olarak dışa aktarın.  
- Aynı mantığı tek satırda **save excel worksheet as image** olarak genişletin.  
- Birden fazla pivot tablo, büyük aralıklar ve yaygın tuzaklarla başa çıkmak için ipuçları.

### Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır).  
- Aspose.Cells for .NET ≥ 23.9 (Aspose web sitesinden ücretsiz deneme alabilirsiniz).  
- C# ve dosya I/O konusunda temel bir anlayış.  

Eğer bunlara sahipseniz, başlayalım.

## Adım 1: Projeyi Kurun ve Ad Alanlarını İçe Aktarın

İlk olarak, yeni bir konsol uygulaması oluşturun (veya kodu mevcut bir projeye entegre edin). Aspose.Cells NuGet paketini ekleyin:

```bash
dotnet add package Aspose.Cells
```

Ardından gerekli ad alanlarını kapsam içine alın:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;   // For ImageOrPrintOptions
using System.Drawing.Imaging; // For ImageFormat enum
```

> **Pro ipucu:** `using` ifadelerinizi dosyanın en üstünde tutun; bu, kodu taramayı kolaylaştırır—özellikle daha sonra daha fazla Aspose özelliği eklediğinizde.

## Adım 2: Hedef Aralığı İçeren Çalışma Kitabını Yükleyin

Diskte bir çalışma kitabına ihtiyacınız var. `YOUR_DIRECTORY/input.xlsx` ifadesini dosyanızın gerçek yolu ile değiştirin.

```csharp
// Step 2: Load the workbook containing the data you want to capture
Workbook workbook = new Workbook(@"YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – make sure the file loaded correctly
if (workbook == null)
{
    Console.WriteLine("Failed to load workbook. Check the file path.");
    return;
}
```

Bu adımın önemi: `Workbook` nesnesi, her Aspose.Cells işleminin giriş noktasıdır. Onsuz çalışma sayfalarına, aralıklara veya pivot tablolara referans veremezsiniz.

## Adım 3: Dışa Aktarılacak Aralığı Belirleyin

İki yaygın senaryonuz var:

1. **Belirli bir pivot tablo** – gönderdiğiniz kod `PivotTables[0].PivotTableRange` kullanır.  
2. **İsteğe bağlı bir hücre bloğu** – `worksheet.Cells.CreateRange("B2:D10")` kullanabilirsiniz.

Aşağıda ikisini de ele alıyoruz, böylece ihtiyacınıza uygun olanı seçebilirsiniz.

```csharp
// Step 3a: Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];

// Option A: Export the first pivot table's range
Range exportRange;
if (worksheet.PivotTables.Count > 0)
{
    exportRange = worksheet.PivotTables[0].PivotTableRange;
}
else
{
    // Option B: Fallback to a manual range (e.g., B2:D10)
    exportRange = worksheet.Cells.CreateRange("B2:D10");
}
```

> **Pivot tabloları önce kontrol etmemizin nedeni:** Birçok raporlama dosyası dinamik pivot verilerine dayanır. Hiçbiri yoksa, geri dönüş mekanizması öğreticinin hâlâ çalışmasını sağlar.

## Adım 4: Görüntü Dışa Aktarma Seçeneklerini Yapılandırın

Aspose.Cells, çıktı görüntüsü üzerinde ayrıntılı kontrol sağlar. En yaygın ayarlar format, çözünürlük (DPI) ve ızgara çizgilerini dahil edip etmeme seçenekleridir.

```csharp
// Step 4: Set up image export options
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG works well for lossless quality
    HorizontalResolution = 300,      // 300 DPI for crisp prints
    VerticalResolution = 300,
    // Optional: uncomment to hide gridlines
    // IsGridlinesVisible = false
};
```

`ImageFormat.Jpeg` veya `ImageFormat.Bmp` değerlerine geçebilirsiniz, eğer sonraki sisteminiz bu türleri tercih ediyorsa. DPI ayarı, görüntüyü yüksek çözünürlüklü PDF'lere veya slayt setlerine gömmeniz gerektiğinde önemlidir.

## Adım 5: Aralığı (veya Tüm Çalışma Sayfasını) Görüntü Olarak Dışa Aktarın

Şimdi sihir gerçekleşir. `ToImage` yöntemi, aralığın görsel temsilini doğrudan diske yazar.

```csharp
// Step 5a: Export the selected range to an image file
string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
exportRange.ToImage(rangeImagePath, imgOptions);
Console.WriteLine($"Range exported to: {rangeImagePath}");

// Step 5b: If you need to **save excel worksheet as image**, use the worksheet's ToImage overload
string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";
worksheet.ToImage(sheetImagePath, imgOptions);
Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
```

### Kodun yaptığı şey

- `exportRange.ToImage` sadece aralık içindeki hücreleri (pivot tablo veya özel blok) yakalar.  
- `worksheet.ToImage` çalışma sayfasının *tüm* görünen alanını yakalar, etkili bir şekilde **save excel worksheet as image**.  

Her iki çağrı da daha önce ayarladığınız seçeneklere saygı gösterir—bu sayede 300 DPI çözünürlüklü PNG dosyaları elde edersiniz.

## Kenar Durumlarını ve Yaygın Soruları Ele Alma

### Birden Çok Pivot Tablo

Çalışma kitabınız birden fazla pivot tablo içeriyorsa, bunlar üzerinde döngü kurabilirsiniz:

```csharp
for (int i = 0; i < worksheet.PivotTables.Count; i++)
{
    Range ptRange = worksheet.PivotTables[i].PivotTableRange;
    string outPath = $@"YOUR_DIRECTORY/Pivot_{i}.png";
    ptRange.ToImage(outPath, imgOptions);
    Console.WriteLine($"Pivot {i} saved to {outPath}");
}
```

### Çok Büyük Aralıklar

Milyonlarca satır gibi devasa bir aralığı dışa aktarmak çok fazla bellek tüketebilir. Bunu azaltmak için:

- `HorizontalResolution` / `VerticalResolution` değerlerini azaltmak.  
- Bölümlere ayırarak dışa aktarmak (aralığı daha küçük bloklara bölmek).  

### Şeffaf Arka Planlar

Şeffaf bir arka plana ihtiyacınız varsa (web sayfalarına bindirme için faydalı), dışa aktarmadan önce arka plan rengini `Color.Transparent` olarak ayarlayın:

```csharp
imgOptions.BackgroundColor = System.Drawing.Color.Transparent;
```

### Dosya İzinleri

Hedef dizinin mevcut olduğundan ve işleminizin yazma iznine sahip olduğundan emin olun. Aksi takdirde `ToImage` bir `IOException` fırlatır.

## Tam Çalışan Örnek

Hepsini bir araya getirerek, işte çalıştırmaya hazır bir konsol programı:

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System.Drawing.Imaging;

namespace ExcelImageExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths for your environment
            string inputPath = @"YOUR_DIRECTORY/input.xlsx";
            string rangeImagePath = @"YOUR_DIRECTORY/PivotRange.png";
            string sheetImagePath = @"YOUR_DIRECTORY/FullSheet.png";

            // Load workbook
            Workbook workbook = new Workbook(inputPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // Determine which range to export
            Range exportRange;
            if (worksheet.PivotTables.Count > 0)
            {
                exportRange = worksheet.PivotTables[0].PivotTableRange;
            }
            else
            {
                exportRange = worksheet.Cells.CreateRange("B2:D10");
            }

            // Configure image options
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions
            {
                ImageFormat = ImageFormat.Png,
                HorizontalResolution = 300,
                VerticalResolution = 300
            };

            // Export range as image
            exportRange.ToImage(rangeImagePath, imgOptions);
            Console.WriteLine($"Range exported to: {rangeImagePath}");

            // Export entire worksheet as image
            worksheet.ToImage(sheetImagePath, imgOptions);
            Console.WriteLine($"Worksheet exported to: {sheetImagePath}");
        }
    }
}
```

**Beklenen çıktı** (konsol):

```
Range exported to: YOUR_DIRECTORY/PivotRange.png
Worksheet exported to: YOUR_DIRECTORY/FullSheet.png
```

Oluşturulan PNG dosyalarını açın ve seçilen aralığın ve tam sayfanın piksel mükemmel bir anlık görüntüsünü göreceksiniz.

## Sonuç

Aspose.Cells ve C# kullanarak **export excel range as image** ve ayrıca **save excel worksheet as image** yapmak için ihtiyacınız olan her şeyi ele aldık. Çalışma kitabını yüklemekten görüntü seçeneklerini ince ayarlamaya ve birden çok pivotla başa çıkmaya kadar adımlar basit ve tamamen tekrarlanabilir.

Sonra şunları yapmak isteyebilirsiniz:

- `ImageFormat` değerleriyle (JPEG, BMP) denemeler yapın.  
- Rapor oluşturmak için görüntüyü `Document` sınıfı ile bir PDF'e birleştirin.  
- Bir klasördeki dosyalar topluluğu için süreci otomatikleştirin.

Kod parçacığını kendi iş akışınıza uyarlamaktan çekinmeyin—görüntüleri bir web API'sine gönderiyor, e-postalara gömüyor ya da yazdırılabilir raporlar oluşturuyorsanız. Kodlamaktan keyif alın ve görüntüler Excel verilerinizi konuşsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Export Excel Cells to Image Using Aspose.Cells .NET&#58; A Step-by-Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}