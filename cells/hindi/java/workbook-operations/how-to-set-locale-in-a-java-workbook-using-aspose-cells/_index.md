---
category: general
date: 2026-11-22
description: जावा वर्कबुक में लोकेल सेट करना, वर्कबुक की भाषा बदलना, और कैलेंडर को
  जापानी सेट करना सीखें, स्पष्ट कोड उदाहरणों के साथ।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: hi
lastmod: 2026-11-22
og_description: जावा वर्कबुक में लोकेल को जल्दी से कैसे सेट करें। इस ट्यूटोरियल का
  पालन करके वर्कबुक की भाषा बदलें, लोकेल को जापानी सेट करें, और जापानी कैलेंडर को
  कॉन्फ़िगर करें।
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: जावा वर्कबुक में लोकेल सेट करने का तरीका – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Aspose.Cells का उपयोग करके जावा वर्कबुक में लोकेल कैसे सेट करें
url: /hi/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells का उपयोग करके Java वर्कबुक में लोकैल सेट कैसे करें

Java वर्कबुक में लोकैल सेट करना एक सामान्य आवश्यकता है जब आपको अपनी स्प्रेडशीट को विभिन्न क्षेत्रों के अनुसार अनुकूलित करना होता है। इस गाइड में आप सीखेंगे कि कैसे लोकैल सेट करें, वर्कबुक की भाषा बदलें, और Aspose.Cells API का उपयोग करके कैलेंडर को जापानी सेट करें।

एक वर्कबुक को अंतर्राष्ट्रीयकरण करना केवल टेक्स्ट का अनुवाद करने से अधिक है; यह नंबर फ़ॉर्मेट, डेट पार्सिंग, और डिफ़ॉल्ट कैलेंडर सिस्टम को भी प्रभावित करता है। इस ट्यूटोरियल के अंत तक आप सक्षम होंगे:

* वर्कबुक का लोकैल जापानी (Japan) में कॉन्फ़िगर करें – **set locale to japanese**।  
* वर्कबुक की भाषा बदलें ताकि फ़ॉर्मूले और UI स्ट्रिंग्स लक्ष्य संस्कृति का सम्मान करें – **change workbook language**।  
* कैलेंडर को जापानी इम्पीरियल कैलेंडर में बदलें – **how to set calendar**।  

इन चरणों को किसी भी हालिया Aspose.Cells for Java संस्करण (v23.9 या बाद) के साथ उपयोग किया जा सकता है और केवल एक मानक Java विकास वातावरण की आवश्यकता होती है।

## Prerequisites

| आवश्यकता | कारण |
|-------------|--------|
| Java 8 या उससे ऊपर | लाइब्रेरी Java 8+ को लक्षित करती है। |
| Aspose.Cells for Java (v23.9+) | `Workbook`, `WorkbookSettings`, और लोकैल यूटिलिटीज़ प्रदान करता है। |
| IDE (IntelliJ IDEA, Eclipse, or VS Code) | सैंपल को कम्पाइल और रन करने के लिए। |
| Basic knowledge of Java | कोड स्निपेट्स को समझने के लिए आवश्यक। |

Add the Aspose.Cells Maven dependency to your `pom.xml` (or download the JAR manually):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## How to set locale and calendar in a workbook

पहला कदम एक वर्कबुक इंस्टेंस बनाना और उसकी सेटिंग्स ऑब्जेक्ट प्राप्त करना है। सेटिंग्स ऑब्जेक्ट लोकैल और कैलेंडर API को उजागर करता है।

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Why each line matters

* **`new Workbook()`** – एक खाली वर्कबुक बनाता है जिसे आप सहेजने से पहले संशोधित कर सकते हैं।  
* **`getSettings()`** – एक `WorkbookSettings` ऑब्जेक्ट लौटाता है; सभी क्षेत्रीय विकल्प यहाँ होते हैं।  
* **`setCalendar(...)`** – डिफ़ॉल्ट ग्रेगोरियन कैलेंडर को जापानी इम्पीरियल कैलेंडर से बदलता है, जिससे तिथियों के रेंडरिंग और पार्सिंग पर असर पड़ता है।  
* **`setLocale(new Locale("ja","JP"))`** – भाषा और क्षेत्रीय मानकों (जैसे महीने, दशमलव विभाजक) को बदलता है। यह वर्कबुक के लिए **how to set locale** का मुख्य भाग है।  

प्रोग्राम चलाने से `LocaleDemo.xlsx` बनता है। इसे Excel या LibreOffice में खोलें और आप जापानी महीने के नाम, जापानी येन मुद्रा प्रतीक, और जापानी कैलेंडर के अनुसार फॉर्मेट की गई तिथियाँ देखेंगे।

## Change workbook language (set locale to Japanese)

यदि आपका मुख्य लक्ष्य **change workbook language** है, तो आप केवल `setLocale` कॉल पर ध्यान केंद्रित कर सकते हैं। निम्न स्निपेट इस कदम को अलग करता है:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**क्या बदलता है?**  
* सेल फ़ॉर्मेटिंग स्ट्रिंग्स जापानी में बदल जाती हैं (उदाहरण के लिए `#,##0.00` में येन प्रतीक के साथ `#,##0.00` बन जाता है)।  
* बिल्ट‑इन फ़ंक्शन नाम (जैसे `SUM`) अंग्रेज़ी ही रहते हैं क्योंकि Excel का फ़ंक्शन लोकैल स्वतंत्र है, लेकिन डेट स्ट्रिंग्स और एरर मैसेजेज़ जापानी मानकों का पालन करते हैं।  

**इसे कब उपयोग करें?**  
* जब आपको एक स्प्रेडशीट चाहिए जो जापानी दर्शकों के लिए संख्याएँ और तिथियाँ दिखाए, लेकिन अंतर्निहित कैलेंडर ग्रेगोरियन ही रहे।  
* उन रिपोर्टों के लिए जो PDF में एक्सपोर्ट या प्रिंट की जाती हैं, यह सुनिश्चित करने के लिए कि दृश्य भाषा लक्ष्य बाजार से मेल खाती हो।

## How to set calendar to the Japanese calendar

कभी‑कभी **how to set calendar** की आवश्यकता लोकैल से अलग होती है। उन लेगेसी सिस्टमों के लिए जो जापानी इम्पीरियल युग में तिथियों को संग्रहीत करते हैं, आपको स्पष्ट रूप से कैलेंडर सेट करना होगा जबकि वैकल्पिक रूप से डिफ़ॉल्ट लोकैल को रख सकते हैं।

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**मुख्य बिंदु:**

* `Calendar.getInstance(Locale.JAPAN)` एक `java.util.Calendar` लौटाता है जो जापानी युग के लिए कॉन्फ़िगर किया गया है।  
* वर्कबुक अब तिथियों को युग प्रतीकों (R रीवा के लिए, H हेइसेई के लिए, आदि) के साथ रेंडर करेगा।  
* यह सेटिंग संख्या फ़ॉर्मेटिंग या UI भाषा को **प्रभावित नहीं** करती; यदि आपको दोनों चाहिए तो इसे `setLocale` के साथ मिलाएँ।

## Full end‑to‑end example

नीचे एक पूर्ण, चलाने योग्य प्रोग्राम है जो **how to set locale**, **change workbook language**, और **set the calendar** को एक सुसंगत प्रवाह में दर्शाता है। यह प्रभाव को दिखाने के लिए एक नमूना सेल भी जोड़ता है।

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**अपेक्षित आउटपुट:**  
`FullJapaneseLocale.xlsx` खोलने पर पहला सेल `R3/04/01` (रीवा 3) जैसी तिथि दिखाएगा और दूसरा सेल `¥1,234,567.89` के रूप में फॉर्मेट होगा। यह पुष्टि करता है कि **how to set locale**, **change workbook language**, और **how to set calendar** सभी मिलकर काम करते हैं।

## Common pitfalls and how to avoid them

| समस्या | क्यों होता है | समाधान |
|---------|----------------|-----|
| `Locale.CHINA` का उपयोग `new Locale("ja","JP")` के बजाय | `Locale.CHINA` चीनी भाषा सेट करता है, न कि जापानी। | जापानी के लिए हमेशा `Locale` को `"ja", "JP"` के साथ इंस्टैंशिएट करें। |
| `setLocale` के बाद `settings.setCalendar(...)` कॉल करना भूल जाना | कैलेंडर डिफ़ॉल्ट रूप से ग्रेगोरियन रहता है, इसलिए तिथियाँ गलत युग में दिखती हैं। | `setLocale` सेट करने के बाद **`setCalendar`** कॉल करें, या जैसा दिखाया गया है दोनों को साथ में सेट करें। |
| सेटिंग्स लागू करने से पहले वर्कबुक को सेव करना | सेटिंग्स मेमोरी में ऑब्जेक्ट पर लागू होती हैं; जल्दी सेव करने से डिफ़ॉल्ट लोकैल लिखा जाता है। | सभी लोकैल/कैलेंडर परिवर्तन `workbook.save()` कॉल करने से **पहले** लागू करें। |
| पुराने Aspose.Cells संस्करण का उपयोग करना | पुराने संस्करणों में `setCalendar` ओवरलोड नहीं होते। | v23.9+ में अपग्रेड करें या लोकैल सपोर्ट के लिए रिलीज़ नोट्स देखें। |

## Testing your configuration

1. **FullLocaleExample** क्लास चलाएँ।  
2. जनरेट किए गए `FullJapaneseLocale.xlsx` को Excel में खोलें।  
3. सुनिश्चित करें कि:  
   * डेट कॉलम में जापानी युग प्रतीक (`R`, `H`, आदि) दिखें।  
   * नंबर कॉलम में येन प्रतीक और कॉमा सेपरेटर हों।  
   * कोई भी बिल्ट‑इन एरर मैसेज (जैसे `#DIV/0!`) यदि वर्कबुक में त्रुटियाँ हैं तो जापानी में दिखें।  

यदि इन जाँचों में से कोई भी विफल हो, तो दोबारा जाँचें कि आप द्वारा संशोधित `WorkbookSettings` ऑब्जेक्ट वही इंस्टेंस है जिसका उपयोग सेव करते समय किया गया था।

## Next steps

* **फ़ॉर्मूले स्थानीयकृत करें** – जबकि लोकैल फ़ॉर्मेटिंग को नियंत्रित करता है, आप `FormulaParser` का उपयोग करके कस्टम फ़ंक्शन नाम भी अनुवादित कर सकते हैं।  
* **मौजूदा वर्कबुक्स पर लोकैल लागू करें** – `new Workbook` का उपयोग करके वर्कबुक लोड करें।  

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल निकटता से संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Aspose Cells डेट फ़ॉर्मेट: Java में कस्टम डेट फ़ॉर्मेट कैसे सेट करें](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Aspose.Cells .NET का उपयोग करके Excel फ़ाइलों में भाषा कैसे सेट करें बहुभाषी समर्थन के लिए](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Aspose.Cells का उपयोग करके C# में सेल नंबर फ़ॉर्मेट सेट करना और जापानी तिथियों को परिवर्तित करना](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}