---
category: general
date: 2026-10-23
description: जावा में एक्सेल शीट को डुप्लिकेट करते हुए पिवट टेबल्स को संरक्षित रखना
  सीखें। यह गाइड पिवट टेबल्स को कॉपी करने, एक्सेल रेंजेज़ को कॉपी करने और पिवट डेटा
  वाली शीट को कॉपी करने का तरीका भी दिखाता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- duplicate excel sheet
- how to copy pivot
- copy excel range
- copy sheet with pivot
- copy pivot to workbook
language: hi
lastmod: 2026-10-23
og_description: जावा में एक्सेल शीट को डुप्लिकेट करें और पिवट टेबल्स को संरक्षित रखें।
  पिवट टेबल्स कॉपी करने, एक्सेल रेंजेज कॉपी करने और पिवट डेटा वाली शीट कॉपी करने के
  लिए इस पूर्ण ट्यूटोरियल का पालन करें।
og_image_alt: Screenshot showing a duplicated Excel sheet with pivot tables preserved
og_title: जावा में पिवट टेबल्स वाले एक्सेल शीट को डुप्लिकेट करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-23'
  description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  headline: How to duplicate an Excel sheet and keep pivot tables intact in Java
  type: TechArticle
- description: Learn how to duplicate an Excel sheet in Java while preserving pivot
    tables. This guide also shows how to copy pivot tables, copy Excel ranges, and
    copy a sheet with pivot data.
  name: How to duplicate an Excel sheet and keep pivot tables intact in Java
  steps:
  - name: Expected output
    text: 'Running the program creates `DuplicatedWithPivot.xlsx` in the target directory.
      Open the file in Excel and you will see:'
  - name: How to copy pivot to another workbook without copying the whole sheet?
    text: If you only need the pivot and its underlying data, copy the range that
      contains both the source data and the pivot, then use `setCopyPivotTable(true)`.
      The same code from **Step 4** applies; just ensure the range covers the data
      source.
  - name: What if the source workbook has multiple worksheets with pivots?
    text: 'Repeat **Step 3** for each worksheet you want to duplicate:'
  - name: Does this work with protected worksheets?
    text: 'Aspose.Cells can copy protected sheets, but you must unprotect them first
      if you need to modify the pivot after copying:'
  - name: Can I copy a pivot table to an existing workbook that already contains a
      sheet with the same name?
    text: 'Yes. Use `addCopy` with a unique name:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
- Pivot tables
title: जावा में एक्सेल शीट को डुप्लिकेट कैसे करें और पिवट टेबल्स को अपरिवर्तित रखें
url: /hi/java/excel-pivot-tables/how-to-duplicate-an-excel-sheet-and-keep-pivot-tables-intact/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में Excel शीट को डुप्लिकेट करें और Pivot Table को अपरिवर्तित रखें

यदि आपको **Excel शीट को डुप्लिकेट** करना है और सभी Pivot Table को जीवित रखना है, तो यह गाइड आपको बिल्कुल वही तरीका दिखाएगा। आप एक संक्षिप्त समाधान देखेंगे जो शीट को कॉपी करता है, एक विशिष्ट रेंज को कॉपी करता है, और यहाँ तक कि Pivot Table को दूसरे वर्कबुक में भी कॉपी करता है—सभी शुद्ध Java में Aspose.Cells का उपयोग करके।

Excel शीट को डुप्लिकेट करना एक सामान्य कार्य है जब आप टेम्पलेट से मासिक रिपोर्ट बनाते हैं या परीक्षण के लिए एक सैंडबॉक्स कॉपी की आवश्यकता होती है। नीचे दिया गया कोड Aspose.Cells 25.11 या बाद के संस्करण के साथ काम करता है, जिसमें `setCopyPivotTable(true)` विकल्प पेश किया गया था।

## आपको क्या चाहिए

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

- Java 17 (या कोई भी नवीनतम JDK) स्थापित
- आपके प्रोजेक्ट में Aspose.Cells for Java 25.11 या नया (Maven coordinate `com.aspose:aspose-cells:25.11`)
- एक स्रोत वर्कबुक (`SourceWithPivot.xlsx`) जिसमें पहले से ही Pivot Table मौजूद है
- आपका पसंदीदा IDE या बिल्ड टूल (IntelliJ IDEA, Eclipse, Maven, Gradle, आदि)

## चरण 1: स्रोत वर्कबुक लोड करें जिसमें Pivot Table है

पहला कार्य वह वर्कबुक खोलना है जिसमें वह Pivot है जिसे आप संरक्षित रखना चाहते हैं।

```java
import com.aspose.cells.*;

public class DuplicateExcelSheet {
    public static void main(String[] args) throws Exception {
        // Load the source workbook with the pivot table
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/SourceWithPivot.xlsx");
```

> **यह चरण क्यों महत्वपूर्ण है:** स्रोत वर्कबुक को लोड करने से आपको वर्कशीट ऑब्जेक्ट्स, सेल्स, और एम्बेडेड Pivot Tables तक पहुंच मिलती है। इसके बिना आप उस Pivot डेटा को रेफ़र नहीं कर पाएंगे जिसे आप कॉपी करना चाहते हैं।

## चरण 2: एक खाली लक्ष्य वर्कबुक बनाएं (या मौजूदा को लोड करें)

आप या तो एक खाली वर्कबुक से शुरू कर सकते हैं या किसी मौजूदा फ़ाइल को खोल सकते हैं जो डुप्लिकेटेड शीट प्राप्त करेगी।

```java
        // Create a new, empty destination workbook
        Workbook dstWb = new Workbook();
```

> **टिप:** यदि आपके पास पहले से ही एक रिपोर्टिंग वर्कबुक है, तो ऊपर की लाइन को `new Workbook("ExistingReport.xlsx")` से बदल दें ताकि डुप्लिकेटेड शीट उसमें जोड़ सकें।

## चरण 3: पूरी वर्कशीट कॉपी करें – Pivot Table स्वचालित रूप से संरक्षित रहता है

पूरी वर्कशीट को कॉपी करना **शीट को Pivot के साथ कॉपी** करने का सबसे सरल तरीका है। Aspose.Cells Pivot की परिभाषा और उसका कैश स्वचालित रूप से कॉपी करता है।

```java
        // Access the first worksheet (index 0) from the source workbook
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Add a copy of the source worksheet to the destination workbook
        Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
```

> **यह क्यों काम करता है:** `addCopy` शीट की संरचना, सेल वैल्यूज़, स्टाइल्स और किसी भी एम्बेडेड Pivot Table को क्लोन करता है। `dstWb` में नई वर्कशीट मूल के समान दिखेगी, जिसमें Pivot Cache भी शामिल होगा।

## चरण 4: (वैकल्पिक) केवल वह रेंज कॉपी करें जिसमें Pivot Table शामिल है

कभी-कभी आपको पूरी शीट की आवश्यकता नहीं होती—शायद आप केवल वह भाग चाहते हैं जिसमें Pivot है। यही वह जगह है जहाँ आप **Excel रेंज कॉपी** करते हैं और स्पष्ट रूप से Pivot को कॉपी करने का अनुरोध करते हैं।

```java
        // Define the source range that covers the pivot table (adjust as needed)
        Range srcRange = srcWs.getCells().createRange("A1:G30");

        // Define the target range in the destination worksheet
        Range dstRange = dstWs.getCells().createRange("A1");

        // Copy the range and tell Aspose.Cells to include the pivot table
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setCopyPivotTable(true); // new option in 25.11
        dstRange.copy(srcRange, copyOptions);
```

> **यह कैसे मदद करता है:** `setCopyPivotTable(true)` इंजन को सीमित रेंज कॉपी करने पर भी Pivot की परिभाषा डुप्लिकेट करने के लिए मजबूर करता है। इस फ़्लैग के बिना केवल कच्चा डेटा कॉपी होगा और Pivot खो जाएगा।

## चरण 5: लक्ष्य वर्कबुक को सेव करें

अंत में, डुप्लिकेटेड सामग्री को नई फ़ाइल में लिखें।

```java
        // Save the destination workbook to a new file
        dstWb.save("YOUR_DIRECTORY/DuplicatedWithPivot.xlsx");
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर `DuplicatedWithPivot.xlsx` लक्ष्य डायरेक्टरी में बन जाएगा। Excel में फ़ाइल खोलें और आप देखेंगे:

- एक नई वर्कशीट जिसका नाम `Sheet1 (Copy)` (या मूल नाम के साथ “Copy” जोड़ा हुआ) है
- Pivot Table स्रोत शीट जैसा ही दिखेगा और पूरी तरह कार्यशील रहेगा
- यदि आपने वैकल्पिक रेंज कॉपी का उपयोग किया है, तो केवल सेल्स A1:G30 मौजूद होंगे, लेकिन Pivot अभी भी काम करेगा क्योंकि उसका कैश कॉपी किया गया था

## सामान्य प्रश्न और किनारे के मामलों

### पूरी शीट कॉपी किए बिना Pivot को दूसरे वर्कबुक में कैसे कॉपी करें?

यदि आपको केवल Pivot और उसके अंतर्निहित डेटा की आवश्यकता है, तो वह रेंज कॉपी करें जिसमें स्रोत डेटा और Pivot दोनों शामिल हों, फिर `setCopyPivotTable(true)` का उपयोग करें। **चरण 4** का वही कोड लागू होता है; बस यह सुनिश्चित करें कि रेंज डेटा स्रोत को कवर करे।

### यदि स्रोत वर्कबुक में कई वर्कशीट्स हैं जिनमें Pivot हैं तो क्या करें?

आप जिस प्रत्येक वर्कशीट को डुप्लिकेट करना चाहते हैं, उसके लिए **चरण 3** दोहराएँ:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet ws = srcWb.getWorksheets().get(i);
    dstWb.getWorksheets().addCopy(ws);
}
```

### क्या यह संरक्षित (protected) वर्कशीट्स के साथ काम करता है?

Aspose.Cells संरक्षित शीट्स को कॉपी कर सकता है, लेकिन यदि कॉपी के बाद आपको Pivot को संशोधित करना है तो पहले उन्हें अनप्रोटेक्ट करना होगा:

```java
srcWs.unprotect("password");
dstWs.unprotect("password");
```

### क्या मैं Pivot Table को किसी मौजूदा वर्कबुक में कॉपी कर सकता हूँ जिसमें वही नाम की शीट पहले से मौजूद है?

हां। `addCopy` को एक अद्वितीय नाम के साथ उपयोग करें:

```java
Worksheet dstWs = dstWb.getWorksheets().addCopy(srcWs);
dstWs.setName("PivotCopy_" + System.currentTimeMillis());
```

## प्रो टिप: Pivot Cache की जाँच करें

कॉपी करने के बाद, आप प्रोग्रामेटिक रूप से यह पुष्टि कर सकते हैं कि Pivot Cache मौजूद है:

```java
PivotTable pt = dstWs.getPivotTables().get(0);
System.out.println("Pivot cache ID: " + pt.getCacheIndex());
```

यदि Cache ID एक गैर‑नकारात्मक संख्या प्रिंट करती है, तो Pivot सफलतापूर्वक डुप्लिकेट हो गया है।

## निष्कर्ष

अब आप जानते हैं कि Java में **Excel शीट को डुप्लिकेट** कैसे करें जबकि सभी Pivot Table को संरक्षित रखें, **Pivot** टेबल को सीधे कैसे कॉपी करें, **Excel रेंज** को Pivot सहित कैसे कॉपी करें, और Aspose.Cells 25.11+ का उपयोग करके **शीट को Pivot के साथ कॉपी** या **Pivot को वर्कबुक में कॉपी** कैसे करें। इन पैटर्न को रिपोर्ट जेनरेशन को स्वचालित करने, टेम्पलेट क्लोन बनाने, या समान Pivot‑ड्रिवेन एनालिटिक्स की आवश्यकता वाले टेस्टिंग एन्वायरनमेंट बनाने के लिए लागू करें।

और अधिक खोजने के लिए तैयार हैं? डुप्लिकेटेड वर्कबुक को PDF में एक्सपोर्ट करने की कोशिश करें, या कॉपी करने के बाद प्रोग्रामेटिक रूप से Pivot Cache को रिफ्रेश करें ताकि नवीनतम डेटा प्रतिबिंबित हो। Happy coding!

## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ का पता लगा सकें।

- [Java में Worksheet को डुप्लिकेट करें और Pivot Tables को संरक्षित रखें](/cells/english/java/excel-pivot-tables/how-to-duplicate-worksheet-and-preserve-pivot-tables-in-java/)
- [Java में Pivot Table को कॉपी करें – पूर्ण Aspose.Cells गाइड](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Java में रेंज कॉपी करें और Pivot Table को संरक्षित रखें](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}