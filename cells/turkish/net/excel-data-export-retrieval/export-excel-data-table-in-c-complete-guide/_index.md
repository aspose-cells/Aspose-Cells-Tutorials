---
category: general
date: 2026-03-21
description: Excel veri tablosunu başlıklarla bir DataTable'a aktar, ondalık basamaklarını
  sınırlı tut ve Aspose.Cells kullanarak ilk 100 satırı dışa aktar.
draft: false
keywords:
- export excel data table
- export excel to datatable
- limit decimal places excel
- export first 100 rows
- export excel with headers
language: tr
og_description: Excel veri tablosunu bir DataTable'a nasıl aktaracağınızı, başlıkları
  korumayı, ondalık basamakları sınırlamayı ve C#'ta ilk 100 satırı almayı öğrenin.
og_title: C#'ta Excel Veri Tablosunu Dışa Aktarma – Adım Adım Rehber
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: C#'ta Excel Veri Tablosunu Dışa Aktarma – Tam Kılavuz
url: /tr/net/excel-data-export-retrieval/export-excel-data-table-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Veri Tablosunu Dışa Aktarma – Tam C# Kılavuzu

Bir çalışma kitabından .NET `DataTable`'a **excel veri tablosunu dışa aktar** mı istiyorsunuz? Doğru yerdesiniz—bu kılavuz tam olarak nasıl yapılacağını, sütun başlıklarını korumayı, ondalık basamakları sınırlamayı ve yalnızca ilk 100 satırı çekmeyi gösteriyor.  

Eğer bir zamanlar bir elektronik tabloya bakıp “Bunu uygulamama format kaybı olmadan nasıl alabilirim?” diye düşündüyseniz, yalnız değilsiniz. Önümüzdeki birkaç dakikada bu “ne olurdu” sorusunu Aspose.Cells ile çalışan somut, kopyala‑yapıştır çözümüne dönüştüreceğiz; Aspose.Cells, Excel manipülasyonu için popüler bir kütüphanedir.

## Öğrenecekleriniz

- `ExportDataTable` metodunu kullanarak **excel'i DataTable'a dışa aktar** nasıl yapılır.  
- Orijinal sütun adlarını (`export excel with headers`) koruma.  
- `ExportTableOptions` yapılandırmasıyla **excel'de ondalık basamakları sınırlama** nasıl yapılır.  
- Yalnızca ilk 100 satırı (`export first 100 rows`) güvenli bir şekilde alma.  

Harici betikler, sihirli dizgeler yok—herhangi bir .NET projesine ekleyebileceğiniz sade C# kodu.

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6 veya üzeri (veya .NET Framework 4.7+) | Aspose.Cells her ikisini de destekler, ancak daha yeni çalışma zamanları async‑hazır API'ler sunar. |
| Aspose.Cells for .NET NuGet paketi | `Workbook`, `ExportTableOptions` ve `ExportDataTable` yardımcı aracını sağlar. |
| Örnek bir Excel dosyası (ör. `Numbers.xlsx`) | Dışa aktaracağınız verinin kaynağı. |
| Temel C# bilgisi | Kod parçacıklarıyla ilerleyeceksiniz, ama karmaşık bir şey gerekmiyor. |

Eğer bunlardan biri size yabancı geliyorsa, `dotnet add package Aspose.Cells` komutuyla NuGet paketini alın ve birkaç sayı içeren küçük bir Excel dosyası oluşturun—test veriniz olsun.

![excel veri tablosu dışa aktarım örneği](excel-data-table.png "DataTable'a dışa aktarılacak bir Excel sayfasının ekran görüntüsü")

## Adım 1: Çalışma Kitabını Yükle (excel veri tablosunu dışa aktar)

İlk olarak, Excel dosyanıza işaret eden bir `Workbook` örneğine ihtiyacınız var. Bunu, bir kitabın bölümlerini okuyabilmek için önce kitabı açmak gibi düşünün.

```csharp
using Aspose.Cells;

// 1️⃣ Load the workbook that contains the source data
Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");
```

> **Neden Önemli:** Çalışma kitabını yüklemek, çalışma sayfalarına, hücrelere ve stillere erişim sağlar. Dosya yolu yanlışsa, Aspose bir `FileNotFoundException` fırlatır, bu yüzden konumu iki kez kontrol edin.

## Adım 2: Dışa Aktarım Seçeneklerini Yapılandır – excel'de ondalık basamakları sınırlama

Varsayılan olarak Aspose, her sayısal değeri tam hassasiyetle dışa aktarır. Çoğu zaman, özellikle veriyi bir UI ızgarasına ya da yuvarlanmış sayılar bekleyen bir API'ye beslerken, sadece birkaç anlamlı basamağa ihtiyacınız olur.

```csharp
using Aspose.Cells;

// 2️⃣ Configure export options – keep only 4 significant digits
ExportTableOptions exportOptions = new ExportTableOptions
{
    // This property trims the number of significant digits.
    SignificantDigits = 4
};
```

> **Pro tip:** Farklı bir yuvarlama stratejisine (ör. her zaman yukarı yuvarla) ihtiyacınız varsa, dışa aktardıktan sonra `DataTable` üzerinde post‑process yapabilirsiniz. `SignificantDigits` ayarı, **excel'de ondalık basamakları sınırlama** için ekstra döngüler yazmadan en hızlı yoldur.

## Adım 3: İstenen Aralığı Dışa Aktar (ilk 100 satırı dışa aktar)

Şimdi Aspose'a hangi hücre bloğunu `DataTable`'a çekmek istediğimizi söylüyoruz. Bu öğreticide ilk 100 satırı ve ilk 10 sütunu alıyoruz, ancak senaryonuza göre bu sayıları ayarlayabilirsiniz.

```csharp
using System.Data;
using Aspose.Cells;

// 3️⃣ Export a block of cells (first 100 rows × 10 columns) to a DataTable
DataTable dataTable = workbook.Worksheets[0].Cells.ExportDataTable(
    startRow: 0,          // zero‑based index, first row
    startColumn: 0,       // first column (A)
    totalRows: 100,       // export only the first 100 rows
    totalColumns: 10,     // and the first 10 columns
    exportColumnNames: true, // keep column headers (export excel with headers)
    options: exportOptions);
```

> **Köşe Durumu:** Sayfa 100 satırdan az içeriyorsa, Aspose hata fırlatmadan mevcut olanları dışa aktarır. Yine de beklenmedik şekilde küçük bir aralıkla karşılaşmamak için koruma eklemek isteyebilirsiniz:

```csharp
int rowsToExport = Math.Min(100, workbook.Worksheets[0].Cells.MaxDataRow + 1);
```

## Adım 4: Sonucu Doğrula – Hızlı Konsol Çıktısı

Veriyi hata ayıklayıcınızda görmek güzel, ancak birkaç satırı konsola yazdırmak, **excel'i DataTable'a dışa aktar** işleminin gerçekten çalıştığını ve ondalık basamakların kırpıldığını doğrular.

```csharp
static void PrintDataTable(DataTable table)
{
    foreach (DataRow row in table.Rows)
    {
        foreach (var item in row.ItemArray)
            Console.Write($"{item}\t");
        Console.WriteLine();
    }
}

// Call the helper
PrintDataTable(dataTable);
```

### Beklenen Çıktı

```
ID      Name    Score   Ratio   Date        ...
1       Alice   95.12   0.8234  2023-01-15  ...
2       Bob     88.5    0.7612  2023-01-16  ...
3       Carol   73.33   0.6721  2023-01-17  ...
...
```

Şimdi sayısal sütunların yalnızca dört anlamlı basamak gösterdiğine dikkat edin; bu, daha önce uyguladığımız `SignificantDigits = 4` ayarıyla eşleşiyor.

## Adım 5: Hepsini Birleştir – Tam, Çalıştırılabilir Örnek

Aşağıda, bir konsol uygulamasına kopyala‑yapıştır yapabileceğiniz tam program bulunuyor. Hata yönetimi, isteğe bağlı satır‑sayısı koruması ve yazdırma yardımcı yöntemi dahildir.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class ExportExcelDemo
{
    static void Main()
    {
        try
        {
            // 👉 Load the workbook
            Workbook workbook = new Workbook(@"C:\Path\To\Numbers.xlsx");

            // 👉 Set up export options (limit decimal places excel)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                SignificantDigits = 4
            };

            // 👉 Determine safe row count (export first 100 rows)
            int maxRows = workbook.Worksheets[0].Cells.MaxDataRow + 1;
            int rowsToExport = Math.Min(100, maxRows);

            // 👉 Export to DataTable (export excel to datatable, export excel with headers)
            DataTable dt = workbook.Worksheets[0].Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: rowsToExport,
                totalColumns: 10,
                exportColumnNames: true,
                options: exportOptions);

            // 👉 Show a glimpse of the data
            PrintDataTable(dt);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }

    static void PrintDataTable(DataTable table)
    {
        foreach (DataRow row in table.Rows)
        {
            foreach (var item in row.ItemArray)
                Console.Write($"{item}\t");
            Console.WriteLine();
        }
    }
}
```

Programı çalıştırın, ve sayfanızın ilk 100 satırını, güzelce yuvarlanmış ve sütun adları korunmuş şekilde göreceksiniz.

## Yaygın Sorular & Tuzaklar

| Soru | Cevap |
|----------|--------|
| **Sayfamda birleştirilmiş hücreler varsa ne olur?** | `ExportDataTable` birleştirilmiş hücreleri, sol‑üst hücrenin değerini alarak düzleştirir. Özel bir işleme ihtiyacınız varsa, önce birleştirmeyi kaldırın ya da ham `Cell` nesnelerini okuyun. |
| **Bunun yerine bir `DataSet`'e dışa aktarabilir miyim?** | Evet—`ExportDataTable` kullanın |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}