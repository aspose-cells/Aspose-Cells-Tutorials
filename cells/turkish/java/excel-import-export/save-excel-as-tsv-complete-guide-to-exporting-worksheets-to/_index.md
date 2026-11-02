---
category: general
date: 2026-06-27
description: Java kullanarak Excel'i hızlıca TSV olarak kaydedin. Çalışma sayfasını
  metne dışa aktarmayı, sayfayı düz metin olarak dışa aktarmayı ve Aspose.Cells ile
  Excel veri dizesini dışa aktarmayı öğrenin.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: tr
og_description: Java kullanarak Excel'i TSV olarak kaydedin. Bu öğretici, çalışma
  sayfasını metne nasıl dışa aktaracağınızı, sayfayı düz metin olarak dışa aktaracağınızı
  ve Excel veri dizesini verimli bir şekilde dışa aktaracağınızı gösterir.
og_title: Excel'i TSV Olarak Kaydet – Adım Adım Dışa Aktarma Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Excel'i TSV Olarak Kaydet – Çalışma Sayfalarını Metne Dışa Aktarma Tam Kılavuzu
url: /tr/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i TSV Olarak Kaydet – Çalışma Sayfalarını Metne Aktarmanın Tam Kılavuzu

Hiç **Excel'i TSV olarak kaydetmek** istediğinizde hangi API çağrısını kullanacağınızı bilemediniz mi? Yalnız değilsiniz. Birçok geliştirici, bir elektronik tabloyu aşağı akış işlemleri için sekme‑ayırıcı bir dosyaya dönüştürmeye çalışırken bir engelle karşılaşıyor. İyi haber? Birkaç Java satırı ve Aspose.Cells ile bir çalışma sayfasını metne, çalışma sayfasını düz metne ve hatta Excel veri dizesini sorunsuz bir şekilde dışa aktarabilirsiniz.

Bu öğreticide, bir çalışma kitabını yüklemekten dışa aktarma seçeneklerini yapılandırmaya ve sonunda bir TSV dosyasını diske yazmaya kadar tüm süreci adım adım göstereceğiz. Sonunda, tek bir sayfa ya da onlarca dosyayı toplu olarak işleseniz de, herhangi bir Java projesinde **Excel'i TSV olarak kaydedebileceksiniz**.

## Bu Kılavuzda Neler Ele Alınıyor

- Diskten bir Excel çalışma kitabını yükleme  
- Doğru çalışma sayfasını seçme (veya birden fazlasını döngüyle işleme)  
- `ExportTableOptions` yapılandırarak düz‑metin çıktısı üretme  
- Veriyi sekme‑ayırıcı değerler (TSV) dosyası olarak yazma  
- Büyük aralıkları, farklı ayırıcıları ve Unicode karakterleri ele alma ipuçları  

Harici bir araç gerekmiyor—sadece Java için Aspose.Cells ve Java 8+ çalışma zamanı yeterli.

---

## Adım 1: Projenizi Kurun ve Çalışma Kitabını Yükleyin

Koda geçmeden önce, Aspose.Cells JAR dosyasını projenizin classpath'ine eklediğinizden emin olun. Maven kullanıyorsanız, bağımlılık şu şekilde görünür:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Şimdi çalışma kitabını yükleyebiliriz:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Neden önemli:** Dosyanın yüklenmesi, herhangi bir **export Excel data string** iş akışının ilk adımıdır. Dosya açılamazsa, başka hiçbir şey çalışmaz.

### Pro ipucu
Şifre korumalı dosyalarla çalışıyorsanız, şu şekilde çağırın: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## Adım 2: Dışa Aktarmak İstediğiniz Çalışma Sayfasını Seçin

İlk sayfayı, adıyla bir sayfayı alabilir ya da hepsini döngüyle işleyebilirsiniz. İşte en basit örnek—ilk çalışma sayfasını dışa aktarmak:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Eğer her sayfa için **export worksheet to text** yapmanız gerekiyorsa, yukarıdakini bir `for` döngüsü içinde sarın:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## Adım 3: Dışa Aktarma Seçeneklerini Oluşturun ve Yapılandırın

**export sheet plain text** işleminin kalbi `ExportTableOptions` içinde yatar. Birkaç özelliği değiştirerek aralığı sekme ayırıcıyla düz‑metin dizesine dönüştürüyoruz:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Neden `setExportAsString(true)` kullanmalı?**  
> Bu, Aspose.Cells'e çıktıyı ham metin olarak ele almasını söyler; bu da **Excel'i TSV olarak kaydetmek** istediğinizde tam olarak ihtiyacınız olan şeydir. Alternatif olarak CSV ya da HTML dışa aktarımı yapılabilir, ancak bunların hiçbiri temiz sekme ayrımı sağlamaz.

### Kenar Durumu: Özel Ayırıcılar
Eğer aşağı akış sisteminiz sekme yerine bir boru (`|`) karakteri bekliyorsa, sadece ayırıcıyı değiştirin:

```java
exportOptions.setDelimiter('|');
```

---

## Adım 4: İstenen Aralığı Metin Dosyasına Dışa Aktarın

Şimdi gerçekten TSV dosyasını yazıyoruz. `exportTable` metodu üç argüman alır: hücre aralığı, çıktı yolu ve az önce yapılandırdığımız `ExportTableOptions`.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

*Kullanılan* tüm aralığı dışa aktarmak istiyorsanız, `"A1:D20"` ifadesini `ws.getCells().getMaxDisplayRange()` ile değiştirin:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Pro ipucu
Dışa aktardıktan sonra, dizeyi doğrudan yakalayabilirsiniz:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Bu, dosya sistemine dokunmadan ham **export Excel data string** elde etmenizi sağlar.

---

## Adım 5: Büyük Dosyalarla Çalışma ve Performans İpuçları

Yüz binlerce satır içeren devasa elektronik tablolarla çalışırken, aşağıdaki iyileştirmeleri göz önünde bulundurun:

| Sorun | Çözüm |
|-------|----------|
| Bellek baskısı | Dosyayı tamamen yüklemek yerine akış olarak okumak için `WorkbookFactory.create(InputStream)` kullanın. |
| Yavaş G/Ç | `BufferedWriter` ile yazın ya da NIO `Files.newBufferedWriter` kullanın. |
| Unicode karakterleri | Çıktı dosyasının UTF‑8 ile yazıldığından emin olun: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Aşağıda, akış ve UTF‑8 kodlamasını birleştiren bir snippet bulunmaktadır:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## Yaygın Tuzaklar ve Nasıl Kaçınılır

1. **`setExportAsString(true)` ayarlamayı unutmak.**  
   Bu bayrak olmadan Aspose, ikili bir Excel dosyası üretir ve **export worksheet to text** hedefinizi bozar.

2. **Yanlış ayırıcı kullanmak.**  
   Sekme yerine virgül kullanmak CSV verir, TSV değil. `setDelimiter('\t')` değerini iki kez kontrol edin.

3. **Yanlış aralık sözdizimi.**  
   `"A1:D20"` doğru, ancak `"A1:D20:"` (fazladan iki nokta) bir `IllegalArgumentException` fırlatır.

4. **Dosya izinleri.**  
   Hedef dizinin yazılabilir olduğundan emin olun. Linux'ta genellikle `chmod 755` sorunu çözer.

---

## Hepsini Özetlemek – Tam Çalışan Örnek

İşte **Excel'i TSV olarak kaydet** işlemini baştan sona gösteren, eksiksiz ve çalıştırmaya hazır program:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

Bu programı çalıştırdığınızda, herhangi bir aşağı akış sistemi—veritabanı yükleyicisi, Unix `awk` betiği ya da basit bir elektronik tablo görüntüleyicisi—kullanabilecek sekme‑ayırıcı bir dosya (`out.tsv`) oluşturulur.

---

## Sonuç

Java ve Aspose.Cells kullanarak **Excel'i TSV olarak kaydetmek** için ihtiyacınız olan her şeyi ele aldık. Çalışma kitabını yüklemek, doğru sayfayı seçmek, `ExportTableOptions` yapılandırmak ve sonunda dosyayı yazmakla, artık **export worksheet to text**, **export sheet plain text** ve **export Excel data string** senaryoları için sağlam, üretime hazır bir deseniniz var.

Sırada ne var? Birden fazla aralığı dışa aktarmayı, ayırıcıları anlık olarak değiştirmeyi ya da çıktıyı doğrudan bir HTTP yanıtına akıtmayı deneyin. Aynı prensipler geçerlidir ve temel bilgiler yerinde olduğunda Excel verilerini düz metin olarak işlemek çok kolay olur.

Sorularınız mı var ya da tuhaf bir kenar durumuyla mı karşılaştınız? Aşağıya bir yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}