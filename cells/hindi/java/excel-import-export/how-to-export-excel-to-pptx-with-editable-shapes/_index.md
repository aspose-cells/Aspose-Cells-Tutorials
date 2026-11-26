---
category: general
date: 2026-11-25
description: Excel को PPTX में संपादन योग्य आकारों के साथ निर्यात करना सीखें। यह गाइड
  यह भी दिखाता है कि प्रिंट एरिया कैसे सेट करें और प्रस्तुतियों के लिए Excel चार्ट
  को कैसे बदलें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel
- set print area
- how to convert xlsx
- set print area excel
- convert excel chart
language: hi
lastmod: 2026-11-25
og_description: Aspose.Cells का उपयोग करके संपादन योग्य आकारों के साथ Excel को PPTX
  में निर्यात करने का तरीका, साथ ही प्रिंट एरिया सेट करने और प्रस्तुति के लिए Excel
  चार्ट को परिवर्तित करने के टिप्स।
og_image_alt: Screenshot showing how to export Excel to PPTX with editable shapes
og_title: Excel को PPTX में संपादन योग्य आकारों के साथ कैसे निर्यात करें
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  headline: How to export Excel to PPTX with editable shapes
  type: TechArticle
- description: Learn how to export Excel to PPTX with editable shapes. This guide
    also shows how to set print area and convert Excel chart for presentations.
  name: How to export Excel to PPTX with editable shapes
  steps:
  - name: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
    text: '**Dependency** – Aspose.Cells provides the `ImageOrPrintOptions` class
      that can render worksheets as PPTX slides. Adding it via Maven ensures the library
      is on the classpath.'
  - name: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
    text: '**Imports** – Importing the right classes keeps the code clean and avoids
      fully‑qualified names.'
  - name: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
    text: '**Loading the workbook** – You must point to the exact file that contains
      the objects you want to export. The path can be absolute or relative to the
      project root.'
  - name: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
    text: '**Export options** – Setting `setEditable(true)` is the key to **how to
      export Excel** so that the resulting PowerPoint shapes remain editable. Without
      this flag, text boxes become static images.'
  - name: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
    text: '**Print area** – The `setPrintArea` call limits the export to the region
      you care about, which reduces file size and removes unwanted rows/columns. This
      directly addresses the **set print area excel** requirement.'
  - name: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
    text: '**Saving** – The `SaveFormat.PPTX` constant tells Aspose.Cells to generate
      a PowerPoint file rather than an image or PDF.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: संपादन योग्य आकृतियों के साथ एक्सेल को पीपीटीएक्स में निर्यात कैसे करें
url: /hi/java/excel-import-export/how-to-export-excel-to-pptx-with-editable-shapes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को PPTX में संपादन योग्य आकारों के साथ निर्यात करने का तरीका

यदि आपको **how to export Excel** फ़ाइलों को PowerPoint में निर्यात करने की आवश्यकता है जबकि संपादन योग्य टेक्स्ट बॉक्स और आकारों को संरक्षित रखा जाए, तो यह गाइड आपको पूरी प्रक्रिया से परिचित कराएगा। आप यह भी सीखेंगे कि **set print area** को कैसे सेट करें ताकि स्लाइड केंद्रित रहे और **convert Excel chart** ऑब्जेक्ट्स को कैसे बदलें ताकि निर्यात के बाद वे पूरी तरह से संपादन योग्य रहें।

डेटा‑ड्रिवेन रिपोर्टों से प्रस्तुति डेक बनाने के दौरान Excel को PPTX में निर्यात करना आम है। Aspose.Cells for Java का उपयोग करके आप मैन्युअल कॉपी‑पेस्ट से बचते हैं, फ़ॉर्मेटिंग को बरकरार रखते हैं, और आउटपुट पर प्रोग्रामेटिक नियंत्रण प्राप्त करते हैं।

## आप क्या सीखेंगे

* एक मौजूदा XLSX वर्कबुक लोड करें जिसमें टेक्स्ट बॉक्स या चार्ट हो।  
* एक्सपोर्ट विकल्पों को कॉन्फ़िगर करें ताकि परिणामी PPTX फ़ाइल में **editable shapes** हों।  
* **Set the print area** को सेट करें ताकि निर्यातित रेंज को आवश्यक सेल्स तक सीमित किया जा सके।  
* वर्कशीट को PPTX फ़ाइल के रूप में सहेजें और सत्यापित करें कि टेक्स्ट बॉक्स और चार्ट PowerPoint में संपादित किए जा सकते हैं।  

**Prerequisites**

* Java 17 या उससे नया स्थापित हो।  
* डिपेंडेंसी प्रबंधन के लिए Maven या Gradle।  
* Excel वर्कबुक और Java प्रोग्रामिंग की बुनियादी समझ।

---

## Excel को PPTX में संपादन योग्य आकारों के साथ निर्यात करने का तरीका

यह सेक्शन वह कोर कोड प्रदान करता है जो निर्यात करता है। उदाहरण में Aspose.Cells 23.9 (लेखन के समय नवीनतम) का उपयोग किया गया है और सभी आवश्यक चरणों को दर्शाता है।

```java
// ------------------------------------------------------------
// 1. Add Aspose.Cells dependency (Maven example)
// ------------------------------------------------------------
/*
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
*/

// ------------------------------------------------------------
// 2. Import required classes
// ------------------------------------------------------------
import com.aspose.cells.*;

public class ExcelToPptxExporter {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------
        // 3. Load the workbook that contains a text box or chart
        // --------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/WithTextBox.xlsx");

        // --------------------------------------------------------
        // 4. Set up export options for PPTX and enable shape editing
        // --------------------------------------------------------
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setFormat(ImageFormat.PPTX);          // output format
        exportOptions.setExportType(ExportType.PPTX);      // explicit PPTX export
        exportOptions.setEditable(true);                   // makes text boxes/shapes editable

        // --------------------------------------------------------
        // 5. Define the print area to limit the exported range
        // --------------------------------------------------------
        // This is the **set print area** step. Adjust the range as needed.
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:H30");

        // --------------------------------------------------------
        // 6. Save the first worksheet as an editable PPTX file
        // --------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/EditableShapes.pptx", SaveFormat.PPTX);

        System.out.println("Export completed: EditableShapes.pptx");
    }
}
```

### Why each line matters

1. **Dependency** – Aspose.Cells `ImageOrPrintOptions` क्लास प्रदान करता है जो वर्कशीट्स को PPTX स्लाइड्स के रूप में रेंडर कर सकता है। Maven के माध्यम से इसे जोड़ने से लाइब्रेरी क्लासपाथ में शामिल हो जाती है।  
2. **Imports** – सही क्लासेस को इम्पोर्ट करने से कोड साफ़ रहता है और पूरी तरह से योग्य नामों से बचा जा सकता है।  
3. **Loading the workbook** – आपको उस सटीक फ़ाइल की ओर इंगित करना होगा जिसमें वे ऑब्जेक्ट्स हों जिन्हें आप निर्यात करना चाहते हैं। पाथ पूर्ण (absolute) या प्रोजेक्ट रूट के सापेक्ष (relative) हो सकता है।  
4. **Export options** – `setEditable(true)` सेट करना **how to export Excel** का मुख्य बिंदु है जिससे परिणामी PowerPoint आकार संपादन योग्य रहते हैं। इस फ़्लैग के बिना, टेक्स्ट बॉक्स स्थिर छवियों में बदल जाते हैं।  
5. **Print area** – `setPrintArea` कॉल निर्यात को उस क्षेत्र तक सीमित करता है जिसमें आपकी रुचि है, जिससे फ़ाइल आकार घटता है और अनावश्यक पंक्तियों/कॉलम हटते हैं। यह सीधे **set print area excel** की आवश्यकता को पूरा करता है।  
6. **Saving** – `SaveFormat.PPTX` कॉन्स्टेंट Aspose.Cells को इमेज या PDF के बजाय PowerPoint फ़ाइल बनाने के लिए बताता है।

#### Expected output

प्रोग्राम चलाने के बाद, PowerPoint में `EditableShapes.pptx` खोलें। आपको एक स्लाइड दिखेगी जो चयनित Excel रेंज को प्रतिबिंबित करती है, और कोई भी टेक्स्ट बॉक्स या चार्ट लेजेंड डबल‑क्लिक करके मूल PowerPoint ऑब्जेक्ट्स की तरह संपादित किए जा सकते हैं।

---

## Excel में प्रिंट एरिया सेट करना

जब आपको केवल वर्कशीट का एक उपसमुच्चय चाहिए, तो **print area** को परिभाषित करने से प्रदर्शन और दृश्य स्पष्टता दोनों में सुधार होता है।

```java
// Example: set print area to the first 10 rows and columns A‑J
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.getPageSetup().setPrintArea("A1:J10");
```

*Tip:* यदि आप बाद में डेटा रेंज बदलते हैं, तो निर्यात करने से पहले `setPrintArea` को फिर से कॉल करें। निर्यात नवीनतम सेटिंग का सम्मान करता है।

---

## XLSX चार्ट को संपादन योग्य PowerPoint चार्ट में बदलना

Aspose.Cells चार्ट को ड्राइंग ऑब्जेक्ट के रूप में मानता है। `setEditable(true)` सक्षम करने से, चार्ट को एक मूल PowerPoint चार्ट में परिवर्तित किया जाता है जिसे संपादित किया जा सकता है (जैसे, सीरीज़, अक्ष शीर्षक बदलना)।

```java
// No extra code needed – the same exportOptions handle chart conversion.
// Just ensure the workbook contains a chart object.
```

यदि आपको कई चार्ट वाले **how to convert xlsx** फ़ाइलों की आवश्यकता है, तो प्रत्येक वर्कशीट के लिए निर्यात दोहराएँ या सक्रिय शीट को समायोजित करने के बाद `Workbook.save` को `SaveFormat.PPTX` के साथ उपयोग करें।

---

## प्रोग्रामेटिक रूप से XLSX को बदलना (बोनस)

PPTX के अलावा, आप वर्कबुक को किसी अन्य फ़ॉर्मेट जैसे PDF या PNG में भी बदलना चाह सकते हैं। वही `ImageOrPrintOptions` क्लास उन लक्ष्यों के लिए काम करता है:

```java
exportOptions.setFormat(ImageFormat.PDF);   // for PDF output
workbook.save("Converted.pdf", SaveFormat.PDF);
```

यह Aspose.Cells की व्यापक **how to convert xlsx** क्षमता को दर्शाता है।

---

## Common pitfalls and best‑practice tips

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| Shapes become images | `setEditable(false)` (default) | `exportOptions.setEditable(true)` को कॉल करें |
| Exported slide is blank | Print area में कोई डेटा शामिल नहीं है | `setPrintArea` को पास की गई रेंज स्ट्रिंग की जाँच करें |
| Chart loses formatting | पुराने Aspose.Cells संस्करण का उपयोग करना | नवीनतम लाइब्रेरी (≥ 23.9) में अपग्रेड करें |
| फ़ाइल आकार बड़ा | पूरी वर्कशीट का निर्यात | Print area को सीमित करें या अनावश्यक पंक्तियों/कॉलम को छुपाएँ |

---

## निष्कर्ष

आप अब **how to export Excel** वर्कबुक को PPTX में पूरी तरह से संपादन योग्य आकारों और चार्टों के साथ निर्यात करना, आउटपुट को केंद्रित करने के लिए **set print area** सेट करना, और सहज प्रस्तुति संपादन के लिए **convert Excel chart** ऑब्जेक्ट्स को बदलना जानते हैं। ऊपर दिया गया पूर्ण, चलाने योग्य Java उदाहरण किसी भी प्रोजेक्ट में डाला जा सकता है जो पहले से Aspose.Cells उपयोग करता है।

**अगले कदम**

* PowerPoint में **convert excel chart** विकल्पों का अन्वेषण करें (जैसे, चार्ट प्रकार बदलना)।  
* इस निर्यात को **set print area excel** ऑटोमेशन के साथ मिलाकर एक वर्कबुक से कई स्लाइड्स बनाएं।  
* इसी `ImageOrPrintOptions` पैटर्न का उपयोग करके अन्य फ़ॉर्मेट (PDF, PNG) में निर्यात करने का प्रयास करें।

विभिन्न रेंज, कई वर्कशीट या कस्टम स्लाइड लेआउट के साथ प्रयोग करने में संकोच न करें। कोडिंग का आनंद लें!

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Excel में प्रिंट एरिया सेट करें और PowerPoint में निर्यात करें](/cells/english/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/)
- [Excel को PowerPoint में बदलें और प्रिंट एरिया सेट करें](/cells/english/net/converting-excel-files-to-other-formats/convert-excel-to-powerpoint-and-set-print-area/)
- [Excel में प्रिंट एरिया सेट करें और PowerPoint में निर्यात करें – चरण‑दर‑चरण गाइड](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}