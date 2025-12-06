---
date: 2025-12-06
description: Excel grafik türünü nasıl değiştireceğinizi ve Aspose.Cells kullanarak
  Java ile etkileşimli grafikler oluşturmayı öğrenin. Grafiklere araç ipuçları, veri
  etiketleri ekleyin ve daha zengin veri görselleştirme için drill‑down yapın.
language: tr
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells Java ile Excel Grafik Türünü Değiştir
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel Grafik Türünü Değiştirin ve Etkileşim Ekleyin

## Giriş

Etkileşimli grafikler, Excel raporlarınıza yeni bir içgörü seviyesi kazandırır; kullanıcıların veri noktalarının üzerine gelerek, tıklayarak ve doğrudan keşfetmesini sağlar. Bu öğreticide **Excel grafik türünü değiştirecek** ve **Aspose.Cells for Java** ile **etkileşimli grafik Java** çözümleri oluşturacaksınız. Grafiklere araç ipuçları, veri etiketleri eklemeyi ve izleyicilerinizin sayılarla daha derinlemesine etkileşime girebilmesi için basit bir drill‑down (derinlemesine) bağlantısını nasıl ekleyeceğinizi adım adım göstereceğiz.

## Hızlı Yanıtlar
- **Hangi kütüphane kullanılıyor?** Aspose.Cells for Java  
- **Grafik türünü değiştirebilir miyim?** Evet – grafik oluştururken `ChartType` enumunu değiştirmeniz yeterli.  
- **Grafiğe araç ipuçları nasıl eklenir?** Veri‑etiket API'sini (`setHasDataLabels(true)`) kullanın ve değer gösterimini etkinleştirin.  
- **Drill‑down destekleniyor mu?** Veri noktalarına hiperlink ekleyerek temel drill‑down davranışı sağlayabilirsiniz.  
- **Önkoşullar?** Java IDE, Aspose.Cells JAR ve örnek veri içeren bir Excel dosyası.

## Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- Java Geliştirme Ortamı (JDK 8+ önerilir)  
- Aspose.Cells for Java kütüphanesi (indir: [here](https://releases.aspose.com/cells/java/))  
- Görselleştirmek istediğiniz verileri içeren bir örnek çalışma kitabı (`data.xlsx`)  

## Adım 1: Java Projenizi Kurun

1. Favori IDE'nizde (IntelliJ IDEA, Eclipse vb.) yeni bir Java projesi oluşturun.  
2. Aspose.Cells JAR dosyasını projenizin derleme yoluna veya Maven/Gradle bağımlılıklarına ekleyin.

## Adım 2: Verileri Yükleme

Grafiklerle çalışabilmek için önce bir çalışma kitabını belleğe yüklemeniz gerekir.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Adım 3: Grafik Oluşturma (ve Türünü Değiştirme)

Analizinize uygun herhangi bir grafik türünü seçebilirsiniz. Aşağıda **sütun grafiği** oluşturuyoruz, ancak `ChartType` enumunu değiştirerek kolayca çizgi, pasta veya çubuk grafiklerine geçebilirsiniz.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **İpucu:** **Excel grafik türünü değiştirmek** için `ChartType.COLUMN` yerine `ChartType.LINE`, `ChartType.PIE` vb. değerleri kullanın.

## Adım 4: Etkileşim Eklemek

### 4.1. Araç İpuçları Ekleme (Add Tooltips to Chart)

Kullanıcı bir veri noktasının üzerine geldiğinde araç ipuçları görünür. Aşağıdaki kod veri etiketlerini etkinleştirir ve değeri araç ipucu olarak gösterir.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Veri Etiketleri Ekleme

Veri etiketleri, grafiğin üzerinde kalıcı bir görsel ipucu sağlar. Daha iyi okunabilirlik için bunları çağrı balonları (callouts) şeklinde gösterebilirsiniz.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Drill‑Down Uygulama (Veri Noktasına Hiperlink)

Drill‑down yeteneği eklemenin basit bir yolu, belirli bir noktaya hiperlink eklemektir. Noktaya tıklandığında detaylı bilgileri içeren bir web sayfası açılır.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Adım 5: Çalışma Kitabını Kaydetme

Grafiği yapılandırdıktan sonra, etkileşimli özelliklerin çıktıda saklanması için çalışma kitabını kalıcı hale getirin.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|----------|
| **Araç ipuçları görünmüyor** | `setHasDataLabels(true)` çağrısının `setShowValue(true)` yapılandırmasından önce yapıldığından emin olun. |
| **Hiperlink tıklanabilir değil** | Çıktı formatının hiperlinkleri desteklediğini doğrulayın (ör. XLSX, CSV değil). |
| **Grafik türü değişmiyor** | Grafiği eklerken doğru `ChartType` enumunu değiştirdiğinizi iki kez kontrol edin. |

## Sıkça Sorulan Sorular

**S: Grafik oluşturulduktan sonra türünü nasıl değiştirebilirim?**  
C: İstenen `ChartType` ile yeni bir grafik oluşturmanız gerekir. Aspose.Cells, yerinde tür dönüşümünü sağlamaz; eski grafiği kaldırıp yenisini ekleyin.

**S: Araç ipuçlarının görünümünü özelleştirebilir miyim?**  
C: Evet. `DataLabel` özelliklerini (`setFontSize`, `setFontColor`, `setBackgroundColor` vb.) kullanarak araç ipucu metnini stilize edebilirsiniz.

**S: Web uygulamasında kullanıcı etkileşimlerini nasıl yönetirim?**  
C: Çalışma kitabını HTML veya XLSX dosyasına dışa aktarın ve istemci tarafında grafik öğelerine tıklama olaylarını yakalamak için JavaScript kullanın.

**S: Daha fazla örnek ve dokümantasyon nerede?**  
C: Tüm grafik‑ile‑ilgili sınıf ve metodların tam listesini [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) adresinde bulabilirsiniz.

## Sonuç

Artık **Excel grafik türünü değiştirebilir**, **Aspose.Cells for Java** ile **etkileşimli grafik Java** çözümleri oluşturabilir ve bunları araç ipuçları, veri etiketleri ve drill‑down hiperlinkleriyle zenginleştirebilirsiniz. Bu geliştirmeler, Excel raporlarınızı son kullanıcılar için çok daha çekici ve içgörülü hâle getirir.

---

**Son Güncelleme:** 2025-12-06  
**Test Edilen Sürüm:** Aspose.Cells for Java 24.12  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}