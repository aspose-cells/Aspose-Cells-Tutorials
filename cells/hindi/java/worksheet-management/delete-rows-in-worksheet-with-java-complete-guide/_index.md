---
category: general
date: 2026-06-18
description: Aspose.Cells for Java का उपयोग करके वर्कशीट में पंक्तियों को हटाएँ। सीखें
  कि टेबल हेडर पंक्ति को कैसे हटाएँ और Excel टेबल से पंक्तियों को सुरक्षित रूप से
  कैसे हटाएँ।
draft: false
keywords:
- delete rows in worksheet
- remove table header row
- remove rows from excel table
language: hi
og_description: Aspose.Cells for Java के साथ वर्कशीट में पंक्तियों को हटाएँ। यह गाइड
  दिखाता है कि तालिका की हेडर पंक्ति को कैसे हटाएँ और Excel तालिका से पंक्तियों को
  प्रभावी ढंग से कैसे हटाएँ।
og_title: जावा के साथ वर्कशीट में पंक्तियों को हटाएँ – चरण-दर-चरण
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  headline: Delete rows in worksheet with Java – Complete Guide
  type: TechArticle
- description: Delete rows in worksheet using Aspose.Cells for Java. Learn how to
    remove table header row and delete rows from Excel table safely.
  name: Delete rows in worksheet with Java – Complete Guide
  steps:
  - name: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
    text: '`table.unlist()` strips the table metadata, turning the block into ordinary
      cells.'
  - name: With the header now a regular row, `deleteRows(0, …)` works without complaints.
    text: With the header now a regular row, `deleteRows(0, …)` works without complaints.
  - name: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
    text: If you still need a table after the cleanup, you can recreate it using `ws.getTables().add(...)`.
  - name: Loads a workbook.
    text: Loads a workbook.
  - name: Checks if the first table exists.
    text: Checks if the first table exists.
  - name: Deletes **all** rows *including* the header safely.
    text: Deletes **all** rows *including* the header safely.
  - name: Re‑creates the table from the remaining rows (if any).
    text: Re‑creates the table from the remaining rows (if any).
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Worksheet
title: जावा के साथ वर्कशीट में पंक्तियों को हटाएँ – पूर्ण गाइड
url: /hi/java/worksheet-management/delete-rows-in-worksheet-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# वर्कशीट में पंक्तियों को हटाएँ – पूर्ण जावा ट्यूटोरियल

क्या आपको **वर्कशीट में पंक्तियों को हटाने** की ज़रूरत पड़ी है लेकिन टेबल हेडर हटाने से रोकता है? आप अकेले नहीं हैं। कई Excel ऑटोमेशन परिदृश्यों में पहली पंक्ति एक संरचित टेबल की होती है, और `deleteRows` को एक साधारण कॉल करने से अपवाद उत्पन्न हो सकता है या हेडर अपरिवर्तित रह जाता है।  

इस ट्यूटोरियल में हम ठीक‑ठीक बताएँगे कि *टेबल हेडर पंक्ति को कैसे हटाएँ* और *Excel टेबल से पंक्तियों को कैसे हटाएँ* बिना शीट को तोड़े। अंत तक आपके पास एक साफ़, चलने योग्य स्निपेट होगा जो नवीनतम Aspose.Cells for Java (लेखन के समय v23.10) के साथ काम करता है।  

हम आवश्यकताओं, तीन व्यावहारिक दृष्टिकोणों, और कुछ टिप्स को कवर करेंगे जिन्हें आप बुकमार्क करना चाहेंगे। कोई फालतू नहीं—सिर्फ वही उत्तर जो एक अनुभवी डेवलपर कॉफ़ी के साथ देता है।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

- Java 17 या नया (कोड पुराने संस्करणों के साथ भी संकलित हो सकता है, लेकिन 17 की सिफारिश की जाती है)।
- Aspose.Cells for Java 23.10 या बाद का संस्करण, जिसे अपने Maven `pom.xml` में जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
</dependency>
```

- एक नमूना Excel फ़ाइल (`Sample.xlsx`) जिसमें पहले वर्कशीट पर एक टेबल हो। टेबल का हेडर पंक्ति 0 (Excel पंक्ति 1) में स्थित है।

बस इतना ही। तैयार हैं? चलिए शुरू करते हैं।

## वर्कशीट में पंक्तियों को हटाएँ – हेडर पंक्ति क्यों महत्वपूर्ण है

जब आप कॉल करते हैं:

```java
ws.getCells().deleteRows(0, 2, true);
```

Aspose.Cells पंक्ति 0 को हटाने से इनकार करता है क्योंकि वह **टेबल** का हिस्सा है। API टेबल की अखंडता की रक्षा करता है; हेडर हटाने से डेटा पंक्तियाँ अनाथ हो जाएँगी। आपको जो अपवाद मिलेगा वह कुछ इस प्रकार होगा *“The specified row belongs to a table and cannot be deleted.”*  

इस सुरक्षा तंत्र को समझना सफल समाधान की पहली कदम है।

## दृष्टिकोण 1 – हेडर के **नीचे** पंक्तियों को हटाएँ (सबसे आम)

यदि आप केवल डेटा को साफ़ करना चाहते हैं जबकि टेबल संरचना बनी रहे, तो हेडर के **बाद** पंक्ति से हटाना शुरू करें।

```java
import com.aspose.cells.*;

public class DeleteRowsBelowHeader {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Determine how many data rows the table currently has
        Table table = ws.getTables().get(0);
        int dataRowCount = table.getDataRange().getRowCount();

        // Delete all data rows (keep header)
        // startRow = 1 because row index 0 is the header
        ws.getCells().deleteRows(1, dataRowCount, true);

        // Save the result
        wb.save("Result_DeleteRowsBelowHeader.xlsx");
    }
}
```

**यह क्यों काम करता है:** `deleteRows` को प्रारंभिक इंडेक्स 1 दिया जाता है, इसलिए हेडर अपरिवर्तित रहता है। `true` फ़्लैग शेष पंक्तियों को ऊपर शिफ्ट करता है, जिससे उन पर निर्भर फ़ॉर्मूले सुरक्षित रहते हैं। कोड चलाने के बाद आपको केवल हेडर पंक्ति वाली साफ़ टेबल दिखेगी।

### त्वरित टिप

यदि आपको *विशिष्ट* पंक्तियों की रेंज (जैसे, पंक्तियाँ 5‑10) हटानी है, तो बस प्रारंभिक इंडेक्स और गिनती को तदनुसार समायोजित करें। टेबल स्वचालित रूप से नए डेटा रेंज के अनुसार आकार बदल लेगा।

## दृष्टिकोण 2 – टेबल को साधारण रेंज में बदलें, फिर हटाएँ

कभी‑कभी आपको **टेबल हेडर पंक्ति को हटाना** और डेटा को सामान्य रेंज के रूप में मानना आवश्यक होता है। ट्रिक यह है कि पहले टेबल को *अनलिस्ट* कर दें।

```java
import com.aspose.cells.*;

public class RemoveHeaderAndDeleteRows {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // 1️⃣ Unlist the table – it becomes a normal range
        table.unlist();

        // 2️⃣ Now you can delete the header row (row 0) and any other rows
        // Delete header + first two data rows (total 3 rows)
        ws.getCells().deleteRows(0, 3, true);

        // 3️⃣ (Optional) Re‑create a table from the remaining data
        // Assuming you still have data starting at row 0
        int firstDataRow = 0;
        int lastDataRow = ws.getCells().getMaxDataRow();
        int firstCol = ws.getCells().getMaxDataColumn();
        int lastCol = ws.getCells().getMaxDataColumn();

        String range = new CellArea(firstDataRow, 0, lastDataRow, firstCol).format();
        ws.getTables().add(range, true);
        ws.getTables().get(0).setName("NewTable");

        wb.save("Result_RemoveHeaderAndDeleteRows.xlsx");
    }
}
```

**व्याख्या:**  

1. `table.unlist()` टेबल मेटाडेटा को हटाता है, ब्लॉक को सामान्य सेल्स में बदल देता है।  
2. हेडर अब सामान्य पंक्ति बन गया है, इसलिए `deleteRows(0, …)` बिना किसी शिकायत के काम करता है।  
3. यदि सफ़ाई के बाद आपको फिर से टेबल चाहिए, तो आप `ws.getTables().add(...)` से इसे पुनः बना सकते हैं।

यह दृष्टिकोण तब उपयोगी है जब हेडर स्वयं गलत हो या आप पूरी टेबल परिभाषा को बदलना चाहते हों।

## दृष्टिकोण 3 – टेबल API का उपयोग करके विशिष्ट पंक्तियों को हटाएँ

Aspose.Cells एक **टेबल‑स्तरीय** मेथड भी प्रदान करता है पंक्तियों को हटाने के लिए, जो स्वचालित रूप से हेडर सुरक्षा को संभालता है।

```java
import com.aspose.cells.*;

public class DeleteRowsViaTableAPI {
    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);
        Table table = ws.getTables().get(0);

        // Delete the first two data rows (index 0 = first data row, not the header)
        // The Table API counts only data rows, so we don't touch the header.
        table.deleteRows(0, 2);

        wb.save("Result_DeleteRowsViaTableAPI.xlsx");
    }
}
```

**आप इसे क्यों चुन सकते हैं:** यह सबसे *सार्थक* तरीका है—आप टेबल को बता रहे हैं, “मेरी डेटा पंक्तियों को हटाओ।” API टेबल की रेंज को स्वचालित रूप से अपडेट करता है, और आपको कच्चे पंक्ति इंडेक्स के साथ छेड़छाड़ नहीं करनी पड़ती।

## किनारे के मामलों और सामान्य गलतियों

| स्थिति | ध्यान रखने योग्य बात | सुझाया गया समाधान |
|-----------|------------------|-----------------|
| **एक ही शीट पर कई टेबल** | `ws.getTables().get(0)` गलत टेबल को लक्षित कर सकता है। | `ws.getTables().stream().filter(t -> t.getName().equals("MyTable")).findFirst().orElse(null)` का उपयोग करें |
| **हेडर में मर्ज्ड सेल्स** | पंक्तियों को हटाने से मर्ज्ड एरिया टूट सकते हैं, जिससे लेआउट गड़बड़ हो सकता है। | हटाने से पहले अनमर्ज करें: `ws.getCells().get("A1").getMergedRange().unmerge();` |
| **हेडर को संदर्भित करने वाले फ़ॉर्मूले** | हेडर हटाने से बाहरी रेफ़रेंसेज़ टूट जाएँगी। | हटाने के बाद फ़ॉर्मूले अपडेट करें या एक प्लेसहोल्डर पंक्ति रखें। |
| **बड़ी वर्कशीट (>10 000 पंक्तियाँ)** | `deleteRows` आंतरिक शिफ्टिंग के कारण धीमा हो सकता है। | यदि शिफ्टिंग की ज़रूरत नहीं है तो `ws.getCells().clearRows(start, count)` उपयोग करें |

## पूर्ण कार्यशील उदाहरण – सभी तरीकों का संयोजन

नीचे एक स्व-निहित प्रोग्राम है जो:

1. एक वर्कबुक लोड करता है।  
2. जाँचता है कि पहली टेबल मौजूद है या नहीं।  
3. **सभी** पंक्तियों *हेडर सहित* को सुरक्षित रूप से हटाता है।  
4. शेष पंक्तियों से (यदि कोई बची हो) टेबल को पुनः बनाता है।

```java
import com.aspose.cells.*;

public class DeleteRowsInWorksheetFullDemo {
    public static void main(String[] args) throws Exception {
        // ① Load the workbook
        Workbook wb = new Workbook("Sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // ② Guard: make sure a table is present
        if (ws.getTables().getCount() == 0) {
            System.out.println("No tables found – nothing to delete.");
            return;
        }

        // ③ Grab the first table (adjust if you have a named table)
        Table table = ws.getTables().get(0);

        // ④ Unlist so we can delete the header row
        table.unlist();

        // ⑤ Determine total rows to delete (header + data)
        int totalRows = table.getRange().getRowCount(); // includes header
        ws.getCells().deleteRows(0, totalRows, true);

        // ⑥ If there are still rows left, rebuild the table
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();

        if (maxRow >= 0) { // there is at least one row left
            String newRange = new CellArea(0, 0, maxRow, maxCol).format();
            Table newTable = ws.getTables().add(newRange, true);
            newTable.setName("RebuiltTable");
        }

        // ⑦ Save the result
        wb.save("Result_DeleteRowsInWorksheetFullDemo.xlsx");
        System.out.println("Rows deleted and table rebuilt successfully.");
    }
}
```

**अपेक्षित आउटपुट:** निष्पादन के बाद आपको `Result_DeleteRowsInWorksheetFullDemo.xlsx` मिलेगा जिसमें मूल टेबल हटाया गया होगा, और यदि कोई डेटा बचा है तो `RebuiltTable` नाम की नई टेबल बनेगी। कंसोल पर एक संक्षिप्त सफलता संदेश प्रदर्शित होगा।

## दृश्य सारांश

![Excel worksheet before and after deleting rows](https://example.com/images/delete-rows-workbook.png "Before and after deleting rows in worksheet")

*Alt text:* “वर्कशीट में पंक्तियों को हटाने से पहले और बाद – हेडर हटाया गया, डेटा पंक्तियाँ साफ़ हो गईं।”

## निष्कर्ष

हमने तीन भरोसेमंद तरीकों को कवर किया है **वर्कशीट में पंक्तियों को हटाने** के लिए, जबकि जटिल *टेबल हेडर पंक्ति हटाने* परिदृश्य को संभालते हुए सुरक्षित रूप से **Excel टेबल से पंक्तियों को हटाने** का तरीका बताया। चाहे आप कच्ची सेल ऑपरेशन्स, Table API, या पूर्ण अनलिस्ट‑रिलिस्ट चक्र पसंद करें, ऊपर दिए गए कोड स्निपेट्स आपके प्रोजेक्ट में सीधे उपयोग के लिए तैयार हैं।  

अगला कदम? इन तकनीकों को शर्तीय लॉजिक के साथ मिलाएँ—केवल तब पंक्तियों को हटाएँ जब किसी विशेष कॉलम में “Inactive” हो, या कई फ़ाइलों को बैच‑प्रोसेस करें।

## आप अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट संबंधी विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में महारत हासिल कर सकें और अपने प्रोजेक्ट में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Efficient Row Management in Excel using Aspose.Cells for Java&#58; Insert and Delete Rows](/cells/english/java/worksheet-management/aspose-cells-java-row-operations-excel/)
- [How to Remove Blank Rows from Excel Files using Aspose.Cells for Java](/cells/english/java/data-manipulation/delete-blank-rows-aspose-cells-java/)
- [How to Delete Rows in Excel Using Aspose.Cells for Java | Guide & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}