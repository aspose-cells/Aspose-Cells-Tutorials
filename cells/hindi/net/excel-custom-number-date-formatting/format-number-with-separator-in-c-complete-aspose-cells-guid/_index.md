---
category: general
date: 2026-03-30
description: Aspose.Cells का उपयोग करके C# में विभाजक के साथ संख्या को फ़ॉर्मेट करना
  सीखें। इसमें कस्टम नंबर फ़ॉर्मेट सेट करना, हजारों विभाजक जोड़ना, दशमलव स्थानों को
  फ़ॉर्मेट करना, और सेल को फ़ॉर्मेट करने का तरीका शामिल है।
draft: false
keywords:
- format number with separator
- set custom number format
- add thousands separator
- format decimal places
- how to format cell
language: hi
og_description: C# में विभाजक के साथ संख्या को फ़ॉर्मेट करें। यह गाइड दिखाता है कि
  कैसे कस्टम नंबर फ़ॉर्मेट सेट करें, हजारों विभाजक जोड़ें, दशमलव स्थानों को फ़ॉर्मेट
  करें, और Aspose.Cells का उपयोग करके सेल को फ़ॉर्मेट करें।
og_title: C# में विभाजक के साथ संख्या को फ़ॉर्मेट करें – Aspose.Cells ट्यूटोरियल
tags:
- C#
- Aspose.Cells
- Number Formatting
title: C# में विभाजक के साथ संख्या को फॉर्मेट करें – पूर्ण Aspose.Cells गाइड
url: /hi/net/excel-custom-number-date-formatting/format-number-with-separator-in-c-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में संख्या को विभाजक के साथ फ़ॉर्मेट करें – पूर्ण Aspose.Cells गाइड

क्या आपको कभी **स्प्रेडशीट में संख्या को विभाजक के साथ फ़ॉर्मेट** करने की ज़रूरत पड़ी, लेकिन सही API कॉल नहीं पता चला? आप अकेले नहीं हैं—डेवलपर्स अक्सर हजारों विभाजक, दशमलव स्थान, और कस्टम पैटर्न से जूझते रहते हैं जब डेटा एक्सपोर्ट करते हैं।  

अच्छी ख़बर: Aspose.Cells इसे बहुत आसान बनाता है। इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से **कस्टम नंबर फ़ॉर्मेट सेट करना**, **हजारों विभाजक जोड़ना**, **दशमलव स्थान फ़ॉर्मेट करना**, और **सेल को स्ट्रिंग के रूप में फ़ॉर्मेट करने** का तरीका दिखाएंगे। अंत तक आपके पास एक तैयार‑से‑चलाने वाला स्निपेट होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

## इस गाइड में क्या कवर किया गया है

* वह सटीक NuGet पैकेज जो आपको चाहिए और इसे कैसे इंस्टॉल करें।  
* चरण‑बद्ध कोड जो एक वर्कबुक बनाता है, एक संख्यात्मक मान लिखता है, और कस्टम फ़ॉर्मेट लागू करता है।  
* क्यों `ExportTableOptions.ExportAsString` फ़ॉर्मेटेड वैल्यू प्राप्त करने का पसंदीदा तरीका है।  
* सामान्य ग़लतियाँ—जैसे `ExportAsString` को सक्षम करना भूल जाना या गलत फ़ॉर्मेट मास्क उपयोग करना।  
* यदि आपको अलग दशमलव स्थान या अलग विभाजक शैली चाहिए तो फ़ॉर्मेट मास्क को कैसे बदलें।

कोई बाहरी दस्तावेज़ लिंक आवश्यक नहीं है; सब कुछ यहाँ उपलब्ध है। चलिए शुरू करते हैं।

---

## पूर्वापेक्षाएँ

| आवश्यकता | कारण |
|-------------|--------|
| .NET 6.0 या बाद का संस्करण | Aspose.Cells 23.10+ .NET Standard 2.0+ को टारगेट करता है, इसलिए .NET 6 सुरक्षित और वर्तमान है। |
| Visual Studio 2022 (या कोई भी C# IDE) | डिबगिंग और पैकेज मैनेजमेंट को आसान बनाता है। |
| Aspose.Cells for .NET NuGet पैकेज | वह `Workbook`, `Worksheet`, और `ExportTableOptions` क्लासेज़ प्रदान करता है जिनका हम उपयोग करेंगे। |

आप पैकेज को Package Manager Console के माध्यम से इंस्टॉल कर सकते हैं:

```powershell
Install-Package Aspose.Cells
```

बस इतना ही—कोई अतिरिक्त DLLs नहीं, कोई COM इंटरऑप नहीं, सिर्फ एक NuGet रेफ़रेंस।

---

## चरण 1: नई वर्कबुक इनिशियलाइज़ करें (सेल को फ़ॉर्मेट कैसे करें)

सबसे पहले हम एक नई `Workbook` इंस्टेंस बनाते हैं। इसे एक खाली Excel फ़ाइल समझें जो डेटा प्राप्त करने के लिए तैयार है।

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is where we’ll format the cell.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];
```

> **यह क्यों महत्वपूर्ण है:** `Workbook` Aspose.Cells में हर ऑपरेशन का एंट्री पॉइंट है। पहले वर्कशीट (`Worksheets[0]`) को पकड़कर हमें एक साफ़ कैनवास मिलता है बिना शीट का नाम बताए।

---

## चरण 2: लक्ष्य सेल में संख्यात्मक मान लिखें

अब हम सेल **A1** में एक कच्ची संख्या डालते हैं। यह मान अभी तक फ़ॉर्मेट नहीं किया गया है—यह सिर्फ एक डबल है।

```csharp
        // Step 2: Insert a raw numeric value.
        worksheet.Cells["A1"].PutValue(12345.6789);
```

> **प्रो टिप:** जब आप बाद में संख्यात्मक फ़ॉर्मेट लागू करने वाले हों तो `PutString` के बजाय `PutValue` उपयोग करें। यह मूल डेटा टाइप को संरक्षित रखता है, जिससे Excel‑संगत गणनाएँ संभव होती हैं।

---

## चरण 3: कस्टम नंबर फ़ॉर्मेट सेट करें (हजारों विभाजक जोड़ें & दशमलव स्थान फ़ॉर्मेट करें)

अब ट्यूटोरियल का मुख्य भाग: एक फ़ॉर्मेट मास्क परिभाषित करना जो Aspose.Cells को बताता है कि संख्या कैसे दिखे। मास्क `#,##0.00` तीन चीज़ें करता है:

1. **`#,##0`** – डिफ़ॉल्ट रूप से कॉमा के साथ हजारों विभाजक जोड़ता है।  
2. **`.00`** – ठीक दो दशमलव स्थान फोर्स करता है।  

यदि आपको अलग संख्या में दशमलव चाहिए, तो दशमलव बिंदु के बाद `0` की संख्या बदल दें।

```csharp
        // Step 3: Configure the custom number format.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,          // Return the value as a formatted string.
            NumberFormat = "#,##0.00"       // Add thousands separator and fix to 2 decimals.
        };
```

> **हम `ExportAsString` क्यों उपयोग करते हैं:** डिफ़ॉल्ट रूप से, `ExportString` कच्चा मान लौटाता है। `ExportAsString = true` सेट करने से API `NumberFormat` मास्क को टेक्स्ट में बदलने से पहले लागू करता है। यह रिपोर्ट, JSON पेलोड, या UI डिस्प्ले के लिए सटीक स्ट्रिंग प्रतिनिधित्व चाहिए होने पर आवश्यक है।

---

## चरण 4: फ़ॉर्मेटेड टेक्स्ट एक्सपोर्ट करें (सेल को फ़ॉर्मेट कैसे करें)

ऑप्शन तैयार होने के बाद, हम उसी सेल पर `ExportString` कॉल करते हैं। यह मेथड हमने अभी परिभाषित किया हुआ मास्क सम्मानित करता है और एक सुंदर फ़ॉर्मेटेड स्ट्रिंग वापस देता है।

```csharp
        // Step 4: Export the formatted value.
        string formattedCellText = worksheet.Cells["A1"].ExportString(exportOptions);

        // Step 5: Show the result.
        Console.WriteLine(formattedCellText); // Expected output: 12,345.68
    }
}
```

प्रोग्राम चलाने पर **`12,345.68`** कंसोल में प्रिंट होगा—बिल्कुल वही फ़ॉर्मेट जो हमने माँगा था।

> **एज केस:** यदि स्रोत संख्या में दो से अधिक दशमलव हैं, तो मास्क उसे राउंड कर देगा। यदि आपको राउंडिंग की बजाय ट्रंकेशन चाहिए, तो `PutValue` से पहले `Math.Truncate` से मान को प्रोसेस करना होगा।

---

## चरण 5: फ़ॉर्मेट को ट्यून करना – सामान्य वैरिएशन

### 5.1 दशमलव प्रिसीजन बदलें

तीन दशमलव चाहिए? बस मास्क बदलें:

```csharp
NumberFormat = "#,##0.000"   // → 12,345.679
```

### 5.2 अलग हजारों विभाजक उपयोग करें

कुछ लोकेल स्पेस या पीरियड को पसंद करते हैं। आप सीधे वह कैरेक्टर एम्बेड कर सकते हैं:

```csharp
NumberFormat = "# ##0.00"    // Uses a non‑breaking space as separator.
```

या वर्कबुक की कल्चर सेटिंग्स पर भरोसा करें:

```csharp
workbook.Settings.CultureInfo = new System.Globalization.CultureInfo("de-DE");
NumberFormat = "#.##0,00";   // German style: 12.345,68
```

### 5.3 प्रीफ़िक्स या सफ़िक्स (करेंसी, प्रतिशत)

मास्क में सीधे डॉलर साइन या प्रतिशत साइन जोड़ें:

```csharp
NumberFormat = "$#,##0.00";   // → $12,345.68
NumberFormat = "0.00%";       // → 1,234,568.00%
```

> **नोट:** मास्क केस‑सेंसिटिव है। `$` और `%` लिटरल सिंबल हैं; ये मूल संख्यात्मक मान को प्रभावित नहीं करते।

---

## चरण 6: पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है जिसे आप नई कंसोल एप में कॉपी कर सकते हैं। इसमें सभी चरण, टिप्पणी, और अंतिम आउटपुट वेरिफिकेशन शामिल है।

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise workbook and worksheet.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write raw numeric value to A1.
        worksheet.Cells["A1"].PutValue(12345.6789);

        // 3️⃣ Define custom format: thousands separator + two decimals.
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00"
        };

        // 4️⃣ Export the formatted string.
        string result = worksheet.Cells["A1"].ExportString(exportOptions);

        // 5️⃣ Display the outcome.
        Console.WriteLine(result); // Output: 12,345.68

        // Optional: keep console open.
        Console.WriteLine("Press any key to exit...");
        Console.ReadKey();
    }
}
```

प्रोग्राम चलाएँ (`dotnet run` टर्मिनल से या Visual Studio में F5 दबाएँ) और आपको फ़ॉर्मेटेड संख्या ठीक उसी तरह प्रिंट होती दिखेगी जैसा दिखाया गया है।

---

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**प्रश्न: क्या यह पुराने Excel संस्करणों के साथ काम करता है?**  
**उत्तर:** हाँ। फ़ॉर्मेट मास्क Excel के नेटिव नंबर‑फ़ॉर्मेट सिंटैक्स का पालन करता है, इसलिए कोई भी संस्करण जो `#,##0.00` समझता है वही स्ट्रिंग रेंडर करेगा।

**प्रश्न: यदि मुझे कई सेल्स की रेंज को फ़ॉर्मेट करना हो तो क्या करें?**  
**उत्तर:** इच्छित रेंज पर लूप चलाएँ और प्रत्येक सेल पर वही `ExportTableOptions` लागू करें, या रेंज पर `Style.Custom` प्रॉपर्टी सेट करें और फिर एक ही सेल पर `ExportString` कॉल करें।

**प्रश्न: क्या मैं इन फ़ॉर्मेट्स को लागू करके सीधे CSV में एक्सपोर्ट कर सकता हूँ?**  
**उत्तर:** बिल्कुल। सभी सेल्स पर फ़ॉर्मेट सेट करने के बाद `Workbook.Save("output.csv", SaveFormat.CSV);` उपयोग करें। Aspose.Cells CSV जनरेट करते समय सेल की `Style` का सम्मान करता है।

---

## निष्कर्ष

हमने अभी दिखाया कि कैसे **C# में Aspose.Cells का उपयोग करके संख्या को विभाजक के साथ फ़ॉर्मेट** किया जाता है, जिसमें **कस्टम नंबर फ़ॉर्मेट सेट करना**, **हजारों विभाजक जोड़ना**, **दशमलव स्थान फ़ॉर्मेट करना**, और स्ट्रिंग एक्सपोर्ट के लिए **सेल को फ़ॉर्मेट कैसे करें** शामिल है। कोड पूरी तरह से स्व-निहित है, .NET 6+ के साथ काम करता है, और किसी भी लोकेल या प्रिसीजन आवश्यकता के अनुसार अनुकूलित किया जा सकता है।

आगे आप देख सकते हैं:

* उसी तकनीक को डेट और टाइम पर लागू करना (`NumberFormat = "dd‑MMM‑yyyy"`).  
* बैच एक्सपोर्ट को ऑटोमेट करना जहाँ प्रत्येक कॉलम को अलग मास्क चाहिए।  
* फ़ॉर्मेटेड स्ट्रिंग्स को Aspose.Words के साथ PDF रिपोर्ट में इंटीग्रेट करना।

इनका प्रयोग करें, और आप अपनी टीम में स्प्रेडशीट फ़ॉर्मेटिंग के लिए go‑to व्यक्ति बन जाएंगे। कोडिंग का आनंद लें!   ![Screenshot showing formatted number with separator in Aspose.Cells](image-placeholder.png){alt="फ़ॉर्मेटेड संख्या को विभाजक के साथ Aspose.Cells आउटपुट में दिखाते हुए स्क्रीनशॉट"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}