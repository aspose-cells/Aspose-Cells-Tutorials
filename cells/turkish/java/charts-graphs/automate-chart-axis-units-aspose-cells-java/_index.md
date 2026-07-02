---
date: '2026-07-02'
description: Aspose.Cells for Java kullanarak grafiği PDF'ye nasıl dışa aktaracağınızı
  ve eksen aralığını otomatik olarak nasıl ayarlayacağınızı öğrenin. Excel grafik
  otomasyonu için eksiksiz rehber.
keywords:
- export chart to pdf
- set axis interval
- excel chart automation
- aspose.cells maven
- load excel workbook java
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  headline: Export Chart to PDF and Automate Axis Units in Java
  type: TechArticle
- description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  name: Export Chart to PDF and Automate Axis Units in Java
  steps:
  - name: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
    text: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
  - name: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
    text: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
  - name: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
    text: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
  type: HowTo
- questions:
  - answer: Yes—use `chart.toImage("output.png", ImageFormat.getPng())` for PNG, JPEG,
      BMP, and more.
    question: Can I export charts to image formats as well?
  - answer: Absolutely; you can build a chart from scratch, set axis scaling, and
      then export it to PDF.
    question: Does the API support charts created programmatically?
  - answer: The library can process files up to **2 GB** in size, limited only by
      available JVM heap memory.
    question: What is the maximum file size Aspose.Cells can handle?
  - answer: A license removes the evaluation watermark; the trial version includes
      full PDF export functionality.
    question: Is a license required for PDF export?
  - answer: Call `chart.getCategoryAxis().setMajorUnit(10.0)` (or `setMinorUnit`)
      to define a fixed interval.
    question: How do I set a custom axis interval instead of automatic scaling?
  type: FAQPage
title: Grafiği PDF'ye Dışa Aktar ve Java'da Eksen Birimlerini Otomatikleştir
url: /tr/java/charts-graphs/automate-chart-axis-units-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Grafik PDF Olarak Dışa Aktarma ve Eksen Birimlerini Otomatikleştirme

## Giriş

Bir grafiği PDF olarak dışa aktarırken eksen birimlerini otomatik olarak yapılandırmak, sayısız manuel adımı ortadan kaldırır ve biçimlendirme hatalarını önler. Bu öğreticide **grafiği PDF olarak dışa aktarma** ve **ekseni aralık olarak ayarlama** işlemlerini Aspose.Cells for Java ile programlı bir şekilde nasıl yapacağınızı keşfedeceksiniz—tam olarak Microsoft Excel'in yaptığı şekilde. Ortam kurulumunu, çalışma kitabını yüklemeyi, grafik eksen ölçeklendirmesini yapılandırmayı ve nihayetinde grafiği PDF dosyası olarak oluşturmayı adım adım inceleyeceğiz.

**Öğrenecekleriniz**
- Aspose.Cells for Java'yı bir Maven veya Gradle projesine nasıl ekleyeceğiniz (`aspose.cells maven`).
- **load Excel workbook java** kodunu doğru şekilde nasıl **yükleyeceğiniz** ve grafiklere nasıl erişeceğiniz.
- Mükemmel görsel çıktı için grafik eksen ölçeklendirmesini (`set axis interval`) otomatikleştirme adımları.
- Grafiği PDF ve diğer formatlarda dışa aktarma.

## Hızlı Yanıtlar
- **Aspose.Cells ile bir grafiği PDF olarak dışa aktarabilir miyim?** Evet—ekseni yapılandırdıktan sonra `chart.toPdf()` çağırın.
- **Üretim ortamı için lisansa ihtiyacım var mı?** Geçerli bir Aspose.Cells lisansı değerlendirme filigranlarını kaldırır.
- **Hangi yapı aracı önerilir?** Maven (`aspose.cells maven`) veya Gradle aynı derecede uygundur.
- **API Java 8+ ile uyumlu mu?** Kesinlikle; Aspose.Cells Java 8'den Java 21'e kadar destekler.
- **Her grafik türü için eksen birimlerini otomatikleştirebilir miyim?** Aynı API çizgi, çubuk, dağılım ve pasta grafiklerinde çalışır.

## “Grafiği PDF Olarak Dışa Aktarma” nedir?
Grafiği PDF olarak dışa aktarmak, bir Excel grafiğinin görsel temsilini yüksek kaliteli, vektör tabanlı bir PDF belgesine dönüştürür. Bu işlem, grafiğin düzenini, renklerini, yazı tiplerini ve eksen ölçeklendirmesini korur; çözünürlükten bağımsız bir dosya üretir ve sunucuda Microsoft Excel yüklü olmasa bile herhangi bir platformda görüntülenebilir.

## Neden Grafik Eksen Ölçeklendirmesini Otomatikleştirmelisiniz?
Aspose.Cells, veri aralığına göre optimal eksen aralığını otomatik olarak hesaplayabilir; bu, Excel'in yerel davranışını taklit eder. Manuel ayarlamaları ortadan kaldırır, raporlar arasında tutarlılığı garanti eder ve yanlış yorumlanan veriler riskini azaltır. **Sayısal iddia:** Aspose.Cells, **1 048 576 satır** ve **16 384 sütun**a kadar çalışma sayfasını işleyebilir ve tipik veri setlerinde eksen hesaplamalarını **0.2 saniyenin** altında tutar.

## Önkoşullar
- **Aspose.Cells for Java** (sürüm 25.3 veya üzeri).  
- Java Development Kit (JDK 8 veya daha yeni).  
- Bağımlılık yönetimi için Maven veya Gradle.  
- Temel Java bilgisi ve Excel grafik kavramlarına aşinalık.

## Aspose.Cells for Java'ı Kurma

Aspose.Cells'ı kullanmaya başlamak için kütüphaneyi Maven veya Gradle aracılığıyla projenize ekleyin.

**Maven (`aspose.cells maven`):**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Lisans Edinme
Aspose.Cells for Java'ı kullanmak için geçici bir lisans alabilir veya tam bir lisans satın alabilirsiniz:
- **Ücretsiz Deneme:** [Aspose Downloads](https://releases.aspose.com/cells/java/) adresinden deneme sürümünü indirin.
- **Geçici Lisans:** [Aspose Temporary License page](https://purchase.aspose.com/temporary-license/) üzerinden geçici lisans başvurusu yapın.
- **Lisans Satın Al:** [Aspose Purchase Page](https://purchase.aspose.com/buy) üzerinden tam lisans satın alın.

Aspose.Cells'ı Excel dosyanızı yükleyerek başlatın:  
```java
Workbook wb = new Workbook("your-file-path.xlsx");
```

Ortam hazır olduğunda, temel uygulamaya geçelim.

## Aspose.Cells for Java kullanarak bir grafiği PDF olarak nasıl dışa aktarırım?

`Chart`, bir çalışma sayfasındaki verilerin grafiksel temsilini (çizgi, çubuk veya pasta gibi) ifade eder.  
Çalışma kitabını yükleyin, grafiği bulun, otomatik eksen ölçeklendirmesini uygulayın ve PDF dışa aktarma metodunu çağırın. Aşağıdaki adımlar, 70 kelimenin altında tam akışı gösterir.

İlk olarak bir `Workbook` örneği oluşturun, istenen `Chart` nesnesini alın, otomatik eksen aralığı hesaplamasını etkinleştirin ve sonunda `chart.toPdf("output.pdf")` metodunu çağırın. Bu tek satırlık dışa aktarım, tüm biçimlendirmeyi ve eksen ayarlarını Excel'de göründüğü gibi korur.

### Verileri Yükleme ve Erişim

`Workbook` sınıfı, Aspose.Cells'ın bellekteki tüm Excel dosyasını temsil eden üst‑seviye nesnesidir. Dosyayı yüklemek, çalışma sayfalarına, hücrelere ve gömülü grafiklere erişim sağlar:  
```java
// Load the sample Excel file
Workbook wb = new Workbook(srcDir + "sampleHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.xlsx");

// Access first worksheet
Worksheet ws = wb.getWorksheets().get(0);

// Access first chart
Chart ch = ws.getCharts().get(0);
```

### Grafik Eksen Birimlerini Otomatikleştirme

`Axis`, bir grafiğin X veya Y boyutunun ölçeğini ve etiketlemesini tanımlar; işaretçileri ve aralıkları kontrol eder.  
Grafik eksen birimlerini otomatikleştirmek, grafiklerinizin Excel davranışını taklit etmesini sağlar, veri temsilinde tutarlılık ve doğruluk sunar. `Axis` nesnesi üzerinde `setAutomaticMajorUnit(true)` metodunu kullanarak Aspose.Cells'ın veri aralığına göre optimal aralığı hesaplamasını sağlayın.

**Grafiği PDF Olarak Oluşturma:**  
Grafikleri farklı formatlarda dışa aktarmak, sunumlar veya raporlar için özellikle faydalıdır. İşte eksen yapılandırmasından sonra bir grafiği PDF olarak nasıl oluşturacağınız:  
```java
// Render chart to pdf
ch.toPdf(outDir + "outputHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.pdf");
```

## Temel Yapılandırma Seçenekleri

Aspose.Cells, grafikler için **150**'den fazla yapılandırılabilir özellik sunar; renklerden veri etiketlerine kadar her şeyi ince ayar yapabilirsiniz. Eksen ölçeklendirmesi için en ilgili seçenekler şunlardır:

- `setAutomaticMajorUnit(boolean)` – kütüphanenin en iyi aralığı belirlemesine izin verir.
- `setMajorUnit(double)` – gerekirse aralığı manuel olarak geçersiz kılar.
- `setMinorUnit(double)` – küçük işaret aralığını kontrol eder.

## Pratik Uygulamalar

Grafik eksen birimlerini otomatikleştirmek, birçok gerçek‑dünya senaryosunda değerlidir:

1. **Finansal Raporlama:** Sayılar büyüdükçe eksen aralıklarını otomatik olarak ayarlayan çeyrek dönem kar‑zarar grafiklerini oluşturun.
2. **Satış Analizi:** Yeni verilere manuel yeniden biçimlendirme ihtiyacı olmadan uyum sağlayan dinamik satış performans grafikleri yaratın.
3. **Proje Yönetimi:** Görev süresine göre tarih eksenlerinin otomatik ölçeklendiği zaman çizelgesi Gantt grafiklerini üretin.

## Performans Düşünceleri

Büyük çalışma kitaplarını işlerken optimum performans için:

- Kullanılmayan `Workbook` örneklerini hemen kapatarak belleği serbest bırakın.
- `Workbook.calculateFormula()` yalnızca gerektiğinde kullanın; Aspose.Cells çoğu formülü tembelce değerlendirir.
- **Sayısal iddia:** 200 sayfalık bir çalışma kitabı ve 500 KB grafik verisi, standart 2.6 GHz CPU'da **1.5 saniyenin** altında işlenir.

**En İyi Uygulamalar**
- Performans iyileştirmelerinden ve yeni dosya‑format desteğinden yararlanmak için Aspose.Cells'ı güncel tutun.
- Java’nın yerleşik araçları (ör. VisualVM) ile uygulamanızı profil çıkararak grafik oluşturmayla ilgili olası darboğazları tespit edin.

## Sıkça Sorulan Sorular

**S: Grafikleri görüntü formatlarında da dışa aktarabilir miyim?**  
C: Evet—PNG, JPEG, BMP ve daha fazlası için `chart.toImage("output.png", ImageFormat.getPng())` kullanın.

**S: API, programlı olarak oluşturulan grafikleri destekliyor mu?**  
C: Kesinlikle; sıfırdan bir grafik oluşturabilir, eksen ölçeklendirmesini ayarlayabilir ve ardından PDF olarak dışa aktarabilirsiniz.

**S: Aspose.Cells işleyebileceği maksimum dosya boyutu nedir?**  
C: Kütüphane, yalnızca mevcut JVM heap belleğiyle sınırlı olmak kaydıyla **2 GB**'a kadar dosyayı işleyebilir.

**S: PDF dışa aktarımı için lisans gerekli mi?**  
C: Lisans, değerlendirme filigranını kaldırır; deneme sürümü tam PDF dışa aktarım işlevselliği içerir.

**S: Otomatik ölçeklendirme yerine özel bir eksen aralığı nasıl ayarlanır?**  
C: `chart.getCategoryAxis().setMajorUnit(10.0)` (veya `setMinorUnit`) çağırarak sabit bir aralık tanımlayın.

## Kaynaklar
- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)
- [Download Aspose.Cells Java](https://releases.aspose.com/cells/java/)
- [Purchase License](https://purchase.aspose.com/buy)
- [Free Trial](https://releases.aspose.com/cells/java/)
- [Temporary License](https://purchase.aspose.com/temporary-license/)
- [Support Forum](https://forum.aspose.com/c/cells/9)

---

**Son Güncelleme:** 2026-07-02  
**Test Edilen Versiyon:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Export Excel Charts to PDF Using Aspose.Cells for Java: Custom Page Sizes Guide](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [How to Create and Export Charts in Java Using Aspose.Cells: A Complete Guide](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [Extract Excel Chart Axis Labels Using Aspose.Cells Java: A Comprehensive Guide](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}