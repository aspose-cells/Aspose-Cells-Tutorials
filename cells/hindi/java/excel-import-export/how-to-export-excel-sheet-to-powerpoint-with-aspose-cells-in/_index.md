---
category: general
date: 2026-09-27
description: Aspose.Cells का उपयोग करके जावा में Excel शीट को PowerPoint में निर्यात
  करने का तरीका – एक चरण‑दर‑चरण गाइड जो यह भी दिखाता है कि Excel वर्कबुक को PowerPoint
  प्रस्तुति में कैसे परिवर्तित किया जाए।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export excel sheet to powerpoint
- convert excel workbook to powerpoint presentation
language: hi
lastmod: 2026-09-27
og_description: Java में Aspose.Cells का उपयोग करके Excel शीट को PowerPoint में निर्यात
  करने का तरीका। पूर्ण कोड के साथ Excel वर्कबुक को PowerPoint प्रस्तुति में बदलना
  सीखें।
og_image_alt: Java code snippet that exports an Excel sheet to a PowerPoint file using
  Aspose.Cells
og_title: Excel शीट को PowerPoint में निर्यात कैसे करें – Aspose.Cells के साथ Java
  गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: How to export Excel sheet to PowerPoint with Aspose.Cells in Java –
    a step‑by‑step guide that also shows how to convert Excel workbook to PowerPoint
    presentation.
  headline: How to export Excel sheet to PowerPoint with Aspose.Cells in Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- Document conversion
title: जावा में Aspose.Cells के साथ Excel शीट को PowerPoint में निर्यात कैसे करें
url: /hi/java/excel-import-export/how-to-export-excel-sheet-to-powerpoint-with-aspose-cells-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ Java में Excel शीट को PowerPoint में निर्यात कैसे करें

यदि आपको **Excel शीट को PowerPoint में निर्यात करने का तरीका** चाहिए, तो यह ट्यूटोरियल आपको एक पूर्ण, तैयार‑से‑चलाने वाला समाधान प्रदान करता है। आप बिल्कुल देखेंगे कि **Excel वर्कबुक को PowerPoint प्रस्तुति में कैसे परिवर्तित किया जाए** जबकि संपादन योग्य टेक्स्ट बॉक्स और मूल फ़ॉर्मेटिंग को संरक्षित रखा जाए।

यह गाइड मानता है कि आपके पास एक कार्यशील Java विकास वातावरण और एक वैध Aspose.Cells for Java लाइसेंस है। लेख के अंत तक आपके पास एक Java प्रोग्राम होगा जो Excel वर्कबुक को लोड करता है, पहली वर्कशीट को निर्यात करता है, और एक `.pptx` फ़ाइल लिखता है जिसे Microsoft PowerPoint में खोला और संपादित किया जा सकता है।

## आवश्यकताएँ

| Requirement | Why it matters |
|-------------|----------------|
| Java 17 or later | Aspose.Cells आधुनिक Java रनटाइम्स को समर्थन देता है और बेहतर प्रदर्शन प्रदान करता है। |
| Aspose.Cells for Java (version 23.10 or newer) | लाइब्रेरी में `Workbook.save(..., SaveFormat.PPTX)` ओवरलोड शामिल है जो रूपांतरण के लिए उपयोग होता है। |
| A licensed copy of Aspose.Cells | बिना लाइसेंस के लाइब्रेरी मूल्यांकन मोड में चलती है और वॉटरमार्क जोड़ती है। |
| An Excel file that contains at least one editable textbox | रूपांतरण टेक्स्टबॉक्स को PowerPoint में एक संपादन योग्य आकार के रूप में संरक्षित रखता है। |
| IDE or build tool (e.g., Maven, Gradle) | उदाहरण कोड को संकलित और चलाने के लिए। |

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

यदि आप Maven का उपयोग करते हैं, तो `pom.xml` में निम्नलिखित निर्भरता जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

Gradle के लिए, इस स्निपेट को `build.gradle` में रखें:

```gradle
implementation 'com.aspose:aspose-cells:23.10:jdk17'
```

> **Pro tip:** यदि आपको सर्वर पर केवल रनटाइम पर लाइब्रेरी की आवश्यकता है, तो निर्भरता को `provided` स्कोप में घोषित करें।

## चरण 2: Excel वर्कबुक तैयार करें

`WorkbookWithTextbox.xlsx` नाम की एक Excel फ़ाइल बनाएं जिसमें पहली वर्कशीट पर एक संपादन योग्य टेक्स्टबॉक्स हो। टेक्स्टबॉक्स को Excel में **Insert → Text Box** के माध्यम से डाला जा सकता है। फ़ाइल को ऐसे डायरेक्टरी में सहेजें जिसे आप Java से संदर्भित कर सकें, उदाहरण के लिए `src/main/resources`।

## चरण 3: रूपांतरण कोड लिखें

`ExportEditableTextbox` नाम की एक Java क्लास बनाएं। नीचे दिया गया कोड पूर्ण इम्पोर्ट्स, त्रुटि संभालना, और टिप्पणियों को शामिल करता है जो प्रत्येक ऑपरेशन को समझाते हैं।

```java
package com.example.excel2ppt;

import com.aspose.cells.SaveFormat;
import com.aspose.cells.Workbook;

/**
 * Demonstrates how to export an Excel sheet to PowerPoint while preserving
 * editable text boxes. The example uses Aspose.Cells for Java.
 */
public class ExportEditableTextbox {

    public static void main(String[] args) throws Exception {
        // --------------------------------------------------------------------
        // Step 1: Load the Excel workbook that contains the editable textbox.
        // --------------------------------------------------------------------
        String workbookPath = "src/main/resources/WorkbookWithTextbox.xlsx";
        Workbook workbook = new Workbook(workbookPath);

        // --------------------------------------------------------------------
        // Step 2: Export the first worksheet to a PowerPoint presentation.
        //         The SaveFormat.PPTX option writes a .pptx file that PowerPoint
        //         can open and edit. The textbox remains editable.
        // --------------------------------------------------------------------
        String outputPath = "src/main/resources/Worksheet.pptx";
        workbook.save(outputPath, SaveFormat.PPTX);

        System.out.println("Conversion successful. PowerPoint saved to: " + outputPath);
    }
}
```

### यह क्यों काम करता है

* `Workbook` पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। इसे लोड करने से सभी वर्कशीट्स, चार्ट्स और शैप्स पार्स हो जाते हैं।
* `workbook.save(..., SaveFormat.PPTX)` Aspose.Cells के अंतर्निहित रूपांतरण इंजन को सक्रिय करता है। यह इंजन Excel की सेल्स, पंक्तियों और शैप्स को PowerPoint स्लाइड्स में मैप करता है, और संपादन योग्य टेक्स्ट बॉक्स को PowerPoint शैप्स के रूप में संरक्षित रखता है।
* यह मेथड प्रत्येक वर्कशीट के लिए एक स्लाइड लिखता है। इस उदाहरण में पहली वर्कशीट ही एकमात्र स्लाइड बन जाती है।

## चरण 4: प्रोग्राम चलाएँ

अपने बिल्ड टूल के साथ क्लास को संकलित और निष्पादित करें:

```bash
mvn compile exec:java -Dexec.mainClass=com.example.excel2ppt.ExportEditableTextbox
```

या, यदि आप Gradle का उपयोग करते हैं:

```bash
gradle run --args='com.example.excel2ppt.ExportEditableTextbox'
```

प्रोग्राम समाप्त होने के बाद, Microsoft PowerPoint में `Worksheet.pptx` खोलें। आपको एक स्लाइड दिखेगी जो Excel शीट को प्रतिबिंबित करती है, और Excel में बनाया गया टेक्स्टबॉक्स एक संपादन योग्य आकार के रूप में दिखाई देगा जिसे आप डबल‑क्लिक करके संशोधित कर सकते हैं।

## चरण 5: कई वर्कशीट्स को संभालना (वैकल्पिक)

यदि आपको वर्कबुक की **सभी** वर्कशीट्स निर्यात करनी हैं, तो एकल‑वर्कशीट कॉल को लूप से बदलें:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    workbook.save("Worksheet_" + i + ".pptx", SaveFormat.PPTX);
}
```

प्रत्येक इटरेशन एक अलग PowerPoint फ़ाइल बनाता है (`Worksheet_0.pptx`, `Worksheet_1.pptx`, …)। कई स्लाइड्स वाली एक ही प्रस्तुति के लिए, जब आप `save` एक बार कॉल करते हैं, तो Aspose.Cells स्वचालित रूप से प्रत्येक वर्कशीट के लिए एक स्लाइड जोड़ देता है; अतिरिक्त कोड की आवश्यकता नहीं है।

## एज केस और सर्वोत्तम प्रथाएँ

| Situation | Recommended approach |
|-----------|----------------------|
| Large workbook (hundreds of MB) | JVM हीप (`-Xmx4g`) बढ़ाएँ और मेमोरी समाप्ति त्रुटियों से बचने के लिए वर्कशीट्स को व्यक्तिगत रूप से निर्यात करने पर विचार करें। |
| Password‑protected workbook | `LoadOptions` का उपयोग करके लोड करने से पहले पासवर्ड प्रदान करें: `new LoadOptions(LoadFormat.XLSX, "pwd")`। |
| Need to keep Excel formulas | PowerPoint फ़ॉर्मूले का समर्थन नहीं करता; रूपांतरण के दौरान उन्हें स्थिर मानों के रूप में रेंडर किया जाता है। |
| Custom slide layout required | रूपांतरण के बाद, उत्पन्न `.pptx` को Aspose.Slides for Java के साथ संशोधित करें ताकि स्लाइड मास्टर्स को समायोजित किया जा सके या एनीमेशन जोड़े जा सकें। |
| Running in a web service | फ़ाइल लिखने के बजाय आउटपुट को सीधे HTTP प्रतिक्रिया में स्ट्रीम करें: `workbook.save(response.getOutputStream(), SaveFormat.PPTX);` |

## अपेक्षित आउटपुट

उदाहरण चलाने से `Worksheet.pptx` नाम की फ़ाइल बनती है। इसे PowerPoint में खोलने पर दिखता है:

* एक स्लाइड जो दृश्य रूप से पहली Excel वर्कशीट से मेल खाती है।
* एक संपादन योग्य टेक्स्टबॉक्स जो बिल्कुल उसी स्थान पर स्थित है जहाँ वह Excel में था।
* मूलभूत सेल फ़ॉर्मेटिंग (फ़ॉन्ट आकार, रंग, बॉर्डर) संरक्षित रहती है।

कंसोल प्रिंट करता है:

```
Conversion successful. PowerPoint saved to: src/main/resources/Worksheet.pptx
```

## निष्कर्ष

अब आप Aspose.Cells for Java का उपयोग करके **Excel शीट को PowerPoint में निर्यात करने** का तरीका जानते हैं, और आप वास्तविक परिदृश्यों में **Excel वर्कबुक को PowerPoint प्रस्तुति में परिवर्तित करने** को भी समझते हैं। यह समाधान एकल‑वर्कशीट निर्यात, बहु‑वर्कशीट वर्कबुक के लिए काम करता है, और आगे की स्लाइड कस्टमाइज़ेशन के लिए Aspose.Slides के साथ विस्तारित किया जा सकता है।

---

### अगले कदम

* **Aspose.Slides for Java** का अन्वेषण करें ताकि रूपांतरण के बाद एनीमेशन, चार्ट्स, या कस्टम स्लाइड मास्टर्स जोड़े जा सकें।  
* ऐसे वर्कबुक को रूपांतरित करने का प्रयास करें जिनमें चार्ट्स हों; Aspose.Cells चार्ट्स को मूल PowerPoint चार्ट ऑब्जेक्ट्स के रूप में रेंडर करता है।  
* Excel फ़ाइलों की एक डायरेक्टरी पढ़कर और प्रत्येक फ़ाइल के लिए एक PowerPoint बनाकर बैच प्रोसेसिंग की जाँच करें।

कोड के साथ प्रयोग करने, फ़ाइल पाथ को अनुकूलित करने, और रूपांतरण को बड़े Java एप्लिकेशनों जैसे रिपोर्टिंग सर्विसेज या स्वचालित दस्तावेज़ पाइपलाइन में एकीकृत करने में स्वतंत्र महसूस करें। कोडिंग का आनंद लें!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में निपुण होने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [How to Export Excel to PowerPoint – Step‑by‑Step Guide](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells: A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}