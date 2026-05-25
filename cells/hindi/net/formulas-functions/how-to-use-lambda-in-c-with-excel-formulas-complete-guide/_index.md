---
category: general
date: 2026-03-22
description: C# में लैम्ब्डा का उपयोग करके Excel फ़ॉर्मूले के साथ काम करना। फ़ॉर्मूला
  को सेल में लिखना, रेंज को एरे में बदलना, एरे को कंसोल में दिखाना, और Excel में कोटैन्जेंट
  की गणना करना सीखें।
draft: false
keywords:
- how to use lambda
- display array in console
- convert range to array
- write formula to cell
- calculate cotangent in excel
language: hi
og_description: C# में लैम्ब्डा का उपयोग करके Excel फ़ॉर्मूले को नियंत्रित करना, रेंज
  को एरे में बदलना, सेल में फ़ॉर्मूला लिखना, कंसोल में एरे प्रदर्शित करना, और Excel
  में कोटैन्जेंट की गणना करना।
og_title: C# में लैम्ब्डा को Excel फ़ॉर्मूले के साथ कैसे उपयोग करें – चरण‑दर‑चरण
tags:
- C#
- Aspose.Cells
- Excel Automation
- Lambda Expressions
title: C# में लैम्ब्डा को Excel फ़ॉर्मूले के साथ कैसे उपयोग करें – पूर्ण गाइड
url: /hi/net/formulas-functions/how-to-use-lambda-in-c-with-excel-formulas-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Lambda का उपयोग Excel फ़ॉर्मूले के साथ – पूर्ण गाइड

क्या आपने कभी सोचा है **how to use lambda** जब आप C# से Excel को ऑटोमेट कर रहे हैं? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब उन्हें Excel के नए डायनामिक एरे फ़ंक्शन की शक्ति को C# के `LAMBDA` क्षमता के साथ मिलाना पड़ता है। अच्छी खबर? यह वास्तव में काफी सरल है जब आप देखेंगे कि भाग कैसे फिट होते हैं।

इस ट्यूटोरियल में हम **writing a formula to a cell**, **converting a range to an array**, **displaying that array in the console**, और यहाँ तक कि **calculating cotangent in Excel** को कवर करेंगे—साथ ही आपको `REDUCE` कॉल के अंदर **how to use lambda** दिखाएंगे। अंत तक आपके पास एक runnable स्निपेट होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं जो Aspose.Cells (या समान लाइब्रेरी) को रेफ़रेंस करता है।

---

## आप क्या सीखेंगे

- C# का उपयोग करके **write formula to cell** कैसे करें।
- `EXPAND` फ़ंक्शन के साथ **convert range to array** कैसे करें।
- गणना के बाद **display array in console** कैसे करें।
- `COT` और `COTH` का उपयोग करके **calculate cotangent in Excel** कैसे करें।
- C# से Excel के `REDUCE` फ़ंक्शन के अंदर **how to use lambda** के लिए सटीक सिंटैक्स।

> **Prerequisite:** आपको .NET (Core 6+ या .NET Framework 4.7+) का नवीनतम संस्करण और Aspose.Cells for .NET लाइब्रेरी की आवश्यकता है, जिसे आप NuGet के माध्यम से इंस्टॉल कर सकते हैं।

## चरण 1: वर्कबुक सेट अप करें और फ़ॉर्मूला को सेल में लिखें

सबसे पहले हम एक नई वर्कबुक बनाते हैं और पहली वर्कशीट प्राप्त करते हैं। फिर हम **write a formula to a cell** — इस मामले में `A1` में `EXPAND` कॉल का परिणाम रहेगा।

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write formula to A1 – we’ll expand B1:C2 into a 4‑by‑5 array later
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";
```

**Why this matters:** कोड से सीधे फ़ॉर्मूला लिखने से आप बिना Excel खोले जटिल स्प्रेडशीट बना सकते हैं। यह अगले चरण के लिए भी मंच तैयार करता है जहाँ हम **convert range to array** करेंगे।

## चरण 2: EXPAND के साथ रेंज को एरे में बदलें

`EXPAND` Excel का वह तरीका है जिससे एक छोटी रेंज को बड़े मैट्रिक्स में बदला जाता है। फ़ॉर्मूला को `A1` में रखने पर Excel उस सेल से शुरू होकर 4 × 5 ब्लॉक को स्पिल करेगा। C# से हमें मानों को मैन्युअली कॉपी करने की जरूरत नहीं है – लाइब्रेरी `Calculate` कॉल करने पर भारी काम खुद कर लेगी।

```csharp
        // The EXPAND formula will spill into A1:E4 (4 rows × 5 columns)
        // No extra code needed – the workbook will handle the spill.
```

**How to use lambda:** अभी नहीं, लेकिन बने रहें। पहले हमें शीट में डेटा चाहिए, फिर हम उसे एक lambda के साथ reduce करेंगे।

## चरण 3: REDUCE के अंदर LAMBDA का उपयोग – “How to Use Lambda” का मूल

Excel 365 ने `REDUCE` पेश किया, जो एक **initial value**, एक **range**, और एक **LAMBDA** लेता है जो प्रत्येक तत्व को कैसे जोड़ना है बताता है। C# से हम बस फ़ॉर्मूला स्ट्रिंग असाइन करते हैं; lambda Excel फ़ॉर्मूला के अंदर रहता है, C# कोड में नहीं।

```csharp
        // Reduce the spilled array by summing all its values.
        // This demonstrates how to use lambda inside REDUCE.
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";
```

**Explanation:**  
- `0` प्रारंभिक accumulator (`acc`) है।  
- `A1:D4` वह रेंज है जिसे हम प्रोसेस करना चाहते हैं (स्पिल के पहले चार कॉलम)।  
- `LAMBDA(acc, x, acc + x)` Excel को बताता है कि प्रत्येक सेल (`x`) को accumulator में जोड़ें।  

यह **how to use lambda** का सार है जो स्प्रेडशीट संदर्भ में एग्रीगेशन के लिए उपयोग होता है।

## चरण 4: Excel में Cotangent की गणना – डिग्री से हाइपरबोलिक

यदि आपको त्रिकोणमितीय परिणाम चाहिए, तो Excel के `COT` और `COTH` फ़ंक्शन बहुत आसान हैं। हम उन्हें क्रमशः `G1` और `G2` में रखेंगे।

```csharp
        // Demonstrate trigonometric functions – cotangent and hyperbolic cotangent
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected result: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";      // Hyperbolic cotangent of 1
```

**Why this is handy:** **calculate cotangent in Excel** जानने से आप कस्टम गणित कोड लिखने से बच सकते हैं, विशेषकर जब वर्कबुक को गैर‑डेवलपर्स के साथ साझा किया जाएगा।

## चरण 5: गणना को मजबूर करें और विस्तारित एरे प्राप्त करें

अब हम वर्कबुक को हर फ़ॉर्मूला का मूल्यांकन करने के लिए कहते हैं, फिर `A1` से स्पिल्ड एरे को निकालते हैं। यहीं पर हम **display array in console** करेंगे।

```csharp
        // Force calculation of all formulas
        workbook.Calculate();

        // Retrieve the spilled array from A1 as a 2‑D object
        var expanded = worksheet.Cells["A1"].Value;

        // Pretty‑print the 2‑D array to the console
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show the result of the REDUCE lambda
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**What you’ll see:**  
- लाइन‑बाय‑लाइन प्रिंट किया गया एक सुंदर 4 × 5 मैट्रिक्स।  
- `REDUCE` lambda द्वारा गणना किया गया योग।  
- दो cotangent मान।

यह प्रवाह **write formula to cell** से लेकर **display array in console** तक पूरा करता है।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट के लिए तैयार)

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉन्सोल ऐप में डाल सकते हैं। याद रखें कि पहले `Aspose.Cells` NuGet पैकेज जोड़ें (`dotnet add package Aspose.Cells`)।

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Initialize workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Step 2: Write EXPAND formula (convert range to array)
        worksheet.Cells["A1"].Formula = "=EXPAND(B1:C2, 4, 5)";

        // Step 3: Use REDUCE with LAMBDA (how to use lambda)
        worksheet.Cells["E1"].Formula = "=REDUCE(0, A1:D4, LAMBDA(acc, x, acc + x))";

        // Step 4: Calculate cotangent values (calculate cotangent in excel)
        worksheet.Cells["G1"].Formula = "=COT(PI()/4)";   // Expected: 1
        worksheet.Cells["G2"].Formula = "=COTH(1)";

        // Step 5: Force calculation
        workbook.Calculate();

        // Step 6: Retrieve and display the expanded array (display array in console)
        var expanded = worksheet.Cells["A1"].Value;
        Console.WriteLine("Expanded array from A1 (4×5):");
        if (expanded is object[,] matrix)
        {
            for (int r = 0; r < matrix.GetLength(0); r++)
            {
                for (int c = 0; c < matrix.GetLength(1); c++)
                {
                    Console.Write($"{matrix[r, c]}\t");
                }
                Console.WriteLine();
            }
        }
        else
        {
            Console.WriteLine("Unexpected data type.");
        }

        // Show REDUCE result
        Console.WriteLine($"\nSum of A1:D4 (via REDUCE lambda): {worksheet.Cells["E1"].Value}");

        // Show cotangent results
        Console.WriteLine($"Cotangent of π/4: {worksheet.Cells["G1"].Value}");
        Console.WriteLine($"Hyperbolic cotangent of 1: {worksheet.Cells["G2"].Value}");
    }
}
```

**Expected console output (values will vary based on the default contents of B1:C2, which are 0 by default):**  
**अपेक्षित कंसोल आउटपुट (मान B1:C2 की डिफ़ॉल्ट सामग्री के आधार पर बदलेंगे, जो डिफ़ॉल्ट रूप से 0 हैं):**

```
Expanded array from A1 (4×5):
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0
0   0   0   0   0

Sum of A1:D4 (via REDUCE lambda): 0
Cotangent of π/4: 1
Hyperbolic cotangent of 1: 1.31303528549933
```

`B1:C2` को अपने स्वयं के नंबरों से भरने में संकोच न करें—मैट्रिक्स उन मानों को दर्शाएगा।

## प्रो टिप्स और सामान्य pitfalls

- **Pro tip:** यदि आपको स्पिल्ड रेंज को कहीं और शुरू करना है, तो केवल टार्गेट सेल (`A1`) बदलें। `EXPAND` फ़ंक्शन एंकर का सम्मान करता है।
- **Watch out for:** स्रोत रेंज में खाली सेल्स स्पिल्ड एरे में `0` बन जाते हैं, जो आपके `REDUCE` योग को प्रभावित कर सकते हैं।
- **Edge case:** जब वर्कबुक में फ़ॉर्मूले होते हैं जो वोलैटाइल फ़ंक्शन (जैसे `NOW()`) पर निर्भर होते हैं, तो सभी फ़ॉर्मूले सेट करने के बाद `workbook.Calculate()` कॉल करें ताकि सब कुछ अपडेटेड रहे।
- **Performance note:** बड़े स्पिल्स के लिए, `EXPAND` कॉल में आकार सीमित करने पर विचार करें; अन्यथा आप आवश्यक से अधिक मेमोरी आवंटित कर सकते हैं।
- **Compatibility:** The `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}