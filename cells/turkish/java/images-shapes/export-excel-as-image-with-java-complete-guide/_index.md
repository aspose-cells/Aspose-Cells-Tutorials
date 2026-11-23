---
category: general
date: 2026-11-22
description: Aspose.Cells kullanarak Java ile Excel'i görüntü olarak dışa aktarın.
  Çalışma sayfasına resim eklemeyi ve Excel'i birkaç adımda PNG dosyası olarak kaydetmeyi
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: tr
lastmod: 2026-11-22
og_description: Aspose.Cells kullanarak Java ile Excel'i resim olarak dışa aktarın.
  Bu kılavuzu izleyerek çalışma sayfasına resim ekleyin ve Excel'i hızlıca PNG dosyası
  olarak kaydedin.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Java ile Excel'i resim olarak dışa aktar – adım adım öğretici
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Java ile Excel'i Görüntü Olarak Dışa Aktarma – Tam Kılavuz
url: /tr/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Excel’i Görüntü Olarak Dışa Aktarma – tam kılavuz

Bir Java uygulamasında **Excel’i görüntü olarak dışa aktarmanız** gerektiğinde, bu öğretici hazır‑çalıştır çözümü gösterir. Çalışma sayfasına resim eklemeyi, dışa aktarma seçeneklerini yapılandırmayı ve sonunda sadece birkaç satır kodla **Excel’i PNG dosyası olarak kaydetmeyi** öğreneceksiniz.

Kılavuz, Maven kurulumundan kenar durumlarının ele alınmasına kadar her şeyi kapsar; böylece elektronik tablo anlık görüntülerine ihtiyaç duyan herhangi bir projeye tekniği entegre edebilirsiniz.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Java 17 veya daha yeni bir sürüm.
* Bağımlılık yönetimi için Maven 3.6+ (veya Gradle).
* Aspose.Cells for Java lisansı (ücretsiz deneme sürümü test için yeterlidir).
* Dışa aktarmak istediğiniz verileri içeren bir örnek Excel çalışma kitabı (`sample.xlsx`).

## Adım 1: Aspose.Cells bağımlılığını ekleyin

Aspose.Cells, **Excel’i görüntü olarak dışa aktarma** için kullanılan `ImageOrPrintOptions` sınıfını sağlar. Aşağıdaki bağımlılığı `pom.xml` dosyanıza (veya eşdeğer Gradle girdisine) ekleyin.

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Sürüm numarasını güncel tutun; yeni sürümler görüntü işleme performans iyileştirmeleri içerir.

## Adım 2: Çalışma kitabını yükleyin ve çalışma sayfasını seçin

İlk programatik adım, Excel dosyasını açmak ve dışa aktarmak istediğiniz çalışma sayfasına bir referans almaktır.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Bu neden önemlidir*: Çalışma kitabını yüklemek, iç nesnelere erişmenizi sağlar ve doğru çalışma sayfasını seçmek, istenen aralığın işlenmesini garantiler.

## Adım 3: ImageOrPrintOptions’ı yapılandırın (excel’i görüntü olarak dışa aktar)

`ImageOrPrintOptions`, görüntü formatını, çözünürlüğü ve diğer işleme ayrıntılarını kontrol eder. Burada formatı PNG olarak ayarlıyoruz; bu, **excel sayfasını png’ye dışa aktarma** gereksinimini karşılar.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Formatı `PNG` olarak ayarlamak, kayıpsız sıkıştırma sağlar ve dosyanın raporlara ya da diğer iş akışlarına dahil edilmesini kolaylaştırır.

## Adım 4: Çalışma sayfasına resim ekleyin (add picture to worksheet)

Bir logo ya da başka bir aralığın anlık görüntüsü gibi bir resmi gömmek istiyorsanız, `Pictures` koleksiyonunu kullanın. Aşağıdaki kod, `A1:G20` aralığının resmini çalışma sayfasının sol‑üst köşesine ekler.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Neden yapabilirsiniz:** Dışa aktarmadan önce bir resim eklemek, statik grafiklerle çalışma sayfası verilerini birleştirmenizi sağlar ve daha zengin bir son görüntü elde edersiniz.

## Adım 5: Çalışma sayfasını PNG dosyası olarak kaydedin (save excel as png file, save workbook as image)

Son olarak, yapılandırılmış seçeneklerle `Workbook.save` metodunu çağırın. Metot, belirtilen dizine bir PNG dosyası yazar.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

Program tamamlandığında, `output/pivot.png` dosyası, eklediğiniz resim dahil olmak üzere çalışma sayfasının piksel‑tam bir temsilini içerir.

### Tam kaynak dosyası

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

Sınıfı çalıştırdığınızda aşağıdaki PNG dosyası üretilir (görsel örnek amaçlıdır; sizin dosyanız gerçek çalışma sayfası içeriğini yansıtacaktır).

![Excel çalışma sayfası PNG olarak dışa aktarıldı](/images/excel-to-png.png "Java kullanarak excel’i görüntü olarak dışa aktarma sonucu")

*Alt metin (image alt):* **Java kullanarak Excel’i görüntü olarak dışa aktarma sonucu – çalışma sayfasının PNG anlık görüntüsü** (görsel alt gereksinimini karşılar).

## Yaygın hatalar ve nasıl önlenir

| Sorun | Sebep | Çözüm |
|-------|--------|-----|
| **Dosya bulunamadı** | `sample.xlsx` dosyasının yolu hatalı. | Mutlak bir yol kullanın ya da dosyayı proje köküne yerleştirin. |
| **Boş görüntü** | Çalışma sayfasında görünür içerik yok veya resim aralığı boş. | `A1:G20` hücrelerinin veri içerdiğini doğrulayın ya da aralığı değiştirin. |
| **Düşük çözünürlük** | Varsayılan DPI 96, baskıda bulanık görünebilir. | Kaydetmeden önce `opts.setResolution(300)` (veya daha yüksek) çağırın. |
| **Lisans istisnası** | Değerlendirme sürümü su işareti ekleyebilir. | `License license = new License(); license.setLicense("Aspose.Total.lic");` kodu ile geçerli bir Aspose.Cells lisansı uygulayın. |

## Sonraki adımlar

Artık **Excel’i görüntü olarak dışa aktarabildiğinize** göre, aşağıdaki konuları keşfedebilirsiniz:

* **Excel sayfasını png’ye dışa aktar** (her çalışma kitabı sayfası için döngü `wb.getWorksheets()` kullanarak).
* PNG’yi PDF’ye dönüştürmek için Aspose.PDF kullanarak belge‑dostu bir format elde edin.
* Oluşturulan PNG’yi doğrudan Java’dan bir web sayfasına ya da e‑posta ekine gömün.

Bu genişletmeler aynı `ImageOrPrintOptions` desenine dayanır ve kod tabanının tutarlılığını korur.

## Sonuç

Java ile **Excel’i görüntü olarak dışa aktarmayı**, **çalışma sayfasına resim eklemeyi** ve **Excel’i PNG dosyası olarak kaydetmeyi** Aspose.Cells kullanarak öğrendiniz. Tam örnek, **çalışma kitabını görüntü olarak kaydetme**, çözünürlük ayarları ve yaygın hatalardan kaçınma konusunda güvenilir bir yol gösterir. Bu deseni rapor otomasyonu, küçük resim üretimi veya herhangi bir Java‑tabanlı iş akışına elektronik tablo görselleri entegrasyonu için uygulayın.


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Export Excel Workbook As Image Using Aspose Cells For Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}