---
category: general
date: 2026-10-07
description: Aspose.Cells for Java का उपयोग करके कॉलम कैसे विभाजित करें। स्ट्रिंग
  को कॉलम में विभाजित करना सीखें, Excel फ़ॉर्मूला को स्वचालित करें, और कुछ पंक्तियों
  के कोड में सेल में फ़ॉर्मूला लिखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: hi
lastmod: 2026-10-07
og_description: Java में Aspose.Cells के साथ कॉलम कैसे विभाजित करें। यह ट्यूटोरियल
  आपको दिखाता है कि स्ट्रिंग को कॉलम में कैसे विभाजित करें, Excel फ़ॉर्मूला मूल्यांकन
  को स्वचालित करें, और किसी सेल में फ़ॉर्मूला लिखें।
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Aspose.Cells के साथ जावा में कॉलम कैसे विभाजित करें – त्वरित ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells के साथ जावा में कॉलम कैसे विभाजित करें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java के साथ Aspose.Cells में कॉलम कैसे विभाजित करें – चरण‑दर‑चरण गाइड

यदि आपको प्रोग्रामेटिक रूप से Excel वर्कशीट में **how to split columns** करने की आवश्यकता है, तो यह गाइड Aspose.Cells for Java के साथ पूरी प्रक्रिया दिखाता है। आप यह भी सीखेंगे कि **split string into columns**, **automate Excel formula** मूल्यांकन कैसे किया जाता है, और **write formula to a cell** को संक्षिप्त, प्रोडक्शन‑रेडी कोड का उपयोग करके कैसे लिखा जाता है।

प्रोग्रामेटिक कॉलम विभाजन मैन्युअल कॉपी‑पेस्ट को समाप्त करता है, त्रुटियों को कम करता है, और बड़े‑पैमाने पर डेटा ट्रांसफ़ॉर्मेशन को सक्षम बनाता है। इस ट्यूटोरियल के अंत तक आप फ़ॉर्मूले को ऑन‑द‑फ़्लाई जेनरेट, मॉडिफ़ाई और मूल्यांकन कर सकते हैं, जिससे Excel आपके Java बैकएंड का वास्तविक भाग बन जाता है।

## आवश्यकताएँ

* Java 17 या बाद का संस्करण स्थापित हो।
* Maven 3.8+ (या Gradle) डिपेंडेंसी मैनेजमेंट के लिए।
* Aspose.Cells for Java लाइसेंस (शिक्षा के लिए फ्री इवैल्यूएशन वर्ज़न काम करता है)।
* Java सिंटैक्स और Excel अवधारणाओं की बुनियादी समझ।

यदि इनमें से कोई भी आइटम गायब है, तो पहले उन्हें इंस्टॉल करें; कोड सैंपल मानक Maven प्रोजेक्ट मानते हैं।

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

अपने `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें। यह नवीनतम स्थिर Aspose.Cells लाइब्रेरी को पुल करता है।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Why this step matters:** लाइब्रेरी `Workbook`, `Worksheet`, और `Cell` क्लासेज़ प्रदान करती है जो Microsoft Office के बिना Excel फ़ाइलों को मैनीपुलेट करने के लिए आवश्यक हैं। डिपेंडेंसी के बिना कोड कंपाइल नहीं होगा।

## चरण 2: एक वर्कबुक बनाएं और पहली वर्कशीट चुनें

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

`Workbook` ऑब्जेक्ट पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। पहली वर्कशीट को एक्सेस करने से फ़ॉर्मूला लिखने के लिए एक पूर्वानुमेय शुरुआती बिंदु मिलता है।

## चरण 3: लक्ष्य सेल में WRAPCOLS फ़ॉर्मूला लिखें

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Why we use `WRAPCOLS`:** बिल्ट‑इन Excel फ़ंक्शन `WRAPCOLS` स्वचालित रूप से एकल टेक्स्ट वैल्यू को परिभाषित संख्या के कॉलम में विभाजित करता है, शब्द सीमाओं को बुद्धिमानी से संभालता है। यह **split string into columns** करने का सबसे भरोसेमंद तरीका है बिना कस्टम पार्सिंग लॉजिक के।

## चरण 4: वर्कबुक को फ़ॉर्मूला का मूल्यांकन करने के लिए मजबूर करें

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

`calculateFormula()` को कॉल करने से **automate Excel formula** मूल्यांकन सर्वर साइड पर होता है। इस कॉल के बिना सेल में अभी भी फ़ॉर्मूला टेक्स्ट रहेगा, न कि गणना किए गए मान।

## चरण 5: रैप्ड परिणाम प्राप्त करें और प्रदर्शित करें

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

जब आप प्रोग्राम चलाते हैं, तो कंसोल प्रिंट करता है:

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

जनरेट हुई `SplitColumnsResult.xlsx` फ़ाइल दिखाती है कि तीन कॉलम विभाजित टेक्स्ट से भर गए हैं।

## WRAPCOLS फ़ंक्शन को समझना

* **Syntax:** `WRAPCOLS(text, columns, [delimiter])`
* **Parameters:**
  * `text` – वह स्ट्रिंग जिसे आप विभाजित करना चाहते हैं।
  * `columns` – वह कॉलम संख्या जिसमें टेक्स्ट को वितरित किया जाएगा।
  * `delimiter` (optional) – स्ट्रिंग को तोड़ने के लिए उपयोग किया जाने वाला कैरेक्टर; डिफ़ॉल्ट स्पेस है।
* **Return value:** एक एरे जो सटे हुए सेल्स में फैलता है, प्रत्येक एलिमेंट मूल टेक्स्ट का एक भाग रखता है।

क्योंकि फ़ंक्शन क्षैतिज रूप से फैलता है, आपको केवल फ़ॉर्मूला बाएँmost सेल (उदाहरण में A1) में लिखना है। Excel स्वचालित रूप से B1, C1, … को आवश्यकतानुसार भर देता है।

## सामान्य विविधताएँ और किनारे के मामलों

| Situation | Recommended adjustment |
|-----------|------------------------|
| **Variable column count** | हार्ड‑कोडेड `3` को एक वेरिएबल से बदलें: `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Custom delimiter** | तीसरे आर्ग्यूमेंट का उपयोग करें, उदाहरण: `=WRAPCOLS(A2,4,",")` जिससे कॉमा पर विभाजन हो। |
| **Empty source string** | फ़ंक्शन खाली सेल्स लौटाता है; फ़ॉर्मूला सेट करने से पहले `null` या खाली स्ट्रिंग्स की जाँच करें। |
| **Large datasets** | प्रत्येक रो के लिए लूप में फ़ॉर्मूला लागू करें, फिर लूप के बाद एक बार `calculateFormula()` कॉल करें ताकि प्रदर्शन बेहतर हो। |
| **Non‑ASCII characters** | WRAPCOLS यूनिकोड के साथ काम करता है; सुनिश्चित करें कि आपका Java स्रोत फ़ाइल UTF‑8 में सेव हो। |

**Pro tip:** कई रो प्रोसेस करते समय फ़ॉर्मूला को एक स्ट्रिंग वेरिएबल में स्टोर करें और पुन: उपयोग करें ताकि बार‑बार स्ट्रिंग कंकैटनेशन ओवरहेड से बचा जा सके।

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी‑पेस्ट कर सकते हैं। इसमें इम्पोर्ट स्टेटमेंट्स, एक्सेप्शन हैंडलिंग, और एक वैकल्पिक सेव ऑपरेशन शामिल है।

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

इस प्रोग्राम को चलाने से वही कंसोल आउटपुट प्राप्त होता है जैसा पहले दिखाया गया था और एक Excel फ़ाइल लिखी जाती है जो स्पष्ट रूप से **how to split columns** को दर्शाती है।

## समस्या निवारण चेकलिस्ट

* **Formula not evaluating** – फ़ॉर्मूला सेट करने के बाद `workbook.calculateFormula()` कॉल करना सुनिश्चित करें।
* **Empty cells after split** – स्रोत स्ट्रिंग `null` या खाली न हो, और कॉलम काउंट शून्य से बड़ा हो, यह जाँचें।
* **License exception** – वर्कबुक बनाने से पहले वैध Aspose.Cells लाइसेंस फ़ाइल प्रदान करें (`License license = new License(); license.setLicense("Aspose.Total.lic");`) ताकि इवैल्यूएशन वाटरमार्क हट जाएँ।
* **Performance lag on large sheets** – सभी फ़ॉर्मूले लिखने के बाद एक बार `calculateFormula()` कॉल करें, प्रत्येक सेल के बाद नहीं।

## निष्कर्ष

आप अब जानते हैं कि Java में Aspose.Cells का उपयोग करके **how to split columns** कैसे किया जाता है, `WRAPCOLS` फ़ंक्शन के साथ **split string into columns** कैसे किया जाता है, **automate Excel formula** मूल्यांकन कैसे किया जाता है, और प्रोग्रामेटिक रूप से **write formula to a cell** कैसे किया जाता है। यह तकनीक मैन्युअल डेटा‑प्रिपरेशन चरणों को हटाती है और Excel की शक्तिशाली टेक्स्ट‑हैंडलिंग क्षमताओं को सीधे आपके Java एप्लिकेशन में एकीकृत करती है।

### अगले कदम

* `TEXTSPLIT` और `FILTERXML` जैसे अन्य टेक्स्ट फ़ंक्शन का अन्वेषण करें ताकि अधिक जटिल पार्सिंग परिदृश्य संभाले जा सकें।
* अप्रत्याशित इनपुट को सुगमता से हैंडल करने के लिए `WRAPCOLS` को `IFERROR` के साथ संयोजित करें।
* समाधान को एक Spring Boot सर्विस में इंटीग्रेट करें जो REST के माध्यम से CSV डेटा प्राप्त करता है और एक पॉप्युलेटेड Excel फ़ाइल लौटाता है।

इन पैटर्न को मास्टर करके आप मजबूत, ऑटोमेटेड Excel वर्कफ़्लो बना सकते हैं जो आपके व्यवसाय की जरूरतों के साथ स्केल होते हैं। Happy coding!

## आपको अगला क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [aspose cells java – नामों को कॉलम में विभाजित करें](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Aspose.Cells का उपयोग करके Java में Excel कॉलम को ऑटो‑फ़िट करें](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [Aspose.Cells Java का उपयोग करके Excel में खाली कॉलम कैसे हटाएँ&#58; एक व्यापक गाइड](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}