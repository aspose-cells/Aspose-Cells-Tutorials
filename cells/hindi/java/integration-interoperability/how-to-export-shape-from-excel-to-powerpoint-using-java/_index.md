---
category: general
date: 2026-11-16
description: जावा में एक्सेल से पावरपॉइंट में शैप निर्यात करना सीखें, एक्सेल चार्ट
  को PPTX फ़ाइल में बदलें और Aspose.Cells के साथ शैप को PPTX में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shape
- convert excel chart
- shape to powerpoint
- save shape pptx
- export shape from excel
language: hi
lastmod: 2026-11-16
og_description: जावा में एक्सेल से पावरपॉइंट में शैप निर्यात करने का तरीका। इस पूर्ण
  ट्यूटोरियल का पालन करके एक्सेल चार्ट को कनवर्ट करें, शैप को PPTX में सहेजें, और
  शैप को पावरपॉइंट फ़ाइल में एम्बेड करें।
og_image_alt: Diagram illustrating how to export shape from Excel to PowerPoint using
  Java
og_title: जावा में एक्सेल से पावरपॉइंट में आकृति निर्यात करने की चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  headline: How to export shape from Excel to PowerPoint using Java
  type: TechArticle
- description: Learn how to export shape from Excel to PowerPoint in Java, convert
    Excel chart to a PPTX file and save shape PPTX with Aspose.Cells.
  name: How to export shape from Excel to PowerPoint using Java
  steps:
  - name: '**Load the workbook** that contains the shape.'
    text: '**Load the workbook** that contains the shape.'
  - name: '**Locate the shape** on the first worksheet.'
    text: '**Locate the shape** on the first worksheet.'
  - name: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
    text: '**Configure export options** so the shape becomes an editable PowerPoint
      object.'
  - name: '**Save the shape as a PPTX file**.'
    text: '**Save the shape as a PPTX file**.'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
- PowerPoint integration
title: जावा का उपयोग करके एक्सेल से पावरपॉइंट में शैप निर्यात कैसे करें
url: /hi/java/integration-interoperability/how-to-export-shape-from-excel-to-powerpoint-using-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to export shape from Excel to PowerPoint using Java

यदि आपको **Excel workbook** से **shape** को PowerPoint स्लाइड में निर्यात करने की आवश्यकता है, तो यह गाइड आपको सटीक चरण दिखाता है। आप देखेंगे कि **Excel chart** ऑब्जेक्ट को कैसे **shape to PowerPoint** में बदलें, और अंत में **save shape PPTX** सही निर्यात विकल्पों के साथ कैसे करें।

एक shape का निर्यात करना प्रोग्रामेटिक रूप से रिपोर्ट जनरेट करते समय एक सामान्य आवश्यकता है। इस ट्यूटोरियल के अंत तक आपके पास एक स्व-समाहित Java प्रोग्राम होगा जो `shape.pptx` फ़ाइल बनाता है, जिसे प्रस्तुति में उपयोग किया जा सकता है। कोई बाहरी स्क्रिप्ट आवश्यक नहीं है, और कोड Aspose.Cells 2024‑R2 या बाद के संस्करण के साथ काम करता है।

## Prerequisites

* Java 17 या नया (कोड किसी भी JDK 8+ के साथ संकलित हो सकता है)
* Aspose.Cells for Java लाइब्रेरी (Aspose वेबसाइट से डाउनलोड करें या Maven डिपेंडेंसी जोड़ें)
* एक Excel फ़ाइल (`chart.xls`) जिसमें कम से कम एक shape (चार्ट, टेक्स्टबॉक्स, या SmartArt) हो
* Java एक्सेप्शन हैंडलिंग का बुनियादी ज्ञान

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version>
</dependency>
```

## How to export shape from Excel to PowerPoint (overall flow)

प्रक्रिया चार तार्किक भागों में विभाजित है:

1. **Load the workbook** जिसमें shape मौजूद है।  
2. **Locate the shape** पहले worksheet पर।  
3. **Configure export options** ताकि shape एक संपादन योग्य PowerPoint ऑब्जेक्ट बन जाए।  
4. **Save the shape as a PPTX file**।

प्रत्येक भाग का विवरण नीचे दिया गया है, और पूरी चलाने योग्य प्रोग्राम व्याख्याओं के बाद प्रस्तुत किया गया है।

## Step 1: Load the workbook that contains the shape

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // Load the Excel workbook. Adjust the path to your environment.
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");
```

*Why this step?*  
`Workbook` सभी Aspose.Cells ऑपरेशन्स का प्रवेश बिंदु है। फ़ाइल को लोड करने से आपको worksheets, cells, और shape संग्रह तक पहुंच मिलती है। यदि फ़ाइल नहीं मिलती, तो Aspose.Cells `FileNotFoundException` फेंकता है, जिसे हम बाद में पकड़ते हैं।

## Step 2: Access the first worksheet and retrieve the target shape

```java
            // Access the first worksheet (index 0)
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // Retrieve the first shape. In most examples the chart is the first shape.
            Shape shape = worksheet.getShapes().get(0);
```

*Why this step?*  
Worksheets शून्य‑आधारित संग्रह में संग्रहीत होते हैं, इसलिए `get(0)` पहला शीट लौटाता है। Shapes भी अनुक्रमित होते हैं; `get(0)` पहला shape लाता है, जो आमतौर पर वह चार्ट होता है जिसे आप निर्यात करना चाहते हैं। यदि आपके workbook में कई shapes हैं, तो आप संग्रह को इटररेट कर सकते हैं या `shape.getName()` का उपयोग करके विशिष्ट shape चुन सकते हैं।

## Step 3: Prepare export options – we want the shape as an editable PPTX object

```java
            // Create export options. Setting the save format to PPTX tells Aspose.Cells
            // to generate a PowerPoint file rather than an image.
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);
```

*Why this step?*  
`ImageOrPrintOptions` नियंत्रित करता है कि shape कैसे रेंडर हो। `SaveFormat.PPTX` चुनने पर लाइब्रेरी Excel ग्राफ़िक को एक वेक्टर‑आधारित PowerPoint shape में बदल देती है जो आयात के बाद भी संपादन योग्य रहता है। यह वास्तविक **shape to PowerPoint** रूपांतरण के लिए आवश्यक है; PNG या JPEG का उपयोग करने पर ग्राफ़िक लॉक हो जाता है।

## Step 4: Export the shape to a PowerPoint file

```java
            // Export the shape. The output file will contain a single slide with the shape.
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

*Why this step?*  
`save` मेथड पहले परिभाषित विकल्पों के साथ shape को लिखता है। परिणामी `shape.pptx` में एक ही स्लाइड होती है जहाँ shape Excel में जैसा था वैसा ही दिखता है, लेकिन अब आप इसे PowerPoint में संपादित कर सकते हैं (रंग बदलें, आकार बदलें, एनीमेशन जोड़ें आदि)। यह **save shape PPTX** की आवश्यकता को पूरा करता है।

## Full, runnable example

पूरे क्लास को `ExportShapeDemo.java` नामक फ़ाइल में कॉपी करें, `YOUR_DIRECTORY` को पूर्ण या सापेक्ष पथ से बदलें, और `javac ExportShapeDemo.java && java ExportShapeDemo` चलाएँ। निष्पादन के बाद आपको लक्ष्य फ़ोल्डर में `shape.pptx` मिलेगा।

```java
import com.aspose.cells.*;

public class ExportShapeDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook that contains the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chart.xls");

            // 2. Access the first worksheet
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Retrieve the first shape (assumed to be a chart or textbox)
            Shape shape = worksheet.getShapes().get(0);

            // 4. Prepare export options – we want the shape as an editable PPTX object
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);

            // 5. Export the shape to a PowerPoint file
            shape.save("YOUR_DIRECTORY/shape.pptx", exportOptions);

            System.out.println("Export completed. File saved as shape.pptx");
        } catch (Exception e) {
            System.err.println("An error occurred while exporting the shape:");
            e.printStackTrace();
        }
    }
}
```

### Expected output

```
Export completed. File saved as shape.pptx
```

`shape.pptx` को Microsoft PowerPoint में खोलें। आपको एक ही स्लाइड दिखेगी जिसमें मूल Excel चार्ट (या टेक्स्टबॉक्स) एक पूरी तरह से संपादन योग्य PowerPoint shape के रूप में होगा।

## Common variations and edge cases

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Multiple shapes** | `worksheet.getShapes()` को लूप करें और प्रत्येक shape के लिए `save` कॉल करें, या `shape.getName()` द्वारा विशिष्ट shape चुनें। |
| **Shape is a chart with data series** | `exportOptions.setExportChartAsEditable(true)` का उपयोग करें ताकि series भी संपादन योग्य रहें। |
| **Need a specific slide layout** | सहेजने के बाद, Aspose.Slides के साथ PPTX खोलें और shape को कस्टम लेआउट में डालें। |
| **Large workbook** | मेमोरी उपयोग कम करने के लिए `Workbook(String, LoadOptions)` से केवल आवश्यक worksheet लोड करें। |
| **Different output format (PDF, PNG)** | `exportOptions.setSaveFormat(SaveFormat.PDF)` या `SaveFormat.PNG` में बदलें। यह तब उपयोगी है जब आप **convert Excel chart** को स्थिर छवि के रूप में निर्यात करना चाहते हैं न कि PowerPoint shape के रूप में। |

**Pro tip:** हमेशा यह सत्यापित करें कि shape इंडेक्स (`get(0)`) वही दृश्य तत्व है जिसे आप निर्यात करना चाहते हैं। shape संग्रह का क्रम Excel में insertion क्रम को दर्शाता है, जो दृश्य stacking क्रम से अलग हो सकता है।

## How to export shape from Excel to PowerPoint – troubleshooting checklist

* **File not found** – सुनिश्चित करें कि `new Workbook()` में दिया गया पथ मौजूद `.xls` या `.xlsx` फ़ाइल की ओर इशारा कर रहा है।  
* **No shapes returned** – पुष्टि करें कि worksheet में वास्तव में कोई shape है; डिबग करने के लिए `worksheet.getShapes().getCount()` कॉल कर सकते हैं।  
* **Exported file is empty** – जाँचें कि `exportOptions.setSaveFormat(SaveFormat.PPTX)` सेट है; इमेज फ़ॉर्मेट उपयोग करने पर picture बनता है न कि shape।  
* **Compatibility issues** – Aspose.Cells 24.9+ सभी प्रमुख प्लेटफ़ॉर्म पर PPTX निर्यात का समर्थन करता है। यदि `UnsupportedOperationException` मिलता है तो अपग्रेड करें।

## Conclusion

अब आप जानते हैं कि **how to export shape** को Excel workbook से निकालकर Java के माध्यम से PowerPoint प्रस्तुति में कैसे एम्बेड किया जाए। इस ट्यूटोरियल ने workbook लोड करना, shape ढूँढना, **export shape from Excel** विकल्प कॉन्फ़िगर करना, और अंत में **save shape PPTX** करना कवर किया। इस आधार पर आप रिपोर्ट जनरेशन को स्वचालित कर सकते हैं, डैशबोर्ड बना सकते हैं, या Excel विज़ुअल को स्लाइड डेक में बिना मैन्युअल कॉपी‑पेस्ट के एकीकृत कर सकते हैं।

### Next steps

* **convert Excel chart** को PDF या DOCX जैसे अन्य Office फ़ॉर्मेट में बदलने का अन्वेषण करें।  
* इस तकनीक को Aspose.Slides के साथ मिलाकर एक ही स्लाइड पर कई shapes रखें।  
* `ImageOrPrintOptions` प्रॉपर्टीज़ (जैसे `setResolution`, `setTransparent`) के साथ प्रयोग करें ताकि निर्यात किए गए shape की दृश्य गुणवत्ता को बारीकी से ट्यून किया जा सके।

कोड को बैच प्रोसेसिंग के लिए अनुकूलित करने या बड़े रिपोर्टिंग सर्विस में इंटीग्रेट करने में संकोच न करें। Happy coding!

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकते हैं।

- [How to export shape with ShapeExportOptions in Java](/cells/english/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/)
- [How to export Excel sheet to PowerPoint with Aspose.Cells in Java](/cells/english/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/)
- [How to Export Charts from Excel to PowerPoint – Full Java Guide](/cells/english/java/integration-interoperability/how-to-export-charts-from-excel-to-powerpoint-full-java-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}