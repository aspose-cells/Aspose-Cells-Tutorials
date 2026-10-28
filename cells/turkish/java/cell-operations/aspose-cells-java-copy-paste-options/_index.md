---
date: '2026-10-28'
description: Java'da Aspose.Cells copy and paste seçeneklerini kullanarak değerleri
  nasıl yapıştıracağınızı, adım adım kod, Maven dependency kurulumu ve licensing ipuçlarıyla
  öğrenin.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Java'da Aspose.Cells copy and paste seçeneklerini kullanarak değerleri
  nasıl yapıştıracağınızı, adım adım kod, Maven dependency kurulumu ve licensing ipuçlarıyla
  öğrenin.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Aspose.Cells copy and paste seçenekleriyle değerleri nasıl yapıştırılır
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Aspose.Cells copy and paste seçenekleriyle değerleri nasıl yapıştırılır
url: /tr/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells kopyalama ve yapıştırma seçenekleriyle değerleri nasıl yapıştırılır

Excel raporlamasını Java’da otomatikleştirmek, Excel’i manuel olarak açmadan çalışma kitapları oluşturmanıza, birleştirmenize ve biçimlendirmenize olanak tanır. **Aspose.Cells** ile formüller, gizli satırlar ve hücre değerleri üzerinde tam kontrol elde eder, böylece raporlarınız doğru ve hafif kalır. Bu öğreticide **CopyOptions.ReferToDestinationSheet** kullanarak formüllerin doğru kalmasını ve **PasteOptions** ile yalnızca görünür değerleri nasıl yapıştıracağınızı öğreneceksiniz.

## Hızlı yanıtlar
- **`CopyOptions.ReferToDestinationSheet` ne yapar?** Kopyalama işleminden sonra formülleri hedef sayfaya yönlendirecek şekilde yeniden yazar.  
- **Yalnızca görünür hücreleri nasıl yapıştırırım?** `PasteOptions.setOnlyVisibleCells(true)` ile birlikte `PasteType.VALUES` çağırın.  
- **Hangi kütüphane sürümü gereklidir?** Aspose.Cells 25.3 veya daha yenisi.  
- **Üretim ortamı için lisansa ihtiyacım var mı?** Evet – kalıcı veya geçici bir lisans değerlendirme sınırlamalarını kaldırır.  
- **Maven veya Gradle kullanabilir miyim?** Her ikisi de desteklenir; aşağıdaki bağımlılık snippet’lerine bakın.

## “Excel raporlamasını otomatikleştirmek” ne demektir?
Excel raporlamasını otomatikleştirmek, Excel çalışma kitaplarını programlı olarak oluşturup güncellemeyi, raporları manuel kopyala‑yapıştır olmadan birleştirmeyi ve biçimlendirmeyi sağlar; bu da hataları azaltır ve tekrarlayan işleri saatlerce tasarruf ettirir. Bu yaklaşım zamanlanmış toplu işler, veri odaklı panolar ve finansal konsolidasyon hatları için idealdir.

## Raporlama için CopyOptions ve PasteOptions neden kullanılmalı?
Bu iki sınıf, veri kopyalarken formül referanslarını bozulmadan tutmanıza **ve** filtreleme ya da satır gizleme sonrası yalnızca görünür hücreleri çıkarmanıza olanak tanır. Birlikte kullanıldıklarında tipik filtreli tablo senaryolarında aktarılacak veri miktarını %80’e kadar azaltır ve formüllerin hedef sayfada doğru hesaplanmasını garanti eder.

## Önkoşullar
- Java 8 ve üzeri.  
- Bağımlılık yönetimi için Maven veya Gradle.  
- Aspose.Cells 25.3+ (deneme, geçici veya kalıcı lisans).  

## Aspose.Cells for Java kurulumu

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

### Lisans edinimi
- **Ücretsiz deneme** – değerlendirme için tam özellik seti.  
- **Geçici lisans** – test ederken deneme sınırlamalarını kaldırır.  
- **Kalıcı lisans** – üretim iş yükleri için önerilir.

Java kodunuzda Aspose.Cells’i başlatın:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Adım‑adım kılavuz

### 1. referToDestinationSheet ile copyOptions

#### Genel bakış
`CopyOptions`, Aspose.Cells'ın kopyalama işlemi sırasında formüllerin ve hücre referanslarının nasıl ele alınacağını kontrol eden yapılandırma nesnesidir. `CopyOptions.ReferToDestinationSheet` özelliğini `true` olarak ayarlamak, kopyalama işleminden sonra formül referanslarını yeni sayfaya yönlendirecek şekilde yeniden yazar.

#### Adım 1: çalışma kitabı ve sayfaları başlatma  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Adım 2: copyOptions yapılandırması  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Adım 3: kopyalama işlemini yürütme  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Neden önemli*: Başlangıçta `Sheet1`’e referans veren formüller artık `DestSheet`’e doğru referans verir, böylece otomatik raporlarınız güvenilir kalır.

**Sorun giderme ipucu**: Formüller hâlâ eski sayfaya referans veriyorsa, `setReferToDestinationSheet(true)` çağrısının **kopyalamadan önce** yapıldığından emin olun.

### 2. visible cells‑only için pasteOptions

#### Genel bakış
`PasteOptions`, Aspose.Cells'ın neyin yapıştırılacağını tanımlayan ayar nesnesidir. `PasteType.VALUES` ile birlikte `onlyVisibleCells=true` kullanmak, yalnızca görüntülenen değerleri kopyalar; gizli satır/sütunları ve biçimlendirmeyi yok sayar.

#### Adım 1: çalışma kitabı ve sayfaları başlatma  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Adım 2: pasteOptions yapılandırması  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Adım 3: yapıştırma işlemini yürütme  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Neden önemli*: Filtrelenmiş verileri çıkarmak veya gizli satır ve biçimlendirme gürültüsü olmayan temiz raporlar oluşturmak için idealdir.

**Sorun giderme ipucu**: Kopyalamadan önce satırların/sütunların gerçekten Excel’de gizli olduğundan emin olun; aksi takdirde dahil edilirler.

## Pratik uygulamalar
1. **Finansal konsolidasyon** – aylık sayfaları bir ana çalışma kitabına birleştirirken tüm formüllerin doğru kalmasını sağlar.  
2. **Filtreli veri dışa aktarımı** – filtrelenmiş bir tablodan yalnızca görünür satırları özet sayfaya çeker.  
3. **Zamanlanmış rapor üretimi** – gece yarısı Excel raporlarını doğru hücre değerleri ve doğru referanslarla otomatikleştirir.

## Performans hususları
- **Çalışma kitaplarını serbest bırakın** (`wb.dispose();`) ve yerel kaynakları serbest bırakın.  
- **Toplu işlemler** – birden fazla kopyala‑yapıştır çağrısını gruplayarak ek yükü azaltın.  
- **Belleği izleyin** – büyük çalışma kitapları daha yüksek yığın gerektirebilir (`-Xmx2g`).  
- Aspose.Cells **50+ giriş ve çıkış formatını** destekler ve **2 milyon satıra** kadar olan çalışma kitaplarını tüm dosyayı belleğe yüklemeden işleyebilir; bu da kurumsal iş yükleri için yüksek verimli performans sunar.

## Sıkça sorulan sorular

**S: `CopyOptions.ReferToDestinationSheet` ne için kullanılır?**  
C: Kopyalama sonrası formül referanslarını hedef sayfaya yönlendirerek raporlama formüllerinin doğru kalmasını sağlar.

**S: Yalnızca görünür hücreleri nasıl yapıştırırım?**  
C: `PasteOptions.setOnlyVisibleCells(true)` ayarlayın ve `PasteType.VALUES` seçin.

**S: Aspose.Cells’i lisans satın almadan kullanabilir miyim?**  
C: Evet, değerlendirme için ücretsiz deneme veya geçici lisans mevcuttur, ancak üretim için kalıcı lisans gereklidir.

**S: Kopyalama sonrası bazı referanslar hâlâ yanlış neden?**  
C: `ReferToDestinationSheet` özelliğinin **kopyalamadan önce** etkinleştirildiğini ve kaynak formüllerin harici çalışma kitabı bağlantıları içermediğini kontrol edin.

**S: Bellek yönetimiyle ilgili en iyi uygulamalar nelerdir?**  
C: `Workbook` nesnelerini iş bitince serbest bırakın, büyük dosyaları parçalara bölerek işleyin ve JVM yığın kullanımını izleyin.

**S: CopyOptions ve PasteOptions tek bir işlemde birleştirilebilir mi?**  
C: Evet, önce `CopyOptions` ile kopyalayıp ardından hedef aralıkta `PasteOptions` uygulayarak zincirleme yapabilirsiniz.

## Kaynaklar
- **Dokümantasyon**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **İndirme**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Satın Alma**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Ücretsiz deneme**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Geçici lisans**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Destek forumu**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Son güncelleme:** 2026-10-28  
**Test edilen sürüm:** Aspose.Cells 25.3 for Java  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Read Excel File Java – Master Workbook Cell Manipulation with Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Add Data to Cell in Excel Using Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convert Excel Cell Row Column Indices with Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}