---
category: general
date: 2026-11-22
description: Excel'i metin olarak dışa aktarmayı ve sekme ile ayrılmış bir dosya oluşturmayı
  öğrenin. Bu rehber, tüm alanları tırnak içine almayı ayarlamayı ve elektronik tablo
  metnini verimli bir şekilde kaydetmeyi gösterir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: tr
lastmod: 2026-11-22
og_description: Excel'i metin olarak dışa aktarın ve sekme sınırlı bir dosya oluşturun.
  Tüm alanları tırnak içine alıp elektronik tablo metnini Java ile kaydetmek için
  bu adım adım öğreticiyi izleyin.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Excel'i Metin Olarak Dışa Aktar – Tab‑Ayırmalı Dosya Rehberi
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Excel'i sekme ayrımlı metin olarak nasıl dışa aktarılır
url: /tr/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i Metin Olarak Dışa Aktarma ve Sekme‑Ayırmalı Çıktı Oluşturma

Eğer **Excel'i metin olarak dışa aktarmanız** gerekiyorsa, bu öğretici bir çalışma kitabından sekme‑ayırmalı bir dosya oluşturma sürecini adım adım gösterir. Veri‑göçü hattı kuruyor olsanız ya da sonraki işleme için hızlı bir CSV‑stilinde döküm ihtiyacınız varsa, aşağıdaki adımlar **tablo metnini kaydetmenize** izin verir ve ayırıcılar ile alıntılamalar üzerinde tam kontrol sağlar.

Spreadsheet verilerini düz metin olarak dışa aktarmak, yerel `.xlsx` formatını tutmaktan genellikle daha taşınabilir olur. Bu rehberde ayrıca **tüm alanları alıntılamayı** öğreneceksiniz; bu, sekme, virgül veya satır sonu içeren değerlerin güvenli bir şekilde kapsüllenmesini garanti eder.

## Gerekenler

* Java 17 veya daha yeni bir sürüm kurulu.
* Aspose.Cells for Java kütüphanesi (kod bu kütüphaneden `ExportOptions` ve `ExportTableOptions` kullanıyor). Maven üzerinden ekleyebilirsiniz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Java programını derlemek ve çalıştırmak için bir IDE veya basit bir metin düzenleyici.

## Excel'i Metin Olarak Dışa Aktarma – adım‑adım

Aşağıdaki bölümler görevi üç mantıksal adıma ayırır. Her adım **neden** önemli olduğunu, sadece **ne** yazılması gerektiğini açıklamaz.

### Adım 1: Çalışma kitabını ve örnek veriyi hazırlama

Bir çalışma kitabı oluşturmak, dışa aktarabileceğiniz bir şey sağlar. Gerçek bir projede `new Workbook("input.xlsx")` ile mevcut bir dosyayı yüklersiniz; burada örnek kutudan çıkmadan çalışması için küçük bir sayfa oluşturuyoruz.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Bu adım neden?*  
Bir çalışma kitabı, herhangi bir dışa aktarma işleminin kaynak nesnesidir. Birkaç satır ekleyerek **tüm alanları alıntıla** seçeneğinin gerçekten virgül ve diğer özel karakterleri koruduğunu doğrulayabilirsiniz.

### Adım 2: Dışa aktarma seçeneklerini yapılandırma – ayırıcı, alıntı ve çıktı modu

**tab‑ayırmalı tablo dışa aktarma**'nın temeli `ExportTableOptions` içinde yatar. Ayırıcıyı bir sekme (`'\t'`) olarak ayarlarsınız ve `setQuoteAllFields(true)`'ı etkinleştirerek her hücre çift tırnak içinde olur. Bu, bir hücrede sekme veya yeni satır olduğunda belirsizliği ortadan kaldırır.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Bu adım neden?*  
- **Delimiter** (Ayırıcı) sütunların nasıl ayrılacağını belirler. Bir sekme (`\t`) birçok veri‑işleme aracının kabul ettiği bir **sekme‑ayırmalı dosya** oluşturur.  
- **Quote all fields** (Tüm alanları alıntıla) bir hücre ayırıcı içeriyor olsa bile, ortaya çıkan metnin ayrıştırılabilir kalmasını garanti eder.  
- `ExportAsString` ayarı, Aspose.Cells'in ikili bir çalışma kitabı yerine bir dize üretmesini söyler; bu da **tablo metnini kaydetmek** için tam olarak ihtiyacınız olan şeydir.

### Adım 3: Çalışma kitabını sekme‑ayırmalı bir metin dosyası olarak kaydetme

Şimdi gerçekten **Excel'i metin olarak dışa aktarıyorsunuz**. `save` yöntemi hedef yolu ve yapılandırdığınız `ExportOptions`'ı alır.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

Program tamamlandığında, içinde `output/table.txt` dosyasını bulacaksınız:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Bu adım neden?*  
`save` çağrısı **sekme‑ayırmalı dosyayı** diske yazar, etkili bir şekilde **tablo metnini kaydeder**; bu format Excel, Notepad veya sekmeleri anlayan herhangi bir veri‑ithalat aracıyla açılabilir.

## Excel'i Metin Olarak Dışa Aktarırken Tüm Alanları Nasıl Alıntılayabilirsiniz

`setQuoteAllFields(true)`'ı atladığınızda, sekme, virgül veya satır sonu içeren hücreler çıktı dosyasının yapısını bozar. Örneğin, `Bob, Jr.` satırı iki sütuna bölünerek veri kümesini bozar. Alıntılamayı her zaman şu durumlarda etkinleştirin:

* Kaynak veriniz virgül, sekme veya yeni satır içerebilir.
* Sonraki aşamadaki ayrıştırıcılar alıntılı CSV/TSV dosyaları bekler.
* Hücre içeriğine bakılmaksızın belirli bir dışa aktarma ihtiyacınız var.

## Aspose.Cells Olmadan Sekme‑Ayırmalı Dosya Oluşturma (isteğe bağlı)

Üçüncü‑taraf kütüphaneler olmadan saf Java çözümünü tercih ediyorsanız, satırları döngüyle gezip manuel olarak yazabilirsiniz:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

Bu kod parçacığı aynı **tab‑ayırmalı tablo dışa aktarma** mantığını gösterir: sekme ayırıcı, her alanı alıntılamak ve sonucu düz metin olarak yazmak. Ancak, Aspose.Cells kullanmak büyük çalışma kitaplarını yönetmeyi basitleştirir, biçimlendirmeyi korur ve gereksiz kodu azaltır.

## Yaygın Tuzaklar ve Uzman İpuçları

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| **Çıktıda sekmeler eksik** | Ayırıcı varsayılan virgül olarak bırakıldı. | `setDelimiter('\t')` metodunu açıkça çağırın. |
| **Alıntılanmamış virgüller sütunları bozar** | `quoteAllFields` etkinleştirilmedi. | `setQuoteAllFields(true)` kullanın veya manuel olarak alıntılayın. |
| **Dosya oluşturulmadı** | Çıktı dizini mevcut değil. | `output/` klasörünün var olduğundan emin olun veya `Files.createDirectories` kullanın. |
| **Kodlama sorunları** | Varsayılan platform kodlaması ASCII olmayan karakterleri bozabilir. | Gerekirse `ExportOptions.setEncoding(Encoding.getUTF8())` parametresini geçin. |

## Sonucu Test Etme

Programı çalıştırdıktan sonra:

1. `output/table.txt` dosyasını bir düz‑metin düzenleyicide açın. Her değerin çift tırnak içinde ve sütunların tek bir sekme karakteriyle ayrılmış olduğunu görmelisiniz.  
2. Dosyayı Excel'e aktarın (`Data → From Text/CSV`). Ayırıcı olarak **Tab** seçin; Excel her alıntılanmış değeri kendi hücresine doğru şekilde yerleştirir.  
3. Özel karakterleri (virgüller, satır sonları

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [excel'i dışa aktarma – Sekme‑Ayırmalı Metin Rehberi](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Aspose.Cells kullanarak Özel Ayırıcıyla Excel'i Metin Dosyası Olarak Kaydet](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Aspose.Cells ile Excel'i Metin Olarak Kaydetme – adım‑adım rehber](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}