---
category: general
date: 2026-07-16
description: Java'da Aspose.Cells kullanarak Excel'i TXT'ye aktarın. Önemli basamakları
  nasıl ayarlayacağınızı, Excel'i metin dosyası olarak nasıl kaydedeceğinizi ve çıktı
  formatını nasıl kontrol edeceğinizi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set significant digits
- save excel as text file
- save workbook as txt
language: tr
lastmod: 2026-07-16
og_description: Aspose.Cells ile Java’da Excel’i TXT’ye aktarın. Bu öğreticide, anlamlı
  basamakları nasıl ayarlayacağınızı, Excel’i metin dosyası olarak nasıl kaydedeceğinizi
  ve güvenilir sonuçlar almayı gösterir.
og_image_alt: Screenshot of Java code exporting an Excel workbook to a TXT file with
  4 significant digits
og_title: Java'da Excel'i TXT'ye Dışa Aktarma – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  headline: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  name: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java Development Kit (JDK) 8 or newer. - Maven or Gradle to manage the
      Aspose.Cells dependency (we’ll show the Maven snippet). - A basic understanding
      of Java syntax (if you’ve written a “Hello World”, you’re good).'
  - name: Understanding `setSignificantDigits`
    text: '- **Definition:** The number of digits that remain after the decimal point,
      *including* leading digits. For `123.456789` with `4` significant digits, the
      output becomes `123.5`. - **When to use:** If the downstream system expects
      a fixed precision (e.g., scientific data files), or you need to trunca'
  - name: Folder Considerations
    text: '- The `output` folder must exist, or you’ll get an `IOException`. You can
      create it programmatically:'
  - name: 1️⃣ What if I need a different delimiter?
    text: "`TxtSaveOptions` also offers `setSeparator('\t')` for tabs or `setSeparator(',')`
      for CSV‑style output. Example:"
  - name: 2️⃣ How does locale affect decimal separators?
    text: 'By default Aspose uses the system locale. If you need a period (`.`) regardless
      of locale, set:'
  - name: 3️⃣ Large worksheets – memory concerns?
    text: Aspose.Cells streams data to disk when working with worksheets larger than
      1 GB, so you usually won’t hit an `OutOfMemoryError`. Still, avoid loading massive
      sheets into memory if you only need a subset; use `Workbook.getWorksheets().get(index)`
      to target a specific sheet.
  - name: 4️⃣ Can I export only a range?
    text: Yes. Use `txtOptions.setExportRange("A1:B10")` to restrict the output to
      a specific area. This reduces file size and speeds up the export.
  - name: 5️⃣ What if I don’t have a license?
    text: The evaluation mode adds a watermark line (`"Aspose.Cells for Java Evaluation
      Version"`). For production you’ll need a license; otherwise the watermark may
      break downstream parsers.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java ile Excel'i TXT'ye Dışa Aktarma – Tam Adım Adım Kılavuz
url: /tr/java/excel-import-export/export-excel-to-txt-with-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i TXT'ye Java ile Dışa Aktarma – Tam Adım‑Adım Kılavuz

Hiç **Excel'i TXT'ye nasıl dışa aktaracağınızı** sayısal hassasiyeti kaybetmeden merak ettiniz mi? Belki eski bir sistem için düz metin dökümüne ihtiyacınız var ya da belirli bir anlamlı basamak sayısı bekleyen bir bilimsel veri hattına veri besliyorsunuz. Bu öğreticide **tam, çalıştırılabilir bir Java örneği** üzerinden bunu gösterecek, ayrıca **anlamlı basamakları nasıl ayarlayacağınızı**, **Excel'i metin dosyası olarak nasıl kaydedeceğinizi** ve **çalışma kitabını txt olarak nasıl kaydedeceğinizi** Aspose.Cells kullanarak anlatacağız.

Projeyi kurulumundan son doğrulama adımına kadar her şeyi ele alacağız, böylece kodu kopyalayıp yapıştırabilir, çalıştırabilir ve sonucu anında görebilirsiniz. Gizli bağımlılıklar yok, “belgelere bak” kısayolları yok—sadece net, uçtan uca bir çözüm.

---

## Öğrenecekleriniz

- Aspose.Cells ile programatik olarak bir çalışma kitabı oluşturmayı.
- TXT dışa aktarımı için **anlamlı basamakları ayarlama** API çağrısını.
- `TxtSaveOptions` ile diğer kaydetme seçenekleri arasındaki farkı.
- **Excel'i metin dosyası olarak** herhangi bir işletim sisteminde (Windows, macOS, Linux) kaydetmeyi.
- Yaygın tuzaklar (yerel ayara özgü ondalık ayırıcılar, büyük çalışma sayfaları) ve bunlardan nasıl kaçınılacağını.
- Kendi projelerinize uyarlayabileceğiniz tam, çalıştırılabilir bir Java sınıfı.

### Önkoşullar

- Java Development Kit (JDK) 8 veya daha yeni bir sürüm.
- Aspose.Cells bağımlılığını yönetmek için Maven ya da Gradle (Maven örneğini göstereceğiz).
- Java sözdizimi hakkında temel bir anlayış (eğer “Hello World” yazdıysanız yeterli).

---

## Adım 1: Projeyi Kurun ve Aspose.Cells'i Ekleyin

İlk olarak kütüphaneyi derlemeye ekleyelim. Maven kullanıyorsanız `pom.xml` dosyanıza şunu ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **İpucu:** Aspose ücretsiz 30‑günlük bir değerlendirme lisansı sunar. `Aspose.Total.lic` dosyasını proje kök dizinine koyun ya da herhangi bir API kullanımından önce `License.setLicense("path/to/license")` çağrısını yapın.

Bağımlılık çözüldükten sonra kodlamaya başlayabilirsiniz. Gradle tercih ediyorsanız eşdeğeri şu şekildedir:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

---

## Adım 2: Excel'i TXT'ye Dışa Aktarın – Bir Çalışma Kitabı Oluşturun

Şimdi yeni bir çalışma kitabı oluşturacağız, sayısal bir değer ekleyeceğiz ve dışa aktarma için hazırlayacağız. Bu, **export excel to txt** işleminin kalbidir.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fresh workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet – it's created by default
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 3️⃣ Put a numeric value into cell A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue(123.456789); // Example number with many decimals
```

**Neden önemli:** Çalışma kitabını kod içinde oluşturduğumuzda, şablon dosyasından gelebilecek gizli biçimlendirmelerden kaçınmış oluruz. `putValue` metodu veri tipini otomatik algılar, böylece hücre **sayısal** bir hücre olur—string değil.

---

## Adım 3: TXT Çıktısı İçin Anlamlı Basamakları Nasıl Ayarlarsınız

Düz metne dışa aktardığınızda, Aspose.Cells varsayılan olarak ham sayısal değeri yazar. Çıktıyı örneğin **4 anlamlı basamak** ile sınırlamak için `TxtSaveOptions`'ı değiştirmeniz gerekir.

```java
        // 4️⃣ Configure TXT save options – this is where we set the precision
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4); // <-- controls significant digits
```

### `setSignificantDigits` Anlamak

- **Tanım:** Ondalık nokta sonrası kalan basamak sayısı, *öncü basamaklar dahil*. `123.456789` sayısı için `4` anlamlı basamak verildiğinde çıktı `123.5` olur.
- **Ne zaman kullanılmalı:** Alt sistem sabit bir hassasiyet bekliyorsa (ör. bilimsel veri dosyaları) ya da kayan nokta gürültüsünü azaltmak için kırpma yapmanız gerekiyorsa.
- **Köşe durumu:** Sayının basamak sayısı belirtilen değerden az ise Aspose orijinal değeri korur (sıfırlarla doldurmaz).

> **Neden `setDecimalPlaces` kullanılmaz?** Bu özellik sadece ondalık nokta sonrası basamakları kontrol eder, öncü basamakları göz ardı eder. Bilimsel verilerde genellikle `significantDigits` doğru seçimdir.

---

## Adım 4: Excel'i Metin Dosyası (TXT) Olarak Kaydedin

Seçenekler hazır olduğunda, çalışma kitabını bir `.txt` dosyasına yazıyoruz. Bu, **save workbook as txt** adımıdır.

```java
        // 5️⃣ Persist the workbook as a TXT file
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Excel exported to TXT at: " + outputPath);
    }
}
```

### Klasör Dikkat Edilmesi Gerekenler

- `output` klasörü mevcut olmalı, aksi takdirde `IOException` alırsınız. Programatik olarak şu şekilde oluşturabilirsiniz:

```java
new java.io.File("output").mkdirs();
```

- Linux/macOS'ta yollar büyük/küçük harfe duyarlıdır; Windows'ta değildir. Çapraz platform güvenliği için klasör adlarını küçük harfle tutun.

---

## Adım 5: Sonucu Doğrulayın

Programı çalıştırın (`mvn compile exec:java -Dexec.mainClass=ExportExcelToTxtDemo`) ve `output/SignificantDigits.txt` dosyasını açın. Şu satırı görmelisiniz:

```
123.5
```

Bu tek satır şunları kanıtlar:

- Çalışma kitabı **metin dosyası olarak başarıyla kaydedildi**.
- Sayısal değer, ayarladığımız **4 anlamlı basamağa** uymaktadır.
- Dosyaya ekstra virgül, sekme ya da Excel‑özel meta verisi sızmamıştır.

Birden fazla sütun için sekme‑ayırmalı bir düzen isterseniz, sadece daha fazla hücre doldurun; Aspose otomatik olarak sekmeleri ekleyecektir.

---

## Yaygın Sorular & Köşe Durumları

### 1️⃣ Farklı bir ayırıcıya ihtiyacım olursa?

`TxtSaveOptions` ayrıca sekmeler için `setSeparator('\t')` ya da CSV‑stil çıktı için `setSeparator(',')` sunar. Örnek:

```java
txtOptions.setSeparator('\t'); // Tab delimiter
```

### 2️⃣ Yerel ayar ondalık ayırıcıyı nasıl etkiler?

Varsayılan olarak Aspose sistem yerel ayarını kullanır. Yerel ayardan bağımsız olarak nokta (`.`) kullanmak isterseniz şunu ayarlayın:

```java
txtOptions.setCultureInfo(java.util.Locale.US);
```

### 3️⃣ Büyük çalışma sayfaları – bellek kaygıları?

Aspose.Cells, 1 GB'den büyük çalışma sayfalarıyla çalışırken veriyi diske akıtır, bu yüzden genellikle `OutOfMemoryError` ile karşılaşmazsınız. Yine de sadece bir alt küme gerekiyorsa devasa sayfaları belleğe yüklemekten kaçının; belirli bir sayfayı hedeflemek için `Workbook.getWorksheets().get(index)` kullanın.

### 4️⃣ Sadece bir aralığı dışa aktarmak mümkün mü?

Evet. Çıktıyı belirli bir alana sınırlamak için `txtOptions.setExportRange("A1:B10")` kullanın. Bu, dosya boyutunu azaltır ve dışa aktarma süresini hızlandırır.

### 5️⃣ Lisansım yoksa ne olur?

Değerlendirme modu bir filigran satırı ekler (`"Aspose.Cells for Java Evaluation Version"`). Üretim ortamında bir lisansa ihtiyacınız olacak; aksi takdirde filigran alt sistem ayrıştırıcılarını bozabilir.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Ensure output directory exists
        new File("output").mkdirs();

        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 2️⃣ Put several numbers to illustrate formatting
        sheet.getCells().get("A1").putValue(123.456789);
        sheet.getCells().get("A2").putValue(0.0012345);
        sheet.getCells().get("A3").putValue(98765.4321);

        // 3️⃣ Configure TXT options – 4 significant digits, tab delimiter
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4);
        txtOptions.setSeparator('\t'); // optional, defaults to tab
        txtOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator

        // 4️⃣ Save as TXT
        String outPath = "output/SignificantDigits.txt";
        workbook.save(outPath, txtOptions);

        System.out.println("Export completed: " + outPath);
    }
}
```

Yukarıdaki kodu çalıştırdığınızda `output/SignificantDigits.txt` şu şekilde oluşur:

```
123.5
0.001235
98770
```

Her sayının **4 anlamlı basamak** kuralına uyduğuna, çok küçük ve çok büyük değerler dahil, dikkat edin.

---

## Sonuç

Java ve Aspose.Cells kullanarak **Excel'i TXT'ye dışa aktarmanın** tam, bağımsız bir yolunu gösterdik; **anlamlı basamakları nasıl ayarlayacağınızı**, **excel'i metin dosyası olarak nasıl kaydedeceğinizi** ve **çalışma kitabını txt olarak nasıl kaydedeceğinizi** kapsadık. Özetle:

- Sayısal hassasiyeti kontrol etmek için `TxtSaveOptions.setSignificantDigits` kullanın.
- Gerektiğinde ayırıcıları, kültürü ve dışa aktarma aralıklarını ayarlayın.
- Kod herhangi bir platformda çalışır, tek bir kütüphane gerektirir ve temiz, boşluk‑ayırmalı metin üretir; bu da sonraki işlem adımları için hazırdır.

Bir sonraki adıma hazır mısınız? Birden fazla sütun ekleyin, farklı ayırıcılarla deney yapın ya da dışa aktarmayı daha büyük bir ETL hattına entegre edin. Bir sorunla karşılaşırsanız—örneğin yerel ayar problemi ya da devasa bir sayfa—yukarıdaki “Yaygın Sorular & Köşe Durumları” bölümüne geri dönün.

Paylaşmak istediğiniz bir kullanım senaryosu var mı? Yorum bırakın, ya da depoyu fork edip bir pull request gönderin. Mutlu kodlamalar ve elektronik tabloları düz metne dönüştürmenin sadeliğinin tadını çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, kendi projelerinizde ek API özelliklerini ustalaşmanız ve alternatif uygulama yaklaşımlarını keşfetmeniz için adım‑adım açıklamalı tam çalışan kod örnekleri içerir.

- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}