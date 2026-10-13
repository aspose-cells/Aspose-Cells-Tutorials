---
category: general
date: 2026-03-01
description: Aspose.Cells for Java ile PDF oluşturma ve çalışma kitabını PDF olarak
  kaydetme, Excel'i HTML’ye dışa aktarma ve genişletme işlevini kullanma. Adım adım
  kod dahil.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: tr
og_description: Aspose.Cells for Java kullanarak bir çalışma kitabından PDF nasıl
  oluşturulur. Çalışma kitabını PDF olarak kaydetmeyi, Excel'i HTML’ye dışa aktarmayı
  ve EXPAND işlevini kullanmayı öğrenin.
og_title: Çalışma Kitabından PDF Oluşturma – Java Öğreticisi
tags:
- Aspose.Cells
- Java
- PDF generation
title: Bir Çalışma Kitabından PDF Oluşturma – Tam Java Rehberi
url: /tr/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bir Çalışma Kitabından PDF Oluşturma – Tam Java Rehberi

Hiç **PDF oluşturmayı** doğrudan bir Excel çalışma kitabından üçüncü‑taraf dönüştürücülerle uğraşmadan nasıl yapabileceğinizi merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, hızlı bir PDF dışa aktarımı, HTML önizlemesi veya şık dizi formüllerine aynı anda ihtiyaç duyduklarında bir çıkmaza giriyor.  

Bu öğreticide, tam olarak bunu yapan tek bir, bağımsız Java programını adım adım inceleyeceğiz. **Çalışma kitabını PDF olarak kaydedecek**, **Excel'i HTML’ye dışa aktarırken dondurulmuş satırları koruyacak** ve bir çalışma sayfası içinde **EXPAND işlevini** nasıl kullanacağınızı göstereceğiz. Sonunda, herhangi bir Maven ya da Gradle projesine ekleyebileceğiniz çalıştırılabilir bir proje elde edeceksiniz.

> **İpucu:** Aşağıdaki tüm kodlar Aspose.Cells 23.10 (veya daha yeni) sürümüyle çalışır. Daha eski bir sürüm kullanıyorsanız, bazı metot adları hafifçe farklı olabilir.

---

## Önkoşullar

- **Java 17** (veya herhangi bir LTS sürümü) yüklü ve yapılandırılmış.
- **Aspose.Cells for Java** kütüphanesi. `pom.xml` dosyanıza aşağıdaki Maven bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Tercih ettiğiniz bir IDE ya da metin editörü (IntelliJ IDEA, VS Code, Eclipse…).

Harici API’ler, web servisleri yok—sadece saf Java ve Aspose.Cells SDK’sı.

---

## Çözümün Genel Bakışı

Uygulamayı **yedi mantıksal adıma** böleceğiz:

1. Bir çalışma kitabı oluşturun ve **EXPAND** işlevini gösterin.  
2. Yazı tipi varyasyon seçicilerini etkinleştirin ve **çalışma kitabını PDF olarak kaydedin**.  
3. Aynı çalışma kitabını HTML’ye dışa aktarırken dondurulmuş satırları koruyun.  
4. Koşullu metin eklemek için bir `IF`‑parametresi içeren Smart Marker kullanın.  
5. Hiyerarşik veri için bir master‑detail Smart Marker uygulayın.  
6. Base‑64‑kodlu görüntüler içeren bir Markdown dosyası yükleyin.  
7. Hizalama ve kenarlıklar için GridJs seçeneklerini yapılandırın, ardından verileri ekleyin.

Her adım, `main` metodunu düzenli tutmak ve **ne** yaptığımızı değil, **neden** yaptığımızı göstermek için kendi metodunda sarılmıştır.

---

## Adım 1 – Bir Çalışma Kitabı Oluşturun ve EXPAND İşlevini Kullanın

**EXPAND** işlevi, Office 365’te tanıtılan yeni bir dinamik‑dizi formülüdür. Hücreleri manuel olarak kopyalamadan bir aralığı daha büyük bir alana yaymanıza olanak tanır.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Neden önemli:**  
- `EXPAND` sonucu boşluklarla otomatik doldurur; bu, **çalışma kitabını PDF olarak kaydettiğinizde** PDF’nin temiz, dikdörtgen bir tablo göstermesini sağlar.  
- `calculateFormula()` çağrısı, dışa aktarmadan önce formül motorunun çalışmasını garantiler.

---

## Adım 2 – Yazı Tipi Varyasyon Seçicilerini Etkinleştirin ve **Çalışma Kitabını PDF Olarak Kaydedin**

Gelişmiş tipografi (ör. emoji veya CJK varyasyon seçicileri) desteklemeniz gerekiyorsa, bu özelliği **kaydetmeden önce** açmalısınız.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Ana nokta:** Burada temel anahtar kelime **how to create pdf** burada yanıtlanıyor—ayarları yaptıktan sonra `workbook.save(..., SaveFormat.PDF)` çağrısıyla.

---

## Adım 3 – **Excel'i HTML’ye Dışa Aktarın** ve Dondurulmuş Satırları Koruyun

Çoğu paydaş hızlı bir web önizlemesi ister. Aspose.Cells HTML’ye dışa aktarabilir ve `setPreserveFrozenRows(true)` ile Excel’deki kaydırma deneyimini aynı tutar.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Neden önemlidir:** Dondurulmuş satırlar bir kullanılabilirlik lüksüdür; bunlar olmadan, sayfa aşağı kaydırıldığında başlık satırları kaybolur.

---

## Adım 4 – IF‑Parametresiyle Smart Marker

Smart Marker’lar, döngü yazmadan verileri bir şablona birleştirmenizi sağlar. `if`‑parametresi, işaretçi içinde doğrudan koşullu mantık ekler.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

Çıktı PDF’si **“VIP Customer: Acme Corp”** olarak görünecek çünkü `IsVIP` `true`. Bayrağı `false` yaparsanız **“Regular Customer: Acme Corp”** alırsınız—ekstra kod gerekmez.

---

## Adım 5 – Hiyerarşik Bir Aralık Kullanarak Master‑Detail Smart Marker

Üst‑alt veri (ör. siparişler ve satır öğeleri) olduğunda, master‑detail işaretçi manuel satır eklemeden işinizi kolaylaştırır.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**Ne kazanırsınız:** Motor, her sipariş için master satırlarını genişletir ve detay satırlarını otomatik olarak altına yerleştirir—faturalar veya satın alma raporları için mükemmeldir.

---

## Adım 6 – Base‑64 Görüntüler İçeren Bir Markdown Belgesi Yükleyin

Kaynak veriniz Markdown’da (dokümantasyon hatlarında yaygın) ise, Aspose.Cells bunu doğrudan bir çalışma kitabına işleyebilir.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Köşe durum notu:** Base‑64 dizesi hatalıysa, Aspose görüntüyü atlayıp belgenin geri kalanını işlemeye devam eder—çökmez.

---

## Adım 7 – GridJs Seçeneklerini Yapılandırın ve Veri Ekleyin

GridJs, Aspose’un HTML’ye render edebildiği hafif bir JavaScript ızgarasıdır. Sayıları hizalamak ve kenarlık eklemek okunabilirliği artırır.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Neden önemlidir:** Doğru hizalama ve kenarlıklar, oluşturulan HTML’nin cilalı bir elektronik tablo gibi görünmesini sağlar—panolar için faydalıdır.

---

## Hepsini Bir Araya Getirmek – `main` Metodu

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}