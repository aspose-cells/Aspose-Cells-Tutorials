---
category: general
date: 2026-09-08
description: जावा और Aspose.Cells का उपयोग करके एक्सेल को पावरपॉइंट में निर्यात करना
  सीखें, PPTX आउटपुट में संपादन योग्य टेक्स्ट बॉक्स को संरक्षित रखते हुए।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to powerpoint
- Aspose.Cells Java
- editable text boxes
- ImageOrPrintOptions
- Workbook save
- PowerPoint PPTX export
language: hi
lastmod: 2026-09-08
og_description: Aspose.Cells का उपयोग करके जावा के साथ एक्सेल को पावरपॉइंट में निर्यात
  करें। यह गाइड आपको दिखाता है कि चार्ट टेक्स्ट को संपादन योग्य कैसे रखें और मिनटों
  में PPTX फ़ाइल बनाएं।
og_image_alt: Screenshot of Java code exporting an Excel worksheet to a PowerPoint
  slide
og_title: जावा के साथ एक्सेल को पावरपॉइंट में निर्यात करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to export Excel to PowerPoint using Java and Aspose.Cells,
    preserving editable text boxes in the PPTX output.
  headline: How to export Excel to PowerPoint with Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- PowerPoint
title: जावा के साथ एक्सेल को पावरपॉइंट में निर्यात कैसे करें
url: /hi/java/excel-import-export/how-to-export-excel-to-powerpoint-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java के साथ Excel को PowerPoint में निर्यात कैसे करें

यदि आपको **Excel को PowerPoint में निर्यात** करना है, तो यह ट्यूटोरियल आपको एक साफ़ Java समाधान दिखाता है। **Aspose.Cells Java** का उपयोग करके आप चार्ट फ़ॉर्मेटिंग को बनाए रख सकते हैं और उत्पन्न PPTX फ़ाइल में **editable text boxes** को सक्षम कर सकते हैं।

स्प्रेडशीट को प्रेज़ेंटेशन में निर्यात करना एक सामान्य आवश्यकता है जब आप डेटा‑ड्रिवन चार्ट को स्लाइड डेक में पुन: उपयोग करना चाहते हैं। इस गाइड में आप सीखेंगे कि कैसे:

* एक मौजूदा Excel वर्कबुक लोड करें जिसमें एक चार्ट हो।
* **ImageOrPrintOptions** को कॉन्फ़िगर करें ताकि निर्यात किया गया स्लाइड टेक्स्ट बॉक्स को संपादन योग्य रखे।
* एक ही मेथड कॉल में वर्कशीट को **PowerPoint PPTX** फ़ाइल के रूप में सहेजें।
* एक पूर्ण, स्व-निहित उदाहरण चलाएँ जिसे आप अपने प्रोजेक्ट में कॉपी कर सकते हैं।

एकमात्र पूर्वापेक्षाएँ हैं Java 8 (या नया) रनटाइम और एक वैध Aspose.Cells for Java लाइसेंस। यदि आप फ्री इवैल्यूएशन संस्करण का उपयोग कर रहे हैं, तो आउटपुट में वॉटरमार्क रहेगा, लेकिन कोड समान रूप से काम करता है।

---

## Export Excel to PowerPoint – विकास पर्यावरण सेट अप करें

कोड लिखने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

| आइटम | कारण |
|------|--------|
| **Java Development Kit (JDK) 8+** | उदाहरण को कंपाइल और चलाने के लिए आवश्यक। |
| **Aspose.Cells for Java** लाइब्रेरी | `Workbook`, `ImageOrPrintOptions`, और `SaveFormat` क्लासेज़ प्रदान करती है जो रूपांतरण के लिए उपयोग होती हैं। |
| **एक वैध Aspose.Cells लाइसेंस** (वैकल्पिक) | इवैल्यूएशन वॉटरमार्क हटाता है और पूरी कार्यक्षमता अनलॉक करता है। |
| **एक Excel फ़ाइल (`chartSheet.xlsx`)** जिसमें कम से कम एक चार्ट हो | वह स्रोत वर्कबुक जिसे आप निर्यात करेंगे। |

Aspose.Cells JAR को अपने प्रोजेक्ट की क्लासपाथ में जोड़ें। यदि आप Maven उपयोग कर रहे हैं, तो डिपेंडेंसी शामिल करें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest version -->
</dependency>
```

---

## Editable text boxes के लिए ImageOrPrintOptions कॉन्फ़िगर करें

`ImageOrPrintOptions` क्लास नियंत्रित करती है कि वर्कशीट निर्यात करते समय कैसे रेंडर होती है। `setExportEditableTextBox(true)` सेट करने से Aspose.Cells चार्ट के भीतर टेक्स्ट एलिमेंट्स को PowerPoint में **editable text boxes** के रूप में रखता है, न कि उन्हें स्थिर इमेज में बदलता है।

```java
// Create export options for PowerPoint
ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
exportOptions.setSaveFormat(SaveFormat.PPTX);          // Target format is PPTX
exportOptions.setExportEditableTextBox(true);        // Keep chart text editable
```

क्यों महत्वपूर्ण है: जब आप बाद में PPTX फ़ाइल को PowerPoint में खोलते हैं, तो आप चार्ट के लेबल पर क्लिक करके उसकी सामग्री को सीधे संपादित कर सकते हैं, जो उन प्रेज़ेंटेशन्स के लिए आवश्यक है जिन्हें ऑन‑द‑फ़्लाई समायोजन की जरूरत होती है।

---

## वर्कबुक लोड करें और इसे PPTX फ़ाइल के रूप में निर्यात करें

अब Excel फ़ाइल लोड करें, पिछले चरण के विकल्प लागू करें, और `save` को कॉल करें। `Workbook.save` मेथड आउटपुट पाथ और `ImageOrPrintOptions` इंस्टेंस को स्वीकार करता है, और रूपांतरण को आंतरिक रूप से संभालता है।

```java
// Load the workbook that contains the chart
Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

// Export the first worksheet to PowerPoint using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);
```

**मुख्य बिंदु**

* `Workbook` पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। यदि आप केवल एक शीट निर्यात करना चाहते हैं तो `workbook.getWorksheets().get(0)` से विशिष्ट शीट चुन सकते हैं।
* `save` मेथड डिफ़ॉल्ट रूप से प्रत्येक वर्कशीट के लिए एक स्लाइड वाला PPTX फ़ाइल लिखता है।
* यदि आपके वर्कबुक में कई शीट्स हैं और आपको केवल चार्ट शीट चाहिए, तो सहेजने से पहले अनावश्यक शीट्स को हटा दें या पेजिनेशन को नियंत्रित करने के लिए `ExportOptions.setOnePagePerSheet(false)` का उपयोग करें।

---

## पूर्ण चलाने योग्य उदाहरण

नीचे एक न्यूनतम, पूरी तरह चलाने योग्य Java प्रोग्राम है जो संपूर्ण प्रवाह को दर्शाता है। `YOUR_DIRECTORY` को अपने फ़ाइलों की ओर संकेत करने वाले पूर्ण या सापेक्ष पाथ से बदलें।

```java
import com.aspose.cells.*;

public class ExcelToPowerPointDemo {
    public static void main(String[] args) {
        try {
            // 1. Load the Excel workbook that holds the chart
            Workbook workbook = new Workbook("YOUR_DIRECTORY/chartSheet.xlsx");

            // 2. Prepare export options for PowerPoint and enable editable text boxes
            ImageOrPrintOptions exportOptions = new ImageOrPrintOptions();
            exportOptions.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
            exportOptions.setExportEditableTextBox(true);        // Keep text boxes editable

            // 3. Export the worksheet(s) to a PPTX file
            workbook.save("YOUR_DIRECTORY/output.pptx", exportOptions);

            System.out.println("Export completed successfully. Check output.pptx.");
        } catch (Exception e) {
            System.err.println("Error during export: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**अपेक्षित आउटपुट**

प्रोग्राम चलाने पर यह प्रिंट करेगा:

```
Export completed successfully. Check output.pptx.
```

जब आप `output.pptx` को Microsoft PowerPoint में खोलेंगे, तो आपको एक स्लाइड दिखाई देगी जो Excel चार्ट को प्रतिबिंबित करती है। किसी भी चार्ट लेबल पर डबल‑क्लिक करें और आप सीधे टेक्स्ट को संपादित कर पाएँगे, जिससे यह पुष्टि होती है कि **editable text boxes** सक्रिय हैं।

---

## सामान्य विविधताओं और किनारे के मामलों को संभालना

| स्थिति | अनुशंसित दृष्टिकोण |
|-----------|----------------------|
| **एकाधिक वर्कशीट्स** लेकिन केवल एक चार्ट शीट निर्यात करनी है | `workbook.getWorksheets().removeAt(index)` से अनावश्यक शीट्स को हटाएँ, या `exportOptions.setOnePagePerSheet(false)` सेट करें और फिर मैन्युअली वह शीट चुनें जिसे आप रेंडर करना चाहते हैं। |
| **बड़ी Excel फ़ाइलें** जो मेमोरी पर दबाव डालती हैं | `Workbook` बनाते समय `loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` के साथ स्ट्रीमिंग मोड सक्षम करें। |
| **लाइसेंस सेट नहीं है** (इवैल्यूएशन संस्करण) | उत्पन्न PPTX में वॉटरमार्क रहेगा। `main` की शुरुआत में `License license = new License(); license.setLicense("Aspose.Cells.lic");` जोड़ें ताकि इसे हटाया जा सके। |
| **केवल एक विशिष्ट रेंज निर्यात करनी है** | एक अस्थायी वर्कशीट बनाएं, इच्छित रेंज को `worksheet.getCells().copyRange(...)` से कॉपी करें, और उस अस्थायी शीट को निर्यात करें। |
| **PowerPoint संस्करण संगतता** | Aspose.Cells हमेशा Office Open XML (PPTX) उत्पन्न करता है जो PowerPoint 2007 और बाद के संस्करणों के साथ काम करता है। पुराने PPT फ़ॉर्मेट के लिए `SaveFormat.PPT` बदलें (हालाँकि editable text boxes केवल PPTX में समर्थित हैं)। |

---

## उत्पादन उपयोग के लिए प्रो टिप्स

* **बैच रूपांतरण** – Excel फ़ाइलों की एक डायरेक्टरी पर लूप चलाएँ, एक ही `ImageOrPrintOptions` इंस्टेंस को पुन: उपयोग करके ऑब्जेक्ट निर्माण ओवरहेड को कम करें।
* **परफ़ॉर्मेंस प्रोफ़ाइलिंग** – बड़े फ़ाइलों के लिए `workbook.save` द्वारा लिया गया समय मापें; यदि `OutOfMemoryError` मिलता है तो JVM हीप (`-Xmx2g`) बढ़ाने पर विचार करें।
* **कस्टम स्लाइड लेआउट** – निर्यात के बाद, आप Aspose.Slides for Java का उपयोग करके PPTX को और भी संशोधित कर सकते हैं, जैसे शीर्षक, फुटर जोड़ना, या मास्टर स्लाइड लागू करना।

---

## निष्कर्ष

आप अब जानते हैं कि **Java के साथ Excel को PowerPoint में निर्यात** कैसे किया जाता है, चार्ट की फ़िडेलिटी को बनाए रखते हुए और `ImageOrPrintOptions` के माध्यम से **editable text boxes** को सक्षम किया जाता है। पूर्ण उदाहरण वर्कबुक लोड करने, निर्यात विकल्प कॉन्फ़िगर करने, और केवल तीन संक्षिप्त चरणों में PPTX फ़ाइल सहेजने को दर्शाता है।

अब आप **Aspose.Cells Java चार्ट मैनिपुलेशन**, **कस्टम टेम्प्लेट्स के साथ PowerPoint PPTX निर्यात**, या **एकाधिक स्प्रेडशीट्स का बैच प्रोसेसिंग** जैसे संबंधित विषयों का अन्वेषण कर सकते हैं। विभिन्न `SaveFormat` मानों के साथ प्रयोग करें, इस दृष्टिकोण को Aspose.Slides के साथ मिलाएँ, और अपने रिपोर्टिंग पाइपलाइन में वर्कफ़्लो को एकीकृत करें।

---

![Java code exporting Excel to PowerPoint](/images/export-excel-to-powerpoint.png){: .responsive-img alt="Java कोड का स्क्रीनशॉट जो Excel वर्कशीट को PowerPoint स्लाइड में निर्यात कर रहा है"}

## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Aspose.Cells Java का उपयोग करके Excel में टेक्स्ट बॉक्स बनाना और कॉन्फ़िगर करना](/cells/english/java/images-shapes/create-text-boxes-excel-aspose-cells-java/)
- [Aspose.Cells Java का उपयोग करके Excel चार्ट को SVG के रूप में निर्यात करना](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells Java का उपयोग करके Excel वर्कशीट को PNG में निर्यात करना](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}