---
category: general
date: 2026-08-14
description: Aspose.Cells का उपयोग करके जावा में वर्कबुक्स के बीच रेंज कॉपी करें।
  पिवट टेबल वर्कबुक को कॉपी करना, चित्र को PowerPoint में निर्यात करना और Excel टेबल
  से AutoFilter हटाना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy range between workbooks
- copy pivot table workbook
- export picture to powerpoint
- copy excel range to new workbook
- remove autofilter from excel table
language: hi
lastmod: 2026-08-14
og_description: जावा में वर्कबुक्स के बीच रेंज कॉपी करें। यह गाइड दिखाता है कि पिवट
  टेबल वर्कबुक को कैसे कॉपी करें, चित्र को पावरपॉइंट में निर्यात करें और एक्सेल टेबल
  से ऑटोफ़िल्टर हटाएँ।
og_image_alt: Screenshot of Java code copying range between workbooks with Aspose.Cells
og_title: जावा में वर्कबुक्स के बीच रेंज कॉपी करें – पूर्ण Aspose.Cells ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Copy range between workbooks with Java using Aspose.Cells. Learn to
    copy pivot table workbook, export picture to PowerPoint and remove AutoFilter
    from Excel table.
  headline: Copy range between workbooks in Java – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: जावा में वर्कबुक्स के बीच रेंज कॉपी करें – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/java/range-management/copy-range-between-workbooks-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में वर्कबुक्स के बीच रेंज कॉपी करना – चरण‑दर‑चरण गाइड

यदि आपको Java में **वर्कबुक्स के बीच रेंज कॉपी** करनी है, तो Aspose.Cells एक साफ़ API प्रदान करता है जो पिवट टेबल और चित्र जैसी जटिल वस्तुओं को संभालता है। यह ट्यूटोरियल दिखाता है कि कैसे **पिवट टेबल वर्कबुक कॉपी** करें, **चित्र को PowerPoint में एक्सपोर्ट** करें, और **Excel टेबल से AutoFilter हटाएँ** जबकि कोड को पढ़ने और बनाए रखने में आसान रखें।

आप सीखेंगे कि:

* स्रोत वर्कबुक लोड करें और स्रोत रेंज निर्धारित करें।  
* एक गंतव्य वर्कबुक बनाएं और रेंज कॉपी करें ताकि पिवट टेबल अपरिवर्तित रहे।  
* शीट पर पहला चित्र एक संपादन योग्य PowerPoint ऑब्जेक्ट के रूप में एक्सपोर्ट करें।  
* पहले Excel टेबल से AutoFilter हटाएँ।  
* `SmartMarkerOptions` के साथ एक वर्कबुक लोड करें ताकि JSON एरे को एकल सेल मान के रूप में माना जा सके।

उदाहरण में Aspose.Cells 23.10 for Java का उपयोग किया गया है, लेकिन अवधारणाएँ पहले के संस्करणों पर भी लागू होती हैं।

---

## Prerequisites

| आवश्यकता | क्यों महत्वपूर्ण है |
|-----------|-------------------|
| Java 17 या नया | नवीनतम Aspose.Cells रनटाइम द्वारा आवश्यक। |
| Aspose.Cells for Java (Maven आर्टिफैक्ट `com.aspose:aspose-cells`) | कोड में उपयोग किए गए `Workbook`, `Worksheet`, `Range` और संबंधित क्लासेज़ प्रदान करता है। |
| एक स्रोत Excel फ़ाइल (`src.xlsx`) जिसमें पिवट टेबल, चित्र, और AutoFilter वाला टेबल हो। | ट्यूटोरियल इन वस्तुओं को हेरफेर करके प्रत्येक सुविधा को प्रदर्शित करता है। |

अपने `pom.xml` में Maven निर्भरता जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Copy range between workbooks – load source and destination

पहला कदम स्रोत वर्कबुक खोलना, वह रेंज चुनना है जिसमें वह डेटा हो जिसे आप कॉपी करना चाहते हैं, और एक खाली गंतव्य वर्कबुक बनाना है।

```java
import com.aspose.cells.*;

public class CopyRangeDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that holds the pivot table, picture, and table.
        Workbook sourceWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceWs = sourceWb.getWorksheets().get(0);

        // Define the range that includes the pivot table (A1:G20 in this example).
        Range sourceRange = sourceWs.getCells().createRange("A1:G20");

        // Create a new workbook that will receive the copied range.
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);
        Range destRange = destWs.getCells().createRange("A1");
```

> **Why this matters:** By using `Range.copy`, Aspose.Cells copies not only raw cell values but also the underlying pivot cache, keeping the pivot table functional in the destination workbook.

> **यह क्यों महत्वपूर्ण है:** `Range.copy` का उपयोग करके, Aspose.Cells न केवल कच्चे सेल मान कॉपी करता है बल्कि अंतर्निहित पिवट कैश भी कॉपी करता है, जिससे पिवट टेबल गंतव्य वर्कबुक में कार्यात्मक बनी रहती है।

---

## Copy pivot table workbook while copying the range

अब परिभाषित रेंज को स्रोत वर्कबुक से गंतव्य वर्कबुक में कॉपी करें। पिवट टेबल स्वचालित रूप से संरक्षित रहती है क्योंकि रेंज में पिवट कैश शामिल है।

```java
        // Copy the source range to the destination range.
        destRange.copy(sourceRange);

        // Save the intermediate workbook to verify that the pivot table was copied.
        destWb.save("YOUR_DIRECTORY/destination.xlsx");
```

> **Result:** Opening `destination.xlsx` shows the same pivot table layout as `src.xlsx`. No additional code is required to rebuild the pivot cache.

> **परिणाम:** `destination.xlsx` खोलने पर वही पिवट टेबल लेआउट दिखता है जो `src.xlsx` में था। पिवट कैश को पुनः बनाने के लिए अतिरिक्त कोड की आवश्यकता नहीं है।

---

## Export picture to PowerPoint

Aspose.Cells एक चित्र को संपादन योग्य PowerPoint ऑब्जेक्ट के रूप में एक्सपोर्ट करने के लिए चिह्नित कर सकता है। नीचे दिया गया कोड गंतव्य शीट पर पहला चित्र चुनता है और एक्सपोर्ट फ़्लैग सेट करता है।

```java
        // Retrieve the first picture on the destination sheet.
        Shape picture = destWs.getPictures().get(0);

        // Instruct Aspose.Cells to export this picture as a PowerPoint object.
        picture.getPictureFormat().setExportToPptx(true);

        // Optionally, save the workbook as PPTX to see the result.
        destWb.save("YOUR_DIRECTORY/destination.pptx");
```

> **What you see:** Opening `destination.pptx` in PowerPoint shows the picture as a native shape that you can edit, resize, or animate.

> **जो आप देखते हैं:** PowerPoint में `destination.pptx` खोलने पर चित्र एक मूल आकार (shape) के रूप में दिखता है जिसे आप संपादित, आकार बदल या एनीमेट कर सकते हैं।

---

## Remove AutoFilter from Excel table

यदि स्रोत शीट में AutoFilter वाला टेबल है, तो कॉपी करने के बाद आप इसे साफ़ करना चाह सकते हैं। नीचे दिया गया कोड पहले टेबल तक पहुँचता है और उसका फ़िल्टर हटाता है।

```java
        // Access the first table on the destination sheet.
        Table table = destWs.getTables().get(0);

        // Remove the AutoFilter by assigning null.
        table.setAutoFilter(null);

        // Save the final workbook.
        destWb.save("YOUR_DIRECTORY/final_output.xlsx");
```

> **Effect:** The table remains in the workbook, but the drop‑down filter arrows disappear, giving you a clean data view.

> **प्रभाव:** टेबल वर्कबुक में बना रहता है, लेकिन ड्रॉप‑डाउन फ़िल्टर तीर गायब हो जाते हैं, जिससे आपको एक साफ़ डेटा दृश्य मिलता है।

---

## Load workbook with SmartMarker options – treat JSON arrays as a single cell

जब आप JSON से रिपोर्ट बनाते हैं, तो Aspose.Cells पूरी एरे को एकल सेल मान के रूप में ले सकता है। यह टेम्पलेट में JSON स्ट्रिंग को कई सेल्स में विस्तारित किए बिना एम्बेड करने के लिए उपयोगी है।

```java
        // Configure LoadOptions to enable SmartMarker array handling.
        LoadOptions loadOptions = new LoadOptions();
        SmartMarkerOptions smOptions = new SmartMarkerOptions();
        smOptions.setArrayAsSingle(true);
        loadOptions.setSmartMarkerOptions(smOptions);

        // Load a template workbook using the configured options.
        Workbook smartMarkerWb = new Workbook("YOUR_DIRECTORY/template.xlsx", loadOptions);

        // Continue processing (e.g., populate markers) as needed.
        // ...

        // Save the processed workbook.
        smartMarkerWb.save("YOUR_DIRECTORY/template_filled.xlsx");
    }
}
```

> **Why you might use this:** If your JSON payload contains an array that should appear as a JSON string in a single cell, `setArrayAsSingle(true)` prevents Aspose.Cells from expanding the array into separate rows or columns.

> **आप इसे क्यों उपयोग कर सकते हैं:** यदि आपके JSON पेलोड में ऐसी एरे है जिसे एकल सेल में JSON स्ट्रिंग के रूप में दिखना चाहिए, तो `setArrayAsSingle(true)` Aspose.Cells को एरे को अलग‑अलग पंक्तियों या कॉलमों में विस्तारित करने से रोकता है।

---

![Copy range between workbooks in Java – Aspose.Cells code example](copy-range-workbooks.png)

*छवि वैकल्पिक पाठ:* **Java में वर्कबुक्स के बीच रेंज कॉपी – Aspose.Cells कोड उदाहरण** (मुख्य कीवर्ड से मेल खाता है)।

---

## Expected output

| फ़ाइल नाम                | सामग्री |
|--------------------------|----------|
| `destination.xlsx`       | कार्यात्मक पिवट टेबल के साथ कॉपी किया गया रेंज। |
| `destination.pptx`       | संपादन योग्य PowerPoint आकार के रूप में एक्सपोर्ट किया गया चित्र। |
| `final_output.xlsx`      | AutoFilter तीरों के बिना टेबल। |
| `template_filled.xlsx`   | एकल सेल मान के रूप में संग्रहीत JSON एरे। |

प्रत्येक फ़ाइल को उपयुक्त एप्लिकेशन (Excel या PowerPoint) में खोलें ताकि यह सत्यापित किया जा सके कि ऑपरेशन सफल रहा।

---

## Conclusion

आप अब जानते हैं कि Aspose.Cells का उपयोग करके Java में **वर्कबुक्स के बीच रेंज कॉपी** कैसे करें, जबकि पिवट टेबल को संरक्षित रखें, चित्र को PowerPoint में एक्सपोर्ट करें, और Excel टेबल से AutoFilter हटाएँ। वही पैटर्न किसी भी Excel रेंज को नई वर्कबुक में कॉपी करने, SmartMarker JSON एरे को संभालने, या अतिरिक्त ट्रांसफ़ॉर्मेशन को चेन करने के लिए विस्तारित किया जा सकता है।

अगले कदम जिन्हें आप अन्वेषण कर सकते हैं:

* **एक्सेल रेंज को नई वर्कबुक** में कई शीट्स के साथ कॉपी करें।  
* बैच इमेज एक्सट्रैक्शन के लिए **चित्र को PowerPoint में एक्सपोर्ट** का उपयोग करें।  
* बड़े रिपोर्टिंग पाइपलाइन में **Excel टेबल से autofilter हटाएँ**।  
* पूर्ण Excel‑to‑PowerPoint ऑटोमेशन के लिए इन तकनीकों को Aspose.Slides के साथ संयोजित करें।

विभिन्न रेंज एड्रेस, कई पिवट टेबल, या कस्टम चित्र फ़ॉर्मेट के साथ प्रयोग करने में संकोच न करें। Aspose.Cells API प्रोग्रामेटिक लचीलापन प्रदान करने के लिए डिज़ाइन किया गया है, इसलिए आप यहाँ दिखाए गए पैटर्न को किसी भी एंटरप्राइज़ Excel ऑटोमेशन परिदृश्य में अनुकूलित कर सकते हैं।

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells for Java का उपयोग करके Excel में शीट्स के बीच चित्र कॉपी करना: एक व्यापक गाइड](/cells/english/java/images-shapes/copy-images-between-sheets-excel-aspose-cells-java/)
- [Aspose.Cells Java का उपयोग करके Excel में वर्कशीट्स के बीच पेज सेटअप सेटिंग्स कॉपी करना](/cells/english/java/headers-footers/copy-page-setup-excel-aspose-cells-java/)
- [वर्कबुक्स के बीच Excel वर्कशीट कॉपी करना](/cells/english/net/excel-copy-worksheet/excel-copy-worksheets-between-workbooks/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}