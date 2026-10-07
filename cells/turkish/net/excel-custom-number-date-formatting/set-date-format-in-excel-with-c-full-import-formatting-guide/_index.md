---
category: general
date: 2026-06-17
description: C# kullanarak Excel’de tarih formatını ayarlayın, ayrıca hücre arka planını
  belirleyin, ön plan rengini uygulayın ve içe aktarma sırasında Excel sütununu renklendirin.
  Adım adım öğrenin.
draft: false
keywords:
- set date format
- set cell background
- apply foreground color
- color excel column
- excel import formatting
language: tr
og_description: C# ile hücre arka planını ayarlarken, ön plan rengini uygularken ve
  içe aktarma sırasında Excel sütununu renklendirirken Excel’de tarih formatını ayarlayın.
  Tam öğretici.
og_title: C# ile Excel’de tarih formatını ayarlama – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-17'
  description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  headline: Set date format in Excel with C# – Full Import Formatting Guide
  type: TechArticle
- description: Set date format in Excel using C# and also set cell background, apply
    foreground color, and color Excel column during import. Learn step‑by‑step.
  name: Set date format in Excel with C# – Full Import Formatting Guide
  steps:
  - name: 2.1 Set Date Format for the First Column
    text: The first column (`OrderDate`) should display as “MM/dd/yyyy”. Aspose uses
      the built‑in number format index 14 for the short date, but you can also supply
      a custom format string if you prefer.
  - name: 2.2 Set Cell Background for the Second Column
    text: Let’s give the `CustomerName` column a light blue background. This is where
      **set cell background** comes into play.
  - name: 2.3 Apply Foreground (Text) Color – Optional Extra
    text: 'If you also want the text itself to be a contrasting color, you can tweak
      the same style:'
  - name: 3.1 Save the Workbook
    text: '```csharp // Save to a file – change path as needed wb.Save("FormattedReport.xlsx",
      SaveFormat.Xlsx); Console.WriteLine("Excel file created with date format and
      colors."); ```'
  - name: What if I have more than two columns?
    text: Just expand the `columnStyles` array and assign a `Style` to each index
      you care about. Unassigned indexes will fall back to the default style, which
      is perfectly fine.
  - name: How do I format a column as currency?
    text: '```csharp columnStyles[3] = wb.CreateStyle(); columnStyles[3].Number =
      164; // Built‑in currency format (e.g., $#,##0.00) ```'
  - name: Can I change the header row style separately?
    text: 'Yes. After the import, you can grab the first row and apply a distinct
      style:'
  - name: What if the DataTable contains null dates?
    text: 'Aspose will leave those cells blank. If you prefer a placeholder like “N/A”,
      you can preprocess the table:'
  type: HowTo
tags:
- excel
- csharp
- aspnet
- data-import
title: C# ile Excel’de tarih formatını ayarlayın – Tam İçe Aktarma Biçimlendirme Rehberi
url: /tr/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Excel'de Tarih Biçimini Ayarlama – Tam İçe Aktarma Biçimlendirme Kılavuzu

C# kodu ile oluşturulan bir Excel sayfasında **tarih biçimini ayarlamayı** ve aynı zamanda sütunun özel bir arka plan veya metin rengine sahip olmasını hiç istediniz mi? Tek başınıza değilsiniz. Birçok raporlama senaryosunda bir veritabanından bir `DataTable` alır, bir çalışma sayfasına yerleştirir ve ardından tarihleri doğru göstermek ve sütunları doğru renklerle öne çıkarmak için çabalamış olursunuz.  

Bu öğreticide, veri içe aktarırken **tarih biçimini ayarlar**, **hücre arka planını ayarlar**, **ön plan rengini uygular** ve hatta **Excel sütununu renklendirir** gibi temiz, uçtan uca bir çözümü adım adım inceleyeceğiz. Sonunda, **excel import formatting** için tipik deneme‑yanılma sürecine gerek kalmadan yeniden kullanılabilir bir desen elde edeceksiniz.

> **İhtiyacınız olanlar**  
> * .NET 6+ (or .NET Framework 4.7+)  
> * Aspose.Cells for .NET (free trial works for testing)  
> * A `DataTable` source – any ADO.NET query will do  
> * Visual Studio or your favorite IDE  

Haydi başlayalım.

---

## Çözümün Genel Bakışı

We’ll break the problem into three logical chunks:

1. **Kaynak veriyi al** – dışa aktarmak istediğiniz satırları içeren bir `DataTable`.
2. **Sütun‑özel stiller oluştur** – tarih sütunu için bir stil, metin sütunu için bir başka stil ve istediğiniz ekstra stil.
3. **Stillerle tabloyu içe aktar** – her sütunun hazırladığınız stili devralması için `Worksheet.Cells.ImportDataTable` kullanın.

Bu yaklaşım neden? Aspose.Cells, `ImportDataTable` çağrısına doğrudan bir `Style` dizisi eklemenize izin verir, bu da biçimlendirmeyi yeniden uygulamak için ikinci bir geçişe ihtiyaç duymadığınız anlamına gelir. Daha hızlı, daha az hataya açık ve kodunuzu düzenli tutar.

---

## Adım 1: Dışa Aktarılacak Veriyi Al

İlk iş olarak bir `DataTable`'a ihtiyacınız var. Gerçek bir projede muhtemelen bir saklı prosedür çağırır veya Entity Framework kullanarak doldurursunuz, ancak örnekleme amacıyla bir tarih ve bir metin sütunu içeren basit bir tabloyu taklit edeceğiz.

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable GetData()
{
    var table = new DataTable();
    table.Columns.Add("OrderDate", typeof(DateTime));
    table.Columns.Add("CustomerName", typeof(string));

    // Sample rows – replace with your DB call
    table.Rows.Add(DateTime.Today.AddDays(-2), "Acme Corp");
    table.Rows.Add(DateTime.Today.AddDays(-1), "Globex Inc");
    table.Rows.Add(DateTime.Today, "Soylent Co");

    return table;
}
```

> **Pro ipucu:** Kaynağınız nullable (boş) tarihleri kullanıyorsa, sütun tipinin `typeof(DateTime?)` olduğundan emin olun – Aspose, daha sonra atadığınız biçimi yine de saygı gösterecektir.

---

## Adım 2: Stil Dizisi Hazırla – Her Sütun İçin Bir Stil

Şimdi, `DataTable`'daki sütun sayısıyla aynı uzunlukta bir `Style[]` oluşturuyoruz. Her giriş, ilgili sütun için biçimlendirmeyi tutacak.

```csharp
// Create a new workbook and get the first worksheet
Workbook wb = new Workbook();
Worksheet ws = wb.Worksheets[0];

// Pull the data
DataTable dataTable = GetData();

// Allocate the style array
Style[] columnStyles = new Style[dataTable.Columns.Count];
```

### 2.1 İlk Sütun İçin Tarih Biçimini Ayarla

İlk sütun (`OrderDate`) “MM/dd/yyyy” biçiminde gösterilmelidir. Aspose, kısa tarih için yerleşik sayı formatı indeksi 14'ü kullanır, ancak isterseniz özel bir format dizesi de sağlayabilirsiniz.

```csharp
// Style for the date column (index 0)
columnStyles[0] = wb.CreateStyle();
columnStyles[0].Number = 14;               // Built‑in short date format
// Or a custom pattern:
// columnStyles[0].Custom = "mm/dd/yyyy";
```

**Neden önemli?** Excel tarihleri seri numaralar olarak depolar. Bir sayı formatı atayarak, Excel'e bu serileri ham sayılar yerine insan tarafından okunabilir tarihler olarak göstermesini söylersiniz.

### 2.2 İkinci Sütun İçin Hücre Arka Planını Ayarla

`CustomerName` sütununa açık mavi bir arka plan verelim. İşte **set cell background** (hücre arka planını ayarla) burada devreye giriyor.

```csharp
// Style for the text column (index 1)
columnStyles[1] = wb.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightBlue;
columnStyles[1].Pattern = BackgroundType.Solid; // Needed to show the color
```

> **Not:** `Pattern`'i `Solid` olarak ayarlamazsanız, ön plan rengi görünmez çünkü varsayılan desen “None” (yok) durumundadır.

### 2.3 Ön Plan (Metin) Rengini Uygula – İsteğe Bağlı Ek

Metnin kendisinin de zıt bir renkte olmasını isterseniz, aynı stili ayarlayabilirsiniz:

```csharp
columnStyles[1].Font.Color = System.Drawing.Color.DarkBlue; // apply foreground color
```

Bu, **apply foreground color** (ön plan rengini uygula) gereksinimini karşılar ve sütunun arka planını aynı tutar.

---

## Adım 3: Tanımlı Stillerle DataTable'ı İçe Aktar

Stiller hazır olduğunda, son adım veriyi içe aktaran ve stilleri sütun‑sütun uygulayan tek bir satırdır.

```csharp
// Import the DataTable starting at cell A1 (row 0, column 0)
// includeColumnNames = true to add a header row
ws.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);
```

**Nasıl çalışır:** Aspose, `columnStyles` dizisini okur ve her `Style`'ı ilgili sütun indeksine eşler. Başlık satırı, satır 0 için ayrı bir stil sağlamadığınız sürece varsayılan stili devralır.

### 3.1 Çalışma Kitabını Kaydet

```csharp
// Save to a file – change path as needed
wb.Save("FormattedReport.xlsx", SaveFormat.Xlsx);
Console.WriteLine("Excel file created with date format and colors.");
```

Programı çalıştırın, *FormattedReport.xlsx* dosyasını açın ve şunları görmelisiniz:

- **OrderDate** sütunu tarih olarak gösterilir (ör. `06/15/2026`).  
- **CustomerName** sütunu açık mavi dolgu ve koyu mavi metin ile.  

Bu, 30 satırdan az C# koduyla **excel import formatting** (excel içe aktarma biçimlendirmesi) iş akışının tamamıdır.

---

## Adım‑Adım Özet (Nedenleriyle)

| Adım | Yapılan İşlem | Neden Önemli |
|------|---------------|--------------|
| **Veriyi Al** | `GetData()`'ı çağırarak bir `DataTable` doldurur. | Aspose'un doğrudan alabileceği yapılandırılmış bir kaynak sağlar. |
| **Stil Dizisi Oluştur** | Sütun sayısıyla eşleşen bir `Style[]` tahsis eder. | Tek bir içe aktarma çağrısında sütun‑başına stil uygulamaya izin verir. |
| **Tarih Biçimini Ayarla** | `columnStyles[0].Number = 14;` | Tarihlerin Excel'de doğru görüntülenmesini sağlar. |
| **Arka Plan Rengini Ayarla** | `ForegroundColor = LightBlue; Pattern = Solid;` | Sütunu vurgular, **set cell background** (hücre arka planını ayarla) gereksinimini karşılar. |
| **Ön Plan Rengini Uygula** | `Font.Color = DarkBlue;` | Okunabilirliği artırır ve **apply foreground color** (ön plan rengini uygula) gereksinimini karşılar. |
| **Stillerle İçe Aktar** | `ImportDataTable(..., columnStyles);` | Tüm biçimlendirmeyi dikkate alan tek geçişli içe aktarma. |
| **Çalışma Kitabını Kaydet** | `wb.Save(...);` | Sonucu sonraki kullanıcılar için kalıcı hale getirir. |

---

## Kenar Durumları ve Sık Sorulan Sorular

### Daha Fazla Sütunum Olursa Ne Olur?

Sadece `columnStyles` dizisini genişletin ve ilgilendiğiniz her indeks için bir `Style` atayın. Atanmamış indeksler varsayılan stile geri dönecek, bu da tamamen uygundur.

```csharp
columnStyles[2] = wb.CreateStyle();
columnStyles[2].Number = 0; // General format for numeric columns
```

### Bir Sütunu Para Birimi Olarak Nasıl Biçimlendiririm?

```csharp
columnStyles[3] = wb.CreateStyle();
columnStyles[3].Number = 164; // Built‑in currency format (e.g., $#,##0.00)
```

### Başlık Satırı Stilini Ayrı Ayrı Değiştirebilir miyim?

Evet. İçe aktarmadan sonra, ilk satırı alıp ayrı bir stil uygulayabilirsiniz:

```csharp
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = System.Drawing.Color.Gold;
headerStyle.Pattern = BackgroundType.Solid;

ws.Cells.Rows[0].ApplyStyle(headerStyle, new StyleFlag { All = true });
```

### DataTable Boş (null) Tarihler İçeriyorsa Ne Olur?

Aspose bu hücreleri boş bırakır. “N/A” gibi bir yer tutucu tercih ederseniz, tabloyu ön işlemden geçirebilirsiniz:

```csharp
foreach (DataRow row in dataTable.Rows)
{
    if (row.IsNull("OrderDate"))
        row["OrderDate"] = DateTime.MinValue; // or any sentinel
}
```

Ardından, sentinel değer için “N/A” gösteren özel bir format görüntüleyecek şekilde stili ayarlayın.

---

## Tam Çalışan Örnek

Aşağıda eksiksiz, kopyala‑yapıştır hazır program bulunmaktadır. Bir konsol uygulaması olarak çalıştırın ve güzel biçimlendirilmiş bir Excel dosyası elde edeceksiniz.



## Sonraki Öğrenmeniz Gerekenler?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Aspose.Cells for .NET kullanarak Excel Hücrelerinde Yazı Rengini Ayarlama](/cells/english/net/formatting/setting-font-color/)
- [Aspose.Cells ile .NET Excel'de Yazı Rengini Ayarlama](/cells/english/net/formatting/set-font-color-net-excel-aspose-cells/)
- [Aspose.Cells for .NET kullanarak Piksel Cinsinden Excel Sütun Genişliklerini Ayarlama | Adım Adım Kılavuz](/cells/english/net/formatting/set-excel-column-width-pixels-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}