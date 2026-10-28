---
category: general
date: 2026-07-03
description: जावा का उपयोग करके एक्सेल फ़ाइलों को स्टाइल कैसे करें। कॉलम की डेट को
  फ़ॉर्मेट करना, नंबर फ़ॉर्मेट लागू करना, DataTable को XLSX में एक्सपोर्ट करना और
  Aspose Cells के साथ DataTable को एक्सेल में इम्पोर्ट करना सीखें।
draft: false
keywords:
- how to style excel
- format column date excel
- apply number format excel
- export datatable to xlsx
- import datatable into excel
language: hi
og_description: जावा में एक्सेल फ़ाइलों को कैसे स्टाइल करें। यह ट्यूटोरियल दिखाता
  है कि कॉलम की तिथि को एक्सेल में कैसे फ़ॉर्मेट करें, एक्सेल में नंबर फ़ॉर्मेट कैसे
  लागू करें, डेटा टेबल को XLSX में एक्सपोर्ट करें और डेटा टेबल को एक्सेल में इम्पोर्ट
  करें।
og_title: Excel को कैसे स्टाइल करें – कस्टम कॉलम फ़ॉर्मेटिंग के लिए जावा गाइड
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: How to style Excel files using Java. Learn to format column date Excel,
    apply number format Excel, export DataTable to XLSX and import DataTable into
    Excel with Aspose Cells.
  headline: How to Style Excel – Import DataTable with Custom Formatting in Java
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
title: Excel को स्टाइल कैसे करें – Java में कस्टम फ़ॉर्मेटिंग के साथ DataTable आयात
  करें
url: /hi/java/excel-import-export/how-to-style-excel-import-datatable-with-custom-formatting-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को स्टाइल कैसे करें – कस्टम फ़ॉर्मेटिंग के साथ DataTable इम्पोर्ट करें Java में

क्या आपने कभी **Excel शीट्स को प्रोग्रामेटिकली स्टाइल** करने के बारे में सोचा है बिना फ़ाइल को मैन्युअली खोले? आप अकेले नहीं हैं। कई डेवलपर्स को ऐसे रिपोर्ट जनरेट करने होते हैं जहाँ पहली कॉलम बोल्ड हो, दूसरी कॉलम में डेट्स दिखें, और बाकी एक साफ़ लेआउट का पालन करें। इस गाइड में हम एक पूर्ण, रन करने योग्य उदाहरण के माध्यम से **DataTable को Excel में इम्पोर्ट** करेंगे, बोल्ड हेडर लगाएंगे, डेट कॉलम को फ़ॉर्मेट करेंगे, और अंत में **DataTable को XLSX में एक्सपोर्ट** करेंगे।

हम Aspose.Cells for Java का उपयोग करेंगे, लेकिन ये कॉन्सेप्ट किसी भी लाइब्रेरी पर लागू होते हैं जो आपको स्टाइल्स के साथ काम करने देती है। अंत तक आप **apply number format Excel** सेल्स, **format column date Excel**, और एक पॉलिश्ड वर्कबुक को अपने यूज़र्स तक पहुँचाने का पुन: उपयोग योग्य पैटर्न प्राप्त कर लेंगे।

## Prerequisites

- Java 17 (या कोई भी हालिया JDK)  
- Aspose.Cells for Java 23.9 या नया (फ्री ट्रायल ठीक काम करता है)  
- एक `DataTable`‑जैसी स्ट्रक्चर (उदाहरण में एक सरल मॉक इस्तेमाल किया गया है)  
- आपका पसंदीदा IDE (IntelliJ IDEA, Eclipse, VS Code…)

कोई अतिरिक्त Maven प्लगइन्स आवश्यक नहीं हैं; बस Aspose.Cells JAR को अपने क्लासपाथ में जोड़ दें।

---

## Step 1: Obtain the Source DataTable – “Export DataTable to XLSX” Preparation

**डेटा टेबल को Excel में इम्पोर्ट** करने से पहले हमें एक `DataTable` ऑब्जेक्ट चाहिए जो उस डेटा का प्रतिनिधित्व करे जिसे आप एक्सपोर्ट करना चाहते हैं। वास्तविक प्रोजेक्ट्स में आप इसे डेटाबेस, CSV फ़ाइल, या API से प्राप्त कर सकते हैं। इस ट्यूटोरियल के लिए हम एक छोटी टेबल को मॉक करेंगे:

```java
import java.util.*;
import com.aspose.cells.*;

public class DemoData {
    public static DataTable getDataTable() {
        // Create a simple table with three columns: ID, Date, Amount
        DataTable dt = new DataTable();
        dt.getColumns().add("ID", DataType.INTEGER);
        dt.getColumns().add("OrderDate", DataType.DATE_TIME);
        dt.getColumns().add("Total", DataType.DOUBLE);

        // Add a few rows
        dt.getRows().add(new Object[]{1, new Date(), 125.50});
        dt.getRows().add(new Object[]{2, new Date(System.currentTimeMillis() - 86400000L), 99.99});
        dt.getRows().add(new Object[]{3, new Date(System.currentTimeMillis() - 2*86400000L), 250.00});
        return dt;
    }
}
```

> **Why this matters:** डेटा को पहले से सही ढंग से प्राप्त करना मतलब बाकी स्टाइलिंग लॉजिक केवल प्रेजेंटेशन पर फोकस कर सके, डेटा रैंगलिंग नहीं।

---

## Step 2: Create an Array to Hold Style Definitions for Each Column

Aspose.Cells आपको `DataTable` इम्पोर्ट करते समय **Style[]** एरे पास करने की सुविधा देता है। एरे का प्रत्येक एंट्री एक कॉलम से मेल खाता है और इम्पोर्ट के बाद उस कॉलम की दिखावट तय करता है। चलिए कॉलम की संख्या के आधार पर एरे अलोकेट करते हैं:

```java
DataTable dataTable = DemoData.getDataTable();
Style[] columnStyles = new Style[dataTable.getColumns().size()];
```

> **Tip:** यदि आपके पास कई कॉलम हैं, तो एरे को लूप में बनाकर एक ही `Style` ऑब्जेक्ट को पुन: उपयोग करने पर विचार करें जहाँ फ़ॉर्मेटिंग समान हो। इससे मेमोरी ओवरहेड कम होता है।

---

## Step 3: Define the Styles – Bold Header & Date Formatting

अब हम क्लासिक **format column date excel** सवाल का जवाब देते हैं और साथ ही **apply number format excel** को भी दिखाते हैं।

```java
// --- Style for the first column (header bold) ---
columnStyles[0] = new Style();
columnStyles[0].getFont().setBold(true);          // Makes header text bold

// --- Style for the second column (date formatting) ---
columnStyles[1] = new Style();
columnStyles[1].setNumber(StyleNumberFormat.DATE); // Uses the built‑in DATE format

// --- Optional: Style for the third column (currency) ---
columnStyles[2] = new Style();
columnStyles[2].setNumber(StyleNumberFormat.CURRENCY_USD);
```

**यहाँ क्या हो रहा है?**  
- `StyleNumberFormat.DATE` Excel को बताता है कि सेल का वैल्यू एक शॉर्ट डेट (जैसे *01/31/2024*) के रूप में ट्रीट किया जाए।  
- `StyleNumberFormat.CURRENCY_USD` स्वचालित रूप से `$` सिम्बल और दो दशमलव जोड़ता है।  
- पहली कॉलम पर फ़ॉन्ट को बोल्ड सेट करने से हेडर उभर कर दिखता है, जो **how to style excel** स्प्रेडशीट्स को पढ़ने योग्य बनाने की आम आवश्यकता है।

> **Edge case:** यदि आपका सोर्स डेटा पहले से फ़ॉर्मेटेड स्ट्रिंग्स रखता है, तो इम्पोर्ट से पहले उन्हें `java.util.Date` ऑब्जेक्ट में बदलना पड़ सकता है; अन्यथा Excel उन्हें प्लेन टेक्स्ट मान लेगा।

---

## Step 4: Create a New Workbook and Access Its First Worksheet

एक नया वर्कबुक हमें एक साफ़ कैनवास देता है। हम पहली वर्कशीट को पकड़ेंगे, जहाँ इम्पोर्ट होगा।

```java
Workbook workbook = new Workbook();               // New empty workbook
Worksheet worksheet = workbook.getWorksheets().get(0); // First sheet (index 0)
```

> **Why a new workbook?** शुरू से बनाना यह गारंटी देता है कि कोई भी लिफ़्ट‑ओवर स्टाइल या हिडन रो अंतिम आउटपुट को प्रभावित न करे—यह **how to style excel** फ़ाइलों को लगातार कई रन में बनाए रखने के लिए आवश्यक है।

---

## Step 5: Import the DataTable with the Column Styles

यह ऑपरेशन का दिल है: `DataTable` को शीट में फीड करना और हमने जो स्टाइल एरे बनाया था उसे लागू करना।

```java
// The third argument (true) tells Aspose.Cells to include column headers.
worksheet.getCells().importDataTable(dataTable, true, columnStyles);
```

**Explanation:**  
- `importDataTable` हेडर रो और डेटा रो दोनों को कॉपी करता है।  
- `columnStyles` एरे प्रत्येक कॉलम के साथ मेल खाता है, इसलिए पहली कॉलम का हेडर बोल्ड हो जाता है, दूसरी कॉलम डेट्स दिखाता है, और तीसरी कॉलम करंसी के रूप में दिखती है।  
- यह एक लाइन कई मैन्युअल सेल‑बाय‑सेल फ़ॉर्मेटिंग स्टेप्स को रिप्लेस करती है, जिससे **apply number format excel** प्रोग्रामेटिकली करने का साफ़ तरीका दिखता है।

---

## Step 6: Save the Styled Workbook – Completing the “Export DataTable to XLSX”

अंत में हम वर्कबुक को डिस्क पर सेव करते हैं। अपने मशीन पर लिखने योग्य फ़ोल्डर का पाथ एडजस्ट करें।

```java
String outputPath = "C:/temp/styledImport.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Excel में फ़ाइल खोलें और आपको दिखना चाहिए:

- कॉलम **ID** हेडर बोल्ड में।  
- **OrderDate** कॉलम डेट्स के रूप में फ़ॉर्मेटेड (जैसे *04/27/2024*)।  
- **Total** कॉलम डॉलर सिम्बल और दो दशमलव के साथ दिखता है।

> **Pro tip:** यदि आपको पुराने Excel संस्करणों को सपोर्ट करना है, तो डिफ़ॉल्ट XLSX के बजाय `workbook.save(outputPath, SaveFormat.XLS)` कॉल करें।

---

## Step 7: Verify the Result & Optional Tweaks

ऑटोमेटेड रिपोर्ट्स बनाते समय जेनरेटेड फ़ाइल को दोबारा चेक करना एक अच्छी प्रैक्टिस है।

```java
// Quick verification: read the first cell's style
Cell firstHeader = worksheet.getCells().get(0, 0);
boolean isBold = firstHeader.getStyle().getFont().isBold();
System.out.println("Header bold? " + isBold);
```

यदि `isBold` `true` प्रिंट करता है, तो आपका **how to style excel** रूटीन सही काम कर रहा है। अब आप कर सकते हैं:

- कंडीशनल फ़ॉर्मेटिंग जोड़ें (जैसे, टोटल्स > $200 को हाईलाइट करें)।  
- आसान स्क्रॉलिंग के लिए टॉप रो को फ्रीज़ करें।  
- इम्पोर्टेड डेटा को रेफ़र करने वाला चार्ट इन्सर्ट करें।

इन सभी एक्सटेंशन का पैटर्न समान है: `Style` डिफाइन करें, उसे अप्लाई करें, और सेव करें।

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **क्या मैं एक से अधिक कॉलम को एक ही तरीके से स्टाइल कर सकता हूँ?** | हाँ—उन सभी कॉलम के लिए एक ही `Style` इंस्टेंस को री‑यूज़ करें जो एक ही फ़ॉर्मेटिंग शेयर करते हैं। |
| **अगर मेरे DataTable में कॉलम की संख्या स्टाइल एरे से अधिक हो तो क्या होगा?** | जिन कॉलमों के लिए `columnStyles` में एंट्री नहीं होगी, वे डिफ़ॉल्ट स्टाइल उपयोग करेंगे। |
| **डेट फ़ॉर्मेट को “dd‑MMM‑yyyy” कैसे बदलूँ?** | बिल्ट‑इन `DATE` के बजाय `columnStyles[1].setCustom("#dd-MMM-yyyy#");` इस्तेमाल करें। |
| **इम्पोर्ट के बाद कॉलम्स को ऑटो‑साइज़ करने का तरीका?** | `importDataTable` के बाद `worksheet.autoFitColumns();` कॉल करें। |
| **क्या यह Linux/macOS पर काम करेगा?** | बिल्कुल—Aspose.Cells प्लेटफ़ॉर्म‑अज्ञेय है जब तक आपके पास संगत JDK हो। |

---

## Conclusion

अब आपके पास **how to style Excel** वर्कबुक्स को **importing datatable into excel**, **format column date excel**, और **apply number format excel** Java के साथ बनाने का एक ठोस, एंड‑टू‑एंड उदाहरण है। कोड **export datatable to xlsx** से लेकर Excel में फ़ाइल खोलने तक का पूरा फ्लो दिखाता है, साथ ही प्रत्येक स्टेप के *what* और *why* को भी समझाता है।

इसे आज़माएँ: स्टाइल एरे को एडजस्ट करें, और अधिक कॉलम जोड़ें, या वास्तविक डेटाबेस क्वेरी को प्लग इन करें। वही पैटर्न आपको बटन क्लिक पर प्रोफ़ेशनल‑लुकिंग रिपोर्ट्स जनरेट करने देगा, बिना मैन्युअल फ़ॉर्मेटिंग की ज़रूरत के।

---

![Styled Excel worksheet generated by the tutorial code](https://example.com/images/styled-worksheet.png "Screenshot of styled Excel worksheet created using Java and Aspose.Cells")

*Image alt text: “Styled Excel worksheet created using Java and Aspose.Cells, showing bold header and formatted date column.”*


## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप एक्सप्लैनेशन शामिल है, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Create & Format Excel Cells Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [How to Style Excel Cells and Add Hyperlinks Using Aspose.Cells for Java](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}