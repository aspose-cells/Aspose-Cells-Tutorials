---
category: general
date: 2026-08-20
description: जाने कैसे चार्ट को docx में निर्यात करें और Aspose.Cells के साथ जावा
  में Excel वर्कबुक को docx में परिवर्तित करें। पूर्ण कोड के साथ चरण‑दर‑चरण मार्गदर्शिका।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export chart to docx
- convert excel workbook to docx
- Aspose.Cells Java
- editable chart DOCX
- Excel to Word conversion
language: hi
lastmod: 2026-08-20
og_description: Aspose.Cells for Java का उपयोग करके चार्ट को docx में निर्यात करें
  और Excel वर्कबुक को docx में परिवर्तित करें। इस पूर्ण, चलाने योग्य ट्यूटोरियल का
  पालन करें।
og_image_alt: Screenshot showing a Java code editor exporting an Excel chart to a
  DOCX file
og_title: Aspose.Cells के साथ चार्ट को docx में निर्यात करें – Java गाइड
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
title: Aspose.Cells for Java का उपयोग करके Excel से चार्ट को DOCX में निर्यात कैसे
  करें
url: /hi/java/integration-interoperability/how-to-export-chart-to-docx-from-excel-using-aspose-cells-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel वर्कबुक से Java का उपयोग करके चार्ट को DOCX में निर्यात करें

यदि आपको Excel फ़ाइल से सीधे **export chart to docx** करने की आवश्यकता है, तो यह ट्यूटोरियल एक तैयार‑से‑चलाने योग्य समाधान दिखाता है। गाइड के अंत तक आप यह भी जानेंगे कि **convert Excel workbook to docx** कैसे किया जाए जबकि संपादन योग्य चार्ट को संरक्षित रखा जाए, ताकि उत्पन्न Word दस्तावेज़ को बिना गुणवत्ता खोए संशोधित किया जा सके।

स्प्रेडशीट गणनाओं को समृद्ध Word लेआउट के साथ मिलाकर रिपोर्ट बनाते समय चार्ट निर्यात करना आम बात है। Aspose.Cells for Java इस रूपांतरण को सरल बनाता है, और API आपको चार्ट को संपादन योग्य रखने देता है—कोई स्थिर छवि आवश्यक नहीं।

## What this tutorial covers

* मौजूदा वर्कबुक को लोड करना जिसमें एक चार्ट हो।  
* `ImageOrPrintOptions` को DOCX फ़ॉर्मेट के लिए कॉन्फ़िगर करना।  
* `ExportEditableCharts` फ़्लैग को सक्षम करना (संस्करण 25.10 से उपलब्ध)।  
* वर्कबुक को ऐसे DOCX फ़ाइल के रूप में सहेजना जो संपादन योग्य चार्ट को बनाए रखे।  

Aspose.Cells JAR के अलावा कोई बाहरी टूल आवश्यक नहीं है। कोड Java 8+ और Aspose.Cells के किसी भी हालिया संस्करण के साथ काम करता है।

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| **Aspose.Cells for Java** (v25.10 या बाद का) | इस रिलीज़ में `setExportEditableCharts` फीचर पेश किया गया था। |
| **Java Development Kit (JDK) 8 या नया** | उदाहरण को संकलित और चलाने के लिए रनटाइम प्रदान करता है। |
| **एक Excel वर्कबुक (`.xlsx`) जिसमें कम से कम एक चार्ट हो** | वही चार्ट है जिसे DOCX में निर्यात किया जाएगा। |
| **एक Java IDE या बिल्ड टूल (जैसे Maven, Gradle)** | निर्भरताओं के प्रबंधन और निष्पादन को सरल बनाता है। |

आप नवीनतम Aspose.Cells JAR को [Aspose website](https://products.aspose.com/cells/java/) से डाउनलोड कर सकते हैं।

## Step 1: Set up the project and add the Aspose.Cells dependency

यदि आप Maven का उपयोग करते हैं, तो अपने `pom.xml` में निम्नलिखित निर्भरता जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version> <!-- use the latest version -->
</dependency>
```

Gradle के लिए, जोड़ें:

```gradle
implementation 'com.aspose:aspose-cells:25.10'
```

> **Pro tip:** वह सटीक संस्करण उपयोग करें जिसमें `ExportEditableCharts` पेश किया गया था (25.10) या कोई नया रिलीज़। पुराने संस्करण इस फ़्लैग को अनदेखा करेंगे और स्थिर छवि उत्पन्न करेंगे।

## Step 2: Load the workbook that contains the chart

`Workbook` क्लास पूरे Excel फ़ाइल का प्रतिनिधित्व करती है। इसे लोड करना एक‑लाइन का ऑपरेशन है:

```java
import com.aspose.cells.*;

public class ExportEditableChartToDocx {
    public static void main(String[] args) throws Exception {
        // Load the workbook with the chart you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ChartWorkbook.xlsx");
```

> **Why this matters:** वर्कबुक को पूरी तरह लोड होना चाहिए इससे पहले कि आप कोई निर्यात विकल्प लागू कर सकें। यदि फ़ाइल पथ गलत है, तो Aspose.Cells `FileNotFoundException` फेंकेगा।

## Step 3: Configure image/print options for DOCX output

`ImageOrPrintOptions` नियंत्रित करता है कि वर्कबुक कैसे रेंडर होगी। सहेजने के फ़ॉर्मेट को `DOCX` सेट करने से Aspose.Cells को एक Word दस्तावेज़ बनाने को कहा जाता है, न कि एक छवि।

```java
        // Create options and specify DOCX as the target format
        ImageOrPrintOptions options = new ImageOrPrintOptions();
        options.setSaveFormat(SaveFormat.DOCX);
```

आप यहाँ पेज साइज, DPI, या इमेज क्वालिटी भी समायोजित कर सकते हैं, लेकिन चार्ट निर्यात के लिए ये वैकल्पिक हैं।

## Step 4: Enable exporting of editable charts

संस्करण 25.10 से आगे, Aspose.Cells चार्ट को मूल Word चार्ट ऑब्जेक्ट के रूप में एम्बेड कर सकता है। इससे वे Microsoft Word में पूरी तरह संपादन योग्य बन जाते हैं।

```java
        // Turn on the editable chart export flag
        options.setExportEditableCharts(true);
```

> **Edge case:** यदि आप इस फ़्लैग को `false` सेट करते हैं (या इसे छोड़ देते हैं), तो चार्ट एक स्थिर चित्र के रूप में रेंडर होगा। `true` केवल तभी उपयोग करें जब लक्ष्य दर्शकों को रूपांतरण के बाद चार्ट को संपादित करने की आवश्यकता हो।

## Step 5: Save the workbook as a DOCX file

अंत में, कॉन्फ़िगर किए गए विकल्पों के साथ `Workbook.save` को कॉल करें:

```java
        // Save the workbook as a DOCX document that contains an editable chart
        workbook.save("YOUR_DIRECTORY/ChartEditable.docx", options);
    }
}
```

जब प्रोग्राम समाप्त हो जाए, तो `ChartEditable.docx` को Microsoft Word में खोलें। आपको मूल चार्ट दिखाई देगा, और यदि आप उस पर राइट‑क्लिक करेंगे, तो **Edit Data** विकल्प उपलब्ध होगा—जिससे पुष्टि होती है कि चार्ट वास्तव में संपादन योग्य है।

## Full, runnable example

नीचे पूरा स्रोत फ़ाइल दिया गया है। इसे अपने IDE में कॉपी करें, `YOUR_DIRECTORY` को एक पूर्ण या सापेक्ष पथ से बदलें, और चलाएँ।

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

**Expected output**

* निर्दिष्ट डायरेक्टरी में `ChartEditable.docx` नामक फ़ाइल बन जाएगी।  
* Word में फ़ाइल खोलने पर चार्ट वही दिखेगा जैसा Excel में था, और आप चार्ट पर डबल‑क्लिक करके उसके डेटा सीरीज़ को संपादित कर सकते हैं।

## Common pitfalls and how to avoid them

| Symptom | Cause | Fix |
|---------|-------|-----|
| Word में **स्थिर छवि** दिखती है, संपादन योग्य चार्ट नहीं | `setExportEditableCharts` नहीं बुलाया गया या संस्करण 25.10 से पुराना उपयोग किया गया | फ़्लैग को `true` सेट करें और सुनिश्चित करें कि आप Aspose.Cells 25.10 या नया उपयोग कर रहे हैं। |
| उत्पन्न DOCX **खाली** है | स्रोत वर्कबुक का फ़ाइल पथ गलत है या पर्याप्त अनुमतियां नहीं हैं | वर्कबुक पथ की जाँच करें और सुनिश्चित करें कि एप्लिकेशन के पास पढ़ने/लिखने की अनुमति है। |
| चार्ट लेआउट **विकृत** दिखता है | Excel में पेज सेटअप (जैसे छिपी हुई पंक्तियाँ/कॉलम) Word के डिफ़ॉल्ट से अलग है | `ImageOrPrintOptions` (जैसे `setOnePagePerSheet(true)`) को समायोजित करके स्केलिंग नियंत्रित करें। |
| बड़े वर्कबुक पर **प्रदर्शन** गिरता है | कई चार्ट या बड़े डेटा सेट निर्यात करना | केवल आवश्यक शीट्स निर्यात करें या `setSheetIndex` का उपयोग करके प्रोसेसिंग को सीमित करें। |

## Extending the solution

* **एकाधिक चार्ट:** सभी वर्कशीट्स पर इटररेट करें और `worksheet.getCharts()` को कॉल करके प्रत्येक चार्ट को अलग‑अलग निर्यात करें।  
* **कस्टम DOCX स्टाइलिंग:** सहेजने के बाद, Aspose.Words का उपयोग करके उत्पन्न दस्तावेज़ में हेडर, फुटर या स्टाइल जोड़ें।  
* **बैच रूपांतरण:** कोड को लूप में रखें जो `.xlsx` फ़ाइलों की डायरेक्टरी को प्रोसेस करे, प्रत्येक के लिए एक DOCX बनाता है।

## Conclusion

अब आपके पास **export chart to docx** और **convert Excel workbook to docx** करने का विश्वसनीय तरीका है, जबकि चार्ट की पूरी संपादन क्षमता बनी रहती है। मुख्य चरण हैं वर्कबुक लोड करना, DOCX के लिए `ImageOrPrintOptions` कॉन्फ़िगर करना, `ExportEditableCharts` सक्षम करना, और परिणाम सहेजना।

पेज मार्जिन सेट करने या वर्कबुक के फ़ॉर्मूले एम्बेड करने जैसे अतिरिक्त विकल्पों के साथ प्रयोग करें ताकि आउटपुट को अपनी रिपोर्टिंग वर्कफ़्लो के अनुसार अनुकूलित किया जा सके। जब आपको प्रोग्रामेटिक रूप से Excel डेटा से Word रिपोर्ट बनानी हो, तो यह तरीका साफ़, रखरखाव‑योग्य समाधान प्रदान करता है।

--- 

*इसे आज़माने के लिए तैयार हैं? उदाहरण को क्लोन करें, फ़ाइल पथ अपडेट करें, और प्रोग्राम चलाएँ। यदि कोई समस्या आती है, तो Aspose.Cells for Java दस्तावेज़ देखें या नीचे दिए गए संबंधित विषयों की जाँच करें।*  

### Related topics you might explore next

* **convert excel workbook to pdf** – उसी वर्कबुक से PDF रिपोर्ट बनाएं।  
* **Aspose.Cells chart formatting** – निर्यात से पहले रंग, मार्कर और एक्सिस को कस्टमाइज़ करें।  
* **Embedding images in DOCX with Aspose.Words** – चार्ट को अन्य Word सामग्री के साथ मिलाएं।  

Happy coding!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन तरीकों का अन्वेषण कर सकें।

- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Automate Excel Chart Access Using Aspose.Cells Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/excel-charts-access-aspose-cells-java/)
- [Customize Excel Chart Data Labels Using Aspose.Cells for Java: A Step-by-Step Guide](/cells/english/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}