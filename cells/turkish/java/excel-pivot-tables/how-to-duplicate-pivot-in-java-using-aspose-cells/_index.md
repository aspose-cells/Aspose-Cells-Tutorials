---
category: general
date: 2026-09-18
description: Java'da Aspose.Cells ile pivot nasıl çoğaltılır – pivot tablosunu çalışma
  kitapları arasında hızlı ve güvenilir bir şekilde kopyalayın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: tr
lastmod: 2026-09-18
og_description: Aspose.Cells kullanarak Java’da pivot tablo nasıl çoğaltılır. Temiz
  Java kodu ile çalışma kitapları arasında bir pivot tabloyu kopyalamak için bu kapsamlı
  öğreticiyi izleyin.
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: Java’da bir pivot tabloyu kopyala – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells kullanarak Java'da pivot tabloyu nasıl kopyalarız
url: /tr/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.Cells kullanarak pivot nasıl çoğaltılır

Java uygulamasında **pivot nasıl çoğaltılır** ihtiyacınız varsa, bu kılavuz size tam adımları gösterir. Bir Excel çalışma kitabını yükleyerek, pivotun hücre alanını tanımlayarak ve bu aralığı yeni bir çalışma kitabına kopyalayarak, pivot tablosunu tanımını veya verilerini kaybetmeden taşıyabilirsiniz.

Pivot tablosunu kopyalamak, raporlar oluştururken, analizleri arşivlerken veya büyük bir çalışma kitabını modüler parçalara ayırırken yaygın bir gereksinimdir. Bu öğreticide **çalışma kitapları arasında aralık kopyalama**, **Excel çalışma kitabını Java’da yükleme** ve **pivot nasıl kopyalanır** konularını güvenli bir şekilde öğreneceksiniz.

Aspose.Cells for Java kullanarak `Source.xlsx` dosyasındaki pivot tablosunu `PivotCopied.xlsx` dosyasına çoğaltan, çalıştırmaya hazır bir Java programı ile bitireceksiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* JDK 8 veya daha yeni bir sürüm yüklü.
* Maven (veya başka bir yapı aracı) bağımlılıkları yönetmek için.
* Aspose.Cells for Java sürüm 23.10 veya üzeri. Aşağıdaki Maven bağımlılığını `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* Pivot tablosunu **A1:H30** aralığında içeren bir kaynak çalışma kitabı (`Source.xlsx`).

## Java'da pivot nasıl çoğaltılır

Temel fikir basittir:

1. **Kaynak çalışma kitabını yükleyin** – bu, pivotun bulunduğu çalışma sayfasına erişmenizi sağlar.
2. **Pivotu kapsayan hücre alanını tanımlayın**.
3. **Hedef çalışma kitabını oluşturun** – kopyalanan aralığı alacak boş bir dosya.
4. **Aralığı kopyalayın** – Aspose.Cells otomatik olarak pivot tanımını çoğaltır.
5. **Hedef çalışma kitabını kaydedin** – artık aynı pivotla ayrı bir dosyanız var.

Aşağıda bu adımları izleyen tam, çalıştırılabilir bir Java programı bulunmaktadır.

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### Neden bu çalışıyor

* **Aspose.Cells**, bir pivot tablosunu çalışma sayfasının hücre koleksiyonunun bir parçası olarak kabul eder. `copyRange` metodunu çağırdığınızda, kütüphane yalnızca hücre değerlerini değil, aynı zamanda temel pivot önbelleğini ve tanımını da kopyalar, böylece yeni çalışma kitabı tam işlevsel bir kopya içerir.
* `CopyOptions` nesnesi varsayılan olarak formülleri, biçimleri ve gömülü nesneleri korur. Daha fazla kontrol gerektiğinde (ör. `setCopyColumnWidths(true)`) özelleştirebilirsiniz.

## Çalışma kitapları arasında aralık kopyalama – daha derin bakış

Yukarıdaki örnek tek bir bitişik bloğu kopyalarken, `copyRange` herhangi bir dikdörtgen alanı işleyebilir. Pivotunuz bitişik olmayan aralıkları kapsıyorsa, `copyRange` metodunu birden çok kez çağırabilir veya tüm sayfayı çoğaltmak için `Worksheet.copy` kullanabilirsiniz.

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**İpucu:** Büyük çalışma kitaplarını kopyalarken, gereksiz stil çoğaltmayı önlemek ve performansı artırmak için `CopyOptions.setPreserveCellStyle(true)` özelliğini etkinleştirin.

## Pivotu çalışma kitabına kopyalama – birden fazla pivotu işleme

Kaynak sayfada birden fazla pivot varsa, çalışma sayfasının pivot tabloları üzerinde döngü kurarak her birini ayrı ayrı kopyalayabilirsiniz:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

Bu yaklaşım, her pivotun orijinal adını ve veri kaynağını korumasını sağlar.

## Excel çalışma kitabını Java’da yükleme – yaygın tuzaklar

* **Dosya yolu ayırıcıları:** Kodu platform bağımsız tutmak için ileri eğik çizgi (`/`) veya `File.separator` kullanın.
* **Lisans eksikliği:** Aspose.Cells değerlendirme modunda çalışır, ancak çıktı bir filigran içerir. Filigranı kaldırmak için çalışma kitabını yüklemeden önce `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` kodu ile lisans kaydedin.
* **Büyük dosyalar:** 100 MB'den büyük çalışma kitapları için bellek tüketimini azaltmak amacıyla `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` ve akış seçeneklerini kullanmayı düşünün.

## Tam uçtan uca örnek özeti

Her şeyi bir araya getirdiğimizde, IDE'nize kopyalayıp yapıştırabileceğiniz son program aşağıdadır:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Beklenen çıktı:** Çalıştırdıktan sonra `PivotCopied.xlsx` belirtilen dizinde ortaya çıkar. Excel'de açtığınızda, `Source.xlsx` dosyasındaki aynı pivot tablo düzeni, filtreler ve veriler gösterilir. Tüm hesaplanmış alanlar ve biçimlendirme korunur.

## Sıkça Sorulan Sorular

* **Bu eski Excel formatlarıyla (.xls) çalışır mı?**  
  Evet. Aspose.Cells formatı otomatik olarak algılar. `new Workbook("file.xls")` kullanın ve aynı kopyalama mantığı geçerli olur.

* **Pivot dış veri kaynaklarına başvuruyorsa ne olur?**  
  Kopya, orijinal veri kaynağı referansını korur. Hedef ortam bu kaynağa ulaşamazsa, pivot `#REF!` hataları gösterir. Bunu önlemek için kopyaladıktan sonra pivotu yenileyin veya veri kaynağını `PivotTable.setDataSource(...)` ile değiştirin.

* **Pivotu belirli bir sayfa adına kopyalayabilir miyim?**  
  Kesinlikle. Hedef çalışma sayfasını oluşturduktan sonra adını yeniden adlandırın:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## Sonuç

Artık Java’da Aspose.Cells kullanarak **pivot nasıl çoğaltılır** tablolarını, **çalışma kitapları arasında aralık kopyalama** yöntemini ve **Excel çalışma kitabını Java’da yükleme** için en iyi uygulamaları biliyorsunuz. Yükle, tanımla, hedef oluştur, kopyala ve kaydet adımlarını izleyerek rapor üretimini otomatikleştirebilir, analizleri arşivleyebilir veya karmaşık çalışma kitaplarını pivot işlevselliğini kaybetmeden bölüştürebilirsiniz.

Sonraki adımda, birden fazla sayfa içeren **pivotu çalışma kitabına kopyalama** gibi ilgili konuları keşfedebilir veya Aspose dışı senaryolar için Apache POI kullanarak çoğaltılan pivotu daha büyük bir veri işleme hattına entegre edebilirsiniz. Büyük çalışma kitapları için performansı ince ayarlamak amacıyla farklı `CopyOptions` ayarlarıyla deneyler yapın.

İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [Aspose.Cells for Java ile Excel'de Pivot Tabloları Nasıl Oluşturulur: Kapsamlı Rehber](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java ile Excel Pivot Tablosu Kaynağını Güncelleme: Kapsamlı Rehber](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java Kullanarak Excel Çalışma Kitaplarında Pivot Alanlarını Gruplama - Kapsamlı Rehber](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}