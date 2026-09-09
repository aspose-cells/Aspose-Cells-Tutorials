---
category: general
date: 2026-02-21
description: C# में शीघ्रता से सेल स्टाइल बनाएं। जानें कैसे एक सेल पर स्टाइल लागू
  करें, सेल में टेक्स्ट को केंद्रित करें, सेल संरेखण सेट करें, और सेल फ़ॉर्मेटिंग
  में निपुण बनें।
draft: false
keywords:
- create cell style
- apply style to cell
- center text in cell
- set cell alignment
- how to center text
language: hi
og_description: C# में सेल स्टाइल बनाएं और सीखें कि कैसे स्टाइल को सेल पर लागू करें,
  सेल में टेक्स्ट को केंद्रित करें, और स्पष्ट चरण‑दर‑चरण गाइड के साथ सेल अलाइनमेंट
  सेट करें।
og_title: C# में सेल स्टाइल बनाएं – एक सेल पर स्टाइल लागू करें और टेक्स्ट को केंद्रित
  करें
tags:
- C#
- Aspose.Cells
- Excel automation
title: C# में सेल स्टाइल बनाएं – सेल पर स्टाइल लागू करने और टेक्स्ट को केंद्रित करने
  का तरीका
url: /hi/net/excel-formatting-and-styling/create-cell-style-in-c-how-to-apply-style-to-a-cell-and-cent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में सेल स्टाइल बनाएं – स्टाइल लागू करने और टेक्स्ट सेंटर करने की पूरी गाइड

क्या आपको कभी **create cell style** Excel वर्कशीट में बनाना पड़ा लेकिन शुरू कहाँ से करें, समझ नहीं आया? आप अकेले नहीं हैं। कई ऑटोमेशन प्रोजेक्ट्स में, **apply style to cell** ऑब्जेक्ट्स की क्षमता एक साधारण स्प्रेडशीट और एक पॉलिश्ड रिपोर्ट के बीच का अंतर बनाती है।  

इस ट्यूटोरियल में हम एक पूर्ण, रन करने योग्य उदाहरण के माध्यम से दिखाएंगे कि **how to center text** एक सेल के अंदर कैसे किया जाए, एलाइनमेंट सेट किया जाए, और एक पतली बॉर्डर जोड़ी जाए—सिर्फ कुछ ही लाइनों के C# कोड में। अंत तक आप समझ जाएंगे कि हर भाग क्यों महत्वपूर्ण है और इसे अपने परिदृश्यों के अनुसार कैसे कस्टमाइज़ किया जाए।

## आप क्या सीखेंगे

- Aspose.Cells (या किसी समान लाइब्रेरी) का उपयोग करके **create cell style** वर्कफ़्लो की स्पष्ट समझ।
- वह सटीक कोड जिसे आप कॉपी‑पेस्ट करके एक कंसोल ऐप में **apply style to cell** कर सकते हैं।
- **center text in cell**, **set cell alignment** और मर्ज्ड सेल या कस्टम नंबर फ़ॉर्मेट जैसे एज केस को कैसे हैंडल करें, इस पर अंतर्दृष्टि।
- स्टाइल को विस्तारित करने के टिप्स—विभिन्न फ़ॉन्ट, बैकग्राउंड रंग, या कंडीशनल फ़ॉर्मेटिंग।

> **Prerequisite:** Visual Studio 2022 (या कोई भी C# IDE) और Aspose.Cells for .NET NuGet पैकेज। अन्य कोई डिपेंडेंसी आवश्यक नहीं है।

---

## Step 1: Set Up Your Project and Import Namespaces

**create cell style** करने से पहले हमें एक प्रोजेक्ट चाहिए जो Excel लाइब्रेरी को रेफ़रेंस करता हो।

```csharp
// Program.cs – entry point
using System;
using Aspose.Cells;   // Make sure the Aspose.Cells NuGet package is installed

class Program
{
    static void Main()
    {
        // We'll fill in the rest of the steps here.
    }
}
```

*Why this matters:* `Aspose.Cells` को इम्पोर्ट करने से हमें `Workbook`, `Worksheet`, `Style`, और `Border` क्लासेज़ तक पहुंच मिलती है। यदि आप कोई अलग लाइब्रेरी (जैसे EPPlus) उपयोग कर रहे हैं, तो क्लास नाम बदल सकते हैं लेकिन अवधारणा वही रहती है।

---

## Step 2: Create a Workbook and Grab the First Cell

अब हम **create cell style** करते हैं, पहले उस सेल का रेफ़रेंस लेकर जिसे हम फॉर्मेट करना चाहते हैं।

```csharp
// Inside Main()
Workbook workbook = new Workbook();           // New, empty workbook
Worksheet ws = workbook.Worksheets[0];        // First worksheet (index 0)

// Step 1: Get a reference to the first cell (row 0, column 0) in the worksheet
Cell firstCell = ws.Cells[0, 0];               // A1 in Excel terms
firstCell.PutValue("Hello, styled world!");
```

ध्यान दें कि हमने `var` की बजाय `Cell` का उपयोग किया है—स्पष्ट टाइपिंग कोड को नए लोगों के लिए अधिक समझने योग्य बनाती है। `PutValue` कॉल एक स्ट्रिंग लिखता है ताकि बाद में हम स्टाइल इफ़ेक्ट देख सकें।

---

## Step 3: Define the Style – Center Text, Add a Thin Border

यहाँ **create cell style** ऑपरेशन का मुख्य भाग है। हम हॉरिज़ॉन्टल एलाइनमेंट, एक पतली बॉर्डर, और कुछ वैकल्पिक सौंदर्य सेट करेंगे।

```csharp
// Step 2: Define a style that centers the text and adds a thin border
Style cellStyle = workbook.CreateStyle();          // Create a fresh Style object
cellStyle.HorizontalAlignment = TextAlignmentType.Center; // Center text horizontally
cellStyle.VerticalAlignment = TextAlignmentType.Center;   // Center vertically – often forgotten
cellStyle.Borders[BorderType.TopBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.LeftBorder].LineStyle = CellBorderType.Thin;
cellStyle.Borders[BorderType.RightBorder].LineStyle = CellBorderType.Thin;

// Optional: set a light gray background to make the border pop
cellStyle.ForegroundColor = System.Drawing.Color.LightGray;
cellStyle.Pattern = BackgroundType.Solid;
```

*Why we do this:*  
- **HorizontalAlignment** और **VerticalAlignment** मिलकर “**how to center text** in a cell?” सवाल का जवाब देते हैं।  
- सभी चार बॉर्डर जोड़ने से सेल एक बॉक्स्ड लेबल जैसा दिखता है, जो हेडर के लिए उपयोगी है।  
- बैकग्राउंड कलर आवश्यक नहीं है, लेकिन यह दिखाता है कि आप बाद में स्टाइल को कैसे विस्तारित कर सकते हैं।

---

## Step 4: Apply the Defined Style to the Selected Cell

अब स्टाइल मौजूद है, हम **apply style to cell** एक ही मेथड कॉल से करेंगे।

```csharp
// Step 3: Apply the defined style to the selected cell
firstCell.SetStyle(cellStyle);
```

बस—Aspose.Cells स्टाइल को सेल की इंटरनल स्टाइल कलेक्शन में कॉपी कर देता है। यदि आपको समान फ़ॉर्मेटिंग रेंज पर चाहिए, तो आप `ws.Cells.CreateRange("A1:D1").ApplyStyle(cellStyle, new StyleFlag { All = true });` का उपयोग कर सकते हैं।

---

## Step 5: Save the Workbook and Verify the Result

एक तेज़ सेव से आप फ़ाइल को Excel में खोल सकते हैं और पुष्टि कर सकते हैं कि टेक्स्ट वास्तव में सेंटर है और बॉर्डर दिखाई दे रहा है।

```csharp
// Save the workbook to disk
string outputPath = "StyledCell.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
```

*Expected output:* जब आप **StyledCell.xlsx** खोलेंगे, तो सेल **A1** में “Hello, styled world!” हॉरिज़ॉन्टली और वर्टिकली दोनों सेंटर होगा, पतली ग्रे बॉर्डर से घिरा होगा, और हल्के‑ग्रे बैकग्राउंड पर होगा।

---

## Common Variations & Edge Cases

### 1. Center Text in a Merged Region

यदि आप सेल **A1:C1** को मर्ज करते हैं और फिर भी टेक्स्ट सेंटर चाहते हैं, तो मर्ज करने के **बाद** टॉप‑लेफ़्ट सेल पर स्टाइल लागू करें:

```csharp
ws.Cells.Merge(0, 0, 1, 3); // Merge A1:C1
firstCell.SetStyle(cellStyle); // Style still works because it’s applied to the anchor cell
```

### 2. Using a Numeric Format

कभी‑कभी आपको **set cell alignment** के साथ-साथ नंबर को एक विशिष्ट फ़ॉर्मेट में दिखाना पड़ता है:

```csharp
cellStyle.Custom = "#,##0.00"; // Two decimal places
firstCell.PutValue(12345.678);
firstCell.SetStyle(cellStyle);
```

एलाइनमेंट सेंटर रहता है जबकि नंबर `12,345.68` के रूप में दिखता है।

### 3. Reusing Styles Efficiently

हर सेल के लिए नया `Style` बनाना प्रदर्शन को नुकसान पहुंचा सकता है। इसके बजाय, एक स्टाइल ऑब्जेक्ट बनाएं और उसे कई सेल या रेंज में पुन: उपयोग करें। `StyleFlag` क्लास आपको केवल उन भागों को लागू करने देती है जिनकी आपको ज़रूरत है, जिससे मेमोरी बचती है।

```csharp
StyleFlag flag = new StyleFlag { HorizontalAlignment = true, Borders = true };
ws.Cells.CreateRange("B2:B10").ApplyStyle(cellStyle, flag);
```

---

## Pro Tips & Pitfalls to Watch

- **Don’t forget vertical alignment** – केवल हॉरिज़ॉन्टल सेंटरिंग अक्सर टालरहित दिखती है, खासकर ऊँची पंक्तियों में।  
- **Border types**: `CellBorderType.Thin` अधिकांश रिपोर्ट्स के लिए ठीक है, लेकिन आप विज़ुअल हाइरार्की के लिए `Medium` या `Dashed` में स्विच कर सकते हैं।  
- **Color handling**: .NET Core को टार्गेट करते समय `System.Drawing.Color` को `System.Drawing.Common` पैकेज से उपयोग करें; अन्यथा रनटाइम एरर आएगा।  
- **Saving format**: यदि आपको पुराने Excel संस्करणों के साथ संगतता चाहिए, तो `SaveFormat.Xlsx` को `SaveFormat.Xls` में बदलें।

---

![Create cell style example](https://example.com/images/create-cell-style.png "C# में सेल स्टाइल बनाना")

*Alt text: एक सेल का स्क्रीनशॉट जिसमें टेक्स्ट सेंटर किया गया है और पतली बॉर्डर है, जो create cell style ट्यूटोरियल द्वारा बनाया गया है।*

---

## Full Working Example (Copy‑Paste Ready)

```csharp
using System;
using Aspose.Cells;
using System.Drawing; // For Color

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Grab the first cell and put a sample value
        Cell firstCell = ws.Cells[0, 0];
        firstCell.PutValue("Hello, styled world!");

        // 3️⃣ Create the style: center text, thin border, light gray background
        Style cellStyle = workbook.CreateStyle();
        cellStyle.HorizontalAlignment = TextAlignmentType.Center;
        cellStyle.VerticalAlignment   = TextAlignmentType.Center;
        cellStyle.Borders[BorderType.TopBorder].LineStyle    = CellBorderType.Thin;
        cellStyle.Borders[BorderType.BottomBorder].LineStyle = CellBorderType.Thin;
        cellStyle.Borders[BorderType.LeftBorder].LineStyle   = CellBorderType.Thin;
        cellStyle.Borders[BorderType.RightBorder].LineStyle  = CellBorderType.Thin;
        cellStyle.ForegroundColor = Color.LightGray;
        cellStyle.Pattern = BackgroundType.Solid;

        // 4️⃣ Apply the style to the cell
        firstCell.SetStyle(cellStyle);

        // 5️⃣ Save the result
        string outputPath = "StyledCell.xlsx";
        workbook.Save(outputPath, SaveFormat.Xlsx);
        Console.WriteLine($"Workbook saved to {outputPath}. Open it to see the styled cell.");
    }
}
```

इस प्रोग्राम को चलाएँ, **StyledCell.xlsx** खोलें, और आप पहले वर्णित सटीक परिणाम देखेंगे। टेक्स्ट, बॉर्डर स्टाइल, या बैकग्राउंड कलर को बदलकर इसे अपने ब्रांडिंग के अनुसार कस्टमाइज़ करें।

---

## Conclusion

हमने अभी-अभी **created cell style** शून्य से बनाया, **applied style to cell** किया, और **how to center text** दोनों हॉरिज़ॉन्टली और वर्टिकली दिखाया। इन बिल्डिंग ब्लॉक्स को मास्टर करके आप हेडर फॉर्मेट कर सकते हैं, टोटल हाइलाइट कर सकते हैं, या पूरी रिपोर्ट टेम्पलेट बना सकते हैं बिना C# छोड़े।  

यदि आप अगले कदमों के बारे में जिज्ञासु हैं, तो कोशिश करें:

- **Applying the same style to a whole row** (`ws.Cells.CreateRange("A2:E2").ApplyStyle(cellStyle, new StyleFlag { All = true });`)।  
- **Adding conditional formatting** ताकि सेल वैल्यू के आधार पर बैकग्राउंड बदल सके।  
- **Exporting to PDF** जबकि स्टाइल बरकरार रहे।

याद रखें, स्टाइलिंग केवल सौंदर्य नहीं, बल्कि पठनीयता भी है। प्रयोग करें, दोहराएँ, और जल्द ही आपके स्प्रेडशीट्स आपके कोड जितने ही प्रोफ़ेशनल दिखेंगे।

*Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}