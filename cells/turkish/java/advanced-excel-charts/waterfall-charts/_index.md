---
date: 2026-09-02
description: Aspose.Cells ile Java'da excel waterfall chart oluşturmayı öğrenin, chart
  data range'i ayarlayın, etiketleri özelleştirin ve XLSX'e export edin.
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: Waterfall Charts
og_description: Aspose.Cells for Java kullanarak excel waterfall chart oluşturun –
  chart data range'i ayarlayın, data labels ekleyin ve birkaç adımda XLSX'e export
  edin.
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Aspose.Cells for Java ile excel waterfall chart oluşturun
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Aspose.Cells for Java ile excel waterfall chart oluşturun
url: /tr/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Şelale grafikleri

## Aspose.Cells for Java kullanarak şelale grafiklerine giriş

Bu öğreticide **excel şelale grafiği oluşturmayı** ve **grafik veri aralığını ayarlamayı** Aspose.Cells for Java ile öğreneceksiniz. Şelale grafikleri, pozitif ve negatif sayı serilerini net bir görsel hikayeye dönüştürerek finansal tablolar, satış performans incelemeleri ve bireysel öğelerin toplam üzerindeki etkisini görmek istediğiniz her senaryo için idealdir.

## Hızlı cevaplar
- **Şelale grafiği nedir?** Başlangıç değerinin bir dizi ara değerle artırılıp azaltıldığını gösteren, sonunda bir toplamla biten görsel bir sunum.  
- **Hangi kütüphane kullanılıyor?** Aspose.Cells for Java.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim için ticari lisans gerekir.  
- **Dosyayı XLSX olarak kaydedebilir miyim?** Evet – `workbook.save("FileName.xlsx")` kullanın.  
- **Java veri görselleştirmesi için uygun mu?** Kesinlikle; Aspose.Cells, Office yüklü olmadan zengin grafik özellikleri sunar.

## Şelale grafiği nedir?
Şelale grafiği, bir başlangıç değerine sırasıyla eklenen pozitif ve negatif katkıları gösterir, böylece her bileşenin genel sonuç üzerindeki etkisini anlamanızı sağlar. Kazançları ve kayıpları yan yana görselleştirerek karmaşık finansal akışları anında okunabilir hâle getirir.

## Aspose.Cells for Java'ı şelale grafiği eklemek için neden kullanmalısınız?
Aspose.Cells, Microsoft Excel'e ihtiyaç duymadan herhangi bir sunucu, CI pipeline veya masaüstünde Excel grafikleri oluşturmanıza olanak tanır. **15+ çıktı formatını** (XLSX, PDF, HTML, CSV vb.) destekler, **500+ satır** içeren çalışma kitaplarını bir saniyeden kısa sürede işler ve renklerden veri etiketlerine kadar her grafik öğesi üzerinde programatik kontrol sağlar.

## Önkoşullar

Kodlamaya başlamadan önce aşağıdaki önkoşulların sağlandığından emin olun:

- Aspose.Cells for Java: Aspose.Cells for Java yüklü olmalıdır. İndirmek için Aspose.Cells for Java sürüm sayfasını ziyaret edin: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Java geliştirme ortamı: Sisteminizde Java kurulu olmalı ve bir derleme aracı (Maven/Gradle) hazır bulunmalıdır.

Şimdi, şelale grafiğini adım adım oluşturmaya başlayalım.

## Java'da şelale grafiği için grafik veri aralığını nasıl ayarlarsınız
Yeni bir çalışma kitabı yükleyin, verileri doldurun, bir `Chart` nesnesi ekleyin, seri aralığını tanımlayın ve son olarak dosyayı kaydedin. Bu süreç basittir: bir çalışma kitabı oluşturur, hücreleri kategori ve değerlerle doldurur, bir grafik oluşturur, veri aralıklarını bağlar ve ardından çalışma kitabını dışa aktarırsınız. Sonuç, raporlar veya panolar için hazır tam işlevsel bir şelale grafiğidir.

### Adım 1: Aspose.Cells'i içe aktar
`com.aspose.cells` paketi, çalışma kitabı oluşturma, çalışma sayfası işleme ve grafik üretimi dahil olmak üzere Excel manipülasyonu için gereken tüm sınıfları içerir.

### Adım 2: çalışma kitabını ve çalışma sayfasını başlat
**Workbook**, bir Excel dosyasını temsil eder ve **Worksheet**, o dosya içindeki tek bir sayfadır. Bu nesneleri oluşturmak, ham veri ve grafiğin kanvasını sağlar.

### Adım 3: veri gir
A sütunu kategori etiketlerini, B sütunu ise şelale için sayısal değerleri tutar. Bu düzen, finansal analizde kullanılan tipik kar‑zarar akışına uygundur.

### Adım 4: şelale grafiği oluştur
**Chart** nesnesi görsel bir temsil oluşturur; tipini `ChartType.WATERFALL` olarak ayarlamak grafiği şelale biçiminde yapılandırır. Seri için veri aralığını (`"B2:B6"`) ayarlamak üzere `add` metodunu kullanın ve kategori eksenini `"A2:A6"` ile bağlayın.

### Adım 5: çalışma kitabını kaydet
Çalışma kitabını kaydetmek, grafiği ve verileri belirtilen dosya formatına yazar. `workbook.save("WaterfallChart.xlsx")` çağrısı bir XLSX dosyası üretir; format parametresini değiştirerek PDF, CSV veya HTML olarak dışa aktarabilirsiniz.

## Yaygın sorunlar ve çözümler

- **Grafik boş görünüyor** – Veri aralığı referanslarının (`B2:B6` ve `A2:A6`) değer ve kategori hücrelerinizle eşleştiğinden emin olun.  
- **Negatif değerler doğru gösterilmiyor** – Serinin tipinin `ChartType.WATERFALL` olarak ayarlandığını doğrulayın; diğer grafik tipleri negatifleri farklı işler.  
- **Dosya Excel'de açılmıyor** – En son Aspose.Cells sürümünü kullanın ve dosya uzantısının formatla eşleştiğini kontrol edin (`.xlsx` Excel için).

## Sıkça Sorulan Sorular

### Şelale grafiğimin görünümünü nasıl özelleştirebilirim?
`Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` gibi özellikleri değiştirerek çubuk renklerini ayarlayabilir, `setShowDataLabels(true)` ile veri etiketlerini etkinleştirebilir ve `getCategoryAxis().setTitle("Stage")` ile eksen başlıklarını düzenleyebilirsiniz. Aspose.Cells API referansı, özelleştirilebilir seçeneklerin tam listesini sunar.

### Aynı çalışma sayfasında birden fazla şelale grafiği oluşturabilir miyim?
Evet. İlk grafiği ekledikten sonra farklı bir veri aralığı ve yeni bir `Chart` nesnesiyle grafik‑oluşturma adımlarını tekrarlayın. Her grafik bağımsızdır ve sayfa üzerindeki istediğiniz konuma yerleştirilebilir.

### Aspose.Cells farklı Java geliştirme ortamlarıyla uyumlu mu?
Kesinlikle. Kütüphane Eclipse, IntelliJ IDEA, NetBeans ve Maven veya Gradle destekleyen herhangi bir derleme sistemiyle çalışır. Ek bir eklenti gerekmez.

### Şelale grafiğime ek veri serileri ekleyebilir miyim?
`chart.getNSeries().add("C2:C6", true)` çağrısı yaparak daha fazla seri ekleyebilir ve her birini ayrı ayrı yapılandırabilirsiniz. Bu, birden fazla senaryoyu yan yana karşılaştırmanıza olanak tanır.

### Aspose.Cells for Java için daha fazla kaynak ve örnek nerede bulunabilir?
Tam dökümantasyonu Aspose.Cells Java API referansında keşfedin: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## SSS

**S: Finansal bir şelale grafiği için grafik veri aralığını nasıl ayarlarım?**  
C: Grafiğin serisine `add` metodunu kullanarak değerlerin bulunduğu hücre aralığını, örneğin `"B2:B6"` şeklinde geçirin.

**S: Çalışma kitabını XLSX yerine PDF olarak dışa aktarabilir miyim?**  
C: Evet, `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` çağrısı bir PDF sürümü üretir.

**S: Daha fazla kategori içeren bir şelale grafiği oluşturmam gerekirse ne yapmalıyım?**  
C: Hem değer sütununda hem de kategori sütununda veri aralığını genişletin, ardından `add` ve `setCategoryData` çağrılarını buna göre güncelleyin.

**S: Pozitif ve negatif çubukları otomatik olarak biçimlendirmek mümkün mü?**  
C: `Series` koleksiyonunu döngüyle gezerek her değerin işaretine göre `FillFormat` rengini ayarlayabilirsiniz; Aspose.Cells programatik olarak koşullu biçimlendirme uygulamayı destekler.

**S: Aspose.Cells grafikler için dinamik veri güncellemelerini destekliyor mu?**  
C: Evet. Hücre değerlerini değiştirdikten sonra sadece çalışma kitabını yeniden kaydedin — grafik yeni verileri otomatik olarak yansıtacaktır.

---

**Son Güncelleme:** 2026-09-02  
**Test Edilen:** Aspose.Cells for Java (latest)  
**Yazar:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## İlgili Eğitimler

- [Aspose.Cells for Java kullanarak Excel Grafik Veri Etiketlerini Özelleştirme: Adım Adım Kılavuz](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Aspose.Cells Java ile Excel Grafiğine Veri Etiketleri Ekle](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Aspose.Cells Kullanarak Java'da Grafik Oluşturma ve Dışa Aktarma: Tam Kılavuz](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}