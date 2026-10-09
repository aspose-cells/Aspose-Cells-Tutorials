---
category: general
date: 2026-06-21
description: Java kullanarak Excel'de birden fazla sayfa oluşturun. Verileri sayfalara
  nasıl dışa aktaracağınızı, şablon tabanlı Excel yaklaşımını nasıl kullanacağınızı
  öğrenin ve çalışma kitabını xlsx formatında verimli bir şekilde kaydedin.
draft: false
keywords:
- create multiple sheets
- export data to sheets
- template based excel
- save workbook xlsx
- insert index worksheet
language: tr
og_description: Java kullanarak Excel'de birden fazla sayfa oluşturun. Bu kılavuz,
  verileri sayfalara nasıl dışa aktaracağınızı, şablon tabanlı bir Excel iş akışı
  uygulamayı ve çalışma kitabını xlsx olarak kaydetmeyi gösterir.
og_title: Java ile Excel'de Birden Çok Sayfa Oluşturma – Adım Adım
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiple sheets in Excel using Java. Learn how to export data
    to sheets, use a template based Excel approach, and save workbook xlsx efficiently.
  headline: Create Multiple Sheets in Excel with Java – Complete Template‑Based Guide
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Automation
title: Java ile Excel'de Birden Fazla Sayfa Oluşturma – Tam Şablon Tabanlı Rehber
url: /tr/java/worksheet-management/create-multiple-sheets-in-excel-with-java-complete-template/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Excel’de Birden Çok Sayfa Oluşturma – Tam Şablon‑Tabanlı Rehber

Bir Java uygulamasından **birden çok sayfa** oluşturmanız gerektiğinde nereden başlayacağınızı bilemediğiniz oldu mu? Tek başınıza değilsiniz. İster bir raporlama motoru, bir veri‑dışa aktarma aracı ya da sadece sıkıcı bir elektronik tablo görevini otomatikleştirmeye çalışıyor olun, *verileri sayfalara dışa aktarma* konusunu öğrenmek saatlerce manuel işi tasarruf ettirebilir.

Bu öğreticide, bir **şablon tabanlı Excel** çözümünü adım adım inceleyeceğiz; bu çözüm bir indeks çalışma sayfası eklemenize, her veri öğesi için bir sayfa oluşturmanıza ve sonunda **workbook xlsx** dosyasını tek bir metod çağrısıyla **kaydetmenize** olanak tanır. Gereksiz ayrıntı yok, sadece projenize hemen ekleyebileceğiniz pratik, uçtan uca bir örnek.

## Öğrenecekleriniz

- **Birden çok sayfa** tutacak bir workbook’u nasıl başlatacağınız.
- Aspose.Cells Smart Marker sözdizimini kullanarak çalışma sayfalarını otomatik olarak tekrarlama.
- Şablon için bir veri kaynağı (harita listesi, POJO’lar veya herhangi bir koleksiyon) hazırlama.
- `SmartMarkerProcessor` ile şablonu uygulama.
- Sonucu bir **xlsx** dosyası olarak kaydetme.
- İndeks çalışma sayfası ekleme ve kenar durumlarını yönetme üzerine isteğe bağlı ipuçları.

*Önkoşullar*: Java 8+, Maven veya Gradle ve Aspose.Cells for Java kütüphanesi (deneme sürümü test için yeterli). Aspose’a yeniyseniz endişelenmeyin—kurulum adımlarını kısa tutacağız.

---

## 1. Adım: Workbook’u Başlatma – **Create Multiple Sheets** İçin Tuval

Herhangi bir sayfa görünmeden önce bir `Workbook` örneğine ihtiyacınız var. Bunu, daha sonra oluşturulacak her çalışma sayfasını tutacak boş bir tuval olarak düşünün.

```java
import com.aspose.cells.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an empty workbook that will hold the generated worksheets
        Workbook workbook = new Workbook();
        // ... we'll add more code here later
    }
}
```

> **Neden önemli:** `Workbook` nesnesi tüm Excel dosyasını soyutlar. Boş bir workbook ile başlayarak sayfa oluşturma, biçimlendirme ve son kaydetme üzerinde tam kontrol sağlarsınız.

---

## 2. Adım: **Template Based Excel** İşaretleyicisini Tanımlama – Her Sayfa İçin Mavi Çizgi

Aspose.Cells’ın Smart Marker motoru, yer tutucuları doğrudan bir dize şablonuna gömmenizi sağlar. Özel `${#WorksheetRepeat}` işaretleyicisi, işlemciye veri koleksiyonundaki her öğe için **yeni bir çalışma sayfası** başlatmasını söyler.

```java
// Step 2: Define a Smart Marker template.
// ${#WorksheetRepeat} starts a new worksheet for each item in the data collection.
// ${Index} inserts the current item index, and ${Data} inserts the item value.
String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";
```

> **Pro ipucu:** `\n` karakteri sayfa adından sonra yeni bir satır oluşturur, böylece her sayfanın ilk satırı gerçek veri değerini tutar. Şablonu başlıklar, formüller veya stil eklemek için gerektiği gibi ayarlayın.

---

## 3. Adım: Veri Kaynağınızı Hazırlama – **Export Data to Sheets** Artık Çok Kolay

Şablon, Aspose’ın yineleyebileceği herhangi bir koleksiyonla çalışır. Bu örnek için `List<Map<String,Object>>` kullanacağız, ancak aynı kolaylıkla POJO listesi de geçebilir.

```java
// Step 3: Prepare the data source (a list of maps, objects, etc.).
// Replace this with your actual data collection.
List<Map<String, Object>> dataList = getData(); // placeholder for your data
```

Test ederken kopyalayıp yapıştırabileceğiniz hızlı bir mock uygulama:

```java
private static List<Map<String, Object>> getData() {
    List<Map<String, Object>> list = new ArrayList<>();
    for (int i = 1; i <= 5; i++) {
        Map<String, Object> row = new HashMap<>();
        row.put("Data", "Row value " + i);
        list.add(row);
    }
    return list;
}
```

> **Neden bir harita?** Harita, `${Data}` yer tutucusuyla eşleşen anahtar‑değer çiftleri sağlar. POJO tercih ederseniz, alan adlarının işaretleyicilerle aynı olduğundan emin olun.

---

## 4. Adım: **SmartMarkerProcessor**’ı Başlatma – Sihri Gerçekleştiren Motor

Artık bir workbook ve bir şablonumuz olduğuna göre, bunları birleştirecek işlemciye ihtiyacımız var.

```java
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);
```

İşlemci şablonu okur, `dataList` üzerinde yineleme yapar ve her giriş için yeni bir çalışma sayfası oluşturur. Manuel döngü yazmaya gerek kalmaz.

---

## 5. Adım: Şablonu Uygulama – **Insert Index Worksheet** ve Sayfaları Oluşturma

Bu noktada sadece `processor.apply(template, dataList);` çağrısını yapabilirsiniz. Ancak birçok kullanıcı, tüm oluşturulan sayfa adlarını tıklanabilir bağlantılarla listeleyen bir **indeks çalışma sayfası** da ister. İşte iki adımlı bir yaklaşım:

1. Şablonu kullanarak **veri sayfalarını** oluşturun.
2. Bir **indeks sayfası** oluşturun ve içine hiperlinkler ekleyin.

```java
// Step 5a: Apply the template to the data.
// A new worksheet is created for each element in dataList.
processor.apply(template, dataList);

// Step 5b (optional): Insert an index worksheet at the beginning.
Worksheet indexSheet = workbook.getWorksheets().add("Index");
int row = 0;
indexSheet.getCells().setColumnWidth(0, 25);
indexSheet.getCells().setColumnWidth(1, 30);
indexSheet.getCells().setRowHeight(row, 20);
indexSheet.getCells().get(row, 0).setValue("Sheet Name");
indexSheet.getCells().get(row, 1).setValue("Link");

// Loop through generated sheets and add a hyperlink entry.
for (int i = 0; i < dataList.size(); i++) {
    String sheetName = "Sheet" + (i + 1);
    row++;
    indexSheet.getCells().get(row, 0).setValue(sheetName);
    // Create a hyperlink that points to the generated worksheet.
    Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
            "'" + sheetName + "'!A1", "Go to " + sheetName);
    indexSheet.getCells().get(row, 1).setValue("Open");
}
```

> **Açıklama:**  
> - Döngü, her satırın ilgili sayfaya bağlandığı düzenli bir tablo oluşturur.  
> - `Hyperlink.add` kullanımı, Excel içinde tıklanabilir bir referans sağlar.  
> - Bu adım, **insert index worksheet** özelliğinin nasıl çalıştığını gösterir ve son kullanıcılar için gezinmeyi sorunsuz hâle getirir.

---

## 6. Adım: **Save Workbook Xlsx** – Tek Çağrı, Dağıtıma Hazır

Son olarak workbook’u diske yazın. `save` metodu, uzantıya göre dosya formatını otomatik algılar.

```java
// Step 6: Save the workbook to a file
workbook.save("YOUR_DIRECTORY/output.xlsx");
System.out.println("Workbook saved successfully!");
```

> **İpucu:** Dosyayı doğrudan bir HTTP yanıtına (ör. bir Spring denetleyicisi) akıtmanız gerekiyorsa, `workbook.save(outputStream, SaveFormat.XLSX);` kullanın.

---

## Tam Çalışan Örnek – Kopyala‑Yapıştır Hazır

Aşağıda tüm parçaları bir araya getiren tam program yer alıyor. `"YOUR_DIRECTORY"` kısmını makinenizdeki gerçek bir yol ile değiştirin.

```java
import com.aspose.cells.*;
import java.util.*;

public class MultiSheetExporter {
    public static void main(String[] args) throws Exception {
        // Initialise an empty workbook (Step 1)
        Workbook workbook = new Workbook();

        // Define the Smart Marker template (Step 2)
        String template = "${#WorksheetRepeat}Sheet${Index}\n${Data}";

        // Prepare data (Step 3)
        List<Map<String, Object>> dataList = getData();

        // Initialise the processor (Step 4)
        SmartMarkerProcessor processor = new SmartMarkerProcessor(workbook);

        // Apply template (Step 5a)
        processor.apply(template, dataList);

        // Optional: Insert an index worksheet (Step 5b)
        Worksheet indexSheet = workbook.getWorksheets().add("Index");
        int row = 0;
        indexSheet.getCells().setColumnWidth(0, 25);
        indexSheet.getCells().setColumnWidth(1, 30);
        indexSheet.getCells().setRowHeight(row, 20);
        indexSheet.getCells().get(row, 0).setValue("Sheet Name");
        indexSheet.getCells().get(row, 1).setValue("Link");

        for (int i = 0; i < dataList.size(); i++) {
            String sheetName = "Sheet" + (i + 1);
            row++;
            indexSheet.getCells().get(row, 0).setValue(sheetName);
            Hyperlink link = indexSheet.getHyperlinks().add(row, 1, 1, 1,
                    "'" + sheetName + "'!A1", "Go to " + sheetName);
            indexSheet.getCells().get(row, 1).setValue("Open");
        }

        // Save the workbook (Step 6)
        workbook.save("YOUR_DIRECTORY/output.xlsx");
        System.out.println("Workbook saved successfully!");
    }

    // Mock data generator
    private static List<Map<String, Object>> getData() {
        List<Map<String, Object>> list = new ArrayList<>();
        for (int i = 1; i <= 5; i++) {
            Map<String, Object> row = new HashMap<>();
            row.put("Data", "Row value " + i);
            list.add(row);
        }
        return list;
    }
}
```

**Beklenen çıktı:**  
- Altı çalışma sayfası (`Index`, `Sheet1` … `Sheet5`) içeren bir `output.xlsx` dosyası.  
- `Index` sayfası, her oluşturulan sayfa adını tıklanabilir “Open” bağlantısı ile listeler.  
- Her `SheetX` sayfası, `A1` hücresinde “Row value X” metnini barındırır.

---

## Yaygın Sorular & Kenar Durumları

| Soru | Cevap |
|------|-------|
| **`List<Map>` yerine bir CSV veya JSON kaynağı kullanabilir miyim?** | Kesinlikle. Aspose’ın Smart Marker’ı herhangi bir `Iterable` koleksiyonla çalışır. JSON alanlarınızı işaretleyici adlarıyla eşleştirmeniz yeterlidir. |
| **Veri listem boş olursa ne olur?** | İşlemci ek bir çalışma sayfası oluşturmaz, ancak indeks sayfası hâlâ eklenir (bunu önlemek isteyebilirsiniz). |
| **Her oluşturulan sayfaya başlık veya stil eklemek istiyorum, nasıl yaparım?** | Şablonu genişletin: `"${#WorksheetRepeat}Sheet${Index}\nHeader1,Header2\n${Data}"`. Ayrıca `apply` sonrası programatik olarak stil uygulayabilirsiniz. |
| **Sayfa sayısı için bir limit var mı?** | Pratikte, Excel bir sayfada 1.048.576 satırla sınırlıdır; sayfa sayısı yalnızca bellekle sınırlıdır. |
| **Aspose.Cells için bir lisansa ihtiyacım var mı?** | Geliştirme aşamasında ücretsiz deneme sürümü yeterlidir. Üretim için bir lisans, değerlendirme filigranını kaldırır ve tam özellikleri açar. |

---

## Sonuç

Artık Java’da **birden çok sayfa oluşturma** iş akışını, **şablon tabanlı Excel** yaklaşımıyla, **verileri sayfalara dışa aktarma**, isteğe bağlı **indeks çalışma sayfası ekleme** ve tek satır kodla **workbook xlsx** kaydetme adımlarını biliyorsunuz. Bu desen, birkaç satırdan büyük veri dışa aktarımlarına kadar sorunsuz ölçeklenir ve kodunuzu temiz ve sürdürülebilir tutar.

Bir sonraki adıma hazır mısınız? Koşullu biçimlendirme ekleyin, grafik yerleştirin veya indeksi bir özet panosu ile birleştirin. Aynı Smart Marker motoru, birkaç ekstra işaretleyiciyle bu senaryoları da halledebilir.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da Aspose.Cells’ın kapsamlı belgelerini inceleyin. İyi kodlamalar ve bu elektronik tabloları otomatikleştirmenin tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Create & Access Excel Sheets, Add PDF Bookmarks Using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Export Excel Sheets to Images Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/workbook-operations/export-excel-sheets-images-aspose-cells-java/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}