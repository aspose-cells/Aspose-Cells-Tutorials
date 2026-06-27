---
category: general
date: 2026-06-27
description: जावा में पिवट टेबल को एक्सेल पिवट इमेज के रूप में निर्यात करें। जानें
  कि PNG फ़ॉर्मेट कैसे सेट करें, विकल्पों को कॉन्फ़िगर करें, और कुछ ही चरणों में फ़ाइल
  को सहेजें।
draft: false
keywords:
- export pivot table
- excel pivot image
- set png format
language: hi
og_description: जावा का उपयोग करके पिवट टेबल को एक्सेल पिवट इमेज के रूप में निर्यात
  करें। यह गाइड दिखाता है कि PNG फ़ॉर्मेट कैसे सेट करें और इमेज को आत्मविश्वास के
  साथ सहेजें।
og_title: जावा में पिवट टेबल को PNG में निर्यात करें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Export pivot table as an Excel pivot image in Java. Learn how to set
    PNG format, configure options, and save the file in just a few steps.
  headline: Export pivot table to PNG in Java – Complete Programming Guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel Automation
title: जावा में पिवट टेबल को PNG में निर्यात करें – पूर्ण प्रोग्रामिंग गाइड
url: /hi/java/excel-pivot-tables/export-pivot-table-to-png-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में पिवट टेबल को PNG में निर्यात करें – पूर्ण प्रोग्रामिंग गाइड

क्या आपको कभी Excel वर्कबुक से **export pivot table** करने की ज़रूरत पड़ी है लेकिन साफ़ इमेज फ़ाइल कैसे प्राप्त करें, यह नहीं पता था? आप अकेले नहीं हैं—कई डेवलपर्स रिपोर्टिंग डैशबोर्ड बनाते समय इस समस्या का सामना करते हैं। अच्छी खबर यह है कि कुछ ही Java कोड लाइनों से आप किसी भी पिवट टेबल को एक स्पष्ट **Excel pivot image** में बदल सकते हैं और उसे PNG के रूप में सहेज सकते हैं।  

इस ट्यूटोरियल में हम पूरी प्रक्रिया को चरण दर चरण देखेंगे: वर्कबुक पढ़ना, पहले पिवट टेबल को ढूँढ़ना, निर्यात को **set PNG format** के लिए कॉन्फ़िगर करना, और अंत में इमेज को डिस्क पर लिखना। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी प्रोजेक्ट में जोड़ सकते हैं।

## आप क्या सीखेंगे

- Aspose.Cells (या यदि आप चाहें तो Apache POI) के साथ Excel फ़ाइल को लोड करने का तरीका।  
- PNG के रूप में **export pivot table** करने के लिए आवश्यक सटीक API कॉल्स।  
- इमेज फ़ॉर्मेट सेट करने का महत्व और **set PNG format** को सही तरीके से कैसे सेट करें।  
- सामान्य समस्याएँ—जैसे कई पिवट टेबल्स को संभालना या गायब वर्कशीट्स—और उन्हें कैसे टालें।  
- एक पूर्ण, तैयार‑चलाने‑योग्य Java उदाहरण जिसे आप कॉपी‑पेस्ट कर सकते हैं।  

> **Prerequisites**  
> • Java 17 या नया (कोड पहले के संस्करणों के साथ भी काम करता है, लेकिन 17 की सिफारिश की जाती है)।  
> • Aspose.Cells for Java लाइब्रेरी (फ्री ट्रायल ठीक काम करता है)।  
> • Excel फ़ाइलों और Java I/O की बुनियादी परिचितता।  

---

## चरण 1: Aspose.Cells निर्भरता जोड़ें

यदि आप Maven का उपयोग कर रहे हैं, तो निम्न निर्भरता को अपने `pom.xml` में डालें। अन्यथा, Aspose वेबसाइट से JAR डाउनलोड करें और उसे अपने क्लासपाथ में जोड़ें।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- latest as of June 2026 -->
</dependency>
```

*Pro tip:* लाइब्रेरी संस्करणों को आधिकारिक रिलीज़ नोट्स के साथ सिंक में रखें ताकि अनपेक्षित बग्स से बचा जा सके।

## चरण 2: वर्कबुक लोड करें और पिवट टेबल खोजें

पहले हम Excel फ़ाइल खोलते हैं, फिर पहले वर्कशीट पर पहला पिवट टेबल प्राप्त करते हैं। यदि वर्कबुक में कोई पिवट टेबल नहीं है, तो हम शालीनता से बाहर निकलते हैं।

```java
import com.aspose.cells.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        try {
            // Load the workbook (replace with your actual path)
            Workbook workbook = new Workbook("C:/data/report.xlsx");

            // Access the first worksheet – you can also loop through all sheets
            Worksheet ws = workbook.getWorksheets().get(0);

            // Verify that the sheet actually contains pivot tables
            if (ws.getPivotTables().getCount() == 0) {
                System.out.println("No pivot tables found on the first sheet.");
                return;
            }

            // Retrieve the first pivot table (this is the target for export)
            PivotTable pivotTable = ws.getPivotTables().get(0);
```

> **Why this step matters** – `PivotTable` ऑब्जेक्ट किसी भी इमेज निर्यात का प्रवेश बिंदु है। गैर‑मौजूद पिवट पर `toImage` कॉल करने से `NullPointerException` फेंका जाएगा, इसलिए हम पहले काउंट जांचते हैं।  

## चरण 3: इमेज निर्यात विकल्प कॉन्फ़िगर करें (Set PNG Format)

अब हम एक `ImageOrPrintOptions` इंस्टेंस बनाते हैं और स्पष्ट रूप से **set PNG format** करते हैं। PNG लॉस‑लेस है, जो ग्रिडलाइन और फ़ॉन्ट की तीक्ष्णता को बनाए रखता है।

```java
            // Step 3: Configure image export options – we want PNG
            ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
            imgOptions.setImageFormat(ImageFormat.PNG);   // <-- set png format
            imgOptions.setOnePagePerSheet(true);          // optional: force single‑page output
            imgOptions.setTransparent(true);              // optional: keep background transparent
```

*Note:* यदि आपको JPEG चाहिए, तो बस `ImageFormat.PNG` को `ImageFormat.JPEG` से बदल दें। वही विकल्प ऑब्जेक्ट दोनों के लिए काम करता है।

## चरण 4: पिवट टेबल को इमेज फ़ाइल के रूप में निर्यात करें

विकल्प तैयार होने पर, हम `toImage` को कॉल करते हैं। यह मेथड फ़ाइल को सीधे लिखता है, इसलिए अतिरिक्त स्ट्रीम की आवश्यकता नहीं होती।

```java
            // Step 4: Export the pivot table as an image file
            String outputPath = "C:/exports/pivot.png";
            pivotTable.toImage(outputPath, imgOptions);

            System.out.println("Pivot table exported successfully to: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

प्रोग्राम चलाने पर `pivot.png` नाम की फ़ाइल बनती है जो Excel में दिखने वाले पिवट जैसी ही दिखती है। इसे किसी भी इमेज व्यूअर से खोलकर सत्यापित करें।

### अपेक्षित आउटपुट

```
Pivot table exported successfully to: C:/exports/pivot.png
```

परिणामी इमेज स्क्रीन पर दिखाए गए लेआउट से मेल खाएगी, जिसमें कॉलम चौड़ाई, पंक्ति ऊँचाई, और आप द्वारा लागू कोई भी कंडीशनल फ़ॉर्मेटिंग शामिल है।

## कई पिवट टेबल्स को संभालना (उन्नत)

यदि आपके वर्कशीट में कई पिवट टेबल्स हैं और आप केवल एक विशिष्ट चाहते हैं तो क्या करें? आप `ws.getPivotTables()` पर लूप कर सकते हैं और नाम से चुन सकते हैं:

```java
PivotTable target = null;
for (int i = 0; i < ws.getPivotTables().getCount(); i++) {
    PivotTable pt = ws.getPivotTables().get(i);
    if ("SalesByRegion".equals(pt.getName())) {
        target = pt;
        break;
    }
}
if (target == null) {
    System.out.println("Desired pivot table not found.");
    return;
}
target.toImage("C:/exports/sales_by_region.png", imgOptions);
```

*Why this is useful*: वास्तविक‑दुनिया की रिपोर्टों में अक्सर एक सारांश पिवट और एक विस्तृत पिवट होता है। नाम से चयन करने से आकस्मिक ओवरराइट से बचा जा सकता है।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| Issue | Symptom | Fix |
|------|----------|-----|
| **Missing worksheet** | `IndexOutOfBoundsException` जब `ws` तक पहुँच रहे हों | `workbook.getWorksheets().getCount() > 0` को इंडेक्स करने से पहले सत्यापित करें। |
| **No pivot tables** | चुपचाप विफलता या खाली इमेज | `ws.getPivotTables().getCount()` जाँच का उपयोग करें (देखें चरण 2)। |
| **Wrong image format** | आउटपुट धुंधला दिखता है या उसमें आर्टिफैक्ट्स होते हैं | हमेशा लॉसलेस आउटपुट के लिए `setImageFormat(ImageFormat.PNG)` का उपयोग करें; टेक्स्ट‑भारी टेबल्स के लिए JPEG से बचें। |
| **File path not writable** | `IOException` `toImage` पर | सुनिश्चित करें कि डायरेक्टरी मौजूद है (`new File(outputPath).getParentFile().mkdirs()`)। |

## प्रो टिप: वेब ऐप्स के लिए बाइट एरे में निर्यात करें

यदि आप एक वेब सर्विस बना रहे हैं जो PNG को सीधे ब्राउज़र में लौटाती है, तो आप फ़ाइल की बजाय `ByteArrayOutputStream` में लिख सकते हैं:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
pivotTable.toImage(baos, imgOptions);
byte[] pngBytes = baos.toByteArray();
// Send pngBytes as HTTP response with Content-Type: image/png
```

यह अस्थायी फ़ाइलों की आवश्यकता को समाप्त करता है और प्रतिक्रिया को तेज़ बनाता है।

## पूर्ण कार्यशील उदाहरण (सभी चरणों का संयोजन)

नीचे पूर्ण, कॉपी‑एंड‑पेस्ट‑तैयार प्रोग्राम दिया गया है जिसमें सभी चर्चा किए गए सर्वोत्तम अभ्यास शामिल हैं।

```java
import com.aspose.cells.*;
import java.io.*;

public class PivotTableExporter {

    public static void main(String[] args) {
        // 1️⃣ Load workbook
        Workbook workbook;
        try {
            workbook = new Workbook("C:/data/report.xlsx");
        } catch (Exception e) {
            System.err.println("Failed to load workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Get first worksheet and ensure a pivot exists
        if (workbook.getWorksheets().getCount() == 0) {
            System.out.println("Workbook contains no worksheets.");
            return;
        }
        Worksheet ws = workbook.getWorksheets().get(0);
        if (ws.getPivotTables().getCount() == 0) {
            System.out.println("No pivot tables on the first sheet.");
            return;
        }
        PivotTable pivotTable = ws.getPivotTables().get(0); // export pivot table

        // 3️⃣ Configure export options – set png format
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.PNG); // <-- set png format
        imgOptions.setOnePagePerSheet(true);
        imgOptions.setTransparent(true);

        // 4️⃣ Prepare output directory
        String outDir = "C:/exports";
        new File(outDir).mkdirs(); // create if missing

        // 5️⃣ Export the image
        String outPath = outDir + "/pivot.png";
        try {
            pivotTable.toImage(outPath, imgOptions);
            System.out.println("Pivot table exported successfully to: " + outPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

इस क्लास को चलाने से `C:/exports` के अंदर `pivot.png` बन जाएगा। फ़ाइल खोलें और आप मूल पिवट टेबल की बिल्कुल समान दृश्य प्रतिलिपि देखेंगे—रिपोर्ट, ईमेल या वेब पेज में एम्बेड करने के लिए एकदम उपयुक्त।

![PNG के रूप में निर्यात किया गया पिवट टेबल – एक्सेल पिवट इमेज का उदाहरण](https://example.com/images/pivot-export.png "पिवट टेबल निर्यात उदाहरण")

*Image alt text:* **PNG Excel पिवट इमेज दिखाते हुए पिवट टेबल निर्यात उदाहरण**

## निष्कर्ष

हमने अभी आपको दिखाया है कि Java का उपयोग करके Excel से **export pivot table** डेटा को उच्च‑गुणवत्ता वाले PNG में कैसे निर्यात करें। मुख्य चरण हैं वर्कबुक लोड करना, पिवट को ढूँढ़ना, `ImageOrPrintOptions` को **set PNG format** के लिए कॉन्फ़िगर करना, और अंत में `toImage` को कॉल करना।  

इस ज्ञान के साथ आप अब रिपोर्ट जनरेशन को स्वचालित कर सकते हैं, डैशबोर्ड में पिवट स्नैपशॉट एम्बेड कर सकते हैं, या उन्हें सीधे वेब API से सर्व कर सकते हैं। आगे आप **excel pivot image** स्केलिंग विकल्पों का अन्वेषण कर सकते हैं, वॉटरमार्क जोड़ सकते हैं, या यहां तक कि PNG को PDF में बदल सकते हैं प्रिंटेबल रिपोर्ट्स के लिए।  

बड़े वर्कबुक को संभालने या Spring Boot के साथ इंटीग्रेशन के बारे में प्रश्न हैं? नीचे टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Aspose.Cells for Java के साथ Excel पिवट टेबल स्रोत को अपडेट करने का तरीका: एक व्यापक गाइड](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)
- [Aspose.Cells for Java के साथ Excel पिवट टेबल स्टाइलिंग और सहेजने का स्वचालन: एक व्यापक गाइड](/cells/english/java/data-analysis/excel-pivot-table-styling-saving-aspose-cells-java/)
- [Aspose.Cells Java के साथ Excel पिवट टेबल मैनिपुलेशन: एक व्यापक गाइड](/cells/english/java/data-analysis/excel-pivot-table-manipulation-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}