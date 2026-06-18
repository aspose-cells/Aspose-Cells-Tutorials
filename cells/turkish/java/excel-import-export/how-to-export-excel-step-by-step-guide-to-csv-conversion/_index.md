---
category: general
date: 2026-06-18
description: Excel dosyalarını hızlıca dışa aktarmak – xlsx'i csv'ye dönüştürmeyi,
  aralığı csv'ye dışa aktarmayı ve Java kullanarak csv'yi dosyaya yazmayı öğrenin.
  Basit, güvenilir çözüm.
draft: false
keywords:
- how to export excel
- convert xlsx to csv
- write csv to file
- export range to csv
- export excel to csv
language: tr
og_description: Java’da Excel dosyalarını nasıl dışa aktarılır. xlsx’i csv’ye dönüştürme,
  aralığı csv’ye dışa aktarma ve çalıştırmaya hazır bir örnekle csv’yi dosyaya yazma.
og_title: Excel'i Nasıl Dışa Aktarılır – Tam CSV Dönüştürme Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: How to export Excel files quickly – learn to convert xlsx to csv, export
    range to csv, and write csv to file using Java. Simple, reliable solution.
  headline: 'How to Export Excel: Step‑by‑Step Guide to CSV Conversion'
  type: TechArticle
tags:
- Java
- Excel
- CSV
- File I/O
title: 'Excel''i Nasıl Dışa Aktarılır: CSV Dönüştürme İçin Adım Adım Rehber'
url: /tr/java/excel-import-export/how-to-export-excel-step-by-step-guide-to-csv-conversion/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i Nasıl Dışa Aktarılır: Tam CSV Dönüştürme Öğreticisi

Excel verilerini manuel olarak elektronik tabloyu açmadan **Excel'i nasıl dışa aktaracağınızı** hiç merak ettiniz mi? Tek başınıza değilsiniz—birçok geliştirici, bir *.xlsx* çalışma kitabını düz metin CSV dosyasına hızlı ve programatik bir şekilde dönüştürmenin yolunu arıyor. Bu rehberde bir Excel çalışma kitabını CSV'ye dönüştürmeyi, belirli bir aralığı dışa aktarmayı ve sonunda o CSV dizesini bir dosyaya yazmayı adım adım göstereceğiz. Sonunda bunu tam olarak yapan bağımsız bir Java kod parçacığına sahip olacaksınız.

Ayrıca, özel sayı ve tarih formatlarıyla **xlsx'i csv'ye dönüştürme** gibi faydalı ipuçlarını ve tüm sayfa yerine bir aralığı dışa aktarmayı neden tercih edebileceğinizi de ekleyeceğiz. Gereksiz ayrıntı yok, sadece herhangi bir projeye ekleyebileceğiniz pratik bir çözüm.

## Önkoşullar

Before we dive in, make sure you have:

- Java 17 veya daha yeni (kod modern `Files.writeString` API'sini kullanıyor).
- Java için Aspose.Cells kütüphanesi (veya `ExportTableOptions` sağlayan herhangi bir uyumlu kütüphane). Maven Central'dan alabilirsiniz:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

- Basit bir Excel dosyası (`input.xlsx`) kontrol ettiğiniz bir klasöre yerleştirilmiş ( `YOUR_DIRECTORY` ifadesini gerçek yol ile değiştirin).

Bunlar hazır mı? Harika—haydi başlayalım.

## Adım 1: Dışa Aktarma Seçeneklerini Ayarlama (Aralığı CSV'ye Dışa Aktar)

İlk yapmanız gereken, kütüphaneye **Excel'i nasıl dışa aktaracağını** söylemektir. `ExportTableOptions` tek bir düzenli nesnede dize çıktısı, sayı biçimlendirmesi ve tarih biçimlendirmesi tanımlamanızı sağlar.

```java
// Configure export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);               // Export as a plain string
exportOptions.setNumberFormat("#,##0.00");           // Two‑decimal numbers
exportOptions.setDateFormat("yyyy-MM-dd");           // ISO‑style dates
```

> **Neden önemli:** Dışa aktarmayı bir dize olarak yaparak ara bayt akışlarıyla uğraşmazsınız ve özel formatlar CSV'nin tam istediğiniz gibi görünmesini sağlar—özellikle daha sonra **csv'yi dosyaya yazdığınızda**.

## Adım 2: Çalışma Kitabını Yükleme (XLSX'i CSV'ye Dönüştürme)

Sonra, kaynak çalışma kitabını açın. Bu, aslında **xlsx'i csv'ye dönüştürdüğümüz** noktadır—dönüştürme daha sonra gerçekleşir, ancak dosyayı yüklemek ilk adımdır.

```java
// Load the workbook from disk
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Grab the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);
```

Farklı bir sayfayla çalışmanız gerekiyorsa, sadece dizini değiştirin veya `get("SheetName")` kullanın. Kütüphane hem `.xlsx` hem de eski `.xls` formatlarını destekler, böylece çoğu senaryo için hazırsınız.

## Adım 3: Belirli Bir Aralığı Dışa Aktarma (Aralığı CSV'ye Dışa Aktar)

Genellikle tüm sayfaya ihtiyacınız olmaz—belki sadece `A1:D10` hücrelerindeki satış tablosu. İşte **export range to csv** burada devreye girer. Metot, CSV verisini içeren tek bir `String` döndürür.

```java
// Export the range A1:D10 as a CSV string using the options defined above
String csvData = worksheet.getCells()
                          .exportTableAsString("A1:D10", exportOptions);
```

> **Pro ipucu:** Aralık dizesi Excel'in A1 notasyonunu izler, böylece bunu `"B2:F20"` gibi kolayca ayarlayabilir veya çalışma zamanında hesapladığınız herhangi bir dinamik aralığa dönüştürebilirsiniz.

## Adım 4: CSV Dizesini Bir Dosyaya Yazma (CSV'yi Dosyaya Yazma)

Şimdi CSV metni bellekte olduğuna göre, son adım onu kalıcı hale getirmektir. Java 11+ bunu `Files.writeString` ile tek satırda yapar.

```java
// Write the CSV string to an output text file
Files.writeString(Paths.get("YOUR_DIRECTORY/output.txt"), csvData);
```

Dosya mevcut değilse oluşturulur, mevcutsa üzerine yazılır—günlük raporları yeniden üreten toplu işler için mükemmeldir.

## Adım 5: Çıktıyı Doğrulama (Excel'i CSV'ye Dışa Aktarma)

Hızlı bir mantık kontrolü saatler süren hata ayıklamayı önler. `output.txt` dosyasını herhangi bir metin düzenleyicide açın veya dönüşümün başarılı olduğunu doğrulamak için Excel'e geri aktarın.

```text
Product,Quantity,Price,Total
Widget A,10,12.50,125.00
Widget B,5,8.75,43.75
...
```

Sayilar iki ondalık basamakla ve tarih `yyyy‑MM‑dd` biçiminde görünüyorsa, istediğiniz formatlamayla **export excel to csv** işlemini başarıyla gerçekleştirmişsiniz demektir.

## Kenar Durumları ve Yaygın Tuzaklar

- **Büyük çalışma sayfaları:** Tüm sayfayı dışa aktarmak çok fazla bellek tüketebilir. Mümkün olduğunca belirli bir aralığa bağlı kalın.
- **Özel karakterler:** CSV virgülü ayırıcı olarak kullanır; verinizde virgül varsa alanı çift tırnak içinde sarın (`"value, with comma"`). Çoğu kütüphane bunu otomatik olarak halleder, ancak bozuk satırlar görürseniz iki kez kontrol edin.
- **Kodlama:** `Files.writeString` varsayılan olarak UTF‑8 kullanır. Farklı bir karakter setine (ör. Windows‑1252) ihtiyacınız varsa, bir `Charset` argümanı geçirin.
- **Boş hücreler:** CSV çıktısında boş string olarak görünür—sabit bir sütun sayısına bağlı değilseniz endişelenecek bir şey yok.

## Tam, Çalıştırmaya Hazır Örnek

Aşağıda kopyalayıp yapıştırıp çalıştırabileceğiniz tam Java sınıfı bulunmaktadır. `YOUR_DIRECTORY` ifadesini makinenizdeki gerçek klasör yolu ile değiştirin.

```java
import com.aspose.cells.*;
import java.nio.file.*;

public class ExcelToCsvExporter {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Configure export options
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setNumberFormat("#,##0.00");
        exportOptions.setDateFormat("yyyy-MM-dd");

        // 2️⃣ Load the workbook (convert xlsx to csv later)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Export the desired range (export range to csv)
        String csvData = worksheet.getCells()
                                  .exportTableAsString("A1:D10", exportOptions);

        // 4️⃣ Write the CSV string to a file (write csv to file)
        Path outputPath = Paths.get("YOUR_DIRECTORY/output.txt");
        Files.writeString(outputPath, csvData);

        // 5️⃣ Simple verification message
        System.out.println("✅ CSV export complete! File saved to: " + outputPath);
    }
}
```

**Beklenen konsol çıktısı**

```
✅ CSV export complete! File saved to: /path/to/YOUR_DIRECTORY/output.txt
```

Oluşturulan `output.txt` dosyasını açın ve seçilen aralığın temiz, virgülle ayrılmış bir görünümünü görmelisiniz.

## Sonuç

**Excel'i CSV'ye nasıl dışa aktaracağınızı** temiz ve tekrarlanabilir bir şekilde ele aldık: dışa aktarma seçeneklerini yapılandırın, çalışma kitabını yükleyin, belirli bir aralığı dışa aktarın ve sonunda **csv'yi dosyaya yazın**. Bu yaklaşım sayı ve tarih formatları üzerinde tam kontrol sağlar, böylece ortaya çıkan **export excel to csv** dosyası sonraki sistemler için hazır olur.

Sonraki adımda şunları keşfedebilirsiniz:

- Tek bir çalıştırmada birden fazla aralığı dışa aktarma (adlandırılmış aralıklar üzerinde döngü).
- Tercih edilen yerel ayarlar için farklı bir ayırıcı (noktalı virgül) kullanma.
- CSV'yi doğrudan bir HTTP yanıtına akıtma, web tabanlı indirmeler için.

Deneyin, aralığı ayarlayın ve CSV oluşturmayı Java araç kutunuzun sorunsuz bir parçası haline getirin. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Export Excel to CSV with Blank Rows Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/german/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)
- [Export Excel Csv Blank Rows Aspose Cells Net](/cells/french/net/workbook-operations/export-excel-csv-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}