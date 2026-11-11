---
category: general
date: 2026-10-26
description: C# ve Aspose.Cells ile bir DataTable'ı Excel çalışma sayfasına, stilleri
  ve başlıkları koruyarak sadece birkaç satır kodla nasıl aktaracağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to import datatable
- ImportTableOptions
- ImportDataTableStyle
- Aspose.Cells
- Excel worksheet import
- C# DataTable import
language: tr
lastmod: 2026-10-26
og_description: C# ve Aspose.Cells kullanarak bir DataTable'ı Excel çalışma sayfasına
  nasıl aktarılır? Stilleri, başlıkları ve biçimlendirmeyi korumak için bu kapsamlı
  rehberi izleyin.
og_image_alt: Screenshot of C# code that imports a DataTable into an Excel worksheet
  with Aspose.Cells
og_title: DataTable'ı bir Excel çalışma sayfasına nasıl aktarılır – C# adım adım rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to import DataTable into an Excel worksheet with C# and Aspose.Cells,
    preserving styles and headers in just a few lines of code.
  headline: How to import DataTable into an Excel worksheet using C#
  type: TechArticle
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: C# kullanarak DataTable'ı bir Excel çalışma sayfasına nasıl aktarılır
url: /tr/net/excel-data-import-export/how-to-import-datatable-into-an-excel-worksheet-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# kullanarak bir Excel çalışma sayfasına DataTable nasıl içe aktarılır

Excel çalışma sayfasına **how to import datatable** ihtiyacınız varsa, bu kılavuz C#'ta tam adımları gösterir. Raporlama motoru oluşturuyor ya da ızgara verilerini dışa aktarıyorsanız, Aspose.Cells ile sütun başlıklarını ve hücre stillerini nasıl koruyacağınızı göreceksiniz. Çözüm .NET 6+ ile çalışır ve sadece birkaç satır kod gerektirir.

Bir DataTable'ı içe aktarmak, elektronik tablo ile çalışırken yaygın bir görevdir, ancak geliştiriciler genellikle stil aktarımını etkinleştirmeyi veya başlık bayrağını doğru şekilde geçmeyi unuturlar. Bu öğreticide **ImportTableOptions** nasıl yapılandırılır, **ImportDataTableStyle** nasıl etkinleştirilir ve `ImportDataTable` güvenli bir şekilde nasıl çağrılır öğreneceksiniz. Sonunda, herhangi bir C# projesine ekleyebileceğiniz hazır‑çalıştır bir metoda sahip olacaksınız.

## Önkoşullar

* .NET 6 SDK veya daha yeni bir sürüm yüklü.
* **Aspose.Cells for .NET**'in lisanslı bir kopyası (ücretsiz deneme sürümü test için çalışır).
* `DataTable` ve Excel kavramlarına temel aşinalık.
* Visual Studio 2022 gibi bir IDE (C#'ı destekleyen herhangi bir editör çalışır).

`Aspose.Cells` dışında ek NuGet paketlerine gerek yok.

## Adım 1: Kaynak veriyi bir DataTable içine alın

**how to import datatable** sorusunu yanıtladığınızda ilk yapmanız gereken veri hazır olmaktır. Çoğu gerçek dünya senaryosunda `DataTable`, bir veritabanı sorgusu, bir CSV ayrıştırıcı veya bellek içi bir koleksiyondan gelir. İşte birkaç satır içeren bir tablo oluşturan minimal bir örnek:

```csharp
using System;
using System.Data;

public static DataTable GetSampleData()
{
    var table = new DataTable("Employees");
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Department", typeof(string));

    table.Rows.Add(1, "Alice Johnson", "Finance");
    table.Rows.Add(2, "Bob Smith", "Engineering");
    table.Rows.Add(3, "Carol White", "Marketing");

    return table;
}
```

*Neden önemli*: `DataTable`'ı önce oluşturduğunuzda, sütun sırasını, veri tiplerini ve başlık adlarını kontrol edersiniz—bunların tümü tabloyu daha sonra bir Excel çalışma sayfasına içe aktardığınızda korunur.

## Adım 2: `ImportTableOptions` oluşturun ve stil içe aktarmayı etkinleştirin

**how to import datatable** sorusunu yanıtladığınızda bir sonraki karar, kaynak `DataTable`'da zaten tanımlı olabilecek görsel stili (yazı tipleri, renkler, kenarlıklar) isteyip istemediğinizdir. Aspose.Cells, ayrıntılı kontrol için `ImportTableOptions` sınıfını sunar. `ImportDataTableStyle = true` ayarı, stil bilgilerini hedef çalışma sayfasına kopyalar.

```csharp
using Aspose.Cells;

public static ImportTableOptions CreateImportOptions()
{
    var options = new ImportTableOptions
    {
        // Preserve the style of the DataTable cells (font, background, borders)
        ImportDataTableStyle = true
    };
    return options;
}
```

*Neden önemli*: `ImportDataTableStyle` etkinleştirilmezse, içe aktarılan hücreler varsayılan çalışma sayfası stilini kullanır ve `DataTable`'a uyguladığınız özel biçimlendirmeyi kaybeder. Bu bayrak, düzgün bir dışa aktarma için gereklidir.

## Adım 3: DataTable'ı çalışma sayfasına, başlıkları dahil ederek içe aktarın

Artık **how to import datatable** sorusunu bir Excel dosyasına yanıtlamak için gereken her şeye sahipsiniz. Bir çalışma kitabı oluşturur, bir çalışma sayfası seçer ve `ImportDataTable`'ı çağırırsınız. Metodun ikinci argümanı (`true`), Aspose.Cells'e sütun başlıklarını ilk satır olarak yazmasını söyler.

```csharp
using Aspose.Cells;
using System.IO;

public static void ExportDataTableToExcel(string filePath)
{
    // 1️⃣ Retrieve the source data
    DataTable dataTable = GetSampleData();

    // 2️⃣ Prepare import options (style preservation)
    ImportTableOptions importOptions = CreateImportOptions();

    // 3️⃣ Create a new workbook and select the first worksheet
    var workbook = new Workbook();
    Worksheet ws = workbook.Worksheets[0];
    ws.Name = "Employees";

    // 4️⃣ Import the DataTable, include headers, and apply options
    ws.Cells.ImportDataTable(dataTable, true, importOptions);

    // 5️⃣ Save the workbook to the specified path
    workbook.Save(filePath, SaveFormat.Xlsx);
}
```

`ExportDataTableToExcel("Employees.xlsx")` çalıştırıldığında, ilk satırda **Id**, **Name** ve **Department** bulunan bir `Employees.xlsx` dosyası oluşturulur ve her hücre, orijinal `DataTable`'da tanımlı stili korur.

### Tam çalıştırılabilir örnek

Aşağıda, **how to import datatable**'ı gösteren ve sonucu geçerli dizine kaydeden eksiksiz, bağımsız bir konsol programı bulunmaktadır. Yeni bir konsol projesine kopyalayıp çalıştırın.

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace DataTableImportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            string outputPath = Path.Combine(Directory.GetCurrentDirectory(), "Employees.xlsx");
            ExportDataTableToExcel(outputPath);
            Console.WriteLine($"Excel file created at: {outputPath}");
        }

        // Retrieves sample data
        private static DataTable GetSampleData()
        {
            var table = new DataTable("Employees");
            table.Columns.Add("Id", typeof(int));
            table.Columns.Add("Name", typeof(string));
            table.Columns.Add("Department", typeof(string));

            table.Rows.Add(1, "Alice Johnson", "Finance");
            table.Rows.Add(2, "Bob Smith", "Engineering");
            table.Rows.Add(3, "Carol White", "Marketing");
            return table;
        }

        // Configures import options to keep styles
        private static ImportTableOptions CreateImportOptions()
        {
            return new ImportTableOptions
            {
                ImportDataTableStyle = true
            };
        }

        // Performs the import and saves the workbook
        private static void ExportDataTableToExcel(string filePath)
        {
            DataTable dataTable = GetSampleData();
            ImportTableOptions importOptions = CreateImportOptions();

            var workbook = new Workbook();
            Worksheet ws = workbook.Worksheets[0];
            ws.Name = "Employees";

            // Here we answer the core question: how to import datatable
            ws.Cells.ImportDataTable(dataTable, true, importOptions);
            workbook.Save(filePath, SaveFormat.Xlsx);
        }
    }
}
```

**Beklenen çıktı**  
`Employees.xlsx` dosyasını açtığınızda şunları göreceksiniz:

| Id | Name          | Department |
|----|---------------|------------|
| 1  | Alice Johnson | Finance    |
| 2  | Bob Smith     | Engineering|
| 3  | Carol White   | Marketing  |

Tüm hücreler varsayılan DataTable stilini (yazı tipi, hizalama) korur. İçe aktarmadan önce `DataTable`'a özel stiller uyguladıysanız, bu stiller `ImportDataTableStyle` true olarak ayarlandığı için çalışma sayfasında aynı şekilde görünür.

## Yaygın tuzaklar ve en iyi uygulama ipuçları

| Sorun | Neden olur | Nasıl önlenir |
|-------|------------|---------------|
| **Başlıklar eksik** | `ImportDataTable`'a ikinci argüman olarak `false` geçirilmesi sütun adlarını atlar. | Başlıklara ihtiyacınız olduğunda her zaman `true` kullanın veya içe aktarmadan önce manuel olarak yazın. |
| **Stil aktarılmadı** | `ImportDataTableStyle`'ı etkinleştirmeyi unutmak. | `ImportTableOptions` içinde `ImportDataTableStyle = true` ayarlayın. |
| **Büyük tablolar performans gecikmesine neden olur** | Sayfalandırma olmadan milyonlarca satırı içe aktarmak. | Verileri partiler halinde içe aktarın veya verileri akıtmak için `ImportDataTable`'ı `startRow` aşırı yüklemesiyle kullanın. |
| **Yanlış çalışma sayfası referansı** | Sadece bir sayfa olduğunda `workbook.Worksheets[1]` kullanmak. | `workbook.Worksheets[0]` kullanın veya `workbook.Worksheets.Add()` ile yeni bir sayfa oluşturun. |
| **Lisans süresi dolması** | Aspose.Cells deneme sürümü 30 gün sonra filigran ekler. | `License license = new License(); license.SetLicense("Aspose.Cells.lic");` kodu ile geçerli bir lisans uygulayın. |

**Pro ipucu**: İçe aktarmadan sonra özel bir tema uygulamanız gerekiyorsa, `style`'ı bir kez yapılandırıp satırlar arasında yeniden kullandığınız bir `Style` nesnesi olarak `ws.Cells.ApplyStyle(style)` çağırın.

## Çözümü genişletmek

Artık **how to import datatable**'ı bildiğinize göre ilgili senaryoları keşfedebilirsiniz:

* **Birden fazla tablo içe aktarma** – farklı çalışma sayfalarında içe aktarmayı tekrarlayın.
* **Koşullu biçimlendirme** – içe aktarmadan sonra `ws.Cells.ApplyConditionalFormatting` ile kurallar ekleyin.
* **CSV'ye dışa aktarma** – düz metin formatı gerekiyorsa `workbook.Save("file.csv", SaveFormat.Csv)` kullanın.
* **DataTable'a geri okuma** – `ws.Cells.ExportDataTable` kullanarak çift yönlü bütünlüğü doğrulayın.

Bu uzantıların tümü, yukarıda gösterilen temel desen üzerine kuruludur: veriyi al, içe aktarma seçeneklerini yapılandır ve tek bir Aspose.Cells metodunu çağır.

## Sonuç

Artık C# kullanarak bir Excel çalışma sayfasına **how to import datatable** sorusunun eksiksiz, üretim‑hazır cevabına sahipsiniz. Öğreticide kaynak veriyi almayı, `ImportDataTableStyle` ile `ImportTableOptions` yapılandırmayı ve `ImportDataTable` ile içe aktarmayı ele aldık. Kod örneğini izleyerek başlıkları ve stilleri otomatik olarak koruyacak ve bu deseni daha büyük veri kümeleri, birden fazla sayfa veya ek biçimlendirme ihtiyaçları için uyarlayabileceksiniz.

Raporlama iş akışınızı otomatikleştirmeye hazır mısınız? Örnek `DataTable`'ı gerçek bir veritabanı sorgusuyla değiştirin, özel hücre stilleriyle deney yapın ve yöntemi mevcut servis katmanınıza entegre edin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET ile Excel'e Dizi İçe Aktarma: Adım Adım Kılavuz](/cells/english/net/import-export/import-arrays-excel-aspose-cells-net/)
- [Aspose.Cells for .NET ile Excel'e XML Verisi İçe Aktarma: Adım Adım Kılavuz](/cells/english/net/import-export/import-xml-data-net-aspose-cells-guide/)
- [Aspose.Cells for .NET ile Excel'e HTML Biçimli DataTable'lar İçe Aktarma](/cells/english/net/import-export/aspose-cells-net-data-table-import-html-formatting/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}