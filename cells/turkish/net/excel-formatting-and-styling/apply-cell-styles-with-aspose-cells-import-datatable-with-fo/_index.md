---
category: general
date: 2026-06-05
description: Aspose.Cells içe aktarma sırasında hücre stillerini uygulayın. Biçimlendirme
  ile DataTable'ı nasıl içe aktaracağınızı, satırları nasıl stillendireceğinizi ve
  çalışma sayfalarını düzenli tutacağınızı öğrenin.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: tr
og_description: Bir DataTable'ı Aspose.Cells çalışma sayfasına aktarırken hücre stillerini
  uygulayın. Tam kod ve ipuçlarıyla adım adım kılavuz.
og_title: Aspose.Cells ile Hücre Stillerini Uygulayın – DataTable'ı İçe Aktarın
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Aspose.Cells ile Hücre Stillerini Uygula – Biçimlendirmeli DataTable'ı İçe
  Aktar
url: /tr/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Hücre Stilleri Uygulama – Veri Tablosunu Biçimlendirme ile İçe Aktarma

Bir `DataTable`’ı bir Excel sayfasına çekerken **hücre stillerini nasıl uygularsınız** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok raporlama senaryosunda verilerin kutudan çıktığı anda güzel görünmesi gerekir—daha sonra manuel biçimlendirme yapmaya gerek kalmasın. İyi haber şu ki Aspose.Cells, **biçimlendirme ile içe aktarmayı** sorunsuz hâle getiriyor; böylece satırlarınız kırmızı, mavi, kalın ya da istediğiniz gibi olabilir.

Bu öğreticide, **veri tablosunu** bir çalışma sayfasına **hücre stilleriyle birlikte** nasıl içe aktaracağınızı gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, bir çalışma kitabı oluşturan, ilk iki sütunu stillendiren ve dosyayı kaydeden, `aspose cells import` API’si kullanılarak hazırlanmış bir C# konsol uygulamanız olacak.

## Öğrenecekleriniz

- .NET projesinde Aspose.Cells kurulumunu
- Gerçek dünya verisini taklit eden örnek bir `DataTable` oluşturmayı
- Kırmızı ve mavi yazı tipleri için `Style` nesneleri tanımlamayı
- `Worksheet.Cells.ImportDataTable` metodunu **veri tablosunu çalışma sayfasına içe aktarırken** stilleri uygulayacak şekilde kullanmayı
- Sonucu doğrulamayı ve çalışma kitabını kaydetmeyi

Harici bir araç gerektirmiyor, sadece saf C# ve Aspose.Cells. Hadi başlayalım.

---

## Ön Koşullar

Kodlamaya başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6.0 veya üzeri | Aspose.Cells 23.x, .NET Standard 2.0+ hedefler; .NET 6 en yeni çalışma zamanı özelliklerini sunar. |
| Aspose.Cells for .NET (NuGet) | `Workbook`, `Worksheet`, `Style` ve `ImportDataTable` metodlarını sağlayan kütüphane. |
| Temel C# bilgisi | Sınıfları, dizileri ve `using` ifadelerini anlayacaksınız. |
| Bir IDE (Visual Studio, VS Code, Rider) | Herhangi bir editör iş görür, ancak NuGet paketlerini geri yüklemeniz gerekir. |

Paketi komut satırından şu şekilde kurabilirsiniz:

```bash
dotnet add package Aspose.Cells
```

---

## Adım 1: Yeni Bir Çalışma Kitabı Oluşturun ve İlk Çalışma Sayfasına Erişin

İlk iş olarak bir `Workbook` nesnesi oluşturup ilk sayfayı alalım. Çalışma kitabını boş bir defter, ilk çalışma sayfasını ise üzerine yazacağımız sayfa olarak düşünün.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **İpucu:** Birden fazla sayfaya ihtiyacınız olursa, `wb.Worksheets.Add()` ile ekleyebilir ve onları isim ya da indeks ile referans alabilirsiniz.

---

## Adım 2: Örnek Bir DataTable Hazırlayın (DataTable Nasıl İçe Aktarılır?)

Şimdi içe aktaracak bir şeyimiz olmalı. Gerçek projelerde bir veritabanı çağırırsınız, ancak açıklık olması için bir `DataTable`’ı bellek içinde oluşturacağız.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Neden Önemli:** Bir `DataTable` sayesinde **aspose cells import** akışını dış bağımlılık olmadan test edebiliriz.

---

## Adım 3: İçe Aktarılan Hücrelere Uygulanacak Stilleri Tanımlayın

İşte sihir burada gerçekleşiyor. İki `Style` nesnesi oluşturacağız: biri kırmızı yazı tipi, diğeri mavi yazı tipi içerecek. Bu stiller, içe aktarım sırasında sütun bazında uygulanacak.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Dikkat:** `importStyles` dizisinin uzunluğu, içe aktaracağınız sütun sayısıyla aynı olmalıdır; aksi takdirde Aspose bir `ArgumentException` fırlatır.

---

## Adım 4: DataTable’ı **Biçimlendirme ile** Çalışma Sayfasına İçe Aktarın

Şimdi her şeyi bir araya getiriyoruz. Kullandığımız `ImportDataTable` aşırı yüklemesi, `Style[]` dizisini kabul eder; böylece veri sayfaya düşerken **hücre stilleri** uygulanır.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Nasıl Çalışır

1. **Başlıklar** – `true` gönderdiğimiz için Aspose “Name” ve “Score” değerlerini ilk satıra yazar.  
2. **Veri Satırları** – Sonraki her satır, `importStyles` dizisindeki karşılık gelen stil ile biçimlendirilir.  
3. **Performans** – Metod, veriyi doğrudan çalışma sayfasına akıtarak hücre‑hücre döngüden daha hızlı bir işlem sağlar.

---

## Adım 5: Sonucu Doğrulayın ve Çalışma Kitabını Kaydedin

İlk birkaç hücreyi inceleyerek stillerin uygulandığını kontrol edelim, ardından dosyayı diske yazalım.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**StyledImport.xlsx** dosyasını açtığınızda şunları göreceksiniz:

- “Name” sütunu **kırmızı** metin olarak.
- “Score” sütunu **mavi** metin olarak.
- Sütun başlıkları varsayılan stil ile (başlıkları da stilize edebilirsiniz, ama bu başka bir öğreticinin konusu).

![Apply cell styles example](https://example.com/images/apply-cell-styles.png "Aspose.Cells'ta Hücre Stilleri Uygulama")

> **Not:** Yukarıdaki görsel, son görünümü göstermektedir. `alt` özniteliği anahtar kelimeyi içerir, SEO gereksinimlerini karşılar.

---

## Sık Sorulan Sorular & Kenar Durumlar

### DataTable’ım Stillerden Daha Fazla Sütun İçeriyorsa Ne Olur?

Aspose, dizideki son stili ekstra sütunlara uygular. Beklenmedik renkler oluşmasını önlemek için dizi uzunluğunu sütun sayısıyla eşleştirin ya da stil istemediğiniz sütunlar için `null` gönderin.

### Belirli Satırlara Farklı Stiller Uygulayabilir miyim?

Kesinlikle. İçe aktarmadan sonra, koşullara göre yeni `Style` nesneleri atayarak satırları döngüyle gezebilir ve stil verebilirsiniz (ör. 90’dan büyük puanları yeşil yap). İşte kısa bir örnek:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### Büyük Veri Setleriyle Çalışır mı?

Evet. `ImportDataTable` veriyi verimli bir şekilde akıtır ve statik stil dizisi ek bir yük getirmez. Milyonlarca satır için, veriyi parçalar halinde `ImportDataTable` ile içe aktarmayı ya da `Cells.ImportDataTable` metodunu bir `DataReader` ile kullanmayı düşünebilirsiniz.

### Çalışma Sayfasındaki Mevcut Biçimlendirmeyi Nasıl Korurum?

Hedef aralıkta zaten istediğiniz bir biçimlendirme varsa, `ImportDataTable` aşırı yüklemesinin `importOptions` parametresini (`ImportTableOptions`) ayarlayın ve `ImportDataTableOptions.PreserveCellFormatting` özelliğini değiştirin. Varsayılan davranış, sağladığınız stillerle üzerine yazar.

---

## Özet: Neler Başardık

- **aspose cells import** işlemi sırasında **hücre stilleri** uyguladık.  
- `Style[]` dizisi geçirerek **biçimlendirme ile içe aktarma** gösterdik.  
- **DataTable**’ı bir çalışma sayfasına içe aktarıp sonucu kaydettik.  
- Stil sayısı uyuşmazlıkları ve koşullu satır stilizasyonu gibi kenar durumları ele alındı.

Tüm bunlar tek bir, bağımsız konsol uygulaması içinde gerçekleştirildi—harici betikler, manuel Excel düzenlemeleri yok. Artık raporlama ya da veri dışa aktarma özellikleriniz için şık Excel çıktıları üretmeye hazırsınız.

---

## Sonraki Adımlar

Hazır mısınız? İşte öğrendiklerinizi genişletecek birkaç öneri:

- **Başlık satırını stilize edin** (ör. kalın, arka plan rengi).  
- `Worksheet.Cells[i, j].ConditionalFormattingCollection` kullanarak **koşullu biçimlendirme** ekleyin.  
- `wb.Save("file.pdf", SaveFormat.Pdf)` ile **CSV veya PDF** gibi diğer formatlara dışa aktarın.  
- Aynı stil yaklaşımını kullanarak birden fazla `DataTable`’ı tek bir çalışma kitabına, her biri ayrı bir sayfada, ekleyin.

Herhangi bir sorunla karşılaşırsanız yorum bırakın ya da `ImportDataTable` hakkında Aspose’un resmi dokümantasyonuna göz atın. İyi kodlamalar ve güzel stilize Excel dosyalarının tadını çıkarın!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere yakın konuları kapsar ve kendi projelerinizde alternatif uygulama yaklaşımları keşfetmenize yardımcı olur. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step‑By‑Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [How to Apply Text Shadow in Excel Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}