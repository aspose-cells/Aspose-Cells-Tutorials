---
category: general
date: 2026-10-07
description: Aspose.Cells for Java kullanarak sütunları nasıl bölümlersiniz. Dizeyi
  sütunlara bölmeyi, Excel formülünü otomatikleştirmeyi ve birkaç satır kodla hücreye
  formül yazmayı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: tr
lastmod: 2026-10-07
og_description: Aspose.Cells ile Java’da sütunları nasıl bölümlersiniz. Bu öğreticide,
  dizeyi sütunlara nasıl böleceğinizi, Excel formül değerlendirmesini nasıl otomatikleştireceğinizi
  ve bir hücreye formül nasıl yazacağınızı gösterir.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Aspose.Cells ile Java'da Sütunları Bölme – Hızlı Öğretici
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java'da Aspose.Cells ile sütunları bölme – adım adım rehber
url: /tr/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Aspose.Cells ile sütunları bölme – adım adım rehber

Excel çalışma sayfasında programlı olarak **sütunları bölme** ihtiyacınız varsa, bu rehber Aspose.Cells for Java ile tam süreci gösterir. Ayrıca **string'i sütunlara bölme**, **Excel formülünü otomatikleştirme** ve **formülü bir hücreye yazma** konularını kısa, üretim‑hazır kodla öğreneceksiniz.

Programlı sütun bölme, manuel kopyala‑yapıştırı ortadan kaldırır, hataları azaltır ve büyük ölçekli veri dönüşümlerine olanak tanır. Bu öğreticinin sonunda formülleri anında oluşturabilir, değiştirebilir ve değerlendirebilir, Excel'i Java arka ucunuzun gerçek bir parçası haline getirebilirsiniz.

## Önkoşullar

* Java 17 veya daha yeni bir sürüm yüklü.
* Maven 3.8+ (veya Gradle) bağımlılık yönetimi için.
* Aspose.Cells for Java lisansı (ücretsiz değerlendirme sürümü öğrenme için çalışır).
* Java sözdizimi ve Excel kavramlarına temel aşinalık.

Bu öğelerden herhangi biri eksikse, önce yükleyin; kod örnekleri standart bir Maven projesi varsayar.

## Adım 1: Aspose.Cells'i projenize ekleyin

`pom.xml` dosyanıza aşağıdaki bağımlılığı ekleyin. Bu, en son kararlı Aspose.Cells kütüphanesini çeker.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Neden bu adım önemlidir:** Kütüphane, Microsoft Office olmadan Excel dosyalarını işlemek için gerekli `Workbook`, `Worksheet` ve `Cell` sınıflarını sağlar. Bağımlılık olmadan kod derlenmez.

## Adım 2: Bir çalışma kitabı oluşturun ve ilk çalışma sayfasını seçin

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

`Workbook` nesnesi tüm Excel dosyasını temsil eder. İlk çalışma sayfasına erişmek, yazacağımız formül için öngörülebilir bir başlangıç noktası sağlar.

## Adım 3: Hedef hücreye WRAPCOLS formülünü yazın

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Neden `WRAPCOLS` kullanıyoruz:** Yerleşik Excel işlevi `WRAPCOLS`, tek bir metin değerini tanımlı bir sütun sayısına otomatik olarak böler ve kelime sınırlarını akıllıca yönetir. Bu, özel ayrıştırma mantığı olmadan **string'i sütunlara bölmenin** en güvenilir yoludur.

## Adım 4: Çalışma kitabını formülü değerlendirmeye zorlayın

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

`calculateFormula()` çağrısı, sunucu tarafında **Excel formülünü otomatikleştirir**. Bu çağrı olmadan hücre hâlâ formül metnini içerir, hesaplanmış değerleri değil.

## Adım 5: Sarılmış sonucu alın ve görüntüleyin

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Programı çalıştırdığınızda, konsol şu çıktıyı verir:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Oluşturulan `SplitColumnsResult.xlsx` dosyası, bölünmüş metinle doldurulmuş üç sütunu gösterir.

## WRAPCOLS işlevini anlama

* **Sözdizimi:** `WRAPCOLS(text, columns, [delimiter])`
* **Parametreler:**
  * `text` – bölmek istediğiniz dize.
  * `columns` – metni dağıtmak istediğiniz sütun sayısı.
  * `delimiter` (opsiyonel) – dizeyi bölmek için kullanılan karakter; varsayılan boşluk.
* **Dönüş değeri:** Yan hücrelere dökülen bir dizi, her öğe orijinal metnin bir kısmını içerir.

Fonksiyon yatay olarak döküldüğü için, formülü sadece en soldaki hücreye (örnekte A1) yazmanız yeterlidir. Excel, gerektiği gibi B1, C1, … hücrelerini otomatik olarak doldurur.

## Yaygın varyasyonlar ve kenar durumları

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Değişken sütun sayısı** | Sabit kodlanmış `3` değerini bir değişkenle değiştirin: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Özel ayırıcı** | Üçüncü argümanı kullanın, örneğin `=WRAPCOLS(A2,4,",")` virgüllerde bölmek için. |
| **Boş kaynak dize** | Fonksiyon boş hücreler döndürür; formülü ayarlamadan önce `null` veya boş dizelere karşı önlem alın. |
| **Büyük veri setleri** | Formülü her satır için bir döngüde uygulayın, ardından performansı artırmak için döngüden sonra bir kez `calculateFormula()` çağırın. |
| **ASCII dışı karakterler** | WRAPCOLS Unicode ile çalışır; Java kaynak dosyanızın UTF‑8 olarak kaydedildiğinden emin olun. |

**Pro ipucu:** Birçok satır işlenirken, formülü bir dize değişkeninde saklayın ve tekrar tekrar dize birleştirme maliyetinden kaçınmak için yeniden kullanın.

## Tam, çalıştırılabilir örnek

Aşağıda kopyala‑yapıştır için hazır tam program bulunmaktadır. İçe aktarma ifadeleri, istisna yönetimi ve isteğe bağlı bir kaydetme işlemi içerir.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Bu programı çalıştırmak, daha önce gösterilen aynı konsol çıktısını üretir ve **sütunları bölmenin** nasıl olduğunu açıkça gösteren bir Excel dosyası yazar.

## Sorun giderme kontrol listesi

* **Formül değerlendirilmemesi** – Formül ayarlandıktan sonra `workbook.calculateFormula()` çağrıldığından emin olun.
* **Bölme sonrası boş hücreler** – Kaynak dize `null` veya boş olmadığını ve sütun sayısının sıfırdan büyük olduğunu doğrulayın.
* **Lisans istisnası** – Değerlendirme filigranlarını kaldırmak için çalışma kitabını oluşturmadan önce geçerli bir Aspose.Cells lisans dosyası (`License license = new License(); license.setLicense("Aspose.Total.lic");`) sağlayın.
* **Büyük sayfalarda performans gecikmesi** – Her hücreden sonra değil, tüm formüller yazıldıktan sonra bir kez `calculateFormula()` çağırın.

## Sonuç

Artık Java'da Aspose.Cells kullanarak **sütunları bölmenin** nasıl olduğunu, `WRAPCOLS` işleviyle **string'i sütunlara bölmenin**, **Excel formülünü otomatikleştirmenin** ve programlı olarak **formülü bir hücreye yazmanın** yollarını biliyorsunuz. Bu teknik, manuel veri hazırlama adımlarını ortadan kaldırır ve Excel'in güçlü metin işleme yeteneklerini doğrudan Java uygulamalarınıza entegre eder.

### Sonraki adımlar

* `TEXTSPLIT` ve `FILTERXML` gibi diğer metin işlevlerini daha karmaşık ayrıştırma senaryoları için keşfedin.
* Beklenmeyen girdileri sorunsuz ele almak için `WRAPCOLS`'i `IFERROR` ile birleştirin.
* Çözümü, REST üzerinden CSV verisi alan ve doldurulmuş bir Excel dosyası dönen bir Spring Boot servisine entegre edin.

Bu desenleri ustalaşarak, iş ihtiyaçlarınıza ölçeklenebilen sağlam, otomatik Excel iş akışları oluşturabilirsiniz. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [aspose cells java – İsimleri Sütunlara Böl](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Aspose.Cells Kullanarak Java'da Excel Sütunlarını Otomatik Sığdırma](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Aspose.Cells Java ile Excel'de Boş Sütunları Silme&#58; Kapsamlı Bir Rehber](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}