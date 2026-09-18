---
category: general
date: 2026-09-18
description: Aspose.Cells का उपयोग करके जावा में JSON को Excel में निर्यात करें। JSON
  को Excel में डालना सीखें, JSON को Excel में परिवर्तित करें, और वर्कबुक को XLSX के
  रूप में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export json to excel
- insert json into excel
- how to insert json
- convert json to excel
- save workbook as xlsx
language: hi
lastmod: 2026-09-18
og_description: Aspose.Cells for Java का उपयोग करके JSON को Excel में निर्यात करें।
  चरण‑दर‑चरण ट्यूटोरियल दिखाता है कि JSON को Excel में कैसे डालें, JSON को Excel में
  कैसे परिवर्तित करें, और वर्कबुक को XLSX के रूप में कैसे सहेजें।
og_image_alt: Aspose.Cells Java code inserting JSON array into a single Excel cell
og_title: Aspose.Cells के साथ JSON को Excel में निर्यात करें – Java गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  headline: Export JSON to Excel with Aspose.Cells in Java
  type: TechArticle
- description: Export JSON to Excel using Aspose.Cells in Java. Learn to insert JSON
    into Excel, convert JSON to Excel, and save workbook as XLSX.
  name: Export JSON to Excel with Aspose.Cells in Java
  steps:
  - name: Prepare your development environment.
    text: Prepare your development environment.
  - name: Define the JSON data source.
    text: Define the JSON data source.
  - name: Create a workbook and worksheet.
    text: Create a workbook and worksheet.
  - name: Insert JSON into Excel using a Smart Marker.
    text: Insert JSON into Excel using a Smart Marker.
  - name: Process the Smart Marker so the JSON appears in a single cell.
    text: Process the Smart Marker so the JSON appears in a single cell.
  - name: Save the workbook as an XLSX file.
    text: Save the workbook as an XLSX file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: जावा में Aspose.Cells के साथ JSON को एक्सेल में निर्यात करें
url: /hi/java/excel-import-export/export-json-to-excel-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells in Java के साथ JSON को Excel में निर्यात करें

यदि आपको **JSON को Excel में निर्यात** करना है, तो यह गाइड Aspose.Cells for Java का उपयोग करके एक पूर्ण समाधान दिखाता है। आप देखेंगे कि JSON को Excel में कैसे डालें, JSON को Excel में कैसे बदलें, और अंत में **वर्कबुक को XLSX के रूप में सहेजें** बिना अपने IDE से निकले।

API बनाते समय, रिपोर्टिंग डैशबोर्ड या डेटा‑माइग्रेशन टूल्स बनाते समय JSON डेटा के साथ काम करना आम है। मैन्युअल कॉपी‑पेस्ट करने के बजाय, नीचे दिया गया तरीका पूरी पाइपलाइन को स्वचालित करता है ताकि आप प्रोग्रामेटिक रूप से Excel फ़ाइलें बना सकें।

## JSON को Excel में निर्यात – चरण‑दर‑चरण गाइड

निम्नलिखित अनुभाग आपको प्रत्येक आवश्यक चरण के माध्यम से ले जाएंगे:

1. अपने विकास पर्यावरण को तैयार करें।  
2. JSON डेटा स्रोत को परिभाषित करें।  
3. एक वर्कबुक और वर्कशीट बनाएं।  
4. Smart Marker का उपयोग करके JSON को Excel में डालें।  
5. Smart Marker को प्रोसेस करें ताकि JSON एक ही सेल में दिखाई दे।  
6. वर्कबुक को XLSX फ़ाइल के रूप में सहेजें।

इस ट्यूटोरियल के अंत तक आपके पास एक चलने योग्य Java प्रोग्राम होगा जो `JsonExport.xlsx` फ़ाइल बनाता है जिसमें JSON एरे सेल **A1** में होगा।

## पूर्वापेक्षाएँ

- Java Development Kit 8 या नया।  
- निर्भरताओं को प्रबंधित करने के लिए Maven या Gradle।  
- Aspose.Cells for Java (लेखन के समय उपलब्ध नवीनतम संस्करण, 24.10)।  
- Java सिंटैक्स और JSON फ़ॉर्मेट का बुनियादी ज्ञान।

> **Pro tip:** Aspose.Cells एक व्यावसायिक लाइब्रेरी है, लेकिन एक मुफ्त इवैल्यूएशन लाइसेंस विकास और परीक्षण के लिए काम करता है।

## चरण 1: अपना Java प्रोजेक्ट सेट अप करें

अपने `pom.xml` (Maven) या `build.gradle` (Gradle) में Aspose.Cells निर्भरता जोड़ें।

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

**Gradle**

```groovy
implementation 'com.aspose:aspose-cells:24.10'
```

निर्भरता हल हो जाने के बाद, आप आवश्यक क्लासेस इम्पोर्ट कर सकते हैं:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;
```

## चरण 2: JSON डेटा स्रोत को परिभाषित करें

JSON स्ट्रिंग ऑब्जेक्ट्स की एक एरे को दर्शाती है। वास्तविक प्रोजेक्ट में आप इसे फ़ाइल, REST एंडपॉइंट, या डेटाबेस से पढ़ सकते हैं। उदाहरण के लिए हम JSON को सीधे कोड में एम्बेड करते हैं।

```java
// Step 2: Define the JSON data source (an array of objects)
String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";
```

**Why this matters:** Aspose.Cells `ArrayAsSingle` विकल्प का उपयोग करने पर JSON एरे को एक ही सेल के रूप में ले सकता है। इससे एरे को पंक्तियों और कॉलम में विभाजित करने की आवश्यकता नहीं रहती, जो कच्चे JSON पेलोड को निर्यात करने के लिए आदर्श है।

## चरण 3: एक वर्कबुक बनाएं और पहली वर्कशीट प्राप्त करें

`Workbook` ऑब्जेक्ट पूरे Excel फ़ाइल को दर्शाता है। पहली वर्कशीट (इंडेक्स 0) वह जगह है जहाँ हम JSON रखेंगे।

```java
// Step 3: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Explanation:** पैरामीटर के बिना `Workbook` को इंस्टैंशिएट करने से एक खाली वर्कबुक डिफ़ॉल्ट शीट के साथ बनता है। यदि आपके परिदृश्य में कई डेटा सेट की आवश्यकता है तो आप बाद में और शीट्स जोड़ सकते हैं।

## चरण 4: Smart Marker का उपयोग करके JSON को Excel में डालें

Smart Markers प्लेसहोल्डर होते हैं जिन्हें Aspose.Cells रनटाइम पर डेटा से बदलता है। मार्कर `&=jsonArray(ArrayAsSingle)` इंजन को बताता है कि पूरी JSON एरे को एक ही सेल में लिखें।

```java
// Step 4: Insert a Smart Marker that tells Aspose.Cells to treat the JSON array as a single cell
worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");
```

**Why use a Smart Marker?** यह डेटा‑बाइंडिंग लॉजिक को एब्स्ट्रैक्ट करता है, जिससे आप स्रोत फ़ॉर्मेट (JSON) पर ध्यान केंद्रित कर सकते हैं न कि लो‑लेवल सेल मैनिपुलेशन पर।

## चरण 5: Smart Marker नाम को JSON डेटा से जोड़ें

आपको मार्कर पहचानकर्ता (`jsonArray`) को वास्तविक JSON स्ट्रिंग से बाइंड करना होगा।

```java
// Step 5: Associate the Smart Marker name with the JSON data
workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);
```

**Note:** `setDataSource` मेथड किसी भी ऑब्जेक्ट को स्वीकार करता है जिसे Smart Marker इंजन सीरियलाइज़ कर सकता है, जिसमें JSON स्ट्रिंग्स, Java कलेक्शन, या DataTables शामिल हैं।

## चरण 6: Smart Markers को प्रोसेस करें ताकि JSON एरे सेल में लिखी जाए

`processSmartMarkers()` को कॉल करने से मार्कर को बाउंड JSON से बदल दिया जाता है।

```java
// Step 6: Process the Smart Markers so the JSON array is written into the cell
workbook.processSmartMarkers();
```

यदि JSON खराब फॉर्मेट में है, तो Aspose.Cells `SmartMarkerException` फेंकेगा। प्रोडक्शन‑ग्रेड मजबूती के लिए कॉल को try‑catch ब्लॉक में रैप करें।

## चरण 7: वर्कबुक को XLSX फ़ाइल के रूप में सहेजें

अंत में, वर्कबुक को डिस्क पर लिखें। फ़ाइल एक्सटेंशन आउटपुट फ़ॉर्मेट निर्धारित करता है; `.xlsx` का उपयोग करने से आधुनिक Office Open XML फ़ॉर्मेट सुनिश्चित होता है।

```java
// Step 7: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/JsonExport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

**Result:** `JsonExport.xlsx` खोलने पर JSON एरे बिल्कुल उसी तरह दिखेगा जैसा `jsonData` में है, जो सेल **A1** में स्थित है।

## पूर्ण चलने योग्य उदाहरण

नीचे एक स्व-निहित Java क्लास है जिसे आप कॉपी, पेस्ट और चलाकर उपयोग कर सकते हैं।

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.SmartMarkerException;

/**
 * Demonstrates how to export JSON to Excel using Aspose.Cells.
 * The program inserts a JSON array into a single cell and saves the workbook as XLSX.
 */
public class JsonToExcelExporter {
    public static void main(String[] args) {
        // 1. Define the JSON data source (an array of objects)
        String jsonData = "[{\"Name\":\"John\",\"Score\":85},{\"Name\":\"Anna\",\"Score\":92}]";

        try {
            // 2. Create a new workbook and obtain the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.getWorksheets().get(0);

            // 3. Insert a Smart Marker that treats the JSON array as a single cell
            worksheet.getCells().putValue(0, 0, "&=jsonArray(ArrayAsSingle)");

            // 4. Bind the Smart Marker name to the JSON string
            workbook.getSmartMarkers().setDataSource("jsonArray", jsonData);

            // 5. Process Smart Markers – this writes the JSON into cell A1
            workbook.processSmartMarkers();

            // 6. Save the workbook as an XLSX file
            String outputPath = "JsonExport.xlsx";
            workbook.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (SmartMarkerException e) {
            System.err.println("Error processing Smart Markers: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error: " + e.getMessage());
        }
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर प्रिंट होता है:

```
Workbook saved to JsonExport.xlsx
```

**JsonExport.xlsx** खोलने पर सेल **A1** में यह दिखता है:

```
[{"Name":"John","Score":85},{"Name":"Anna","Score":92}]
```

## सामान्य विविधताएँ और किनारी मामलों

| स्थिति | कोड को कैसे अनुकूलित करें |
|-----------|----------------------|
| **बड़ी JSON पेलोड** ( > 1 MB) | JVM हीप साइज (`-Xmx2g`) बढ़ाएँ ताकि `OutOfMemoryError` से बचा जा सके। |
| **एकाधिक JSON ऑब्जेक्ट्स** जिन्हें अलग-अलग पंक्तियों की आवश्यकता है | `ArrayAsSingle` के बजाय `ArrayAsRows` का उपयोग करें और मार्कर को POJOs के संग्रह से मैप करें। |
| **CSV में सहेजना** | `workbook.save(outputPath)` को `workbook.save(outputPath, com.aspose.cells.SaveFormat.CSV);` से बदलें। |
| **हेडर पंक्ति जोड़ना** | Smart Marker डालने से पहले `worksheet.getCells().putValue(0, 0, "JSON Payload");` में एक स्थिर स्ट्रिंग लिखें। |
| **भिन्न डायरेक्टरी का उपयोग** | डायरेक्टरी मौजूद है यह सुनिश्चित करें या `new java.io.File(dir).mkdirs();` से बनाएं। |

## प्रोडक्शन उपयोग के टिप्स

- **Validate JSON** को Aspose.Cells को पास करने से पहले वैलिडेट करें ताकि रनटाइम एक्सेप्शन से बचा जा सके।  
- **Use try‑with‑resources** का उपयोग करें जब आप बाहरी स्रोतों से JSON पढ़ने के लिए कोई स्ट्रीम खोलें।  
- **Lock the workbook** यदि कई थ्रेड्स एक ही फ़ाइल को एक साथ लिख सकते हैं।  
- **License registration**: एप्लिकेशन स्टार्टअप पर `com.aspose.cells.License license = new com.aspose.cells.License(); license.setLicense("Aspose.Cells.lic");` कॉल करें।

## अगले कदम

अब जब आप **JSON को Excel में निर्यात** कर सकते हैं, तो संबंधित क्षमताओं का अन्वेषण करने पर विचार करें:

- **Insert JSON into Excel** को फ़ॉर्मेटिंग के साथ: Smart Marker प्रोसेस करने के बाद सेल स्टाइल लागू करें।  
- **Convert JSON to Excel** टेबल्स: JSON ऑब्जेक्ट्स को पंक्तियों और कॉलम में मैप करें।

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स इस गाइड में प्रदर्शित तकनीकों पर आधारित निकटतम संबंधित विषयों को कवर करते हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Aspose.Cells Java का उपयोग करके Excel में JSON डेटा आयात करें: एक व्यापक गाइड](/cells/english/java/import-export/import-json-data-excel-aspose-cells-java/)
- [Aspose.Cells for Java का उपयोग करके Excel में कई पंक्तियाँ कैसे डालें](/cells/english/java/cell-operations/excel-automation-aspose-cells-java-insert-multiple-rows/)
- [Java और Aspose.Cells का उपयोग करके Excel में छवियाँ कैसे डालें](/cells/english/java/images-shapes/insert-image-into-excel-java-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}