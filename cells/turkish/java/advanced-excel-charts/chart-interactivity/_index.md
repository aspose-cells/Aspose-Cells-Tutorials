---
date: 2025-12-05
description: Aspose.Cells kullanarak Java’da veri etiketi eklemeyi ve etkileşimli
  grafik oluşturmayı öğrenin. Araç ipuçları, veri etiketleri ve drill‑down işlevselliği
  ekleyin.
language: tr
linktitle: Add Data Labels Chart with Interactivity
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells Java'da Etkileşimli Veri Etiketli Grafik Ekle
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java'da Etkileşimli Veri Etiketleri Grafiği Ekleme

Etkileşimli grafikler, kullanıcılarınıza verileri anında keşfetme imkanı sağlar. Bu öğreticide Aspose.Cells for Java kullanarak **add data labels chart** özelliklerini—araç ipuçları, veri etiketleri ve drill‑down eylemleri—ekleyeceksiniz. Sonunda, karmaşık verileri anında anlaşılır kılan, şık bir etkileşimli grafik elde edeceksiniz.

## Hızlı Yanıtlar
- **Hangi kütüphaneye ihtiyacım var?** Aspose.Cells for Java  
- **Excel grafiğine araç ipuçları ekleyebilir miyim?** Evet – API'nin veri etiketi ayarlarını kullanın.  
- **Hangi grafik türleri etkileşimi destekler?** Çoğu yerleşik tür (sütun, çizgi, pasta vb.).  
- **Üretim için lisans gerekiyor mu?** Geçerli bir Aspose.Cells lisansı gereklidir.  
- **Uygulama ne kadar sürer?** Temel bir grafik için yaklaşık 10–15 dakika.

## “add data labels chart” nedir?
*add data labels chart*, her veri noktasının görsel üzerinde doğrudan bir etiket (değer, ad veya özel metin) gösterdiği bir grafiktir. Bu, izleyicilerin ayrı bir lejandaya bakmadan ya da üzerine gelmeden kesin değerleri okumasını kolaylaştırır.

## Neden etkileşimli Java grafik çözümleri oluşturmalıyız?
Etkileşim eklemek—araç ipuçları, tıklanabilir noktalar, drill‑down bağlantıları—statik elektronik tabloları keşif panolarına dönüştürür. Kullanıcılar şunları yapabilir:
- Aykırı değerleri hızlıca tanımlamak.
- Tek bir tıklama ile daha derin veri katmanlarına erişmek.
- Ayrı rapor ihtiyacını azaltarak karar verme hızını artırmak.

## Önkoşullar

Başlamadan önce, şunların olduğundan emin olun:
- Java geliştirme ortamı (JDK 8+ önerilir).  
- Aspose.Cells for Java kütüphanesi ([buradan](https://releases.aspose.com/cells/java/) indirin).

## Adım 1: Java Projenizi Kurma

1. Sevdiğiniz IDE'de (IntelliJ, Eclipse, VS Code vb.) yeni bir Java projesi oluşturun.  
2. Aspose.Cells for Java JAR dosyasını projenizin sınıf yoluna ekleyin.

## Adım 2: Verileri Yükleme

Etkileşimli bir grafik oluşturmak için önce bir çalışma sayfasında veri gerekir. Aşağıdaki kod parçacığı **data.xlsx** adlı mevcut bir çalışma kitabını yükler.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Adım 3: Grafik Oluşturma

Şimdi bir sütun grafiği oluşturup çalışma sayfasına yerleştiriyoruz. İsterseniz `ChartType.COLUMN` ifadesini başka bir türle değiştirebilirsiniz.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adım 4: Etkileşim Ekleme – “add data labels chart”ın Çekirdeği

### 4.1. Araç İpuçları Ekleme (add tooltips excel chart)

Araç ipuçları, bir kullanıcı veri noktasının üzerine geldiğinde görünür. Aşağıdaki kod, veri etiketlerini etkinleştirerek ve değeri göstererek bunları aktif eder.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Veri Etiketleri Ekleme (add data labels chart)

Veri etiketleri, her noktanın yanına yerleşen görsel metindir. Bu kod parçacığı, grafiği düz değerler yerine çağrı etiketleri (callout) gösterecek şekilde yapılandırır.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Drill‑Down Uygulama (create interactive chart java)

Drill‑down, kullanıcıların bir noktaya tıklayıp ayrıntılı bir görünüme geçmesini sağlar. Burada ilk veri noktasına bir hiperlink ekliyoruz; ihtiyacınız olan herhangi bir nokta için bu işlemi tekrarlayabilirsiniz.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Adım 5: Çalışma Kitabını Kaydetme

Grafiği yapılandırdıktan sonra, etkileşimi test edebilmek ve Excel'de açabilmek için çalışma kitabını yeni bir dosyaya kaydedin.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Yaygın Sorunlar ve İpuçları

| Sorun | Çözüm |
|-------|----------|
| **Araç ipuçları görünmüyor** | `setHasDataLabels(true)`'in `ShowValue` ayarlamadan önce çağrıldığından emin olun. |
| **Hiperlink tıklanabilir değil** | URL'nin doğru biçimlendirildiğini ve Excel'in güvenlik ayarlarının dış bağlantılara izin verdiğini doğrulayın. |
| **Grafik türü uyumsuzluğu** | Bazı grafik türlerinin (ör. radar) sınırlı etiket desteği vardır—sütun veya çizgi gibi uyumlu bir tür seçin. |
| **Büyük veri setlerinde performans gecikmesi** | Veri etiketli nokta sayısını sınırlayın; daha az kritik seriler için `setShowValue(false)` kullanmayı düşünün. |

## Sık Sorulan Sorular

**S: Grafiğin türünü nasıl değiştirebilirim?**  
C: Grafik oluşturma satırındaki `ChartType` enum'ını değiştirin (ör. çizgi grafiği için `ChartType.LINE`).

**S: Araç ipuçlarının görünümünü özelleştirebilir miyim?**  
C: Evet—araç ipuçlarını stilize etmek için `DataLabel` nesnesinin yazı tipi, arka plan rengi ve kenarlık özelliklerini kullanın.

**S: Web uygulamasında kullanıcı etkileşimlerini nasıl yönetirim?**  
C: Çalışma kitabını bir HTML sayfasına dışa aktarın veya grafiği oluşturmak için Aspose.Cells Cloud'ı kullanın, ardından tıklama olaylarını JavaScript ile yakalayın.

**S: Daha fazla örnek ve belgeyi nerede bulabilirim?**  
C: Grafikle ilgili sınıflar ve yöntemlerin tam listesini görmek için [Aspose.Cells Java API Referansı](https://reference.aspose.com/cells/java/) adresini ziyaret edin.

## Sonuç

Bu rehberde **add data labels chart** özelliklerini nasıl ekleyeceğimizi ve Aspose.Cells ile **interactive chart Java** çözümünü nasıl oluşturacağımızı gösterdik. Araç ipuçları, veri çağrı etiketleri ve drill‑down hiperlinkleri ekleyerek, statik bir Excel grafiğini içgörü ve kullanılabilirliği artıran dinamik bir veri keşif aracına dönüştürürsünüz.

---

**Son Güncelleme:** 2025-12-05  
**Test Edilen Sürüm:** Aspose.Cells for Java 24.12  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}