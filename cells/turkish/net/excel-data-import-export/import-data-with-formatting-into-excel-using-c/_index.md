---
category: general
date: 2026-03-01
description: C# kullanarak biçimlendirilmiş verileri Excel'e aktarın. DataTable'ı
  Excel'e nasıl aktaracağınızı ve hücrelere sadece birkaç adımda arka plan rengi eklemeyi
  öğrenin.
draft: false
keywords:
- import data with formatting
- how to import datatable into excel
- add background color to excel cells
language: tr
og_description: C# kullanarak biçimlendirilmiş verileri Excel'e aktarın. DataTable'ı
  nasıl içe aktaracağınızı ve hücrelere arka plan rengi ekleyeceğinizi gösteren adım
  adım rehber.
og_title: Biçimlendirme ile Verileri Excel'e Aktarma – C# Rehberi
tags:
- C#
- Excel
- DataTable
- Formatting
title: C# ile Biçimlendirilmiş Verileri Excel'e Aktarma
url: /tr/net/excel-data-import-export/import-data-with-formatting-into-excel-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'e Biçimlendirme ile Veri Aktarma C# Kullanarak

Hiç bir Excel çalışma kitabına **import data with formatting** yapmanız gerektiğinde, ama sadece sade ve sıkıcı bir sayfa elde ettiğiniz oldu mu? Yalnız değilsiniz. Çoğu geliştirici, varsayılan içe aktarmanın kaynak verilerinizde özenle ayarladığınız tüm renk ve stilleri kaldırdığını keşfettiklerinde bu duvara çarpar.

Bu öğreticide, **imports a DataTable into Excel** ve **adds background color to Excel cells** aynı anda yapan eksiksiz, hemen çalıştırılabilir bir çözümü adım adım inceleyeceğiz. Ek bir son işleme gerek yok—elektronik tablonuz kutudan çıktığı gibi tam istediğiniz gibi görünecek.

## Öğrenecekleriniz

- `DataTable` içine veri almanın nasıl yapılacağını.
- `Style` nesnelerinin bir dizisini, arka plan renklerini taşıyacak şekilde nasıl tanımlayacağınızı.
- `ImportDataTable` metodunu bu stillerle nasıl çağıracağınızı, böylece içe aktarma biçimlendirmeyi korur.
- Konsol uygulamasına ekleyebileceğiniz ve sonucu anında görebileceğiniz tam, çalıştırılabilir bir örnek.
- Gerçek dünya projeleri için ipuçları, tuzaklar ve varyasyonlar.

### Önkoşullar

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Framework 4.6+ ile de çalışır).
- **GemBox.Spreadsheet** kütüphanesi (demo için ücretsiz sürüm yeterlidir).
- C# ve Excel kavramlarına temel aşinalık.

Eğer *neden GemBox?* diye merak ediyorsanız, çünkü tek satırda `ImportDataTable` metodunu sunar ve stil dizilerini kabul eder—döngü yazmadan **import data with formatting** yapmamız için tam olarak ihtiyacımız olan şey.

---

## Adım 1: Projeyi Kurun ve GemBox.Spreadsheet'i Ekleyin

Başlamak için yeni bir konsol uygulaması oluşturun:

```bash
dotnet new console -n ExcelImportDemo
cd ExcelImportDemo
dotnet add package GemBox.Spreadsheet
```

> **Pro tip:** Ücretsiz sürüm, çalışma sayfalarını 150 k hücreyle sınırlar; bu demo için fazladır. Eğer sınıra ulaşırsanız, yükseltin veya EPPlus'a geçin, ancak API biraz farklı görünecektir.

## Adım 2: Kaynak Veriyi `DataTable` Olarak Alın

İlk olarak, normalde bir veritabanından çekeceğiniz veriyi taklit eden bir `DataTable`'a ihtiyacımız var. İşte bellekte bir tane oluşturan küçük bir yardımcı:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register the free license (remove for paid version).
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve the source data as a DataTable.
        DataTable dataTable = GetSampleData();

        // Remaining steps will follow...
    }

    /// <summary>
    /// Generates a sample DataTable with three columns and five rows.
    /// In a real app you’d replace this with a DB call.
    /// </summary>
    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

**Neden önemli?** Veri alımını ayrı bir metoda ayırarak, SQL, CSV, web servisi gibi herhangi bir kaynağı içe aktarma mantığını değiştirmeden değiştirebilirsiniz. Bu kodu temiz tutar ve öğreticiyi **how to import datatable into excel** yeniden kullanılabilir kılar.

## Adım 3: Uygulamak İstediğiniz Stilleri Tanımlayın

Şimdi eğlenceli kısma geliyoruz: her biri farklı bir `ForegroundColor` içeren bir `Style` nesnesi dizisi oluşturacağız. GemBox, `BackgroundPatternColor` (hücre doldurması) ve `ForegroundColor` (metin rengi) ayarlamanıza izin verir. Bu demo için ilk iki sütunu farklı renklerle boyayacağız.

```csharp
        // 2️⃣ Define the styles to apply to the imported cells.
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // Column 0 – Light blue fill
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Column 1 – Light green fill
            // No style for column 2 – it will keep the default look.
        };
```

**Açıklama:**  
- `Style` nesneleri hafif konteynerlerdir; her hücre için yeni bir tane oluşturmanıza gerek yoktur.  
- Dizinin sırasını sütun sırası ile hizalayarak, GemBox içe aktarma sırasında eşleşen stili otomatik olarak uygular.  
- Bu, **import data with formatting** için anahtardır—biçimlendirme verilerle birlikte taşınır, sonradan eklenmez.

## Adım 4: `DataTable`'ı Stillerle Çalışma Sayfasına İçe Aktarın

Veri ve stiller hazır olduğunda, bir çalışma kitabı oluşturabilir, ilk çalışma sayfasını seçebilir ve `ImportDataTable` metodunu çağırabiliriz. Metodun imzası şu şekildedir:

```csharp
public void ImportDataTable(
    DataTable dataTable,
    bool includeColumnNames,
    int startRow,
    int startColumn,
    Style[] columnStyles = null);
```

İşte nasıl kullandığımız:

```csharp
        // 3️⃣ Create a new workbook and import the DataTable.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        // Import, include column headers, start at A1 (0,0), apply our styles.
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the file to disk.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Excel file 'Report.xlsx' created with formatted data.");
```

**Arka planda ne oluyor?**  
- `true`, GemBox'a sütun adlarını ilk satır olarak yazmasını söyler.  
- `0, 0` içe aktarmayı A1 hücresine konumlandırır.  
- `importStyles`, her sütunu daha önce tanımladığımız renklere bağlar.  

*Report.xlsx* dosyasını açtığınızda, **ID** sütununun açık mavi, **Name** sütununun açık yeşil renkte gölgelendiğini ve **Score** sütununun dokunulmadığını göreceksiniz. Bu, tek bir çağrıda **import data with formatting** demektir.

## Adım 5: Sonucu Doğrulayın (Beklenen Çıktı)

Oluşturulan `Report.xlsx` dosyasını açın. Şuna benzer bir şey görmelisiniz:

| ID (açık mavi) | Name (açık yeşil) | Score |
|-----------------|--------------------|-------|
| 1               | Alice              | 93.5 |
| 2               | Bob                | 78.0 |
| 3               | Charlie            | 85.2 |
| 4               | Diana              | 91.3 |
| 5               | Ethan              | 67.8 |

- **ID** sütunu hücreleri açık mavi arka plana sahiptir.  
- **Name** sütunu hücreleri açık yeşil arka plana sahiptir.  
- **Score** sütunu varsayılan beyaz arka planı korur.

Bu görsel ipucu, raporu anında taranabilir kılar—kullanıcı deneyimini büyük ölçüde artırabilecek küçük bir dokunuş.

![Excel sayfası import data with formatting gösteriyor – ID sütunu açık mavi, Name sütunu açık yeşil](excel-screenshot.png "import data with formatting örneği")

*Görsel alt metni, SEO için ana anahtar kelimeyi içerir.*

## Yaygın Sorular & Kenar Durumları

### Arka plan renklerinden daha fazlasını uygulayabilir miyim?

Kesinlikle. `Style` fontları, kenarlıkları, sayı formatlarını ve hatta koşullu biçimlendirmeyi ayarlamanıza izin verir. Örneğin, 90'ın üzerindeki puanları kalın ve kırmızı yapmak için:

```csharp
Style highScoreStyle = new Style()
{
    FontColor = Color.Red,
    FontBold = true
};
worksheet.Cells["C2:C6"].ConditionalFormatting.Add(
    ConditionalFormattingCondition.GreaterThan, "90", highScoreStyle);
```

### DataTable'ım stil sayısından daha fazla sütun içerirse ne olur?

GemBox, sadece dizi içinde eşleşen bir girişe sahip sütunlara stil uygular. Fazla sütunlar varsayılan stile geri döner—hata atılmaz.

### Büyük veri setleriyle çalışır mı?

Evet, ancak ücretsiz sürümün hücre limitine (150 k hücre) dikkat edin. Çok büyük raporlar için, ücretli lisansı düşünün veya veriyi satır‑satır `worksheet.Cells[row, col].Value = …` ile akıtın—bu durumda tek satır kolaylığını kaybedersiniz.

### Mevcut bir Excel şablonundan biçimlendirilmiş veri nasıl içe aktarılır?

Önce bir şablon çalışma kitabı yükleyebilirsiniz:

```csharp
var template = ExcelFile.Load("Template.xlsx");
var targetSheet = template.Worksheets[0];
targetSheet.Cells.ImportDataTable(dataTable, true, 5, 2, importStyles);
template.Save("FilledReport.xlsx");
```

Bu, başlık logolarını, altbilgileri ve önceden var olan stilleri korumanıza izin verirken, dinamik kısım için hâlâ **import data with formatting** yapmanızı sağlar.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıdaki kod tam çalışan örnektir:

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;

class Program
{
    static void Main()
    {
        // Register free license key.
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Get the source data.
        DataTable dataTable = GetSampleData();

        // 2️⃣ Define column styles (background colors).
        Style[] importStyles = new Style[]
        {
            new Style() { BackgroundPatternColor = Color.LightBlue },   // ID column
            new Style() { BackgroundPatternColor = Color.LightGreen }   // Name column
            // Score column gets default style.
        };

        // 3️⃣ Create workbook and import with styles.
        var workbook = new ExcelFile();
        var worksheet = workbook.Worksheets.Add("Report");

        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);

        // Save the result.
        workbook.Save("Report.xlsx");

        Console.WriteLine("Report.xlsx created – import data with formatting complete.");
    }

    static DataTable GetSampleData()
    {
        var table = new DataTable("Report");
        table.Columns.Add("ID", typeof(int));
        table.Columns.Add("Name", typeof(string));
        table.Columns.Add("Score", typeof(double));

        table.Rows.Add(1, "Alice", 93.5);
        table.Rows.Add(2, "Bob", 78.0);
        table.Rows.Add(3, "Charlie", 85.2);
        table.Rows.Add(4, "Diana", 91.3);
        table.Rows.Add(5, "Ethan", 67.8);

        return table;
    }
}
```

Programı çalıştırın (`dotnet run`) ve oluşturulan *Report.xlsx* dosyasını açarak renklerin anında uygulandığını görün.

## Sonuç

Artık sağlam bir temele sahipsiniz,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}