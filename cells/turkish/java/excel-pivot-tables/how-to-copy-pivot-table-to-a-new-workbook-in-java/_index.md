---
category: general
date: 2026-10-26
description: Java kullanarak pivot tabloyu yeni bir çalışma kitabına nasıl kopyalayacağınızı,
  biçimlendirmeyi ve pivot tanımını koruyarak, Aspose.Cells aracılığıyla biçimlendirilmiş
  Excel aralığını kopyalarken öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- copy excel range
- create empty workbook
- copy range with formatting
language: tr
lastmod: 2026-10-26
og_description: Aspose.Cells ile Java’da bir pivot tabloyu yeni bir çalışma kitabına
  kopyalayın. Bu kılavuz, Excel aralığını nasıl kopyalayacağınızı, biçimlendirmeyi
  koruyarak ve boş bir çalışma kitabını verimli bir şekilde oluşturacağınızı gösterir.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new Excel
  workbook
og_title: Java’da bir pivot tabloyu yeni bir çalışma kitabına kopyalama – adım adım
  rehber
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  headline: How to copy pivot table to a new workbook in Java
  type: TechArticle
- description: Learn how to copy pivot table to a new workbook using Java, preserving
    formatting and the pivot definition while you copy excel range with formatting
    via Aspose.Cells.
  name: How to copy pivot table to a new workbook in Java
  steps:
  - name: Prerequisites
    text: '* Java 17 or later. * Aspose.Cells for Java (version 23.10 or newer). *
      Basic familiarity with Java IDEs (IntelliJ IDEA, Eclipse, etc.).'
  - name: Why this works
    text: '* `new Workbook()` **creates empty workbook** with a default sheet, avoiding
      the need to delete existing data. * `CopyOptions` tells Aspose.Cells to copy
      **pivot table** metadata, not just raw values. The `PASTE_ALL` mode also carries
      cell styles, number formats, and conditional formatting—fulfillin'
  - name: Edge cases to consider
    text: '| Situation | Recommended handling | |----------------------------------------|----------------------|
      | Source workbook has multiple pivots | Copy each pivot’s range separately or
      copy the whole sheet. | | Destination already contains data | Choose a non‑conflicting
      start cell (e.g., "H1") when cal'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java'da pivot tabloyu yeni bir çalışma kitabına nasıl kopyalarım?
url: /tr/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Pivot Tablosunu Yeni Bir Çalışma Kitabına Kopyalama

Bir Excel dosyasından diğerine **copy pivot table** (pivot tablosunu) kopyalamanız gerekiyorsa, bu rehber size eksiksiz, çalıştırılabilir bir çözüm sunar. Pivot tanımını nasıl koruyacağınızı, tüm biçimlendirmeyi nasıl tutacağınızı ve bir Excel aralığını kopyalarken yaygın hatalardan nasıl kaçınacağınızı göreceksiniz.

Pivot tablosunu kopyalamak genellikle *how to copy pivot* gibi soruları gündeme getirir; veri kaynağını bozmadan ya da stilleri kaybetmeden nasıl kopyalanır? Bu öğreticinin sonunda, boş bir çalışma kitabı oluşturan, istenen aralığı kopyalayan ve sonucu pivot tablo bozulmadan kaydeden, kendi içinde çalışan bir Java programına sahip olacaksınız.

## Ne elde edeceksiniz

* Pivot tablo içeren bir kaynak çalışma kitabını yükleyin.  
* **Create empty workbook** kopyalanan verileri alacak.  
* **Copy excel range** pivotu içeren, pivotu ve biçimlendirmeyi koruyan seçeneklerle.  
* Hedef dosyayı kaydedin ve pivotun orijinali gibi tam olarak çalıştığını doğrulayın.

### Önkoşullar

* Java 17 veya üzeri.  
* Aspose.Cells for Java (sürüm 23.10 veya daha yeni).  
* Java IDE'lerine (IntelliJ IDEA, Eclipse vb.) temel aşinalık.  

> **Pro tip:** Hızlı test için ücretsiz Aspose.Cells değerlendirme lisansını kullanın; üretim ortamında tam lisansla değiştirin.

## Pivot Tablosunu Yeni Bir Çalışma Kitabına Kopyalama

İlk adım, kaynak ve hedef çalışma kitaplarını ayarlamaktır. Hedef, **create empty workbook** çağrısı ile başlar; bu, tek bir çalışma sayfasına sahip temiz bir dosya sağlar.

```java
import com.aspose.cells.*;

public class CopyPivotExample {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Create an empty workbook that will receive the copied range
        Workbook destWb = new Workbook();

        // Get the first worksheet from each workbook
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        Worksheet destSheet = destWb.getWorksheets().get(0);

        // Configure copy options to preserve the pivot table and formatting
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // ensures pivot and styles are kept

        // Copy the range that contains the pivot table
        srcSheet.getCells().copyRange("A1:D20", destSheet.getCells(), "A1", copyOptions);

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
    }
}
```

### Neden Bu Çalışır

* `new Workbook()` **creates empty workbook** varsayılan bir sayfa ile oluşturur, mevcut verileri silme ihtiyacını ortadan kaldırır.  
* `CopyOptions` Aspose.Cells'e sadece ham değerleri değil, **pivot table** meta verilerini kopyamasını söyler. `PASTE_ALL` modu ayrıca hücre stillerini, sayı biçimlerini ve koşullu biçimlendirmeyi taşır—**copy range with formatting** gereksinimini karşılar.  
* `copyRange` **copy excel range** işlemini gerçekleştirir ve kaynağın iç yapısını korur, böylece kopyadan sonra pivot işlevsel kalır.

## Pivotu Biçimlendirmeyi Kaybetmeden Nasıl Kopyalarsınız

Yalnızca varsayılan `CopyOptions` kullanırsanız, eski Aspose.Cells sürümlerinde bazı stil bilgileri atlanabilir. Yapıştırma tipini açıkça ayarlamak, **copy range with formatting**'in dikkate alındığını garanti eder.

```java
CopyOptions copyOptions = new CopyOptions();
copyOptions.setPasteType(PasteType.PASTE_ALL);          // copy values, formulas, formats
copyOptions.setPasteSpecialType(PasteSpecialType.ALL); // include column widths and row heights
```

`setPasteSpecialType` eklemek, sütun genişliklerinin, satır yüksekliklerinin ve hatta veri doğrulama kurallarının aralıkla birlikte taşınmasını sağlar. Bu, pivot tablosu özel genişlikli birden fazla sütunu kapsadığında özellikle faydalıdır.

## Kopyalamadan Önce Boş Çalışma Kitabı Oluşturma

Bazen geliştiriciler, zaten veri içeren mevcut bir çalışma kitabına kopyalamaya çalışırlar. Bu, çakışan aralıklar veya beklenmeyen üzerine yazmalara neden olabilir. **create empty workbook** çağrısı ile başlamak işlemi izole eder:

```java
Workbook destWb = new Workbook(); // fresh file with one sheet
Worksheet destSheet = destWb.getWorksheets().get(0); // reference the clean sheet
```

Hedefte birden fazla sayfa gerekiyorsa, kopyalamadan sonra ekleyebilirsiniz:

```java
destWb.getWorksheets().add("Summary");
```

## CopyOptions Kullanarak Biçimlendirmeli Excel Aralığını Kopyalama

Pivot tabloların ötesinde, aynı desen biçimlendirme korunması gereken herhangi bir **copy excel range** için çalışır—grafikler, tablolar veya koşullu biçimler.

```java
// Example: copy a styled table from A1 to G15
srcSheet.getCells().copyRange("A1:G15", destSheet.getCells(), "A1", copyOptions);
```

`CopyOptions` örneği aynı kalır, böylece farklı aralıklar arasında tutarlı davranış elde edersiniz.

### Dikkate Alınması Gereken Kenar Durumları

| Durum                                 | Önerilen işlem |
|---------------------------------------|-----------------|
| Kaynak çalışma kitabında birden fazla pivot var | Her pivotun aralığını ayrı ayrı kopyalayın veya tüm sayfayı kopyalayın. |
| Hedef zaten veri içeriyor             | `copyRange` çağırırken çakışmayan bir başlangıç hücresi seçin (ör. "H1"). |
| Pivot veri kaynağı harici (ör. DB)    | Hedef çalışma kitabının aynı harici veri kaynağına işaret ettiğinden emin olun veya kopyadan sonra pivotu yenileyin. |
| Büyük çalışma kitabı ( > 10 MB )      | `OutOfMemoryError` hatasından kaçınmak için Java yığın boyutunu (`-Xmx2g`) artırın. |

## Sonucu Doğrulama

Programı çalıştırdıktan sonra `destination.xlsx` dosyasını açın. Şunları görmelisiniz:

* `source.xlsx` içindeki aynı pivot tablo düzeni.  
* Tüm hücre renkleri, sayı biçimleri ve sütun genişlikleri korunmuş.  
* Pivotun veri kaynağı yeni dosya içindeki orijinal veri aralığına hâlâ işaret ediyor, bu yüzden pivotu yenilediğinizde değerler doğru şekilde güncellenir.

Pivot statik bir tablo olarak görünüyorsa, `CopyOptions.setPasteType(PasteType.PASTE_ALL)` ayarlandığını iki kez kontrol edin. Bu seçenek olmadan Aspose.Cells pivotu düz veri olarak işler.

## Sonuç

Artık Java'da **copy pivot table**'ı yeni bir çalışma kitabına biçimlendirme, veri bağlantıları ve sayfa düzeni korunarak nasıl kopyalayacağınızı biliyorsunuz. Tam çözüm, bir kaynak dosyayı yüklemeyi, **create empty workbook**'ı, **copy excel range** seçeneklerini yapılandırmayı ve sonucu kaydetmeyi gösterir.

Buradan, **how to copy pivot**'ı farklı çalışma sayfalarına kopyalama, pivotların yanına grafik ekleme veya birden fazla çalışma kitabının toplu işlenmesini otomatikleştirme gibi ilgili konuları keşfedebilirsiniz. `CopyOptions` ayarlarıyla deneyler yaparak özel otomasyon ihtiyaçlarınıza uyarlayın; böylece elinizde güçlü bir Excel işleme araç seti olacaktır.

## Sonra Ne Öğrenmelisiniz?

Bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsayan aşağıdaki öğreticiler bulunmaktadır. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Java'da Yeni Çalışma Kitabı Oluşturma – Pivot Tablosunu Kopyalama Tam Rehberi](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Çalışma Kitapları Arasında Pivot Tablosu Kopyalama – Adım Adım Java Rehberi](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)
- [Java'da Aralığı Nasıl Kopyalar ve Pivot Tablosunu Nasıl Korur](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}