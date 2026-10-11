---
category: general
date: 2026-10-10
description: जावा में एक्सेल फ़ाइलें पढ़ते और लिखते समय एक्सपैंड फ़ंक्शन का उपयोग
  कैसे करें, सीखें। पूर्ण कोड और व्याख्याओं के साथ चरण‑दर‑चरण गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use expand function
- read and write excel file java
- Java Excel formula
- Aspose.Cells expand
- Excel dynamic range Java
language: hi
lastmod: 2026-10-10
og_description: जावा में एक्सेल फ़ाइलें पढ़ते और लिखते समय एक्सपैंड फ़ंक्शन का उपयोग
  कैसे करें। Aspose.Cells के साथ डायनेमिक रेंज जोड़ने के लिए इस पूर्ण ट्यूटोरियल का
  पालन करें।
og_image_alt: Screenshot of Java code using the EXPAND function on an Excel worksheet
og_title: जावा एक्सेल प्रोसेसिंग में एक्सपैंड फ़ंक्शन का उपयोग कैसे करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to use expand function while reading and writing Excel files
    in Java. Step‑by‑step guide with complete code and explanations.
  headline: How to use expand function in Java Excel processing
  type: TechArticle
tags:
- Java
- Excel
- Aspose.Cells
- Formula
title: जावा एक्सेल प्रोसेसिंग में एक्सपैंड फ़ंक्शन का उपयोग कैसे करें
url: /hi/java/range-management/how-to-use-expand-function-in-java-excel-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java Excel प्रोसेसिंग में EXPAND फ़ंक्शन का उपयोग कैसे करें

यदि आपको Java में Excel फ़ाइलों के साथ काम करते समय **EXPAND फ़ंक्शन का उपयोग कैसे करें** की आवश्यकता है, तो यह गाइड आपको बिल्कुल वही दिखाता है। ट्यूटोरियल के अंत तक आप Excel फ़ाइल Java प्रोजेक्ट्स को पढ़ने और लिखने में सक्षम होंगे जो `EXPAND` फ़ॉर्मूला के साथ सेल रेंज को गतिशील रूप से विस्तारित करते हैं।

Excel स्प्रेडशीट्स के साथ काम करना अक्सर उन फ़ॉर्मूलों को संभालने का मतलब होता है जो बदलते डेटा आकार के अनुसार अनुकूलित होते हैं। `EXPAND` फ़ंक्शन, जो Excel के हालिया संस्करणों में पेश किया गया है, आपको किसी रेफ़रेंस को निर्दिष्ट संख्या में पंक्तियों और कॉलमों द्वारा बढ़ाने की अनुमति देता है। एक मजबूत Java लाइब्रेरी के साथ मिलाकर, आप इस व्यवहार को अपने कोडबेस से बाहर निकले बिना स्वचालित कर सकते हैं।

इस ट्यूटोरियल में आप करेंगे:

* मौजूदा वर्कबुक लोड करें (`read and write excel file java` परिदृश्य)  
* `EXPAND` फ़ॉर्मूला को किसी सेल पर लागू करें  
* फ़ॉर्मूलों को पुनः गणना करें ताकि नया मान दिखाई दे  
* अपडेटेड वर्कबुक सहेजें  

**पूर्वापेक्षाएँ:**

* Java 17 या बाद का संस्करण स्थापित हो  
* निर्भरता प्रबंधन के लिए Maven या Gradle  
* Aspose.Cells for Java (लाइब्रेरी जो `Workbook`, `Worksheet`, आदि प्रदान करती है)  

> **Pro tip:** Aspose.Cells दोनों `.xlsx` और `.xls` फ़ॉर्मैट्स के साथ काम करता है और होस्ट मशीन पर Microsoft Office की आवश्यकता नहीं होती।

## आपको क्या चाहिए

| आइटम | कारण |
|------|--------|
| JDK 17+ | आधुनिक भाषा सुविधाएँ और बेहतर प्रदर्शन |
| Maven/Gradle | लाइब्रेरी को आसानी से शामिल करना |
| Aspose.Cells for Java | `Workbook`, `Worksheet`, और फ़ॉर्मूला इंजन प्रदान करता है |
| एक Excel फ़ाइल (`input.xlsx`) | `EXPAND` फ़ंक्शन को दर्शाने के लिए स्रोत वर्कबुक |

Maven के साथ अपने प्रोजेक्ट में Aspose.Cells जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

या Gradle के साथ:

```groovy
implementation 'com.aspose:aspose-cells:23.12'
```

## चरण 1: वर्कबुक लोड करें (EXPAND फ़ंक्शन का उपयोग – प्रारंभिक सेटअप)

पहला कार्य वह Excel फ़ाइल खोलना है जिसे आप संशोधित करना चाहते हैं। `Workbook` पूरी फ़ाइल को मेमोरी में प्रतिनिधित्व करता है।

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load the workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**Why this matters:** वर्कबुक लोड करने से आपको सभी वर्कशीट्स, सेल्स और आंतरिक फ़ॉर्मूला इंजन तक पहुँच मिलती है। बिना लोडेड वर्कबुक के आप Excel फ़ाइल Java डेटा को पढ़ या लिख नहीं सकते।

## चरण 2: लक्ष्य Worksheet तक पहुँचें

अधिकांश वर्कबुक में कई शीट्स होती हैं; उदाहरण में पहली शीट (इंडेक्स 0) का उपयोग किया गया है। आप नाम द्वारा भी शीट प्राप्त कर सकते हैं।

```java
        // Access the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

**Explanation:** `Worksheet` ऑब्जेक्ट्स `Cells` कलेक्शन को उजागर करते हैं, जहाँ आप फ़ॉर्मूले सेट करते हैं। यदि आपको किसी अलग शीट को लक्षित करना है, तो इंडेक्स को उपयुक्त संख्या से बदलें या `get("SheetName")` कॉल करें।

## चरण 3: EXPAND फ़ॉर्मूला सेट करें (व्यावहारिक उपयोग)

अब हम `EXPAND` फ़ॉर्मूला को सेल **B1** में लिखते हैं। फ़ॉर्मूला रेफ़रेंस `A1` को **5 पंक्तियों** और **1 कॉलम** द्वारा विस्तारित करता है, जिससे `A1:A6` की रेंज एक कॉलम दाईं ओर शिफ्ट हो जाती है।

```java
        // Apply the EXPAND formula to B1
        // =EXPAND(A1,5,1) expands A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");
```

**Why this works:** `setFormula` फ़ॉर्मूला स्ट्रिंग को संग्रहीत करता है; Aspose.Cells इसे तुरंत मूल्यांकन नहीं करता। `EXPAND` फ़ंक्शन बाद में जब हम गणना पास ट्रिगर करते हैं, तब मूल्यांकित होता है।

## चरण 4: फ़ॉर्मूले पुनः गणना करें (EXPAND फ़ंक्शन को अंतिम रूप देना)

फ़ॉर्मूला डालने के बाद, वर्कबुक को सभी निर्भर सेल्स को पुनः गणना करने के लिए कहें। यह कदम सुनिश्चित करता है कि नया मान वर्कशीट में दिखाई दे।

```java
        // Recalculate all formulas so the EXPAND result is evaluated
        workbook.calculateFormula();
```

**What happens behind the scenes:** गणना इंजन `EXPAND` अभिव्यक्ति को पार्स करता है, नई रेंज निर्धारित करता है, और परिणामी मानों की एरे को शीट में वापस लिखता है। यदि `A1` में कोई संख्या है, तो विस्तारित रेंज में वह संख्या नई सेल्स में दोहराई जाएगी।

## चरण 5: अपडेटेड वर्कबुक सहेजें

अंत में, संशोधित वर्कबुक को डिस्क (या आउटपुट स्ट्रीम) पर लिखें। इससे **read and write excel file java** चक्र पूरा होता है।

```java
        // Save the workbook with the new formula evaluated
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

प्रोग्राम चलाने पर `output.xlsx` बनता है जहाँ सेल **B1** अब एक स्पिल रेंज रखता है जो `A1` के मान को पाँच पंक्तियों और एक कॉलम में दोहराता है। फ़ाइल को Excel में खोलें और गतिशील एरे को कार्य करते देखें।

### अपेक्षित आउटपुट

मान लीजिए `A1` मूल रूप से संख्या `42` रखता था, तो परिणामी सेल्स इस प्रकार होंगे:

| B1 | B2 | B3 | B4 | B5 | B6 |
|----|----|----|----|----|----|
| 42 | 42 | 42 | 42 | 42 | 42 |

यदि `A1` में टेक्स्ट स्ट्रिंग है, तो वही टेक्स्ट विस्तारित रेंज में स्पिल हो जाएगा।

## सामान्य विविधताएँ और किनारे के मामले

| परिदृश्य | समायोजन |
|----------|------------|
| **Different start cell** | `"B1"` को किसी भी एड्रेस में बदलें, जैसे `"C3"` |
| **Expand by columns only** | तीन कॉलम बढ़ाने के लिए `=EXPAND(A1,0,3)` उपयोग करें |
| **Dynamic row count** | स्थिर `5` को किसी सेल रेफ़रेंस जैसे `D1` से बदलें जो इच्छित पंक्ति संख्या रखता हो |
| **Using a named range** | `A1` को परिभाषित नाम से बदलें, जैसे `=EXPAND(MyRange,5,1)` |
| **Formula errors** | सुनिश्चित करें कि वर्कबुक ऐसे फ़ॉर्मैट में सहेजी गई है जो डायनामिक एरे को सपोर्ट करता है (`.xlsx`)। पुराने `.xls` फ़ाइलें स्पिल को ट्रंकेट कर देंगी। |

### बड़े स्प्रेडशीट्स को संभालना

बहुत बड़े वर्कबुक्स के साथ काम करते समय, मेमोरी उपयोग को सीमित करने या मल्टी‑थ्रेडेड गणना सक्षम करने के लिए कस्टम `CalcOptions` ऑब्जेक्ट के साथ `workbook.calculateFormula(CalcOptions)` कॉल करें।

```java
CalcOptions options = new CalcOptions();
options.setCalculateOnOpen(true); // Faster if you only need the result later
workbook.calculateFormula(options);
```

## पूर्ण स्रोत कोड (कॉपी‑पेस्ट तैयार)

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Set a formula that expands the range of A1 by 5 rows and 1 column
        worksheet.getCells().get("B1").setFormula("=EXPAND(A1,5,1)");

        // Step 4: Recalculate all formulas so the new value is evaluated
        workbook.calculateFormula();

        // Step 5: Save the workbook with the updated data
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

> **Note:** `YOUR_DIRECTORY` को अपने Excel फ़ाइलों के पूर्ण या सापेक्ष पथ से बदलें। कोड किसी भी प्लेटफ़ॉर्म पर काम करता है जो Java द्वारा समर्थित है (Windows, macOS, Linux)।

## निष्कर्ष

अब आप **EXPAND फ़ंक्शन का उपयोग** Java वातावरण में गतिशील रूप से सेल रेफ़रेंसेज़ को बढ़ाने के लिए जानते हैं, और आपने Aspose.Cells का उपयोग करके एक पूर्ण **read and write excel file java** वर्कफ़्लो देखा है। चरण—वर्कबुक लोड करना, `EXPAND` फ़ॉर्मूला लागू करना, पुनः गणना करना, और सहेजना—Excel ऑटोमेशन के पूरे जीवनचक्र को कवर करते हैं।

**अगले कदम** जिन्हें आप एक्सप्लोर कर सकते हैं:

* `EXPAND` को `FILTER` या `SORT` जैसे अन्य डायनामिक‑एरे फ़ंक्शनों के साथ संयोजित करें।  
* उसी पैटर्न का उपयोग करके **read and write excel file java** डेटा को डेटाबेस या REST API से प्राप्त करें।  
* विस्तारित रेंज के आधार पर कंडीशनल फ़ॉर्मेटिंग के साथ प्रयोग करें।  

उदाहरण को अपने प्रोजेक्ट्स में अनुकूलित करने के लिए स्वतंत्र महसूस करें, और `EXPAND` फ़ंक्शन को किसी भी ऐसे परिदृश्य में सरल बनाते देखें जहाँ डेटा आकार समय के साथ बदलता रहता है।

--- 

*कोडिंग का आनंद लें!*

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [How to Use SEQUENCE in Java Excel Workbook – Step‑by‑Step Guide](/cells/english/java/formulas-functions/how-to-use-sequence-in-java-excel-workbook-step-by-step-guid/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [How to Use Reduce in Excel with Java – Lambda Formula Guide](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}