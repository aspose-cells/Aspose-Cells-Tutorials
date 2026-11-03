---
category: general
date: 2026-10-10
description: Aspose.Cells kullanarak Java’da Excel aralığını görüntü olarak dışa aktarmayı
  öğrenin. Kılavuz ayrıca seçili hücreleri görüntü olarak dışa aktarmayı ve Excel
  çalışma sayfasını resim olarak kaydetmeyi kapsar.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: tr
lastmod: 2026-10-10
og_description: Java’da Excel aralığını resim olarak dışa aktarın; adım adım çözüm.
  Seçili hücreleri resim olarak dışa aktarmayı ve Excel çalışma sayfasını resim olarak
  kaydetmeyi içerir.
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: Java'da Excel aralığını resim olarak dışa aktar – tam Aspose.Cells rehberi
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Java'da Aspose.Cells kullanarak Excel aralığını resim olarak nasıl dışa aktarılır
url: /tr/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Aspose.Cells kullanarak Excel aralığını resim olarak dışa aktarma

Eğer **Excel aralığını resim olarak dışa aktarmanız** gerekiyorsa, bu öğretici Aspose.Cells kütüphanesini kullanarak eksiksiz bir Java çözümünü adım adım gösterir. Ayrıca **seçili hücreleri resim olarak dışa aktarma** ve **Excel çalışma sayfasını resim olarak kaydetme** konularını da öğreneceksiniz.

Bir çalışma kitabının bir bölümünü resim olarak dışa aktarmak, üçüncü‑taraf ekran görüntüsü araçlarına ihtiyaç duymadan piksel‑tam sonuçlar elde etmenizi sağlar. Bu kılavuzun sonunda, PNG (veya desteklenen başka bir format) dosyasını doğrudan diske yazan, PDF, e‑posta veya web sayfalarına eklemek için kullanılabilecek yeniden kullanılabilir bir metoda sahip olacaksınız.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Java 17 veya daha yeni bir sürüm.
* Maven 3.8+ (veya Maven bağımlılıklarını yönetebilen başka bir yapı aracı).
* Aspose.Cells for Java lisansı (ücretsiz deneme sürümü çalışır ancak filigran ekler).
* Bilinen bir dizine yerleştirilmiş örnek bir Excel dosyası (`input.xlsx`).

Aşağıdaki bölümler, temel Java geliştirme ve Maven proje kurulumuna aşina olduğunuzu varsayar.

## Adım 1: Aspose.Cells'i projenize ekleyin

`pom.xml` dosyanıza Aspose.Cells Maven bağımlılığını ekleyin. Bu kütüphane, kod örneğinde kullanılan `Workbook`, `Worksheet` ve `ImageOrPrintOptions` sınıflarını sağlar.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro ipucu:** Sürüm numarasını güncel tutun; yeni sürümler format desteği ve performans iyileştirmeleri ekler.

## Adım 2: Bir aralığı dışa aktarmak için yardımcı bir metod oluşturun

Dışa aktarma mantığını bir metod içinde kapsüllemek, projeler arasında yeniden kullanımı kolaylaştırır ve birleştirilmiş hücreler ya da gizli satırlar gibi kenar durumlarını ele almayı basitleştirir.

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Bu metod neden önemlidir

* **Sorumlulukların ayrılması:** Yükleme, seçenek yapılandırması ve dışa aktarma net bir şekilde ayrılmıştır.
* **Esneklik:** Görüntü formatını veya DPI değerini, temel mantığı değiştirmeden değiştirebilirsiniz.
* **Hata yönetimi:** `Exception` fırlatmak, çağıranın kaydetme, yeniden deneme veya iptal etme kararını vermesine olanak tanır.

## Adım 3: Metodu gerçek parametrelerle çağırın

Aşağıda, **seçili hücreleri resim olarak dışa aktarma** ve aynı zamanda **Excel çalışma sayfasını resim olarak kaydetme** işlemini tam sayfa aralığını kullanarak gösteren minimal bir `main` metodu yer almaktadır.

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Beklenen çıktı

Program çalıştırıldığında iki adet PNG dosyası oluşturulur:

* `range.png` – yalnızca **A1:G20** hücrelerini içeren bir resim.
* `full_sheet.png` – ilk çalışma sayfasının kullanılan tüm alanının resmi, dolayısıyla **Excel çalışma sayfasını resim olarak kaydetme** işleminin bir örneği.

Dosyaları herhangi bir görüntü görüntüleyiciyle açarak, görsel düzenin Excel görünümüyle (hücre kenarlıkları, renkler ve birleştirilmiş hücreler dahil) eşleştiğini doğrulayabilirsiniz.

## Adım 4: Yaygın kenar durumlarını ele alın

### 1. Birleştirilmiş hücreler

Aspose.Cells birleştirilmiş hücre görünümünü otomatik olarak korur, ancak renderlamayı kontrol etmek isterseniz `options.setOnePagePerSheet(true)` ayarını kullanarak tüm sayfayı tek bir sayfaya zorlayabilirsiniz.

### 2. Gizli satırlar veya sütunlar

Varsayılan olarak gizli satır/sütunlar renderlanmaz. Bunları dahil etmek için şu ayarı etkinleştirin:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Büyük aralıklar ve bellek tüketimi

Çok büyük aralıkların dışa aktarılması önemli bellek tüketimine yol açabilir. `OutOfMemoryError` alırsanız şu yöntemleri değerlendirin:

* DPI değerini düşürün (`options.setHorizontalResolution(150)`).
* Aralığı daha küçük parçalara bölerek dışa aktarın ve görüntüleri bir grafik kütüphanesiyle birleştirin.

## Adım 5: Sonucu programatik olarak doğrulayın (isteğe bağlı)

Aşağı akışta, görüntünün doğru oluşturulup oluşturulmadığını kontrol etmek için PNG'yi `javax.imageio.ImageIO` ile yükleyip boyutlarını inceleyebilirsiniz:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

Sıfırdan farklı bir genişlik ve yükseklik, başarılı bir dışa aktarımı gösterir.

## Sonuç

Artık Java’da **Excel aralığını resim olarak dışa aktarma**, **seçili hücreleri resim olarak dışa aktarma** ve **Excel çalışma sayfasını resim olarak kaydetme** konularını Aspose.Cells kullanarak nasıl yapacağınızı biliyorsunuz. Yeniden kullanılabilir `exportRangeAsImage` metodu karmaşıklığı soyutlar, görüntü kalitesini kontrol etmenizi sağlar ve herhangi bir çalışma sayfası indeksi ya da hücre aralığıyla çalışır.

İleride keşfedebileceğiniz adımlar:

* Raporlama için PNG'yi Aspose.PDF ile PDF'e dönüştürmek.
* Bir dizindeki birden fazla çalışma kitabını toplu iş olarak işlemek.
* Görüntü dışa aktarımını bir Spring Boot REST uç noktasına entegre ederek istemcilerin talep üzerine resim almasını sağlamak.

Farklı görüntü formatlarını (`ImageFormat.JPEG`, `ImageFormat.BMP`) ve DPI ayarlarını projenizin görsel gereksinimlerine göre deneyin. İyi kodlamalar!


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}