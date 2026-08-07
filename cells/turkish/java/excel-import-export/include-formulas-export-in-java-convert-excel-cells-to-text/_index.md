---
category: general
date: 2026-07-03
description: Aspose.Cells kullanarak Java'da formüllerin dışa aktarımını dahil edin
  ve Excel hücrelerini metne dönüştürün. Excel aralığını nasıl yazdıracağınızı ve
  hücre değerlerini string olarak verimli bir şekilde alacağınızı öğrenin.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: tr
og_description: Java’da formüllerin dışa aktarımını ekleyerek Excel hücrelerini metne
  dönüştürün. Excel aralığını nasıl yazdıracağınızı ve hücre değerlerini dize olarak
  nasıl alacağınızı gösteren adım adım rehber.
og_title: Java'da Formülleri Dışa Aktarma – Excel Hücrelerini Metne Dönüştür
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Java’da Formüller İhracatını Dahil Et – Excel Hücrelerini Metne Dönüştür
url: /tr/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Formüllerin Dışa Aktarılmasıyla Java’da Excel Hücrelerini Metne Dönüştürme

Bir Excel çalışma kitabından veri çekerken **formüllerin dışa aktarılmasını** dahil etmeniz gerektiğinde hiç zorlandınız mı? Belki orijinal formülleri korurken hâlâ temiz bir metin bloğu sunması gereken bir raporlama servisi geliştiriyorsunuzdur. Bu durumda doğru yerdesiniz. Bu kılavuz, Aspose.Cells for Java kullanarak Excel hücrelerini düz metne—*gömülü formüller dahil*—dönüştürmenizi adım adım gösterir.

Ayrıca **Excel aralığını yazdırma**, **dışa aktarma tablo seçeneklerini** ayarlama ve sonunda **hücre değerlerini dize olarak alma** konularına da değineceğiz; bu değerleri loglayabilir, bir API üzerinden gönderebilir ya da bir veritabanına kaydedebilirsiniz. Sonuna geldiğinizde tamamen çalıştırılabilir bir kod örneğine ve her çağrının nedenine dair sağlam bir anlayışa sahip olacaksınız.

## Öğrenecekleriniz

- `.xlsx` dosyasını okuyan, bir aralık seçen ve bunu biçimlendirilmiş bir dize olarak dışa aktaran, kopyala‑yapıştır‑hazır bir Java programı.
- `ExportTableOptions` sınıfının ne işe yaradığını ve `setExportAsString` ile `setIncludeFormula` bayraklarını neden değiştirmeniz gerektiğini.
- Büyük çalışma sayfalarını yönetme, farklı veri tipleriyle başa çıkma ve çıktıyı özelleştirme ipuçları.
- Yaygın tuzaklar için hızlı bir kontrol listesi (birleştirilmiş hücreler, gizli satırlar ve bölge‑özel sayı formatları gibi).

### Önkoşullar

- Java 17 veya daha yeni bir sürüm (kod daha eski sürümlerde de derlenebilir ancak en yeni LTS sürümünü kullanacağız).
- Aspose.Cells for Java 23.10 (veya daha yeni bir sürüm) — Maven Central’dan temin edebilirsiniz.
- Kontrol ettiğiniz bir klasörde bulunan örnek bir `input.xlsx` (örnek açıklık sağlamak amacıyla yol kod içinde sabitlenmiştir).

Bu koşullara sahipseniz, başlayalım.

## Adım 1: Projeyi Oluşturun ve Bağımlılıkları Ekleyin

İlk olarak bir Maven projesi (ya da tercih ederseniz Gradle) oluşturun. `pom.xml` dosyanıza Aspose.Cells bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **İpucu:** Kurumsal bir proxy kullanıyorsanız, depoya erişilebilir olduğundan emin olun; aksi takdirde “Could not resolve dependencies” hatası alırsınız.

Maven indirmeleri tamamlandığında Java kodunu yazmaya hazırsınız.

## Adım 2: Çalışma Kitabını Yükleyin ve İstenen Çalışma Sayfasını Alın

Kod örneğinin ilk satırı, mevcut bir çalışma kitabını nasıl açacağınızı gösterir:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`YOUR_DIRECTORY` kısmını dosyanızın mutlak ya da göreli yolu ile değiştirin. `Workbook` yapıcı, dosya formatını (XLS, XLSX, CSV vb.) otomatik olarak algılar; bu yüzden formatı belirtmeniz gerekmez.

Sonra ilk sayfayı alıyoruz:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Neden ilk sayfa? Birçok şablonda veri ilk sekmede bulunur, ancak istediğiniz herhangi bir indeksle ya da isimli bir yaklaşım için `get("SheetName")` kullanabilirsiniz.

## Adım 3: Dışa Aktarmak İstediğiniz Aralığı Tanımlayın

Şimdi **excel hücrelerini metne dönüştürme** işleminin kalbi geliyor. Aspose.Cells’e hangi hücreleri çekeceğinizi bir `Range` nesnesi oluşturarak bildirirsiniz:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

`"A1:C3"` dizesi klasik A1‑stili bir adresdir. Programatik olarak da oluşturulabilir:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Bu esneklik, aralık boyutu dinamik olduğunda işe yarar—örneğin, son kullanılan satırı `ws.getCells().getMaxDataRow()` ile okuyabilirsiniz.

## Adım 4: Formülleri Dahil Etmek İçin Dışa Aktarma Tablo Seçeneklerini Yapılandırın

İşte **formüllerin dışa aktarılması** sihrinin olduğu yer. Varsayılan olarak Aspose.Cells *görüntülenen* değerleri döndürür. Bir hücre `=SUM(A1:A3)` içeriyorsa, formül metni yerine hesaplanan sayı elde edilir. Bunu değiştirmek için `ExportTableOptions` ayarlayın:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

İki bayrak neden birlikte? `setExportAsString(true)` API’ye hücreleri varsayılan ayırıcı (sütunlar için sekme, satırlar için yeni satır) ile birleştirmesini söyler. `setIncludeFormula(true)` ise değer kaynağını “görüntülenen değer”den “ham formül”e çevirir. Sadece değerleri istiyorsanız `false` bırakın.

### İsteğe Bağlı Ayarlamalar

- `eto.setExportHiddenRows(true);` – Excel’de gizli satırları da dahil eder.
- `eto.setExportHiddenColumns(true);` – Gizli sütunlar için aynı.
- `eto.setExportAsHTML(true);` – Düz metin yerine HTML almanızı sağlar.

Deneyin; seçenek sınıfı bir **export table options** oyun alanıdır.

## Adım 5: Aralığı Biçimlendirilmiş Bir Dize Olarak Alın

Şimdi veriyi çekiyoruz:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Dönen `txt` şu şekilde görünebilir (A1:C3 karışık değer ve formül içeriyorsa):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Sütunları ayıran sekme (`\t`) ve satırları ayıran yeni satır (`\n`) dikkat edin. Daha sonra 2‑D bir diziye bölmek isterseniz:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Adım 6: Sonucu Yazdırın – “Print Excel Range” Kolaylaştırıldı

Son olarak dizeyi konsola döküyoruz:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

Programı çalıştırdığınızda yukarıda gösterilen tam çıktı ekrana basılır. Buradan itibaren dizeyi bir log dosyasına yazabilir, HTTP üzerinden gönderebilir ya da bir NoSQL belgeye kaydedebilirsiniz.

## Tam, Çalıştırmaya Hazır Örnek

Hepsini bir araya getirdiğimizde, eksiksiz program aşağıdadır. Kopyalayıp yapıştırın, **Run** tuşuna basın—eksik import yok.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Beklenen Çıktı (örnek)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Çalışma kitabınız tarih olarak biçimlendirilmiş sayılar içeriyorsa, bölge‑özel formatta (ör. `2026‑07‑03`) görüneceklerdir. ISO tarihleri zorlamak isterseniz, `ExportTableOptions` içinde özel bir `NumberFormat` ayarlayabilirsiniz.

## Kenar Durumları ve Yaygın Sorular

### Aralık birleştirilmiş hücreler içeriyorsa ne olur?

Birleştirilmiş hücreler, sol‑üst hücrenin değeri olarak işlenir. Birleştirilmiş alanın geri kalanı boş dize olarak görünür. Birleştirilmiş bölgenin adresine ihtiyacınız varsa, dışa aktarmadan önce `Cell.getMergedRange()` sorgulayın.

### Çok büyük bir sayfayı (yüz binlerce satır) dışa aktarabilir miyim?

Evet, ancak bellek tüketimine dikkat edin. `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` kullanarak Aspose.Cells’in veriyi diske akıtmasını sağlayabilirsiniz. Ayrıca dizeyi yönetilebilir tutmak için (ör. 10 000 satırlık parçalar) bölerek dışa aktarmayı düşünün.

### Sütun ayırıcıyı nasıl değiştiririm?

`ExportTableOptions` sınıfı `setSeparator(char separator)` metodunu sunar. CSV‑stil bir çıktı için ayırıcıyı `','` olarak ayarlayın:

```java
eto.setSeparator(',');
```

### Formüller dış referansları destekliyor mu?

Bir formül başka bir çalışma kitabına işaret ediyorsa, Aspose.Cells referans metnini (`='[Other.xlsx]Sheet1'!A1`) korur. Dış değeri değerlendirmez; bunu yapabilmek için ilgili çalışma kitabını da yüklemeniz gerekir.

## Üretim‑Hazır Kod İçin Pro İpuçları

- **Çalışma kitabını önbellekle** eğer aynı dosyayı birden çok kez okuyacaksanız…

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan örnekler sunar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir; böylece API özelliklerini daha iyi kavrayabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}