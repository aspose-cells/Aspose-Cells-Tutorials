---
date: '2026-03-15'
description: Aspose Cells Java kullanarak adları ayrı sütunlara bölmeyi ve çalışma
  kitabını xlsx olarak kaydetmeyi adım adım bir öğreticide öğrenin.
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – İsimleri Sütunlara Böl
url: /tr/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ustalıkla **aspose cells java**: İsimleri Sütunlara Bölme

Kapsamlı **aspose cells java** öğreticimize hoş geldiniz. Bu rehberde, tek bir Excel sütununda depolanan **isimleri nasıl bölümlendireceğinizi** güçlü metin‑sütunlara‑bölme özelliğiyle iki ayrı sütuna—ilk ad ve soyad—bölmeyi öğreneceksiniz. İster bir iletişim listesini temizliyor olun, ister bir CRM içe aktarma için verileri hazırlıyor olun, ya da sadece elektronik tabloları yeniden yapılandırmak için hızlı bir yol ihtiyacınız olsun, bu öğretici dönüşümden sonra **save workbook xlsx** nasıl yapılacağını tam olarak gösterir.

## Hızlı Yanıtlar
- **Bu öğretici neyi kapsıyor?** Tam ad dizelerini Aspose.Cells for Java ile ilk ve soyad sütunlarına bölme.  
- **Hangi kütüphane sürümü kullanılıyor?** En son kararlı sürüm (2026 itibarıyla).  
- **Bir lisansa ihtiyacım var mı?** Geliştirme için ücretsiz deneme çalışır; üretim için ticari lisans gereklidir.  
- **Başka ayırıcılarla bölünebilir miyim?** Evet—`TxtLoadOptions` içindeki ayırıcıyı değiştirmeniz yeterlidir.  
- **Çıktı bir .xlsx dosyası mı?** Kesinlikle, çalışma kitabı XLSX formatında kaydedilir.

## **aspose cells java** nedir?
**Aspose.Cells java**, Microsoft Office gerektirmeden geliştiricilerin Excel dosyaları oluşturmasına, değiştirmesine, dönüştürmesine ve render etmesine olanak tanıyan yüksek performanslı bir Java API'sidir. Tüm ana Excel formatlarını destekler ve formüller, grafikler ve veri işleme gibi gelişmiş özellikler sunar.

## İsimleri bölmek için **aspose cells java** neden kullanılmalı?
- **Zero‑install**: Herhangi bir sunucu‑tarafı Java ortamında çalışır.  
- **Speed**: Büyük elektronik tabloları yerel Excel interop'undan daha hızlı işler.  
- **Precision**: Ayırıcılar, sütun aralıkları ve çıktı formatları üzerinde tam kontrol.  
- **Reliability**: COM veya Office bağımlılığı yoktur, bu da bulut veya konteyner dağıtımları için idealdir.

## Önkoşullar
- Java Development Kit (JDK) 8 veya daha yeni sürüm.  
- IntelliJ IDEA veya Eclipse gibi bir IDE (isteğe bağlı ancak önerilir).  
- Bağımlılık yönetimi için Maven veya Gradle.

### Maven Kurulumu
Add the Aspose.Cells dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle Kurulumu
Add the library to your `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tip:** Geliştirme sırasında tam işlevselliği açmak için Aspose portalından geçici bir lisans kullanın.

## Adım‑Adım Uygulama

### Adım 1: Bir Çalışma Kitabı Oluşturun ve İlk Çalışma Sayfasına Erişin
İlk olarak, temel sınıfları içe aktarın ve yeni bir çalışma kitabı örneği oluşturun. Bu, veri eklemeye hazır temiz bir Excel dosyası sağlar.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### Adım 2: Çalışma Sayfasını Örnek İsimlerle Doldurun
Sonra, **A** sütununa birkaç tam ad dizesi ekleyin. Gerçek bir projede bunları bir veritabanı veya CSV dosyasından okursunuz.

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### Adım 3: Sütun Bölme İçin Metin Yükleme Seçeneklerini Yapılandırın
`TxtLoadOptions` sınıfı, Aspose.Cells'e metni nasıl yorumlayacağını söyler. Burada ayırıcı olarak bir boşluk (`' '`) kullanıyoruz.

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### Adım 4: Metni İki Sütuna Bölün
Şimdi, isimleri içeren hücre alanında `textToColumns()` metodunu çağırın. `(0, 0, 5, opts)` parametreleri *satır 0, sütun 0'da başla, 5 satırı işle, az önce tanımladığımız seçenekleri kullan* anlamına gelir.

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

Bu çağrıdan sonra, A sütunu ilk adları, B sütunu ise soyadları tutar.

### Adım 5: Çalışma Kitabını XLSX Dosyası Olarak Kaydedin
Son olarak, değiştirilmiş çalışma kitabını diske yazın. `SaveFormat` enum'ı dosyanın modern XLSX formatında saklanmasını sağlar.

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **Neden önemli:** **save workbook xlsx** kullanarak, Excel, Google Sheets ve diğer elektronik tablo araçlarının en son sürümleriyle uyumluluğu garantilersiniz.

## Pratik Uygulamalar
- **Data Cleaning:** Analitik boru hatlarına yüklemeden önce birleştirilmiş alanları hızlıca ayırın.  
- **CRM Integration:** Düz bir iletişim listesini içe aktarım için yapılandırılmış bir tabloya dönüştürün.  
- **HR Systems:** Çalışan tam adlarını maaş veya fayda işlemleri için bölün.

## Performans Düşünceleri
Binlerce satırla çalışırken:

1. **Batch Updates:** `ws.getCells().setRowHeight()` veya benzeri toplu yöntemleri kullanarak yükü azaltın.  
2. **Memory Management:** `wb.calculateFormula()` yalnızca gerektiğinde çağırın ve büyük nesneleri hemen serbest bırakın.  
3. **Garbage Collection:** JVM'yi uygun yığın ayarlarıyla (`-Xmx2g` büyük dosyalar için) çalıştırarak OutOfMemory hatalarını önleyin.

## Yaygın Sorunlar ve Çözümler

| Sorun | Çözüm |
|-------|----------|
| **İsimler orta harf içeriyor** (örneğin “John A. Doe”) | Ayırıcıyı ayarlayın veya ikinci sütunu son adı çıkarmak için sonradan işleyin. |
| **Beklenmeyen boş hücreler** | Kaynak aralığın (`textToColumns` parametreleri) gerçek veri satırlarıyla eşleştiğini doğrulayın. |
| **Lisans bulunamadı** | Geçici lisans dosyasını (`Aspose.Cells.lic`) proje köküne yerleştirin veya lisansı programatik olarak ayarlayın. |

## Sıkça Sorulan Sorular

**Q:** Aspose.Cells Java nedir?  
A: Java kullanarak programlı bir şekilde Excel dosyaları oluşturmanıza, değiştirmenize ve dönüştürmenize olanak tanıyan güçlü bir kütüphane.

**Q:** Boşluk dışındaki ayırıcılarla sütunları bölebilir miyim?  
A: Evet, `TxtLoadOptions` ayırıcıyı verileriniz için gerektiği gibi özelleştirin.

**Q:** Aspose.Cells ile büyük veri setlerini nasıl yönetebilirim?  
A: Yukarıda açıklandığı gibi, belleği yöneterek ve çalışma kitabı işlemlerini en aza indirerek performansı optimize edin.

**Q:** Sorunlarla karşılaşırsam destek mevcut mu?  
A: Topluluk yardımı için [Aspose Forum](https://forum.aspose.com/c/cells/9) adresini ziyaret edin veya doğrudan Aspose destek ekibiyle iletişime geçin.

**Q:** Aspose.Cells çalışma kitaplarını hangi formatlarda kaydedebilir?  
A: XLSX, XLS, CSV ve daha fazlası dahil olmak üzere geniş bir Excel dosya formatı yelpazesini destekler.

## Kaynaklar

- **Dokümantasyon**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **İndirme**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **Satın Alma**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Ücretsiz Deneme**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **Geçici Lisans**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

Kodlamanın tadını çıkarın ve projelerinizde **aspose cells java**'ın tam gücünden yararlanın!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Son Güncelleme:** 2026-03-15  
**Test Edildi:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose