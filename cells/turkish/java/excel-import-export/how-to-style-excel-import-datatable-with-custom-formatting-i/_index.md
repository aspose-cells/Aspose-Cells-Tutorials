---
category: general
date: 2026-07-03
description: Java kullanarak Excel dosyalarını nasıl biçimlendireceğinizi öğrenin.
  Sütun tarihini Excel'de biçimlendirmeyi, sayı formatını Excel'de uygulamayı, DataTable'ı
  XLSX'e dışa aktarmayı ve Aspose Cells ile DataTable'ı Excel'e içe aktarmayı keşfedin.
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: tr
og_description: Java'da Excel dosyalarını nasıl biçimlendirilir. Bu öğreticide sütun
  tarihini Excel'de nasıl biçimlendireceğiniz, sayı formatını Excel'de nasıl uygulayacağınız,
  DataTable'ı XLSX'e nasıl dışa aktaracağınız ve DataTable'ı Excel'e nasıl içe aktaracağınız
  gösterilmektedir.
og_title: Excel'i Nasıl Stilize Edilir – Özel Sütun Biçimlendirme için Java Rehberi
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Excel'i Nasıl Stilize Edilir – Java'da Özel Biçimlendirme ile DataTable İçe
  Aktarma
url: /tr/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel’i Nasıl Stilize Edilir – Java’da DataTable’ı Özel Biçimlendirme ile İçe Aktarma

Excel sayfalarını dosyayı manuel olarak açmadan programlı bir şekilde **nasıl stilize edeceğinizi** hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, ilk sütunun kalın, ikinci sütunun tarih gösterdiği ve geri kalanının temiz bir düzen izlediği raporlar üretmek zorunda. Bu rehberde **DataTable’ı Excel’e içe aktaran**, kalın bir başlık ekleyen, tarih sütununu biçimlendiren ve sonunda **DataTable’ı XLSX’e dışa aktaran** tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.  

Aspose.Cells for Java’yı kullanacağız, ancak kavramlar stil ile çalışmanıza izin veren herhangi bir kütüphane için geçerlidir. Sonunda **apply number format Excel** hücreleri, **format column date Excel** ve kullanıcılarınıza şık bir çalışma kitabı gönderme konusunda yeniden kullanılabilir bir deseniniz olacak.

## Önkoşullar

- Java 17 (veya herhangi bir güncel JDK)  
- Aspose.Cells for Java 23.9 veya daha yeni (ücretsiz deneme yeterli)  
- `DataTable`‑benzeri bir yapı (örnek basit bir mock kullanıyor)  
- Sevdiğiniz IDE (IntelliJ IDEA, Eclipse, VS Code…)

Ek Maven eklentileri gerekmez; sadece Aspose.Cells JAR dosyasını sınıf yolunuza ekleyin.

---

## Adım 1: Kaynak DataTable’ı Edinin – “Export DataTable to XLSX” Hazırlığı

**datatable’ı excel’e içe aktarmadan** önce dışa aktarmak istediğiniz veriyi temsil eden bir `DataTable` nesnesine ihtiyacımız var. Gerçek projelerde bunu bir veritabanı, CSV dosyası veya bir API’dan alabilirsiniz. Bu öğreticide küçük bir tabloyu mock’layacağız:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Neden önemli:** Veriyi baştan doğru almak, stil mantığının sadece sunuma odaklanmasını sağlar, veri işleme ile uğraşmazsınız.

---

## Adım 2: Her Sütun İçin Stil Tanımları Tutacak Bir Dizi Oluşturun

Aspose.Cells, bir `DataTable` içe aktarırken **Style[]** dizisi almanıza izin verir. Her giriş bir sütuna karşılık gelir ve içe aktarıldıktan sonra o sütunun nasıl görüneceğini belirler. Sütun sayısına göre diziyi ayıralım:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **İpucu:** Çok sayıda sütununuz varsa diziyi bir döngüde oluşturup aynı biçimlendirmeye sahip sütunlar için tek bir `Style` nesnesini yeniden kullanın. Bu bellek yükünü azaltır.

---

## Adım 3: Stilleri Tanımlayın – Kalın Başlık ve Tarih Biçimlendirme

Şimdi klasik **format column date excel** sorusuna yanıt veriyoruz ve aynı zamanda diğer sütunlar için **apply number format excel** gösteriyoruz.

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**Burada ne oluyor?**  
- `StyleNumberFormat.DATE`, Excel’in hücre değerini kısa tarih olarak (ör. *01/31/2024*) ele almasını sağlar.  
- `StyleNumberFormat.CURRENCY_USD` otomatik olarak `$` sembolünü ve iki ondalık basamağı ekler.  
- İlk sütunda fontu kalın yaparak başlık öne çıkar; bu, **how to style excel** elektronik tablolarının okunabilirliğini artırmak için sıkça istenen bir durumdur.

> **Köşe durumu:** Kaynak veriniz zaten biçimlendirilmiş stringler içeriyorsa, içe aktarmadan önce bunları `java.util.Date` nesnelerine dönüştürmeniz gerekir; aksi takdirde Excel bunları düz metin olarak algılar.

---

## Adım 4: Yeni Bir Workbook Oluşturun ve İlk Worksheet’ine Erişin

Temiz bir çalışma kitabı bize boş bir tuval sağlar. İçe aktarımın gerçekleşeceği ilk worksheet’i alacağız.

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Neden yeni bir workbook?** Sıfırdan başlamak, kalan stil ya da gizli satırların son çıktıyı etkilemesini önler—bu, **how to style excel** dosyalarını tutarlı bir şekilde birden çok çalıştırma için kritiktir.

---

## Adım 5: DataTable’ı Sütun Stilleriyle İçe Aktarın

İşlemin kalbi burada: `DataTable`’ı sheet’e beslerken daha önce oluşturduğumuz stil dizisini uyguluyoruz.

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Açıklama:**  
- `importDataTable` hem başlık satırını hem de veri satırlarını kopyalar.  
- `columnStyles` dizisi her sütunla hizalanır, böylece ilk sütun başlığı kalın, ikinci sütun tarih, üçüncü sütun para birimi olarak görünür.  
- Bu tek satır, elle hücre‑hücre biçimlendirme adımlarını onlarla değiştirir ve **apply number format excel**’i programatik olarak temiz bir şekilde gösterir.

---

## Adım 6: Stilize Workbook’u Kaydedin – “Export DataTable to XLSX” Tamamlanıyor

Son olarak workbook’u diske kalıcı olarak kaydediyoruz. Yolunuzu makinenizde yazılabilir bir klasöre göre ayarlayın.

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Dosyayı Excel’de açtığınızda şunları görmelisiniz:

- **ID** sütun başlığı kalın.  
- **OrderDate** sütunu tarih olarak biçimlendirilmiş (ör. *04/27/2024*).  
- **Total** sütunu dolar işareti ve iki ondalık basamakla gösterilir.

> **Pro ipucu:** Daha eski Excel sürümlerini desteklemeniz gerekiyorsa, varsayılan XLSX yerine `workbook.save(outputPath, SaveFormat.XLS)` çağrısını kullanın.

---

## Adım 7: Sonucu Doğrulayın ve İsteğe Bağlı Ayarlamalar Yapın

Oluşturulan dosyayı, özellikle paydaşlar için rapor otomasyonu yapıyorsanız, iki kez kontrol etmek iyi bir uygulamadır.

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

`isBold` `true` yazdırıyorsa, **how to style excel** rutininiz beklendiği gibi çalıştı. Buradan sonra şunları yapabilirsiniz:

- Koşullu biçimlendirme ekleyin (ör. $200 > tutarları vurgulayın).  
- Daha kolay kaydırma için üst satırı dondurun.  
- İçe aktarılan veriye referans veren bir grafik ekleyin.

Tüm bu uzantılar aynı deseni izler: bir `Style` tanımlayın, uygulayın ve kaydedin.

---

## Yaygın Sorular & Köşe Durumları

| Soru | Cevap |
|----------|--------|
| **Birden fazla sütunu aynı şekilde stilize edebilir miyim?** | Evet—biçimlendirmeyi paylaşan tüm sütunlar için tek bir `Style` örneğini yeniden kullanın. |
| **DataTable’ım stil dizisinden daha fazla sütun içeriyorsa ne olur?** | `columnStyles` içinde karşılığı olmayan sütunlar varsayılan stil kullanır. |
| **Tarih formatını “dd‑MMM‑yyyy” olarak nasıl değiştiririm?** | Yerleşik `DATE` yerine `columnStyles[1].setCustom("#dd-MMM-yyyy#");` kullanın. |
| **İçe aktarma sonrası sütunları otomatik olarak boyutlandırabilir miyim?** | `importDataTable` sonrası `worksheet.autoFitColumns();` çağırın. |
| **Bu Linux/macOS’ta çalışır mı?** | Kesinlikle—Aspose.Cells, uyumlu bir JDK olduğu sürece platform bağımsızdır. |

---

## Sonuç

Artık **how to style Excel** çalışma kitaplarını **importing datatable into excel**, **format column date excel** ve **apply number format excel** kullanarak Java ile oluşturmanın tam bir uçtan uca örneğine sahipsiniz. Kod, **export datatable to xlsx** aşamasından dosyayı Excel’de açmaya kadar tüm akışı gösteriyor ve her adımın *ne* ve *neden* olduğunu açıklıyor.  

Deneyin: stil dizisini ayarlayın, daha fazla sütun ekleyin ya da gerçek bir veritabanı sorgusu bağlayın. Aynı desen, tek bir tıkla profesyonel görünümlü raporlar üretmenizi sağlar, manuel biçimlendirme gerekmez.

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Resim alt metni: “Java ve Aspose.Cells kullanılarak oluşturulan, kalın başlık ve biçimlendirilmiş tarih sütunu gösteren stilize Excel çalışma sayfası.”*


## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımları keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}