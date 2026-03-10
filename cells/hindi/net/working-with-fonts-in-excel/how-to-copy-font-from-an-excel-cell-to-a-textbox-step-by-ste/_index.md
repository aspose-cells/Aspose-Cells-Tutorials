---
category: general
date: 2026-02-15
description: C# में फ़ॉन्ट कॉपी करने और सेल स्टाइल लागू करने का सरल उदाहरण। जानें
  कि कैसे सेल स्टाइल प्राप्त करें और सेल फ़ॉर्मेटिंग का उपयोग करके टेक्स्टबॉक्स का
  फ़ॉन्ट आकार सेट करें।
draft: false
keywords:
- how to copy font
- apply cell style
- get cell style
- use cell formatting
- set textbox font size
language: hi
og_description: वर्कशीट की सेल से फ़ॉन्ट कॉपी करके उसे टेक्स्टबॉक्स पर लागू कैसे करें।
  यह गाइड दिखाता है कि सेल स्टाइल कैसे प्राप्त करें, सेल फ़ॉर्मेटिंग का उपयोग करें,
  और टेक्स्टबॉक्स का फ़ॉन्ट आकार सेट करें।
og_title: Excel सेल से फ़ॉन्ट कैसे कॉपी करें – पूर्ण C# ट्यूटोरियल
tags:
- C#
- EPPlus
- UI‑grid
- Excel‑interop
title: Excel सेल से फ़ॉन्ट को TextBox में कॉपी कैसे करें – चरण‑दर‑चरण गाइड
url: /hi/net/working-with-fonts-in-excel/how-to-copy-font-from-an-excel-cell-to-a-textbox-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कैसे Excel सेल से फ़ॉन्ट को TextBox में कॉपी करें – पूरा C# ट्यूटोरियल

क्या आपको कभी **फ़ॉन्ट कॉपी** करना पड़ा है किसी स्प्रेडशीट सेल से और UI टेक्स्ट बॉक्स को बिल्कुल वही दिखाना पड़ा है? आप अकेले नहीं हैं। कई रिपोर्टिंग टूल्स या कस्टम डैशबोर्ड्स में आप अक्सर Excel से डेटा निकालते हैं और फिर फ़ॉन्ट फ़ैमिली, साइज और colour जैसी विज़ुअल फ़िडेलिटी को बरकरार रखने की कोशिश करते हैं।  

अच्छी खबर यह है कि कुछ ही लाइनों के C# कोड से आप **सेल स्टाइल प्राप्त** कर सकते हैं, उसकी फ़ॉन्ट प्रॉपर्टीज़ पढ़ सकते हैं, और **सेल स्टाइल लागू** कर सकते हैं किसी भी टेक्स्ट‑बॉक्स कंट्रोल पर। इस ट्यूटोरियल में हम एक पूर्ण, रन करने योग्य उदाहरण के माध्यम से दिखाएंगे कि कैसे **सेल फ़ॉर्मेटिंग का उपयोग** करें और प्रोग्रामेटिकली **टेक्स्टबॉक्स फ़ॉन्ट साइज सेट** करें।

---

## आप क्या सीखेंगे

- कैसे एक `TextBox` ऑब्जेक्ट को ग्रिड कंपोनेंट (`gridJs` हमारे सैंपल में) से प्राप्त करें
- कैसे एक विशिष्ट Excel सेल (`B2`) से फ़ॉन्ट फ़ैमिली, साइज और colour पढ़ें
- कैसे उन फ़ॉन्ट एट्रिब्यूट्स को टेक्स्ट बॉक्स में कॉपी करें ताकि UI स्प्रेडशीट की तरह दिखे
- सामान्य pitfalls (जैसे colour कन्वर्ज़न) और कुछ **प्रो टिप्स** जो आपके कोड को मजबूत बनाते हैं
- एक तैयार‑से‑रन कोड स्निपेट जो आप सीधे एक console app या WinForms प्रोजेक्ट में डाल सकते हैं

**Prerequisites**  
आपके पास होना चाहिए:

1. .NET 6+ (या .NET Framework 4.8) इंस्टॉल हो  
2. EPPlus NuGet पैकेज (Excel हैंडलिंग के लिए)  
3. एक ग्रिड कंट्रोल जो `TextBoxes` डिक्शनरी एक्सपोज़ करता हो (उदाहरण में एक काल्पनिक `gridJs` इस्तेमाल किया गया है लेकिन विचार किसी भी UI लाइब्रेरी में काम करेगा)

अब चलिए काम शुरू करते हैं।

---

## Step 1: प्रोजेक्ट सेट अप करें और Worksheet लोड करें

पहले, एक नया console या WinForms प्रोजेक्ट बनाएं और EPPlus जोड़ें:

```bash
dotnet add package EPPlus --version 6.*
```

फिर, वर्कबुक लोड करें और उस सेल को पकड़ें जिसका स्टाइल आप कॉपी करना चाहते हैं।

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System.Drawing;

// ...

// Load the Excel file (make sure the file exists at the given path)
var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
using var package = new ExcelPackage(fileInfo);
ExcelWorksheet ws = package.Workbook.Worksheets["Sheet1"]; // adjust sheet name if needed

// Retrieve the style of cell B2
ExcelStyle cellStyle = ws.Cells["B2"].Style;
```

**यह क्यों महत्वपूर्ण है:** EPPlus आपको `Style` ऑब्जेक्ट तक सीधे पहुँच देता है, जिसमें `Font` सब‑ऑब्जेक्ट होता है। यहाँ से आप `Name`, `Size`, और `Color` पढ़ सकते हैं। यह **सेल स्टाइल प्राप्त** करने का मूल भाग है।

---

## Step 2: अपने ग्रिड से टार्गेट TextBox प्राप्त करें

मान लीजिए आपका UI ग्रिड (`gridJs`) टेक्स्ट बॉक्स को कॉलम नाम के आधार पर डिक्शनरी में स्टोर करता है, तो आप इसे इस तरह प्राप्त कर सकते हैं:

```csharp
// Fake grid class for illustration – replace with your actual grid component
var gridJs = new MyGrid(); // MyGrid is a placeholder for your UI control

// Step 1: Retrieve the "Notes" text box from the grid
var notesTextBox = gridJs.TextBoxes["Notes"];
```

यदि आप WinForms इस्तेमाल कर रहे हैं, तो `notesTextBox` एक `TextBox` कंट्रोल हो सकता है; WPF में यह एक `TextBox` एलिमेंट हो सकता है, और वेब‑बेस्ड ग्रिड में यह एक JavaScript इंटरऑप ऑब्जेक्ट हो सकता है। मुख्य बात यह है कि आपके पास एक रेफ़रेंस हो जिसे आप मैनीपुलेट कर सकें।

---

## Step 3: फ़ॉन्ट फ़ैमिली ट्रांसफ़र करें

अब हमारे पास स्रोत स्टाइल और डेस्टिनेशन कंट्रोल दोनों हैं, फ़ॉन्ट फ़ैमिली कॉपी करें।

```csharp
// Apply the cell's font family to the text box
notesTextBox.FontFamily = cellStyle.Font.Name;
```

**प्रो टिप:** सभी UI फ्रेमवर्क्स `FontFamily` प्रॉपर्टी को साधारण स्ट्रिंग के रूप में एक्सपोज़ नहीं करते। WinForms में आप `notesTextBox.Font = new Font(cellStyle.Font.Name, notesTextBox.Font.Size);` सेट करेंगे। उसी अनुसार एडजस्ट करें।

---

## Step 4: फ़ॉन्ट साइज ट्रांसफ़र करें

फ़ॉन्ट साइज EPPlus में `float` के रूप में स्टोर होता है। इसे सीधे लागू करें:

```csharp
// Apply the cell's font size to the text box
notesTextBox.FontSize = cellStyle.Font.Size;
```

यदि आपका कंट्रोल पॉइंट्स (ज्यादातर करते हैं) इस्तेमाल करता है, तो आप वैल्यू को बिना किसी कन्वर्ज़न के असाइन कर सकते हैं। CSS‑आधारित ग्रिड्स में आपको `"pt"` जोड़ना पड़ सकता है।

---

## Step 5: फ़ॉन्ट colour ट्रांसफ़र करें

colour कन्वर्ज़न सबसे जटिल हिस्सा है क्योंकि EPPlus colour को ARGB इंटीजर के रूप में स्टोर करता है, जबकि कई UI फ्रेमवर्क्स `System.Drawing.Color` या CSS hex स्ट्रिंग की अपेक्षा करते हैं।

```csharp
// Apply the cell's font colour to the text box
// EPPlus stores colour as a System.Drawing.Color when using .Color property
var excelColor = cellStyle.Font.Color?.GetColor();

// Fallback to black if the cell has no explicit colour
var safeColor = excelColor ?? Color.Black;

// Convert to the format your UI expects (example for WinForms)
notesTextBox.FontColor = safeColor;
```

> **यह क्यों काम करता है:** `GetColor()` थीम‑बेस्ड colour को रिजॉल्व करता है और एक ठोस `System.Drawing.Color` रिटर्न करता है। यदि सेल डिफ़ॉल्ट colour (कोई स्पष्ट सेटिंग नहीं) इस्तेमाल कर रहा है, तो हम null रेफ़रेंस एक्सेप्शन से बचने के लिए डिफ़ॉल्ट रूप में ब्लैक सेट करते हैं।

---

## Full Working Example

सब कुछ मिलाकर, यहाँ एक न्यूनतम console app है जो Excel फ़ाइल पढ़ता है, **B2** से फ़ॉन्ट निकालता है, और उसे एक मॉक टेक्स्ट बॉक्स पर लागू करता है।

```csharp
using OfficeOpenXml;
using OfficeOpenXml.Style;
using System;
using System.Collections.Generic;
using System.Drawing;

namespace FontCopyDemo
{
    // Mock grid control – replace with your real UI component
    public class MyGrid
    {
        public Dictionary<string, TextBoxMock> TextBoxes { get; } = new()
        {
            { "Notes", new TextBoxMock() }
        };
    }

    // Simple text box representation for demonstration
    public class TextBoxMock
    {
        public string FontFamily { get; set; }
        public float FontSize { get; set; }
        public Color FontColor { get; set; }

        public override string ToString()
        {
            return $"FontFamily: {FontFamily}, FontSize: {FontSize}, FontColor: {FontColor.Name}";
        }
    }

    class Program
    {
        static void Main()
        {
            // 1️⃣ Load Excel worksheet
            var fileInfo = new FileInfo(@"C:\Data\Sample.xlsx");
            using var package = new ExcelPackage(fileInfo);
            var ws = package.Workbook.Worksheets["Sheet1"];
            var cellStyle = ws.Cells["B2"].Style;

            // 2️⃣ Grab the target TextBox from the grid
            var gridJs = new MyGrid();
            var notesTextBox = gridJs.TextBoxes["Notes"];

            // 3️⃣ Apply font family
            notesTextBox.FontFamily = cellStyle.Font.Name;

            // 4️⃣ Apply font size
            notesTextBox.FontSize = cellStyle.Font.Size;

            // 5️⃣ Apply font colour (with safety net)
            var excelColor = cellStyle.Font.Color?.GetColor();
            notesTextBox.FontColor = excelColor ?? Color.Black;

            // Output the result for verification
            Console.WriteLine("TextBox after copying font:");
            Console.WriteLine(notesTextBox);
        }
    }
}
```

**Expected output (मान लीजिए B2 में Arial, 12 pt, नीला है):**

```
TextBox after copying font:
FontFamily: Arial, FontSize: 12, FontColor: Blue
```

प्रोग्राम चलाएँ, अपना UI खोलें, और आप देखेंगे कि “Notes” टेक्स्ट बॉक्स अब सेल **B2** की बिल्कुल वही फ़ॉन्ट स्टाइल दिखा रहा है। कोई मैनुअल ट्यूनिंग की जरूरत नहीं।

---

## Frequently Asked Questions & Edge Cases

### यदि सेल थीम colour इस्तेमाल कर रहा हो तो क्या करें?

EPPlus का `GetColor()` स्वचालित रूप से थीम colour को ठोस `System.Drawing.Color` में बदल देता है। लेकिन यदि आप कोई पुराना लाइब्रेरी इस्तेमाल कर रहे हैं जो केवल थीम इंडेक्स रिटर्न करता है, तो आपको वह इंडेक्स अपने colour पैलेट से मैप करना पड़ेगा।

### क्या मैं अन्य स्टाइल एट्रिब्यूट्स (जैसे bold, italic) भी कॉपी कर सकता हूँ?

बिल्कुल। `ExcelStyle.Font` ऑब्जेक्ट `Bold`, `Italic`, `Underline`, और `Strike` भी एक्सपोज़ करता है। बस अपने UI कंट्रोल पर संबंधित प्रॉपर्टीज़ सेट करें:

```csharp
notesTextBox.FontBold = cellStyle.Font.Bold;
notesTextBox.FontItalic = cellStyle.Font.Italic;
```

### यदि ग्रिड कंट्रोल में `FontColor` प्रॉपर्टी नहीं है तो क्या करें?

अधिकांश आधुनिक UI फ्रेमवर्क्स में यह प्रॉपर्टी होती है, लेकिन यदि आपका केवल CSS स्ट्रिंग लेता है, तो `Color` को hex में बदलें:

```csharp
string hex = $"#{notesTextBox.FontColor.R:X2}{notesTextBox.FontColor.G:X2}{notesTextBox.FontColor.B:X2}";
notesTextBox.Style["color"] = hex; // for web‑based grids
```

### कई सेल्स को एक साथ कैसे हैंडल करें?

इच्छित रेंज पर लूप चलाएँ, प्रत्येक सेल की स्टाइल फ़ेच करें, और उसे संबंधित टेक्स्ट बॉक्स पर लागू करें। यदि आप कई रो प्रोसेस कर रहे हैं तो स्टाइल ऑब्जेक्ट्स को कैश करना न भूलें ताकि परफ़ॉर्मेंस इम्पैक्ट कम हो।

---

## Pro Tips & Common Pitfalls

- **ExcelPackage को कैश करें** – हर सेल के लिए फ़ाइल खोलना‑बंद करना महंगा है। वर्कबुक को एक बार लोड करें और `ExcelWorksheet` ऑब्जेक्ट को री‑यूज़ करें।
- **null colours पर ध्यान दें** – जो सेल डिफ़ॉल्ट colour इनहेरिट करता है वह `null` रिटर्न कर सकता है। हमेशा एक fallback (ब्लैक या कंट्रोल का डिफ़ॉल्ट) दें।
- **DPI स्केलिंग का ख्याल रखें** – हाई‑DPI मॉनिटर्स के लिए फ़ॉन्ट साइज थोड़ा बड़ा दिख सकता है। आवश्यकता पड़ने पर `Graphics.DpiX` से एडजस्ट करें।
- **थ्रेड सेफ़्टी** – EPPlus थ्रेड‑सेफ़ नहीं है। यदि आप कई शीट्स को पैरलल प्रोसेस कर रहे हैं, तो प्रत्येक थ्रेड के लिए अलग `ExcelPackage` बनाएँ।

---

## निष्कर्ष

अब आप जानते हैं **कैसे Excel सेल से फ़ॉन्ट कॉपी** करें और **सेल स्टाइल को किसी भी टेक्स्ट‑बॉक्स कंट्रोल पर लागू** करें C# के माध्यम से। सेल की `Style` को रिट्रीव करके, उसकी `Font` प्रॉपर्टीज़ को एक्सट्रैक्ट करके, और उन्हें UI एलिमेंट पर असाइन करके आप विज़ुअल कंसिस्टेंसी को मैनुअल कॉपी‑पेस्ट के बिना बनाए रख सकते हैं।  

पूरा समाधान—वर्कबुक लोड करना, सेल स्टाइल प्राप्त करना, और टेक्स्ट बॉक्स की फ़ॉन्ट फ़ैमिली, साइज, और colour सेट करना—**सेल फ़ॉर्मेटिंग का उपयोग** और **टेक्स्टबॉक्स फ़ॉन्ट साइज सेट** करने के कोर को कवर करता है।  

अब इस उदाहरण को एक्सटेंड करके बैकग्राउंड colour, बॉर्डर, या पूरी सेल कंटेंट कॉपी करने की कोशिश करें। यदि आप किसी डेटा‑ग्रिड लाइब्रेरी के साथ काम कर रहे हैं जो रिच सेल रेंडरिंग सपोर्ट करती है, तो आप अब Excel से निकाली गई वही स्टाइलिंग जानकारी उसे फीड कर सकते हैं, जिससे आपका UI और रिपोर्ट्स पूरी तरह सिंक में रहें।

और सवाल हैं? कमेंट करें या “dynamic Excel‑to‑UI binding” और “theme‑aware colour conversion” जैसे संबंधित टॉपिक्स देखें। Happy coding!

---

![how to copy font example](placeholder-image.jpg "how to copy font from Excel cell to TextBox")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}