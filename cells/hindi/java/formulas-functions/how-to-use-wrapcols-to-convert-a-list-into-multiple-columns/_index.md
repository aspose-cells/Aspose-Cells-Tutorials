---
category: general
date: 2026-10-16
description: Java में wrapcols का उपयोग कैसे करें और फ़ॉर्मूला के साथ सूची को जल्दी
  से कॉलम में बदलें – मल्टी‑कॉलम लेआउट के लिए फ़ॉर्मूला सेट करना सीखें.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert list to columns
- how to set formula
- create multi‑column layout
language: hi
lastmod: 2026-10-16
og_description: Java में सूची को कॉलम में बदलने के लिए wrapcols का उपयोग कैसे करें।
  फ़ॉर्मूला सेट करने और Excel में मल्टी‑कॉलम लेआउट बनाने के लिए इस पूर्ण गाइड का पालन
  करें।
og_image_alt: Screenshot of an Excel sheet showing a wrapped list in three columns
og_title: wrapcols का उपयोग कैसे करें – जावा डेवलपर्स के लिए चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  headline: How to use wrapcols to convert a list into multiple columns in Java
  type: TechArticle
- description: how to use wrapcols in Java and quickly convert list to columns with
    a formula – learn how to set formula for a multi‑column layout
  name: How to use wrapcols to convert a list into multiple columns in Java
  steps:
  - name: What happens behind the scenes
    text: 'When the workbook is saved, Aspose.Cells evaluates the formula and writes
      the expanded values to the file. If you open `WrapColsResult.xlsx` in Excel,
      you’ll see:'
  - name: Changing the number of columns
    text: If you need a different column count, modify the second argument of `WRAPCOLS`.
      For example, `=WRAPCOLS(A2:A100,5)` creates five columns. The function automatically
      adjusts the row count to accommodate the new layout.
  - name: Handling a non‑even list size
    text: When the source range length isn’t divisible by the column count, `WRAPCOLS`
      pads the final column with blanks. This behavior is useful for creating balanced
      tables without manual trimming.
  - name: Using a dynamic range
    text: You can replace `A2:A100` with a named range or a formula that calculates
      the last row, such as `A2:INDEX(A:A, COUNTA(A:A))`. This makes the solution
      robust when the list length changes.
  - name: Avoiding circular references
    text: Place the formula in a cell that isn’t part of the source range. If you
      accidentally set the formula inside `A2:A100`, Excel will report a circular
      reference error. Always write the formula to a separate cell (commonly `A1`).
  type: HowTo
tags:
- wrapcols
- Aspose.Cells
- Java
- Excel automation
title: Java में wrapcols का उपयोग करके सूची को कई कॉलम में कैसे बदलें
url: /hi/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में wrapcols का उपयोग करके सूची को कई कॉलम में बदलें

यदि आपको Java प्रोजेक्ट में **how to use wrapcols** की आवश्यकता है, तो यह गाइड आपको सटीक चरण दिखाता है। आप सीखेंगे कि फ़ॉर्मूला कैसे सेट करें, सूची को कॉलम में कैसे बदलें, और मैन्युअल कॉपी‑पेस्ट के बिना मल्टी‑कॉलम लेआउट कैसे बनाएं।

यह ट्यूटोरियल प्रोजेक्ट सेटअप से लेकर एज‑केस हैंडलिंग तक सब कुछ कवर करता है, ताकि आप समाधान को किसी भी स्प्रेडशीट पर लागू कर सकें जिसमें सिंगल‑कॉलम सूची हो। Aspose.Cells for Java के अलावा कोई अतिरिक्त टूल आवश्यक नहीं है।

## पूर्वापेक्षाएँ

* Java 17 या उससे नया स्थापित हो  
* निर्भरता प्रबंधन के लिए Maven 3.8+ (या Gradle)  
* **Aspose.Cells for Java** का लाइसेंस – परीक्षण के लिए मुफ्त इवैल्यूएशन काम करता है  
* Excel फ़ॉर्मूलों की बुनियादी समझ  

ये चीज़ें सुनिश्चित करती हैं कि कोड बिना कंपाइलेशन त्रुटियों के चले।

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

`pom.xml` में निम्नलिखित Maven डिपेंडेंसी जोड़ें। यदि आप Gradle उपयोग करते हैं, तो वही कोऑर्डिनेट्स लागू होते हैं।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

यह लाइब्रेरी `Cell` और `Worksheet` क्लासेस प्रदान करती है, जो बाद में जब आप रेंज के लिए **how to set formula** करेंगे, उपयोग होती हैं।

## चरण 2: एक वर्कबुक बनाएं और स्रोत सूची को भरें

पहला कार्य एक वर्कबुक बनाना है जिसमें एक वर्टिकल सूची (A2:A100) हो। यह सूची वह डेटा दर्शाती है जिसे आप **convert list to columns** करना चाहते हैं।

```java
import com.aspose.cells.*;

public class WrapColsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Populate A2:A100 with sample data
        for (int i = 0; i < 99; i++) {
            cells.get("A" + (i + 2)).setValue("Item " + (i + 1));
        }

        // Apply WRAPCOLS formula (see next step)
        applyWrapCols(cells);

        // Save the result
        workbook.save("WrapColsResult.xlsx");
    }
```

लूप पहले कॉलम को 99 आइटम्स से भरता है, जिससे आपको काम करने के लिए एक वास्तविक सूची मिलती है। आप जनरेट किए गए मानों को डेटाबेस या किसी अन्य स्रोत से पढ़े गए डेटा से बदल सकते हैं।

## चरण 3: फ़ॉर्मूला सेट करने के लिए wrapcols का उपयोग कैसे करें

अब आप ट्यूटोरियल का मुख्य भाग देखेंगे: `WRAPCOLS` फ़ंक्शन का उपयोग करके **create multi‑column layout**। यह फ़ंक्शन दो आर्ग्युमेंट लेता है – स्रोत रेंज और इच्छित कॉलमों की संख्या।

```java
    private static void applyWrapCols(Cells cells) {
        // Step 1: Get the cell where the formula will be placed (A1)
        Cell target = cells.get("A1");

        // Step 2: Apply the WRAPCOLS function to wrap A2:A100 into 3 columns
        target.setFormula("=WRAPCOLS(A2:A100,3)");
    }
}
```

*Why this works* – `WRAPCOLS` वर्टिकल रेंज `A2:A100` को पढ़ता है, फिर मानों को पंक्ति‑दर‑पंक्ति तीन कॉलम (B, C, और D) में वितरित करता है। परिणाम उस सेल से शुरू होता है जिसमें फ़ॉर्मूला है (`A1`)। क्योंकि फ़ॉर्मूला एक एरे लौटाता है, Aspose.Cells स्वचालित रूप से परिणाम को आवश्यक सेल्स में विस्तारित कर देता है।

### पर्दे के पीछे क्या होता है

जब वर्कबुक सहेजी जाती है, तो Aspose.Cells फ़ॉर्मूला का मूल्यांकन करता है और विस्तारित मानों को फ़ाइल में लिखता है। यदि आप Excel में `WrapColsResult.xlsx` खोलते हैं, तो आप देखेंगे:

| A1 | B1 | C1 | D1 |
|----|----|----|----|
| Item 1 | Item 34 | Item 67 |
| Item 2 | Item 35 | Item 68 |
| … | … | … |

यह लेआउट **create multi‑column layout** पैटर्न को दर्शाता है, जो रिपोर्ट, डैशबोर्ड या प्रिंटेबल फ़ॉर्म के लिए उपयोगी है।

## चरण 4: प्रोग्रामेटिक रूप से आउटपुट की पुष्टि करें (वैकल्पिक)

यदि आप यह पुष्टि करना चाहते हैं कि फ़ॉर्मूला ने अपेक्षित मैट्रिक्स उत्पन्न किया है बिना Excel खोले, तो आप गणना के बाद मानों को पुनः पढ़ सकते हैं।

```java
        // Force calculation to ensure the array result is materialized
        workbook.calculateFormula();

        // Print the first three rows of the wrapped layout
        for (int row = 0; row < 3; row++) {
            StringBuilder line = new StringBuilder();
            for (int col = 0; col < 4; col++) { // A‑D columns
                line.append(cells.get(row, col).getStringValue()).append("\t");
            }
            System.out.println(line.toString().trim());
        }
```

प्रोग्राम चलाने पर कुछ इस तरह प्रिंट होगा:

```
Item 1    Item 34    Item 67    Item 100
Item 2    Item 35    Item 68    Item 101
Item 3    Item 36    Item 69    Item 102
```

यह पुष्टि करता है कि **how to use wrapcols** इच्छानुसार काम करता है और **convert list to columns** ऑपरेशन सफल रहा।

## चरण 5: सामान्य विविधताएँ और एज केस

### कॉलमों की संख्या बदलना

यदि आपको अलग कॉलम संख्या चाहिए, तो `WRAPCOLS` के दूसरे आर्ग्युमेंट को बदलें। उदाहरण के लिए, `=WRAPCOLS(A2:A100,5)` पाँच कॉलम बनाता है। फ़ंक्शन स्वचालित रूप से नई लेआउट को समायोजित करने के लिए पंक्तियों की संख्या को एडजस्ट कर देता है।

### असमान सूची आकार को संभालना

जब स्रोत रेंज की लंबाई कॉलम संख्या से विभाज्य नहीं होती, तो `WRAPCOLS` अंतिम कॉलम को खाली स्थानों से पैड करता है। यह व्यवहार मैन्युअल ट्रिमिंग के बिना संतुलित टेबल बनाने में उपयोगी है।

### डायनेमिक रेंज का उपयोग

आप `A2:A100` को एक नेम्ड रेंज या ऐसी फ़ॉर्मूला से बदल सकते हैं जो अंतिम पंक्ति की गणना करे, जैसे `A2:INDEX(A:A, COUNTA(A:A))`। इससे सूची की लंबाई बदलने पर समाधान मजबूत बनता है।

### सर्कुलर रेफ़रेंस से बचना

फ़ॉर्मूला को ऐसे सेल में रखें जो स्रोत रेंज का हिस्सा न हो। यदि आप गलती से फ़ॉर्मूला को `A2:A100` के भीतर सेट कर देते हैं, तो Excel सर्कुलर रेफ़रेंस त्रुटि रिपोर्ट करेगा। हमेशा फ़ॉर्मूला को एक अलग सेल में लिखें (आमतौर पर `A1`)।

## चरण 6: प्रोडक्शन उपयोग के लिए टिप्स

* **Cache the workbook** – यदि आप लूप में कई रिपोर्ट बनाते हैं, तो एक ही `Workbook` इंस्टेंस को पुन: उपयोग करें और मेमोरी ओवरहेड कम करने के लिए पिछले डेटा को साफ़ करें।  
* **Set calculation mode** – जब आपको तुरंत मूल्यांकन के बिना केवल कच्चा फ़ॉर्मूला चाहिए, तो `workbook.getSettings().setCalculateFormulaOnOpen(false)` का उपयोग करें।  
* **Internationalization** – फ़ंक्शन नाम `WRAPCOLS` लोकेल‑स्वतंत्र है, लेकिन अन्य फ़ॉर्मूलों में दशमलव विभाजक अलग हो सकते हैं। असंगतियों से बचने के लिए फ़ॉर्मूले अंग्रेज़ी में रखें।  
* **Performance** – 10 000 पंक्तियों से अधिक वाली सूचियों के लिए, फ़ॉर्मूला को एक बार मूल्यांकन करें और फिर एरे मानों को सीधे पढ़ें ताकि दोहराए गए गणनाओं से बचा जा सके।

## निष्कर्ष

अब आप जानते हैं कि Java में **how to use wrapcols** करके **convert list to columns** और **create multi‑column layout** एक ही फ़ॉर्मूला से कैसे किया जाता है। पूर्ण, चलाने योग्य उदाहरण पूरे वर्कफ़्लो को दर्शाता है: लाइब्रेरी जोड़ना, डेटा भरना, फ़ॉर्मूला लागू करना, और परिणाम की पुष्टि करना।  

अब आप कर सकते हैं:

* रिपोर्टिंग शैली के अनुसार कॉलम संख्या समायोजित करें  
* `WRAPCOLS` को `SORT` या `FILTER` जैसे अन्य फ़ंक्शनों के साथ मिलाकर उन्नत डेटा शेपिंग करें  
* Aspose.Cells के बिल्ट‑इन कन्वर्टर्स का उपयोग करके वर्कबुक को PDF, CSV, या HTML में एक्सपोर्ट करें  

इन विविधताओं के साथ प्रयोग करें ताकि आपके Excel ऑटोमेशन कार्य सुगम हो सकें। यदि आपको कोई समस्या आती है, तो ऊपर के एज‑केस हैंडलिंग सेक्शन को देखें या अतिरिक्त फ़ॉर्मूला समर्थन के लिए Aspose.Cells दस्तावेज़ देखें। कोडिंग का आनंद लें!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [Java में WRAPCOLS का उपयोग कैसे करें – Excel एरे फ़ॉर्मूलों के लिए पूर्ण गाइड](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [Java में WRAPCOLS का उपयोग कैसे करें – पूर्ण Excel WRAPCOLS उदाहरण](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)
- [Java के साथ Excel में Reduce का उपयोग – लैम्ब्डा फ़ॉर्मूला गाइड](/cells/english/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}