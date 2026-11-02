---
category: general
date: 2026-09-18
description: Aspose.Cells ile Excel'den PowerPoint oluşturun – özet tabloları kopyalayın,
  aralıkları dışa aktarın ve birkaç satır C# koduyla PPTX olarak kaydedin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: tr
lastmod: 2026-09-18
og_description: Excel'den hızlıca PowerPoint oluşturun. Pivot tabloları kopyalamayı,
  aralıkları dışa aktarmayı ve bir çalışma kitabını PPTX olarak kaydetmeyi Aspose.Cells
  ile öğrenin.
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Aspose.Cells ile Excel'den PowerPoint Oluşturma – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Aspose.Cells kullanarak Excel'den PowerPoint nasıl oluşturulur
url: /tr/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'den PowerPoint Oluşturma Aspose.Cells Kullanarak

Excel'den PowerPoint oluşturmanız gerekiyorsa, bu kılavuz size kısa ve uçtan uca bir çözüm gösterir. Bir pivot tabloyu nasıl kopyalayacağınızı, seçili bir aralığı nasıl dışa aktaracağınızı ve sonucu sadece birkaç C# satırıyla PPTX dosyası olarak nasıl kaydedeceğinizi göreceksiniz.

Veri tablosundan doğrudan bir slayt destesi oluşturmak, raporlama iş akışlarını yavaşlatan manuel kopyala‑yapıştır adımını ortadan kaldırır. Bu öğretici, proje kurulumundan son PPTX dosyasına kadar ihtiyacınız olan her şeyi kapsar ve en yeni Aspose.Cells for .NET ile çalışır.

## Prerequisites

Başlamadan önce şunların yüklü olduğundan emin olun:

* **Aspose.Cells for .NET** (sürüm 23.12 veya daha yeni). NuGet üzerinden kurun: `Install-Package Aspose.Cells`.
* **.NET 6+** geliştirme ortamı (Visual Studio 2022 veya VS Code yeterlidir).
* Veri ve yeniden kullanmak istediğiniz pivot tabloyu içeren bir Excel çalışma kitabı (`Source.xlsx`).
* Çıktı klasörüne yazma izni.

Ek bir üçüncü‑taraf kütüphanesi gerekmez.

## Create PowerPoint from Excel – step‑by‑step

İşlem, daha sonra göreceğiniz kod örneğiyle doğrudan eşleşen dört mantıksal adımdan oluşur.

### Step 1: Load the source workbook and define the range

Kaynak veriyi ve pivot tabloyu içeren çalışma kitabını yüklemelisiniz. Kesin bir aralık seçmek, yalnızca gerekli hücrelerin aktarılmasını sağlar ve ortaya çıkan slaytın hafif kalmasını sağlar.

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**Why this matters:**  
`CreateRange` bir `Range` nesnesi oluşturur ve bu nesne bütün olarak kopyalanabilir. Aralığı `A1:G20` ile sınırlayarak, aksi takdirde PowerPoint dosyasını şişirebilecek alakasız hücreleri çekmekten kaçınırsınız.

### Step 2: Prepare the destination workbook

Aspose.Cells, PPTX formatında kaydettiğinizde bir PowerPoint slaytını bir çalışma kitabı olarak ele alır. Yeni bir çalışma kitabı oluşturmak, kopyalanan aralık için temiz bir tuval sağlar.

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**Tip:** Birden fazla slayt ihtiyacınız varsa, ek çalışma sayfaları ekleyebilir ve daha sonra her birini ayrı bir PPTX dosyası olarak kaydedebilirsiniz.

### Step 3: Copy the range while preserving the pivot table

`CopyRange` yöntemi bir `PasteOptions` nesnesi alır. `CopyPivotTables = true` ayarı, Aspose.Cells'in sadece render edilmiş değerleri değil, pivot tablo yapısını da korumasını sağlar.

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**How it works:**  
`CopyPivotTables` true olduğunda, hedef sayfa hem kaynak veriyi hem de pivot önbelleğini alır. Bu, pivot tablonun tam fonksiyonel kalmasını ve kaynak veri değiştiğinde daha sonra yenilenebilmesini sağlar.

### Step 4: Save the workbook as a PowerPoint file

Son olarak, çalışma kitabını PPTX formatına dışa aktarın. `SaveFormat.Pptx` bayrağı, Aspose.Cells'in çalışma sayfasını bir PowerPoint slaytı olarak yazmasını söyler.

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**Result:**  
`CopyWithPivot.pptx` Microsoft PowerPoint (veya uyumlu bir görüntüleyici) içinde tek bir slayt olarak açılır; bu slayt kopyalanan aralığı, içinde canlı bir pivot tabloyla birlikte, PowerPoint içinde etkileşimli olarak gösterir.

## Full runnable example

Aşağıda, yeni bir konsol projesine yapıştırıp hemen çalıştırabileceğiniz tam program yer almaktadır.

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**Expected output:**  
Program çalıştırıldığında “PowerPoint file created successfully.” mesajı basılır ve `CopyWithPivot.pptx` adlı bir dosya üretilir. PowerPoint’te dosyayı açtığınızda, kopyalanan Excel aralığının kaynak çalışma sayfasındaki gibi göründüğü, içinde aktif bir pivot tablonun bulunduğu tek bir slayt gösterilir; bu pivot tablo PowerPoint içinde yenilenebilir.

## Common variations and edge cases

| Situation | What to change |
|-----------|----------------|
| **Multiple pivot tables** | Her tablo için ayrı `Range` nesneleri tanımlayın ve her biri için `CopyRange` çağırın, ya da aynı veri kaynağını paylaşıyorsa tüm sayfayı kopyalayın. |
| **Large data sets** | Aralığı artırın (ör. `"A1:Z5000"`). PPTX boyutunu azaltmak için `PasteOptions.CompressData = true` etkinleştirmeyi düşünün. |
| **Different slide layouts** | PPTX olarak kaydettikten sonra dosyayı PowerPoint’te açıp özel bir düzen veya tema uygulayın; veri düzenlenebilir kalır. |
| **Saving to a stream** | PPTX’i bir web API üzerinden döndürmeniz gerektiğinde `destinationWorkbook.Save(stream, SaveFormat.Pptx)` kullanın. |
| **Preserving cell formatting** | Fontları, renkleri ve kenarlıkları korumak için `PasteOptions.PasteType = PasteType.All` ayarlayın. |

**Pro tip:** `Save` metodunu çağırmadan önce hedef klasörün var olduğundan emin olun. Klasör eksikse, `Save` bir `DirectoryNotFoundException` fırlatır.

## Conclusion

Artık Aspose.Cells kullanarak Excel'den PowerPoint oluşturmayı, bir pivot tabloyu kopyalamayı ve sonucu PPTX dosyası olarak dışa aktarmayı biliyorsunuz. Kaynak çalışma kitabını yükleme, bir aralık tanımlama, `CopyPivotTables` ile kopyalama ve PPTX olarak kaydetme adımları, güvenilir ve üretim‑hazır bir iş akışını tamamen kapsar.

Sonraki adımda, **birden fazla çalışma sayfası için Excel’i PPTX’e dışa aktarma** ya da **birden fazla kaynaktan veri birleştirerek slayt destesi oluşturma** konularını keşfedin. Her iki konu da aynı API yüzeyine dayanır ve karmaşık raporlama hatlarını otomatikleştirmek için birleştirilebilir.

İyi kodlamalar ve elektronik tablolarınızı şık sunumlara dönüştürmenin tadını çıkarın!


## What Should You Learn Next?


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakın ilişkili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [How to Copy Pivot Table in C# – Convert Excel to PPTX, Copy Range & Make Textbox](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [Create New Workbook – How to Copy a Worksheet with a Pivot Table](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [How to Create and Save Excel Files with Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}