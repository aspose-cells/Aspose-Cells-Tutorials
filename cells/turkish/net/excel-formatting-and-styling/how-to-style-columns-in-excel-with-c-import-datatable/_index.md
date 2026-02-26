---
category: general
date: 2026-02-21
description: C# kullanarak bir DataTable'ı Excel'e aktarırken sütunları nasıl biçimlendireceğinizi
  öğrenin. İkinci sütunu renklendirme ipuçları ve DataTable'ı Excel'e import etme
  (C#) konularını içerir.
draft: false
keywords:
- how to style columns
- import datatable to excel
- how to import datatable
- color second column excel
- import datatable excel c#
language: tr
og_description: C# kullanarak bir DataTable'ı Excel'e aktarırken sütunları nasıl biçimlendirilir.
  Adım adım kod, Excel'de ikinci sütunu renklendirme ve en iyi uygulamalar.
og_title: C# ile Excel'de Sütunları Stilize Etme – Tam Rehber
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: C# ile Excel’de Sütunları Stil Verme – DataTable’ı İçe Aktarma
url: /tr/net/excel-formatting-and-styling/how-to-style-columns-in-excel-with-c-import-datatable/
---

final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Sütunları C# ile Nasıl Stilize Edilir – DataTable'ı İçe Aktarma

Hiç **sütunları nasıl stilize edeceğinizi** bir Excel çalışma sayfasında doğrudan bir `DataTable`'dan veri çekerken merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, hızlı bir renk dokunuşuna ihtiyaç duyduklarında—belki ilk sütun kırmızı, ikinci sütun mavi—içe aktarmadan sonra her hücreyi manuel olarak ayarlamadan bir engelle karşılaşıyor.  

İyi haber? Cevap birkaç satır C# kodu ve veriler geldiği anda tamamen stilize edilmiş bir sayfaya sahip olacaksınız. Bu öğreticide ayrıca **import datatable to excel**, **color second column excel** konularını da ele alacak ve yaklaşımın hem .NET Framework hem de .NET 6+ projelerinde neden çalıştığını açıklayacağız.

---

## Öğrenecekleriniz

- Dolu bir `DataTable` alın (veya anında oluşturun).  
- Her sütun için `Style` nesneleri tanımlayarak ön plan renklerini ayarlayın.  
- Bir çalışma kitabı oluşturun, ilk çalışma sayfasını alın ve tabloyu stiller uygulanmış şekilde içe aktarın.  
- Boş tablolar, özel başlangıç satırları ve dinamik sütun sayıları gibi kenar durumlarını yönetin.  

Sonunda, stilize bir Excel dosyasını herhangi bir raporlama hattına ekleyebileceksiniz—ek işleme gerek kalmayacak.

> **Önkoşul:** C#'a temel aşinalık ve `ImportDataTable`'ı destekleyen bir elektronik tablo kütüphanesine referans (ör. Aspose.Cells, GemBox.Spreadsheet veya bir yardımcı ile EPPlus). Aşağıdaki kod **Aspose.Cells** kullanıyor çünkü `ImportDataTable` aşırı yüklemesi doğrudan bir `Style[]` kabul ediyor.

## Adım 1: Projeyi Kurun ve Excel Kütüphanesini Ekleyin

Herhangi bir şeyi stilize edebilmemiz için, Excel manipülasyon kütüphanesine referans veren bir projeye ihtiyacımız var.

```csharp
// Install-Package Aspose.Cells -Version 24.7
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;   // For Color
```

*İpucu:* .NET 6 kullanıyorsanız, paketi `dotnet add package Aspose.Cells` komutuyla ekleyin. Kütüphane Windows, Linux ve macOS'ta çalışır, böylece geleceğe hazır olursunuz.

---

## Adım 2: Kaynak DataTable'ı Alın veya Oluşturun

Öğreticinin temel odak noktası stil verme olsa da bir `DataTable`'a ihtiyacınız var. Aşağıda örnek veri oluşturan hızlı bir yardımcı bulunuyor; üretimde kendi `GetTable()` çağrınızla değiştirin.

```csharp
/// <summary>
/// Returns a DataTable with three columns and five rows of demo data.
/// </summary>
static DataTable GetTable()
{
    var dt = new DataTable("Demo");
    dt.Columns.Add("ID", typeof(int));
    dt.Columns.Add("Name", typeof(string));
    dt.Columns.Add("Score", typeof(double));

    dt.Rows.Add(1, "Alice", 92.5);
    dt.Rows.Add(2, "Bob", 85.3);
    dt.Rows.Add(3, "Charlie", 78.9);
    dt.Rows.Add(4, "Diana", 88.1);
    dt.Rows.Add(5, "Ethan", 91.4);

    return dt;
}
```

> **Neden önemli:** `DataTable` kullanmak veri kaynağınızı soyut tutar—SQL, CSV veya bellek içi bir koleksiyon olsun, içe aktarma mantığı aynı kalır. Bu, **how to import datatable** verimli bir şekilde yapmanın temelidir.

## Adım 3: Sütun Stillerini Tanımlayın (“Sütunları Nasıl Stilize Edilir”in Kalbi)

Şimdi çalışma sayfasına her sütunun nasıl görünmesi gerektiğini söylüyoruz. `Style` sınıfı fontları, renkleri, kenarlıkları ve daha fazlasını ayarlamanıza izin verir. Bu örnek için sadece ön plan rengini değiştiriyoruz.

```csharp
// Step 3: Define column styles – red for first, blue for second, default for others
Style[] columnStyles = new Style[3]; // Assuming three columns; adjust as needed

// Style for column 0 (first column) – red text
columnStyles[0] = new Style();
columnStyles[0].ForegroundColor = Color.Red;

// Style for column 1 (second column) – blue text
columnStyles[1] = new Style();
columnStyles[1].ForegroundColor = Color.Blue;

// Column 2 (third column) – keep default styling
columnStyles[2] = new Style(); // No changes, but array entry required
```

*Daha fazla sütununuz olsaydı ne olur?* Sadece dizi boyutunu artırın ve ilgilendiğiniz stilleri doldurun. Stil verilmemiş sütunlar otomatik olarak çalışma sayfasının varsayılan stilini devralır.

## Adım 4: Çalışma Kitabını Oluşturun ve DataTable'ı Stillerle İçe Aktarın

Veri ve stiller hazır olduğunda, her şeyi bir araya getirmenin zamanı geldi.

```csharp
static void Main()
{
    // Retrieve the data
    DataTable dataTable = GetTable();

    // Initialize a new workbook (in‑memory)
    Workbook workbook = new Workbook();

    // Grab the first worksheet (index 0)
    Worksheet worksheet = workbook.Worksheets[0];

    // Import the DataTable starting at cell A1 (row 0, column 0)
    // The 'true' flag tells Aspose.Cells to include column headers
    worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

    // Optional: Auto‑fit columns for a cleaner look
    worksheet.AutoFitColumns();

    // Save the result to disk
    string outputPath = "StyledDataTable.xlsx";
    workbook.Save(outputPath);

    Console.WriteLine($"Excel file saved to {outputPath}");
}
```

**Şimdi ne oldu?**  
- `ImportDataTable` satırları, sütunları ve *isteğe bağlı* başlık satırını kopyalar.  
- `columnStyles` parametresini geçirerek, her sütun daha önce tanımladığımız `Style`'ı alır.  
- Çağrı tek bir satırdır, bu da **import datatable excel c#**'ın bu kadar basit olduğu anlamına gelir.

## Adım 5: Sonucu Doğrulayın – Beklenen Çıktı

`StyledDataTable.xlsx` dosyasını Excel'de (veya LibreOffice'de) açın. Şu şekilde görmelisiniz:

| **ID** (kırmızı) | **Name** (mavi) | **Score** (varsayılan) |
|--------------|-----------------|----------------------|
| 1            | Alice           | 92.5                 |
| 2            | Bob             | 85.3                 |
| …            | …               | …                    |

- İlk sütunun metni **kırmızı** olarak görünür, bu da “sütunları nasıl stilize ederiz” gereksinimini karşılar.  
- İkinci sütunun metni **mavi** olup, **color second column excel** sorgusunu da kapsar.  

Dosya hatasız açılırsa, sütunları stilize ederken **how to import datatable** konusunda başarıyla uzmanlaştınız.

## Yaygın Sorular ve Kenar Durumları

### DataTable boş olursa ne olur?

`ImportDataTable` hâlâ başlık satırını oluşturur (`true` geçirdiyseniz). Veri satırı eklenmez, ancak stiller başlık hücrelerine uygulanır.

### İçe aktarmayı farklı bir hücreden başlatmak mı gerekiyor?

`ImportDataTable` içindeki `rowIndex` ve `columnIndex` parametrelerini değiştirin. Örneğin, `B2`'den başlamak için `0, 0` yerine `1, 1` kullanın.

### Satırları sütunlar yerine stilize etmek ister misiniz?

İçe aktarmadan sonra `worksheet.Cells.Rows` üzerinde döngü yaparak satır başına bir `Style` atayabilirsiniz. Ancak, sütun‑seviyesinde stil vermek çok daha performanslıdır çünkü kütüphane stili her sütun için bir kez uygular.

### EPPlus veya ClosedXML mi kullanıyorsunuz?

Bu kütüphaneler stil dizisiyle doğrudan bir `ImportDataTable` aşırı yüklemesi sunmaz. Çözüm, tabloyu önce içe aktarmak, ardından sütun aralığında döngü yaparak `Style.Font.Color.SetColor(...)` ayarlamaktır. Mantık aynı kalır, sadece birkaç ekstra satır eklenir.

## Üretim‑Hazır Kod İçin Pro İpuçları

- **Stilleri Yeniden Kullan:** Her sütun için yeni bir `Style` oluşturmak israf olabilir. Yeniden kullanılabilir stilleri renk veya font ağırlığına göre anahtarlanan bir sözlükte saklayın.  
- **Sabit Sütun Sayılarından Kaçının:** `dataTable.Columns.Count` değerini tespit edin ve `columnStyles` dizisini dinamik olarak oluşturun.  
- **İş Parçacığı Güvenliği:** Paralel olarak çok sayıda çalışma kitabı oluşturuyorsanız, her iş parçacığı için ayrı bir `Workbook` örneği oluşturun; Aspose.Cells nesneleri iş parçacığı‑güvenli değildir.  
- **Performans:** 10 k'den fazla satır içeren tablolar için `AutoFitColumns`'ı devre dışı bırakmayı (her hücreyi tarar) ve sütun genişliklerini manuel ayarlamayı düşünün.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
// ------------------------------------------------------------
// Full example: How to style columns while importing a DataTable
// ------------------------------------------------------------
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Retrieve data
        DataTable dataTable = GetTable();

        // 2️⃣ Define per‑column styles
        int colCount = dataTable.Columns.Count;
        Style[] columnStyles = new Style[colCount];

        // Red for first column
        columnStyles[0] = new Style { ForegroundColor = Color.Red };

        // Blue for second column (if it exists)
        if (colCount > 1)
            columnStyles[1] = new Style { ForegroundColor = Color.Blue };

        // Default style for remaining columns
        for (int i = 2; i < colCount; i++)
            columnStyles[i] = new Style(); // no special formatting

        // 3️⃣ Create workbook and import with styles
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
        sheet.AutoFitColumns();

        // 4️⃣ Save to file
        string path = "StyledDataTable.xlsx";
        workbook.Save(path);
        Console.WriteLine($"File saved: {path}");
    }

    // Helper: sample DataTable
    static DataTable GetTable()
    {
        var dt = new DataTable("Demo");
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Name", typeof(string));
        dt.Columns.Add("Score", typeof(double));

        dt.Rows.Add(1, "Alice", 92.5);
        dt.Rows.Add(2, "Bob", 85.3);
        dt.Rows.Add(3, "Charlie", 78.9);
        dt.Rows.Add(4, "Diana", 88.1);
        dt.Rows.Add(5, "Ethan", 91.4);
        return dt;
    }
}
```

Programı çalıştırın, oluşturulan `StyledDataTable.xlsx` dosyasını açın ve renkli sütunları anında görün. Bu, **import datatable excel c#** iş akışının tüm özeti.

## Sonuç

C# kullanarak **datatable'ı excel'e içe aktarırken** **sütunları nasıl stilize ederiz** konusunu ele aldık. Bir `Style[]` dizisi tanımlayıp `ImportDataTable`'a geçirerek, ilk sütunu kırmızı, ikinci sütunu mavi renklendirebilir ve geri kalanını dokunulmamış bırakabilirsiniz—hepsi tek bir kod satırıyla.

Yaklaşım ölçeklenebilir: ek sütunlar için daha fazla `Style` nesnesi ekleyin, başlangıç satırlarını ayarlayın veya Aspose.Cells'i benzer bir API'ye sahip başka bir kütüphane ile değiştirin. Artık dosyayı manuel olarak dokunmadan şık Excel raporları oluşturabilirsiniz.

**Sonraki adımlar** keşfedebileceğiniz:

- Değerleri dinamik olarak vurgulamak için **conditional formatting** kullanın (“color second column excel” ile bağlantılı).  
- Tek bir `DataTable` kümesinden birden fazla çalışma sayfası dışa aktarın (aylık panolar için harika).  
- Bunu **CSV → DataTable** dönüşümüyle birleştirerek uç‑uç bir çözüm oluşturun

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}