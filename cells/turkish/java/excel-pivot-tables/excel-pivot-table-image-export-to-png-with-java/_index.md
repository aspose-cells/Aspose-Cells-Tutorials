---
category: general
date: 2026-07-03
description: Java kullanarak bir Excel pivot tablo görüntüsünü dışa aktarın. Aspose.Cells
  ile adım adım PNG görüntü formatını nasıl ayarlayacağınızı öğrenin.
draft: false
keywords:
- excel pivot table image
- set image format png
- Aspose.Cells export
- Java Excel automation
- pivot table to image
language: tr
og_description: Java’da Excel pivot tablo görüntü dışa aktarımı açıklandı. Bu öğreticiyi
  izleyerek görüntü formatını PNG olarak hızlı ve güvenilir bir şekilde ayarlayın.
og_title: excel pivot tablo resmi – PNG dışa aktarımı için Java rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Export an excel pivot table image using Java. Learn how to set image
    format png with Aspose.Cells step‑by‑step.
  headline: 'excel pivot table image: Export to PNG with Java'
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel
- ImageExport
title: 'excel pivot tablo görüntüsü: Java ile PNG olarak dışa aktar'
url: /tr/java/excel-pivot-tables/excel-pivot-table-image-export-to-png-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel pivot table image – Java’da Pivot Tablosunu PNG Olarak Dışa Aktarma

Hiç **excel pivot table image**’ı paylaşılabilir bir PNG’ye dönüştürmek istediniz ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz. Birçok raporlama sürecinde pivot tablo yıldızdır, ancak ekip sadece sabit bir görsel ister. İyi haber? Birkaç satır Java ve Aspose.Cells kodu ile **set image format png** yapabilir ve tam ihtiyacınız olanı elde edebilirsiniz.

Bu rehberde, bir çalışma kitabını yükleme, ilk pivot tabloyu yakalama, dışa aktarma seçeneklerini yapılandırma ve sonunda net bir PNG dosyasını diske yazma sürecini adım adım inceleyeceğiz. Sonunda, herhangi bir Java projesine ekleyebileceğiniz yeniden kullanılabilir bir kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- Dosya sisteminden bir Excel çalışma kitabını nasıl yüklersiniz.
- Bir çalışma sayfasında belirli bir pivot tabloyu nasıl bulursunuz.
- Dışa aktarılan görsel için **set image format png** işleminin tam adımları.
- Yaygın tuzaklar (birden çok pivot tablo, büyük veri setleri) ve bunlardan nasıl kaçınılır.
- Kopyala‑yapıştır yapabileceğiniz hazır bir Java sınıfı.

### Önkoşullar

- Java 8 veya daha yeni bir sürüm yüklü.
- Aspose.Cells for Java kütüphanesi (2026‑07‑03 tarihi itibarıyla en son sürüm).
- En az bir pivot tablo içeren bir Excel dosyası (`input.xlsx`).
- Bağımlılık yönetimi için Maven ya da Gradle hakkında temel bilgi.

---

## Adım 1: Aspose.Cells’i Projenize Ekleyin

İlk iş, Aspose.Cells JAR dosyasının sınıf yolunuzda olduğundan emin olmaktır. Maven kullanıyorsanız, aşağıdakini `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest at time of writing -->
</dependency>
```

Gradle için ise aynı şekilde basittir:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **İpucu:** Aspose ücretsiz 30‑günlük bir değerlendirme anahtarı sunar. Sitelerinden kaydolun, ardından programınızın başına `License.setLicense("Aspose.Cells.lic");` ekleyerek tam özellikleri açın.

## Adım 2: Çalışma Kitabını Yükleyin ve Pivot Tabloya Erişin

Şimdi Excel dosyasını açıp ilk pivot tabloyu alacağız. Aşağıdaki kod tam olarak bunu yapar ve savunmacı bir yaklaşımla—çalışma kitabında sayfa yoksa ya da sayfada pivot tablo bulunmuyorsa net bir istisna fırlatır.

```java
import com.aspose.cells.*;

import java.io.File;

public class PivotTableToPng {

    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load the workbook from disk
            Workbook wb = new Workbook(inputPath);

            // Ensure there is at least one worksheet
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("The workbook contains no worksheets.");
            }

            // Grab the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // Verify that the worksheet actually has a pivot table
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables found on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // -------------------------------------------------
            // Step 3: Configure image export options (PNG)
            // -------------------------------------------------
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            // This is where we **set image format png**
            imgOpt.setImageFormat(ImageFormat.PNG);
            // Optional: increase the DPI for sharper output (default is 96)
            imgOpt.setResolution(300);

            // -------------------------------------------------
            // Step 4: Export the pivot table as an image file
            // -------------------------------------------------
            pt.toImage(outputPath, imgOpt);

            System.out.println("Successfully exported the excel pivot table image to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### Bu Adımlar Neden Önemli

- **Çalışma kitabını yüklemek**, alt yapı veri yapılarına erişim sağlar; Aspose.Cells düşük‑seviye OpenXML ayrıştırmasını soyutlar.
- **Çalışma sayfasına erişmek**, pivot tabloların belirli bir sayfaya bağlı olması nedeniyle gereklidir. Birden çok sayfanız varsa `wb.getWorksheets()` üzerinden döngü kurarak istenen tabloyu içeren sayfayı seçebilirsiniz.
- **Pivot tabloyu almak**, işlemin kalbidir. `ws.getPivotTables().get(0)` ilk tabloyu getirir, ancak `ws.getPivotTables().get("MyPivot")` ile isimle de arayabilirsiniz.
- **Setting image format png** (ikincil anahtar kelime) Aspose.Cells’in çıktıyı kayıpsız bir PNG olarak oluşturmasını söyler. Bu format keskin çizgileri ve metni korur, raporlar için idealdir.
- **`toImage` ile dışa aktarmak**, dosyayı tek bir çağrıda yazar, sayfalama ve ölçeklendirmeyi otomatik olarak halleder.

## Adım 3: Çıktıyı Doğrulayın

Programı çalıştırdıktan sonra `YOUR_DIRECTORY` konumuna gidin; `pivot.png` dosyasını görmelisiniz. Herhangi bir görüntü görüntüleyicide açın—Excel’de gördüğünüz net ızgara çizgileri ve tam yerleşimi fark edeceksiniz. Görsel bulanıksa, `imgOpt.setResolution()` ile DPI değerini artırın; 300‑600 arası baskı kalitesi için iyi çalışır.

![excel pivot table image exported as PNG](excel-pivot-table-image.png "excel pivot table image exported as PNG")

*Image alt text:* **excel pivot table image exported as PNG**

## Birden Çok Pivot Tabloyla Çalışma

Sayfanızda birden fazla pivot tablo varsa ne yaparsınız? Yukarıdaki kod ilk tabloyu alır, ancak döngü kurabilirsiniz:

```java
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    String outFile = "YOUR_DIRECTORY/pivot_" + i + ".png";
    pt.toImage(outFile, imgOpt);
}
```

Bu döngü `pivot_0.png`, `pivot_1.png` vb. dosyaları üretir; her biri farklı bir pivot tabloyu temsil eder. Döngüden önce **set image format png**’i bir kez ayarlamayı unutmayın; aynı `ImageOrPrintOptions` örneği yeniden kullanılabilir.

## Kenar Durumları & İpuçları

| Durum | Dikkat Edilmesi Gereken | Önerilen Çözüm |
|-----------|-------------------|---------------|
| **Büyük pivot (çok satır/sütun)** | PNG dosyası çok büyük olabilir, bellek baskısına yol açar. | `imgOpt.setOnePagePerSheet(false)` ile birden çok sayfaya bölün veya DPI değerini düşürün. |
| **Gizli satır/sütun** | Aspose görünürlüğü korur; gizli veriler görünmez. | `ws.showRows(start, count, true)` ile programatik olarak gösterin. |
| **Özel stiller (yazı tipleri, renkler)** | Sunucuda yüklü olmayan kurumsal fontlar renderlanmayabilir. | JVM içine font ekleyin veya `imgOpt.setFontEmbeddingMode(FontEmbeddingMode.EMBED_ALL)` ile sistem fontlarına geri dönün. |
| **Daha sonra farklı çıktı formatı gerekirse** | JPEG veya BMP gibi bir format isteyebilirsiniz. | `imgOpt.setImageFormat(ImageFormat.JPEG)` ile değiştirin—kod aynı kalır, sadece enum değeri farklıdır. |

## Tam Çalışan Örnek (Kopyala‑Yapıştır)

Aşağıda, derlenmeye hazır bütün sınıf yer alıyor. `PivotTableToPng.java` dosyasına yapıştırın, yolları ayarlayın ve `javac PivotTableToPng.java && java PivotTableToPng` komutlarıyla çalıştırın.

```java
import com.aspose.cells.*;

public class PivotTableToPng {

    public static void main(String[] args) {
        // ----- Configuration -----
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/pivot.png";

        try {
            // Load workbook
            Workbook wb = new Workbook(inputPath);

            // Guard clauses
            if (wb.getWorksheets().getCount() == 0) {
                throw new IllegalStateException("Workbook has no worksheets.");
            }

            Worksheet ws = wb.getWorksheets().get(0);
            if (ws.getPivotTables().getCount() == 0) {
                throw new IllegalStateException("No pivot tables on the first worksheet.");
            }

            // Retrieve the first pivot table
            PivotTable pt = ws.getPivotTables().get(0);

            // ----- Set image format png -----
            ImageOrPrintOptions imgOpt = new ImageOrPrintOptions();
            imgOpt.setImageFormat(ImageFormat.PNG);   // <-- key line
            imgOpt.setResolution(300);                // optional, for sharper output

            // Export to PNG
            pt.toImage(outputPath, imgOpt);

            System.out.println("excel pivot table image exported successfully: " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error during export:");
            ex.printStackTrace();
        }
    }
}
```

Çalıştırın ve **excel pivot table image**’ı PNG dosyası olarak kaydedilmiş olarak elde edin—tam da öğreticinin vaat ettiği gibi.

---

## Sonuç

Java kullanarak **excel pivot table image** dışa aktarmak için gereken her şeyi, Aspose.Cells ile **set image format png** nasıl yapılır sorusunun yanıtını ele aldık. Çalışma kitabını yüklemekten kenar durumlarını yönetmeye kadar çözüm kompakt, güvenilir ve üretime hazır.

Sırada ne var? Birden çok pivot tabloyu toplu olarak dışa aktarın, baskı kalitesi için farklı DPI ayarları deneyin ya da web‑optimizasyonu için JPEG formatına geçin. PNG’yi bir PDF raporuna gömmeyi de keşfedebilirsiniz—Aspose.PDF bunu çok kolay hâle getirir.

İş akışınızda bir değişiklik ya da takıldığınız bir nokta mı var? Yorum bırakın, birlikte çözümleyelim. Mutlu kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak ilgili konuları kapsar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Update Excel Pivot Table Source with Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}