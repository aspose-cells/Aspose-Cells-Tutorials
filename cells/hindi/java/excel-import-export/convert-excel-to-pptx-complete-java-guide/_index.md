---
category: general
date: 2026-06-30
description: Aspose.Cells Java का उपयोग करके Excel को PPTX में बदलें – संपादन योग्य
  आकार, PptxSaveOptions, और संपादन योग्य वस्तुओं को निर्यात करने के साथ चरण‑दर‑चरण
  गाइड।
draft: false
keywords:
- convert excel to pptx
- aspose.cells
- java excel to powerpoint
- pptxsaveoptions
- export editable objects
language: hi
og_description: Aspose.Cells Java का उपयोग करके Excel को PPTX में बदलें – जानें कैसे
  PptxSaveOptions के साथ शैप्स को संपादन योग्य रखा जाए।
og_title: 'Excel को PPTX में परिवर्तित करें: पूर्ण Java गाइड'
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Convert Excel to PPTX using Aspose.Cells Java – step‑by‑step guide
    with editable shapes, PptxSaveOptions, and export editable objects.
  headline: 'Convert Excel to PPTX: Complete Java Guide'
  type: TechArticle
- description: Convert Excel to PPTX using Aspose.Cells Java – step‑by‑step guide
    with editable shapes, PptxSaveOptions, and export editable objects.
  name: 'Convert Excel to PPTX: Complete Java Guide'
  steps:
  - name: Add the Aspose.Cells dependency.
    text: Add the Aspose.Cells dependency.
  - name: Load your Excel workbook.
    text: Load your Excel workbook.
  - name: Enable `exportEditableObjects` on `PptxSaveOptions`.
    text: Enable `exportEditableObjects` on `PptxSaveOptions`.
  - name: Save the workbook as a PPTX file.
    text: Save the workbook as a PPTX file.
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- PowerPoint
- Automation
title: 'एक्सेल को PPTX में बदलें: पूर्ण जावा गाइड'
url: /hi/java/excel-import-export/convert-excel-to-pptx-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को PPTX में बदलें: पूर्ण Java गाइड

क्या आपको कभी **Excel को PPTX में बदलने** की जरूरत पड़ी है लेकिन यह नहीं पता था कि कौन सी लाइब्रेरी आपके टेक्स्ट बॉक्स और शेप्स को एडिटेबल रखेगी? आप अकेले नहीं हैं। इस ट्यूटोरियल में हम **Aspose.Cells for Java** का उपयोग करके एक व्यावहारिक समाधान दिखाएंगे जो न केवल वर्कबुक को PowerPoint प्रेजेंटेशन में बदलता है बल्कि एडिटेबल ऑब्जेक्ट्स को भी संरक्षित रखता है ताकि आप बाद में उन्हें संशोधित कर सकें।

हम सब कुछ कवर करेंगे—Aspose.Cells JAR को प्रोजेक्ट में जोड़ना, **export editable objects** के लिए `PptxSaveOptions` को कॉन्फ़िगर करना, और अंत में फ़ाइल को सहेजना। अंत तक आप एक ही Java मेथड चलाकर पूरी तरह एडिटेबल PPTX प्राप्त कर पाएँगे—कोई मैन्युअल कॉपी‑पेस्टिंग नहीं।

## पूर्वापेक्षाएँ

- **Java Development Kit (JDK) 8+** – ट्यूटोरियल का परीक्षण JDK 11 पर किया गया था।
- **Maven** या कोई भी बिल्ड टूल जो आप पसंद करते हैं (Gradle भी काम करता है)।
- Aspose.Cells for Java का **लाइसेंस** (आप परीक्षण के लिए एक मुफ्त टेम्पररी लाइसेंस से शुरू कर सकते हैं)।
- एक Excel फ़ाइल (`shapes.xlsx`) जिसमें कम से कम एक शेप या टेक्स्ट बॉक्स हो जिसे आप PowerPoint में बनाए रखना चाहते हैं।

यदि इनमें से कोई भी चीज़ अपरिचित लग रही हो, तो घबराएँ नहीं—इन्हें सेट अप करने में सिर्फ कुछ मिनट लगते हैं।

## चरण 1: Aspose.Cells निर्भरता जोड़ें

सबसे पहले, लाइब्रेरी को अपने प्रोजेक्ट में लाएँ। Maven के साथ, अपने `pom.xml` में निम्न स्निपेट जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** यदि आप Gradle का उपयोग कर रहे हैं, तो समकक्ष है `implementation 'com.aspose:aspose-cells:24.10'`।  
> 
> बिल्ड फ़ाइल को संपादित करने के बाद अपने प्रोजेक्ट को रिफ्रेश करना याद रखें ताकि JAR डाउनलोड हो सके।

## चरण 2: Excel वर्कबुक लोड करें

अब लाइब्रेरी उपलब्ध है, हम स्रोत फ़ाइल खोल सकते हैं। `Workbook` क्लास सभी भारी काम करती है:

```java
import com.aspose.cells.Workbook;

public class ExcelToPptxConverter {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the Excel workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");
        // Continue with conversion...
    }
}
```

`Workbook` क्यों उपयोग करें? यह पूरे Excel फ़ाइल—वर्कशीट्स, सेल्स, चार्ट्स, और हमारे लिए सबसे महत्वपूर्ण **एडिटेबल शेप्स**—को एब्स्ट्रैक्ट करता है। वर्कबुक लोड करना हल्का है; असली जादू तब आता है जब हम Aspose को बताते हैं कि इसे कैसे एक्सपोर्ट करना है।

## चरण 3: Editable Objects के लिए PptxSaveOptions कॉन्फ़िगर करें

यदि आप केवल `workbook.save("output.pptx")` कॉल करते हैं, तो Aspose अधिकांश शेप्स को रास्टराइज़ कर देगा और उन्हें स्थैतिक इमेज में बदल देगा। उन्हें एडिटेबल रखने के लिए हमें `PptxSaveOptions` के अंदर `exportEditableObjects` फ़्लैग को सक्षम करना होगा।

```java
import com.aspose.cells.PptxSaveOptions;

        // Step 3: Create PPTX save options and enable editable objects
        PptxSaveOptions pptxOptions = new PptxSaveOptions();
        pptxOptions.setExportEditableObjects(true); // <-- key setting
```

### `export editable objects` वास्तव में क्या करता है?

जब इसे `true` पर सेट किया जाता है, तो Aspose Excel के टेक्स्ट बॉक्स, शेप्स, और SmartArt को नेटिव PowerPoint ऑब्जेक्ट्स में बदल देता है। इसका मतलब है कि कन्वर्ज़न के बाद आप PPTX को Microsoft PowerPoint में खोल सकते हैं, किसी शेप को चुन सकते हैं, उसका रंग बदल सकते हैं, या टेक्स्ट एडिट कर सकते हैं—जैसे आपने इसे सीधे PowerPoint में बनाया हो। इस फ़्लैग के बिना, ये तत्व फ्लैट इमेज बन जाते हैं और आप वह लचीलापन खो देते हैं।

## चरण 4: वर्कबुक को PPTX फ़ाइल के रूप में सहेजें

वर्कबुक लोड हो गया है और विकल्प तैयार हैं, अंतिम लाइन सीधी है:

```java
        // Step 4: Save the workbook as a PPTX file using the configured options
        workbook.save("YOUR_DIRECTORY/shapes.pptx", pptxOptions);
        System.out.println("Conversion complete! Check your PPTX file.");
    }
}
```

`main` मेथड चलाएँ, और आपको आपके Excel फ़ाइल के बगल में एक नई `shapes.pptx` दिखनी चाहिए। इसे PowerPoint में खोलें—आपके मूल शेप्स और टेक्स्ट बॉक्स पूरी तरह एडिटेबल होंगे।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ रखते हुए, यहाँ पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PptxSaveOptions;

public class ExcelToPptxConverter {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook (make sure the path is correct)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/shapes.xlsx");

        // Configure PPTX options to keep shapes editable
        PptxSaveOptions pptxOptions = new PptxSaveOptions();
        pptxOptions.setExportEditableObjects(true); // preserve text boxes & shapes

        // Save as PPTX
        workbook.save("YOUR_DIRECTORY/shapes.pptx", pptxOptions);
        System.out.println("Conversion complete! Check your PPTX file.");
    }
}
```

### अपेक्षित आउटपुट

```
Conversion complete! Check your PPTX file.
```

`shapes.pptx` खोलें → किसी भी शेप को चुनें → उसका टेक्स्ट, रंग, या आकार संपादित करें। यदि आप इन बदलावों को प्रतिबिंबित होते देखते हैं, तो आपने सफलतापूर्वक **convert excel to pptx** को एडिटेबल ऑब्जेक्ट्स के साथ पूरा कर लिया है।

## सामान्य किनारे मामलों को संभालना

| स्थिति | ध्यान रखने योग्य बातें | सुझाया गया समाधान |
|-----------|-------------------|-----------------|
| **बड़ी वर्कबुक ( > 200 MB )** | कन्वर्ज़न के दौरान मेमोरी उपयोग में तेज़ी से वृद्धि हो सकती है। | JVM हीप बढ़ाएँ (`-Xmx2g`) या कन्वर्ज़न से पहले वर्कबुक को छोटे हिस्सों में विभाजित करें। |
| **असमर्थित चार्ट प्रकार** | कुछ Excel चार्ट सुविधाएँ (जैसे 3‑D मैप्स) PowerPoint में पूरी तरह से मैप नहीं होतीं। | सेव करने से पहले उन चार्ट्स को `Chart.toImage()` का उपयोग करके मैन्युअली इमेज में बदलें। |
| **लाइसेंस अनुपलब्ध** | Aspose.Cells आउटपुट PPTX में वॉटरमार्क जोड़ देगा। | परीक्षण के लिए एक अस्थायी मुफ्त लाइसेंस (`License.setLicense("Aspose.Total.lic")`) लागू करें; प्रोडक्शन के लिए पूर्ण लाइसेंस प्राप्त करें। |
| **पाथ में स्पेस हैं** | स्पेस वाले Windows पाथ्स `FileNotFoundException` का कारण बन सकते हैं। | एस्केप्ड बैकस्लैश (`C:\\My Documents\\shapes.xlsx`) या Java `Path` API का उपयोग करें। |

## बोनस: कई शीट्स को अलग-अलग स्लाइड्स में बदलना

यदि आप चाहते हैं कि प्रत्येक वर्कशीट अपनी स्वयं की स्लाइड बन जाए, तो आप वर्कबुक की वर्कशीट्स पर लूप कर सकते हैं और प्रत्येक को अलग‑अलग सहेज सकते हैं:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.PptxSaveOptions;

Workbook wb = new Workbook("YOUR_DIRECTORY/multiSheet.xlsx");
PptxSaveOptions opts = new PptxSaveOptions();
opts.setExportEditableObjects(true);

int sheetCount = wb.getWorksheets().getCount();
for (int i = 0; i < sheetCount; i++) {
    Worksheet sheet = wb.getWorksheets().get(i);
    // Create a temporary workbook containing only this sheet
    Workbook temp = new Workbook();
    temp.getWorksheets().addCopy(sheet);
    temp.getWorksheets().removeAt(0); // remove the default empty sheet
    String outPath = String.format("YOUR_DIRECTORY/slide_%d.pptx", i + 1);
    temp.save(outPath, opts);
    System.out.println("Saved slide: " + outPath);
}
```

## दृश्य अवलोकन

![Excel से PPTX में रूपांतरण प्रवाह दिखाने वाला आरेख – वर्कबुक लोड करना, PptxSaveOptions कॉन्फ़िगर करना, और संपादन योग्य PowerPoint के रूप में सहेजना](https://example.com/convert-excel-to-pptx-diagram.png "excel को pptx प्रवाह आरेख")

*छवि वैकल्पिक पाठ*: **Excel से PPTX में रूपांतरण प्रवाह दिखाने वाला आरेख** – यह छवि वैकल्पिक पाठ आवश्यकता को पूरा करता है जबकि मुख्य कीवर्ड को सुदृढ़ करता है।

## पुनरावलोकन

हमने Aspose.Cells for Java का उपयोग करके **Excel को PPTX में बदलने** के बारे में बताया, जिसमें `PptxSaveOptions` के माध्यम से **एडिटेबल शेप्स** को संरक्षित रखने पर ध्यान दिया गया। चरण इस प्रकार हैं:

1. Aspose.Cells निर्भरता जोड़ें।
2. अपने Excel वर्कबुक को लोड करें।
3. `PptxSaveOptions` पर `exportEditableObjects` को सक्षम करें।
4. वर्कबुक को PPTX फ़ाइल के रूप में सहेजें।

अब आपके पास एक पुन: उपयोग योग्य स्निपेट है जिसे आप किसी भी Java प्रोजेक्ट में डाल सकते हैं—कोई मैन्युअल कॉपी‑पेस्ट नहीं, कोई फॉर्मेटिंग खोना नहीं।

## आगे क्या?

- [Java में Aspose.Cells का उपयोग करके Excel को PDF में कैसे बदलें: चरण-दर-चरण गाइड](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Aspose.Cells Java का उपयोग करके Excel को HTML में बदलें: चरण-दर-चरण गाइड](/cells/english/java/workbook-operations/excel-to-html-aspose-cells-java/)
- [Aspose.Cells का उपयोग करके Java में Excel वर्कशीट को JPEG में बदलें: चरण-दर-चरण गाइड](/cells/english/java/workbook-operations/convert-excel-worksheet-jpeg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}