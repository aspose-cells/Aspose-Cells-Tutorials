---
category: general
date: 2026-07-03
description: Java के java.time API का उपयोग करके लोकल के साथ तिथि पार्स करें। जापानी
  युग स्वरूप संभालना, लोकल तिथि रूपांतरण, और मजबूत Java तिथि पार्सिंग तकनीकों को सीखें।
draft: false
keywords:
- parse date with locale
- java date parsing
- japanese era format
- locale date conversion
- java time API
language: hi
og_description: java.time API का उपयोग करके जावा में लोकल के साथ तिथि पार्स करें।
  यह गाइड जापानी युग फ़ॉर्मेट हैंडलिंग, लोकल तिथि रूपांतरण, और विश्वसनीय तिथि पार्सिंग
  के लिए सर्वोत्तम प्रथाओं को दर्शाता है।
og_title: जावा में लोकेल के साथ तिथि पार्स करें – पूर्ण प्रोग्रामिंग ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  headline: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Parse date with locale using Java’s java.time API. Learn Japanese era
    format handling, locale date conversion, and robust java date parsing techniques.
  name: Parse Date with Locale in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Define the Era Date String
    text: First, store the Japanese era string exactly as you receive it (e.g., from
      a CSV file or UI).
  - name: Build a Locale‑Aware Formatter
    text: Java’s **java.time API** lets you tie a `DateTimeFormatter` to a specific
      chronology (calendar system) and `Locale`. For the Japanese era we use `JapaneseChronology`.
  - name: Parse and Convert to Gregorian `LocalDate`
    text: Now we actually parse the string and transform the result into a classic
      `LocalDate` that any Java library can consume.
  - name: What if the input uses a different era symbol?
    text: Japanese eras change roughly every few decades. The formatter automatically
      recognises `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), and `R` (Reiwa).
      If you receive an older era not covered by the default `JapaneseChronology`,
      you’ll get a `DateTimeParseException`. In that case, verify the s
  - name: How to support other non‑Gregorian calendars?
    text: 'The pattern is identical; you just swap the chronology and locale. For
      example, Thai Buddhist dates (`BuddhistChronology`) look like this:'
  - name: Can I parse without an era symbol (pure year‑month‑day)?
    text: Yes—simply omit `G` from the pattern and use the default `ISO_LOCAL_DATE`
      formatter. That’s the classic *java date parsing* route for Gregorian strings.
  - name: What about lenient parsing (e.g., missing leading zeros)?
    text: Switch `ResolverStyle.STRICT` to `ResolverStyle.LENIENT`. Be aware that
      lenient mode may silently roll over invalid dates (e.g., `R5/13/40` becomes
      `2024‑02‑09`). For production code, strict mode is usually safer.
  type: HowTo
tags:
- java
- date-time
- localization
title: जावा में लोकेल के साथ तिथि पार्स करें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/java/advanced-features/parse-date-with-locale-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में लोकेल के साथ तिथि पार्स करें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपको कभी जावा में **parse date with locale** करने की ज़रूरत पड़ी लेकिन यह नहीं पता था कि कौन सी क्लासेज़ इस्तेमाल करें? आप अकेले नहीं हैं—गैर‑ग्रेगोरियन कैलेंडर या क्षेत्रीय फ़ॉर्मेट से निपटना एक गुप्त भाषा को डिकोड करने जैसा लग सकता है। इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से दिखाएंगे: `R5/04/01` जैसी जापानी युग स्ट्रिंग को मानक ग्रेगोरियन `2023‑04‑01` `Date` ऑब्जेक्ट में बदलना। अंत तक आपके पास किसी भी लोकेल‑विशिष्ट तिथि फ़ॉर्मेट के लिए पुन: उपयोग योग्य पैटर्न होगा।

हम आवश्यक इम्पोर्ट्स से लेकर एज‑केस हैंडलिंग तक सब कुछ कवर करेंगे, और कुछ संबंधित अवधारणाओं को भी जोड़ेंगे—*java date parsing*, *japanese era format*, *locale date conversion*, और आधुनिक *java time API*—ताकि आप समाधान को अपने प्रोजेक्ट्स में अनुकूलित कर सकें। कोई बाहरी लाइब्रेरी नहीं, सिर्फ सादा जावा 8+.

---

## इस ट्यूटोरियल में क्या कवर किया गया है

- **Japanese era** (`Reiwa`) फ़ॉर्मेट स्ट्रिंग सेट करना।
- `JapaneseChronology` और `Locale` के साथ `DateTimeFormatter` का उपयोग करना।
- प्राप्त `JapaneseDate` को `LocalDate` (Gregorian) में बदलना।
- अंतिम ISO‑8601 तिथि को प्रिंट करना।
- सामान्य समस्याएँ जैसे असमर्थित युग या असंगत पैटर्न।
- अन्य लोकेल्स (Thai Buddhist, Islamic, आदि) के लिए त्वरित वैरिएशन।

**Prerequisites**  
JDK 8 या उससे नया, `java.time` की बुनियादी समझ, और जावा कोड चलाने के लिए एक IDE या CLI। बस इतना ही—कोई अतिरिक्त Maven डिपेंडेंसी नहीं।

## लोकेल के साथ तिथि पार्स करना – चरण‑दर‑चरण

नीचे हम समाधान को तीन प्राकृतिक चरणों में विभाजित करेंगे। प्रत्येक चरण में आपको आवश्यक सटीक कोड, *क्यों* यह महत्वपूर्ण है इसका संक्षिप्त स्पष्टीकरण, और एक टिप शामिल है जो आप आधिकारिक दस्तावेज़ों में नहीं पा सकते।

### चरण 1: युग तिथि स्ट्रिंग को परिभाषित करें

सबसे पहले, जापानी युग स्ट्रिंग को ठीक उसी रूप में सहेजें जैसा आपको प्राप्त हुआ (जैसे CSV फ़ाइल या UI से)।

```java
// Step 1: Define a date string using the Japanese era format (Reiwa 5)
String eraDateString = "R5/04/01";
```

> **यह क्यों महत्वपूर्ण है:**  
> अग्रणी `R` *Reiwa* को दर्शाता है, जो जापान का वर्तमान युग है। यदि आप युग संकेतक को नजरअंदाज़ करते हैं, तो पार्सर ग्रेगोरियन कैलेंडर मान लेगा और गलत वर्ष उत्पन्न करेगा।

### चरण 2: लोकेल‑सजग फ़ॉर्मेटर बनाएं

जावा का **java.time API** आपको `DateTimeFormatter` को एक विशिष्ट कालक्रम (कैलेंडर सिस्टम) और `Locale` से जोड़ने देता है। जापानी युग के लिए हम `JapaneseChronology` का उपयोग करते हैं।

```java
import java.time.chrono.JapaneseChronology;
import java.time.format.DateTimeFormatter;
import java.time.format.ResolverStyle;
import java.util.Locale;

// Step 2: Create a formatter that understands the Japanese era pattern
DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
        .parseCaseInsensitive()
        .appendPattern("Gyy/MM/dd")          // G = era symbol, yy = year-of-era
        .toFormatter(Locale.JAPAN)           // Locale for Japanese symbols
        .withChronology(JapaneseChronology.INSTANCE)
        .withResolverStyle(ResolverStyle.STRICT);
```

**मुख्य बिंदु**  
- `G` युग टेक्स्ट को पार्स करता है (`R` Reiwa के लिए, `H` Heisei के लिए, आदि)।  
- `ResolverStyle.STRICT` पार्सर को `R0/13/32` जैसी असंभव तिथियों को अस्वीकार करने के लिए बाध्य करता है।  
- `Locale` को `Locale.JAPAN` सेट करने से युग प्रतीक जापानी मानकों से मेल खाते हैं।

> **प्रो टिप:** यदि आपको *कई* युग फ़ॉर्मेट्स (जैसे `HEISEI` लिखित) का समर्थन करना है, तो दिखाए अनुसार `.parseCaseInsensitive()` जोड़ें, और पूर्ण नामों के लिए पैटर्न को `Guuuu` तक विस्तारित करें।

### चरण 3: पार्स करें और Gregorian `LocalDate` में बदलें

अब हम वास्तव में स्ट्रिंग को पार्स करते हैं और परिणाम को एक क्लासिक `LocalDate` में बदलते हैं जिसे कोई भी जावा लाइब्रेरी उपयोग कर सकती है।

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseDate;

// Step 3: Parse the era string and convert to Gregorian LocalDate
JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
LocalDate gregorianDate = LocalDate.from(japaneseDate);

// Verify the conversion
System.out.println(gregorianDate);   // Expected output: 2023-04-01
```

**व्याख्या**  
`JapaneseDate.from(...)` जापानी कैलेंडर में आधारित एक तिथि ऑब्जेक्ट बनाता है। `LocalDate.from(...)` को कॉल करके हम युग जानकारी को हटाते हैं और समकक्ष ISO‑8601 तिथि प्राप्त करते हैं—स्टोरेज, तुलना, या API कॉल्स के लिए उत्तम।

> **क्यों बदलें?** अधिकांश डेटाबेस, REST सेवाएँ, और थर्ड‑पार्टी लाइब्रेरीज़ Gregorian तिथि की अपेक्षा करती हैं। आपके पार्सिंग रूटीन के भीतर परिवर्तन को रखने से बाद में सूक्ष्म बग्स से बचा जा सकता है।

## पूर्ण कार्यशील उदाहरण

सब कुछ एक साथ मिलाकर, यहाँ एक एकल, चलाने के लिए तैयार जावा क्लास है। इसे `ParseDateWithLocale.java` में कॉपी‑पेस्ट करके चलाने के लिए स्वतंत्र महसूस करें।

```java
import java.time.LocalDate;
import java.time.chrono.JapaneseChronology;
import java.time.chrono.JapaneseDate;
import java.time.format.DateTimeFormatter;
import java.time.format.DateTimeFormatterBuilder;
import java.time.format.ResolverStyle;
import java.util.Locale;

public class ParseDateWithLocale {

    public static void main(String[] args) {
        // --- Step 1: Input ---
        String eraDateString = "R5/04/01";

        // --- Step 2: Formatter ---
        DateTimeFormatter japaneseFormatter = new DateTimeFormatterBuilder()
                .parseCaseInsensitive()
                .appendPattern("Gyy/MM/dd")
                .toFormatter(Locale.JAPAN)
                .withChronology(JapaneseChronology.INSTANCE)
                .withResolverStyle(ResolverStyle.STRICT);

        // --- Step 3: Parse & Convert ---
        JapaneseDate japaneseDate = JapaneseDate.from(japaneseFormatter.parse(eraDateString));
        LocalDate gregorianDate = LocalDate.from(japaneseDate);

        // Output
        System.out.println("Original era string: " + eraDateString);
        System.out.println("Converted Gregorian date: " + gregorianDate);
    }
}
```

**अपेक्षित कंसोल आउटपुट**

```
Original era string: R5/04/01
Converted Gregorian date: 2023-04-01
```

`javac ParseDateWithLocale.java && java ParseDateWithLocale` के साथ प्रोग्राम चलाएँ। यदि आप ऊपर दो लाइनें देखते हैं, तो आपने सफलतापूर्वक **parsed date with locale** किया है।

## एज केस हैंडलिंग और सामान्य प्रश्न

### यदि इनपुट में अलग युग प्रतीक हो तो क्या करें?

जापानी युग लगभग हर कुछ दशकों में बदलते हैं। फ़ॉर्मेटर स्वचालित रूप से `M` (Meiji), `T` (Taisho), `S` (Showa), `H` (Heisei), और `R` (Reiwa) को पहचानता है। यदि आपको कोई पुराना युग मिलता है जो डिफ़ॉल्ट `JapaneseChronology` में नहीं है, तो आपको `DateTimeParseException` मिलेगा। ऐसे में स्रोत डेटा की जाँच करें या कस्टम मैपिंग प्रदान करें।

### अन्य गैर‑Gregorian कैलेंडरों का समर्थन कैसे करें?

पैटर्न समान है; आप केवल कालक्रम और लोकेल बदलते हैं। उदाहरण के लिए, थाई बौद्ध तिथियाँ (`BuddhistChronology`) इस प्रकार दिखती हैं:

```java
DateTimeFormatter thaiFormatter = new DateTimeFormatterBuilder()
        .appendPattern("Gyy/MM/dd")
        .toFormatter(new Locale("th", "TH"))
        .withChronology(java.time.chrono.ThaiBuddhistChronology.INSTANCE);
```

### क्या मैं युग प्रतीक के बिना (सिर्फ वर्ष‑माह‑दिन) पार्स कर सकता हूँ?

हां—पैटर्न से बस `G` को हटाएँ और डिफ़ॉल्ट `ISO_LOCAL_DATE` फ़ॉर्मेटर का उपयोग करें। यह ग्रेगोरियन स्ट्रिंग्स के लिए क्लासिक *java date parsing* मार्ग है।

### लीनिएंट पार्सिंग (जैसे अग्रणी शून्य नहीं) के बारे में क्या?

`ResolverStyle.STRICT` को `ResolverStyle.LENIENT` में बदलें। ध्यान रखें कि लीनिएंट मोड अमान्य तिथियों को चुपचाप रोल ओवर कर सकता है (जैसे, `R5/13/40` बन जाता है `2024‑02‑09`)। प्रोडक्शन कोड के लिए, स्ट्रिक्ट मोड आमतौर पर सुरक्षित रहता है।

## मजबूत लोकेल तिथि रूपांतरण के लिए प्रो टिप्स

1. **फ़ॉर्मेटर को कैश करें** – `DateTimeFormatter` बनाना अपेक्षाकृत सस्ता है, लेकिन यदि आप प्रति सेकंड हजारों तिथियों को पार्स करते हैं, तो इसे एक static final फ़ील्ड में रखें।
2. **इनपुट लंबाई की जाँच करें** – एक त्वरित `if (eraDateString.length() != 8)` गार्ड अनावश्यक पार्सिंग एक्सेप्शन से बचा सकता है।
3. **मूल स्ट्रिंग को लॉग करें** – लोकेल समस्याओं को डिबग करते समय, कच्चा इनपुट अक्सर अदृश्य अक्षर (ज़ीरो‑विथ स्पेस) दिखाता है जो पार्सर को तोड़ते हैं।
4. **प्रत्येक युग का यूनिट‑टेस्ट करें** – `R`, `H`, `S`, आदि के लिए JUnit टेस्ट लिखें ताकि भविष्य के जावा अपडेट्स मैपिंग को न बदलें।

## निष्कर्ष

हमने अभी दिखाया कि जावा में आधुनिक *java time API*, लोकेल‑सजग `DateTimeFormatter`, और `JapaneseChronology` का उपयोग करके **parse date with locale** कैसे किया जाता है। पूर्ण उदाहरण पूरी प्रक्रिया को दर्शाता है—कच्ची जापानी युग स्ट्रिंग से लेकर साफ़ Gregorian `LocalDate` तक—और आपको अन्य कैलेंडरों, जैसे थाई बौद्ध या इस्लामिक सिस्टम, के लिए पैटर्न को अनुकूलित करने का ज्ञान प्रदान करता है।

अगले कदम? `JapaneseChronology` को `ThaiBuddhistChronology` या `HijrahChronology` से बदलें और देखें कि समान कोड संरचना पूरी तरह अलग सांस्कृतिक कैलेंडरों को कैसे संभालती है। आप `DateTimeFormatter.ofLocalizedDate(FormatStyle.FULL)` का उपयोग करके प्राप्त `LocalDate` को फिर से लोकेल‑विशिष्ट स्ट्रिंग में फ़ॉर्मेट करने का भी अन्वेषण कर सकते हैं।

कोई जटिल लोकेल या अप्रत्याशित पार्सिंग त्रुटि है? नीचे टिप्पणी छोड़ें, और हम साथ मिलकर समस्या हल करें। कोडिंग का आनंद लें!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Excel में डेटा प्रस्तुति में महारत: Aspose.Cells for Java के साथ संख्या और कस्टम तिथि फ़ॉर्मेटिंग](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Aspose.Cells for Java का उपयोग करके कस्टम तिथि फ़ॉर्मेट के साथ Excel को PDF में कुशलतापूर्वक परिवर्तित करें](/cells/english/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Excel में 1904 तिथि प्रणाली को Aspose.Cells Java के साथ मास्टर करें प्रभावी सेल ऑपरेशन्स के लिए](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}