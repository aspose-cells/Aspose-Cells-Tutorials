---
date: '2026-03-28'
description: Aspose.Cells for Java kullanarak Excel grafiklerine gizli bir filigran
  eklemeyi, Aspose Cells Maven bağımlılığını ve WordArt stilini içerecek şekilde öğrenin.
keywords:
- Aspose.Cells Java
- Excel chart watermark
- WordArt in Excel
title: Aspose.Cells for Java ile Excel Grafiğine Gizli Su İşareti Ekleme
url: /tr/java/charts-graphs/add-wordart-watermark-excel-chart-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for Java Kullanarak Gizli Filigranlı Excel Grafiği Nasıl Eklenir

## Giriş

Bu öğreticide, Aspose.Cells for Java kullanarak **Excel grafiğine gizli bir filigran eklemeyi** öğreneceksiniz. Bir WordArt filigranı yalnızca markalaşmayı güçlendirmekle kalmaz, aynı zamanda gizliliği de gösterir—“CONFIDENTIAL” olarak işaretlenmiş raporlar için mükemmeldir. Maven bağımlılığını kurmaktan son çalışma kitabını kaydetmeye kadar tam süreci adım adım göstereceğiz.

**Neler Öğreneceksiniz**
- Aspose.Cells for Java kullanarak Excel grafiklerine WordArt filigranı ekleme.  
- Grafik filigranlarının şeffaflığını ve çizgi formatlarını ayarlama teknikleri.  
- Değiştirilmiş çalışma kitabınızı kaydetmek için en iyi uygulamalar.

## Hızlı Yanıtlar
- **Anahtar kelimenin anlamı nedir?** Excel grafiğine gizli bir filigran eklemek, hassas verileri korur.  
- **Hangi kütüphane gereklidir?** Aspose.Cells for Java (Maven bağımlılığına bakın).  
- **Metin efektini özelleştirebilir miyim?** Evet, `MsoPresetTextEffect` seçeneklerini kullanarak.  
- **Lisans gerekli mi?** Deneme sürümü test için çalışır; üretim için kalıcı bir lisans gereklidir.  
- **Performansı etkileyecek mi?** Minimum etki; sadece birkaç ekstra nesne oluşturulur.

## Excel'de Gizli Filigran Nedir?
Gizli bir filigran, içeriğin hassas olduğunu göstermek için grafik verilerinin arkasına yerleştirilen yarı şeffaf bir metin veya grafiktir. Alttaki verileri gizlemeden, baskıda ve ekranda görünür kalır.

## Filigran Eklemek İçin Neden Aspose.Cells Kullanılmalı?
Aspose.Cells, Microsoft Office gerektirmeden Excel dosyalarını manipüle etmek için zengin bir API sunar. WordArt şekillerini, ayrıntılı şeffaflık kontrolünü destekler ve tüm Java platformlarında çalışır.

## Önkoşullar
- Java Development Kit (JDK) yüklü ve yapılandırılmış.  
- IntelliJ IDEA veya Eclipse gibi bir IDE.  
- Temel Java bilgisi ve Maven/Gradle ile aşinalık.

### Gerekli Kütüphaneler
Aşağıda gösterildiği gibi Maven veya Gradle kullanarak projenize Aspose.Cells kütüphanesini ekleyin.

### Ortam Kurulum Gereksinimleri
- Java Development Kit (JDK) yüklü ve yapılandırılmış.  
- Geliştirme için IntelliJ IDEA veya Eclipse gibi bir IDE.

### Bilgi Önkoşulları
Java programlaması, Aspose.Cells ile Excel dosyası manipülasyonu ve Maven/Gradle yapı araçları hakkında temel bir anlayış önerilir.

## Aspose Cells Maven Bağımlılığı
Aspose.Cells'i kullanmaya başlamak için projenize ekleyin.

**Maven:**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

## Lisans Edinimi
Aspose'un satın alma seçenekleriyle bir lisans edinin veya sitelerinden geçici lisansı indirerek ücretsiz deneme ile başlayın. Kurulumunuzu şu şekilde başlatın:
```java
// Load an existing workbook and apply a license if available.
Workbook workbook = new Workbook("path_to_license_file");
```

## Uygulama Kılavuzu
Uygulamayı net bölümlere ayıralım.

### Grafiğe WordArt Filigranı Ekle
1. **Mevcut Bir Excel Dosyasını Aç**  
   Filigranı eklemek istediğiniz Excel dosyanızı yükleyin:  
```java
String dataDir = Utils.getSharedDataDir(AddWordArtWatermarkToChart.class) + "TechnicalArticles/";
Workbook workbook = new Workbook(dataDir + "sample.xlsx");
```

2. **Grafiğe Eriş**  
   Değiştirmek istediğiniz ilk çalışma sayfasındaki grafiği alın:  
```java
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
```

3. **WordArt Şekli Ekle**  
   Grafiğinizin çizim alanına yeni bir WordArt şekli ekleyin:  
```java
Shape wordart = chart.getShapes().addTextEffectInChart(
    MsoPresetTextEffect.TEXT_EFFECT_1,
    "CONFIDENTIAL",
    "Arial Black", 66, false, false, 
    1200, 500, 2000, 3000);
```

4. **Dolgu ve Çizgi Formatını Yapılandır**  
   Filigranı hafif yapmak için şeffaflığı ayarlayın:  
```java
// Configure transparency.
FillFormat wordArtFormat = wordart.getFill();
wordArtFormat.setTransparency(0.9);

// Make line format invisible.
LineFormat lineFormat = wordart.getLine();
lineFormat.setWeight(0.0);
```

5. **Çalışma Kitabını Kaydet**  
   Değişikliklerinizi yeni bir dosyaya kaydedin:  
```java
workbook.save(dataDir + "AWArtWToC_out.xlsx");
```

### Sorun Giderme İpuçları
- Dosyaları yüklemek ve kaydetmek için tüm yolların doğru belirtildiğinden emin olun.  
- Dizinde okuma/yazma izninizin olduğundan emin olun.  
- Aspose.Cells sürümünün Java ortamınızla uyumlu olduğunu kontrol edin.

## Pratik Uygulamalar
WordArt filigranı eklemek aşağıdaki senaryolarda faydalı olabilir:
1. **Markalaşma** – Tutarlı bir markalaşma için tüm grafiklerde şirket logolarını veya sloganlarını kullanın.  
2. **Gizlilik** – Yetkisiz paylaşımı önlemek için gizli raporları işaretleyin.  
3. **Sürüm Kontrolü** – Belge onay aşamalarında sürüm numaralarını ekleyin.

## Performans Düşünceleri
Aspose.Cells kullanırken şunları göz önünde bulundurun:
- Artık ihtiyaç duyulmayan nesneleri serbest bırakarak verimli bellek yönetimi.  
- Mümkün olduğunca dosya G/Ç işlemlerini azaltarak performansı optimize etme.  
- Büyük çalışma kitapları veya karmaşık manipülasyonlar için çoklu iş parçacığı kullanma.

## Sonuç
Artık Aspose.Cells for Java kullanarak **Excel grafiğine gizli bir filigran ekleme** konusunda işlevsel bir anlayışa sahipsiniz. Bu özellik görsel çekiciliği artırır ve belgelerinize bir güvenlik katmanı ekler. Daha fazla keşif için farklı metin efektleriyle denemeler yapın veya bu işlevi daha büyük uygulamalara entegre edin.

## Sık Sorulan Sorular
1. **Aspose.Cells nedir?**  
   - Java'da Excel dosyalarını yönetmek için güçlü bir kütüphane.  
2. **Aspose.Cells ile nasıl başlayabilirim?**  
   - Maven/Gradle üzerinden kurun ve gerekirse bir lisans ayarlayın.  
3. **Filigrana farklı metin efektleri ekleyebilir miyim?**  
   - Evet, çeşitli stiller için `MsoPresetTextEffect` seçeneklerini keşfedin.  
4. **Şeffaflık ayarlarken yaygın sorunlar nelerdir?**  
   - Şeffaflık seviyesinin 0 (opak) ile 1 (tamamen şeffaf) arasında olduğundan emin olun.  
5. **Aspose.Cells hakkında daha fazla kaynağı nerede bulabilirim?**  
   - Kapsamlı kılavuzlar için [Dokümantasyon](https://reference.aspose.com/cells/java/) sayfasını ziyaret edin.

## Kaynaklar
- [Dokümantasyon](https://reference.aspose.com/cells/java/)
- [En Son Sürümü İndir](https://releases.aspose.com/cells/java/)
- [Lisans Satın Al](https://purchase.aspose.com/buy)
- [Ücretsiz Deneme](https://releases.aspose.com/cells/java/)
- [Geçici Lisans](https://purchase.aspose.com/temporary-license/)
- [Destek Forumu](https://forum.aspose.com/c/cells/9)

## Sık Sorulan Sorular

**S: Filigran, yazdırılan Excel sayfalarında görünür mü?**  
Evet, WordArt şekli grafiğin bir parçasıdır ve grafik verileriyle birlikte yazdırılır.

**S: Aynı filigranı birden fazla grafik üzerine otomatik olarak uygulayabilir miyim?**  
`workbook.getWorksheets().get(i).getCharts()` üzerinde döngü yaparak aynı adımları her grafik için uygulayın.

**S: Filigran rengini değiştirmek mümkün mü?**  
Kesinlikle—özel bir renk ayarlamak için `wordArtFormat.getSolidFill().setColor(Color.getRGB(255,0,0))` kullanın.

**S: Filigran eklemek dosya boyutunu önemli ölçüde artırır mı?**  
Artış minimaldir, çünkü sadece tek bir şekil nesnesi eklenir.

**S: Filigranı daha sonra nasıl kaldırabilirim?**  
Şekli `chart.getShapes()` içinde adı veya indeksiyle bulun ve `shape.delete()` çağırın.

---

**Son Güncelleme:** 2026-03-28  
**Test Edilen Sürüm:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}