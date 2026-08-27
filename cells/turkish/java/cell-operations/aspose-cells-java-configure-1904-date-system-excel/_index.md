---
date: '2026-02-22'
description: Aspose.Cells for Java kullanarak Excel tarih sistemini 1904'e nasıl değiştireceğinizi
  öğrenin, Excel tarih formatını ayarlayın ve Excel 1904 sistemini verimli bir şekilde
  dönüştürün.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Aspose.Cells Java ile Excel tarih sistemini 1904'e değiştir
url: /tr/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

)

Translate the labels but keep links unchanged.

So "Documentation:" -> "Dokümantasyon:" etc.

Now close shortcodes.

Let's assemble final content.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel tarih sistemini 1904'e Aspose.Cells Java ile değiştirin

Excel'de tarihsel verileri yönetmek zor olabilir çünkü Excel iki farklı tarih sistemini destekler. **Bu öğreticide Aspose.Cells for Java kullanarak Excel tarih sistemini 1904 formatına nasıl değiştireceğinizi öğreneceksiniz**, bu da eski tarihleri sorunsuz bir şekilde ele almanızı sağlar. Bir çalışma kitabını başlatma, 1904 tarih sistemini etkinleştirme ve değişikliği kalıcı hale getirme adımlarını göstereceğiz.

## Hızlı Yanıtlar
- **1904 tarih sistemi ne yapar?** 1 Ocak 1904'ten itibaren gün saymaya başlar ve varsayılan 1900 sistemine göre tüm tarihleri 1462 gün kaydırır.  
- **Tarih sistemini değiştirmek için neden Aspose.Cells kullanmalı?** Excel yüklü olmadan çalışan basit bir API sağlar ve büyük dosyaları destekler.  
- **Hangi Java sürümleri destekleniyor?** JDK 8 ve üzeri.  
- **Lisans gerekir mi?** Değerlendirme için ücretsiz deneme çalışır; bir lisans kullanım sınırlamalarını kaldırır.  
- **Daha sonra 1900 sistemine geri dönüp dönemez miyim?** Evet, sadece `setDate1904(false)` ayarlayın.

## Excel'de 1904 tarih sistemi nedir?
1904 tarih sistemi, ilk Macintosh Excel sürümlerinde orijinal olarak kullanılmıştır. 1 Ocak 1904'ten itibaren gün sayar ve eski elektronik tablolar ve bazı finansal modellerle uyumluluk için faydalıdır.

## Neden Excel tarih sistemini Aspose.Cells ile değiştirmelisiniz?
- **Çapraz platform uyumluluğu** – Windows, Linux ve macOS'ta çalışır.  
- **Excel kurulumu gerekmez** – sunucu tarafı işleme için idealdir.  
- **Yüksek performans** – büyük çalışma kitaplarını minimum bellek kullanımıyla işler.  

## Önkoşullar
- Java Development Kit (JDK) 8 ve üzeri.  
- Bağımlılık yönetimi için Maven veya Gradle.  
- Temel Java programlama bilgisi.  

## Aspose.Cells for Java'ı Kurma

### Maven
pom.xml dosyanıza aşağıdaki bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
`build.gradle` dosyanıza bu satırı ekleyin:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Lisans Edinme
Aspose ücretsiz deneme, geçici lisans ve tam ticari lisanslar sunar. [Ücretsiz deneme](https://releases.aspose.com/cells/java/) ile başlayabilir veya [geçici lisans sayfasından](https://purchase.aspose.com/temporary-license/) geçici bir lisans edinebilirsiniz.

## Aspose.Cells Java ile Excel tarih sistemini değiştirin

Aşağıda Excel tarih sistemini **gerçekten değiştiren** adım adım bir rehber bulunmaktadır. Her adım kısa bir açıklama ve ardından ihtiyacınız olan tam kodu içerir.

### Adım 1: Çalışma kitabını başlat ve yükle
İlk olarak, mevcut Excel dosyanıza işaret eden bir `Workbook` örneği oluşturun.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Adım 2: 1904 tarih sistemini etkinleştir
Tarih sistemini değiştirmek için çalışma kitabı ayarlarını kullanın.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro ipucu:** Daha sonra geri dönmeniz gerekirse `setDate1904(false)` çağırabilirsiniz.

### Adım 3: Değiştirilen çalışma kitabını kaydedin
Son olarak, değişiklikleri yeni bir dosyaya (veya orijinali üzerine yazarak) kaydedin.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Not:** Yukarıdaki kod, orijinal olarak verilen `tWorkbook` sınıf adını kullanıyor. Bu yazım hatasının projenizin adlandırma kurallarıyla eşleştiğinden emin olun veya gerekirse `Workbook` olarak düzeltin.

## Excel tarihini programlı olarak ayarlama (ikincil anahtar kelime)
Sistemi değiştirdikten sonra tek tek hücre değerlerini ayarlamanız gerekiyorsa, tarih aktif tarih sistemine göre yorumlanacak şekilde `Cells.get(i, j).putValue(Date)` kullanabilirsiniz.

## Excel 1904 sistemini 1900'e geri dönüştürme (ikincil anahtar kelime)
Geri dönmek için sadece şu kodu çağırın:

```java
workbook.getSettings().setDate1904(false);
```

Ardından çalışma kitabını tekrar kaydedin.

## Pratik Uygulamalar
1. **Veri Arşivleme** – Eski Mac tabanlı elektronik tabloları taşırken eski zaman damgalarını koruyun.  
2. **Çapraz Platform Raporlama** – Windows ve macOS'ta tarih uyumsuzluğu olmadan açılabilen raporlar oluşturun.  
3. **Finansal Modelleme** – 1904 sistemini bekleyen eski finansal modellerle tarih hesaplamalarını hizalayın.

## Performans Düşünceleri
- Tek bir oturumda çalışma kitabı işlemlerini sınırlayarak bellek kullanımını düşük tutun.  
- Çok büyük dosyalar için Java'nın çöp toplama ayarlarını kullanın.  

## Sıkça Sorulan Sorular

**S: 1900 ve 1904 tarih sistemleri arasındaki fark nedir?**  
C: 1900 sistemi 1 Ocak 1900'de başlarken, 1904 sistemi 1 Ocak 1904'te başlar ve tüm tarihleri 1462 gün kaydırır.

**S: Şu anda Excel'de açık olan bir çalışma kitabının tarih sistemini değiştirebilir miyim?**  
C: Evet, ancak önce dosyayı Excel'de kapatmanız gerekir; aksi takdirde kaydetme işlemi başarısız olur.

**S: `setDate1904` kullanmak için lisansa ihtiyacım var mı?**  
C: Metot ücretsiz denemede çalışır, ancak tam lisans değerlendirme sınırlamalarını kaldırır.

**S: Tarih sistemini sadece tek bir çalışma sayfası için değiştirmek mümkün mü?**  
C: Hayır, tarih sistemi çalışma kitabı düzeyinde bir ayardır; tüm çalışma sayfalarına uygulanır.

**S: Tarih sisteminin değiştirildiğini nasıl doğrulayabilirim?**  
C: Kaydedilen dosyayı Excel'de açın, **Dosya → Seçenekler → Gelişmiş** menüsüne gidin ve **"1904 tarih sistemini kullan"** kutusunu işaretleyin.

## Sonuç
Artık Aspose.Cells for Java kullanarak Excel tarih sistemini 1904'e **nasıl değiştireceğinizi**, Excel tarih formatlarını nasıl ayarlayacağınızı ve gerektiğinde nasıl geri dönüştüreceğinizi biliyorsunuz. Bu kod parçacıklarını veri işleme hatlarınıza ekleyerek platformlar arasında tarih uyumluluğunu garanti edebilirsiniz.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

**Resources**
- **Dokümantasyon:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **İndirme:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Lisans Satın Al:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Ücretsiz Deneme:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Geçici Lisans:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Destek Forum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}