---
category: general
date: 2026-08-20
description: Java'da Aspose.Cells kullanarak Excel çalışma kitabı oluşturun, para
  birimi formatı ayarlayın, kalın yazı tipi ekleyin ve stil verilen hücreler için
  stil dizisini içe aktarın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: tr
lastmod: 2026-08-20
og_description: Java'da Excel çalışma kitabı oluşturun, para birimi biçimini ayarlayın,
  kalın yazı tipi ekleyin ve Aspose.Cells kullanarak stili nasıl içe aktaracağınızı
  öğrenin.
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: Java'da stilize edilmiş para birimi hücreleriyle Excel çalışma kitabı oluşturun
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Java'da para birimi formatı ve kalın yazı tipiyle Excel çalışma kitabı nasıl
  oluşturulur
url: /tr/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da para birimi biçimi ve kalın yazı tipiyle Excel çalışma kitabı nasıl oluşturulur

Programlı olarak **excel çalışma kitabı** oluşturmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Bir çalışma kitabı oluşturmayı, para birimi biçimi uygulamayı, kalın yazı tipi eklemeyi ve Aspose.Cells’in **stil nasıl içe aktarılır** özelliğini kullanarak her içe aktarılan hücrenin tutarlı görünmesini adım adım anlatacağız.

Sonuçta, sayıları dolar olarak gösteren ve kalın olarak vurgulayan `DataTableWithStyleArray.xlsx` dosyasına sahip olacaksınız. Excel’de manuel biçimlendirme yapmanız gerekmeyecek.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

- Java 17 veya daha yeni bir sürüm.
- Aspose.Cells for Java lisansı (veya ücretsiz değerlendirme anahtarı).
- `aspose-cells` bağımlılığını yönetmek için Maven veya Gradle.
- Java koleksiyonları ve `DataTable` hakkında temel bilgi.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **İpucu:** `LicenseException` alırsanız, lisans dosyanızı sınıf yoluna (classpath) koyun ve çalışma kitabını oluşturmadan önce `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` satırını çalıştırın.

## Stil uygulanmış para birimi hücreleriyle excel çalışma kitabı nasıl oluşturulur

Bu bölüm temel adımları içerir. Her adım **ne** yazmanız gerektiğini değil, **neden** önemli olduğunu açıklar.

### Adım 1: Çalışma kitabı ve çalışma sayfasını başlatma

Yeni bir çalışma kitabı oluşturmak, sonraki tüm biçimlendirmeler için temiz bir kapsayıcı sağlar.

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Neden:** `Workbook` nesnesi tüm Excel dosyasını temsil eder. İlk `Worksheet`e erişmek, verileri hemen doldurmaya başlamanızı sağlar.

### Adım 2: Sayısal verilerle bir DataTable oluşturma

`DataTable`, bir veritabanı tablosunu taklit eder ve satırları toplu olarak içe aktarmayı kolaylaştırır.

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Neden:** `DOUBLE` kullanmak, değerlerin ondalık hassasiyetini korur; bu, daha sonra **hücreleri para birimi olarak biçimlendirme** için kritiktir.

### Adım 3: Stil tanımlama – para birimi biçimi ve kalın yazı tipi

Burada bir `Style` nesnesine **para birimi biçimi** ve **kalın yazı tipi** ekliyoruz.

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Neden:** `Number` biçim dizesi `$#,##0.00` Excel’e hücreyi para birimi olarak ele almasını söyler, `setBold(true)` ise sayılara dikkat çeker. Stili bir diziye koymak, **stil nasıl içe aktarılır** adımına hazırlık sağlar.

### Adım 4: Stil dizisini kullanmak için içe aktarma seçeneklerini yapılandırma

Aspose.Cells, `ImportTableOptions` aracılığıyla bir `Style[]` geçirmenize izin verir. Bu, resmi **stil nasıl içe aktarılır** yöntemidir.

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Neden:** `ImportTableOptions` olmadan, içe aktarılan hücreler varsayılan stili miras alır ve tanımladığımız para birimi biçimi ve kalınlık kaybolur.

### Adım 5: DataTable’ı çalışma sayfasına içe aktarma

Şimdi verileri `A1` hücresinden başlayarak sayfaya getiriyoruz; stil dizisi otomatik olarak uygulanır.

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` değeri, `DataTable`ın ilk satırının sütun başlıkları içerdiğini gösterir.
- `"A1"` içe aktarmanın başladığı sol‑üst köşedir.

> **Neden:** Stil dizisiyle içe aktarma, her içe aktarılan hücrenin daha önce hazırladığımız **hücreleri para birimi olarak biçimlendirme** stilini almasını garantiler.

### Adım 6: Çalışma kitabını diske kaydetme

Son olarak, bellek içindeki çalışma kitabını fiziksel bir dosyaya yazıyoruz.

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Neden:** Kaydetmek, biçimlendirmeyi kalıcı hâle getirir; böylece siz veya sonraki süreçler dosyayı Excel’de istediğiniz görünüme sahip olarak açabilir.

## Tam kaynak kodu

Aşağıda, çalıştırmaya hazır tam Java sınıfı yer alıyor. IDE’nize kopyalayın, `YOUR_DIRECTORY` kısmını mevcut bir klasörle değiştirin ve çalıştırın.

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### Beklenen çıktı

`DataTableWithStyleArray.xlsx` dosyasını Microsoft Excel’de açtığınızda şu tabloyu görmelisiniz:

| Amount |
|--------|
| **$1,234.56** |
| **$7,890.12** |

- Sayılar **para birimi biçimi** (`$` işareti, iki ondalık basamak) ile gösterilir.
- Her iki hücrenin yazı tipi **kalındır**, böylece öne çıkar.

## Yaygın varyasyonlar ve kenar durumları

| Senaryo | Değiştirilecek şey | Sebep |
|----------|--------------------|--------|
| **Farklı para birimi** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | Euro simgesi veya başka bir yerel biçim kullanmak. |
| **Farklı stillere sahip birden çok sütun** | Birden fazla `Style` nesnesi oluşturun, `styleArray`i sütun sırasına göre doldurun. | Her sütun kendi sayı biçimi, yazı tipi, arka plan vb. stiline sahip olabilir. |
| **Büyük veri setleri** | `cells.importDataTable(dataTable, false, "A1", importOptions);` ve `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` kullanın. | Başlık satırları veya gereksiz meta verileri atlayarak performansı artırır. |
| **İçe aktarmadan sonra stil uygulama** | Tek tek hücreler için `cells.get("A2").setStyle(currencyStyle);` çağırın. | Yalnızca belirli satırların özel biçimlendirmeye ihtiyacı olduğunda kullanışlıdır. |

## Üretim ortamı için ipuçları

- **Erken lisanslayın**: Değerlendirme filigranını önlemek için çalışma kitabını oluşturmadan önce Aspose.Cells lisansınızı kaydedin.
- **İş parçacığı güvenliği**: `Workbook` nesneleri **iş parçacığı güvenli değildir**. Aynı anda çok sayıda dosya üretmeniz gerekiyorsa, her iş parçacığı için ayrı bir örnek oluşturun.
- **Bellek yönetimi**: Çok büyük sayfalar için `Workbook`ın akış (streaming) API’sini (`Workbook` → `WorkbookDesigner`) kullanarak bellek tüketimini düşük tutun.
- **Test**: Kaydedilen dosyayı Apache POI ile açan ve hücre stilinin sayı biçiminin `"$#,##0.00"` olduğuna dair bir birim testi ekleyin.

## Sonuç

Artık Java’da **excel çalışma kitabı** oluşturmayı, **para birimi biçimi** ayarlamayı, **kalın yazı tipi** eklemeyi ve Aspose.Cells’in `ImportTableOptions` ile **stil nasıl içe aktarılır** konusunu doğru şekilde uygulamayı biliyorsunuz. Bu uçtan uca çözüm, manuel Excel adımlarını ortadan kaldırır ve her içe aktarılan hücrenin aynı **hücreleri para birimi olarak biçimlendirme** stilini taşımasını garanti eder.

Bir sonraki zorluğa hazır mısınız? Koşullu biçimlendirme eklemeyi, grafik yerleştirmeyi veya çalışma kitabını PDF’ye dönüştürmeyi deneyin — aynı stil‑dizisi tekniğini yeniden kullanarak. Mutlu kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve ilgili konuları ayrıntılı örneklerle ele alan içeriklerdir.

- [Create an Excel Workbook using Aspose.Cells in Java: A Step-by-Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}