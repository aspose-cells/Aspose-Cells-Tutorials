---
category: general
date: 2026-08-20
description: Java kullanarak ondalık basamakları sınırlayarak, anlamlı basamakları
  koruyarak ve çalışma kitabını TXT olarak kaydederek Excel'i TXT'ye dışa aktarmayı
  öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: tr
lastmod: 2026-08-20
og_description: Aspose.Cells ile Excel'i TXT'ye dışa aktarın. Bu kılavuz, ondalık
  basamakları sınırlamayı, anlamlı basamakları korumayı ve Java'da çalışma kitabını
  TXT olarak kaydetmeyi gösterir.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Java'da Excel'i TXT'ye Dışa Aktar – Ondalık Basamakları ve Anlamlı Basamakları
  Kontrol Et
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Aspose.Cells ile Excel'i TXT'ye nasıl dışa aktarır ve ondalık hassasiyetini
  kontrol edersiniz
url: /tr/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i TXT'ye Aktarmak ve Aspose.Cells ile Ondalık Hassasiyetini Kontrol Etmek

Eğer **Excel'i TXT'ye aktarmanız** ve çıktının belirli bir ondalık basamak sayısına uymasını sağlamak istiyorsanız, bu kılavuz tam bir çözüm sunar. Ondalık basamakları nasıl sınırlayacağınızı, anlamlı basamakları nasıl koruyacağınızı ve Aspose.Cells Java kütüphanesini kullanarak **workbook'u TXT olarak kaydetmeyi** göreceksiniz.

Bu öğretici, bir workbook oluşturmayı, yüksek hassasiyetli bir değer eklemeyi, TXT kaydetme seçeneklerini yapılandırmayı ve dosyayı diske yazmayı adım adım gösterir. Sonunda, manuel sonrası işleme gerek kalmadan, tam olarak ihtiyacınız olan hassasiyeti içeren bir metin dosyası oluşturabilirsiniz.

## Gereksinimler

- Java 17 (veya desteklenen herhangi bir JDK)
- Aspose.Cells for Java 23.10 veya daha yeni sürüm
- Bağımlılıkları yönetmek için bir IDE veya derleme aracı (Maven/Gradle)
- Çıktı dizinine yazma izni

## Adım 1: Bir workbook oluşturun ve ilk çalışma sayfasına erişin

Bir workbook oluşturmak, **Excel'i TXT'ye aktarmak** istediğinizde ilk adımdır. `Workbook` sınıfı tüm Excel dosyasını temsil eder ve `Worksheet` hücrelere erişim sağlar.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Neden önemli*: workbook nesnesi tüm veri, stil ve meta verileri tutar. Yeni bir workbook ile başlamak, gizli biçimlendirmelerin metin dışa aktarmasını etkilememesini garanti eder.

## Adım 2: Sayısal bir değer ekleyin ve ondalık basamakları sınırlayın

Dışa aktarım sırasında **ondalık basamakları sınırlamayı** gösterebilmek için birçok ondalık basamağa sahip bir sayı ekleyin.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Neden önemli*: Excel tam hassasiyeti saklar, ancak daha sonra dışa aktardığınızda değeri kırpmak veya yuvarlamak isteyebilirsiniz. `limit decimal places` ayarı bunu otomatik olarak halleder.

## Adım 3: TXT kaydetme seçeneklerini anlamlı basamakları koruyacak şekilde yapılandırın

Aspose.Cells `TxtSaveOptions` sağlar. `significantDigits` ayarı, dışa aktarıcıya yalnızca gerekli anlamlı basamak sayısını tutmasını söyler, önde gelen sıfırları yok sayar.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Neden önemli*: **keep significant digits** seçeneği, çıktının tahmin edilebilir bir hassasiyet içermesini sağlar; bu, sabit genişlikli sayısal format bekleyen sonraki sistemler için kritiktir.

## Adım 4: Workbook'u TXT olarak kaydedin

Son olarak, workbook'u bir metin dosyasına yazın. `save` yöntemi yapılandırdığınız seçeneklere uyar, böylece ortaya çıkan dosya sınırlı ondalık temsili içerir.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Neden önemli*: Hazırlanan `TxtSaveOptions` ile **save workbook as txt** kullanmak, dışa aktarılan dosyanın önceki adımda belirlediğiniz hassasiyet kısıtlamalarına uymasını garanti eder.

### `SignificantDigits.txt` dosyasının beklenen içeriği

```
0.00012346
```

Değer, yuvarlamadan sonra beş anlamlı basamağı (`12346`) gösterir ve önde gelen sıfırlar TXT formatına göre korunur.

## Varyasyonlar ve kenar durumları

| Senaryo | Ayarlama |
|----------|------------|
| **Farklı sayıda anlamlı basamak** | `txtOptions.setSignificantDigits(n)` çağırın, burada `n` 1‑15 arasındadır. |
| **Tüm sayfa yerine bir aralık dışa aktarmak** | Kaydetmeden önce `txtOptions.setExportRange("A1:B10")` kullanın. |
| **Sütun ayırıcılarını korumak** | Sekme‑ayırmalı çıktı için `txtOptions.setSeparator('\t')` ayarlayın. |
| **Büyük çalışma sayfaları** | `OutOfMemoryError` hatasından kaçınmak için `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` değerini artırın. |

## Yaygın tuzaklar ve profesyonel ipuçları

- **Anlamlı basamakları ondalık basamaklarla karıştırmayın**. Önde gelen sıfırlar anlamlı sayılmaz; anlamlı hassasiyet için `setSignificantDigits`, ondalık noktadan sonra sabit sayıdaki basamak gerekiyorsa `setDecimalPlaces` kullanın.
- **IDE'den çalıştırırken her zaman mutlak bir çıktı yolu belirtin**; bu, izin hatalarını önler.
- **Oluşturulan dosyayı doğrulayın**; `java.nio.file.Files.readAllLines(Paths.get(outputPath))` çağrısı ile içeriğin beklentilere uygun olduğunu kontrol edin, ardından sonraki süreçlere aktarın.

## Referans için tam kaynak kodu

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

Programı çalıştırdığınızda, tek satır `0.00012346` içeren `SignificantDigits.txt` dosyası üretilir; bu, **export excel to txt** sürecinin hem **limit decimal places** hem de **keep significant digits** gereksinimlerine uyduğunu gösterir.

## Sonuç

Artık Aspose.Cells for Java kullanarak **Excel'i TXT'ye aktarmayı** ve sayısal hassasiyeti kontrol etmeyi biliyorsunuz. `TxtSaveOptions` yapılandırarak **ondalık basamakları sınırlayabilir**, **anlamlı basamakları koruyabilir** ve ek bir sonrası işleme gerek kalmadan **workbook'u txt olarak kaydedebilirsiniz**.

Sonraki adımda şunları keşfedebilirsiniz:

- Birden fazla sayfayı ayrı TXT dosyalarına aktarmak (`save workbook as txt` her sayfa için)
- `setSeparator` kullanarak CSV uyumlu çıktı oluşturmak
- Büyük veri setleri için toplu dönüşümleri otomatikleştirmek

Projenizin tam ihtiyaçlarına göre farklı basamak sayıları ve ayırıcılarla denemeler yapmaktan çekinmeyin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalı tam çalışan kod örnekleri içerir.

- [Aspose.Cells Java Kullanarak Excel'i HTML'ye Oluşturma ve Aktarma | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Excel'i Metin Olarak Kaydet – Excel'i TXT'ye Aktarmak İçin Tam C# Kılavuzu](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Aspose.Cells for Java Kullanarak Excel Workbook'u Görüntü Olarak Aktarma: Adım Adım Kılavuz](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}