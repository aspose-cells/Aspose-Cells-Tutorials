---
category: general
date: 2026-07-03
description: Aspose.Cells का उपयोग करके जावा में फ़ॉर्मूला निर्यात शामिल करें ताकि
  Excel कोशिकाओं को टेक्स्ट में बदला जा सके। जानें कि Excel रेंज को कैसे प्रिंट करें
  और कोशिका मानों को स्ट्रिंग के रूप में कुशलतापूर्वक प्राप्त करें।
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: hi
og_description: जावा में फ़ॉर्मूला निर्यात शामिल करें ताकि एक्सेल सेल्स को टेक्स्ट
  में बदला जा सके। चरण‑दर‑चरण गाइड जो दिखाता है कि एक्सेल रेंज को कैसे प्रिंट करें
  और सेल मानों को स्ट्रिंग के रूप में कैसे प्राप्त करें।
og_title: जावा में फॉर्मूला निर्यात शामिल करें – एक्सेल सेल्स को टेक्स्ट में बदलें
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: जावा में फ़ॉर्मूला निर्यात शामिल करें – एक्सेल सेल्स को टेक्स्ट में परिवर्तित
  करें
url: /hi/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# फ़ॉर्मूला निर्यात को Java में शामिल करें – Excel सेल्स को टेक्स्ट में बदलें

क्या आपको कभी Excel वर्कबुक से डेटा निकालते समय **include formulas export** की आवश्यकता पड़ी है? शायद आप एक रिपोर्टिंग सेवा बना रहे हैं जिसे मूल फ़ॉर्मूले को संरक्षित रखना है जबकि एक साफ़ टेक्स्ट ब्लॉब प्रदान करना है। ऐसे में आप सही जगह पर हैं। यह गाइड आपको Excel सेल्स को साधारण टेक्स्ट में बदलने की प्रक्रिया दिखाता है—*including* कोई भी एम्बेडेड फ़ॉर्मूले—Aspose.Cells for Java का उपयोग करके।

हम यह भी बताएँगे कि कैसे **print Excel range** किया जाता है, **export table options** को समायोजित किया जाए, और अंत में **get cell values string** प्राप्त किया जाए जिसे आप लॉग कर सकते हैं, API के माध्यम से भेज सकते हैं, या डेटाबेस में स्टोर कर सकते हैं। अंत तक आपके पास एक पूरी तरह चलने योग्य स्निपेट होगा और प्रत्येक कॉल के पीछे का कारण स्पष्ट रूप से समझ में आएगा।

## आप क्या सीखेंगे

- एक पूर्ण, कॉपी‑पेस्ट‑तैयार Java प्रोग्राम जो `.xlsx` फ़ाइल पढ़ता है, रेंज चुनता है, और उसे फ़ॉर्मेटेड स्ट्रिंग के रूप में निर्यात करता है।
- `ExportTableOptions` क्लास की समझ और क्यों `setExportAsString` और `setIncludeFormula` को टॉगल करना महत्वपूर्ण है।
- बड़े वर्कशीट्स को संभालने, विभिन्न डेटा टाइप्स से निपटने, और आउटपुट फ़ॉर्मेट को कस्टमाइज़ करने के टिप्स।
- सामान्य समस्याओं के लिए एक त्वरित चेकलिस्ट (जैसे मर्ज्ड सेल्स, छिपी हुई पंक्तियाँ, और लोकेल‑विशिष्ट नंबर फ़ॉर्मेट)।

### आवश्यकताएँ

- Java 17 या उससे नया (कोड पुराने संस्करणों पर भी कम्पाइल हो जाता है लेकिन हम नवीनतम LTS का उपयोग करेंगे)।
- Aspose.Cells for Java 23.10 (या कोई भी हालिया रिलीज़) — आप इसे Maven Central से प्राप्त कर सकते हैं।
- एक नमूना `input.xlsx` जिसे आप नियंत्रित फ़ोल्डर में रखें (उदाहरण में पाथ स्पष्टता के लिए हार्ड‑कोडेड है)।

यदि आपके पास ये सब हैं, तो चलिए शुरू करते हैं।

## चरण 1: प्रोजेक्ट सेट अप करें और डिपेंडेंसीज़ जोड़ें

सबसे पहले, एक Maven प्रोजेक्ट बनाएँ (या यदि आप पसंद करते हैं तो Gradle)। अपने `pom.xml` में Aspose.Cells डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Pro tip:** यदि आप कॉरपोरेट प्रॉक्सी का उपयोग कर रहे हैं, तो सुनिश्चित करें कि रिपॉज़िटरी उपलब्ध है; अन्यथा बिल्ड “Could not resolve dependencies” त्रुटि के साथ फेल हो जाएगा।

एक बार Maven डाउनलोड पूरा कर लेगा, आप Java लिखने के लिए तैयार हैं।

## चरण 2: वर्कबुक लोड करें और इच्छित वर्कशीट प्राप्त करें

कोड उदाहरण की पहली पंक्ति दिखाती है कि मौजूदा वर्कबुक कैसे खोली जाए:

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

`YOUR_DIRECTORY` को अपनी फ़ाइल के पूर्ण या सापेक्ष पाथ से बदलें। `Workbook` कंस्ट्रक्टर फ़ाइल फ़ॉर्मेट (XLS, XLSX, CSV, आदि) को स्वचालित रूप से पहचान लेता है, इसलिए आपको इसे मैन्युअल रूप से निर्दिष्ट करने की जरूरत नहीं है।

अब हम पहली शीट प्राप्त करते हैं:

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

पहली शीट क्यों? कई टेम्प्लेट्स में डेटा पहली टैब पर रहता है, लेकिन आप कोई भी इंडेक्स पास कर सकते हैं या यदि आप नामित दृष्टिकोण पसंद करते हैं तो `get("SheetName")` का उपयोग कर सकते हैं।

## चरण 3: वह रेंज निर्धारित करें जिसे आप निर्यात करना चाहते हैं

अब **convert excel cells text** ऑपरेशन का मुख्य भाग आता है। आप Aspose.Cells को बताते हैं कि किन सेल्स को निकालना है, एक `Range` ऑब्जेक्ट बनाकर:

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

`"A1:C3"` स्ट्रिंग एक क्लासिक A1‑स्टाइल एड्रेस है। इसे प्रोग्रामेटिकली भी बनाया जा सकता है:

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

यह लचीलापन तब मददगार होता है जब रेंज का आकार डायनामिक हो—जैसे, आप अंतिम उपयोग की गई पंक्ति को `ws.getCells().getMaxDataRow()` से पढ़ते हैं।

## चरण 4: फ़ॉर्मूले शामिल करने के लिए Export Table Options कॉन्फ़िगर करें

यहीं पर **include formulas export** जादू काम करता है। डिफ़ॉल्ट रूप से, Aspose.Cells *दिखाए गए* मान लौटाता है। यदि किसी सेल में `=SUM(A1:A3)` है, तो आपको गणना किया हुआ नंबर मिलेगा, न कि फ़ॉर्मूला टेक्स्ट। इसे बदलने के लिए, `ExportTableOptions` सेट करें:

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

दोनों फ़्लैग क्यों? `setExportAsString(true)` API को बताता है कि सेल्स को डिफ़ॉल्ट डिलिमिटर (कॉलम के लिए टैब, पंक्तियों के लिए नई लाइन) का उपयोग करके जोड़ना है। `setIncludeFormula(true)` मान स्रोत को “दिखाया गया मान” से “कच्चा फ़ॉर्मूला” में बदल देता है। यदि आप केवल मान चाहते हैं, तो इसे `false` रखें।

### वैकल्पिक समायोजन

- `eto.setExportHiddenRows(true);` – Excel में छिपी हुई पंक्तियों को शामिल करें।
- `eto.setExportHiddenColumns(true);` – कॉलम के लिए भी यही।
- `eto.setExportAsHTML(true);` – साधारण टेक्स्ट के बजाय HTML प्राप्त करें।

बिना झिझक प्रयोग करें; विकल्प क्लास एक **export table options** खेल का मैदान है।

## चरण 5: रेंज को फ़ॉर्मेटेड स्ट्रिंग के रूप में प्राप्त करें

अब हम डेटा निकालते हैं:

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

वापसी में मिला `txt` कुछ इस प्रकार दिखेगा (मान लेते हैं कि A1:C3 में मान और फ़ॉर्मूले दोनों हैं):

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

ध्यान दें कि टैब (`\t`) कॉलम को अलग करता है और नई लाइन (`\n`) पंक्तियों को। यदि आपको 2‑D एरे चाहिए तो आप बाद में स्ट्रिंग को विभाजित कर सकते हैं:

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## चरण 6: परिणाम प्रिंट करें – “Print Excel Range” को सरल बनाएं

अंत में, हम स्ट्रिंग को कंसोल में प्रिंट करते हैं:

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

प्रोग्राम चलाने पर ऊपर दिखाए गए सटीक आउटपुट को प्रिंट करेगा। यहाँ से आप स्ट्रिंग को लॉग फ़ाइल में लिख सकते हैं, HTTP के माध्यम से भेज सकते हैं, या NoSQL दस्तावेज़ में स्टोर कर सकते हैं।

## पूर्ण, तैयार‑चलाने‑योग्य उदाहरण

सब कुछ मिलाकर, यहाँ पूरा प्रोग्राम है। कॉपी, पेस्ट करें, और **Run** दबाएँ—कोई इम्पोर्ट गायब नहीं है।

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### अपेक्षित आउटपुट (उदाहरण)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

यदि आपकी वर्कबुक में संख्याएँ डेट के रूप में फ़ॉर्मेटेड हैं, तो वे लोकेल‑विशिष्ट फ़ॉर्मेट में दिखेंगी (जैसे, `2026‑07‑03`)। ISO डेट्स को मजबूर करने के लिए, आप `ExportTableOptions` को कस्टम `NumberFormat` के साथ समायोजित कर सकते हैं।

## किनारे के मामलों और सामान्य प्रश्नों को संभालना

### यदि रेंज में मर्ज्ड सेल्स हों तो क्या करें?

मर्ज्ड सेल्स को टॉप‑लेफ़्ट सेल के मान के रूप में माना जाता है। मर्ज्ड क्षेत्र का बाकी हिस्सा खाली स्ट्रिंग्स के रूप में दिखेगा। यदि आपको मर्ज्ड रेंज का एड्रेस चाहिए, तो निर्यात से पहले `Cell.getMergedRange()` को क्वेरी करें।

### क्या मैं सैकड़ों हजारों पंक्तियों वाली बड़ी शीट निर्यात कर सकता हूँ?

हां, लेकिन मेमोरी उपयोग का ध्यान रखें। `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` का उपयोग करके Aspose.Cells को डेटा डिस्क पर स्ट्रीम करने दें। साथ ही, स्ट्रिंग को संभालने योग्य रखने के लिए चंक्स में निर्यात करने पर विचार करें (जैसे, एक बार में 10 000 पंक्तियाँ)।

### कॉलम डिलिमिटर कैसे बदलें?

`ExportTableOptions` में `setSeparator(char separator)` उपलब्ध है। CSV‑स्टाइल आउटपुट के लिए, इसे `','` पर सेट करें:

```java
eto.setSeparator(',');
```

### क्या फ़ॉर्मूले बाहरी रेफ़रेंसेज़ का सम्मान करते हैं?

यदि कोई फ़ॉर्मूला दूसरे वर्कबुक की ओर इशारा करता है, तो Aspose.Cells रेफ़रेंस टेक्स्ट (`='[Other.xlsx]Sheet1'!A1`) को रखेगा। यह बाहरी मान का मूल्यांकन नहीं करेगा जब तक आप वह वर्कबुक भी लोड न करें।

## प्रोडक्शन‑रेडी कोड के लिए प्रो टिप्स

- **Cache the workbook** यदि आप पढ़ रहे हैं

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Convert Excel to PDF in Java Using Aspose.Cells&#58; A Step-by-Step Guide](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Export Excel Workbook as Image Using Aspose.Cells for Java&#58; A Step-by-Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}