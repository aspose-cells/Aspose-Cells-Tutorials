---
category: general
date: 2026-05-04
description: C# ile özel biçimlendirme kullanarak çalışma sayfası aralığını dışa aktarın.
  Excel aralığını nasıl dışa aktaracağınızı ve hücre dışa aktarmayı nasıl özelleştireceğinizi
  birkaç kolay adımda öğrenin.
draft: false
keywords:
- export worksheet range
- how to export excel range
- how to customize cell export
- C# Excel export
- worksheet export options
language: tr
og_description: C# ile çalışma sayfası aralığını dışa aktarın. Bu kılavuz, Excel aralığını
  nasıl dışa aktaracağınızı ve hücre dışa aktarımını hızlı ve güvenilir bir şekilde
  nasıl özelleştireceğinizi gösterir.
og_title: C#'de Çalışma Sayfası Aralığını Dışa Aktarma – Tam Programlama Rehberi
tags:
- C#
- Excel
- Data Export
title: C#'de Çalışma Sayfası Aralığını Dışa Aktarma – Tam Programlama Rehberi
url: /tr/net/excel-data-export-retrieval/export-worksheet-range-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta Çalışma Sayfası Aralığını Dışa Aktarma – Tam Programlama Rehberi

Hiç **export worksheet range** ihtiyacınız oldu mu, ancak varsayılan çıktı istediğiniz gibi değildi? Tek başınıza değilsiniz—birçok geliştirici, hücre bloğunu bir CSV veya JSON dosyasına çekmeye çalıştığında bu engelle karşılaşıyor. İyi haber? Birkaç C# satırıyla sadece **export excel range** değil, aynı zamanda **customize cell export** da yapabilirsiniz, böylece herhangi bir sonraki formatla eşleşir.

Bu öğreticide gerçek bir senaryoyu adım adım inceleyeceğiz: bir Excel çalışma kitabından *A1:D10* hücrelerini alıp, her değeri köşeli parantezli bir dizeye dönüştürmek ve sonucu bir dosyaya yazmak. Sonunda **how to export worksheet range** (çalışma sayfası aralığını nasıl dışa aktaracağınızı) tam kontrolle, her hücrenin temsilini nasıl yöneteceğinizi ve daha sonra karşılaşabileceğiniz uç durumlar için birkaç ipucu öğreneceksiniz.

## İhtiyacınız Olanlar

- .NET 6 veya daha yenisi (kod .NET Framework 4.7+ ile de çalışır)  
- **GemBox.Spreadsheet** NuGet paketi (veya `ExportTableOptions` sağlayan herhangi bir kütüphane; gösterilen API GemBox’tan alınmıştır)  
- C# sözdizimi hakkında temel bir anlayış – karmaşık bir şey değil, sadece tipik `using` ifadeleri ve nesne oluşturma  

Eğer bunlara sahipseniz, derinlemesine incelemeye hazırsınız.

## Adım 1: Dışa Aktarma Seçeneklerini Ayarlama – Birincil Kontrol Noktası  

İlk olarak bir `ExportTableOptions` örneği oluşturur ve her hücreyi bir string olarak ele almasını söylersiniz. Bu, veri tipini tutarlı tutarken **how to export excel range** (excel aralığını nasıl dışa aktaracağınızı) temin eden temeldir.

```csharp
using GemBox.Spreadsheet;

public class WorksheetExporter
{
    public void ExportRange(string sourcePath, string destinationPath)
    {
        // Load the workbook.
        var workbook = ExcelFile.Load(sourcePath);
        var worksheet = workbook.Worksheets[0]; // assume first sheet

        // Step 1: Create export options and enable string export.
        var exportOptions = new ExportTableOptions
        {
            ExportAsString = true // forces every cell to be exported as text
        };
```

*Neden string dışa aktarımı zorunlu kılınsın?*  
Daha sonra her hücreyi özelleştirdiğinizde, köşeli parantezler ve muhtemelen başka semboller ekleyeceksiniz. Her şeyi string olarak tutmak, tip dönüşümü sürprizlerini önler (ör. tarihlerin seri numaralarına dönüşmesi).

## Adım 2: CellExport Olayına Bağlanma – Her Hücreyi Özelleştirme  

Şimdi eğlenceli kısım geliyor: **how to customize cell export** (hücre dışa aktarmayı nasıl özelleştirirsiniz). GemBox, yazılmak üzere olan her hücre için bir `CellExport` olayı tetikler. Bunu işleyerek değeri köşeli parantez içine alabilir, bir önek ekleyebilir veya hatta bir hücreyi tamamen atlayabilirsiniz.

```csharp
        // Step 2: Customize each cell's exported value.
        exportOptions.CellExport += (sender, e) =>
        {
            // e.Value holds the original cell content.
            // We'll wrap it in square brackets.
            e.Value = $"[{e.Value}]";
        };
```

*Pro ipucu:* Yalnızca sayısal hücreleri değiştirmek istiyorsanız, köşeli parantezleri uygulamadan önce `e.Value.GetType()` kontrol edin. Bu küçük koruma, başlık metnini istemeden bozmanızı önleyebilir.

## Adım 3: İstenen Aralığı Dışa Aktarma – Temel Eylem  

Seçenekler hazır olduğunda `ExportTable` metodunu çağırırsınız. Bu metod, yüklediğiniz çalışma kitabını, istediğiniz aralığın adresini ve az önce yapılandırdığınız seçenekleri alır.

```csharp
        // Step 3: Export the range A1:D10 using the configured options.
        worksheet.ExportTable(workbook, "A1:D10", exportOptions, destinationPath);
    }
}
```

Kullandığımız aşırı yükleme doğrudan bir dosyaya (varsayılan olarak CSV) yazar. Bellek içi bir dize tercih ediyorsanız, son argümanı bir `StringWriter` ile değiştirin ve ardından sonucu okuyun.

### Tam Çalışan Örnek

Aşağıda, yeni bir projeye yapıştırıp anında çalıştırabileceğiniz (dosya yollarını değiştirmeniz yeterli) bağımsız bir konsol uygulaması bulunmaktadır.

```csharp
using System;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // License key (free version works with limited rows/columns).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        var exporter = new WorksheetExporter();
        exporter.ExportRange(
            sourcePath: @"C:\Temp\Sample.xlsx",
            destinationPath: @"C:\Temp\ExportedRange.csv");

        Console.WriteLine("Export completed. Check C:\\Temp\\ExportedRange.csv");
    }
}
```

**Beklenen çıktı (CSV kesiti):**

```
[Header1],[Header2],[Header3],[Header4]
[123],[456],[789],[012]
[ABC],[DEF],[GHI],[JKL]
...
```

*A1*'den *D10*'a kadar her hücre artık köşeli parantez içinde, `CellExport` işleyicisinde tanımladığımız gibi.

## Yaygın Uç Durumları Ele Alma  

### 1. Boş Hücreler  
Bir hücre boşsa, `e.Value` `null` olacaktır. String interpolasyonu ile biçimlendirmeye çalışmak bir istisna fırlatır. Buna karşı koruma sağlayın:

```csharp
exportOptions.CellExport += (s, e) =>
{
    var raw = e.Value?.ToString() ?? string.Empty;
    e.Value = $"[{raw}]";
};
```

### 2. Büyük Aralıklar  
Milyonlarca satırı dışa aktarmak bellek sınırlarına çarpabilir. Bu durumda, tüm çalışma kitabını belleğe yüklemek yerine çıktıyı akış olarak gönderin:

```csharp
using (var writer = new StreamWriter(destinationPath))
{
    worksheet.ExportTable(workbook, "A1:D1000000", exportOptions, writer);
}
```

### 3. Farklı Ayırıcılar  
CSV tek ihtiyacınız olabilecek tek format değildir. Ayırıcıyı `ExportTableOptions.CsvSeparator` ayarlayarak değiştirin:

```csharp
exportOptions.CsvSeparator = '\t'; // Tab‑delimited
```

## Sık Sorulan Sorular  

**S: Bu, Excel 365 tarafından oluşturulan .xlsx dosyalarıyla çalışır mı?**  
Kesinlikle. GemBox, ek yapılandırma gerektirmeden modern OpenXML formatını okur.

**S: Tek seferde birden fazla ayrı aralığı dışa aktarabilir miyim?**  
Tek bir `ExportTable` çağrısıyla doğrudan mümkün değildir. Her aralık dizesi (`"A1:D10"`, `"F1:H5"` vb.) üzerinde döngü yapın ve çıktıları kendiniz birleştirin.

**S: Her sütun için farklı biçimlendirme uygulamam gerekirse ne olur?**  
`CellExport` işleyicisinin içinde `e.ColumnIndex` erişiminiz vardır. Sütuna özgü mantığı uygulamak için bir `switch` ifadesi kullanın.

## Özet  

**how to export worksheet range** (çalışma sayfası aralığını nasıl dışa aktaracağınızı) her hücrenin görünümü üzerinde tam kontrolle ele aldık, `ExportTableOptions` kullanarak **how to export excel range** (excel aralığını nasıl dışa aktaracağınızı) gösterdik ve `CellExport` olayıyla **how to customize cell export** (hücre dışa aktarmayı nasıl özelleştireceğinizi) sergiledik. Tam çözüm birkaç düzine C# satırında yer alıyor, ancak üretim‑düzeyi senaryolar için yeterince esnek.

Sonraki adımlar? Köşeli parantez sarmalayıcısını JSON‑uyumlu bir formatla değiştirmeyi deneyin veya gizli satırları atlayan koşullu mantıkla deney yapın. Ayrıca web‑API yanıtları için doğrudan bir `MemoryStream`'e dışa aktarmayı keşfedebilirsiniz—geçici dosyalara gerek yok.

Eğer bu adımları izlediyseniz, artık ihtiyacınıza tam olarak uyan herhangi bir çalışma sayfası aralığını dışa aktarmak için sağlam, yeniden kullanılabilir bir modele sahipsiniz. Kodlamanın tadını çıkarın ve bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}