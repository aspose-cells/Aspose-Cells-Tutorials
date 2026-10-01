---
category: general
date: 2026-10-01
description: C# kullanarak Excel'de değişen sütun renkleri – DataTable'dan bir Excel
  dosyası oluşturmayı, C# ile hücre arka plan rengini ayarlamayı ve stil verilmiş
  sütunlarla DataTable'ı Excel'e aktarmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- alternating column colors excel
- set cell background color c#
- create excel file from datatable c#
- import datatable to excel
language: tr
lastmod: 2026-10-01
og_description: Excel'de değişen sütun renkleri artık çok kolay. Bu rehberi izleyerek
  bir DataTable'dan Excel dosyası oluşturun, hücre arka plan rengini C# ile ayarlayın
  ve stilize sütunlarla DataTable'ı Excel'e aktarın.
og_image_alt: Screenshot of an Excel sheet showing alternating column colors applied
  by C# code
og_title: C# ile Excel'de alternatif sütun renkleri ekleyin – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: alternating column colors excel using C# – learn to create an Excel
    file from a DataTable, set cell background color c#, and import datatable to excel
    with styled columns.
  headline: How to add alternating column colors in Excel using C#
  type: TechArticle
tags:
- C#
- Excel automation
- Aspose.Cells
title: C# kullanarak Excel'de alternatif sütun renkleri ekleme
url: /tr/net/excel-colors-and-background-settings/how-to-add-alternating-column-colors-in-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# kullanarak Excel'de alternatif sütun renkleri nasıl eklenir

Uygulamanızdan oluşturulan bir raporda **alternating column colors excel** ihtiyacınız varsa, bu kılavuz size eksiksiz bir çözüm gösterir. `DataTable`'dan bir Excel dosyası oluşturmayı, hücre arka plan rengini C# stiliyle ayarlamayı ve her sütuna ayrı bir stil uygulayarak datatable'ı Excel'e aktarmayı göreceksiniz.

Bu öğretici ihtiyacınız olan her şeyi kapsar: gerekli NuGet paketleri, tam ve çalıştırılabilir bir kod örneği ve her adımın neden önemli olduğuna dair açıklamalar. Sonunda, doğrudan Microsoft Excel'de açılabilen stillendirilmiş bir çalışma kitabına sahip olacaksınız.

## Önkoşullar

* .NET 6.0 (veya daha yeni) SDK yüklü  
* Visual Studio 2022 (veya C# uyumlu herhangi bir IDE)  
* **Aspose.Cells for .NET** kütüphanesi – şu şekilde kurun  

```bash
dotnet add package Aspose.Cells
```

Aspose.Cells, örnekte kullanılan `Workbook`, `Worksheet`, `Style` ve `BackgroundType` sınıflarını sağlar.

## Adım 1: Kaynak veriyi `DataTable` olarak alın

İlk görev, dışa aktarmak istediğiniz veriyi elde etmektir. Gerçek projelerde `DataTable`'ı bir veritabanı sorgusu, bir API çağrısı veya herhangi bir bellek içi koleksiyonla doldurabilirsiniz.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetData()
{
    // Create a sample DataTable with three columns and five rows
    DataTable table = new DataTable("Sample");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    for (int i = 1; i <= 5; i++)
    {
        table.Rows.Add(i, $"Student {i}", 60 + i * 5);
    }
    return table;
}
```

**Bu neden önemlidir:**  
`DataTable`, Excel çalışma sayfasına sorunsuz bir şekilde eşlenen evrensel bir konteynerdir. `DataTable` kullanarak **create excel file from datatable c#** ifadesiyle her sütun için özel döngüler yazmadan Excel dosyası oluşturabilirsiniz.

## Adım 2: Yeni bir çalışma kitabı oluşturun ve ilk çalışma sayfasını alın

```csharp
// Initialize a new workbook – this represents the Excel file
Workbook workbook = new Workbook();

// The first worksheet is created by default
Worksheet worksheet = workbook.Worksheets[0];
```

**Açıklama:**  
`Workbook` kök nesnedir; `Worksheets[0]` verinin yerleştirileceği varsayılan sayfayı verir.

## Adım 3: Her sütun için ayrı bir stil hazırlayın (alternatif arka plan renkleri)

**alternating column colors excel** elde etmek için her sütun için bir `Style` oluşturur ve iki ton arasında değişen açık bir arka plan rengi atarız.

```csharp
// Determine how many columns we have
int columnCount = dataTable.Columns.Count;
Style[] columnStyles = new Style[columnCount];

// Create a style for each column
for (int i = 0; i < columnCount; i++)
{
    // Create a fresh style instance
    Style style = workbook.CreateStyle();

    // Alternate between LightYellow and LightCyan
    style.ForegroundColor = (i % 2 == 0)
        ? System.Drawing.Color.LightYellow
        : System.Drawing.Color.LightCyan;

    // Use a solid fill pattern
    style.Pattern = BackgroundType.Solid;

    columnStyles[i] = style;
}
```

**Neden bir döngü kullanıyoruz:**  
Döngü, çalışma zamanında sütun sayısı değişse bile **set cell background color c#** ifadesinin tutarlı bir şekilde uygulanmasını garanti eder. Bu, çözümü dinamik raporlar için sağlam kılar.

## Adım 4: `DataTable`'ı çalışma sayfasına aktarın, sütun stillerini uygulayarak

Aspose.Cells, bir `DataTable`'ı doğrudan içe aktarabilir ve her sütunu renklendirmek için stil dizisini geçebiliriz.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// The second argument (true) tells the API to add column headers
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Arka planda ne olur:**  
`ImportDataTable` başlık satırını, ardından her veri satırını yazar. `columnStyles` sağladığımız için, belirli bir sütundaki her hücre ilgili stili alır ve istenen alternatif renkleri elde ederiz.

## Adım 5: Stil verilen çalışma kitabını bir dosyaya kaydedin

```csharp
// Choose an output path – adjust as needed for your environment
string outputPath = @"C:\Temp\StyledTable.xlsx";
workbook.Save(outputPath);

Console.WriteLine($"Workbook saved to {outputPath}");
```

*StyledTable.xlsx* dosyasını Excel'de açtığınızda, her sütunun alternatif olarak gölgelendiğini göreceksiniz, bu da tabloyu okumayı kolaylaştırır.

## Tam, çalıştırılabilir örnek

Tüm parçaları bir araya getirerek, kopyalayıp yapıştırıp çalıştırabileceğiniz bağımsız bir program aşağıdadır.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Get the source data
        DataTable dataTable = GetData();

        // Step 2: Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 3: Build alternating column styles
        int columnCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++)
        {
            Style style = workbook.CreateStyle();
            style.ForegroundColor = (i % 2 == 0)
                ? System.Drawing.Color.LightYellow
                : System.Drawing.Color.LightCyan;
            style.Pattern = BackgroundType.Solid;
            columnStyles[i] = style;
        }

        // Step 4: Import DataTable with styles
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

        // Step 5: Save the file
        string outputPath = @"C:\Temp\StyledTable.xlsx";
        workbook.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }

    static DataTable GetData()
    {
        DataTable table = new DataTable("Students");
        table.Columns.Add("Id", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        for (int i = 1; i <= 5; i++)
        {
            table.Rows.Add(i, $"Student {i}", 60 + i * 5);
        }
        return table;
    }
}
```

### Beklenen çıktı

* `C:\Temp\` konumunda **StyledTable.xlsx** adlı bir dosya.  
* Çalışma sayfası, `Id`, `Name`, `Score` olmak üzere üç sütunu alternatif arka plan renkleriyle gösterir: 1. ve 3. sütun *LightYellow*, 2. sütun *LightCyan*.  
* `DataTable`'daki tüm satırlar başlık satırının altında görünür.

## Yaygın sorular ve kenar durumları

| Soru | Cevap |
|----------|--------|
| *Başka renkler kullanabilir miyim?* | Evet. `System.Drawing.Color.LightYellow` ve `LightCyan` yerine herhangi bir `System.Drawing.Color` değerini kullanın. |
| *DataTable'da çok sayıda sütun olursa ne olur?* | Döngü otomatik olarak her sütun için bir stil oluşturur, bu yüzden desen kod değişikliği olmadan ölçeklenir. |
| *Workbook'u dispose etmem gerekiyor mu?* | Aspose.Cells `IDisposable` uygular. `Workbook`'u bir `using` bloğu içinde sararsanız kaynaklar hemen serbest bırakılır. |
| *Aynı alternatif renkleri sütunlar yerine satırlara nasıl uygularım?* | Satırlar için bir `Style[]` oluşturun ve `worksheet.Cells.ImportDataTable(..., rowStyles)` çağırın – Aspose.Cells aşırı yüklemeleri her ikisini de destekler. |
| *Dosyayı doğrudan bir akıma (ör. bir web API için) yazabilir miyim?* | Evet. Dosya yolunun yerine `workbook.Save(stream, SaveFormat.Xlsx);` kullanın. |

## Alandan ipuçları

* **Pro tip:** Tek bir çalıştırmada birden fazla çalışma sayfası oluşturuyorsanız stil nesnelerini önbelleğe alın – bir stil oluşturmak nispeten ucuzdur, ancak yeniden kullanmak bellek tüketimini azaltır.  
* **Dikkat:** `System.Drawing.Color`'ı Windows dışı platformlarda kullanırken `System.Drawing.Common` NuGet paketini ekleyin ve çalışma zamanının GDI+ desteklediğinden emin olun.

## Sonuç

Artık C#'ta bir `DataTable`'dan Excel dosyası oluşturarak, Aspose.Cells ile hücre arka plan renklerini ayarlayarak ve stil verilen bir sütun dizisiyle **import datatable to excel** yaparak **alternating column colors excel** elde etmeyi biliyorsunuz. Bu yaklaşım hızlı, sürdürülebilir ve herhangi bir veri seti boyutunda çalışır.

### Sonraki adımlar

* **set cell background color c#**'ı koşullu biçimlendirme için keşfedin (ör. düşük puanları vurgulama).  
* Bu tekniği **create excel file from datatable c#** ile birleştirerek çok sayfalı raporlar oluşturun.  
* Aynı çalışma kitabına görsel özetler eklemek için Aspose.Cells’ın grafik API'sine bakın.

Renkleri, dosya formatını veya veri kaynağını projenizin ihtiyaçlarına göre uyarlamaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [C# ile Excel'de Sütun Arka Planını Ayarlama – Tam Kılavuz](/cells/english/net/excel-colors-and-background-settings/set-column-background-in-excel-with-c-complete-guide/)
- [Excel'de arka plan rengi ekle – C#'ta Alternatif Satır Stilleri](/cells/english/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/)
- [Workbook Oluşturma C# – Stil ile DataTable'ı Excel'e Aktarma](/cells/english/net/excel-data-import-export/create-workbook-c-import-datatable-to-excel-with-styles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}