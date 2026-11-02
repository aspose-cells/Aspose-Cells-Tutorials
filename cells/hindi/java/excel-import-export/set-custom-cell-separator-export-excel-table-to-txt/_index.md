---
category: general
date: 2026-07-16
description: Aspose.Cells का उपयोग करके Excel तालिका को TXT में निर्यात करते समय कस्टम
  सेल विभाजक सेट करें। जानें कि Excel सूत्रों को टेक्स्ट में कैसे निर्यात करें और
  वर्कशीट को TXT फ़ाइल के रूप में कैसे सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: hi
lastmod: 2026-07-16
og_description: Aspose.Cells में कस्टम सेल सेपरेटर सेट करने से आप Excel तालिका को
  सटीक फ़ॉर्मेटिंग के साथ TXT में निर्यात कर सकते हैं। Excel फ़ॉर्मूले को टेक्स्ट
  में निर्यात करें और वर्कशीट को आसानी से TXT फ़ाइल के रूप में सहेजें।
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: कस्टम सेल विभाजक सेट करें – एक्सेल तालिका को TXT में निर्यात करें
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: कस्टम सेल सेपरेटर सेट करें – एक्सेल टेबल को TXT में निर्यात करें
url: /hi/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कस्टम सेल सेपरेटर सेट करें – एक्सेल टेबल को TXT में एक्सपोर्ट करें

कस्टम सेल सेपरेटर सेट करना वह गुप्त मसाला है जिसकी आपको आवश्यकता होती है जब आप एक्सेल शीट से एक साफ़ टेक्स्ट डम्प चाहते हैं। क्या आपने कभी सोचा है कि **export excel table to txt** कैसे किया जाए बिना कॉमा और लाइन‑ब्रेक के गड़बड़ में फँसे? इस ट्यूटोरियल में हम Aspose.Cells for Java का उपयोग करके पूरी प्रक्रिया को समझेंगे, वर्कबुक लोड करने से लेकर **save worksheet as txt file** तक, जिसमें आप अपनी पसंद का डिलिमिटर चुन सकते हैं।

## आप क्या सीखेंगे

- टेक्स्ट एक्सपोर्ट के लिए **set custom cell separator** कैसे सेट करें।
- **export excel formulas to text** के सटीक चरण, जिससे मूल्यांकित मान आपके साथ रहें।
- **export excel data as plain text** करने के तरीके, जबकि लेआउट को संरक्षित रखें।
- एक पूर्ण, तैयार‑चलाने योग्य कोड नमूना जिसे आप अपने प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

इस गाइड के अंत तक आप किसी भी एक्सेल वर्कबुक को ले सकते हैं, एक पाइप (`|`), टैब (`\t`) या कोई भी पसंदीदा अक्षर चुन सकते हैं, और एक साफ़, डिलिमिटेड टेक्स्ट फ़ाइल बना सकते हैं जिसे डाउनस्ट्रीम सिस्टम पसंद करेंगे।

### पूर्वापेक्षाएँ

- Java 8 या नया स्थापित हो।
- Maven (या कोई भी बिल्ड टूल) ताकि Aspose.Cells for Java लाइब्रेरी को प्राप्त किया जा सके।
- एक सैंपल वर्कबुक (`TableDemo.xlsx`) जिसमें फ़ॉर्मूले वाली टेबल हो।

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं—कोई अतिरिक्त फालतू नहीं, सिर्फ़ व्यावहारिक कदम।

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

**set custom cell separator** करने से पहले, आपको क्लासपाथ पर Aspose.Cells JAR चाहिए। सबसे आसान तरीका Maven के माध्यम से है:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

यदि आप Gradle पसंद करते हैं, तो XML को समकक्ष `implementation 'com.aspose:aspose-cells:24.10'` से बदलें। एक बार निर्भरता हल हो जाने पर, आप एक्सेल फ़ाइलों के साथ काम करने वाला जावा कोड लिखने के लिए तैयार हैं।

## चरण 2: वर्कबुक लोड करें – एक्सेल टेबल को TXT में एक्सपोर्ट करने की तैयारी

पहली वास्तविक कोड लाइन हमेशा वही होती है: वह वर्कबुक खोलें जिसमें वह टेबल हो जिसे आप एक्सपोर्ट करना चाहते हैं।

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

यहाँ हम पहली वर्कशीट (`get(0)`) ले रहे हैं। यदि आपका डेटा किसी अन्य शीट पर है, तो केवल इंडेक्स बदलें या `get("SheetName")` का उपयोग करें। यह भाग **export excel table to txt** के लिए आवश्यक है क्योंकि एक्सपोर्टर वर्कशीट स्तर पर काम करता है।

## चरण 3: कस्टम सेल सेपरेटर सेट करें – एक्सपोर्ट का मूल

अब आता है मुख्य भाग: `ExportTableOptions` को कॉन्फ़िगर करना। यह ऑब्जेक्ट आपको यह तय करने देता है कि अंतिम टेक्स्ट फ़ाइल में प्रत्येक सेल कैसे दिखेगा।

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

हम **set custom cell separator** क्यों करते हैं? क्योंकि डिफ़ॉल्ट सेपरेटर टैब होता है, जो उन डेटा के साथ टकरा सकता है जिनमें पहले से टैब मौजूद हैं। पाइप (`|`) या सेमीकोलन चुनकर आप सुनिश्चित करते हैं कि प्रत्येक कॉलम अलग रहे जब डाउनस्ट्रीम पार्सर फ़ाइल पढ़े।

### एक्सेल फ़ॉर्मूले को टेक्स्ट में एक्सपोर्ट करें

`setFormulaValueInCell(true)` लाइन Aspose.Cells को बताती है कि **export excel formulas to text** को फ़ॉर्मूले के *परिणाम* के रूप में लिखे, न कि फ़ॉर्मूला स्ट्रिंग को। यदि आप इसे छोड़ देते हैं, तो `=SUM(A1:A5)` वाला सेल TXT में `=SUM(A1:A5)` ही दिखेगा, जो आमतौर पर आप नहीं चाहते।

## चरण 4: एक्सपोर्ट विकल्पों को TXT सेव ऑप्शन्स से जोड़ें

अब हम उन टेबल विकल्पों को संपूर्ण TXT एक्सपोर्ट कॉन्फ़िगरेशन से बाइंड करते हैं।

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` वह मुख्य ऑब्जेक्ट है जो नियंत्रित करता है कि पूरी वर्कशीट कैसे लिखी जाए। `exportTableOptions` को इसमें प्लग करके, आप सुनिश्चित करते हैं कि शीट की हर टेबल **set custom cell separator** नियम का पालन करे।

## चरण 5: वर्कशीट को TXT फ़ाइल के रूप में सेव करें – एक्सपोर्ट समाप्त करना

अंत में, हम फ़ाइल को डिस्क पर लिखते हैं।

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

इस प्रोग्राम को चलाने से `TableExported.txt` बनता है। मूल एक्सेल टेबल की प्रत्येक पंक्ति अब पाइप‑सेपरेटेड वैल्यू की एक लाइन के रूप में दिखेगी, जैसे:

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

ध्यान दें कि **Total** कॉलम में फ़ॉर्मूला लिखे जाने से पहले मूल्यांकित हो गया—`setFormulaValueInCell(true)` के धन्यवाद से। यही है **export excel data as plain text** का सार, जबकि गणना किए गए परिणामों को संरक्षित रखा जाता है।

## चरण 6: आउटपुट की जाँच करें – क्या यह सही दिख रहा है?

किसी भी टेक्स्ट एडिटर में उत्पन्न `TableExported.txt` खोलें। आपको यह दिखना चाहिए:

- प्रत्येक एक्सेल पंक्ति के लिए एक लाइन।
- `setCellValueSeparator` से सेट किए गए पाइप कैरेक्टर द्वारा कॉलम अलग किए गए।
- कोई अनावश्यक कॉमा या टैब नहीं, जब तक वे मूल सेल वैल्यू का हिस्सा न हों।
- फ़ॉर्मूला के परिणाम, न कि स्वयं फ़ॉर्मूले।

यदि आप कोई अनपेक्षित कैरेक्टर देखते हैं, तो चुने हुए सेपरेटर को दोबारा जांचें। कुछ कैरेक्टर (जैसे पाइप) अधिकांश CSV‑स्टाइल पार्सर्स के लिए सुरक्षित होते हैं, लेकिन यदि आपके डेटा में पहले से पाइप हैं, तो `~` या टैब (`\t`) जैसे अलग डिलिमिटर पर विचार करें।

## टिप्स, किनारे के केस, और सर्वोत्तम प्रथाएँ – एक्सेल डेटा को प्लेन टेक्स्ट में एक्सपोर्ट करें

| स्थिति | क्या करें |
|-----------|------------|
| **डेटा में पहले से आपका चुना हुआ सेपरेटर मौजूद है** | कम सामान्य कैरेक्टर (`^`, `~`, या यूनिकोड नॉन‑प्रिंटिंग कैरेक्टर्स) पर स्विच करें। |
| **आपको UTF‑8 एन्कोडिंग चाहिए** |  |

## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Aspose.Cells का उपयोग करके कस्टम सेपरेटर के साथ एक्सेल को टेक्स्ट फ़ाइल में सेव करें](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Aspose Cells Net के साथ एक्सेल टेक्स्ट कस्टम सेपरेटर सेव करें](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Aspose Cells Net के साथ एक्सेल टेक्स्ट कस्टम सेपरेटर सेव करें](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}