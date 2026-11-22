---
category: general
date: 2026-11-22
description: Aspose.Cells का उपयोग करके जावा में wrapcols का उपयोग करके एक रेंज को
  कॉलम में बदलना सीखें। यह गाइड wrap columns एक्सेल फ़ंक्शन को चरण‑दर‑चरण समझाता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- convert range to columns
- wrap columns excel function
language: hi
lastmod: 2026-11-22
og_description: जावा में wrapcols का उपयोग करके रेंज को कॉलम में कैसे बदलें। Aspose.Cells
  के साथ wrap columns एक्सेल फ़ंक्शन में महारत हासिल करने के लिए इस ट्यूटोरियल का
  अनुसरण करें।
og_image_alt: Screenshot showing how to use wrapcols formula in Excel
og_title: Java में wrapcols का उपयोग कैसे करें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  headline: How to use wrapcols in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to use wrapcols in Java to convert a range to columns using
    Aspose.Cells. This guide walks through the wrap columns excel function step by
    step.
  name: How to use wrapcols in Java with Aspose.Cells
  steps:
  - name: Load the workbook
    text: '```java import com.aspose.cells.*;'
  - name: Access the first worksheet
    text: '```java // Step 2: Access the first worksheet Worksheet worksheet = workbook.getWorksheets().get(0);
      ```'
  - name: Set the WRAPCOLS formula
    text: '```java // Step 3: Set the WRAPCOLS formula in cell A1 worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10,
      3)"); ```'
  - name: Save the workbook
    text: '```java // Step 4: Save the workbook with the formula applied workbook.save("YOUR_DIRECTORY/output.xlsx");
      } } ```'
  - name: Expected output
    text: 'When you open `output.xlsx`, cells `A1:C4` (or however many rows are needed)
      will contain the original list from `A1:A10` spread across three columns. The
      layout looks like this:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Aspose.Cells के साथ Java में wrapcols का उपयोग कैसे करें
url: /hi/java/range-management/how-to-use-wrapcols-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to use wrapcols in Java with Aspose.Cells

यदि आपको **how to use wrapcols** की आवश्यकता है ताकि Excel वर्कबुक में डेटा को पुनः आकार दिया जा सके, तो यह ट्यूटोरियल पूरी प्रक्रिया दिखाता है। आप देखेंगे कि WRAPCOLS फ़ॉर्मूला एक वर्टिकल रेंज को कई कॉलम में कैसे बदलता है, जिससे सूची को साइड‑बाय‑साइड प्रस्तुत करना आसान हो जाता है।

यह गाइड वह सब कवर करता है जिसकी आपको जरूरत है: वर्कबुक लोड करना, WRAPCOLS फ़ॉर्मूला लागू करना, और परिणाम को सहेजना। कोई बाहरी रेफ़रेंस आवश्यक नहीं है, इसलिए आप कोड को कॉपी करके तुरंत चला सकते हैं। साथ ही हम *wrap columns excel function* की व्याख्या करेंगे और सामान्य रिपोर्टिंग परिदृश्यों के लिए **convert range to columns** कैसे किया जाए, यह दिखाएंगे।

## What you’ll need

- Java 17 या नया संस्करण  
- Aspose.Cells for Java (नवीनतम संस्करण)  
- एक Java IDE (IntelliJ IDEA, Eclipse, या VS Code)  
- एक इनपुट Excel फ़ाइल (`input.xlsx`) जिसमें कॉलम A में डेटा हो  

## How to use wrapcols in Java with Aspose.Cells

निम्नलिखित चार चरण **how to use wrapcols** वर्कफ़्लो को लागू करते हैं। प्रत्येक चरण में एक कोड स्निपेट, उसका महत्व, और सामान्य त्रुटियों से बचने के लिए एक टिप शामिल है।

### Step 1: Load the workbook

```java
import com.aspose.cells.*;

public class WrapColsExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Load a workbook (or create a new one)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Why this step matters*: `Workbook` Aspose.Cells में सभी Excel ऑपरेशन्स का एंट्री पॉइंट है। फ़ाइल को लोड करने से आपको वर्कशीट्स, सेल्स, और फ़ॉर्मूले तक पहुँच मिलती है।  

**Pro tip**: विकास के दौरान `FileNotFoundException` से बचने के लिए एक एब्सोल्यूट पाथ उपयोग करें। प्रोजेक्ट पैकेज होने के बाद रिलेटिव पाथ पर स्विच करें।

### Step 2: Access the first worksheet

```java
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

पहली वर्कशीट (`index 0`) आमतौर पर वह डेटा रखती है जिसे आप ट्रांसफ़ॉर्म करना चाहते हैं। यदि आपका डेटा किसी अन्य शीट में है, तो इंडेक्स बदलें या `get("SheetName")` का उपयोग करें।  

**Why this step matters**: सही वर्कशीट के साथ काम करने से WRAPCOLS फ़ॉर्मूला इच्छित रेंज को रेफ़र करता है।

### Step 3: Set the WRAPCOLS formula

```java
        // Step 3: Set the WRAPCOLS formula in cell A1
        worksheet.getCells().get("A1").setFormula("=WRAPCOLS(A1:A10, 3)");
```

`WRAPCOLS(range, columns)` **wrap columns excel function** है जो `range` के मानों को निर्दिष्ट कॉलम संख्या में वितरित करता है। इस उदाहरण में हम `A1:A10` की वैल्यूज़ को तीन कॉलम में रैप करते हैं, शुरूआत `A1` से।  

**Why this step matters**: फ़ॉर्मूला भारी काम करता है—कोई मैन्युअल लूपिंग या एरे हैंडलिंग आवश्यक नहीं।  

**Tip for convert range to columns**: दूसरे आर्ग्यूमेंट (`3`) को अपनी आवश्यक कॉलम संख्या के अनुसार समायोजित करें। यदि रेंज की लंबाई कॉलम संख्या का गुणज नहीं है, तो अंतिम कॉलम में शेष आइटम रखे जाएंगे।

### Step 4: Save the workbook

```java
        // Step 4: Save the workbook with the formula applied
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

सेव करने से WRAPCOLS फ़ॉर्मूला `output.xlsx` में लिखा जाता है। जब आप फ़ाइल को Excel में खोलेंगे, तो फ़ॉर्मूला मूल्यांकन करेगा और डेटा को कॉलम में रैप करके दिखाएगा।  

**Why this step matters**: वर्कबुक को स्थायी बनाकर आप परिणाम की पुष्टि कर सकते हैं और फ़ाइल को गैर‑Java उपयोगकर्ताओं के साथ साझा कर सकते हैं।

![Wrapcols formula applied in Excel](wrapcols-example.png){: .align-center alt="How to use wrapcols in Excel screenshot"}

### Expected output

जब आप `output.xlsx` खोलेंगे, तो सेल्स `A1:C4` (या आवश्यकतानुसार अधिक पंक्तियाँ) में मूल सूची `A1:A10` के आइटम तीन कॉलम में वितरित दिखेंगे। लेआउट इस प्रकार होगा:

| A | B | C |
|---|---|---|
| Item 1 | Item 4 | Item 7 |
| Item 2 | Item 5 | Item 8 |
| Item 3 | Item 6 | Item 9 |
| Item 10 |   |   |

**wrap columns excel function** स्वचालित रूप से खाली सेल्स को ब्लैंक्स से भर देता है, इसलिए अतिरिक्त क्लीन‑अप कोड की आवश्यकता नहीं है।

## Understanding the wrap columns excel function

WRAPCOLS फ़ॉर्मूला Excel 365 में पेश किए गए डायनामिक एरे फ़ंक्शन्स का हिस्सा है। यह `TEXTSPLIT` के समान है, लेकिन कॉलम‑वाइज वितरण पर केंद्रित है।  

- **Syntax**: `=WRAPCOLS(source_range, columns)`  
- **Parameters**:  
  - `source_range` – वह वर्टिकल रेंज जिसे आप पुनः आकार देना चाहते हैं।  
  - `columns` – डेटा को रैप करने के लिए कॉलमों की संख्या।  

जब आप `=WRAPCOLS(A1:A10, 3)` कॉल करते हैं, तो Excel स्रोत को एक‑डायमेंशनल एरे मानता है और पहले कॉलम, फिर दूसरे, और इसी प्रकार भरता है, जब तक सभी वैल्यूज़ रखी नहीं जातीं। यह **how to use wrapcols** को एक सिंगल कॉलम सूची को मल्टी‑कॉलम रिपोर्ट में बदलने के लिए VBA के बिना एक आदर्श टूल बनाता है।

## Convert range to columns without formulas (optional)

यदि आप **convert range to columns** ऑपरेशन पूरी तरह Java में करना चाहते हैं—Excel के कैलकुलेशन इंजन पर निर्भर हुए बिना—तो आप स्रोत वैल्यूज़ पढ़ सकते हैं, दो‑डायमेंशनल एरे बना सकते हैं, और मैन्युअली लिख सकते हैं:

```java
        // Optional: programmatic conversion without WRAPCOLS
        Cells cells = worksheet.getCells();
        int rows = 10; // A1:A10
        int cols = 3;
        String[][] matrix = new String[rows][cols];

        // Fill matrix column‑wise
        for (int i = 0; i < rows; i++) {
            String value = cells.get(i, 0).getStringValue(); // column A
            int colIdx = i % cols;
            int rowIdx = i / cols;
            matrix[rowIdx][colIdx] = value;
        }

        // Write matrix back starting at A1
        for (int r = 0; r < rows / cols + 1; r++) {
            for (int c = 0; c < cols; c++) {
                if (matrix[r][c] != null) {
                    cells.get(r, c).putValue(matrix[r][c]);
                }
            }
        }
```

यह स्निपेट दिखाता है कि जब आपको आउटपुट पर पूर्ण नियंत्रण चाहिए (जैसे प्रत्येक कॉलम के लिए कस्टम फ़ॉर्मेटिंग लागू करना) तो **convert range to columns** कैसे किया जा सकता है। हालांकि, WRAPCOLS के माध्यम से **wrap columns excel function** का उपयोग आमतौर पर अधिक संक्षिप्त होता है और Excel को री‑कैल्कुलेशन स्वचालित रूप से संभालने देता है।

## Edge cases and best practices

- **Empty cells**: WRAPCOLS खाली सेल्स को ब्लैंक्स के रूप में मानता है। यदि आपके स्रोत रेंज में गैप हैं, तो आउटपुट में वही ब्लैंक्स रहेंगे।  
- **Dynamic ranges**: एक नेम्ड रेंज या टेबल रेफ़रेंस (`Table1[Column]`) का उपयोग करें ताकि फ़ॉर्मूला पंक्तियों के जोड़ने पर भी अनुकूलित हो सके।  
- **Performance**: फ़ॉर्मूला लागू करना O(1) है क्योंकि Excel इसे लेज़ीली इवैल्युएट करता है। ऊपर दिखाया गया प्रोग्रामेटिक कन्वर्ज़न O(n) है और बहुत बड़े रेंज के लिए धीमा हो सकता है।  
- **Version compatibility**: WRAPCOLS फ़ंक्शन को Excel 365 या उसके बाद के संस्करण की आवश्यकता होती है। यदि आपको पुराने संस्करणों को सपोर्ट करना है, तो Java‑साइड कन्वर्ज़न मेथड का उपयोग करें।

## How to use wrapcols in other scenarios

- **Reporting dashboards**: KPI नामों की वर्टिकल सूची को तीन कॉलम प्रति पंक्ति वाले कॉम्पैक्ट टेबल में बदलें।  
- **Data entry forms**: उपयोगकर्ता इनपुट की कॉलम को साइड‑बाय‑साइड लेआउट में बदलें जिससे विज़ुअल तुलना आसान हो।  
- **Exporting to CSV**: WRAPCOLS लागू करने के बाद वर्कबुक को CSV के रूप में सहेजें ताकि कॉलम लेआउट के अनुरूप डिलिमिटेड व्यू प्राप्त हो सके।

इन सभी मामलों में वही **how to use wrapcols** पैटर्न फॉलो किया जाता है: लोड, रेफ़रेंस, फ़ॉर्मूला सेट, सेव।

## Conclusion

अब आप जानते हैं कि **how to use wrapcols** को Java में Aspose.Cells के साथ कैसे लागू किया जाता है ताकि **convert range to columns** प्रभावी रूप से किया जा सके। `WRAPCOLS` फ़ॉर्मूला का उपयोग करके आप नेटीव *wrap columns excel function* का लाभ उठाते हैं, जिससे आपका कोड संक्षिप्त रहता है और Excel को कैलकुलेशन और डिस्प्ले का पूरा नियंत्रण मिलता है।  

विभिन्न कॉलम काउंट, डायनामिक रेंज, या वैकल्पिक Java‑साइड कन्वर्ज़न के साथ प्रयोग करें ताकि आपके प्रोजेक्ट की जरूरतों को पूरा किया जा सके। जब आप इस तकनीक में निपुण हो जाएंगे, तो Excel में डेटा को री‑शेप करना एक‑लाइन ऑपरेशन बन जाएगा, न कि मैन्युअल मेहनत।

---


## What Should You Learn Next?


निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to use wrapcols to convert a list into multiple columns in Java](/cells/english/java/formulas-functions/how-to-use-wrapcols-to-convert-a-list-into-multiple-columns/)
- [How to Use WRAPCOLS in Java – Complete Guide to Excel Array Formulas](/cells/english/java/integration-interoperability/how-to-use-wrapcols-in-java-complete-guide-to-excel-array-fo/)
- [How to Use WRAPCOLS in Java – Complete Excel WRAPCOLS Example](/cells/english/java/formulas-functions/how-to-use-wrapcols-in-java-complete-excel-wrapcols-example/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}