---
date: 2025-11-28
description: Aspose.Cells kullanarak Java'da etkileşimli bir grafik oluşturmak için
  araç ipuçları, veri etiketleri ve drill‑down özelliklerini nasıl ekleyeceğinizi
  öğrenin.
language: tr
linktitle: How to Add Tooltips in Interactive Charts
second_title: Aspose.Cells Java Excel Processing API
title: Etkileşimli Grafiklere Araç İpuçları Nasıl Eklenir (Aspose.Cells Java)
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Etkileşimli Grafiklerde İpucu (Tooltip) Nasıl Eklenir (Aspose.Cells Java)

## Giriş

Etkileşimli grafikler, kullanıcıların veriyi üzerine gelerek, tıklayarak veya detaylara inerek keşfetmesini sağlar. Bu öğreticide **grafiğe ipucu (tooltip) eklemeyi**, **veri etiketleri eklemeyi** ve **drill‑down** (detaylı gezinme) navigasyonunu Aspose.Cells for Java ile nasıl gerçekleştireceğinizi öğreneceksiniz. Sonunda, veri sunumlarınızı daha çekici ve içgörülü hâle getiren tam özellikli bir etkileşimli grafik oluşturabileceksiniz.

## Hızlı Yanıtlar
- **Hangi kütüphane gerekiyor?** Aspose.Cells for Java (en son sürüm).  
- **Bu kılavuz hangi ana özelliği kapsıyor?** Grafiklere ipucu (tooltip) ekleme.  
- **Veri etiketleri de ekleyebilir miyim?** Evet – “Veri Etiketleri Ekleme” bölümüne bakın.  
- **Drill‑down destekleniyor mu?** Evet, veri noktalarındaki hiperlinkler aracılığıyla.  
- **Hangi dosya formatı üretilir?** Etkileşimli bir grafik içeren Excel çalışma kitabı (`.xlsx`).

## İpucu (Tooltip) Eklemek Nedir?

İpucu, bir kullanıcı grafik öğesinin üzerine geldiğinde ortaya çıkan küçük bir açılır penceredir ve kesin değer ya da özel bir mesaj gibi ek bilgiler gösterir. İpuçları, görsel düzeni kalabalıklaştırmadan veri okunabilirliğini artırır.

## Java’da Etkileşimli Grafikler Neden Oluşturulur?

- **Daha iyi karar‑alma:** Kullanıcılar anında kesin değerleri görebilir.  
- **Profesyonel raporlar:** Etkileşimli öğeler panoları modern gösterir.  
- **Yeniden kullanılabilir bileşenler:** API’yı öğrendikten sonra herhangi bir Excel tabanlı raporlama çözümüne uygulayabilirsiniz.

## Önkoşullar

- Java geliştirme ortamı (JDK 8 veya daha yeni).  
- Aspose.Cells for Java kütüphanesi (indirmek için [buraya](https://releases.aspose.com/cells/java/)).  
- Görselleştirmek istediğiniz verileri içeren **data.xlsx** adlı örnek Excel dosyası.

## Adım 1: Java Projenizi Kurma

1. Tercih ettiğiniz IDE’de (IntelliJ IDEA, Eclipse vb.) yeni bir Java projesi oluşturun.  
2. Aspose.Cells JAR dosyasını projenizin sınıf yoluna ekleyin.

## Adım 2: Veriyi Yükleme

Aşağıdaki kod, **data.xlsx** dosyasının ilk çalışma sayfasını yükler.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Adım 3: Grafik Oluşturma

Şimdi çalışma sayfasına bir sütun grafiği ekleyeceğiz. Grafik, F6 ‑ K16 hücrelerini kapsayacak.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## Adım 4: Etkileşim Eklemek

### 4.1. İpucu (Tooltip) Nasıl Eklenir

Aşağıdaki snippet, grafiğin ilk serisi için ipuçlarını etkinleştirir. Her veri noktası üzerine gelindiğinde değeri gösterilir.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. Grafik'e Veri Etiketleri Ekleme

Her sütunun yanına görünür etiketler eklemek isterseniz, aşağıdaki **add data labels chart** yaklaşımını kullanın. Bu, *add data labels chart* ikincil anahtar kelimesini karşılar.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. Drill‑Down Nasıl Yapılır (Drill‑Down Uygulama)

Drill‑down, kullanıcıların bir veri noktasına tıklayıp ayrıntılı bir görünüme (ör. bir web sayfası) geçmesini sağlar. Burada serinin ilk noktasına bir hiperlink ekliyoruz.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **İpucu:** Noktanın değerine göre URL’yi dinamik olarak oluşturabilir ve gerçek veri‑odaklı bir drill‑down deneyimi yaratabilirsiniz.

## Adım 5: Çalışma Kitabını Kaydetme

Grafiği yapılandırdıktan sonra çalışma kitabını kaydedin. Ortaya çıkan dosya, Excel’de açılmaya hazır etkileşimli bir grafik içerir.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Yaygın Sorunlar ve Çözümler

| Sorun | Neden | Çözüm |
|-------|-------|-----|
| İpucu (tooltip) görünmüyor | Veri etiketleri etkin değil | `ShowValue` ayarlamadan önce `setHasDataLabels(true)` çağrıldığından emin olun. |
| Hiperlink tıklanabilir değil | Yanlış nokta indeksi | Doğru noktayı (`get(0)` ilk noktadır) referans aldığınızdan emin olun. |
| Grafik yanlış konumda görünüyor | Yanlış hücre aralığı | `add(ChartType.COLUMN, row1, col1, row2, col2)` içindeki satır/sütun indekslerini ayarlayın. |

## Sıkça Sorulan Sorular

**S: Grafik tipini nasıl değiştirebilirim?**  
C: `worksheet.getCharts().add(...)` çağrısında `ChartType.COLUMN` yerine `ChartType.LINE` veya `ChartType.PIE` gibi başka bir enum değeri kullanın.

**S: İpuçlarının görünümünü özelleştirebilir miyim?**  
C: Evet. `DataLabel` nesnesinin biçimlendirme özelliklerini (yazı tipi boyutu, arka plan rengi vb.) kullanarak ipucu metnini stilize edebilirsiniz.

**S: Web uygulamasında kullanıcı etkileşimlerini nasıl yönetirim?**  
C: Çalışma kitabını web‑uyumlu bir formata (ör. HTML) dışa aktarın ve grafik öğelerindeki tıklama olaylarını yakalamak için JavaScript kullanın.

**S: Daha fazla örnek ve dokümantasyona nereden ulaşabilirim?**  
C: Resmi API referansına [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) adresinden göz atın.

**S: Aynı grafikte birden fazla drill‑down bağlantısı eklemek mümkün mü?**  
C: Kesinlikle. Seri noktaları üzerinde döngü kurarak her bir noktanın `Hyperlinks` koleksiyonuna benzersiz bir URL atayabilirsiniz.

## Sonuç

Bu rehberde **ipucu (tooltip) eklemeyi**, **veri etiketleri eklemeyi** ve **drill‑down** işlevselliğini Aspose.Cells kullanarak **create interactive chart java** çözümüyle nasıl uygulayacağınızı öğrendiniz. Bu özellikler, statik Excel grafiklerini dinamik, kullanıcı‑dostu görselleştirmelere dönüştürerek paydaşların veriyi kolayca keşfetmesini sağlar.

---

**Son Güncelleme:** 2025-11-28  
**Test Edilen Sürüm:** Aspose.Cells for Java 24.12  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}