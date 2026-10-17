---
date: '2026-10-17'
description: Aspose.Cells kullanarak Java'da Excel chart data labels şeklini nasıl
  ayarlayacağınızı öğrenin. Bu rehber, Excel chart labels'ı hızlı ve verimli bir şekilde
  nasıl değiştireceğinizi gösterir.
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Aspose.Cells kullanarak Java'da Excel chart data labels şeklini nasıl
  ayarlayacağınızı öğrenin. Bu adım adım rehber, Excel chart labels'ı hızlı bir şekilde
  değiştirmenize yardımcı olur.
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Java'da Excel chart data labels şeklini nasıl ayarlarsınız
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Java'da Excel chart data labels şeklini nasıl ayarlarsınız
url: /tr/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Aspose.Cells'te grafik özelleştirmeyi ustalaştırma: veri etiketi şekillerini değiştirme

## Giriş

Excel grafiklerinin görsel çekiciliğini artırmak, raporlar veya panolar hazırlarken, özellikle Java kullanıyorsanız, çok önemlidir. Aspose.Cells—tablo yönetimi ve manipülasyonu için güçlü bir kütüphane—ile **şekli nasıl ayarlayacağınızı** sadece birkaç satır kodla gerçekleştirebilirsiniz. Bu öğretici, Aspose.Cells for Java kullanarak bir Excel grafiğinde veri etiketlerinin şeklini değiştirmeyi size gösterecek. Sonunda şunları öğreneceksiniz:

- Grafik veri etiketlerine erişme ve bunları değiştirme
- Veri etiketleri için özel şekiller ayarlama
- Çalışma kitabınızdaki değişiklikleri kaydetme

## Hızlı cevaplar
- **Excel dosyalarıyla çalışmak için birincil sınıf nedir?** `Workbook` represents an entire Excel file in memory.  
- **Etiket şekli hangi yöntemle ayarlanır?** `setShapeType(DataLabelShapeType shape)` on a `DataLabel` object.  
- **Geliştirme için lisansa ihtiyacım var mı?** Ücretsiz geçici bir lisans değerlendirme için çalışır; üretim için tam lisans gereklidir.  
- **Şekli birden fazla seriye uygulayabilir miyim?** Evet—her seriyi döngüyle işleyip `setShapeType` metodunu çağırın.  
- **Bu yaklaşım büyük çalışma kitaplarıyla uyumlu mu?** Aspose.Cells, tüm dosyayı belleğe yüklemeden çok sayfalı çalışma kitaplarını işler.

## Şekli nasıl ayarlayacağınız nedir?
**Şekli nasıl ayarlayacağınız** ifadesi, bir grafiğin veri etiketinin görsel çerçevesini, örneğin düz bir dikdörtgeni bir balon ya da elips haline getirmeyi ifade eder. Şekli değiştirmek okunabilirliği artırır ve önemli veri noktalarını vurgular. Uygun bir şekil seçerek etiketi öne çıkarabilir, ilgili noktaları gruplayabilir veya kurumsal marka yönergelerine uyum sağlayarak grafiğin genel okunabilirliğini iyileştirebilirsiniz.

## Neden Aspose.Cells'i grafik etiketi özelleştirmesi için kullanmalısınız?
Aspose.Cells **50+ giriş ve çıkış formatını**—XLSX, CSV, ODS, PDF dahil—destekler ve **1 milyon satıra kadar** çalışma kitaplarını bellek tüketmeden işleyebilir. API'si, grafikleri programlı olarak değiştirmenize olanak tanır, manuel Excel düzenlemelerine gerek kalmaz ve otomatik raporların stil tutarlılığını sağlar.

## Önkoşullar

- **Aspose.Cells for Java Library**: Version 25.3 or later is required.
- **Java Development Environment**: JDK installed on your machine.
- **IDE Setup**: IntelliJ IDEA veya Eclipse gibi bir IDE kullanarak kodunuzu yazın ve çalıştırın.

### Gerekli kütüphaneler ve bağımlılıklar

Maven kullanıcıları için aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Gradle kullanıcıları ise bu satırı `build.gradle` dosyasına eklemelidir:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Lisans edinme

Aspose.Cells, ücretsiz bir deneme lisansı sunar; bu lisansı [Aspose temporary license page](https://purchase.aspose.com/temporary-license/) adresinden edinebilirsiniz. Bu lisans, sınırlı bir süre için tüm özelliklere tam erişim sağlar.

## Aspose.Cells'i Java için kurma

Ortamınız hazır olduğunda, Aspose.Cells'i kurmaya başlayalım:

### Kurulum adımları

1. **Kütüphaneyi indirin**: Yukarıda gösterildiği gibi Maven veya Gradle kullanın.  
2. **Lisans yapılandırması**:  
   - `License` sınıfı, Aspose.Cells lisans dosyanızı tam işlevsellik için uygular.  
   - `Workbook` nesnesini başlattıktan sonra aşağıdaki kod parçacığını kullanarak geçici bir lisans indirin ve uygulayın:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **Temel başlatma**: Excel dosyalarıyla çalışmaya başlamak için bir `Workbook` örneği oluşturun.

## Bir grafikte veri etiketlerinin şeklini nasıl ayarlarsınız?

Çalışma kitabınızı yükleyin, hedef grafiği bulun ve veri etiketlerine istediğiniz şekli uygulayın. Aşağıdaki adımlar bir dakikadan kısa sürede bu işlemi gerçekleştirir.

### Adım adım kılavuz

#### Adım 1: Çalışma kitabınızı yükleyin

`Workbook` sınıfı, Aspose.Cells'in bellekte tek bir Excel dosyasını temsil eden üst‑seviye nesnesidir. `new Workbook("input.xlsx")` koduyla değiştirmek istediğiniz dosyayı yükleyin.

#### Adım 2: Grafiğe erişin

`Worksheet` bir çalışma kitabındaki tek bir sayfayı temsil eder.  
`Worksheet ws = workbook.getWorksheets().get(0);` ilk çalışma sayfasını alır.  
`Chart` ise bir çalışma sayfasına gömülü grafiği temsil eder.  
`Chart chart = ws.getCharts().get(0);` o sayfadaki ilk grafiği elde eder.

#### Adım 3: Serileri alın ve veri etiketlerini değiştirin

`Series` bir grafikte çizilen veri serisini temsil eder.  
Her `Series` nesnesi bir `DataLabel` koleksiyonu içerir.  
`DataLabel` bir serinin veri etiketinin görünümünü kontrol eder.  
`DataLabelShapeType` veri etiketleri için olası şekillerin bir enum'udur.  
`series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` koduyla şekli ayarlayın. Enum, `RECTANGLE`, `CLOUD` ve `WEDGE_ELLIPSE_CALLOUT` gibi onlarca seçenek sunar.

#### Adım 4: Çalışma kitabınızı kaydedin

Şekli uyguladıktan sonra `workbook.save("output.xlsx");` koduyla değişiklikleri diske yazın.

## Sorun giderme ipuçları

- **Dosya yolu sorunları**: Dosya yolunun mutlak ya da proje çalışma dizinine göre doğru göreli olduğundan emin olun.  
- **Kütüphane sürüm uyumsuzluğu**: Aspose.Cells sürüm 25.3 veya üzeri kullandığınızdan emin olun; eski sürümlerde `setShapeType` metodu bulunmaz.  
- **Desteklenmeyen grafik türleri**: Bazı eski grafik türleri (ör. radar) veri etiketi şekli özelliklerini ortaya koymayabilir; sütun ya da çizgi gibi desteklenen bir grafik türüne geçin.

## Pratik uygulamalar

1. **Finansal raporlama** – Kâr marjlarını balon‑stil etiketlerle vurgulayın.  
2. **Eğitim içeriği** – Bulut‑şeklinde etiketler kullanarak öğretim materyallerindeki önemli veri noktalarına dikkat çekin.  
3. **Pazarlama analitiği** – Gösterge panolarında kampanya performans metriklerini ayırt etmek için özel şekiller uygulayın.

Aspose.Cells'i veri akışları veya CRM sistemleriyle entegre ederek tamamen biçimlendirilmiş raporlar otomatik olarak oluşturabilir, manuel çabayı azaltabilir ve marka tutarlı görseller sağlayabilirsiniz.

## Performans değerlendirmeleri

Büyük Excel dosyalarıyla çalışırken:

- **Bellek kullanımını optimize edin**: Kaydetme sonrası `workbook.dispose();` çağırarak yerel kaynakları hemen serbest bırakın.  
- **Toplu işleme**: Nesne oluşturma yükünü azaltmak için grafikleri tek tek değil, gruplar halinde işleyin.  
- **Verimli veri işleme**: Binlerce satırı döngü içinde ağır hesaplamalardan kaçının; değerleri önceden hesaplayın.

## Sonuç

Artık Java'da Aspose.Cells kullanarak Excel grafik veri etiketlerinin **şekli nasıl ayarlayacağınızı** biliyorsunuz. Bu yetenek, grafik estetiğini artırmakla kalmaz, aynı zamanda son kullanıcıların veri anlayışını da geliştirir. Etiket renkleri, yazı tipleri ve lider çizgileri gibi ek özelleştirme seçeneklerini keşfederek görselleştirmelerinizi daha da iyileştirebilirsiniz.

Herhangi bir sorunuz veya desteğe ihtiyacınız olursa, [Aspose support forum](https://forum.aspose.com/c/cells/9) adresine başvurun.

## Sıkça sorulan sorular

**Q: Birden fazla veri etiketinin şeklini aynı anda nasıl değiştiririm?**  
A: Grafikteki her seriyi döngüyle işleyin ve serinin `DataLabel` nesnesi üzerinde `setShapeType` metodunu çağırın.

**Q: Aspose.Cells for Java büyük Excel dosyalarını verimli bir şekilde işleyebilir mi?**  
A: Evet. Doğru bellek yönetimiyle, tüm dosyayı belleğe yüklemeden yüz binlerce satır içeren çalışma kitaplarını işleyebilir.

**Q: Aspose.Cells'i kurarken sık karşılaşılan sorunlar nelerdir?**  
A: Maven bağımlılıklarının eksik olması, eski bir kütüphane sürümü kullanılması veya geçersiz bir lisans dosyası sağlanması tipik problemler arasındadır.

**Q: Veri etiketi şekillerini varsayılan hâle geri döndürmenin bir yolu var mı?**  
A: `DataLabelShapeType.DEFAULT` değerini ayarlayarak orijinal görünümü geri getirebilirsiniz.

**Q: Bu özelleştirmeyi bir çalışma kitabındaki birden fazla grafiğe nasıl uygularım?**  
A: `ws.getCharts()` üzerinden döngü kurarak her grafiğin serileri için aynı `setShapeType` mantığını uygulayın.

## Kaynaklar

- [Aspose.Cells Belgeleri](https://reference.aspose.com/cells/java/)
- [Aspose.Cells for Java'ı İndirin](https://releases.aspose.com/cells/java/)
- [Lisans Satın Alın](https://purchase.aspose.com/buy)
- [Ücretsiz Deneme Lisansı](https://releases.aspose.com/cells/java/)
- [Geçici Lisans](https://purchase.aspose.com/temporary-license/)

---  

**Son Güncelleme:** 2026-10-17  
**Test Edilen Versiyon:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## İlgili Eğitimler

- [Modify Excel Chart Data Labels Using Aspose.Cells Java](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [How to Resize Labels in Excel Charts with Aspose.Cells for Java](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Add Labels to Excel Charts with Aspose Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}