---
date: 2025-12-04
description: Aspose.Cells kullanarak Java'da etkileşimli grafik oluşturmayı, grafiğe
  araç ipuçları eklemeyi ve daha zengin veri görselleştirme için drill‑down grafik
  eklemeyi öğrenin.
language: tr
linktitle: Create Interactive Chart Java
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells ile Java'da Etkileşimli Grafik Oluştur
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Etkileşimli Grafik Java Oluşturma

## Giriş

Etkileşimli grafikler, kullanıcılarınıza veri noktalarını keşfetme, üzerine gelindiğinde detayları görme ve hatta daha derin veri setlerine dalma imkanı sunar—bütün bunlar elektronik tabloyu terk etmeden gerçekleşir. Bu öğreticide **Java için etkileşimli grafik** uygulamaları oluşturmayı Aspose.Cells kullanarak öğreneceksiniz. Araç ipuçları, veri etiketleri eklemeyi ve bir drill‑down deneyimi uygulamayı adım adım gösterecek, böylece grafikleriniz daha çekici ve bilgilendirici hâle gelecek.

## Hızlı Yanıtlar
- **Hangi kütüphane kullanılıyor?** Aspose.Cells for Java  
- **Grafiğe araç ipucu ekleyebilir miyim?** Evet, NSeries veri‑etiket API’si ile  
- **Drill‑down destekleniyor mu?** Evet, veri noktalarına hiperlink ekleyerek  
- **Hangi dosya formatı üretiliyor?** Gömülü grafiklerle standart XLSX çalışma kitabı  
- **Lisans gerekiyor mu?** Değerlendirme için ücretsiz deneme yeterli; üretim için ticari lisans gereklidir  

## Ön Koşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

- Java geliştirme ortamı (JDK 8+ önerilir)  
- Aspose.Cells for Java kütüphanesi (resmi [Aspose sürüm sayfasından](https://releases.aspose.com/cells/java/) indirilebilir)  
- Görselleştirmek istediğiniz verileri içeren **data.xlsx** adlı örnek Excel dosyası  

## Adım 1: Java Projenizi Kurma

1. Sevdiğiniz IDE’de (IntelliJ IDEA, Eclipse, VS Code vb.) yeni bir Java projesi oluşturun.  
2. Aspose.Cells JAR dosyasını projenizin sınıf yoluna ekleyin—JAR’ı `libs` klasörüne koyarak ya da Maven/Gradle bağımlılığı ekleyerek.

## Adım 2: Verileri Yükleme

Etkileşimli bir grafik oluşturmak için önce veri içeren bir çalışma sayfasına ihtiyacınız var. Aşağıdaki kod parçacığı mevcut bir çalışma kitabını açar ve ilk çalışma sayfasını alır.

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro tip:** Grafikle göstermek istediğiniz veri aralığının bitişik olduğundan emin olun; Aspose.Cells seriyi bağladığınızda aralığı otomatik olarak algılar.

## Adım 3: Grafik Oluşturma

Şimdi bir sütun grafiği oluşturup çalışma sayfasına yerleştiriyoruz. Görsel stili değiştirmek isterseniz `ChartType.COLUMN` ifadesini başka bir tipe (ör. `ChartType.LINE`) değiştirebilirsiniz.

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Neden önemli:** Grafiği programatik olarak eklemek, boyut, konum ve veri kaynağı üzerinde tam kontrol sağlar; bu da etkileşimli deneyimler inşa etmek için şarttır.

## Adım 4: Etkileşim Ekleme

### Grafiğe araç ipucu nasıl eklenir

Araç ipuçları (veya değer gösteren veri etiketleri), kullanıcıların her çubuğun arkasındaki tam sayıyı anında görmesini sağlar. Aşağıdaki kod veri etiketlerini etkinleştirir ve değeri göstermesi için yapılandırır.

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### Veri etiketlerini (callout) nasıl eklenir

Etiketlerin düz metin yerine balon (callout) şeklinde görünmesini istiyorsanız `ShowLabelAsDataCallout` özelliğini değiştirin.

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### Drill‑down grafiği nasıl eklenir

Drill‑down, bir kullanıcı veri noktasına tıkladığında ilgili detay görünümüne yönlendirme yapar—genellikle bir hiperlink ile uygulanır. Aşağıda serinin ilk noktasına bir URL ekliyoruz.

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

> **Yaygın tuzak:** Hiperlink hedefinin detay veriyi render edebilecek bir sayfa (ör. web raporu veya başka bir Excel sayfası) olduğundan emin olun. Aksi takdirde tıklama bozuk bir bağlantıya yönlendirilir.

## Adım 5: Çalışma Kitabını Kaydetme

Grafiği yapılandırdıktan sonra çalışma kitabını kalıcı hale getirin. Oluşan dosya, Excel ya da uyumlu bir görüntüleyicide açılabilecek etkileşimli grafik içerir.

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## Sonuç

Bu rehberde **Java için etkileşimli grafik** çözümlerini Aspose.Cells ile nasıl oluşturacağınızı öğrendiniz; kapsamlı olarak:

- Mevcut bir çalışma kitabından veri yükleme  
- Programatik olarak sütun grafiği oluşturma  
- Araç ipuçları ve balon veri etiketleri ekleme  
- Hiperlinkler aracılığıyla drill‑down işlevi uygulama  
- Son çalışma kitabını kaydetme  

Bu teknikler, statik elektronik tabloları dinamik, kullanıcı‑dostu panolara dönüştürerek veri anlayışını ve karar verme süreçlerini artırır.

## Sıkça Sorulan Sorular

**S: Grafik tipini nasıl değiştiririm?**  
C: `add` metodundaki `ChartType` enum’unu değiştirin (ör. çizgi grafik için `ChartType.LINE`).

**S: Araç ipuçlarının görünümünü özelleştirebilir miyim?**  
C: Evet, `DataLabels` nesnesi üzerinden yazı tipi boyutu, renk, arka plan ve diğer stil özelliklerini ayarlayabilirsiniz.

**S: Web uygulamasında grafik etkileşimini nasıl yönetirim?**  
C: Çalışma kitabını XLSX olarak dışa aktarın, ardından JavaScript grafik kütüphanesi (ör. Highcharts) ile veriyi istemci tarafında render edin ya da hiperlinkleri destekleyen Office Web Viewer’da Excel dosyasını gömün.

**S: Daha fazla örnek nereden bulabilirim?**  
C: Tam grafik‑ilişkili sınıf ve metod listesi için resmi [Aspose.Cells Java API Referansına](https://reference.aspose.com/cells/java/) göz atın.

**S: Üretim ortamında lisans gerekiyor mu?**  
C: Evet, dağıtım için ticari lisans zorunludur; test için ücretsiz değerlendirme lisansı mevcuttur.

---

**Son Güncelleme:** 2025-12-04  
**Test Edilen Versiyon:** Aspose.Cells for Java 24.12 (yazım anındaki en yeni)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}