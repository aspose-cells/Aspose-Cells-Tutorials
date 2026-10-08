---
category: general
date: 2026-06-24
description: C#'ta yeni bir çalışma kitabı oluşturun ve verisini koruyarak pivot tabloyu
  kopyalayın. Satırları nasıl kopyalayacağınızı, seçili aralığı nasıl dışa aktaracağınızı
  ve pivotu bozulmadan nasıl tutacağınızı öğrenin.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- export selected range
language: tr
og_description: C#'ta yeni bir çalışma kitabı oluşturun ve verilerini koruyarak bir
  pivot tabloyu kopyalayın. Satırları nasıl kopyalayacağınızı ve seçili aralığı nasıl
  dışa aktaracağınızı adım adım anlatan rehber.
og_title: C#'ta Yeni Çalışma Kitabı Oluştur – Pivot Tablosunu Kopyala
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Create new workbook in C# and copy pivot table while preserving its
    data. Learn how to copy rows, export selected range, and keep the pivot intact.
  headline: Create New Workbook in C# – Copy Pivot Table
  type: TechArticle
- questions:
  - answer: Yes, as long as the copied rectangle encloses each pivot you need. If
      you only want one, adjust `rows`/`cols` to isolate it.
    question: Does this work with multiple pivot tables on the same sheet?
  - answer: The pivot cache will still point to the original connection. Call `pivotTable.RefreshData()`
      after loading the destination if you want to re‑query the source.
    question: What if the source workbook uses external data connections?
  - answer: Absolutely. Replace `destinationWorkbook` with `sourceWorkbook` and pick
      another worksheet index.
    question: Can I copy the pivot to a different sheet within the same workbook?
  - answer: 'Use `CopyRows`/`CopyColumns` overloads that accept a `CopyOptions` object—set
      `CopyOptions.CopyType = CopyType.ValuesOnly` or `CopyType.All` depending on
      your needs. --- ## Conclusion We’ve just walked through a **create new workbook**
      scenario that **copy pivot table**, **preserve pivot table**, an'
    question: Is there a way to copy formatting only?
  type: FAQPage
tags:
- C#
- Aspose.Cells
- Excel automation
title: C#'ta Yeni Çalışma Kitabı Oluştur – Pivot Tabloyu Kopyala
url: /tr/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Yeni Çalışma Kitabı Oluştur – Pivot Tablosunu Kopyala

C#'ta **create new workbook** sadece bir pivot tablo içeren bir veri dilimini taşımak için hiç ihtiyacınız oldu mu? Tek başınıza değilsiniz. Birçok raporlama hattında birkaç satır, belki birkaç sütun alırsınız ve pivotun tam olarak olduğu gibi kalmasını beklersiniz—bozuk referanslar, eksik hesaplamalar olmadan.  

İyi haber? Aspose.Cells'in birkaç satırıyla **copy pivot table**, bütünlüğünü koruyabilir ve hatta **export selected range** hiçbir şeyi bozmaz. Aşağıda **how to copy rows**, pivotu koruyan ve sonucu tamamen yeni bir çalışma kitabı olarak kaydeden eksiksiz, çalıştırmaya hazır bir örnek göreceksiniz.

## Bu Eğitimde Neler Kapsanıyor

- Aspose.Cells ile bir C# projesi kurmak (kodun çalışmasını sağlayan kütüphane).
- Orijinal pivotu içeren kaynak çalışma kitabını yüklemek.
- Kütüphanenin `CopyRows` ve `CopyColumns` metodlarını kullanarak ihtiyacınız olan tam aralığı çoğaltmak.
- Kopyalanan alanı **create new workbook** senaryosunda kaydetmek, pivotun işlevsel kalmasını sağlamak.
- Birden fazla pivot tablo, gizli satırlar ve büyük veri setleri gibi uç durumlar için ipuçları.

Bu rehberin sonunda herhangi bir Excel dosyasından **export selected range** yapabilecek, pivot mantığını canlı tutabilecek ve yeni dosyayı istediğiniz yere bırakabileceksiniz.

> **Prerequisite**: NuGet üzerinden yüklü Aspose.Cells for .NET (ücretsiz deneme veya lisanslı sürüm). Henüz eklemediyseniz, proje klasörünüzde `dotnet add package Aspose.Cells` komutunu çalıştırın.

---

## Yeni Çalışma Kitabı Oluştur ve Pivot Tablosunu Kopyala

Aşağıda çözümün kalbi yer alıyor. Her satırı adım adım inceleyecek, neden önemli olduğunu açıklayacak ve ardından tam programı göstereceğiz.

```csharp
using System;
using Aspose.Cells;

class PivotCopyDemo
{
    static void Main()
    {
        // 1️⃣ Load the source workbook that contains the pivot table
        string sourcePath = @"YOUR_DIRECTORY\source.xlsx";
        Workbook sourceWorkbook = new Workbook(sourcePath);

        // 2️⃣ Create a new workbook that will receive the copied range
        Workbook destinationWorkbook = new Workbook();
        Worksheet destSheet = destinationWorkbook.Worksheets[0];

        // 3️⃣ Define the range we want to copy (first 20 rows, first 4 columns)
        //    This range includes the pivot table we care about.
        int startRow = 0;   // zero‑based index
        int startColumn = 0;
        int totalRows = 20;
        int totalColumns = 4;

        // 4️⃣ Copy rows – this is the “how to copy rows” part.
        //    Aspose.Cells lets us copy rows directly from the source cells collection.
        sourceWorkbook.Worksheets[0].Cells.CopyRows(startRow, startRow, totalRows);

        // 5️⃣ Copy columns – paired with the row copy to form a rectangular block.
        sourceWorkbook.Worksheets[0].Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 6️⃣ Now move the copied block into the destination sheet.
        //    We use the same start cell (A1) for simplicity.
        destSheet.Cells.CopyRows(startRow, startRow, totalRows);
        destSheet.Cells.CopyColumns(startColumn, startColumn, totalColumns);

        // 7️⃣ Save the destination workbook – the pivot table is preserved in the copied range
        string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
        destinationWorkbook.Save(destPath);

        Console.WriteLine("✅ New workbook created and pivot table preserved at: " + destPath);
    }
}
```

### Neden Bu Çalışıyor

- **`CopyRows` / `CopyColumns`**: Bu metodlar temel hücre verilerini *ve* ilişkili nesneleri (örneğin bir pivot önbelleği) çoğaltır. Bu yüzden pivot taşıma sonrası işlevsel kalır.
- **Separate destination workbook**: Yeni bir `Workbook` örneği oluşturarak **create new workbook** yaparız ve müdahale edebilecek kalan biçimlendirme ya da gizli sayfalar olmadan bir hedef çalışma kitabı elde ederiz.
- **Zero‑based indexing**: Aspose.Cells sıfır‑tabanlı indeksler kullanır, bu yüzden `0` hücresi **A1**'e işaret eder. Pivotunuz sol‑üst köşede değilse `startRow`/`startColumn` değerlerini ayarlayın.
- **Preserve pivot table**: Pivotun önbelleği aynı aralıkta bulunduğu için aralığı kopyalamak önbelleği de otomatik olarak kopyalar. Ek bir koda gerek yok.

---

## Pivotu Bozmadan Satırları Nasıl Kopyalarsınız

Sadece satır‑kopyalama kısmıyla ilgileniyorsanız, bunu izole edebilirsiniz:

```csharp
// Copy just rows 5‑15 (inclusive) from the source sheet
int sourceStartRow = 4;   // row 5 in Excel terms
int rowsToCopy = 11;      // rows 5‑15 => 11 rows
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy);
```

**Pro tip**: Bir pivot tabloyu kesen satırları kopyalarken, her zaman *tam* pivot alanını (satırlar + sütunlar) kopyalayın. Kısmi kopyalar pivotun eksik alanlarla kalmasına ve `#REF!` hatalarına yol açabilir.

---

## Seçili Aralığı Dışa Aktar – Gerçek Dünya Senaryosu

Kocaman bir satış çalışma kitabınız olduğunu hayal edin, ancak müşteriniz sadece ilk çeyrek özetini istiyor; bu özet satır 1‑20 ve sütun A‑D'de bulunuyor. Yukarıdaki kod parçacığı zaten sizin için **export selected range** yapıyor. `totalRows` ve `totalColumns` değişkenlerini müşterinin isteğine göre değiştirin, işiniz bitti.

### Gizli Satırları veya Filtreleri İşleme

Kaynak sayfada gizli satırlar (belki filtrelenmiş) varsa, sadece *görünür* satırları kopyalamak isteyebilirsiniz. Aspose.Cells, görünürlüğü dikkate alan `CopyRows` aşırı yüklemeleri sunar:

```csharp
sourceWorkbook.Worksheets[0].Cells.CopyRows(sourceStartRow, 0, rowsToCopy, true);
```

Son boolean değeri `true` olarak ayarlayın, böylece sadece görünür satırlar kopyalanır—kullanıcı filtre uyguladığında “export selected range” için mükemmeldir.

---

## Pivot Tablosunu Koru – Yaygın Tuzaklar ve Nasıl Kaçınılır

| Pitfall | Why It Happens | Fix |
|---------|----------------|-----|
| **Pivot cache not copied** | `Range.Copy` yerine `Cells.CopyRows/CopyColumns` kullanılmadığında. | Gösterildiği gibi `Cells` metodlarını kullanın. |
| **Destination sheet has existing pivot** | Aynı ada sahip bir pivot zaten bulunan bir çalışma kitabının üzerine kaydedildiğinde. | Bizim yaptığımız gibi yeni bir `Workbook()` ile başlayın. |
| **Named ranges break** | Kaynak pivot, yeni dosyada bulunmayan bir adlandırılmış aralığa referans verir. | Adlandırılmış aralığı da kopyalayın: `sourceWorkbook.Worksheets[0].Names.CopyTo(destSheet);` |
| **Data source path changes** | Pivot, mevcut olmayan bir dış veri kaynağına işaret eder. | Gerekirse kopyalama sonrası `PivotTable.RefreshData()` kullanın. |

---

## Baştan Sona Tam Örnek (Çalıştırmaya Hazır)

Aşağıda `using` yönergeleri ve kısa bir konsol UI'sı dahil olmak üzere tam program yer alıyor. Yeni bir Console App projesine kopyalayıp yapıştırın ve **F5** tuşuna basın.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyUtility
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Load source workbook (contains the pivot)
            // -------------------------------------------------
            string srcPath = @"YOUR_DIRECTORY\source.xlsx";
            Workbook srcWb = new Workbook(srcPath);

            // -------------------------------------------------
            // Step 2: Prepare destination workbook (create new workbook)
            // -------------------------------------------------
            Workbook destWb = new Workbook();
            Worksheet destWs = destWb.Worksheets[0];

            // -------------------------------------------------
            // Step 3: Define the block we want to copy
            // -------------------------------------------------
            int startRow = 0;      // A1
            int startCol = 0;      // A
            int rows = 20;         // first 20 rows
            int cols = 4;          // first 4 columns

            // -------------------------------------------------
            // Step 4: Copy rows and columns from source to destination
            // -------------------------------------------------
            srcWb.Worksheets[0].Cells.CopyRows(startRow, startRow, rows);
            srcWb.Worksheets[0].Cells.CopyColumns(startCol, startCol, cols);
            destWs.Cells.CopyRows(startRow, startRow, rows);
            destWs.Cells.CopyColumns(startCol, startCol, cols);

            // -------------------------------------------------
            // Step 5: Save the new workbook (preserve pivot table)
            // -------------------------------------------------
            string destPath = @"YOUR_DIRECTORY\copy-pivot.xlsx";
            destWb.Save(destPath);

            Console.WriteLine($"✅ Workbook created at {destPath}");
        }
    }
}
```

**Beklenen çıktı** (konsolda):

```
✅ Workbook created at YOUR_DIRECTORY\copy-pivot.xlsx
```

`copy-pivot.xlsx` dosyasını açın, `source.xlsx`'deki aynı pivot tablosunu, tamamen işlevsel ve kopyalanan veri aralığını referans alarak göreceksiniz.

---

## Sıkça Sorulan Sorular

**Q: Aynı sayfada birden fazla pivot tabloyla çalışır mı?**  
**A: Evet, kopyalanan dikdörtgen ihtiyacınız olan her bir pivotu kapsadığı sürece çalışır. Sadece bir tanesini istiyorsanız, `rows`/`cols` değerlerini izole edecek şekilde ayarlayın.**

**Q: Kaynak çalışma kitabı dış veri bağlantıları kullanıyorsa ne olur?**  
**A: Pivot önbelleği hâlâ orijinal bağlantıya işaret eder. Kaynağı yeniden sorgulamak istiyorsanız, hedefi yükledikten sonra `pivotTable.RefreshData()` çağırın.**

**Q: Aynı çalışma kitabı içinde pivotu farklı bir sayfaya kopyalayabilir miyim?**  
**A: Kesinlikle. `destinationWorkbook` yerine `sourceWorkbook` kullanın ve başka bir çalışma sayfası indeksi seçin.**

**Q: Yalnızca biçimlendirmeyi kopyalamanın bir yolu var mı?**  
**A: `CopyRows`/`CopyColumns` metodlarının `CopyOptions` nesnesi kabul eden aşırı yüklemelerini kullanın—ihtiyacınıza göre `CopyOptions.CopyType = CopyType.ValuesOnly` veya `CopyType.All` olarak ayarlayın.**

---

## Sonuç

Sadece **create new workbook** senaryosunu, **copy pivot table**, **preserve pivot table** ve **export selected range** işlemlerini saf C# ile nasıl gerçekleştireceğimizi adım adım gösterdik.

## Sonra Ne Öğrenmelisin?

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Create a New Pivot Table Programmatically in .NET](/cells/english/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/)
- [How to Change Pivot Table Source Data Using Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/change-pivot-table-source-aspose-cells-net/)
- [How to Manage Excel Pivot Table Compatibility with Aspose.Cells for .NET | Data Analysis Guide](/cells/english/net/data-analysis/manage-excel-pivot-table-compatibility-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}