---
category: general
date: 2026-10-10
description: C#'ta Excel şablonunu nasıl işleyip sayfaları otomatik olarak adlandıracağınızı
  öğrenin. SmartMarkerProcessor kodu ve en iyi uygulamalarla adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- process excel template
- automatically name sheets
- SmartMarkerProcessor
- Excel automation C#
- worksheet data binding
language: tr
lastmod: 2026-10-10
og_description: Excel şablonunu C# ile işleyin ve SmartMarkerProcessor ile sayfaları
  otomatik olarak adlandırın. Dinamik çalışma kitapları oluşturmak için bu ayrıntılı
  öğreticiyi izleyin.
og_image_alt: Screenshot showing process excel template with automatically named sheets
  in a C# application
og_title: Excel şablonunu işleyin ve C#'ta sayfaları otomatik olarak adlandırın –
  tam rehber
schemas:
- author: GroupDocs
  dateModified: '2026-10-10'
  description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  headline: How to process Excel template and automatically name sheets in C#
  type: TechArticle
- description: Learn how to process Excel template in C# while automatically name
    sheets. Step‑by‑step guide with SmartMarkerProcessor code and best practices.
  name: How to process Excel template and automatically name sheets in C#
  steps:
  - name: Large data sets
    text: 'When the data source contains hundreds of rows, the processor creates a
      separate sheet for each row by default. To keep the workbook from exploding,
      you can:'
  - name: Existing sheet name conflicts
    text: If the template already contains a sheet named `Detail`, the processor appends
      a numeric suffix to avoid collision (`Detail_0`, `Detail_1`, …). To enforce
      a custom conflict‑resolution strategy, inspect `Worksheet.Sheets` before processing
      and rename any conflicting sheets.
  - name: Non‑Excel templates
    text: The same `SmartMarkerProcessor` can process Word, PowerPoint, or PDF templates.
      The only change is the class you instantiate (`Document`, `Presentation`, etc.).
      The **process excel template** pattern stays identical, which means you can
      reuse the code with minimal adjustments.
  type: HowTo
tags:
- Excel
- C#
- SmartMarker
- Automation
title: Excel şablonunu işlemek ve C#'ta sayfaları otomatik olarak adlandırmak
url: /tr/net/templates-reporting/how-to-process-excel-template-and-automatically-name-sheets/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel şablonunu işleme ve C#'ta sayfaları otomatik olarak adlandırma

Bir .NET uygulamasında **Excel şablonunu işlemek** istiyorsanız, bu kılavuz size çalışma kitapları oluşturmanın ve **sayfaları otomatik olarak adlandırmanın** güvenilir bir yolunu gösterir. GroupDocs.Parser'ın `SmartMarkerProcessor`'ını kullanarak verileri bir şablona bağlayabilir, detay sayfalarını anında oluşturabilir ve çalışma kitabını manuel yeniden adlandırma yapmadan düzenli tutabilirsiniz.

Kılavuzu, bir şablonu okuyan, bir veri kaynağı uygulayan ve `Detail`, `Detail_1`, `Detail_2`, … adlı sayfalar üreten tamamen çalıştırılabilir bir örnekle tamamlayacaksınız. Gerekli tüm ad alanları, yapılandırma adımları ve yaygın hatalar ele alındı, böylece kodu kendi projenize güvenle kopyalayabilirsiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* .NET 6.0 veya üzeri (kod .NET Core ve .NET Framework ile çalışır)
* **GroupDocs.Parser** NuGet paketine referans (versiyon 23.5 veya daha yeni)
* SmartMarker etiketleri (ör. `{{Table}}`) içeren bir Excel şablonu (`Template.xlsx`)
* Şablondaki etiketlerle eşleşen basit bir veri modeli (ör. `DataTable` veya nesne listesi)

Bu öğelerden herhangi biri eksikse, NuGet paketini aşağıdaki komutla kurun:

```bash
dotnet add package GroupDocs.Parser
```

## Çözümün Genel Görünümü

Çözüm üç mantıksal aşamayı izler:

1. **`SmartMarkerProcessor` örneği oluşturun** – bu nesne tüm şablon motorunu yönlendirir.
2. **İşlemciyi detay sayfalarını otomatik olarak adlandıracak şekilde yapılandırın** – `DetailSheetNewName` seçeneği temel adı tanımlar ve kütüphane artan ekler ekler.
3. **`Process` metodunu çalıştırın** – metod şablonu okur, veri kaynağını birleştirir ve sonucu yeni bir çalışma kitabına yazar.

Her aşama aşağıda, ihtiyacınız olan tam kodla birlikte açıklanmıştır.

## Adım 1: SmartMarkerProcessor Örneği Oluşturma

İşlemci, tüm SmartMarker işlemlerinin giriş noktasıdır. Herhangi bir yapıcı argümana ihtiyaç duymaz, ancak ileri düzey ayarlara ihtiyacınız olursa daha sonra özel bir `SmartMarkerOptions` nesnesi geçirebilirsiniz.

```csharp
using GroupDocs.Parser;
using GroupDocs.Parser.Options;

// ...

// Step 1: Instantiate the processor
SmartMarkerProcessor processor = new SmartMarkerProcessor();
```

*Why this matters*: İşlemciyi her işlem için bir kez örneklemek bellek kullanımını düşük tutar ve gerektiğinde aynı nesneyi birden fazla şablon için yeniden kullanmanıza olanak tanır.

## Adım 2: Otomatik Sayfa Adlandırmayı Yapılandırma

Bir master‑detail tablosu ayrı çalışma sayfalarına genişlediğinde, kütüphane yeni sayfaları otomatik olarak oluşturur. `DetailSheetNewName` ayarını yaparak motorun kullandığı temel adı kontrol edersiniz. Kütüphane, her ek sayfa için bir alt çizgi ve artan bir sayı ekler.

```csharp
// Step 2: Define the base name for automatically created detail sheets
processor.Options.DetailSheetNewName = "Detail"; // Sheets become Detail, Detail_1, Detail_2, …
```

*İpuçları*:

* Şablondaki mevcut sayfa adlarıyla çakışmayan bir temel ad seçin.
* Adlandırma şeması, herhangi bir sayıda detay satırı için çalışır; kütüphane son sayfa oluşturulduğunda ek eklemeyi durdurur.
* Farklı bir adlandırma deseni (ör. ek yerine ön ek) gerekiyorsa, her çağrıdan önce `processor.Options.DetailSheetNewName` değerini değiştirebilirsiniz.

## Adım 3: Çalışma Sayfasını Bir Veri Kaynağıyla İşleyin

`Process` metodu üç argüman alır:

* **kaynak çalışma sayfası** (`Worksheet` nesnesi) – şablon dosyasını yükleyerek elde edersiniz.
* **hedef akış** – işlenmiş çalışma kitabının yazılacağı yer.
* **veri kaynağı** – `IDataSource` arayüzünü uygulayan herhangi bir nesne (ör. `DataTable`, `IEnumerable<T>`).

Aşağıda `Template.xlsx` dosyasını yükleyen, bir `DataTable` bağlayan ve sonucu `Result.xlsx` olarak kaydeden eksiksiz bir örnek yer alıyor.

```csharp
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

// ...

// Load the Excel template into a Worksheet object
using (FileStream templateStream = File.OpenRead("Template.xlsx"))
{
    // Create a Worksheet instance from the template
    Worksheet ws = new Worksheet(templateStream);

    // Prepare a simple DataTable as the data source
    DataTable dt = new DataTable("Employees");
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Department", typeof(string));
    dt.Columns.Add("Salary", typeof(decimal));

    // Populate the table with sample rows
    dt.Rows.Add("Alice", "Engineering", 95000);
    dt.Rows.Add("Bob", "Marketing", 72000);
    dt.Rows.Add("Charlie", "Sales", 68000);

    // Wrap the DataTable in a DataSource object required by SmartMarker
    IDataSource dataSource = new DataTableSource(dt);

    // Step 1 and Step 2 have already been performed earlier
    // Now process the worksheet
    using (MemoryStream resultStream = new MemoryStream())
    {
        processor.Process(ws, dataSource, resultStream);

        // Write the processed workbook to a physical file
        File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
    }
}
```

*Ana satırların açıklaması*:

* `new Worksheet(templateStream)` Excel dosyasını okur ve SmartMarker'ın manipüle edebileceği bellek içi bir temsil oluşturur.
* `DataTableSource` `IDataSource` arayüzünü uygular, işlemcinin satırları döndürmesine ve `{{Employees.Name}}` gibi etiketleri değiştirmesine olanak tanır.
* `processor.Process(ws, dataSource, resultStream)` verileri birleştirir ve son çalışma kitabını `resultStream`'e yazar. Metod, Adım 2'de ayarlanan seçenek sayesinde `Detail`, `Detail_1` vb. adlarda detay sayfaları otomatik olarak oluşturur.
* İşlemden sonra sonuç `Result.xlsx` olarak kaydedilir. Excel'de dosyayı açarak üç detay sayfasının mevcut olduğunu ve her birinin `Employees` tablosundaki satırları içerdiğini doğrulayın.

## Çıktıyı Doğrulama

`Result.xlsx` dosyasını açın ve aşağıdakileri kontrol edin:

| Sayfa adı | Beklenen içerik |
|------------|------------------|
| Detail | Başlık satırı (`Name`, `Department`, `Salary`) ve ilk veri satırı (`Alice`) |
| Detail_1 | İkinci veri satırı (`Bob`) |
| Detail_2 | Üçüncü veri satırı (`Charlie`) |

Sayfalar doğru temel ad ve artan eklerle görünüyor ise **Excel şablonunu işleme** akışı başarılı olmuş ve **sayfaları otomatik olarak adlandırma** özelliği amaçlandığı gibi çalışmıştır.

## Kenar Durumlarını Ele Alma

### Büyük Veri Setleri

Veri kaynağı yüzlerce satır içerdiğinde, işlemci varsayılan olarak her satır için ayrı bir sayfa oluşturur. Çalışma kitabının aşırı büyümesini önlemek için şunları yapabilirsiniz:

* **Satırları gruplayın**: şablonu, her satır için yeni bir sayfa oluşturmak yerine tek bir sayfada tekrarlanan bir tablo işareti kullanacak şekilde değiştirin.
* **Sayfa oluşturmayı sınırlayın**: `processor.Options.MaxDetailSheets` değerini makul bir sayıya (ör. 50) ayarlayın ve taşmayı manuel olarak yönetin.

```csharp
processor.Options.MaxDetailSheets = 50; // Prevent more than 50 auto‑generated sheets
```

### Mevcut Sayfa Adı Çakışmaları

Şablonda zaten `Detail` adlı bir sayfa varsa, işlemci çakışmayı önlemek için sayfaya sayısal bir ek ekler (`Detail_0`, `Detail_1`, …). Özel bir çakışma çözüm stratejisi uygulamak için işlemden önce `Worksheet.Sheets` koleksiyonunu inceleyin ve çakışan sayfaları yeniden adlandırın.

```csharp
foreach (var sheet in ws.Sheets)
{
    if (sheet.Name.Equals("Detail", StringComparison.OrdinalIgnoreCase))
    {
        sheet.Name = "BaseDetail";
    }
}
```

### Excel Olmayan Şablonlar

Aynı `SmartMarkerProcessor` Word, PowerPoint veya PDF şablonlarını da işleyebilir. Tek değişiklik, örneklediğiniz sınıf (`Document`, `Presentation` vb.) olur. **Excel şablonunu işleme** deseni aynı kalır, bu da kodu minimal ayarlamalarla yeniden kullanabileceğiniz anlamına gelir.

## Üretim Kullanımı için Profesyonel İpuçları

* **İşlemciyi yeniden kullanın**: bir web hizmetinde birçok şablon işliyorsanız singleton `SmartMarkerProcessor` oluşturun. Bu, tahsis yükünü azaltır.
* **Dosya yerine akış kullanın**: yüksek verim senaryolarında, şablonu ve sonucu disk I/O'dan kaçınmak için bellek akışlarında tutun.
* **Nesneleri serbest bırakın**: Tüm `Worksheet`, `FileStream` ve `MemoryStream` örnekleri `IDisposable` uygular. Gösterildiği gibi `using` blokları kullanmak, kaynakların doğru şekilde serbest bırakılmasını sağlar.
* **Günlükleme**: Ayrıntılı işlem bilgilerini yakalamak için `processor.Options.Logging`'i etkinleştirin; bu, şablon hatalarını hızlıca teşhis etmenize yardımcı olur.

## Tam Çalıştırılabilir Örnek

Aşağıda tüm program tek bir dosyada derlenmiş olarak verilmiştir. Bir console projesine kopyalayıp çalıştırın; çıktı çalışma kitabı proje klasöründe görünecektir.

```csharp
using System;
using System.Data;
using System.IO;
using GroupDocs.Parser;
using GroupDocs.Parser.Data;
using GroupDocs.Parser.Options;

class ExcelTemplateProcessor
{
    static void Main()
    {
        // 1️⃣ Create the processor
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // 2️⃣ Set automatic sheet naming
        processor.Options.DetailSheetNewName = "Detail";

        // Load the template
        using (FileStream templateStream = File.OpenRead("Template.xlsx"))
        {
            Worksheet ws = new Worksheet(templateStream);

            // Build a sample data source
            DataTable dt = new DataTable("Employees");
            dt.Columns.Add("Name", typeof(string));
            dt.Columns.Add("Department", typeof(string));
            dt.Columns.Add("Salary", typeof(decimal));
            dt.Rows.Add("Alice", "Engineering", 95000);
            dt.Rows.Add("Bob", "Marketing", 72000);
            dt.Rows.Add("Charlie", "Sales", 68000);
            IDataSource dataSource = new DataTableSource(dt);

            // 3️⃣ Process the worksheet
            using (MemoryStream resultStream = new MemoryStream())
            {
                processor.Process(ws, dataSource, resultStream);
                File.WriteAllBytes("Result.xlsx", resultStream.ToArray());
            }
        }

        Console.WriteLine("Processing complete. Check Result.xlsx.");
    }
}
```

Programı çalıştırdığınızda “Processing complete. Check Result.xlsx.” mesajı yazdırılır ve **Excel şablonunu işleme** akışını **sayfaları otomatik olarak adlandırma** özelliğiyle gösteren bir Excel dosyası oluşturulur.

## Sonuç

Artık C# içinde **Excel şablonlarını işleme** ve kütüphanenin **sayfaları otomatik olarak adlandırmasını** özel bir temel ada göre nasıl yapacağınızı biliyorsunuz. Kılavuz, işlemci oluşturma, seçenek yapılandırma, veri bağlama ve doğrulama adımlarını, kenar durumları yönetimini ve üretim ipuçlarını kapsadı. Aynı deseni daha büyük projelere uygulayın, web API'lerine entegre edin veya diğer Office formatlarına genişletin.

**İleride keşfedebileceğiniz adımlar**:

* `processor.Options.DetailSheetNewName`'i dinamik değerlerle (ör. tarih veya kullanıcı kimliği) kullanın.
* Birden fazla veri kaynağını birleştirerek birkaç çalışma sayfası üzerinde master‑detail hiyerarşileri oluşturun.
* SmartMarker etiketlerini stilize ederek yazı tiplerini, renkleri ve sayı formatlarını doğrudan şablondan kontrol etmeyi deneyin.

Kodlamanın tadını çıkarın ve sorunsuz Excel otomasyonunun keyfini sürün!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Şablondan Excel Oluşturma – .NET Geliştiricileri için Adım Adım Kılavuz](/cells/english/net/templates-reporting/create-excel-from-template-step-by-step-guide-for-net-develo/)
- [Aspose.Cells for .NET Kullanarak Excel Sayfalarını Birleştirme ve Yeniden Adlandırma: Adım Adım Kılavuz](/cells/english/net/worksheet-management/merge-rename-excel-sheets-aspose-cells-net/)
- [SmartMarker ile Excel Sayfalarını Bağlama – Adım Adım Kılavuz](/cells/english/net/smart-markers-dynamic-data/how-to-link-sheets-in-excel-with-smartmarker-step-by-step-gu/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}