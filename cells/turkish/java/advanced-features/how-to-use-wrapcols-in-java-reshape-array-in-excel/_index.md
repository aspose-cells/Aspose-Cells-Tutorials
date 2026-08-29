---
category: general
date: 2026-08-04
description: wrapcols'i tam bir Java örneğiyle nasıl kullanılır, Excel'de dizi yeniden
  şekillendirme ve Aspose.Cells kullanarak çalışma kitabını dosyaya kaydetme
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: tr
lastmod: 2026-08-04
og_description: Java ile Excel'de bir diziyi yeniden şekillendirmek için wrapcols
  nasıl kullanılır. Tam bir Excel wrapcols örneğini öğrenin, Java ile Excel çalışma
  kitabı oluşturun ve çalışma kitabını dosyaya kaydedin.
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: Java'da wrapcols nasıl kullanılır – adım adım rehber
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java'da wrapcols nasıl kullanılır – Excel'de dizi yeniden şekillendirme
url: /tr/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da wrapcols nasıl kullanılır – Excel'de dizi yeniden şekillendirme

Düz bir değer listesini çok‑satırlı bir aralığa dönüştürmek için **how to use wrapcols**'a ihtiyacınız varsa, bu kılavuz size tam adımları gösterir. **excel wrapcols example**'ı göreceksiniz; bu örnek 1‑D bir diziyi 3 satır × 2 sütunluk bir bloğa yeniden şekillendirir ve Aspose.Cells ile **save workbook to file**'ı nasıl yapacağınızı öğreneceksiniz.

Bu öğreticinin sonunda **create excel workbook java** kodunu şu şekilde yazabilecek duruma geleceksiniz:

* Yeni bir çalışma kitabı başlatır ve A1 hücresini seçer.  
* `WRAPCOLS` işlevini uygulayarak verileri yeniden şekillendirir.  
* Formül hesaplamasını zorlayarak sonucun anında görünmesini sağlar.  
* Hesaplanan diziden bir değer alır.  
* Çalışma kitabını diske kaydeder.

Tek gereksinim, bir Java geliştirme ortamı (JDK 8 veya daha yeni) ve Aspose.Cells for Java kütüphanesidir.

---

## Önkoşullar

* JDK 8 + (veya daha yeni bir sürüm).  
* Aspose.Cells bağımlılığını yönetmek için Maven veya Gradle.  
* Java sözdizimi ve Excel formüllerine temel aşinalık.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Gradle kullanıyorsanız, XML parçacığını ilgili `implementation` satırıyla değiştirin.

---

## Adım 1: Java'da bir Excel çalışma kitabı oluşturma

İlk işlem, yeni bir çalışma kitabı açan ve ilk çalışma sayfasını ve A1 hücresini alan **create excel workbook java** kodunu **create excel workbook java** yazmaktır.

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

Çalışma kitabını bu şekilde oluşturmak size temiz bir başlangıç sağlar ve örneğin mevcut bir dosya olmadan herhangi bir makinede çalışmasını garantiler.

---

## Adım 2: WRAPCOLS işlevini uygulama – bir excel wrapcols örneği

`WRAPCOLS`, tek‑boyutlu bir dizi ve bir sütun sayısı alır, ardından önce satırları dolduran bir aralık döndürür. Bu, **reshape array in excel**'in çekirdeğidir.

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

Neden bu çalışıyor:

* Literal dizi `{1,2,3,4,5,6}` altı sayı sağlar.  
* `WRAPCOLS(..., 2)`, Excel'e değerleri 2 sütuna sarmasını söyler ve tüm öğeleri sığdırmak için otomatik olarak yeterli satır (bu örnekte 3) oluşturur.  
* Ortaya çıkan aralık **A1:B3** hücrelerini kaplar:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## Adım 3: Formülün yansıtılması için hesaplamayı zorlamak

Aspose.Cells, formülleri ayarladığınızda otomatik olarak değerlendirmez. Sonucu somutlaştırmak için `calculateFormula()` metodunu çağırmanız gerekir.

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

Bu yöntemi çağırmak, `WRAPCOLS` tarafından üretilen dizinin hücrelere yazılmasını sağlar ve değerleri anında okumanıza imkan tanır.

---

## Adım 4: Yeniden şekillendirilmiş diziden bir değer almak

Formülün çalıştığını kanıtlamak için hedef hücrenin dize temsilini okuyun. `WRAPCOLS` bir dizi döndürdüğü için Excel, formülün bulunduğu hücrede **ilk öğeyi** (değer `1`) gösterir.

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**Beklenen konsol çıktısı**

```
First element: 1
```

Excel'de çalışma sayfasını incelerseniz, daha önce açıklanan tam 3 × 2 bloğun doldurulduğunu göreceksiniz.

---

## Adım 5: Çalışma kitabını bir dosyaya kaydetme – how to save workbook to file

Çalışma kitabını kalıcı hale getirmek, daha sonra Excel'de açmanıza veya iş arkadaşlarınızla paylaşmanıza olanak tanır. Tam bir yol ile `save` metodunu kullanın.

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

Programı çalıştırmak, çalışma dizininde `WrapFunctions.xlsx` dosyasını oluşturur. Dosyayı açtığınızda A1:B3 hücrelerinde yeniden şekillendirilmiş dizi görünür ve **save workbook to file** işleminin başarılı olduğu doğrulanır.

---

## Tam, çalıştırılabilir örnek

Tüm parçaları bir araya getirerek, bir IDE'ye kopyalayıp çalıştırabileceğiniz tam program aşağıdadır:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**Sonuç doğrulaması**

1. Konsol `First element: 1` yazdırır.  
2. Oluşturulan `WrapFunctions.xlsx` şunları içerir:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

Diziyi başka bir yerde referans göstermeniz gerekirse, örneğin `worksheet.getCells().get("B2").getIntValue()` kullanarak doldurulmuş hücrelerden herhangi birini okuyabilirsiniz.

---

## Yaygın sorular ve kenar durumları

| Question | Answer |
|----------|--------|
| *WRAPCOLS sayısal olmayan dizileri işleyebilir mi?* | Evet. Küme parantezleri içinde metin, tarih veya mantıksal değerler geçirebilir ve Excel bunları buna göre sarar. |
| *Excel'in görüntüleyebileceğinden daha fazla satıra ihtiyacım olursa ne olur?* | WRAPCOLS, kaynak dizi tükenene kadar ek satırlara dökmeye devam eder. Çalışma sayfasının yeterli satıra (varsayılan limit 1.048.576) sahip olduğundan emin olun. |
| *Sütun sayısını nasıl değiştiririm?* | `WRAPCOLS`'in ikinci argümanını değiştirin. Üç sütun için `=WRAPCOLS({1,2,3,4,5,6}, 3)` kullanın; bu 2 × 3 bir blok üretir. |
| *Sonucu farklı bir başlangıç hücresine yazmak mümkün mü?* | Evet. Formülü herhangi bir hücreye (ör. `C5`) ayarlayın; sarılmış aralık o hücreye göre genişleyecektir. |
| *Formülü her değiştirdiğimde `calculateFormula` çağırmam gerekir mi?* | Programatik olarak bir formülü değiştirdiğinizde, bağımlı hücreleri yenilemek için `calculateFormula` veya `calculateFormula(true)` metodunu çağırın. |

---

## Sonuç

Bu öğretici, Java'da **how to use wrapcols**'ı **reshape array in excel** için nasıl kullanacağınızı gösterdi, net bir **excel wrapcols example** sundu ve **save workbook to file**'ı doğru şekilde yapmayı gösterdi. Artık dinamik dizi dönüşümleri gerektiren **create excel workbook java** projeleri için sağlam bir temele sahipsiniz.

Sonraki adımda, **using other array functions** (`TRANSPOSE`, `SEQUENCE`) gibi ilgili konuları veya Aspose.Cells akış API'sı ile **writing large data sets**'i keşfedin. Farklı kaynak dizileri, sütun sayıları ve başlangıç konumlarıyla deneyler yaparak bu deseni kendi raporlama veya veri işleme iş akışlarınıza uyarlayın. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java için Aspose.Cells kullanarak Excel Dosyası Açma: Tam Kılavuz](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [Java için Aspose.Cells ile Excel Çalışma Kitapları Oluşturma ve Birleştirme | Tam Kılavuz](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [Java için Aspose.Cells ile Excel Sayfalarını Görüntü Olarak Render Etme (Çalışma Kitabı İşlemleri)](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}