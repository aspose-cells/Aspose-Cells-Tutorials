---
category: general
date: 2026-02-09
description: C#'ta açık mavi arka planlı bir çalışma kitabı oluşturma ve başlıklarla
  veri içe aktarma. Açık mavi arka plan eklemeyi, varsayılan Excel stilini kullanmayı
  ve veri tablosunu içe aktarmayı öğrenin.
draft: false
keywords:
- how to create workbook
- add light blue background
- import data with headers
- excel import datatable c#
- use default style excel
language: tr
og_description: C#'ta açık mavi arka planlı bir çalışma kitabı oluşturma, başlıklarla
  veri içe aktarma ve varsayılan Excel stilini uygulama—hepsi tek bir özlü rehberde.
og_title: Çalışma Kitabı Nasıl Oluşturulur – Açık Mavi Arka Plan, Veri İçe Aktarma
tags:
- C#
- Excel
- Aspose.Cells
title: Çalışma Kitabı Nasıl Oluşturulur – Açık Mavi Arka Plan, Veri İçe Aktarma
url: /tr/net/excel-data-import-export/how-to-create-workbook-light-blue-background-data-import/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabı Nasıl Oluşturulur – Açık Mavi Arka Plan, Veri İçe Aktarma

C#'ta **how to create workbook**'in kutudan çıktığı gibi biraz daha şık görünmesini hiç merak ettiniz mi? Belki bir veritabanından bir `DataTable` çektiniz ve sıradan, varsayılan beyaz hücrelerden sıkıldınız. Bu öğreticide yeni bir çalışma kitabı oluşturmayı, bir sütuna açık mavi arka plan eklemeyi ve başlıklarla veri içe aktarmayı adım adım göstereceğiz — tüm bunları Excel'in sağladığı varsayılan stil ile yapacağız.

Ayrıca birkaç “what‑if” senaryosu ekleyeceğiz; örneğin null değerleri işlemek ya da birden fazla sütunu özelleştirmek gibi. Sonunda, paydaşlara herhangi bir son işlem yapmadan gönderebileceğiniz tamamen stillendirilmiş bir Excel dosyanız olacak.

## Önkoşullar

* **.NET 6+** (kod .NET Framework 4.6+ üzerinde de çalışır)  
* **Aspose.Cells for .NET** – `Workbook`, `Style` ve `ImportDataTable` çağrılarını sağlayan kütüphane. NuGet üzerinden kurun:  

  ```bash
  dotnet add package Aspose.Cells
  ```

* `DataTable` kaynağı – örnekte bir tane sahte oluşturacağız, ancak herhangi bir ADO.NET sorgusuyla değiştirebilirsiniz.

Bunlar hazır mı? Harika, başlayalım.

## Step 1: Initialize a New Workbook (Primary Keyword)

İlk yapmanız gereken **how to create workbook** – kelimenin tam anlamıyla. `Workbook` sınıfı tüm Excel dosyasını temsil eder ve yapıcı (constructor) size temiz bir sayfa sunar.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

namespace ExcelStylingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook (or obtain an existing one)
            Workbook workbook = new Workbook();   // <-- this is how to create workbook
```

> **Neden önemli?**: Yeni bir `Workbook` ile başlamak, her stili baştan kontrol etmenizi sağlar. Mevcut bir dosya açarsanız, orijinal yazarın bıraktığı stilleri devralırsınız ve bu tutarsız biçimlendirmelere yol açabilir.

## Step 2: Prepare the DataTable You’ll Import

Örnek olması açısından basit bir `DataTable` oluşturalım. Gerçek dünyada muhtemelen bir saklı prosedür ya da bir ORM yöntemi çağırırsınız.

```csharp
            // Step 2: Retrieve the data you want to import (e.g., from a database)
            DataTable dataTable = GetSampleData(); // replace with your own GetData()
```

```csharp
        // Helper method that returns a dummy DataTable
        static DataTable GetSampleData()
        {
            DataTable table = new DataTable("Employees");
            table.Columns.Add("ID", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("HireDate", typeof(DateTime));
            table.Columns.Add("Salary", typeof(decimal));

            table.Rows.Add(1, "Alice Johnson", new DateTime(2020, 5, 12), 72000);
            table.Rows.Add(2, "Bob Smith", new DateTime(2019, 3, 4), 68000);
            table.Rows.Add(3, "Carol White", DBNull.Value, 75000); // demonstrates a null value
            return table;
        }
```

> **İpucu:** Sütun sırasını veritabanında göründüğü gibi tam olarak korumanız gerekiyorsa, `ImportDataTable` metodunun `importColumnNames` parametresini `true` olarak ayarlayın. Bu, Aspose.Cells'in sizin için sütun başlıklarını yazmasını sağlar.

## Step 3: Define Column Styles – Default + Light‑Blue Background

Şimdi **add light blue background** sorusunun cevabını veriyoruz. Aspose.Cells, içe aktardığınız her sütuna karşılık gelen bir `Style` nesnesi dizisi geçirmenize izin verir. İlk giriş sütun 0 için stil, ikincisi sütun 1 için stil vb. Eğer stil sayısı sütun sayısından azsa, kalan sütunlar varsayılan stile geri döner.

```csharp
            // Step 3: Define column styles – the default style and a custom style with a light‑blue foreground
            Style defaultStyle = workbook.DefaultStyle; // this is the use default style excel
            Style lightBlueStyle = workbook.CreateStyle();
            lightBlueStyle.ForegroundColor = Color.LightBlue;
            lightBlueStyle.Pattern = BackgroundType.Solid; // make sure the color shows

            // Apply default style to the first column, light blue to the second column
            Style[] columnStyles = { defaultStyle, lightBlueStyle };
```

> **Neden sadece iki stil?** Örneğimizde dört sütun var, ancak sadece ikinci sütunu (Name) öne çıkarmak istiyoruz. Dizi uzunluğunun sütun sayısıyla eşleşmesi gerekmez; eksik girişler otomatik olarak çalışma kitabının varsayılan stilini devralır.

## Step 4: Import the DataTable with Headers and Styles

Burada **excel import datatable c#** ve **import data with headers** ifadelerini birleştiriyoruz. `ImportDataTable` metodu işi halleder: sütun adlarını, satırları yazar ve az önce oluşturduğumuz stil dizisini uygular.

```csharp
            // Step 4: Import the DataTable into the first worksheet starting at cell A1, applying the styles
            Worksheet sheet = workbook.Worksheets[0];
            sheet.Cells.ImportDataTable(dataTable, // the source DataTable
                                        true,       // import column names as headers
                                        0,          // start row (0‑based)
                                        0,          // start column (0‑based)
                                        columnStyles);
```

### Expected Result

Programı çalıştırdıktan sonra, `workbook` aşağıdaki gibi tek bir çalışma sayfası içerecek:

| **ID** | **Name** (light‑blue) | **HireDate** | **Salary** |
|-------|------------------------|--------------|------------|
| 1     | Alice Johnson          | 5/12/2020    | 72000      |
| 2     | Bob Smith              | 3/4/2019     | 68000      |
| 3     | Carol White            | *(blank)*    | 75000      |

* **Name** sütunu açık mavi arka plana sahip, stil dizisinin çalıştığını gösterir.
* Sütun başlıkları otomatik olarak oluşturulur çünkü `importColumnNames` için `true` verdik.
* Null değerler boş hücreler olarak görünür; bu Aspose.Cells'in varsayılan davranışıdır.

## Step 5: Save the Workbook (Optional but Useful)

Muhtemelen dosyayı diske yazmak ya da bir web istemcisine geri akıtmak isteyeceksiniz. Kaydetmek basittir:

```csharp
            // Step 5: Save the workbook to a file
            string outputPath = "StyledEmployees.xlsx";
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

> **Pro ipucu:** Daha eski Excel sürümlerini hedefliyorsanız, `SaveFormat.Xlsx` yerine `SaveFormat.Xls` kullanın. API dönüşümü sizin için halleder.

## Edge Cases & Variations

### Multiple Styled Columns

Birden fazla stil sahibi sütun gerekiyorsa, sadece `columnStyles` dizisini genişletin:

```csharp
Style[] columnStyles = { defaultStyle, lightBlueStyle, defaultStyle, lightBlueStyle };
```

Artık hem **Name** hem de **Salary** açık mavi olacak.

### Conditional Formatting Instead of Fixed Styles

Bazen bir değer bir eşiği aştığında sütunun kırmızıya dönmesini istersiniz. İşte **use default style excel** ifadesinin koşullu biçimlendirme ile buluştuğu yer:

```csharp
int salaryColIdx = 3; // zero‑based index for Salary column
FormatCondition condition = sheet.ConditionalFormattings[0]
    .AddCondition(FormatConditionType.CellValue, OperatorType.GreaterThan, "70000");
condition.Style.ForegroundColor = Color.LightCoral;
condition.Style.Pattern = BackgroundType.Solid;
```

### Importing Without Headers

Eğer alt sisteminiz zaten kendi başlıklarını sağlıyorsa, `importColumnNames` argümanı için sadece `false` geçin. Veri `A1` hücresinden başlayacak ve sonrasında özel başlıklar yazabilirsiniz.

```csharp
sheet.Cells.ImportDataTable(dataTable, false, 1, 0); // start at row 2 (index 1)
```

## Full Working Example (All

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}