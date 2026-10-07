---
category: general
date: 2026-05-30
description: C# Excel otomasyonunda AutoFilter nasıl kullanılır. Excel çalışma kitabı
  oluşturmayı, satırları değerle filtrelemeyi ve elektronik tablo görevlerinizi kolaylaştırmayı
  öğrenin.
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: tr
og_description: C# Excel otomasyonunda AutoFilter nasıl kullanılır. Excel çalışma
  kitabı oluşturmayı, değere göre satırları filtrelemeyi ve elektronik tabloları kolayca
  otomatikleştirmeyi öğrenin.
og_title: C# Excel Otomasyonunda AutoFilter Nasıl Kullanılır – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: C# Excel Otomasyonunda AutoFilter Nasıl Kullanılır – Tam Adım Adım Kılavuz
url: /tr/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# Excel Otomasyonunda AutoFilter Nasıl Kullanılır – Tam Kılavuz

C# kodundan Excel dosyaları oluştururken **AutoFilter nasıl kullanılır** diye hiç merak ettiniz mi? Yalnız değilsiniz—birçok geliştirici, belirli bir kritere uymayan satırları gizlemeleri gerektiğinde bu soruna takılıyor.

Bu öğreticide, **bir Excel çalışma kitabı oluşturur**, bir tablo ekler ve ardından sütun B'deki **değere göre satırları filtreler** somut, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, Excel otomasyonu gerektiren herhangi bir C# projesine ekleyebileceğiniz temiz, yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- Aspose.Cells (veya Microsoft.Office.Interop) kütüphanesiyle bir C# projesi kurun.  
- Programlı olarak **Excel çalışma kitabı oluşturun** ve stil verilen bir tablo ekleyin.  
- **AutoFilter**'ı uygulayarak yalnızca **B sütunu** belirli bir dizeye eşit olan satırları gösterin.  
- Filtreyi tamamen kaldırarak tam veri kümesini geri yükleyin.  
- Eksik sütunlar veya birden fazla filtre kriteri gibi uç durumları ele almak için ipuçları.

Önceden Excel‑VBA deneyimi gerekmez; sadece C# ve NuGet paketleri hakkında temel bir anlayış yeterlidir.

---

## Önkoşullar

| Gereksinim | Neden Önemlidir |
|-------------|----------------|
| .NET 6.0 or later (or .NET Framework 4.7+) | Modern çalışma zamanları size daha iyi performans ve daha kolay paket yönetimi sağlar. |
| Aspose.Cells for .NET (or Microsoft.Office.Interop.Excel) installed via NuGet | Bu kütüphane, kodda kullanılan `Workbook`, `Worksheet` ve `Table` nesnelerini sağlar. |
| A code editor (Visual Studio, VS Code, Rider, etc.) | Örneği derleyip çalıştırmanız gerekecek. |
| Basic C# knowledge | Öğretici, her satırın *neden* var olduğunu, sadece *ne* yaptığını açıklamaz. |

Aspose.Cells'i şu şekilde kurabilirsiniz:

```bash
dotnet add package Aspose.Cells
```

---

## Aspose.Cells ile C#'ta AutoFilter Nasıl Kullanılır

Aşağıda tam, bağımsız program yer alıyor. Bir konsol projesinde `Program.cs` olarak kaydedin ve çalıştırın – çıktı klasöründe `FilteredWorkbook.xlsx` dosyasını elde edeceksiniz.

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### Kodun Çalışma Şekli

1. **Çalışma kitabını oluşturma** – `new Workbook()` size temiz bir dosya verir; `Worksheets[0]` varsayılan sayfayı alır.  
2. **Örnek veri doldurma** – Filtreyi çalışırken görebilmeniz için küçük bir veri kümesi yazarız.  
3. **Tablo ekleme** – `ListObjects.Add` aralığı bir Excel tablosuna dönüştürür; bu tablo otomatik olarak filtreleme ve stil desteği sağlar.  
4. **AutoFilter uygulama** – `table.AutoFilter.Filter(1, "Apple")` motoru şu şekilde yönlendirir: “Sadece ikinci sütun (B) *Apple* eşit olan satırları göster.”  
5. **Dosyaları kaydetme** – İki dosya yazılır: biri filtreli, diğeri filtre kaldırılmış, `RemoveAutoFilter()`'ın beklendiği gibi çalıştığını gösterir.

> **Pro ipucu:** Birden fazla kriterle filtrelemeniz gerekiyorsa (ör. “Apple” *veya* “Banana”), `Filter(int columnIndex, string criteria1, string criteria2)` aşırı yüklemesini kullanın veya bir dizi dize geçirin.

---

## Değere Göre Satırları Filtreleme – Yaygın Varyasyonlar

Yukarıdaki örnek **B sütununu filtrelemeye** odaklansa da, diğer sütunları filtrelemek veya sayısal kriterler kullanmak isteyebilirsiniz. İşte hızlı bir özet:

| İstenen filtre | Kod parçacığı |
|----------------|--------------|
| C sütununda metin eşleşmesi | `table.AutoFilter.Filter(2, "Cherry");` |
| C sütununda 10'dan büyük sayılar | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| B sütununda birden fazla değer | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Kenar durumu:** Sütun başlığı yanlış yazılmışsa veya sütun indeksi aralık dışındaysa, Aspose.Cells bir `ArgumentException` fırlatır. Filtreyi uygulamadan önce `table.ListColumns.Count` kontrol ederek buna karşı önlem alın.

---

## AutoFilter'ı Kaldırma – Ne Zaman Sıfırlanmalı

Bazen tam veri kümesini tekrar sunmanız gerekir (ör. bir kullanıcı arama kutusunu temizlediğinde). `table.RemoveAutoFilter()` çağrısı tek satırda işi çözer. Microsoft.Office.Interop kullanıyorsanız, `worksheet.AutoFilterMode = false;` çağırmanız gerekir.

---

## Tam Çalışan Örnek Özeti

Aşağıda, yorumlar çıkarılmış *tam* program tekrar yer alıyor; daha öz bir görünüm tercih edenler için:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

Bu programı çalıştırdığınızda iki dosya oluşur:

- **FilteredWorkbook.xlsx** – yalnızca *Apple* içeren satırlar görünür.  
- **UnfilteredWorkbook.xlsx** – orijinal veri geri yüklenir.

---

## Sıkça Sorulan Sorular

**S: Bu eski .xls dosyalarıyla çalışır mı?**  
C: Evet. Aspose.Cells, dosya uzantısını değiştirerek veya `SaveOptions` kullanarak hem `.xlsx` hem de `.xls` olarak kaydedebilir.

**S: Çalışma kitabı zaten kaydedildikten sonra filtre uygulamam gerekirse ne yapmalıyım?**  
C: Dosyayı `new Workbook("path.xlsx")` ile yükleyin, filtreyi uygulayın ve ardından tekrar `Save` edin.

**S: Tablo olmayan bir *aralığa* filtre uygulayabilir miyim?**  
C: Kesinlikle. `worksheet.AutoFilter.Range = "A1:C5";` kullanın ve ardından `worksheet.AutoFilter.ApplyFilter();` çağırın. Ancak, tablolar yerleşik stil ve daha kolay sütun referansı sağlar.

---

## Görsel – Görsel Doğrulama

![C# ile oluşturulan bir Excel çalışma kitabında B sütununa uygulanan AutoFilter'ı gösteren ekran görüntüsü](/images/autofilter-column-b.png "B sütununda AutoFilter")

*(Görsel, yalnızca “Apple” içeren satırların kaldığı filtreli görünümü göstermektedir.)*

---

## Sonuç

C# tabanlı bir Excel otomasyon senaryosunda **AutoFilter nasıl kullanılır** konusunu, **Excel çalışma kitabı oluşturma**, **B sütununda değere göre satırları filtreleme** ve sonunda **gerekmediğinde filtreyi kaldırma** adımlarıyla ele aldık. Temel adımlar—başlatma, tablo ekleme, filtre uygulama ve temizleme—**excel automation c#** ihtiyacı olan herhangi bir projede yeniden kullanılabilir.

Bir sonraki meydan okumaya hazır mısınız? Şunları deneyin:

- Filtrelenmiş satırları vurgulamak için koşullu biçimlendirme ekleme.  
- Filtrelenmiş veriyi sonraki işleme için bir CSV'ye dışa aktarma.  
- Birden fazla filtreyi birleştirme (ör. “Apple” *ve* miktar > 8).

Deneyin, hatalar yapın ve ardından düzeltin—

---

## Sonra Ne Öğrenmelisiniz?

- [Aspose.Cells for .NET kullanarak Excel'de AutoFilter Nasıl Uygulanır (Veri Analizi Kılavuzu)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [Aspose.Cells .NET ile Excel Veri Analizinde Autofilter Not Contains Nasıl Kullanılır](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [Aspose.Cells for .NET kullanarak Excel Autofilter 'EndsWith' Nasıl Uygulanır](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}