---
category: general
date: 2026-11-16
description: Java’da Excel çalışma kitapları arasında hücreleri nasıl kopyalanır –
  bir çalışma kitabını yükle, çalışma kitapları arasında (pivot tablo dahil) bir aralığı
  kopyala ve çalışma kitabı dosyasını kaydet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: tr
lastmod: 2026-11-16
og_description: Java’da Excel çalışma kitapları arasında hücreleri nasıl kopyalanır.
  Bir Excel çalışma kitabını nasıl yükleyeceğinizi, bir aralığı (pivot tablo dahil)
  çalışma kitapları arasında nasıl kopyalayacağınızı ve çalışma kitabı dosyasını nasıl
  kaydedeceğinizi öğrenin.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Java'da Excel çalışma kitapları arasında hücreleri nasıl kopyalarsınız –
  tam kılavuz
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Java'da Excel çalışma kitapları arasında hücreleri nasıl kopyalarım
url: /tr/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Excel çalışma kitapları arasında hücreleri nasıl kopyalarsınız

Bir Excel çalışma kitabından diğerine **hücreleri kopyalamanız** gerektiğinde, bu kılavuz güvenilir bir yöntemi gösterir. **Excel çalışma kitabını Java ile yükleme**, bir pivot tablo içerebilecek bir aralığı kopyalama ve sonunda **kopyalanan verilerle çalışma kitabı dosyasını kaydetme** konularını öğreneceksiniz.

Bu öğreticide şunlar ele alınmaktadır:

* Kaynak bir çalışma kitabını yükleme ve bir çalışma sayfası seçme.  
* Taşımak istediğiniz kesin aralığı tanımlama (pivot tablo dahil).  
* Hedef bir çalışma kitabı oluşturma ve aralığı kopyalama.  
* Hedef dosyayı kaydetme.  

Örnek, Microsoft Office gerektirmeden Excel dosyalarıyla çalışabilen Aspose.Cells for Java kütüphanesini kullanır. Kod, Java 8+ ve herhangi bir modern IDE (IntelliJ IDEA, Eclipse, VS Code vb.) üzerinde çalışır.

---

## Önkoşullar

Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

| Gereksinim | Açıklama |
|-------------|----------|
| Java Development Kit (JDK) 8 veya daha yeni bir sürüm | Kodu derlemek ve çalıştırmak için gereklidir. |
| Maven veya Gradle yapı aracı | Aspose.Cells bağımlılığını eklemeyi kolaylaştırır. |
| Aspose.Cells for Java kütüphanesi (en son sürüm) | Örnekte kullanılan `Workbook`, `Worksheet` ve `Range` sınıflarını sağlar. |
| İki Excel dosyası (`source.xlsx` ve `dest.xlsx` için boş bir klasör) | Kaynak dosya, kopyalamak istediğiniz verileri ve isteğe bağlı olarak bir pivot tabloyu içermelidir. |

Aspose.Cells bağımlılığını `pom.xml` (Maven) ya da `build.gradle` (Gradle) dosyanıza ekleyin. Maven için örnek:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Aspose.Cells ile hücreleri nasıl kopyalarsınız

Aşağıdaki adımlar, sürecin tamamını adım adım gösterir. Her adımda Java kodu, adımın **neden** önemli olduğu ve yaygın hatalardan kaçınmak için bir ipucu bulunur.

### Adım 1: Kaynak çalışma kitabını yükleyin

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**Neden?**  
`Workbook`, tüm Excel dosyasını temsil eder. Onu yüklemek, tüm çalışma sayfalarına, hücrelere ve pivot tablolar gibi nesnelere erişmenizi sağlar. İlk çalışma sayfasını kullanmak yaygındır, ancak isterseniz adıyla (`srcWb.getWorksheets().get("Sheet2")`) başka bir sayfayı da seçebilirsiniz.

**İpucu:**  
Kaynak dosya büyükse, *bellek‑verimli* modda yüklemeyi düşünün: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }})`

### Adım 2: Pivot tabloyu içeren aralığı tanımlayın

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**Neden?**  
`Range` nesnesi, dikdörtgen bir hücre bloğunu soyutlar. `"A1:G20"` adresini belirterek Aspose.Cells'e, içinde gömülü bir pivot tablo olsun, hangi hücreleri kopyalayacağını söylersiniz. Kütüphane, alttaki veri, stil ve pivot tanımlarını otomatik olarak kopyalar.

**Köşe durumu:**  
Pivot tablo tanımlı aralığın dışına çıkıyorsa, adresi genişletin (ör. `"A1:Z100"`). Kullanılan alanı dinamik olarak hesaplamak için `srcWs.getCells().getMaxDataColumn()` ve `getMaxDataRow()` yöntemlerini de kullanabilirsiniz.

### Adım 3: Hedef çalışma kitabını oluşturun

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**Neden?**  
Yeni bir çalışma kitabı, istenmeyen biçimlendirmelerin veya gizli sayfaların kopyalanan içeriği etkilemesini önler. Varsayılan çalışma kitabı zaten bir çalışma sayfası içerir; bu sayfayı hedef olarak kullanacağız.

### Adım 4: Aralığı hedef çalışma kitabına kopyalayın

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**Neden?**  
`copyRange`, hücre değerleri, formüller, biçimlendirme ve hatta pivot önbellekleri dahil tüm hücre özniteliklerini işler. `"A1"` konumuna kopyalayarak, aralığı hedef sayfanın sol‑üst köşesine yerleştirir ve orijinal düzeni korursunuz.

**Sık sorulan soru:** *Pivot tablo çalışmaya devam eder mi?*  
Evet. Aspose.Cells, pivot tablo tanımını ve önbelleğini kopyalar; böylece pivot, kaynak çalışma kitabındaki gibi aynı şekilde çalışır.

### Adım 5: Hedef çalışma kitabını kaydedin

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Neden?**  
`save` çağrısı, bellek içindeki çalışma kitabını fiziksel bir `.xlsx` dosyasına yazar. Dosya uzantısını değiştirerek ya da `SaveOptions` kullanarak diğer formatlara (`.xls`, `.csv`, `.pdf` vb.) da kaydedebilirsiniz.

**İpucu:**  
Dosyayı bir web yanıtına akıtmanız gerekiyorsa, dosya yolunu kullanmak yerine `destWb.save(OutputStream, SaveFormat.XLSX);` yöntemini tercih edin.

---

## Çalışma kitapları arasında aralık kopyalama – tam kaynak kodu

Aşağıda, doğrudan çalıştırabileceğiniz tam Java sınıfı yer almaktadır. `YOUR_DIRECTORY` kısmını makinenizdeki gerçek klasörle değiştirin.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Beklenen sonuç:**  
`dest.xlsx`, `source.xlsx` dosyasındaki `A1:G20` aralığının tam bir kopyasını içerir. Kaynak aralık bir pivot tablo içeriyorsa, hedef dosyada aynı pivot tablo, veri kaynağı doğru şekilde kopyalanmış hücrelere bağlı olarak gösterilir.

`dest.xlsx` dosyasını Excel, LibreOffice ya da `.xlsx` destekleyen herhangi bir görüntüleyicide açarak değerlerin, biçimlendirmelerin ve pivot işlevselliğinin korunduğunu doğrulayabilirsiniz.

---

## Pivot tablo çalışma kitabı kopyalama – bilmeniz gerekenler

* **Pivot önbelleği otomatik olarak kopyalanır.** Kütüphane, alttaki önbelleği aktarır; bu sayede pivotun manuel olarak yenilenmesi gerekmez.  
* **Harici veri kaynakları aktarılmaz.** Pivot, dış bir veritabanından veri çekiyorsa, hedef çalışma kitabının aynı kaynağa erişebildiğinden emin olmalı ya da önbelleği yerel olarak yeniden oluşturmalısınız.  
* **Büyük pivot tablolar bellek kullanımını artırabilir.** Çok büyük çalışma kitapları için JVM yığın boyutunu (`-Xmx2g`) artırarak `OutOfMemoryError` hatasından kaçının.

---

## Çalışma kitabı dosyasını farklı formatlarda kaydetme

Aspose.Cells, ek kod değişikliği yapmadan sonucu birçok formata kaydetmenizi sağlar:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

İş akışınıza en uygun formatı seçin. Aynı `copyRange` mantığı, hedef format ne olursa olsun aynı şekilde çalışır.

---

## Java ile Excel çalışma kitabı yükleme – ek ipuçları

* **Şifreli dosyaları yükleme:** Şifreyle birlikte `LoadOptions` kullanın:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Yalnızca belirli sayfaları okuma:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Bu seçenekler, özellikle büyük dosyalar için **load excel workbook java** adımını hızlandırabilir.

---

## Sonuç

Artık **Java ile Excel çalışma kitapları arasında hücreleri nasıl kopyalarsınız**, **pivot tablo içeren bir aralığı çalışma kitapları arasında nasıl kopyalarsınız** ve **çalışma kitabı dosyasını ihtiyacınıza göre nasıl kaydedersiniz** biliyorsunuz. Yukarıdaki adımları izleyerek, Excel veri manipülasyonunu herhangi bir Java uygulamasına entegre edebilirsiniz—raporlama motoru, ETL boru hattı ya da basit bir dosya‑dönüştürme aracını geliştirmek isterken.

**Bir sonraki adımlar** olarak şunları keşfedebilirsiniz:

* **copy range between workbooks** kullanarak birden fazla raporu birleştirme

## Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}