---
category: general
date: 2026-07-16
description: Aspose.Cells kullanarak Excel tablosunu TXT'ye dışa aktarırken özel hücre
  ayırıcı ayarlayın. Excel formüllerini metne nasıl dışa aktaracağınızı ve çalışma
  sayfasını txt dosyası olarak nasıl kaydedeceğinizi öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: tr
lastmod: 2026-07-16
og_description: Aspose.Cells'te özel hücre ayırıcı ayarlamak, Excel tablosunu tam
  formatlamayla TXT'ye dışa aktarmanızı sağlar. Excel formüllerini metne dışa aktarın
  ve çalışma sayfasını kolayca txt dosyası olarak kaydedin.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Özel Hücre Ayırıcı Ayarla – Excel Tablosunu TXT'ye Aktar
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Özel Hücre Ayırıcıyı Ayarla – Excel Tablosunu TXT'ye Dışa Aktar
url: /tr/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Özel Hücre Ayırıcı Ayarla – Excel Tablosunu TXT’ye Dışa Aktar

Özel hücre ayırıcı, bir Excel sayfasından düzenli bir metin dökümü elde etmek istediğinizde ihtiyacınız olan gizli sosdur. **excel tablosunu txt’ye dışa aktarma** işlemini virgül ve satır sonu karışıklığı olmadan nasıl yapacağınızı hiç merak ettiniz mi? Bu öğreticide, bir çalışma kitabını yüklemekten **çalışma sayfasını txt dosyası olarak kaydetme** ve istediğiniz ayırıcıyı kullanmaya kadar tüm süreci Aspose.Cells for Java ile adım adım inceleyeceğiz.

## Öğrenecekleriniz

- Metin dışa aktarımları için **özel hücre ayırıcı ayarlama**.
- **excel formüllerini metne dışa aktarma** adımları, böylece değerlendirilen sonuçlar da dışa aktarılır.
- **excel verilerini düz metin olarak dışa aktarma** ve düzeni koruma yolları.
- Projenize kopyalayıp yapıştırabileceğiniz, çalıştırmaya hazır tam bir kod örneği.

Bu rehberi tamamladığınızda, herhangi bir Excel çalışma kitabını alıp bir boru (`|`), sekme (`\t`) ya da istediğiniz herhangi bir karakterle temiz, ayırıcıyla bölünmüş bir metin dosyasına dönüştürebileceksiniz; bu dosyalar sonraki sistemler tarafından sevilecek.

### Önkoşullar

- Java 8 veya daha yeni bir sürüm yüklü.
- Aspose.Cells for Java kütüphanesini çekmek için Maven (veya herhangi bir build aracı).
- Formüller içeren bir tabloyu barındıran örnek çalışma kitabı (`TableDemo.xlsx`).

Eğer bunlara sahipseniz, ekstra süssiz, sadece pratik adımlarla ilerleyelim.

## Adım 1: Aspose.Cells’i Projenize Ekleyin

**özel hücre ayırıcı ayarlamadan** önce, sınıf yolunda Aspose.Cells JAR dosyasının bulunması gerekir. En kolay yol Maven kullanmaktır:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Gradle tercih ediyorsanız, XML’i eşdeğer `implementation 'com.aspose:aspose-cells:24.10'` ifadesiyle değiştirin. Bağımlılık çözüldükten sonra, Excel dosyalarıyla iletişim kuran Java kodunu yazmaya hazırsınız.

## Adım 2: Çalışma Kitabını Yükleyin – Excel Tablosunu TXT’ye Dışa Aktarmaya Hazırlık

İlk gerçek kod satırı her zaman aynıdır: dışa aktarmak istediğiniz tabloyu içeren çalışma kitabını açın.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Burada ilk çalışma sayfasını (`get(0)`) alıyoruz. Verileriniz farklı bir sayfada ise, indeks’i değiştirin ya da `get("SheetName")` kullanın. Bu adım, **excel tablosunu txt’ye dışa aktarma** için kritiktir çünkü dışa aktarıcı çalışma sayfası seviyesinde çalışır.

## Adım 3: Özel Hücre Ayırıcıyı Ayarla – Dışa Aktarmanın Çekirdeği

Şimdi gösterinin yıldızı: `ExportTableOptions` yapılandırması. Bu nesne, her hücrenin nihai metin dosyasında nasıl görüneceğini tam olarak belirlemenizi sağlar.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Neden **özel hücre ayırıcı ayarlıyoruz**? Çünkü varsayılan ayırıcı bir sekmedir ve zaten sekme içeren verilerle çakışabilir. Bir boru (`|`) ya da noktalı virgül seçerek, her sütunun aşağı akışta ayrıştırıcı tarafından ayrı tutulmasını garantilersiniz.

### Excel Formüllerini Metne Dışa Aktarma

`setFormulaValueInCell(true)` satırı, Aspose.Cells’in **excel formüllerini metne dışa aktarma** sırasında formülün *sonucu*nu, formül metninin kendisini değil, yazmasını sağlar. Bunu atlayıp `=SUM(A1:A5)` gibi bir hücreyi dışa aktarırsanız, TXT dosyasında `=SUM(A1:A5)` olarak görünecektir; bu genellikle istenen şey değildir.

## Adım 4: Dışa Aktarım Seçeneklerini TXT Kaydetme Seçeneklerine Bağlayın

Şimdi bu tablo seçeneklerini genel TXT dışa aktarma yapılandırmasına ekliyoruz.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` tüm çalışma sayfasının nasıl yazılacağını kontrol eden üst nesnedir. `exportTableOptions`ı ona takarak, sayfadaki her tablonun **özel hücre ayırıcı ayarlama** kuralına uymasını sağlarsınız.

## Adım 5: Çalışma Sayfasını TXT Dosyası Olarak Kaydet – Dışa Aktarmayı Tamamla

Son olarak dosyayı diske yazıyoruz.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

Bu programı çalıştırdığınızda `TableExported.txt` oluşturulur. Orijinal Excel tablosunun her satırı, şu şekilde bir boru‑ayırıcıyla ayrılmış değer satırı olarak görünür:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

**Toplam** sütunundaki formülün, `setFormulaValueInCell(true)` sayesinde yazılmadan önce değerlendirildiğine dikkat edin. İşte **excel verilerini düz metin olarak dışa aktarma** ve hesaplanmış sonuçları korumanın özü budur.

## Adım 6: Çıktıyı Doğrula – Görünümü Doğru mu?

Oluşturulan `TableExported.txt` dosyasını herhangi bir metin düzenleyicide açın. Şunları görmelisiniz:

- Excel satırı başına bir satır.
- `setCellValueSeparator` ile belirlediğiniz boru karakteriyle ayrılmış sütunlar.
- Orijinal hücre değerlerinin bir parçası olmadıkça rastgele virgül veya sekme yok.
- Formül sonuçları, formül metinleri değil.

Beklenmeyen karakterler görürseniz, seçtiğiniz ayırıcıyı tekrar kontrol edin. Boru gibi karakterler çoğu CSV‑tarzı ayrıştırıcı için güvenlidir, ancak verinizde zaten boru karakteri varsa, `~` ya da sekme (`\t`) gibi farklı bir ayırıcı düşünün.

## İpuçları, Kenar Durumları ve En İyi Uygulamalar – Excel Verilerini Düz Metin Olarak Dışa Aktarma

| Durum | Yapılması Gereken |
|-----------|------------|
| **Veri zaten seçtiğiniz ayırıcıyı içeriyorsa** | Daha az yaygın bir karaktere geçin (`^`, `~` veya Unicode görünmez karakterler). |
| **UTF‑8 kodlamasına ihtiyacınız varsa** | `TxtSaveOptions` içinde `setEncoding(Encoding.getUTF8())` kullanın. |

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan içeriklerdir. Her kaynak, adım adım açıklamalarla birlikte tam çalışan kod örnekleri sunar; böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}