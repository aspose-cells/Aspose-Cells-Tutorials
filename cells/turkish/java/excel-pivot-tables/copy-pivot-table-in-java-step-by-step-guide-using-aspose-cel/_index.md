---
category: general
date: 2026-08-04
description: Aspose.Cells for Java ile pivot tablo kopyalama. Excel aralığını nasıl
  kopyalayacağınızı, pivot tabloyu nasıl çoğaltacağınızı ve pivotlu çalışma sayfasını
  sadece birkaç satırda nasıl kopyalayacağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- copy excel range
- copy range java
- duplicate pivot table
- copy worksheet with pivot
language: tr
lastmod: 2026-08-04
og_description: Aspose.Cells for Java kullanarak pivot tablo kopyalama. Bu öğretici,
  bir Excel aralığını kopyalamanızı, bir pivot tabloyu çoğaltmanızı ve tüm verileri
  yeni bir çalışma sayfasında korumanızı adım adım gösterir.
og_image_alt: Screenshot of a Java program that copies a pivot table to a new worksheet
og_title: Java’da Pivot Tablosunu Kopyalama – Tam Aspose.Cells Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  headline: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  type: TechArticle
- description: Copy pivot table with Aspose.Cells for Java. Learn how to copy excel
    range, duplicate pivot table, and copy worksheet with pivot in just a few lines.
  name: Copy pivot table in Java – step‑by‑step guide using Aspose.Cells
  steps:
  - name: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
    text: '`CopyWithPivot.xlsx` appears in `YOUR_DIRECTORY`.'
  - name: Opening the file in Excel shows a new sheet named **CopySheet**.
    text: Opening the file in Excel shows a new sheet named **CopySheet**.
  - name: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
    text: '**CopySheet** contains a fully functional pivot table identical to the
      original, ready to refresh.'
  - name: All formatting, filters, and calculated fields are preserved.
    text: All formatting, filters, and calculated fields are preserved.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PivotTable
- Data copying
title: Java’da Pivot Tablosunu Kopyalama – Aspose.Cells Kullanarak Adım Adım Rehber
url: /tr/java/excel-pivot-tables/copy-pivot-table-in-java-step-by-step-guide-using-aspose-cel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Pivot Tablosu Kopyalama – Aspose.Cells Kullanarak Adım Adım Rehber

Java’da bir çalışma sayfasından diğerine **pivot tablo kopyalamak** istiyorsanız, bu rehber Aspose.Cells ile bunu tam olarak nasıl yapacağınızı gösterir. Raporları programlı olarak oluşturuyor ya da bir veri taşıma aracı inşa ediyor olun, pivot tablonun tanımını ve verilerini koruyan tam, çalıştırılabilir bir örnek göreceksiniz.

Pivot tablo kopyalamak sadece bir hücre aralığını kopyalamaktan daha fazlasıdır; temel önbellek ve veri kaynağı aynı kalmalıdır. Bu öğreticide ayrıca **excel aralığını kopyalama**, **pivot tablo çoğaltma** çalışma sayfaları arasında ve aynı API’yi kullanarak **pivotlu çalışma sayfasını kopyalama** konularını da ele alıyoruz.

## Önkoşullar

Başlamadan önce şunlara sahip olduğunuzdan emin olun:

* Java Development Kit (JDK) 8 veya daha yeni bir sürüm.
* Bağımlılıkları yönetmek için Maven veya Gradle.
* Aspose.Cells for Java (en son sürüm, ör. 23.12). `pom.xml` dosyanıza aşağıdaki Maven koordinatını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* İlk çalışma sayfasında bir pivot tablo içeren bir kaynak çalışma kitabı (`Source.xlsx`).

## Aspose.Cells ile Java’da Pivot Tablosu Nasıl Kopyalanır

Temel fikir, pivot tabloyu kapsayan *kaynak aralığı* kopyalamak ve ardından yeni bir çalışma sayfasına yapıştırmaktır. Aspose.Cells otomatik olarak pivot önbelleğini kopyalar, böylece ortaya çıkan sayfa tam işlevsel bir **kopya pivot tablo** içerir.

```java
import com.aspose.cells.*;

public class CopyPivotTableDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the PivotTable
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

        // Step 2: Define the source range (including the PivotTable) to be copied
        // The range must cover the entire pivot table area, e.g., A1:G20
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)                 // first worksheet
                                    .getCells()
                                    .createRange("A1:G20");

        // Step 3: Add a new worksheet that will receive the copied range
        Worksheet destinationSheet = workbook.getWorksheets().add("CopySheet");

        // Step 4: Copy the source range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // Step 5: Save the workbook with the copied PivotTable intact
        workbook.save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
    }
}
```

### Bunun Neden Çalıştığı

* **Aralık kopyalama pivot önbelleğini içerir** – Aspose.Cells bir pivot tabloyu hücre aralığına gömülü özel bir nesne olarak kabul eder. `Range.copy` çağırdığınızda kütüphane hem görünen hücreleri hem de pivotu besleyen gizli önbelleği kopyalar.
* **Manuel yeniden oluşturma gerekmez** – Pivot alanlarını veya veri kaynağını yeniden oluşturmanız gerekmez; kopya anında yenilenmeye hazırdır.
* **Her Excel sürümüyle çalışır** – Oluşturulan dosya Office Open XML (XLSX) standardını izler, bu yüzden Excel 2007+ uyarı vermeden açabilir.

## Excel aralığını kopyalama – pivot olmayan veri için aynı kodun yeniden kullanımı

Sadece **excel aralığını kopyalamanız** gerekiyorsa ve pivot tablo yoksa, aynı desen geçerlidir. Kopyalamak istediğiniz bölgeye göre aralık adresini ayarlamanız yeterlidir.

```java
// Example: copy A1:D10 from Sheet1 to Sheet2
Range dataRange = workbook.getWorksheets()
                          .get(0)
                          .getCells()
                          .createRange("A1:D10");
Worksheet sheet2 = workbook.getWorksheets().add("DataCopy");
dataRange.copy(sheet2.getCells().createRange("A1"));
```

`copy` yöntemi formülleri, biçimlendirmeyi ve yorumları korur, bu da herhangi bir Excel veri bloğu için evrensel bir çözüm sağlar.

## Pivot Tablosunu Birden Çok Çalışma Sayfasına Çoğaltma

Bazen **pivot tabloyu** birden çok kez çoğaltmanız gerekir—ör. departman başına bir. Hedef çalışma sayfaları üzerinde döngü yapın ve aynı `sourceRange.copy` çağrısını yeniden kullanın:

```java
String[] departments = {"Sales", "Marketing", "Finance"};
for (String dept : departments) {
    Worksheet ws = workbook.getWorksheets().add(dept + "Pivot");
    sourceRange.copy(ws.getCells().createRange("A1"));
}
```

Her yeni sayfa, ayrı ayrı yenilenebilen bağımsız bir pivot içerir. Önbellek çoğaltılır, böylece bir sayfadaki değişiklikler diğerlerini etkilemez.

## Pivotlu Çalışma Sayfasını Kopyalama – Sayfa Düzeyindeki Ayarları Korumak

Sayfa ayarlarını, sütun genişliklerini ve adlandırılmış aralıkları da koruyarak **pivotlu çalışma sayfasını kopyalamak** istiyorsanız, aralığı manuel olarak kopyalamak yerine `Worksheet.copy` kullanın. Bu yöntem pivot tablo dahil tüm sayfayı klonlar.

```java
Worksheet original = workbook.getWorksheets().get(0);
Worksheet clone = workbook.getWorksheets().addCopy(original);
clone.setName("FullCopy");
workbook.save("YOUR_DIRECTORY/FullCopy.xlsx");
```

`addCopy`, çalışma sayfasında pivotla birlikte taşınması gereken grafikler, görseller veya özel stiller bulunduğunda kullanışlıdır.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Sorun | Neden Olur | Çözüm |
|-------|------------|-------|
| **Kopyalama sonrası pivot önbelleği kayboldu** | `Cell.copy`'i tek tek hücrelerde (aralık yerine) kullanmak gizli önbelleği atar. | Pivot tabloyu kapsayan *tüm* aralığı, Adım 2'de gösterildiği gibi her zaman kopyalayın. |
| **Kaynak aralık çok küçük** | Aralık pivotun veri alanını içermediği için yeni sayfa sadece statik değerleri gösterir. | Adresi (ör. `A1:G20`) genişleterek tam pivot tabloyu ve varsa dilimleyicileri ya da filtreleri kapsayın. |
| **Hedef çalışma kitabı sürüm uyumsuzluğu** | XLS (eski) olarak kaydetmek modern pivot özelliklerini kaybeder. | `XLSX` (varsayılan) olarak kaydedin ya da açıkça `SaveFormat.XLSX` ayarlayın. |
| **Harici veri kaynağı bozuk** | Pivot, çalışma kitabı dışındaki bir veri kaynağına işaret eder; kopyalama bunu gömme yapmaz. | Kopyalama sonrası `PivotTable.refreshData()` kullanın veya kaynak veriyi aynı çalışma kitabına gömün. |

## Beklenen Çıktı

Programı çalıştırdıktan sonra:

1. `CopyWithPivot.xlsx` `YOUR_DIRECTORY` içinde görünür.
2. Excel'de dosyayı açtığınızda **CopySheet** adlı yeni bir sayfa gösterilir.
3. **CopySheet**, orijinaliyle aynı, tamamen işlevsel bir pivot tablo içerir ve yenilenmeye hazırdır.
4. Tüm biçimlendirme, filtreler ve hesaplanmış alanlar korunur.

`FullCopy.xlsx` dosyasını açarsanız, kaynak sayfada bulunan tüm grafikler ve görseller dahil orijinal çalışma sayfasının tam bir kopyasını göreceksiniz.

## Özet

* Aspose.Cells kullanarak Java’da **pivot tablo kopyalama** yöntemini öğrendiniz.
* Aynı yaklaşım, basit **excel aralığını kopyalama** veya **copy range java** senaryoları için de çalışır.
* Toplu işlemler için, birçok sayfada **pivot tabloyu çoğaltabilirsiniz**.
* Tüm sayfaya ihtiyacınız olduğunda, `addCopy` kullanarak **pivotlu çalışma sayfasını kopyalayabilirsiniz**.

## Sonraki Adımlar

* **PivotTable.refreshData()**'ı keşfederek kopyalama sonrası önbelleği programlı olarak güncelleyebilirsiniz.
* Kopyalama mantığını **Excel dosya akışı** ile birleştirerek büyük çalışma kitaplarını belleğe tamamen yüklemeden işleyebilirsiniz.
* Raporlarınız etkileşimli filtrelere dayanıyorsa Aspose.Cells’in **pivot dilimleyicileri** desteğine göz atın.

Kodu kendi proje yapınıza uyarlamaktan, farklı aralık boyutlarıyla denemeler yapmaktan veya daha büyük bir veri işleme hattına entegre etmekten çekinmeyin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java ile Excel Pivot Tablo Kaynağını Güncelleme: Kapsamlı Rehber](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Excel Pivot Tablo Manipülasyonu Aspose Cells Java](/cells/hongkong/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)
- [Yeni Excel Çalışma Kitabı Oluştur – Pivot Tablo Kopyala & Çoğalt](/cells/english/net/pivot-tables/create-new-excel-workbook-copy-duplicate-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}