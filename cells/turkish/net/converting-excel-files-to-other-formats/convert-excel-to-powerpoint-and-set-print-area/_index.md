---
category: general
date: 2026-10-10
description: Aspose.Cells ile C#'ta Excel'i PowerPoint'e dönüştürün ve yazdırma alanını
  ayarlayın – Excel'i nasıl dışa aktaracağınızı, yazdırma alanını nasıl ayarlayacağınızı
  ve bir PPTX dosyası nasıl oluşturacağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- set print area excel
- how to export excel
- how to set print area
- convert excel to pptx
language: tr
lastmod: 2026-10-10
og_description: Aspose.Cells ile Excel'i PowerPoint'e dönüştürün. Bu öğreticide, yazdırma
  alanını nasıl ayarlayacağınızı, Excel'i dışa aktaracağınızı ve C#'ta PPTX dosyası
  oluşturacağınızı gösterir.
og_image_alt: Screenshot of code that converts Excel to PowerPoint while setting the
  print area
og_title: Excel'i PowerPoint'e Dönüştür – C# Geliştiricileri için Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Convert Excel to PowerPoint and set print area in C# with Aspose.Cells
    – learn how to export Excel, set print area, and generate a PPTX file.
  headline: Convert Excel to PowerPoint and set print area
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- PowerPoint export
title: Excel'i PowerPoint'e dönüştür ve yazdırma alanını ayarla
url: /tr/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i PowerPoint'e Dönüştürme ve Yazdırma Alanını Ayarlama

If you need to **convert Excel to PowerPoint**, this guide shows you exactly how to do it in C#. By defining a print area first, you control which cells appear on each slide, and the final PPTX file matches your layout expectations. The solution also answers “how to export Excel” and “how to set print area” using the same code base.

Excel'i PowerPoint'e **convert Excel to PowerPoint** yapmanız gerekiyorsa, bu rehber C#'ta bunu tam olarak nasıl yapacağınızı gösterir. Önce bir yazdırma alanı tanımlayarak, her slaytta hangi hücrelerin görüneceğini kontrol eder ve son PPTX dosyası düzen beklentilerinize uyar. Çözüm aynı kod tabanını kullanarak “how to export Excel” ve “how to set print area” sorularına da yanıt verir.

In this tutorial you will:

* Load an existing workbook.
* Set the print area for a worksheet (the **set print area excel** step).
* Configure conversion options for PowerPoint output.
* Generate a **convert excel to pptx** file in a single method call.

Bu öğreticide şunları yapacaksınız:

* Mevcut bir çalışma kitabını yükleyin.
* Bir çalışma sayfası için yazdırma alanını ayarlayın (**set print area excel** adımı).
* PowerPoint çıktısı için dönüşüm seçeneklerini yapılandırın.
* Tek bir yöntem çağrısıyla **convert excel to pptx** dosyası oluşturun.

All required code is included, so you can copy, paste, and run it immediately.

Gerekli tüm kod dahil edilmiştir, böylece kopyalayıp yapıştırabilir ve hemen çalıştırabilirsiniz.

## Prerequisites

## Önkoşullar

Before you begin, make sure you have:

Başlamadan önce, şunların olduğundan emin olun:

| Requirement | Why it matters |
|-------------|----------------|
| **.NET 6.0 or later** | The sample targets .NET 6+, but any .NET version that supports C# 10 works. |
| **Aspose.Cells for .NET** | This library provides `Workbook`, `ImageOrPrintOptions`, and the `ConvertToPdf` (used for PPTX) method. Install it via NuGet: `dotnet add package Aspose.Cells` |
| **An input Excel file** | The tutorial uses `input.xlsx`. Place it in a folder you can reference from code. |
| **Write permission to the output folder** | The program writes `output.pptx`. Ensure the directory exists and is writable. |

| Gereksinim | Neden önemlidir |
|------------|-----------------|
| **.NET 6.0 or later** | Örnek .NET 6+ hedeflemektedir, ancak C# 10'ı destekleyen herhangi bir .NET sürümü çalışır. |
| **Aspose.Cells for .NET** | Bu kütüphane `Workbook`, `ImageOrPrintOptions` ve `ConvertToPdf` (PPTX için kullanılır) metodunu sağlar. NuGet üzerinden şu komutla kurun: `dotnet add package Aspose.Cells` |
| **An input Excel file** | Öğreticide `input.xlsx` dosyası kullanılır. Kodu referans alabileceğiniz bir klasöre yerleştirin. |
| **Write permission to the output folder** | Program `output.pptx` dosyasını yazar. Dizin mevcut ve yazılabilir olduğundan emin olun. |

> **Pro tip:** If you work with multiple worksheets, repeat the print‑area step for each sheet before conversion.

> **Pro tip:** Birden fazla çalışma sayfası ile çalışıyorsanız, dönüşümden önce her sayfa için yazdırma alanı adımını tekrarlayın.

## Step 1: Create a new C# console project

## Adım 1: Yeni bir C# konsol projesi oluşturun

Open a terminal or PowerShell window and run:

Bir terminal veya PowerShell penceresi açın ve şu komutu çalıştırın:

```bash
dotnet new console -n ExcelToPowerPointDemo
cd ExcelToPowerPointDemo
dotnet add package Aspose.Cells
```

This creates a fresh project named **ExcelToPowerPointDemo** and adds the Aspose.Cells package, which is the core dependency for **how to export Excel** to other formats.

Bu, **ExcelToPowerPointDemo** adlı yeni bir proje oluşturur ve Aspose.Cells paketini ekler; bu paket, **how to export Excel** işlemi için diğer formatlara temel bağımlılıktır.

## Step 2: Write the conversion code

## Adım 2: Dönüşüm kodunu yazın

Replace the content of `Program.cs` with the complete example below. The code demonstrates **convert excel to powerpoint**, shows **how to set print area**, and produces a **convert excel to pptx** file.

`Program.cs` dosyasının içeriğini aşağıdaki tam örnekle değiştirin. Kod, **convert excel to powerpoint** işlemini gösterir, **how to set print area**'ı gösterir ve bir **convert excel to pptx** dosyası üretir.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the workbook (how to export Excel)
            // -----------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(inputPath);
            Console.WriteLine($"Loaded workbook with {workbook.Worksheets.Count} worksheet(s).");

            // -----------------------------------------------------------------
            // 2️⃣ Define the print area for the first worksheet (set print area excel)
            // -----------------------------------------------------------------
            // The range "A1:G30" will be the only part visible on the slide.
            // Adjust the range to match the data you want to show.
            Worksheet sheet = workbook.Worksheets[0];
            sheet.PageSetup.PrintArea = "A1:G30";
            Console.WriteLine($"Print area set to {sheet.PageSetup.PrintArea} on sheet \"{sheet.Name}\".");

            // -----------------------------------------------------------------
            // 3️⃣ Configure conversion options for PowerPoint output
            // -----------------------------------------------------------------
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                // SaveFormat.Pptx tells Aspose.Cells to generate a PowerPoint file.
                SaveFormat = SaveFormat.Pptx,
                // Optional: set the slide size or DPI if needed.
                // HorizontalResolution = 300,
                // VerticalResolution = 300
            };

            // -----------------------------------------------------------------
            // 4️⃣ Convert the worksheet to a PowerPoint presentation (convert excel to powerpoint)
            // -----------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);
            Console.WriteLine($"Successfully created PowerPoint file at: {outputPath}");
        }
    }
}
```

### Why each part matters

### Her bir kısmın önemi

* **Loading the workbook** – This is the first step in any **how to export Excel** scenario. `Workbook` reads the file into memory, giving you full access to sheets, cells, and formatting.
* **Setting the print area** – By assigning `PageSetup.PrintArea`, you tell Aspose.Cells which cells to render. This is the core of **set print area excel**; without it, the entire sheet would be exported, potentially creating huge, unreadable slides.
* **Choosing `SaveFormat.Pptx`** – The `ImageOrPrintOptions` object lets you switch output formats. Setting `SaveFormat` to `Pptx` triggers the **convert excel to pptx** pipeline.
* **Calling `ConvertToPdf`** – Despite the method name, when `SaveFormat` is `Pptx` the library outputs a PowerPoint file. This is the recommended way to **convert excel to powerpoint** in a single call.

* **Loading the workbook** – Bu, herhangi bir **how to export Excel** senaryosundaki ilk adımdır. `Workbook` dosyayı belleğe okur ve sayfalara, hücrelere ve biçimlendirmeye tam erişim sağlar.
* **Setting the print area** – `PageSetup.PrintArea` atayarak Aspose.Cells'e hangi hücrelerin işleneceğini bildirirsiniz. Bu, **set print area excel**'in özüdür; olmadan tüm sayfa dışa aktarılır ve muhtemelen çok büyük, okunamaz slaytlar oluşur.
* **Choosing `SaveFormat.Pptx`** – `ImageOrPrintOptions` nesnesi çıktı formatlarını değiştirmenizi sağlar. `SaveFormat`'ı `Pptx` olarak ayarlamak **convert excel to pptx** işlem hattını tetikler.
* **Calling `ConvertToPdf`** – Metodun adı ne olursa olsun, `SaveFormat` `Pptx` olduğunda kütüphane bir PowerPoint dosyası üretir. Bu, **convert excel to powerpoint** işlemini tek bir çağrıda yapmanın önerilen yoludur.

## Step 3: Run the program

## Adım 3: Programı çalıştırın

From the project folder, execute:

Proje klasöründen şu komutu çalıştırın:

```bash
dotnet run
```

If everything is configured correctly, you should see console output similar to:

Her şey doğru yapılandırıldıysa, aşağıdaki gibi bir konsol çıktısı görmelisiniz:

```
Loaded workbook with 1 worksheet(s).
Print area set to A1:G30 on sheet "Sheet1".
Successfully created PowerPoint file at: YOUR_DIRECTORY\output.pptx
```

Open `output.pptx` in Microsoft PowerPoint or any compatible viewer. Each slide corresponds to the printed page of the worksheet, limited to the range you defined.

`output.pptx` dosyasını Microsoft PowerPoint ya da uyumlu bir görüntüleyicide açın. Her slayt, tanımladığınız aralığa sınırlı olarak çalışma sayfasının yazdırılan sayfasına karşılık gelir.

## Handling multiple worksheets

## Birden fazla çalışma sayfasını işleme

If your workbook contains more than one sheet and you want each sheet on its own slide deck, loop through the collection:

Çalışma kitabınız birden fazla sayfa içeriyorsa ve her sayfayı ayrı bir slayt seti olarak istiyorsanız, koleksiyon üzerinde döngü oluşturun:

```csharp
for (int i = 0; i < workbook.Worksheets.Count; i++)
{
    Worksheet ws = workbook.Worksheets[i];
    ws.PageSetup.PrintArea = "A1:G30"; // adjust per sheet if needed
    string slidePath = $@"YOUR_DIRECTORY\output_sheet{i + 1}.pptx";
    ws.ConvertToPdf(conversionOptions, slidePath);
    Console.WriteLine($"Created {slidePath}");
}
```

This pattern shows **how to export Excel** data sheet‑by‑sheet while still **setting print area** individually.

Bu desen, **how to export Excel** verilerini sayfa‑sayfa gösterirken **setting print area**'ı da ayrı ayrı ayarlamayı gösterir.

## Edge cases and best‑practice tips

## Kenar durumları ve en iyi uygulama ipuçları

| Situation | Recommended approach |
|-----------|----------------------|
| **Very large worksheets** | Reduce the print area or increase `HorizontalResolution`/`VerticalResolution` to keep the PPTX size manageable. |
| **Different page orientations** | Set `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` before conversion. |
| **Custom slide size** | Use `conversionOptions.OnePagePerSheet = false;` and adjust `conversionOptions.Width` / `conversionOptions.Height`. |
| **Missing input file** | Wrap the loading code in a `try { … } catch (FileNotFoundException)` block to provide a clear error message. |
| **Non‑ASCII characters** | Ensure the workbook is saved with UTF‑8 encoding; Aspose.Cells handles Unicode automatically. |

| Durum | Önerilen yaklaşım |
|-------|-------------------|
| **Very large worksheets** | Yazdırma alanını azaltın veya PPTX boyutunun yönetilebilir kalması için `HorizontalResolution`/`VerticalResolution` değerlerini artırın. |
| **Different page orientations** | Dönüşümden önce `sheet.PageSetup.Orientation = PageOrientationType.Landscape;` ayarlayın. |
| **Custom slide size** | `conversionOptions.OnePagePerSheet = false;` kullanın ve `conversionOptions.Width` / `conversionOptions.Height` değerlerini ayarlayın. |
| **Missing input file** | Yükleme kodunu `try { … } catch (FileNotFoundException)` bloğu içinde sararak net bir hata mesajı sağlayın. |
| **Non‑ASCII characters** | Çalışma kitabının UTF‑8 kodlamasıyla kaydedildiğinden emin olun; Aspose.Cells Unicode'u otomatik olarak işler. |

## Full source code for reference

## Referans için tam kaynak kodu

Below is the entire program, including `using` directives and comments. Save it as `Program.cs` inside the project created in **Step 1**.

Aşağıda, `using` yönergeleri ve yorumlar dahil olmak üzere tüm program yer almaktadır. **Adım 1**'de oluşturulan projenin içinde `Program.cs` olarak kaydedin.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the Excel file you want to convert.
            string inputPath = @"YOUR_DIRECTORY\input.xlsx";

            // 1️⃣ Load the workbook (how to export Excel)
            Workbook workbook = new Workbook(inputPath);

            // Select the first worksheet – you can loop for multiple sheets.
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Set the print area (set print area excel)
            sheet.PageSetup.PrintArea = "A1:G30";

            // 3️⃣ Prepare conversion options for PowerPoint output.
            ImageOrPrintOptions conversionOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx   // This triggers convert excel to pptx
            };

            // 4️⃣ Convert the worksheet to PowerPoint (convert excel to powerpoint)
            string outputPath = @"YOUR_DIRECTORY\output.pptx";
            sheet.ConvertToPdf(conversionOptions, outputPath);

            Console.WriteLine("Conversion complete.");
        }
    }
}
```

## Expected output

## Beklenen çıktı

Running the program produces a PowerPoint file (`output.pptx`) that contains:

Programı çalıştırmak, aşağıdakileri içeren bir PowerPoint dosyası (`output.pptx`) üretir:

* One slide per printed page of the worksheet.
* Only the cells inside **A1:G30** visible on each slide.
* Preserved formatting (fonts, colors, borders) as they appear in Excel.

* Çalışma sayfasının her yazdırılan sayfası için bir slayt.
* Her slaytta yalnızca **A1:G30** aralığındaki hücreler görünür.
* Excel'de göründüğü gibi biçimlendirme (yazı tipleri, renkler, kenarlıklar) korunur.

Open the file in PowerPoint to verify that the layout matches the defined print area.

Dosyayı PowerPoint'te açarak düzenin tanımlanan yazdırma alanına uygun olduğunu doğrulayın.

## Conclusion

## Sonuç

You now know how to **convert Excel to PowerPoint** while precisely **set print area excel** using Aspose.Cells in C#. The tutorial covered **how to export Excel**, demonstrated **how to set print area**, and showed the full **convert excel to pptx**


Artık Aspose.Cells kullanarak C#'ta **convert Excel to PowerPoint** yaparken **set print area excel**'i kesin bir şekilde ayarlamayı biliyorsunuz. Öğreticide **how to export Excel** ele alındı, **how to set print area** gösterildi ve tam **convert excel to pptx** örneği sunuldu.

## What Should You Learn Next?

## Sonra Ne Öğrenmelisiniz?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET Kullanarak Excel'de Yazdırma Alanı Nasıl Ayarlanır](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Excel'de Yazdırma Alanı Ayarlama ve PowerPoint'e Dışa Aktarma – Adım Adım Kılavuz](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Yazdırma Alanı Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}