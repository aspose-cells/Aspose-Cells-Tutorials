---
category: general
date: 2026-06-30
description: Grafiği resim olarak dışa aktar ve grafiği dışa aktarmayı, Excel'i Word
  olarak kaydetmeyi, Excel'i Word'e dönüştürmeyi ve XLSX'i DOCX'e birkaç kolay adımda
  nasıl yapacağınızı öğrenin.
draft: false
keywords:
- export chart as image
- how to export chart
- save excel as word
- convert excel to word
- convert xlsx to docx
language: tr
og_description: Grafiği resim olarak dışa aktar ve Excel'i hızlıca Word'e dönüştür.
  Bu rehberi izleyerek Excel'i Word olarak kaydedin, grafikleri dışa aktarın ve XLSX'i
  DOCX'e dönüştürün.
og_title: Grafiği Görüntü Olarak Dışa Aktar – Adım Adım Excel'den Word'e Dönüştürme
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  headline: Export Chart as Image – Complete Guide to Convert Excel to Word
  type: TechArticle
- description: Export chart as image and learn how to export chart, save Excel as
    Word, convert Excel to Word, and convert XLSX to DOCX in a few easy steps.
  name: Export Chart as Image – Complete Guide to Convert Excel to Word
  steps:
  - name: What if my workbook has multiple charts?
    text: You don’t need to change anything—setting `setExportChartAsImage(true)`
      applies to **all** charts in the workbook. If you only want specific charts
      as images, you’ll have to export them manually using `chart.toImage()` and then
      insert them into the Word file yourself.
  - name: Can I control the image format (PNG vs JPEG)?
    text: 'Aspose.Cells uses PNG by default for chart‑as‑image exports. To switch
      to JPEG, you can adjust the `ImageOrPrintOptions` before saving:'
  - name: Does this work with older Excel files (.xls)?
    text: Absolutely. The same code works for both `.xls` and `.xlsx`. Aspose.Cells
      auto‑detects the format, so you can **save Excel as Word** regardless of the
      source version.
  - name: How does this differ from “convert Excel to Word” with native Office interop?
    text: Native interop often requires a Windows machine with Office installed, and
      charts may lose fidelity. Using Aspose.Cells is platform‑agnostic, works on
      Linux/macOS, and preserves chart quality by rasterizing them.
  type: HowTo
tags:
- Excel
- Word
- Chart
- Java
- Aspose.Cells
title: Grafiği Görüntü Olarak Dışa Aktarma – Excel'den Word'e Dönüştürme Tam Kılavuzu
url: /tr/java/excel-import-export/export-chart-as-image-complete-guide-to-convert-excel-to-wor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Grafiği Görüntü Olarak Dışa Aktarma – Excel'i Word'e Dönüştürme Tam Kılavuzu

Bir Excel çalışma kitabındaki grafiği görüntü olarak dışa aktarıp doğrudan bir Word belgesine yerleştirmeyi hiç merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli olarak, “XLSX'ten grafiği nasıl dışa aktarırım ve kalite kaybı olmadan DOCX'e gömerim?” sorusunu soruyor.  

İyi haber şu ki, birkaç satır Java kodu ile **grafiği görüntü olarak dışa aktarabilir**, ardından **Excel'i Word olarak kaydedebilirsiniz** tek bir akışta. Bu öğreticide tüm süreci adım adım inceleyecek, çalışma kitabını yüklemeden grafiklerinizi DOCX dosyası içinde net PNG'lere dönüştüren kaydetme seçeneklerini yapılandırmaya kadar her şeyi ele alacağız.

Ayrıca **Excel'i Word'e dönüştürme**, **Excel'i Word olarak kaydetme** ve **XLSX'i DOCX'e dönüştürme** gibi ilgili görevlerden de bahsedeceğiz—kod temiz ve çalıştırılabilir kalacak. Gereksiz ayrıntı yok, bugün kopyalayıp‑yapıştırabileceğiniz pratik bir çözüm.

---

## Gerekenler

- **Java Development Kit (JDK) 8+** – kod herhangi bir modern JDK'da çalışır.
- **Aspose.Cells for Java** kütüphanesi (sürüm 23.10 veya daha yenisi). Maven Central'dan alabilir veya JAR dosyasını doğrudan indirebilirsiniz.
- **Excel dosyası** (`charts.xlsx`) – içinde dışa aktarmak istediğiniz en az bir grafik bulunmalı.
- **Java IDE** (IntelliJ IDEA, Eclipse veya VS Code) – herhangi biri yeterli.
- Java ve Maven/Gradle hakkında temel bilgi (isteğe bağlı ama faydalı).

Hepsi bu. Ek bir eklenti, COM interop yok, sadece saf Java.

---

## Adım 1: Excel Çalışma Kitabını Yükleyin ve Grafiği Bulun

İlk olarak grafiği barındıran çalışma kitabını açmamız gerekiyor. Aspose.Cells bunu çok kolay hâle getiriyor—sadece dosya yolunu gösterin.

```java
// Step 1: Load the Excel workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

// Grab the first worksheet (index 0) and its first chart (index 0)
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

> **Neden önemli:** Çalışma kitabını yüklemek, grafik nesnesine erişmemizi sağlar; daha sonra Aspose'a bu grafiği bir görüntü olarak oluşturmasını söyleyeceğiz. Çalışma kitabı birden fazla sayfa veya grafik içeriyorsa, indeksleri ayarlayabilir veya döngüyle işleyebilirsiniz.

---

## Adım 2: Grafikleri Görüntü Olarak Dışa Aktarmak İçin DOCX Kaydetme Seçeneklerini Yapılandırın

Aspose.Cells, dönüşüm davranışını kontrol etmenizi sağlayan bir `DocxSaveOptions` sınıfı sunar. `setExportChartAsImage(true)` ayarı, kütüphaneye her grafiği Word dosyasına yerleştirmeden önce bir görüntüye rasterleştirmesini söyler.

```java
// Step 2: Create DOCX save options and enable chart‑as‑image export
DocxSaveOptions saveOptions = new DocxSaveOptions();
saveOptions.setExportChartAsImage(true); // This is the key line
```

> **Pro ipucu:** Vektör grafik (EMF/WMF) tercih ediyorsanız bu bayrağı kapalı bırakabilirsiniz, ancak raster görüntüler genellikle Word sürümleri arasında daha tutarlı render edilir.

---

## Adım 3: Çalışma Kitabını DOCX Dosyası Olarak Kaydedin

Seçenekler ayarlandığına göre, sadece çalışma kitabını kaydediyoruz. Kütüphane, tüm çalışma sayfalarını, tabloları ve—bayrağımız sayesinde—grafikleri görüntü olarak dönüştürmeyi halleder.

```java
// Step 3: Save the workbook as a DOCX file, applying the chart‑export option
workbook.save("YOUR_DIRECTORY/charts.docx", saveOptions);
```

> **Ne elde edersiniz:** `charts.docx` dosyası, orijinal Excel grafiğinin yüksek çözünürlüklü bir PNG (veya ayarlarınıza bağlı olarak JPEG) olarak Word belgesi içinde göründüğü bir dosyadır. Sonucu görmek için Microsoft Word'de açın.

---

## Adım 4: Çıktıyı Doğrulayın (İsteğe Bağlı ama Tavsiye Edilir)

Özellikle toplu işlemler otomatikleştirildiğinde, dönüşümün başarılı olduğunu programatik olarak doğrulamak her zaman iyi bir fikirdir.

```java
// Optional: Verify that the DOCX file exists and is not empty
File docxFile = new File("YOUR_DIRECTORY/charts.docx");
if (docxFile.exists() && docxFile.length() > 0) {
    System.out.println("Success! DOCX created with chart as image.");
} else {
    System.err.println("Conversion failed – check the source file and options.");
}
```

Kod parçacığını çalıştırıp başarı mesajını görürseniz, **XLSX'i DOCX'e dönüştürmüş** ve grafik görsellerini görüntü olarak korumuş olursunuz.

---

## Tam Çalışan Örnek

Aşağıda tüm adımları bir araya getiren, doğrudan çalıştırılabilir Java programı yer alıyor. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek yol ile değiştirmeniz yeterli.

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportChartAsImageDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook containing the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/charts.xlsx");

        // Access the first worksheet and its first chart
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        if (chart == null) {
            System.err.println("No chart found in the first worksheet.");
            return;
        }

        // Configure DOCX save options to export charts as images
        DocxSaveOptions saveOptions = new DocxSaveOptions();
        saveOptions.setExportChartAsImage(true);   // Export chart as image

        // Save as DOCX
        String outputPath = "YOUR_DIRECTORY/charts.docx";
        workbook.save(outputPath, saveOptions);

        // Verify the output file
        File outFile = new File(outputPath);
        if (outFile.exists() && outFile.length() > 0) {
            System.out.println("File saved successfully: " + outputPath);
        } else {
            System.err.println("Failed to create the DOCX file.");
        }
    }
}
```

**Programı çalıştırdığınızda beklenen çıktı:**

```
File saved successfully: YOUR_DIRECTORY/charts.docx
```

`charts.docx` dosyasını Microsoft Word'de açın; grafiğin temiz bir görüntü olarak, orijinal Excel grafiğinin bulunduğu konuma mükemmel bir şekilde yerleştirildiğini göreceksiniz.

---

## Yaygın Sorular & Kenar Durumları

### Çalışma kitabımda birden fazla grafik varsa ne olur?

Hiçbir şey değiştirmenize gerek yok—`setExportChartAsImage(true)` ayarı **tüm** grafiklere uygulanır. Sadece belirli grafikleri görüntü olarak dışa aktarmak isterseniz, `chart.toImage()` ile manuel olarak dışa aktarıp ardından Word dosyasına kendiniz eklemeniz gerekir.

### Görüntü formatını (PNG vs JPEG) kontrol edebilir miyim?

Aspose.Cells, grafik‑görüntü dışa aktarmaları için varsayılan olarak PNG kullanır. JPEG'e geçmek isterseniz, kaydetmeden önce `ImageOrPrintOptions` ayarını değiştirebilirsiniz:

```java
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.getJpeg());
saveOptions.setImageOrPrintOptions(imgOptions);
```

### Eski Excel dosyaları (.xls) ile çalışır mı?

Kesinlikle. Aynı kod hem `.xls` hem de `.xlsx` için çalışır. Aspose.Cells formatı otomatik algılar, böylece **Excel'i Word olarak kaydedebilir** kaynak sürüm ne olursa olsun.

### Yerel Office interop ile “Excel'i Word'e dönüştürme” arasındaki fark nedir?

Yerel interop genellikle Office yüklü bir Windows makine gerektirir ve grafikler kalite kaybına uğrayabilir. Aspose.Cells platform‑bağımsızdır, Linux/macOS'ta çalışır ve grafikleri rasterleştirerek kaliteyi korur.

---

## Üretim‑Hazır Uygulamalar İçin İpuçları

- **Toplu işleme:** Bir klasördeki tüm XLSX dosyalarını döngüyle işleyin, aynı `DocxSaveOptions` ayarını uygulayın. Dönüşümü bir try‑catch bloğuna sararak bozuk dosyaları zarifçe ele alın.
- **Bellek yönetimi:** Çok büyük çalışma kitapları için kaydetme işleminden sonra `workbook.dispose()` çağırarak yerel kaynakları serbest bırakın.
- **Özelleştirme:** Dönüştürürken hücre stillerinin korunması gerekiyorsa `saveOptions.setPreserveCellFormatting(true)` ayarını ekleyebilirsiniz.
- **Günlükleme:** Dönüşüm istatistiklerini yakalamak için bir günlükleme çerçevesi (SLF4J, Log4j) entegre edin—denetim izleri için faydalıdır.

---

## Sonuç

Artık sadece birkaç Java ifadesiyle **grafiği görüntü olarak dışa aktar**, **Excel'i Word olarak kaydet** ve **XLSX'i DOCX'e dönüştür** gibi sağlam, uçtan uca bir çözümünüz var. Ana çıkarım, Aspose.Cells’ın `DocxSaveOptions` sınıfının grafik işleme sürecini zahmetsiz hâle getirmesi—manuel görüntü çıkarma, COM interop yok ve tam çapraz‑platform desteği.

Denemekten çekinmeyin: birden fazla çalışma sayfasını dışa aktarın, görüntü çözünürlüklerini ayarlayın veya bu yaklaşımı diğer Aspose kütüphaneleri (ör. Aspose.Words) ile birleştirerek daha zengin Word belgeleri oluşturun. Grafiği doğru şekilde dışa aktarmayı bildiğinizde sınır yoktur.

Excel dosyalarını dönüştürme, görüntü ekleme veya performans optimizasyonu hakkında daha fazla sorunuz mu var? Aşağıya yorum bırakın, iyi kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose.Cells .NET ile Excel Grafiğini Görüntü Olarak Dönüştür](/cells/english/net/charts-graphs/convert-excel-chart-image-aspose-cells-dotnet/)
- [Aspose.Cells for Java ile Trendline'lı Excel Grafiği Oluşturma ve Görüntü Olarak Dışa Aktarma](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells .NET ile Excel Pasta Grafiğini Görüntü Olarak Dönüştürme: Adım Adım Kılavuz](/cells/english/net/charts-graphs/convert-excel-pie-chart-image-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}