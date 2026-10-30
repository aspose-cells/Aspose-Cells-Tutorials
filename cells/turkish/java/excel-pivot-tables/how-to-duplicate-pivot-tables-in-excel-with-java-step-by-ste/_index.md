---
category: general
date: 2026-10-07
description: Java ve Aspose.Cells kullanarak Excel'de pivot tabloları nasıl çoğaltacağınızı
  öğrenin. Pivot tabloyu, aralığını çalışma kitapları arasında hızlıca kopyalayarak
  kopyalayın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: tr
lastmod: 2026-10-07
og_description: Java ve Aspose.Cells kullanarak Excel'de pivot tabloları nasıl çoğaltılır?
  Bu kılavuzu izleyerek bir pivot tabloyu, çalışma kitapları arasında aralığını kopyalayarak
  nasıl kopyalayacağınızı öğrenin.
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: Java ile Excel’de Pivot Tabloları Nasıl Çoğaltılır – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: Java ile Excel'de Pivot Tabloları Nasıl Çoğaltılır – Adım Adım Rehber
url: /tr/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Java ile Pivot Tabloları Nasıl Çoğaltılır – Adım‑Adım Rehber

Eğer bir Excel çalışma kitabında **pivot tabloları nasıl çoğaltılır** ihtiyacınız varsa, bu öğretici size eksiksiz, çalıştırmaya hazır bir çözüm gösterir. Aspose.Cells for Java kullanarak bir pivot tabloyu kaynak verileriyle birlikte, temel aralığı kopyalayarak ve ardından sonucu yeni bir çalışma kitabı olarak kaydederek kopyalayabilirsiniz.

Pivot tabloyu çoğaltmak genellikle zor gibi hissedilir çünkü pivot önbelleği sayfanın içinde gizlidir. Pivotu içeren tüm aralığı kopyalayarak, Aspose.Cells hedef çalışma kitabında önbelleği otomatik olarak yeniden oluşturur, böylece manuel XML düzenlemesi yapmadan tam işlevsel bir kopya elde edersiniz.

Bu rehberde şunları yapacaksınız:

* Pivot tablo içeren bir kaynak çalışma kitabını yükleyin.  
* Pivotu tutan kesin aralığı tanımlayın.  
* Pivot tanımını koruyarak bu aralığı yeni bir çalışma kitabına kopyalayın.  
* Yeni dosyayı kaydedin ve pivotun çalıştığını doğrulayın.  

Adımlar, Aspose.Cells tarafından desteklenen (2007‑2024) herhangi bir Excel sürümüyle çalışır ve yalnızca birkaç satır Java kodu gerektirir.

## Önkoşullar

| Gereksinim | Neden Önemli |
|------------|--------------|
| **Java 8 or newer** | Aspose.Cells, Java 8+ için geliştirilmiştir. |
| **Aspose.Cells for Java** (latest version) | Örnekte kullanılan `Workbook`, `Range` ve `CopyRange` API'lerini sağlar. |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | Çoğaltmak istediğiniz pivot. |
| **Write permission** to the target directory | `CopyWithPivot.xlsx` dosyasını kaydetmek için gereklidir. |

Add the Aspose.Cells Maven dependency to your `pom.xml` (or download the JAR manually):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## Pivot Tablolarını Nasıl Çoğaltılır – Tam Uygulama

Below is a self‑contained Java program that demonstrates **how to duplicate pivot** tables by copying the range that contains the pivot. The code includes error handling, comments, and a verification step.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### Her Adımın Açıklaması

| Adım | Kodun yaptığı şey | Neden **pivot tablo kopyalama** için önemlidir |
|------|-------------------|-----------------------------------------------|
| **1️⃣ Kaynak çalışma kitabını yükle** | `new Workbook(srcPath)` `Source.xlsx` dosyasını okur. | Kaynak dosya, orijinal pivotun bulunduğu tek yerdir. |
| **2️⃣ Aralığı tanımla** | `createRange("A1:G20")` pivot ve verilerini kapsayan bir `Range` nesnesi oluşturur. | Pivot tablo, önbelleğiyle birlikte depolanır; tüm aralığı kopyalamak önbelleğin de taşınmasını sağlar. |
| **3️⃣ Aralığı kopyala** | `copyRange(srcRange, "A1")` aralığı hedef sayfaya yazar. | Bu, **çalışma kitapları arasında aralık kopyalama** işleminin çekirdeğidir – API gizli nesneleri otomatik olarak yönetir. |
| **4️⃣ Pivotu yenile** | `pivotTable.refresh()` pivotun yeniden hesaplanmasını zorlar. | Kopyalanan pivotun, özellikle değişikliklerden sonra, orijinaliyle aynı değerleri göstermesini garanti eder. |
| **5️⃣ Çalışma kitabını kaydet** | `destWb.save(destPath)` dosyayı diske yazar. | Excel'de açabileceğiniz son **excel aralığını kopyala** sonucunu üretir. |

#### Beklenen Çıktı

Programı çalıştırdıktan sonra `CopyWithPivot.xlsx` dosyasını açın. Kaynak sayfaya tamamen aynı görünümlü bir çalışma sayfası göreceksiniz ve pivot tablo, orijinali gibi sorunsuz çalışacak – satırları genişletebilir, alanları filtreleyebilir ve verileri hatasız bir şekilde yenileyebilirsiniz.

## Yaygın varyasyonlar ve kenar durumları

### 1️⃣ Birden fazla sayfaya yayılan pivotu kopyalama

Pivotun kaynak verileri, pivotun kendisinden farklı bir sayfada bulunuyorsa, her iki sayfayı da kopyalama işlemine dahil edin. En basit yaklaşım, önce tüm kaynak sayfayı kopyalamak, ardından pivot sayfasını kopyalamaktır:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ Adlandırılmış aralıklarla çalışmak

Aspose.Cells, bir aralığı kopyaladığınızda adlandırılmış aralıkları korur. Ancak, hedef çalışma kitabı aynı tanımlayıcıya sahip bir adı zaten içeriyorsa, bir `CellsException` fırlatılır. Bu durumu, kopyalamadan önce çakışan adı yeniden adlandırarak çözün:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ Büyük çalışma kitapları ve performans

Çok büyük aralıkları (yüz binlerce satır) kopyalamak bellek yoğun olabilir. **Bellek optimizasyonu**nu etkinleştirin:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ Formülleri bozulmadan tutma

Kaynak aralık, kopyalanan alanın dışındaki hücrelere referans veren formüller içeriyorsa, bu referanslar kopyalama sonrası kırılır. Bunu önlemek için, tüm bağımlı hücreleri kapsayacak şekilde aralığı genişletin veya `copyRange` metodunu `CopyOptions` bayrağı `CopyOptions.COPY_FORMULA` ile kullanın:

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## Güvenilir **çalışma kitapları arasında aralık kopyalama** için uzman ipuçları

* **Her zaman mutlak adresler kullanın** (`$A$1:$G$20`) kaynak sayfa yeniden adlandırılabilecek durumlarda.  
* **Kopyalama sonrası yenileyin** – Aspose.Cells önbelleği yeniden oluştursa da, `refresh()` çağrısı Excel'de zaman zaman görülen eski‑bellek uyarılarını ortadan kaldırır.  
* **Pivotu doğrulayın**: kaydettikten sonra dosyayı programatik olarak açın ve `pivotTable.validate()` çağrısıyla kırık referans olmadığını kontrol edin.  
* **Sürüm uyumluluğu**: kod, Excel 2007‑2024 dosyaları (`.xlsx`, `.xlsm`) ile çalışır. Eski `.xls` dosyaları için `LoadOptions.setLoadFormat(LoadFormat.XLS)` ayarlayın.

## Tam kaynak listesi (derlemeye hazır)



## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla birlikte tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Java'da Pivot Tablosunu Kopyalama – Tam Aspose.Cells Rehberi](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Aspose.Cells for Java Kullanarak Excel'de Pivot Tabloları Oluşturma: Kapsamlı Rehber](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java ile Excel Pivot Tablosu Kaynağını Güncelleme: Kapsamlı Rehber](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}