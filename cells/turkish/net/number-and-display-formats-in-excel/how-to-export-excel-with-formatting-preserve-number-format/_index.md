---
category: general
date: 2026-03-22
description: Biçimlendirme ile Excel'i dışa aktarma ve sayı formatını koruma. Excel
  aralığını dönüştürmeyi, formül sonucunu almayı ve Aspose.Cells kullanarak biçimlendirme
  ile Excel'i dışa aktarmayı öğrenin.
draft: false
keywords:
- how to export excel
- preserve number format
- convert excel range
- get formula result
- export excel with formatting
language: tr
og_description: Excel'i biçimlendirme ile dışa aktarma ve sayı formatını koruma. Excel
  aralığını dönüştürme, formül sonucunu alma ve C#'ta biçimlendirme ile Excel'i dışa
  aktarma adım adım rehberi.
og_title: Excel'i Biçimlendirme ile Nasıl Dışa Aktarılır – Sayı Formatını Koru
tags:
- C#
- Aspose.Cells
- Excel automation
title: Excel'i Biçimlendirme ile Dışa Aktarma – Sayı Formatını Koru
url: /tr/net/number-and-display-formats-in-excel/how-to-export-excel-with-formatting-preserve-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i Biçimlendirme ile Dışa Aktarma – Sayı Biçimini Korumak

Hiç **Excel'i nasıl dışa aktaracağınızı** merak ettiniz mi ve her hücrenin görünümünün çalışma kitabında gördüğünüz gibi kalmasını istediniz mi? Belki bir raporu müşteriye göndermeniz, bir grid kontrolüne beslemeniz ya da sadece değerleri bir veritabanına kaydetmeniz gerekiyor. En büyük sorun genellikle sayı biçimlerinin kaybolması ya da formüllerin ham stringlere dönüşmesidir.  

Bu öğreticide, **sayı biçimini koruyan**, **Excel aralığını** bir `DataTable`'a **dönüştüren**, **formül sonucunu** alan ve sonunda **Aspose.Cells** kullanarak **biçimlendirilmiş Excel dışa aktaran** eksiksiz, çalıştırmaya hazır bir C# örneği üzerinden ilerleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz ve bir çalışma sayfası referansı ile çağırabileceğiniz tek bir metoda sahip olacaksınız.

> **Hızlı ön izleme:** kod bir çalışma kitabı oluşturur, bir değer ve bir formül yazar, Aspose.Cells'e hücreleri biçimlendirilmiş stringler olarak dışa aktarmasını söyler ve `123.456 | 246.912` çıktısını verir – tam da Excel'de görmeyi beklediğiniz gibi.

---

## Gereksinimler

- **Aspose.Cells for .NET** (ücretsiz deneme sürümü öğrenme için yeterli)
- .NET 6.0 veya üzeri (API .NET Framework'ta da aynı)
- Temel bir C# geliştirme ortamı (Visual Studio, VS Code, Rider… seçiminize göre)

Aspose.Cells dışındaki ekstra NuGet paketlerine ihtiyaç yoktur. Henüz kurmadıysanız, şu komutu çalıştırın:

```bash
dotnet add package Aspose.Cells
```

---

## Adım 1 – Çalışma Kitabı Oluşturma ve Değer Yazma (formül dahil)

İlk olarak yeni bir çalışma kitabı oluşturup **A1** hücresine sayısal bir değer yerleştiriyoruz. Ardından **B1** hücresine ilk hücreyi ikiyle çarpan basit bir formül ekliyoruz. Bu, daha sonra **formül sonucunu alma** gösterimi için sahneyi hazırlar.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get its first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a numeric value and a formula that uses it
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Continue with export options...
        ExportRangeAsDataTable(worksheet);
    }
}
```

**Neden önemli:**  
- `PutValue` ham sayıyı, `PutFormula` ise hesabı saklar.  
- Aspose.Cells formülü **canlı** tutar, böylece hücrenin değerini istediğimizde gerçekte `246.912` elde ederiz, `"=A1*2"` stringi değil.

---

## Adım 2 – Aspose.Cells'e Değerleri Biçimlendirilmiş Stringler Olarak Dışa Aktarmasını Söyleyin

`ExportDataTable`i varsayılan ayarlarla çağırırsanız, sayısal hücreler temel `double` değerleri olarak döner. Bu, binlik ayırıcıları, para birimi simgelerini veya özel ondalık basamakları kaldırır. `ExportTableOptions` sınıfı sayesinde **sayı biçimini koruyabilir** ve **string olarak dışa aktarabilir**iz.

```csharp
static void ExportRangeAsDataTable(Worksheet worksheet)
{
    // Step 2: Set export options to retrieve values as formatted strings
    ExportTableOptions exportOptions = new ExportTableOptions
    {
        ExportAsString = true,          // Return values as strings
        ExportNumberFormat = true      // Preserve the cell's number format
    };

    // Step 3: Export the range A1:B1 to a DataTable
    DataTable dataTable = worksheet.Cells.ExportDataTable(
        firstRow: 0,
        firstColumn: 0,
        totalRows: 1,
        totalColumns: 2,
        includeColumnNames: true,
        options: exportOptions);

    PrintDataTable(dataTable);
}
```

**Ana nokta:** `ExportNumberFormat = true` bayrağı, **sayı biçimini koruma** işlevini etkinleştirir. Bu olmadan `"123.456"` ve `"246.912"` gibi ham sayılar görürsünüz; kod içinde düzgün görünebilir ama Excel ile aynı biçimlendirmeyi bekleyen bir UI'ye yapıştırdığınızda farklı görünür.

---

## Adım 3 – Dışa Aktarılan Veriyi Yazdırma (Doğrulama)

Şimdi `DataTable`ımız biçimlendirilmiş stringlerle dolu, içeriği konsola dökelim. Bu aynı zamanda **formül sonucunu alma** işlemini, formülü kendimiz değerlendirmeden başarıyla yaptığımızı gösterir.

```csharp
static void PrintDataTable(DataTable table)
{
    // Step 4: Print the exported values (already formatted)
    foreach (DataRow row in table.Rows)
    {
        // The output will look like: 123.456 | 246.912
        Console.WriteLine($"{row[0]} | {row[1]}");
    }
}
```

Programı çalıştırdığınızda şu çıktı görülür:

```
123.456 | 246.912
```

İkinci sütunun **formül sonucunu** gösterdiğine, formül metnini değil, dikkat edin. Bu, **biçimlendirilmiş Excel dışa aktarma** işlemi sırasında aşağı akışta işlemek istediğiniz tam şeydir.

---

## Adım 4 – Daha Büyük Excel Aralıklarını Dönüştürme (Opsiyonel)

Yukarıdaki örnek küçük bir `A1:B1` dilimini ele alıyor, ancak gerçek dünyada genellikle tüm tabloları dışa aktarmak gerekir. Aynı yöntem herhangi bir dikdörtgen blok için çalışır – sadece `firstRow`, `firstColumn`, `totalRows` ve `totalColumns` parametrelerini ayarlamanız yeterlidir.

```csharp
// Example: Export a 10‑row by 5‑column block starting at C3
DataTable bigTable = worksheet.Cells.ExportDataTable(
    firstRow: 2,          // Zero‑based index (C3 = row 2, column 2)
    firstColumn: 2,
    totalRows: 10,
    totalColumns: 5,
    includeColumnNames: true,
    options: exportOptions);
```

**İpucu:** Sayfanızda zaten bir başlık satırı varsa, `includeColumnNames` değerini `true` yapın. Aspose.Cells aralığın ilk satırını sütun adı olarak kullanır; bu, `DataTable`ı bir UI gridine bağladığınızda çok işe yarar.

---

## Adım 5 – Yaygın Tuzaklar ve Çözüm Önerileri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| **Sayılar virgül veya para birimi simgesi kaybeder** | `ExportAsString` `false` veya `ExportNumberFormat` atlanmış | Hem `ExportAsString = true` hem de `ExportNumberFormat = true` ayarlayın. |
| **Formül hücreleri formül metnini döner** | Dışa aktarmadan önce `CalculateFormula` çağırmadınız (çalışma kitabı otomatik hesaplamaya ayarlı değilse gerekir) | Otomatik hesaplamayı etkinleştirin (`workbook.CalculateFormula()`) veya `ExportAsString` kullanın; bu, değerlendirmeyi zorlar. |
| **Başlıklar veri satırı olarak görünür** | `includeColumnNames` `false` iken aralığınızda bir başlık satırı var | `includeColumnNames = true` yaparak ilk satırı sütun adı olarak kabul edin. |
| **Büyük aralıklar bellek baskısı oluşturur** | Tüm sayfayı bir kerede dışa aktarmak tüm veriyi belleğe yükler | Veriyi parçalara (ör. 500 satır) bölerek dışa aktarın ve gerekirse `DataTable`ları birleştirin. |

---

## Adım 6 – Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda `using` ifadelerinden `Main` metoduna kadar tüm program yer alıyor. Bir console uygulamasına yapıştırın ve **F5** tuşuna basın – biçimlendirilmiş çıktıyı anında göreceksiniz.

```csharp
using Aspose.Cells;
using System;
using System.Data;

class ExportExcelDemo
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate cells
        worksheet.Cells["A1"].PutValue(123.456);
        worksheet.Cells["B1"].PutFormula("=A1*2");

        // Export options: keep formatting and return strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            ExportNumberFormat = true
        };

        // Export A1:B1 as a DataTable
        DataTable dataTable = worksheet.Cells.ExportDataTable(
            firstRow: 0,
            firstColumn: 0,
            totalRows: 1,
            totalColumns: 2,
            includeColumnNames: true,
            options: exportOptions);

        // Print results
        foreach (DataRow row in dataTable.Rows)
        {
            Console.WriteLine($"{row[0]} | {row[1]}"); // Expected: "123.456 | 246.912"
        }

        // Keep console window open
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**Beklenen çıktı**

```
123.456 | 246.912

Press any key to exit...
```

İşte **Excel'i nasıl dışa aktaracağınız** iş akışı, biçimlendirme korunmuş, formül sonuçları değerlendirilmiş ve herhangi bir .NET tüketicisi için temiz bir `DataTable` hazır.

---

## Sonuç

**Excel verilerini dışa aktarırken sayı biçimini koruma**, **Excel aralığını `DataTable`a dönüştürme** ve **formül sonuçlarını ekstra ayrıştırma olmadan alma** konularında ihtiyacınız olan her şeyi ele aldık. Anahtar, `ExportTableOptions` yapılandırmasıdır – `ExportAsString` ve `ExportNumberFormat` değerlerini `true` yaptığınızda, Aspose.Cells geri kalanını sizin yerinize halleder.

Bundan sonra şunları yapabilirsiniz:

- `DataTable`ı bir WPF `DataGrid`ine veya ASP.NET MVC görünümüne bağlamak.
- Tabloyu tam görsel temsili koruyarak bir CSV dosyasına yazmak.
- Yaklaşımı birden çok sayfaya veya dinamik aralıklara genişletmek.

Farklı biçimler (para birimi, yüzde) ve daha büyük veri bloklarıyla denemeler yapın. Herhangi bir tuhaflıkla karşılaşırsanız, **yaygın tuzaklar** tablosuna geri dönün – **biçimlendirilmiş Excel dışa aktarma** sırasında en sık karşılaşılan sorunları kapsar.

İyi kodlamalar, ve dışa aktardığınız elektronik tablolar her zaman orijinali kadar şık olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}