---
category: general
date: 2026-07-03
description: C# kullanarak Excel tablosunu .txt dosyasına nasıl dışa aktaracağınızı
  ve .txt dosyasına nasıl kaydedeceğinizi öğrenin. Excel verilerini düz metin olarak
  tam kod örneğiyle dışa aktarın.
draft: false
keywords:
- how to export excel table
- save excel table to .txt file
- export excel data as plain text
- Aspose.Cells export table
- C# Excel to text
language: tr
og_description: Excel tablosunu düz metin olarak nasıl dışa aktarılır. Bu kılavuz,
  Excel verilerini düz metin olarak dışa aktarmayı ve Excel tablosunu Aspose.Cells
  ile .txt dosyasına kaydetmeyi gösterir.
og_title: Excel Tablosunu Nasıl Dışa Aktarılır – Tam C# Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to export Excel table to a .txt file and save Excel table
    to .txt file using C#. Export Excel data as plain text with full code example.
  headline: How to Export Excel Table – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- File I/O
title: Excel Tablosunu Nasıl Dışa Aktarılır – Tam Adım Adım Kılavuz
url: /tr/net/excel-data-export-retrieval/how-to-export-excel-table-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Tablosunu Dışa Aktarma – Tam Adım‑Adım Kılavuz

Hiç **Excel tablosunu nasıl dışa aktar** tüm çalışma kitabını belleğe almadan merak ettiniz mi? Tek başınıza değilsiniz. Birçok otomasyon işinde aşağı akış sistemi sadece basit bir `.txt` dosyasını kabul eder, bu yüzden **Excel tablosunu .txt dosyasına kaydet** için hızlı ve güvenilir bir yol gerekir.  

Bu öğreticide, Aspose.Cells kullanarak **Excel verilerini düz metin olarak dışa aktar** temiz bir C# çözümünü adım adım inceleyeceğiz. Sonunda çalıştırmaya hazır bir programınız olacak, her satırın neden önemli olduğunu anlayacaksınız ve dışa aktarmayı kendi özel durumlarınıza göre nasıl ayarlayacağınızı göreceksiniz.

## Gerekenler

- **Aspose.Cells for .NET** (herhangi bir yeni sürüm, ör. 23.12).  
- .NET 6 SDK veya daha yeni bir sürüm – kod .NET Core ile de derlenir.  
- En az bir Excel tablosu içeren örnek bir `input.xlsx` dosyası.  
- Bir metin düzenleyici veya IDE (Visual Studio, VS Code, Rider… seçiminiz).

Aspose.Cells dışındaki ekstra NuGet paketlerine gerek yoktur ve tüm süreç Windows, Linux veya macOS üzerinde çalışır.

## Adım 1: Projeyi ve İçe Aktarmaları Ayarlama

İlk olarak, bir konsol uygulaması oluşturun ve gerekli ad alanlarını kapsam içine alın.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll place the export logic here.
        }
    }
}
```

> **Pro ipucu:** .NET CLI kullanıyorsanız, kodu yapıştırmadan önce `dotnet new console -n ExcelTableExport` komutunu çalıştırın ve ardından `dotnet add package Aspose.Cells` komutunu yürütün.

## Adım 2: Çalışma Kitabını Yükleyin ve İlk Çalışma Sayfasını Alın

Workbook nesnesi tüm Excel dosyasını temsil eder. Tek seferde yüklemek bellek kullanımını düşük tutar.

```csharp
// Step 2: Load the workbook and get the first worksheet
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = wb.Worksheets[0];
```

Neden ilk çalışma sayfasını seçiyoruz? Birçok oluşturulan raporda veriler ilk sayfada bulunur, ancak dizini değiştirebilir veya adlandırılmış bir sayfa için `wb.Worksheets["SheetName"]` kullanabilirsiniz.

## Adım 3: Çalışma Sayfasında Tanımlı İlk Tabloyu Alın

Excel tabloları (ListObjects) yapılandırılmış veri sağlar, bu da dışa aktarmayı öngörülebilir kılar.

```csharp
// Step 3: Retrieve the first table defined on the worksheet
Table tbl = ws.Tables[0];
```

Çalışma kitabınız birden fazla tablo içeriyorsa, sadece `ws.Tables` üzerinden döngü yapın veya `tbl.Name` ile seçin.

## Adım 4: Dışa Aktarma Seçeneklerini Yapılandırma – Her Hücreyi Dize Olarak Dışa Aktar

Aspose.Cells, dışa aktarma sırasında her hücrenin formatını kontrol etmenizi sağlar. `ExportAsString` ayarı, sayıların, tarihlerin ve formüllerin düz metin olmasını garantiler.

```csharp
// Step 4: Set up export options – export every cell as a string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true
};
```

### Boşlukları Kırpmak İçin Özel Bir Dışa Aktarma Eylemi Ekleme

Kaynak veriler genellikle başta veya sonda boşluklar içerir. Bunları kırpmak son `.txt` dosyasını daha temiz hâle getirir.

```csharp
// Define a custom export action to trim cell values before writing
exportOptions.CustomExport = (cell, writer) =>
{
    writer.Write(cell.StringValue.Trim());
};
```

Lambda, `Cell` nesnesini ve bir `TextWriter` alır. Burada koşullu mantık da ekleyebilirsiniz—ör. CSV tarzı çıktı için virgülleri noktalı virgül ile değiştirmek.

## Adım 5: Tabloyu A1 Hücresinden Başlayarak Metin Dosyasına Dışa Aktar

Şimdi tabloyu diske gerçekten yazıyoruz. `ExportTable` metodu tabloyu satır satır dolaşır ve az önce tanımladığımız seçenekleri uygular.

```csharp
// Step 5: Export the table starting at cell A1 to a text file
using (StreamWriter writer = new StreamWriter("YOUR_DIRECTORY/Table.txt"))
{
    ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
}
```

**Gördükleriniz:** Excel tablosunun her satırı `Table.txt` içinde bir satır olur. Sütunlar varsayılan olarak bir sekme karakteri (`\t`) ile ayrılır—aşağı akışta ayrıştırma için mükemmeldir.

### Beklenen Çıktı Örneği

`input.xlsx` dosyasının üç sütunlu (`ID`, `Name`, `Score`) ve iki veri satırı içeren bir tablo olduğunu varsayarsak, `Table.txt` şöyle görünecektir:

```
1    Alice    85
2    Bob      92
```

Boşlukların kırpıldığını ve her şeyin düz metin olduğunu fark edin—tam da **Excel verilerini düz metin olarak dışa aktarma** gereksiniminin istediği gibi.

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Ne Yapmalı | Neden |
|-----------|------------|-----|
| **Tablonun boş hücreleri var** | Lambda, boş hücreler için boş bir dize döndüren `cell.StringValue.Trim()` yazar. | İstenmeyen karakterler eklemeden sütun hizalamasını korur. |
| **Özel bir ayırıcıya ihtiyacınız var** | `writer.Write(cell.StringValue.Trim());` satırını `writer.Write($"{cell.StringValue.Trim()},");` ile değiştirin ve her satırdan sonra son ayırıcıyı kırpın. | Bazı sistemler sekmeler yerine virgül veya boru işaretini tercih eder. |
| **Büyük çalışma sayfaları ( > 100 k satır )** | `ExportAsString = true` ile `ExportTableOptions` kullanın ve dosyayı gösterildiği gibi akış olarak yazın; Aspose.Cells satırları akış modunda işler, OOM hatalarını önler. | Ölçeklenebilirliği garantiler. |
| **Tek bir sayfada birden fazla tablo** | `ws.Tables` üzerinde döngü yapın ve her biri için `ExportTable` çağırın, isteğe bağlı olarak dışa aktarmalar arasında bir ayırıcı satır ekleyebilirsiniz. | Her tablo için **Excel tablosunu .txt dosyasına kaydet** yapmanızı sağlar. |

## Tam Çalışan Örnek

Aşağıda `Program.cs` içine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. `YOUR_DIRECTORY` ifadesini makinenizde mevcut olan mutlak ya da göreli bir yol ile değiştirin.

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelTableExport
{
    class Program
    {
        static void Main(string[] args)
        {
            // Load workbook
            Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
            Worksheet ws = wb.Worksheets[0];

            // Get first table
            if (ws.Tables.Count == 0)
            {
                Console.WriteLine("No tables found on the first worksheet.");
                return;
            }
            Table tbl = ws.Tables[0];

            // Configure export options
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, writer) =>
                {
                    // Trim whitespace and write value
                    writer.Write(cell.StringValue.Trim());
                }
            };

            // Export to text file
            string outputPath = "YOUR_DIRECTORY/Table.txt";
            using (StreamWriter writer = new StreamWriter(outputPath))
            {
                ws.Cells.ExportTable(tbl, "A1", exportOptions, writer);
            }

            Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

Programı `dotnet run` ile çalıştırın. Her şey doğru ayarlandıysa, onay mesajını ve **Excel verilerini düz metin olarak dışa aktarma** içeren yeni oluşturulmuş bir `Table.txt` dosyasını göreceksiniz.

## Bonus: Görsel Onay (Opsiyonel)

Elde edilen dosyanın hızlı bir ekran görüntüsünü görmek isterseniz, herhangi bir metin düzenleyicide açabilirsiniz. Aşağıda beklenen düzeni gösteren bir yer tutucu resim var.

![how to export excel table screenshot](https://example.com/images/export-excel-table.png "how to export excel table")

*Alt text:* **Excel tablo dışa aktarma** – dışa aktarılmış bir Excel tablosunun düz‑metin çıktısını gösterir.

## Özet & Sonraki Adımlar

Aspose.Cells kullanarak **Excel tablosunu nasıl dışa aktar** hakkında bilmeniz gereken her şeyi, workbook yüklemeden hücre değerlerini kırpmaya ve son olarak temiz bir `.txt` dosyası yazmaya kadar ele aldık.  

- Artık **Excel tablosunu .txt dosyasına kaydet** işlemini özel mantıkla anlayabiliyorsunuz.  
- Lambda’yı tarih, sayı veya özel ayırıcıları işlemek için uyarlayabilirsiniz.  
- Daha büyük projeler için, mantığı yeniden kullanılabilir bir yöntem veya sınıf içine sarmayı düşünün.

**Sonraki Adım?** Birden fazla tablo dışa aktarmayı deneyin veya ayırıcıyı değiştirerek çıktıyı CSV’ye dönüştürün. Ayrıca **Excel verilerini düz metin olarak dışa aktar** doğrudan bir ağ akışına göndererek gerçek zamanlı entegrasyonları keşfedebilirsiniz.

Sorularınız mı var ya da bir sorunla mı karşılaştınız? Yorum bırakın, iyi kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells Kullanarak .NET’te Excel Dosyalarını Dışa Aktarma: Kapsamlı Kılavuz](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Aspose.Cells for .NET Kullanarak Görünür Excel Satırlarını Dışa Aktarma: Adım‑Adım Kılavuz](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Aspose.Cells for .NET Kullanarak Excel Sayfalarını Tek Metin Dosyasında Birleştirme](/cells/english/net/workbook-operations/combine-excel-sheets-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}