---
category: general
date: 2026-03-01
description: Java’da pivot tablosunu koruyarak kopyalama, ardından Excel’i PPTX’e
  dışa aktarma, Excel Otomatik Filtreyi devre dışı bırakma ve JSON dizileri için Akıllı
  İşaretleyici kullanma – tam adım adım rehber.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: tr
og_description: Java'da pivot tabloyu kopyala, pivot tanımını koru, PPTX'e dışa aktar,
  AutoFilter'ı devre dışı bırak ve Smart Marker'ı kullan – geliştiriciler için tam
  rehber.
og_title: Java’da Pivot Tablosunu Kopyala – Koruyun, PPTX’e Aktarın
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Java’da Pivot Tablosunu Kopyala – Koruyun, PPTX’e Aktarın
url: /tr/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Pivot Tablosunu Kopyala – Koruyun, PPTX’e Dışa Aktarın

Hiç bir çalışma kitabından diğerine **pivot tabloyu kopyalamak** zorunda kaldınız mı ve alttaki pivot tanımını kaybetmeden? Bu konuda yalnız değilsiniz. Gerçek dünyadaki birçok projede verileri taşımanız gerekir ve en son istediğiniz, çalışma zamanında hata veren kırık bir pivot olur.  

Bu öğreticide, sadece **pivot tabloyu kopyalamak** değil, aynı zamanda kopyalama sırasında **pivot tabloyu korumak**, **Excel’i PPTX’e dışa aktarmak**, **Excel AutoFilter’ı devre dışı bırakmak** ve **smart marker** kullanarak bir JSON dizisini tek bir hücreye yerleştirmek için eksiksiz bir çözüm üzerinden geçeceğiz. Sonunda, dört senaryoyu da kapsayan tek bir çalıştırılabilir Java programına sahip olacaksınız.

## Önkoşullar

- Java 8 ve üzeri (kod Java 11 ile de çalışır)  
- Aspose.Cells for Java kütüphanesi (versiyon 23.9 veya üzeri) – Maven Central’dan edinebilirsiniz  
- Pivot tablolar, tablolar ve metin kutuları gibi Excel kavramlarına temel aşinalık  

Eğer Aspose.Cells JAR dosyanız yoksa, `pom.xml` dosyanıza şunu ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Şimdi, başlayalım.

## Adım 1: Pivot Tablosunu Kopyala – Pivot Tanımını Korumak

Bir pivot tablosunu barındıran hücre aralığını sadece kopyaladığınızda, pivot meta verileri genellikle geride kalır. Aspose.Cells, `copyRange` metodunu bir `CopyOptions` örneğiyle kullanarak tanımı bozulmadan tutmamıza olanak tanır.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Neden bu çalışır:** `CopyOptions`, Aspose.Cells’e pivot önbelleği ve alan ayarları dahil her şeyi taşımayı söyler. Bu olmadan, sadece düz değerler elde eder ve pivotu yenileme yeteneğini kaybedersiniz.

**Köşe durum:** Kaynak pivotunuz sabit kodlanmış `A1:G20` aralığından daha genişse, aralığı buna göre ayarlayın veya dinamik olarak almak için `sourceSheet.getPivotTables().get(0).getDataRange()` kullanın.

![Pivot tablo kopyalama örneği](image.png "Java’da pivot tablo kopyalama")

*Görsel alt metni: Java’da pivot tablo diagramı*

## Adım 2: Düzenlenebilir Metin Kutulu Çalışma Sayfasını PPTX’e Dışa Aktar

Çoğu zaman bir Excel sayfasını PowerPoint slaytına dönüştürmeniz gerekir—örneğin sunulması gereken haftalık panolar. Aspose.Cells, metin kutuları gibi şekilleri koruyarak bir çalışma sayfasını doğrudan PPTX dosyası olarak kaydedebilir.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Ne oluyor:** `SaveFormat.PPTX` ile `save` yöntemi, tüm sayfayı, içinde bulunan düzenlenebilir TextBox dahil, bir PowerPoint slaytına dönüştürür. PPTX’i PowerPoint’te açtığınızda kutu içindeki metin düzenlenebilir kalır.

**İpucu:** Birden fazla sayfanız varsa ve sadece belirli birini istiyorsanız, kaydetmeden önce diğerleri için `wb.getWorksheets().removeAt(index)` metodunu çağırın.

## Adım 3: Bir Tablodan Excel AutoFilter’ı Devre Dışı Bırak

AutoFilter son kullanıcılar için kullanışlıdır, ancak bazen programatik olarak kapatmanız gerekir—belki verileri dışa aktarmadan önce ya da temiz bir rapor oluştururken. İşte bir Excel tablosunda **excel autofilter’ı devre dışı bırakma** yöntemi.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Bunun neden gerekli olabileceği:** AutoFilter’ı desteklemeyen formatlara (CSV veya PDF gibi) dışa aktarmak, rastgele filtre simgelerinin görünmesine neden olabilir. Devre dışı bırakmak temiz bir çıktı sağlar.

**Yaygın tuzak:** Sayfada tablo yoksa, `getTables().get(0)` bir `IndexOutOfBoundsException` fırlatır. Üretim kodunda her zaman önce `sheet.getTables().size()` kontrol edin.

## Adım 4: Smart Marker Kullan – JSON Dizisini Tek Hücre Değeri Olarak Ekle

Smart Marker, Aspose’un şablon motorudur. Kullanışlı bir yöntem, tüm bir JSON dizisini tek bir hücre değeri olarak ele almaktır; bu, günlükleme veya yapılandırılmış veriyi aşağı akışa geçirmek için mükemmeldir. Bunu başarmak için **smart marker** kullanalım.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Nasıl çalışır:** Çalışma kitabındaki `${json}` işareti, `ArrayAsSingle` ayarını yaptığımız için tüm JSON dizesiyle değiştirilir. Bu seçenek olmadan, Aspose her dizi öğesini ayrı satırlara genişletmeye çalışır.

**Varyasyon:** Diziyi satırlara bölmeniz gerekiyorsa, sadece `ArrayAsSingle` seçeneğini kaldırın ve Smart Marker’ın otomatik genişletmesine izin verin.

## Tam Çalışan Örnek – Tüm Adımlar Birleştirildi

Aşağıda, ele aldığımız tüm işlemleri bir araya getiren tek bir Java sınıfı bulunmaktadır. Bunu normal bir `main` metodu olarak çalıştırın; sadece dosya yollarını ortamınıza göre ayarlayın.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}