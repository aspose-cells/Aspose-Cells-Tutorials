---
category: general
date: 2026-10-23
description: Pivot tablolarını koruyarak Java’da bir Excel sayfasını nasıl çoğaltacağınızı
  öğrenin. Bu kılavuz ayrıca pivot tablolarını kopyalama, Excel aralıklarını kopyalama
  ve pivot verileriyle bir sayfayı kopyalama yöntemlerini gösterir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: tr
lastmod: 2026-10-23
og_description: Pivot tablolarını koruyarak Java’da bir Excel sayfasını çoğaltın.
  Pivot tablolarını kopyalamak, Excel aralıklarını kopyalamak ve pivot verileriyle
  bir sayfayı kopyalamak için bu eksiksiz öğreticiyi izleyin.
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: Java’da pivot tabloları içeren bir Excel sayfasını kopyalama – adım adım
  rehber
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: Java'da bir Excel sayfasını nasıl çoğaltır ve pivot tablolarını bozulmadan
  korursunuz
url: /tr/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Excel sayfasını nasıl çoğaltır ve pivot tablolarını bozulmadan tutarsınız

Eğer **Excel sayfasını çoğaltmanız** ve tüm pivot tablolarının çalışır durumda kalmasını istiyorsanız, bu kılavuz tam olarak bunu nasıl yapacağınızı gösterir. Bir sayfayı, belirli bir aralığı ve hatta bir pivot tabloyu başka bir çalışma kitabına kopyalayan özlü bir çözümü, tamamen Java ve Aspose.Cells kullanarak göreceksiniz.

Excel sayfasını çoğaltmak, bir şablondan aylık raporlar üretirken ya da test amaçlı bir kum havuzu kopyasına ihtiyaç duyduğunuzda yaygın bir görevdir. Aşağıdaki kod, `setCopyPivotTable(true)` seçeneğini tanıtan Aspose.Cells 25.11 veya daha yeni sürümleriyle çalışır.

## Gerekenler

Başlamadan önce şunların yüklü olduğundan emin olun:

- Java 17 (veya daha yeni bir JDK)
- Projenizde Aspose.Cells for Java 25.11 veya daha yeni sürüm (`com.aspose:aspose-cells:25.11` Maven koordinatı)
- Pivot tablo içeren bir kaynak çalışma kitabı (`SourceWithPivot.xlsx`)
- Tercih ettiğiniz IDE veya derleme aracı (IntelliJ IDEA, Eclipse, Maven, Gradle vb.)

## Adım 1: Pivot tablosunu içeren kaynak çalışma kitabını yükleyin

İlk işlem, korumak istediğiniz pivotun bulunduğu çalışma kitabını açmaktır.

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **Neden önemli:** Kaynak çalışma kitabını yüklemek, çalışma sayfası nesnelerine, hücrelere ve gömülü pivot tablolara erişmenizi sağlar. Bunu yapmadan kopyalamak istediğiniz pivot verisine referans veremezsiniz.

## Adım 2: Boş bir hedef çalışma kitabı oluşturun (veya mevcut birini yükleyin)

Boş bir çalışma kitabı ile başlayabilir ya da çoğaltılmış sayfayı alacak mevcut bir dosyayı açabilirsiniz.

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **İpucu:** Zaten bir raporlama çalışma kitabınız varsa, yukarıdaki satırı `new Workbook("ExistingReport.xlsx")` ile değiştirerek çoğaltılmış sayfayı ona ekleyebilirsiniz.

## Adım 3: Tüm çalışma sayfasını kopyalayın – pivot tablo otomatik olarak korunur

Tüm çalışma sayfasını kopyalamak, **pivotlu sayfayı kopyalama** için en basit yoldur. Aspose.Cells, pivot tanımını ve önbelleğini otomatik olarak kopyalar.

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **Neden işe yarar:** `addCopy`, sayfa yapısını, hücre değerlerini, stilleri ve gömülü pivot tabloları klonlar. `dstWb` içindeki yeni çalışma sayfası, orijinaliyle aynı görünecek ve pivot önbelleği dahil olacaktır.

## Adım 4: (İsteğe bağlı) Pivot tabloyu içeren belirli bir aralığı kopyalayın

Bazen tüm sayfayı istemezsiniz—belki sadece pivotun bulunduğu bölümü ihtiyacınız vardır. İşte **Excel aralığını kopyalama** ve pivotun da kopyalanmasını açıkça talep etme zamanı.

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **Nasıl yardımcı olur:** `setCopyPivotTable(true)` bayrağı, sınırlı bir aralık kopyalansa bile pivot tanımının çoğaltılmasını zorlar. Bu bayrak olmadan yalnızca ham veri kopyalanır ve pivot kaybolur.

## Adım 5: Hedef çalışma kitabını kaydedin

Son olarak, çoğaltılmış içeriği yeni bir dosyaya yazın.

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### Beklenen çıktı

Programı çalıştırdığınızda hedef dizinde `DuplicatedWithPivot.xlsx` oluşturulur. Dosyayı Excel’de açtığınızda şunları görürsünüz:

- `Sheet1 (Copy)` (veya “Copy” eklenmiş orijinal ad) adlı yeni bir çalışma sayfası
- Pivot tablo, kaynak sayfadaki gibi tam işlevsel olarak görünür
- İsteğe bağlı aralık kopyası kullandıysanız, yalnızca A1:G30 hücreleri bulunur, ancak pivot hâlâ çalışır çünkü önbelleği kopyalanmıştır

## Yaygın sorular ve kenar durumları

### Tüm sayfayı kopyalamadan pivotu başka bir çalışma kitabına nasıl kopyalarım?

Sadece pivot ve temel verilerini içeren aralığı kopyalayın, ardından `setCopyPivotTable(true)` kullanın. **Adım 4**'teki aynı kod geçerlidir; sadece aralığın veri kaynağını kapsadığından emin olun.

### Kaynak çalışma kitabında birden fazla pivotlu çalışma sayfası varsa ne olur?

Çoğaltmak istediğiniz her çalışma sayfası için **Adım 3**'ü tekrarlayın:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### Korunan (protected) çalışma sayfalarıyla bu çalışır mı?

Aspose.Cells korunan sayfaları kopyalayabilir, ancak pivotu kopyaladıktan sonra değiştirmek istiyorsanız önce korumayı kaldırmanız gerekir:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### Aynı ada sahip bir sayfa zaten bulunan bir çalışma kitabına pivot tabloyu kopyalayabilir miyim?

Evet. `addCopy` metodunu benzersiz bir adla kullanın:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## Pro ipucu: pivot önbelleğini doğrulayın

Kopyalama sonrası, pivot önbelleğinin varlığını programatik olarak kontrol edebilirsiniz:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

Önbellek kimliği negatif olmayan bir sayı olarak yazdırıyorsa, pivot başarıyla çoğaltılmış demektir.

## Sonuç

Artık Java’da **Excel sayfasını çoğaltma** ve tüm pivot tablolarını koruma, **pivot tabloyu kopyalama**, **pivotlu bir Excel aralığını kopyalama** ve **pivotlu sayfa kopyalama** ya da **pivotu çalışma kitabına kopyalama** konularını Aspose.Cells 25.11+ ile nasıl yapacağınızı biliyorsunuz. Bu desenleri rapor üretimini otomatikleştirmek, şablon klonları oluşturmak veya aynı pivot‑tabanlı analizlere ihtiyaç duyan test ortamları inşa etmek için uygulayın.

Daha fazlasını keşfetmeye hazır mısınız? Çoğaltılmış çalışma kitabını PDF’ye dışa aktarın ya da kopyalama sonrası pivot önbelleğini programatik olarak yenileyerek en güncel verilerin yansıtıldığından emin olun. İyi kodlamalar!


## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve kendi projelerinizde ek API özelliklerini öğrenmenize ve alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olur.

- [How to duplicate worksheet and preserve pivot tables in Java](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [How to Copy Pivot Table in Java – Complete Aspose.Cells Guide](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [How to copy range and preserve a pivot table in Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}