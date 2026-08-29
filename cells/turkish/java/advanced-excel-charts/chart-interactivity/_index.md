---
date: 2026-08-21
description: Aspose.Cells for Java kullanarak Excel grafiklerine araç ipuçları, veri
  etiketleri eklemeyi ve grafik tipini değiştirmeyi öğrenin – etkileşimli örneklerle
  adım adım kılavuz.
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Excel Grafik Tipini Değiştir
og_description: Aspose.Cells for Java kullanarak Excel grafiklerine araç ipuçları,
  veri etiketleri eklemeyi ve grafik tipini değiştirmeyi öğrenin – etkileşimli örneklerle
  adım adım kılavuz.
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Java'da Excel grafiklerine araç ipuçları ve veri etiketleri ekleme
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Java'da Excel grafiklerine araç ipuçları ve veri etiketleri ekleme
url: /tr/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel grafiğine veri etiketleri ekleyin ve grafik tipini değiştirin – Aspose.Cells Java

Etkileşimli grafikler Excel raporlarınıza yeni bir içgörü seviyesi kazandırır ve **araç ipuçları ekleme** bilgiyi anında okunabilir hâle getirir. Bu öğreticide **Excel grafiğine veri etiketleri ekleme**, **grafik tipini değiştirme** ve Aspose.Cells ile etkileşimli Java çözümleri oluşturmayı öğreneceksiniz. Ayrıca araç ipuçları eklemeyi ve izleyicilerinizin veriyi derinlemesine keşfetmesi için basit bir drill‑down (derinlemesine) hiperlinki nasıl ekleyeceğinizi de göstereceğiz.

## Hızlı yanıtlar
- **Hangi kütüphane kullanılıyor?** Aspose.Cells for Java  
- **Grafik tipini değiştirebilir miyim?** Evet – grafiği oluştururken `ChartType` enum değerini değiştirmeniz yeterlidir.  
- **Bir grafiğe araç ipuçları nasıl eklenir?** Veri‑etiket API'sini (`setHasDataLabels(true)`) kullanın ve değer gösterimini etkinleştirin.  
- **Drill‑down destekleniyor mu?** Veri noktalarına hiperlink ekleyerek temel drill‑down davranışı sağlayabilirsiniz.  
- **Önkoşullar?** Java IDE, Aspose.Cells JAR ve örnek veri içeren bir Excel dosyası.

## Araç ipuçları ekleme nedir?
**Araç ipuçları ekleme**, bir Excel grafiğinde veri noktasının değerini veya özel bilgiyi gösteren üzerine gelindiğinde (hover) metni etkinleştirme sürecine denir. Aspose.Cells'te bu, grafiğin veri‑etiket ayarlarıyla sağlanır. Araç ipuçları, kullanıcıların veriyi grafiği karıştırmadan hızlıca anlamalarına yardımcı olur ve yazı tipi, renk ve biçim için özelleştirilebilir.

## Aspose.Cells ile etkileşimli grafikleri neden kullanmalısınız?
Aspose.Cells, **50+ giriş ve çıkış formatını**—XLSX, CSV, PDF ve HTML dahil—destekler ve tüm dosyayı belleğe yüklemeden **1 000'den fazla sayfa** içeren çalışma kitaplarını işleyebilir, kurumsal raporlama için hızlı, sunucu‑tarafı grafik oluşturma sağlar. Etkileşimli grafikler ayrıca hiperlink eklemeye, dinamik veri güncellemelerine ve web‑uyumlu formatlara dışa aktarmaya olanak tanır; bu da onları gösterge panoları ve raporlama portalları için ideal kılar.

## Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- Java Geliştirme Ortamı (JDK 8+ önerilir)  
- Aspose.Cells for Java kütüphanesi ([Aspose.Cells for Java indirme sayfasından](https://releases.aspose.com/cells/java/))  
- Görselleştirmek istediğiniz verileri içeren örnek bir çalışma kitabı (`data.xlsx`)  

## Adım 1: Java projenizi kurma

1. Favori IDE'nizde (IntelliJ IDEA, Eclipse vb.) yeni bir Java projesi oluşturun.  
2. Aspose.Cells JAR dosyasını projenizin derleme yoluna veya Maven/Gradle bağımlılıklarına ekleyin.

## Adım 2: Verileri yükleme

Grafiklerle çalışmak için önce bir çalışma kitabının belleğe yüklenmesi gerekir.

`Workbook` sınıfı bir Excel dosyasını temsil eder ve `Worksheet` bu dosya içindeki tek bir sayfayı temsil eder.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Aspose.Cells'te grafik tipini nasıl değiştirirsiniz?

İstenen `ChartType` enum değeriyle yeni bir grafik oluşturun; Aspose.Cells mevcut bir grafiğin tipini yerinde değiştirmez, bu yüzden doğru tipte yeni bir grafik eklemeli ve isteğe bağlı olarak eski grafiği kaldırmalısınız. Bu yaklaşım, tüm serilerin ve eksenlerin yeni görsel temsile uygun şekilde yeniden oluşturulmasını garanti eder.

## Adım 3: Grafik oluşturma (ve tipini değiştirme)

Analizinize uygun herhangi bir grafik tipini seçebilirsiniz. Aşağıda bir **sütun grafiği** oluşturuyoruz, ancak `ChartType` enum değerini değiştirerek kolayca çizgi, pasta veya çubuk grafiklerine geçebilirsiniz.

`Chart` nesnesi, çalışma sayfasındaki verilerin görsel temsili için yapılandırma yöntemleri sağlar.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro tip:** **Excel grafik tipini değiştirmek** için `ChartType.COLUMN` yerine `ChartType.LINE`, `ChartType.PIE` vb. kullanın.

## Excel grafiğine araç ipuçları nasıl eklenir?

Grafiğinizi yükleyin, veri etiketlerini etkinleştirin ve `showValue` bayrağını ayarlayın. Böylece bir kullanıcı render edilmiş Excel dosyasında veya HTML görünümünde bir veri noktasının üzerine geldiğinde araç ipucu, alttaki hücre değerini gösterir. Ayrıca araç ipucunun yazı tipini, rengini ve arka planını rapor stilinize uygun şekilde özelleştirebilirsiniz.

`DataLabel` sınıfı, veri etiketlerinin görünümünü ve içeriğini kontrol eder; bu etiketler aynı zamanda araç ipuçları olarak da işlev görür.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## Adım 4: Etkileşim ekleme

### 4.1. Araç ipuçları ekleme (grafiğe araç ipuçları ekleme)

Araç ipuçları, kullanıcı bir veri noktasının üzerine geldiğinde görünür. Aşağıdaki kod veri etiketlerini etkinleştirir ve değeri bir araç ipucu olarak gösterir.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. Veri etiketleri ekleme – **Excel grafiğine veri etiketleri ekleme**

Veri etiketleri, grafiğin kendisinde kalıcı bir görsel ipucu sağlar. Daha iyi okunabilirlik için bunları açıklama balonları şeklinde gösterebilirsiniz.

`DataLabel` sınıfı, her seri için etiketlerin görünümünü kontrol eder. `setHasDataLabels(true)` çağırarak ve `setShowValue(true)` gibi özellikleri yapılandırarak sayısal değeri doğrudan grafiğe yerleştirirsiniz; bu, herhangi bir etkileşim olmadan anında görünür hâle getirir. Ek seçenekler, seri adlarını, yüzde değerlerini veya özel metinleri göstererek daha zengin bir bağlam sağlar.

> **Veri etiketleri neden eklenir?** Veri etiketlerini doğrudan grafiğe eklemek, kullanıcıların üzerine gelme veya değer tahmin etme ihtiyacını ortadan kaldırır, rapor netliğini artırır.

### 4.3. Drill‑down uygulama (veri noktasına hiperlink ekleme)

Drill‑down yeteneği eklemenin basit bir yolu, belirli bir noktaya hiperlink eklemektir. Noktaya tıklandığında detaylı bilgileri içeren bir web sayfası açılır.

`Hyperlink` sınıfı, bir grafik öğesine tıklanabilir bir bağlantı ekleyerek drill‑down navigasyonunu sağlar.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Excel grafiğine veri etiketleri nasıl eklenir?

`DataLabel` sınıfı, her seri için etiketlerin görünümünü kontrol eder. `setHasDataLabels(true)` çağırarak ve `setShowValue(true)` gibi özellikleri yapılandırarak sayısal değeri doğrudan grafiğe yerleştirirsiniz; bu, etkileşim olmadan anında görünür hâle getirir. Ek seçenekler, seri adlarını, yüzde değerlerini veya özel metinleri göstererek daha zengin bir bağlam sağlar.

## Adım 5: Çalışma kitabını kaydetme

Grafiği yapılandırdıktan sonra, etkileşimli özelliklerin çıktı dosyasında saklanması için çalışma kitabını kalıcı hâle getirin.

`workbook.save` çağrısı, değiştirilmiş çalışma kitabını seçilen formatta bir dosyaya yazar.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Yaygın sorunlar ve çözümler

| Sorun | Çözüm |
|-------|----------|
| **Araç ipuçları görünmüyor** | `setHasDataLabels(true)`'in `setShowValue(true)` yapılandırılmadan önce çağrıldığından emin olun. |
| **Hiperlink tıklanabilir değil** | Çıktı formatının hiperlinkleri desteklediğini doğrulayın (ör. XLSX, CSV değil). |
| **Grafik tipi değişmiyor** | Grafik eklerken doğru `ChartType` enum değerini değiştirdiğinizi iki kez kontrol edin. |

## Sıkça sorulan sorular

**S:** Grafik oluşturulduktan sonra tipini nasıl değiştirebilirim?  
**C:** İstenen `ChartType` ile yeni bir grafik oluşturmanız gerekir. Aspose.Cells yerinde tip dönüşümü sağlamaz, bu yüzden eski grafiği kaldırıp yenisini ekleyin.

**S:** Araç ipuçlarının görünümünü özelleştirebilir miyim?  
**C:** Evet. `DataLabel` özelliklerini, örneğin `setFontSize`, `setFontColor` ve `setBackgroundColor` kullanarak araç ipucu metnini biçimlendirebilirsiniz.

**S:** Web uygulamasında kullanıcı etkileşimlerini nasıl yönetirim?  
**C:** Çalışma kitabını HTML veya XLSX dosyasına dışa aktarın ve istemci tarafında JavaScript kullanarak grafik öğelerindeki tıklama olaylarını yakalayın.

**S:** Daha fazla örnek ve belgeleri nerede bulabilirim?  
**C:** Tam bir grafik‑ilişkili sınıf ve metod listesi için [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) adresini ziyaret edin.

## Sonuç

Artık **Excel grafiğine veri etiketleri eklemeyi**, **Excel grafik tipini değiştirmeyi**, **etkileşimli grafik Java** çözümleri oluşturmayı ve bunları Aspose.Cells for Java kullanarak araç ipuçları, veri etiketleri ve drill‑down hiperlinkleriyle zenginleştirmeyi biliyorsunuz. Bu geliştirmeler, Excel raporlarınızı son kullanıcılar için çok daha ilgi çekici ve içgörülü hâle getirir.

---

**Son Güncelleme:** 2026-08-21  
**Test Edilen Sürüm:** Aspose.Cells for Java 24.12  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose.Cells for Java Kullanarak Excel Grafiklerini ve Veri Etiketlerini Nasıl Değiştirilir](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Aspose.Cells Java Kullanarak Excel Grafik Eksen Etiketlerini Çıkarma: Kapsamlı Bir Rehber](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Aspose.Cells for Java Kullanarak Excel'de Balon Grafikler Oluşturma: Adım Adım Rehber](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}