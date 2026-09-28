---
category: general
date: 2026-09-27
description: C# ile Excel tablosundan satırları nasıl sileceğinizi, ayrıca Excel çalışma
  kitabını C#'ta hızlıca nasıl yükleyeceğinizi gösteren adım adım bir rehberle öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: tr
lastmod: 2026-09-27
og_description: C# ile Excel tablosundan satırları silme, net bir örnekle. Bu öğreticide
  ayrıca C# ile Excel çalışma kitabını nasıl yükleyeceğiniz ve yaygın kenar durumlarını
  nasıl ele alacağınız da ele alınmaktadır.
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: C#'ta Excel tablosundan satırları sil – tam kod rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: C# kullanarak Excel tablosundan satırları nasıl sileriz
url: /tr/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel tablosundan satırları silme C# – tam programlama rehberi

Bir .xlsx dosyasında **Excel tablosundan satırları silmeniz** gerekiyorsa, bu öğretici C# ile bunu tam olarak nasıl yapacağınızı gösterir. Excel çalışma kitabını yükleyen, ilk tablodan belirli satırları kaldıran ve sonucu kaydeden kısa, çalıştırılabilir bir örnek göreceksiniz. Yaklaşım, popüler Aspose.Cells kütüphanesiyle çalışır ve diğer .NET Excel API'lerine uyarlanabilir.

Bir tablodan satırları kaldırmak, içe aktarılan verileri temizlerken, rapor bölümlerini kısaltırken veya elektronik tablo güncellemelerini otomatikleştirirken yaygın bir görevdir. Bu rehberin sonunda **Excel çalışma kitabını C# ile yükleyebilir**, bir tabloyu (ListObject) bulabilir, istediğiniz satırları silebilir ve değiştirilmiş dosyayı diske yazabilirsiniz.

## Önkoşullar

* .NET 6.0 veya daha yeni bir sürüm yüklü olmalı (kod .NET Framework 4.7+ ile de çalışır).
* **Aspose.Cells** NuGet paketine referans (veya `Workbook`, `Worksheet` ve `ListObject` tiplerini sunan uyumlu bir kütüphane).
* `input.xlsx` adlı bir giriş dosyası, projenizden referans verebileceğiniz bir klasöre yerleştirilmiş olmalı.
* C# sözdizimi ve Visual Studio (veya tercih ettiğiniz IDE) hakkında temel bilgi.

> **Pro ipucu:** Açık kaynak bir alternatif tercih ediyorsanız, aynı mantık **ClosedXML** ile uygulanabilir – sadece Aspose‑özel sınıflarını `XLWorkbook`, `IXLWorksheet` ve `IXLTable` ile değiştirin.

## Adım 1: Excel çalışma kitabını C# ile yükleme

İlk işlem, kaynak dosyayı belleğe okumaktır. Çalışma kitabını yüklemek tipik elektronik tablo boyutları için maliyetli değildir ve size çalışma sayfalarına, tablolara ve hücre değerlerine tam erişim sağlar.

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Neden önemli:* `Workbook`, .xlsx dosyasının Open XML yapısını ayrıştırır ve bir `Worksheet` nesnesi koleksiyonu sunar. Dosya bulunamazsa, Aspose bir `FileNotFoundException` fırlatır, bu yüzden yolun doğru olduğundan emin olun.

## Adım 2: Hedef çalışma sayfasına erişme

Çoğu elektronik tablo birden fazla sayfa içerir; değiştirmek istediğiniz tabloyu barındıran sayfayı seçmeniz gerekir. Burada, basit dosyalar için güvenli bir varsayılan olan ilk sayfayı (`Worksheets[0]`) kullanıyoruz.

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Neden önemli:* `Worksheet`, tablolar (`ListObjects`) için kapsayıcıdır. Doğru sayfaya erişmek, alakasız verilere yanlışlıkla değişiklik yapılmasını önler.

## Adım 3: Excel tablosundan satırları silme

Excel tabloları `ListObject` nesneleriyle temsil edilir. Sayfadaki ilk tablo `ListObjects[0]`'dır. `DeleteRows(startIndex, rowCount)` yöntemi, satırları **tablonun veri alanına göre** kaldırır, çalışma sayfasının mutlak satır numaralarına göre değil.  

Bu örnekte, tablonun ikinci ve üçüncü satırlarını siliyoruz (başlık satırı 0, bu yüzden indeks 1'den başlıyoruz).

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### Tablo farklı bir isim veya konuma sahipse ne olur?

* **Adlandırılmış tablo:** İndeks yerine `ws.ListObjects["MyTableName"]` kullanın.
* **Birden çok tablo:** `ws.ListObjects` üzerinde döngü yapın ve bir koşula (ör. sütun başlığı adları) uyanı seçin.
* **Dinamik satır sayısı:** `ws.ListObjects[0].DataRange.RowCount` inceleyerek çalışma zamanında `rowCount` değerini hesaplayabilirsiniz.

### Kenar‑durumları yönetimi

| Durum                                   | Önerilen kod değişikliği                                      |
|----------------------------------------|--------------------------------------------------------------|
| Tablo boş veya daha az satıra sahipse   | Silmeden önce `ws.ListObjects[0].DataRange.RowCount` kontrol edin. |
| Silinecek satır sayısı tablo boyutunu aşıyorsa | `rowCount` değerini `DataRange.RowCount - startIndex` ile sınırlayın. |
| Koşula dayalı satır silme ihtiyacı (ör. C sütunundaki değer) | `DataRange.Rows` üzerinde döngü yapın, eşleşen indeksleri toplayın ve indekslerin stabil kalması için ters sırada silin. |

## Adım 4: Değiştirilen çalışma kitabını kaydetme

Silme işleminden sonra, çalışma kitabını yeni bir dosyaya (veya isterseniz orijinali üzerine) yazın. Kaydetmek, güncellenmiş tabloyu yansıtan yeni bir .xlsx oluşturur.

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Neden önemli:* `Save`, bellek içindeki temsili diske serileştirir. Orijinal dosyayı korumanız gerekiyorsa, her zaman farklı bir yola yazın.

## Tam, çalıştırılabilir örnek

Tüm adımları bir araya getirerek, kopyalayıp yapıştırıp çalıştırabileceğiniz bağımsız bir program elde edersiniz.

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**Beklenen çıktı** (konsol):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

`output.xlsx` dosyasını açın – ilk tablo artık kaldırdığınız satırları içermiyor, başlık satırı ise aynı kalıyor.

## Yaygın sorular ve varyasyonlar

### Bir çalışma kitabındaki **tüm** tablolardan satırları nasıl silerim?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### **Hücre değeri**ne göre satırları silebilir miyim?

Evet. `DataRange` içinde eşleşen hücreleri tarayın, sıfır‑tabanlı indekslerini toplayın ve ardından azalan sırada silin:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### **Biçimlendirmeyi korumam** gerekirse ne olur?

`DeleteRows`, tablodan tüm satırı kaldırır ancak kalan satırlar için tablonun stilini korur. Silmekte olduğunuz bir satırda belirli bir biçimlendirmeyi tutmanız gerekiyorsa, silmeden önce stili başka bir satıra kopyalayın.

### Bu **.xls** (Excel 97‑2003) dosyalarıyla çalışır mı?

Evet. Aspose.Cells dosya formatını otomatik olarak algılar, bu yüzden aynı kod `.xls` ile de çalışır. `Workbook` yapıcısındaki dosya uzantısını değiştirmeniz yeterlidir.

## Performans ipuçları

* **Toplu silme:** Birçok satırı tek tek silmek daha yavaş olabilir. Mümkün olduğunda tek bir `DeleteRows(start, count)` çağrısı kullanın.
* **UI iş parçacığını engellemekten kaçının:** Bunu bir masaüstü uygulamasına entegre ediyorsanız, UI'nin yanıt vermesini sağlamak için çalışma kitabı işlemini arka plan iş parçacığında çalıştırın.
* **Doğru şekilde dispose edin:** Aspose.Cells yönetilen bellek kullansa da, büyük dosyalarla çalışıyorsanız `Workbook`'u bir `using` bloğu içinde sararak kaynakları hızlıca serbest bırakın.

## Sonuç

Artık C# kullanarak **Excel tablosundan satırları silen** eksiksiz, üretim‑hazır bir örneğe sahipsiniz. Rehber, **Excel çalışma kitabını C# ile yükleme**, istenen `ListObject`'i bulma, satırları güvenli bir şekilde kaldırma ve güncellenmiş dosyayı kaydetme konularını kapsadı. Kenar‑durum yönetimi ve performans önerileri sayesinde bu deseni koşullu silme, birden çok tablo veya alternatif .NET Excel kütüphaneleri gibi daha karmaşık senaryolara uyarlayabilirsiniz.

### Sonraki adımlar

* **ClosedXML** veya **EPPlus**'ı keşfedin, tamamen açık kaynak bir yığını tercih ediyorsanız.
* Satır silmeyi **veri doğrulama** ile birleştirerek elektronik tabloları veritabanına aktarmadan önce temizleyin.
* `Directory.GetFiles` ve bir döngü kullanarak bir klasördeki çalışma kitapları için süreci otomatikleştirin.

Farklı satır aralıkları, tablo adları ve koşullu mantıklarla denemeler yapmaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Excel Dosyasını Yükle C# – Satırları Silme ve Belirli Satırları Kaldırma](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [Aspose.Cells for .NET ile Excel'e Satır Ekleme ve Silme: Kapsamlı Rehber](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Aspose.Cells .NET ile Excel'de Boş Satırları Silme – Veri Temizliği](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}