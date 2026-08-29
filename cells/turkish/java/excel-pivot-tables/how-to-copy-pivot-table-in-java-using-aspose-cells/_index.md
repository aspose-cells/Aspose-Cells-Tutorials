---
category: general
date: 2026-07-06
description: Java'da Aspose.Cells ile pivot tablo nasıl kopyalanır – Excel pivot tablolarını
  programlı olarak çoğaltmak için adım adım rehber.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot
- duplicate excel pivot
language: tr
lastmod: 2026-07-06
og_description: Aspose.Cells kullanarak Java’da pivot tablo kopyalama, Excel pivot
  tablolarını hızlı ve güvenilir bir şekilde çoğaltmanızı sağlar.
og_image_alt: Screenshot of Java code copying an Excel pivot table with Aspose.Cells
og_title: Java'da Pivot Tablosunu Nasıl Kopyalarsınız – Tam Aspose.Cells Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
    to duplicate Excel pivot tables programmatically.
  headline: How to copy pivot table in Java using Aspose.Cells
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Pivot Table
title: Aspose.Cells kullanarak Java'da pivot tablo nasıl kopyalanır
url: /tr/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Aspose.Cells Kullanarak Pivot Tablosunu Kopyalama

Excel dosyası içinde çalışma kitabını manuel olarak açmadan **pivot tablolarını nasıl kopyalayacağınızı** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok raporlama sürecinde **Excel pivot** tablolarını anında çoğaltmanız gerekir—belki bir anlık görüntü oluşturmak, yeni bir sayfaya taşımak veya sonraki kullanıcılar için bir şablon üretmek amacıyla.

Bu öğreticide, tam olarak bunu gösteren eksiksiz ve çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Aspose.Cells for Java kütüphanesini kullanarak bir çalışma kitabını yükleyecek, kaynak pivot aralığını bulacak, yeni bir konuma kopyalayacak ve sonucu kaydedeceğiz. Belirsiz referanslar yok, sadece projenize hemen ekleyebileceğiniz somut bir çözüm.

---

## Önkoşullar

* **Java Development Kit (JDK) 8+** – kod, herhangi bir yeni JDK ile derlenir.
* **Aspose.Cells for Java** sürüm 25.11 veya daha yeni – pivot tablolarını destekleyen `Range.copy` yöntemi bu sürümde tanıtıldı.
* İçinde zaten bir pivot tablo bulunan bir **input.xlsx** dosyası (test için Excel'de bir tane oluşturabilirsiniz).
* Tercih ettiğiniz bir derleme aracı (Maven, Gradle veya düz `javac`). Hızlı başlangıç için Maven bağımlılığını göstereceğiz.

```xml
<!-- Add this to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.12</version> <!-- Use the latest stable -->
</dependency>
```

---

## Adım 1: Kaynak Çalışma Kitabını Yükleme

İlk olarak, orijinal pivot tablosunu içeren Excel dosyasını açıyoruz. Aspose.Cells, çalışma kitabını bellek içi bir nesne olarak ele alır, böylece Excel'i başlatmadan üzerinde işlem yapabilirsiniz.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

> **Neden önemli:** Çalışma kitabını yüklemek, çalışma sayfalarına, hücrelere ve özellikle pivot tablosunun arkasındaki pivot önbelleğine erişim sağlar. Bu adım olmadan kütüphanenin kopyalayacak bir şeyi olmaz.

---

## Adım 2: Pivotun Bulunduğu Çalışma Sayfasını Almak

Çalışma kitabınızda birden fazla sayfa varsa, doğru olanı işaretlemeniz gerekir. Burada sadece ilk sayfayı alıyoruz, ancak adlandırılmış bir arama için `get("SheetName")` de kullanabilirsiniz.

```java
// Obtain the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

> **Pro ipucu:** Çok sayıda sayfa ile çalışırken, sayıların sabit kodlanmasını önlemek için indeks veya adı bir yapılandırma dosyasında önbelleğe alın.

---

## Adım 3: Pivot Tablosunu İçeren Kaynak Aralığı Tanımlama

25.11 sürümünden itibaren Aspose.Cells, bir pivot tablosunu normal bir hücre aralığı gibi ele almanıza izin verir. Tüm pivotu kapsayan sol‑üst ve sağ‑alt hücreleri belirtin.

```java
// The range A1:D20 covers the whole pivot table in this example
Range sourceRange = worksheet.getCells().createRange("A1:D20");
```

> **Köşe durum:** Pivotunuz dinamik olarak genişliyorsa (ör. daha sonra satırlar ekleniyorsa), tam aralığı programlı olarak almak için `worksheet.getPivotTables().get(0).getDataRange()` kullanmayı düşünün.

---

## Adım 4: Pivotun Kopyalanacağı Hedef Aralığı Tanımlama

Kopyalanan pivotun görünmesini istediğiniz herhangi bir boş hücreyi seçin. Bu demoda **F1**'den başlıyoruz, böylece orijinal ve kopya arasında bir boşluk bırakıyoruz.

```java
// Destination starts at cell F1 – adjust as needed
Range destinationRange = worksheet.getCells().createRange("F1");
```

> **Neden yeni bir sayfa?** Ayrıca yeni bir çalışma sayfası oluşturabilirsiniz (`workbook.getWorksheets().add("Copy")`) ve hücrelerini hedef olarak kullanabilirsiniz. Aynı `copy` yöntemi sayfalar arasında da çalışır.

---

## Adım 5: Pivot Tablosunu Yeni Konuma Kopyalama

Şimdi sihir gerçekleşir. `copy` yöntemi pivotu, önbelleğini, biçimlendirmesini ve hatta ilişkili dilimleyicileri (en son sürümde) bile kopyalar.

```java
// Perform the copy – the pivot is now duplicated at the destination
sourceRange.copy(destinationRange);
```

> **Önemli:** Kopyalama işlemi *derin* bir işlemdir; orijinal pivota bir referans **oluşturmaz**. Yeni pivotu, kaynağı etkilemeden bağımsız olarak değiştirebilirsiniz.

---

## Adım 6: Kopyalanmış Pivotla Çalışma Kitabını Kaydetme

Son olarak, değiştirilmiş çalışma kitabını diske yazın. Orijinali üzerine yazabilir veya yeni bir dosya oluşturabilirsiniz; burada kaynağı dokunulmaz tutmak için ikincisini seçiyoruz.

```java
// Save the workbook – the duplicated pivot lives in output.xlsx
workbook.save("YOUR_DIRECTORY/output.xlsx");
```

**output.xlsx** dosyasını Excel'de açtığınızda, orijinal pivotun A‑D sütunlarında ve F sütununda başlayan mükemmel bir kopyasını göreceksiniz. Her iki pivot da ayrı ayrı yenilenebilir.

---

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, doğrudan derleyip çalıştırabileceğiniz eksiksiz Java sınıfı burada:

```java
import com.aspose.cells.*;

public class ExportPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Get the worksheet that contains the pivot table
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Define the source range that includes the pivot table (supported from version 25.11)
        // Adjust the range to match your actual pivot dimensions
        Range sourceRange = worksheet.getCells().createRange("A1:D20");

        // Step 4: Define the destination range where the pivot table will be copied
        // Change "F1" to any starting cell you prefer
        Range destinationRange = worksheet.getCells().createRange("F1");

        // Step 5: Copy the pivot table to the new location
        sourceRange.copy(destinationRange);

        // Step 6: Save the workbook with the copied pivot table
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

**Beklenen sonuç:** `output.xlsx` dosyasını açtığınızda orijinal pivot (A1:D20) ve F1'den başlayan aynı pivot gösterilir. Her iki tablo da filtrelerini, stillerini ve hesaplanmış alanlarını korur.

---

## Yaygın Varyasyonları Ele Alma

| Durum | Ne Ayarlanmalı |
|-----------|----------------|
| **Aynı sayfada birden fazla pivot** | `worksheet.getPivotTables()` üzerinden döngü yapın ve her birini kendi hedef aralığıyla kopyalayın. |
| **Dinamik veri aralığı** | Kaynak alanı otomatik algılamak için `worksheet.getPivotTables().get(0).getDataRange()` kullanın. |
| **Başka bir çalışma kitabına kopyalama** | İkinci bir `Workbook` örneği yükleyin, hedef çalışma sayfası oluşturun ve ardından `sourceRange.copy(destWorksheet.getCells().createRange("A1"))` çağrısını yapın. |
| **Dilimleyicileri koruma** | 25.12 sürümünden itibaren, aralık dilimleyicileri içeriyorsa otomatik olarak kopyalanır. Kaydettikten sonra Excel'de doğrulayın. |

---

## Pro İpuçları ve Tuzaklar

* **Sürüm kontrolü:** Pivotları destekleyen `copy` yöntemi **Aspose.Cells 25.11**'de eklendi. Daha eski bir sürüm kullanıyorsanız bir istisna alırsınız. `pom.xml` dosyanızda `aspose-cells` sürümünü her zaman doğrulayın.
* **Performans:** Büyük pivotların kopyalanması bellek yoğun olabilir. Sadece verilere ihtiyacınız varsa, tüm nesneyi klonlamak yerine pivotu düz bir tabloya dışa aktarmayı düşünün.
* **Yenileme davranışı:** Kopyalanan pivot kendi önbelleğini korur. Alt verileri değiştirirseniz, yeni pivotu yeniden hesaplamak için `pivotTable.refresh()` çağırın.
* **Biçimlendirme tuhaflıkları:** Bazı özel sayı formatları çok eski Excel sürümlerinde (<2007) kopyalama sonrasında korunmayabilir. Hedef kitlenizin Excel sürümüyle test edin.

---

## Sonuç

Artık Aspose.Cells for Java kullanarak **pivot tablolarını nasıl kopyalayacağınıza** dair sağlam, uçtan uca bir cevaba sahipsiniz ve birkaç satır kodla **Excel pivot** tablolarını nasıl çoğaltacağınızı gördünüz. Yaklaşım tek veya birden fazla pivot için, çalışma sayfaları arasında ve hatta çalışma kitapları arasında da çalışır.

Sonraki adımlar şunları içerebilir:

* Toplu işte her pivot için kopyalamayı otomatikleştirmek.
* Kopyalanan pivotun adını değiştirecek kod eklemek (ör. `pivotTable.setName("Copy_of_Sales")`).
* Rutin'i PDF veya CSV dışa aktarımları üreten daha büyük bir raporlama servisine entegre etmek.

Deneyin, aralıkları gerçek verilerinize göre ayarlayın ve kütüphanenin zor işleri halletmesine izin verin. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren eksiksiz çalışan kod örnekleri sunar.

- [Java için Aspose.Cells Kullanarak Excel'de Pivot Tabloları Oluşturma: Kapsamlı Rehber](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells Java ile Excel Pivot Tablosu Manipülasyonu: Kapsamlı Rehber](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Java için Aspose.Cells ile Excel Pivot Tablosu Kaynağını Güncelleme: Kapsamlı Rehber](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}