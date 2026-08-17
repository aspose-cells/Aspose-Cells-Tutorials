---
category: general
date: 2026-08-17
description: Aspose.Cells for Java ile yinelenen detay sayfaları oluşturmayı öğrenin
  ve SmartMarkerProcessor kullanarak yinelenen sayfa adlarına izin verin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: tr
lastmod: 2026-08-17
og_description: Aspose.Cells for Java'da yinelenen detay sayfaları oluşturun ve yinelenen
  sayfa adlarına izin verin. Anında sonuçlar için bu eksiksiz öğreticiyi izleyin.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Aspose.Cells for Java'da Detay Sayfalarının Kopyasını Oluşturma – Adım Adım
  Rehber
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells for Java'da yinelenen detay sayfaları nasıl oluşturulur
url: /tr/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for Java'da yinelenen detay sayfaları nasıl oluşturulur

Bir Excel çalışma kitabında **yinelenen detay sayfaları** oluşturmanız gerekiyorsa, Aspose.Cells for Java bu işlemi oldukça basitleştirir. Bu öğreticide, SmartMarkerProcessor kullanarak detay sayfaları oluştururken aynı sayfa adının birden çok kez kullanılmasına izin vermenin tam yolunu gösteriyoruz; böylece aynı adı paylaşan birden fazla sayfa içeren bir çalışma kitabı üretebilirsiniz.

Tam, çalıştırılabilir bir örnek, her yapılandırma seçeneğinin ayrıntılı açıklaması ve adlandırma çakışmaları ile büyük veri setleri gibi yaygın kenar durumlarını ele almanın ipuçları yer alıyor. Harici referanslara gerek yok—aşağıdaki kodda ihtiyacınız olan her şey mevcut.

## Önkoşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

* Java Development Kit (JDK) 8 veya daha yeni bir sürüm.
* Bağımlılıkları yönetmek için Maven veya Gradle.
* Aspose.Cells for Java kütüphanesi (sürüm 23.9 veya üzeri). `pom.xml` dosyanıza aşağıdaki Maven bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Detay verileri için bir Smart Marker bölgesi içeren bir ana şablon çalışma kitabı (`master_template.xlsx`).

## Çözümün genel görünümü

Çözüm dört mantıksal adımdan oluşur:

1. Ana şablon çalışma kitabını yükleyin.
2. `SmartMarkerProcessor`ı **yinelenen sayfa adlarına izin verecek** şekilde yapılandırın.
3. Her veri grubu için yeni bir detay sayfası oluşturacak şekilde çalışma kitabını işleyin.
4. Şimdi yinelenen detay sayfalarını içeren sonuç çalışma kitabını kaydedin.

Her adım aşağıda ayrıntılı olarak açıklanmıştır ve kılavuzun sonunda tam kaynak dosyası sağlanmıştır.

## Adım 1: Ana şablon çalışma kitabını yükleyin

İlk işlem, şablon dosyasını temsil eden bir `Workbook` örneği oluşturur. Şablon, işleyicinin veriyi nereye ekleyeceğini belirten bir Smart Marker yer tutucusu (ör. `&=DetailData`) içermelidir.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Neden önemli:** Şablonu yüklemek, düzen ve biçimlendirmeyi veri üretim mantığından ayırır; bu da kodunuzu temiz tutar ve aynı şablonu farklı veri setleri için yeniden kullanmayı kolaylaştırır.

## Adım 2: SmartMarkerProcessor'ı yinelenen sayfa adlarına izin verecek şekilde yapılandırın

Varsayılan olarak, Aspose.Cells detay sayfaları oluştururken benzersiz sayfa adları üretir. **Yinelenen sayfa adlarına izin vermek** için `DetailSheetNewName` seçeneğini sabit bir değere ayarlayın. İşleyici, oluşturulan her sayfa için bu adı yeniden kullanacaktır.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Neden önemli:** `DetailSheetNewName` ayarı, motorun her detay sayfası için aynı adı yeniden kullanmasını sağlar; bu da **yinelenen sayfa adlarına izin verme** gereksinimini doğrudan karşılar. Bu yaklaşım, sonraki araçların sayfaları adlarından ziyade konumlarıyla tanımladığı durumlarda faydalıdır.

## Adım 3: Detay sayfalarını oluşturmak için çalışma kitabını işleyin

Yapılandırmadan sonra, çalışma kitabı üzerinde `process` metodunu çağırın. İşleyici Smart Marker bölgesini okur, her veri grubu için yeni bir sayfa oluşturur ve ilgili satırları doldurur.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Neden önemli:** `process` çağrısı, Smart Marker'ların ayrıştırılması, şablon sayfasının klonlanması ve verinin eklenmesi gibi ağır işleri yapar. `DetailSheetNewName` seçeneği zaten ayarlandığı için, her yeni sayfa aynı adı alır ve sonuç dosyada yinelenen sayfa adları oluşur.

## Adım 4: Sonuç çalışma kitabını kaydedin

Son olarak, değiştirilmiş çalışma kitabını yeni bir dosyaya yazın. Çıktı dosyası, veri grupları kadar “DetailSheet” sekmesi içerecektir.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Neden önemli:** Dosyanın kaydedilmesi, işleyici tarafından yapılan değişiklikleri sonlandırır. Ortaya çıkan çalışma kitabı Microsoft Excel, LibreOffice veya XLSX formatını destekleyen herhangi bir başka tablo uygulamasında açılabilir.

## Tam kaynak kodu

Tüm parçaları bir araya getirdiğimizde, kopyalayıp yapıştırıp çalıştırabileceğiniz tam program aşağıdadır:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Beklenen çıktı

`duplicate_detail.xlsx` dosyasını açtığınızda, **DetailSheet** adlı birden çok sekme göreceksiniz. Her sekme, şablondaki belirli bir Smart Marker grubuna karşılık gelen veri setini içerir. Ana şablondan gelen düzen, biçimlendirme ve formüller her yinelenen sayfada korunur.

## Yaygın hatalarla başa çıkma

| Sorun | Açıklama | Çözüm |
|-------|----------|------|
| Excel, yinelenen sayfa adları hakkında bir uyarı gösteriyor | Excel yinelenen adlara izin verir ancak dosya açıldığında bir uyarı gösterebilir. | Uyarı zararsızdır; çalışma kitabı düzgün çalışır. Uyarıyı bastırmak isterseniz, işleme sonrası `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);` ile sayfaları yeniden adlandırabilirsiniz. |
| Büyük veri setleri yüksek bellek tüketimine neden oluyor | Her yinelenen sayfa şablonun tam bir kopyasını oluşturur, bu da RAM kullanımını artırabilir. | Şablonu yüklemeden önce `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` ile akış (streaming) modunu etkinleştirin. |
| Smart Marker bölgesi bulunamadı | İşleyici şablonda `&=DetailData` yer tutucusunu bulamıyor. | Yer tutucu sözdiziminin veri kaynağıyla eşleştiğini ve şablon sayfasının gizli olmadığını doğrulayın. |

## Pro ipucu: Yinelenen adlandırma şemasını özelleştirme

Yinelenen adlara izin verirken öngörülebilir bir adlandırma modeli istiyorsanız, temel adı bir indeksle birleştirin:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

`{0}` yer tutucusu, sayfa indeksine göre değiştirilir ve `DetailSheet_1`, `DetailSheet_2` gibi adlar üretir. Temel ad sabit kaldığı için bu hâlâ **yinelenen sayfa adlarına izin verme** gereksinimini karşılar.

## Sonraki adımlar

Artık **yinelenen detay sayfaları** oluşturabildiğinize göre aşağıdaki konuları keşfedebilirsiniz:

* **Detay sayfalarına resim ekleme** – `Picture` nesnelerini kullanarak logo veya grafik yerleştirin.
* **Koşullu biçimlendirme uygulama** – `FormatCondition` kurallarını ekleyerek değer bazlı satırları vurgulayın.
* **PDF olarak dışa aktarma** – `workbook.save("output.pdf", SaveFormat.PDF);` çağrısıyla yinelenen sayfaların PDF sürümünü oluşturun.

Bu uzantıların her biri, burada gösterilen aynı Smart Marker iş akışına dayanır ve karmaşık Excel raporlama görevlerini güvenle otomatikleştirmenizi sağlar.

---

*Aspose.Cells for Java'da yinelenen detay sayfaları oluşturmayı ve SmartMarkerProcessor ile yinelenen sayfa adlarına izin vermeyi öğrendiniz. Kodu uygulayın, şablonu uyarlayın ve tekniği raporlama hatlarınızda entegre edin.*

## Bir sonraki öğrenmeniz gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları ayrıntılı olarak ele alan örnekler içerir. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım adım kod örnekleri sunar.

- [Create & Access Excel Sheets, Add PDF Bookmarks Using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Create Access Excel Sheets Add Pdf Bookmarks Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}