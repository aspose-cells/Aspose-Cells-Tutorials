---
category: general
date: 2026-08-20
description: जावा का उपयोग करके एक्सेल को TXT में निर्यात करना सीखें, दशमलव स्थानों
  को सीमित करते हुए, महत्वपूर्ण अंकों को बनाए रखते हुए, और वर्कबुक को TXT के रूप में
  सहेजते हुए।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: hi
lastmod: 2026-08-20
og_description: Aspose.Cells के साथ Excel को TXT में निर्यात करें। यह गाइड दिखाता
  है कि दशमलव स्थानों को कैसे सीमित करें, महत्वपूर्ण अंकों को कैसे रखें, और जावा में
  वर्कबुक को TXT के रूप में कैसे सहेजें।
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: जावा में एक्सेल को TXT में निर्यात करें – दशमलव स्थान और महत्वपूर्ण अंकों
  को नियंत्रित करें
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Aspose.Cells के साथ Excel को TXT में निर्यात कैसे करें और दशमलव सटीकता को नियंत्रित
  करें
url: /hi/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ Excel को TXT में निर्यात करने और दशमलव सटीकता को नियंत्रित करने का तरीका

यदि आपको **Excel को TXT में निर्यात** करना है और सुनिश्चित करना है कि आउटपुट एक विशिष्ट दशमलव स्थानों की संख्या का सम्मान करे, तो यह गाइड एक पूर्ण समाधान प्रदान करता है। आप देखेंगे कि कैसे दशमलव स्थानों को सीमित किया जाए, महत्वपूर्ण अंकों को रखा जाए, और Aspose.Cells लाइब्रेरी for Java का उपयोग करके **वर्कबुक को TXT के रूप में सहेजा** जाए।

ट्यूटोरियल वर्कबुक बनाने, उच्च‑सटीकता मान डालने, TXT सहेजने विकल्प कॉन्फ़िगर करने, और फ़ाइल को डिस्क पर लिखने की प्रक्रिया को चरण‑दर‑चरण दिखाता है। अंत तक आप एक टेक्स्ट फ़ाइल जेनरेट कर सकते हैं जिसमें बिल्कुल वही सटीकता हो जो आप चाहते हैं, बिना मैन्युअल पोस्ट‑प्रोसेसिंग के।

## आपको क्या चाहिए

- Java 17 (या कोई भी समर्थित JDK)
- Aspose.Cells for Java 23.10 या नया
- एक IDE या बिल्ड टूल (Maven/Gradle) जो निर्भरताओं को प्रबंधित करे
- आउटपुट डायरेक्टरी में लिखने की अनुमति

## चरण 1: एक वर्कबुक बनाएं और पहली वर्कशीट तक पहुंचें

एक वर्कबुक बनाना वह पहला कदम है जब आप **Excel को TXT में निर्यात** करना चाहते हैं। `Workbook` क्लास पूरी Excel फ़ाइल का प्रतिनिधित्व करती है, और `Worksheet` आपको सेल्स तक पहुंच देती है।

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Why this matters*: वर्कबुक ऑब्जेक्ट सभी डेटा, शैलियों और मेटाडेटा को रखता है। एक नई वर्कबुक से शुरू करने से यह सुनिश्चित होता है कि कोई छिपा हुआ फॉर्मेटिंग टेक्स्ट निर्यात में बाधा न बनाये।

## चरण 2: एक संख्यात्मक मान जोड़ें और दशमलव स्थानों को सीमित करें

एक ऐसा नंबर डालें जिसमें कई दशमलव स्थान हों ताकि आप दिखा सकें कि निर्यात के दौरान **दशमलव स्थानों को सीमित** कैसे किया जाता है।

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Why this matters*: Excel पूरी सटीकता को स्टोर करता है, लेकिन जब आप बाद में निर्यात करते हैं, तो आप मान को ट्रंकेट या राउंड करना चाह सकते हैं। `limit decimal places` सेटिंग इसे स्वचालित रूप से संभाल लेगी।

## चरण 3: महत्वपूर्ण अंकों को रखने के लिए TXT सहेजने विकल्प कॉन्फ़िगर करें

Aspose.Cells `TxtSaveOptions` प्रदान करता है। `significantDigits` सेट करने से एक्सपोर्टर केवल आवश्यक संख्या के अर्थपूर्ण अंकों को रखता है, अग्रणी शून्यों को अनदेखा करता है।

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Why this matters*: **keep significant digits** विकल्प सुनिश्चित करता है कि आउटपुट फ़ाइल में पूर्वानुमेय मात्रा में सटीकता हो, जो उन डाउनस्ट्रीम सिस्टम्स के लिए आवश्यक है जो निश्चित‑चौड़ाई वाले संख्यात्मक फ़ॉर्मेट की अपेक्षा करते हैं।

## चरण 4: वर्कबुक को TXT के रूप में सहेजें

अंत में, वर्कबुक को एक टेक्स्ट फ़ाइल में लिखें। `save` मेथड आपके द्वारा कॉन्फ़िगर किए गए विकल्पों का सम्मान करता है, इसलिए परिणामी फ़ाइल सीमित दशमलव प्रतिनिधित्व रखेगी।

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Why this matters*: तैयार `TxtSaveOptions` के साथ **save workbook as txt** का उपयोग यह गारंटी देता है कि निर्यातित फ़ाइल पिछले चरण में सेट किए गए सटीकता प्रतिबंधों से मेल खाती है।

### अपेक्षित सामग्री `SignificantDigits.txt` की

```
0.00012346
```

यह मान राउंडिंग के बाद पाँच महत्वपूर्ण अंक (`12346`) दिखाता है, और अग्रणी शून्य TXT फ़ॉर्मेट के अनुसार संरक्षित रहते हैं।

## विविधताएँ और किनारे के मामले

| परिदृश्य | समायोजन |
|----------|------------|
| **विभिन्न संख्या के महत्वपूर्ण अंक** | Call `txtOptions.setSignificantDigits(n)` where `n` is 1‑15. |
| **पूरे शीट के बजाय एक रेंज निर्यात करना** | Use `txtOptions.setExportRange("A1:B10")` before saving. |
| **कॉलम विभाजकों को संरक्षित करना** | Set `txtOptions.setSeparator('\t')` for tab‑delimited output. |
| **बड़ी वर्कशीट्स** | Increase `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` to avoid `OutOfMemoryError`. |

## सामान्य गड़बड़ियाँ और प्रो टिप्स

- **महत्वपूर्ण अंकों को दशमलव स्थानों से भ्रमित न करें**। अग्रणी शून्य महत्वपूर्ण नहीं माने जाते; अर्थपूर्ण सटीकता के लिए `setSignificantDigits` उपयोग करें और यदि आपको दशमलव के बाद निश्चित संख्या के अंक चाहिए तो `setDecimalPlaces` उपयोग करें।
- **IDE से चलाते समय हमेशा एक पूर्ण (absolute) आउटपुट पाथ निर्दिष्ट करें** ताकि अनुमति त्रुटियों से बचा जा सके।
- **जनरेट की गई फ़ाइल को सत्यापित करें** एक सरल `java.nio.file.Files.readAllLines(Paths.get(outputPath))` कॉल से यह सुनिश्चित करने के लिए कि सामग्री अपेक्षाओं के अनुरूप है, इससे पहले कि आप इसे डाउनस्ट्रीम प्रोसेस में फीड करें।

## संदर्भ के लिए पूर्ण स्रोत कोड

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

प्रोग्राम चलाने पर `SignificantDigits.txt` बनता है जिसमें एकल पंक्ति `0.00012346` होती है, जो दर्शाता है कि **export excel to txt** प्रक्रिया दोनों **limit decimal places** और **keep significant digits** आवश्यकताओं का सम्मान करती है।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells for Java का उपयोग करके **Excel को TXT में निर्यात** कैसे किया जाए जबकि संख्यात्मक सटीकता को नियंत्रित किया जाए। `TxtSaveOptions` को कॉन्फ़िगर करके आप **दशमलव स्थानों को सीमित**, **महत्वपूर्ण अंक रख**, और अतिरिक्त पोस्ट‑प्रोसेसिंग के बिना विश्वसनीय रूप से **वर्कबुक को txt के रूप में सहेज** सकते हैं।

अगला, आप खोज सकते हैं:

- एकाधिक शीट्स को अलग-अलग TXT फ़ाइलों में निर्यात करना (`save workbook as txt` प्रति शीट)
- `setSeparator` का उपयोग करके CSV‑संगत आउटपुट बनाना
- बड़े डेटा सेटों के लिए बैच रूपांतरण को स्वचालित करना

विभिन्न अंक गणना और विभाजकों के साथ प्रयोग करने में संकोच न करें ताकि आपके प्रोजेक्ट की सटीक आवश्यकताओं के अनुरूप हो सके। कोडिंग का आनंद लें!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Aspose.Cells Java का उपयोग करके Excel को HTML में बनाना और निर्यात करना | वर्कबुक ऑपरेशन्स गाइड](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Excel को टेक्स्ट के रूप में सहेजें – Excel को TXT में निर्यात करने के लिए पूर्ण C# गाइड](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Aspose.Cells for Java का उपयोग करके Excel वर्कबुक को इमेज के रूप में निर्यात करना: एक चरण-दर-चरण गाइड](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}