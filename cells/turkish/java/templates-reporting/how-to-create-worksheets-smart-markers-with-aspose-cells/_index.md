---
category: general
date: 2026-08-20
description: Aspose.Cells kullanarak Java'da çalışma sayfaları için akıllı işaretçiler
  oluşturun ve SmartMarkerOptions ile detay sayfası adlandırmasını kontrol edin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create worksheets smart markers
- Aspose.Cells Java
- smart marker options
- duplicate sheet names
- detail sheet naming
language: tr
lastmod: 2026-08-20
og_description: Aspose.Cells ile Java’da çalışma sayfaları için akıllı işaretçiler
  oluşturun. SmartMarkerOptions kullanarak detay sayfalarını dinamik olarak nasıl
  adlandıracağınızı öğrenin.
og_image_alt: create worksheets smart markers example diagram
og_title: Çalışma sayfaları akıllı işaretçileri oluştur – Aspose.Cells ile Java rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  headline: How to create worksheets smart markers with Aspose.Cells
  type: TechArticle
- description: Create worksheets smart markers in Java using Aspose.Cells and control
    detail sheet naming with SmartMarkerOptions.
  name: How to create worksheets smart markers with Aspose.Cells
  steps:
  - name: Set up the Maven project and add Aspose.Cells
    text: 'Create a new Maven module (or Gradle project) and add the Aspose.Cells
      dependency:'
  - name: Load the master workbook that contains smart markers
    text: '```java import com.aspose.cells.*;'
  - name: Configure SmartMarkerOptions for custom detail sheet names
    text: '```java // Define naming pattern for detail sheets. SmartMarkerOptions
      smartMarkerOptions = new SmartMarkerOptions(); // {0} is automatically replaced
      by the row index (starting at 1). smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
      ```'
  - name: Build a DataTable that matches the smart marker fields
    text: '```java // Build a simple DataTable with two columns. DataTable data =
      new DataTable(); data.getColumns().add("Id", DataType.INTEGER); data.getColumns().add("Value",
      DataType.STRING); // Add sample rows. data.getRows().add(new Object[] { 1, "A"
      }); data.getRows().add(new Object[] { 2, "B" }); ```'
  - name: Apply the data to the smart markers with the naming options
    text: '```java // Apply the data to the first worksheet (index 0). workbook.getWorksheets().get(0).getSmartMarkers().apply(data,
      smartMarkerOptions); ```'
  - name: Save the workbook and verify the result
    text: '```java // Save the expanded workbook. workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
      } } ```'
  - name: Multiple master sheets
    text: 'If your template contains more than one master sheet, iterate over each
      sheet’s smart markers:'
  - name: Custom naming beyond the row index
    text: 'You can embed any data column into the sheet name by using placeholders
      like `{ColumnName}`:'
  - name: Preventing overly long sheet names
    text: 'Excel limits sheet names to 31 characters. If your naming pattern risks
      exceeding this limit, truncate or hash the value:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Smart Markers
- Excel Automation
title: Aspose.Cells ile çalışma sayfalarında akıllı işaretçileri nasıl oluşturulur
url: /tr/java/templates-reporting/how-to-create-worksheets-smart-markers-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile çalışma sayfalarında akıllı işaretçiler nasıl oluşturulur

Bir Java çalışma kitabında **çalışma sayfaları akıllı işaretçileri oluşturmanız** gerekiyorsa, bu rehber Aspose.Cells ile bunu nasıl yapacağınızı adım adım gösterir. `SmartMarkerOptions` nasıl yapılandırılır, böylece her detay sayfasının benzersiz ve tahmin edilebilir bir adı olur, göreceksiniz.

Master‑detail şablonunu genişleten Excel raporları oluşturmak, finans, envanter ve raporlama sistemlerinde yaygın bir gereksinimdir. Akıllı işaretçiler kullanmak, manuel sayfa çoğaltmayı ortadan kaldırır ve altyapı yerine verilere odaklanmanızı sağlar.

## Öğrenecekleriniz

* Akıllı işaretçiler içeren bir master çalışma kitabını nasıl yükleyeceğinizi.  
* `SmartMarkerOptions`'ı, oluşturulan detay sayfalarının adlandırmasını kontrol edecek şekilde nasıl ayarlayacağınızı.  
* Örnek verilerle bir `DataTable` sağlayıp bunu akıllı işaretçilere nasıl uygulayacağınızı.  
* Sonucu nasıl kaydedeceğinizi, böylece her detay çalışma sayfasının ayrı bir adı olur ve yinelenen sayfa adlarından kaçınılır.

**Önkoşullar**  
* Java 17 veya daha yeni bir sürüm (kod JDK 8+ ile de derlenir).  
* Aspose.Cells for Java 23.9 veya daha yeni – kütüphane `Workbook`, `SmartMarkerOptions` ve ilgili sınıfları sağlar.  
* IntelliJ IDEA, Eclipse veya VS Code gibi bir IDE.

Karşılaşacağınız ikincil kavramlar arasında **Aspose.Cells Java**, **smart marker options** ve şablon genişlediğinde **duplicate sheet names** (yinelenen sayfa adları) yönetimi bulunur.

## Çalışma sayfalarında akıllı işaretçiler oluşturma – adım adım kılavuz

Aşağıdaki bölümler süreci ayrı, yeniden kullanılabilir adımlara ayırır. Her adım bir kod parçacığı, neden önemli olduğuna dair bir açıklama ve yaygın hatalardan kaçınmak için pratik ipuçları içerir.

### Adım 1: Maven projesini kurun ve Aspose.Cells'i ekleyin

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

**Bu adımın önemi** – Kütüphane, Excel dosyalarını okuyan ve yazan `Workbook` sınıfını ve şablonunuzu otomatik olarak genişleten smart‑marker motorunu sağlar. Doğru bağımlılık olmadan, derleyici daha sonra kullanılan API çağrılarını çözemez.

> **Pro tip:** Kurumsal bir proxy arkasında çalışıyorsanız, Maven'in `settings.xml` dosyasını Aspose deposunu güvenli bir şekilde çekmek için yapılandırın.

### Adım 2: Akıllı işaretçiler içeren master çalışma kitabını yükleyin

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // Load the template that holds the smart marker tags.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");
```

**Bu adımın önemi** – Master çalışma kitabı, motorun değiştireceği düzeni, formülleri ve yer tutucu etiketleri (`«SmartMarker»`) tanımlar. Dosyayı bir kez yüklemek bellek kullanımını düşük tutar ve aynı çalışma kitabını birden fazla veri seti için yeniden kullanmanıza olanak tanır.

### Adım 3: Özel detay sayfa adları için SmartMarkerOptions'ı yapılandırın

```java
        // Define naming pattern for detail sheets.
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is automatically replaced by the row index (starting at 1).
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");
```

**Bu adımın önemi** – Varsayılan olarak Aspose.Cells, “DetailSheet” gibi genel adlarla detay sayfaları oluşturur. Şablon birçok satır için genişlediğinde bu adlar çakışır ve **duplicate sheet names** (yinelenen sayfa adları) ve bir çalışma zamanı istisnasına yol açar. `"DetailSheet_{0}"` deseni, satır başına benzersiz bir ad garantileyerek çoğaltma sorununu çözer.

### Adım 4: Akıllı işaretçi alanlarıyla eşleşen bir DataTable oluşturun

```java
        // Build a simple DataTable with two columns.
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        // Add sample rows.
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });
```

**Bu adımın önemi** – `DataTable`, akıllı işaretçi yer tutucularını değiştiren gerçek değerleri sağlar. Sütun adları şablondaki işaretçi adlarıyla eşleşmelidir; aksi takdirde motor değişikliği sessizce atlar.

> **Common mistake:** Büyük/küçük harf farkı olan bir sütun adı kullanmak (ör. “id” vs “Id”) oluşturulan sayfalarda veri eksikliğine yol açar.

### Adım 5: Veriyi adlandırma seçenekleriyle akıllı işaretçilere uygulayın

```java
        // Apply the data to the first worksheet (index 0).
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);
```

**Bu adımın önemi** – `apply` metodu, akıllı işaretçi motorunu tetikler. Her satırı okur, `SmartMarkerOptions`'tan gelen adlandırma desenini kullanarak yeni bir detay sayfası oluşturur ve sayfayı satırın verileriyle doldurur. Bu tek çağrı, manuel sayfa kopyalama ve hücre doldurma işlemlerinin onlarca satırını değiştirir.

### Adım 6: Çalışma kitabını kaydedin ve sonucu doğrulayın

```java
        // Save the expanded workbook.
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

Çalıştırdıktan sonra `MasterDetailDuplicatedNames.xlsx` dosyasını açın. Şunları görmelisiniz:

* Orijinal master sayfa değişmemiş.  
* `DetailSheet_1` ve `DetailSheet_2` adında iki yeni çalışma sayfası.  
* Her detay sayfası, `DataTable`'ın ilgili satırındaki değerleri içerir.

**Bu adımın önemi** – Çalışma kitabını kalıcı hale getirmek, akıllı işaretçi genişlemesini tamamlar. Dosya artık alt sistemlere gönderilebilir, e-postalara eklenebilir veya daha fazla analiz için Excel'de açılabilir.

## Kenar durumları ve varyasyonların ele alınması

### Birden fazla master sayfa

Şablonunuz birden fazla master sayfa içeriyorsa, her sayfanın akıllı işaretçileri üzerinde döngü yapın:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.getWorksheets().get(i).getSmartMarkers().apply(data, smartMarkerOptions);
}
```

### Satır indeksinin ötesinde özel adlandırma

Herhangi bir veri sütununu `{ColumnName}` gibi yer tutucularla sayfa adına gömebilirsiniz:

```java
smartMarkerOptions.setDetailSheetNewName("Order_{OrderId}");
```

Sağlanan `DataTable` içinde `OrderId` sütununun mevcut olduğundan emin olun.

### Çok uzun sayfa adlarını önleme

Excel, sayfa adlarını 31 karakterle sınırlar. Adlandırma deseniniz bu sınırı aşma riski taşıyorsa, değeri kırpın veya hash'leyin:

```java
String pattern = "Detail_{0}_{1}";
smartMarkerOptions.setDetailSheetNewName(pattern);
```

Ardından, oluşturulan adı Aspose'e geçirmeden önce `StringUtils.abbreviate` ile son işleme tabi tutun.

## Tam çalıştırılabilir örnek

Aşağıda, doğrudan kopyalayıp dosya yollarını ayarlayarak çalıştırabileceğiniz tam kaynak dosya bulunmaktadır:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheetNames {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the master workbook that contains smart markers
        Workbook workbook = new Workbook("YOUR_DIRECTORY/MasterDetailTemplate.xlsx");

        // 2️⃣ Define how detail sheets will be named when they are created
        SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions();
        // {0} is replaced by the row index (starting at 1)
        smartMarkerOptions.setDetailSheetNewName("DetailSheet_{0}");

        // 3️⃣ Prepare sample data to populate the smart markers
        DataTable data = new DataTable();
        data.getColumns().add("Id", DataType.INTEGER);
        data.getColumns().add("Value", DataType.STRING);
        data.getRows().add(new Object[] { 1, "A" });
        data.getRows().add(new Object[] { 2, "B" });

        // 4️⃣ Apply the data to the smart markers using the naming options
        workbook.getWorksheets().get(0).getSmartMarkers().apply(data, smartMarkerOptions);

        // 5️⃣ Save the workbook – each detail sheet now has a unique name
        workbook.save("YOUR_DIRECTORY/MasterDetailDuplicatedNames.xlsx");
    }
}
```

**Beklenen çıktı**

* `MasterDetailDuplicatedNames.xlsx` şunları içerir:

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells Java'yı Ustalaştırma: Çalışma Sayfalarında Dinamik Veri İçin Akıllı İşaretçileri Kullanma](/cells/english/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)
- [Aspose.Cells for Java'da Akıllı İşaretçilerle Dinamik Grafikler Oluşturma | Adım Adım Kılavuz](/cells/english/java/charts-graphs/dynamic-charts-smart-markers-aspose-cells-java/)
- [Aspose Cells Java Akıllı İşaretçiler Çalışma Sayfaları](/cells/german/java/worksheet-management/aspose-cells-java-smart-markers-worksheets/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}