---
category: general
date: 2026-05-04
description: C# में Excel वर्कबुक बनाते समय कोटैन्जेंट कैसे गणना करें। EXPAND फ़ंक्शन
  का उपयोग करना, वर्कबुक को सहेजना, और गणनाओं को स्वचालित करना सीखें।
draft: false
keywords:
- how to calculate cotangent
- create excel workbook
- how to use expand
- how to save workbook
- use expand function
language: hi
og_description: C# का उपयोग करके Excel में कोटैन्जेंट कैसे गणना करें। यह ट्यूटोरियल
  दिखाता है कि Excel वर्कबुक कैसे बनाएं, EXPAND का उपयोग करें, और फ़ाइल को सहेजें।
og_title: Excel में कोटैन्जेंट कैसे गणना करें – पूर्ण C# वर्कबुक गाइड
tags:
- C#
- Aspose.Cells
- Excel Automation
title: C# के साथ Excel में कोटैन्जेंट कैसे गणना करें – वर्कबुक बनाएं, EXPAND का उपयोग
  करें, और सहेजें
url: /hi/net/formulas-functions/how-to-calculate-cotangent-in-excel-with-c-create-workbook-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में C# के साथ कोटैन्जेंट कैसे गणना करें – पूर्ण गाइड

क्या आपने कभी सोचा है **how to calculate cotangent** को सीधे C# द्वारा जेनरेट किए गए Excel फ़ाइल में? शायद आप एक वित्तीय मॉडल, एक वैज्ञानिक रिपोर्ट बना रहे हैं, या सिर्फ एक उबाऊ स्प्रेडशीट कार्य को ऑटोमेट कर रहे हैं। अच्छी खबर? आप इसे कुछ कोड लाइनों में कर सकते हैं—कोई मैन्युअल फ़ॉर्मूला नहीं, कोई कॉपी‑पेस्ट जिम्नास्टिक नहीं।

इस ट्यूटोरियल में हम एक Excel वर्कबुक बनाने, **EXPAND** फ़ंक्शन के साथ एक एरे को विस्तारित करने, 45° का कोटैन्जेंट निकालने के लिए **COT** फ़ॉर्मूला डालने, और अंत में फ़ाइल को सेव करने की प्रक्रिया देखेंगे ताकि आप इसे Excel में खोलकर परिणाम देख सकें। साथ ही हम **how to use expand**, **how to save workbook** और कुछ उपयोगी टिप्स भी कवर करेंगे जो अक्सर छूट जाते हैं।

> **त्वरित उत्तर:** Aspose.Cells (या Microsoft Interop) का उपयोग करके एक वर्कबुक बनाएं, `ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"` सेट करें, `ws.Cells["B1"].Formula = "=COT(PI()/4)"` सेट करें, फिर `workbook.Save("output.xlsx")` कॉल करें।

---

## आपको क्या चाहिए

- **.NET 6+** (या कोई भी नवीनतम .NET रनटाइम)।
- **Aspose.Cells for .NET** (फ़्री ट्रायल या लाइसेंस्ड संस्करण)।
- C# सिंटैक्स की बुनियादी समझ।
- Visual Studio, Rider, या कोई भी एडिटर जो आपको पसंद हो।

कोई अतिरिक्त Excel ऐड‑इन की आवश्यकता नहीं है; सब कुछ सर्वर‑साइड चलता है और उत्पन्न फ़ाइल किसी भी नवीनतम Excel संस्करण में काम करती है।

## चरण 1: C# से एक Excel वर्कबुक बनाएं  

वर्कबुक बनाना बुनियाद है। इसे ऐसे समझें जैसे आप लिखना शुरू करने से पहले एक नई नोटबुक खोल रहे हों।

```csharp
using Aspose.Cells;

// Step 1: Initialize a new workbook object
Workbook workbook = new Workbook();               // Empty workbook
Worksheet ws = workbook.Worksheets[0];            // Grab the first sheet
```

**यह क्यों महत्वपूर्ण है:**  
`Workbook` पूरे `.xlsx` पैकेज का प्रतिनिधित्व करता है। डिफ़ॉल्ट रूप से इसमें एक शीट होती है, जिसे हम `Worksheets[0]` के माध्यम से एक्सेस करते हैं। यदि बाद में आपको अधिक शीट्स चाहिए, तो आप उन्हें `workbook.Worksheets.Add()` से जोड़ सकते हैं।

> **प्रो टिप:** यदि आप .NET Core को टार्गेट कर रहे हैं, तो सुनिश्चित करें कि Aspose.Cells NuGet पैकेज आपके रनटाइम से मेल खाता हो ताकि नेटिव डिपेंडेंसीज़ की कमी न हो।

## चरण 2: कॉलम भरने के लिए EXPAND फ़ंक्शन का उपयोग करें  

**EXPAND** फ़ंक्शन Excel का तरीका है एक स्थैतिक एरे को डायनामिक रेंज में बदलने का। यह तब परफेक्ट है जब आप प्रत्येक सेल को हार्ड‑कोड किए बिना मानों की एक कॉलम जनरेट करना चाहते हैं।

```csharp
// Step 2: Write an EXPAND formula in cell A1
ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)"; // Expands to a 5‑row column
```

### यह कैसे काम करता है  

- `{1,2,3}` स्रोत एरे है (तीन संख्याएँ)।
- `5` Excel को **5 पंक्तियाँ** बनाने के लिए कहता है।
- `1` Excel को **1 कॉलम** बनाने के लिए कहता है।

जब आप सेव की गई फ़ाइल खोलेंगे, तो सेल A1 से A5 तक `1, 2, 3, 0, 0` दिखाएंगे (अतिरिक्त पंक्तियों को शून्य से भरा जाता है)।

**एज केस:** यदि `rows` आर्ग्युमेंट स्रोत एरे की लंबाई से छोटा है, तो Excel एरे को ट्रंकेट कर देता है। इसलिए `=EXPAND({1,2,3},2,1)` केवल `1` और `2` दिखाएगा।

## चरण 3: कोटैन्जेंट निकालने के लिए COT फ़ॉर्मूला डालें  

अब मुख्य भाग: Excel में **how to calculate cotangent**। `COT` फ़ंक्शन रैडियन में कोण की अपेक्षा करता है, इसलिए हम इसे `PI()/4` (जो 45° के बराबर है) देते हैं।

```csharp
// Step 3: Write a COT formula in cell B1
ws.Cells["B1"].Formula = "=COT(PI()/4)"; // Returns 1
```

### Tan की बजाय COT क्यों उपयोग करें?  

कोटैन्जेंट टैंजेंट का प्रतिलोम है (`cot = 1 / tan`)। जबकि आप `=1/TAN(PI()/4)` लिख सकते हैं, `COT` का उपयोग साफ़ है और जब कोण 0° या 180° हो तो शून्य से विभाजन की त्रुटियों से बचाता है।

**अपेक्षित आउटपुट:** `output.xlsx` खोलने पर B1 में `1` दिखेगा, क्योंकि 45° (π/4 रैडियन) का कोटैन्जेंट 1 के बराबर है।

**यदि मुझे डिग्री चाहिए तो?**  
Excel के त्रिकोणमितीय फ़ंक्शन रैडियन में काम करते हैं। डिग्री को `RADIANS(deg)` से बदलें। उदाहरण: `=COT(RADIANS(60))`।

## चरण 4: वर्कबुक को सेव करें ताकि आप परिणाम देख सकें  

सेव करना पहेली का अंतिम टुकड़ा है। आप किसी भी फ़ोल्डर में लिख सकते हैं जहाँ आपके पास लिखने की अनुमति हो।

```csharp
// Step 4: Persist the workbook to disk
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "output.xlsx");

// Save the workbook (the default format is .xlsx)
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### विभिन्न फ़ॉर्मैट में कैसे सेव करें  

- **XLS** – `workbook.Save("output.xls", SaveFormat.Excel97To2003);`  
- **CSV** – `workbook.Save("output.csv", SaveFormat.CSV);`  

यदि आपको फ़ाइल को स्ट्रीम करना हो (जैसे वेब API के लिए), तो `workbook.Save(stream, SaveFormat.Xlsx)` का उपयोग करें।

## पूर्ण कार्यशील उदाहरण  

सब कुछ एक साथ मिलाकर, यहाँ एक स्व-निहित प्रोग्राम है जिसे आप कॉपी‑पेस्ट करके कंसोल ऐप में उपयोग कर सकते हैं।

```csharp
using System;
using System.IO;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet ws = workbook.Worksheets[0];

        // 2️⃣ Expand an array {1,2,3} into a 5‑row column starting at A1
        ws.Cells["A1"].Formula = "=EXPAND({1,2,3},5,1)";

        // 3️⃣ Calculate cotangent of 45° (π/4) in B1
        ws.Cells["B1"].Formula = "=COT(PI()/4)";

        // 4️⃣ Define where to save the file (Desktop for easy access)
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "output.xlsx");

        // 5️⃣ Save the workbook
        workbook.Save(outputPath);
        Console.WriteLine($"✅ Workbook saved at: {outputPath}");
    }
}
```

**परिणाम सत्यापन:**  
- `output.xlsx` खोलें।  
- कॉलम A में `1, 2, 3, 0, 0` होना चाहिए।  
- सेल B1 में `1` दिखना चाहिए।  

यदि आप ये मान देखते हैं, तो आपने प्रोग्रामेटिक रूप से **how to calculate cotangent** सीख लिया है और **create excel workbook**, **use expand function**, और **save workbook** कैसे किया जाए—सब एक साथ।

## सामान्य प्रश्न और समस्याएँ  

### क्या `COT` पुराने Excel संस्करणों में काम करता है?  

हां, `COT` Excel 2007 से उपलब्ध है। यदि आप Excel 2003 (`.xls`) को टार्गेट करते हैं, तो आपको इसे `1/TAN(...)` से बदलना होगा क्योंकि `COT` वहाँ उपलब्ध नहीं है।

### यदि फ़ॉर्मूला स्वतः पुनः गणना नहीं करता तो क्या करें?  

Aspose.Cells फ़ॉर्मूलों को लेज़ीली इवैल्यूएट करता है। यदि आपको फ़ाइल में गणना किए हुए मान चाहिए तो सेव करने से पहले `workbook.CalculateFormula()` कॉल करें।

```csharp
workbook.CalculateFormula();
workbook.Save(outputPath);
```

### क्या मैं फ़ॉर्मूला के बिना सीधे परिणाम लिख सकता हूँ?  

बिल्कुल, आप C# में मान निकाल सकते हैं (`Math.Cos(Math.PI / 4) / Math.Sin(Math.PI / 4)`) और इसे `ws.Cells["B1"].Value = result;` में असाइन कर सकते हैं। ट्यूटोरियल Excel फ़ॉर्मूलों पर केंद्रित है क्योंकि वे डायनामिक रहते हैं—कोण बदलने पर स्वचालित रूप से अपडेट हो जाता है।

## वास्तविक‑दुनिया प्रोजेक्ट्स के लिए प्रो टिप्स  

- **बैच ऑपरेशन्स:** यदि आप हजारों पंक्तियों को भर रहे हैं, तो लिखते समय कैलकुलेशन को डिसेबल करें (`workbook.Settings.CalculateFormulaOnOpen = false`), फिर समाप्त होने पर इसे एनेबल करें।  
- **रेंज नामकरण:** `ws.Cells.CreateRange("MyArray", "A1:A5")` का उपयोग करें और फ़ॉर्मूलों में नाम का संदर्भ दें ताकि स्प्रेडशीट साफ़ रहे।  
- **एरर हैंडलिंग:** `workbook.Save` को try/catch में रैप करें ताकि परमिशन समस्याओं (`UnauthorizedAccessException`) को पकड़ा जा सके।

## निष्कर्ष  

हमने C# द्वारा जेनरेट किए गए Excel शीट में **how to calculate cotangent** को कवर किया, कॉलम भरने के लिए **how to use expand** दिखाया, और तुरंत निरीक्षण के लिए **how to save workbook** दिखाया। ऊपर दिया गया पूर्ण, चलाने योग्य उदाहरण आपको स्थैतिक डेटा को त्रिकोणमितीय गणनाओं के साथ मिलाकर किसी भी स्प्रेडशीट को ऑटोमेट करने की ठोस नींव देता है।

अगला कदम? `COT` फ़ॉर्मूला में कोण को रेफ़रेंस सेल (`=COT(PI()*A1/180)`) से बदलें ताकि उपयोगकर्ता डिग्री इनपुट कर सकें। या अन्य गणितीय फ़ंक्शन जैसे `SIN`, `COS`, और `ATAN2` को एक्सप्लोर करें—वे सभी जेनरेटेड वर्कबुक में समान रूप से काम करते हैं।

कोडिंग का आनंद लें, और आपकी स्प्रेडशीट्स त्रुटि‑रहित रहें! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}