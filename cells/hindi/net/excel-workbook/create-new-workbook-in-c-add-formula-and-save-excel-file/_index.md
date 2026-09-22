---
category: general
date: 2026-02-23
description: C# में प्रोग्रामेटिकली नया वर्कबुक बनाएं और एक सेल में फ़ॉर्मूला जोड़ें।
  EXPAND का उपयोग कैसे करें सीखें, फिर Excel वर्कबुक को आसानी से सहेजें।
draft: false
keywords:
- create new workbook
- add formula to cell
- save excel workbook
- how to use expand
- create excel file programmatically
language: hi
og_description: C# में प्रोग्रामेटिकली नया वर्कबुक बनाएं। एक सेल में फ़ॉर्मूला जोड़ें,
  EXPAND का उपयोग कैसे करें सीखें, और सेकंडों में Excel वर्कबुक को सहेजें।
og_title: C# में नया वर्कबुक बनाएं – फ़ॉर्मूला जोड़ें और एक्सेल फ़ाइल सहेजें
tags:
- C#
- Excel Automation
- Aspose.Cells
title: C# में नया वर्कबुक बनाएं – फ़ॉर्मूला जोड़ें और एक्सेल फ़ाइल सहेजें
url: /hi/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में नया वर्कबुक बनाएं – फ़ॉर्मूला जोड़ें और Excel फ़ाइल सहेजें

क्या आपने कभी सोचा है कि **create new workbook** ऑब्जेक्ट कोड से बिना Excel खोले कैसे बनाएं? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब उन्हें तुरंत एक स्प्रेडशीट जेनरेट करनी होती है—शायद रिपोर्ट, एक्सपोर्ट, या तेज़ डेटा डंप के लिए।  

अच्छी खबर? इस गाइड में आप देखेंगे कि **create new workbook** कैसे बनाएं, **add formula to cell** कैसे डालें, और फिर **save excel workbook** को कुछ ही लाइनों के C# कोड से कैसे सहेजें। हम यह भी देखेंगे **how to use expand** ताकि आप मैन्युअल कॉपी किए बिना डायनेमिक एरे जेनरेट कर सकें। अंत तक, आप **create excel file programmatically** करके इसे यूज़र्स या डाउनस्ट्रीम सर्विसेज़ को भेज सकेंगे।

## Prerequisites

- .NET 6.0 या बाद का संस्करण (कोई भी हालिया .NET रनटाइम काम करेगा)
- Aspose.Cells for .NET (फ्री ट्रायल या लाइसेंस्ड संस्करण) – यह लाइब्रेरी नीचे उपयोग की गई `Workbook` और `Worksheet` क्लासेज़ प्रदान करती है।
- C# सिंटैक्स की बुनियादी समझ—Excel का गहरा ज्ञान आवश्यक नहीं।

यदि आपके पास ये सब है, तो बढ़िया! यदि नहीं, तो NuGet से Aspose.Cells (`Install-Package Aspose.Cells`) प्राप्त करें और आप तैयार हैं।

---

## Step 1: Create New Workbook – The Foundation

शुरू करने के लिए, हमें एक नया वर्कबुक ऑब्जेक्ट इंस्टैंशिएट करना होगा। इसे ऐसे समझें जैसे आप एक बिल्कुल नई, खाली Excel फ़ाइल खोल रहे हों।

```csharp
using Aspose.Cells;

public class ExcelGenerator
{
    public void Generate()
    {
        // Step 1: Create a new workbook (this is the core of create new workbook)
        Workbook workbook = new Workbook();
```

> **Why this matters:** `Workbook` क्लास किसी भी Excel मैनिपुलेशन की एंट्री पॉइंट है। नया इंस्टेंस बनाकर हम शीट्स, स्टाइल्स, और फ़ॉर्मूले के लिए मेमोरी अलोकेट करते हैं—बिना फ़ाइल सिस्टम को छुए।

---

## Step 2: Access the First Worksheet

हर नए वर्कबुक में एक डिफ़ॉल्ट वर्कशीट (नाम *Sheet1*) होती है। हम इसे पकड़ेंगे ताकि डेटा और फ़ॉर्मूले रख सकें।

```csharp
        // Step 2: Access the first worksheet
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** यदि आपको कई शीट्स चाहिए, तो बस `workbook.Worksheets.Add("MySheet")` कॉल करें और रिटर्न किए गए `Worksheet` ऑब्जेक्ट के साथ काम करें।

---

## Step 3: Add Formula to Cell – Using EXPAND

अब मज़े का हिस्सा: फ़ॉर्मूला डालना। `EXPAND` फ़ंक्शन तब एकदम सही है जब आप एक स्थिर एरे को बड़े, ऑटो‑फ़िल्ड रेंज में बदलना चाहते हैं।

```csharp
        // Step 3: Add formula to cell A1 using EXPAND
        // This creates a 5‑row array from the constant {1,2,3}
        worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";
```

### How the EXPAND Formula Works

| Argument | Meaning |
|----------|---------|
| `{1,2,3}` | स्रोत एरे (तीन संख्याओं की हॉरिज़ॉन्टल लिस्ट) |
| `5`       | परिणाम में वांछित पंक्तियों की संख्या |
| `1`       | वांछित कॉलम की संख्या (वर्टिकल रखने के लिए 1 रखें) |

जब Excel इसको इवैल्यूएट करता है, तो यह एक **vertical** लिस्ट बनाता है:

```
A1: 1
A2: 2
A3: 3
A4: 0   (filled with zeros)
A5: 0
```

> **Why use EXPAND?** यह मैन्युअल कॉपी या VBA लूप की जरूरत को खत्म कर देता है। फ़ंक्शन डायनेमिक रूप से डेटा को रीशेप करता है, जिससे आपकी स्प्रेडशीट अधिक मजबूत और मेंटेन करने में आसान बनती है।

---

## Step 4: Save Excel Workbook – Persist the Result

फ़ॉर्मूला सेट होने के बाद, अंतिम कदम है वर्कबुक को डिस्क पर लिखना। आप कोई भी फ़ोल्डर चुन सकते हैं जहाँ आपके पास लिखने की अनुमति हो।

```csharp
        // Step 4: Save the workbook to view the result
        string outputPath = @"C:\Temp\ExpandFormula.xlsx";
        workbook.Save(outputPath);
    }
}
```

> **What you’ll see:** `ExpandFormula.xlsx` को Excel में खोलें, और सेल `A1` विस्तारित एरे दिखाएगा। फ़ॉर्मूला स्वयं सेल में रहता है, इसलिए यदि आप स्रोत एरे बदलते हैं, तो आउटपुट ऑटोमैटिक अपडेट हो जाएगा।

---

## Optional: Verify the Output Programmatically

यदि आप मैन्युअल रूप से Excel नहीं खोलना चाहते, तो आप मानों को वापस पढ़ कर पुष्टि कर सकते हैं कि वे अपेक्षित हैं या नहीं।

```csharp
        // Verify values without opening Excel
        for (int row = 0; row < 5; row++)
        {
            var value = worksheet.Cells[row, 0].Value; // column 0 = A
            Console.WriteLine($"Row {row + 1}: {value}");
        }
```

ऊपर वाला कोड चलाने पर यह प्रिंट करेगा:

```
Row 1: 1
Row 2: 2
Row 3: 3
Row 4: 0
Row 5: 0
```

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **Can I use EXPAND with a larger source array?** | बिल्कुल। बस `{1,2,3}` को किसी भी कॉन्स्टेंट या सेल रेंज से बदल दें, जैसे `EXPAND(A1:C1,10,1)`। |
| **What if I need a horizontal result?** | रो/कॉलम आर्ग्यूमेंट्स को स्वैप करें: `EXPAND({1,2,3},1,5)` एक 1‑रो, 5‑कॉलम स्प्रेड देगा। |
| **Will this work on older Excel versions?** | `EXPAND` Excel 365/2021 से उपलब्ध है। पुराने संस्करणों के लिए आपको `INDEX`/`SEQUENCE` से एरे सिमुलेट करना पड़ेगा। |
| **Do I need to call `workbook.CalculateFormula()`?** | नहीं। Aspose.Cells सेव पर फ़ॉर्मूले को ऑटोमैटिक इवैल्यूएट करता है, इसलिए मान तुरंत दिखते हैं। |
| **How to add more than one sheet before saving?** | `workbook.Worksheets.Add("SecondSheet")` कॉल करें और नई शीट पर सेल‑मैनिपुलेशन स्टेप्स दोहराएँ। |

---

## Full Working Example

नीचे पूरा, रन‑टू‑डेड प्रोग्राम दिया गया है। इसे कॉन्सोल ऐप में कॉपी‑पेस्ट करें, आउटपुट पाथ एडजस्ट करें, और **F5** दबाएँ।

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutomationDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create new workbook
            Workbook workbook = new Workbook();

            // Access first worksheet
            Worksheet worksheet = workbook.Worksheets[0];

            // Add EXPAND formula to A1
            worksheet.Cells["A1"].Formula = "EXPAND({1,2,3},5,1)";

            // Optional: verify values in console
            workbook.CalculateFormula(); // ensures formulas are evaluated now
            for (int i = 0; i < 5; i++)
            {
                Console.WriteLine($"A{i + 1} = {worksheet.Cells[i, 0].Value}");
            }

            // Save the workbook
            string filePath = @"C:\Temp\ExpandFormula.xlsx";
            workbook.Save(filePath);
            Console.WriteLine($"Workbook saved to {filePath}");
        }
    }
}
```

**Expected output in the console:**

```
A1 = 1
A2 = 2
A3 = 3
A4 = 0
A5 = 0
Workbook saved to C:\Temp\ExpandFormula.xlsx
```

जेनरेट की गई फ़ाइल खोलें और आप कॉलम **A** में वही संख्याएँ देखेंगे।

---

## Visual Summary

![Create new workbook example](create-new-workbook.png "Screenshot showing a new workbook created with create new workbook in C#")

*छवि में नया बनाया गया वर्कबुक और EXPAND परिणाम दिखाया गया है।*

---

## Conclusion

अब आप जानते हैं कि **create new workbook**, **add formula to cell**, और **save excel workbook** को C# से कैसे करें। **how to use expand** को मास्टर करके आप मैन्युअल प्रयास के बिना डायनेमिक एरे जेनरेट कर सकते हैं, और पूरा प्रोसेस आपको किसी भी ऑटोमेशन सीनारियो के लिए **create excel file programmatically** करने की सुविधा देता है।

अगला कदम? कॉन्स्टेंट एरे को रेंज रेफ़रेंस से बदलें, विभिन्न `EXPAND` डाइमेंशन के साथ प्रयोग करें, या कई शीट्स में फ़ॉर्मूले चेन करें। यही पैटर्न चार्ट्स, स्टाइलिंग, और पिवट टेबल्स के लिए भी काम करता है—तो एक्सप्लोर करते रहें।

यदि आपको कोई समस्या आती है, तो नीचे कमेंट करें। हैप्पी कोडिंग, और प्रोग्रामेटिक Excel की शक्ति का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}