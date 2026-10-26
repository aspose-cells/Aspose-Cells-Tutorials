---
category: general
date: 2026-10-26
description: WRAPCOLS'i C#'ta bir aralığı sütunlara bölmek, satırlar için WRAPROWS'u
  uygulamak ve çalışma kitabını programlı olarak XLSX olarak kaydetmek konusunda bilgi
  edinin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: tr
lastmod: 2026-10-26
og_description: C#'ta WRAPCOLS'i kullanarak verileri sütunlara bölme, WRAPROWS'i satırlar
  için kullanma ve çalışma kitabını XLSX olarak kaydetme. Tam adım adım rehberi izleyin.
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: C#'de WRAPCOLS Nasıl Kullanılır – Aralıkları Böl ve XLSX Olarak Kaydet
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: C#'de WRAPCOLS nasıl kullanılır ve çalışma kitabı XLSX olarak nasıl kaydedilir
url: /tr/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta WRAPCOLS Nasıl Kullanılır ve Çalışma Kitabı XLSX Olarak Kaydedilir

Excel dosyasındaki verileri yeniden düzenlemek için **how to use WRAPCOLS**'a ihtiyacınız varsa, bu kılavuz size eksiksiz, çalıştırılabilir bir çözüm gösterir. **excel wrapcols example**'ı görecek, **split range into rows**'u WRAPROWS ile nasıl öğrenip, **save workbook as XLSX** ile bitireceksiniz—tümü **programmatically** yapılır.

C#'tan Excel ile çalışmak genellikle bir çalışma kitabı oluşturmayı, formüller uygulamayı ve dosyayı kalıcı hale getirmeyi içerir. Aşağıdaki kod, Microsoft Office kurulu olmadan Excel dosyalarını manipüle etmenizi sağlayan Aspose.Cells kütüphanesini kullanır. Bu öğreticinin sonunda **create excel workbook programmatically** yapabilecek, verileri hem yatay hem dikey olarak bölebilecek ve sonraki işlemler için hazır temiz bir `.xlsx` dosyası üretebileceksiniz.

## Prerequisites

Before you start, make sure you have:

* .NET 6.0 veya daha yeni (kod ayrıca .NET Framework 4.7+ ile de çalışır)
* Aspose.Cells NuGet paketine bir referans  
  ```bash
  dotnet add package Aspose.Cells
  ```
* C# ve Excel formüllerine temel aşinalık

## Adım 1: WRAPCOLS'ı Kullanarak Bir Aralığı Sütunlara Bölme

The **WRAPCOLS** function takes a one‑dimensional range and spreads its values across the specified number of columns. In this example we start with values in `A1:A10` and ask WRAPCOLS to create three columns.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **Result:** `C1:E4` hücreleri artık orijinal on öğeyi üç sütunda düzenlenmiş şekilde içerir (son sütun kalan öğeleri tutar).

![Excel'de bir aralığı sütunlara bölmek için WRAPCOLS kullanımını gösteren ekran görüntüsü](image-url.png)

## Adım 2: WRAPROWS ile Aralığı Satırlara Bölme

While **WRAPCOLS** works horizontally, **WRAPROWS** performs the opposite: it spreads a range across a given number of rows. Here we take values from `B1:B10` and arrange them into two rows starting at `F1`.

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **Result:** Formül, `F1:K2` hücrelerini iki satırda dağıtılmış on değerle doldurur.

## Adım 3: Çalışma Kitabını XLSX Olarak Kaydetme

After applying the formulas, the final step is to persist the file. The **save workbook as xlsx** operation writes the in‑memory workbook to disk in the modern OpenXML format.

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### Kaydedilen Dosyanın Görünümü

When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:

| C | D | E |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
|        |        | Item 10 |

and

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| Value 1 | Value 3 | Value 5 | Value 7 | Value 9 | |
| Value 2 | Value 4 | Value 6 | Value 8 | Value 10 | |

Formüller hücrelerde kalır, böylece kaynak aralıklardaki sonraki değişiklikler otomatik olarak yansıtılır.

## Adım 4: Yaygın Varyasyonlar ve Kenar Durumları

### Sütun veya Satır Sayısını Değiştirme

* **More columns:** `WRAPCOLS`'ın ikinci argümanını artırın.  
  Örnek: `=WRAPCOLS(A1:A10,5)` beş sütun oluşturur, veri bittiğinde boş hücreler bırakır.
* **Dynamic column count:** Sabit bir sayı yerine hücre referansı kullanın.  
  `=WRAPCOLS(A1:A10, G1)` burada `G1` istenen sütun sayısını tutar.

### Boş veya Sayısal Olmayan Hücreleri İşleme

WRAPCOLS ve WRAPROWS varsayılan olarak boş hücreleri yok sayar, ancak boş olmayan değerlerin sırasını korur. Boşlukları korumanız gerekiyorsa, WRAPCOLS uygulamadan önce kaynak aralığı `IFERROR` veya `TEXT` işlevleriyle sarmalayın.

### Diğer Formatlarda Kaydetme

While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells supports many formats (`.xls`, `.csv`, `.pdf`, etc.):

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## Pro İpuçları ve Tuzaklar

* **Pro tip:** Kaydetmeden hemen sonra formülleri değerlendirmeyi planlıyorsanız `Workbook.Settings.CalcEngineEnabled = true` ayarlayın.
* **Watch out for:** Büyük kaynak aralıkları çok büyük dökülen alanlar oluşturabilir, bu da performansı etkileyebilir. Aralık boyutunu sınırlayın veya işlemi birden fazla çalışma sayfasına bölün.
* **Thread safety:** Aspose.Cells nesneleri **thread‑safe** değildir. Dosyaları paralel işliyorsanız her iş parçacığı için ayrı bir `Workbook` örneği oluşturun.

## Sonuç

Artık **how to use WRAPCOLS**'ı kullanarak dikey bir aralığı birden fazla sütuna bölmeyi, **split range into rows**'u WRAPROWS ile nasıl yapacağınızı ve bu dönüşümleri yaptıktan sonra **save workbook as XLSX**'i nasıl gerçekleştireceğinizi biliyorsunuz. Yukarıdaki adımları izleyerek **create excel workbook programmatically** yapabilir, güçlü dökülen formüller uygulayabilir ve manuel müdahale olmadan paylaşılmaya hazır Excel dosyaları oluşturabilirsiniz.

### Sıradaki Ne?

* **conditional formatting**'i keşfederek dökülen verileri vurgulayın.
* **WRAPCOLS**'ı **SORT** veya **FILTER** ile birleştirerek dinamik panolar oluşturun.
* Aspose.Cells'in **charting API**'sini kullanarak yeniden düzenlenen verileri doğrudan koddan görselleştirin.

Kodlamaktan keyif alın ve Excel iş akışlarınızı otomatikleştirmenin tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [C#'ta wrapcols nasıl kullanılır – Excel WRAPROWS ve Formülleri Yeniden Hesaplama ile Tam Kılavuz](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [C#'ta WRAPCOLS Nasıl Kullanılır – Excel'de Bir Diziyi Matrise Dönüştürme](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [WRAPCOLS Nasıl Kullanılır – C# Excel Otomasyonu için Tam Kılavuz](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}