---
category: general
date: 2026-08-17
description: Excel को TXT में निर्यात करें और महत्वपूर्ण अंकों को सीमित रखें – अंक
  सेट करना और Java में Excel को टेक्स्ट में बदलना सीखें, एक पूर्ण Aspose.Cells उदाहरण
  के साथ।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: hi
lastmod: 2026-08-17
og_description: महत्वपूर्ण अंकों की सीमा निर्धारित करते हुए Excel को TXT में निर्यात
  करें। यह ट्यूटोरियल दिखाता है कि कैसे अंकों को सेट करें और Aspose.Cells for Java
  का उपयोग करके Excel को टेक्स्ट में बदलें।
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: सीमित महत्वपूर्ण अंकों के साथ एक्सेल को TXT में निर्यात करें – जावा गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: जावा का उपयोग करके सीमित महत्वपूर्ण अंकों के साथ एक्सेल को TXT में निर्यात
  कैसे करें
url: /hi/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा का उपयोग करके सीमित महत्वपूर्ण अंकों के साथ Excel को TXT में निर्यात करें

यदि आपको **Excel को TXT में निर्यात** करने की आवश्यकता है और साथ ही महत्वपूर्ण अंकों की संख्या को नियंत्रित करना है, तो यह गाइड एक तैयार‑से‑चलाने वाला समाधान प्रदान करता है। आप देखेंगे कि अंकों को कैसे सेट करें, Excel को टेक्स्ट में कैसे बदलें, और एक ही कॉन्फ़िगरेशन परिवर्तन से आउटपुट को साफ़ कैसे रखें।

यह उदाहरण Aspose.Cells for Java 25.10 का उपयोग करता है, जिसमें `setSignificantDigits` विकल्प पेश किया गया है। ट्यूटोरियल के अंत तक आप एक TXT फ़ाइल बना सकते हैं जिसमें केवल वही अंक हों जो आप चाहते हैं, अतिरिक्त राउंडिंग कोड के बिना।

## आप क्या हासिल करेंगे

- एक वर्कबुक को प्रोग्रामेटिकली बनाएं।
- एक सेल में संख्यात्मक मान डालें।
- `TXT` सहेजने के विकल्प को महत्वपूर्ण अंकों को सीमित करने के लिए कॉन्फ़िगर करें।
- वर्कबुक को प्लेन‑टेक्स्ट फ़ाइल के रूप में सहेजें।
- `significantDigits` सेटिंग कैसे काम करती है और इसे अन्य परिदृश्यों के लिए कैसे अनुकूलित करें, समझें।

### पूर्वापेक्षाएँ

- Java 17 या बाद का संस्करण (कोड Java 8 के साथ भी कम्पाइल होता है)।
- Aspose.Cells for Java 25.10 या नया संस्करण। JAR को [Aspose वेबसाइट](https://products.aspose.com/cells/java) से डाउनलोड करें और इसे अपने प्रोजेक्ट की क्लासपाथ में जोड़ें।
- एक IDE या साधारण टेक्स्ट एडिटर और कमांड‑लाइन बिल्ड टूल (Maven/Gradle)।

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose.Cells इम्पोर्ट करें

एक नया Java प्रोजेक्ट बनाएं और Aspose.Cells JAR को बिल्ड पाथ में जोड़ें। यदि आप Maven का उपयोग करते हैं, तो `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **प्रो टिप:** नवीनतम Java रनटाइम के लिए `jdk17` क्लासिफायर का उपयोग करें; यह संगतता चेतावनियों के जोखिम को कम करता है।

## चरण 2: एक वर्कबुक बनाएं और मान लिखें

वर्कबुक मेमोरी में एक Excel फ़ाइल का प्रतिनिधित्व करता है। आप `putValue` मेथड का उपयोग करके किसी भी सेल में डेटा जोड़ सकते हैं।

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

`123.456789` संख्या हमारे TXT निर्यात का स्रोत होगी। डिफ़ॉल्ट रूप से Aspose.Cells सभी दशमलव स्थान लिखेगा, जिससे अक्सर शोरयुक्त टेक्स्ट फ़ाइलें बनती हैं।

## चरण 3: महत्वपूर्ण अंकों को सीमित करने के लिए TXT सहेजने के विकल्प कॉन्फ़िगर करें

Aspose.Cells `TxtSaveOptions` प्रदान करता है जो प्लेन‑टेक्स्ट आउटपुट पर सूक्ष्म नियंत्रण देता है। `setSignificantDigits` मेथड एक्सपोर्टर को बताता है कि कुल मिलाकर कितने अंक रखने हैं, न कि केवल दशमलव बिंदु के बाद।

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

जब `significantDigits` को `4` सेट किया जाता है, तो एक्सपोर्टर मान `123.456789` को `123.5` में राउंड करता है। यह व्यवहार महत्वपूर्ण अंकों की गणितीय परिभाषा से मेल खाता है: पहले चार गैर‑शून्य अंक रखे जाते हैं।

### सेटिंग “limit decimals” से कैसे अलग है

- **limit decimals** (`setDecimalPlaces`) दशमलव बिंदु के *बाद* के अंकों को ट्रिम करता है, चाहे पूर्णांक भाग कुछ भी हो।
- **significant digits** (`setSignificantDigits`) पहले गैर‑शून्य अंक से अंकों की गिनती करता है, जो तब उपयोगी होता है जब संख्याओं का परिमाण अलग‑अलग हो।

यदि आपको इसके बजाय निश्चित संख्या में दशमलव स्थान चाहिए, तो ऊपर की पंक्ति को इस प्रकार बदलें:

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## चरण 4: वर्कबुक को TXT फ़ाइल के रूप में सहेजें

अब कॉन्फ़िगर किए गए विकल्पों का उपयोग करके वर्कबुक को डिस्क पर लिखें।

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

प्रोग्राम चलाने पर `significant_digits.txt` कार्य निर्देशिका में बनता है। फ़ाइल में एक ही पंक्ति होती है:

```
123.5
```

### अपेक्षित आउटपुट

| सेल | मूल मान | निर्यातित (4 महत्वपूर्ण अंक) |
|------|----------|----------------------------|
| A1   | 123.456789 | 123.5 |

यदि आप `setSignificantDigits(4)` को `6` बदलते हैं, तो आउटपुट `123.457` हो जाता है। विभिन्न मानों के साथ प्रयोग करें ताकि देखें कि राउंडिंग कैसे अनुकूलित होती है।

## चरण 5: सामान्य विविधताएँ और किनारे के मामलों

### पूरी रेंज निर्यात करना

यदि आप एक से अधिक सेल निर्यात करना चाहते हैं, तो सहेजने से पहले बस रेंज को भरें:

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

एक ही `significantDigits` सेटिंग हर संख्यात्मक सेल पर लागू होती है, जिससे फ़ाइल में सुसंगत परिशुद्धता सुनिश्चित होती है।

### लोकेल‑विशिष्ट दशमलव विभाजकों को संभालना

Aspose.Cells टेक्स्ट लिखते समय सिस्टम लोकेल का सम्मान करता है। दशमलव विभाजक के रूप में डॉट (`.`) को मजबूर करने के लिए, `TxtSaveOptions` की कल्चर सेट करें:

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

यह तब उपयोगी है जब लक्ष्य एप्लिकेशन एक विशिष्ट फ़ॉर्मेट की अपेक्षा करता है, जैसे CSV पार्सर जो केवल `.` स्वीकार करते हैं।

### मौजूदा फ़ाइलों को ओवरराइट करना

`save` मेथड डिफ़ॉल्ट रूप से लक्ष्य फ़ाइल को ओवरराइट करता है। यदि आप आकस्मिक डेटा हानि से बचना चाहते हैं, तो पहले फ़ाइल की मौजूदगी जांचें:

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### बड़े वर्कबुक और मेमोरी उपयोग

बहुत बड़े वर्कशीट निर्यात करते समय, आउटपुट को स्ट्रीम करने पर विचार करें:

```java
saveOptions.setEnableMemorySaving(true);
```

यह विकल्प पंक्तियों को क्रमिक रूप से लिखकर हीप उपयोग को कम करता है।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी, पेस्ट और तुरंत चला सकते हैं:

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

इस कोड को चलाने पर `significant_digits.txt` निम्नलिखित सामग्री (टैब‑सेपरेटेड कॉलम) के साथ बनता है:

```
123.5	0.001235	98770
```

प्रत्येक संख्या **4 महत्वपूर्ण अंकों** नियम का पालन करती है, जो दर्शाता है कि सेटिंग विभिन्न परिमाणों में काम करती है।

## निष्कर्ष

अब आप जानते हैं कि **Excel को TXT में निर्यात** कैसे करें जबकि महत्वपूर्ण अंकों की संख्या को नियंत्रित किया जाए। `TxtSaveOptions.setSignificantDigits` का उपयोग करके आप **अंकों को सेट करना**, **दशमलव को सीमित करना**, और **महत्वपूर्ण अंकों को सीमित करना** एक ही, रखरखाव योग्य कोड लाइन में कर सकते हैं। यह तरीका एकल सेल, पूरी रेंज, और बड़े वर्कबुक के लिए समान रूप से काम करता है।

### अगले कदम

- `TxtSaveOptions` की अन्य प्रॉपर्टीज़ जैसे `setDelimiter('\t')` को एक्सप्लोर करें ताकि कॉलम सेपरेटर को कस्टमाइज़ किया जा सके।
- यदि आपको प्लेन टेक्स्ट के बजाय कॉमा‑सेपरेटेड वैल्यू चाहिए, तो एक्सपोर्टर को `CsvSaveOptions` के साथ संयोजित करें।
- रूटीन को वेब सर्विस में इंटीग्रेट करें जो अपलोडेड Excel फ़ाइलें स्वीकार करे और तुरंत ट्रिम्ड TXT आउटपुट लौटाए।

विभिन्न अंक सीमाओं और लोकेल्स के साथ प्रयोग करने में संकोच न करें। यदि आपको ऐसा परिदृश्य मिलता है जहाँ बिल्ट‑इन विकल्प विशेष आवश्यकता को पूरा नहीं करते, तो आप हमेशा जनरेटेड TXT फ़ाइल को मानक Java I/O यूटिलिटीज़ से पोस्ट‑प्रोसेस कर सकते हैं।

कोडिंग का आनंद लें!

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दर्शाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करती हैं।

- [Aspose.Cells for Java का उपयोग करके Excel में टेक्स्ट को नंबर में बदलना](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Aspose.Cells Java का उपयोग करके Excel को HTML में बनाना और निर्यात करना | वर्कबुक ऑपरेशन्स गाइड](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Aspose.Cells for Java का उपयोग करके कस्टम Excel प्रॉपर्टीज़ को PDF में निर्यात करना](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}