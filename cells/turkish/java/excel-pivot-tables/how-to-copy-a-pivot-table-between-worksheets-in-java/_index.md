---
category: general
date: 2026-10-16
description: Aspose.Cells ile Java’da özet tabloyu nasıl kopyalarsınız – aralığı başka
  bir sayfaya ve sayfalar arasında verimli bir şekilde kopyalamayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: tr
lastmod: 2026-10-16
og_description: Java’da Aspose.Cells kullanarak pivot tablo nasıl kopyalanır. Bu öğreticide,
  bir aralığı başka bir sayfaya kopyalama ve çalışma sayfaları arasında aralığı kopyalama
  işlemlerini tam kod ile gösteriyoruz.
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: Java'da Çalışma Sayfaları Arasında Pivot Tablo Nasıl Kopyalanır – Adım Adım
  Rehber
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: Java'da çalışma sayfaları arasında bir pivot tabloyu nasıl kopyalarım
url: /tr/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da çalışma sayfaları arasında bir pivot tabloyu nasıl kopyalanır

Aynı çalışma kitabında bir sayfadan diğerine **how to copy pivot table** yapmanız gerekiyorsa, bu kılavuz eksiksiz, çalıştırmaya hazır bir çözüm sunar. Pivot tabloyu içeren kaynak aralığı nasıl kopyalayacağınızı, işlevselliğini nasıl koruyacağınızı ve sonucu nasıl doğrulayacağınızı göreceksiniz — tümü Aspose.Cells for Java kullanılarak.

Pivot tablo kopyalamak, raporları programlı olarak oluşturduğunuzda yaygın bir görevdir ve bunu doğru yapmak pivot önbelleğini kaybetmeyi veya formüllerin kırılmasını önler. Bu öğreticinin sonunda **copy range to another sheet** ve **copy range between worksheets** ifadelerini manuel adım olmadan yapabilecek durumdasınız.

## Öğrenecekleriniz

* Bir pivot tablo içeren mevcut bir Excel dosyasını yükleyin.
* Pivot tabloyu tutan kaynak aralığı tanımlayın.
* Farklı bir çalışma sayfasında hedef aralığı tanımlayın.
* `CopyOptions` kullanarak pivot tablonun bütünlüğünü koruyun.
* Kopyalanan pivot tablonun beklendiği gibi çalıştığını doğrulayın.

**Önkoşullar**

* Java 17 veya daha yeni bir sürüm.
* Aspose.Cells for Java (versiyon 23.12 veya daha yeni).  
* İlk sayfada bir pivot tablo içeren bir Excel dosyası (`input.xlsx`).

---

## Aspose.Cells ile pivot tabloyu nasıl kopyalanır

İşlemin temeli dört adımlı bir süreçtir: çalışma kitabını yüklemek, kaynak aralığı bulmak, hedef aralığı ayarlamak ve kopyalamayı gerçekleştirmek. Aşağıda her adım ayrıntılı olarak açıklanmıştır.

### Adım 1: Çalışma kitabını yükleyin

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*Bu adım neden?*  
Çalışma kitabını yüklemek, tüm dosyayı belleğe getirir ve size çalışma sayfalarına, hücrelere ve pivot önbelleğine erişim sağlar. Aspose.Cells dosya formatını otomatik olarak okur, bu yüzden `.xls` ve `.xlsx` arasında endişelenmenize gerek yok.

### Adım 2: Pivot tabloyu içeren kaynak aralığı bulun

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*Bu adım neden?*  
Pivot tablo, gizli bir önbelleğe de referans veren bir hücre bloğunda depolanır. Bu örnekteki (`A1:G20`) tam aralığı seçerek, aralık kopyalandığında önbelleğin bağlı kalmasını sağlarsınız.

### Adım 3: Başka bir sayfada hedef aralığı tanımlayın

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*Bu adım neden?*  
Farklı bir çalışma sayfasında bir hedef seçmek, **copy range to another sheet** yapmanızı sağlar. Sol‑üst hücre (`A1`) yaygın bir başlangıç noktasıdır, ancak adresi değiştirerek istediğiniz yere yerleştirebilirsiniz.

### Adım 4: Pivot tabloyu koruyarak kaynak aralığı kopyalayın

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*Bu adım neden?*  
`CopyOptions` neyin aktarılacağını kontrol eder. `PasteType.PASTE_ALL` kullanmak, pivot tablonun, biçimlendirmesinin ve temel formüllerin kopyalanmasını garanti eder. Bu seçenekler olmadan, yalnızca ham değerler kopyalanabilir ve pivot işlevselliği bozulur.

### Adım 5: Çalışma kitabını kaydedin ve sonucu doğrulayın

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

`output.xlsx` dosyasını Excel'de açın ve şunları doğrulayın:

* İkinci sayfa, orijinaliyle aynı tam işlevsel pivot tabloyu içerir.
* Pivot tabloyu yenilediğinizde veri güncellenir, önbelleğin bütün olduğunu kanıtlar.

## Java kullanarak bir sayfaya aralık kopyalama

Amacınız sadece pivot tablo olmadan **copy range to another sheet** ise, aynı kod normal bir hücre aralığıyla çalışır. Tek değişiklik kaynak adresidir. `CopyOptions` yapılandırması aynı kalır ve formüllerin ve biçimlendirmelerin korunmasını sağlar.

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

Bu kod parçacığı, API'nin hem pivot hem de pivot olmayan senaryolar için esnekliğini gösterir.

## Formülleri kaybetmeden çalışma sayfaları arasında aralık kopyalama

**copy range between worksheets** yaptığınızda, diğer sayfalara referans veren formüller göreli referanslar değişirse kırılabilir. Bunu önlemek için:

1. Sadece formüllere ihtiyacınız varsa `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` kullanın.
2. Hedef sayfayı aynı çalışma kitabında tutun, böylece iç referanslar geçerli kalır.
3. Kopyaladıktan sonra `workbook.calculateFormula();` çağırarak yeniden hesaplamayı zorlayın.

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

Bu ek adımlar, kopyalanan aralığın, birden fazla çalışma sayfasına yayılsa bile, orijinali gibi tam olarak davranmasını sağlar.

## Profesyonel ipuçları ve yaygın tuzaklar

| Durum | İpucu |
|-----------|-----|
| **Pivot önbelleği güncellenmiyor** | Kopyaladıktan sonra, önbelleği yenilemek için `destSheet.getPivotTables().get(0).refresh();` çağırın. |
| **Farklı bir çalışma kitabına kopyalama** | `Workbook destWorkbook = new Workbook();` kullanın ve ardından `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);` yapın. Gerekirse pivot önbelleğini ayrı olarak kopyalamayı unutmayın. |
| **Büyük pivot tablolar** | `-Xmx2g` gibi Java yığın boyutunu artırarak kopyalama sırasında `OutOfMemoryError` hatasını önleyin. |
| **Stilleri koruma** | `copyOptions.setPasteType(PasteType.PASTE_ALL)` ayarlayın; aksi takdirde yalnızca değerler kopyalanır. |

## Beklenen çıktı

Tam programı çalıştırdığınızda `output.xlsx` oluşturulur. Excel'de açıldığında:

* **Sheet2!A1:G20** aynı pivot tabloyu **Sheet1!A1:G20** ile aynı şekilde gösterir.
* Pivot alan listesi, satır/sütun etiketleri ve veri değerleri kaynağa eşittir.
* Pivotu yenilediğinizde sayılar güncellenir, önbelleğin işlevsel olduğunu doğrular.

Konsol şu çıktıyı verir:

```
Pivot table copied successfully.
```

## Sonuç

Bu öğreticide, Aspose.Cells for Java kullanarak bir çalışma sayfasından diğerine **how to copy pivot table** yaptığınızı öğrendiniz. Çalışma kitabını yükleyerek, doğru kaynak aralığını seçerek, bir hedef tanımlayarak ve `CopyOptions` yapılandırarak, tüm pivot işlevselliğini koruyarak **copy range to another sheet** ve **copy range between worksheets** işlemlerini güvenilir şekilde yapabilirsiniz.

Sonraki adımda şunları keşfedebilirsiniz:

* Kopyalanan pivot tabloyu PDF veya HTML'ye dışa aktarmak.
* Birden fazla çalışma kitabında pivot tablo yenilemelerini otomatikleştirmek.
* `CopyOptions` kullanarak yalnızca belirli öğeleri (ör. değerler, biçimler) kopyalamak.

Farklı aralık adresleri, çalışma kitabı yapıları veya hatta çapraz‑çalışma kitabı kopyalarıyla denemeler yapmaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java'da aralık kopyalama – Aspose.Cells ile Pivot Tablo Kopyalama](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Java'da Pivot Tabloyu Kopyalama – Tam Aspose.Cells Rehberi](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Excel'de Pivot Tablo Kopyalama – Java Kullanarak Adım Adım Rehber](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}