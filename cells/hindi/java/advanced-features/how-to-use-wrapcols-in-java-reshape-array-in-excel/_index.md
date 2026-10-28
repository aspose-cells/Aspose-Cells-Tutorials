---
category: general
date: 2026-08-04
description: wrapcols का उपयोग कैसे करें, एक पूर्ण Java उदाहरण के साथ, Excel में एरे
  को पुनः आकार दें और Aspose.Cells का उपयोग करके वर्कबुक को फ़ाइल में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- save workbook to file
- reshape array in excel
- excel wrapcols example
- create excel workbook java
language: hi
lastmod: 2026-08-04
og_description: Java के साथ Excel में wrapcols का उपयोग करके एक array को reshape कैसे
  करें। एक पूर्ण Excel wrapcols उदाहरण सीखें, Java में Excel वर्कबुक बनाएं और वर्कबुक
  को फ़ाइल में सहेजें।
og_image_alt: Screenshot showing how to use WRAPCOLS in Java to reshape an array in
  Excel
og_title: Java में wrapcols का उपयोग कैसे करें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-04'
  description: how to use wrapcols with a complete Java example, reshape array in
    Excel and save workbook to file using Aspose.Cells
  headline: how to use wrapcols in Java – reshape array in Excel
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Java में wrapcols का उपयोग कैसे करें – Excel में एरे को पुनः आकार दें
url: /hi/java/advanced-features/how-to-use-wrapcols-in-java-reshape-array-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में wrapcols का उपयोग कैसे करें – Excel में एरे को पुनः आकार देना

यदि आपको **how to use wrapcols** की आवश्यकता है ताकि आप मानों की एक सपाट सूची को कई‑पंक्तियों की रेंज में बदल सकें, तो यह गाइड आपको सटीक चरण दिखाता है। आप एक **excel wrapcols example** देखेंगे जो 1‑D एरे को 3‑पंक्ति × 2‑कॉलम ब्लॉक में पुनः आकार देता है, और आप सीखेंगे कि Aspose.Cells के साथ **save workbook to file** कैसे किया जाता है।

इस ट्यूटोरियल के अंत तक आप **create excel workbook java** कोड बना पाएँगे जो:

* एक नया वर्कबुक इनिशियलाइज़ करता है और सेल A1 को चुनता है।  
* डेटा को पुनः आकार देने के लिए `WRAPCOLS` फ़ंक्शन लागू करता है।  
* फ़ॉर्मूला की गणना को मजबूर करता है ताकि परिणाम तुरंत दिखे।  
* गणना किए गए एरे से एक मान प्राप्त करता है।  
* वर्कबुक को डिस्क पर सहेजता है।

केवल पूर्वापेक्षा यह है कि आपके पास एक Java विकास वातावरण (JDK 8 या नया) और Aspose.Cells for Java लाइब्रेरी हो।

---

## आवश्यकताएँ

* JDK 8 + (या कोई भी नया संस्करण)।  
* Maven या Gradle का उपयोग करके Aspose.Cells निर्भरता को प्रबंधित करें।  
* Java सिंटैक्स और Excel फ़ॉर्मूले की बुनियादी परिचितता।

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** यदि आप Gradle का उपयोग करते हैं, तो XML स्निपेट को संबंधित `implementation` लाइन से बदलें।

---

## चरण 1: Java में एक Excel वर्कबुक बनाएं

पहला ऑपरेशन यह है कि **create excel workbook java** कोड लिखा जाए जो एक नई वर्कबुक खोलता है और पहली वर्कशीट तथा सेल A1 को प्राप्त करता है।

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Access cell A1 where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");
```

इस तरह वर्कबुक बनाकर आपको एक साफ़ प्रारंभ मिलता है, जिससे यह उदाहरण किसी भी मशीन पर बिना मौजूदा फ़ाइल के काम करता है।

---

## चरण 2: WRAPCOLS फ़ंक्शन लागू करें – एक excel wrapcols example

`WRAPCOLS` एक‑आयामी एरे और कॉलम गिनती लेता है, फिर एक रेंज लौटाता है जो पहले पंक्तियों को भरता है। यह **reshape array in excel** का मूल है।

```java
        // Step 2: Set the WRAPCOLS formula
        // {1,2,3,4,5,6} is the source 1‑D array
        // 2 tells WRAPCOLS to create 2 columns per row
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");
```

यह क्यों काम करता है:

* लिटरल एरे `{1,2,3,4,5,6}` छह संख्याएँ प्रदान करता है।  
* `WRAPCOLS(..., 2)` Excel को बताता है कि मानों को 2 कॉलम में लपेटे, और स्वचालित रूप से पर्याप्त पंक्तियाँ (इस मामले में 3) बनाता है ताकि सभी आइटम फिट हो सकें।  
* परिणामी रेंज सेल **A1:B3** को कवर करती है:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

---

## चरण 3: गणना को मजबूर करें ताकि वर्कबुक फ़ॉर्मूला को प्रतिबिंबित करे

Aspose.Cells फ़ॉर्मूले को स्वचालित रूप से मूल्यांकन नहीं करता जब आप उन्हें सेट करते हैं। आपको परिणाम को वास्तविक बनाने के लिए `calculateFormula()` को कॉल करना होगा।

```java
        // Step 3: Recalculate all formulas in the workbook
        workbook.calculateFormula();
```

इस मेथड को कॉल करने से यह सुनिश्चित होता है कि `WRAPCOLS` द्वारा उत्पन्न एरे सेल्स में लिखा जाए, जिससे आप तुरंत मान पढ़ सकें।

---

## चरण 4: पुनः आकारित एरे से एक मान प्राप्त करें

यह सिद्ध करने के लिए कि फ़ॉर्मूला काम किया, लक्ष्य सेल की स्ट्रिंग प्रतिनिधित्व पढ़ें। क्योंकि `WRAPCOLS` एक एरे लौटाता है, Excel उस सेल में **पहला तत्व** (मान `1`) दिखाता है जहाँ फ़ॉर्मूला स्थित है।

```java
        // Step 4: Print the first element of the array (cell A1)
        System.out.println("First element: " + targetCell.getStringValue());
```

**अपेक्षित कंसोल आउटपुट**

```
First element: 1
```

यदि आप Excel में वर्कशीट की जाँच करते हैं, तो आप देखेंगे कि पूरा 3 × 2 ब्लॉक पहले वर्णित अनुसार भर गया है।

---

## चरण 5: वर्कबुक को फ़ाइल में सहेजें – how to save workbook to file

वर्कबुक को स्थायी बनाना आपको बाद में Excel में खोलने या सहयोगियों के साथ साझा करने की अनुमति देता है। पूर्ण पथ के साथ `save` मेथड का उपयोग करें।

```java
        // Step 5: Save the workbook to disk
        String outputPath = "WrapFunctions.xlsx"; // adjust directory as needed
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

प्रोग्राम चलाने से कार्य निर्देशिका में `WrapFunctions.xlsx` बनता है। फ़ाइल खोलने पर सेल A1:B3 में पुनः आकारित एरे दिखता है, जिससे यह पुष्टि होती है कि **save workbook to file** सफल रहा।

---

## पूर्ण, चलाने योग्य उदाहरण

सभी भागों को जोड़ते हुए, यहाँ पूरा प्रोग्राम है जिसे आप IDE में कॉपी‑पेस्ट करके चला सकते हैं:

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cell targetCell = worksheet.getCells().get("A1");

        // Apply WRAPCOLS to reshape a 1‑D array into a 3‑row × 2‑col range
        targetCell.setFormula("=WRAPCOLS({1,2,3,4,5,6}, 2)");

        // Force formula evaluation
        workbook.calculateFormula();

        // Output the first element of the resulting array
        System.out.println("First element: " + targetCell.getStringValue());

        // Save the workbook to a file
        String outputPath = "WrapFunctions.xlsx";
        workbook.save(outputPath);
        System.out.println("Workbook saved to " + outputPath);
    }
}
```

**परिणाम सत्यापन**

1. कंसोल `First element: 1` प्रिंट करता है।  
2. उत्पन्न `WrapFunctions.xlsx` में यह है:

| A | B |
|---|---|
| 1 | 2 |
| 3 | 4 |
| 5 | 6 |

यदि आपको एरे को कहीं और संदर्भित करने की आवश्यकता है, तो आप उदाहरण के तौर पर `worksheet.getCells().get("B2").getIntValue()` का उपयोग करके किसी भी भरे हुए सेल को पढ़ सकते हैं।

---

## सामान्य प्रश्न और किनारे के मामले

| Question | Answer |
|----------|--------|
| *क्या WRAPCOLS गैर‑संख्यात्मक एरे को संभाल सकता है?* | हाँ। आप कर्ली ब्रेसेस के अंदर स्ट्रिंग, तिथि, या लॉजिकल मान पास कर सकते हैं, और Excel उन्हें उसी अनुसार लपेट देगा। |
| *यदि मुझे Excel की प्रदर्शित सीमा से अधिक पंक्तियों की आवश्यकता हो तो?* | WRAPCOLS स्रोत एरे समाप्त होने तक अतिरिक्त पंक्तियों में फैलता रहेगा। सुनिश्चित करें कि वर्कशीट में पर्याप्त पंक्तियाँ हों (डिफ़ॉल्ट सीमा 1,048,576 है)। |
| *कॉलम की संख्या कैसे बदलें?* | `WRAPCOLS` के दूसरे तर्क को बदलें। तीन कॉलम के लिए `=WRAPCOLS({1,2,3,4,5,6}, 3)` उपयोग करें, जो 2 × 3 ब्लॉक बनाता है। |
| *क्या परिणाम को किसी अलग प्रारंभिक सेल में लिखना संभव है?* | हाँ। फ़ॉर्मूला को किसी भी सेल (जैसे `C5`) पर सेट करें और लपेटी हुई रेंज उस सेल के सापेक्ष विस्तारित होगी। |
| *क्या प्रत्येक बार फ़ॉर्मूला बदलने पर `calculateFormula` को कॉल करना आवश्यक है?* | जब भी आप प्रोग्रामेटिक रूप से फ़ॉर्मूला बदलते हैं, `calculateFormula` या `calculateFormula(true)` को कॉल करके निर्भर सेल्स को रिफ्रेश करें। |

---

## निष्कर्ष

इस ट्यूटोरियल ने Java में **how to use wrapcols** को **reshape array in excel** करने का प्रदर्शन किया, एक स्पष्ट **excel wrapcols example** प्रदान किया, और **save workbook to file** करने का सही तरीका दिखाया। अब आपके पास **create excel workbook java** प्रोजेक्ट्स के लिए एक ठोस आधार है जिन्हें डायनामिक एरे ट्रांसफ़ॉर्मेशन की आवश्यकता है।

अगले चरण में, **using other array functions** (`TRANSPOSE`, `SEQUENCE`) या Aspose.Cells की streaming API के साथ **writing large data sets** जैसे संबंधित विषयों का अन्वेषण करें। विभिन्न स्रोत एरे, कॉलम गिनती, और प्रारंभिक स्थितियों के साथ प्रयोग करें ताकि आप इस पैटर्न को अपनी रिपोर्टिंग या डेटा‑प्रोसेसिंग वर्कफ़्लो में अनुकूलित कर सकें। कोडिंग का आनंद लें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells for Java का उपयोग करके Excel फ़ाइल कैसे खोलें: एक पूर्ण गाइड](/cells/english/java/getting-started/open-excel-aspose-cells-java-guide/)
- [Aspose.Cells for Java का उपयोग करके Excel वर्कबुक कैसे बनाएं और मर्ज करें | पूर्ण गाइड](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)
- [Aspose.Cells for Java (वर्कबुक ऑपरेशन्स) का उपयोग करके Excel शीट्स को इमेजेज़ के रूप में रेंडर कैसे करें](/cells/english/java/workbook-operations/render-excel-sheets-images-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}