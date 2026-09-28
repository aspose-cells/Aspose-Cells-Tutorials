---
category: general
date: 2026-09-27
description: Java ile Excel şablonunu doldururken ve veriden sayfalar oluştururken,
  dinamik sayfa adları oluşturmayı öğrenin ve güçlü raporlamalar yapın.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- dynamic sheet names
- generate multiple sheets
- create sheets from data
- populate excel template java
language: tr
lastmod: 2026-09-27
og_description: Dinamik sayfa adları, bir veri kümesinden birden fazla sayfa oluşturmanıza
  olanak tanır. Bu öğreticide, Java'da bir Excel şablonunu nasıl dolduracağınız ve
  Aspose.Cells kullanarak verilerden sayfalar oluşturacağınız gösterilmektedir.
og_image_alt: Screenshot showing an Excel workbook with dynamically generated sheet
  names using Java
og_title: Java ile Excel'de dinamik sayfa adları oluşturun
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  headline: How to generate dynamic sheet names in Excel with Java
  type: TechArticle
- description: Learn how to generate dynamic sheet names in Excel with Java while
    you populate an Excel template and create sheets from data for robust reporting.
  name: How to generate dynamic sheet names in Excel with Java
  steps:
  - name: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
    text: Add the Aspose.Cells for Java JAR to your project’s classpath (available
      from Maven Central or the Aspose website).
  - name: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
    text: Place `MasterDetailTemplate.xlsx` in `templates/` relative to the project
      root.
  - name: Execute the `main` method. The `output/` folder will contain the generated
      file.
    text: Execute the `main` method. The `output/` folder will contain the generated
      file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java ile Excel'de dinamik sayfa adları nasıl oluşturulur
url: /tr/java/worksheet-management/how-to-generate-dynamic-sheet-names-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Java ile dinamik sayfa adları nasıl oluşturulur

Java'da bir Excel şablonunu doldururken **dinamik sayfa adlarına** ihtiyacınız varsa, bu rehber sizi sürecin tamamı boyunca yönlendirecek. Veriler koleksiyonundan *birden fazla sayfa oluşturmayı* göreceksiniz ve her sayfanın otomatik olarak benzersiz bir ad almasını sağlayacaksınız. Sonunda, verilerden sayfalar oluşturan ve sonucu istediğiniz adlandırma kuralı ile kaydeden çalıştırılabilir bir örnek elde edeceksiniz.

Sayfaları anlık olarak oluşturmak, raporlama panoları, fatura partileri veya detay bölümlerinin sayısının önceden bilinmediği herhangi bir senaryo için yaygın bir gereksinimdir. Aspose.Cells Smart Marker motoru bu görevi öz ve güvenilir kılar ve aşağıdaki kod önerilen yaklaşımı gösterir.

## Aspose.Cells ile dinamik sayfa adları kullanma

Aspose.Cells for Java, bir şablon çalışma kitabındaki yer tutucuları okuyabilen ve bunları satır, sütun ya da yeni çalışma sayfalarına genişletebilen bir **Smart Marker** işlemcisi sağlar. `SmartMarkerOptions.DetailSheetNewName` yapılandırılarak her oluşturulan sayfanın adı kontrol edilir. `{0}` yer tutucusu, mevcut veri satırının sıfır‑tabanlı indeksine göre değiştirilir ve size `Detail_0`, `Detail_1`, …​ gibi tamamen **dinamik sayfa adları** sağlar.

> **Pro ipucu:** Şablon çalışma kitabını özel bir kaynak klasöründe tutun ve mümkün olduğunda göreli bir yol kullanın. Bu, farklı ortamlar üzerinde kırılmaya neden olan mutlak yolların sabit kodlanmasını önler.

## Adım 1: Excel şablonunu yükleyin (populate excel template java)

İlk olarak, Smart Marker etiketlerini içeren çalışma kitabını yükleyin. Şablonda, örneğin `Detail` adlı bir sayfa ve işlemcinin satır eklemeye nereden başlayacağını belirten `&=Orders!A1` gibi bir işaretçi bulunmalıdır.

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // Load the template workbook that already contains Smart Markers.
        // Replace "templates/MasterDetailTemplate.xlsx" with the actual path.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");
```

*Neden bu adım önemlidir:* Şablon, her oluşturulan sayfaya kopyalanacak düzeni (başlıklar, formüller, biçimlendirme) tanımlar. Uygun bir şablon olmadan, çıktı stil ve formüllerini kaybeder.

## Adım 2: Verilerden sayfalar oluşturmak için veri kaynağını hazırlayın

Sonra, Smart Marker işlemcisinin üzerinde dönebileceği bir veri kaynağı oluşturun. Bu örnekte, anahtar `"Orders"` şablondaki işaretçi adıyla eşleşen bir `Map<String, Object>` kullanıyoruz.

```java
        // Prepare a data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();

        // Each element of the Object[] array represents one row.
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });
```

*Neden bu adım önemlidir:* Smart Marker motoru diziyi okur, her iç `Object[]` için bir satır oluşturur ve—yeni sayfalar oluşturmasını istediğimiz için—her satır için ayrı bir çalışma sayfası yaratır. Bu, **verilerden sayfalar oluşturma** işleminin özüdür.

## Adım 3: SmartMarkerOptions'ı benzersiz adlarla birden çok sayfa oluşturacak şekilde yapılandırın

Şimdi Aspose.Cells'e her yeni çalışma sayfasının nasıl adlandırılacağını söyleyin. `{0}` yer tutucusu, mevcut satır indeksiyle değiştirilir.

```java
        // Configure options so every generated sheet gets a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} → row index (0‑based). Resulting names: Detail_0, Detail_1, …
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");
```

*Neden bu adım önemlidir:* `DetailSheetNewName` ayarlanmazsa, işlemci her satır için orijinal sayfa adını yeniden kullanır ve verileri üzerine yazar. Bu seçenek **dinamik sayfa adlarını** etkinleştirir.

## Adım 4: SmartMarker'ları işleyin ve çalışma kitabını oluşturun

İşlemciyi veri kaynağı ve az önce yapılandırdığımız seçeneklerle çalıştırın.

```java
        // Execute the Smart Marker processor.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);
```

*Neden bu adım önemlidir:* İşlemci işaretçileri genişletir, gerekli sayıda çalışma sayfası oluşturur, şablon düzenini kopyalar ve her sayfayı ilgili satır verileriyle doldurur.

## Adım 5: Sonucu kaydedin ve doğrulayın

Son olarak, çalışma kitabını diske yazın. Excel'de dosyayı açarak otomatik oluşturulan sayfaları görün.

```java
        // Save the workbook containing the newly generated sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

**Beklenen çıktı**

`MasterDetailResult.xlsx` dosyasını açtığınızda üç yeni çalışma sayfası görmelisiniz:

* `Detail_0` – sipariş 101 (Alice, 250.00) içerir  
* `Detail_1` – sipariş 102 (Bob, 175.50) içerir  
* `Detail_2` – sipariş 103 (Carol, 320.75) içerir

Her sayfa, orijinal `Detail` şablon sayfasında bulunan biçimlendirmeyi, sütun genişliklerini ve tüm formülleri korur.

## Tam çalıştırılabilir örnek

Tüm bölümleri bir araya getirerek derleyip çalıştırabileceğiniz bağımsız bir program elde edersiniz:

```java
import com.aspose.cells.*;

public class DynamicSheetNamesExample {

    public static void main(String[] args) throws Exception {
        // 1. Load the template workbook that contains Smart Markers.
        Workbook templateWorkbook = new Workbook("templates/MasterDetailTemplate.xlsx");

        // 2. Prepare the data source with multiple detail rows.
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        dataSource.put("Orders", new Object[] {
            new Object[] { 101, "Alice", 250.00 },
            new Object[] { 102, "Bob",   175.50 },
            new Object[] { 103, "Carol", 320.75 }
        });

        // 3. Configure SmartMarkerOptions to give each generated sheet a unique name.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.setDetailSheetNewName("Detail_{0}");

        // 4. Process the Smart Markers using the data source and the configured options.
        templateWorkbook.getSmartMarkerProcessor().process(dataSource, smartMarkerOptions);

        // 5. Save the resulting workbook with the newly created sheets.
        templateWorkbook.save("output/MasterDetailResult.xlsx");
    }
}
```

### Nasıl çalıştırılır

1. Aspose.Cells for Java JAR'ını projenizin sınıf yoluna ekleyin (Maven Central veya Aspose web sitesinden temin edilebilir).  
2. `MasterDetailTemplate.xlsx` dosyasını proje köküne göre `templates/` klasörüne yerleştirin.  
3. `main` metodunu çalıştırın. `output/` klasörü oluşturulan dosyayı içerecektir.

## Yaygın varyasyonlar ve uç durumlar

| Durum | Ne değiştirilmeli |
|-----------|----------------|
| **Farklı adlandırma deseni** | `"OrderSheet_{0}_v{1}"` kullanın ve ikinci bir indeks (örneğin sayfa numarası) için `{1}` gibi ek yer tutucular ekleyin. |
| **Büyük veri setleri** | Yüzlerce sayfa oluştururken `OutOfMemoryError` hatasından kaçınmak için JVM yığın belleğini (`-Xmx2g`) artırın. |
| **Koşullu sayfa oluşturma** | `process` çağrısı öncesinde veri dizisini filtreleyerek kriteri karşılamayan satırları dışarı bırakın, böylece gereksiz sayfalar oluşmaz. |
| **Diğer sayfalara referans veren formüllerin korunması** | Orijinal sayfa adını gizli bir yer tutucu olarak tutun (ör. `DetailTemplate`) ve `SmartMarkerOptions.setDetailSheetNewName` yalnızca görünür ad için kullanın; gizli adı referans alan formüller hâlâ doğru şekilde çözülecektir. |

## Sağlam Excel otomasyonu için ipuçları

* **Veri kaynağını doğrulayın** – Her iç dizinin, şablonda tanımlanan sütun sayısıyla aynı sayıda öğeye sahip olduğundan emin olun; uyumsuz uzunluklar çalışma zamanı hatalarına neden olur.  
* **Şablonda adlandırılmış aralıklar kullanın** – Smart Marker sözdizimini daha net hâle getirmek için (`&=Orders!A1`).  
* **Kaynakları kapatın** – Aspose.Cells akışları dahili olarak yönetse de, bir `finally` bloğunda `templateWorkbook.dispose()` çağırmak yerel belleği daha hızlı serbest bırakabilir.  
* **Köşe değerlerle test edin** – Sıfır satır, yalnızca orijinal şablon sayfasını içeren bir çalışma kitabı üretmelidir; boş bir veri kaynağı kodunuzun “veri yok” durumunu sorunsuz ele aldığını doğrular.

## Sonuç

Artık Java kullanarak Excel'de **dinamik sayfa adları oluşturmayı**, **Excel şablonunu doldurmayı** ve **verilerden sayfalar yaratmayı**, ayrıca Aspose.Cells Smart Marker'lar ile **otomatik olarak birden çok sayfa oluşturmayı** biliyorsunuz. Yukarıdaki adımları izleyerek bu deseni, onlarca detay sayfasına, özel adlandırma kurallarına veya koşullu sayfa oluşturma ihtiyacına sahip herhangi bir raporlama senaryosuna uyarlayabilirsiniz.

Bu çözümü genişletmeye hazır mısınız? Her oluşturulan sayfaya grafik eklemeyi deneyin veya çalışma kitabını `Workbook.save("result.pdf", SaveFormat.PDF)` kullanarak PDF olarak dışa aktarın. Her iki teknik de az önce öğrendiğiniz aynı dinamik‑sayfa temeline dayanır. Kodlamanın tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Java ile Aspose.Cells ile Dinamik Excel Sayfalarını Ustalaştırın: Kapsamlı Rehber](/cells/english/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dinamik Excel Sayfaları Aspose Cells Java Rehberi](/cells/german/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)
- [Dinamik Excel Sayfaları Aspose Cells Java Rehberi](/cells/french/java/formulas-functions/dynamic-excel-sheets-aspose-cells-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}