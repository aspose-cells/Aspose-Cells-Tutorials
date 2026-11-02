---
category: general
date: 2026-09-27
description: Aspose.Cells kullanarak C#'ta bir pivot tabloyu nasıl kopyalayacağınızı
  öğrenin. Biçimlendirme ile satırları kopyalama, pivot tabloyu başka bir sayfaya
  kopyalama ve pivot tabloyu yeni bir çalışma kitabına dışa aktarma içerir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy rows with formatting
- copy pivot table to another sheet
- how to copy excel rows
- export pivot table to new workbook
language: tr
lastmod: 2026-09-27
og_description: Aspose.Cells kullanarak C#'de bir pivot tabloyu nasıl kopyalanır.
  Biçimlendirme ile satırları kopyalamak, pivot tabloyu başka bir sayfaya taşımak
  ve yeni bir çalışma kitabına aktarmak için adım adım rehberi izleyin.
og_image_alt: Excel sheet showing a copied pivot table after using Aspose.Cells
og_title: C#'de bir pivot tabloyu nasıl kopyalarsınız – tam Aspose.Cells rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to copy a pivot table in C# using Aspose.Cells. Includes
    copy rows with formatting, copy pivot table to another sheet, and export pivot
    table to a new workbook.
  headline: How to copy a pivot table in C# with Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
- Pivot table
title: Aspose.Cells ile C#'ta bir pivot tablo nasıl kopyalanır
url: /tr/net/pivot-tables/how-to-copy-a-pivot-table-in-c-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.Cells Kullanarak Pivot Tablo Nasıl Kopyalanır

Bir çalışma sayfasından diğerine **pivot tablo kopyalamanız** gerekiyorsa, C# ile Aspose.Cells kullanarak **pivot tablo nasıl kopyalanır** öğrenmek size saatlerce manuel çalışma kazandırabilir. Bu yöntem ayrıca **biçimlendirmeli satırları kopyalamanıza**, pivot önbelleğini korumanıza ve hatta **pivot tabloyu yeni bir çalışma kitabına dışa aktarmanıza** olanak tanır.

Bu öğretici, tam iş akışını adım adım gösterir:

* bir çalışma kitabı oluşturma,  
* biçimlendirmeyi koruyarak pivot‑tablo aralığını kopyalama,  
* kopyalanan veriyi yeni bir sayfaya yerleştirme ve  
* sonucu ayrı bir dosya olarak kaydetme.

`CopyRows` yerleşik yöntemi neden **pivot tabloyu başka bir sayfaya kopyalamanın** en güvenilir yolu olduğunu göreceksiniz ve gizli satırlar ya da harici veri kaynakları gibi uç durumları ele almak için ipuçları alacaksınız.

## Önkoşullar

Başlamadan önce şunların olduğundan emin olun:

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6.0 or later | Aspose.Cells, .NET 6+’ı destekler ve en iyi performansı sağlar. |
| Visual Studio 2022 (or any C# IDE) | NuGet paketlerini geri yükleyebilen bir editöre ihtiyacınız var. |
| Aspose.Cells for .NET (NuGet package `Aspose.Cells`) | Bu kütüphane, örnekte kullanılan `CopyRows` API’sini sağlar. |
| A source Excel file (`source.xlsx`) that contains a pivot table in the range `A1:G20` | Kod bu belirli aralığı kopyalar; pivot tablonuz daha büyükse aralığı ayarlayın. |

Kütüphaneyi NuGet CLI veya Package Manager Console ile kurun:

```bash
dotnet add package Aspose.Cells
```

## Adım 1: Pivot tabloyu içeren çalışma kitabını yükleyin

İlk satır, tüm Excel dosyasını temsil eden bir `Workbook` nesnesi oluşturur. Dosyayı bir kez yüklemek, her çalışma sayfasına okuma/yazma erişimi sağlar.

```csharp
using Aspose.Cells;

// Load the source workbook
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\source.xlsx");
```

> **Bu adımın önemi** – Çalışma kitabı yüklenmeden, sonraki `CopyRows` çağrılarının hiçbiri kaynak veriye ya da pivot önbelleğine başvuramaz.

## Adım 2: Kaynak ve hedef çalışma sayfalarını hazırlayın

Kopyalanan pivot tablonun bulunacağı bir hedef sayfaya ihtiyacınız var. Aşağıdaki kod, orijinal pivot tablonun bulunduğu ilk çalışma sayfasını alır ve **Copy** adlı yeni bir sayfa ekler.

```csharp
// Get the source worksheet (index 0 = first sheet)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a new worksheet that will receive the copied rows
Worksheet destinationSheet = workbook.Worksheets.Add("Copy");
```

> **Pro ipucu:** Hedef sayfa zaten varsa, aynı isimlerin oluşmasını önlemek için önce `Worksheets.RemoveAt(index)` metodunu çağırın.

## Adım 3: Pivot tabloyu kapsayan hücre alanını tanımlayın

`CellArea` nesnesi, taşımak istediğiniz aralığın sol‑üst ve sağ‑alt hücrelerini tanımlar. Bu örnekte pivot tablo `A1:G20` aralığını kaplar. Daha büyük tablolar için koordinatları ayarlayın.

```csharp
// Define the range that includes the pivot table (A1:G20)
CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");
```

## Adım 4: Biçimlendirmeyi koruyarak satırları kopyalayın ve pivot önbelleğini koruyun

`CopyRows` yöntemi, kaynak sayfadan hedef sayfaya **satırları** kopyalar. `CopyOptions.CopyAll` parametresini geçirerek, değerlerin, biçimlendirmelerin, grafiklerin ve gömülü nesnelerin—pivot tablonun bir parçası olan—tümünün aktarılmasını sağlarsınız.

```csharp
// Copy the rows from the source area to the destination sheet
sourceSheet.CopyRows(
    sourceArea.StartRow,          // start row in the source sheet
    destinationSheet,            // target worksheet
    0,                            // start row in the destination sheet
    sourceArea.RowCount,          // number of rows to copy
    CopyOptions.CopyAll);        // copy everything (values, formats, objects, etc.)
```

### Neden `CopyRows`, pivot tablolar için `Copy`'den daha iyi çalışır

* `CopyRows`, dahili pivot önbelleğine saygı gösterir, böylece kopyalanan pivot tablo işlevsel kalır.
* Orijinal sayfada göründüğü gibi **biçimlendirmeli satırları kopyalamayı** tam olarak korur.
* Basit bir aralık `Copy`'iyle karşılaştırıldığında, gizli satırları ve ilişkili dilimleyicileri de taşır.

## Adım 5: Kopyalanan pivot tabloyla çalışma kitabını kaydedin

Son olarak, değiştirilmiş çalışma kitabını diske yazın. Yeni dosya, orijinal sayfayı ve orijinal pivot tablonun tam işlevsel bir kopyasını içeren **Copy** sayfasını içerir.

```csharp
// Save the workbook to a new file
workbook.Save(@"YOUR_DIRECTORY\pivot_copied.xlsx");
```

### Beklenen sonuç

`pivot_copied.xlsx` dosyasını açtığınızda:

* **Sheet1** sayfası hâlâ orijinal veri ve pivot tabloyu içerir.
* **Copy** sayfası aynı düzen, filtre ve biçimlendirmeye sahip aynı pivot tabloyu gösterir.
* Tüm formüller ve veri bağlantıları, pivot önbelleği satırlarla birlikte kopyalandığı için sağlam kalır.

## Aynı çalışma kitabında pivot tabloyu başka bir sayfaya nasıl kopyalarsınız

Sadece pivot tabloyu farklı bir mevcut sayfada (ör. “Report”) istiyorsanız, hedef oluşturma adımını hedef sayfaya referansla değiştirin:

```csharp
Worksheet destinationSheet = workbook.Worksheets["Report"]; // existing sheet
sourceSheet.CopyRows(sourceArea.StartRow, destinationSheet, 0,
                     sourceArea.RowCount, CopyOptions.CopyAll);
```

Bu kod parçacığı, yeni bir çalışma sayfası oluşturmadan **pivot tabloyu başka bir sayfaya kopyalamayı** gösterir.

## Pivot tabloyu yeni bir çalışma kitabına dışa aktar

Bazen pivot tabloyu tamamen ayrı bir dosyada istiyorsunuz. Kopyalama işleminden sonra, kopyalanan pivot tabloyu tutan sayfa dışındaki tüm çalışma sayfalarını kaldırabilir ve ardından kaydedebilirsiniz:

```csharp
// Keep only the copied sheet
for (int i = workbook.Worksheets.Count - 1; i >= 0; i--)
{
    if (workbook.Worksheets[i].Name != "Copy")
        workbook.Worksheets.RemoveAt(i);
}

// Save as a new workbook containing only the pivot table
workbook.Save(@"YOUR_DIRECTORY\pivot_only.xlsx");
```

Artık `pivot_only.xlsx` dosyası, kopyalanan pivot tabloyu içeren tek bir sayfa içerir ve **pivot tabloyu yeni bir çalışma kitabına dışa aktarma** gereksinimini karşılar.

## Biçimlendirmeyi kaybetmeden Excel satırlarını nasıl kopyalarsınız

Aynı `CopyRows` çağrısı, sadece pivot tablolar için değil, herhangi bir aralık için de çalışır. Koşullu biçimlendirme, veri doğrulama veya birleştirilmiş hücreler içeren **excel satırlarını kopyalamanız** gerekiyorsa, aynı yöntemi kullanın:

```csharp
// Example: copy rows 30‑40 from Sheet1 to Sheet2
sourceSheet.CopyRows(29, // zero‑based index for row 30
                     workbook.Worksheets["Sheet2"],
                     0,
                     11, // rows 30‑40 = 11 rows
                     CopyOptions.CopyAll);
```

`CopyOptions.CopyAll` her şeyi aktardığı için, hedef satırlar kaynak satırlarla tamamen aynı görünür.

## Yaygın tuzaklar ve nasıl önlenir

| Sorun | Belirti | Çözüm |
|---------|---------|-----|
| Kaynak aralık tüm pivot tabloyu içermiyor | Kopyalanan pivot tablo kesik görünüyor. | `CellArea`'nin pivot tablonun tüm satır/ sütunlarını kapsadığını doğrulayın. |
| Hedef sayfa zaten veri içeriyor | Üzerine yazılan satırlar veri kaybına neden olur. | Yeni bir sayfa seçin veya kopyalamaya daha yüksek bir satır indeksinden başlayın. |
| Pivot tablo harici bir veri kaynağı kullanıyor | Kopya bağlantısını kaybeder. | Kopyaladıktan sonra, bağlantıyı yeniden kurmak için `pivotTable.RefreshData()` metodunu çağırın. |
| Gizli satırlar atlanıyor | Kopyada bazı satırlar kaybolur. | `CopyRows` gizli satırları otomatik olarak kopyalar; `CopyOptions.CopyValuesOnly` kullanmadığınızdan emin olun. |

## Tam, çalıştırılabilir örnek

Aşağıda, yeni bir konsol projesine yapıştırabileceğiniz bağımsız bir program bulunmaktadır. Yukarıda tartışılan tüm adımları gösterir.

```csharp
using System;
using Aspose.Cells;

namespace PivotTableCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the workbook that contains the pivot table
            string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2️⃣ Get source and destination worksheets
            Worksheet sourceSheet = workbook.Worksheets[0]; // first sheet
            Worksheet destinationSheet = workbook.Worksheets.Add("Copy");

            // 3️⃣ Define the cell area that holds the pivot table (A1:G20)
            CellArea sourceArea = CellArea.CreateCellArea("A1", "G20");

            // 4️⃣ Copy rows with formatting and keep the pivot cache
            sourceSheet.CopyRows(
                sourceArea.StartRow,      // start row index (0‑based)
                destinationSheet,        // target sheet
                0,                        // start row in destination
                sourceArea.RowCount,      // number of rows to copy
                CopyOptions.CopyAll);    // copy everything

            // 5️⃣ Save the workbook with the copied pivot table
            string destPath = @"YOUR_DIRECTORY\pivot_copied.xlsx";
            workbook.Save(destPath);

            Console.WriteLine("Pivot table copied successfully to " + destPath);
        }
    }
}
```

**Programı çalıştırmak**, **Copy** adlı yeni bir sayfada orijinal pivot tablonun bir kopyasını içeren `pivot_copied.xlsx` dosyasını oluşturur.

## Sonuç

Artık C# kullanarak **pivot tabloyu nasıl kopyalayacağınızı** biliyorsunuz

## Sonra Ne Öğrenmelisiniz?

Bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Yeni Çalışma Kitabı Oluştur – Pivot Tablo İçeren Çalışma Sayfasını Kopyalama](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [C# ile Pivot Tablo Kopyalama – Tam Adım Adım Kılavuz](/cells/english/net/pivot-tables/copy-pivot-table-in-c-complete-step-by-step-guide/)
- [C# ile Pivot Tablolarla Aralık Kopyalama – Tam Kılavuz](/cells/english/net/pivot-tables/how-to-copy-range-with-pivot-tables-in-c-complete-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}