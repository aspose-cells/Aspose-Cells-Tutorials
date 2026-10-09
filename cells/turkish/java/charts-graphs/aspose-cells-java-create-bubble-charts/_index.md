---
date: '2026-04-02'
description: Aspose.Cells for Java kullanarak nasıl grafik oluşturulur ve Excel balon
  grafiği üretilir öğrenin. Bu rehber, kurulum, veri ve grafiğin kaydedilmesi adımlarını
  size gösterir.
keywords:
- how to create chart
- generate excel bubble chart
- set bubble chart data
title: 'Grafik Nasıl Oluşturulur: Aspose.Cells Java ile Excel Balon Grafiği'
url: /tr/java/charts-graphs/aspose-cells-java-create-bubble-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Grafik Oluşturma: Aspose.Cells Java ile Excel Balon Grafiği

Aspose.Cells for Java kullanarak dinamik balon grafiklerle Excel raporlarınızı geliştirin. Bu öğreticide, verileri balon grafik olarak görselleştiren **grafik oluşturma** nesnelerini öğreneceksiniz, bu da sunumlarınızı daha içgörülü ve etkileşimli hâle getirir. Geliştirme ortamını kurmaktan grafik verilerini yapılandırmaya ve sonunda çalışma kitabını kaydetmeye kadar her adımı adım adım göstereceğiz.

## Hızlı Yanıtlar
- **Java'da Excel grafikler için en iyi kütüphane hangisidir?** Aspose.Cells for Java.
- **Programlı olarak bir Excel balon grafiği oluşturabilir miyim?** Evet, aşağıda gösterilen grafik API'si kullanılarak.
- **Kodu çalıştırmak için lisansa ihtiyacım var mı?** Ücretsiz deneme çalışır, ancak tam lisans tüm özelliklerin kilidini açar.
- **Hangi Java yapı araçları destekleniyor?** Maven ve Gradle her ikisi de desteklenir.
- **Balon grafiği verilerini ayarlamak için temel yöntem nedir?** Seride `setBubbleSizes`, `setXValues` ve `setValues` kullanın.

## Balon Grafiği Nedir?
Balon grafiği, her veri noktasının bir balonla temsil edildiği bir dağılım grafiği çeşididir. X‑ekseni ve Y‑ekseni konumu belirlerken, balon boyutu üçüncü bir bilgi boyutunu iletir—finansal, satış veya bilimsel verileri görselleştirmek için mükemmeldir.

## Neden Aspose.Cells for Java Kullanmalı?
- **Sıfır‑kurulum Excel motoru** – sunucuda Microsoft Office gerekmez.
- **Zengin grafik API'si** – balon grafikler dahil tüm modern grafik türlerini destekler.
- **Çapraz‑platform** – Windows, Linux ve macOS'ta çalışır.
- **Yüksek performans** – büyük veri setleri ve yüksek hacimli rapor üretimi için optimize edilmiştir.

## Ön Koşullar
Aspose.Cells for Java kullanarak balon grafikler oluşturmak için aşağıdaki ön koşulları karşıladığınızdan emin olun:

### Gerekli Kütüphaneler ve Bağımlılıklar
- **Aspose.Cells for Java**: En son sürümü (ör. 25.3) kurun.

### Ortam Kurulum Gereksinimleri
- Uyumlu Java Development Kit (JDK) yüklü.
- Projenizi Maven veya Gradle kullanacak şekilde yapılandırın.

### Bilgi Ön Koşulları
- Java programlamaya temel bir anlayış.
- Excel dosya yapıları ve grafik türleri hakkında aşinalık.

## Aspose.Cells for Java Kurulumu
Ortamınızı kurmak çok önemlidir. İşte nasıl başlayabileceğiniz:

### Maven ile Kurulum
Aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle ile Kurulum
Gradle kullananlar için, bunu `build.gradle` dosyanıza ekleyin:
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Lisans Edinme
Aspose.Cells sınırlı işlevsellikte ücretsiz bir deneme sunar. Tam yetenekler için:
- **Satın Al**: Lisans seçenekleri için [satın alma sayfasını](https://purchase.aspose.com/buy) ziyaret edin.
- **Geçici Lisans**: Tam test için geçici lisansı [buradan](https://purchase.aspose.com/temporary-license/) edinin.

### Temel Başlatma
Aspose.Cells'i kullanmadan önce, Java projenizde başlatın:
```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook object
Workbook workbook = new Workbook();
```

## Uygulama Kılavuzu
Aspose.Cells ile balon grafiklerin oluşturulması ve yapılandırılması sürecini adım adım inceleyelim:

### Grafik Oluşturma: Workbook Nesnesi Başlatma
`Workbook`, tüm bir Excel dosyasını temsil eder ve sayfalar, hücreler vb. üzerinde işlem yapmanıza olanak tanır. Aşağıdaki gibi başlatın:
```java
import com.aspose.cells.Workbook;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

### Balon Grafiği Verilerini Ayarlama: Çalışma Sayfalarına Erişim ve Manipülasyon
Balon grafiğine veri sağlayacak verileri hazırlayın:
```java
import com.aspose.cells.WorksheetCollection;
import com.aspose.cells.Cells;
import com.aspose.cells.Cell;

// Get the collection of worksheets
WorksheetCollection worksheets = workbook.getWorksheets();
Worksheet sheet = worksheets.get(0);
Cells cells = sheet.getCells();

// Set values in specific cells to prepare data for charting
cells.get("A1").setValue(50);
cells.get("A2").setValue(100);
cells.get("A3").setValue(150);
cells.get("B1").setValue(4);
cells.get("B2").setValue(20);
cells.get("B3").setValue(180);
cells.get("C1").setValue(320);
cells.get("C2").setValue(110);
cells.get("C3").setValue(180);
cells.get("D1").setValue(40);
cells.get("D2").setValue(120);
cells.get("D3").setValue(250);
```

### Excel Balon Grafiği Oluşturma: Grafik Oluşturma ve Yapılandırma
Çalışma sayfasına ekleyerek ve veri kaynaklarını ayarlayarak bir balon grafiği oluşturun:
```java
import com.aspose.cells.ChartCollection;
import com.aspose.cells.Chart;
import com.aspose.cells.SeriesCollection;
import com.aspose.cells.ChartType;

// Access the collection of charts in the sheet
ChartCollection charts = sheet.getCharts();
int chartIndex = charts.add(ChartType.BUBBLE, 5, 0, 15, 5);
Chart chart = charts.get(chartIndex);

// Add series to the chart and set data sources
SeriesCollection serieses = chart.getNSeries();
serieses.add("A1:B3", true);

// Set bubble sizes, X values, and Y values for the chart
chart.getNSeries().get(0).setBubbleSizes("B2:D2");
chart.getNSeries().get(0).setXValues("B3:D3");
chart.getNSeries().get(0).setValues("B1:D1");
```

### Grafiği Kaydetme: Workbook'u Kaydetme
Workbook'u (ve gömülü grafiği) diske kaydedin:
```java
import com.aspose.cells.SaveFormat;

// Define the directory to save the file
String dataDir = "YOUR_DATA_DIRECTORY";
workbook.save(dataDir + "/HToCrBChart_out.xls", SaveFormat.EXCEL_97_TO_2003);
```

## Pratik Uygulamalar
- **Finansal Raporlama** – Gelir, kar ve pazar payını tek bir görünümde görselleştirin.
- **Satış Veri Analizi** – Bölgesel satış performansını vurgulayın, balon boyutu hacmi gösterir.
- **Bilimsel Araştırma** – Deneysel sonuçları aynı anda üç değişkenle gösterin.

## Performans Düşünceleri
- Kullanılmayan nesneleri hemen serbest bırakın, böylece bellek boşalır.
- Veri aralıklarını mümkün olduğunca dar tutun; gereksiz büyük aralıklar render süresini yavaşlatabilir.
- Büyük veri setlerini işlerken Java’nın bellek yönetimi en iyi uygulamalarını kullanın.

## Yaygın Sorunlar ve Çözümler
| Sorun | Neden | Çözüm |
|-------|-------|----------|
| **Boş grafik** | Veri aralıkları serilerle eşleşmiyor | `setBubbleSizes`, `setXValues` ve `setValues`'ın doğru hücrelere referans verdiğini doğrulayın. |
| **Yanlış balon boyutları** | Aralık uzunlukları eşleşmiyor | Üç aralığın da aynı sayıda nokta içerdiğinden emin olun. |
| **Lisans istisnası** | Geçerli bir lisans olmadan çalıştırma | Workbook oluşturulmadan önce geçici veya satın alınmış bir lisans uygulayın. |

## Sıkça Sorulan Sorular

**Q: Aspose.Cells'in minimum sürümü nedir?**  
A: Bu öğreticide tüm gösterilen özelliklerle uyumluluğu sağlamak için 25.3 sürümü önerilir.

**Q: Balon grafiği renklerini nasıl özelleştirebilirim?**  
A: Serinin biçimlendirme yöntemlerini kullanın, örneğin `chart.getNSeries().get(0).getArea().getFillFormat().setForeColor(Color.getRed())`.

**Q: Bu kodu Linux sunucularında çalıştırabilir miyim?**  
A: Evet, Aspose.Cells for Java tamamen çapraz platformdur ve uyumlu bir JDK'ya sahip herhangi bir işletim sisteminde çalışır.

**Q: “Veri kaynağı boyut uyuşmazlığı” hatası alırsam ne yapmalıyım?**  
A: Balon boyutları, X değerleri ve Y değerleri için aralıkların aynı sayıda hücre içerdiğini iki kez kontrol edin.

**Q: Test için geçici bir lisans nereden alabilirim?**  
A: Deneme lisansı talep etmek için [Aspose'un geçici lisans sayfasını](https://purchase.aspose.com/temporary-license/) ziyaret edin.

## Kaynaklar
- **Dokümantasyon**: Daha fazla detay için [resmi dokümantasyona](https://reference.aspose.com/cells/java/) bakın.
- **İndirme**: En son sürümü [sürüm sayfasından](https://releases.aspose.com/cells/java/) alın.
- **Satın Alma**: Lisans seçeneklerini [bu sayfada](https://purchase.aspose.com/buy) keşfedin.
- **Ücretsiz Deneme**: Özellikleri test etmek için [Aspose'un sürüm bölümünde](https://releases.aspose.com/cells/java/) ücretsiz deneme ile başlayın.
- **Destek Forumu**: Herhangi bir sorunuz için [destek forumu](https://forum.aspose.com/c/cells/9) mevcuttur.

---

**Son Güncelleme:** 2026-04-02  
**Test Edilen Versiyon:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}