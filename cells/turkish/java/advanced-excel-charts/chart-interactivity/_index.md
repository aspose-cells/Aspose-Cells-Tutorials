---
date: 2025-12-01
description: Aspose.Cells for Java kullanarak Excel grafik türünü nasıl değiştireceğinizi
  ve araç ipuçları, veri etiketleri ve drill‑down gibi etkileşimli özellikler eklemeyi
  öğrenin.
language: tr
linktitle: Change Excel chart type and add interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Excel grafik türünü değiştirin ve etkileşim ekleyin – Aspose.Cells Java
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel grafik tipini değiştirin ve etkileşim ekleyin

## Giriş

Etkileşimli grafikler, izleyicilerinizin verileri anında keşfetmesini sağlar, **Excel grafik tipini değiştirme** yeteneği ise bilgileri en etkili görsel formatta sunma esnekliği verir. Bu öğreticide, Aspose.Cells for Java kullanarak bir grafiğin tipini nasıl değiştireceğinizi, araç ipuçları ekleyeceğinizi, veri etiketlerini gömeceğinizi ve hatta drill‑down bağlantıları oluşturacağınızı öğreneceksiniz—tüm bunlar Java kodunuzdan çıkmadan. Sonunda, raporlar, gösterge panelleri veya web uygulamalarına gömebileceğiniz tam özellikli, etkileşimli bir Excel çalışma kitabına sahip olacaksınız.

## Hızlı Yanıtlar
- **Grafik tipini programlı olarak değiştirebilir miyim?** Evet – bir grafik oluştururken veya güncellerken `ChartType` enum'ını kullanın.  
- **Bir grafiğe araç ipuçları nasıl eklenir?** Veri etiketlerini etkinleştirin ve `ShowValue` değerini true yapın.  
- **Drill‑down bağlantıları eklemenin en kolay yolu nedir?** `getHyperlinks().add(url)` yöntemiyle bir veri noktasına hiperlink ekleyin.  
- **Aspose.Cells için lisans gerekli mi?** Geliştirme için ücretsiz deneme sürümü çalışır; üretim için lisans gereklidir.  
- **Hangi Java sürümü destekleniyor?** Java 8 ve üzeri tam olarak desteklenir.

## “Excel grafik tipini değiştirme” nedir?

Grafik tipini değiştirmek, temel verileri aynı tutarak görsel temsili (ör. sütun grafiğinden çizgi grafiğine) değiştirmek anlamına gelir. Bu, farklı bir grafiğin trendleri, karşılaştırmaları veya dağılımları daha iyi ilettiğini fark ettiğinizde faydalıdır.

## Excel grafiklerine neden etkileşim eklenmeli?

- **Daha iyi veri içgörüsü:** Araç ipuçları ve veri etiketleri, kullanıcıların tam değerleri kaydırmadan görmesini sağlar.  
- **Etkileyici sunumlar:** Etkileşimli öğeler izleyicilerin ilgisini çeker.  
- **Drill‑down yeteneği:** Hiperlinkler, kullanıcıların ayrıntılı çalışma sayfalarına veya dış kaynaklara atlamasını sağlar.  
- **Yeniden kullanılabilir varlıklar:** Tek bir çalışma kitabı, sadece grafik tiplerini değiştirerek birden fazla raporlama senaryosuna hizmet edebilir.

## Önkoşullar

- Java Geliştirme Ortamı (JDK 8+)  
- Aspose.Cells for Java kütüphanesi (indirme linki: [here](https://releases.aspose.com/cells/java/))  
- Görselleştirmek istediğiniz verileri içeren örnek bir Excel dosyası (`data.xlsx`)

## Adım adım kılavuz

### Adım 1: Java projenizi kurun

1. Favori IDE'nizde (IntelliJ IDEA, Eclipse, VS Code vb.) yeni bir Java projesi oluşturun.  
2. Aspose.Cells JAR dosyasını projenizin sınıf yoluna ekleyin.

### Adım 2: Kaynak çalışma kitabını yükleyin

Grafiğimizin verilerini içeren mevcut bir çalışma kitabını yükleyerek başlıyoruz.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### Adım 3: Bir grafik oluşturun ve **tipini değiştirin**

Aşağıda bir sütun grafiği oluşturuyoruz, ardından ihtiyacınız olduğunda onu bir çizgi grafiğine nasıl dönüştürebileceğinizi hemen gösteriyoruz.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// OPTIONAL: Change the chart type to LINE
chart.setChartType(ChartType.LINE);
```

> **Pro ipucu:** Oluşturulduktan sonra grafik tipini değiştirmek, `setChartType(...)` çağrısı kadar basittir. Bu, yeni bir grafik nesnesi oluşturmadan **Excel grafik tipini değiştirme** anahtar kelimesini karşılar.

### Adım 4: Etkileşim ekleyin

#### 4.1 Grafiğe araç ipuçları ekleyin

Araç ipuçları, bir kullanıcı veri noktasının üzerine geldiğinde gösterilir. Aspose.Cells'te bunlar veri etiketleri aracılığıyla uygulanır.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

#### 4.2 Veri etiketleri ekleyin ( **add data labels chart** )

Veri etiketleri tam değeri, kategori adını veya her ikisini gösterebilir. Burada bir açıklama (callout) stili kullanıyoruz.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

#### 4.3 Drill‑down uygulayın ( **add drill down excel** )

Bir drill‑down bağlantısı, kullanıcıların bir noktaya tıklayıp detaylı bir görünüme, ya çalışma kitabı içinde ya da bir web sayfasına atlamasını sağlar.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

### Adım 5: Çalışma kitabını kaydedin

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Yaygın sorunlar ve çözümler

| Sorun | Neden | Çözüm |
|-------|--------|-----|
| Araç ipuçları gösterilmiyor | `HasDataLabels` etkinleştirilmemiş | `ShowValue` yapılandırılmadan önce `setHasDataLabels(true)` çağrıldığından emin olun. |
| Drill‑down bağlantısı çalışmıyor | Hiperlink URL'si hatalı | URL'nin `http://` veya `https://` ile başladığını doğrulayın. |
| Grafik tipi değişmiyor | Eski bir Aspose.Cells sürümü kullanılıyor | En son sürüme yükseltin (24.12 ile test edilmiştir). |

## Sıkça Sorulan Sorular

**S: Bir grafik oluşturulduktan sonra tipini nasıl değiştirebilirim?**  
C: Mevcut `Chart` nesnesi üzerinde `chart.setChartType(ChartType.YOUR_CHOICE)` çağrısı yapın. Bu, **Excel grafik tipini değiştirme** gereksinimini doğrudan karşılar.

**S: Araç ipuçlarının görünümünü özelleştirebilir miyim?**  
C: Evet. Yazı tipi boyutu, renk ve arka planı ayarlamak için `chart.getNSeries().get(0).getPoints().getDataLabels()` kullanın.

**S: Tek bir grafikte birden fazla drill‑down bağlantısı eklemek mümkün mü?**  
C: Kesinlikle. Noktalar üzerinde döngü kurarak bağlamak istediğiniz her nokta için `getHyperlinks().add(url)` çağrısı yapın.

**S: Aspose.Cells pasta veya radar gibi diğer grafik tiplerini destekliyor mu?**  
C: `ChartType` enum'ında tanımlı tüm grafik tipleri desteklenir; `PIE`, `RADAR`, `AREA` vb. dahil.

**S: Daha fazla örnek nerede bulunabilir?**  
C: Grafik‑ile ilgili tüm yöntemlerin tam listesini görmek için resmi [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) sayfasını ziyaret edin.

## Sonuç

Artık Aspose.Cells for Java kullanarak **Excel grafik tipini değiştirme**, **araç ipuçları** ekleme, **veri etiketleri** ekleme ve **drill‑down** bağlantıları oluşturma konusunda bilgi sahibisiniz. Bu etkileşimli özellikler, statik elektronik tabloları dinamik veri keşif araçlarına dönüştürür; gösterge panelleri, raporlar ve web tabanlı analizler için mükemmeldir.

---

**Last Updated:** 2025-12-01  
**Tested With:** Aspose.Cells 24.12 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}