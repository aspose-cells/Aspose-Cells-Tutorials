---
category: general
date: 2026-11-25
description: Aspose.Cells के साथ Java में Excel को SVG में निर्यात करें – Excel को
  SVG के रूप में सहेजने और एक वेक्टर इमेज बनाने के लिए चरण‑दर‑चरण मार्गदर्शिका।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to svg
- save excel as svg
- excel to vector image
- convert excel to svg
- export excel as svg
language: hi
lastmod: 2026-11-25
og_description: Aspose.Cells in Java के साथ Excel को SVG में निर्यात करें। जानें कि
  कैसे Excel को SVG के रूप में सहेजें और कुछ ही पंक्तियों के कोड से उच्च‑गुणवत्ता
  वाले वेक्टर इमेज बनाएं।
og_image_alt: Screenshot of an Excel worksheet exported to SVG format
og_title: जावा में एक्सेल को SVG में निर्यात करें – पूर्ण Aspose.Cells ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  headline: How to export Excel to SVG using Aspose.Cells in Java
  type: TechArticle
- description: Export Excel to SVG with Aspose.Cells in Java – a step‑by‑step guide
    to save Excel as SVG and create a vector image.
  name: How to export Excel to SVG using Aspose.Cells in Java
  steps:
  - name: Load the workbook containing the data
    text: '```java import com.aspose.cells.Workbook;'
  - name: Set up image export options for SVG
    text: '```java import com.aspose.cells.ImageOrPrintOptions; import com.aspose.cells.ImageFormat;'
  - name: Save the workbook as an SVG file
    text: '```java import com.aspose.cells.SaveFormat;'
  - name: What to explore next
    text: '* **Export Excel as PNG or JPEG** – change `exportOptions.setImageFormat(ImageFormat.PNG)`
      for raster output. * **Convert Excel to PDF** – use `PdfSaveOptions` for printable
      documents. * **Batch processing** – combine the above code with a file‑system
      watcher to automatically **convert Excel to SVG*'
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
- Excel
title: Aspose.Cells का उपयोग करके जावा में एक्सेल को SVG में निर्यात कैसे करें
url: /hi/java/excel-import-export/how-to-export-excel-to-svg-using-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for Java के साथ Excel को SVG में निर्यात करने का तरीका

यदि आपको **Excel को SVG में निर्यात** करना है, तो यह गाइड आपको Aspose.Cells for Java के साथ यह करने का तरीका दिखाता है। आप सीखेंगे कि **Excel को SVG के रूप में सहेजें** और केवल कुछ कोड लाइनों में उच्च‑गुणवत्ता की **वेक्टर इमेज** उत्पन्न करें।

Excel वर्कबुक को SVG फ़ाइल में निर्यात करने से आप शीट को वेब पेज, रिपोर्ट या किसी भी ऐसे वातावरण में एम्बेड कर सकते हैं जो स्केलेबल ग्राफ़िक्स को प्राथमिकता देता है। SVG फ़ॉर्मेट फ़ॉन्ट, रंग और सेल बॉर्डर को बिना पिक्सेलेशन के संरक्षित रखता है, जो रास्टर इमेज में अक्सर देखा जाता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

* Java 17 या उसके बाद का संस्करण स्थापित हो।
* Aspose.Cells for Java का सक्रिय लाइसेंस (या एक अस्थायी इवैल्यूएशन की)।
* एक Maven या Gradle प्रोजेक्ट जहाँ आप Aspose.Cells डिपेंडेंसी जोड़ सकें।

अपने प्रोजेक्ट में Aspose.Cells लाइब्रेरी जोड़ें:

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

```gradle
// Gradle
implementation 'com.aspose:aspose-cells:24.10'
```

## Export Excel to SVG – step‑by‑step

यह प्रक्रिया तीन सरल चरणों में विभाजित है: वर्कबुक लोड करना, SVG निर्यात विकल्प सेट करना, और परिणाम को सहेजना। प्रत्येक चरण नीचे समझाया गया है।

### Step 1: Load the workbook containing the data

```java
import com.aspose.cells.Workbook;

public class ExcelToSvgDemo {
    public static void main(String[] args) throws Exception {
        // Load the Excel file you want to convert.
        Workbook workbook = new Workbook("C:/Data/Report.xlsx");
        // Continue with export options...
    }
}
```

**Why this matters:**  
`Workbook` Aspose.Cells में मुख्य ऑब्जेक्ट है। फ़ाइल को एक बार लोड करने से आपको सभी वर्कशीट्स, स्टाइल्स और एम्बेडेड ऑब्जेक्ट्स तक पहुँच मिलती है, जिन्हें बाद में SVG एक्सपोर्टर रेंडर करेगा।

### Step 2: Set up image export options for SVG

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;

ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setImageFormat(ImageFormat.SVG); // Guarantees a vector output
exportOptions.setOnePagePerSheet(true);       // Export each sheet as a single SVG page
exportOptions.setTransparent(true);           // Preserve transparent backgrounds
```

**Why this matters:**  
`ImageOrPrintOptions` आपको आउटपुट फ़ॉर्मेट को नियंत्रित करने देता है। `ImageFormat.SVG` चुनने से परिणाम **वेक्टर इमेज** बनता है, न कि बिटमैप। `OnePagePerSheet` को सक्षम करने से शीट के भीतर पेज ब्रेक नहीं आते, जो आमतौर पर तब वांछित होता है जब SVG को वेब व्यू में दिखाया जाता है।

### Step 3: Save the workbook as an SVG file

```java
import com.aspose.cells.SaveFormat;

workbook.save("C:/Output/Report.svg", exportOptions);
System.out.println("Excel workbook successfully exported to SVG.");
```

**Why this matters:**  
`save` मेथड लोडेड वर्कबुक को कॉन्फ़िगर किए गए `exportOptions` के साथ मिलाता है। यह कॉल एक पूरी‑तरह से मानक SVG फ़ाइल लिखता है जिसे ब्राउज़र, Inkscape या किसी भी वेक्टर‑सक्षम एडिटर में खोला जा सकता है।

## Full runnable example

तीन चरणों को मिलाकर आपको एक स्व-निहित प्रोग्राम मिलता है जिसे आप तुरंत कंपाइल और रन कर सकते हैं:

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("C:/Data/FontVariation.xlsx");

        // 2. Configure SVG export options
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setImageFormat(ImageFormat.SVG);
        exportOptions.setOnePagePerSheet(true);
        exportOptions.setTransparent(true);

        // 3. Export to SVG
        workbook.save("C:/Output/WithVariationSelectors.svg", exportOptions);
        System.out.println("Export complete: Excel saved as SVG.");
    }
}
```

**Expected output**

प्रोग्राम चलाने पर यह प्रिंट करता है:

```
Export complete: Excel saved as SVG.
```

आपको `C:/Output` में `WithVariationSelectors.svg` मिलेगा। ब्राउज़र में फ़ाइल खोलने पर वर्कशीट स्केलेबल ग्राफ़िक्स के रूप में रेंडर होती है, जिसमें टेक्स्ट, बॉर्डर और सेल रंग संरक्षित रहते हैं।

## Common variations and edge cases

| स्थिति | सिफारिशित समायोजन |
|-----------|------------------------|
| **एकाधिक वर्कशीट्स** | `workbook.getWorksheets()` पर लूप करें और प्रत्येक शीट के लिए `save` कॉल करें, वैकल्पिक रूप से फ़ाइल नाम में शीट का नाम जोड़ें। |
| **बड़े वर्कबुक** | `exportOptions.setRenderThreadCount(int)` को बढ़ाएँ ताकि समानांतर रेंडरिंग हो, जिससे रूपांतरण समय घटे। |
| **कस्टम DPI** | `exportOptions.setHorizontalResolution(int)` और `exportOptions.setVerticalResolution(int)` को कॉल करके SVG के viewBox स्केलिंग को नियंत्रित करें। |
| **फ़ॉन्ट एम्बेड करना** | `exportOptions.setExportFontAsSVG(true)` सेट करें ताकि फ़ॉन्ट परिभाषाएँ सीधे SVG में एम्बेड हो जाएँ, जिससे मूल फ़ॉन्ट न होने वाले मशीनों पर भी दृश्य समानता बनी रहे। |
| **पासवर्ड‑सुरक्षित फ़ाइलें** | लोड करते समय पासवर्ड प्रदान करें: `Workbook workbook = new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("pwd"); }});` |

## Pro tips

* **रास्टर फ़ॉलबैक से बचें** – यदि वर्कशीट में जटिल चार्ट हैं, तो सुनिश्चित करें कि वे SVG में वेक्टर एलिमेंट के रूप में दिख रहे हैं। यदि नहीं, तो `exportOptions.setExportChartAsSVG(true)` सक्षम करें।
* **परफ़ॉर्मेंस** – बैच रूपांतरण के लिए प्रत्येक फ़ाइल के लिए नया `ImageOrPrintOptions` बनाने की बजाय एक ही इंस्टेंस को पुनः उपयोग करें।
* **टेस्टिंग** – उत्पन्न SVG को ऑनलाइन वैलिडेटर (जैसे W3C SVG Validator) से वैलिडेट करें ताकि किसी भी खराब मार्कअप को जल्दी पकड़ा जा सके।

## Verify the conversion

आप प्रोग्रामेटिकली यह पुष्टि कर सकते हैं कि आउटपुट फ़ाइल वास्तव में SVG है:

```java
import java.nio.file.Files;
import java.nio.file.Paths;

byte[] data = Files.readAllBytes(Paths.get("C:/Output/Report.svg"));
String content = new String(data, "UTF-8");
if (content.contains("<svg")) {
    System.out.println("File is a valid SVG.");
}
```

`<svg>` रूट एलिमेंट की उपस्थिति यह दर्शाती है कि **Excel को SVG में रूपांतरण** सफल रहा।

## Conclusion

इस ट्यूटोरियल ने दिखाया कि कैसे Aspose.Cells for Java का उपयोग करके **Excel को SVG में निर्यात** किया जाता है। वर्कबुक लोड करके, `ImageOrPrintOptions` को SVG के लिए कॉन्फ़िगर करके, और `save` कॉल करके आप **Excel को SVG के रूप में सहेज** सकते हैं और एक साफ़ **Excel से वेक्टर इमेज** रूपांतरण प्राप्त कर सकते हैं। अब आप SVG को वेब पेज में एम्बेड कर सकते हैं, दस्तावेज़ीकरण में शामिल कर सकते हैं, या किसी भी वेक्टर‑ग्राफ़िक्स टूल के साथ आगे प्रोसेस कर सकते हैं।

### What to explore next

* **Export Excel as PNG or JPEG** – रास्टर आउटपुट के लिए `exportOptions.setImageFormat(ImageFormat.PNG)` बदलें।
* **Convert Excel to PDF** – प्रिंटेबल दस्तावेज़ों के लिए `PdfSaveOptions` का उपयोग करें।
* **Batch processing** – फ़ाइल‑सिस्टम वॉचर के साथ ऊपर दिया गया कोड मिलाकर फ़ोल्डर में हर नई वर्कबुक के लिए स्वचालित रूप से **Excel को SVG में रूपांतरण** करें।

Feel free to experiment with the options, and let the flexibility of Aspose.Cells turn your Excel data into any visual format you need. Happy coding!

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों की खोज करने में मदद करेंगे।

- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [How to Export Excel to SVG – Step‑by‑Step Java Guide](/cells/english/java/excel-import-export/how-to-export-excel-to-svg-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}