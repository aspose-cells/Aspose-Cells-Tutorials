---
category: general
date: 2026-11-25
description: Java ve Aspose.Cells kullanarak Excel çalışma kitabı oluşturmayı, hücreyi
  genel biçimde formatlamayı, Excel hücresine stil uygulamayı ve çalışma kitabını
  XLSX olarak kaydetmeyi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- format cell general
- apply style excel cell
- save workbook xlsx
language: tr
lastmod: 2026-11-25
og_description: Java'da Excel çalışma kitabı oluştur, hücreyi genel biçimde formatla,
  Excel hücresine stil uygula ve Japon era tarihlerini işleyerek çalışma kitabını
  XLSX olarak kaydet.
og_image_alt: Screenshot of a Java IDE showing code that creates an Excel workbook
  with a formatted date cell
og_title: Japon dönem tarihleriyle Excel çalışma kitabı oluşturma – adım adım Java
  rehberi
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to create Excel workbook, format cell general, apply style
    Excel cell, and save workbook XLSX using Java and Aspose.Cells.
  headline: How to create Excel workbook with Japanese era dates in Java
  type: TechArticle
tags:
- Java
- Excel automation
- Aspose.Cells
title: Java'da Japon dönem tarihleriyle Excel çalışma kitabı nasıl oluşturulur
url: /tr/java/formatting/how-to-create-excel-workbook-with-japanese-era-dates-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da Japon era tarihleriyle Excel çalışma kitabı nasıl oluşturulur

Japon era tarihlerini (ör. “R3‑04‑01”) depolayan **Excel çalışma kitabı** oluşturmanız gerekiyorsa, bu kılavuz tam adımları gösterir. Hücreyi Genel olarak biçimlendirmeyi, Excel hücresine stil uygulamayı ve sonunda **XLSX çalışma kitabını kaydetmeyi** göreceksiniz; böylece tarih doğru şekilde yorumlanır.

Japon era dizeleriyle (ör. “R3‑04‑01”) çalışmak zor olabilir çünkü Excel yalnızca metin değil gerçek bir `DateTime` değeri bekler. Bu öğreticinin sonunda, orijinal era gösterimini korurken doğru Gregoryen tarihi gösteren tam işlevsel bir `.xlsx` dosyanız olacak.

## Önkoşullar

- Java 17 veya daha yeni bir sürüm (kod daha eski sürümlerle de derlenebilir)
- Aspose.Cells for Java kütüphanesi (`aspose-cells-xx.x.jar`) – kütüphane değerlendirme için ücretsiz ve üretim için tam özelliklidir
- Java ve Maven/Gradle temelleri (veya JAR dosyasını sınıf yolunuza ekleyebilme)
- IntelliJ IDEA, Eclipse veya VS Code gibi bir IDE (herhangi biri çalışır)

## Adım 1 – Bir Excel çalışma kitabı oluşturun

İlk işlem, yeni bir çalışma kitabı nesnesi örneklemektir. Bu nesne, bellekteki tüm Excel dosyasını temsil eder ve çalışma sayfalarına, hücrelere ve stillere erişim sağlar.

```java
import com.aspose.cells.*;

public class JapaneseEraExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook (an empty .xlsx file in memory)
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Neden önemli:**  
Çalışma kitabını programlı olarak oluşturmak, bir şablon dosyasına ihtiyaç duymadan temiz bir başlangıç sağlar. `Workbook` yapıcı, otomatik olarak bir varsayılan sayfa oluşturur; bu sayfayı daha sonra manipüle etmek için alırız.

## Adım 2 – Hücreyi Genel olarak biçimlendirin

Excel, sayıları farklı biçimlerde saklar. Daha sonra Japon era dizisinden dönüştüreceğimiz tarih için, hücrenin sayı biçimini *Genel* olarak ayarlarız; böylece Excel metni erken yorumlamaz.

```java
        // Step 2: Get the target cell (A1) where the era date will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Write the raw Japanese era string (e.g., "R3-04-01")
        targetCell.putValue("R3-04-01");

        // Ensure the cell uses the General number format
        Style cellStyle = targetCell.getStyle();
        cellStyle.setNumber(0); // 0 = General format in Aspose.Cells
        targetCell.setStyle(cellStyle);
```

**Neden önemli:**  
**format cell general** ayarı, Excel'in era dizisini özel bir metin biçimi olarak otomatik biçimlendirmesini engeller; bu da daha sonra gerçek bir `DateTime`a dönüşümü engeller. `setNumber(0)` çağrısı, Aspose.Cells'in Excel’in “General” biçimine eşdeğeridir.

## Adım 3 – Excel hücresine stil uygulayın

Temel amaç bir tarih depolamak olsa da, hücrenin sayfanın geri kalanıyla tutarlı görünmesini isteyebilirsiniz—örneğin ince bir kenarlık veya belirli bir yazı tipi. Stil uygulamak, aynı zamanda hücre estetiğini programlı olarak nasıl manipüle edeceğinizi gösterir.

```java
        // Step 3: Apply additional styling (optional but common)
        // Example: add a thin border around the cell
        cellStyle.setBorder(BorderType.TOP_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.BOTTOM_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.LEFT_BORDER, CellBorderType.THIN);
        cellStyle.setBorder(BorderType.RIGHT_BORDER, CellBorderType.THIN);

        // Set a light gray background to highlight the date cell
        cellStyle.setPattern(BackgroundType.SOLID);
        cellStyle.setBackgroundColor(Color.getGray());

        // Apply the updated style back to the cell
        targetCell.setStyle(cellStyle);
```

**Neden önemli:**  
**apply style excel cell** adımı, temel veriyi etkilemeden görsel sunumu zenginleştirmenin yolunu gösterir. Kenarlıklar ve arka plan renkleri, hücrenin stil nesnesinin bir parçası olarak saklanır; böylece açıldığında çalışma kitabı şık görünür.

## Adım 4 – Japon era dizisini bir DateTime nesnesine dönüştürün

Şimdi ham metni gerçek bir `DateTime` değeriyle değiştiriyoruz. Aspose.Cells, belirli bir `CultureInfo` kullanarak bir dizeyi ayrıştırabilir. Japon kültürünü (`ja-JP`) geçirerek, kütüphane “R3‑04‑01” ifadesini Reiwa döneminin 3. yılı olarak doğru şekilde yorumlar; bu da Gregoryen takvimde 2021‑04‑01 tarihine karşılık gelir.

```java
        // Step 4: Convert the era string to a DateTime using Japanese culture
        // The fromString method respects the culture’s calendar (Japanese Imperial)
        DateTime japaneseDate = DateTime.fromString(
                "R3-04-01", // era string
                CultureInfo.createSpecificCulture("ja-JP") // Japanese locale
        );

        // Overwrite the cell value with the parsed DateTime
        targetCell.setValue(japaneseDate);
```

**Neden önemli:**  
Kültür belirtilmezse, “R3‑04‑01” düz metin olarak kabul edilir ve tarih anlamı kaybolur. `CultureInfo` nesnesi, Aspose.Cells'e Japon takvim sistemini kullanmasını söyler; böylece era dönüşümü otomatik olarak yapılır. Sonuçta hücre gerçek bir Excel tarihi içerir ve sıralama, filtreleme ve tarih aritmetiği gibi işlemler mümkün olur.

## Adım 5 – Çalışma kitabını XLSX olarak kaydedin

Son olarak, bellek içindeki çalışma kitabını fiziksel bir dosyaya yazarız. `.xlsx` formatını kullanmak, modern Excel sürümleri, Google Sheets ve diğer tablo araçlarıyla uyumluluğu garantiler.

```java
        // Step 5: Save the workbook to the desired location
        String outputPath = "JapaneseEra.xlsx"; // adjust the path as needed
        workbook.save(outputPath, SaveFormat.XLSX);

        System.out.println("Workbook saved successfully to " + outputPath);
    }
}
```

**Neden önemli:**  
**save workbook xlsx** işlemi tüm değişiklikleri sonlandırır. Aspose.Cells, çalışma kitabını Open XML formatında yazar; önceki adımlarda uygulanan veri ve stil korunur. Oluşan dosya doğrudan Excel’de açılabilir; hücre `2021‑04‑01` (Gregoryen eşdeğeri) gösterir, ancak orijinal era dizesi Excel’in “Format Cells → Number → Custom” menüsüyle hâlâ elde edilebilir.

## Beklenen çıktı

`JapaneseEra.xlsx` dosyasını Microsoft Excel’de açtığınızda:

- **A1** hücresi `2021‑04‑01` tarihini (Excel’in varsayılan tarih biçimi) gösterir.  
- Hücre ince gri bir kenarlığa ve açık gri bir arka plana sahiptir; bu da **apply style excel cell** adımının başarılı olduğunu kanıtlar.  
- Hücre biçimini “General” olarak değiştirirseniz, temel değer gerçek bir tarih olmaya devam eder; orijinal dize değişmez.

Konsol şu çıktıyı verir:

```
Workbook saved successfully to JapaneseEra.xlsx
```

## Yaygın varyasyonlar ve kenar durumları

| Durum | Ne değiştirilmeli |
|-----------|----------------|
| **Farklı era (ör. Heisei)** | Girdi dizesinde uygun era ön ekini (`H` Heisei için) kullanın. Aynı `CultureInfo` dönüşümü halleder. |
| **Birden fazla tarih** | Hücre aralığını döngüye alın ve aynı dönüşüm mantığını her birine uygulayın. |
| **Özel tarih biçimi** | `setValue(japaneseDate)` sonrası `cellStyle.setNumber(14)` (veya başka bir Excel sayı formatı kimliği) çağırarak tarihleri `yyyy/MM/dd` şeklinde gösterin. |
| **Büyük çalışma kitapları** | Performans için tek bir `Style` nesnesi yeniden kullanın veya sadece gerekli özellikleri değiştirmek için `StyleFlag` kullanın. |
| **Akışa kaydetme** | Dosyayı HTTP üzerinden gönderirken `workbook.save(outputPath, SaveFormat.XLSX)` yerine `workbook.save(outputStream, SaveFormat.XLSX)` kullanın. |

## Alandan ipuçları

- **Pro ipucu:** `DateTime` atamadan önce hücrenin sayı biçimini *her zaman* ayarlayın. Sonradan biçim değiştirmek, Excel’in yanlış görsel temsil göstermesine neden olabilir.  
- **Dikkat edilmesi gereken:** `CultureInfo("ja-JP")` kullanırken `createSpecificCulture` eklenmezse takvim Gregorian’e geri dönebilir ve tarih hatalı olur.  
- **Performans notu:** Çok sayıda stil uygulanmış hücre oluştururken, her hücre için `getStyle()` çağırmak yerine mevcut bir `Style` nesnesini klonlayın; bu iç kopyalama yükünü azaltır.

## Sonuç

Bu öğreticide **Excel çalışma kitabı oluşturma**, **hücreyi genel biçimde ayarlama**, **excel hücresine stil uygulama** ve **XLSX olarak kaydetme** işlemlerini, Japon era tarihlerini doğru şekilde işleyerek nasıl yapacağınızı öğrendiniz. Tam kod örneği kopyalanıp yapıştırılarak çalıştırılmaya hazır; böylece Gregoryen olmayan takvimleri içeren herhangi bir Excel otomasyonu için güvenilir bir temel elde edersiniz.

İleride şunları keşfedebilirsiniz:

- Dönüştürülmüş tarihlere referans veren formüller ekleme (ör. `=YEAR(A1)`).  
- `workbook.save("output.pdf", SaveFormat.PDF)` kullanarak çalışma kitabını PDF’ye dışa aktarma.  
- Bu mantığı bir Spring Boot REST uç noktasına entegre ederek talep üzerine raporlar üretme.

Farklı kültürler, özel sayı biçimleri veya toplu veri aktarımıyla denemeler yapmaktan çekinmeyin. Mutlu kodlamalar!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan yakın konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaştırabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Excel Workbook Initialization & Cell Styling using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/formatting/excel-workbook-initialization-cell-styling-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}