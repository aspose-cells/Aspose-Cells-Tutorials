---
category: general
date: 2026-11-22
description: Aspose.Cells for Java का उपयोग करके Excel को PowerPoint में कैसे बदलें,
  सीखें, जिसमें एक ही कार्यप्रवाह में Excel चार्ट को PowerPoint में निर्यात करने के
  चरण शामिल हैं।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- export excel chart to powerpoint
- Aspose.Cells Java
- Excel to PPTX conversion
- Java file format conversion
language: hi
lastmod: 2026-11-22
og_description: Aspose.Cells for Java का उपयोग करके Excel को PowerPoint में बदलें।
  इस पूर्ण चरण‑दर‑चरण ट्यूटोरियल का पालन करके Excel चार्ट को भी PowerPoint में निर्यात
  करें।
og_image_alt: Diagram showing conversion of Excel to PowerPoint using Aspose.Cells
og_title: Aspose.Cells के साथ Excel को PowerPoint में बदलें – Java गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  headline: How to convert Excel to PowerPoint with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to convert Excel to PowerPoint using Aspose.Cells for Java,
    including steps to export Excel chart to PowerPoint in a single workflow.
  name: How to convert Excel to PowerPoint with Aspose.Cells for Java
  steps:
  - name: Open `withShapes.pptx` in PowerPoint.
    text: Open `withShapes.pptx` in PowerPoint.
  - name: Confirm that each Excel sheet appears as a separate slide.
    text: Confirm that each Excel sheet appears as a separate slide.
  - name: Check that charts retain their colors, legends, and data labels.
    text: Check that charts retain their colors, legends, and data labels.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: Aspose.Cells for Java के साथ Excel को PowerPoint में कैसे बदलें
url: /hi/java/integration-interoperability/how-to-convert-excel-to-powerpoint-with-aspose-cells-for-jav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को PowerPoint में Aspose.Cells for Java के साथ कैसे कनवर्ट करें

यदि आपको **Excel को PowerPoint में कनवर्ट** करना है, तो यह गाइड Aspose.Cells for Java के साथ एक सरल तरीका दिखाता है। आप यह भी देखेंगे कि **Excel चार्ट को PowerPoint में एक्सपोर्ट** कैसे किया जाता है, जिससे आप मैन्युअल कॉपी‑पेस्ट के बिना सीधे प्रस्तुति में चार्ट एम्बेड कर सकते हैं।

स्प्रेडशीट को स्लाइड डेक में बदलना आम है जब आप गैर‑तकनीकी दर्शकों के साथ डेटा‑आधारित अंतर्दृष्टि साझा करना चाहते हैं। PowerPoint में चार्ट को फिर से बनाने के बजाय, आप पूरे पाइपलाइन को स्वचालित कर सकते हैं, फ़ॉर्मेटिंग को बरकरार रख सकते हैं, और कई घंटे का काम बचा सकते हैं।

इस ट्यूटोरियल में आप करेंगे:

* Maven या Gradle प्रोजेक्ट में Aspose.Cells सेट अप करें।  
* डेटा और चार्ट वाले मौजूदा वर्कबुक को लोड करें।  
* `ImageOrPrintOptions` को PPTX फ़ॉर्मेट के लिए कॉन्फ़िगर करें।  
* वर्कबुक को PowerPoint प्रेज़ेंटेशन के रूप में सेव करें।  
* परिणाम को सत्यापित करें और सामान्य किनारी मामलों को संभालें।

> **Prerequisite** – आपको एक वैध Aspose.Cells for Java लाइसेंस चाहिए (या आप एवाल्यूएशन संस्करण के साथ काम कर सकते हैं)। कोड Java 8+ और किसी भी IDE के साथ काम करता है जो Maven/Gradle को सपोर्ट करता है।

![Diagram showing conversion of Excel to PowerPoint using Aspose.Cells](convert_excel_to_powerpoint.png)

## आपको क्या चाहिए

| आइटम | कारण |
|------|--------|
| **Java Development Kit (JDK) 8 या नया** | उदाहरण को कंपाइल और रन करने के लिए आवश्यक। |
| **Maven or Gradle** | Aspose.Cells के लिए डिपेंडेंसी मैनेजमेंट को सरल बनाता है। |
| **Aspose.Cells for Java** | `Workbook` और `ImageOrPrintOptions` API प्रदान करता है जो कनवर्ज़न में उपयोग होते हैं। |
| **एक Excel फ़ाइल (`shapes.xlsx`) जिसमें कम से कम एक चार्ट हो** | *export Excel chart to PowerPoint* परिदृश्य को दर्शाता है। |

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

### Maven

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

### Gradle

```gradle
implementation 'com.aspose:aspose-cells:24.10' // latest version as of 2026
```

> **Why this step matters** – लाइब्रेरी जोड़ने से `Workbook`, `ImageOrPrintOptions`, और `SaveFormat` क्लास उपलब्ध हो जाते हैं। सही डिपेंडेंसी के बिना कोड कंपाइल नहीं होगा।

## चरण 2: वह वर्कबुक लोड करें जिसमें चार्ट(स) हैं

```java
import com.aspose.cells.Workbook;

// Load the Excel file. Replace the path with your actual location.
Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
```

**Explanation:**  
`Workbook` सभी Excel ऑपरेशन्स का एंट्री पॉइंट है। `shapes.xlsx` लोड करके आप डेटा टेबल्स और एम्बेडेड चार्ट दोनों को मेमोरी में लाते हैं, जिससे आगे का कनवर्ज़न संभव होता है।

## चरण 3: कनवर्ज़न विकल्प बनाएं और टार्गेट फ़ॉर्मेट को PPTX सेट करें

```java
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.SaveFormat;

// Configure options for image/print conversion.
ImageOrPrintOptions options = new ImageOrPrintOptions();
// The SaveFormat.PPTX constant tells Aspose.Cells to generate a PowerPoint file.
options.setSaveFormat(SaveFormat.PPTX);
```

**Why use `ImageOrPrintOptions`?**  
ये विकल्प नियंत्रित करते हैं कि प्रत्येक वर्कशीट या चार्ट कैसे रेंडर किया जाए। `SaveFormat.PPTX` सेट करने से लाइब्रेरी प्रत्येक शीट (या चार्ट) को अपनी स्लाइड पर रखती है, जिससे विज़ुअल फ़िडेलिटी बनी रहती है।

## चरण 4: वर्कबुक को PowerPoint प्रेज़ेंटेशन के रूप में सेव करें

```java
// The second argument is the options object we just configured.
workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);
```

**What happens here?**  
Aspose.Cells वर्कबुक की वर्कशीट्स और चार्ट्स पर इटरेट करता है, उन्हें स्लाइड‑संगत ग्राफ़िक्स में रास्टराइज़ करता है, और निर्दिष्ट स्थान पर एक `.pptx` पैकेज लिखता है। परिणामी फ़ाइल को Microsoft PowerPoint, Google Slides, या किसी भी PPTX‑संगत व्यूअर में खोला जा सकता है।

## चरण 5: कनवर्ज़न को सत्यापित करें

1. `withShapes.pptx` को PowerPoint में खोलें।  
2. पुष्टि करें कि प्रत्येक Excel शीट एक अलग स्लाइड के रूप में दिखाई देती है।  
3. जाँचें कि चार्ट अपने रंग, लेजेंड, और डेटा लेबल्स को बरकरार रखते हैं।  

यदि कोई चार्ट विकृत दिखता है, तो आपको `ImageOrPrintOptions` DPI को समायोजित करने की आवश्यकता हो सकती है:

```java
options.setResolution(300); // 300 DPI gives higher quality for complex charts
```

## Excel चार्ट को PowerPoint में एक्सपोर्ट करें – एक केंद्रित वैरिएशन

कभी-कभी आपको पूरे वर्कबुक के बजाय केवल एक चार्ट को स्थानांतरित करना होता है। आप पहले चार्ट को इमेज में बदलकर फिर मैन्युअली PowerPoint स्लाइड में इन्सर्ट करके यह कर सकते हैं, लेकिन Aspose.Cells प्रक्रिया को सरल बनाता है:

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ImageOrPrintOptions;
import com.aspose.cells.ImageFormat;
import com.aspose.cells.SaveOptions;

// Assume the chart is on the first worksheet, first chart object.
Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);

// Create options for converting the chart to an image.
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions();
chartOptions.setImageFormat(ImageFormat.PNG);
chartOptions.setSaveFormat(SaveFormat.PPTX);

// Save only the chart as a PPTX slide.
chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOptions);
```

**Why this matters:**  
यह स्निपेट एक एकल चार्ट को अलग करता है, फ़ाइल आकार घटाता है, और आपको यह नियंत्रित करने की सूक्ष्म क्षमता देता है कि कौन से विज़ुअल स्लाइड बनेंगे। जब आपको पूरे वर्कबुक की आवश्यकता नहीं होती, तब **export Excel chart to PowerPoint** करने का यह सबसे सीधा तरीका है।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | कारण | समाधान |
|-------|-------|-----|
| **खाली स्लाइड्स** | वर्कशीट में कोई दृश्यमान डेटा नहीं है या चार्ट छिपा हुआ है। | सेव करने से पहले सुनिश्चित करें कि चार्ट दृश्यमान है और वर्कशीट में डेटा है। |
| **कम‑रिज़ॉल्यूशन इमेजेज़** | डिफ़ॉल्ट DPI 96 है, जो प्रिंटेड स्लाइड्स के लिए पर्याप्त नहीं हो सकता। | `workbook.save` से पहले `options.setResolution(200‑300)` कॉल करें। |
| **असमर्थित चार्ट प्रकार** | बहुत नए या कस्टम चार्ट प्रकार पूरी तरह से रेंडर नहीं हो सकते। | चार्ट को इमेज (`ImageFormat.PNG`) के रूप में एक्सपोर्ट करें और फिर मैन्युअली इन्सर्ट करें। |
| **फ़ाइल‑पाथ त्रुटियाँ** | विभिन्न OS पर गलत रिलेटिव पाथ। | प्लेटफ़ॉर्म‑स्वतंत्र पाथ के लिए `Paths.get("YOUR_DIRECTORY", "file.xlsx").toString()` उपयोग करें। |

## प्रोडक्शन‑ग्रेड कनवर्ज़न के लिए प्रो टिप्स

* **बैच प्रोसेसिंग:** Excel फ़ाइलों की डायरेक्टरी पर लूप करें और समान कनवर्ज़न लॉजिक को कॉल करें।  
* **मेमोरी मैनेजमेंट:** बड़े वर्कबुक के लिए, हीप उपयोग को कम करने हेतु `workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` को इनवोक करें।  
* **लाइसेंस एक्टिवेशन:** अपने लाइसेंस फ़ाइल (`Aspose.Cells.lic`) को क्लासपाथ में रखें और किसी भी Aspose API उपयोग से पहले `License license = new License(); license.setLicense("Aspose.Cells.lic");` को कॉल करें।  
* **थ्रेड सेफ़्टी:** प्रत्येक थ्रेड को अपना `Workbook` इंस्टेंस उपयोग करना चाहिए; Aspose.Cells ऑब्जेक्ट थ्रेड‑सेफ़ नहीं हैं।

## पूर्ण कार्यशील उदाहरण

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) throws Exception {
        // 1. Optional: activate your Aspose.Cells license.
        // License license = new License();
        // license.setLicense("Aspose.Cells.lic");

        // 2. Load the workbook that contains charts.
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // 3. Set conversion options – target PPTX format.
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.PPTX);
        // Increase resolution for sharper charts (optional).
        options.setResolution(300);

        // 4. Save the workbook as a PowerPoint presentation.
        workbook.save("YOUR_DIRECTORY/withShapes.pptx", options);

        // 5. (Optional) Export only the first chart to its own PPTX.
        Chart chart = workbook.getWorksheets().get(0).getCharts().get(0);
        ImageOrPrintOptions chartOpts = new ImageOrPrintOptions();
        chartOpts.setSaveFormat(SaveFormat.PPTX);
        chart.save("YOUR_DIRECTORY/singleChart.pptx", chartOpts);

        System.out.println("Conversion completed successfully.");
    }
}
```

**Expected output:**  

प्रोग्राम चलाने पर `Conversion completed successfully.` प्रिंट होता है और दो फ़ाइलें बनती हैं:

* `withShapes.pptx` – एक स्लाइड डेक जहाँ प्रत्येक वर्कशीट (और उसके चार्ट) अलग स्लाइड पर दिखते हैं।  
* `singleChart.pptx` – एक सिंगल‑स्लाइड प्रेज़ेंटेशन जिसमें वर्कबुक के पहले चार्ट ही शामिल है।

इन फ़ाइलों को PowerPoint में खोलें ताकि यह सत्यापित हो सके कि चार्ट अपनी मूल स्टाइलिंग और डेटा लेबल्स को बरकरार रखते हैं।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells for Java का उपयोग करके **Excel को PowerPoint में कनवर्ट** कैसे किया जाता है, और आपने यह भी देखा कि जब केवल एक विशिष्ट विज़ुअल की आवश्यकता हो तो **Excel चार्ट को PowerPoint में एक्सपोर्ट** करने का सबसे प्रभावी तरीका क्या है। `ImageOrPrintOptions` को कॉन्फ़िगर करके और `SaveFormat` को `PPTX` सेट करके, लाइब्रेरी वर्कशीट्स और चार्ट्स को स्लाइड‑संगत ग्राफ़िक्स में रेंडर करने का भारी काम संभालती है।

रिपोर्टिंग पाइपलाइन के लिए बैच कनवर्ज़न को ऑटोमेट करें।  
जनरेटेड PPTX को Apache POI `XSLF` API का उपयोग करके अन्य स्लाइड एसेट्स के साथ मिलाएँ।  
PDF या HTML जैसे अतिरिक्त एक्सपोर्ट फ़ॉर्मेट्स को एक्सप्लोर करें ताकि मल्टी‑चैनल वितरण हो सके।

DPI सेटिंग्स, कस्टम स्लाइड लेआउट्स, या जनरेटेड PPTX को ईमेल वर्कफ़्लो में एम्बेड करने के साथ प्रयोग करने में संकोच न करें। कोडिंग का आनंद लें!

## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [How to export Excel sheet to PowerPoint with Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step‑by‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to export chart to docx from Excel using Aspose.Cells for Java](/cells/english/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}