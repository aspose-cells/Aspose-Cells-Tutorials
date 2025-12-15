---
date: 2025-12-10
description: Aspose.Cells kullanarak Java’da şelale grafiği oluşturmayı öğrenin. Çalışma
  sayfasına grafik ekleme, özelleştirme ve çalışma kitabını XLSX olarak kaydetme adım
  adım rehberi.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells for Java ile Şelale Grafiği Nasıl Oluşturulur
url: /tr/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Şelale Grafikler

## Aspose.Cells for Java kullanarak Şelale Grafiklerine Giriş

Bu öğreticide Aspose.Cells for Java ile **şelale grafiği oluşturmayı** öğreneceksiniz. Şelale grafikleri, pozitif ve negatif değerlerin bir dizi halinde birikimli etkisini görmenizi sağladığı için veri görselleştirmede vazgeçilmez bir araçtır. Finansal bir tablo, satış performans raporu ya da başka bir veri‑odaklı analiz hazırlıyor olun, şelale grafiği ham sayıları net, eyleme dönüştürülebilir içgörülere dönüştürebilir.

## Hızlı Yanıtlar
- **Şelale grafiği nedir?** Başlangıç değerinin bir dizi ara değerle artırılıp azaltılarak nihai toplamda nasıl bir değişim gösterdiğini gösteren görsel.  
- **Hangi kütüphane kullanılıyor?** Aspose.Cells for Java.  
- **Lisans gerekir mi?** Geliştirme için ücretsiz deneme sürümü yeterlidir; üretim ortamı için ticari lisans gereklidir.  
- **Dosyayı XLSX olarak kaydedebilir miyim?** Evet – `workbook.save("FileName.xlsx")` kullanın.  
- **Java veri görselleştirmesi için uygun mu?** Kesinlikle; Aspose.Cells, Office yüklü olmadan zengin grafik özellikleri sunar.

## Şelale Grafiği Nedir?
Şelale grafiği, bir başlangıç değerine sıralı pozitif ve negatif katkıları göstererek her bir bileşenin genel sonuca nasıl etki ettiğini anlamanızı sağlar.

## Aspose.Cells for Java ile Şelale Grafiği Eklemek Neden?
- **Microsoft Excel gerekmez** – grafikleri herhangi bir sunucu ya da CI boru hattında oluşturabilirsiniz.  
- **Biçimlendirme üzerinde tam kontrol** – renkler, veri etiketleri ve eksenler programatik olarak özelleştirilebilir.  
- **Birden çok çıktı formatını destekler** – XLSX, PDF, HTML ve daha fazlası.  
- **Yüksek performans** – büyük çalışma kitapları ve otomatik raporlamalar için idealdir.

## Önkoşullar

Kodlamaya başlamadan önce aşağıdaki önkoşulların sağlandığından emin olun:

- Aspose.Cells for Java: Aspose.Cells for Java yüklü olmalıdır. İndirmek için [buraya](https://releases.aspose.com/cells/java/) tıklayın.

- Java Geliştirme Ortamı: Sisteminizde Java yüklü olmalıdır.

Şimdi adım adım şelale grafiği oluşturmaya başlayalım.

## Java’da Şelale Grafiği Nasıl Oluşturulur

### Adım 1: Aspose.Cells’ı İçe Aktarın

```java
import com.aspose.cells.*;
```

İlk olarak Aspose.Cells kütüphanesini Java projenize dahil etmeniz gerekir. Bu kütüphane, Excel dosyalarıyla çalışmak ve grafik oluşturmak için kapsamlı işlevsellik sağlar.

### Adım 2: Çalışma Kitabı ve Çalışma Sayfası Başlatın

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Yeni bir çalışma kitabı oluşturun ve içine bir çalışma sayfası ekleyin. Bu sayfayı verileri girmek ve **çalışma sayfasına grafik eklemek** için kullanacağız.

### Adım 3: Verileri Girin

Şimdi, şelale grafiğinde temsil etmek istediğimiz verileri çalışma sayfasına dolduralım.

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

Bu örnekte, A sütununda kategoriler ve B sütununda ilgili değerler bulunuyor. Bu verileri kendi veri kümenizle değiştirebilirsiniz.

### Adım 4: Şelale Grafiğini Oluşturun

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Çalışma sayfamıza bir şelale grafiği ekledik, veri serisini ve kategori verisini belirttik. Bu, **şelale grafiği ekleyen** temel adımdır. `Chart` nesnesinin özelliklerini kullanarak grafik görünümünü (renkler, veri etiketleri vb.) daha da özelleştirebilirsiniz.

### Adım 5: Çalışma Kitabını Kaydedin

```java
workbook.save("WaterfallChart.xlsx");
```

Çalışma kitabını bir dosyaya kaydedin. Örnek XLSX formatını kullanıyor, ancak Aspose.Cells PDF, CSV ve birçok diğer formatta dışa aktarmayı da destekler. Bu, **workbook x kaydet** gereksinimini karşılar.

## Yaygın Sorunlar ve Çözümler

- **Grafik boş görünüyor** – Veri aralığı referanslarının (`B2:B6` ve `A2:A6`) gerçek hücrelerle eşleştiğinden emin olun.  
- **Negatif değerler doğru görüntülenmiyor** – Serinin türünün `ChartType.WATERFALL` olarak ayarlandığını kontrol edin; diğer grafik türleri negatifleri farklı işler.  
- **Dosya Excel’de açılamıyor** – Aspose.Cells’in (en son sürüm) güncel bir versiyonunu kullandığınızdan ve dosya uzantısının formatla eşleştiğinden (`.xlsx` Excel için) emin olun.

## Sık Sorulan Sorular

### Şelale grafiğimin görünümünü nasıl özelleştirebilirim?

Renkler, veri etiketleri ve eksen etiketleri gibi özellikleri değiştirerek şelale grafiğinizin görünümünü özelleştirebilirsiniz. Ayrıntılı rehberlik için Aspose.Cells belgelerine bakın.

### Aynı çalışma sayfasında birden fazla şelale grafiği oluşturabilir miyim?

Evet, farklı veri aralıklarıyla aynı adımları izleyerek aynı çalışma sayfasında birden fazla şelale grafiği oluşturabilirsiniz.

### Aspose.Cells farklı Java geliştirme ortamlarıyla uyumlu mu?

Evet, Aspose.Cells for Java Eclipse, IntelliJ IDEA, NetBeans gibi çeşitli Java geliştirme ortamlarıyla uyumludur.

### Şelale grafiğime ek veri serileri ekleyebilir miyim?

Elbette, şelale grafiğinize daha karmaşık veri senaryolarını etkili bir şekilde temsil etmek için ek veri serileri ekleyebilirsiniz.

### Aspose.Cells for Java için daha fazla kaynak ve örnek nereden bulabilirim?

Aspose.Cells for Java belgelerini [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) adresinde bulabilir, derinlemesine bilgi ve kod örneklerine ulaşabilirsiniz.

---

**Son Güncelleme:** 2025-12-10  
**Test Edilen Sürüm:** Aspose.Cells for Java 24.12 (latest)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}