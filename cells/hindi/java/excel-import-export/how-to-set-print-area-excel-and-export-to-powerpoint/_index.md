---
category: general
date: 2026-08-20
description: जानेँ कैसे एक्सेल में प्रिंट एरिया सेट करें, फिर Aspose.Cells के साथ
  एक्सेल को PPTX में एक्सपोर्ट करें। यह गाइड आपको वर्कशीट को पावरपॉइंट में बदलने और
  उसे PPTX के रूप में सहेजने की प्रक्रिया दिखाता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- export excel to pptx
- convert worksheet to powerpoint
- save worksheet as powerpoint
language: hi
lastmod: 2026-08-20
og_description: Excel में प्रिंट एरिया सेट करें और फिर Aspose.Cells का उपयोग करके
  Excel को PPTX में निर्यात करें। इस चरण‑दर‑चरण ट्यूटोरियल का पालन करके वर्कशीट को
  PowerPoint में बदलें और इसे PPTX फ़ाइल के रूप में सहेजें।
og_image_alt: Screenshot showing Excel print area set and PPTX export using Aspose.Cells
og_title: एक्सेल में प्रिंट एरिया सेट करें और पावरपॉइंट में निर्यात करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to set print area excel, then export excel to pptx with Aspose.Cells.
    This guide walks you through converting a worksheet to PowerPoint and saving it
    as a PPTX.
  headline: How to set print area excel and export to PowerPoint
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint generation
title: एक्सेल में प्रिंट एरिया कैसे सेट करें और पावरपॉइंट में निर्यात करें
url: /hi/java/excel-import-export/how-to-set-print-area-excel-and-export-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to set print area excel and export to PowerPoint

यदि आपको स्लाइड डेक में डेटा साझा करने से पहले **set print area excel** सेट करने की आवश्यकता है, तो यह ट्यूटोरियल आपको बिल्कुल वही दिखाता है। आप देखेंगे कि प्रिंट एरिया कैसे कॉन्फ़िगर करें, फिर **export excel to pptx** कैसे करें जबकि टेक्स्ट बॉक्स एडिटेबल रहें, ताकि परिणामी PowerPoint आगे के संपादन के लिए तैयार हो।

हम Aspose.Cells for Java का उपयोग करके **convert worksheet to PowerPoint** करेंगे और अंत में **save worksheet as PowerPoint** को PPTX फ़ॉर्मेट में सहेजेंगे। Aspose.Cells JAR के अलावा कोई अतिरिक्त लाइब्रेरी आवश्यक नहीं है। इस गाइड के अंत तक आप कोड को किसी भी Java‑compatible environment में चला सकते हैं और चयनित Excel रेंज के समान एक प्रेज़ेंटेशन बना सकते हैं।

## Prerequisites

- Java Development Kit 17 या बाद का संस्करण  
- Aspose.Cells for Java (आधिकारिक Aspose साइट से डाउनलोड करें)  
- एक Excel वर्कबुक जिसमें वे शैप्स हों जिन्हें आप एडिटेबल रखना चाहते हैं (उदा., `BookWithShapes.xlsx`)  

सुनिश्चित करें कि Aspose.Cells JAR आपके क्लासपाथ में है:

```bash
javac -cp "aspose-cells-23.12.jar" ExportEditableShapesToPptx.java
java -cp ".:aspose-cells-23.12.jar" ExportEditableShapesToPptx
```

## Step 1: Set print area excel using Aspose.Cells

पहला कदम वह रेंज निर्धारित करना है जिसे एक्सपोर्ट किया जाएगा। प्रिंट एरिया सेट करने से कन्वर्ज़न केवल उन सेल्स तक सीमित हो जाता है जिनकी आपको ज़रूरत है और प्रदर्शन में सुधार होता है।

```java
// Load the workbook that contains shapes
Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

// Define the print area for the first worksheet (A1:G30)
workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");
```

**Why this matters** – `setPrintArea` मेथड Aspose.Cells को बताता है कि कौन से सेल्स प्रिंटेबल पेज का हिस्सा हैं। जब आप बाद में **export excel to pptx** करेंगे, तो केवल यह एरिया रेंडर होगा, इसलिए अनावश्यक डेटा स्लाइड में नहीं दिखेगा।

### Pro tip
यदि आपको डायनामिक रेंज चाहिए, तो आप प्रोग्रामेटिकली एड्रेस की गणना कर सकते हैं:

```java
int lastRow = workbook.getWorksheets().get(0).getCells().getMaxDataRow() + 1;
int lastCol = workbook.getWorksheets().get(0).getCells().getMaxDataColumn() + 1;
String range = String.format("A1:%s%d", CellsHelper.columnIndexToName(lastCol - 1), lastRow);
workbook.getWorksheets().get(0).getPageSetup().setPrintArea(range);
```

## Step 2: Export excel to pptx with editable text boxes

प्रिंट एरिया निर्धारित होने के बाद, एक्सपोर्ट विकल्प कॉन्फ़िगर करें। `setExportEditableTextBoxes` को एनेबल करने से शैप्स का टेक्स्ट PowerPoint में एडिटेबल फ़ील्ड के रूप में बना रहता है।

```java
// Create export options and enable editable text boxes in the PPTX
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);
exportOptions.setExportEditableTextBoxes(true);   // keeps text boxes editable
```

**Why this matters** – डिफ़ॉल्ट रूप से Aspose.Cells टेक्स्ट बॉक्स को रास्टराइज़ कर देता है, जिससे वे इमेज का हिस्सा बन जाते हैं। `ExportEditableTextBoxes` को `true` सेट करने से मूल शैप ऑब्जेक्ट्स बरकरार रहते हैं, जिससे उपयोगकर्ता PowerPoint में सीधे टेक्स्ट को संशोधित कर सकते हैं।

## Step 3: Convert worksheet to PowerPoint and save the file

अब वास्तविक कन्वर्ज़न करें। `Workbook.save` मेथड टार्गेट फ़ाइल नाम और पहले तैयार किए गए विकल्प लेता है।

```java
// Export the first worksheet to PPTX using the configured options
workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
```

जब कोड समाप्त हो जाता है, `SheetWithEditableShapes.pptx` में एक ही स्लाइड होगी जो निर्धारित प्रिंट एरिया (`A1:G30`) को दर्शाती है। सभी शैप्स, जिसमें टेक्स्ट बॉक्स भी शामिल हैं, एडिटेबल रहते हैं।

### Expected output
जनरेटेड PPTX को Microsoft PowerPoint में खोलें:

- स्लाइड में **A1 से G30** तक के सेल्स बिल्कुल उसी तरह दिखेंगे जैसे Excel में हैं।  
- मूल वर्कशीट में मौजूद सभी शैप्स PowerPoint शैप्स के रूप में दिखाई देंगे।  
- उन शैप्स के अंदर का टेक्स्ट सीधे PowerPoint में एडिट किया जा सकता है (कोई रास्टराइज़ेशन नहीं)।

## Step 4: Full, runnable example

नीचे पूरा प्रोग्राम दिया गया है। `YOUR_DIRECTORY` को अपने मशीन पर वास्तविक फ़ोल्डर पाथ से बदलें।

```java
import com.aspose.cells.*;

public class ExportEditableShapesToPptx {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook that contains shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/BookWithShapes.xlsx");

        // Step 2: Create export options and enable editable text boxes in the PPTX
        ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
        exportOptions.setSaveFormat(SaveFormat.PPTX);
        exportOptions.setExportEditableTextBoxes(true); // keeps text boxes editable

        // Step 3: Define the print area to limit the exported range
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G30");

        // Step 4: Export the first worksheet to PPTX using the configured options
        workbook.save("YOUR_DIRECTORY/SheetWithEditableShapes.pptx", exportOptions);
    }
}
```

प्रोग्राम को *Prerequisites* सेक्शन में बताए अनुसार चलाएँ। जनरेटेड PowerPoint फ़ाइल उसी डायरेक्टरी में रखी जाएगी जिसे आपने निर्दिष्ट किया है।

## Common questions and edge cases

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मैं कई वर्कशीट्स को एक्सपोर्ट कर सकता हूँ?** | हाँ। `workbook.getWorksheets()` पर लूप करें और प्रत्येक शीट के लिए `save` कॉल करें, वैकल्पिक रूप से आउटपुट फ़ाइलनाम बदलें। |
| **अगर मेरी वर्कबुक में चार्ट्स हों तो?** | डिफ़ॉल्ट रूप से चार्ट्स इमेज के रूप में रेंडर होते हैं। उन्हें एडिटेबल रखने के लिए आपको मैन्युअली PowerPoint शैप्स में बदलना पड़ेगा, जो इस गाइड के दायरे से बाहर है। |
| **क्या प्रिंट एरिया अनिवार्य है?** | नहीं। यदि आप `setPrintArea` को छोड़ देते हैं, तो Aspose.Cells वर्कशीट की पूरी उपयोग की गई रेंज को एक्सपोर्ट करता है। प्रिंट एरिया सेट करने से आपको सटीक नियंत्रण मिलता है। |
| **क्या यह .xlsx फ़ाइलों के साथ काम करता है जो अन्य टूल्स द्वारा बनाई गई हों?** | बिल्कुल। Aspose.Cells किसी भी वैध Office Open XML वर्कबुक को सपोर्ट करता है, चाहे उसकी उत्पत्ति कुछ भी हो। |

## Next steps

- **Save worksheet as PowerPoint** को कस्टम स्लाइड लेआउट्स के साथ: Aspose.Slides की `Presentation` क्लास का उपयोग करके एक्सपोर्टेड स्लाइड को बड़े डेक में मर्ज करें।  
- **Export excel to pptx** को विभिन्न इमेज रिज़ॉल्यूशन के साथ: हाई‑DPI आउटपुट के लिए `exportOptions.setResolution(300)` सेट करें।  
- **Automate batch conversions**: इस कोड को फ़ाइल‑वॉचर के साथ जोड़ें ताकि फ़ोल्डर में कई Excel फ़ाइलों को प्रोसेस किया जा सके।

**set print area excel**, **export excel to pptx**, **convert worksheet to powerpoint**, और **save worksheet as powerpoint** में महारत हासिल करके आप प्रोग्रामेटिकली Excel डेटा को स्लाइड डेक में इंटीग्रेट कर सकते हैं, रिपोर्टिंग पाइपलाइन को सुव्यवस्थित कर सकते हैं और मैन्युअल कॉपी‑पेस्ट कार्य को कम कर सकते हैं।

---


## What Should You Learn Next?


निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}