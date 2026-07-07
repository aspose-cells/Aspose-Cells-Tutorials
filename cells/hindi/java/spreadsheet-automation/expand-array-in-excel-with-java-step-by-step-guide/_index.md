---
category: general
date: 2026-07-03
description: जावा का उपयोग करके एक्सेल में एरे को कैसे विस्तारित करें, सीखें। यह ट्यूटोरियल
  एरे को पंक्तियों में विस्तारित करने, विस्तारण का उपयोग कैसे करें, और फ़ॉर्मूला को
  कुशलतापूर्वक कैसे डालें, को कवर करता है।
draft: false
keywords:
- expand array in excel
- expand array to rows
- how to use expand
- how to insert formula
- set formula in cell
language: hi
og_description: जावा का उपयोग करके एक्सेल में एरे का विस्तार करें। इस गाइड का पालन
  करके सीखें कि कैसे विस्तार करें, सेल में फ़ॉर्मूला सेट करें, और एरे को तुरंत पंक्तियों
  में विस्तारित करें।
og_title: जावा के साथ एक्सेल में एरे का विस्तार – पूर्ण प्रोग्रामिंग गाइड
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  headline: Expand Array in Excel with Java – Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to expand array in Excel using Java. This tutorial covers
    expand array to rows, how to use expand, and how to insert formula efficiently.
  name: Expand Array in Excel with Java – Step‑by‑Step Guide
  steps:
  - name: Why Use EXPAND?
    text: '`EXPAND` removes the tedious step of dragging the fill handle. It also
      works with dynamic arrays, meaning if your source array changes, the spilled
      range updates automatically. This is especially handy when generating reports
      programmatically.'
  - name: 1. Expanding a Horizontal Array to Multiple Columns
    text: 'If you need to **expand array to rows** *and* columns, just change the
      third argument:'
  - name: 2. Using a Named Range as the Source
    text: 'Instead of a literal `{1,2,3}`, you can reference a named range that may
      change at runtime:'
  - name: 3. Handling Non‑Numeric Data
    text: '`EXPAND` works with text as well. For example:'
  - name: 4. Avoiding Zero Fill with `IFERROR`
    text: 'If you’d rather see blanks instead of zeros, wrap the `EXPAND` in `IFERROR`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: जावा के साथ एक्सेल में एरे का विस्तार – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/java/spreadsheet-automation/expand-array-in-excel-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में एरे को Java के साथ विस्तारित करें – पूर्ण प्रोग्रामिंग गाइड

क्या आपने कभी सोचा है कि **Excel में एरे को विस्तारित** कैसे किया जाए बिना मैन्युअली सेल्स को ड्रैग किए? आप अकेले नहीं हैं। कई डेवलपर्स को तब समस्या आती है जब उन्हें प्रोग्रामेटिकली एक डायनामिक रेंज जेनरेट करनी होती है—विशेषकर जब नया Excel `EXPAND` फ़ंक्शन अभी नया‑नया है। इस गाइड में हम आपको बिल्कुल **EXPAND का उपयोग कैसे करें**, फ़ॉर्मूला को वर्कशीट में कैसे डालें, और परिणाम को इच्छित पंक्तियों में कैसे फैलाएँ, दिखाएंगे। अंत तक आप **एक ही Java लाइन में एरे को पंक्तियों में विस्तारित** करना सीख जाएंगे।

हम Aspose.Cells for Java लाइब्रेरी का उपयोग करके एक पूर्ण, चलने योग्य उदाहरण के माध्यम से चलेंगे। कोई अस्पष्ट संदर्भ नहीं, सिर्फ ठोस कोड जिसे आप कॉपी‑पेस्ट, कंपाइल और रन कर सकते हैं। रास्ते में हम प्रत्येक कदम के महत्व पर चर्चा करेंगे, गैर‑सतत एरे जैसे किनारे के मामलों को कवर करेंगे, और कुछ प्रो टिप्स देंगे जो आधिकारिक दस्तावेज़ों में नहीं मिलते। तैयार हैं? चलिए शुरू करते हैं।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास ये हों:

* Java 17 (या कोई भी नवीनतम JDK) स्थापित हो।
* Maven या Gradle, जिससे डिपेंडेंसीज़ मैनेज की जा सकें।
* एक वैध Aspose.Cells for Java लाइसेंस (टेस्टिंग के लिए फ्री ट्रायल चल जाएगा)।
* Excel फ़ॉर्मूले की बेसिक समझ—यदि आपने पहले `VLOOKUP` या `SUMIF` इस्तेमाल किया है, तो आप तैयार हैं।

यदि इनमें से कोई भी चीज़ अपरिचित लग रही हो, तो पहले उन्हें सेट‑अप कर लें; बाकी ट्यूटोरियल मानता है कि ये तैयार हैं।

## Step 1: Set Up Your Maven Project and Add Aspose.Cells

सभी चीज़ों को व्यवस्थित रखने के लिए, `ExpandArrayDemo` नाम का एक नया Maven प्रोजेक्ट बनाएँ। `pom.xml` में Aspose.Cells डिपेंडेंसी जोड़ें:

```xml
<!-- pom.xml -->
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ExpandArrayDemo</artifactId>
    <version>1.0.0</version>
    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.12</version> <!-- Use the latest version -->
        </dependency>
    </dependencies>
</project>
```

> **Pro tip:** यदि आप Gradle उपयोग कर रहे हैं, तो वही डिपेंडेंसी इस तरह दिखेगी `implementation 'com.aspose:aspose-cells:23.12'`।

Maven ने सभी पैकेज डाउनलोड कर लिए, अब आप Java कोड लिखने के लिए तैयार हैं जो **सेल में फ़ॉर्मूला सेट** करता है।

## Step 2: Create a Workbook and Access the First Worksheet

पहला कोड स्निपेट वह है जो आपने पहले देखा था, लेकिन हम इसमें कुछ सुरक्षा जाँच और टिप्पणियाँ जोड़ेंगे ताकि आप प्रत्येक लाइन के *क्यों* को समझ सकें।

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook – this gives us a blank Excel file.
        Workbook wb = new Workbook();

        // 2️⃣ Access the first worksheet (index 0). 
        //    If you ever need a different sheet, just change the index or name.
        Worksheet ws = wb.getWorksheets().get(0);

        // From here on we’ll work with ws (the active sheet).
```

*यह क्यों महत्वपूर्ण है:* `Workbook` का इंस्टैंसिएशन Aspose को सेल्स, फ़ॉर्मूले और स्टाइल्स को मैनेज करने के लिए आवश्यक आंतरिक संरचनाएँ प्रदान करता है। पहली वर्कशीट तक पहुंचना सबसे आम एंट्री पॉइंट है, खासकर जब आप अभी‑अभी प्रयोग कर रहे हों।

## Step 3: Insert the EXPAND Formula – “How to Insert Formula”

अब ट्यूटोरियल का मुख्य भाग: **फ़ॉर्मूला कैसे डालें** जो एरे को विस्तारित करता है। Excel `EXPAND` फ़ंक्शन तीन आर्ग्यूमेंट लेता है—स्रोत एरे, आवश्यक पंक्तियाँ, और आवश्यक कॉलम। हमारे मामले में हम `{1,2,3}` को **5 पंक्तियों** और **1 कॉलम** में विस्तारित करना चाहते हैं।

```java
        // 3️⃣ Put the EXPAND formula into cell A1.
        //    The formula string must be exactly as Excel would see it.
        String formula = "=EXPAND({1,2,3},5,1)";
        ws.getCells().putFormula("A1", formula);
```

ध्यान दें कि हमने `putValue` की बजाय `putFormula` इस्तेमाल किया है। यह Aspose को स्ट्रिंग को वास्तविक Excel फ़ॉर्मूला के रूप में ट्रीट करने को बताता है, न कि साधारण टेक्स्ट एंट्री के रूप में। `putFormula` मेथड स्वचालित रूप से स्ट्रिंग को पार्स करता है और फ़ॉर्मूला ट्री को आंतरिक रूप से स्टोर करता है।

### Why Use EXPAND?

`EXPAND` ड्रैग‑हैंडल को मैन्युअल रूप से खींचने की थकाऊ प्रक्रिया को हटा देता है। यह डायनामिक एरे के साथ भी काम करता है, अर्थात यदि आपका स्रोत एरे बदलता है, तो स्पिल्ड रेंज अपने‑आप अपडेट हो जाती है। यह प्रोग्रामेटिक रूप से रिपोर्ट जनरेट करते समय बहुत उपयोगी है।

## Step 4: Force Calculation – Materializing the Result

जब आप API के माध्यम से *सेल में फ़ॉर्मूला सेट* करते हैं, तो वर्कबुक स्वचालित रूप से री‑कैल्कुलेट नहीं होती। आपको एक कैल्कुलेशन पास ट्रिगर करना पड़ता है ताकि एरे **पंक्तियों में विस्तारित** हो और मान शीट में दिखें।

```java
        // 4️⃣ Recalculate the worksheet so the formula result is materialized.
        ws.getCells().calculate();
```

यदि आप इस कदम को छोड़ देते हैं, तो उत्पन्न `.xlsx` फ़ाइल को Excel में खोलने पर फ़ॉर्मूला दिखेगा लेकिन स्पिल्ड वैल्यूज़ नहीं दिखेंगी, जब तक आप **F9** नहीं दबाते। `calculate()` को कॉल करके आप सुनिश्चित करते हैं कि वर्कबुक तुरंत उपयोग के लिए तैयार है।

## Step 5: Save the Workbook and Verify Output

अंत में, वर्कबुक को फ़ाइल में सेव करें और वैकल्पिक रूप से कंसोल पर स्पिल्ड वैल्यूज़ प्रिंट करके सत्यापित करें।

```java
        // 5️⃣ Save the workbook to disk.
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // 6️⃣ (Optional) Read back the spilled values to prove it worked.
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A = index 0
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

प्रोग्राम चलाने पर आपको कंसोल आउटपुट दिखना चाहिए:

```
Workbook saved to ExpandArrayResult.xlsx
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

Excel शेष पंक्तियों को शून्य (zero) से भर देता है क्योंकि स्रोत एरे में केवल तीन तत्व थे। यह `EXPAND` का डिफ़ॉल्ट व्यवहार है। यदि आप शून्य की जगह खाली सेल चाहते हैं, तो एरे को `IFERROR` में रैप कर सकते हैं या `CHOOSE` ट्रिक्स इस्तेमाल कर सकते हैं—इस पर आगे “Advanced Variations” सेक्शन में चर्चा होगी।

## Advanced Variations & Edge Cases

### 1. Expanding a Horizontal Array to Multiple Columns

यदि आपको **एरे को पंक्तियों** *और* कॉलम में विस्तारित करना है, तो केवल तीसरा आर्ग्यूमेंट बदलें:

```java
ws.getCells().putFormula("B2", "=EXPAND({1,2,3},5,3)");
```

अब रेंज 5 × 3 ब्लॉक में फैल जाएगी, और गायब सेल्स शून्य से भरेंगे।

### 2. Using a Named Range as the Source

लिटरल `{1,2,3}` की बजाय आप एक नेम्ड रेंज रेफ़रेंस कर सकते हैं जो रन‑टाइम पर बदल सकता है:

```java
ws.getCells().putFormula("C1", "=EXPAND(MySourceRange,10,1)");
```

सुनिश्चित करें कि `MySourceRange` मौजूद है (आप इसे `ws.getNames().add("MySourceRange", "Sheet1!$D$1:$D$3")` के ज़रिए बना सकते हैं)।

### 3. Handling Non‑Numeric Data

`EXPAND` टेक्स्ट के साथ भी काम करता है। उदाहरण के लिए:

```java
ws.getCells().putFormula("D1", "=EXPAND({\"Jan\",\"Feb\",\"Mar\"},4,1)");
```

अतिरिक्त पंक्ति एक खाली स्ट्रिंग के रूप में दिखाई देगी, न कि शून्य।

### 4. Avoiding Zero Fill with `IFERROR`

यदि आप शून्य की जगह खाली सेल देखना चाहते हैं, तो `EXPAND` को `IFERROR` में रैप करें:

```java
ws.getCells().putFormula("E1", "=IFERROR(EXPAND({1,2,3},5,1), \"\")");
```

अब पंक्तियाँ 4 और 5 वास्तव में खाली रहेंगी।

## Common Pitfalls and How to Dodge Them

| Pitfall | Why It Happens | Fix |
|---------|----------------|-----|
| **Formula not recalculated** | `ws.getCells().calculate()` को भूल जाना | `putFormula` के बाद हमेशा `calculate()` कॉल करें। |
| **Zero values where blanks expected** | `EXPAND` डिफ़ॉल्ट रूप से शून्य से पैड करता है | `IFERROR(..., "")` या `CHOOSE` के साथ रैप करें। |
| **Incorrect cell address** | `"A0"` या `"1A"` का उपयोग | Excel एड्रेस 1 से शुरू होते हैं; Aspose को `"A1"` शैली चाहिए। |
| **Library version mismatch** | पुराना Aspose.Cells संस्करण उपयोग करना जिसमें `EXPAND` सपोर्ट नहीं है | नवीनतम संस्करण (लेख लिखने के समय 23.12) पर अपग्रेड करें। |

## Full Working Example (All Steps Combined)

नीचे पूरा, कॉपी‑पेस्ट‑रेडी प्रोग्राम दिया गया है। इसे `ExpandArrayDemo.java` के रूप में सेव करें, कंपाइल करें और रन करें।

```java
import com.aspose.cells.*;

public class ExpandArrayDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (blank Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);

        // Insert the EXPAND formula in A1 to expand {1,2,3} to 5 rows × 1 column
        ws.getCells().putFormula("A1", "=EXPAND({1,2,3},5,1)");

        // Force calculation so the array is materialized
        ws.getCells().calculate();

        // Save the workbook to disk
        String outPath = "ExpandArrayResult.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);

        // Verify the spilled values
        System.out.println("Spilled values:");
        for (int row = 0; row < 5; row++) {
            Cell cell = ws.getCells().get(row, 0); // Column A
            System.out.println("Row " + (row + 1) + ": " + cell.getStringValue());
        }
    }
}
```

इस प्रोग्राम को चलाने पर एक Excel फ़ाइल बनेगी जहाँ **सेल A1** में अब `EXPAND` फ़ॉर्मूला होगा, और कॉलम A की पंक्तियाँ 1‑5 में `1, 2, 3, 0, 0` दिखेंगे। फ़ाइल को Excel में खोलें और तुरंत वही परिणाम देखें—कोई मैन्युअल ड्रैगिंग नहीं।

## Conclusion

आपने अभी सीखा कि **Excel में एरे को Java के साथ विस्तारित** कैसे किया जाता है, **EXPAND का उपयोग कैसे किया जाता है**, और प्रोग्रामेटिक रूप से **सेल में फ़ॉर्मूला सेट** करके **एरे को पंक्तियों में विस्तारित** किया जाता है। Aspose.Cells की मदद से आप क्लंकी UI ट्रिक्स से बचते हैं और कोड को ही भारी काम करने देते हैं। चाहे आप रिपोर्टिंग इंजन बना रहे हों, ऑटोमेटेड डेटा‑एंट्री टूल, या कस्टम स्प्रेडशीट जेनरेटर, यह तकनीक आपको अनगिनत घंटे बचाएगी।

अगला क्या? स्थैतिक एरे को किसी अन्य शीट से खींचे गए डायनामिक रेंज से बदलें, मल्टी‑कॉलम स्पिल्स के साथ प्रयोग करें, या `EXPAND` को `FILTER` के साथ मिलाकर शक्तिशाली डेटा ट्रांसफ़ॉर्मेशन बनाएं। संभावनाएँ असीमित हैं, और अब आपके पास एक मजबूत आधार है जिस पर आप निर्माण कर सकते हैं।

कोई प्रश्न हैं या कोई कूल यूज़‑केस शेयर करना चाहते हैं? नीचे टिप्पणी करें।

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)
- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}