---
category: general
date: 2026-06-21
description: 'WRAPCOLS''i Aspose.Cells Java ile nasıl kullanılır: diziyi satırlara
  dönüştürme, hücreye formül yazma ve hücreleri formülle doldurma – adım adım rehber.'
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: tr
og_description: Aspose.Cells ile Java’da WRAPCOLS kullanarak bir diziyi satırlara
  dönüştürme, bir hücreye formül yazma ve hücreleri formülle doldurma—hepsi tek bir
  rehberde.
og_title: Java'da WRAPCOLS Nasıl Kullanılır – Tam Excel WRAPCOLS Örneği
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: Java'da WRAPCOLS Nasıl Kullanılır – Tam Excel WRAPCOLS Örneği
url: /tr/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da WRAPCOLS Kullanımı – Tam Excel WRAPCOLS Örneği

Hiç **WRAPCOLS nasıl kullanılır** diye merak ettiniz mi, basit bir diziyi Excel’de düzenli bir tabloya dönüştürmeniz gerektiğinde? Tek başınıza değilsiniz. Birçok geliştirici `WRAPCOLS` fonksiyonunu ilk gördüklerinde bir duvara çarpar ve “Bu formülü Java’dan bir hücreye nasıl yazarım?” diye düşünür. İyi haber? Doğru adımları bildiğinizde oldukça basit.

Bu öğreticide, **diziyi satırlara dönüştüren**, formülü doğrudan bir hücreye yazan ve gerçek dünya senaryoları için **formülle hücreleri doldurmayı** gösteren tamamen çalıştırılabilir bir Aspose.Cells Java örneği üzerinden ilerleyeceğiz. Sonunda **excel wrapcols example** hakkında net bir resim elde edecek ve bunu kendi projelerinize uyarlamaya hazır olacaksınız.

## Önkoşullar

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

- Java 17 veya üzeri (kod, herhangi bir yeni JDK ile çalışır).
- Aspose.Cells for Java kütüphanesi (en son JAR dosyasını Maven Central’dan alabilirsiniz).
- Java sözdizimi ve Excel formülleri hakkında temel bir anlayış.
- Bir IDE ya da basit bir metin düzenleyici—özel bir araç gerekmiyor.

Her şey hazır mı? Harika, başlayalım.

## Adım 1: Projeyi Kurun ve Bir Çalışma Kitabı Yükleyin

İlk olarak—yeni bir Maven (veya Gradle) projesi oluşturun ve Aspose.Cells bağımlılığını ekleyin:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

Şimdi mevcut bir çalışma kitabını (veya yeni bir tane oluşturup) yükleyebilir ve ilk çalışma sayfasını alabiliriz:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Neden bir çalışma kitabı yüklüyoruz** – Aspose.Cells, bir Excel dosyasının bellek içi temsilinde çalışır. Bir çalışma kitabını yükleyerek (veya oluşturarak) hücrelere, satırlara ve formüllere erişim elde ederiz; bu, herhangi bir **write formula to cell** işlemi için gereklidir.

## Adım 2: WRAPCOLS Formülünü Bir Hücreye Ekleyin

Öğreticinin kalbi `WRAPCOLS` fonksiyonunda yatıyor. Tek boyutlu bir diziyi alır ve belirli bir sütun sayısına “sararak” yeni satırlara otomatik olarak taşır. Kullanacağımız sözdizimi şu şekildedir:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

Formülün `setFormula` metoduna düz bir metin olarak geçtiğine dikkat edin. Aspose.Cells ağır işi yapar—formülü ayrıştırır, değerlendirir ve sonuçları çalışma sayfasına yayar. Bu, satır ve sütunlar üzerinde manuel döngü yapmadan **populate cells with formula** işlemini gerçekleştirmenin en doğrudan yoludur.

### Formülün Ne Yaptığı

- `{1,2,3}` – üç sayı içeren bir dizi literalı.
- `2` – satır başına sütun sayısı.
- Sonuç:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (boş)

Üç sütun isteseydiniz, ikinci argümanı `3` olarak değiştirmeniz yeterli olur ve dizi tek bir satırı doldururdu.

## Adım 3: Çalışma Kitabını Kaydedin ve Çıktıyı Doğrulayın

Formül artık **A1** hücresinde olduğuna göre, çalışma kitabını diske kaydedelim ki Excel’de açıp yayılımı görebilesiniz:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

`output.xlsx` dosyasını açtığınızda yorumda anlatılanı tam olarak göreceksiniz—ilk satırda iki sütun ve kalan değer ikinci satırda. İşte **excel wrapcols example**’ın özü bu.

## Adım 4: Örneği Genişletmek – Daha Büyük Dizileri Dönüştürmek

Gerçek projeler nadiren sadece üç sayı ile çalışır. Diyelim ki `{10,20,30,40,50,60,70}` gibi daha büyük bir koleksiyonunuz var ve satır başına üç sütun istiyorsunuz. Kodu şu şekilde ayarlarsınız:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

Şimdi yayılım **C5** hücresinden başlayarak şu tabloyu üretir:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

Bu, formül dizesini sadece değiştirerek **convert array to rows** işlemini dinamik olarak nasıl yapabileceğinizi gösterir. Döngü yok, manuel hücre ataması yok—gerisini Aspose.Cells halleder.

## Adım 5: Kenar Durumlarını ve Yaygın Tuzakları Ele Alma

### 1. Boş Diziler

Dizi literalı boşsa (`{}`), `WRAPCOLS` bir `#VALUE!` hatası döndürür. Sayfanızın kırılmasını önlemek için formül oluşturmayı koruyun:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Sayısal Olmayan Veri

`WRAPCOLS` metinle de çalışır. Örneğin, `WRAPCOLS({"A","B","C","D"},2)` iki sütunluk bir dize düzeni üretir. Dizi literalı içinde metinleri tırnak içinde tutmayı unutmayın.

### 3. Uyumluluk

`WRAPCOLS` fonksiyonu Excel 365 ve Excel 2019+ (Office 2019, web Excel) sürümlerinde mevcuttur. Daha eski sürümleri desteklemeniz gerekiyorsa, manuel döngüye geri dönmeli veya farklı bir spill‑uyumlu fonksiyon kullanmalısınız.

## Adım 6: Pratik İpuçları ve Uzman Tüyoları

- **Pro tip:** Kullanıcının bölgesel ayarlarına bağlı olarak (virgül vs noktalı virgül) yerel ayarlı bir ayırıcıya ihtiyacınız varsa `Cell.setFormulaLocal` kullanın.
- **Dikkat:** Mevcut verilerin üzerine yazma. Yayılım alanı hedef aralıktaki mevcut içeriği değiştirecektir.
- **Performans notu:** Formül ayarlamak ucuzdur; asıl iş **save** veya **recalculate** sırasında gerçekleşir. Binlerce formül üretiyorsanız, otomatik hesaplamayı devre dışı bırakmayı (`wb.calculateFormula()` daha sonra) düşünün.

## Tam Çalışan Örnek

Aşağıda, tartıştığımız her şeyi içeren, eksiksiz ve çalıştırılabilir Java sınıfı yer almaktadır:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Beklenen çıktı:** `output.xlsx` dosyasını açtığınızda üç ayrı yayılım bölgesi göreceksiniz:

- **A1:B2** – 1‑3 sayıları iki sütuna sarılmış.
- **C5:E7** – 10‑70 sayıları üç sütuna sarılmış.
- **G1:H2** – meyve adları iki sütuna sarılmış.

## Sonuç

**WRAPCOLS**’ı Aspose.Cells for Java ile nasıl kullanacağınızı, **convert array to rows**, **write formula to cell** ve **populate cells with formula** işlemlerini temiz ve tekrarlanabilir bir şekilde nasıl yapacağınızı yeni öğrendik. Bu yaklaşım zahmetli döngüleri ortadan kaldırır, Excel’in yerel spill davranışından yararlanır ve kodunuzu özlü tutar.

Bir sonraki zorluğa hazır mısınız? `WRAPCOLS`’ı dinamik veri kaynaklarıyla birleştirin—belki bir veritabanından değerler çekip dizi dizesini anlık oluşturup Excel’in düzenleme işini yapmasına izin verin. `SEQUENCE` veya `FILTER` gibi diğer spill fonksiyonlarıyla da deneyler yaparak daha zengin raporlar oluşturabilirsiniz.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da Aspose’un kapsamlı dokümantasyonuna göz atın. İyi kodlamalar ve Java’dan modern Excel formüllerinin gücünün tadını çıkarın! 

![how to use wrapcols example](/images/wrapcols-demo.png "how to use wrapcols in Java – screenshot of spilled data")


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım‑adım açıklamalar içerir.

- [Java için Aspose.Cells ile Excel’de Hücre Aralıklarını Nasıl Seçilir (2023 Rehberi)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [Java için Aspose.Cells ile Excel’de Aktif Hücreyi Nasıl Ayarlarsınız: Tam Rehber](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Java için Aspose.Cells ile Excel Çalışma Kitaplarına Satır Nasıl Eklenir](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}