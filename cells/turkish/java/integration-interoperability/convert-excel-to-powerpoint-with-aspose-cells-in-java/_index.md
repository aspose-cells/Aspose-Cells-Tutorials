---
category: general
date: 2026-09-21
description: Aspose.Cells ile Java'da Excel'i PowerPoint'e dönüştürün – grafiği PPTX'e
  nasıl dışa aktaracağınızı ve çalışma kitabını sadece birkaç satır kodla PPTX olarak
  nasıl kaydedeceğinizi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: tr
lastmod: 2026-09-21
og_description: Java'da Aspose.Cells kullanarak Excel'i PowerPoint'e dönüştürün. Bu
  öğreticide bir grafiği PPTX olarak dışa aktarma ve çalışma kitabını düzenlenebilir
  metin kutuları içeren PPTX olarak kaydetme gösterilmektedir.
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: Aspose.Cells ile Excel'i PowerPoint'e Dönüştür – Java Rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: Java'da Aspose.Cells ile Excel'i PowerPoint'e Dönüştür
url: /tr/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i PowerPoint'e Aspose.Cells ile Java'da Dönüştürme

Eğer **Excel'i PowerPoint'e dönüştürmeniz** gerekiyorsa, bu kılavuz bunu yapmanın özlü ve üretim‑hazır bir yolunu gösterir. Bir grafiği PPTX olarak dışa aktarmayı, metin kutularını düzenlenebilir tutmayı ve **çalışma kitabını PPTX olarak kaydetmeyi** sadece üç satır Java kodu ile göreceksiniz.

Birçok geliştirici verileri PDF'ye dışa aktarır, ancak PowerPoint, canlı grafikler ve düzenlenebilir öğeler gerektiren sunumlar için genellikle daha uygundur. Bu eğitim, proje kurulumundan yaygın hataların ele alınmasına kadar ihtiyacınız olan her şeyi kapsar— böylece Java IDE'nizden çıkmadan bir Excel grafiğinden PowerPoint oluşturabilirsiniz.

## Önkoşullar

* Java 17 veya daha yeni bir sürüm yüklü.
* Bağımlılıkları yönetmek için Maven (veya Gradle).
* Aspose.Cells for Java lisansı (ücretsiz deneme değerlendirme için çalışır).
* En az bir grafik ve bir metin kutusu içeren bir Excel dosyası (`ChartAndTextbox.xlsx`).

## Adım 1: Aspose.Cells'i projenize ekleyin

İlk adım, Aspose.Cells kütüphanesini projeye eklemektir. Maven kullanıyorsanız, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Gradle kullanıyorsanız eşdeğeri şudur:
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

Kütüphaneyi eklemek, dönüşüm için gerekli olan `Workbook`, `PdfSaveOptions` ve `SaveFormat` enum'ına erişmenizi sağlar.

## Adım 2: Grafik ve metin kutusunu içeren çalışma kitabını yükleyin

Şimdi Excel dosyasını yükleyin. `Workbook` sınıfı, tüm çalışma kitabını belleğe okuyarak grafikler, formüller ve metin kutularını korur.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**Neden önemli:** Çalışma kitabını önce yüklemek, tüm gömülü nesnelerin (grafikler, görüntüler, metin kutuları) dışa aktarma sürecinde mevcut olmasını sağlar. Dosya bulunamazsa, Aspose.Cells net bir `FileNotFoundException` fırlatır; bunu yakalayarak daha iyi bir kullanıcı deneyimi sağlayabilirsiniz.

## Adım 3: Metin kutularının düzenlenebilir kalmasını sağlamak için dışa aktarma seçeneklerini yapılandırın

Aspose.Cells, hedef format PowerPoint olduğunda nesnelerin nasıl yazılacağını kontrol etmek için `PdfSaveOptions` kullanır. `setExportEditableTextBoxes(true)` özelliğini etkinleştirerek, Excel sayfasındaki tüm metin kutuları dönüşüm sonrası düzenlenebilir kalır.

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **Neden PPTX için `PdfSaveOptions` kullanılır?**  
> İçeride, Aspose.Cells PDF renderleme hattını PowerPoint çıktısı için yeniden kullanır ve düzenlenebilir öğeler üzerinde ayrıntılı kontrol sağlar. Bu bayrağı ayarlamak, metin kutusu düzenlenebilirliğini korumanın önerilen yoludur.

## Adım 4: Çalışma kitabını PowerPoint sunumu olarak kaydedin

Son olarak, `workbook.save` metodunu `SaveFormat.PPTX` ile çağırın. Bu adım **Excel grafiğinden PowerPoint oluşturma** iş akışını tamamlar.

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

Hepsini bir araya getirdiğimizde, tam program şu şekildedir:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### Beklenen çıktı

Programı çalıştırdığınızda şu çıktı verir:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

`Result.pptx` dosyasını Microsoft PowerPoint'te açtığınızda şunları göreceksiniz:

* Orijinal Excel grafiği, yerel bir PowerPoint grafiği olarak render edilir (PowerPoint'in grafik düzenleyicisinde düzenlenebilir).
* Excel'den gelen metin kutusu, düzenlenebilir bir şekil olarak görünür ve metnini doğrudan slaytta değiştirebilmenizi sağlar.

## Yaygın kenar durumlarını ele alma

| Durum | Önerilen yaklaşım |
|-----------|----------------------|
| **Dosya bulunamadı** | `Workbook` yapıcısını bir `try‑catch` bloğuna sarın ve net bir mesaj gösterin. |
| **Çalışma kitabında grafik yok** | Dönüştürmeden önce sayfanın bir grafik içerdiğini (`worksheet.getCharts().getCount() > 0`) doğrulayın; aksi takdirde adımı atlayın veya bir yer tutucu ekleyin. |
| **Büyük Excel dosyaları** | Render sırasında `OutOfMemoryError` oluşmasını önlemek için JVM yığın boyutunu (`-Xmx2g`) artırın. |
| **Lisans ayarlanmamış** | Değerlendirme filigranını kaldırmak için çalışma kitabını yüklemeden önce `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` çağrısını yapın. |

## Sıkça Sorulan Sorular

**S: Birden fazla çalışma sayfasını ayrı PowerPoint slaytlarına dönüştürebilir miyim?**  
C: Evet. Her çalışma sayfası üzerinde döngü kurarak, grafiğini `PdfSaveOptions` ile yeni bir slayta dışa aktarın ve tüm sayfalar işlendiğinde çalışma kitabını bir kez kaydedin.

**S: Bu yöntem hücre biçimlendirmesini korur mu?**  
C: Yalnızca grafik ve metin kutusu nesneleri PowerPoint'e aktarılır. Hücre biçimlendirmesi Excel dosyasında kalır; PPTX içinde görünmez.

**S: PPTX yerine PDF olarak dışa aktarmam gerekirse ne yapmalıyım?**  
C: `SaveFormat.PDF` ve aynı `PdfSaveOptions` kullanın. `setExportEditableTextBoxes` bayrağı PDF için de çalışır.

## Sonraki Adımlar

Artık **çalışma kitabını PPTX olarak kaydetmeyi** ve **grafiği PPTX olarak dışa aktarmayı** bildiğinize göre, şunları keşfedebilirsiniz:

* Farklı slaytlara birden fazla grafik eklemek (`create powerpoint from excel chart` döngüsüyle).
* Daha zengin sunum stili için Aspose.Slides for Java kullanarak slayt düzenlerini özelleştirmek.
* `Picture` sınıfını kullanarak Excel hücrelerindeki görüntüleri PowerPoint'e gömmek.

Bu uzantılar, Excel verilerinden doğrudan şık sunumlar üreten tam otomatik raporlama hatları oluşturmanızı sağlar.

---

**Özet:** Bu eğitim, Aspose.Cells for Java kullanarak **Excel'i PowerPoint'e dönüştürmenin** güvenilir bir yolunu gösterdi. Çalışma kitabını yükleyerek, metin kutularının düzenlenebilir kalmasını sağlamak için `PdfSaveOptions` yapılandırarak ve `SaveFormat.PPTX` ile kaydederek, canlı grafikler ve düzenlenebilir şekiller içeren bir PowerPoint dosyası elde edersiniz—dinamik iş sunumları için mükemmel. Kodu toplu işleme uyarlamaktan veya daha büyük raporlama çözümlerine entegre etmekten çekinmeyin.

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki eğitimler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java kullanarak Trendline ile Excel Grafiği Oluşturma ve Görüntü Olarak Dışa Aktarma](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells ile Java'da Excel Grafiklerini SVG'ye Dönüştürme](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells&#58; Java'da Excel'i PDF'ye Dönüştürme — Adım Adım Kılavuz](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}