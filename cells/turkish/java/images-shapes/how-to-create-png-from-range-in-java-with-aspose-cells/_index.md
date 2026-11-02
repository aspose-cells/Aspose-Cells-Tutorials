---
category: general
date: 2026-10-07
description: Aralıktan PNG oluşturmayı ve verileri Java’da PNG olarak dışa aktarmayı
  öğrenin. Bu kılavuz, Aspose.Cells kullanarak Excel aralığı görüntüsünü nasıl kaydedeceğinizi
  gösterir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: tr
lastmod: 2026-10-07
og_description: Java'da bir aralıktan PNG oluşturun ve verileri Aspose.Cells ile PNG
  olarak dışa aktarın. Excel aralık görüntüsünü anında kaydetmek için bu kapsamlı
  öğreticiyi izleyin.
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: Java'da aralıktan PNG oluşturma – adım adım Aspose.Cells rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells ile Java'da aralıktan PNG nasıl oluşturulur
url: /tr/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Aspose.Cells kullanarak aralıktan PNG oluşturma

Bir Excel çalışma kitabında **aralıktan PNG oluşturmanız** gerekiyorsa, bu öğretici bunu tam olarak nasıl yapacağınızı gösterir. Kılavuzun sonunda **verileri PNG olarak dışa aktarabilir**, bir Excel aralık görüntüsü kaydedebilir ve dosyayı raporlar veya web sayfalarında yeniden kullanabilirsiniz.

Bir çalışma kitabını yükleyen, istenen hücreleri seçen, bunları PNG olarak işleyen ve sonucu diske kaydeden tam, çalıştırılabilir bir Java programı göreceksiniz. Harici araçlara gerek yok—Aspose.Cells her şeyi dahili olarak yönetir.

## Bu öğreticide neler ele alınır

* Aspose.Cells için önkoşullar ve Maven kurulumu
* Bir pivot tablo veya herhangi bir veri aralığı içeren bir çalışma kitabını yükleme
* Dönüştürmek istediğiniz tam hücre aralığını tanımlama
* PNG çıktısı için görüntü seçeneklerini yapılandırma
* Aralığı işleyip PNG dosyasını kaydetme
* Yüksek kaliteli görüntüler için yaygın tuzaklar ve ipuçları

Bu adımları tamamladıktan sonra, basit bir tablo ya da karmaşık bir pivot grafik olsun, herhangi bir aralık için **çalışma sayfasını PNG'ye dönüştürebileceksiniz**.

## Önkoşullar

* Java 17 veya daha yeni (kod JDK 11+ ile derlenir)
* Maven 3.6+ (veya tercih ederseniz Gradle)
* Aspose.Cells for Java 23.12 veya daha yeni – aşağıda gösterilen bağımlılığı ekleyin
* İçinde yakalamak istediğiniz aralığı barındıran mevcut bir Excel dosyası (`PivotWithStyle.xlsx`)

> **Pro ipucu:** Lisansınız yoksa, Aspose'tan geçici bir değerlendirme anahtarı talep edebilirsiniz. Kütüphane ek bir yapılandırma olmadan değerlendirme modunda çalışır.

### Maven bağımlılığı

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## Adım 1: Hedef aralığı içeren çalışma kitabını yükleyin

İlk işlem Excel dosyasını açmaktır. Aspose.Cells, Microsoft Office gerektirmeden dosyayı belleğe okur.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*Neden önemli*: Çalışma kitabını yüklemek, işleme için gereken çalışma sayfalarına, hücrelere ve sayfa‑ayarları özelliklerine erişim sağlar.

## Adım 2: Aralığı içeren çalışma sayfasına erişin

Çoğu çalışma kitabının varsayılan sayfası indeks 0'da bulunur, ancak sayfa adını da kullanabilirsiniz.

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Verileriniz farklı bir sayfada ise, `0` yerine uygun indeksi koyun veya `workbook.getWorksheets().get("SheetName")` kullanın.

## Adım 3: Dönüştürmek istediğiniz hücre aralığını tanımlayın

A1 notasyonu kullanarak herhangi bir dikdörtgen alanı belirtebilirsiniz. Bu örnekte `A1:D15` aralığını yakalıyoruz; bu bir pivot tablo veya normal bir veri bloğu olabilir.

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*Köşe durumu*: Aralık birleştirilmiş hücreler içeriyorsa, Aspose.Cells görüntüyü otomatik olarak birleştirilmiş alanı kapsayacak şekilde genişletir.

## Adım 4: PNG görüntü seçeneklerini hazırlayın

`ImageOrPrintOptions`, format, çözünürlük ve diğer işleme ayrıntılarını kontrol etmenizi sağlar. Kaydetme formatını PNG olarak ayarlamak kayıpsız kalite sağlar.

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

Kaynak hücrelerde küçük yazı tipleri veya ayrıntılı grafikler varsa DPI artırmak faydalıdır.

## Adım 5: İşleme alanını seçilen aralığa sınırlayın

Aralığı baskı alanı olarak atayarak, Aspose.Cells yalnızca bu hücreleri işler ve sayfanın geri kalanını yok sayar.

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

Bu adımı atlayarsanız, tüm çalışma sayfası rasterleştirilecek, bu da belleği tüketebilir ve daha büyük bir görüntü üretebilir.

## Adım 6: Aralığı işleyin ve çalışma sayfasına resmi ekleyin (isteğe bağlı)

Oluşturulan PNG'yi çalışma kitabına (ön izleme amacıyla) gömmek isterseniz, resmi bir resim olarak ekleyebilirsiniz. Bu adım, yalnızca dışa aktarım senaryoları için isteğe bağlıdır.

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*Neden bunu yapabilirsiniz*: Bazı iş akışları, dağıtımdan önce görüntünün çalışma kitabının bir parçası olmasını gerektirir, örneğin yerel hücreler ve görüntüler karışık bir yazdırılabilir rapor oluşturmak gibi.

## Adım 7: PNG dosyasını diske kaydedin

Son olarak, görüntüyü bir dosyaya yazın. `save` yöntemi `imageOptions` içinde belirtilen formatı dikkate alır.

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Program tamamlandığında, `PivotImage.png` hücreler `A1:D15`'in piksel‑tam bir anlık görüntüsünü içerecek.

### Beklenen çıktı

* `YOUR_DIRECTORY` içinde bulunan `PivotImage.png` adlı bir dosya.
* Görüntü, seçilen aralıktaki tam düzeni, yazı tiplerini, renkleri ve kenarlıkları gösterir.
* Kaynak aralık bir pivot tablo içeriyorsa, işlenen görüntü Excel'de gösterildiği gibi aynı stil ve hesaplanmış değerleri içerir.

## Yaygın senaryoların ele alınması

### Ayrık bir aralığı dışa aktarma

Aspose.Cells, ayrık aralıkları tek bir görüntüde işleme yapmaz. Birden fazla alanı dışa aktarmak için, her aralık için ayrı görüntüler oluşturun ve daha sonra bir görüntü işleme kütüphanesi (ör. ImageIO) ile birleştirin.

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### Büyük bir çalışma sayfasını PNG olarak kaydetme

Binlerce satırı kapsayan bir bütün sayfayı işlemek önemli miktarda bellek tüketebilir. Bunu şu şekilde azaltabilirsiniz:

* Daha küçük bir dosya için DPI'yi (`imageOptions.setResolution(72)`) düşürmek.
* İşlenen sayfa sayısını sınırlamak için `setPageCount` kullanmak.
* `worksheet.getPageSetup().setPrintArea(...)` ile bir seferde bir yazdırılabilir sayfa dışa aktarmak.

### Hücre formüllerini koruma

PNG bir raster formatıdır; formüller korunmaz. Alt akış tüketicileri ham veriye ihtiyaç duyuyorsa, aralığı ayrıca `Range.exportDataTable()` kullanarak CSV veya JSON olarak dışa aktarın.

## Tam, çalıştırılabilir örnek

Aşağıda IDE'nize kopyalayıp yapıştırabileceğiniz tam Java sınıfı bulunmaktadır. `YOUR_DIRECTORY` öğesini makinenizdeki mutlak veya göreli bir yol ile değiştirin.

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

Programı `mvn compile exec:java` (veya tercih ettiğiniz yapı aracı) ile çalıştırın. Çalıştırmadan sonra sonucu doğrulamak için `PivotImage.png` dosyasını açın.

## Sonuç

Artık Java'da Aspose.Cells kullanarak **aralıktan PNG oluşturmayı**, etkili bir şekilde **verileri PNG olarak dışa aktarmayı** ve **excel aralık görüntüsünü kaydetmeyi** biliyorsunuz. Bu adımlar—çalışma kitabını yükleme, aralığı tanımlama, görüntü seçeneklerini yapılandırma, baskı alanını ayarlama ve dosyayı kaydetme—**çalışma sayfasını PNG'ye dönüştürme** ve **hücreleri PNG olarak kaydetme** için tüm iş akışını kapsar.

### Sonraki adımlar

* Kalite ve dosya boyutunu dengelemek için farklı `Resolution` değerleriyle deney yapın.
* Şeffaf arka planlı bir PNG'ye ihtiyacınız varsa `ImageOrPrintOptions.setTransparent(true)` kullanın.
* Çok sayfalı raporlar için birden fazla aralık görüntüsünü `PdfSaveOptions` ile tek bir PDF'e birleştirin.
* `setSaveFormat` değiştirerek diğer raster formatlara (JPEG, BMP) dışa aktarmayı keşfedin.

Bu deseni grafiklere, tablolara veya tüm çalışma sayfalarına uyarlamaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells Java Kullanarak Excel Çalışma Sayfasını PNG Olarak Dışa Aktarma](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Aspose.Cells for Java Kullanarak Excel'i PNG'ye Dönüştürme: Adım Adım Kılavuz](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Aspose.Cells Java Kullanarak Excel'de Birleşik Aralık Oluşturma: Kapsamlı Rehber](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}