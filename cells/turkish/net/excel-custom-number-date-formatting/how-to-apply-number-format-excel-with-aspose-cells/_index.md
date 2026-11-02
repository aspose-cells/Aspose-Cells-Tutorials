---
category: general
date: 2026-10-10
description: Excel'de sayı biçimini hızlıca uygulamak için bir DataTable'ı içe aktarın,
  tarih ve para birimi biçimlerini ayarlayın ve başlık satırını koruyarak tek adımda
  gerçekleştirin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: tr
lastmod: 2026-10-10
og_description: C#'ta Aspose.Cells kullanarak Excel'de sayı formatı uygulayın. Excel'de
  tarih formatı ayarlamayı, para birimi formatı ayarlamayı ve bir DataTable içe aktarırken
  başlık satırını korumayı öğrenin.
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: C#'de Excel sayı formatı uygulama – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Aspose.Cells ile Excel’de sayı formatı nasıl uygulanır
url: /tr/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Excel'de sayı formatı nasıl uygulanır

Bir `DataTable`'dan veri yüklerken **apply number format excel** uygulamanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Ayrıca **set date format excel**, **set currency format excel** ve **preserve header row excel** nasıl yapılacağını öğrenecek ve içe aktarma sırasında sonuç çalışma sayfasının ekstra bir işlem yapmadan profesyonel görünmesini sağlayacaksınız.

Kütüphanenin kurulumundan tam, çalıştırılabilir bir kod parçacığı yazmaya kadar her şeyi ele alacağız. Sonunda herhangi bir `DataTable`'ı bir Excel çalışma kitabına aktarabilecek, sayısal sütunları otomatik olarak biçimlendirebilecek ve başlık satırını bozulmadan tutabileceksiniz — sadece birkaç C# satırıyla.

## Önkoşullar

* .NET 6.0 veya üzeri (kod .NET Framework 4.6+ ile de çalışır)
* Visual Studio 2022 (veya tercih ettiğiniz herhangi bir C# IDE)
* **Aspose.Cells for .NET** – NuGet üzerinden kurun:

```bash
dotnet add package Aspose.Cells
```

* Bir `DataTable` kaynağı – örnek, örnek veri döndüren `GetTable()` yardımcı metodunu kullanır.

> **Pro tip:** Aspose.Cells ticari bir kütüphanedir, ancak 30 güne kadar filigranı devre dışı bırakan ücretsiz bir değerlendirme modu sunar.

## Adım 1: Bir çalışma kitabı oluşturun ve ilk çalışma sayfasına erişin

Workbook nesnesi tüm Excel işlemleri için giriş noktasıdır. Yeni bir çalışma kitabı oluşturmak, size indeks 0'da varsayılan bir çalışma sayfası sağlar.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Bu adım neden?*  
`Workbook`, dosya formatını, hesaplama motorunu ve stil deposunu yönetir. `Worksheet`'e erken erişmek, hedef sayfayı daha sonra içe aktarma metoduna geçmemizi sağlar.

## Adım 2: Kaynak veriyi DataTable olarak alın

Gerçek projelerde veri genellikle bir veritabanı sorgusu, CSV ayrıştırıcısı veya bir API yanıtı ile gelir. Örnek olarak üç sütunlu basit bir `DataTable` oluşturuyoruz: **Product**, **Price** ve **ReleaseDate**.

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Bu adım neden?*  
`DataTable`, Aspose.Cells'in doğrudan içe aktarabileceği, sütun sırasını ve veri tiplerini koruyan tablo şeklinde bir bellek içi temsildir.

## Adım 3: `Style` dizisini hazırlayın – sütun başına bir stil

Aspose.Cells, içe aktarma sırasında `Style` nesnelerinden oluşan bir dizi geçirerek her sütuna ayrı bir stil uygulamanıza izin verir. Dizi uzunluğu, kaynak tablodaki sütun sayısıyla eşleşmelidir.

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Bu adım neden?*  
Açık oluşturmayı (`CreateStyle()`) atlayıp `Number` ayarlamaya çalışırsanız `NullReferenceException` hatası alırsınız. Her `Style` nesnesinin başlatılması, sonraki atamaların başarılı olmasını sağlar.

## Adım 4: Sayı formatlarını atayın – para birimi ve tarih

Excel, yerleşik sayı formatlarını kimlik (ID) ile tanımlar.

* **14** – Para birimi (örn., `$1,234.00`)
* **22** – Kısa Tarih (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Not:** Özel bir formata ihtiyacınız varsa (örn., `"¥#,##0.00"`), yerleşik bir ID yerine `Style.Custom = "¥#,##0.00"` kullanın.

*Bu adım neden?*  
İçe aktarma sırasında doğru **number format** uygulanması, hücreleri dolaşarak formatı değiştiren ikinci bir geçişe gerek kalmaz. Ayrıca **format excel cells date** ve **set currency format excel**'in tüm satırlarda tutarlı olmasını garanti eder.

## Adım 5: DataTable'ı içe aktarırken başlık satırını koruyun

`ImportDataTable` metodu veriyi kopyalayabilir, ilk satırı başlık olarak tutabilir ve hazırladığımız sütun stillerini uygulayabilir.

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Beklenen çıktı** – `FormattedReport.xlsx` dosyasını açın ve şunları göreceksiniz:

| Ürün    | Fiyat (para birimi) | Yayın Tarihi (tarih) |
|---------|---------------------|----------------------|
| Widget A| $12.99              | 05/01/2023           |
| Widget B| $23.50              | 06/15/2023           |
| Widget C| $7.75               | 07/30/2023           |

Başlık satırı bozulmamış, **Price** sütunu para birimi simgesini gösteriyor ve **ReleaseDate** sütunu kısa tarih formatını gösteriyor — ek bir stil koduna gerek kalmadan.

### Yaygın kenar durumlarını ele alma

| Durum                                   | Çözüm |
|----------------------------------------|----------|
| **Stil sayısından daha fazla sütun**   | `columnStyles.Length` değerinin `sourceTable.Columns.Count` ile eşleştiğinden emin olun. Eksik girişler, çalışma kitabının varsayılan stiline düşer. |
| **Sayısal sütunlarda null değerler**   | Excel, `null` değerini boş bir hücre olarak kabul eder; sayı formatı, daha sonra bir değer girildiğinde de geçerli olur. |
| **Özel yerel para birimi**              | `columnStyles[i].Custom = "\"€\"#,##0.00"` kullanın ve yerleşik kimliği devre dışı bırakmak için `columnStyles[i].Number = -1` ayarlayın. |
| **Büyük tablolar ( > 100 000 satır )**  | Veriyi akış olarak işlemek ve bellek yükünü azaltmak için `ImportTableOptions` ile `ImportDataTable` aşırı yüklemesini kullanmayı düşünün. |
| **Aynı stili birden fazla sütuna uygulama** | Dizide aynı `Style` örneğini yeniden kullanın (ör. `columnStyles[1] = columnStyles[2] = dateStyle;`). |

## Bonus: Özel bir format dizesi kullanma

Yerleşik kimlikler ihtiyaçlarınızı karşılamıyorsa, özel bir sayı formatı tanımlayabilirsiniz:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

Bu yaklaşım, önceden tanımlı kimliklerin ötesinde **format excel cells date** ve **set currency format excel** üzerinde tam kontrol sağlar.

## Sonuç

Artık Aspose.Cells ile bir `DataTable` içe aktarırken **apply number format excel**'i verimli bir şekilde nasıl uygulayacağınızı biliyorsunuz. Sütun başına bir `Style` dizisi oluşturarak, yerleşik veya özel sayı kimliklerini atayarak ve **preserve header row excel**'i sağlayan `ImportDataTable` aşırı yüklemesini kullanarak, tek bir işlemle yayımlamaya hazır çalışma sayfaları oluşturabilirsiniz.

### Sıradaki adım?

* `"dddd, mmmm dd, yyyy"` gibi özel desenlerle **set date format excel**'i keşfedin.
* Bu tekniği **conditional formatting** ile birleştirerek aralık dışı değerleri vurgulayın.
* Dinamik raporlama için pivot tablolarında veya grafiklerde **format excel cells date** kullanın.

Farklı sayı kimlikleri veya özel dizelerle kuruluşunuzun stil kılavuzuna uygun denemeler yapmaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}