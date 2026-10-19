---
category: general
date: 2026-06-21
description: Aspose.Cells Java के साथ WRAPCOLS का उपयोग करके एरे को पंक्तियों में
  बदलना, सेल में सूत्र लिखना, और सूत्र के साथ सेल्स को भरना – चरण‑दर‑चरण गाइड।
draft: false
keywords:
- how to use wrapcols
- convert array to rows
- write formula to cell
- excel wrapcols example
- populate cells with formula
language: hi
og_description: Aspose.Cells के साथ Java में WRAPCOLS का उपयोग करके एरे को पंक्तियों
  में बदलना, किसी सेल में फ़ॉर्मूला लिखना, और फ़ॉर्मूला के साथ सेल्स को भरना—सभी एक
  ही गाइड में।
og_title: जावा में WRAPCOLS का उपयोग कैसे करें – पूर्ण Excel WRAPCOLS उदाहरण
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  headline: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  type: TechArticle
- description: How to use WRAPCOLS with Aspose.Cells Java to convert array to rows,
    write formula to cell, and populate cells with formula – step‑by‑step guide.
  name: How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example
  steps:
  - name: What the Formula Does
    text: '- `{1,2,3}` – a literal array containing three numbers. - `2` – the number
      of columns per row. - Result: - **A1** = 1, **B1** = 2 - **A2** = 3, **B2**
      = (blank)'
  - name: 1. Empty Arrays
    text: 'If the array literal is empty (`{}`), `WRAPCOLS` returns a `#VALUE!` error.
      To avoid breaking your sheet, guard the formula generation:'
  - name: 2. Non‑Numeric Data
    text: '`WRAPCOLS` works with text as well. For example, `WRAPCOLS({"A","B","C","D"},2)`
      produces a two‑column layout of strings. Just remember to quote strings inside
      the array literal.'
  - name: 3. Compatibility
    text: The `WRAPCOLS` function is available in Excel 365 and Excel 2019+ (Office
      2019, Excel for the web). If you need to support older versions, you’ll have
      to fall back to manual looping or use a different spill‑compatible function.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel formulas
- WRAPCOLS
title: जावा में WRAPCOLS का उपयोग कैसे करें – पूर्ण Excel WRAPCOLS उदाहरण
url: /hi/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example

क्या आपने कभी सोचा है **WRAPCOLS का उपयोग कैसे करें** जब आपको एक साधारण एरे को Excel में एक साफ़ टेबल में बदलना हो? आप अकेले नहीं हैं। कई डेवलपर्स `WRAPCOLS` फ़ंक्शन को पहली बार देखते ही रुक जाते हैं और सोचते हैं, “मैं इस फ़ॉर्मूला को Java से सेल में कैसे लिखूँ?” अच्छी खबर? सही कदम जानने के बाद यह काफी आसान है।

इस ट्यूटोरियल में हम एक पूरी तरह चलने योग्य Aspose.Cells Java उदाहरण के माध्यम से **एरे को पंक्तियों में बदलना**, फ़ॉर्मूला को सीधे सेल में लिखना, और वास्तविक‑दुनिया के परिदृश्यों के लिए **फ़ॉर्मूला के साथ सेल्स को भरना** दिखाएंगे। अंत तक आप **excel wrapcols example** की स्पष्ट समझ प्राप्त करेंगे और इसे अपने प्रोजेक्ट्स में लागू करने के लिए तैयार होंगे।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- Java 17 या उससे नया (कोड किसी भी हालिया JDK के साथ काम करता है)।
- Aspose.Cells for Java लाइब्रेरी (आप Maven Central से नवीनतम JAR प्राप्त कर सकते हैं)।
- Java सिंटैक्स और Excel फ़ॉर्मूलों की बुनियादी समझ।
- एक IDE या साधारण टेक्स्ट एडिटर—कोई विशेष टूलिंग आवश्यक नहीं।

सब कुछ तैयार? बढ़िया, चलिए शुरू करते हैं।

## Step 1: Set Up the Project and Load a Workbook

सबसे पहले—एक नया Maven (या Gradle) प्रोजेक्ट बनाएं और Aspose.Cells डिपेंडेंसी जोड़ें:

```xml
<!-- pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- check for the latest version -->
</dependency>
```

अब हम एक मौजूदा वर्कबुक लोड कर सकते हैं (या नया बना सकते हैं) और पहली वर्कशीट प्राप्त कर सकते हैं:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook (or create a new one)
        Workbook wb = new Workbook();               // creates a blank workbook
        // Alternatively, load an existing file:
        // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);
```

> **Why we load a workbook** – Aspose.Cells Excel फ़ाइल का इन‑मेमोरी प्रतिनिधित्व लेकर काम करता है। वर्कबुक को लोड (या बनाकर) हमें सेल्स, रोज़, और फ़ॉर्मूलों तक पहुँच मिलती है, जो किसी भी **write formula to cell** ऑपरेशन के लिए आवश्यक है।

## Step 2: Insert the WRAPCOLS Formula into a Cell

ट्यूटोरियल का मुख्य भाग `WRAPCOLS` फ़ंक्शन है। यह एक‑आयामी एरे को लेता है और इसे निर्दिष्ट कॉलम संख्या में “रैप” करता है, शेष को नई पंक्तियों में स्वचालित रूप से फैलाता है। यहाँ वह सिंटैक्स है जिसका हम उपयोग करेंगे:

```java
// Step 3: Set a formula that wraps a collection into rows of 2 columns
// The formula WRAPCOLS({1,2,3},2) will produce:
//   Row 1: 1, 2
//   Row 2: 3
ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");
```

ध्यान दें कि फ़ॉर्मूला एक साधारण स्ट्रिंग है जिसे `setFormula` को पास किया गया है। Aspose.Cells भारी काम करता है—फ़ॉर्मूला को पार्स करना, उसका मूल्यांकन करना, और परिणामों को वर्कशीट में फैलाना। यह **populate cells with formula** करने का सबसे सीधा तरीका है, बिना पंक्तियों और कॉलमों पर मैन्युअल इटरेशन के।

### What the Formula Does

- `{1,2,3}` – तीन संख्याओं वाला लिटरल एरे।
- `2` – प्रति पंक्ति कॉलम की संख्या।
- परिणाम:
  - **A1** = 1, **B1** = 2
  - **A2** = 3, **B2** = (खाली)

यदि आप तीन कॉलम चाहते हैं, तो दूसरे आर्ग्यूमेंट को `3` कर दें, और एरे एक ही पंक्ति में भर जाएगा।

## Step 3: Save the Workbook and Verify the Output

अब फ़ॉर्मूला **A1** में बैठ गया है, चलिए वर्कबुक को डिस्क पर सेव करते हैं ताकि आप इसे Excel में खोलकर स्पिल देख सकें:

```java
        // (Optional) Save the workbook to see the result
        wb.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

`output.xlsx` खोलें और आपको ठीक वही मिलेगा जैसा टिप्पणी में बताया गया था—पहली पंक्ति में दो कॉलम और शेष मान दूसरी पंक्ति में। यही **excel wrapcols example** का सार है।

## Step 4: Extending the Example – Converting Larger Arrays

वास्तविक प्रोजेक्ट्स में अक्सर केवल तीन संख्याएँ नहीं होतीं। मान लीजिए आपके पास बड़ा कलेक्शन है, जैसे `{10,20,30,40,50,60,70}` और आप प्रति पंक्ति तीन कॉलम चाहते हैं। कोड को इस प्रकार बदलें:

```java
String largeArray = "{10,20,30,40,50,60,70}";
int columnsPerRow = 3;
String formula = String.format("=WRAPCOLS(%s,%d)", largeArray, columnsPerRow);
ws.getCells().get("C5").setFormula(formula);
```

अब स्पिल **C5** से शुरू होगा, और परिणाम होगा:

| C5 | D5 | E5 |
|----|----|----|
|10  |20  |30  |
|40  |50  |60  |
|70  |    |    |

यह दर्शाता है कि आप **convert array to rows** को डायनामिक रूप से कैसे कर सकते हैं, केवल फ़ॉर्मूला स्ट्रिंग को बदलकर। कोई लूप नहीं, कोई मैन्युअल सेल असाइनमेंट नहीं—Aspose.Cells बाकी सब संभालता है।

## Step 5: Handling Edge Cases and Common Gotchas

### 1. Empty Arrays

यदि एरे लिटरल खाली है (`{}`), तो `WRAPCOLS` `#VALUE!` एरर लौटाता है। शीट को टूटने से बचाने के लिए फ़ॉर्मूला जेनरेशन को गार्ड करें:

```java
if (arrayContent.isEmpty()) {
    ws.getCells().get("F1").setValue("No data");
} else {
    ws.getCells().get("F1").setFormula(formula);
}
```

### 2. Non‑Numeric Data

`WRAPCOLS` टेक्स्ट के साथ भी काम करता है। उदाहरण के लिए, `WRAPCOLS({"A","B","C","D"},2)` दो‑कॉलम लेआउट में स्ट्रिंग्स बनाता है। बस एरे लिटरल के अंदर स्ट्रिंग्स को कोट्स में रखें।

### 3. Compatibility

`WRAPCOLS` फ़ंक्शन Excel 365 और Excel 2019+ (Office 2019, Excel for the web) में उपलब्ध है। यदि आपको पुराने संस्करणों को सपोर्ट करना है, तो आपको मैन्युअल लूपिंग या किसी अन्य स्पिल‑कम्पैटिबल फ़ंक्शन का उपयोग करना पड़ेगा।

## Step 6: Practical Tips and Pro Tricks

- **Pro tip:** यदि आपको उपयोगकर्ता की क्षेत्रीय सेटिंग्स के अनुसार सेपरेटर (कॉमा बनाम सेमिकॉलन) बदलना है तो `Cell.setFormulaLocal` का उपयोग करें।
- **Watch out for:** मौजूदा डेटा को ओवरराइट करना। स्पिल एरिया लक्ष्य रेंज में पहले से मौजूद किसी भी सामग्री को बदल देगा।
- **Performance note:** फ़ॉर्मूला सेट करना सस्ता है; भारी काम तब होता है जब आप **save** या **recalculate** वर्कबुक करते हैं। यदि आप हजारों फ़ॉर्मूले जनरेट कर रहे हैं, तो प्रोसेसिंग तेज़ करने के लिए ऑटोमैटिक कैलकुलेशन को डिसेबल करने (`wb.calculateFormula()` बाद में) पर विचार करें।

## Full Working Example

नीचे पूरी, तैयार‑चलाने योग्य Java क्लास दी गई है जो हमने अब तक चर्चा किए सभी बिंदुओं को सम्मिलित करती है:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook
        Workbook wb = new Workbook();

        // 2️⃣ Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // 3️⃣ Simple WRAPCOLS formula – basic excel wrapcols example
        ws.getCells().get("A1").setFormula("=WRAPCOLS({1,2,3},2)");

        // 4️⃣ Larger array with three columns per row
        String largeArray = "{10,20,30,40,50,60,70}";
        int cols = 3;
        String largeFormula = String.format("=WRAPCOLS(%s,%d)", largeArray, cols);
        ws.getCells().get("C5").setFormula(largeFormula);

        // 5️⃣ Text array demonstration
        ws.getCells().get("G1").setFormula("=WRAPCOLS({\"Apple\",\"Banana\",\"Cherry\",\"Date\"},2)");

        // 6️⃣ Save the result
        wb.save("output.xlsx");
    }
}
```

**Expected output:** `output.xlsx` खोलें और आपको तीन अलग‑अलग स्पिल रीज़न दिखेंगे:

- **A1:B2** – दो कॉलम में 1‑3 संख्याएँ रैप हुईं।
- **C5:E7** – तीन कॉलम में 10‑70 संख्याएँ रैप हुईं।
- **G1:H2** – दो कॉलम में फल के नाम रैप हुए।

## Conclusion

हमने अभी **WRAPCOLS का उपयोग Aspose.Cells for Java के साथ** किया, आपको दिखाया कि कैसे **convert array to rows**, **write formula to cell**, और **populate cells with formula** को साफ़, दोहराने योग्य तरीके से किया जा सकता है। यह तरीका थकाऊ लूपिंग को समाप्त करता है, Excel के नेटिव स्पिल व्यवहार का लाभ उठाता है, और आपके कोड को संक्षिप्त रखता है।

अगली चुनौती के लिए तैयार हैं? `WRAPCOLS` को डायनामिक डेटा स्रोतों के साथ मिलाएँ—शायद डेटाबेस से मान निकालें, एरे स्ट्रिंग को रन‑टाइम पर बनाएं, और लेआउट काम Excel को सौंपें। आप `SEQUENCE` या `FILTER` जैसे अन्य स्पिल फ़ंक्शन्स के साथ प्रयोग करके और भी समृद्ध रिपोर्ट बना सकते हैं।

यदि कोई समस्या आती है, तो नीचे कमेंट करें या Aspose की विस्तृत डॉक्यूमेंटेशन देखें। Happy coding, और Java से आधुनिक Excel फ़ॉर्मूलों की शक्ति का आनंद लें! 

![how to use wrapcols example](/images/wrapcols-demo.png "how to use wrapcols in Java – screenshot of spilled data")


## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [How to Select Cell Ranges in Excel Using Aspose.Cells for Java (2023 Guide)](/cells/english/java/range-management/aspose-cells-java-select-cell-ranges-excel/)
- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}