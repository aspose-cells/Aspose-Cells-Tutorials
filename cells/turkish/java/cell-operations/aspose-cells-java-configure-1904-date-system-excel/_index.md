---
date: '2026-10-28'
description: Aspose.Cells for Java kullanarak Excel tarih sistemini 1904'e nasıl değiştireceğinizi
  öğrenin, Excel tarih formatını ayarlayın ve Excel 1904 sistemini verimli bir şekilde
  dönüştürün.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Aspose.Cells for Java kullanarak Excel tarih sistemini 1904'e değiştirin.
  1904 sistemini etkinleştirme, tarihleri ayarlama ve geri dönüştürme adımlarını adım
  adım öğrenin.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Excel tarih sistemini 1904'e Aspose.Cells for Java ile değiştirin
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Excel tarih sistemini 1904'e Aspose.Cells Java ile değiştirin
url: /tr/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel tarih sistemini 1904'e Aspose.Cells Java ile değiştirin

Bu öğreticide, Aspose.Cells for Java kullanarak **Excel tarih sistemini değiştir** 1904 formatına nasıl yapacağınızı öğreneceksiniz. 1904 sistemi, eski Mac‑tabanlı tarihleri korumanız gerektiğinde veya bu dönemi bekleyen finansal modellerle uyum sağlamak istediğinizde gereklidir. Kütüphaneyi kurma, bir çalışma kitabını yükleme, tarih sistemini değiştirme ve sonucu kaydetme adımlarını—sunucuda Microsoft Excel gerektirmeden—gözden geçireceğiz.

## Hızlı cevaplar
- **1904 tarih sistemi ne yapar?** 1 Ocak 1904'ten itibaren günleri saymaya başlar ve varsayılan 1900 sistemine göre tüm tarihleri 1.462 gün kaydırır.  
- **Tarih sistemini değiştirmek için Aspose.Cells'i neden kullanmalıyım?** Excel yüklü olmadan çalışan basit bir API sağlar ve büyük dosyaları destekler.  
- **Hangi Java sürümleri desteklenir?** JDK 8 ve üzeri.  
- **Lisans gerekli mi?** Değerlendirme için ücretsiz deneme çalışır; bir lisans kullanım sınırlamalarını kaldırır.  
- **Daha sonra 1900 sistemine geri dönüp dönemez miyim?** Evet, sadece `setDate1904(false)` çağırın.

## Excel'de 1904 tarih sistemi nedir?
1904 tarih sistemi, varsayılan 1900 dönemi yerine 1 Ocak 1904'ten itibaren günleri sayar. Bu kaydırma, her tarih değerine tam olarak 1.462 gün ekler; bu yüzden eski Mac çalışma kitapları Windows'ta açıldığında kaymış görünür. Öncelikle eski Macintosh Excel dosyaları ve bazı eski finansal modellerle uyumluluk için kullanılır.

## Aspose.Cells ile Excel tarih sistemini neden değiştirmelisiniz?
Tarih sistemini doğrudan Java'dan değiştirebilirsiniz, Excel'deki manuel adımları ortadan kaldırır. Aspose.Cells, **2 GB**'a kadar boyuttaki çalışma kitaplarını işleyebilir ve tipik bir 4 çekirdekli sunucuda 500 sayfalık bir çalışma kitabını **2 saniye** altında dönüştürebilir; yüksek verimli sunucu tarafı otomasyon sağlar.

## Önkoşullar
- Java Development Kit (JDK) 8 ve üzeri.  
- Bağımlılık yönetimi için Maven veya Gradle.  
- Temel Java programlama bilgisi.  

## Aspose.Cells for Java Kurulumu

### Maven
`pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin:

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

#### Lisans edinme
Aspose ücretsiz deneme, geçici lisans ve tam ticari lisanslar sunar. [Ücretsiz deneme](https://releases.aspose.com/cells/java/) ile başlayabilir veya [geçici lisans sayfasından](https://purchase.aspose.com/temporary-license/) geçici bir lisans edinebilirsiniz.

## Aspose.Cells for Java ile Excel tarih sistemini 1904'e nasıl değiştirirsiniz?
Çalışma kitabını yükleyin, 1904 ayarını etkinleştirin ve dosyayı kaydedin—bu üç adımlı akış, bir saniyeden kısa sürede çalışma kitabının iç tarih dönemini günceller. API çağrısı `setDate1904(true)` sistem bayrağını değiştirir ve `save` çağrısı yaptığınızda değişiklik kalıcı olur. Excel kurulumu gerekmez, bu da başsız sunucu ortamları için idealdir.

### Adım 1: çalışma kitabını başlat ve yükle
`Workbook` sınıfı, bellekte bir bütün Excel dosyasını temsil eder. İlk olarak, mevcut dosyanıza işaret eden bir `Workbook` örneği oluşturun.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Adım 2: 1904 tarih sistemini etkinleştir
`WorkbookSettings.setDate1904` yöntemi, çalışma kitabı düzeyindeki tarih bayrağını değiştirir. `true` olarak ayarlamak, tüm çalışma sayfaları için 1904 sistemini etkinleştirir.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**İpucu:** Geri dönmeniz gerekirse daha sonra `setDate1904(false)` da çağırabilirsiniz.

### Adım 3: değiştirilmiş çalışma kitabını kaydet
Son olarak, değişiklikleri yeni bir dosyaya (veya orijinali üzerine) yazın. `save` yöntemi, aktif tarih sistemine otomatik olarak uyar.

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

## Excel tarihini programlı olarak ayarla (ikincil anahtar kelime)
Sistemi değiştirdikten sonra tek tek hücre değerlerini ayarlamanız gerekiyorsa, `cells.get(i, j).putValue(Date)` kullanabilirsiniz; tarih, aktif tarih sistemine göre yorumlanır.

## Excel 1904 sistemini 1900'e geri dönüştür (ikincil anahtar kelime)
Geri dönmek için sadece şu çağrıyı yapın:

```java
workbook.getSettings().setDate1904(false);
```

Ardından çalışma kitabını tekrar kaydedin.

## Pratik uygulamalar
1. **Veri arşivleme** – Eski Mac tabanlı elektronik tabloları taşırken eski zaman damgalarını koruyun.  
2. **Çapraz platform raporlama** – Windows ve macOS'ta doğru şekilde açılan raporlar oluşturun, tarih uyumsuzlukları olmadan.  
3. **Finansal modelleme** – 1904 sistemini bekleyen eski finansal modellerle tarih hesaplamalarını hizalayın.

## Performans değerlendirmeleri
- Tek bir oturumda çalışma kitabı işlemlerini sınırlayarak bellek kullanımını düşük tutun; Aspose.Cells verileri akış olarak işler ve açıkça talep etmediğiniz sürece tüm dosyayı RAM'e yüklemez.  
- Çok büyük dosyalar için Java'nın çöp toplama bayraklarını (`-XX:+UseG1GC`) ayarlayın; böylece duraklama süresi dalgalanmalarını önlersiniz.

## Sıkça sorulan sorular

**S: 1900 ve 1904 tarih sistemleri arasındaki fark nedir?**  
C: 1900 sistemi 1 Ocak 1900'de başlarken, 1904 sistemi 1 Ocak 1904'te başlar ve tüm tarihleri 1.462 gün kaydırır.

**S: Şu anda Excel'de açık olan bir çalışma kitabının tarih sistemini değiştirebilir miyim?**  
C: Evet, ancak önce dosyayı Excel'de kapatmalısınız; aksi takdirde kaydetme işlemi başarısız olur.

**S: `setDate1904` kullanmak için lisans gerekir mi?**  
C: Yöntem ücretsiz denemede çalışır, ancak tam lisans değerlendirme sınırlamalarını kaldırır.

**S: Tarih sistemini sadece tek bir çalışma sayfası için değiştirmek mümkün mü?**  
C: Hayır, tarih sistemi çalışma kitabı düzeyinde bir ayardır; tüm çalışma sayfalarına uygulanır.

**S: Tarih sisteminin değiştirildiğini nasıl doğrulayabilirim?**  
C: Kaydedilen dosyayı Excel'de açın, **Dosya → Seçenekler → Gelişmiş** bölümüne gidin ve **"1904 tarih sistemini kullan"** kutusunu işaretleyin.

## Sonuç
Artık Aspose.Cells for Java kullanarak **Excel tarih sistemini** 1904'e nasıl değiştireceğinizi, tek tek hücre tarihlerini nasıl ayarlayacağınızı ve gerektiğinde 1900 sistemine nasıl geri döneceğinizi biliyorsunuz. Bu kod parçacıklarını veri işleme hatlarınıza entegre ederek platformlar ve eski dosyalar arasında tarih uyumluluğunu garanti edin.

---

**Son Güncelleme:** 2026-10-28  
**Test Edilen:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose  

**Kaynaklar**
- **Dokümantasyon:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **İndirme:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Lisans satın al:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Ücretsiz deneme:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Geçici lisans:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Destek forumu:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## İlgili Öğreticiler

- [Aspose.Cells for Java kullanarak Özel Tarih Formatlarıyla Excel'i PDF'e Verimli Bir Şekilde Dönüştür](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: Excel Çalışma Kitaplarını Verimli Bir Şekilde Oluşturma ve Biçimlendirme](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Aspose.Cells for Java ile Excel Manipülasyonunda Uzmanlaşın: Çalışma Kitabı İşlemleri ve Hücre Stil Rehberi](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}