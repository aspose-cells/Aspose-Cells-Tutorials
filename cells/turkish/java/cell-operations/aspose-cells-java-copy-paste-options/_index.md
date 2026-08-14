---
date: '2026-02-22'
description: CopyOptions ve PasteOptions kullanarak formüllerin doğru kalmasını ve
  yalnızca görünen değerlerin yapıştırılmasını sağlayarak Java’da Aspose.Cells ile
  Excel raporlamasını otomatikleştirmeyi öğrenin.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Excel Raporlamasını Otomatikleştirin – Aspose.Cells ile Java’da CopyOptions
  ve PasteOptions’ı Ustalıkla Kullanma
url: /tr/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.Cells ile Excel Raporlamasını Otomatikleştirme: CopyOptions ve PasteOptions

Java kullanarak **Excel raporlamasını otomatikleştirmek** ister misiniz? Aspose.Cells ile formülleri programlı olarak kopyalayıp yapıştırabilir ve yalnızca ihtiyacınız olan verileri aktararak raporlarınızın doğru kalmasını sağlayabilirsiniz. Bu öğreticide, formül referanslarını korumanızı ve yalnızca görünen hücrelerin değerlerini yapıştırmanızı sağlayan iki temel özellik—**CopyOptions.ReferToDestinationSheet** ve **PasteOptions**—üzerinden geçeceğiz.

## Hızlı Yanıtlar
- **`CopyOptions.ReferToDestinationSheet` ne işe yarar?** Verileri kopyalarken formülleri hedef sayfaya yönlendirir.  
- **Yalnızca görünen hücreleri nasıl yapıştırırım?** `PasteOptions.setOnlyVisibleCells(true)` ile `PasteType.VALUES` kullanın.  
- **Hangi kütüphane sürümü gereklidir?** Aspose.Cells 25.3 veya daha yenisi.  
- **Üretim ortamında lisansa ihtiyacım var mı?** Evet, kalıcı veya geçici bir lisans değerlendirme sınırlamalarını kaldırır.  
- **Maven veya Gradle kullanabilir miyim?** Her ikisi de desteklenir; aşağıdaki bağımlılık snippet'lerine bakın.

## “Excel raporlamasını otomatikleştirmek” ne demektir?
Excel raporlamasını otomatikleştirmek, Excel çalışma kitaplarını programlı olarak oluşturmak, birleştirmek ve biçimlendirmek anlamına gelir; manuel kopyala‑yapıştır adımlarını ortadan kaldırır ve hataları azaltır. Aspose.Cells, Java geliştiricilerinin elektronik tabloları ölçekli bir şekilde manipüle etmelerini sağlayan zengin bir API sunar.

## Raporlama için CopyOptions ve PasteOptions neden kullanılmalı?
- **Formül bütünlüğünü koruma**: Veri sayfalar arasında taşındığında formüller bozulmaz.  
- **Gizli satır/sütunları dışarıda bırakma**: Raporlar daha temiz ve odaklı olur.  
- **Performansı artırma**: Tüm aralıklar yerine yalnızca gerekli veriler kopyalanır.

## Ön Koşullar
- Java 8 ve üzeri.  
- Bağımlılık yönetimi için Maven veya Gradle.  
- Aspose.Cells 25.3+ (deneme, geçici veya kalıcı lisans).  

## Java için Aspose.Cells Kurulumu

Projeye aşağıdaki yöntemlerden biriyle kütüphane ekleyin:

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Lisans Edinme
- **Ücretsiz Deneme** – Değerlendirme için tam özellik seti.  
- **Geçici Lisans** – Test aşamasında deneme kısıtlamalarını kaldırır.  
- **Kalıcı Lisans** – Üretim yükleri için önerilir.

Java kodunuzda Aspose.Cells’i başlatın:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Adım‑Adım Kılavuz

### 1. ReferToDestinationSheet ile CopyOptions

#### Genel Bakış
`CopyOptions.ReferToDestinationSheet` değerini `true` yapmak, kopyalama işleminden sonra formül referanslarını yeni sayfaya yönlendirir.

#### Adım 1: Workbook ve Worksheet’leri Başlatma
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Adım 2: CopyOptions’u Yapılandırma
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Adım 3: Kopyalama İşlemini Gerçekleştirme
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Neden önemli*: Başlangıçta `Sheet1`’e referans veren formüller, artık `DestSheet`’e doğru referans verir ve otomatik raporlarınız güvenilir kalır.

**Sorun Giderme İpucu**: Formüller hâlâ eski sayfaya referans veriyorsa, `setReferToDestinationSheet(true)` çağrısının **kopyalamadan önce** yapıldığından emin olun.

### 2. Görünür Hücrelerden Yalnızca Değerler İçin PasteOptions

#### Genel Bakış
`PasteOptions`, neyin yapıştırılacağını tanımlamanızı sağlar. `PasteType.VALUES` ile `onlyVisibleCells=true` kombinasyonu, gizli satır/sütunları ve biçimlendirmeyi yok sayarak yalnızca görüntülenen değerleri kopyalar.

#### Adım 1: Workbook ve Worksheet’leri Başlatma
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Adım 2: PasteOptions’u Yapılandırma
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Adım 3: Yapıştırma İşlemini Gerçekleştirme
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Neden önemli*: Filtrelenmiş verileri çıkarmak veya gizli satır/sütun içermeyen temiz raporlar oluşturmak için idealdir.

**Sorun Giderme İpucu**: Kopyalamadan önce satırların/sütunların gerçekten Excel’de gizli olduğundan emin olun; aksi takdirde dahil edilirler.

## Pratik Uygulamalar
1. **Finansal Konsolidasyon** – Aylık sayfaları bir ana çalışma kitabına birleştirirken tüm formüllerin doğru kalmasını sağlar.  
2. **Filtrelenmiş Veri Dışa Aktarma** – Filtreli bir tablodan yalnızca görünür satırları özet sayfaya çeker.  
3. **Planlı Rapor Oluşturma** – Gece yarısı Excel raporlarını, doğru hücre değerleri ve doğru referanslarla otomatik olarak üretir.

## Performans Düşünceleri
- **Workbook’ları serbest bırakın** (`wb.dispose();`) native kaynakları temizlemek için.  
- **Toplu İşlemler** – Birden fazla kopyala/yapıştır çağrısını gruplayarak ek yükü azaltın.  
- **Belleği İzleyin** – Büyük çalışma kitapları için heap artırımı gerekebilir (`-Xmx2g`).

## Sıkça Sorulan Sorular

**S1: `CopyOptions.ReferToDestinationSheet` ne için kullanılır?**  
C: Kopyalama sonrası formül referanslarını hedef sayfaya yönlendirir, böylece rapor formülleri doğru kalır.

**S2: Yalnızca görünen hücreleri nasıl yapıştırırım?**  
C: `PasteOptions.setOnlyVisibleCells(true)` ayarlayın ve `PasteType.VALUES` seçin.

**S3: Aspose.Cells’i lisans satın almadan kullanabilir miyim?**  
C: Değerlendirme için ücretsiz deneme veya geçici lisans mevcuttur, ancak üretim için kalıcı lisans gerekir.

**S4: Kopyalama sonrası bazı referanslar hâlâ yanlış neden?**  
C: `ReferToDestinationSheet` özelliğinin **kopyalamadan önce** etkinleştirildiğini ve kaynak formüllerin dış çalışma kitabı bağlantısı içermediğini kontrol edin.

**S5: Bellek yönetimi konusunda hangi en iyi uygulamaları izlemeliyim?**  
C: `Workbook` nesnelerini iş bitince serbest bırakın, büyük dosyaları parçalar halinde işleyin ve JVM heap kullanımını izleyin.

**S6: CopyOptions ve PasteOptions tek bir işlemde birleştirilebilir mi?**  
C: Evet, önce `CopyOptions` ile kopyalayıp ardından hedef aralıkta `PasteOptions` uygulayarak zincirleme yapabilirsiniz.

## Kaynaklar
- **Dokümantasyon**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **İndirme**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Satın Alma**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Ücretsiz Deneme**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Geçici Lisans**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Destek Forumu**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Son Güncelleme:** 2026-02-22  
**Test Edilen Sürüm:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose