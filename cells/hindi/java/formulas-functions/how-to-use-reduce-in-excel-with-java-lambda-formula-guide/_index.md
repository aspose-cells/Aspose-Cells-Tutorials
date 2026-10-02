---
category: general
date: 2026-06-08
description: Java के साथ Aspose.Cells का उपयोग करके Excel में reduce कैसे उपयोग करें।
  Lambda फ़ॉर्मूला Excel, डायनामिक एरेज़ Java, Lambda कैसे लिखें, और reduce के साथ
  sum को स्पष्ट चरण‑दर‑चरण ट्यूटोरियल में सीखें।
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: hi
og_description: Java के साथ Excel में reduce का उपयोग कैसे करें। Lambda फ़ॉर्मूला
  Excel, डायनेमिक एरेज़ Java में महारत हासिल करें, और पूरी, चलाने योग्य उदाहरण के
  साथ reduce का उपयोग करके योग करें।
og_title: जावा के साथ एक्सेल में रिड्यूस का उपयोग कैसे करें – लैम्ब्डा फॉर्मूला गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: जावा के साथ एक्सेल में Reduce का उपयोग कैसे करें – लैम्ब्डा फ़ॉर्मूला गाइड
url: /hi/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में Reduce का उपयोग कैसे करें Java के साथ – Lambda Formula गाइड

क्या आप कभी सोचते थे कि **how to use reduce** Excel में Java कोड लिखते समय कैसे उपयोग किया जाए? आप अकेले नहीं हैं। कई डेवलपर्स को Excel के नए डायनामिक एरे फ़ंक्शन्स को Java‑आधारित ऑटोमेशन के साथ मिलाने में कठिनाई होती है, और उत्तर उतना जटिल नहीं है जितना पहली बार लगता है।

इस ट्यूटोरियल में हम एक ठोस उदाहरण के माध्यम से दिखाएँगे कि **how to use reduce** को **lambda formula Excel** अभिव्यक्ति के साथ कैसे उपयोग किया जाए, सभी Aspose.Cells for Java लाइब्रेरी द्वारा समर्थित। अंत तक आप Java में डायनामिक एरे जेनरेट कर पाएँगे, लैम्ब्डा फ़ंक्शन लिख पाएँगे, और **sum with reduce** की गणना कर पाएँगे—कोई मैन्युअल स्प्रेडशीट छेड़छाड़ नहीं।

---

## आप क्या बनाएँगे

- पूरी तरह से Java से बनाया गया एक नया वर्कबुक।  
- एक **EXPAND** डायनामिक एरे जो सेल्स A1:A5 को संख्याएँ 1‑5 से भरता है।  
- एक **REDUCE** फ़ॉर्मूला जो उन संख्याओं को **lambda formula Excel** का उपयोग करके जोड़ता है।  
- एक सहेजी गई `.xlsx` फ़ाइल जिसे आप किसी भी स्प्रेडशीट प्रोग्राम में खोलकर परिणाम की पुष्टि कर सकते हैं।

कोई बाहरी मैक्रो नहीं, कोई VBA नहीं—सिर्फ शुद्ध Java कोड और Excel के आधुनिक फ़ंक्शन।

---

## आवश्यकताएँ

- Java 17 (या कोई भी नवीनतम JDK) – पुराने संस्करण काम करेंगे लेकिन आप `var` की सुविधा से वंचित रहेंगे।  
- Aspose.Cells for Java (इस डेमो के लिए फ्री ट्रायल पर्याप्त है)।  
- Java सिंटैक्स और Excel फ़ॉर्मूलों की बुनियादी परिचितता।  

यदि आप **dynamic arrays java** में नए हैं, तो चिंता न करें—यह गाइड हर भाग को समझाता है।

---

## चरण 1: अपना प्रोजेक्ट सेट अप करें और Aspose.Cells इम्पोर्ट करें

सबसे पहले, अपने `pom.xml` में Aspose.Cells Maven डिपेंडेंसी जोड़ें (या JAR को मैन्युअली प्राप्त करें)।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Pro tip:** अपनी डिपेंडेंसियों को अप‑टू‑डेट रखें; नए संस्करण फ़ॉर्मूला इवैल्यूएशन की गति को सुधारते हैं, जो बड़े शीट्स में **how to use reduce** करते समय महत्वपूर्ण है।

---

## चरण 2: एक Workbook बनाएँ और पहली Worksheet तक पहुँचें

अब हम एक बिल्कुल नया वर्कबुक बनाएँगे। यह **how to use reduce** सीखने की नींव है क्योंकि वर्कबुक ऑब्जेक्ट हमें फ़ॉर्मूले डालने के लिए एक सैंडबॉक्स देता है।

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Why this matters:* `Workbook` क्लास पूरी Excel फ़ाइल को एब्स्ट्रैक्ट करती है, जबकि `Worksheet` एकल टैब को दर्शाता है। बाद में आप देखेंगे कि **dynamic arrays java** कैसे एक ही फ़ॉर्मूले को A1 में रखकर कई सेल्स भर सकता है।

---

## चरण 3: EXPAND के साथ एक वर्टिकल एरे जेनरेट करें

Excel का `EXPAND` फ़ंक्शन मानों को एक रेंज में स्पिल कर सकता है। हम इसे कॉलम A में 1 से 5 तक की संख्याएँ बनाने के लिए उपयोग करेंगे।

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

यदि आप उत्पन्न वर्कबुक खोलते हैं, तो सेल्स A1:A5 क्रमशः 1, 2, 3, 4, 5 दिखाएँगे। यह **dynamic arrays java** भाग है—एक फ़ॉर्मूला पूरे रेंज को भर देता है।

---

## चरण 4: एरे को जोड़ने के लिए REDUCE लैम्ब्डा लिखें

यहाँ हम मुख्य प्रश्न का उत्तर देते हैं: **how to use reduce** Excel में Java से। `REDUCE` फ़ंक्शन एरे पर इटरेट करता है और आप द्वारा प्रदान किए गए लैम्ब्डा को लागू करता है। हमारे मामले में हम संख्याओं को जोड़ेंगे।

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

आइए इसे तोड़‑कर देखें:

- `0` – प्रारंभिक एक्यूमुलेटर मान (`acc`)।  
- `A1:A5` – वह एरे जिसे हमने **EXPAND** से जेनरेट किया था।  
- `LAMBDA(acc, x, acc + x)` – वह **lambda formula Excel** जो प्रत्येक तत्व (`x`) को एक्यूमुलेटर (`acc`) में जोड़ता है।  

जब फ़ॉर्मूला चलाया जाता है, तो `B1` में **15** आता है, यानी 1‑5 संख्याओं का **sum with reduce**।

> **How to write lambda** in Excel? इसे एक अनाम फ़ंक्शन के रूप में सोचें जहाँ पहले आर्ग्युमेंट पैरामीटर होते हैं, और अंतिम अभिव्यक्ति रिटर्न वैल्यू होती है। Java में हम केवल टेक्स्ट एम्बेड करते हैं; वास्तविक कार्य Excel इंजन करता है।

---

## चरण 5: वर्कबुक को सेव करें

अंत में, हम वर्कबुक को डिस्क पर सहेजते हैं ताकि आप इसे Excel, Google Sheets, या किसी भी `.xlsx` सपोर्ट करने वाले व्यूअर में खोल सकें।

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

फ़ाइल खोलें और आपको यह दिखेगा:

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

**sum with reduce** B1 में दिखाई देता है, जो पुष्टि करता है कि हमने **how to use reduce** को **lambda formula Excel** के साथ Java से सफलतापूर्वक प्रदर्शित किया है।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, तैयार‑to‑run Java प्रोग्राम दिया गया है। इसे अपने IDE में कॉपी‑पेस्ट करें, आउटपुट डायरेक्टरी समायोजित करें, और **Run** दबाएँ।

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Expected output** जब आप `new-functions.xlsx` खोलते हैं:

- सेल्स **A1:A5** में `1, 2, 3, 4, 5` होते हैं।  
- सेल **B1** `15` दिखाता है, जो **sum with reduce** की पुष्टि करता है।

---

## सामान्य प्रश्न एवं किनारे के मामले

### यदि मुझे वर्टिकल के बजाय हॉरिज़ॉन्टल एरे चाहिए तो क्या करें?

`EXPAND` में कॉलम/रो आर्ग्युमेंट बदलें। B1:F1 तक हॉरिज़ॉन्टल स्पिल के लिए:

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### क्या मैं SUM के बजाय गुणा करने के लिए REDUCE का उपयोग कर सकता हूँ?

बिल्कुल। केवल लैम्ब्डा बॉडी बदलें:

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

अब B1 में `120` दिखेगा (5 ! = 120)।

### क्या Aspose.Cells कस्टम LAMBDA फ़ंक्शन सपोर्ट करता है?

हाँ, आप वर्कबुक के `Names` कलेक्शन के माध्यम से नामित LAMBDA फ़ंक्शन परिभाषित कर सकते हैं, फिर उन्हें किसी भी बिल्ट‑इन फ़ॉर्मूले की तरह कॉल कर सकते हैं। यह बाद के ट्यूटोरियल में **how to write lambda** फ़ंक्शन के बारे में गहराई से चर्चा करेगा जो एकल सेल से परे रहते हैं।

### पुराने Excel संस्करण जो REDUCE को पहचानते नहीं हैं, उनके बारे में क्या?

यदि आप Excel 2019 या उससे पहले को टार्गेट करते हैं, तो इंजन `#NAME?` रिटर्न करेगा। ऐसे मामलों में

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच खोजने में मदद करेंगे।

- [Aspose.Cells Java में महारत: Excel वर्कबुक में फ़ॉर्मूला कैलकुलेशन को इंटरप्ट कैसे करें](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Aspose.Cells for Java के साथ Excel सेल नामों को इंडेक्स में बदलना: चरण‑दर‑चरण गाइड](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [Aspose.Cells for Java के साथ Excel सेल बनाना और फॉर्मेट करना: चरण‑दर‑चरण गाइड](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}