---
category: general
date: 2026-10-16
description: Aspose.Cells के साथ जावा में पिवट टेबल कैसे कॉपी करें – रेंज को दूसरे
  शीट में कॉपी करना और वर्कशीट्स के बीच रेंज को कुशलतापूर्वक कॉपी करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to another sheet
- copy range between worksheets
language: hi
lastmod: 2026-10-16
og_description: जावा में Aspose.Cells का उपयोग करके पिवट टेबल कैसे कॉपी करें। यह ट्यूटोरियल
  आपको दिखाता है कि रेंज को दूसरे शीट में कैसे कॉपी करें और वर्कशीट्स के बीच रेंज
  को कैसे कॉपी करें, पूर्ण कोड के साथ।
og_image_alt: Diagram illustrating how to copy pivot table from one worksheet to another
  in Java
og_title: जावा में वर्कशीट्स के बीच पिवट टेबल कैसे कॉपी करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  headline: How to copy a pivot table between worksheets in Java
  type: TechArticle
- description: How to copy pivot table in Java with Aspose.Cells – learn to copy range
    to another sheet and copy range between worksheets efficiently.
  name: How to copy a pivot table between worksheets in Java
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Locate the source range that contains the pivot table
    text: '```java // The first worksheet (index 0) holds the pivot table. Worksheet
      sourceSheet = workbook.getWorksheets().get(0);'
  - name: Define the destination range on another sheet
    text: '```java // The second worksheet (index 1) will receive the copied pivot
      table. Worksheet destSheet = workbook.getWorksheets().get(1);'
  - name: Copy the source range while preserving the pivot table
    text: '```java // Configure copy options to keep all formatting, formulas, and
      pivot data. CopyOptions copyOptions = new CopyOptions(); copyOptions.setPasteType(PasteType.PASTE_ALL);
      // copies everything copyOptions.setSkipEmptyRows(false); copyOptions.setSkipEmptyColumns(false);'
  - name: Save the workbook and verify the result
    text: '```java // Save the modified workbook to a new file. workbook.save("output.xlsx");
      System.out.println("Pivot table copied successfully."); } } ```'
  type: HowTo
tags:
- Aspose.Cells
- Java
- PivotTable
- Excel automation
title: जावा में वर्कशीट्स के बीच पिवट टेबल कैसे कॉपी करें
url: /hi/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में वर्कशीट्स के बीच पिवट टेबल कॉपी कैसे करें

यदि आपको एक ही वर्कबुक में एक शीट से दूसरी शीट पर **पिवट टेबल कॉपी करने का तरीका** चाहिए, तो यह गाइड एक पूर्ण, तैयार‑से‑चलाने वाला समाधान प्रदान करता है। आप देखेंगे कि पिवट टेबल वाले स्रोत रेंज को कैसे कॉपी किया जाए, उसकी कार्यक्षमता को कैसे बनाए रखा जाए, और परिणाम को कैसे सत्यापित किया जाए—सभी Aspose.Cells for Java का उपयोग करके।

पिवट टेबल को कॉपी करना एक सामान्य कार्य है जब आप प्रोग्रामेटिक रूप से रिपोर्ट बनाते हैं, और इसे सही तरीके से करने से पिवट कैश खोने या फ़ॉर्मूले टूटने से बचा जा सकता है। इस ट्यूटोरियल के अंत तक आप **रेंज को दूसरी शीट पर कॉपी** और **वर्कशीट्स के बीच रेंज कॉपी** बिना किसी मैनुअल कदम के कर सकेंगे।

## आप क्या सीखेंगे

* एक मौजूदा Excel फ़ाइल जिसमें पिवट टेबल है, लोड करें।
* पिवट टेबल को रखने वाली स्रोत रेंज को परिभाषित करें।
* एक अलग वर्कशीट पर गंतव्य रेंज को परिभाषित करें।
* `CopyOptions` का उपयोग करके पिवट टेबल को अपरिवर्तित रखें।
* सत्यापित करें कि कॉपी किया गया पिवट टेबल अपेक्षित रूप से काम करता है।

**पूर्वापेक्षाएँ**

* Java 17 या बाद का संस्करण।
* Aspose.Cells for Java (संस्करण 23.12 या नया)।  
* एक Excel फ़ाइल (`input.xlsx`) जिसमें पहली शीट पर पिवट टेबल है।

---

## Aspose.Cells के साथ पिवट टेबल कॉपी कैसे करें

ऑपरेशन का मूल चार‑स्टेप प्रक्रिया है: वर्कबुक लोड करना, स्रोत रेंज को ढूँढ़ना, गंतव्य रेंज सेट करना, और कॉपी करना। नीचे प्रत्येक चरण को विस्तार से समझाया गया है।

### चरण 1: वर्कबुक लोड करें

```java
import com.aspose.cells.*;

public class CopyPivotTableExample {
    public static void main(String[] args) throws Exception {
        // Load the workbook that contains the original pivot table
        Workbook workbook = new Workbook("input.xlsx");
```

*इस चरण की आवश्यकता क्यों है?*  
वर्कबुक लोड करने से पूरी फ़ाइल मेमोरी में आ जाती है, जिससे आपको वर्कशीट्स, सेल्स और पिवट कैश तक पहुँच मिलती है। Aspose.Cells फ़ाइल फ़ॉर्मेट को स्वचालित रूप से पढ़ता है, इसलिए आपको `.xls` बनाम `.xlsx` की चिंता नहीं करनी पड़ती।

### चरण 2: पिवट टेबल वाली स्रोत रेंज को ढूँढ़ें

```java
        // The first worksheet (index 0) holds the pivot table.
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // Define the exact area that includes the pivot table.
        // Adjust the address if your pivot table spans a different range.
        Range sourceRange = sourceSheet.getCells().createRange("A1:G20");
```

*इस चरण की आवश्यकता क्यों है?*  
पिवट टेबल एक सेल ब्लॉक में संग्रहीत होती है जो एक छिपे हुए कैश को भी संदर्भित करता है। सटीक रेंज (`A1:G20` इस उदाहरण में) चुनकर आप सुनिश्चित करते हैं कि रेंज कॉपी होने पर कैश लिंक बना रहे।

### चरण 3: दूसरी शीट पर गंतव्य रेंज को परिभाषित करें

```java
        // The second worksheet (index 1) will receive the copied pivot table.
        Worksheet destSheet = workbook.getWorksheets().get(1);

        // Destination starts at cell A1 of the second sheet.
        Range destRange = destSheet.getCells().createRange("A1");
```

*इस चरण की आवश्यकता क्यों है?*  
एक अलग वर्कशीट पर गंतव्य चुनने से आप **रेंज को दूसरी शीट पर कॉपी** कर सकते हैं। शीर्ष‑बाएँ सेल (`A1`) एक सामान्य प्रारंभिक बिंदु है, लेकिन आप पता बदलकर इसे कहीं भी रख सकते हैं।

### चरण 4: पिवट टेबल को संरक्षित रखते हुए स्रोत रेंज कॉपी करें

```java
        // Configure copy options to keep all formatting, formulas, and pivot data.
        CopyOptions copyOptions = new CopyOptions();
        copyOptions.setPasteType(PasteType.PASTE_ALL); // copies everything
        copyOptions.setSkipEmptyRows(false);
        copyOptions.setSkipEmptyColumns(false);

        // Perform the copy operation.
        sourceRange.copy(destRange, copyOptions);
```

*इस चरण की आवश्यकता क्यों है?*  
`CopyOptions` यह नियंत्रित करता है कि क्या ट्रांसफ़र किया जाता है। `PasteType.PASTE_ALL` का उपयोग करने से पिवट टेबल, उसका फॉर्मेटिंग, और अंतर्निहित फ़ॉर्मूले डुप्लिकेट होते हैं। इन विकल्पों के बिना केवल कच्चे मान कॉपी हो सकते हैं, जिससे पिवट कार्यक्षमता टूट सकती है।

### चरण 5: वर्कबुक सहेजें और परिणाम सत्यापित करें

```java
        // Save the modified workbook to a new file.
        workbook.save("output.xlsx");
        System.out.println("Pivot table copied successfully.");
    }
}
```

`output.xlsx` को Excel में खोलें और पुष्टि करें कि:

* दूसरी शीट में एक पूरी तरह कार्यशील पिवट टेबल है जो मूल के समान है।
* पिवट टेबल को रिफ्रेश करने से डेटा अपडेट होता है, जिससे कैश अपरिवर्तित रहने का प्रमाण मिलता है।

## Java का उपयोग करके रेंज को दूसरी शीट पर कॉपी करें

यदि आपका लक्ष्य केवल **रेंज को दूसरी शीट पर कॉपी** करना है बिना पिवट टेबल के, तो वही कोड सामान्य सेल रेंज के साथ काम करता है। केवल स्रोत पता बदलना होता है। `CopyOptions` कॉन्फ़िगरेशन वही रहता है, जिससे फ़ॉर्मूले और फॉर्मेटिंग संरक्षित रहती है।

```java
// Example: copy a plain data table from Sheet1!B2:D10 to Sheet3!A1
Range plainSource = workbook.getWorksheets().get(0)
                            .getCells().createRange("B2:D10");
Range plainDest = workbook.getWorksheets().get(2)
                          .getCells().createRange("A1");
plainSource.copy(plainDest, copyOptions);
```

यह स्निपेट API की लचीलापन को पिवट और गैर‑पिवट दोनों परिदृश्यों के लिए दर्शाता है।

## फ़ॉर्मूले खोए बिना वर्कशीट्स के बीच रेंज कॉपी करें

जब आप **वर्कशीट्स के बीच रेंज कॉपी** करते हैं, तो अन्य शीट्स को संदर्भित करने वाले फ़ॉर्मूले टूट सकते हैं यदि सापेक्ष संदर्भ बदल जाएँ। इसे रोकने के लिए:

1. यदि आपको केवल फ़ॉर्मूले चाहिए तो `CopyOptions.setPasteType(PasteType.PASTE_FORMULAS)` का उपयोग करें।
2. गंतव्य शीट को उसी वर्कबुक में रखें ताकि आंतरिक संदर्भ वैध रहें।
3. कॉपी करने के बाद, `workbook.calculateFormula();` को कॉल करके पुनः गणना को मजबूर करें।

```java
copyOptions.setPasteType(PasteType.PASTE_FORMULAS);
sourceRange.copy(destRange, copyOptions);
workbook.calculateFormula();
```

ये अतिरिक्त चरण सुनिश्चित करते हैं कि कॉपी किया गया रेंज मूल जैसा ही व्यवहार करे, भले ही वह कई वर्कशीट्स में फैला हो।

## प्रो टिप्स और सामान्य जाल

| स्थिति | सलाह |
|-----------|-----|
| **पिवट कैश अपडेट नहीं हो रहा** | कॉपी करने के बाद, `destSheet.getPivotTables().get(0).refresh();` को कॉल करके कैश को रिफ्रेश करें। |
| **विभिन्न वर्कबुक में कॉपी करना** | `Workbook destWorkbook = new Workbook();` का उपयोग करें और फिर `sourceRange.copy(destWorkbook.getWorksheets().get(0).getCells().createRange("A1"), copyOptions);`। आवश्यक होने पर पिवट कैश को अलग से कॉपी करना याद रखें। |
| **बड़ी पिवट टेबल्स** | कॉपी के दौरान `OutOfMemoryError` से बचने के लिए Java हीप आकार (`-Xmx2g`) बढ़ाएँ। |
| **स्टाइल्स को संरक्षित रखना** | `copyOptions.setPasteType(PasteType.PASTE_ALL)` सेट करें; अन्यथा केवल मान कॉपी होते हैं। |

## अपेक्षित आउटपुट

पूरा प्रोग्राम चलाने से `output.xlsx` बनता है। जब इसे Excel में खोलते हैं:

* **Sheet2!A1:G20** वही पिवट टेबल दिखाता है जो **Sheet1!A1:G20** में है।
* पिवट फ़ील्ड सूची, पंक्ति/स्तंभ लेबल, और डेटा मान स्रोत से मेल खाते हैं।
* पिवट को रिफ्रेश करने से संख्याएँ अपडेट होती हैं, जिससे कैश कार्यात्मक होने की पुष्टि होती है।

```
Pivot table copied successfully.
```

## निष्कर्ष

इस ट्यूटोरियल में आपने **पिवट टेबल कॉपी करने का तरीका** सीख लिया है, एक वर्कशीट से दूसरी में Aspose.Cells for Java का उपयोग करके। वर्कबुक लोड करके, सही स्रोत रेंज चुनकर, गंतव्य परिभाषित करके, और `CopyOptions` को कॉन्फ़िगर करके आप विश्वसनीय रूप से **रेंज को दूसरी शीट पर कॉपी** और **वर्कशीट्स के बीच रेंज कॉपी** कर सकते हैं, जबकि सभी पिवट कार्यक्षमता संरक्षित रहती है।  

आगे आप निम्नलिखित का अन्वेषण कर सकते हैं:

* कॉपी किए गए पिवट टेबल को PDF या HTML में निर्यात करना।
* कई वर्कबुक में पिवट टेबल रिफ्रेश को स्वचालित करना।
* `CopyOptions` का उपयोग करके केवल विशिष्ट तत्व (जैसे, मान, फ़ॉर्मेट) कॉपी करना।

विभिन्न रेंज पते, वर्कबुक संरचनाओं, या यहाँ तक कि क्रॉस‑वर्कबुक कॉपी के साथ प्रयोग करने में संकोच न करें। कोडिंग का आनंद लें!

## आगे आप क्या सीखें

निम्नलिखित ट्यूटोरियल्स उन निकटतम संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑बद्ध व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Java में रेंज कॉपी कैसे करें – Aspose.Cells के साथ पिवट टेबल कॉपी](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)
- [Java में पिवट टेबल कॉपी कैसे करें – पूर्ण Aspose.Cells गाइड](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [पिवट टेबल एक्सेल कॉपी – Java का उपयोग करके चरण‑बद्ध गाइड](/cells/english/java/excel-pivot-tables/copy-pivot-table-excel-step-by-step-guide-using-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}