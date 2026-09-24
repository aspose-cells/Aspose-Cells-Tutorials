---
date: '2026-04-11'
description: Aspose.Cells ile Excel otomasyonunu Java öğrenin. Bu öğreticide, Excel
  çalışma kitabını Java ile nasıl oluşturacağınızı, Excel verilerini Java ile nasıl
  dolduracağınızı ve grafikleri içeren Excel dosyasını Java ile nasıl kaydedeceğinizi
  gösterir.
keywords:
- excel automation java
- create excel workbook java
- save excel file java
- populate excel data java
- aspose cells java
title: 'Excel Otomasyonu Java: Aspose Kullanarak Çalışma Kitapları ve Grafikler Oluşturma'
url: /tr/java/charts-graphs/aspose-cells-java-excel-workbook-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel Otomasyonu Java: Aspose ile Çalışma Kitapları ve Grafikler Oluşturma

## Giriş

Java ile Excel görevlerini otomatikleştirmek, özellikle raporlar, gösterge panelleri veya veri odaklı grafikler anında oluşturmanız gerektiğinde saatlerce süren manuel çalışmayı tasarruf ettirebilir. **Excel automation java** ile Aspose.Cells, çalışma kitabı oluşturulmasından gelişmiş grafik stiline kadar her şeyi yöneten temiz, yüksek performanslı bir API sunar. Bu öğreticide Aspose.Cells'i nasıl kuracağınızı, **Java ile bir Excel çalışma kitabı oluşturma**, verilerle doldurmayı, bir grafik eklemeyi, 3‑D biçimlendirme uygulamayı ve sonunda **Java ile Excel dosyasını kaydetme** öğreneceksiniz.

### Hızlı Yanıtlar
- **Java'da Excel otomasyonunu basitleştiren kütüphane hangisidir?** Aspose.Cells for Java.  
- **Programlı olarak 3‑D grafikler ekleyebilir miyim?** Evet – API 3‑D biçimlendirme ve ışıklandırma efektlerini destekler.  
- **Geliştirme için lisansa ihtiyacım var mı?** Ücretsiz deneme lisansı mevcuttur; üretim için ticari lisans gereklidir.  
- **Hangi Java yapı araçları destekleniyor?** Maven ve Gradle tamamen desteklenir.  
- **Hangi dosya formatlarını dışa aktarabilirim?** XLS, XLSX, CSV, PDF ve daha fazlası.

## Excel otomasyonu java nedir?

Excel automation java, Java kodu kullanarak Excel çalışma kitaplarını programlı bir şekilde oluşturma, değiştirme ve kaydetme sürecine denir. Manuel elektronik tablo düzenlemelerini ortadan kaldırır, tutarlılığı sağlar ve veritabanları veya web hizmetleri gibi diğer sistemlerle entegrasyonu mümkün kılar.

## Neden Aspose.Cells for Java kullanmalısınız?

- **Zengin özellik seti** – basit hücre değerlerinden karmaşık grafiklere, pivot tablolarına ve koşullu biçimlendirmeye kadar.  
- **Microsoft Office bağımlılığı yok** – herhangi bir sunucu‑tarafı ortamında çalışır.  
- **Yüksek performans** – büyük veri setleri ve çok iş parçacıklı senaryolar için optimize edilmiştir.  
- **Geniş format desteği** – XLS, XLSX, ODS, CSV, PDF, HTML ve daha fazlasını okur/yazar.

## Önkoşullar

- **Java Development Kit (JDK) 8+**  
- **Maven veya Gradle** bağımlılık yönetimi için  
- **Aspose.Cells for Java 25.3 veya sonrası** (deneme veya lisanslı)  

## Aspose.Cells for Java'ı Kurma

Projenize kütüphaneyi aşağıdaki yapılandırmalardan birini kullanarak ekleyin.

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Lisans Alımı

Aspose web sitesinden ücretsiz bir deneme lisansı isteyin veya üretim kullanımı için tam bir lisans satın alın. Lisans dosyasını projenize yerleştirin ve çalışma zamanında yükleyin.

## Temel Başlatma ve Kurulum

Bağımlılık çözüldükten sonra kodlamaya başlayabilirsiniz.

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        // Initialize a new Workbook object
        Workbook book = new Workbook();
        System.out.println("Workbook initialized successfully.");
    }
}
```

## Adım‑Adım Kılavuz

### Adım 1: Java ile Excel çalışma kitabı nasıl oluşturulur

Tüm çalışma sayfalarınızı tutacak yeni bir çalışma kitabı örneği oluşturun.

```java
import com.aspose.cells.Workbook;
// Initialize a new Workbook object
Workbook book = new Workbook();
```

### Adım 2: Çalışma sayfaları ekleyin (grafik sayfası dahil)

```java
import com.aspose.cells.Worksheet;
Worksheet dataSheet = book.getWorksheets().add("DataSheet");
Worksheet chartSheet = book.getWorksheets().add("MyChart");
System.out.println("Worksheets added successfully.");
```

### Adım 3: Java ile Excel verilerini nasıl doldurulur

Grafiğin referans alacağı örnek verileri ekleyin.

```java
import com.aspose.cells.Cells;
Cells cells = dataSheet.getCells();
cells.get("B1").putValue(1);
cells.get("B2").putValue(2);
cells.get("B3").putValue(3);
cells.get("A1").putValue("A");
cells.get("A2").putValue("B");
cells.get("A3").putValue("C");
System.out.println("Data populated successfully.");
```

### Adım 4: Çalışma kitabına bir sütun grafiği ekleyin

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartCollection;
import com.aspose.cells.ChartType;
ChartCollection charts = chartSheet.getCharts();
charts.add(ChartType.COLUMN, 5, 0, 25, 15);
Chart chart = book.getWorksheets().get(2).getCharts().get(0);
System.out.println("Chart added successfully.");
```

### Adım 5: Grafik alanına renk biçimlendirmesi uygulayın

```java
import com.aspose.cells.Color;
chart.getPlotArea().getArea().setBackgroundColor(Color.getWhite());
chart.getChartArea().getArea().setBackgroundColor(Color.getWhite());
chart.getPlotArea().getArea().setForegroundColor(Color.getWhite());
chart.getChartArea().getArea().setForegroundColor(Color.getWhite());
System.out.println("Color formatting applied successfully.");
```

### Adım 6: Lejant ve veri serilerini yapılandırın

```java
import com.aspose.cells.Series;
chart.setShowLegend(false);
chart.getNSeries().add("DataSheet!B1:B3", true);
chart.getNSeries().setCategoryData("DataSheet!A1:A3");
Series ser = chart.getNSeries().get(0);
System.out.println("Chart series configured successfully.");
```

### Adım 7: Serilere 3D biçimlendirme uygulayın

```java
import com.aspose.cells.Bevel;
import com.aspose.cells.BevelPresetType;
import com.aspose.cells.Format3D;
import com.aspose.cells.LightRigType;
import com.aspose.cells.PresetMaterialType;
import com.aspose.cells.ShapePropertyCollection;
ShapePropertyCollection spPr = ser.getShapeProperties();
Format3D fmt3d = spPr.getFormat3D();

Bevel bevel = fmt3d.getTopBevel();
bevel.setType(BevelPresetType.CIRCLE);
bevel.setHeight(5);
bevel.setWidth(9);
fmt3d.setSurfaceMaterialType(PresetMaterialType.WARM_MATTE);
fmt3d.setSurfaceLightingType(LightRigType.THREE_POINT);
fmt3d.setLightingAngle(20);
System.out.println("3D formatting applied successfully.");
```

### Adım 8: Daha iyi görsel ayrım için seri renklerini ayarlayın

```java
ser.getArea().setBackgroundColor(Color.getMaroon());
ser.getArea().setForegroundColor(Color.getMaroon());
ser.getBorder().setColor(Color.getMaroon());
System.out.println("Series color formatting applied successfully.");
```

### Adım 9: Java ile Excel dosyasını nasıl kaydedilir

```java
book.save(outDir + "A3DFormat_out.xls");
System.out.println("Workbook saved successfully.");
```

## Pratik Uygulamalar

- **Finansal Raporlama** – Dinamik grafiklerle çeyrek dönem beyanları oluşturun.  
- **Veri Analizi Gösterge Panelleri** – Otomatik yenilenen etkileşimli gösterge panelleri oluşturun.  
- **Envanter Yönetimi** – Stok seviyelerini ve trendleri Excel'e dışa aktararak paydaşların incelemesi için.  
- **Proje Planlaması** – Java tabanlı zamanlama sistemlerinden doğrudan Gantt‑stil grafikler oluşturun.

## Excel Otomasyonu Java için Performans İpuçları

- **Çalışma Kitabı Nesnelerini Yeniden Kullan** birden fazla sayfa işlenirken bellek tüketimini azaltmak için.  
- **Toplu Hücre Güncellemeleri** büyük veri setleri için `Cells.importArray` kullanın, tek tek `putValue` çağrıları yerine.  
- **Kaynakları Serbest Bırak** büyük dosyaları kaydettikten sonra `book.dispose()` çağırarak.

## Sıkça Sorulan Sorular

**S: XLS yerine XLSX oluşturabilir miyim?**  
C: Evet – sadece `book.save("output.xlsx")` içinde dosya uzantısını değiştirin; Aspose otomatik olarak doğru formatı seçer.

**S: Geliştirme için lisans gerekli mi?**  
C: Ücretsiz deneme lisansı geliştirme ve test için çalışır. Üretim dağıtımları için satın alınmış bir lisans gerekir.

**S: Daha fazla grafik türü nasıl eklenir?**  
C: `ChartType` enum (ör. `ChartType.PIE`, `ChartType.LINE`) kullanarak `charts.add(...)` çağrısında.

**S: Çalışma kitabını korumam gerekirse?**  
C: Kaydetmeden önce `book.getSettings().setPassword("yourPassword")` çağırın.

**S: Aspose.Cells makro‑etkin dosyaları destekliyor mu?**  
C: Evet – XLSM çalışma kitaplarında VBA makrolarını oluşturabilir veya koruyabilirsiniz.

**Last Updated:** 2026-04-11  
**Tested With:** Aspose.Cells 25.3 (Java)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}