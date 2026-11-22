---
category: general
date: 2026-11-22
description: जानिए कैसे Excel को टेक्स्ट के रूप में निर्यात करें और टैब‑डिलिमिटेड
  फ़ाइल बनाएं। यह गाइड सभी फ़ील्ड को कोट करने की सेटिंग और स्प्रेडशीट टेक्स्ट को कुशलतापूर्वक
  सहेजने को दिखाता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: hi
lastmod: 2026-11-22
og_description: Excel को टेक्स्ट के रूप में निर्यात करें और टैब‑डिलिमिटेड फ़ाइल बनाएं।
  सभी फ़ील्ड को कोट करने और Java के साथ स्प्रेडशीट टेक्स्ट को सहेजने के लिए इस चरण‑दर‑चरण
  ट्यूटोरियल का पालन करें।
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: एक्सेल को टेक्स्ट के रूप में निर्यात करें – टैब‑डिलिमिटेड फ़ाइल गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Excel को टैब‑डिलिमिटेड टेक्स्ट के रूप में कैसे निर्यात करें
url: /hi/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को टेक्स्ट के रूप में निर्यात कैसे करें टैब‑डिलिमिटेड आउटपुट के साथ

यदि आपको **Excel को टेक्स्ट के रूप में निर्यात** करना है, तो यह ट्यूटोरियल आपको एक वर्कबुक से टैब‑डिलिमिटेड फ़ाइल बनाने की पूरी प्रक्रिया से परिचित कराता है। चाहे आप डेटा‑माइग्रेशन पाइपलाइन बना रहे हों या डाउनस्ट्रीम प्रोसेसिंग के लिए तेज़ CSV‑स्टाइल डम्प की आवश्यकता हो, नीचे दिए गए चरण आपको **स्प्रेडशीट टेक्स्ट को सहेजने** की अनुमति देते हैं, जिसमें डिलिमिटर और कोटिंग पर पूर्ण नियंत्रण होता है।

स्प्रेडशीट डेटा को प्लेन टेक्स्ट के रूप में निर्यात करना अक्सर मूल `.xlsx` फ़ॉर्मेट को रखने की तुलना में अधिक पोर्टेबल होता है। इस गाइड में आप यह भी सीखेंगे कि **सभी फ़ील्ड को कोट** कैसे किया जाए, जो यह सुनिश्चित करता है कि टैब, कॉमा या लाइन ब्रेक वाले मान सुरक्षित रूप से एन्कैप्सुलेट हो जाएँ।

## आपको क्या चाहिए

* Java 17 या उसके बाद का संस्करण स्थापित हो।
* Aspose.Cells for Java लाइब्रेरी (कोड इस लाइब्रेरी से `ExportOptions` और `ExportTableOptions` का उपयोग करता है)। आप इसे Maven के माध्यम से जोड़ सकते हैं:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* एक IDE या साधारण टेक्स्ट एडिटर ताकि आप Java प्रोग्राम को कंपाइल और रन कर सकें।

## Excel को टेक्स्ट के रूप में निर्यात – चरण‑दर‑चरण

निम्नलिखित अनुभाग कार्य को तीन तार्किक चरणों में विभाजित करते हैं। प्रत्येक चरण यह समझाता है कि **क्यों** यह महत्वपूर्ण है, न कि केवल **क्या** टाइप करना है।

### चरण 1: वर्कबुक और नमूना डेटा तैयार करें

एक वर्कबुक बनाना आपको निर्यात करने के लिए कुछ देता है। वास्तविक प्रोजेक्ट में आप `new Workbook("input.xlsx")` से मौजूदा फ़ाइल लोड करेंगे; यहाँ हम एक छोटा शीट उत्पन्न करते हैं ताकि उदाहरण तुरंत चल सके।

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*इस चरण का कारण?*  
एक वर्कबुक किसी भी निर्यात ऑपरेशन का स्रोत ऑब्जेक्ट है। कुछ पंक्तियों को जोड़कर आप यह सत्यापित कर सकते हैं कि **सभी फ़ील्ड को कोट** विकल्प वास्तव में कॉमा और अन्य विशेष अक्षरों की रक्षा करता है।

### चरण 2: निर्यात विकल्प कॉन्फ़िगर करें – डिलिमिटर, कोटिंग, और आउटपुट मोड

**स्प्रेडशीट टैब‑डिलिमिटेड निर्यात** का मूल `ExportTableOptions` में निहित है। आप डिलिमिटर को टैब (`'\t'`) पर सेट करते हैं और `setQuoteAllFields(true)` को सक्षम करते हैं ताकि हर सेल को डबल कोट्स में लपेटा जाए। यह तब अस्पष्टता को समाप्त करता है जब किसी सेल में स्वयं टैब या न्यूलाइन हो।

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*इस चरण का कारण?*  
- **डिलिमिटर** निर्धारित करता है कि कॉलम कैसे अलग होते हैं। एक टैब (`\t`) एक **टैब‑डिलिमिटेड फ़ाइल** बनाता है जिसे कई डेटा‑प्रोसेसिंग टूल स्वीकार करते हैं।  
- **सभी फ़ील्ड को कोट** यह सुनिश्चित करता है कि यदि किसी सेल में डिलिमिटर हो भी, तो परिणामी टेक्स्ट पार्स करने योग्य बना रहे।  
- `ExportAsString` सेट करने से Aspose.Cells एक स्ट्रिंग उत्पन्न करता है न कि बाइनरी वर्कबुक, जो कि **स्प्रेडशीट टेक्स्ट को सहेजने** के लिए बिल्कुल आवश्यक है।

### चरण 3: वर्कबुक को टैब‑डिलिमिटेड टेक्स्ट फ़ाइल के रूप में सहेजें

अब आप वास्तव में **Excel को टेक्स्ट के रूप में निर्यात** करते हैं। `save` मेथड लक्ष्य पथ और आपके द्वारा कॉन्फ़िगर किए गए `ExportOptions` को लेता है।

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

जब प्रोग्राम समाप्त हो जाएगा, आपको `output/table.txt` मिलेगा जिसमें यह होगा:

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*इस चरण का कारण?*  
`save` कॉल **टैब‑डिलिमिटेड फ़ाइल** को डिस्क पर लिखता है, प्रभावी रूप से **स्प्रेडशीट टेक्स्ट को सहेजता** है एक ऐसे फ़ॉर्मेट में जिसे Excel, Notepad, या कोई भी डेटा‑इम्पोर्ट टूल जो टैब समझता है, खोल सकता है।

## Excel को टेक्स्ट के रूप में निर्यात करते समय सभी फ़ील्ड को कोट कैसे करें

यदि आप `setQuoteAllFields(true)` को छोड़ देते हैं, तो टैब, कॉमा या लाइन ब्रेक वाले सेल आउटपुट फ़ाइल की संरचना को तोड़ देंगे। उदाहरण के लिए, पंक्ति `Bob, Jr.` दो कॉलम में विभाजित हो जाएगी, जिससे डेटासेट खराब हो जाएगा। हमेशा कोटिंग सक्षम करें जब:

* आपका स्रोत डेटा कॉमा, टैब या न्यूलाइन रख सकता है।  
* डाउनस्ट्रीम पार्सर कोटेड CSV/TSV फ़ाइलों की अपेक्षा करते हैं।  
* आपको सेल सामग्री की परवाह किए बिना एक निर्धारित निर्यात चाहिए।

## Aspose.Cells के बिना टैब‑डिलिमिटेड फ़ाइल बनाना (वैकल्पिक)

यदि आप थर्ड‑पार्टी लाइब्रेरीज़ के बिना शुद्ध‑Java समाधान पसंद करते हैं, तो आप पंक्तियों पर इटररेट करके उन्हें मैन्युअली लिख सकते हैं:

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

यह स्निपेट वही **स्प्रेडशीट टैब‑डिलिमिटेड निर्यात** लॉजिक दर्शाता है: एक टैब डिलिमिटर, हर फ़ील्ड को कोट करना, और परिणाम को प्लेन टेक्स्ट के रूप में लिखना। हालांकि, Aspose.Cells का उपयोग बड़े वर्कबुक को संभालना आसान बनाता है, फ़ॉर्मेटिंग को संरक्षित रखता है, और बायलरप्लेट को कम करता है।

## सामान्य समस्याएँ और प्रो टिप्स

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| **आउटपुट में टैब गायब** | डिलिमिटर को डिफ़ॉल्ट कॉमा पर छोड़ दिया गया। | `setDelimiter('\t')` को स्पष्ट रूप से कॉल करें। |
| **बिना कोट किए कॉमा कॉलम तोड़ते हैं** | `quoteAllFields` सक्षम नहीं है। | `setQuoteAllFields(true)` का उपयोग करें या मैन्युअली कोट करें। |
| **फ़ाइल नहीं बनी** | आउटपुट डायरेक्टरी मौजूद नहीं है। | `output/` फ़ोल्डर मौजूद है यह सुनिश्चित करें या `Files.createDirectories` का उपयोग करें। |
| **एन्कोडिंग समस्याएँ** | डिफ़ॉल्ट प्लेटफ़ॉर्म एन्कोडिंग गैर‑ASCII अक्षरों को भ्रष्ट कर सकती है। | यदि आवश्यक हो तो `ExportOptions.setEncoding(Encoding.getUTF8())` पास करें। |

## परिणाम का परीक्षण

प्रोग्राम चलाने के बाद:

1. `output/table.txt` को एक प्लेन‑टेक्स्ट एडिटर में खोलें। आपको प्रत्येक मान डबल कोट्स में लिपटा हुआ और कॉलम एक एकल टैब कैरेक्टर से अलग दिखना चाहिए।  
2. फ़ाइल को Excel में इम्पोर्ट करें (`Data → From Text/CSV`)। डिलिमिटर के रूप में **Tab** चुनें; Excel प्रत्येक कोटेड मान को उसके अपने सेल में सही ढंग से रखेगा।  
3. यह सत्यापित करें कि विशेष अक्षर (कॉमा, लाइन ब्रेक

## अब आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों की खोज करने में मदद करती हैं।

- [Excel निर्यात कैसे करें – टैब‑डिलिमिटेड टेक्स्ट गाइड](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Aspose.Cells का उपयोग करके कस्टम सेपरेटर के साथ Excel को टेक्स्ट फ़ाइल के रूप में सहेजें](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Aspose.Cells के साथ Excel को टेक्स्ट के रूप में सहेजें – चरण‑दर‑चरण गाइड](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}