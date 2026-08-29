---
category: general
date: 2026-08-20
description: Aspose.Cells के साथ Excel तालिका की पंक्ति को कैसे हटाएँ, जबकि तालिका
  की अखंडता को बनाए रखें, सीखें। यह चरण‑दर‑चरण गाइड सुरक्षित पंक्ति हटाने और त्रुटि
  संभालने को दिखाता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to delete excel table row
- delete rows aspose.cells
language: hi
lastmod: 2026-08-20
og_description: Aspose.Cells का उपयोग करके Excel तालिका की पंक्ति कैसे हटाएँ। पंक्तियों
  को सुरक्षित रूप से हटाने और संभावित त्रुटियों को संभालने के लिए इस पूर्ण गाइड का
  पालन करें।
og_image_alt: Screenshot of Java code deleting a row from an Excel table with Aspose.Cells
og_title: Aspose.Cells के साथ Excel तालिका की पंक्ति कैसे हटाएँ
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  headline: How to delete Excel table row safely using Aspose.Cells
  type: TechArticle
- description: Learn how to delete Excel table row with Aspose.Cells while preserving
    table integrity. This step‑by‑step guide shows safe row deletion and error handling.
  name: How to delete Excel table row safely using Aspose.Cells
  steps:
  - name: Why each step matters
    text: 1. **Load the workbook** – `Workbook` reads the `.xlsx` file into memory,
      giving you programmatic access to its sheets, tables, and cells. 2. **Access
      the worksheet** – `getWorksheets().get(0)` selects the first sheet, which is
      where the target table lives. 3. **Retrieve the table** – In Excel, a st
  - name: Expected console output
    text: '*If the deletion is allowed*:'
  - name: Deleting multiple rows
    text: 'To delete three consecutive rows starting at the second data row:'
  - name: Deleting the last data row
    text: 'Attempting to delete the final data row will also raise an exception because
      a table cannot exist without at least one data row. Handle it the same way:'
  type: HowTo
tags:
- Aspose.Cells
- Excel
- Java
title: Aspose.Cells का उपयोग करके Excel तालिका की पंक्ति को सुरक्षित रूप से कैसे हटाएँ
url: /hi/java/tables-structured-references/how-to-delete-excel-table-row-safely-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells का उपयोग करके Excel तालिका पंक्ति को सुरक्षित रूप से कैसे हटाएँ

यदि आपको **how to delete Excel table row** तालिका की संरचना को तोड़े बिना हटाना है, तो यह गाइड Aspose.Cells for Java के साथ एक विश्वसनीय तरीका दिखाता है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो सुरक्षा अपवाद को पकड़ता है और हटाने के प्रयास के बाद वर्कबुक को सहेजता है।

यह ट्यूटोरियल **delete rows aspose.cells** को भी कवर करता है, जो एक‑पंक्ति और बहु‑पंक्ति दोनों परिदृश्यों में काम करता है, ताकि आप कोड को अपने प्रोजेक्ट्स में अनुकूलित कर सकें।

## इस ट्यूटोरियल में क्या कवर किया गया है

* मौजूदा वर्कबुक को लोड करना जिसमें एक Excel तालिका (ListObject) मौजूद है।  
* पहले वर्कशीट और उस शीट पर पहली तालिका तक पहुँच प्राप्त करना।  
* Aspose.Cells द्वारा ऑपरेशन को वैध करने के दौरान पंक्ति हटाने का प्रयास करना।  
* वह अपवाद संभालना जो Aspose.Cells तब फेंकता है जब हटाने से तालिका भ्रष्ट हो जाएगी।  
* सुरक्षित‑हटाने के प्रयास के बाद वर्कबुक को सहेजना।  

पूर्वापेक्षाएँ: Java 17 या उससे नया, Aspose.Cells for Java (संस्करण 23.12 या नया), और Java सिंटैक्स की बुनियादी समझ। अतिरिक्त लाइब्रेरी की आवश्यकता नहीं है।

---

## Aspose.Cells के साथ Excel तालिका पंक्ति को कैसे हटाएँ

नीचे पूरा, स्व-समाहित प्रोग्राम दिया गया है। प्रत्येक चरण की व्याख्या की गई है, और कोड को Java प्रोजेक्ट में कॉपी करके तुरंत चलाया जा सकता है।

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Step 1: Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 3: Retrieve the first table (ListObject) on the worksheet
        ListObject table = worksheet.getListObjects().get(0);

        // Step 4: Attempt to delete a row that would break the table structure
        //         The operation is wrapped in a try‑catch to demonstrate the safety check
        try {
            // Row index is zero‑based; this tries to delete the third data row.
            table.deleteRows(2, 1);
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            // Aspose.Cells throws an exception if the deletion would leave the table invalid.
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Step 5: Save the workbook after the safe‑deletion attempt
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

### प्रत्येक चरण का महत्व

1. **वर्कबुक लोड करें** – `Workbook` `.xlsx` फ़ाइल को मेमोरी में पढ़ता है, जिससे आपको शीट, तालिका और सेल्स तक प्रोग्रामेटिक पहुँच मिलती है।  
2. **वर्कशीट तक पहुँचें** – `getWorksheets().get(0)` पहली शीट चुनता है, जहाँ लक्ष्य तालिका स्थित है।  
3. **तालिका प्राप्त करें** – Excel में संरचित तालिका को `ListObject` द्वारा दर्शाया जाता है। यह ऑब्जेक्ट `deleteRows` जैसी विधियाँ प्रदान करता है।  
4. **सुरक्षित हटाना** – `deleteRows` तालिका की अखंडता जाँचता है। यदि पंक्ति हटाने से तालिका टूटेगी (जैसे हेडर बिना डेटा के रह जाए), तो Aspose.Cells अपवाद फेंकेगा। `try‑catch` ब्लॉक **delete rows aspose.cells** सुरक्षा हैंडलिंग को दर्शाता है।  
5. **वर्कबुक सहेजें** – `workbook.save` परिवर्तन को डिस्क पर लिखता है, जिससे नई फ़ाइल बनती है जो हटाने के प्रयास को दर्शाती है।

### अपेक्षित कंसोल आउटपुट

*यदि हटाना अनुमति है*:

```
Row deleted successfully.
```

*यदि हटाने से तालिका भ्रष्ट होगी* (जब तालिका में केवल एक डेटा पंक्ति बची हो, तब आम):

```
Partial‑deletion prevented: Deleting the specified rows would break the table structure.
```

---

## वर्कबुक लोड करें (चरण 1)

`Workbook` कंस्ट्रक्टर फ़ाइल पाथ स्वीकार करता है। सुनिश्चित करें कि पाथ एक मौजूदा Excel फ़ाइल की ओर इशारा करता है जिसमें कम से कम एक तालिका हो। यदि फ़ाइल नहीं मिलती, तो Aspose.Cells `FileNotFoundException` फेंकेगा, जिसे आप तालिका‑हटाने के अपवाद की तरह ही पकड़ सकते हैं।

```java
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

**टिप:** विकास के दौरान भ्रम से बचने के लिए पूर्ण पाथ (absolute path) का उपयोग करें, विशेषकर जब IDE से चलाया जा रहा हो।

---

## वर्कशीट तक पहुँचें (चरण 2)

एक वर्कबुक में कई वर्कशीट्स हो सकती हैं। उदाहरण में पहली शीट (`index 0`) का उपयोग किया गया है। यदि आपको नाम से किसी विशिष्ट शीट की जरूरत है, तो कॉल को इस प्रकार बदलें:

```java
Worksheet worksheet = workbook.getWorksheets().get("SheetName");
```

---

## तालिका प्राप्त करें (चरण 3)

`ListObject` Excel तालिका को दर्शाता है। यदि वर्कशीट में कोई तालिका नहीं है, तो `getListObjects().size()` `0` लौटाता है, और `get(0)` कॉल करने से `IndexOutOfBoundsException` उत्पन्न होगा। एक रक्षात्मक जाँच इस प्रकार दिखती है:

```java
if (worksheet.getListObjects().getCount() == 0) {
    System.out.println("No tables found on the worksheet.");
    return;
}
ListObject table = worksheet.getListObjects().get(0);
```

---

## Aspose.Cells के साथ पंक्तियों को हटाएँ (चरण 4)

**how to delete Excel table row** का मूल `deleteRows` मेथड है:

```java
table.deleteRows(startIndex, count);
```

* `startIndex` – तालिका के डेटा रेंज के भीतर हटाने वाली पहली पंक्ति का शून्य‑आधारित इंडेक्स।  
* `count` – हटाने वाली पंक्तियों की संख्या।

Aspose.Cells ऑपरेशन को तालिका के हेडर, कुल पंक्तियों और किसी भी फ़ॉर्मूले के विरुद्ध वैध करता है जो तालिका को संदर्भित करते हैं। यदि हटाने से तालिका अमान्य स्थिति में रह जाएगी, तो अपवाद फेंका जाता है, इसलिए `try‑catch` पैटर्न आवश्यक है।

### कई पंक्तियों को हटाना

दूसरी डेटा पंक्ति से शुरू होकर लगातार तीन पंक्तियों को हटाने के लिए:

```java
table.deleteRows(1, 3);
```

### अंतिम डेटा पंक्ति को हटाना

अंतिम डेटा पंक्ति को हटाने का प्रयास भी अपवाद उत्पन्न करेगा क्योंकि तालिका में कम से कम एक डेटा पंक्ति तो होनी ही चाहिए। इसे उसी तरह संभालें:

```java
try {
    table.deleteRows(table.getDataRows().getCount() - 1, 1);
} catch (Exception ex) {
    System.out.println("Cannot delete the last row: " + ex.getMessage());
}
```

---

## वर्कबुक सहेजें (चरण 5)

सुरक्षित‑हटाने के प्रयास के बाद परिवर्तन को स्थायी बनाना सरल है:

```java
workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
```

फ़ाइल एक्सटेंशन बदलकर आप कोई भी समर्थित फ़ॉर्मेट (`.xlsx`, `.xls`, `.csv`, आदि) चुन सकते हैं।

---

## सामान्य गलतियाँ और उन्हें कैसे टालें

| समस्या | कारण | समाधान |
|---------|------|--------|
| **शीट पर कोई तालिका नहीं है** | `getListObjects().get(0)` `IndexOutOfBoundsException` फेंकता है। | एक्सेस करने से पहले `getCount()` जाँचें। |
| **गलत पंक्ति इंडेक्स** | `deleteRows` तालिका के सापेक्ष शून्य‑आधारित इंडेक्स लेता है, वर्कशीट नहीं। | `table.getDataRows().getCount()` प्रिंट करके इंडेक्स सत्यापित करें। |
| **केवल एक डेटा पंक्ति को हटाना** | Aspose.Cells तालिका की अखंडता की रक्षा करता है और अपवाद फेंकता है। | पहले एक प्लेसहोल्डर पंक्ति जोड़ें या पूरी तालिका को `table.remove()` से हटाने का विकल्प चुनें। |
| **फ़ाइल पाथ समस्याएँ** | रिलेटिव पाथ IDE की कार्य निर्देशिका से जुड़ सकते हैं, जिससे `FileNotFoundException` आता है। | पूर्ण पाथ उपयोग करें या IDE की कार्य निर्देशिका को कॉन्फ़िगर करें। |

---

## पूर्ण कार्यशील उदाहरण का सारांश

नीचे पूरा प्रोग्राम फिर से दिया गया है ताकि आप जल्दी कॉपी‑पेस्ट कर सकें। इसमें पहले चर्चा किए गए रक्षात्मक जाँचें शामिल हैं।

```java
import com.aspose.cells.*;

public class SafeTableDeletion {
    public static void main(String[] args) throws Exception {

        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Ensure a table exists
        if (worksheet.getListObjects().getCount() == 0) {
            System.out.println("No tables found on the worksheet.");
            return;
        }

        // Retrieve the first table
        ListObject table = worksheet.getListObjects().get(0);

        // Attempt safe deletion
        try {
            table.deleteRows(2, 1); // zero‑based index
            System.out.println("Row deleted successfully.");
        } catch (Exception ex) {
            System.out.println("Partial‑deletion prevented: " + ex.getMessage());
        }

        // Save the result
        workbook.save("YOUR_DIRECTORY/TableSafeDelete.xlsx");
    }
}
```

इस प्रोग्राम को चलाने पर या तो सफलता संदेश या सुरक्षा अपवाद संदेश प्रदर्शित होगा, और `TableSafeDelete.xlsx` निर्दिष्ट फ़ोल्डर में लिखी जाएगी।

---

## निष्कर्ष

आप अब **how to delete Excel table row** को Aspose.Cells for Java के साथ सुरक्षित रूप से करना जानते हैं। इस गाइड ने वर्कबुक लोड करना, तालिका ढूँढ़ना, संरक्षित पंक्ति हटाना, **delete rows aspose.cells** सुरक्षा अपवाद को संभालना, और अपडेटेड फ़ाइल को सहेजना दिखाया।  

अब आप:

* एक ही कॉल में कई पंक्तियों को हटाएँ।  
* बैच डिलीशन के लिए पंक्ति इंडेक्स की सूची पर इटररेट करें।  
* प्रोडक्शन वातावरण के लिए `try‑catch` को कस्टम लॉगिंग से बदलें।  

विभिन्न तालिका लेआउट, फ़ॉर्मूले और डेटा वैलिडेशन नियमों के साथ प्रयोग करें ताकि देखें कि Aspose.Cells अखंडता को कैसे लागू करता है। जब आपको प्रोग्रामेटिक रूप से Excel फ़ाइलों को बदलना हो, तो यहाँ दिखाया गया पैटर्न एक ठोस, त्रुटि‑सचेत आधार प्रदान करता है।

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Aspose.Cells for .NET के साथ Excel में पंक्तियों को सम्मिलित और हटाने का व्यापक गाइड](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [Aspose.Cells .NET का उपयोग करके Excel में खाली पंक्तियों को हटाना – डेटा सफाई](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)
- [Aspose.Cells .NET में C# का उपयोग करके Excel में कॉलम हटाने का व्यापक गाइड](/cells/english/net/worksheet-management/delete-column-aspose-cells-dotnet-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}