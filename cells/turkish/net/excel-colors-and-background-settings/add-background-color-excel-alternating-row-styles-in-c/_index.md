---
category: general
date: 2026-04-07
description: C# kullanarak Excel satırlarına arka plan rengi ekleyin. Alternatif satır
  renklerini nasıl uygulayacağınızı, katı arka plan stillerini nasıl ayarlayacağınızı
  ve tek bir iş akışında veri tablosunu Excel'e nasıl aktaracağınızı öğrenin.
draft: false
keywords:
- add background color excel
- apply alternating row colors
- style excel rows
- set solid background
- import datatable to excel
language: tr
og_description: C# ile Excel satırlarına arka plan rengi ekleyin. Bu rehber, alternatif
  satır renkleri uygulamayı, tek renk arka plan ayarlamayı ve veri tablosunu verimli
  bir şekilde Excel'e aktarmayı gösterir.
og_title: Excel'e arka plan rengi ekle – C#'ta alternatif satır stilleri
tags:
- C#
- Excel
- DataTable
- Styling
title: Excel'e arka plan rengi ekle – C#'ta Alternatif Satır Stilleri
url: /tr/net/excel-colors-and-background-settings/add-background-color-excel-alternating-row-styles-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'e Arka Plan Rengi Ekle – C#'ta Alternatif Satır Stilleri

Hiç **add background color excel** satırlarına arka plan rengi eklemeniz gerekti, ama binlerce satırlık karmaşık kod olmadan nasıl yapacağınızı bilmiyor muydunuz? Yalnız değilsiniz—çoğu geliştirici, elektronik tablolarını sadece ham veri yığını olmaktan öteye taşımaya çalıştıklarında bu duvara çarpar.  

İyi haber? Sadece birkaç dakika içinde **apply alternating row colors** uygulayabilir, **solid background** ayarlayabilir ve hatta **import datatable to excel** kullanarak C#'ta temiz, yeniden kullanılabilir bir desenle yapabilirsiniz.  

Bu öğreticide, veriyi bir `DataTable` içine çekmekten her satırı hafif‑sarı‑beyaz şerit deseniyle biçimlendirmeye kadar tüm süreci adım adım göstereceğiz. **ClosedXML** veya **GemBox.Spreadsheet** gibi sağlam bir Excel işleme paketi dışındaki harici kütüphanelere ihtiyaç yoktur ve bu yaklaşımın hem yüksek performanslı hem de bakımının kolay olduğunu göreceksiniz.

## Öğrenecekleriniz

- Veriyi nasıl alıp bir Excel çalışma sayfasına besleyeceğinizi.
- Alternatif arka plan renkleriyle **style excel rows** nasıl yapılır.
- `Style` nesnesini kullanarak **set solid background** mekanizması.
- Satır stillerini koruyarak **import datatable to excel** nasıl yapılır.
- Boş tablolar veya özel renk şemaları gibi kenar durumlarını ele almanın ipuçları.

> **Pro tip:** Zaten stil oluşturmayı destekleyen bir kütüphaneden bir çalışma kitabı nesnesi (`wb`) kullanıyorsanız, aynı `Style` örneklerini birden fazla çalışma sayfasında yeniden kullanabilirsiniz—belleği tasarruf eder ve kodunuzu düzenli tutar.

## Adım 1: Veriyi Alın – DataTable'ı Hazırlama

Herhangi bir biçimlendirme yapılmadan önce satırların kaynağına ihtiyacımız var. Çoğu gerçek dünya senaryosunda bu, bir veritabanı, bir API veya bir CSV dosyasından gelir. Örnek olması için, sadece bellek içinde basit bir `DataTable` oluşturacağız.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using GemBox.Spreadsheet;      // Or ClosedXML, whichever you prefer

// Simulated data fetch – replace with your own data access logic
DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("Id", typeof(int));
    table.Columns.Add("Name", typeof(string));
    table.Columns.Add("Score", typeof(double));

    // Populate with sample rows
    for (int i = 1; i <= 10; i++)
        table.Rows.Add(i, $"Student {i}", Math.Round(new Random().NextDouble() * 100, 2));

    return table;
}
```

**Neden önemli:** `DataTable` kullanmak, Excel kütüphanesinin doğrudan içe aktarabileceği tablo‑tabanlı, şema‑bilinçli bir konteyner sağlar ve hücre‑hücre döngüleri yazma ihtiyacını ortadan kaldırır.

## Adım 2: Satır Stilleri Oluşturma – **Apply alternating row colors**

Şimdi, her satır için bir `Style` nesnesi içeren bir dizi oluşturacağız; böylece her satır kendi arka planını alabilir. Kullanacağımız desen, çift satırlar için klasik hafif‑sarı ve tek satırlar için beyazdır.

```csharp
// Assume 'wb' is an existing Workbook instance
Workbook wb = new Workbook();

// Retrieve data
DataTable dataTable = GetData();

// Allocate a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];

for (int i = 0; i < rowStyles.Length; i++)
{
    // Create a fresh style instance
    rowStyles[i] = wb.CreateStyle();

    // Choose background colour based on row index
    rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;

    // Ensure the colour is actually applied
    rowStyles[i].Pattern = BackgroundType.Solid;   // <-- **set solid background**
}
```

**Açıklama:**  
- `wb.CreateStyle()` size diğerlerini etkilemeden ayarlayabileceğiniz temiz bir stil nesnesi verir.  
- Üçlü operatör `(i % 2 == 0)` satırın çift (hafif sarı) mı yoksa tek (beyaz) mı olduğunu belirler.  
- `Pattern = BackgroundType.Solid` ayarlamak, **set solid background** için kritik adımdır; olmadan renk göz ardı edilir.

## Adım 3: Hedef Çalışma Sayfasını Alın

Çoğu kütüphane bir çalışma sayfası koleksiyonu sunar. İlkini kullanacağız, ancak istediğiniz herhangi bir indeks veya ismi hedefleyebilirsiniz.

```csharp
Worksheet worksheet = wb.Worksheets[0];   // First worksheet in the workbook
```

Çalışma kitabı yeni ise, kütüphane genellikle sizin için varsayılan bir sayfa oluşturur. Aksi takdirde, bir sayfayı açıkça ekleyebilirsiniz:

```csharp
// Alternative: create a new sheet named "Report"
Worksheet worksheet = wb.Worksheets.Add("Report");
```

## Adım 4: DataTable'ı Satır Stilleriyle İçe Aktarın – **Import datatable to excel**

Stiller hazır olduğunda, son adım `DataTable`'ı sayfaya itmek ve her satıra karşılık gelen stili uygulamaktır.

```csharp
// Parameters: (DataTable, includeHeaders, startRow, startColumn, stylesArray)
worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

**Arka planda ne oluyor?**  
- `true` yönteme sütun başlıklarını ilk satır olarak yazmasını söyler.  
- `0, 0` üst‑sol köşeyi (A1) ekleme noktası olarak işaretler.  
- `rowStyles` her `Style`'ı eşleşen veri satırıyla hizalar ve önceden hazırladığımız alternatif renkleri verir.

## Adım 5: Çalışma Kitabını Kaydedin

Bulmacanın son parçası, çalışma kitabını bir dosyaya kaydetmek ve böylece Excel'de açıp sonucu görebilmenizdir.

```csharp
// Choose a format – XLSX is the modern default
wb.Save("StudentScores.xlsx");

// Optional: open automatically (Windows only)
System.Diagnostics.Process.Start("StudentScores.xlsx");
```

Dosyayı açın ve düzgün biçimlendirilmiş bir sayfa görmelisiniz:

- Başlık satırı kalın (varsayılan kütüphane stili).  
- Satır 1, 3, 5… temiz beyaz arka planla.  
- Satır 2, 4, 6… hafif sarı dolgu ile, taramayı kolaylaştırır.

### Beklenen Çıktı Görüntüsü

| Id | Name      | Score |
|----|-----------|-------|
| 1  | Student 1 | 78.45 |
| 2  | Student 2 | 62.13 |
| 3  | Student 3 | 91.27 |
| …  | …         | …     |

Satır 2, 4, 6, … hafif‑sarı arka planla görünür—tam olarak **apply alternating row colors** etkisini elde ederiz.

![Excel arka plan rengi ekleme örneği](https://example.com/excel-background.png "Excel arka plan rengi ekleme örneği")

*(Alt metin, SEO için birincil anahtar kelimeyi içerir.)*

## Kenar Durumları ve Varyasyonlarıyla Baş Etme

### Boş DataTable

`dataTable.Rows.Count` sıfır ise, `rowStyles` dizisi boş olur ve `ImportDataTable` yine de başlık satırını yazar (`includeHeaders` `true` ise). Bir istisna atılmaz, ancak neredeyse boş bir dosya oluşturulmasını önlemek isteyebilirsiniz:

```csharp
if (dataTable.Rows.Count == 0)
{
    Console.WriteLine("No data to export – workbook will contain only headers.");
}
```

### Özel Renk Şemaları

Sarı/beyaz yerine mavi/gri şerit mi istiyorsunuz? Sadece `Color` değerlerini değiştirin:

```csharp
rowStyles[i].ForegroundColor = (i % 2 == 0) ? Color.LightBlue : Color.LightGray;
```

Renkleri bir yapılandırma dosyasından çekmekten çekinmeyin, böylece geliştirici olmayan kişiler kodu dokunmadan paleti ayarlayabilir.

### Birden Çok Çalışma Sayfasında Stilleri Yeniden Kullanma

Aynı çalışma kitabına birden fazla tablo dışa aktarıyorsanız, stil dizisini bir kez oluşturup yeniden kullanabilirsiniz:

```csharp
Style[] sharedStyles = CreateAlternatingStyles(dataTable.Rows.Count);
worksheet1.Cells.ImportDataTable(dt1, true, 0, 0, sharedStyles);
worksheet2.Cells.ImportDataTable(dt2, true, 0, 0, sharedStyles);
```

Sadece her iki tablonun da aynı satır sayısına sahip olduğundan emin olun, yoksa her sayfa için yeni bir dizi oluşturun.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz bağımsız bir program burada.

```csharp
using System;
using System.Data;
using System.Drawing;
using GemBox.Spreadsheet;   // Install-Package GemBox.Spreadsheet

class Program
{
    static void Main()
    {
        // License free for small projects – remove for commercial use
        SpreadsheetInfo.SetLicense("FREE-LIMITED-KEY");

        // 1️⃣ Retrieve data
        DataTable dataTable = GetData();

        // 2️⃣ Initialise workbook
        Workbook wb = new Workbook();

        // 3️⃣ Create alternating row styles
        Style[] rowStyles = CreateAlternatingStyles(dataTable.Rows.Count);

        // 4️⃣ Get (or create) the target worksheet
        Worksheet ws = wb.Worksheets.Add("Report");

        // 5️⃣ Import data with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // 6️⃣ Save the file
        wb.Save("Report.xlsx");
        Console.WriteLine("Excel file created – check Report.xlsx");
    }

    // Helper: generate a DataTable with sample data
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("Id", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        var rnd = new Random();
        for (int i = 1; i <= 12; i++)
            dt.Rows.Add(i, $"Student {i}", Math.Round(rnd.NextDouble() * 100, 2));

        return dt;
    }

    // Helper: create style array for alternating colors
    static Style[] CreateAlternatingStyles(int rowCount)
    {
        var wb = new Workbook();               // Temporary workbook for style creation
        var styles = new Style[rowCount];
        for (int i = 0; i < rowCount; i++)
        {
            styles[i] = wb.CreateStyle();
            styles[i].ForegroundColor = (i % 2 == 0) ? Color.LightYellow : Color.White;
            styles[i].Pattern = BackgroundType.Solid;   // **set solid background**
        }
        return styles;
    }
}
```

Programı çalıştırın, `Report.xlsx` dosyasını açın ve açıklanan şekilde alternatif arka planı göreceksiniz.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}