---
category: general
date: 2026-03-01
description: जावा में पिवट टेबल को पिवट को बनाए रखते हुए कॉपी करें, फिर एक्सेल को
  PPTX में निर्यात करें, एक्सेल ऑटोफ़िल्टर को निष्क्रिय करें, और JSON एरेज़ के लिए
  स्मार्ट मार्कर का उपयोग करें – पूर्ण चरण‑दर‑चरण गाइड।
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: hi
og_description: जावा में पिवट टेबल कॉपी करें, पिवट परिभाषा को संरक्षित रखें, PPTX
  में निर्यात करें, ऑटोफ़िल्टर को अक्षम करें, और स्मार्ट मार्कर का उपयोग करें – डेवलपर्स
  के लिए पूर्ण मार्गदर्शिका।
og_title: जावा में पिवट टेबल कॉपी करें – इसे संरक्षित रखें, PPTX में निर्यात करें
tags:
- Aspose.Cells
- Java
- Excel Automation
title: जावा में पिवट टेबल कॉपी करें – इसे संरक्षित रखें, PPTX में निर्यात करें
url: /hi/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में पिवट टेबल कॉपी करें – इसे संरक्षित रखें, PPTX में निर्यात करें

क्या आपको कभी **पिवट टेबल कॉपी** करने की ज़रूरत पड़ी है एक वर्कबुक से दूसरे में बिना मूल पिवट परिभाषा खोए? आप अकेले नहीं हैं जो इस पर सिर खुजा रहे हैं। कई वास्तविक‑दुनिया प्रोजेक्ट्स में आपको डेटा इधर‑उधर ले जाना पड़ेगा, और आखिरी चीज़ जो आप चाहते हैं वह है एक टूटा हुआ पिवट जो रन‑टाइम पर त्रुटियाँ फेंके।  

इस ट्यूटोरियल में हम एक पूर्ण समाधान के माध्यम से चलेंगे जो न केवल **पिवट टेबल कॉपी** करता है बल्कि आपको दिखाता है कि **पिवट टेबल को संरक्षित** कैसे रखें कॉपी करते समय, **Excel को PPTX में निर्यात** करें, **Excel AutoFilter को निष्क्रिय** करें, और **स्मार्ट मार्कर** का उपयोग करके एक JSON एरे को एक ही सेल में डालें। अंत तक आपके पास एक एकल, चलाने योग्य जावा प्रोग्राम होगा जो सभी चार परिदृश्यों को कवर करता है।

## Prerequisites

- Java 8 या नया (कोड Java 11 के साथ भी काम करता है)  
- Aspose.Cells for Java लाइब्रेरी (संस्करण 23.9 या बाद का) – आप इसे Maven Central से प्राप्त कर सकते हैं  
- Excel की अवधारणाओं जैसे पिवट टेबल, टेबल, और टेक्स्ट बॉक्स की बुनियादी परिचितता  

यदि आपके पास Aspose.Cells JAR नहीं है, तो इसे अपने `pom.xml` में जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

अब, चलिए शुरू करते हैं।

## Step 1: Copy Pivot Table – Preserving the Pivot Definition

जब आप केवल वह सेल रेंज कॉपी करते हैं जिसमें पिवट टेबल स्थित है, तो पिवट मेटाडेटा अक्सर पीछे रह जाता है। Aspose.Cells हमें `copyRange` को `CopyOptions` इंस्टेंस के साथ उपयोग करके परिभाषा को अपरिवर्तित रखने का एक साफ़ तरीका देता है।

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Why this works:** `CopyOptions` Aspose.Cells को सब कुछ ले जाने के लिए बताता है, जिसमें पिवट कैश और फ़ील्ड सेटिंग्स शामिल हैं। इसके बिना, आपको केवल साधारण मान मिलेंगे और पिवट को रीफ़्रेश करने की क्षमता खो देंगे।

**Edge case:** यदि आपका स्रोत पिवट हार्ड‑कोडेड `A1:G20` से अधिक विस्तृत है, तो रेंज को उसी अनुसार समायोजित करें या इसे डायनामिक रूप से प्राप्त करने के लिए `sourceSheet.getPivotTables().get(0).getDataRange()` का उपयोग करें।

![पिवट टेबल कॉपी उदाहरण](image.png "जावा में पिवट टेबल कॉपी")

*छवि वैकल्पिक पाठ: जावा में पिवट टेबल कॉपी आरेख*

## Step 2: Export a Worksheet with an Editable TextBox to PPTX

अक्सर आपको एक Excel शीट को PowerPoint स्लाइड में बदलने की आवश्यकता होती है—जैसे साप्ताहिक डैशबोर्ड जिन्हें प्रस्तुत करना होता है। Aspose.Cells सीधे एक वर्कशीट को PPTX फ़ाइल के रूप में सहेज सकता है जबकि टेक्स्ट बॉक्स जैसे आकारों को संरक्षित रखता है।

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**What’s happening:** `save` मेथड के साथ `SaveFormat.PPTX` पूरी शीट को, जिसमें कोई भी Editable TextBox शामिल है, PowerPoint स्लाइड में बदल देता है। बॉक्स के अंदर का टेक्स्ट PPTX को PowerPoint में खोलने पर संपादन योग्य रहता है।

**Tip:** यदि आपके पास कई शीट्स हैं और आप केवल एक विशिष्ट शीट चाहते हैं, तो सहेजने से पहले अन्य शीट्स के लिए `wb.getWorksheets().removeAt(index)` कॉल करें।

## Step 3: Disable Excel AutoFilter from a Table

AutoFilter उपयोगकर्ताओं के लिए सुविधाजनक है, लेकिन कभी‑कभी आपको इसे प्रोग्रामेटिक रूप से बंद करना पड़ता है—शायद डेटा निर्यात करने से पहले या एक साफ़ रिपोर्ट जनरेट करते समय। यहाँ बताया गया है कि **excel autofilter** को एक Excel टेबल पर कैसे **disable** किया जाए।

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Why you might need this:** उन फ़ॉर्मेट्स में निर्यात करना जो AutoFilter को सपोर्ट नहीं करते (जैसे CSV या PDF) फ़िल्टर आइकन को अनजाने में दिखा सकता है। इसे निष्क्रिय करने से आउटपुट साफ़ रहता है।

**Common pitfall:** यदि शीट में कोई टेबल नहीं है, तो `getTables().get(0)` `IndexOutOfBoundsException` फेंकेगा। प्रोडक्शन कोड में हमेशा पहले `sheet.getTables().size()` जांचें।

## Step 4: Use Smart Marker – Insert a JSON Array as a Single Cell Value

Smart Marker Aspose का टेम्प्लेटिंग इंजन है। एक उपयोगी ट्रिक यह है कि पूरे JSON एरे को एक ही सेल वैल्यू के रूप में माना जाए, जो लॉगिंग या संरचित डेटा को डाउनस्ट्रीम पास करने के लिए परिपूर्ण है। चलिए इसे हासिल करने के लिए **smart marker** का उपयोग करते हैं।

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**How it works:** वर्कबुक में `${json}` मार्कर पूरे JSON स्ट्रिंग से बदल जाता है क्योंकि हमने `ArrayAsSingle` सेट किया है। इस विकल्प के बिना, Aspose प्रत्येक एरे एलिमेंट को अलग‑अलग पंक्तियों में विस्तारित करने की कोशिश करेगा।

**Variation:** यदि आपको एरे को पंक्तियों में विभाजित करने की आवश्यकता है, तो बस `ArrayAsSingle` को हटाएँ और Smart Marker को स्वचालित रूप से विस्तार करने दें।

## Full Working Example – All Steps Combined

नीचे एक एकल जावा क्लास है जो हमने कवर किए गए सभी ऑपरेशन्स को जोड़ता है। इसे एक सामान्य `main` मेथड के रूप में चलाएँ; केवल फ़ाइल पाथ को अपने वातावरण के अनुसार समायोजित करें।

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}