---
category: general
date: 2026-08-11
description: Java के साथ xlsx को PowerPoint में बदलें – Aspose.Cells का उपयोग करके
  Excel वर्कबुक को PPTX फ़ॉर्मेट में निर्यात करने के लिए चरण‑दर‑चरण गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert xlsx to powerpoint
- excel workbook to powerpoint
- export excel using java
- excel to powerpoint format
- export excel to pptx
language: hi
lastmod: 2026-08-11
og_description: Aspose.Cells for Java का उपयोग करके xlsx को PowerPoint में बदलें।
  जानें कि Excel वर्कबुक को PPTX फ़ॉर्मेट में कैसे निर्यात करें, संपादन योग्य टेक्स्टबॉक्स
  को बनाए रखें, और सामान्य समस्याओं को कैसे संभालें।
og_image_alt: Screenshot of Java code converting an Excel file to a PowerPoint presentation
og_title: Java के साथ xlsx को PowerPoint में बदलें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: convert xlsx to powerpoint with Java – step‑by‑step guide using Aspose.Cells
    to export an Excel workbook to PPTX format.
  headline: convert xlsx to powerpoint with Java – complete guide
  type: TechArticle
- description: convert xlsx to powerpoint with Java – step‑by‑step guide using Aspose.Cells
    to export an Excel workbook to PPTX format.
  name: convert xlsx to powerpoint with Java – complete guide
  steps:
  - name: '**Increase the JVM heap** – launch the program with `-Xmx2g` (or higher)
      if you encounter `OutOfMemoryError`.'
    text: '**Increase the JVM heap** – launch the program with `-Xmx2g` (or higher)
      if you encounter `OutOfMemoryError`.'
  - name: '**Convert worksheets individually** – loop through `workbook.getWorksheets()`
      and save each sheet to a separate PPTX file.'
    text: '**Convert worksheets individually** – loop through `workbook.getWorksheets()`
      and save each sheet to a separate PPTX file.'
  - name: '**Reduce image resolution** – use `saveOptions.setResolution(150)` to lower
      DPI; the default is 300 DPI.'
    text: '**Reduce image resolution** – use `saveOptions.setResolution(150)` to lower
      DPI; the default is 300 DPI.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
- File conversion
title: Java के साथ xlsx को PowerPoint में बदलें – पूर्ण गाइड
url: /hi/java/excel-import-export/convert-xlsx-to-powerpoint-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java के साथ xlsx को PowerPoint में बदलें – पूर्ण गाइड

यदि आपको Java एप्लिकेशन में **convert xlsx to powerpoint** करने की आवश्यकता है, तो यह ट्यूटोरियल आपको सटीक चरण दिखाता है। Aspose.Cells for Java का उपयोग करके, आप एक Excel वर्कबुक को PPTX फ़ाइल में निर्यात कर सकते हैं जबकि संपादन योग्य TextBoxes और सेल फ़ॉर्मेटिंग को संरक्षित रख सकते हैं।

आप सीखेंगे कि Excel वर्कबुक को कैसे लोड करें, PowerPoint फ़ॉर्मेट के लिए सेव ऑप्शन को कैसे कॉन्फ़िगर करें, और परिणामी PPTX फ़ाइल को डिस्क पर कैसे लिखें। गाइड सामान्य विविधताओं को भी कवर करता है, जैसे केवल एक ही वर्कशीट को बदलना या बड़े वर्कबुक को कुशलतापूर्वक संभालना।

## इस ट्यूटोरियल में क्या कवर किया गया है

* आवश्यकताएँ और आवश्यक लाइब्रेरीज़  
* एक TextBox वाले Excel वर्कबुक को लोड करना  
* **excel workbook to powerpoint** रूपांतरण के लिए `ImageOrPrintOptions` को कॉन्फ़िगर करना  
* वर्कबुक को PPTX फ़ाइल के रूप में सहेजना (`export excel to pptx`)  
* आउटपुट की पुष्टि करना और सामान्य समस्याओं का निवारण करना  

गाइड के अंत तक, आपके पास एक स्व-निहित Java प्रोग्राम होगा जो विश्वसनीय रूप से **excel to powerpoint format** रूपांतरण करता है।

## आवश्यकताएँ

शुरू करने से पहले, सुनिश्चित करें कि आपके पास है:

* Java Development Kit (JDK) 8 या उससे ऊपर स्थापित  
* निर्भरता प्रबंधन के लिए Maven या Gradle (उदाहरण में Maven उपयोग किया गया है)  
* Aspose.Cells for Java लाइसेंस फ़ाइल (इवैल्यूएशन संस्करण परीक्षण के लिए काम करता है)  
* `input.xlsx` इनपुट Excel फ़ाइल जिसमें कम से कम एक TextBox आकार हो  

यदि आप Aspose.Cells से परिचित नहीं हैं, तो यह एक शुद्ध‑Java लाइब्रेरी है जो Microsoft Office स्थापित किए बिना काम करती है, जिससे यह सर्वर‑साइड ऑटोमेशन के लिए आदर्श बनती है।

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

`pom.xml` में निम्नलिखित निर्भरता जोड़ें। यह Aspose.Cells for Java का नवीनतम स्थिर संस्करण लाता है।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest release -->
</dependency>
```

> **Pro tip:** उत्पादन में संस्करण संख्या को लॉक रखें ताकि अप्रत्याशित ब्रेकिंग बदलावों से बचा जा सके।

## चरण 2: वह Excel वर्कबुक लोड करें जिसे आप बदलना चाहते हैं

कोड की पहली पंक्ति स्रोत XLSX फ़ाइल से एक `Workbook` इंस्टेंस बनाती है। वर्कबुक में कई वर्कशीट, चार्ट, और TextBox आकार हो सकते हैं।

```java
import com.aspose.cells.*;

public class ExportToPptx {
    public static void main(String[] args) throws Exception {
        // Load the Excel workbook that contains a TextBox
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Why this matters:* वर्कबुक लोड करने से फ़ाइल फ़ॉर्मेट की वैधता जांची जाती है और एक इन‑मेमोरी प्रतिनिधित्व तैयार होता है जिसे लाइब्रेरी अन्य फ़ॉर्मेट में रेंडर कर सकती है।

## चरण 3: PowerPoint आउटपुट के लिए सेव ऑप्शन कॉन्फ़िगर करें

Aspose.Cells रेंडरिंग को नियंत्रित करने के लिए `ImageOrPrintOptions` क्लास का उपयोग करता है। `SaveFormat` को `PPTX` सेट करने से लाइब्रेरी को इमेज के बजाय PowerPoint प्रेज़ेंटेशन जनरेट करने को कहा जाता है।

```java
        // Set up save options to export as PPTX
        ImageOrPrintOptions saveOptions = new ImageOrPrintOptions();
        saveOptions.setSaveFormat(SaveFormat.PPTX);   // TextBoxes remain editable
```

*Why this matters:* जब फ़ॉर्मेट `PPTX` होता है, Aspose.Cells प्रत्येक प्रिंटेबल पेज के लिए एक स्लाइड बनाता है। TextBoxes को PowerPoint आकारों में परिवर्तित किया जाता है जो संपादन योग्य रहते हैं, जो डाउनस्ट्रीम एडिटिंग के लिए आवश्यक है।

## चरण 4: पूरी वर्कबुक (या एकल शीट) को PPTX में निर्यात करें

आप पूरी वर्कबुक, एक विशिष्ट वर्कशीट, या यहाँ तक कि पेज रेंज को भी निर्यात कर सकते हैं। नीचे दिया गया उदाहरण पूरी वर्कबुक को सहेजता है।

```java
        // Export the entire workbook (including the editable TextBox) to PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", saveOptions);
    }
}
```

यदि आप केवल पहली वर्कशीट को बदलना चाहते हैं, तो `save` कॉल को इस प्रकार बदलें:

```java
        // Export only the first worksheet
        workbook.getWorksheets().get(0).getPageSetup().setPrintArea("A1:G20");
        workbook.save("YOUR_DIRECTORY/output.pptx", saveOptions);
```

*Why this matters:* प्रिंट एरिया को नियंत्रित करने से उत्पन्न स्लाइडों की संख्या सीमित होती है, जो बड़े वर्कबुक के लिए प्रदर्शन में सुधार कर सकता है।

## चरण 5: प्रोग्राम चलाएँ और परिणाम की पुष्टि करें

क्लास को संकलित करें और निष्पादित करें:

```bash
mvn compile exec:java -Dexec.mainClass=ExportToPptx
```

निष्पादन के बाद, `output.pptx` को Microsoft PowerPoint या किसी भी संगत व्यूअर में खोलें। आपको दिखना चाहिए:

* वर्कशीट के प्रत्येक प्रिंटेबल पेज के लिए एक स्लाइड  
* सभी सेल डेटा, फ़ॉर्मेटिंग, और चार्ट इमेज के रूप में पुनः निर्मित  
* TextBox आकार संपादन योग्य PowerPoint टेक्स्ट बॉक्स के रूप में संरक्षित  

यदि TextBox स्थैतिक इमेज के रूप में दिखाई देता है, तो दोबारा जांचें कि `saveOptions.setSaveFormat(SaveFormat.PPTX)` सही ढंग से सेट है। **export excel using java** वर्कफ़्लो इस फ़्लैग पर निर्भर करता है ताकि आकार संपादन योग्य रहें।

## बड़े वर्कबुक और मेमोरी खपत को संभालना

जब कई वर्कशीट या उच्च‑रिज़ॉल्यूशन ग्राफ़िक्स वाले वर्कबुक को बदलते हैं, तो मेमोरी उपयोग बढ़ सकता है। इन रणनीतियों पर विचार करें:

1. **JVM heap बढ़ाएँ** – यदि आप `OutOfMemoryError` का सामना करते हैं तो प्रोग्राम को `-Xmx2g` (या अधिक) के साथ लॉन्च करें।  
2. **वर्कशीट को व्यक्तिगत रूप से बदलें** – `workbook.getWorksheets()` पर लूप करें और प्रत्येक शीट को अलग PPTX फ़ाइल में सहेजें।  
3. **इमेज रिज़ॉल्यूशन घटाएँ** – DPI को कम करने के लिए `saveOptions.setResolution(150)` उपयोग करें; डिफ़ॉल्ट 300 DPI है।  

ये समायोजन सुनिश्चित करते हैं कि **export excel to pptx** प्रक्रिया एंटरप्राइज़ परिदृश्यों के लिए स्केलेबल हो।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| लक्षण | कारण | समाधान |
|---------|-------|-----|
| TextBox साधारण टेक्स्ट बन जाता है | `SaveFormat` को `PDF` या किसी अन्य रास्टर फ़ॉर्मेट पर सेट किया गया | `SaveFormat.PPTX` उपयोग करें |
| स्लाइड खाली हैं | प्रिंट एरिया परिभाषित नहीं है और वर्कशीट में कोई प्रिंटेबल कंटेंट नहीं है | `worksheet.getPageSetup().setPrintArea("A1:Z50")` कॉल करें |
| आउटपुट फ़ाइल भ्रष्ट है | अपूर्ण लिखावट क्योंकि JVM जल्दी समाप्त हो गया | प्रोग्राम समाप्त होने से पहले `workbook.save` पूर्ण होने को सुनिश्चित करें |
| प्रदर्शन धीमा है | कई चार्ट वाले बड़े वर्कबुक | केवल आवश्यक शीट्स को निर्यात करें या रिज़ॉल्यूशन घटाएँ |

## रूपांतरण का विस्तार: कस्टम स्लाइड शीर्षक जोड़ना

आप निर्यातित कंटेंट से पहले एक टाइटल स्लाइड डाल सकते हैं, `aspose.slides` लाइब्रेरी से एक नया `Presentation` ऑब्जेक्ट बनाकर और Aspose.Cells द्वारा उत्पन्न PPTX को मर्ज करके।

```java
import com.aspose.slides.*;

public class MergeWithTitle {
    public static void main(String[] args) throws Exception {
        // First, generate the PPTX from Excel (as shown earlier)
        ExportToPptx.main(args);

        // Load the generated PPTX
        Presentation excelPresentation = new Presentation("YOUR_DIRECTORY/output.pptx");

        // Create a new presentation for the title slide
        Presentation finalPresentation = new Presentation();
        ISlide titleSlide = finalPresentation.getSlides().addEmptySlide(finalPresentation.getLayoutSlides().get_Item(0));
        titleSlide.getShapes().addAutoShape(ShapeType.Rectangle, 50, 150, 600, 100)
                .getTextFrame().setText("Quarterly Sales Report");

        // Append the Excel slides
        finalPresentation.getSlides().insertCloneAfter(titleSlide, excelPresentation.getSlides());

        // Save the combined file
        finalPresentation.save("YOUR_DIRECTORY/final_output.pptx", SaveFormat.Pptx);
    }
}
```

## स्टैंडअलोन कनवर्टर के लिए पूर्ण स्रोत कोड

नीचे पूर्ण, तैयार‑चलाने योग्य Java क्लास है जो बुनियादी **convert xlsx to powerpoint** ऑपरेशन करता है। इसे `ExportToPptx.java` के रूप में सहेजें।

```java
import com.aspose.cells.*;

public class ExportToPptx {
    public static void main(String[] args) throws Exception {
        // 1. Load the source Excel file
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Prepare PPTX save options – keep TextBoxes editable
        ImageOrPrintOptions saveOptions = new ImageOrPrintOptions();
        saveOptions.setSaveFormat(SaveFormat.PPTX);

        // 3. Export the workbook (or a specific worksheet) to PowerPoint
        workbook.save("YOUR_DIRECTORY/output.pptx", saveOptions);

        System.out.println("Conversion complete: output.pptx created.");
    }
}
```

क्लास को **चरण 5** में वर्णित अनुसार संकलित और चलाएँ। फ़ाइल लिखे जाने के बाद कंसोल एक पुष्टि संदेश प्रिंट करेगा।

## निष्कर्ष

यह गाइड आपको Aspose.Cells for Java का उपयोग करके **convert xlsx to powerpoint** प्रक्रिया से परिचित कराता है। आपने सीखा कि कैसे:

* TextBoxes वाले Excel वर्कबुक को लोड करें  
* `ImageOrPrintOptions` को सही ढंग से सेट करें ताकि PPTX फ़ाइल उत्पन्न हो  
* पूरी वर्कबुक या चयनित शीट्स को निर्यात करें  
* आउटपुट की पुष्टि करें और सामान्य समस्याओं का निवारण करें  
* अतिरिक्त PowerPoint कंटेंट के साथ रूपांतरण का विस्तार करें  

इस ज्ञान के साथ, आप रिपोर्टिंग पाइपलाइन, स्वचालित प्रेज़ेंटेशन जेनरेटर, या किसी भी Java‑आधारित वर्कफ़्लो में Excel‑to‑PowerPoint रूपांतरण को एकीकृत कर सकते हैं, जिसे **excel to powerpoint format** की आवश्यकता है।

## अगले कदम

* **export excel using java** को अन्य फ़ॉर्मेट जैसे PDF, HTML, या PNG के लिए खोजें।  
* कनवर्टर को Aspose.Slides के साथ मिलाकर प्रोग्रामेटिक रूप से चार्ट, एनीमेशन, या स्पीकर नोट्स जोड़ें।  
* बैच रूपांतरण के लिए प्रदर्शन को अनुकूलित करें, एकल `Workbook` इंस्टेंस को पुन: उपयोग करके और आउटपुट को `ByteArrayOutputStream` में स्ट्रीम करके।  

कोड के साथ प्रयोग करने, सेव ऑप्शन को अनुकूलित करने, और अपने परिणाम समुदाय के साथ साझा करने में संकोच न करें। कोडिंग का आनंद लें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Convert Excel to XPS Format Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-xps-aspose-cells-java/)
- [Convert Excel to HTML Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/excel-to-html-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}