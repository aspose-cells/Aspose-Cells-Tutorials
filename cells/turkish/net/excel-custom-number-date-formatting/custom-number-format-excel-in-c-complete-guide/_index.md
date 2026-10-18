---
category: general
date: 2026-03-22
description: Özel sayı formatı Excel öğreticisi, veri tablosunu Excel'e nasıl içe
  aktarılacağını, sütun arka plan rengini nasıl ayarlayacağını, sütunu para birimi
  olarak nasıl biçimlendireceğini ve çalışma kitabını xlsx olarak nasıl kaydedeceğini
  gösterir.
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: tr
og_description: Özel sayı formatı Excel öğreticisi, bir DataTable'ı içe aktarmayı,
  sütun arka plan rengini ayarlamayı, bir sütunu para birimi olarak biçimlendirmeyi
  ve çalışma kitabını xlsx olarak kaydetmeyi adım adım gösterir.
og_title: C# ile Excel Özel Sayı Formatı – Adım Adım Rehber
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: C#'ta Excel Özel Sayı Formatı – Tam Kılavuz
url: /tr/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel Sayı Biçimi Excel – Full‑Stack C# Öğreticisi

C#'tan doğrudan **custom number format excel** stilini uygulamayı hiç merak ettiniz mi? Belki bir DataTable'ı bir elektronik tabloya döküp sadece düz sayılar, renksiz hücreler ve para birimi biçimlendirmesi görmüşsünüzdür. Bu, özellikle paydaşlar için şık bir rapor gerektiğinde yaygın bir sıkıntıdır.

Bu rehberde bu sorunu birlikte çözeceğiz: **import datatable to excel**, **set column background color**, **format column as currency** ve sonunda **save workbook as xlsx** işlemlerini özel bir sayı biçimiyle yaparak rakamlarınızı öne çıkaracaksınız. Belirsiz referanslar yok, sadece projenize kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir bir çözüm.

---

## Ne Oluşturacaksınız

Bu öğreticinin sonunda, kendine yeten bir C# konsol uygulamanız olacak:

1. `DataTable` alır (stub'ı kendi sorgunuzla değiştirebilirsiniz).  
2. Aspose.Cells (veya uyumlu bir kütüphane) kullanarak yeni bir Excel çalışma kitabı oluşturur.  
3. İlk sütuna mavi, kalın bir yazı tipi, ikinci sütuna açık sarı bir arka plan ve üçüncü sütuna para birimi biçimi (`$#,##0.00`) uygular.  
4. Dosyayı seçtiğiniz bir klasörde `DataTableWithStyleArray.xlsx` olarak kaydeder.

Her satırın nihai Excel dosyasına nasıl katkıda bulunduğunu tam olarak göreceksiniz ve bu seçimlerin bakım ve performans açısından neden önemli olduğunu tartışacağız.

## Önkoşullar

- .NET 6.0 veya daha yenisi (kod .NET Framework 4.7+ ile de çalışır).  
- Aspose.Cells for .NET (ücretsiz deneme veya lisanslı sürüm). NuGet üzerinden kurun:

```bash
dotnet add package Aspose.Cells
```

- `DataTable` ve C# konsol uygulamaları hakkında temel bilgi.

## Adım 1: Kaynak Veriyi DataTable Olarak Alın

İlk olarak, dışa aktaracak bazı verilere ihtiyacımız var. Gerçek bir senaryoda muhtemelen bir repository'yi çağırır veya bir SQL sorgusu çalıştırırsınız. Örnekleme amacıyla bellekte basit bir tablo oluşturacağız.

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **Neden önemli:** `DataTable` kullanmak, Excel satır ve sütunlarına temiz bir şekilde eşlenen, tablo‑tabanlı, şema‑bilinçli bir kaynak sağlar. Ayrıca aynı dışa aktarma mantığını herhangi bir veri kümesi için kodu yeniden yazmadan yeniden kullanmanıza olanak tanır.

## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun ve İlk Çalışma Sayfasını Alın

Şimdi bir Excel çalışma kitabı oluşturuyoruz. `Workbook` sınıfı tüm dosyayı temsil eder; `Worksheets[0]` ise verilerimizi bırakacağımız varsayılan sayfadır.

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro ipucu:** Birden fazla sayfaya ihtiyacınız varsa, sadece `workbook.Worksheets.Add("SheetName")` çağırın ve stil adımlarını her biri için tekrarlayın.

## Adım 3: Sütun Stillerini Tanımlayın – Yazı Tipi, Arka Plan ve Sayı Biçimi

Aspose.Cells'ta stil oluşturma `Style` nesneleriyle yapılır. DataTable'daki her sütuna karşılık gelen bir dizi oluşturacağız.

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **Neden bir stil dizisi?** `ImportDataTable`'a bir dizi geçmek, tek bir çağrıda her sütuna ayrı bir stil uygulamanızı sağlar; bu hem özlü hem de performanslıdır. Ayrıca biçimlendirmenin veri sırası ile senkron kalmasını garanti eder.

## Adım 4: Stilleri Uygularken DataTable'ı İçe Aktarın

İşlemin kalbi burada: `DataTable`'ı çalışma sayfasına besliyoruz, Aspose'a başlık satırını dahil etmesini söylüyoruz ve `columnStyles` dizimizi iletiyoruz.

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **Arka planda ne oluyor?** Aspose her sütunu iterasyonla dolaşır, başlığı yazar, ardından her satır değerini yazar. Bunu yaparken diziden ilgili `Style`'ı uygular, böylece “Product” için mavi bir başlık, “Quantity” için sarı tonlu bir arka plan ve “Revenue” sütunu güzel bir biçimlendirme elde edersiniz.

## Adım 5: Çalışma Kitabını XLSX Dosyası Olarak Kaydedin

Son olarak, çalışma kitabını diske kaydediyoruz. `Save` yöntemi dosya uzantısına göre otomatik olarak XLSX formatını seçer.

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **İpucu:** Dosyayı akış olarak göndermeniz gerekiyorsa (ör. bir web API için), dosya yolu yerine `workbook.Save(stream, SaveFormat.Xlsx)` kullanın.

## Tam Çalışan Örnek

Aşağıda yeni bir konsol projesine yapıştırabileceğiniz tam program bulunmaktadır. Derlenir ve olduğu gibi çalışır, stil uygulanmış bir Excel dosyası üretir.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### Beklenen Sonuç

`DataTableWithStyleArray.xlsx` dosyasını açtığınızda şunları göreceksiniz:

| **Ürün** (mavi, kalın) | **Miktar** (açık‑sarı) | **Gelir** (para birimi) |
|--------------------------|-----------------------------|------------------------|
| Widget A                 | 120                         | $3,450.75              |
| Widget B                 | 85                          | $2,190.00              |
| Widget C                 | 60                          | $1,580.40              |

Belirttiğiniz **custom number format excel** (`$#,##0.00`), her gelir hücresinin dolar işareti, binlik ayırıcı ve iki ondalık basamakla gösterilmesini sağlar—tam da finans ekiplerinin beklediği gibi.

## Sıkça Sorulan Sorular & Kenar Durumları

### Farklı bir Excel kütüphanesiyle kullanabilir miyim?

Kesinlikle. Her sütun için bir stil oluşturup içe aktarım sırasında uygulama konsepti EPPlus, ClosedXML veya NPOI'ye de uygulanabilir. API çağrıları farklıdır, ancak desen aynı kalır.

### DataTable'ım stil sayısından daha fazla sütun içeriyorsa ne olur?

Aspose, `columnStyles` dizisinde eşleşen bir giriş olmayan sütunlara varsayılan stili uygular. Sürprizleri önlemek için, diziyi `dataTable.Columns.Count` kadar boyutlandırın veya bir döngüde dinamik olarak stiller oluşturun.

### Tarihler için özel bir sayı biçimi nasıl ayarlanır?

`style.Custom = "dd‑mm‑yyyy"` (veya geçerli bir Excel biçim dizesi) olarak ayarlayın. Aynı dizi‑bazlı yaklaşım tarih, yüzde veya bilimsel gösterimler için de çalışır.

### İçe aktarma sonrası sütunları otomatik boyutlandırmanın bir yolu var mı?

Evet—içe aktarmadan sonra `worksheet.AutoFitColumns();` çağırın. Hücre içeriğine göre hızlı bir genişlik hesabı yapar.

### Büyük veri setleri (100k+ satır) hakkında ne söyleyebilirsiniz?

`ImportDataTable` toplu işlemler için optimize edilmiştir, ancak bellek sınırlarına ulaşabilirsiniz. Bu durumda, satırları manuel olarak `Cells[i, j].PutValue(...)` ile akışa almayı ve aşırı yükü azaltmak için tek bir `Style` nesnesini yeniden kullanmayı düşünün.

## Pro İpuçları & Yaygın Tuzaklar

- **Üretim kodunda yolları sabit kodlamaktan kaçının**; `Environment.GetFolderPath` veya yapılandırma ayarlarını kullanın.  
- **Çalışma kitabını serbest bırakın**; uzun süren bir hizmette iseniz, yerel kaynakları serbest bırakmak için `using` bloğu içinde sarın.  
- **Kültüre özgü ayırıcılara dikkat edin**. Özel format `$#,##0.00` işletim sistemi yerel ayarına bakılmaksızın ondalık ayırıcı olarak nokta zorlar; bu genellikle finansal raporlar için istenen durumdur.  
- **System.Drawing'e (veya .NET Core'da `System.Drawing.Common`'a) referans vermeyi unutmayın**; stil oluştururken kullanılan renk yapıları için gereklidir.  
- **Çıktıyı farklı Excel sürümlerinde test edin**; eski sürümler bazı özel formatları biraz farklı yorumlayabilir.

## Sonuç

C#'tan **custom number format excel** dosyaları oluşturmak için ihtiyacınız olan her şeyi ele aldık: bir `DataTable`'dan veri çekmek, **import datatable to excel**, **set column background color** uygulamak, **format column as currency** kullanmak ve sonunda **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}