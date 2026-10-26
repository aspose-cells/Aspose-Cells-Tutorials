---
category: general
date: 2026-10-26
description: ExportAsStrin kullanıldığında Özel ExportTableOptions, Excel verilerini
  C#'ta string olarak dışa aktarmanıza olanak tanır. Dışa aktarmayı yapılandırmak
  ve çalıştırmak için adım adım kılavuzu izleyin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Custom ExportTableOptions when ExportAsStrin
- how to export excel as string
- ExportTableOptions C#
- Excel to DataTable string conversion
- Aspose.Cells export as string
language: tr
lastmod: 2026-10-26
og_description: ExportAsStrin etkinleştirildiğinde, özel ExportTableOptions yalnızca
  metin içeren Excel dışa aktarımını sağlar. C#'ta dışa aktarmayı yapılandırma ve
  çalıştırma adımlarını öğrenin.
og_image_alt: Code snippet showing ExportTableOptions configuration for string export
og_title: ExportAsStrin sırasında Özel ExportTableOptions – C#'ta Excel'i dize olarak
  dışa aktar
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Custom ExportTableOptions when ExportAsStrin lets you export Excel
    data as strings in C#. Follow the step‑by‑step guide to configure and run the
    export.
  headline: Custom ExportTableOptions when ExportAsStrin for Excel
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: Excel için ExportAsStrin sırasında Özel ExportTableOptions
url: /tr/net/excel-data-export-retrieval/custom-exporttableoptions-when-exportasstrin-for-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Custom ExportTableOptions when ExportAsStrin – Excel'i C#'ta string olarak dışa aktar

Eğer **Custom ExportTableOptions when ExportAsStrin** kullanarak her hücre değerini düz bir string olarak elde etmeniz gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Veri içe aktarma hattı oluşturuyor olun ya da temiz bir CSV hazır dökümüne ihtiyacınız olsun, seçenekleri bu şekilde yapılandırmanın tip dönüşümü sürprizlerinden nasıl kaçındığını göreceksiniz.

Bu öğreticide Aspose.Cells kütüphanesini kullanarak **Excel'i string olarak dışa aktarmayı** öğrenecek, tam ve çalıştırılabilir kodu görecek ve her ayarın arkasındaki mantığı anlayacaksınız. Harici bir belgeye ihtiyaç yok – ihtiyacınız olan her şey burada.

## Prerequisites

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 SDK veya daha yeni bir sürüm yüklü  
* Visual Studio 2022 (veya .NET'i destekleyen herhangi bir IDE)  
* Aspose.Cells for .NET paketi (NuGet üzerinden kurun: `Install-Package Aspose.Cells`)  
* Projenin kök klasörüne yerleştirilmiş bir Excel çalışma kitabı (`sample.xlsx`)  

Bu öğeler tek bağımlılıklar olup; kod Windows, Linux veya macOS üzerinde ek kütüphaneler olmadan çalışır.

## Adım 1: Dışa aktarmak istediğiniz çalışma kitabını yükleyin

**Custom ExportTableOptions when ExportAsStrin** kullanırken ilk yaptığınız şey, yüklü bir çalışma kitabından bir `Worksheet` nesnesi elde etmektir. Bu nesne satırlara, sütunlara ve dışa aktarma API'sine erişim sağlar.

```csharp
using Aspose.Cells;
using System.Data;

// Load the workbook from disk
Workbook workbook = new Workbook("sample.xlsx");

// Get the first worksheet (index 0)
Worksheet worksheet = workbook.Worksheets[0];
```

*Why this matters:*  
`Workbook` dosyayı bir kez okur ve tüm biçimlendirme bilgilerini bellekte tutar. Belirli bir `Worksheet` seçerek dışa aktarma kapsamını sınırlarsınız ve gizli sayfaların gereksiz işlenmesini önlersiniz.

## Adım 2: ExportAsString = true ile ExportTableOptions'ı yapılandırın

**Custom ExportTableOptions when ExportAsStrin**'in çekirdeği `ExportTableOptions` nesnesidir. `ExportAsString` ayarlandığında, dışa aktarıcı her hücreyi orijinal veri tipine (tarih, sayı, boolean vb.) bakmaksızın bir string olarak ele alır. `PreserveFormatting` etkinleştirildiğinde, ortaya çıkan string içinde görsel stil (ör. para birimi sembolleri) korunur.

```csharp
// Create and configure the export options
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export every cell value as a string
    PreserveFormatting = true      // Keep the original cell formatting
};
```

*Why this matters:*  
Daha sonra `ExportDataTable` çağırdığınızda, kütüphane normalde her sütunun .NET tipini tahmin etmeye çalışır. `ExportAsString = true` ile bu tahmin adımı atlanır ve aşağı akış CSV ayrıştırıcılarını bozabilecek beklenmedik `DateTime` veya `double` dönüşümleri önlenir.

## Adım 3: Özel seçenekleri kullanarak bir aralığı DataTable'a dışa aktar

Artık çalışma sayfasından dikdörtgen bir aralığı (satırlar 0‑9, sütunlar 0‑4) dışa aktarabilirsiniz. Metot, her alanın `string` olduğu bir `DataTable` döndürür.

```csharp
// Export rows 0‑9 and columns 0‑4 (5 columns total) as a DataTable
DataTable dataTable = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 10,
    totalColumns: 5,
    options: exportOptions);
```

*Why this matters:*  
`ExportDataTable`, Excel verilerini birçok .NET API'sinin (ör. Entity Framework, Dapper) zaten anladığı ilişkisel bir yapıya taşımak için en uygun yoldur. **Custom ExportTableOptions when ExportAsStrin**'i geçirerek, her `DataColumn.DataType`'ın `typeof(string)` olmasını garantilersiniz.

## Adım 4: Sonucu doğrulayın – tüm değerler string

Dışa aktarmanın beklendiği gibi çalıştığını doğrulamak iyi bir uygulamadır. Aşağıdaki döngü her hücreyi ve çalışma zamanındaki tipini yazdırır.

```csharp
Console.WriteLine("Exported DataTable (all values as strings):");
foreach (DataRow row in dataTable.Rows)
{
    for (int i = 0; i < dataTable.Columns.Count; i++)
    {
        object value = row[i];
        Console.Write($"{value} ({value.GetType().Name})\t");
    }
    Console.WriteLine();
}
```

**Expected output**

```
123 (String)    2023‑01‑15 (String)    $45.67 (String)    TRUE (String)    Sample text (String)
...
```

Her hücre tip olarak `String` gösterir, bu da **Custom ExportTableOptions when ExportAsStrin**'in doğru çalıştığını doğrular.

## Adım 5: İsteğe Bağlı – DataTable'ı CSV'ye yazdır

Eğer nihai hedefiniz düz metin bir dosya ise, `DataTable`'ı kolayca CSV'ye serileştirebilirsiniz:



## Sonraki Öğrenmeniz Gerekenler?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla birlikte tam çalışan kod örnekleri içerir ve ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [Aspose.Cells for .NET kullanarak Excel'ten DataTable'a HTML String'leri Dışa Aktarma: Adım Adım Kılavuz](/cells/english/net/import-export/export-html-strings-excel-datatable-aspose-cells-net/)
- [Excel PDF Özel Özelliklerini Dışa Aktarma – Aspose Cells Net](/cells/hongkong/net/workbook-operations/export-custom-properties-excel-pdf-aspose-cells-net/)
- [Aspose Cells Java Özel Yükleme Filtreleri ile Excel Dışa Aktarma](/cells/hongkong/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}