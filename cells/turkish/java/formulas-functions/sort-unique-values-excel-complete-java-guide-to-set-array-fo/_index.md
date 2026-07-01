---
category: general
date: 2026-06-30
description: Java kullanarak Excel'de benzersiz değerleri sıralayın. Formül ayarlamayı,
  formülleri yeniden hesaplamayı ve Aspose.Cells ile benzersiz bir liste Excel'i oluşturmayı
  öğrenin.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: tr
og_description: Java ile Excel’de benzersiz değerleri sıralayın. Bu kılavuz, formülü
  nasıl ayarlayacağınızı, formülleri nasıl yeniden hesaplayacağınızı ve birkaç dakika
  içinde benzersiz bir Excel listesi oluşturacağınızı gösterir.
og_title: Excel'de Benzersiz Değerleri Sırala – Dizi Formülleri için Java Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Excel'de Tekil Değerleri Sırala – Dizi Formüllerini Ayarlamak için Tam Java
  Rehberi
url: /tr/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel’de Tekil Değerleri Sıralama – Dizi Formüllerini Ayarlama İçin Tam Java Rehberi

Hiç **Excel’de tekil değerleri sıralama**yı formülleri sürüklemeden nasıl yapabileceğinizi merak ettiniz mi? Tek başınıza değilsiniz. Birçok raporlama senaryosunda temiz, alfabetik olarak sıralanmış benzersiz girişler listesine ihtiyaç duyarsınız ve bunu manuel olarak yapmak çok zahmetlidir.  

İyi haber? Birkaç satır Java kodu ile bir çalışma sayfasına **dizi formülü ayarlayabilir**, ardından **formülleri yeniden hesaplayarak** dökülen aralığın kendiliğinden doldurulmasını sağlayabilirsiniz. Bu öğreticide, bir çalışma kitabı oluşturmaktan Excel tarzı benzersiz bir liste üretmeye kadar her adımı adım adım inceleyeceğiz; böylece çözümü doğrudan uygulamanıza entegre edebileceksiniz.

## Bu Öğreticide Neler Ele Alınıyor

- Aspose.Cells ile bir Java projesi kurma (kod örneğinin gücünü sağlayan kütüphane).  
- `SORT` ve `UNIQUE` fonksiyonlarını birlikte kullanarak **Excel’de benzersiz liste oluşturma** sonuçları üretme.  
- Programatik olarak bir hücreye **dizi formülü** uygulama.  
- **Formülleri yeniden hesaplama** adımını tetikleyerek sonucun anında ortaya çıkmasını sağlama.  
- Çıktıyı doğrulama ve boş hücreler ya da bitişik olmayan aralıklar gibi kenar durumları için çözümü ayarlama.

Bu rehberi tamamladığınızda, temiz Excel dosyaları dışa aktarması gereken herhangi bir Java servisine hazır bir yöntem ekleyebileceksiniz.

> **Pro ipucu:** Zaten Maven kullanıyorsanız, Aspose.Cells’i bağımlılık olarak eklemek JAR dosyalarını manuel olarak yönetmek zorunda kalmamanızı sağlar.

---

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Java 8 ve üzeri | Aspose.Cells, Java 8+ hedefler. |
| Maven (veya Gradle) | Bağımlılık yönetimini basitleştirir. |
| Aspose.Cells for Java | Kullanacağımız `Workbook`, `Worksheet` ve formül API’lerini sağlar. |
| Excel fonksiyonlarına temel aşinalık | `SORT` ve `UNIQUE`’i anlamak kodu uyarlamanıza yardımcı olur. |

> *Henüz Aspose.Cells’iniz yoksa, `pom.xml` dosyanıza şunu ekleyin*:

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Adım 1: Yeni Bir Çalışma Kitabı Oluşturun (Formül Ayarlamaya Buradan Başlanır)

İlk olarak boş bir çalışma kitabına ihtiyacımız var. Bunu, daha sonra **A1 hücresine dizi formülü ayarlayacağımız** boş bir tuval olarak düşünün.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Neden yeni bir çalışma kitabı oluşturuyoruz?*  
> Temiz bir ortam garantiler, test verilerimize müdahale edebilecek gizli formüllerin oluşmasını önler.

---

## Adım 2: Örnek Verileri Doldurun (İsteğe Bağlı Ama Faydalı)

Sonucu net görmek için **B** sütununu bazı tekrar eden girişlerle dolduralım.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Neden B sütunu?*  
> Yazacağımız formül `B1:B10` aralığını referans alıyor, bu yüzden veriyi orada tutmak klasik Excel örneğiyle aynı hizayı sağlar.

---

## Adım 3: **Excel’de Tekil Değerleri Sıralama** İçin Bir Dizi Formülü Ayarlayın

Şimdi sihir gerçekleşiyor. `UNIQUE` (tekrarları kaldırmak) ile `SORT` (alfabetik sıralama) fonksiyonlarını birleştiriyoruz. Ortaya çıkan ifade bir **dizi formülü**dür; yani otomatik olarak yan hücrelere dökülür.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Nasıl Çalışıyor

- `UNIQUE(B1:B10)` aralığı tarar ve benzersiz metinlerden oluşan dikey bir dizi döndürür.  
- `SORT(...)` bu diziyi alır ve artan sırada düzenler.  
- Sonucun başına `=` koyup `setFormulaArray` metodunu çağırmak, Aspose.Cells’e sonucu Excel’deki gibi **dökülen dizi** olarak işlemeye söyler.

> **Not:** Daha eski bir Excel sürümü kullanıyorsanız ve `SORT` ya da `UNIQUE` bulunmuyorsa, **LET** fonksiyonu ile `SORT(UNIQUE(...))` ya da klasik dizi formülleri (`=INDEX(...)`) kullanabilirsiniz. Bu öğretici, **Excel’de benzersiz liste oluşturma**nın en temiz yolu olduğu için modern dinamik dizi yaklaşımına odaklanıyor.

---

## Adım 4: Dökülen Aralığın Doldurulması İçin Formülleri Yeniden Hesaplayın

Formül yerleştirildikten sonra çalışma kitabı otomatik olarak değerlendirme yapmaz. İşte **formülleri yeniden hesaplama** adımının devreye girdiği nokta.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

`calculateFormula()` çağrısı, Aspose.Cells’in Excel motorunu çalıştırarak `A1`, `A2`, … hücrelerini sıralı tekil değerlerle doldurur.

> *Neden tembel değerlendirmeye güvenmiyoruz?*  
> Sunucu tarafı bir bağlamda, hesaplamadan hemen sonra verinin (CSV, PDF vb.) dışa aktarılmaya hazır olması gerekir; bu yüzden açık bir çağrı tutarlılığı garantiler.

---

## Adım 5: Sonucu Doğrulayın (İsteğe Bağlı Hata Ayıklama)

Yeni bir API öğrenirken, dökülen değerleri konsola yazdırmak her zaman iyi bir fikirdir.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

Programı çalıştırdığınızda şu çıktı gelir:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

`SortedUniqueValues.xlsx` dosyasını açtığınızda aynı verinin `A1` hücresinden aşağı doğru döküldüğünü göreceksiniz.

---

## Kenar Durumlarıyla Baş Etme

### Kaynak Aralıktaki Boş Hücreler

`B1:B10` aralığında boşluklar varsa, `UNIQUE` bunları ayrı bir giriş olarak sayar. Boşlukları yok saymak için aralığı `FILTER` ile sarmalayın:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Bitşık Olmayan (Non‑Contiguous) Veriler

Verileriniz birden fazla sütunda ise, `UNIQUE` uygulamadan önce `CHOOSE` ya da `TEXTJOIN` ile birleştirebilirsiniz. Örneğin:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Bu ayarlamalar, daha karmaşık senaryolar için **formül ayarlama** esnekliğini gösterir.

---

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda eksiksiz, çalıştırılabilir bir Java programı bulunuyor. IDE’nize kopyalayıp yapıştırın, Aspose.Cells bağımlılığını ekleyin ve *Run* tuşuna basın.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Beklenen çıktı** (konsolda gösterildiği gibi) daha önce tartıştığımız sıralı, tekrarsız listeyle eşleşir. Oluşturulan Excel dosyasını açtığınızda aynı değerlerin `A1` hücresinden aşağı doğru döküldüğünü göreceksiniz.

---

## Sıkça Sorulan Sorular

**S: Bu, eski Excel sürümleri (Office 365 öncesi) ile çalışır mı?**  
C: `SORT` ve `UNIQUE` fonksiyonları Excel 365 ile tanıtılan Dinamik Dizi motorunun bir parçasıdır. Eski dosyalar için klasik dizi formülleri gibi `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}` kullanmanız gerekir. Aspose.Cells bunları hâlâ değerlendirebilir, ancak sözdizimi daha uzundur.

**S: Formülümü `A1` dışındaki bir hücreye ayarlayabilir miyim?**  
C: Kesinlikle. `cells.get("A1")` ifadesindeki adresi değiştirmeniz yeterlidir. Dökülen dizi, belirttiğiniz hücreden başlayarak sağa ve aşağı doğru genişleyecektir.

**S: Kaynak verim `B1:B10` aralığından daha büyükse ne yapmalıyım?**  
C: Statik aralığı dinamik bir aralıkla değiştirin, örneğin `B:B` ya da adlandırılmış bir aralık. Formül `=SORT(UNIQUE(B:B))` haline gelir. Çok büyük sayfalarda tüm sütun referansları performansı olumsuz etkileyebileceği için dikkatli olun.

---

## Sonuç

Java’da **formül ayarlama** yoluyla **Excel’de tekil değerleri sıralama**, **formülleri yeniden hesaplama** ve **Excel’de benzersiz liste oluşturma** konularını Aspose.Cells’in güçlü API’siyle ele aldık. Adımlar basit: bir çalışma kitabı oluşturun, verileri doldurun, bir dizi formülü uygulayın, hesaplamayı tetikleyin ve sonucu doğrulayın.  

Bundan sonra koşullu biçimlendirme ekleyebilir, PDF’ye dışa aktarabilir ya da yöntemi hazır raporlar sunan bir web servisine entegre edebilirsiniz. Temel fikir aynı kalır: ağır işi Excel’in kendi fonksiyonlarına bırakın, Java ise süreci yönetsin.

Excel otomasyonunuzu bir üst seviyeye taşımaya hazır mısınız? `SORT` yerine `SORTBY` kullanarak ikinci bir sütuna göre sıralamayı deneyin ya da `FILTER` ile iş kurallarına uymayan satırları dışarıda bırakın. Olanaklar neredeyse sınırsız.

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}