---
category: general
date: 2026-10-10
description: C# में Excel वर्कबुक बनाएं और WRAPCOLS फ़ंक्शन का उपयोग करके एरे डेटा
  को कॉलम में विभाजित करें। चलाने योग्य कोड के साथ एक पूर्ण चरण‑दर‑चरण गाइड का पालन
  करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- excel formula split data
- use wrapcols function
- how to use wrapcols
- split array columns
language: hi
lastmod: 2026-10-10
og_description: C# में Excel वर्कबुक बनाएं और एरे डेटा को कॉलम में विभाजित करने के
  लिए WRAPCOLS फ़ंक्शन लागू करें। यह गाइड पूर्ण कोड दिखाता है और प्रत्येक चरण की व्याख्या
  करता है।
og_image_alt: Screenshot of an Excel sheet showing three columns filled by the WRAPCOLS
  formula
og_title: C# में WRAPCOLS के साथ Excel वर्कबुक बनाएं और डेटा विभाजित करें
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  headline: How to create Excel workbook and split data with WRAPCOLS in C#
  type: TechArticle
- description: Create Excel workbook in C# and use the WRAPCOLS function to split
    array data into columns. Follow a complete step‑by‑step guide with runnable code.
  name: How to create Excel workbook and split data with WRAPCOLS in C#
  steps:
  - name: Using the function with different data types
    text: 'The `WRAPCOLS` function is not limited to numbers. You can split text values,
      dates, or mixed types:'
  - name: Variable column count at runtime
    text: 'Often the number of columns you need depends on user input. You can build
      the formula string dynamically:'
  - name: Large arrays and performance
    text: '`WRAPCOLS` can handle thousands of elements, but evaluating extremely large
      arrays in a single cell may increase calculation time. If you notice slowdown:'
  - name: Handling empty cells
    text: If the source array contains empty strings (`""`) or `NULL` values, `WRAPCOLS`
      inserts blank cells, preserving the column layout. This behavior is useful when
      you need placeholder columns for later data entry.
  - name: Using named ranges instead of literals
    text: 'For maintainability, define a named range that holds the source data, then
      reference it:'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में Excel वर्कबुक कैसे बनाएं और WRAPCOLS के साथ डेटा को विभाजित करें
url: /hi/net/excel-formulas-and-calculation-options/how-to-create-excel-workbook-and-split-data-with-wrapcols-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create Excel workbook and split data with WRAPCOLS in C#

यदि आपको प्रोग्रामेटिक रूप से **Excel workbook बनाना** है, तो यह गाइड आपको दिखाएगा कि इसे कैसे किया जाए और **array डेटा** को `WRAPCOLS` फ़ंक्शन का उपयोग करके कॉलम में कैसे विभाजित किया जाए। आपको एक पूर्ण, चलाने योग्य उदाहरण मिलेगा जो डेटा को तीन कॉलम में वितरित करते हुए `.xlsx` फ़ाइल उत्पन्न करता है।

यह ट्यूटोरियल सभी आवश्यक चीज़ें कवर करता है: आवश्यक NuGet पैकेज, प्रत्येक कोड लाइन, `WRAPCOLS` फ़ॉर्मूला क्यों काम करता है, और विभिन्न array आकार या कॉलम गिनती के लिए समाधान को कैसे अनुकूलित किया जाए। अंत तक आप किसी भी C# प्रोजेक्ट में Excel फ़ाइल जनरेट करने के लिए **use wrapcols function** तकनीक को एम्बेड कर पाएँगे।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 SDK या बाद का संस्करण स्थापित  
* एक C# IDE (Visual Studio, VS Code, Rider, आदि)  
* **Aspose.Cells for .NET** NuGet पैकेज – वह लाइब्रेरी जो उदाहरणों में उपयोग किए गए `Workbook` क्लास को प्रदान करती है  

आपको Office इंस्टॉल करने की आवश्यकता नहीं है; Aspose.Cells सीधे `.xlsx` फ़ाइल लिखता है।

## Step 1 – create Excel workbook

पहला कार्य नया workbook ऑब्जेक्ट बनाना और पहले worksheet का रेफ़रेंस प्राप्त करना है। यह चरण आगे की सभी मैनिपुलेशन की नींव है।

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();                // creates an empty Excel file in memory
        Worksheet ws = wb.Worksheets[0];             // the default worksheet is at index 0
```

`Workbook` पूरी फ़ाइल का प्रतिनिधित्व करता है, जबकि `Worksheet` एकल शीट का। मेमोरी में workbook बनाकर आप डिस्क I/O से बचते हैं जब तक आप इसे स्पष्ट रूप से सेव न करें।

## Step 2 – apply WRAPCOLS to split array columns

अब आप **A1** सेल में एक फ़ॉर्मूला रखेंगे जो `WRAPCOLS` का उपयोग करता है। फ़ंक्शन दो आर्ग्यूमेंट लेता है: स्रोत array और वह कॉलम संख्या जिसमें आप array को रैप करना चाहते हैं।

```csharp
        // Step 2: Apply the WRAPCOLS formula to split the array into 3 columns
        // The array {1,2,3,4,5,6} will be distributed as:
        // 1 2 3
        // 4 5 6
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

**Why this works:** `WRAPCOLS` फ्लैट array `{1,2,3,4,5,6}` को लेता है और worksheet को पंक्ति‑दर‑पंक्ति भरता है, प्रत्येक पंक्ति में तीन कॉलम बनाता है। पहला आर्ग्यूमेंट कोई भी Excel array literal, एक named range, या एक dynamic array फ़ॉर्मूला हो सकता है। दूसरा आर्ग्यूमेंट (`3`) Excel को बताता है कि अगली पंक्ति पर जाने से पहले कितने कॉलम जनरेट करने हैं।

### Using the function with different data types

`WRAPCOLS` फ़ंक्शन केवल संख्याओं तक सीमित नहीं है। आप टेक्स्ट वैल्यूज़, डेट्स, या मिश्रित प्रकारों को भी विभाजित कर सकते हैं:

```csharp
        // Example with mixed data: strings and numbers
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";
```

जब स्रोत array में स्ट्रिंग्स हों, तो Excel स्वचालित रूप से परिणाम को टेक्स्ट सेल्स के रूप में मानता है। यह लचीलापन आपको **excel formula split data** को रिपोर्टिंग, डैशबोर्ड, या डेटा‑माइग्रेशन कार्यों के लिए उपयोग करने की अनुमति देता है।

## Step 3 – calculate formulas so the worksheet is populated

फ़ॉर्मूले स्ट्रिंग्स के रूप में संग्रहीत रहते हैं जब तक आप workbook को उनका मूल्यांकन करने के लिए नहीं कहते। `CalculateFormula` को कॉल करने से मूल्यांकन होता है और परिणाम सेल्स में लिखे जाते हैं।

```csharp
        // Step 3: Calculate formulas so the worksheet is populated
        wb.CalculateFormula();   // evaluates all formulas in the workbook
```

इस कॉल के बिना सेव की गई फ़ाइल में केवल फ़ॉर्मूला टेक्स्ट रहेगा, गणना किए हुए मान नहीं। यह मेथड पूरे workbook पर काम करता है, इसलिए आप कहीं और अतिरिक्त फ़ॉर्मूले रख सकते हैं और वे सभी एक ही कॉल से हल हो जाएंगे।

## Step 4 – save the workbook to see the result

अंत में, workbook को डिस्क पर लिखें। ऐसी फ़ोल्डर चुनें जहाँ आपके पास लिखने की अनुमति हो, और फ़ाइल को स्पष्ट नाम दें।

```csharp
        // Step 4: Save the workbook to see the result
        string outputPath = @"output.xlsx";
        wb.Save(outputPath);      // creates output.xlsx in the application directory
    }
}
```

जब आप `output.xlsx` को Excel (या किसी भी संगत व्यूअर) में खोलेंगे, तो आपको यह दिखेगा:

| A | B | C |
|---|---|---|
| 1 | 2 | 3 |
| 4 | 5 | 6 |

यदि आपने मिश्रित‑प्रकार उदाहरण का उपयोग किया, तो पंक्तियाँ 3‑4 में क्रमशः टेक्स्ट और संख्याएँ होंगी।

## Advanced variations and edge‑case handling

### Variable column count at runtime

अक्सर आवश्यक कॉलम संख्या उपयोगकर्ता इनपुट पर निर्भर करती है। आप फ़ॉर्मूला स्ट्रिंग को डायनामिक रूप से बना सकते हैं:

```csharp
int columns = 4; // could come from UI, config, etc.
string arrayLiteral = "{10,20,30,40,50,60,70,80}";
ws.Cells[5, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
```

### Large arrays and performance

`WRAPCOLS` हजारों तत्वों को संभाल सकता है, लेकिन एक ही सेल में अत्यधिक बड़े arrays का मूल्यांकन करने से गणना समय बढ़ सकता है। यदि आप धीमी गति देखते हैं:

* स्रोत array को छोटे‑छोटे हिस्सों में विभाजित करें और प्रत्येक हिस्से को अलग प्रारंभिक सेल में लिखें।  
* `WorkbookSettings` का उपयोग करके मल्टी‑थ्रेडेड कैलकुलेशन सक्षम करें:

```csharp
wb.Settings.CalcMode = CalculationModeType.Automatic;
wb.Settings.EnableMultiThreadedCalc = true;
```

### Handling empty cells

यदि स्रोत array में खाली स्ट्रिंग्स (`""`) या `NULL` वैल्यूज़ हों, तो `WRAPCOLS` खाली सेल्स डालता है, जिससे कॉलम लेआउट बना रहता है। यह व्यवहार तब उपयोगी होता है जब आपको बाद में डेटा एंट्री के लिए प्लेसहोल्डर कॉलम चाहिए हों।

### Using named ranges instead of literals

मेंटेनेबिलिटी के लिए, एक named range परिभाषित करें जो स्रोत डेटा रखता हो, फिर उसका रेफ़रेंस दें:

```csharp
ws.Cells["D1:D6"].PutValue(new object[] { 11, 12, 13, 14, 15, 16 });
ws.Cells["E1"].Formula = "=WRAPCOLS(D1:D6,3)";
```

अब फ़ॉर्मूला worksheet स्वयं से डेटा पढ़ता है, जिससे **how to use wrapcols** को डायनामिक रिपोर्टिंग परिदृश्यों में उपयोग किया जा सकता है।

## Common pitfalls and pro tips

* **Do not omit the second argument.** `WRAPCOLS(array)` बिना कॉलम काउंट के केवल एक कॉलम लौटाता है, जिससे डेटा विभाजन का उद्देश्य विफल हो जाता है।  
* **Avoid mixing array dimensions.** स्रोत array एक‑डायमेंशनल होना चाहिए; दो‑डायमेंशनल array (जैसे `{ {1,2},{3,4} }`) देने पर `#VALUE!` त्रुटि आती है।  
* **Save after calculation.** यदि आप `wb.Save` को `CalculateFormula` से पहले कॉल करते हैं, तो फ़ाइल में केवल फ़ॉर्मूला टेक्स्ट रहेगा।  
* **Check file permissions.** प्रतिबंधित वातावरण (जैसे ASP.NET) में चलाते समय सुनिश्चित करें कि प्रोसेस आइडेंटिटी लक्ष्य फ़ोल्डर में लिख सकें।

## Full working example

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी, पेस्ट और रन कर सकते हैं। इसमें सभी इम्पोर्ट्स, एरर हैंडलिंग, और टिप्पणियाँ शामिल हैं।

```csharp
using System;
using Aspose.Cells;

class ExcelWrapColsDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Split a numeric array into 3 columns
        ws.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";

        // Split a mixed array (text + numbers) into 3 columns, starting at row 3
        ws.Cells[2, 0].Formula = "=WRAPCOLS({\"Jan\",\"Feb\",\"Mar\",100,200,300},3)";

        // Dynamically build a formula with a variable column count
        int columnCount = 4;
        string sourceArray = "{10,20,30,40,50,60,70,80}";
        ws.Cells[5, 0].Formula = $"=WRAPCOLS({sourceArray},{columnCount})";

        // Evaluate all formulas
        wb.CalculateFormula();

        // Save the workbook
        string outputPath = "output.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

प्रोग्राम चलाने पर `output.xlsx` उत्पन्न होगा जिसमें तीन अलग‑अलग क्षेत्रों में **excel formula split data** को `WRAPCOLS` फ़ंक्शन द्वारा प्रदर्शित किया गया है।

## Conclusion

अब आप जानते हैं कि **create Excel workbook** फ़ाइलें C# में कैसे बनायीँ और **use wrapcols function** का उपयोग करके **split array columns** को प्रभावी रूप से कैसे किया जाए। मुख्य चरण—`Workbook` का इंस्टैंसिएशन, `WRAPCOLS` फ़ॉर्मूला डालना, कैलकुलेशन, और सेव करना—किसी भी ऑटोमेशन टास्क के लिए पुन: उपयोग योग्य पैटर्न बनाते हैं जहाँ डेटा को कॉलम में वितरित करना आवश्यक हो।

अब आप कर सकते हैं:

* `WRAPCOLS` को अन्य dynamic‑array फ़ंक्शन्स जैसे `FILTER` या `SORT` के साथ संयोजित करें।  
* डेटाबेस से बड़े डेटा सेट एक्सपोर्ट करें और Excel को लेआउट स्वचालित रूप से संभालने दें।  
* यूज़र‑ड्रिवेन रिपोर्ट बनाएं जहाँ कॉलम काउंट UI कंट्रोल के माध्यम से चुना जाता है।

विभिन्न array स्रोतों, कॉलम काउंट, और अतिरिक्त फ़ॉर्मूले के साथ प्रयोग करें ताकि इस आधार को विस्तारित किया जा सके। Happy coding!

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच खोजने में मदद करेंगे।

- [How to Use WRAPCOLS in C# – Create Excel Workbook with Wrap Functions](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-create-excel-workbook-with-wrap-fun/)
- [Create Excel Workbook – Convert Array to Matrix with WRAPCOLS](/cells/english/net/calculation-engine/create-excel-workbook-convert-array-to-matrix-with-wrapcols/)
- [Create Excel Workbook C# – Step‑by‑Step Guide](/cells/english/net/excel-workbook/create-excel-workbook-c-step-by-step-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}