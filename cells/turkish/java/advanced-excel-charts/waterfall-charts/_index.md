---
date: 2026-02-16
description: Aspose.Cells kullanarak Java’da grafik veri aralığını nasıl ayarlayacağınızı
  ve şelale grafiği oluşturacağınızı öğrenin. Veri serisi grafiği ekleme, özelleştirme
  ve XLSX olarak dışa aktarma adım adım rehberi.
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: Grafik Veri Aralığını Ayarla – Aspose.Cells for Java Şelale Grafiği
url: /tr/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

 formatting.

Let's craft final output.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Şelale Grafikler

## Aspose.Cells for Java kullanarak Şelale Grafiklerine Giriş

Bu öğreticide **set chart data range** nasıl ayarlanır ve Aspose.Cells for Java ile bir **waterfall chart** nasıl oluşturulur öğreneceksiniz. Şelale grafikleri, pozitif ve negatif değerlerin bir dizi halinde kümülatif etkisini görmenizi sağladığı için veri görselleştirmede vazgeçilmez bir araçtır. Finansal bir tablo, satış performans raporu ya da başka bir veri‑odaklı analiz hazırlıyor olun, şelale grafiği ham sayıları net, eyleme dönüştürülebilir içgörülere dönüştürebilir.

## Hızlı Yanıtlar
- **Şelale grafiği nedir?** Başlangıç değerinin bir dizi ara değerle artırılıp azaltıldığını gösteren ve sonunda toplam bir değerle biten görsel.  
- **Hangi kütüphane kullanılıyor?** Aspose.Cells for Java.  
- **Lisans gerekli mi?** Geliştirme için ücretsiz deneme yeterlidir; üretim ortamı için ticari lisans gerekir.  
- **Dosyayı XLSX olarak kaydedebilir miyim?** Evet – `workbook.save("FileName.xlsx")` kullanın.  
- **Java veri görselleştirmesi için uygun mu?** Kesinlikle; Aspose.Cells, Office yüklü olmadan zengin grafik özellikleri sunar.

## Şelale Grafiği Nedir?
Şelale grafiği, bir başlangıç değerine sıralı pozitif ve negatif katkıları göstererek her bir bileşenin genel sonuca nasıl etki ettiğini anlamanızı sağlar.

## Aspose.Cells for Java ile Şelale Grafiği Eklemek Neden?
- **Microsoft Excel gerekmez** – herhangi bir sunucu veya CI boru hattında grafikler oluşturun.  
- **Biçimlendirme üzerinde tam kontrol** – renkler, veri etiketleri ve eksenler programlı olarak özelleştirilebilir.  
- **Birden fazla çıktı formatını destekler** – XLSX, PDF, HTML ve daha fazlası.  
- **Yüksek performans** – büyük çalışma kitapları ve otomatik raporlama için idealdir.

## Önkoşullar

Kodun içine dalmadan önce aşağıdaki önkoşulların sağlandığından emin olun:

- Aspose.Cells for Java: Aspose.Cells for Java yüklü olmalıdır. [buradan](https://releases.aspose.com/cells/java/) indirebilirsiniz.  
- Java Geliştirme Ortamı: Sisteminizde Java yüklü olduğundan emin olun.

Şimdi adım adım şelale grafiği oluşturmaya başlayalım.

## Java’da Şelale Grafiği İçin Grafik Veri Aralığını Nasıl Ayarlarsınız

### Adım 1: Aspose.Cells'i İçe Aktarın

```java
import com.aspose.cells.*;
```

İlk olarak Aspose.Cells kütüphanesini Java projenize dahil etmeniz gerekir. Bu kütüphane, Excel dosyalarıyla çalışmak ve grafik oluşturmak için kapsamlı işlevsellik sağlar.

### Adım 2: Çalışma Kitabı ve Çalışma Sayfasını Başlatın

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Yeni bir çalışma kitabı oluşturun ve içine bir çalışma sayfası ekleyin. Bu çalışma sayfasını verileri girmek ve **add chart to worksheet** için kullanacağız.

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

Bu örnekte, A sütununda kategoriler ve B sütununda karşılık gelen değerler bulunuyor. Bu verileri kendi veri kümenizle değiştirebilirsiniz.

### Adım 4: Şelale Grafiğini Oluşturun

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

Çalışma sayfamıza bir şelale grafiği ekledik, veri serisini ve kategori verisini belirttik. Bu, **adds waterfall chart** adımıdır. `add` metodunun `"B2:B6"` aralığını kullandığına dikkat edin – burada serinin **set chart data range** ayarlanıyor. `Chart` nesnesinin özelliklerini kullanarak grafik görünümünü (renkler, veri etiketleri vb.) daha da özelleştirebilirsiniz.

### Adım 5: Çalışma Kitabını Kaydedin

```java
workbook.save("WaterfallChart.xlsx");
```

Çalışma kitabını bir dosyaya kaydedin. Örnek XLSX formatını kullanıyor, ancak Aspose.Cells **export excel pdf java**‑uyumlu dosyalar (PDF, CSV vb.) oluşturmanıza da izin verir. Bu, **save workbook xlsx** gereksinimini karşılar.

## Yaygın Sorunlar ve Çözümler

- **Grafik boş görünüyor** – Veri aralığı referanslarının (`B2:B6` ve `A2:A6`) değer ve kategori hücrelerinizle eşleştiğinden emin olun.  
- **Negatif değerler doğru görüntülenmiyor** – Serinin türünün `ChartType.WATERFALL` olduğundan emin olun; diğer grafik türleri negatifleri farklı işler.  
- **Dosya Excel'de açılamıyor** – Aspose.Cells'in en son sürümünü (en yeni sürüm) kullandığınızdan ve dosya uzantısının formatla eşleştiğinden emin olun (`.xlsx` Excel için).

## Sık Sorulan Sorular

### Şelale grafiğimin görünümünü nasıl özelleştirebilirim?

Renkler, veri etiketleri ve eksen etiketleri gibi özellikleri değiştirerek şelale grafiğinizin görünümünü özelleştirebilirsiniz. Ayrıntılı rehberlik için Aspose.Cells belgelerine bakın.

### Aynı çalışma sayfasında birden fazla şelale grafiği oluşturabilir miyim?

Evet, farklı veri aralıklarıyla aynı adımları izleyerek aynı çalışma sayfasında birden fazla şelale grafiği oluşturabilirsiniz.

### Aspose.Cells farklı Java geliştirme ortamlarıyla uyumlu mu?

Evet, Aspose.Cells for Java Eclipse, IntelliJ IDEA ve NetBeans dahil olmak üzere çeşitli Java geliştirme ortamlarıyla uyumludur.

### Şelale grafiğime ek veri serileri ekleyebilir miyim?

Elbette, karmaşık veri senaryolarını etkili bir şekilde temsil etmek için şelale grafiğinize daha fazla veri serisi ekleyebilirsiniz. Bu, **add data series chart** programlı olarak nasıl yapılır örneğidir.

### Aspose.Cells for Java için daha fazla kaynak ve örnek nerede bulunur?

Aspose.Cells for Java belgelerini [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) adresinde bulabilir, derinlemesine bilgi ve kod örneklerine ulaşabilirsiniz.

## SSS

**S: Finansal bir şelale grafiği için grafik veri aralığını nasıl ayarlarım?**  
C: Değerlerin bulunduğu hücre aralığını (`"B2:B6"` gibi) belirterek grafiğin serisine `add` metodunu uygulayın.

**S: Çalışma kitabını XLSX yerine PDF olarak dışa aktarabilir miyim?**  
C: Evet, `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` çağrısını yaparak **export excel pdf java**‑uyumlu çıktı alabilirsiniz.

**S: Daha fazla kategori içeren bir finansal şelale grafiği oluşturmam gerekirse ne yapmalıyım?**  
C: Hem değer sütununda hem de kategori sütununda veri aralığını genişletin, ardından `add` ve `setCategoryData` çağrılarını buna göre güncelleyin.

**S: Pozitif ve negatif çubukları otomatik olarak biçimlendirmek mümkün mü?**  
C: `Series` koleksiyonunu döngüyle gezerek her değerin işaretine göre `FillFormat` rengini ayarlayabilirsiniz.

**S: Aspose.Cells grafikler için dinamik veri güncellemelerini destekliyor mu?**  
C: Evet, grafiği oluşturduktan sonra hücre değerlerini değiştirebilirsiniz; çalışma kitabı kaydedildiğinde grafik bu değişiklikleri yansıtacaktır.

---

**Son Güncelleme:** 2026-02-16  
**Test Edilen Versiyon:** Aspose.Cells for Java (en son)  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}