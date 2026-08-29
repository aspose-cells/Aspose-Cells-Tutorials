---
category: general
date: 2026-07-03
description: Java kullanarak Excel'de dizi genişletmeyi öğrenin. Bu öğreticide dizi
  satırlara genişletme, genişletmenin nasıl kullanılacağı ve formülü verimli bir şekilde
  ekleme konuları ele alınmaktadır.
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: tr
og_description: Java kullanarak Excel'de dizi genişletin. Bu kılavuzu izleyerek genişletmeyi
  nasıl kullanacağınızı, hücreye formül nasıl ekleyeceğinizi ve diziyi anında satırlara
  nasıl genişleteceğinizi öğrenin.
og_title: Java ile Excel'de Dizi Genişletme – Tam Programlama Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Java ile Excel'de Dizi Genişletme – Adım Adım Kılavuz
url: /tr/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Excel'de Dizi Genişletme – Tam Programlama Kılavuzu

Hiç **Excel'de diziyi genişletmeyi** hücreleri manuel olarak sürüklemeden nasıl yapabileceğinizi merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, özellikle yeni Excel `EXPAND` işlevi henüz yeni olduğunda, dinamik bir aralığı programlı olarak oluşturmak zorunda kaldıklarında bir çıkmaza giriyor. Bu rehberde **EXPAND** işlevinin **nasıl kullanılacağını**, formülü bir çalışma sayfasına nasıl ekleyeceğinizi ve sonucun istediğiniz satırlara nasıl yayılacağını adım adım göstereceğiz. Sonuna geldiğinizde **Java kodu ile tek satırda dizi satırlara genişletmeyi** başarabileceksiniz.

Aspose.Cells for Java kütüphanesini kullanarak tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Belirsiz referanslar yok, sadece kopyalayıp‑yapıştırabileceğiniz, derleyip çalıştırabileceğiniz somut kodlar. Yol boyunca her adımın neden önemli olduğunu tartışacağız, kesintili diziler gibi kenar durumlarını ele alacağız ve resmi dokümantasyonda bulunmayan birkaç profesyonel ipucu paylaşacağız. Hazır mısınız? Hadi başlayalım.

## Önkoşullar

Başlamadan önce şunların yüklü olduğundan emin olun:

* Java 17 (veya daha yeni bir JDK)
* Bağımlılık yönetimi için Maven veya Gradle
* Geçerli bir Aspose.Cells for Java lisansı (deneme sürümü test için yeterli)
* Excel formüllerine temel aşinalık – `VLOOKUP` ya da `SUMIF` kullandıysanız, hazırsınız demektir

Eğer bu maddelerden biri size yabancı geliyorsa, önce onları kurun; tutorial’ın geri kalan kısmı bunların hazır olduğunu varsayar.

## Adım 1: Maven Projenizi Oluşturun ve Aspose.Cells'i Ekleyin

İşleri düzenli tutmak için `ExpandArrayDemo` adında yeni bir Maven projesi oluşturun. `pom.xml` dosyanıza Aspose.Cells bağımlılığını ekleyin:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro ipucu:** Gradle kullanıyorsanız aynı bağımlılık şu şekilde görünür: `implementation 'com.aspose:aspose-cells:23.12'`.

Maven indirmeyi tamamladığında, **hücreye formül ayarlama** işini yapacak Java kodunu yazmaya hazırsınız.

## Adım 2: Bir Workbook Oluşturun ve İlk Worksheet'e Erişin

İlk kod parçası, daha önce gördüğünüz snippet'e benziyor, ancak bazı güvenlik kontrolleri ve yorumlar ekleyerek her satırın *neden* gerekli olduğunu anlayacaksınız.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*Neden önemli:* `Workbook` nesnesinin örneklenmesi, Aspose'un hücreleri, formülleri ve stilleri yönetmesi için gereken iç yapıların tahsis edilmesini sağlar. İlk worksheet'e erişmek, özellikle deneme aşamasındaysanız en yaygın giriş noktasıdır.

## Adım 3: EXPAND Formülünü Ekleyin – “Formül Nasıl Eklenir”

Şimdi tutorial’ın kalbi geliyor: **diziyi genişleten formülün nasıl ekleneceği**. Excel `EXPAND` işlevi üç argüman alır – kaynak dizi, istenen satır sayısı ve istenen sütun sayısı. Bizim örneğimizde `{1,2,3}` dizisini **5 satır** ve **1 sütun** olarak genişletmek istiyoruz.

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

`putValue` yerine `putFormula` kullandığımıza dikkat edin. Bu, Aspose'a string’i düz metin olarak değil gerçek bir Excel formülü olarak ele almasını söyler. `putFormula` metodu, string’i otomatik olarak ayrıştırır ve formül ağacını içsel olarak depolar.

### Neden EXPAND Kullanmalı?

`EXPAND`, doldurma tutamacını (fill handle) sürükleme zahmetini ortadan kaldırır. Ayrıca dinamik dizilerle çalışır; kaynak dizi değiştiğinde yayılmış aralık otomatik olarak güncellenir. Bu, raporları programlı olarak oluştururken özellikle kullanışlıdır.

## Adım 4: Hesaplamayı Zorla – Sonucu Somutlaştırma

API üzerinden *hücreye formül ayarladığınızda* workbook otomatik olarak yeniden hesaplanmaz. Dizinin **satırlara genişletilmesi** ve değerlerin sayfada görünmesi için bir hesaplama turu tetiklemeniz gerekir.

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

Bu adımı atlayıp `.xlsx` dosyasını Excel’de açarsanız, formül görünecek ama yayılmış değerler **F9** tuşuna basana kadar gösterilmeyecek. `calculate()` metodunu çağırarak workbook’un kutudan çıktığı gibi kullanılabilir olmasını sağlarsınız.

## Adım 5: Workbook’u Kaydedin ve Çıktıyı Doğrulayın

Son olarak workbook’u bir dosyaya yazın ve isteğe bağlı olarak yayılmış değerleri konsola basarak doğrulama yapın.

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Programı çalıştırdığınızda konsolda şu çıktıyı görmelisiniz:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel, kaynak dizi yalnızca üç eleman içerdiği için kalan satırları sıfırlarla doldurur. Bu, `EXPAND`’in varsayılan davranışıdır. Eğer sıfırlar yerine boş hücreler tercih ediyorsanız, diziyi `IFERROR` ile sarmalayabilir ya da `CHOOSE` hilelerini kullanabilirsiniz – bununla ilgili daha fazla bilgi “İleri Düzey Varyasyonlar” bölümünde.

## İleri Düzey Varyasyonlar & Kenar Durumları

### 1. Yatay Diziyi Birden Çok Sütuna Genişletme

**Diziyi satırlara** *ve* sütunlara genişletmek istiyorsanız, üçüncü argümanı değiştirmeniz yeterlidir:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

Şimdi aralık 5 × 3 bir blok olarak yayılır ve eksik hücreler sıfırlarla doldurulur.

### 2. Kaynak Olarak Adlandırılmış Bir Aralık Kullanma

Literal `{1,2,3}` yerine, çalışma zamanında değişebilecek bir adlandırılmış aralığa referans verebilirsiniz:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

`MySourceRange`’in var olduğundan emin olun (bunu `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")` ile oluşturabilirsiniz).

### 3. Sayısal Olmayan Verileri İşleme

`EXPAND` metinle de çalışır. Örneğin:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

Ekstra satır boş bir string olarak görünecek, sıfır değil.

### 4. `IFERROR` ile Sıfır Doldurmayı Önleme

Eğer sıfırlar yerine boş hücreler görmek istiyorsanız, `EXPAND`i `IFERROR` ile sarmalayın:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

Artık 4. ve 5. satırlar gerçekten boş olacaktır.

## Yaygın Tuzaklar ve Çözüm Önerileri

| Tuzak | Neden Oluşur | Çözüm |
|---------|----------------|-----|
| **Formül yeniden hesaplanmıyor** | `ws.getCells().calculate()` unutulması | `putFormula` sonrası her zaman `calculate()` çağırın. |
| **Boşluk beklenirken sıfır değerleri** | `EXPAND` varsayılan olarak sıfırla doldurur | `IFERROR(..., "")` ya da `CHOOSE` ile sarmalayın. |
| **Yanlış hücre adresi** | `"A0"` ya da `"1A"` kullanmak | Excel adresleri 1’den başlar; Aspose `"A1"` stilini bekler. |
| **Kütüphane sürüm uyumsuzluğu** | `EXPAND` desteği olmayan eski Aspose.Cells sürümü | En yeni sürüme (yazım anında 23.12) yükseltin. |

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda tamamen kopyala‑yapıştır‑hazır program bulunuyor. `ExpandArrayDemo.java` olarak kaydedin, derleyin ve çalıştırın.

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

Bu programı çalıştırdığınızda **A1 hücresi** artık `EXPAND` formülünü içerir ve A sütununun 1‑5 satırları `1, 2, 3, 0, 0` değerlerini gösterir. Dosyayı Excel’de açtığınızda aynı sonucu anında görürsünüz—manuel sürükleme gerekmez.

## Sonuç

Java kullanarak **Excel'de dizi genişletmeyi**, **EXPAND** işlevini nasıl kullanacağınızı ve **hücreye formül ayarlama** ile **diziyi satırlara genişletme** adımlarını programlı olarak nasıl gerçekleştireceğinizi öğrendiniz. Aspose.Cells sayesinde hantal UI hilelerinden kaçınır, kodun işi yapmasını sağlarsınız. İster bir raporlama motoru, ister otomatik veri girişi aracı, ister özel bir elektronik tablo üreticisi geliştirin, bu teknik size sayısız saat tasarrufu sağlayacak.

Sırada ne var? Statik diziyi başka bir sayfadan çekilen dinamik bir aralıkla değiştirin, çok‑sütunlu yayılmaları deneyin ya da güçlü veri dönüşümleri için `EXPAND`i `FILTER` ile birleştirin. Ufuk geniş, ve artık sağlam bir temele sahipsiniz.

Sorularınız mı var ya da ilginç bir kullanım senaryosu paylaşmak mı istiyorsunuz? Bırakın bir yorum bırakın.


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki tutoriallar, bu rehberde gösterilen tekniklere dayalı olarak yakın konuları kapsar ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}