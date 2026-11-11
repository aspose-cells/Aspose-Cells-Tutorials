---
date: '2026-10-28'
description: Java में Aspose.Cells copy and paste options का उपयोग करके मान पेस्ट
  करना सीखें, साथ में चरण‑दर‑चरण कोड, Maven डिपेंडेंसी सेटअप, और लाइसेंसिंग टिप्स।
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Java में Aspose.Cells copy and paste options का उपयोग करके मान पेस्ट
  करना सीखें, साथ में चरण‑दर‑चरण कोड, Maven डिपेंडेंसी सेटअप, और लाइसेंसिंग टिप्स।
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Aspose.Cells copy and paste options के साथ मान पेस्ट करने का तरीका
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Aspose.Cells copy and paste options के साथ मान पेस्ट करने का तरीका
url: /hi/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells कॉपी और पेस्ट विकल्पों के साथ मान कैसे पेस्ट करें

Automating Excel reporting in Java means you can generate, consolidate, and format workbooks without ever opening Excel manually. With **Aspose.Cells** you get full control over formulas, hidden rows, and cell values, so your reports stay accurate and lightweight. In this tutorial you’ll learn how to use **CopyOptions.ReferToDestinationSheet** to keep formulas correct and **PasteOptions** to paste only the visible values you need.

## त्वरित उत्तर
- **`CopyOptions.ReferToDestinationSheet` क्या करता है?** यह फ़ॉर्मूलों को पुनः लिखता है ताकि कॉपी ऑपरेशन के बाद वे गंतव्य शीट की ओर इशारा करें।  
- **मैं केवल दृश्यमान कोशिकाएँ कैसे पेस्ट कर सकता हूँ?** `PasteOptions.setOnlyVisibleCells(true)` को `PasteType.VALUES` के साथ कॉल करें।  
- **कौन सा लाइब्रेरी संस्करण आवश्यक है?** Aspose.Cells 25.3 या बाद का संस्करण।  
- **उत्पादन के लिए मुझे लाइसेंस चाहिए?** हाँ – एक स्थायी या अस्थायी लाइसेंस मूल्यांकन सीमाओं को हटा देता है।  
- **क्या मैं Maven या Gradle का उपयोग कर सकता हूँ?** दोनों समर्थित हैं; नीचे निर्भरता स्निपेट्स देखें।

## “Excel रिपोर्टिंग को स्वचालित करना” क्या है?
Automate Excel reporting means generating and updating Excel workbooks programmatically, allowing you to create, merge, and format reports without manual copy‑paste, which cuts errors and saves hours of repetitive work. This approach is ideal for scheduled batch jobs, data‑driven dashboards, and financial consolidation pipelines.

## रिपोर्टिंग के लिए CopyOptions और PasteOptions का उपयोग क्यों करें?
These two classes let you keep formula references intact while copying data **and** extract only the cells that are visible after filtering or hiding rows. Using them together reduces the amount of data transferred by up to 80 % in typical filtered‑table scenarios and guarantees that formulas continue to calculate correctly in the destination sheet.

## पूर्वापेक्षाएँ
- Java 8 या उससे ऊपर।  
- निर्भरता प्रबंधन के लिए Maven या Gradle।  
- Aspose.Cells 25.3+ (ट्रायल, अस्थायी, या स्थायी लाइसेंस)।  

## Java के लिए Aspose.Cells सेटअप करना

Add the library to your project with one of the following:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### लाइसेंस प्राप्ति
- **Free trial** – मूल्यांकन के लिए पूर्ण फीचर सेट।  
- **Temporary license** – परीक्षण के दौरान ट्रायल सीमाओं को हटाता है।  
- **Permanent license** – उत्पादन वर्कलोड्स के लिए अनुशंसित।

Initialize Aspose.Cells in your Java code:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## स्टेप‑बाय‑स्टेप गाइड

### 1. referToDestinationSheet के साथ copyOptions

#### समीक्षा
`CopyOptions` Aspose.Cells का कॉन्फ़िगरेशन ऑब्जेक्ट है जो कॉपी ऑपरेशन के दौरान फ़ॉर्मूले और सेल रेफ़रेंसेज़ को कैसे संभालता है, इसे नियंत्रित करता है। `CopyOptions.ReferToDestinationSheet` को `true` सेट करने से फ़ॉर्मूला रेफ़रेंसेज़ पुनः लिखे जाते हैं ताकि कॉपी ऑपरेशन के बाद वे नई शीट की ओर इशारा करें।

#### चरण 1: वर्कबुक और वर्कशीट्स को इनिशियलाइज़ करें  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### चरण 2: copyOptions को कॉन्फ़िगर करें  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### चरण 3: कॉपी ऑपरेशन निष्पादित करें  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*क्यों यह महत्वपूर्ण है*: वे फ़ॉर्मूले जो मूल रूप से `Sheet1` को रेफ़र करते थे, अब सही ढंग से `DestSheet` को रेफ़र करेंगे, जिससे आपके स्वचालित रिपोर्ट विश्वसनीय बनी रहेंगी।

**समस्या निवारण टिप**: यदि फ़ॉर्मूले अभी भी पुरानी शीट को रेफ़र कर रहे हैं, तो सुनिश्चित करें कि `setReferToDestinationSheet(true)` को कॉपी से **पहले** कॉल किया गया है।

### 2. दृश्यमान कोशिकाओं से केवल मानों के लिए pasteOptions

#### समीक्षा
`PasteOptions` Aspose.Cells की सेटिंग्स ऑब्जेक्ट है जो यह निर्धारित करती है कि क्या पेस्ट किया जाएगा। `PasteType.VALUES` को `onlyVisibleCells=true` के साथ उपयोग करने से केवल प्रदर्शित मान कॉपी होते हैं, छिपी पंक्तियों/कॉलम और फॉर्मेटिंग को नजरअंदाज किया जाता है।

#### चरण 1: वर्कबुक और वर्कशीट्स को इनिशियलाइज़ करें  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### चरण 2: pasteOptions को कॉन्फ़िगर करें  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### चरण 3: पेस्ट ऑपरेशन निष्पादित करें  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*क्यों यह महत्वपूर्ण है*: फ़िल्टर किए गए डेटा को निकालने या छिपी पंक्तियों या फॉर्मेटिंग शोर के बिना साफ़ रिपोर्ट बनाने के लिए आदर्श।

**समस्या निवारण टिप**: कॉपी करने से पहले सुनिश्चित करें कि पंक्तियाँ/कॉलम Excel में वास्तव में छिपी हुई हैं; अन्यथा, वे शामिल हो जाएँगी।

## व्यावहारिक अनुप्रयोग
1. **Financial consolidation** – सभी फ़ॉर्मूले सटीक रखते हुए मासिक शीट्स को मास्टर वर्कबुक में मर्ज करें।  
2. **Filtered data export** – फ़िल्टर की गई तालिका से केवल दृश्यमान पंक्तियों को सारांश शीट में निकालें।  
3. **Scheduled report generation** – सटीक सेल मान और सही रेफ़रेंसेज़ के साथ रात्रीकालीन Excel रिपोर्ट निर्माण को स्वचालित करें।

## प्रदर्शन संबंधी विचार
- **वर्कबुक्स को डिस्पोज़ करें** जब काम समाप्त हो (`wb.dispose();`) ताकि नेटिव रिसोर्सेज़ मुक्त हो सकें।  
- **बैच ऑपरेशन्स** – ओवरहेड कम करने के लिए कई कॉपी/पेस्ट कॉल्स को समूहित करें।  
- **मेमोरी मॉनिटर करें** – बड़े वर्कबुक्स को बढ़ी हुई हीप (`-Xmx2g`) की आवश्यकता हो सकती है।  
- Aspose.Cells **50+ इनपुट और आउटपुट फॉर्मैट्स** का समर्थन करता है और **2 मिलियन पंक्तियों** तक के वर्कबुक्स को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, जिससे एंटरप्राइज़ वर्कलोड्स के लिए हाई‑थ्रूपुट प्रदर्शन मिलता है।

## अक्सर पूछे जाने वाले प्रश्न

**Q: `CopyOptions.ReferToDestinationSheet` का उपयोग किस लिए किया जाता है?**  
A: यह फ़ॉर्मूला रेफ़रेंसेज़ को पुनः लिखता है ताकि कॉपी के बाद वे गंतव्य शीट की ओर इशारा करें, जिससे रिपोर्टिंग फ़ॉर्मूले सही बने रहें।

**Q: मैं केवल दृश्यमान कोशिकाएँ कैसे पेस्ट करूँ?**  
A: `PasteOptions.setOnlyVisibleCells(true)` सेट करें और `PasteType.VALUES` चुनें।

**Q: क्या मैं Aspose.Cells को लाइसेंस खरीदे बिना उपयोग कर सकता हूँ?**  
A: हाँ, मूल्यांकन के लिए एक फ्री ट्रायल या अस्थायी लाइसेंस उपलब्ध है, लेकिन उत्पादन के लिए स्थायी लाइसेंस आवश्यक है।

**Q: कॉपी करने के बाद कुछ रेफ़रेंसेज़ अभी भी गलत क्यों हैं?**  
A: दोबारा जांचें कि `ReferToDestinationSheet` कॉपी ऑपरेशन से **पहले** सक्षम है और स्रोत फ़ॉर्मूले में बाहरी वर्कबुक लिंक नहीं हैं।

**Q: मुझे कौन सी मेमोरी‑मैनेजमेंट बेस्ट प्रैक्टिसेज़ अपनानी चाहिए?**  
A: समाप्त होने पर `Workbook` ऑब्जेक्ट्स को डिस्पोज़ करें, बड़े फ़ाइलों को भागों में प्रोसेस करें, और JVM हीप उपयोग को मॉनिटर करें।

**Q: क्या एक ही ऑपरेशन में CopyOptions और PasteOptions को मिलाया जा सकता है?**  
A: हाँ, आप पहले `CopyOptions` के साथ कॉपी करके और फिर लक्ष्य रेंज पर `PasteOptions` लागू करके उन्हें चेन कर सकते हैं।

## संसाधन
- **डॉक्यूमेंटेशन**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **डाउनलोड**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **खरीदें**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **फ़्री ट्रायल**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **अस्थायी लाइसेंस**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **सपोर्ट फ़ोरम**: [Aspose support](https://forum.aspose.com/c/cells)

**अंतिम अपडेट:** 2026-10-28  
**परीक्षण किया गया:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Read Excel File Java – Master Workbook Cell Manipulation with Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Add Data to Cell in Excel Using Aspose.Cells for Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convert Excel Cell Row Column Indices with Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}