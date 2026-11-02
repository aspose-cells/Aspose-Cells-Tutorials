---
category: general
date: 2026-08-20
description: Aspose.Cells ile Java’da grafiği docx’e dışa aktarmayı ve Excel çalışma
  kitabını docx’e dönüştürmeyi öğrenin. Tam kodlu adım adım kılavuz.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: tr
lastmod: 2026-08-20
og_description: Aspose.Cells for Java kullanarak grafiği docx'e dışa aktarın ve Excel
  çalışma kitabını docx'e dönüştürün. Bu tam, çalıştırılabilir öğreticiyi izleyin.
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Aspose.Cells ile grafiği docx'e aktar – Java rehberi
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to export chart to docx and convert Excel workbook to docx
    with Aspose.Cells in Java. Step‑by‑step guide with complete code.
  headline: How to export chart to docx from Excel using Aspose.Cells for Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- DOCX
- Excel
title: Aspose.Cells for Java kullanarak Excel'den docx'e grafik nasıl dışa aktarılır
url: /tr/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java kullanarak bir Excel çalışma kitabından docx'e grafik dışa aktarma

Eğer bir Excel dosyasından doğrudan **export chart to docx** yapmanız gerekiyorsa, bu öğretici hazır‑çalıştırılabilir bir çözüm gösterir. Kılavuzun sonunda **convert Excel workbook to docx** işlemini de düzenlenebilir bir grafik koruyarak nasıl yapacağınızı öğreneceksiniz, böylece ortaya çıkan Word belgesi doğruluğunu kaybetmeden değiştirilebilir.

Grafik dışa aktarma, elektronik tablo hesaplamalarını zengin Word düzenleriyle birleştiren raporlar oluşturduğunuzda yaygındır. Aspose.Cells for Java dönüşümü basitleştirir ve API, grafiği düzenlenebilir tutmanıza olanak tanır—statik görüntü gerekmez.

## Bu öğreticide neler ele alınmaktadır

* Grafik içeren mevcut bir çalışma kitabını yükleme.  
* `ImageOrPrintOptions`'ı DOCX formatına hedefleyecek şekilde yapılandırma.  
* `ExportEditableCharts` bayrağını etkinleştirme (sürüm 25.10'dan itibaren kullanılabilir).  
* Çalışma kitabını düzenlenebilir bir grafik içeren DOCX dosyası olarak kaydetme.  

Aspose.Cells JAR dışındaki harici araçlara gerek yoktur. Kod, Java 8+ ve Aspose.Cells'in herhangi bir yeni sürümüyle çalışır.

## Önkoşullar

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 or later) | Bu sürümde `setExportEditableCharts` özelliği tanıtıldı. |
| **Java Development Kit (JDK) 8 or newer** | Örneği derlemek ve çalıştırmak için çalışma zamanını sağlar. |
| **An Excel workbook (`.xlsx`) that contains at least one chart** | Grafik, DOCX'e dışa aktarılacak nesnedir. |
| **A Java IDE or build tool (e.g., Maven, Gradle)** | Bağımlılık yönetimini ve çalıştırmayı basitleştirir. |

En son Aspose.Cells JAR'ı [Aspose web sitesinden](https://products.aspose.com/cells/java/) indirebilirsiniz.

## Adım 1: Projeyi kurun ve Aspose.Cells bağımlılığını ekleyin

Maven kullanıyorsanız, aşağıdaki bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Gradle için, şunu ekleyin:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** `ExportEditableCharts` özelliğini tanıtan tam sürümü (25.10) ya da daha yeni bir sürümü kullanın. Eski sürümler bayrağı görmezden gelir ve bunun yerine statik bir görüntü üretir.

## Adım 2: Grafiği içeren çalışma kitabını yükleyin

`Workbook` sınıfı tüm Excel dosyasını temsil eder. Yüklemesi tek satırlık bir işlemdir:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Neden önemli:** Çıktı seçeneklerini uygulamadan önce çalışma kitabının tamamen yüklenmiş olması gerekir. Dosya yolu yanlışsa, Aspose.Cells bir `FileNotFoundException` fırlatır.

## Adım 3: DOCX çıktısı için görüntü/yazdırma seçeneklerini yapılandırın

`ImageOrPrintOptions`, çalışma kitabının nasıl render edileceğini kontrol eder. Kaydetme formatını `DOCX` olarak ayarlamak, Aspose.Cells'a bir görüntü yerine Word belgesi üretmesini söyler.

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

Burada sayfa boyutunu, DPI'yi veya görüntü kalitesini de ayarlayabilirsiniz, ancak bunlar grafik dışa aktarma için isteğe bağlıdır.

## Adım 4: Düzenlenebilir grafiklerin dışa aktarımını etkinleştirin

Sürüm 25.10'dan itibaren, Aspose.Cells grafiklerini yerel Word grafik nesneleri olarak gömebilir. Bu, onları Microsoft Word'de tamamen düzenlenebilir kılar.

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Köşe durumu:** Bu bayrağı `false` olarak ayarlarsanız (veya atlamazsanız), grafik statik bir resim olarak render edilir. Dönüşümden sonra hedef kitlenin grafiği düzenlemesi gerektiğinde yalnızca `true` kullanın.

## Adım 5: Çalışma kitabını DOCX dosyası olarak kaydedin

Son olarak, yapılandırılmış seçeneklerle `Workbook.save` metodunu çağırın:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

Program tamamlandığında, `ChartEditable.docx` dosyasını Microsoft Word'de açın. Orijinal grafiği görmelisiniz ve üzerine sağ‑tıklarsanız **Edit Data** seçeneği mevcut olacaktır—grafiğin gerçekten düzenlenebilir olduğunu doğrular.

## Tam, çalıştırılabilir örnek

Aşağıda tam kaynak dosyası verilmiştir. IDE'nize kopyalayın, `YOUR_DIRECTORY` ifadesini mutlak ya da göreli bir yol ile değiştirin ve çalıştırın.

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains the chart
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");

        // Step 2: Create image/print options and set the target format to DOCX
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);

        // Step 3: Enable exporting of editable charts (available from version 25.10)
        options.setExportEditableCharts(true);

        // Step 4: Save the workbook as a DOCX document with the configured options
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

**Beklenen çıktı**

* Belirtilen dizinde `ChartEditable.docx` adlı bir dosya.  
* Dosyayı Word'de açtığınızda grafik, Excel'de göründüğü gibi gösterilir ve grafiğe çift tıklayarak veri serisini düzenleyebilirsiniz.

## Yaygın tuzaklar ve nasıl önlenir

| Belirti | Neden | Çözüm |
|---------|-------|-----|
| Word, düzenlenebilir grafik yerine **statik bir görüntü** gösteriyor | `setExportEditableCharts` çağrılmadı veya 25.10'dan düşük bir sürüm kullanılıyor | Bayrağın `true` olarak ayarlandığından ve Aspose.Cells 25.10 veya daha yeni bir sürümde olduğunuzdan emin olun. |
| Oluşturulan DOCX **boş** | Kaynak çalışma kitabının dosya yolu hatalı veya yeterli izin yok | Çalışma kitabı yolunu ve uygulamanın okuma/yazma erişimini doğrulayın. |
| Grafik düzeni **bozulmuş** görünüyor | Excel'deki sayfa ayarı (ör. gizli satırlar/sütunlar) Word'ün varsayılanlarından farklı | `ImageOrPrintOptions`'ı (ör. `setOnePagePerSheet(true)`) ayarlayarak ölçeklemeyi kontrol edin. |
| **Performans** büyük çalışma kitaplarında düşüyor | Birçok grafik veya büyük veri setleri dışa aktarılıyor | Yalnızca gerekli sayfaları dışa aktarın veya işleme sınırlamak için `setSheetIndex` kullanın. |

## Çözümü genişletmek

* **Birden fazla grafik:** Tüm çalışma sayfalarını döngüyle gezerek `worksheet.getCharts()` çağırın ve her grafiği ayrı ayrı dışa aktarın.  
* **Özel DOCX stilizasyonu:** Kaydettikten sonra, Aspose.Words kullanarak oluşturulan belgeye başlık, altbilgi veya stiller uygulayın.  
* **Toplu dönüşüm:** Kodu, bir dizindeki `.xlsx` dosyalarını işleyen bir döngüye sarın ve her biri için bir DOCX üretin.  

## Sonuç

Artık **export chart to docx** ve **convert Excel workbook to docx** işlemlerini grafiğin tam düzenlenebilirliğini koruyarak yapabileceğiniz güvenilir bir yönteme sahipsiniz. Temel adımlar; çalışma kitabını yüklemek, DOCX için `ImageOrPrintOptions`'ı yapılandırmak, `ExportEditableCharts`'ı etkinleştirmek ve sonucu kaydetmek.

Sayfa kenar boşluklarını ayarlama veya çalışma kitabının formüllerini gömme gibi ek seçeneklerle denemeler yaparak çıktıyı raporlama iş akışınıza göre özelleştirin. Excel verilerinden programlı olarak Word raporları üretmeniz gerektiğinde, bu yaklaşım temiz ve sürdürülebilir bir çözüm sunar.

--- 

*Denemeye hazır mısınız? Örneği klonlayın, dosya yollarını güncelleyin ve programı çalıştırın. Herhangi bir sorunla karşılaşırsanız, Aspose.Cells for Java belgelerine bakın veya aşağıdaki ilgili konuları inceleyin.*  

### Sonraki keşfedebileceğiniz ilgili konular

* **excel çalışma kitabını pdf'ye dönüştür** – aynı çalışma kitabından PDF raporları oluşturun.  
* **Aspose.Cells grafik biçimlendirme** – dışa aktarmadan önce renkleri, işaretçileri ve eksenleri özelleştirin.  
* **Aspose.Words ile DOCX'e resim gömme** – grafikleri diğer Word içerikleriyle birleştirin.  

İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells for Java kullanarak Trendline ile Excel Grafiği Oluşturma ve Görüntü Olarak Dışa Aktarma](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells Java ile Excel Grafik Erişimini Otomatikleştirme: Adım Adım Kılavuz](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Aspose.Cells for Java kullanarak Excel Grafik Veri Etiketlerini Özelleştirme: Adım Adım Kılavuz](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}