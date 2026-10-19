---
category: general
date: 2026-08-14
description: Aspose.Cells kullanarak Excel'i SVG'ye dışa aktarırken SVG'ye yazı tiplerini
  gömün. Yazdırma alanını nasıl ayarlayacağınızı, yazdırma seçeneklerini nasıl belirleyeceğinizi
  ve WRAPCOLS işlevini nasıl kullanacağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: tr
lastmod: 2026-08-14
og_description: Aspose.Cells ile Excel'i SVG'ye dışa aktarırken SVG'ye yazı tiplerini
  gömün. Bu rehber, yazdırma alanını nasıl ayarlayacağınızı, yazdırma seçeneklerini
  nasıl yapılandıracağınızı ve WRAPCOLS işlevini nasıl uygulayacağınızı gösterir.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Excel'i SVG'ye dışa aktarırken SVG'ye fontları göm – adım adım
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Excel'i SVG olarak dışa aktarırken SVG'ye yazı tiplerini göm
url: /tr/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i SVG'ye dışa aktarırken SVG'ye yazı tiplerini gömme

Eğer **Excel'i SVG'ye dışa aktarırken SVG'ye yazı tiplerini gömmeniz** gerekiyorsa, bu öğretici Aspose.Cells for Java ile bunu tam olarak nasıl yapacağınızı gösterir. Ayrıca **yazdırma alanını ayarlama**, **yazdırma seçeneklerini ayarlama** ve **WRAPCOLS işlevini kullanma** konularını da kapsayarak verileri düzeni kaybetmeden biçimlendireceksiniz.

Mevcut bir çalışma kitabını yükleyen, `WRAPCOLS` formülünü uygulayan, SVG'ye özgü görüntü seçeneklerini yapılandıran, yazdırma bölgesini tanımlayan ve sonunda dosyayı gömülü yazı tipleriyle bir SVG olarak kaydeden tam, çalıştırılabilir bir örnek üzerinden ilerleyeceksiniz. Harici bir belgeye gerek yok—sadece kodu kopyalayın, çalıştırın ve oluşan SVG'yi inceleyin.

## SVG'ye Yazı Tipi Gömme – ImageOrPrintOptions yapılandırması

Yazı tiplerini gömmek, SVG'nin Excel'de göründüğü gibi tam olarak render edilmesini sağlar, hatta orijinal tipografi yüklü olmayan makinelerde bile.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Neden önemli*: `setEmbedFonts(true)` etkinleştirildiğinde, Aspose.Cells yazı tipi verilerini doğrudan SVG'nin `<defs>` bölümüne yazar. Sonuç, tarayıcılar ve platformlar arasında aynı görünüme sahip, bağımsız bir dosyadır.

## Excel'i SVG'ye Dışa Aktarma – Tam İş Akışı

Aşağıdaki adımlar, çalışma kitabını yüklemekten SVG dosyasını kaydetmeye kadar uçtan uca süreci gösterir.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Beklenen çıktı**: `output.svg`, `YOUR_DIRECTORY` içinde görünür. Bir tarayıcıda açtığınızda, tüm yazı tipleri gömülü çalışma sayfası, `WRAPCOLS` sayesinde üç sütuna sarılmış veri ve yalnızca `A1:H30` içindeki hücreler render edilmiş olarak gösterilir.

## Çalışma Sayfası İçin Yazdırma Alanını Ayarlama

Yazdırma alanı tanımlamak, dışa aktarılan SVG'yi belirli bir aralıkla sınırlar; bu da dosya boyutunu azaltır ve izleyiciyi ilgili verilere odaklar.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*İpucu*: Aralık, Excel'in A1 notasyonunu takip eder. Dinamik bir aralığa ihtiyacınız varsa, bunu programlı olarak `ws.getCells().getMaxDisplayRange()` ile hesaplayabilirsiniz.

## SVG Çıktısı İçin Yazdırma Seçeneklerini Ayarlama

Yazdırma seçenekleri, Aspose.Cells'in çalışma sayfasını bir görüntüye nasıl dönüştürdüğünü kontrol eder. Yazı tiplerini gömmeye ek olarak, çözünürlük, ölçekleme ve sayfa düzenini ayarlayabilirsiniz.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Neden yazdırma seçeneklerini ayarlamalısınız*: Açık seçenekler belirtilmezse, Aspose.Cells yazı tipi gömülmesini atlayabilecek veya istenmeyen bir ölçekleme faktörü uygulayabilecek varsayılanları kullanır; bu da bulanık veya hatalı stillendirilmiş SVG'lere yol açar.

## Sütun Verilerini Sarmak İçin WRAPCOLS İşlevini Kullanma

`WRAPCOLS`, dikey bir aralığı belirli sayıda sütuna dağıtan bir Excel formülüdür. Uzun bir listeyi kompakt bir ızgarada göstermek istediğinizde kullanışlıdır.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Çalışma kitabı kaydedildiğinde, Aspose.Cells formülü değerlendirir ve tanımlı yazdırma alanı içinde üç sütunlu bir düzen üretir. Bu teknik, herhangi bir boyuttaki aralık için çalışır—sadece ikinci argümanı istediğiniz sütun sayısına göre ayarlayın.

## Tam Çalıştırılabilir Örnek

Aşağıda, herhangi bir IDE'ye yapıştırabileceğiniz tam Java programı bulunmaktadır. Aspose.Cells for Java kütüphanesinin sınıf yolunuzda (classpath) olduğundan emin olun.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Doğrulama adımları**

1. Programı çalıştırın.  
2. `output.svg` dosyasını bir web tarayıcısında açın.  
3. Metnin, orijinal Excel dosyasındakiyle aynı yazı tipini kullandığını (yazı tipleri gömülü) doğrulayın.  
4. Yalnızca `A1:H30` içindeki hücrelerin göründüğünü ve `A2:A10` verilerinin üç sütunda gösterildiğini kontrol edin.

## Yaygın tuzaklar ve nasıl önlenir

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| SVG'de yazı tipleri eksik | `setEmbedFonts(false)` veya yazı tipi dosyasına erişilememesi | `setEmbedFonts(true)` ayarlandığından ve yazı tipinin kodu çalıştıran makinede yüklü olduğundan emin olun |
| WRAPCOLS değerlendirilmedi | Hesaplama motoru devre dışı | Dışa aktarmadan önce `workbook.calculateFormula()` çağırın veya Aspose.Cells'in kaydetme sırasında değerlendirmesine izin verin |
| Dışa aktarılan SVG boş | Yazdırma alanı herhangi bir veri içermiyor | `setPrintArea`'ye geçirilen aralığı iki kez kontrol edin |
| SVG dosyası çok büyük | Ölçekleme uygulanmadı, yüksek görüntü çözünürlüğü | `imgOptions.setResolution(96)` gibi DPI kontrolü yaparak çözünürlüğü ayarlayın |

## Pro ipucu: Birden fazla çalışma sayfası için ImageOrPrintOptions'ı yeniden kullanma

Çalışma kitabınızda aynı SVG ayarlarına ihtiyaç duyan birden fazla sayfa varsa, tek bir `ImageOrPrintOptions` örneği oluşturup bunu her çalışma sayfasının `PageSetup`'ına atayın. Bu, bellek tüketimini azaltır ve tüm dışa aktarılan dosyalarda tutarlı yazı tipi gömme garantisi verir.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Sonraki Adımlar

* **Diğer vektör formatlarına dışa aktar** – Yüksek kaliteli PDF'ler için `ImageFormat.SVG` yerine `ImageFormat.PDF` kullanın.  
* **Toplu işleme** – `.xlsx` dosyalarından oluşan bir klasörü döngüye alarak SVG'leri otomatik olarak oluşturun.  
* **Özel yazı tipi yönetimi** – Sistem yazı tipleri yetersiz olduğunda belirli bir dizinden yazı tiplerini yüklemek için `FontSettings` kullanın.  

**SVG'ye yazı tipi gömme**, **excel'i svg'ye dışa aktarma**, **yazdırma alanını ayarlama**, **yazdırma seçeneklerini ayarlama** ve **WRAPCOLS işlevini kullanma** konularında uzmanlaşarak, Excel verilerinden doğrudan raporlar, gösterge panelleri ve web görselleştirmeleri için yüksek doğruluklu SVG üretimini otomatikleştirebilirsiniz. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [Aspose.Cells for .NET Kullanarak Excel'de Yazdırma Alanı Nasıl Ayarlanır](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Excel'de Yazdırma Alanı Ayarlama – Aspose Cells .NET](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Excel'de Yazdırma Alanı Ayarlama – Aspose Cells .NET](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}