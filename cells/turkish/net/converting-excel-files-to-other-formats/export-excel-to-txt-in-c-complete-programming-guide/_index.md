---
category: general
date: 2026-08-11
description: C#'ta Excel'i txt'ye dışa aktarın adım adım bir kılavuzla. Aspose.Cells
  kullanarak xlsx dosyasını düz metne nasıl dönüştüreceğinizi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- convert xlsx to plain text
- how to export excel worksheet as text
- export worksheet as text file
language: tr
lastmod: 2026-08-11
og_description: C#'ta Excel'i hızlıca txt'ye aktar. Bu öğreticide xlsx dosyasını düz
  metne nasıl dönüştüreceğiniz, formatları nasıl yapılandıracağınız ve büyük çalışma
  sayfalarını nasıl yöneteceğiniz gösterilmektedir.
og_image_alt: Code snippet that exports an Excel worksheet to a plain text file using
  C#
og_title: C#'ta Excel'i txt'ye aktar – geliştiriciler için adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  headline: Export excel to txt in C# – complete programming guide
  type: TechArticle
- description: Export excel to txt in C# with a step-by-step guide. Learn how to convert
    xlsx to plain text using Aspose.Cells.
  name: Export excel to txt in C# – complete programming guide
  steps:
  - name: – load the workbook
    text: '```csharp using Aspose.Cells;'
  - name: – get the first worksheet
    text: '```csharp Worksheet sheet = workbook.Worksheets[0]; ```'
  - name: – define export options for text conversion
    text: '```csharp ExportTableOptions exportOptions = new ExportTableOptions { ExportAsString
      = true, // Export all values as text DateTimeFormat = "yyyy-MM-dd", // Desired
      date format NumberFormat = "#,##0.00" // Desired numeric format }; ```'
  - name: – export worksheet as text file
    text: '```csharp // Apply the options to the worksheet sheet.ExportTableOptions
      = exportOptions;'
  type: HowTo
tags:
- excel
- csharp
- text export
- aspose.cells
title: C#'ta Excel'i TXT'ye Aktarma – Tam Programlama Rehberi
url: /tr/net/converting-excel-files-to-other-formats/export-excel-to-txt-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i txt'ye Aktar C#'da – tam programlama rehberi

Eğer **excel'i txt'ye aktarmanız** gerekiyorsa, bunu birkaç satır C# kodu ile başarabilirsiniz. Bu rehber, bir `.xlsx` çalışma kitabını, tanımladığınız veri formatını koruyarak düz metin dosyasına nasıl dönüştüreceğinizi gösterir.

Çalışma sayfalarını metin dosyaları olarak dışa aktarmak, alt sistemlerin yalnızca ayrılmış veri kabul ettiği durumlarda veya ham hücre değerlerini denetlemeniz gerektiğinde yaygın bir gereksinimdir. Aşağıdaki bölümlerde tarih ve sayı formatlarını nasıl yapılandıracağınızı, büyük sayfaları nasıl yöneteceğinizi ve tipik tuzaklardan nasıl kaçınacağınızı öğreneceksiniz.

## .xlsx'yi Düz Metne Dönüştürmek İçin Gereksinimler

* .NET 6.0 (veya daha yeni) yüklü – kod .NET Standard 2.0 hedefliyor, bu yüzden .NET Framework 4.6+ ile de çalışır.
* **Aspose.Cells** için bir lisans (ücretsiz değerlendirme testi için çalışır).
* Visual Studio 2022 veya Visual Studio Code gibi bir IDE.
* Projenizden referans alabileceğiniz bir klasöre yerleştirilmiş `input.xlsx` adlı bir Excel dosyası.

Bu öğeler tek dış gereksinimlerdir; eğitim ek NuGet paketlerine bağımlı değildir.

## Aspose.Cells Kullanarak Excel'i Txt'ye Aktarma

Aspose.Cells, hücre değerlerinin string olarak nasıl işleneceğini kontrol etmenizi sağlayan `ExportTableOptions` sınıfını sunar. `ExportAsString` özelliğini `true` olarak ayarlayarak her hücrenin metin olarak yazılmasını sağlarsınız; bu, belirli bir düz metin çıktısı istediğinizde çok önemlidir.

### Adım 1 – Çalışma Kitabını Yükle

```csharp
using Aspose.Cells;

string inputPath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(inputPath);
```

*`Workbook` yapıcı metodu Excel dosyasını belleğe okur. Dosya mevcut değilse bir istisna fırlatılır, bu yüzden üretim kodunda bu çağrıyı bir try‑catch bloğuna sarmak isteyebilirsiniz.*

### Adım 2 – İlk Çalışma Sayfasını Al

```csharp
Worksheet sheet = workbook.Worksheets[0];
```

*Çalışma sayfaları sıfır‑indeksli olduğundan, indeks 0 ilk sekmeye karşılık gelir. Belirli bir sekmeye hedeflemek istediğinizde indeksi bir sayfa adı (`workbook.Worksheets["Sheet1"]`) ile değiştirebilirsiniz.*

### Adım 3 – Metin Dönüşümü İçin Dışa Aktarma Seçeneklerini Tanımla

```csharp
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,               // Export all values as text
    DateTimeFormat = "yyyy-MM-dd",       // Desired date format
    NumberFormat   = "#,##0.00"          // Desired numeric format
};
```

*`ExportAsString`, her hücrenin, özgün tipine bakılmaksızın, çıktı dosyasında bir string olmasını garanti eder. `DateTimeFormat` ve `NumberFormat` özellikleri, tarih ve sayıların nasıl görüneceğini kontrol etmenizi sağlar; bu, **xlsx'yi düz metne dönüştürürken** belirli bir desen bekleyen sistemler için kritik öneme sahiptir.*

### Adım 4 – Çalışma Sayfasını Metin Dosyası Olarak Dışa Aktar

```csharp
// Apply the options to the worksheet
sheet.ExportTableOptions = exportOptions;

// Export the data to a tab‑delimited text file
string outputPath = @"YOUR_DIRECTORY\Exported.txt";
sheet.ExportDataTable(outputPath);
```

*`ExportDataTable`, sağladığınız seçenekleri kullanarak çalışma sayfası içeriğini düz metin dosyasına yazar. Varsayılan ayırıcı bir sekme karakteridir (`\t`). Farklı bir ayırıcıya ihtiyacınız varsa, bir `ExportTableOptions` örneği kabul eden aşırı yüklemeyi kullanabilir ve `ExportTableOptions.Separator` özelliğini belirtebilirsiniz. Oluşan dosya herhangi bir metin düzenleyicide açılabilir veya bir veritabanına içe aktarılabilir.*

#### Beklenen Çıktı

Assume `input.xlsx` contains:

| A            | B       | C          |
|--------------|---------|------------|
| 2023‑05‑01   | 1234.5  | Örnek metin|

With the options above the `Exported.txt` file will contain:

```
2023-05-01	1,234.50	Sample text
```

Her sütun bir sekme ile ayrılır, tarihler `yyyy‑MM‑dd` biçimini izler ve sayılar binlik ayırıcı olarak virgül ve iki ondalık basamak kullanır.

## Çalışma Sayfasını Metin Dosyası Olarak Dışa Aktarırken Yaygın Tuzaklar

| Sorun | Neden Oluşur | Nasıl Önlenir |
|-------|--------------|---------------|
| Yerel‑bağımlı sayı biçimlendirmesi | Varsayılan format işletim sistemi kültürüne göre ayarlanır, bu da tutarsız şekilde virgül veya nokta üretebilir. | `ExportTableOptions` içinde `NumberFormat`'ı açıkça ayarlayın. |
| Gizli satır veya sütunlar çıktıda görünüyor | Aspose.Cells, gizli satırları da içeren tüm kullanılan aralığı dışa aktarır. | Gizli satırları atlamak istiyorsanız `ExportTableOptions.ExportHiddenRows = false` ve `ExportHiddenColumns = false` olarak ayarlayın. |
| Büyük çalışma sayfaları bellek baskısına neden olur | Dışa aktarmadan önce tüm çalışma kitabı belleğe yüklenir. | Bellek kullanımını azaltmak için `Workbook.LoadOptions` ile `LoadDataOnly = true` kullanın veya dosyayı parçalar halinde işleyin. |
| Tarih hücreleri kaynak dosyada metin olarak saklanıyor | Hücre zaten biçimlendirilmiş bir string içeriyorsa, dışa aktarıcı bunu metin olarak kabul eder ve `DateTimeFormat`'ı yok sayar. | Kaynak çalışma kitabının tarihleri doğru Excel tarih tipinde sakladığından emin olun. |

Bu sorunları ele almak, **excel çalışma sayfasını metin olarak dışa aktarma** sürecini farklı ortamlar arasında güvenilir kılar.

## Çözümü Genişletmek – Özel Ayırıcılar ve Akış Dışa Aktarma

Sekme ile ayrılmış bir dosya yerine virgülle ayrılmış değerler (CSV) dosyasına ihtiyacınız varsa, seçenekleri değiştirin:

```csharp
exportOptions.Separator = ',';
exportOptions.ExportHiddenRows = false;   // optional
exportOptions.ExportHiddenColumns = false; // optional
sheet.ExportTableOptions = exportOptions;
sheet.ExportDataTable(@"YOUR_DIRECTORY\Exported.csv");
```

500 MB'den büyük dosyalar için, çıktıyı akış olarak işlemek uygulamanın RAM'i tükenmesinin önüne geçer:

```csharp
using (FileStream stream = new FileStream(@"YOUR_DIRECTORY\LargeExport.txt",
                                          FileMode.Create,
                                          FileAccess.Write,
                                          FileShare.None,
                                          bufferSize: 81920,
                                          useAsync: true))
{
    sheet.ExportDataTable(stream, exportOptions);
}
```

`Stream` kabul eden aşırı yükleme, satırları artımlı olarak yazar; bu, toplu işler veya metin dosyasını doğrudan istemciye dönen web servisleri için idealdir.

## Sonucu Programatik Olarak Doğrula

Dışa aktarma tamamlandıktan sonra, formatı doğrulamak için ilk satırı belleğe geri okuyabilirsiniz:

```csharp
string firstLine = File.ReadLines(outputPath).First();
Console.WriteLine($"First line: {firstLine}");
```

Bu kod parçasını çalıştırmak, *Beklenen çıktı* bölümünde gösterilen aynı satırı yazdırmalı ve dönüşümün başarılı olduğuna dair güven verir.

## Tam Kodun Özeti

Tüm parçaları bir araya getirdiğinizde, bir konsol uygulamasına kopyalayabileceğiniz bağımsız bir program elde edersiniz:

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Paths – adjust to your environment
        string inputPath  = @"YOUR_DIRECTORY\input.xlsx";
        string outputPath = @"YOUR_DIRECTORY\Exported.txt";

        // Load workbook
        Workbook workbook = new Workbook(inputPath);
        Worksheet sheet = workbook.Worksheets[0];

        // Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            DateTimeFormat = "yyyy-MM-dd",
            NumberFormat   = "#,##0.00",
            Separator      = '\t' // tab delimiter
        };

        // Apply options and export
        sheet.ExportTableOptions = exportOptions;
        sheet.ExportDataTable(outputPath);

        // Simple verification
        string firstLine = File.ReadLines(outputPath).First();
        Console.WriteLine($"Export completed. First line: {firstLine}");
    }
}
```

Programı derleyip çalıştırın; `Exported.txt` dosyası kaynak çalışma kitabıyla aynı dizinde ortaya çıkar.

## Sonraki Adımlar ve İlgili Konular

* **Export worksheet as text file** – farklı ayırıcılar, kodlamalar (UTF‑8 vs. ASCII) ve satır sonu stilleriyle deney yaparak çapraz platform uyumluluğunu test edin.
* **Bulk conversion** – her sekme için ayrı bir metin dosyası oluşturmak üzere `workbook.Worksheets` üzerinde döngü yapın.
* **Integration with databases** – oluşturulan metni doğrudan SQL Server veya PostgreSQL için toplu ekleme (bulk‑insert) işlemiyle birleştirin.
* **

## Sonra Ne Öğrenmelisin?

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells ile .NET'te Excel Dosyalarını Dışa Aktarma: Kapsamlı Rehber](/cells/english/net/workbook-operations/export-excel-files-net-aspose-cells-guide/)
- [Aspose.Cells for .NET ile Görünür Excel Satırlarını Dışa Aktarma: Adım Adım Rehber](/cells/english/net/workbook-operations/export-visible-rows-aspose-cells-dotnet/)
- [Aspose.Cells for .NET ile Excel Grafiklerini PDF'e Dışa Aktarma: Adım Adım Rehber](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}