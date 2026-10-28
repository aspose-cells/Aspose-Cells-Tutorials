---
category: general
date: 2026-09-05
description: Excel'de aralık kopyalamayı, Excel'i PowerPoint'e aktarmayı ve Excel'i
  pptx formatına dönüştürmeyi eksiksiz bir Java örneğiyle öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: tr
lastmod: 2026-09-05
og_description: Java kullanarak aralığı kopyalama ve Excel'i PowerPoint'e aktarma.
  Excel'i PPTX'e verimli bir şekilde dönüştürmek için bu adım adım rehberi izleyin.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Java'da Excel'den bir aralığı kopyalayıp PowerPoint'e nasıl dışa aktarılır
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Java kullanarak Excel'den aralığı kopyalayıp PowerPoint'e dışa aktarma
url: /tr/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Excel'den Aralık Kopyalama ve PowerPoint'e Aktarma

Eğer bir Excel çalışma kitabından **aralık nasıl kopyalanır** ve ardından **Excel'i PowerPoint'e aktar** ihtiyacınız varsa, bu kılavuz size eksiksiz, çalıştırmaya hazır bir çözüm sunar. Pivot tablo içeren bir aralığı nasıl kopyalayacağınızı, kopya için yeni bir çalışma sayfası oluşturmayı ve sonunda tek bir metod çağrısıyla **Excel'i PPTX'e dönüştürmeyi** göreceksiniz.

Aralıkları kopyalamak ve çalışma kitaplarını dışa aktarmak, raporlar, slayt desteleri veya gösterge tabloları oluştururken yaygın bir gereksinimdir. Bu öğreticinin sonunda aşağıdaki özelliklere sahip bir Java programınız olacak:

* Mevcut bir `.xlsx` dosyasını yükler.
* Pivot tablo içeren `A1:H20` aralığını yeni bir sayfaya kopyalar.
* Çalışma kitabını düzenlenebilir bir `.pptx` sunumu olarak kaydeder.

Yalnızca Aspose.Cells for Java kütüphanesine ihtiyacınız var; ek bağımlılık gerektirmez.

## Prerequisites

Başlamadan önce aşağıdakilerin kurulu olduğundan emin olun:

* Java 17 (veya daha yeni bir sürüm) yüklü.
* Bağımlılıkları yönetmek için Maven veya Gradle.
* Aspose.Cells for Java 23.9 (veya en son sürüm) – aşağıdaki Maven örneğinde gösterildiği gibi projenize ekleyin.
* Kopyalamak istediğiniz verileri ve bir pivot tabloyu içeren bir Excel dosyası (`input.xlsx`).

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Step 1: Load the workbook from a file

**aralık nasıl kopyalanır** işleminin ilk adımı, kaynak çalışma kitabını açmaktır. Bu adım, çalışma sayfalarına, hücrelere ve pivot tablolara erişim sağlar.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Why this step?*  
Dosyanın yüklenmesi, Excel belgesinin bellek içi bir temsilini oluşturur; böylece orijinal dosyaya dokunmadan içeriğini manipüle edebilirsiniz.

## Step 2: Get the source worksheet that holds the data

Genellikle ilk sayfa, kopyalamak istediğiniz verileri içerir. Bu sayfayı indeksle alabilirsiniz.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

Çalışma kitabınız pivot tabloyu farklı bir sayfada tutuyorsa, `0` yerine uygun indeksi kullanın veya `get("SheetName")` ile sayfayı alın.

## Step 3: Add a new worksheet for the copied range

Hedef bir sayfa oluşturmak, kopyalanan verileri izole eder ve sonraki dışa aktarma işlemini daha temiz hâle getirir.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

Sayfayı istediğiniz gibi adlandırabilirsiniz; “Copy” adı, çoğaltılan aralığı barındırdığını açıkça gösterir.

## Step 4: Copy the range (how to copy range) including the pivot table

Şimdi temel **aralık nasıl kopyalanır** işlemini gerçekleştiriyoruz. `copyRange` metodu hem değerleri hem de biçimlendirmeyi kopyalar ve pivot tablo tanımını korur.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*Why use `CopyOptions`?*  
Bir `CopyOptions` örneği sağlamak, neyin kopyalanacağını (ör. formüller, sütun genişlikleri) ince ayar yapmanıza olanak tanır. Varsayılan yapıcı her şeyi kopyalar; bu, **copy pivot table sheet** işlemini tam bir kopya olarak almak istediğinizde idealdir.

## Step 5: Prepare options to export the workbook as an editable PowerPoint presentation

PowerPoint'e dışa aktarma, `ImageOrPrintOptions` aracılığıyla yapılır. Kaydetme formatını `SaveFormat.PPTX` olarak ayarlamak, Aspose.Cells'in bir resim yerine PowerPoint dosyası üretmesini sağlar.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

Özel bir düzen ihtiyacınız varsa, `pptOptions` üzerinden slayt boyutlarını, DPI değerini ve diğer sunum ayarlarını da değiştirebilirsiniz.

## Step 6: Save the workbook as a PPTX file (convert excel to pptx)

Son olarak, PPTX seçenekleriyle `workbook.save` metodunu çağırın. Bu adım **excel'i pptx'e nasıl dışa aktarılır** sorusunun cevabıdır.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

Program tamamlandığında, `output.pptx` içinde kopyalanan aralığın Excel'deki gibi göründüğü tek bir slayt bulunur; pivot tablo kontrolleri de korunur.

### Expected output

`output.pptx` dosyasını Microsoft PowerPoint veya uyumlu bir görüntüleyicide açın. `A1:H20` aralığının hücre renkleri, kenarlıkları ve pivot tablo düzeniyle aynı şekilde gösterildiği bir slayt görmelisiniz. Slayt tamamen düzenlenebilir— tabloyu hareket ettirebilir, yeniden boyutlandırabilir veya biçimlendirebilirsiniz, tıpkı yerel PowerPoint içeriği gibi.

## Full runnable example

Tüm adımları bir araya getirdiğinizde aşağıdaki gibi bağımsız bir Java sınıfı elde edersiniz:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

Sınıfı IDE'nizden veya komut satırından çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

Dosya yazıldıktan sonra onay mesajını göreceksiniz.

## Common questions and edge cases

| Question | Answer |
|----------|--------|
| **Kesintili (non‑contiguous) bir aralık kopyalayabilir miyim?** | Birden çok alanı içeren adlandırılmış bir aralıkla `copyRange` kullanın veya her blok için `copyRange` metodunu ayrı ayrı çağırın. |
| **Kaynak sayfa birden fazla pivot tablo içeriyorsa ne olur?** | Kopyalanan dikdörtgen içindeki her pivot tablo aktarılır. Dışındaki tabloları ayrı ayrı kopyalamanız gerekir. |
| **Birden fazla sayfayı ayrı slaytlar olarak nasıl dışa aktarırım?** | Çalışma sayfaları üzerinde döngü kurun, her birini geçici bir sayfaya kopyalayın ve her yineleme için `workbook.save` metodunu `pptOptions` ile çağırarak aynı PPTX'e `Presentation` API'siyle ekleyin. |
| **Oluşturulan PPTX düzenlenebilir mi?** | Evet. Dışa aktarma, yerel PowerPoint nesneleri oluşturur; böylece metni değiştirebilir, tabloları yeniden şekillendirebilir veya animasyon ekleyebilirsiniz. |
| **Büyük çalışma kitaplarıyla ne yapılmalı?** | Daha yüksek doğruluk için `pptOptions.setDpi(300)` değerini artırın, ancak bellek kullanımına dikkat edin; gerekirse sayfaları toplu olarak işleyin. |

## Pro tips

* **Sütun genişliklerini koruyun** – Tam eşleşme gerekiyorsa kopyalamadan önce `CopyOptions.setColumnWidth(true)` ayarlayın.
* **Özel slayt boyutu kullanın** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` ile 16:9 bir sunuma uyum sağlayın.
* **Başlık slaytı ekleyin** – Dışa aktarmadan sonra PPTX'i Aspose.Slides ile açıp bir başlık ve tarih içeren slaytı ön ek olarak ekleyin.

## Conclusion

Artık **aralık nasıl kopyalanır**, **Excel'i PowerPoint'e aktar** ve **excel'i pptx'e dönüştür** işlemlerini Java ile yapabildiğinize emin olabilirsiniz. Yukarıdaki altı adımı izleyerek rapor üretimini otomatikleştirebilir, canlı verilerden slayt desteleri oluşturabilir ve pivot‑tablo işlevselliğini koruyabilirsiniz.

### What’s next?

* **copy pivot table sheet** gibi sadece pivot önbelleğini kopyalama varyasyonlarını keşfedin.
* **Aspose.Slides** ile bu iş akışını birleştirerek özel animasyonlar veya kurumsal kimlik ekleyin.
* Zamanlanmış bir görevde onlarca çalışma kitabını toplu işlemek için otomasyonu geliştirin.

Seçeneklerle denemeler yapın ve kodu kendi raporlama hattınıza uyarlayın. Sorun yaşarsanız, Aspose.Cells for Java dokümantasyonu `CopyOptions` ve `ImageOrPrintOptions` hakkında daha derin bilgiler sunar. Kodlamanın tadını çıkarın!


## What Should You Learn Next?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları ayrıntılı bir şekilde ele alan tam çalışan kod örnekleri içerir. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar sunar.

- [Excel'i PowerPoint'e Aktarma – Adım Adım Kılavuz](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Aspose.Cells Java ile Excel'de Birden Fazla Sütunu Kopyalama: Tam Kılavuz](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Aspose.Cells for .NET ile Excel'i PowerPoint'e Dönüştürme: Tam Kılavuz](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}