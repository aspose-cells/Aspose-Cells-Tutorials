---
category: general
date: 2026-06-30
description: Java kullanarak bir DataTable'ı Excel'e aktarırken yazı tipini kalın
  yapın. Koşullu biçimlendirme kodunu öğrenin, veri tablosunu Excel'e aktarın ve tabloları
  zahmetsizce stilize edin.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: tr
og_description: Java'da bir DataTable'ı Excel'e dışa aktarırken yazı tipini kalın
  yapın. Bu rehber, koşullu biçimlendirme kodu, DataTable'ı Excel'e aktarma ve tabloyu
  stil verme konularını kapsar.
og_title: Java Excel Dışa Aktarımında Yazı Tipini Kalın Yap – Adım Adım Öğretici
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Java Excel Dışa Aktarımında Yazı Tipini Kalın Yap – Tam Kılavuz
url: /tr/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java Excel Dışa Aktarımında Kalın Yazı Tipi Ayarlama – Tam Kılavuz

Belirli sütunlar için **how to set font bold**'ı **import datatable excel** dosyalarıyla ayarlamayı hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, her hücreyi manuel olarak ayarlamadan güzel biçimlendirilmiş bir elektronik tabloya ihtiyaç duyduklarında bir engelle karşılaşıyor. İyi haber? Birkaç Java satırıyla bir `DataTable` içe aktarabilir, kalın yazı tipleri uygulayabilir ve hatta biraz **conditional formatting code** ekleyebilirsiniz—hepsi programatik olarak.

Bu öğreticide, bir Excel çalışma kitabına **how to import datatable**'ı gösteren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz, her çift indeksli sütunda **set font bold** uygulayacağız ve isteğe bağlı olarak basit bir koşullu biçimlendirme ekleyeceğiz. Sonunda, çalıştırmaya hazır bir kod parçacığına ve herhangi bir proje için **import table with styles** konusundaki net bir anlayışa sahip olacaksınız.

## Önkoşullar

- Java 8 ve üzeri (kod Java 17'de de çalışır)  
- Aspose.Cells for Java (ücretsiz deneme sürümü yeterlidir) – Maven bağımlılığını veya JAR dosyasını sınıf yolunuza ekleyin.  
- `java.sql` `ResultSet` → `DataTable` dönüşümüne temel aşinalık (basitlik için bir tablo taklit edeceğiz).  
- Bir IDE veya Maven/Gradle gibi bir yapı aracı.

> **Pro tip:** Maven kullanıyorsanız, bunu `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Çözümün Genel Görünümü

1. **Create a mock `DataTable`**'ı, normalde bir veritabanından alacağınız verileri taklit edecek şekilde oluşturun.  
2. **Generate a `CellStyle` array**'ı, her çift sütunda kalın bir yazı tipi kullanan bir dizi oluşturun – bu, **set font bold**'ın özüdür.  
3. **Grab the first worksheet**'ı, çalışma kitabından alın.  
4. **Import the `DataTable`**'ı sütun başlıklarıyla birlikte hücre `A1`'den başlayarak içe aktarın ve hazırlanan stilleri uygulayın.  
5. (İsteğe bağlı) **Add a conditional formatting rule**'ı ekleyerek **conditional formatting code** anahtar kelimesini gösterin.

Her adım sade İngilizce açıklanmıştır ve kod blokları tamamen bağımsızdır, böylece kopyalayıp anında çalıştırabilirsiniz.

---

## Adım 1: İçeri Aktarılacak DataTable'ı Alın veya Oluşturun

Gerçek dünyadaki uygulamalarda muhtemelen `ResultSet` → `DataTable` dönüşüm yardımcılarını çağırırsınız. Bu kılavuz için, Excel kısmına odaklanabilmeniz adına basit bir `DataTable`'ı manuel olarak oluşturacağız.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Neden önemli:** `DataTable`'ın hazır olması, **import datatable excel** API'sine ve stil mantığına odaklanmamızı sağlar. Yukarıdaki yöntem yeniden kullanılabilir—üretime geçerken sabit kodlanmış satırları bir veritabanı sorgusuyla değiştirmeniz yeterlidir.

## Adım 2: Stilleri Hazırlayın – **Set Font Bold**'ın Yapıldığı Yer

Şimdi her sütun için bir `CellStyle` nesnesi içeren bir dizi oluşturacağız. Kural basittir: her çift indeksli sütun için **set font bold** uygulanır (0, 2, 4,…). Tek sütunlar normal kalır.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Stil Dizisi Kullanmanın Nedenleri?

- **Performance:** Her sütuna bir stil uygulamak, her hücreyi ayrı ayrı biçimlendirmekten daha hızlıdır.  
- **Consistency:** Bir sütundaki her hücre aynı biçimlendirmeyi miras alır, bu da tutarlı bir görünüm sağlar.  
- **Scalability:** Daha sonra daha fazla sütun eklemek sadece diziyi genişletmeyi gerektirir—kod yeniden yazmaya gerek yok.

## Adım 3: Çalışma Kitabındaki İlk Çalışma Sayfasına Erişin

Aspose.Cells bizim için varsayılan bir çalışma sayfası oluşturur, ancak bunu açıkça almak iyi bir uygulamadır. Bu aynı zamanda **how to import datatable**'ı belirli bir sayfaya nasıl içe aktaracağınızı gösterir.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

## Adım 4: Stillerle DataTable'ı İçe Aktarın – Temel **Import Table With Styles** İşlemi

`importDataTable` metodu zor işi yapar. Verileri kopyalar, sütun başlıklarını ekler ve daha önce oluşturduğumuz stil dizisini uygular.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Örneği çalıştırdığınızda, `ID` ve `Score` sütunlarına **set font bold** uygulanmış, `Name` ise normal kalmış olarak göreceksiniz.

## Adım 5 (İsteğe Bağlı): Koşullu Biçimlendirme Ekle – Hızlı Bir **Conditional Formatting Code** Örneği

Skorun 90'ı aştığı satırları vurgulamak istiyorsanız, birkaç ekstra satır işinizi görecektir. Bu, **conditional formatting code** anahtar kelimesini ana akışı bozmadan gösterir.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Not:** Yukarıdaki kod parçacığı isteğe bağlıdır ancak zaten biçimlendirilmiş tablo üzerine **conditional formatting code** katmanını nasıl ekleyebileceğinizi gösterir.

## Her Şeyi Bir Araya Getirmek – Tam, Çalıştırılabilir Örnek



## Sırada Ne Öğrenmeli?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose.Cells for Java ile Excel Koşullu Biçimlendirmeyi Otomatikleştirme: Tam Kılavuz](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Aspose.Cells Java'da Excel Biçimlendirme için Özel Yazı Tipi Ayarlarını Nasıl Uygularsınız](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Aspose.Cells Java ile Excel'de Yazı Tipi Boyutunu Ayarlama - Kapsamlı Kılavuz](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}