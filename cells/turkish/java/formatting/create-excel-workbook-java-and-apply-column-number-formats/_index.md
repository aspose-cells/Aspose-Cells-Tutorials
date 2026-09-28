---
category: general
date: 2026-09-27
description: Java ile Excel çalışma kitabı oluştur, SQL verilerini içe aktar, sayı
  formatı sütununu ayarla ve Aspose.Cells kullanarak çalışma kitabını XLSX olarak
  kaydet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: tr
lastmod: 2026-09-27
og_description: Java ile Excel çalışma kitabı oluşturun, SQL verilerini içe aktarın,
  sayı formatı sütununu ayarlayın ve tam çalışan bir Java örneğiyle çalışma kitabını
  XLSX olarak kaydedin.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Java ile Excel çalışma kitabı oluşturma – SQL verilerini içe aktar ve sütun
  sayı formatlarını ayarla
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Java ile Excel çalışma kitabı oluşturun ve sütun sayı formatlarını uygulayın
url: /tr/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel çalışma kitabı oluşturma java ve sütun sayı formatlarını uygulama

If you need to **create Excel workbook java** and style numeric columns, this guide shows you exactly how. You’ll learn to import SQL data into Excel, set a number format for each column, and **save workbook as XLSX** using the Aspose.Cells library.

Java'dan elektronik tablolarla çalışmak genellikle parçalı hissedilir—geliştiriciler kod parçacıklarını kopyala‑yapıştırır, sayı formatlamayı unuturlar veya gerçek Excel dosyaları yerine CSV dosyalarıyla kalırlar. Bu öğretici, herhangi bir Java projesine ekleyebileceğiniz tek bir uçtan‑uza çözüm sunarak bu sürtünmeyi ortadan kaldırır.

Makalenin sonunda şunları yapabilecek:

* Bir veritabanına bağlanıp bir `DataTable` (veya `ResultSet`) alın  
* Aspose.Cells ile yeni bir çalışma kitabı oluşturun  
* Her sütuna tutarlı bir **add number format excel** stili uygulayın  
* **Save workbook as XLSX**'i istediğiniz bir konuma kaydedin  

Tek ön koşul, bir Java geliştirme ortamı (JDK 8+ önerilir) ve sınıf yolunuzda Aspose.Cells for Java JAR dosyasıdır.

---

## Önkoşullar

| Gereksinim | Neden Önemlidir |
|-------------|----------------|
| JDK 8 veya daha yeni | Örnekte kullanılan dil özelliklerini sağlar. |
| Aspose.Cells for Java (en son sürüm) | Office yüklü olmadan Excel oluşturma, stil verme ve kaydetme işlemlerini yönetir. |
| JDBC uyumlu bir veritabanı (ör. MySQL, PostgreSQL) | İçe aktaracağımız SQL verilerini sağlar. |
| Maven veya Gradle (isteğe bağlı) | Bağımlılık yönetimini basitleştirir. |

Aspose.Cells'i Maven `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Veya JAR dosyasını doğrudan Aspose web sitesinden indirip projenizin sınıf yoluna ekleyin.

## Adım 1: Excel çalışma kitabı java oluşturma

İlk mantıksal blok, yeni bir `Workbook` nesnesi oluşturmaktır. Bu nesne, bellekteki tüm Excel dosyasını temsil eder ve çalışma sayfalarına, hücrelere ve stillere erişim sağlar.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Çalışma kitabını önceden oluşturmak, daha sonra **set number format column** işlemi için ihtiyaç duyacağımız bir `Style` fabrikası da sağlar.

## Adım 2: SQL'den veri al (import sql data excel)

Aşağıda bir JDBC bağlantısı açıyoruz, basit bir `SELECT` ifadesi çalıştırıyoruz ve sonuç kümesini bir Aspose `DataTable`'a yüklüyoruz. `DataTable` sınıfı .NET `DataTable`'ı taklit eder ve `importDataTable` yöntemiyle sorunsuz çalışır.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **İpucu:** Başka bir kaynaktan (ör. CSV ayrıştırması) zaten bir `DataTable`'ınız varsa, JDBC kodunu atlayabilir ve tabloyu doğrudan döndürebilirsiniz.

## Adım 3: Yeniden kullanılabilir bir stil hazırlama (add number format excel)

Her sayısal sütunun iki ondalık basamak ve binlik ayırıcı ile sayıları göstermesini istiyoruz. Her hücreyi ayrı ayrı biçimlendirmek yerine, sütun başına bir kez bir `Style` nesnesi oluşturup içe aktarım sırasında yeniden kullanıyoruz. Bu, **add number format excel** işleminin en verimli yoludur.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

İhtiyacınız olan herhangi bir Excel sayı formatına uyacak şekilde format dizesini (`"#,##0.00"`) uyarlayabilirsiniz. Tarihler için `styles[i].setCustom("mm-dd-yyyy")` gibi bir kullanım yapın, vb.

## Adım 4: DataTable'ı içe aktar ve sütun stillerini uygula

Şimdi her şeyi bir araya getiriyoruz. `importDataTable` aşırı yüklemesi, `DataTable`'ı geçmemize, ilk satırın sütun başlığı olarak ele alınıp alınmayacağını belirtmemize ve stil dizisini sağlamamıza olanak tanır. Bu, ilgili sütundaki her hücre için otomatik olarak **set number format column** uygular.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

`importColumnNames` bayrağı için `true` geçtiğimiz için, çalışma sayfasının ilk satırı `DataTable`'dan gelen sütun adlarını içerir. Sonraki her satır, tanımladığımız stile göre zaten biçimlendirilmiş verileri alır.

## Adım 5: Çalışma kitabını xlsx olarak kaydet

Son adım, bellek içindeki çalışma kitabını fiziksel bir dosyaya kaydetmektir. Aspose.Cells birçok formatı destekler; bugün çoğu uygulamanın beklediği modern XLSX formatını kullanacağız.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

`filePath`'i sisteminizdeki geçerli bir konuma değiştirebilirsiniz. Dizin mevcut değilse veya yazma izniniz yoksa yöntem `IOException` fırlatır.

## Tam, çalıştırılabilir örnek

Tüm parçaları bir araya koymak, hemen derleyip çalıştırabileceğiniz bağımsız bir program ortaya çıkarır.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Beklenen sonuç

Programı çalıştırmak, çalışma dizininde **DataTableWithNumberFormat.xlsx** adlı bir dosya oluşturur. Microsoft Excel, LibreOffice Calc veya herhangi bir XLSX uyumlu görüntüleyici ile açtığınızda şunları göreceksiniz:

| Id | Tutar | OluşturulmaTarihi |
|----|--------|-------------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

* **Tutar** sütunu, iki ondalık basamak ve binlik ayırıcı ile sayıları gösterir; bu, uyguladığımız **add number format excel** stili sayesinde gerçekleşir.*

## Yaygın sorular ve uç‑durum yönetimi

| Soru | Cevap |
|----------|--------|
| **Sorgum satır döndürmezse ne olur?** | `DataTable` boş olacak ancak yine de sütun tanımlarını içerecek. Çalışma kitabı yalnızca başlık satırını içerecek; bu genellikle sonraki işlemler için yeterlidir. |
| **Her sütun için farklı formatlar nasıl uygulanır?** | `buildColumnStyles` metodunu sütun adını veya veri tipini inceleyecek şekilde değiştirin ve özel bir format atayın (ör. tarihler, yüzde değerleri). |
| **Doğrudan bir `ByteArrayOutputStream`'e yazabilir miyim?** | Evet. `workbook.save(filePath, SaveFormat.XLSX);` ifadesini şu şekilde değiştirin |

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java kullanarak Excel Çalışma Kitabını SVG Olarak Oluşturma ve Kaydetme](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel Çalışma Kitabını Oluştur ve Kaydet Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel Çalışma Kitabını Oluştur ve Kaydet Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}