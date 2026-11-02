---
category: general
date: 2026-09-05
description: Excel में रेंज कॉपी करना, Excel को PowerPoint में निर्यात करना और Excel
  को PPTX में बदलना सीखें, एक पूर्ण Java उदाहरण के साथ।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: hi
lastmod: 2026-09-05
og_description: जावा का उपयोग करके रेंज कॉपी करना और एक्सेल को पॉवरपॉइंट में निर्यात
  करना। एक्सेल को PPTX में कुशलतापूर्वक बदलने के लिए इस चरण‑दर‑चरण गाइड का पालन करें।
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Java में Excel से रेंज कॉपी करके उसे PowerPoint में निर्यात कैसे करें
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: जावा का उपयोग करके एक्सेल से रेंज कॉपी करके पावरपॉइंट में निर्यात कैसे करें
url: /hi/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel से रेंज कॉपी करके उसे PowerPoint में Java के माध्यम से निर्यात कैसे करें

यदि आपको **how to copy range** करना है और फिर **export excel to PowerPoint** करना है, तो यह गाइड आपको एक पूर्ण, तैयार‑चलाने योग्य समाधान देता है। आप देखेंगे कि कैसे एक पिवट‑टेबल‑समेत रेंज को कॉपी किया जाए, कॉपी के लिए एक नया वर्कशीट बनाया जाए, और अंत में एक ही मेथड कॉल से **convert Excel to PPTX** किया जाए।

रेंज कॉपी करना और वर्कबुक निर्यात करना सामान्य आवश्यकता है जब आप प्रोग्रामेटिकली रिपोर्ट, स्लाइड डेक या डैशबोर्ड बनाते हैं। इस ट्यूटोरियल के अंत तक आपके पास एक Java प्रोग्राम होगा जो:

* मौजूदा `.xlsx` फ़ाइल लोड करता है।
* रेंज `A1:H20` (पिवट टेबल सहित) को नई शीट में कॉपी करता है।
* वर्कबुक को एक संपादन योग्य `.pptx` प्रस्तुति के रूप में सहेजता है।

आपको केवल Aspose.Cells for Java लाइब्रेरी की आवश्यकता है; अतिरिक्त कोई डिपेंडेंसी नहीं चाहिए।

## आवश्यकताएँ

* Java 17 (या नया) स्थापित हो।
* Maven या Gradle डिपेंडेंसी मैनेजमेंट के लिए।
* Aspose.Cells for Java 23.9 (या नवीनतम संस्करण) – नीचे दिखाए गए Maven स्निपेट की तरह इसे अपने प्रोजेक्ट में जोड़ें।
* एक Excel फ़ाइल (`input.xlsx`) जिसमें वह डेटा और पिवट टेबल हो जिसे आप कॉपी करना चाहते हैं।

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## चरण 1: फ़ाइल से वर्कबुक लोड करें

पहला ऑपरेशन **how to copy range** में स्रोत वर्कबुक को खोलना है। यह आपको वर्कशीट, सेल और पिवट टेबल तक पहुँच देता है।

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*यह कदम क्यों?*  
फ़ाइल को लोड करने से Excel दस्तावेज़ का इन‑मेमोरी प्रतिनिधित्व बनता है, जिससे आप मूल फ़ाइल को छुए बिना उसकी सामग्री को बदल सकते हैं।

## चरण 2: स्रोत वर्कशीट प्राप्त करें जिसमें डेटा है

आमतौर पर पहली शीट में वह डेटा होता है जिसे आप कॉपी करना चाहते हैं। आप इसे इंडेक्स द्वारा प्राप्त कर सकते हैं।

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

यदि आपका वर्कबुक पिवट टेबल को किसी अलग शीट पर रखता है, तो `0` को उपयुक्त इंडेक्स से बदलें या `get("SheetName")` का उपयोग करें।

## चरण 3: कॉपी की गई रेंज के लिए नई वर्कशीट जोड़ें

डेस्टिनेशन शीट बनाना कॉपी किए गए डेटा को अलग करता है और बाद के निर्यात को साफ़ बनाता है।

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

आप शीट का नाम कुछ भी रख सकते हैं; “Copy” नाम स्पष्ट रूप से दर्शाता है कि इसमें डुप्लिकेट रेंज है।

## चरण 4: रेंज (how to copy range) को पिवट टेबल सहित कॉपी करें

अब हम मुख्य **how to copy range** ऑपरेशन करते हैं। `copyRange` मेथड मान और फॉर्मेटिंग दोनों को कॉपी करता है, और पिवट टेबल की परिभाषा को संरक्षित रखता है।

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*`CopyOptions` का उपयोग क्यों करें?*  
`CopyOptions` इंस्टेंस प्रदान करने से आप यह तय कर सकते हैं कि क्या कॉपी किया जाए (जैसे फ़ॉर्मूले, कॉलम चौड़ाई)। डिफ़ॉल्ट कंस्ट्रक्टर सब कुछ कॉपी करता है, जो **copy pivot table sheet** की सटीक प्रतिलिपि बनाने के लिए आदर्श है।

## चरण 5: वर्कबुक को संपादन योग्य PowerPoint प्रस्तुति के रूप में निर्यात करने के विकल्प तैयार करें

PowerPoint में निर्यात `ImageOrPrintOptions` के माध्यम से किया जाता है। `SaveFormat.PPTX` सेट करने से Aspose.Cells को इमेज के बजाय PowerPoint फ़ाइल जनरेट करने का निर्देश मिलता है।

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

यदि आपको कस्टम लेआउट चाहिए तो `pptOptions` के माध्यम से स्लाइड आयाम, DPI और अन्य प्रस्तुति सेटिंग्स भी समायोजित कर सकते हैं।

## चरण 6: वर्कबुक को PPTX फ़ाइल के रूप में सहेजें (convert excel to pptx)

अंत में, `workbook.save` को PPTX विकल्पों के साथ कॉल करें। यह कदम **how to export excel** को एक स्लाइड डेक में बदलता है।

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

प्रोग्राम समाप्त होने के बाद, `output.pptx` में एक ही स्लाइड होगी जहाँ कॉपी की गई रेंज Excel में जैसी थी वैसी ही दिखेगी, पिवट टेबल कंट्रोल सहित।

### अपेक्षित आउटपुट

`output.pptx` को Microsoft PowerPoint या किसी संगत व्यूअर में खोलें। आपको एक स्लाइड दिखेगी जिसमें रेंज `A1:H20` प्रदर्शित होगी, सेल रंग, बॉर्डर और पिवट टेबल लेआउट संरक्षित रहेगा। स्लाइड पूरी तरह से संपादन योग्य है—आप टेबल को किसी भी मूल PowerPoint सामग्री की तरह मूव, रिसाइज़ या फॉर्मेट कर सकते हैं।

## पूर्ण चलाने योग्य उदाहरण

सभी चरणों को मिलाकर आपको एक स्व-निहित Java क्लास मिलती है:

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

IDE से या कमांड लाइन के माध्यम से क्लास चलाएँ:

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

फ़ाइल लिखे जाने के बाद आपको पुष्टि संदेश दिखाई देगा।

## सामान्य प्रश्न और किनारे के मामले

| प्रश्न | उत्तर |
|----------|--------|
| **क्या मैं गैर‑सतत रेंज कॉपी कर सकता हूँ?** | कई क्षेत्रों को शामिल करने वाले नामित रेंज के साथ `copyRange` का उपयोग करें, या प्रत्येक ब्लॉक के लिए `copyRange` को कई बार कॉल करें। |
| **यदि स्रोत शीट में कई पिवट टेबल हों तो क्या होगा?** | कॉपी किए गए आयताकार के भीतर की प्रत्येक पिवट टेबल ट्रांसफ़र हो जाती है। आयताकार के बाहर की टेबल को अलग से कॉपी करना होगा। |
| **मैं कई शीट्स को अलग‑अलग स्लाइड्स के रूप में कैसे निर्यात करूँ?** | वर्कशीट्स पर लूप करें, प्रत्येक को एक अस्थायी शीट में कॉपी करें, और प्रत्येक इटरेशन में `pptOptions` के साथ `workbook.save` कॉल करें, साथ ही `Presentation` API के ज़रिए समान PPTX में जोड़ें। |
| **क्या जनरेट किया गया PPTX संपादन योग्य है?** | हाँ। निर्यात मूल PowerPoint ऑब्जेक्ट बनाता है, इसलिए आप टेक्स्ट बदल सकते हैं, टेबल को री‑शेप कर सकते हैं या बाद में एनीमेशन जोड़ सकते हैं। |
| **बड़ी वर्कबुक्स के बारे में क्या?** | उच्च फिडेलिटी के लिए `pptOptions.setDpi(300)` बढ़ाएँ, लेकिन मेमोरी उपयोग का ध्यान रखें; आवश्यक होने पर शीट्स को बैच में प्रोसेस करें। |

## प्रो टिप्स

* **कॉलम चौड़ाई संरक्षित रखें** – यदि आपको सटीक चौड़ाई चाहिए तो कॉपी करने से पहले `CopyOptions.setColumnWidth(true)` सेट करें।
* **कस्टम स्लाइड आकार उपयोग करें** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` से 16:9 प्रस्तुति मिलती है।
* **टाइटल स्लाइड जोड़ें** – निर्यात के बाद, Aspose.Slides के साथ PPTX खोलें और शीर्षक व तिथि वाली स्लाइड को पहले जोड़ें।

## निष्कर्ष

अब आप **how to copy range** को Excel वर्कबुक से, **export excel to PowerPoint**, और **convert excel to pptx** को Java के माध्यम से कर सकते हैं। ऊपर बताए गए छह चरणों का पालन करके आप रिपोर्ट जनरेशन को स्वचालित कर सकते हैं, लाइव डेटा से स्लाइड डेक बना सकते हैं, और पिवट‑टेबल कार्यक्षमता को बरकरार रख सकते हैं।

### आगे क्या?

* **copy pivot table sheet** के विभिन्न रूपों का अन्वेषण करें जैसे केवल पिवट कैश कॉपी करना।
* इस वर्कफ़्लो को **Aspose.Slides** के साथ मिलाकर कस्टम एनीमेशन या ब्रांडिंग जोड़ें।
* शेड्यूल्ड जॉब में दर्जनों वर्कबुक्स के लिए बैच प्रोसेसिंग को ऑटोमेट करें।

विकल्पों के साथ प्रयोग करने और कोड को अपने रिपोर्टिंग पाइपलाइन के अनुसार अनुकूलित करने में संकोच न करें। यदि कोई समस्या आती है, तो Aspose.Cells for Java दस्तावेज़ `CopyOptions` और `ImageOrPrintOptions` पर गहरी जानकारी प्रदान करता है। Happy coding!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स इस गाइड में दिखाए गए तकनीकों पर आधारित निकटतम विषयों को कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Excel को PowerPoint में निर्यात करने का तरीका – चरण‑दर‑चरण गाइड](/cells/english/net/converting-excel-files-to-other-forms/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Aspose.Cells Java का उपयोग करके Excel में कई कॉलम कॉपी करने का तरीका : एक पूर्ण गाइड](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Aspose.Cells for .NET का उपयोग करके Excel को PowerPoint में बदलने का तरीका : एक पूर्ण गाइड](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}