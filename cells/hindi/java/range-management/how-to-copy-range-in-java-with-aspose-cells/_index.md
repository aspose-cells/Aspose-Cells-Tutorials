---
category: general
date: 2026-09-08
description: Aspose.Cells का उपयोग करके जावा में रेंज कैसे कॉपी करें – पिवट टेबल को
  कॉपी करना, पिवट टेबल को डुप्लिकेट करना, और फॉर्मेटिंग को बनाए रखते हुए पिवट टेबल
  को एक्सपोर्ट करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- copy pivot table
- duplicate pivot table
- export pivot table
- copy range with formatting
language: hi
lastmod: 2026-09-08
og_description: Aspose.Cells के साथ जावा में रेंज कैसे कॉपी करें। यह ट्यूटोरियल आपको
  दिखाता है कि पिवट टेबल को कैसे कॉपी करें, पिवट टेबल को डुप्लिकेट करें, और फॉर्मेटिंग
  को बनाए रखते हुए पिवट टेबल को एक्सपोर्ट करें।
og_image_alt: Screenshot of Java code copying a pivot table range in Aspose.Cells
og_title: जावा में रेंज कैसे कॉपी करें – Aspose.Cells की पूरी गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  headline: How to copy range in Java with Aspose.Cells
  type: TechArticle
- description: How to copy range in Java using Aspose.Cells – learn to copy pivot
    table, duplicate pivot table, and export pivot table while preserving formatting.
  name: How to copy range in Java with Aspose.Cells
  steps:
  - name: Copy pivot table to an existing workbook
    text: 'If you need to **duplicate pivot table** inside a workbook that already
      has data, use the same `copyRange` call but point to a different destination
      address:'
  - name: Export pivot table only (without surrounding data)
    text: 'Sometimes you want just the pivot table, not the source data. Identify
      the pivot table’s display range via its `getPivotTable` method:'
  - name: Preserve conditional formatting
    text: 'Conditional formatting rules are part of the style collection. The `PasteType.ALL`
      flag already copies them, but you can be explicit:'
  - name: Edge cases and troubleshooting
    text: '| Situation | What to watch for | Recommended fix | |-----------|-------------------|-----------------|
      | Source and destination workbooks use different Excel versions | Some newer
      pivot features (e.g., data model) may not render correctly | Use the latest
      Aspose.Cells version and set `Workbook.setF'
  - name: Next steps
    text: '- Explore **copy range with formatting** for charts and images (use `PasteType.PICTURES`).
      - Automate batch processing: loop over multiple source files and consolidate
      their pivot tables into a summary workbook. - Combine this technique with Aspose.Slides
      to generate PowerPoint reports that embed th'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells के साथ जावा में रेंज कैसे कॉपी करें
url: /hi/java/range-management/how-to-copy-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में Aspose.Cells के साथ रेंज कैसे कॉपी करें

यदि आपको जावा में **रेंज कैसे कॉपी करें** की आवश्यकता है, तो Aspose.Cells इस कार्य को सरल बनाता है। चाहे आप एक सामान्य सेल ब्लॉक को ले जा रहे हों या एक पूर्ण‑विशेषताओं वाला पिवट टेबल, लाइब्रेरी कॉपी ऑपरेशन को संभालती है जबकि फ़ॉर्मूले, स्टाइल और पिवट कैश को अपरिवर्तित रखती है। इस गाइड में आप सीखेंगे **पिवट टेबल कॉपी करना**, **पिवट टेबल डुप्लिकेट करना**, और यहाँ तक कि **पिवट टेबल को निर्यात करना** एक नए वर्कबुक में पूरी फ़ॉर्मेटिंग के साथ।

यह ट्यूटोरियल प्रोजेक्ट सेटअप से लेकर अंतिम सत्यापन चरण तक सब कुछ कवर करता है, ताकि आप पढ़ने के बाद तुरंत कोड चला सकें। Aspose.Cells for Java JAR के अलावा कोई बाहरी टूल आवश्यक नहीं है।

## आवश्यकताएँ

- Java 17 (या कोई समर्थित JDK) आपके IDE में स्थापित और कॉन्फ़िगर किया हुआ।
- निर्भरता प्रबंधन के लिए Maven या Gradle (उदाहरण Maven का उपयोग करते हैं)।
- `source.xlsx` नामक स्रोत Excel फ़ाइल जिसमें रेंज `A1:H20` में पिवट टेबल हो।
- जावा प्रोग्रामिंग का बुनियादी परिचय।

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

Aspose.Cells एक व्यावसायिक लाइब्रेरी है, लेकिन एक मुफ्त मूल्यांकन संस्करण उपलब्ध है। अपनी `pom.xml` में निर्भरता जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** यदि आप Gradle पसंद करते हैं, तो समकक्ष एंट्री है:
> ```gradle
> implementation 'com.aspose:aspose-cells:24.9'
> ```

JAR जोड़ने से आपको इस गाइड में उपयोग किए गए `Workbook`, `Worksheet`, `Range`, और `CopyOptions` क्लासेज़ तक पहुँच मिलती है।

## चरण 2: स्रोत वर्कबुक लोड करें और पहली वर्कशीट चुनें

**रेंज कैसे कॉपी करें** का पहला भाग है वह वर्कबुक खोलना जिसमें वह डेटा हो जिसे आप ले जाना चाहते हैं।

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        // Select the first worksheet (index 0)
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);
```

> **क्यों महत्वपूर्ण है:** वर्कबुक खोलने से एक इन‑मेमोरी प्रतिनिधित्व बनता है जिसे API मूल फ़ाइल को डिस्क पर छुए बिना हेर-फेर कर सकता है।

## चरण 3: वह रेंज परिभाषित करें जिसमें पिवट टेबल हो

पिवट टेबल एक आयताकार ब्लॉक के भीतर स्थित होती है। आपको वह ब्लॉक निर्दिष्ट करना होगा ताकि Aspose.Cells को पता चले कि क्या कॉपी करना है।

```java
        // Define the range that holds the pivot table and its source data
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");
```

> **नोट:** `createRange` मेथड अभी तक कुछ भी कॉपी नहीं करता; यह केवल एक `Range` ऑब्जेक्ट बनाता है जो उन सेल्स की ओर इशारा करता है जिन्हें आप डुप्लिकेट करना चाहते हैं।

## चरण 4: एक नया वर्कबुक बनाएं और उसकी पहली वर्कशीट प्राप्त करें

अब वह डेस्टिनेशन वर्कबुक बनाएं जहाँ कॉपी किया गया रेंज रहेगा।

```java
        // Create an empty workbook for the destination
        Workbook destWorkbook = new Workbook();
        // Get its first (and only) worksheet
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);
```

> **नया वर्कबुक क्यों?** एक नई फ़ाइल का उपयोग यह सुनिश्चित करता है कि कोई छिपी हुई स्टाइल या नामित रेंज कॉपी ऑपरेशन में बाधा न बनें, जो विशेष रूप से तब महत्वपूर्ण है जब आप **पिवट टेबल निर्यात** एक अलग फ़ाइल में करते हैं।

## चरण 5: रेंज (पिवट टेबल सहित) को डेस्टिनेशन शीट में कॉपी करें

यह **फ़ॉर्मेटिंग के साथ रेंज कैसे कॉपी करें** का मुख्य भाग है। `CopyOptions` ऑब्जेक्ट Aspose.Cells को सब कुछ संरक्षित करने के लिए बताता है: मान, फ़ॉर्मूले, स्टाइल, और पिवट कैश।

```java
        // Prepare copy options – preserve formatting and pivot cache
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL); // copies everything
        copyOptions.setSkipBlanks(false);        // keep blank cells

        // Copy the defined range to cell A1 of the destination sheet
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);
```

> **पिवट टेबल कॉपी करें:** क्योंकि स्रोत रेंज में पिवट टेबल शामिल है, API स्वचालित रूप से पिवट कैश को डुप्लिकेट करता है, इसलिए नई वर्कशीट में एक पूरी तरह कार्यात्मक पिवट टेबल होती है जो मूल के समान व्यवहार करती है।

## चरण 6: डेस्टिनेशन वर्कबुक को सहेजें

अंत में, परिणाम को डिस्क पर लिखें।

```java
        // Save the destination workbook
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

जब आप `dest.xlsx` खोलेंगे, तो आपको मूल पिवट टेबल की बिल्कुल समान प्रतिलिपि दिखेगी, जिसमें उसकी फ़ॉर्मेटिंग, स्लाइसर, और गणना किए गए फ़ील्ड शामिल हैं।

## अपेक्षित आउटपुट

- `dest.xlsx` में **Sheet1** नामक एक वर्कशीट है।
- सेल `A1:H20` में स्रोत के समान डेटा और पिवट टेबल है।
- सभी सेल स्टाइल (फ़ॉन्ट, रंग, बॉर्डर) संरक्षित रहते हैं।
- पिवट टेबल पूरी तरह इंटरैक्टिव है; इसे रीफ़्रेश करने से कॉपी किए गए रेंज के अंतर्निहित डेटा को प्रतिबिंबित करता है।

## फ़ॉर्मेटिंग के साथ रेंज कैसे कॉपी करें – गहन विश्लेषण

पिछला उदाहरण सबसे सरल परिदृश्य दिखाता है, लेकिन आप ऐसे विविधताओं का सामना कर सकते हैं जिनके लिए थोड़ा अलग तरीका आवश्यक हो सकता है।

### मौजूदा वर्कबुक में पिवट टेबल कॉपी करें

यदि आपको डेटा वाले वर्कबुक के भीतर **पिवट टेबल डुप्लिकेट** करना है, तो वही `copyRange` कॉल उपयोग करें लेकिन एक अलग डेस्टिनेशन एड्रेस की ओर इंगित करें:

```java
// Assume destWorkbook already contains other sheets
Worksheet targetSheet = destWorkbook.getWorksheets().get(2);
targetSheet.getCells().copyRange(sourceRange, "B5", copyOptions);
```

### केवल पिवट टेबल निर्यात करें (आसपास के डेटा के बिना)

कभी-कभी आप केवल पिवट टेबल चाहते हैं, स्रोत डेटा नहीं। `getPivotTable` मेथड के माध्यम से पिवट टेबल की डिस्प्ले रेंज पहचानें:

```java
PivotTable pt = sourceSheet.getPivotTables().get(0);
String ptArea = pt.getDisplayRange(); // e.g., "C5:G15"
Range pivotOnly = sourceSheet.getCells().createRange(ptArea);
destSheet.getCells().copyRange(pivotOnly, "A1", copyOptions);
```

### कंडीशनल फ़ॉर्मेटिंग को संरक्षित रखें

कंडीशनल फ़ॉर्मेटिंग नियम स्टाइल कलेक्शन का हिस्सा होते हैं। `PasteType.ALL` फ़्लैग पहले से ही उन्हें कॉपी करता है, लेकिन आप स्पष्ट रूप से भी कर सकते हैं:

```java
copyOptions.setPasteType(PasteType.FORMATS);
copyOptions.setPasteType(PasteType.ALL); // overrides previous, ensures everything
```

### किनारे के मामलों और समस्या निवारण

| स्थिति | ध्यान रखने योग्य बातें | सिफ़ारिश किया गया समाधान |
|-----------|-------------------|-----------------|
| स्रोत और डेस्टिनेशन वर्कबुक अलग-अलग Excel संस्करणों का उपयोग करते हैं | कुछ नए पिवट फीचर (जैसे, डेटा मॉडल) सही ढंग से रेंडर नहीं हो सकते | दोनों वर्कबुक के लिए नवीनतम Aspose.Cells संस्करण का उपयोग करें और `Workbook.setFileFormatType(FileFormatType.XLSX)` सेट करें |
| बहुत बड़े पिवट टेबल (> 10 000 पंक्तियाँ) मेमोरी दबाव उत्पन्न करते हैं | कॉपी के दौरान मेमोरी समाप्ति त्रुटियाँ | लोड करने से पहले `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` सक्षम करें |
| डेस्टिनेशन शीट में पहले से ही स्रोत के समान नाम वाला एक नामित रेंज मौजूद है | नाम टकराव के कारण `CopyOptions` विफल हो जाता है | `copyOptions.setIgnoreNameConflicts(true)` को कॉल करें |

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूर्ण प्रोग्राम दिया गया है जिसे आप जावा क्लास में कॉपी‑पेस्ट कर सकते हैं। इसमें सभी इम्पोर्ट, एरर हैंडलिंग, और टिप्पणियाँ शामिल हैं।

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot table
        Range sourceRange = sourceSheet.getCells().createRange("A1:H20");

        // 3️⃣ Create a new destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Configure copy options to keep everything (values, formulas, formatting, pivot cache)
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.ALL);
        copyOptions.setSkipBlanks(false);
        copyOptions.setIgnoreNameConflicts(true); // avoid name collisions

        // 5️⃣ Perform the copy
        destSheet.getCells().copyRange(sourceRange, "A1", copyOptions);

        // 6️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
        System.out.println("Copy completed – dest.xlsx now contains the duplicated pivot table.");
    }
}
```

प्रोग्राम चलाएँ, फिर `dest.xlsx` खोलें यह सत्यापित करने के लिए कि पिवट टेबल मूल की तरह ठीक काम कर रहा है।

## निष्कर्ष

अब आप जावा में Aspose.Cells का उपयोग करके **रेंज कैसे कॉपी करें** जानते हैं, जिसमें **पिवट टेबल कॉपी करना**, **पिवट टेबल डुप्लिकेट करना**, और **पिवट टेबल निर्यात करना** शामिल है, जबकि सभी फ़ॉर्मेटिंग संरक्षित रहती है। लाइब्रेरी Excel के XML संरचना के लो‑लेवल विवरणों को अमूर्त बनाती है, जिससे आप व्यापार लॉजिक पर ध्यान केंद्रित कर सकते हैं।

### अगले कदम

- **फ़ॉर्मेटिंग के साथ रेंज कॉपी** को चार्ट और इमेज के लिए एक्सप्लोर करें (`PasteType.PICTURES` का उपयोग करें)।
- बैच प्रोसेसिंग को ऑटोमेट करें: कई स्रोत फ़ाइलों पर लूप चलाएँ और उनके पिवट टेबल को एक सारांश वर्कबुक में समेकित करें।
- इस तकनीक को Aspose.Slides के साथ मिलाएँ ताकि कॉपी किए गए पिवट को एम्बेड करने वाले PowerPoint रिपोर्ट जनरेट किए जा सकें।

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [जावा के लिए Aspose.Cells के साथ Excel पिवट टेबल स्रोत को अपडेट करने का तरीका: एक व्यापक गाइड](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells का उपयोग करके जावा में पिवट टेबल लोडिंग को ऑप्टिमाइज़ करना – एक व्यापक गाइड](/cells/english/java/data-analysis/optimize-pivot-table-loading-aspose-cells-java/)
- [C# में पिवट टेबल कॉपी करने का तरीका – Excel को PPTX में बदलें, रेंज कॉपी करें और टेक्स्टबॉक्स बनाएं](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}