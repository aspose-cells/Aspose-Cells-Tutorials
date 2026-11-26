---
category: general
date: 2026-11-25
description: Aspose.Cells ile Java’da Excel’i SVG’ye dışa aktar – Excel’i SVG olarak
  kaydetmek ve bir vektör görüntüsü oluşturmak için adım adım kılavuz.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: tr
lastmod: 2026-11-25
og_description: Aspose.Cells ile Java’da Excel’i SVG’ye dışa aktarın. Excel’i SVG
  olarak kaydetmeyi ve birkaç satır kodla yüksek kaliteli vektör görüntüler oluşturmayı
  öğrenin.
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: Java’da Excel’i SVG’ye Dışa Aktarma – tam Aspose.Cells öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Java'da Aspose.Cells ile Excel'i SVG'ye dışa aktarma
url: /tr/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for Java kullanarak Excel'i SVG olarak dışa aktarma

Eğer **Excel'i SVG olarak dışa aktarmanız** gerekiyorsa, bu rehber Aspose.Cells for Java ile bunu nasıl yapacağınızı gösterir. **Excel'i SVG olarak kaydetmeyi** ve sadece birkaç satır kodla yüksek kaliteli bir **vektör görüntüsü** oluşturmayı öğreneceksiniz.

Excel çalışma kitabını bir SVG dosyasına dışa aktarmak, sayfayı web sayfalarına, raporlara veya ölçeklenebilir grafikleri tercih eden herhangi bir ortama yerleştirmenizi sağlar. SVG formatı, raster görüntülerde oluşan pikselleşme olmadan yazı tiplerini, renkleri ve hücre kenarlıklarını korur.

## Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

* Java 17 veya daha yeni bir sürüm yüklü.
* Aktif bir Aspose.Cells for Java lisansı (veya geçici bir değerlendirme anahtarı).
* Aspose.Cells bağımlılığını ekleyebileceğiniz bir Maven veya Gradle projesi.

Aspose.Cells kütüphanesini projenize ekleyin:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Excel'i SVG olarak dışa aktarma – adım adım

İşlem üç basit adımdan oluşur: çalışma kitabını yükleme, SVG dışa aktarma seçeneklerini yapılandırma ve sonucu kaydetme. Her adım aşağıda açıklanmıştır.

### Adım 1: Verileri içeren çalışma kitabını yükleyin

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Neden önemli:**  
`Workbook`, Aspose.Cells içinde merkezi nesnedir. Dosyayı bir kez yüklemek, tüm çalışma sayfalarına, stillere ve gömülü nesnelere erişim sağlar; SVG dışa aktarıcısı daha sonra bunları işler.

### Adım 2: SVG için görüntü dışa aktarma seçeneklerini ayarlayın

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Neden önemli:**  
`ImageOrPrintOptions`, çıktı formatını kontrol etmenizi sağlar. `ImageFormat.SVG` seçildiğinde sonuç **vektör görüntüsü** olur, bitmap değil. `OnePagePerSheet` etkinleştirildiğinde bir sayfa içinde sayfa sonları oluşmaz; bu, SVG'nin bir web görünümünde gösterileceği durumlarda genellikle istenen davranıştır.

### Adım 3: Çalışma kitabını SVG dosyası olarak kaydedin

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Neden önemli:**  
`save` yöntemi, yüklenmiş çalışma kitabını yapılandırılmış `exportOptions` ile birleştirir. Bu çağrı, tarayıcılarda, Inkscape'de veya herhangi bir vektör‑uyumlu editörde açılabilecek tam uyumlu bir SVG dosyası yazar.

## Tam çalıştırılabilir örnek

Üç adımı birleştirerek, hemen derleyip çalıştırabileceğiniz bağımsız bir program elde edersiniz:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Beklenen çıktı**

Programı çalıştırdığınızda şu çıktı alınır:

```
Export complete: Excel saved as SVG.
```

`C:/Output` içinde `WithVariationSelectors.svg` dosyasını bulacaksınız. Dosyayı bir tarayıcıda açtığınızda çalışma sayfası ölçeklenebilir grafikler olarak, metin, kenarlıklar ve hücre renkleri korunmuş şekilde görüntülenir.

## Yaygın varyasyonlar ve uç durumlar

| Durum | Önerilen ayarlama |
|-----------|------------------------|
| **Multiple worksheets** | `workbook.getWorksheets()` üzerinden döngü yapın ve her sayfa için `save` çağırın, isteğe bağlı olarak dosya adına sayfa adını ekleyin. |
| **Large workbooks** | `exportOptions.setRenderThreadCount(int)` değerini artırarak paralel işleme izin verin, dönüşüm süresini azaltın. |
| **Custom DPI** | `exportOptions.setHorizontalResolution(int)` ve `exportOptions.setVerticalResolution(int)` çağırarak SVG’nin viewBox ölçeklendirmesini kontrol edin. |
| **Embedding fonts** | `exportOptions.setExportFontAsSVG(true)` ayarını yaparak font tanımlarını doğrudan SVG’ye gömün; bu, orijinal fontlar yüklü olmayan makinelerde görsel tutarlılığı garanti eder. |
| **Password‑protected files** | Yükleme sırasında şifreyi sağlayın: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Profesyonel ipuçları

* **Raster geri dönüşümünden kaçının** – Çalışma sayfası karmaşık grafikler içeriyorsa, SVG içinde vektör öğeleri olarak göründüklerinden emin olun. Görünmüyorlarsa `exportOptions.setExportChartAsSVG(true)` etkinleştirin.  
* **Performans** – Toplu dönüşümler için her dosya için yeni bir `ImageOrPrintOptions` nesnesi oluşturmak yerine tek bir örnek yeniden kullanın.  
* **Test** – Oluşturulan SVG’yi çevrimiçi bir doğrulayıcı (ör. W3C SVG Validator) ile kontrol edin; hatalı işaretlemeleri erken yakalayın.

## Dönüşümü doğrulama

Çıktı dosyasının gerçekten SVG olduğunu programatik olarak şu şekilde doğrulayabilirsiniz:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

`<svg>` kök öğesinin varlığı, başarılı bir **Excel'i SVG olarak dönüştürme** işlemini gösterir.

## Sonuç

Bu öğreticide, Aspose.Cells for Java kullanarak **Excel'i SVG olarak dışa aktarmayı** gösterdik. Çalışma kitabını yükleyip `ImageOrPrintOptions` ile SVG ayarlarını yapılandırarak ve `save` metodunu çağırarak **Excel'i SVG olarak kaydedebilir** ve temiz bir **Excel'ten vektör görüntüsüne** dönüşüm elde edebilirsiniz. Bundan sonra SVG'yi web sayfalarına yerleştirebilir, dokümantasyona ekleyebilir veya herhangi bir vektör‑grafik aracında daha ileri işlemler yapabilirsiniz. İyi kodlamalar!

### Sonraki keşifler

* **Excel'i PNG veya JPEG olarak dışa aktar** – raster çıktı için `exportOptions.setImageFormat(ImageFormat.PNG)` değiştirin.  
* **Excel'i PDF'ye dönüştür** – yazdırılabilir belgeler için `PdfSaveOptions` kullanın.  
* **Toplu işleme** – Yukarıdaki kodu bir dosya sistemi izleyicisiyle birleştirerek klasöre eklenen her yeni çalışma kitabı için otomatik **Excel'i SVG'ye dönüştür** işlemini gerçekleştirin.

Bu seçeneklerle deneyler yapın ve Aspose.Cells’in esnekliği sayesinde Excel verilerinizi ihtiyacınız olan herhangi bir görsel formata dönüştürün. Mutlu kodlamalar!

## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakın konuları kapsayan tam çalışan kod örnekleri içerir; adım adım açıklamalarla API özelliklerini daha iyi öğrenmenizi ve alternatif uygulama yaklaşımlarını keşfetmenizi sağlar.

- [Aspose.Cells Java kullanarak Excel Grafiklerini SVG olarak dışa aktarma (Scalable Vector Graphics)](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells for Java ile bir Excel Çalışma Kitabını SVG olarak oluşturma ve kaydetme](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel'i SVG olarak dışa aktarma – Adım‑adım Java Rehberi](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}