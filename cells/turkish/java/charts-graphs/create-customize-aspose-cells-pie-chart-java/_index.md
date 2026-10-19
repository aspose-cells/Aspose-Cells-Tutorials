---
date: '2026-09-27'
description: Aspose.Cells kullanarak Java'da pasta grafiği oluşturmayı öğrenin. Excel
  pasta grafiğini özelleştirme, Maven bağımlılığını ayarlama ve profesyonel grafikler
  oluşturma konusunda adım adım rehber.
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Aspose.Cells for Java kullanarak Java'da pasta grafiği oluşturun.
  Excel pasta grafiğini özelleştirmeyi, Maven bağımlılığı eklemeyi ve dakikalar içinde
  profesyonel grafikler üretmeyi öğrenin.
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Aspose.Cells ile Java'da pasta grafiği oluşturun – Tam Java Rehberi
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Aspose.Cells ile Java'da pasta grafiği nasıl oluşturulur
url: /tr/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Java'da pasta grafiği oluşturma

## Giriş
Programmatically **pie chart** oluşturmak çoğu zaman bir bulmaca gibi hissettirebilir, özellikle renkler, lejandlar ve başlıklar üzerinde ince ayar kontrolüne ihtiyaç duyduğunuzda. Bu rehberde Aspose.Cells kullanarak **create pie chart java** nasıl yapılacağını öğrenecek, ardından Excel pasta grafiğini markanıza veya raporlama stilinize uygun şekilde özelleştireceksiniz. Ortam kurulumunu, veri doldurmayı, grafik oluşturmayı ve görsel ayarları adım adım inceleyeceğiz—tüm bunları Java IDE'nizden çıkmadan.

**Neler öğreneceksiniz**
- Projenize **Maven dependency Aspose.Cells** ekleyin.
- Bir çalışma kitabı oluşturun, hücreleri veriyle doldurun ve bir pasta grafiği üretin.
- Grafiğe özel renkler, başlıklar ve lejandlar uygulayın.
- Çalışma kitabını paylaşmaya hazır bir XLSX dosyasına dışa aktarın.

Başlamadan önce, temel Java sözdizimine hâkim olmalı ve Maven ya da Gradle kurulu olmalıdır.

## Hızlı cevaplar
- **Java'da pasta grafiği oluşturan kütüphane hangisidir?** Aspose.Cells for Java.
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim için ücretli bir lisans gereklidir.
- **Gerekli Maven koordinatları nelerdir?** `com.aspose:aspose-cells:24.10`.
- **Dilimi renklerini değiştirebilir miyim?** Evet, her seride `setAreaColor` yöntemiyle.
- **Grafik XLSX olarak dışa aktarılabilir mi?** Kesinlikle—sadece `workbook.save("output.xlsx")` çağırın.

## Excel'de pasta grafiği nedir?
Excel'de bir **pie chart** tek bir veri serisini dairenin oranlı dilimlerine dönüştürerek, bir bütünün parçalarını karşılaştırmayı kolaylaştırır. Her dilimin açısı, toplam değere göre kendi değerine karşılık gelir; bu sayede pazar payı, bütçe dağılımı veya demografik yüzdeler gibi kategorilerdeki dağılımı hızlıca görebilirsiniz.

## Aspose.Cells ile Java'da pasta grafiği oluşturmanın nedeni?
Aspose.Cells 50'den fazla grafik türünü destekler ve dosyanın tamamını belleğe yüklemeden bir milyon satıra kadar çalışma sayfasını işleyebilir. Bu performans avantajı, mütevazı donanımla büyük raporlar üretmenizi sağlarken, grafik görünümü, veri bağlama ve dışa aktarma formatları üzerinde ince ayar kontrolü sunar; bu da birçok açık kaynak kütüphaneye göre üstün bir seçimdir.

## Önkoşullar
- **Java Development Kit (JDK)** 8 veya daha yeni.
- **IDE** (IntelliJ IDEA veya Eclipse gibi).
- **Maven** veya **Gradle** bağımlılık yönetimi için.
- Bir **deneme veya satın alınmış Aspose.Cells lisansı**.

### Gerekli kütüphaneler ve bağımlılıklar
Aspose.Cells Maven artefaktını `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Veya Gradle eşdeğeri:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Lisans edinme adımları
Aspose.Cells for Java ticari bir üründür, ancak ücretsiz deneme ile başlayabilirsiniz. Geçici bir lisans anahtarı almak için [satın alma sayfası](https://purchase.aspose.com/buy) adresini ziyaret edin.

## Aspose.Cells for Java'ı ayarlama
İlk olarak, kütüphanenin sınıf yolunuzda olduğundan emin olun. Bağımlılığı ekledikten sonra, API'yi aşağıda gösterildiği gibi başlatabilirsiniz.

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## Uygulama rehberi

### Bir çalışma kitabı oluşturma ve yapılandırma
`Workbook` sınıfı bellekte bir bütün Excel dosyasını temsil eder.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### Adım 1: bir çalışma kitabı örneği oluşturma
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
Bu, hemen veri eklemeye başlayabileceğiniz yeni, boş bir çalışma kitabı oluşturur.

### Çalışma sayfası hücrelerine erişme veya değiştirme
`Worksheet` çalışma kitabı içinde tek bir sayfayı temsil eder; hücreler, satırlar ve sütunlar içerir.  
Pasta grafiğini besleyecek verileri bir çalışma sayfasına yazacaksınız.

#### Adım 2: ilk çalışma sayfasını ve hücrelerini alın
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
Hücreleri, grafiğin kullanacağı kategori adları ve değerlerle doldurun.

### Bir pasta grafiği oluşturma
`Chart` nesneleri bir çalışma sayfasındaki verileri görselleştirir ve pasta, sütun, çizgi gibi çeşitli türleri destekler.

#### Adım 3: çalışma sayfasına bir pasta grafiği ekleyin
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### Pasta grafiği serilerini ve verilerini yapılandırma
`Series` bir grafiğin veri aralığını ve biçimlendirmesini tanımlar; çalışma sayfası hücrelerini görsel öğelere bağlar.

#### Adım 4: grafiğin serisini ayarlayın
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### Grafik lejand ve başlık görünümünü yapılandırma
Bir grafik `Legend` serilerin adlarını ve renklerini gösterir, okuyucuların her dilimi tanımasını sağlar.

#### Adım 5: grafik lejandını ve başlığını özelleştirin
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### Grafik serisi renklerini özelleştirme
`setAreaColor` bir grafik serisi diliminin dolgu rengini RGB değeriyle ayarlar.

#### Adım 6: pasta dilim renklerini değiştirin
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### Sütunları otomatik sığdırma ve çalışma kitabını kaydetme
`autoFitColumns` sütun genişliklerini hücre içeriğine göre otomatik ayarlar.

#### Adım 7: sütun genişliklerini ayarlayın ve dosyayı kaydedin
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## Yaygın kullanım senaryoları
- **Demografik analiz:** Nüfus dağılımını bölgeler arasında gösterin.
- **Pazar payı raporlaması:** Her rakibin payını tek bakışta görselleştirin.
- **Bütçe tahsisi:** Fonların departmanlar arasında nasıl bölündüğünü vurgulayın.

## Performans hususları
- Artık ihtiyaç duyulmadığında nesneleri (`workbook.dispose()`) serbest bırakın, böylece yerel bellek boşalır.
- Büyük veri setleri için, tüm veriyi bir kerede yüklemek yerine `WorkbookDesigner` kullanarak veri akışı yapın.
- Grafik oluşturmadaki darboğazları tespit etmek için Java Flight Recorder ile profil oluşturun.

## Sıkça sorulan sorular

**S: Aynı çalışma kitabında birden fazla pasta grafiği oluşturabilir miyim?**  
C: Evet, her veri aralığı için grafik oluşturma adımlarını tekrarlayın; her grafik bağımsızdır.

**S: Aspose.Cells 3‑D pasta grafiklerini destekliyor mu?**  
C: Evet; grafik eklerken grafik tipini `ChartType.PIE_3D` olarak ayarlayın.

**S: Tüm grafiklere özel bir tema nasıl uygularım?**  
C: Herhangi bir grafik oluşturmadan önce `Workbook.setDefaultTheme` metodunu kullanın.

**S: Çalışma kitabını hangi dosya formatlarına dışa aktarabilirim?**  
C: XLSX, CSV, PDF ve HTML dahil olmak üzere 30'dan fazla format.

**S: Ticari dağıtım için lisans gerekli mi?**  
C: Evet, geçerli bir lisans değerlendirme filigranlarını kaldırır ve tam işlevselliği açar.

## Sonuç
Aspose.Cells ile **create pie chart java** için eksiksiz, uçtan uca bir tarifiniz artık elinizde. Yukarıdaki adımları izleyerek şık Excel pasta grafikleri oluşturabilir, renk ve başlıkları özelleştirebilir ve bunları herhangi bir raporlama hattına entegre edebilirsiniz. Diğer grafik türlerini—sütun, çizgi, radar—keşfederek veri görselleştirme araç kutunuzu genişletin.

---

**Son Güncelleme:** 2026-09-27  
**Test Edilen Sürüm:** Aspose.Cells 24.10 for Java  
**Yazar:** Aspose

## İlgili Eğitimler

- [Aspose.Cells for Java ile Excel Grafik Veri Etiketlerini Özelleştirme&#58; A Step-by-Step Guide](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Aspose.Cells Java ile Dinamik Excel Grafikler Oluşturma&#58; A Comprehensive Guide for Developers](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Aspose.Cells Java ile Excel Çalışma Kitapları Oluşturma ve Özelleştirme&#58; A Step-by-Step Guide](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}