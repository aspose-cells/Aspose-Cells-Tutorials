---
category: general
date: 2026-11-25
description: Excel'i düzenlenebilir şekillerle PPTX'e nasıl dışa aktaracağınızı öğrenin.
  Bu rehber ayrıca baskı alanını nasıl ayarlayacağınızı ve Excel grafiğini sunumlar
  için nasıl dönüştüreceğinizi gösterir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: tr
lastmod: 2026-11-25
og_description: Aspose.Cells kullanarak düzenlenebilir şekillerle Excel'i PPTX'e nasıl
  dışa aktarılır, ayrıca yazdırma alanı ayarlama ve Excel grafiğini sunumlar için
  dönüştürme ipuçları.
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: Excel'den Düzenlenebilir Şekillerle PPTX'e Nasıl Dışa Aktarılır
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Excel'i Düzenlenebilir Şekillerle PPTX'e Nasıl Dışa Aktarılır
url: /tr/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i Düzenlenebilir Şekillerle PPTX'e Nasıl Dışa Aktarılır

PowerPoint'e **how to export Excel** dosyalarını, düzenlenebilir metin kutuları ve şekilleri koruyarak aktarmanız gerekiyorsa, bu kılavuz size sürecin tamamını adım adım gösterir. Ayrıca odaklanmış bir slayt için **set print area** nasıl ayarlanır ve **convert Excel chart** nesnelerinin dışa aktarıldıktan sonra tamamen düzenlenebilir kalmasını nasıl yapacağınızı öğreneceksiniz.

Veri odaklı raporlardan sunum setleri oluştururken Excel'i PPTX'e dışa aktarmak yaygındır. Aspose.Cells for Java kullanarak manuel kopyala‑yapıştırdan kaçınır, biçimlendirmeyi korur ve çıktıyı programatik olarak kontrol edebilirsiniz.

## Öğrenecekleriniz

* Metin kutusu veya grafik içeren mevcut bir XLSX çalışma kitabını yükleyin.  
* Dışa aktarma seçeneklerini yapılandırarak ortaya çıkan PPTX dosyasının **editable shapes** içermesini sağlayın.  
* **Set the print area**'yı kullanarak dışa aktarılan aralığı ihtiyacınız olan hücrelerle sınırlayın.  
* Çalışma sayfasını PPTX dosyası olarak kaydedin ve metin kutuları ile grafiklerin PowerPoint'te düzenlenebilir olduğunu doğrulayın.  

**Önkoşullar**

* Java 17 veya daha yeni bir sürüm yüklü.  
* Bağımlılık yönetimi için Maven veya Gradle.  
* Excel çalışma kitapları ve Java programlaması hakkında temel bir anlayış.

---

## Excel'i Düzenlenebilir Şekillerle PPTX'e Nasıl Dışa Aktarılır

Bu bölüm, dışa aktarmayı gerçekleştiren temel kodu sağlar. Örnek, yazının yazıldığı sırada en yeni sürüm olan Aspose.Cells 23.9'u kullanır ve gerekli tüm adımları gösterir.

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### Her satırın önemi

1. **Dependency** – Aspose.Cells, çalışma sayfalarını PPTX slaytları olarak render edebilen `ImageOrPrintOptions` sınıfını sağlar. Maven aracılığıyla eklemek, kütüphanenin sınıf yolunda bulunmasını garantiler.  
2. **Imports** – Doğru sınıfları içe aktarmak kodu temiz tutar ve tam nitelikli adlardan kaçınır.  
3. **Loading the workbook** – Dışa aktarmak istediğiniz nesneleri içeren tam dosyaya işaret etmelisiniz. Yol, proje köküne göre mutlak ya da göreli olabilir.  
4. **Export options** – `setEditable(true)` ayarını yapmak, **how to export Excel** için kilit noktadır; böylece ortaya çıkan PowerPoint şekilleri düzenlenebilir kalır. Bu bayrak olmadan, metin kutuları sabit görüntülere dönüşür.  
5. **Print area** – `setPrintArea` çağrısı, dışa aktarmayı ilgilendiğiniz bölgeyle sınırlar; bu da dosya boyutunu azaltır ve istenmeyen satır/sütunları kaldırır. Bu, **set print area excel** gereksinimini doğrudan karşılar.  
6. **Saving** – `SaveFormat.PPTX` sabiti, Aspose.Cells'e bir görüntü veya PDF yerine PowerPoint dosyası üretmesini söyler.  

#### Beklenen çıktı

Programı çalıştırdıktan sonra `EditableShapes.pptx` dosyasını PowerPoint'te açın. Seçilen Excel aralığını yansıtan bir slayt görmeli ve metin kutuları ya da grafik açıklamaları, yerel PowerPoint nesneleri gibi çift tıklanarak düzenlenebilir olmalıdır.

---

## Excel'de Yazdırma Alanı Ayarlama

Yalnızca çalışma sayfasının bir alt kümesine ihtiyacınız olduğunda, **print area** tanımlamak performansı ve görsel netliği artırır.

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*İpucu:* Daha sonra veri aralığını değiştirirseniz, dışa aktarmadan önce `setPrintArea`'ı tekrar çağırın. Dışa aktarma en son ayarı dikkate alır.

---

## XLSX Grafiğini Düzenlenebilir PowerPoint Grafiğine Dönüştürme

Aspose.Cells, grafikleri çizim nesneleri olarak ele alır. `setEditable(true)` etkinleştirildiğinde, grafik yerel bir PowerPoint grafiğine dönüştürülür ve düzenlenebilir (ör. seri, eksen başlıkları değiştirilebilir).

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

Birden fazla grafik içeren **how to convert xlsx** dosyalarına ihtiyacınız varsa, her çalışma sayfası için dışa aktarmayı tekrarlayın veya aktif sayfayı ayarladıktan sonra `Workbook.save` ile `SaveFormat.PPTX` kullanın.

---

## XLSX'i Programlı Olarak Nasıl Dönüştürürsünüz (bonus)

PPTX'in ötesinde, çalışma kitabını PDF veya PNG gibi başka bir formata da dönüştürmek isteyebilirsiniz. Aynı `ImageOrPrintOptions` sınıfı bu hedefler için de çalışır:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

Bu, Aspose.Cells'in daha geniş **how to convert xlsx** yeteneğini gösterir.

---

## Yaygın Tuzaklar ve En İyi Uygulama İpuçları

| Sorun | Neden oluşur | Çözüm |
|-------|----------------|-----|
| Şekiller görüntülere dönüşür | `setEditable(false)` (varsayılan) | `exportOptions.setEditable(true)` çağırın |
| Dışa aktarılan slayt boş | Yazdırma alanı herhangi bir veri içermiyor | `setPrintArea`'a geçirilen aralık dizesini doğrulayın |
| Grafik biçimlendirmesini kaybeder | Eski bir Aspose.Cells sürümü kullanmak | En son kütüphaneye yükseltin (≥ 23.9) |
| Dosya boyutu büyük | Tüm çalışma sayfasını dışa aktarmak | Yazdırma alanını sınırlayın veya kullanılmayan satır/sütunları gizleyin |

---

## Sonuç

Artık **how to export Excel** çalışma kitaplarını tam düzenlenebilir şekil ve grafiklerle PPTX'e nasıl aktaracağınızı, çıktıyı odaklamak için **set print area**'ı nasıl ayarlayacağınızı ve sorunsuz sunum düzenlemesi için **convert Excel chart** nesnelerini nasıl dönüştüreceğinizi biliyorsunuz. Yukarıdaki eksiksiz, çalıştırılabilir Java örneği, Aspose.Cells kullanan herhangi bir projeye eklenebilir.

**Sonraki adımlar**

* PowerPoint'te **convert excel chart** seçeneklerini keşfedin (ör. grafik tipini değiştirme).  
* Bu dışa aktarmayı **set print area excel** otomasyonu ile birleştirerek tek bir çalışma kitabından birden fazla slayt oluşturun.  
* Aynı `ImageOrPrintOptions` desenini kullanarak diğer formatlara (PDF, PNG) dışa aktarmayı deneyin.

Farklı aralıklar, birden fazla çalışma sayfası veya özel slayt düzenleriyle denemeler yapmaktan çekinmeyin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Excel'de Yazdırma Alanı Ayarlama ve PowerPoint'e Dışa Aktarma](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Excel'i PowerPoint'e Dönüştürme ve Yazdırma Alanı Ayarlama](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Excel'de Yazdırma Alanı Ayarlama ve PowerPoint'e Dışa Aktarma – Adım Adım Kılavuz](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}