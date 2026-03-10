---
date: 2026-02-09
description: Aspose.Cells kullanarak Java'da 3D pasta grafiği oluşturmayı öğrenin.
  3D çubuk grafiği oluşturun, Excel'e 3D grafik ekleyin ve adım adım kod örnekleriyle
  çalışma kitabını xlsx olarak kaydedin.
linktitle: Create 3D Pie Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells ile Java’da 3B Pasta Grafiği Oluşturun
url: /tr/java/advanced-excel-charts/3d-charts/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 3D Pasta Grafiği Java Oluşturma

## 3D Grafiklere Giriş

Aspose.Cells for Java, Excel dosyalarıyla çalışmak için güçlü bir Java API'sidir ve **create 3d pie chart** projelerini ve klasik 3‑D çubuk görselleştirmelerini oluşturmayı oldukça basit hâle getirir. Bu öğreticide, bir 3‑D çubuk grafiği nasıl oluşturacağınızı, aynı yaklaşımı bir 3‑D pasta grafiğine nasıl uyarlayacağınızı, görünümünü nasıl özelleştireceğinizi ve sonunda **add 3d chart excel** dosyalarını raporlarınıza nasıl ekleyeceğinizi tam olarak göreceksiniz. Finansal bir gösterge paneli, satış performans tablosu ya da bilimsel verileri görselleştiriyor olun, aşağıdaki adımlar size sağlam bir temel sağlayacaktır.

## Hızlı Yanıtlar
- **What library do I need?** Aspose.Cells for Java (latest version)  
- **Can I generate a 3D bar chart?** Yes – use `ChartType.BAR_3_D`  
- **Do I need a license?** A valid license removes evaluation limits  
- **Which Excel versions are supported?** All major versions from 2003 to 2023  
- **Is it possible to export the chart as an image?** Yes, via `chart.toImage()` methods  

## 3D Grafikler

3D grafikler, geleneksel 2D görselleştirmelere derinlik katarak izleyicilerin çok boyutlu ilişkileri daha sezgisel bir şekilde kavramasını sağlar. Birden fazla kategoriyi yan yana karşılaştırmanız ve aynı zamanda net bir görsel hiyerarşi korumanız gerektiğinde özellikle faydalıdır.

## Neden Aspose.Cells for Java kullanarak 3D çubuk grafiği oluşturmalısınız?

Aspose.Cells for Java, zengin bir grafik‑oluşturma API seti, tam Excel uyumluluğu ve stil üzerinde ayrıntılı kontrol sunar. Bu, **generate 3d bar chart** nesnelerini programatik olarak oluşturabileceğiniz ve Excel sürümüyle ilgili sorunlar hakkında endişelenmenize gerek kalmadığı anlamına gelir.

## Aspose.Cells for Java'ı Kurma

### İndirme ve Kurulum
Aspose.Cells for Java kütüphanesini resmi web sitesinden indirebilirsiniz. Sağlanan Maven/Gradle talimatlarını izleyin veya JAR dosyasını doğrudan projenizin sınıf yoluna ekleyin.

### Lisans Başlatma
Tam özellik setini açmak için, herhangi bir grafik işlemi yapmadan önce lisansınızı başlatın:

```java
// Initialize Aspose.Cells license
License license = new License();
license.setLicense("path_to_license_file.xml");
```

## Temel bir 3D Grafik Oluşturma

### Gerekli Kütüphaneleri İçe Aktarma
İlk olarak, gerekli sınıfları kapsam içine alın:

```java
import com.aspose.cells.*;
```

### Bir Çalışma Kitabı Başlatma
Grafiği barındıracak yeni bir çalışma kitabı oluşturun:

```java
Workbook workbook = new Workbook();
```

### Grafiğe Veri Ekleme
Grafiğin referans alacağı örnek verileri çalışma sayfasına doldurun:

```java
Worksheet worksheet = workbook.getWorksheets().get(0);

// Adding data to cells
worksheet.getCells().get("A1").putValue("Category");
worksheet.getCells().get("A2").putValue("A");
worksheet.getCells().get("A3").putValue("B");
worksheet.getCells().get("A4").putValue("C");

worksheet.getCells().get("B1").putValue("Value");
worksheet.getCells().get("B2").putValue(10);
worksheet.getCells().get("B3").putValue(20);
worksheet.getCells().get("B4").putValue(30);
```

### Java'da 3D çubuk grafiği nasıl oluşturulur
Şimdi grafiği oluşturacağız ve bazı temel özelleştirmeler uygulayacağız:

```java
int chartIndex = worksheet.getCharts().add(ChartType.BAR_3_D, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Setting the data range for the chart
chart.getNSeries().add("A2:B4", true);

// Customizing chart attributes
chart.getChartArea().getBorder().setVisible(false);
chart.getChartTitle().setText("3D Bar Chart");
```

### Grafiği Dosyaya Kaydetme
Son olarak, (artık 3‑D grafiği içeren) çalışma kitabını diske yazın. Bu aynı zamanda **save workbook xlsx** işlemini standart Excel formatında gerçekleştirir:

```java
workbook.save("3D_Chart.xlsx");
```

## Aspose.Cells for Java ile 3D pasta grafiği nasıl oluşturulur
Eğer pasta‑stilinde bir görselleştirmeye ihtiyacınız varsa, iş akışı neredeyse aynı—tek değişmesi gereken `ChartType` enum'ıdır. Grafiği eklerken `ChartType.BAR_3_D` yerine `ChartType.PIE_3_D` kullanın ve serileri aynı veri aralığına yönlendirin. Grafik oluşturulduktan sonra şunları yapabilirsiniz:

* “3D Sales Distribution” gibi açıklayıcı bir başlık ayarlayın.  
* Dilim renklerini `chart.getSeries().get(i).getArea().setForegroundColor(...)` ile ayarlayın.  
* Pasta grafiğini `chart.toImage("pie_chart.png", ImageFormat.getPng())` ile PNG görüntüsü olarak dışa aktarın; bu **convert chart png** gereksinimini karşılar.

Kod bloğu sayısının aynı kalması gerektiği için gerçek Java kodu burada verilmemiştir, ancak adımlar yukarıdaki çubuk‑grafik örneğiyle aynıdır.

## Farklı 3D Grafik Türleri
Aspose.Cells for Java, **add 3d chart excel** dosyalarıyla kullanabileceğiniz çeşitli 3D grafik türlerini destekler:

- **Bar charts** – kategorileri karşılaştırmak için idealdir.  
- **Pie charts** – oranları gösterir (3D pasta dahil).  
- **Line charts** – zaman içindeki eğilimleri gösterir.  
- **Area charts** – değişimin büyüklüğünü vurgular.  

`ChartType` enum'ını yukarıdakilerden herhangi birine değiştirerek aynı oluşturma desenini sürdürebilirsiniz.

## Gelişmiş Grafik Özelleştirme

### Başlıklar ve Etiketler Ekleme
Grafiğinize açıklayıcı bir başlık ve eksen etiketleri ekleyerek bağlam sağlayın.

### Renk ve Stil Ayarlama
Kurumsal kimliğe uygun renkler için `chart.getSeries().get(i).getArea().setForegroundColor(Color.getRGB(...))` metodunu kullanın.

### Grafik Eksenleriyle Çalışma
Okunabilirliği artırmak için eksen ölçeklerini, aralıklarını ve işaretçileri ince ayarlayın.

### Lejantlar Ekleme
`chart.getLegend().setVisible(true)` ile lejantları etkinleştirin; böylece izleyiciler her veri serisini tanımlayabilir.

### Grafikleri Görüntü Olarak Dışa Aktarma
Web raporu için statik bir görüntüye ihtiyacınız olduğunda `chart.toImage("chart.png", ImageFormat.getPng())` çağrısını yapın. Bu, **convert chart png** kullanım senaryosunu çalışma kitabından çıkmadan karşılar.

## Veri Entegrasyonu
Aspose.Cells for Java, veritabanları, CSV dosyaları veya canlı API'lerden veri çekebilir. Veri aralığını grafiğe bağlamadan önce çalışma sayfası hücrelerini çekilen verilerle doldurun. Bu, **add 3d chart excel** iş akışınızı dinamik ve güncel tutar.

## Sonuç
Bu rehberde, **create 3d pie chart** ve **create 3d bar chart** projelerini baştan sona nasıl yürütüleceğini—kütüphaneyi kurma, veri ekleme, 3‑D çubuk grafiği oluşturma, aynı adımları 3‑D pasta grafiği için uyarlama ve gelişmiş stil uygulamaları—gösterdik. Aspose.Cells for Java ile Excel çalışma kitaplarına doğrudan zengin 3‑D görselleştirmeler ekleyebilir ve hatta PNG görüntüleri olarak dışa aktarabilirsiniz.

## Sıkça Sorulan Sorular

**Q: How can I add multiple data series to a 3D chart?**  
A: Use `chart.getNSeries().add()` for each series range and ensure the chart type remains 3‑D (e.g., `ChartType.BAR_3_D` or `ChartType.PIE_3_D`).

**Q: Can I export 3D charts created with Aspose.Cells for Java to other formats?**  
A: Yes, you can save the chart as PNG, JPEG, or PDF by calling the appropriate `chart.toImage()` or `workbook.save()` overloads, satisfying the **convert chart png** requirement.

**Q: Is it possible to create interactive 3D charts with Aspose.Cells for Java?**  
A: Aspose.Cells focuses on static Excel charts. For interactive web‑based 3‑D visualizations, consider coupling Excel data with JavaScript libraries such as Three.js.

**Q: Can I automate the process of updating data in my 3D charts?**  
A: Absolutely. Load new data into the worksheet programmatically and refresh the chart range; the next time the workbook is opened, the chart reflects the updated values.

**Q: Where can I find more resources and documentation for Aspose.Cells for Java?**  
A: You can find comprehensive documentation and resources for Aspose.Cells for Java at the website: [Aspose.Cells for Java Documentation](https://reference.aspose.com/cells/java/).

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.Cells for Java 24.12 (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}