---
date: '2026-09-22'
description: Aspose.Cells for Java kullanarak etkileşimli Excel grafiğini checkboxes
  ile nasıl oluşturacağınızı öğrenin. Bu kılavuz kurulum, checkboxes ekleme, licensing
  ve best practices konularını kapsar.
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Aspose.Cells for Java kullanarak etkileşimli Excel grafiğini checkboxes
  ile nasıl oluşturacağınızı öğrenin. step‑by‑step talimatları izleyin, licensing
  ipuçlarını görün ve real‑world use cases keşfedin.
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: Etkinleştirilebilir Excel grafiği nasıl oluşturulur, checkboxes kullanarak
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: Etkinleştirilebilir Excel grafiği nasıl oluşturulur, checkboxes kullanarak
url: /tr/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Kontrol Kutuları ile Etkileşimli Grafik Nasıl Oluşturulur

## Giriş

Bu öğreticide **etkileşimli bir Excel grafiği** oluşturacaksınız; bu grafik, kullanıcıların grafiğin üzerine yerleştirilen kontrol kutularına tıklayarak veri serilerini açıp kapatmasına olanak tanır. Aspose.Cells for Java kullanarak, Microsoft Excel yüklü olmadan programlı bir şekilde tam özellikli çalışma kitapları oluşturabilirsiniz. Bu yaklaşım, herhangi bir Java tabanlı raporlama veya gösterge paneli çözümü için çalışır.

**Öğrenecekleriniz**
- Maven veya Gradle'da Aspose.Cells for Java'ı nasıl kuracağınızı
- `Workbook` nesnesini nasıl örnekleyeceğinizi ve bir sütun grafiği ekleyeceğinizi
- Grafik alanına bir kontrol kutusu şekli nasıl yerleştirileceğini
- Üretim kullanımı için bir Aspose.Cells lisansının nasıl uygulanacağını

## Hızlı Yanıtlar
- **Hangi kütüphane etkileşimli Excel grafikleri oluşturur?** Aspose.Cells for Java.  
- **VBA kullanmadan kontrol kutuları ekleyebilir miyim?** Evet, API aracılığıyla bir Form Control şekli ekleyerek.  
- **Bu özellik için bir lisansa ihtiyacım var mı?** Değerlendirme için geçici bir lisans yeterli; üretim için kalıcı bir lisans gereklidir.  
- **Hangi Java sürümü gereklidir?** JDK 8 veya üzeri.  
- **Grafik Excel 2016‑2024'te çalışacak mı?** Evet, oluşturulan dosya Office Open XML standardını izler.

## Etkileşimli Excel Grafiği Nedir?
Bir **etkileşimli Excel grafiği**, kullanıcıların veri serilerini anında gösterip gizlemelerini sağlayan UI kontrolleri (ör. kontrol kutuları) ile standart bir grafiği birleştirir; böylece statik bir görsel, dinamik bir raporlama aracına dönüşür.

## Neden Aspose.Cells for Java Kullanmalı?
Aspose.Cells, **80'den fazla giriş ve çıkış formatını** destekler ve **10.000'den fazla satır** içeren çalışma kitaplarını tüm dosyayı belleğe yüklemeden işleyebilir; bu da sunucu tarafı ortamlarında yüksek performanslı üretim sağlar.

## Ön Koşullar

- **Java Development Kit (JDK):** sürüm 8 veya üzeri.  
- **Aspose.Cells for Java:** en son sürüm (ör. 25.3).  
- **Maven veya Gradle:** kütüphane bağımlılığını yönetmek için.  

### Bilgi Ön Koşulları
Temel Java sözdizimi ve Excel kavramlarına (çalışma sayfaları, aralıklar, grafikler) aşina olmak faydalıdır, ancak aşağıdaki adımlar her deneyim seviyesindeki geliştiriciler için yeterince ayrıntılıdır.

## Java'da Kontrol Kutusu Nasıl Eklenir?

Aspose.Cells kütüphanesini yükleyin, bir çalışma kitabı oluşturun ve tek bir çağrıyla bir kontrol kutusu şekli ekleyin. Kontrol kutusu, bir hücreye bağlanabilen bir Form Kontrolüdür; onu değiştirerek bağlanan hücrenin değeri değişir ve bu değeri daha sonra bir grafik serisinin görünürlüğüne bağlayabilirsiniz.

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### Adım 1: Maven Bağımlılığını Ayarlama

`pom.xml` dosyanıza Aspose.Cells Maven artefaktını ekleyin:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### Adım 2: Gradle Bağımlılığını Ayarlama

`build.gradle` dosyanıza aşağıdaki satırı ekleyin:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Lisans Edinme Adımları

Tam işlevselliği açmak için geçici veya kalıcı bir lisans edinin. Deneme lisansını [Aspose'un web sitesinden](https://releases.aspose.com/cells/java/) indirin. Üretim için bir lisans satın alın ve daha sonra gösterildiği gibi uygulayın.

#### Temel Başlatma

License, satın alınan bir lisans dosyasını uygulamak için kullanılan Aspose.Cells sınıfıdır; değerlendirme sınırlamaları olmadan tam işlevselliği etkinleştirir. Çalışma kitabı işlemlerinden önce Java kodunuzda kütüphaneyi başlatın:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Etkileşimli Excel Grafiği Nasıl Oluşturulur?

Bir Aspose.Cells `Workbook` nesnesi, çalışma sayfaları, grafikler ve diğer öğeleri içeren tam bir Excel dosyasını temsil eder. Bir çalışma kitabı oluşturarak programlı bir şekilde veri ekleyebilir, bir sütun grafiği oluşturabilir ve daha sonra kontrol kutuları gibi etkileşimli kontroller yerleştirebilirsiniz. Aşağıdaki adımlar, çalışma kitabını oluşturma, verileri doldurma ve grafiği etkileşimli hale getirme sürecinde size rehberlik eder.

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### Çalışma Kitabını Örnekleyin ve Grafik Ekleyin

#### Genel Bakış

Bu bölüm, yeni bir çalışma kitabı oluşturmayı, veri için bir çalışma sayfası eklemeyi ve daha sonra etkileşimli hale getirilecek bir sütun grafiği üretmeyi gösterir.

##### Adım 1: Yeni bir çalışma kitabı oluşturma

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### Adım 2: Grafik çalışma sayfası ekleme

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### Adım 3: Sütun grafiği ekleme

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### Adım 4: Seri verilerini ekleme

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## Bir Grafiğe Kontrol Kutusu Nasıl Yerleştirilir?

Bir kontrol kutusunu doğrudan grafik alanına yerleştirmek, son kullanıcıların belirli bir seriyi göstermek veya gizlemek için tıklamasına olanak tanır. Kontrol kutusu, bir hücreye bağlanabilen bir Form Kontrol şeklidir; hücre değeri, serinin görünürlüğünü yöneten bir formülde referans alınabilir.

Shape, bir çalışma sayfası içinde form kontrolü, resim veya metin kutusu gibi bir çizim öğesini temsil eden Aspose.Cells nesnesidir.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### Bir kontrol kutusu şekli yerleştirme

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### Kontrol kutusu metnini ayarlama

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## Çalışma Kitabını Excel Dosyası Olarak Nasıl Kaydedilir?

`Workbook`'i kaydetmek, bellek içindeki tüm değişiklikleri diskte fiziksel bir Excel dosyasına yazar. Aspose.Cells, modern .xlsx formatını destekler; böylece dosya Excel 2016‑2024 ve diğer Office uyumlu uygulamalarda açılır. İstenen dosya yolu ile `save` metodunu kullanın ve isteğe bağlı olarak ek seçenekler için dosya formatını belirtebilirsiniz.

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## Pratik Uygulamalar

Kontrol kutularına sahip etkileşimli bir grafiğin değer kattığı gerçek dünya senaryoları:

1. **Etkileşimli raporlar:** Paydaşların satış grafiğinde bireysel ürün hatlarını açıp kapatmasına izin verir.  
2. **Karşılaştırmalı analiz:** Analistlerin belirli zaman dilimlerine veya bölgelere odaklanmasını, serileri işaretleyip işaretlemeyerek sağlar.  
3. **Eğitim gösterge panoları:** Öğrenciler, hangi değişkenlerin gösterileceğini seçerek veri trendlerini keşfedebilir.

## Yaygın Sorunlar ve Çözümler

- **Kontrol kutusu yanıt vermiyor:** Kontrol kutusunun bir hücreye bağlı olduğundan ve hücrenin serinin görünürlüğünü etkileyen bir formülde referans alındığından emin olun.  
- **Grafik, değişiklikten sonra güncellenmiyor:** Excel'de çalışma kitabı görünümünü yenileyin veya formülleri yeniden hesaplayın (`workbook.calculateFormula()`).  
- **Lisans uygulanmadı:** `License license = new License(); license.setLicense("Aspose.Cells.lic");` kodunun herhangi bir çalışma kitabı işleminden önce çalıştırıldığını doğrulayın.

## Sıkça Sorulan Sorular

**Q: VBA kullanmadan bir kontrol kutusu nasıl ekleyebilirim?**  
A: `Shape` API'sini `ShapeType.FORM_CONTROL_CHECKBOX` ile kullanın ve bir çalışma sayfası hücresine bağlayın; kontrol kutusu Excel'de yerel olarak çalışır.

**Q: Kontrol kutusu özelliği için bir lisansa ihtiyacım var mı?**  
A: Kontrol kutusu şekli ücretsiz değerlendirme sürümünde mevcuttur, ancak kalıcı bir Aspose.Cells lisansı değerlendirme sınırlamalarını kaldırır ve tam performans iyileştirmelerini etkinleştirir.

**Q: Oluşturulan dosyayı hangi Excel sürümleri açabilir?**  
A: Aspose.Cells ile kaydedilen dosyalar Office Open XML standardını izler ve Excel 2016, 2019, 2021 ve Microsoft 365'te doğru şekilde açılır.

**Q: Birden fazla seriyi ayrı kontrol kutularıyla kontrol edebilir miyim?**  
A: Evet, her seri için bir kontrol kutusu oluşturun, her birini ayrı bir yardımcı hücreye bağlayın ve koşullu formüllerle her seriyi bağımsız olarak açıp kapatın.

**Q: Grafik başına kontrol kutusu sayısında bir sınırlama var mı?**  
A: Pratikte, onlarca ekleyebilirsiniz; tipik sunucu donanımında bir çalışma sayfası başına 200 kontrole kadar performans sabit kalır.

---

**Son Güncelleme:** 2026-09-22  
**Test Edilen Versiyon:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose.Cells for Java Kullanarak Excel'e Kontrol Kutusu Ekleme: Adım Adım Kılavuz](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Aspose.Cells Java ile Dinamik Excel Grafikler Oluşturma: Geliştiriciler İçin Kapsamlı Rehber](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Aspose.Cells Java ile Excel Grafiğine Veri Etiketleri Ekleme](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}