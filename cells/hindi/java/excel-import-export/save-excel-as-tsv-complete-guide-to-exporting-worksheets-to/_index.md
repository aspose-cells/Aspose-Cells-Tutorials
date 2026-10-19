---
category: general
date: 2026-06-27
description: जावा का उपयोग करके एक्सेल को तेज़ी से TSV के रूप में सहेजें। सीखें कैसे
  वर्कशीट को टेक्स्ट में निर्यात करें, शीट को साधारण टेक्स्ट में निर्यात करें, और
  Aspose.Cells के साथ एक्सेल डेटा स्ट्रिंग निर्यात करें।
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: hi
og_description: जावा का उपयोग करके एक्सेल को TSV के रूप में सहेजें। यह ट्यूटोरियल
  दिखाता है कि वर्कशीट को टेक्स्ट में कैसे निर्यात करें, शीट को साधारण टेक्स्ट में
  निर्यात करें, और एक्सेल डेटा स्ट्रिंग को कुशलतापूर्वक निर्यात करें।
og_title: Excel को TSV के रूप में सहेजें – चरण‑दर‑चरण निर्यात गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: एक्सेल को TSV के रूप में सहेजें – वर्कशीट्स को टेक्स्ट में निर्यात करने की
  पूरी गाइड
url: /hi/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को TSV के रूप में सहेजें – वर्कशीट्स को टेक्स्ट में एक्सपोर्ट करने का पूर्ण गाइड

क्या आपको कभी **save Excel as TSV** करने की ज़रूरत पड़ी है लेकिन आपको नहीं पता था कि कौन सा API कॉल उपयोग करना है? आप अकेले नहीं हैं। कई डेवलपर्स को स्प्रेडशीट को टैब‑डिलिमिटेड फ़ाइल में बदलने के दौरान दिक्कत आती है। अच्छी खबर यह है कि कुछ ही लाइनों के Java और Aspose.Cells कोड से आप वर्कशीट को टेक्स्ट में एक्सपोर्ट कर सकते हैं, शीट को प्लेन‑टेक्स्ट में एक्सपोर्ट कर सकते हैं, और यहाँ तक कि **export Excel data string** को भी बिना किसी परेशानी के प्राप्त कर सकते हैं।

इस ट्यूटोरियल में हम पूरे वर्कफ़्लो को चरण‑दर‑चरण देखेंगे—वर्कबुक को लोड करने से लेकर एक्सपोर्ट विकल्पों को कॉन्फ़िगर करने और अंत में डिस्क पर TSV फ़ाइल लिखने तक। अंत तक आप किसी भी Java प्रोजेक्ट में **save Excel as TSV** कर पाएँगे, चाहे आप एक ही शीट को हैंडल कर रहे हों या दर्जनों फ़ाइलों को बैच में प्रोसेस कर रहे हों।

## इस गाइड में क्या-क्या शामिल है

* डिस्क से Excel वर्कबुक लोड करना  
* सही वर्कशीट चुनना (या कई शीट्स पर लूप करना)  
* `ExportTableOptions` को कॉन्फ़िगर करके प्लेन‑टेक्स्ट आउटपुट बनाना  
* डेटा को टैब‑सेपरेटेड वैल्यूज़ (TSV) फ़ाइल के रूप में लिखना  
* बड़े रेंज, विभिन्न डिलिमिटर, और यूनिकोड कैरेक्टर्स को हैंडल करने के टिप्स  

कोई बाहरी टूल आवश्यक नहीं—सिर्फ Aspose.Cells for Java और Java 8+ रनटाइम।

---

## चरण 1: प्रोजेक्ट सेट अप करें और वर्कबुक लोड करें

कोड में जाने से पहले सुनिश्चित करें कि आपने Aspose.Cells JAR को अपने प्रोजेक्ट की क्लासपाथ में जोड़ दिया है। यदि आप Maven उपयोग कर रहे हैं, तो डिपेंडेंसी इस प्रकार दिखेगी:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

अब हम वर्कबुक लोड कर सकते हैं:

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **यह क्यों महत्वपूर्ण है:** फ़ाइल को लोड करना किसी भी **export Excel data string** वर्कफ़्लो का पहला कदम है। अगर फ़ाइल नहीं खुल पाती, तो बाकी सब काम नहीं करेगा।

### प्रो टिप
यदि आप पासवर्ड‑प्रोटेक्टेड फ़ाइलों से निपट रहे हैं, तो इस तरह कॉल करें: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`।

---

## चरण 2: वह वर्कशीट चुनें जिसे आप एक्सपोर्ट करना चाहते हैं

आप पहली शीट, नाम से शीट, या सभी शीट्स पर इटरेट कर सकते हैं। यहाँ सबसे सरल केस है—पहली वर्कशीट को एक्सपोर्ट करना:

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

यदि आपको हर शीट के लिए **export worksheet to text** करना है, तो ऊपर के कोड को `for` लूप में रखें:

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## चरण 3: एक्सपोर्ट विकल्प बनाएं और कॉन्फ़िगर करें

**export sheet plain text** का दिल `ExportTableOptions` में है। कुछ प्रॉपर्टीज़ को टॉगल करके हम रेंज को टैब डिलिमिटर वाले प्लेन‑टेक्स्ट स्ट्रिंग में बदल देते हैं:

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **`setExportAsString(true)` क्यों उपयोग करें?**  
> यह Aspose.Cells को बताता है कि आउटपुट को रॉ टेक्स्ट के रूप में ट्रीट किया जाए, जो बिल्कुल वही है जो आपको **save Excel as TSV** करने के लिए चाहिए। वैकल्पिक रूप से CSV या HTML एक्सपोर्ट हो सकता है, जो टैब सेपरेशन नहीं देता।

### एज केस: कस्टम डिलिमिटर
यदि आपका डाउनस्ट्रीम सिस्टम टैब की बजाय पाइप (`|`) चाहता है, तो बस डिलिमिटर बदल दें:

```java
exportOptions.setDelimiter('|');
```

---

## चरण 4: इच्छित रेंज को टेक्स्ट फ़ाइल में एक्सपोर्ट करें

अब हम वास्तव में TSV फ़ाइल लिखते हैं। `exportTable` मेथड तीन आर्ग्यूमेंट लेता है: सेल रेंज, आउटपुट पाथ, और हमने अभी कॉन्फ़िगर किया हुआ `ExportTableOptions`।

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

यदि आप *पूरी* उपयोग की गई रेंज को एक्सपोर्ट करना चाहते हैं, तो `"A1:D20"` को `ws.getCells().getMaxDisplayRange()` से बदल दें:

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### प्रो टिप
एक्सपोर्ट करने के बाद आप स्ट्रिंग को सीधे भी कैप्चर कर सकते हैं:

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

इससे आपको फ़ाइल सिस्टम को छुए बिना रॉ **export Excel data string** मिल जाता है।

---

## चरण 5: बड़े फ़ाइलों को हैंडल करना और परफ़ॉर्मेंस टिप्स

जब आप सैकड़ों हज़ार रो वाली बड़ी स्प्रेडशीट्स के साथ काम कर रहे हों, तो इन ऑप्टिमाइज़ेशन पर विचार करें:

| समस्या | समाधान |
|--------|--------|
| मेमोरी प्रेशर | `WorkbookFactory.create(InputStream)` का उपयोग करके फ़ाइल को स्ट्रीम करें, पूरी तरह लोड करने के बजाय। |
| धीमा I/O | `BufferedWriter` का उपयोग करें या NIO `Files.newBufferedWriter` अपनाएँ। |
| यूनिकोड कैरेक्टर्स | आउटपुट फ़ाइल को UTF‑8 में लिखें: `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`। |

नीचे एक स्निपेट है जो स्ट्रीमिंग और UTF‑8 एन्कोडिंग को मिलाता है:

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## सामान्य गलतियाँ और उन्हें कैसे टालें

1. **`setExportAsString(true)` सेट करना भूल गए।**  
   इस फ़्लैग के बिना Aspose एक बाइनरी Excel फ़ाइल जेनरेट करेगा, जिससे आपका **export worksheet to text** लक्ष्य टूट जाएगा।

2. **गलत डिलिमिटर उपयोग किया।**  
   कॉमा की बजाय टैब उपयोग न करने पर आपको CSV मिलेगा, TSV नहीं। `setDelimiter('\t')` को दोबारा चेक करें।

3. **रेंज सिंटैक्स गलत है।**  
   `"A1:D20"` ठीक है, लेकिन `"A1:D20:"` (अतिरिक्त कोलन) `IllegalArgumentException` फेंकेगा।

4. **फ़ाइल परमिशन समस्या।**  
   सुनिश्चित करें कि लक्ष्य डायरेक्टरी लिखने योग्य है। Linux पर अक्सर `chmod 755` मदद करता है।

---

## सब कुछ एक साथ – पूर्ण कार्यशील उदाहरण

यहाँ पूरा, तैयार‑चलाने‑योग्य प्रोग्राम है जो **save Excel as TSV** को शुरू से अंत तक दर्शाता है:

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

इस प्रोग्राम को चलाने पर एक टैब‑सेपरेटेड फ़ाइल (`out.tsv`) बनती है जिसे कोई भी डाउनस्ट्रीम सिस्टम—डेटाबेस लोडर, Unix `awk` स्क्रिप्ट, या साधा स्प्रेडशीट व्यूअर—उपयोग कर सकता है।

---

## निष्कर्ष

हमने Java और Aspose.Cells का उपयोग करके **save Excel as TSV** करने के सभी आवश्यक कदम कवर किए। वर्कबुक लोड करने से लेकर सही शीट चुनने, `ExportTableOptions` कॉन्फ़िगर करने और अंत में फ़ाइल लिखने तक, अब आपके पास **export worksheet to text**, **export sheet plain text**, और **export Excel data string** परिदृश्यों के लिए एक ठोस, प्रोडक्शन‑रेडी पैटर्न है।

अब आगे क्या? कई रेंजेज़ को एक्सपोर्ट करने की कोशिश करें, रन‑टाइम पर डिलिमिटर बदलें, या वेब‑आधारित डाउनलोड के लिए आउटपुट को सीधे HTTP रिस्पॉन्स में स्ट्रीम करें। वही सिद्धांत लागू होते हैं, और एक बार बुनियाद समझ में आ जाए तो Excel डेटा को प्लेन टेक्स्ट में हैंडल करना बहुत आसान हो जाता है।

कोई सवाल है या कोई अजीब एज केस मिला? नीचे कमेंट करें, और हैप्पी कोडिंग!

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स को मास्टर कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}