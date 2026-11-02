---
category: general
date: 2026-10-01
description: Java'da ShapeExportOptions ile şekli nasıl dışa aktaracağınızı öğrenin;
  Aspose.Cells kullanarak PPTX'e dönüştürürken şeklin düzenlenebilir kalmasını sağlayın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: tr
lastmod: 2026-10-01
og_description: Java'da ShapeExportOptions ile şekli dışa aktararak düzenlenebilir
  PPTX dosyaları oluşturun. Bu öğretici, Aspose.Cells kullanarak sürecin tamamını
  adım adım gösterir.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Java'da ShapeExportOptions ile şekil dışa aktarma – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Java'da ShapeExportOptions ile şekli nasıl dışa aktarılır
url: /tr/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da ShapeExportOptions ile şekil dışa aktarma

Eğer bir Excel çalışma kitabından **ShapeExportOptions ile şekil dışa aktarma** ihtiyacınız varsa, bu kılavuz tam adımları gösterir. Şekli PPTX dosyasına dönüştürürken düzenlenebilir kalmasını nasıl sağlayacağınızı göreceksiniz; bu, PowerPoint'te sonraki düzenlemeler için çok önemlidir.

Şekilleri dışa aktarmak, elektronik tablolardan slayt desteleri oluştururken yaygın bir görevdir—satış sunumları, raporlama panoları veya otomatik sunumlar oluşturuyor olun. Bu öğretici, proje kurulumundan dışa aktarılan dosyanın doğrulanmasına kadar ihtiyacınız olan her şeyi kapsar ve **Aspose.Cells for Java** kütüphanesini kullanır.

## Gerekenler

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- Java 17 veya daha yeni bir sürüm (kod, herhangi bir güncel JDK ile derlenir)
- Bağımlılık yönetimi için Maven veya Gradle
- En az bir metin kutusu veya başka bir şekil içeren bir Excel dosyası (`Shapes.xlsx`)
- Aspose.Cells API'lerine temel aşinalık

## Adım 1: Aspose.Cells'i projenize ekleyin (Aspose Cells export shape)

Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Gradle için, bu satırı `build.gradle` dosyanıza yerleştirin:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **İpucu:** Değerlendirme su işaretlerini önlemek için lisansınızı erken kaydedin.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Adım 2: Şekli içeren çalışma kitabını yükleyin

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

`Workbook` nesnesi, tüm Excel dosyasını temsil eder. Onu yüklemek, herhangi bir şekil manipülasyonu için ilk ön koşuldur.

## Adım 3: Çalışma sayfasına erişin ve istenen şekli alın (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Neden önemli:** Şekiller çalışma sayfasına göre depolanır, bu yüzden belirli bir şekli dışa aktarabilmek için doğru sayfaya gitmeniz gerekir.

## Adım 4: **ShapeExportOptions**'ı düzenlenebilir tutacak şekilde yapılandırın (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

`ExportAsEditable` özelliğini `true` olarak ayarlamak, Aspose.Cells'in şeklin vektör verilerini korumasını sağlar; böylece PowerPoint kullanıcıları içe aktarıldıktan sonra şekli değiştirebilir.

## Adım 5: Şekli doğrudan bir PPTX dosyasına dışa aktarın (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

`exportToImage` yöntemi çeşitli görüntü formatları için çalışır; hedef dosya adı `.pptx` ile bittiğinde, Aspose.Cells şekli içeren bir PowerPoint slaytı yazar.

### Beklenen sonuç

- Belirtilen dizinde `textbox.pptx` dosyası oluşur.
- PowerPoint'te dosyayı açtığınızda, orijinal metin kutusunu içeren tek bir slayt gösterilir.
- Metin kutusu tamamen düzenlenebilir (metni, yazı tipini, boyutu vb. değiştirebilirsiniz).

## Adım 6: Çıktıyı doğrulayın ve yaygın kenar durumlarını ele alın

### Programatik olarak doğrulama

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

`slideCount` değeri `1` ise dışa aktarma başarılı demektir.

### Kenar durumu: Birden fazla şekil

Çalışma sayfasında birden fazla şekil varsa ve sadece belirli bir tanesini istiyorsanız, adıyla bulun:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Kenar durumu: Şekil bulunamadı

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Kenar durumu: Diğer formatlara dışa aktarma

`ShapeExportOptions` ayrıca PNG, JPEG, SVG ve EMF formatlarını da destekler. Dosya uzantısını değiştirin ve isteğe bağlı olarak `exportOptions.setImageFormat(ImageFormat.PNG)` ayarlayın.

## Tam, çalıştırılabilir örnek

Tüm parçaları bir araya getirdiğinizde, IDE'nize kopyalayıp yapıştırabileceğiniz bağımsız bir program elde edersiniz:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

Programı çalıştırdığınızda `textbox.pptx` oluşturulur. PowerPoint'te açın, metin kutusuna sağ tıklayın; düzenleme tutamaçlarını göreceksiniz—bu da **ShapeExportOptions ile şekil dışa aktarma** işleminin düzenlenebilirliği koruduğunu doğrular.

## Sıkça Sorulan Sorular

| Soru | Cevap |
|----------|--------|
| *Bir grafik şekli dışa aktarabilir miyim?* | Evet. Aynı `exportToImage` çağrısı grafikler, resimler ve SmartArt için de çalışır. |
| *Daha yüksek çözünürlüklü PNG istersem?* | Dışa aktarmadan önce `options.setImageFormat(ImageFormat.PNG)` ve `options.setResolution(300)` ayarlarını yapın. |
| *Dışa aktarılan PPTX eski PowerPoint sürümleriyle uyumlu mu?* | Kütüphane Office Open XML (PPTX) yazar; bu format PowerPoint 2007 ve sonrası tarafından desteklenir. |
| *Bunun çalışması için lisansa ihtiyacım var mı?* | Ücretsiz değerlendirme sürümü çalışır ancak bir su işareti ekler. Su işaretini kaldırmak için lisans kaydedin. |

## Sonraki adımlar

- Birden fazla dışa aktarılan şekli tek bir slayt destesine birleştirmeniz gerekiyorsa **Aspose.Slides for Java**'yı keşfedin.
- Daha hızlı render için raster görüntü (PNG/JPEG) tercih ediyorsanız **ShapeExportOptions.setExportAsEditable(false)** kullanın.
- Toplu işleme otomasyonu: Tüm çalışma sayfalarını döngüye alıp her şekli ayrı PPTX dosyalarına dışa aktarın.

---

### Sonuç

Artık Java'da **ShapeExportOptions ile şekil dışa aktarma** yöntemini biliyorsunuz; bir metin kutusunu (veya başka bir şekli) PPTX dosyasına dönüştürürken düzenlenebilirliği koruyabilirsiniz. Yukarıdaki adımları—kütüphaneyi kurma, çalışma kitabını yükleme, `ShapeExportOptions` yapılandırma ve `exportToImage` çağrısı—takip ederek şekil dışa aktarmayı herhangi bir otomatik raporlama sürecine entegre edebilirsiniz.

Farklı şekiller, çıktı formatları ve çözünürlük ayarlarıyla denemeler yapın. Bu kılavuzu faydalı bulduysanız, ekip arkadaşlarınızla paylaşın veya gelecekteki referans için yer işareti koyun. Kodlamanın tadını çıkarın!

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [How to Adjust Shape Margins in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [How to Apply 3D Shape Formatting in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java Workbook Shape Copying Guide](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}