---
category: general
date: 2026-09-18
description: Java में Aspose.Cells के साथ पिवट को डुप्लिकेट कैसे करें – वर्कबुक्स
  के बीच पिवट टेबल को तेज़ और विश्वसनीय तरीके से कॉपी करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy range between workbooks
- how to copy pivot
- copy pivot to workbook
- load excel workbook java
language: hi
lastmod: 2026-09-18
og_description: Aspose.Cells का उपयोग करके Java में पिवट को डुप्लिकेट कैसे करें। इस
  पूर्ण ट्यूटोरियल का पालन करके पिवट टेबल को वर्कबुक्स के बीच साफ़ Java कोड के साथ
  कॉपी करें।
og_image_alt: Screenshot showing a Java IDE copying a pivot table between two Excel
  workbooks
og_title: जावा में पिवट टेबल को डुप्लिकेट करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  headline: How to duplicate pivot in Java using Aspose.Cells
  type: TechArticle
- description: how to duplicate pivot in Java with Aspose.Cells – copy a pivot table
    between workbooks quickly and reliably.
  name: How to duplicate pivot in Java using Aspose.Cells
  steps:
  - name: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
    text: '**Load the source workbook** – this gives you access to the worksheet that
      holds the pivot.'
  - name: '**Define the cell area** that encloses the pivot.'
    text: '**Define the cell area** that encloses the pivot.'
  - name: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
    text: '**Create a destination workbook** – an empty file that will receive the
      copied range.'
  - name: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
    text: '**Copy the range** – Aspose.Cells automatically duplicates the pivot definition.'
  - name: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
    text: '**Save the destination workbook** – you now have a separate file with the
      same pivot.'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells का उपयोग करके जावा में पिवट को डुप्लिकेट कैसे करें
url: /hi/java/excel-pivot-tables/how-to-duplicate-pivot-in-java-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में Aspose.Cells का उपयोग करके पिवट को डुप्लिकेट कैसे करें

यदि आपको Java एप्लिकेशन में **how to duplicate pivot** की आवश्यकता है, तो यह गाइड आपको सटीक चरण दिखाता है। Excel वर्कबुक को लोड करके, पिवट के सेल एरिया को परिभाषित करके, और उस रेंज को नई वर्कबुक में कॉपी करके, आप पिवट टेबल को उसकी परिभाषा या डेटा खोए बिना स्थानांतरित कर सकते हैं।

रिपोर्ट जनरेट करने, विश्लेषण को आर्काइव करने, या बड़ी वर्कबुक को मॉड्यूलर हिस्सों में विभाजित करने के समय पिवट टेबल को कॉपी करना एक सामान्य आवश्यकता है। इस ट्यूटोरियल में आप सीखेंगे कि **copy range between workbooks** कैसे करें, **load Excel workbook Java** कैसे करें, और **how to copy pivot** को सुरक्षित रूप से कैसे लागू किया जाए।

आप एक तैयार‑चलाने योग्य Java प्रोग्राम के साथ समाप्त करेंगे जो Aspose.Cells for Java का उपयोग करके `Source.xlsx` से `PivotCopied.xlsx` तक पिवट टेबल को डुप्लिकेट करता है।

## पूर्वापेक्षाएँ

* JDK 8 या उससे नया स्थापित हो।
* निर्भरताओं को प्रबंधित करने के लिए Maven (या कोई अन्य बिल्ड टूल)।
* Aspose.Cells for Java संस्करण 23.10 या बाद का। अपने `pom.xml` में निम्नलिखित Maven निर्भरता जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier> <!-- adjust classifier to your JDK version -->
</dependency>
```

* एक स्रोत वर्कबुक (`Source.xlsx`) जिसमें रेंज **A1:H30** में पिवट टेबल हो।

## Java में पिवट को डुप्लिकेट कैसे करें

मुख्य विचार सरल है:

1. **Load the source workbook** – यह आपको पिवट रखने वाले वर्कशीट तक पहुंच देता है।
2. **Define the cell area** – वह सेल एरिया जो पिवट को घेरता है।
3. **Create a destination workbook** – एक खाली फ़ाइल जो कॉपी किए गए रेंज को प्राप्त करेगी।
4. **Copy the range** – Aspose.Cells स्वचालित रूप से पिवट परिभाषा को डुप्लिकेट करता है।
5. **Save the destination workbook** – अब आपके पास समान पिवट वाली एक अलग फ़ाइल है।

नीचे एक पूर्ण, चलाने योग्य Java प्रोग्राम है जो इन चरणों का पालन करता है।

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {

    public static void main(String[] args) throws Exception {
        // ---------- Step 1: Load the source workbook ----------
        // Replace the path with the actual location of your source file.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWorkbook = new Workbook(srcPath);
        // The first worksheet (index 0) contains the pivot table.
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // ---------- Step 2: Define the cell area that contains the pivot ----------
        // The pivot occupies A1:H30 in the source sheet.
        CellArea srcRange = CellArea.create("A1", "H30");

        // ---------- Step 3: Create a new workbook for the copy ----------
        Workbook destWorkbook = new Workbook();               // creates a blank workbook
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // ---------- Step 4: Copy the range (pivot table is duplicated automatically) ----------
        // CopyOptions can be left default; it ensures that all formatting and pivot objects are preserved.
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // ---------- Step 5: Save the destination workbook ----------
        String destPath = "YOUR_DIRECTORY/PivotCopied.xlsx";
        destWorkbook.save(destPath);

        System.out.println("Pivot table duplicated successfully to " + destPath);
    }
}
```

### यह क्यों काम करता है

* **Aspose.Cells** पिवट टेबल को वर्कशीट के सेल संग्रह का हिस्सा मानता है। जब आप `copyRange` को कॉल करते हैं, तो लाइब्रेरी केवल सेल मान ही नहीं, बल्कि अंतर्निहित पिवट कैश और परिभाषा भी कॉपी करती है, जिससे नई वर्कबुक में एक पूर्ण कार्यात्मक डुप्लिकेट बनता है।
* `CopyOptions` ऑब्जेक्ट डिफ़ॉल्ट रूप से फ़ॉर्मूले, फ़ॉर्मेट और एम्बेडेड ऑब्जेक्ट्स को संरक्षित रखता है। यदि आपको अतिरिक्त नियंत्रण चाहिए तो आप इसे कस्टमाइज़ कर सकते हैं (उदाहरण के लिए `setCopyColumnWidths(true)`)।

## वर्कबुक्स के बीच रेंज कॉपी करना – गहरा विश्लेषण

उपरोक्त उदाहरण एकल निरंतर ब्लॉक को कॉपी करता है, `copyRange` किसी भी आयताकार क्षेत्र को संभाल सकता है। यदि आपका पिवट गैर‑सन्निहित रेंज में फैला है, तो आप `copyRange` को कई बार कॉल कर सकते हैं या पूरी शीट को डुप्लिकेट करने के लिए `Worksheet.copy` का उपयोग कर सकते हैं।

```java
// Example: copy the whole sheet, preserving all pivots and charts
srcWorksheet.copy(destWorksheet, new CopyOptions());
```

**Tip:** बड़े वर्कबुक्स को कॉपी करते समय, अनावश्यक स्टाइल डुप्लिकेशन से बचने और प्रदर्शन में सुधार के लिए `CopyOptions.setPreserveCellStyle(true)` सक्षम करें।

## वर्कबुक में पिवट कॉपी करना – कई पिवट्स को संभालना

यदि स्रोत शीट में एक से अधिक पिवट हैं, तो आप वर्कशीट की पिवट टेबल्स पर इटररेट करके प्रत्येक को अलग-अलग कॉपी कर सकते हैं:

```java
for (int i = 0; i < srcWorksheet.getPivotTables().getCount(); i++) {
    PivotTable pt = srcWorksheet.getPivotTables().get(i);
    // Determine the range that the pivot occupies
    CellArea pivotArea = pt.getPivotTableArea();
    srcWorksheet.copyRange(pivotArea, destWorksheet, pt.getName() + "!A1", new CopyOptions());
}
```

यह तरीका सुनिश्चित करता है कि प्रत्येक पिवट अपना मूल नाम और डेटा स्रोत बरकरार रखे।

## Excel वर्कबुक Java लोड करना – सामान्य समस्याएँ

* **File path separators:** कोड को प्लेटफ़ॉर्म‑स्वतंत्र रखने के लिए फ़ॉरवर्ड स्लैश (`/`) या `File.separator` का उपयोग करें।
* **Missing license:** Aspose.Cells मूल्यांकन मोड में काम करता है, लेकिन आउटपुट में वॉटरमार्क रहेगा। वर्कबुक लोड करने से पहले `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` के साथ लाइसेंस रजिस्टर करके वॉटरमार्क हटाएँ।
* **Large files:** 100 MB से बड़ी वर्कबुक्स के लिए, मेमोरी उपयोग कम करने हेतु स्ट्रीमिंग विकल्पों के साथ `WorkbookFactory.create(InputStream, new LoadOptions(LoadFormat.XLSX))` उपयोग करने पर विचार करें।

## पूरा अंत‑से‑अंत उदाहरण सारांश

सब कुछ मिलाकर, यहाँ अंतिम प्रोग्राम है जिसे आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं:

```java
package com.example.excelpivot;

import com.aspose.cells.*;

public class DuplicatePivotExample {
    public static void main(String[] args) throws Exception {
        // Load license (optional, removes evaluation watermark)
        // License lic = new License();
        // lic.setLicense("Aspose.Total.Java.lic");

        // 1️⃣ Load source workbook
        Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
        Worksheet srcWorksheet = srcWorkbook.getWorksheets().get(0);

        // 2️⃣ Define pivot range (A1:H30)
        CellArea srcRange = CellArea.create("A1", "H30");

        // 3️⃣ Prepare destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destWorksheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the pivot (Aspose.Cells handles the pivot cache automatically)
        srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/PivotCopied.xlsx");

        System.out.println("Pivot table duplicated successfully.");
    }
}
```

**Expected output:** निष्पादन के बाद, `PivotCopied.xlsx` निर्दिष्ट डायरेक्टरी में दिखाई देगा। इसे Excel में खोलने पर `Source.xlsx` जैसी ही पिवट टेबल लेआउट, फ़िल्टर और डेटा दिखेगा। सभी गणना किए गए फ़ील्ड और फ़ॉर्मेटिंग संरक्षित रहेंगे।

## अक्सर पूछे जाने वाले प्रश्न

* **क्या यह पुराने Excel फ़ॉर्मेट (.xls) के साथ काम करता है?**  
  हाँ। Aspose.Cells स्वचालित रूप से फ़ॉर्मेट का पता लगाता है। `new Workbook("file.xls")` का उपयोग करें और वही कॉपी लॉजिक लागू होता है।

* **यदि पिवट बाहरी डेटा स्रोतों को संदर्भित करता है तो क्या होगा?**  
  कॉपी मूल डेटा स्रोत संदर्भ को बरकरार रखता है। यदि गंतव्य पर्यावरण उस स्रोत तक नहीं पहुँच सकता, तो पिवट `#REF!` त्रुटियाँ दिखाएगा। इसे रोकने के लिए, कॉपी करने के बाद पिवट को रिफ्रेश करें या `PivotTable.setDataSource(...)` के माध्यम से उसका डेटा स्रोत बदलें।

* **क्या मैं पिवट को किसी विशिष्ट शीट नाम पर कॉपी कर सकता हूँ?**  
  बिल्कुल। गंतव्य वर्कशीट बनाने के बाद, उसका नाम बदलें:

  ```java
  destWorksheet.setName("ReportPivot");
  srcWorksheet.copyRange(srcRange, destWorksheet, "A1", new CopyOptions());
  ```

## निष्कर्ष

अब आप Java में Aspose.Cells का उपयोग करके **how to duplicate pivot** टेबल्स, **copy range between workbooks** कैसे करें, और **load Excel workbook Java** के लिए सर्वोत्तम प्रथाएँ जानते हैं। पाँच‑चरणीय प्रक्रिया—लोड, परिभाषित, गंतव्य बनाएं, कॉपी, और सेव—का पालन करके आप रिपोर्ट जनरेशन, विश्लेषण आर्काइव, या जटिल वर्कबुक को बिना पिवट कार्यक्षमता खोए विभाजित कर सकते हैं।

अगला, **copy pivot to workbook** जैसे संबंधित विषयों का अन्वेषण करें, जिसमें कई शीट्स हों, या गैर‑Aspose परिदृश्यों के लिए Apache POI का उपयोग करके डुप्लिकेट पिवट को बड़े डेटा‑प्रोसेसिंग पाइपलाइन में एकीकृत करें। बड़े वर्कबुक्स के लिए प्रदर्शन को बेहतर बनाने हेतु विभिन्न `CopyOptions` सेटिंग्स के साथ प्रयोग करें।

कोडिंग का आनंद लें!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों की खोज करने में मदद करेंगे।

- [Aspose.Cells for Java का उपयोग करके Excel में पिवट टेबल्स कैसे बनाएं&#58; एक व्यापक गाइड](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Aspose.Cells for Java के साथ Excel पिवट टेबल स्रोत को कैसे अपडेट करें&#58; एक व्यापक गाइड](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java का उपयोग करके Excel वर्कबुक्स में पिवट फ़ील्ड्स को समूहित करना - व्यापक गाइड](/cells/english/java/data-analysis/aspose-cells-java-group-pivot-fields-excel-workbook/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}