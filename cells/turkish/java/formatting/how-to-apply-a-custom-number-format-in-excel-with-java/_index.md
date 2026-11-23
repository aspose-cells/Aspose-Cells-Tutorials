---
category: general
date: 2026-11-22
description: Java kullanarak Excel'de bir sütunu para birimi olarak biçimlendirmek
  için özel bir sayı formatının nasıl kullanılacağını öğrenin. Basit bir stil ile
  Excel sayı formatını hızlıca ayarlayın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: tr
lastmod: 2026-11-22
og_description: Java ile Excel'de özel bir sayı biçimi uygulayın. Bu öğreticide Excel
  sayı biçimini nasıl ayarlayacağınızı ve ilk sütunu para birimi olarak nasıl biçimlendireceğinizi
  gösterir.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Java ile Excel'de Özel Sayı Formatı Uygulama – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Java ile Excel'de özel sayı biçimini nasıl uygularsınız
url: /tr/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Excel'de özel sayı biçimi uygulama

Eğer bir Excel çalışma sayfasındaki bir sütunu **custom number format** ile biçimlendirmeniz gerekiyorsa, bu rehber Java kullanarak bunu tam olarak nasıl yapacağınızı gösterir. Finansal raporlar oluşturuyor ya da muhasebe verilerini dışa aktarıyor olun, ilk sütunu para birimi olarak biçimlendirmek çıktıyı anında okunabilir kılar.

Aşağıdaki örnekte **format column as currency** ifadesini kullanacağız, stili ilk sütuna uygulayacağız ve ardından bir `DataTable`'ı çalışma sayfasına aktaracağız. Aynı yaklaşım, görüntülemek istediğiniz herhangi bir sayısal biçim için çalışır.

## Öğrenecekleriniz

* Apache POI'nin `Style` nesnesiyle **custom number format** oluşturmayı nasıl yapacağınızı.  
* Belirli bir sütun için **set Excel number format**'ı nasıl ayarlayacağınızı, **set currency format** durumunu da içerecek şekilde.  
* `DataTable` aktarırken **style first column**'ı nasıl uygulayacağınızı.  
* Çalışma kitabını kaydetmeyi ve biçimlendirmenin doğru göründüğünü doğrulamayı nasıl yapacağınızı.

### Önkoşullar

* Java 17 veya daha yeni bir sürüm.  
* Apache POI 5.x (`Workbook`, `Worksheet` ve `Style` sağlayan kütüphane).  
* Kod örneğindeki gibi yineleyebilen bir `DataTable` uygulaması.  
* Java ve Excel kavramlarına temel aşinalık.

---

## Adım 1: Projeyi kurma ve verileri içe aktarma

İlk olarak, projenize Apache POI ekleyin. Maven kullanıyorsanız, aşağıdaki bağımlılığı ekleyin:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Sonra, kaynak verileri `DataTable` olarak edinin. Gerçek bir senaryoda bu, bir veritabanı sorgusu, bir CSV dosyası veya bir API yanıtı olabilir.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Pro tip:** `DataTable` sütunlarının doğru Java tiplerine (`Integer`, `Double` vb.) sahip olduğundan emin olun, çünkü sayı biçimi yalnızca sayısal hücreleri etkiler.

---

## Adım 2: İlk sütun için **custom number format** oluşturma

Bir **custom number format**, Excel'e sayısal değerleri nasıl göstereceğini söyler. Değerleri para birimi olarak göstermek için yerleşik `CURRENCY` formatını kullanırız, ancak `"$#,##0.00"` gibi desenler de tanımlayabilirsiniz.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Neden bu çalışıyor:**  
* `createCellStyle()` yeniden kullanılabilir bir stil nesnesi döndürür.  
* `setDataFormat()` **set currency format**'ı stile ekler, Excel bu stili kullanan her hücreye uygular.  
* Stili `columnStyles[0]` içinde saklayarak yalnızca ilk sütunun para birimi biçimlendirmesini almasını garantileriz.

---

## Adım 3: Sütun stillerini uygularken `DataTable`'ı içe aktarma

Şimdi verileri çalışma sayfasına içe aktarıyoruz. `importDataTable` yöntemi stil dizisini kabul eder, bu da **style first column** yapmamıza ve kalan sütunları varsayılan biçimlendirmede bırakmamıza olanak tanır.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

Yukarıdaki çağrı, yalnızca ilk sütun için **set Excel number format** ayarlar. Diğer tüm sütunlar, kodu basit ve verimli tutan çalışma kitabının varsayılan stilini miras alır.

---

## Adım 4: Çalışma kitabını kaydetme ve sonucu doğrulama

Son olarak, çalışma kitabını bir dosyaya yazın ve Excel'de açarak ilk sütunun para birimi simgelerini gösterdiğini doğrulayın.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Beklenen çıktı:**  
*FormattedReport.xlsx* dosyasını açtığınızda, A sütunundaki değerler uygun para birimi simgesiyle (ör. `$1,234.00`) görünür. Diğer tüm sütunlar orijinal sayısal temsillerini korur.

---

## Yaygın varyasyonlar ve uç durumlar

| Durum | Ayarlama |
|-----------|------------|
| **Different currency** (e.g., Euro) | `Style.CustomNumberFormat.CURRENCY` yerine özel bir desen kullanın: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **More than one styled column** | `columnStyles[]` içine kendi `CellStyle` nesneleriyle ek girişler doldurun. |
| **Large data sets** | `importDataTable`'ı toplu olarak kullanın veya `OutOfMemoryError` önlemek için satırları akış olarak işleyin. |
| **Locale‑specific separators** | `java.text.NumberFormat` kullanarak yerel ayara duyarlı bir desen oluşturun ve `setDataFormat`'a geçirin. |

> **Dikkat:** Tek bir `CellStyle` nesnesini birçok sütun arasında yeniden kullanmak, Excel'in bir çalışma kitabındaki farklı stil sayısını sınırlaması nedeniyle beklenmedik biçimlendirmelere yol açabilir. İhtiyacınız olan her benzersiz biçim için ayrı bir stil oluşturun.

---

## Tam çalıştırılabilir örnek

Aşağıda, veri oluşturulmasından biçimlendirilmiş çalışma kitabının kaydedilmesine kadar tüm iş akışını gösteren bağımsız bir program bulunmaktadır.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

Programı çalıştırdığınızda, **FormattedReport.xlsx** oluşturulur; burada A sütunu (“Amount” sütunu) dolar işareti ve iki ondalık basamak gösteren bir **custom number format** ile görüntülenir.

---

## Sonuç

Artık Java'dan bir Excel çalışma sayfasına **custom number format** uygulamayı, **format column as currency** yapmayı ve veri aktarırken **style first column**'ı nasıl yapacağınızı biliyorsunuz. Yeniden kullanılabilir bir `CellStyle` oluşturarak ve bunu `importDataTable`'a geçirerek, her hücreyi manuel olarak döngüye almadan herhangi bir sütun için **set Excel number format** ayarlayabilirsiniz.

Next, try:

* `setDataFormat`'ı yerel‑spesifik desenlerle kullanarak **set currency format**'ı deneyin

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java'da Excel Sayı Biçimini Ayarlama – Tam Kılavuz](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Java'da Excel Sayı Biçimini Uygulama – Tam Aspose.Cells Kılavuzu](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Java'da Para Birimi Biçimi ve Kalın Yazı Tipi ile Excel Çalışma Kitabı Oluşturma](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}