---
category: general
date: 2026-11-19
description: C# ile Excel'de para birimi formatını ayarlayın – bir Excel çalışma sayfası
  içe aktarımı sırasında sayı formatını ve Excel sütunlarının stilini nasıl ayarlayacağınızı
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set currency format
- how to set number format
- assign number format
- excel worksheet import
- style excel columns
language: tr
lastmod: 2026-11-19
og_description: C# ile Excel’de para birimi formatını ayarlayın ve bir Excel çalışma
  sayfası içe aktarımı sırasında sayı formatını nasıl ayarlayacağınızı, sayı formatı
  atayacağınızı ve Excel sütunlarını nasıl biçimlendireceğinizi keşfedin.
og_image_alt: Screenshot showing Excel cells formatted as currency after import
og_title: C# ile Excel'de para birimi formatını ayarlayın – tam adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  headline: Set currency format while importing data into Excel using C#
  type: TechArticle
- description: Set currency format in Excel with C# – learn how to set number format
    and style excel columns during an excel worksheet import.
  name: Set currency format while importing data into Excel using C#
  steps:
  - name: Expected result
    text: 'When you open **FinancialReport.xlsx**, you’ll see:'
  - name: Assign number format to date columns
    text: '```csharp // Suppose column 2 contains dates and you want "dd-MMM-yyyy"
      columnStyles[2].Number = 14; // 14 = built‑in short date ```'
  - name: Use custom number formats for percentages
    text: '```csharp columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00% ```'
  - name: Styling beyond number formats
    text: 'You can also set font, background color, or alignment on the same `Style`
      object:'
  type: HowTo
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
- Formatting
title: C# kullanarak verileri Excel'e aktarırken para birimi formatını ayarlayın
url: /tr/net/excel-custom-number-date-formatting/set-currency-format-while-importing-data-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'e veri aktarırken C# ile para birimi biçimini ayarlama

Bir Excel çalışma sayfasında **para birimi biçimini ayarlamanız** gerektiğinde, bu kılavuz **sayı biçimini ayarlama** ve sütunları stilize etme adımlarını gösterir. `DataTable`'ın her sütununa doğru sayı biçimini atayan ve verileri istenen stil ile içe aktaran tam, çalıştırılabilir bir örnek göreceksiniz.

C# ile Excel üzerinde çalışmak, yalnızca ham değerleri dökmekten daha fazlasını gerektirir—sayıların nasıl görüneceğini de kontrol etmelisiniz. Faturalar, finansal raporlar veya gösterge tabloları oluştururken, para birimi, yüzde veya tarih biçimlendirmesini doğru yapmak çıktıyı anında okunabilir kılar.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 (veya daha yeni)  
* **Aspose.Cells for .NET** (veya `Style` sınıfı içinde `Number` özelliği bulunan herhangi bir kütüphane) referansı.  
  *NuGet*: `Install-Package Aspose.Cells`.  
* `DataTable` ve C# koleksiyonları hakkında temel bilgi.  
* Visual Studio 2022 veya VS Code gibi bir IDE.

## Adım 1: Çalışma sayfasına yazılacak verileri alın

Öncelikle dışa aktarmak istediğiniz ham verileri içeren bir `DataTable` elde edin. Gerçek projelerde bu, bir veritabanı sorgusu, bir API çağrısı veya bir CSV ayrıştırıcıdan gelebilir.

```csharp
using System.Data;

/// <summary>
/// Returns a sample DataTable with three columns:
/// Id (int), Amount (decimal), and Description (string).
/// </summary>
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Amount", typeof(decimal));
    table.Columns.Add("Description", typeof(string));

    // Sample rows
    table.Rows.Add(1, 1234.56m, "Office supplies");
    table.Rows.Add(2, 98765.43m, "Consulting fees");
    table.Rows.Add(3, 0.99m, "Miscellaneous");

    return table;
}

// Retrieve the data
DataTable dataTable = GetData();
```

> **Neden önemli:** Tamamen doldurulmuş bir `DataTable` içe aktarmak, veri‑alma mantığını Excel‑oluşturma mantığından ayırmanıza olanak tanır; bu da test edilebilirliği ve bakım kolaylığını artırır.

## Adım 2: Stil dizisi oluşturun – DataTable'daki her sütun için bir giriş

Aspose.Cells, içe aktaracağınız sütun sayısıyla aynı uzunlukta bir `Style[]` bekler. Her eleman belirli bir sayı biçimi tutabilir.

```csharp
// Allocate a Style object for each column
Style[] columnStyles = new Style[dataTable.Columns.Count];

// Initialize each Style instance (required before assigning properties)
for (int i = 0; i < columnStyles.Length; i++)
{
    columnStyles[i] = ws.Workbook.CreateStyle();
}
```

> **Profesyonel ipucu:** Sadece bir alt küme sütun için biçimlendirme ihtiyacınız olsa bile, her sütun için bir `Style` örneği oluşturmanız gerekir; aksi takdirde içe aktarım sırasında `NullReferenceException` alırsınız.

## Adım 3: İstenen sütunlara sayı biçimini atayın

Yerleşik stil numaraları kütüphaneye göre değişir. Aspose.Cells'ta:

* `0` → General (tam sayı)  
* `2` → Currency (ör. `$#,##0.00`)  
* `3` → Date, vb.

Burada iki sütuna **sayı biçimi** atıyoruz: ilk sütun (Id) tam sayı olarak kalırken, ikinci sütun (Amount) para birimi biçimi alıyor.

```csharp
// Column 0 → integer format (style number 0)
columnStyles[0].Number = 0;

// Column 1 → currency format (style number 2)
columnStyles[1].Number = 2;

// If you need a custom format, you can also use a format string:
// columnStyles[1].Custom = "$#,##0.00";
```

> **Sayı biçimini nasıl ayarlarsınız:** `Number` özelliğini kullanmak, yerleşik bir biçimi seçmenin en hızlı yoludur. Bölge‑spesifik para birimleri için, uygun para birimi simgesini içeren özel bir biçim dizesi kullanmayı düşünün.

## Adım 4: DataTable'ı çalışma sayfasına içe aktarın, sütun stillerini uygulayın

Stil dizisi hazır olduğuna göre, verileri içe aktarın. `ImportDataTable` yöntemi, gönderdiğiniz stilleri dikkate alır.

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet ws = workbook.Worksheets[0];

// Import the DataTable, starting at cell A1 (row 0, column 0)
// The third argument (true) tells the method to write column headers.
ws.Cells.ImportDataTable(
    dataTable,
    /* includeColumnNames */ true,
    /* startRow */ 0,
    /* startColumn */ 0,
    columnStyles);

// Save the workbook
workbook.Save("FinancialReport.xlsx", SaveFormat.Xlsx);
```

### Beklenen sonuç

**FinancialReport.xlsx** dosyasını açtığınızda şunları görmelisiniz:

| Id | Amount      | Description      |
|----|------------|------------------|
| 1  | $1,234.56  | Office supplies |
| 2  | $98,765.43 | Consulting fees |
| 3  | $0.99      | Miscellaneous    |

* **Amount** sütunu, ayarladığınız para birimi biçimiyle gösterilirken, **Id** tam sayı olarak kalır.*

## Ek senaryolar için sayı biçimini nasıl ayarlarsınız

### Tarih sütunlarına sayı biçimi atama

```csharp
// Suppose column 2 contains dates and you want "dd-MMM-yyyy"
columnStyles[2].Number = 14; // 14 = built‑in short date
```

### Yüzde için özel sayı biçimleri kullanma

```csharp
columnStyles[3].Custom = "0.00%"; // Shows 0.75 as 75.00%
```

### Sayı biçimlerinin ötesinde stil uygulama

Aynı `Style` nesnesi üzerinde yazı tipi, arka plan rengi veya hizalama da ayarlanabilir:

```csharp
columnStyles[1].Font.IsBold = true;
columnStyles[1].ForegroundColor = Color.LightYellow;
columnStyles[1].HorizontalAlignment = TextAlignmentType.Center;
```

> **Neden işe yarar:** `Style` nesnesi bir hücrenin tüm görsel özelliklerini toplar. Diziyi `ImportDataTable`'a gönderdiğinizde, her hücre tanımlı stili otomatik olarak devralır.

## Yaygın tuzaklar ve nasıl önlenir

| Tuzak | Belirti | Çözüm |
|---------|---------|-----|
| Her `Style` örneği oluşturulmayı unutmak | `NullReferenceException` içe aktarımda | Dizi üzerinde döngü kurup `CreateStyle()` çağırarak özellikleri ayarlamadan önce örnek oluşturun. |
| Yanlış yerleşik sayı indeksini kullanmak | Yanlış biçim (ör. tarihlerin tam sayı olarak görünmesi) | Doğru `Number` sabitleri için kütüphane dokümantasyonuna bakın. |
| Çalışma kitabını kaydetmemek | Çıktı dosyası yok ya da boş dosya | İçe aktarım tamamlandıktan sonra `workbook.Save(...)` çağırın. |
| Para birimi simgesi için bölge uyumsuzluğu | `$` sembolü ABD dışı bölgelerde görünür | Uygun sembolü içeren özel bir biçim dizesi kullanın (ör. `"€#,##0.00"`). |

## Tam, çalıştırılabilir örnek



## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Create excel file c# – style cells and set currency format](/cells/english/net/excel-formatting-and-styling/create-excel-file-c-style-cells-and-set-currency-format/)
- [How to Format Excel Columns in C# – Complete Guide](/cells/english/net/formatting-rows-and-columns-in-excel/how-to-format-excel-columns-in-c-complete-guide/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}