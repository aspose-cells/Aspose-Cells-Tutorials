---
category: general
date: 2026-06-21
description: जावा में एक्सपैंड का उपयोग करके एरे को पंक्तियों में विस्तारित करना,
  एक्सेल फ़ॉर्मूला कोड लिखना, और जावा शैली में एक्सेल फ़ाइल सहेजना—सभी एक ही ट्यूटोरियल
  में सीखें।
draft: false
keywords:
- how to use expand
- expand array to rows
- write excel formula code
- save excel file java
language: hi
og_description: जावा में एक्सपैंड का उपयोग करके एक्सेल डेटा को कैसे मैनीपुलेट करें,
  एरे को पंक्तियों में विस्तारित करें, एक्सेल फ़ॉर्मूला कोड लिखें, और जावा के माध्यम
  से एक्सेल फ़ाइल सहेजें।
og_title: जावा में एक्सपैंड का उपयोग कैसे करें – पूर्ण एक्सेल गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  headline: How to Use Expand in Java – Complete Excel Guide
  type: TechArticle
- description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  name: How to Use Expand in Java – Complete Excel Guide
  steps:
  - name: Why This Works
    text: '- **`Workbook`**: Represents the entire Excel file. Creating a new one
      gives you a clean canvas; loading an existing file lets you augment a pre‑existing
      template. - **`Worksheet`**: Think of it as a single tab. We grab the first
      one because that’s where we’ll demonstrate the formula. - **`setFormul'
  - name: Real‑World Use Cases
    text: '| Scenario | How EXPAND Helps | |----------|------------------| | Generating
      a month‑long schedule from a short list of tasks | `=EXPAND(taskList,30)` |
      | Padding a matrix for a statistical model | `=EXPAND(matrix,10,10,0)` | | Creating
      placeholder rows for user input | `=EXPAND({""},20)` |'
  - name: Expected Output
    text: 'When you open `output.xlsx`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Formulas
title: जावा में एक्सपैंड का उपयोग कैसे करें – पूर्ण एक्सेल गाइड
url: /hi/java/spreadsheet-automation/how-to-use-expand-in-java-complete-excel-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में EXPAND का उपयोग कैसे करें – पूर्ण Excel गाइड

क्या आप कभी **expand का उपयोग कैसे करें** जब आप जावा के साथ Excel को ऑटोमेट कर रहे हैं? आप अकेले नहीं हैं—डेवलपर्स लगातार पूछते हैं कि कैसे array को rows में expand किया जाए बिना अनंत loops लिखे। अच्छी खबर यह है कि आप इसे एक ही फ़ॉर्मूला से कर सकते हैं, और वह जावा कोड जो इस फ़ॉर्मूले को वर्कबुक में डालता है, आश्चर्यजनक रूप से छोटा है।

इस ट्यूटोरियल में हम एक व्यावहारिक उदाहरण के माध्यम से चलेंगे जो आपको बिल्कुल दिखाएगा कि expand का उपयोग कैसे करें, जावा में Excel फ़ॉर्मूला कोड कैसे लिखें, और Excel फ़ाइल को जावा‑स्टाइल में कैसे सेव करें ताकि आप तुरंत परिणाम देख सकें। अंत तक आपके पास एक रन करने योग्य प्रोग्राम होगा जो मौजूदा वर्कबुक को लोड करता है, `EXPAND` फ़ंक्शन को एक सेल में डालता है, और फ़ाइल को डिस्क पर लिखता है।

## पूर्वापेक्षाएँ

- Java 17 (या कोई भी नवीनतम JDK) स्थापित हो।
- Maven या Gradle निर्भरताओं को प्रबंधित करने के लिए।
- **Aspose.Cells for Java** लाइब्रेरी (जावा से Excel को मैनिपुलेट करने का सबसे आसान तरीका)। आप इसे Maven Central से प्राप्त कर सकते हैं:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
```

कोई अतिरिक्त Excel इंस्टॉलेशन आवश्यक नहीं है; लाइब्रेरी फ़ाइल फ़ॉर्मेट को आंतरिक रूप से संभालती है। यदि आप Gradle पसंद करते हैं, तो बस निर्भरता ब्लॉक को उसी अनुसार बदल दें।

अब जब हमने मूल बातें कवर कर ली हैं, चलिए काम में लगते हैं।

## जावा में EXPAND का उपयोग कैसे करें

`EXPAND` फ़ंक्शन Excel के डायनामिक एरे परिवार का हिस्सा है। यह एक स्रोत एरे लेता है और उसे निर्दिष्ट आकार में विस्तारित करता है, डिफ़ॉल्ट रूप से खाली सेल्स को `#N/A` से भरता है। हमारे मामले में हम एक सरल एक‑आयामी एरे `{1,2,3}` को देंगे और Excel से इसे **5 पंक्तियों** में विस्तारित करने को कहेंगे।

```java
// Import statements
import com.aspose.cells.*;

public class ExpandDemo {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load or create a workbook
            Workbook wb = new Workbook(); // creates a blank workbook
            // Optionally, load an existing file:
            // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // 3️⃣ Apply the EXPAND function in cell A1
            // This is where we **write excel formula code** from Java.
            ws.getCells().get("A1").setFormula("=EXPAND({1,2,3},5)");

            // 4️⃣ Save the workbook — **save excel file java** style.
            wb.save("YOUR_DIRECTORY/output.xlsx");
            System.out.println("Workbook saved successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### यह क्यों काम करता है

- **`Workbook`**: पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। नया बनाना आपको एक साफ़ कैनवास देता है; मौजूदा फ़ाइल लोड करने से आप एक पूर्व‑स्थापित टेम्पलेट को बढ़ा सकते हैं।
- **`Worksheet`**: इसे एक सिंगल टैब के रूप में सोचें। हम पहला टैब लेते हैं क्योंकि वहीं हम फ़ॉर्मूला दिखाएंगे।
- **`setFormula`**: यह मेथड किसी भी वैध Excel फ़ॉर्मूला को स्ट्रिंग के रूप में इंजेक्ट करता है। यहाँ हम `EXPAND` फ़ंक्शन दे रहे हैं, जो Excel को **एरे को पंक्तियों में विस्तारित** करने (और कॉलम्स में भी, यदि आप चाहें) को बताता है।
- **`save`**: बदलावों को डिस्क पर स्थायी रूप से लिखता है। यह **save excel file java** चरण है जो सुनिश्चित करता है कि आप फ़ाइल को Excel या किसी भी व्यूअर में बाद में खोल सकें।

प्रोग्राम चलाएँ, `output.xlsx` खोलें, और आप देखेंगे कि कॉलम A में `1, 2, 3, #N/A, #N/A` भरे हुए हैं। `EXPAND` के दूसरे आर्ग्यूमेंट को `3` करने पर आपको केवल तीन पंक्तियाँ मिलेंगी—डायनामिक रिपोर्ट्स के लिए एकदम सही।

## EXPAND फ़ंक्शन के साथ एरे को पंक्तियों में विस्तारित करें

यदि आप ऐसे पृष्ठभूमि से आ रहे हैं जहाँ आप मैन्युअली पंक्तियों पर लूप करते थे, तो `EXPAND` फ़ंक्शन उस बोइलरप्लेट को बदल सकता है। यहाँ सिंटैक्स का एक त्वरित विवरण है:

```
EXPAND(source, rows, columns, fill)
```

- **source** – वह एरे जिसे आप विस्तारित करना चाहते हैं। हमारे उदाहरण में `{1,2,3}`।
- **rows** – इच्छित पंक्तियों की संख्या। हमने `5` उपयोग किया।
- **columns** – वैकल्पिक; डिफ़ॉल्ट रूप से स्रोत के कॉलम काउंट के बराबर।
- **fill** – खाली सेल्स में क्या रखा जाए (`#N/A` डिफ़ॉल्ट रूप से)।

### वास्तविक उपयोग के मामले

| परिदृश्य | EXPAND कैसे मदद करता है |
|----------|------------------------|
| छोटे कार्य सूची से महीने‑भर का शेड्यूल बनाना | `=EXPAND(taskList,30)` |
| सांख्यिकीय मॉडल के लिए मैट्रिक्स को पैड करना | `=EXPAND(matrix,10,10,0)` |
| उपयोगकर्ता इनपुट के लिए प्लेसहोल्डर पंक्तियाँ बनाना | `=EXPAND({""},20)` |

Excel को भारी काम करने देकर, आप अपना जावा कोड साफ़ रखते हैं और अनावश्यक लूप्स से बचते हैं।

## जावा में Excel फ़ॉर्मूला कोड लिखें

आप सोच सकते हैं, “क्या मैं फ़ॉर्मूला स्ट्रिंग को डायनामिकली बना सकता हूँ?” बिल्कुल। यहाँ एक स्निपेट है जो वेरिएबल्स के आधार पर `EXPAND` कॉल बनाता है:

```java
int[] numbers = {4, 5, 6};
int targetRows = 7;

// Convert int array to Excel‑style literal: {4,5,6}
StringBuilder sb = new StringBuilder("{");
for (int i = 0; i < numbers.length; i++) {
    sb.append(numbers[i]);
    if (i < numbers.length - 1) sb.append(",");
}
sb.append("}");

String formula = String.format("=EXPAND(%s,%d)", sb.toString(), targetRows);
ws.getCells().get("B2").setFormula(formula);
```

ध्यान दें कि हम प्रोग्रामेटिकली **write excel formula code** कैसे लिखते हैं, फिर उसे सेल `B2` में डालते हैं। यह तरीका तब स्केल करता है जब आपको फ़ॉर्मूले तुरंत जनरेट करने हों—जैसे, डेटाबेस से डेटा खींचकर उसे एक डायनामिक Excel रिपोर्ट में बदलना।

## जावा में Excel फ़ाइल सेव करें – बदलावों को स्थायी बनाना

वर्कबुक को सेव करना पहेली का अंतिम टुकड़ा है। Aspose.Cells आपको कुछ विकल्प देता है:

- **`wb.save("path.xlsx")`** – डिफ़ॉल्ट XLSX फ़ॉर्मेट में सेव करता है।
- **`wb.save("path.xls", SaveFormat.EXCEL_97_TO_2003)`** – लेगेसी संगतता के लिए।
- **`wb.save(outputStream, SaveFormat.XLSX)`** – जब आपको फ़ाइल को स्ट्रीम करना हो (जैसे, वेब ऐप में)।

यहाँ एक उदाहरण है जो `ByteArrayOutputStream` में लिखता है ताकि आप बाइट्स को एक REST एंडपॉइंट से रिटर्न कर सकें:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
wb.save(baos, SaveFormat.XLSX);
byte[] excelBytes = baos.toByteArray();
// Now you can send `excelBytes` as a response payload.
```

यह वही **save excel file java** पैटर्न है जिस पर कई एंटरप्राइज़ सर्विसेज़ निर्भर करती हैं।

## सामान्य pitfalls और प्रो टिप्स

- **Formula Evaluation Timing** – Aspose.Cells **स्वतः** `save` पर फ़ॉर्मूले का मूल्यांकन नहीं करता। यदि आपको गणना किए हुए मान चाहिए, तो सेव करने से पहले `wb.calculateFormula()` कॉल करें।
- **Dynamic Array Support** – `EXPAND` फ़ंक्शन केवल Excel 365 / 2021+ में उपलब्ध है। पुराने Excel संस्करणों में फ़ाइल खोलने पर `#NAME?` दिखेगा। यदि आपको लेगेसी क्लाइंट्स को सपोर्ट करना है, तो मैनुअल एक्सपैंशन पर वापस जाने पर विचार करें।
- **Locale Issues** – वर्कबुक के लोकेल की परवाह किए बिना अंग्रेज़ी फ़ंक्शन नाम (`EXPAND`) उपयोग करें; Aspose.Cells अंग्रेज़ी सिंटैक्स का पालन करता है।
- **Large Arrays** – हजारों पंक्तियों में एक्सपैंड करने से फ़ाइल आकार बढ़ सकता है। मेमोरी उपयोग पर नज़र रखें और बड़े डेटा सेट को स्ट्रीम करने पर विचार करें।

## पूर्ण कार्यशील उदाहरण

नीचे पूर्ण, स्व-निहित प्रोग्राम है जिसे आप IDE में कॉपी‑पेस्ट कर सकते हैं। इसमें सभी इम्पोर्ट्स, एरर हैंडलिंग, और मार्गदर्शन के लिए टिप्पणियाँ शामिल हैं।

```java
import com.aspose.cells.*;

public class ExpandDemoFull {
    public static void main(String[] args) {
        // Adjust these paths as needed
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/output.xlsx";

        try {
            // Step 1: Load an existing workbook or create a new one
            Workbook wb;
            if (new java.io.File(inputPath).exists()) {
                wb = new Workbook(inputPath);
                System.out.println("Loaded existing workbook.");
            } else {
                wb = new Workbook(); // brand‑new workbook
                System.out.println("Created a new workbook.");
            }

            // Step 2: Access the first worksheet
            Worksheet ws = wb.getWorksheets().get(0);

            // Step 3: Build a dynamic EXPAND formula (expand array to rows)
            int[] sourceArray = {1, 2, 3};
            int rowsDesired = 5;

            // Convert Java array to Excel literal syntax
            StringBuilder literal = new StringBuilder("{");
            for (int i = 0; i < sourceArray.length; i++) {
                literal.append(sourceArray[i]);
                if (i < sourceArray.length - 1) literal.append(",");
            }
            literal.append("}");

            String formula = String.format("=EXPAND(%s,%d)", literal, rowsDesired);
            ws.getCells().get("A1").setFormula(formula);
            System.out.println("Inserted formula: " + formula);

            // Optional: force calculation so the file contains values, not just formulas
            wb.calculateFormula();

            // Step 4: Save the workbook – **save excel file java** style
            wb.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error occurred: " + ex.getMessage());
            ex.printStackTrace();
        }
    }
}
```

### अपेक्षित आउटपुट

जब आप `output.xlsx` खोलते हैं:

| A   |
|-----|
| 1   |
| 2   |
| 3   |
| #N/A |
| #N/A |

यदि आप `rowsDesired` को `3` बदलते हैं, तो कॉलम तीसरी पंक्ति के बाद रुक जाएगा। `#N/A` प्लेसहोल्डर Excel का तरीका है यह बताने का कि “यहाँ डेटा नहीं है”—आप इसे `EXPAND` को चौथा आर्ग्यूमेंट पास करके बदल सकते हैं, जैसे `=EXPAND({1,

## अब आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [How to Insert Rows into Excel Workbooks Using Aspose.Cells for Java](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [How to Delete Rows in Excel Using Aspose.Cells for Java | Guide & Tutorial](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}