---
category: general
date: 2026-03-01
description: PDF कैसे बनाएं और वर्कबुक को PDF के रूप में सहेजें, Excel को HTML में
  निर्यात करें, और Aspose.Cells for Java के साथ एक्सपैंड फ़ंक्शन का उपयोग करें। चरण‑दर‑चरण
  कोड शामिल है।
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: hi
og_description: Aspose.Cells for Java का उपयोग करके वर्कबुक से PDF कैसे बनाएं। वर्कबुक
  को PDF के रूप में सहेजना, Excel को HTML में निर्यात करना, और EXPAND फ़ंक्शन का उपयोग
  करना सीखें।
og_title: वर्कबुक से PDF कैसे बनाएं – जावा ट्यूटोरियल
tags:
- Aspose.Cells
- Java
- PDF generation
title: वर्कबुक से PDF कैसे बनाएं – पूर्ण जावा गाइड
url: /hi/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# वर्कबुक से PDF कैसे बनाएं – पूर्ण जावा गाइड

क्या आपने कभी सोचा है **कि Excel वर्कबुक से सीधे PDF कैसे बनाएं** बिना थर्ड‑पार्टी कन्वर्टर के झंझट के? आप अकेले नहीं हैं। कई डेवलपर्स को तेज़ PDF एक्सपोर्ट, HTML प्रीव्यू, या फैंसी एरे फ़ॉर्मूले की ज़रूरत पड़ने पर रुकावट आती है—सब एक साथ।  

इस ट्यूटोरियल में हम एक ही, स्व-निहित जावा प्रोग्राम के माध्यम से यह सब करेंगे। हम **वर्कबुक को PDF के रूप में सहेजेंगे**, दिखाएंगे कि **Excel को HTML में एक्सपोर्ट** कैसे करें जबकि फ्रीज़्ड रो को बरकरार रखें, और वर्कशीट के अंदर **EXPAND फ़ंक्शन** का उपयोग करेंगे। अंत तक आपके पास एक रन करने योग्य प्रोजेक्ट होगा जिसे आप किसी भी Maven या Gradle बिल्ड में डाल सकते हैं।

> **प्रो टिप:** नीचे दिया गया सभी कोड Aspose.Cells 23.10 (या नया) के साथ काम करता है। यदि आप पुराना संस्करण उपयोग कर रहे हैं, तो कुछ मेथड नाम थोड़े अलग हो सकते हैं।

---

## प्री‑रिक्विज़िट्स

- **Java 17** (या कोई भी LTS संस्करण) स्थापित और कॉन्फ़िगर किया हुआ।
- **Aspose.Cells for Java** लाइब्रेरी। अपने `pom.xml` में निम्न Maven डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- आपका पसंदीदा IDE या टेक्स्ट एडिटर (IntelliJ IDEA, VS Code, Eclipse…)।

कोई बाहरी API नहीं, कोई वेब सर्विस नहीं—सिर्फ शुद्ध जावा और Aspose.Cells SDK।

---

## समाधान का अवलोकन

हम कार्यान्वयन को **सात तार्किक चरणों** में विभाजित करेंगे:

1. वर्कबुक बनाएं और **EXPAND** फ़ंक्शन दिखाएँ।  
2. फ़ॉन्ट वैरिएशन सिलेक्टर्स सक्षम करें और **वर्कबुक को PDF के रूप में सहेजें**।  
3. वही वर्कबुक को HTML में एक्सपोर्ट करें जबकि फ्रीज़्ड रो को संरक्षित रखें।  
4. एक `IF`‑पैरामीटर वाले Smart Marker का उपयोग करके कंडीशनल टेक्स्ट डालें।  
5. हायरार्किकल डेटा के लिए मास्टर‑डिटेल Smart Marker लागू करें।  
6. बेस‑64‑एन्कोडेड इमेजेज़ वाला Markdown फ़ाइल लोड करें।  
7. GridJs विकल्पों को एलाइनमेंट और बॉर्डर के लिए कॉन्फ़िगर करें, फिर डेटा इन्सर्ट करें।

प्रत्येक चरण को अपने स्वयं के मेथड में रखा गया है ताकि `main` मेथड साफ़ रहे और यह स्पष्ट हो **कि हम क्या कर रहे हैं** (why) न कि सिर्फ **क्या टाइप कर रहे हैं** (what)।

---

## चरण 1 – वर्कबुक बनाएं और EXPAND फ़ंक्शन का उपयोग करें

**EXPAND** फ़ंक्शन Office 365 में पेश किया गया एक नया डायनामिक‑एरे फ़ॉर्मूला है। यह बिना मैन्युअल कॉपी किए रेंज को बड़े क्षेत्र में फैलाता है।

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

**यह क्यों महत्वपूर्ण है:**  
- `EXPAND` स्वचालित रूप से परिणाम को खाली सेल्स से पैड करता है, जो बाद में **वर्कबुक को PDF के रूप में सहेजते** समय एक साफ़, आयताकार टेबल देता है।  
- `calculateFormula()` को कॉल करने से फ़ॉर्मूला इंजन एक्सपोर्ट से पहले चल जाता है।

---

## चरण 2 – फ़ॉन्ट वैरिएशन सिलेक्टर्स सक्षम करें और **वर्कबुक को PDF के रूप में सहेजें**

यदि आपको उन्नत टाइपोग्राफी (जैसे इमोजी या CJK वैरिएशन सिलेक्टर्स) का समर्थन चाहिए, तो सेटिंग को **सहेजने से पहले** चालू करना आवश्यक है।

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

**मुख्य बिंदु:** यहाँ मुख्य कीवर्ड **how to create pdf** का उत्तर दिया गया है—`workbook.save(..., SaveFormat.PDF)` को कॉल करके, सेटिंग्स कॉन्फ़िगर करने के बाद।

---

## चरण 3 – **Excel को HTML में एक्सपोर्ट** करें जबकि फ्रीज़्ड रो को संरक्षित रखें

अक्सर स्टेकहोल्डर जल्दी वेब प्रीव्यू चाहते हैं। Aspose.Cells HTML में एक्सपोर्ट कर सकता है, और `setPreserveFrozenRows(true)` के साथ हम Excel जैसा ही स्क्रॉलिंग अनुभव बनाए रखते हैं।

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**आपको क्यों परवाह है:** फ्रीज़्ड रो एक उपयोगिता सुविधा है; इनके बिना, पेज स्क्रॉल करने पर हेडर रो गायब हो जाते हैं।

---

## चरण 4 – IF‑पैरामीटर वाला Smart Marker

Smart Markers आपको टेम्पलेट में डेटा मर्ज करने की सुविधा देते हैं बिना लूप लिखे। `if`‑पैरामीटर सीधे मार्कर के अंदर कंडीशनल लॉजिक जोड़ता है।

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

आउटपुट PDF में **“VIP Customer: Acme Corp”** दिखेगा क्योंकि `IsVIP` `true` है। फ्लैग को `false` करने पर **“Regular Customer: Acme Corp”** मिलेगा—कोई अतिरिक्त कोड नहीं चाहिए।

---

## चरण 5 – हायरार्किकल रेंज के साथ मास्टर‑डिटेल Smart Marker

जब आपके पास पैरेंट‑चाइल्ड डेटा हो (जैसे ऑर्डर और लाइन आइटम), तो मास्टर‑डिटेल मार्कर मैन्युअल रो इन्सर्शन से बचाता है।

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

**आपको क्या मिलता है:** इंजन प्रत्येक ऑर्डर के लिए मास्टर रो को एक्सपैंड करता है और डिटेल रो को स्वचालित रूप से नीचे नेस्ट करता है—इनवॉइस या खरीद रिपोर्ट के लिए आदर्श।

---

## चरण 6 – एम्बेडेड Base‑64 इमेजेज़ वाला Markdown डॉक्यूमेंट लोड करें

यदि आपका स्रोत डेटा Markdown में है (डॉक्यूमेंटेशन पाइपलाइन में आम), तो Aspose.Cells इसे सीधे वर्कबुक में रेंडर कर सकता है।

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

**एज केस नोट:** यदि Base‑64 स्ट्रिंग खराब है, तो Aspose इमेज को स्किप कर देगा लेकिन बाकी डॉक्यूमेंट प्रोसेसिंग जारी रखेगा—कोई क्रैश नहीं।

---

## चरण 7 – GridJs विकल्प कॉन्फ़िगर करें और डेटा इन्सर्ट करें

GridJs एक हल्का JavaScript ग्रिड है जिसे Aspose HTML में रेंडर कर सकता है। नंबरों को एलाइन करना और बॉर्डर लगाना पठनीयता बढ़ाता है।

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

**हमारी परवाह क्यों है:** सही एलाइनमेंट और बॉर्डर से जनरेटेड HTML एक पॉलिश्ड स्प्रेडशीट जैसा दिखता है—डैशबोर्ड के लिए उपयोगी।

---

## सब कुछ एक साथ – `main` मेथड

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