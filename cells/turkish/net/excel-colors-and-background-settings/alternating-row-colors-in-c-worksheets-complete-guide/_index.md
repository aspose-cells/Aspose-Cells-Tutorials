---
category: general
date: 2026-05-30
description: C# çalışma sayfalarında alternatif satır renkleri eklemeyi, hücre arka
  planını katı dolgu deseniyle ayarlamayı ve çalışma sayfası hücre stilini zahmetsizce
  özelleştirmeyi öğrenin.
draft: false
keywords:
- alternating row colors
- set cell background
- solid fill pattern
- add background color
- worksheet cell style
language: tr
og_description: C# çalışma sayfalarında satır renklerini değiştirmek artık çok kolay.
  Hücre arka planını ayarlamayı, katı dolgu desenini kullanmayı öğrenin ve çalışma
  sayfası hücre stilinde uzmanlaşın.
og_title: C# Çalışma Sayfalarında Alternatif Satır Renkleri – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  headline: Alternating Row Colors in C# Worksheets – Complete Guide
  type: TechArticle
- description: Learn how to add alternating row colors in C# worksheets, set cell
    background with a solid fill pattern, and customize worksheet cell style effortlessly.
  name: Alternating Row Colors in C# Worksheets – Complete Guide
  steps:
  - name: Why Use a **Solid Fill Pattern**?
    text: The `Pattern` property tells the engine how to render the color. A `Solid`
      fill guarantees that the entire cell background is painted, eliminating any
      faint gridlines that might otherwise show through. This is the most common way
      to **set cell background** when you want a clean look.
  - name: Change the Colors
    text: 'If your brand uses different hues, just replace `Color.LightYellow` and
      `Color.LightCyan` with any `System.Drawing.Color` you prefer. For example:'
  - name: Use a Different **Background Type**
    text: While `BackgroundType.Solid` is the most common, you can experiment with
      `BackgroundType.Gray125`, `BackgroundType.Horizontal`, or any pattern that the
      library supports. This changes the visual texture while still **adding background
      color**.
  - name: Apply a **Worksheet Cell Style** to Specific Columns
    text: 'Sometimes you only want the alternating effect on data columns, leaving
      the first column (e.g., IDs) untouched. Create a separate style for that column
      and assign it after the import:'
  type: HowTo
tags:
- C#
- Excel
- Aspose.Cells
- DataTable
- Styling
title: C# Çalışma Sayfalarında Alternatif Satır Renkleri – Tam Kılavuz
url: /tr/net/excel-colors-and-background-settings/alternating-row-colors-in-c-worksheets-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# Çalışma Sayfalarında Satır Renklerini Değiştirme – Tam Kılavuz

Excel dışa aktarmalarınızı **alternating row colors** kullanarak nasıl daha şık hale getirebileceğinizi hiç merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli olarak satırlara *add background color* eklemenin, milyonlarca satır kod yazmadan nasıl yapılacağını soruyor.  

Bu öğreticide, her satırda **set cell background** yapmanın, bir **solid fill pattern** uygulamanın ve **worksheet cell style** kontrol etmenin basit bir yolunu adım adım göstereceğiz, böylece sonuç hem okunaklı hem de görsel olarak çekici olacak.

## Öğrenecekleriniz

- `DataTable` içine veri alın (veya herhangi bir tablo kaynağı).  
- İki renk arasında değişen bir `Style` nesneleri dizisi oluşturun.  
- Bu stilleri uygularken `DataTable`'ı bir çalışma sayfasına aktarın.  
- Çıktıyı doğrulayın ve gerekirse renkleri veya desenleri ayarlayın.  

Örneklerde **Aspose.Cells** kullanacağız) bir .NET ortamı ve bir elektronik tablo kütüphanesi dışında dış araçlara ihtiyaç yoktur. Sonunda, herhangi bir raporlama hattına ekleyebileceğiniz yeniden kullanılabilir bir yönteme sahip olacaksınız.

---

## Adım 1: Kaynak Veriyi `DataTable` Olarak Alın

İlk önce, veri olmadan stil verilecek bir şey yoktur. Aşağıda örnek satırlarla bir `DataTable` oluşturan küçük bir yardımcı bulunmaktadır. Gerçek bir projede bunu bir veritabanı çağrısı veya CSV ayrıştırıcı ile değiştirirsiniz.

```csharp
using System;
using System.Data;

static DataTable GetData()
{
    // Create a simple table with three columns
    DataTable table = new DataTable("Report");
    table.Columns.Add("ID", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with dummy rows
    for (int i = 1; i <= 10; i++)
    {
        table.Rows.Add(i, $"Item {i}", Math.Round(new Random().NextDouble() * 100, 2));
    }

    return table;
}
```

> **Neden önemli:** Verinin bir `DataTable` içinde olması, çalışma sayfası motorunun onu tek bir çağrıda *import* (içe aktarmasını) sağlar ve sütun adlarını ve veri tiplerini otomatik olarak korur.

## Adım 2: **Alternating Row Colors** Stilleri Oluşturun

Şimdi, satır başına bir `Style` nesnesi içeren bir dizi oluşturacağız; çift satırlar açık sarı bir ton alırken tek satırlar hafif bir camgöbeği alır. Bu, **alternating row colors** tekniğinin özüdür.

```csharp
using Aspose.Cells;
using System.Drawing;

// Assume workbook and worksheet are already instantiated
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Retrieve data
DataTable dataTable = GetData();

// Prepare an array of styles – one for each row in the table
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style for the current row
    rowStyles[i] = workbook.CreateStyle();

    // **Add background color**: LightYellow for even rows, LightCyan for odd rows
    rowStyles[i].ForegroundColor = (i % 2 == 0)
        ? Color.LightYellow
        : Color.LightCyan;

    // **Set cell background** using a **solid fill pattern**
    rowStyles[i].Pattern = BackgroundType.Solid;

    // Optional: you could also set font color, borders, etc., here
}
```

### Neden **Solid Fill Pattern** Kullanılır?

`Pattern` özelliği, motorun rengi nasıl çizeceğini belirtir. `Solid` dolgu, tüm hücre arka planının boyanmasını garanti eder ve aksi takdirde görülebilecek hafif ızgara çizgilerini ortadan kaldırır. Temiz bir görünüm istediğinizde **set cell background** (hücre arka planını ayarlama) için en yaygın yöntem budur.

## Adım 3: Hazırlanan Stillerle `DataTable`'ı İçe Aktarın

Stil dizisi hazır olduğunda, içe aktarma çağrısı tek satır haline gelir. Aspose.Cells, her satıra karşılık gelen stili otomatik olarak uygular.

```csharp
// Import the DataTable into the worksheet, applying the prepared styles
worksheet.Cells.ImportDataTable(
    dataTable,                     // source
    true,                          // include column names
    0,                             // start row (0‑based)
    0,                             // start column (0‑based)
    rowStyles);                    // array of styles
```

> **Arka planda ne olur?**  
> Kütüphane her satırı iterasyonla dolaşır, değerleri hücrelere kopyalar ve ardından `rowStyles` içindeki eşleşen `Style`ı uygular. Zaten bir **solid fill pattern** tanımladığımız için, bir satırdaki her hücre aynı arka plan rengini devralır ve size mükemmel **alternating row colors** sağlar.

## Adım 4: Çalışma Kitabını Kaydedin ve Sonucu Doğrulayın

Hızlı bir kaydetme, dosyayı Excel'de (veya uyumlu herhangi bir görüntüleyicide) açıp etkiyi görmenizi sağlar.

```csharp
// Save to disk – you can change the format to .xlsx, .xls, .csv, etc.
workbook.Save("AlternatingRowsReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Workbook saved. Open 'AlternatingRowsReport.xlsx' to see the result.");
```

Dosyayı açtığınızda, 1, 3, 5… satırları açık sarı, 2, 4, 6… satırları ise açık camgöbeği olacaktır. Sütun başlıkları beyaz kalır, veriyi öne çıkarır.

![Alternatif satır renklerini gösteren çalışma sayfası](/images/alternating-row-colors.png "Alternatif satır renklerine sahip çalışma sayfasının ekran görüntüsü")

*Görsel alt metni:* **alternating row colors** ekran görüntüsü, her satırın arka planının açık sarı ve açık camgöbeği arasında değiştiği bir çalışma sayfası.

## Adım 5: Daha Fazla Özelleştirme (İsteğe Bağlı)

### Renkleri Değiştirin

Markanız farklı tonlar kullanıyorsa, sadece `Color.LightYellow` ve `Color.LightCyan` ifadelerini istediğiniz herhangi bir `System.Drawing.Color` ile değiştirin. Örneğin:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.FromArgb(255, 235, 205) // Peach
                                            : Color.FromArgb(205, 235, 255); // Soft blue
```

### Farklı Bir **Background Type** Kullanma

`BackgroundType.Solid` en yaygın olmakla birlikte, `BackgroundType.Gray125`, `BackgroundType.Horizontal` veya kütüphanenin desteklediği herhangi bir desenle deney yapabilirsiniz. Bu, görsel dokuyu değiştirir ve hâlâ **adding background color** (arka plan rengi ekleme) sağlar.

### Belirli Sütunlara **Worksheet Cell Style** Uygulama

Bazen sadece veri sütunlarında alternatif efekti istiyorsunuz, ilk sütunu (ör. ID'ler) dokunulmaz bırakıyorsunuz. O sütun için ayrı bir stil oluşturun ve içe aktarmadan sonra atayın:

```csharp
Style idStyle = workbook.CreateStyle();
idStyle.ForegroundColor = Color.White;
idStyle.Pattern = BackgroundType.Solid;

// Apply to the first column (A)
for (int row = 0; row < dataTable.Rows.Count + 1; row++) // +1 for header
{
    worksheet.Cells[row, 0].SetStyle(idStyle);
}
```

---

## Sonuç

Artık C# çalışma sayfalarında **alternating row colors** için eksiksiz, yeniden kullanılabilir bir çözümünüz var. `Style` nesneleri dizisi oluşturarak, **set cell background** (hücre arka planını ayarlama) **solid fill pattern** (katı dolgu deseni) ile ve `DataTable`'ı tek bir çağrıda içe aktararak, minimum kodla profesyonel görünümlü raporlar üretebilirsiniz.

Bundan sonra şunları yapabilirsiniz:

- **Add background color** (arka plan rengi ekleme) başlık satırlarına ekstra vurgu için.  
- Tekniği koşullu biçimlendirme ile birleştirerek dinamik görsel ipuçları ekleyin.  
- Yazı tipleri, kenarlıklar veya sayı biçimleri gibi diğer **worksheet cell style** (çalışma sayfası hücre stili) özelliklerini keşfedin.

Bir sonraki dışa aktarma rutininizde deneyin—kullanıcılarınız daha temiz ve okunaklı elektronik tablolar için size teşekkür edecek. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

- [Aspose.Cells for .NET ile Çalışma Sayfasında Satır Yüksekliğini Ayarlama](/cells/english/net/size-and-spacing-customization/setting-height-of-all-rows-in-worksheet/)
- [Aspose.Cells for .NET Kullanarak Excel Hücre Adlarını Satır ve Sütun İndekslerine Dönüştürme](/cells/english/net/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-dotnet/)
- [Aspose.Cells .NET ile Excel'de Çalışma Sayfası Sekmesi Renklerini Ayarlama - Kapsamlı Rehber](/cells/english/net/worksheet-management/set-worksheet-tab-colors-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}