---
category: general
date: 2026-06-30
description: जावा का उपयोग करके एक्सेल में अद्वितीय मानों को क्रमबद्ध करें। फ़ॉर्मूला
  सेट करना, फ़ॉर्मूले पुनः गणना करना, और Aspose.Cells के साथ एक्सेल में अद्वितीय सूची
  उत्पन्न करना सीखें।
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: hi
og_description: जावा के साथ एक्सेल में अद्वितीय मानों को सॉर्ट करें। यह गाइड दिखाता
  है कि फ़ॉर्मूला कैसे सेट करें, फ़ॉर्मूले को पुनः गणना करें, और मिनटों में एक्सेल
  में एक अद्वितीय सूची कैसे बनाएं।
og_title: एक्सेल में अद्वितीय मानों को क्रमबद्ध करें – एरे फॉर्मूले के लिए जावा ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: एक्सेल में अद्वितीय मानों को क्रमबद्ध करें – एरे फ़ॉर्मूले सेट करने के लिए
  पूर्ण जावा गाइड
url: /hi/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में यूनिक वैल्यूज़ को सॉर्ट करें – एरे फ़ॉर्मूला सेट करने के लिए पूर्ण जावा गाइड

क्या आप कभी सोचते थे कि **sort unique values Excel** को फ़ॉर्मूले खींचे बिना कैसे किया जाए? आप अकेले नहीं हैं। कई रिपोर्टिंग परिदृश्यों में आपको विशिष्ट प्रविष्टियों की साफ़, वर्णक्रमानुसार सॉर्टेड सूची चाहिए, और इसे मैन्युअल रूप से करना कष्टदायक है।  

अच्छी खबर? कुछ ही जावा लाइनों के साथ आप वर्कशीट पर **set array formula** लगा सकते हैं, फिर **recalculate formulas** करके स्पिल्ड रेंज को स्वतः भरवा सकते हैं। इस ट्यूटोरियल में हम सब कुछ चरण‑दर‑चरण देखेंगे—वर्कबुक बनाने से लेकर Excel‑स्टाइल यूनिक लिस्ट जेनरेट करने तक—ताकि आप इस समाधान को सीधे अपने एप्लिकेशन में एम्बेड कर सकें।

## इस ट्यूटोरियल में क्या कवर किया गया है

- Aspose.Cells (कोड स्निपेट को पावर देने वाली लाइब्रेरी) के साथ जावा प्रोजेक्ट सेट अप करना।  
- `SORT` और `UNIQUE` फ़ंक्शन्स को साथ में उपयोग करके **generate unique list Excel** परिणाम बनाना।  
- प्रोग्रामेटिकली किसी सेल पर **array formula** लागू करना।  
- एक कैलकुलेशन पास ट्रिगर करना ताकि **how to recalculate formulas** कदम तुरंत हो सके।  
- आउटपुट की वैरिफिकेशन और एज केस जैसे खाली सेल या नॉन‑कंटिग्युअस रेंज के लिए समाधान को ट्यून करना।

इस गाइड के अंत तक आप किसी भी जावा सर्विस में एक रेडी‑टू‑यूज़ मेथड डाल सकेंगे जो साफ़ Excel शीट्स एक्सपोर्ट करना चाहती है।

> **Pro tip:** यदि आप पहले से Maven इस्तेमाल कर रहे हैं, तो Aspose.Cells को डिपेंडेंसी के रूप में जोड़ने से आपको JAR फ़ाइलों को मैन्युअली हैंडल करने की ज़रूरत नहीं पड़ेगी।

---

## प्री‑रिक्विज़िट्स

| Requirement | Why it matters |
|-------------|----------------|
| Java 8 or newer | Aspose.Cells targets Java 8+. |
| Maven (or Gradle) | Simplifies dependency management. |
| Aspose.Cells for Java | Provides the `Workbook`, `Worksheet`, and formula APIs we’ll use. |
| Basic familiarity with Excel functions | Understanding `SORT` and `UNIQUE` helps you adapt the code. |

> *यदि आपके पास अभी तक Aspose.Cells नहीं है, तो इसे अपने `pom.xml` में जोड़ें*:  

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Step 1: Create a New Workbook (How to Set Formula Begins Here)

पहले हमें एक खाली वर्कबुक चाहिए। इसे हम उस खाली कैनवास की तरह समझें जहाँ बाद में हम **set array formula** को सेल `A1` पर लागू करेंगे।

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *नया वर्कबुक क्यों बनाते हैं?*  
> यह एक साफ़ वातावरण सुनिश्चित करता है, जिससे छिपे हुए फ़ॉर्मूले जो हमारे टेस्ट डेटा में बाधा डाल सकते हैं, हट जाते हैं।

---

## Step 2: Populate Sample Data (Optional but Helpful)

परिणाम को स्पष्ट रूप से देखने के लिए, चलिए कॉलम **B** को कुछ डुप्लिकेट एंट्रीज़ से भरते हैं।

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *कॉलम B क्यों इस्तेमाल किया?*  
> हमारा फ़ॉर्मूला `B1:B10` को रेफ़र करता है, इसलिए डेटा को वहीं रखने से क्लासिक Excel उदाहरण की नकल होती है।

---

## Step 3: Set an Array Formula That **Sort Unique Values Excel**

अब जादू शुरू होता है। हम `UNIQUE` (डुप्लिकेट हटाने के लिए) को `SORT` (वर्णक्रम में क्रमबद्ध करने के लिए) के साथ मिलाते हैं। परिणामी एक्सप्रेशन एक **array formula** है, जिसका अर्थ है कि यह स्वचालित रूप से पड़ोसी सेल्स में स्पिल हो जाएगा।

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### How It Works

- `UNIQUE(B1:B10)` रेंज को स्कैन करता है और विशिष्ट स्ट्रिंग्स की वर्टिकल एरे रिटर्न करता है।  
- `SORT(...)` उस एरे को आरोही क्रम में व्यवस्थित करता है।  
- पूरी एक्सप्रेशन को `=` से रैप करके `setFormulaArray` कॉल करने से Aspose.Cells इसे **spilled array** के रूप में ट्रीट करता है, ठीक Excel की तरह।

> **Note:** यदि आप पुराने Excel संस्करण का उपयोग कर रहे हैं जिसमें `SORT` या `UNIQUE` नहीं है, तो आप **LET** फ़ंक्शन के साथ `SORT(UNIQUE(...))` या लेगेसी एरे फ़ॉर्मूले (`=INDEX(...)`) का उपयोग कर सकते हैं। यह ट्यूटोरियल आधुनिक डायनामिक एरे अप्रोच पर फोकस करता है क्योंकि यह **generate unique list Excel** करने का सबसे साफ़ तरीका है।

---

## Step 4: Recalculate Formulas So the Spilled Range Is Populated

फ़ॉर्मूला लागू करने के बाद, वर्कबुक स्वतः उसका मूल्यांकन नहीं करती। यहीं पर **how to recalculate formulas** कदम आता है।

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

`calculateFormula()` कॉल करने से Aspose.Cells Excel इंजन को चलाता है, जिससे सेल्स `A1`, `A2`, … स्वचालित रूप से सॉर्टेड यूनिक वैल्यूज़ से भर जाते हैं।

> *लेज़ी इवैल्युएशन पर भरोसा क्यों नहीं करें?*  
> सर्वर‑साइड कॉन्टेक्स्ट में अक्सर आपको डेटा को तुरंत एक्सपोर्ट (CSV, PDF, आदि) करने की ज़रूरत होती है, इसलिए स्पष्ट कॉल कंसिस्टेंसी सुनिश्चित करता है।

---

## Step 5: Verify the Result (Optional Debugging)

जब आप नई API सीख रहे हों, तो स्पिल्ड वैल्यूज़ को कंसोल पर प्रिंट करना हमेशा एक अच्छा विचार है।

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

प्रोग्राम चलाने पर यह आउटपुट देगा:

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

`SortedUniqueValues.xlsx` खोलें और आपको वही डेटा `A1` से नीचे की ओर स्पिल्ड दिखेगा।

---

## Handling Edge Cases

### Empty Cells in the Source Range

यदि `B1:B10` में ब्लैंक्स हैं, तो `UNIQUE` उन्हें एक अलग एंट्री मान लेगा। ब्लैंक्स को इग्नोर करने के लिए रेंज को `FILTER` से रैप करें:

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Non‑Contiguous Data

जब आपका डेटा कई कॉलम में फैला हो, तो आप `CHOOSE` या `TEXTJOIN` के साथ उन्हें जोड़ सकते हैं और फिर `UNIQUE` लागू कर सकते हैं। उदाहरण के लिए:

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

ये ट्यूनिंग दिखाती हैं कि **how to set formula** को अधिक जटिल परिदृश्यों में कैसे लचीलापन मिलता है।

---

## Full Working Example (All Steps Combined)

नीचे पूरा, रन‑एबल जावा प्रोग्राम दिया गया है। इसे अपने IDE में कॉपी‑पेस्ट करें, Aspose.Cells डिपेंडेंसी जोड़ें, और *Run* दबाएँ।

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Expected output** (कंसोल में दिखाया गया) पहले चर्चा किए गए सॉर्टेड, डिडुप्लिकेटेड लिस्ट के समान है। जेनरेटेड Excel फ़ाइल खोलने पर वही वैल्यूज़ `A1` से नीचे की ओर स्पिल्ड दिखेंगी।

---

## Frequently Asked Questions

**Q: Does this work with older Excel versions (pre‑Office 365)?**  
A: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine introduced in Excel 365. For legacy files you’d need to use classic array formulas like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells can still evaluate them, but the syntax is more verbose.

**Q: Can I set the array formula on a range other than `A1`?**  
A: Absolutely. Just change the address in `cells.get("A1")`. The spilled array will always start at the cell you specify and expand right‑and‑down as needed.

**Q: What if my source data is larger than `B1:B10`?**  
A: Replace the static range with a dynamic one, e.g., `B:B` or a named range. The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references on very large sheets; they can impact performance.

---

## Conclusion

हमने अभी **how to set formula** को जावा में उपयोग करके **sort unique values Excel** करने, **recalculate formulas** करने, और Aspose.Cells की पावरफ़ुल API से **generate unique list Excel** बनाने का तरीका कवर किया। कदम सरल हैं: वर्कबुक बनाएं, डेटा पॉपुलेट करें, एरे फ़ॉर्मूला लागू करें, कैलकुलेशन ट्रिगर करें, और परिणाम वैरिफ़ाई करें।  

अब आप आगे बढ़ सकते हैं—कंडीशनल फ़ॉर्मेटिंग जोड़ें, PDF में एक्सपोर्ट करें, या इस मेथड को वेब सर्विस में इंटीग्रेट करें जो तैयार‑रिपोर्ट्स डिलीवर करती है। मुख्य विचार वही रहता है: Excel के फ़ंक्शन्स को भारी काम करने दें, और जावा को प्रोसेस ऑर्केस्ट्रेट करने दें।

क्या आप अपनी Excel ऑटोमेशन को लेवल‑अप करने के लिए तैयार हैं? `SORT` की जगह `SORTBY` इस्तेमाल करके सेकेंडरी कॉलम के आधार पर क्रमबद्ध करें, या `FILTER` के साथ उन रो को बाहर रखें जो बिज़नेस रूल्स को पूरा नहीं करते। संभावनाएँ लगभग अनंत हैं।

---

###

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}