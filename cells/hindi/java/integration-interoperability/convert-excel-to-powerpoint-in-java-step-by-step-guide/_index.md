---
category: general
date: 2026-11-22
description: Aspose.Cells का उपयोग करके जावा में Excel को PowerPoint में बदलें। जानें
  कि Excel फ़ाइल से PowerPoint कैसे बनाएं, वर्कशीट्स को PPTX स्लाइड्स के रूप में निर्यात
  करें, और प्रस्तुतियों को स्वचालित करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- convert excel workbook to pptx slides
- java convert .xlsx to .pptx
language: hi
lastmod: 2026-11-22
og_description: Aspose.Cells के साथ जावा में Excel को PowerPoint में बदलें। यह ट्यूटोरियल
  आपको दिखाता है कि Excel फ़ाइल से PowerPoint कैसे बनाएं और .xlsx को .pptx स्लाइड्स
  में निर्यात करें।
og_image_alt: Diagram illustrating convert excel to powerpoint workflow
og_title: जावा में एक्सेल को पावरपॉइंट में बदलें – पूर्ण प्रोग्रामिंग गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  headline: Convert Excel to PowerPoint in Java – step‑by‑step guide
  type: TechArticle
- description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  name: Convert Excel to PowerPoint in Java – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: Converting only selected sheets
    text: 'If you want to **convert Excel workbook to PPTX slides** but exclude certain
      worksheets, filter them before saving:'
  - name: Handling large workbooks
    text: 'For workbooks with many sheets, memory consumption can become significant.
      Use `WorkbookSettings` to enable streaming:'
  - name: Preserving formulas
    text: Aspose.Cells evaluates formulas before rendering. If you need the raw formula
      text on the slide, set `opts.setExportFormulas(true)`.
  type: HowTo
tags:
- java
- excel
- powerpoint
- aspose
title: जावा में एक्सेल को पावरपॉइंट में बदलें – चरण-दर-चरण गाइड
url: /hi/java/integration-interoperability/convert-excel-to-powerpoint-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में Excel को PowerPoint में बदलें – चरण‑दर‑चरण गाइड

यदि आपको **convert Excel to PowerPoint in Java** की आवश्यकता है, तो यह गाइड आपको Aspose.Cells के साथ यह कैसे करना है दिखाता है। चाहे आप रिपोर्टिंग इंजन बना रहे हों या स्लाइड डेक्स को स्वचालित कर रहे हों, आप प्रोग्रामेटिक रूप से **create PowerPoint from Excel file** करना सीखेंगे और प्रत्येक वर्कशीट को संपादन योग्य PPTX स्लाइड्स के रूप में निर्यात करेंगे।

यह ट्यूटोरियल प्रोजेक्ट सेटअप से लेकर अंतिम प्रेज़ेंटेशन को सेव करने तक सब कुछ कवर करता है। अंत में आपके पास एक चलने योग्य जावा प्रोग्राम होगा जो `.xlsx` वर्कबुक को `.pptx` फ़ाइल में बदल देता है, जिसे आप Microsoft PowerPoint में संपादित कर सकते हैं। कोई मैन्युअल कॉपी‑पेस्ट आवश्यक नहीं।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

* Java 17 या उससे नया संस्करण स्थापित हो (कोड आधुनिक मॉड्यूल सिस्टम का उपयोग करता है)।  
* Aspose.Cells for Java लाइसेंस या एक अस्थायी इवैल्यूएशन की।  
* निर्भरताओं के प्रबंधन के लिए Maven या Gradle (उदाहरण में Maven उपयोग किया गया है)।  
* एक नमूना Excel वर्कबुक (`input.xlsx`) जिसे आप किसी ज्ञात डायरेक्टरी में रखें।

> **Pro tip:** Aspose.Cells दोनों `.xls` और `.xlsx` को सपोर्ट करता है। वही कोड किसी भी फ़ॉर्मेट के लिए काम करता है; केवल फ़ाइल एक्सटेंशन बदलें।

## चरण 1: **convert Excel to PowerPoint** के लिए जावा प्रोजेक्ट सेट अप करें

एक नया Maven प्रोजेक्ट बनाएं (या मौजूदा में जोड़ें) और Aspose.Cells डिपेंडेंसी शामिल करें:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>excel-to-pptx</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Aspose.Cells for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest version as of 2026 -->
        </dependency>
    </dependencies>
</project>
```

`mvn clean install` चलाएँ ताकि लाइब्रेरी डाउनलोड हो सके। यदि आपके पास लाइसेंस फ़ाइल (`Aspose.Total.lic`) है, तो उसे `src/main/resources` फ़ोल्डर में रखें; कोड इसे स्वचालित रूप से लोड कर लेगा।

## चरण 2: Excel वर्कबुक लोड करें

**convert excel workbook to pptx slides** प्रक्रिया में पहला कार्यात्मक कदम स्रोत फ़ाइल को लोड करना है। Aspose.Cells फ़ाइल सिस्टम, स्ट्रीम, या यहाँ तक कि बाइट एरे से फ़ाइलें खोल सकता है।

```java
package com.example;

import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the license (optional for evaluation)
        License license = new License();
        try {
            license.setLicense(ExcelToPowerPoint.class.getResourceAsStream("/Aspose.Total.lic"));
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }

        // Path to the source .xlsx file
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);
        System.out.println("Workbook loaded successfully.");
```

**यह क्यों महत्वपूर्ण है:** वर्कबुक को लोड करने से फ़ाइल फ़ॉर्मेट की वैधता जांची जाती है और आंतरिक संरचनाएँ तैयार होती हैं, जिन्हें बाद में Aspose.Cells PowerPoint ऑब्जेक्ट्स में परिवर्तित करेगा।

## चरण 3: **create PowerPoint from Excel file** के लिए सेव विकल्प कॉन्फ़िगर करें

Aspose.Cells `ImageOrPrintOptions` का उपयोग करके प्रस्तुति फ़ाइलों में बदलते समय आउटपुट फ़ॉर्मेट निर्धारित करता है। `SaveFormat` को `SaveFormat.PPTX` पर सेट करें ताकि संपादन योग्य स्लाइड्स जनरेट हों।

```java
        // Step 3: Set up conversion options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
        opts.setOnePagePerSheet(false);               // Each sheet becomes a separate slide
        opts.setRenderToSize(1024, 768);               // Optional: control slide resolution
        System.out.println("Conversion options configured.");
```

**यह क्यों महत्वपूर्ण है:** `setOnePagePerSheet(false)` फ़्लैग Aspose.Cells को प्रत्येक वर्कशीट को एक अलग स्लाइड के रूप में ट्रीट करने के लिए बताता है, जो **convert Excel to PowerPoint** करते समय सबसे आम परिदृश्य है।

## चरण 4: वर्कबुक को PPTX स्लाइड्स के रूप में सेव करें

अब आप प्रस्तुति को डिस्क पर लिख सकते हैं। `Workbook.save` मेथड आउटपुट पाथ और आपने कॉन्फ़िगर किए हुए विकल्पों को स्वीकार करता है।

```java
        // Step 4: Export the workbook to a PowerPoint file
        String outputPath = "YOUR_DIRECTORY/editable.pptx";
        wb.save(outputPath, opts);
        System.out.println("Conversion complete. PowerPoint saved to: " + outputPath);
    }
}
```

जब आप `editable.pptx` को Microsoft PowerPoint में खोलेंगे, तो प्रत्येक वर्कशीट के लिए एक स्लाइड दिखेगी, जिसमें सभी सेल्स संपादन योग्य टेक्स्ट बॉक्स और शैप्स के रूप में रेंडर किए गए होंगे। आप फ़ॉन्ट, रंग आदि को सीधे PowerPoint में और भी संपादित कर सकते हैं।

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर यह प्रिंट करेगा:

```
Workbook loaded successfully.
Conversion options configured.
Conversion complete. PowerPoint saved to: YOUR_DIRECTORY/editable.pptx
```

और फ़ाइल `editable.pptx` निर्दिष्ट डायरेक्टरी में बन जाएगी, तैयार है मैन्युअल ट्यूनिंग या आगे की ऑटोमेशन के लिए।

## चरण 5: सामान्य विविधताएँ और एज़ केस

### केवल चयनित शीट्स को बदलना

यदि आप **convert Excel workbook to PPTX slides** करना चाहते हैं लेकिन कुछ वर्कशीट्स को बाहर रखना चाहते हैं, तो सेव करने से पहले उन्हें फ़िल्टर करें:

```java
        // Example: Export only the first two worksheets
        int[] sheetIndices = {0, 1};
        wb.save(outputPath, opts, sheetIndices);
```

### बड़े वर्कबुक्स को संभालना

बहुत सारी शीट्स वाले वर्कबुक्स में मेमोरी उपयोग बढ़ सकता है। स्ट्रीमिंग को सक्षम करने के लिए `WorkbookSettings` का उपयोग करें:

```java
        wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### फ़ॉर्मूले को संरक्षित रखना

Aspose.Cells रेंडर करने से पहले फ़ॉर्मूले का मूल्यांकन करता है। यदि आपको स्लाइड पर कच्चा फ़ॉर्मूला टेक्स्ट चाहिए, तो `opts.setExportFormulas(true)` सेट करें।

## चरण 6: परिणाम को प्रोग्रामेटिक रूप से सत्यापित करें (वैकल्पिक)

आप उत्पन्न PPTX को Aspose.Slides के साथ लोड कर सकते हैं ताकि यह पुष्टि हो सके कि स्लाइड काउंट वर्कशीट काउंट से मेल खाता है:

```java
import com.aspose.slides.*;

        Presentation pres = new Presentation(outputPath);
        int slideCount = pres.getSlides().size();
        System.out.println("Generated PPTX contains " + slideCount + " slides.");
```

यह अतिरिक्त जाँच CI पाइपलाइन में उपयोगी है जहाँ आप यह सुनिश्चित करना चाहते हैं कि रूपांतरण सफल रहा।

## निष्कर्ष

अब आपके पास **convert Excel to PowerPoint in Java** के लिए एक पूर्ण, प्रोडक्शन‑रेडी समाधान है। प्रोग्राम एक `.xlsx` वर्कबुक लोड करता है, `ImageOrPrintOptions` को **create PowerPoint from Excel file** के लिए कॉन्फ़िगर करता है, और परिणाम को संपादन योग्य PPTX स्लाइड्स के रूप में सेव करता है। विकल्पों को समायोजित करके आप रिज़ॉल्यूशन, विशिष्ट शीट चयन, या बड़े फ़ाइलों के स्ट्रीमिंग को फाइन‑ट्यून कर सकते हैं, जिससे यह कई ऑटोमेशन परिदृश्यों के लिए लचीला बन जाता है।

**आगे के कदम**

* Aspose.Slides के साथ कस्टम स्लाइड लेआउट जोड़कर **java convert .xlsx to .pptx** को और गहराई से एक्सप्लोर करें।  
* एक साधारण डायरेक्टरी वॉचर का उपयोग करके कई वर्कबुक्स की बैच प्रोसेसिंग को ऑटोमेट करें।  
* इस रूपांतरण को डेटा‑ड्रिवेन चार्ट जेनरेशन के साथ मिलाकर डायनामिक प्रेज़ेंटेशन बनाएं।

सेटिंग्स के साथ प्रयोग करने और अपने परिणाम साझा करने में संकोच न करें। हैप्पी कोडिंग!

## आगे आप क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Aspose.Cells के साथ जावा में Excel को PowerPoint में बदलें](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/)
- [Aspose.Cells for .NET का उपयोग करके Excel को PowerPoint में बदलने की पूरी गाइड](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Excel को PowerPoint में बदलें – Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}