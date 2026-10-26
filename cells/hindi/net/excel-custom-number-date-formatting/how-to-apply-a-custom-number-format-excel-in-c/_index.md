---
category: general
date: 2026-10-26
description: C# में महत्वपूर्ण अंकों को कॉन्फ़िगर करके, एक Excel वर्कबुक बनाकर और
  उसे XLSX दस्तावेज़ के रूप में सहेजकर, कस्टम नंबर फ़ॉर्मेट Excel फ़ाइल कैसे सेट करें,
  सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format excel
- set significant digits
- how to set number format
- create excel workbook c#
- save workbook xlsx
language: hi
lastmod: 2026-10-26
og_description: C# में कस्टम नंबर फ़ॉर्मेट एक्सेल आपको महत्वपूर्ण अंकों को नियंत्रित
  करने, एक एक्सेल वर्कबुक बनाने और इसे XLSX के रूप में सहेजने की सुविधा देता है। इस
  पूर्ण ट्यूटोरियल का पालन करें।
og_image_alt: Excel cell A1 displaying a number formatted with 4 significant digits
  using C#
og_title: C# में Excel के लिए कस्टम नंबर फ़ॉर्मेट – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  headline: How to apply a custom number format excel in C#
  type: TechArticle
- description: Learn how to set a custom number format excel file in C# by configuring
    significant digits, creating an Excel workbook, and saving it as an XLSX document.
  name: How to apply a custom number format excel in C#
  steps:
  - name: Using a custom format string instead of global options
    text: 'If you need a format that applies only to a single range, you can assign
      a format string directly:'
  - name: Applying the setting to an entire column
    text: '```csharp // Apply the same significant‑digit rule to column B ws.Cells.Columns[1].ApplyNumberFormatOptions(
      new NumberFormatOptions { SignificantDigits = 4 }); ```'
  - name: Dealing with negative numbers
    text: 'The global `SignificantDigits` option works uniformly for positive and
      negative numbers. If you want a different display for negatives, combine it
      with a custom format:'
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: C# में Excel में कस्टम नंबर फ़ॉर्मेट कैसे लागू करें
url: /hi/net/excel-custom-number-date-formatting/how-to-apply-a-custom-number-format-excel-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में कस्टम नंबर फ़ॉर्मेट एक्सेल कैसे लागू करें

यदि आपको एक **custom number format excel** चाहिए जो विशिष्ट संख्या में महत्वपूर्ण अंकों को दिखाए, तो यह गाइड आपको बिल्कुल बताता है कि इसे C# में कैसे किया जाए। आप देखेंगे कि महत्वपूर्ण अंक कैसे सेट करें, एक Excel वर्कबुक कैसे बनाएं, और वर्कबुक को XLSX फ़ाइल के रूप में कैसे सहेजें—सिर्फ कुछ लाइनों के कोड से।

प्रोग्रामेटिक रूप से Excel फ़ाइलों के साथ काम करना अक्सर यह मतलब रखता है कि आपको संख्याओं के प्रदर्शित होने के तरीके को नियंत्रित करना पड़ता है। Aspose.Cells for .NET का उपयोग करके आप एक ग्लोबल number‑format विकल्प परिभाषित कर सकते हैं जो हर संख्यात्मक सेल को निर्दिष्ट महत्वपूर्ण अंकों की संख्या का पालन करने के लिए मजबूर करता है। यह ट्यूटोरियल पूरी कार्यप्रवाह को कवर करता है, प्रोजेक्ट सेटअप से लेकर Excel में आउटपुट की पुष्टि तक।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण स्थापित हो (कोड .NET Framework 4.7.2+ के साथ भी काम करता है)
* Visual Studio 2022 या कोई भी पसंदीदा C# IDE
* The **Aspose.Cells** NuGet package (`Install-Package Aspose.Cells`) – Excel हेरफेर के लिए एक पूर्ण रूप से प्रबंधित लाइब्रेरी
* C# सिंटैक्स की बुनियादी परिचितता

## चरण 1: C# में एक Excel वर्कबुक बनाएं

पहला कार्य एक नया `Workbook` ऑब्जेक्ट बनाना है। यह ऑब्जेक्ट मेमोरी में पूरी Excel फ़ाइल का प्रतिनिधित्व करता है।

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook instance
        Workbook wb = new Workbook();

        // The workbook now contains a default worksheet named "Sheet1"
        // You can access it via the Worksheets collection.
        Worksheet ws = wb.Worksheets[0];
```

**Why this matters:** `Workbook` हर Excel ऑपरेशन का प्रवेश बिंदु है। इसे पहले बनाकर, आप सुनिश्चित करते हैं कि एक साफ़ फ़ाइल तैयार हो जो बाद में XLSX के रूप में सहेजी जा सके।

## चरण 2: महत्वपूर्ण अंकों को सेट करने के लिए नंबर फ़ॉर्मेट कॉन्फ़िगर करें

Aspose.Cells एक ग्लोबल सेटिंग `NumberFormatOptions` प्रदान करता है। `SignificantDigits = 4` असाइन करने पर, हर संख्यात्मक सेल चार महत्वपूर्ण अंकों तक दिखाएगा जब तक कि कोई अधिक विशिष्ट फ़ॉर्मेट इसे ओवरराइड न करे।

```csharp
        // Step 2: Set the global number‑format option to 4 significant digits
        WorkbookSettings.SetNumberFormatOptions(
            new NumberFormatOptions { SignificantDigits = 4 });
```

**Why this matters:** `SetNumberFormatOptions` का उपयोग करके आप **custom number format excel** को परिभाषित कर सकते हैं बिना प्रत्येक सेल के लिए फ़ॉर्मेट स्ट्रिंग लिखे। यह Excel के *Format Cells → Number → Custom* डायलॉग में मिलने वाले “Significant Digits” विकल्प को प्रतिबिंबित करता है।

## चरण 3: मान लिखें और कस्टम नंबर फ़ॉर्मेट की पुष्टि करें

अब एक संख्यात्मक मान को सेल में रखें। ग्लोबल सेटिंग स्वचालित रूप से 4‑अंकों के नियम को लागू करेगी।

```csharp
        // Step 3: Write a numeric value into cell A1 (row 0, column 0)
        ws.Cells[0, 0].PutValue(123.456789);

        // Optional: Add a label so you can see the effect in Excel
        ws.Cells[0, 1].PutValue("Original value:");
        ws.Cells[0, 2].PutValue(123.456789);
```

जब आप सहेजी गई फ़ाइल खोलते हैं, तो सेल **A1** `123.5` दिखाएगा (चार महत्वपूर्ण अंकों तक गोल किया गया)। मूल मान अंतर्निहित डेटा में अपरिवर्तित रहता है, जिसे आप फ़ॉर्मूला बार देख कर पुष्टि कर सकते हैं।

**Edge case tip:** यदि आप `12345678.9` जैसी बहुत बड़ी संख्या संग्रहीत करते हैं, तो वही सेटिंग `1.235E+07` (वैज्ञानिक नोटेशन) दिखाएगी क्योंकि Excel चार महत्वपूर्ण अंकों को बनाए रखते हुए सबसे संक्षिप्त प्रतिनिधित्व चुनता है।

## चरण 4: वर्कबुक को XLSX के रूप में सहेजें

अंत में, वर्कबुक को डिस्क पर सहेजें। `Save` मेथड एक्सटेंशन के आधार पर फ़ाइल फ़ॉर्मेट को स्वचालित रूप से चुनता है।

```csharp
        // Step 4: Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\SigDigits.xlsx";
        wb.Save(outputPath);

        // Inform the user
        System.Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

**Why this matters:** **XLSX** (`save workbook xlsx`) के रूप में सहेजना आधुनिक Excel संस्करणों, Office 365, और अन्य स्प्रेडशीट टूल्स के साथ अधिकतम संगतता सुनिश्चित करता है।

## अपेक्षित परिणाम

Microsoft Excel में *C:\Temp\SigDigits.xlsx* खोलें। आपको यह दिखना चाहिए:

| A          | B               | C               |
|------------|-----------------|-----------------|
| **123.5**  | मूल मान: | **123.456789**  |

*Cell A1* संख्या को चार महत्वपूर्ण अंकों तक गोल दिखाता है, जबकि *C1* तुलना के लिए पूरी शुद्धता बनाए रखता है।

## सामान्य विविधताएँ और विशिष्ट सेल्स के लिए नंबर फ़ॉर्मेट कैसे सेट करें

### ग्लोबल विकल्पों के बजाय कस्टम फ़ॉर्मेट स्ट्रिंग का उपयोग

यदि आपको ऐसा फ़ॉर्मेट चाहिए जो केवल एक रेंज पर लागू हो, तो आप सीधे फ़ॉर्मेट स्ट्रिंग असाइन कर सकते हैं:

```csharp
ws.Cells["D1"].PutValue(0.0012345);
Style style = wb.CreateStyle();
style.Custom = "0.####"; // shows up to 4 decimal places, not significant digits
ws.Cells["D1"].SetStyle(style);
```

### पूरे कॉलम पर सेटिंग लागू करना

```csharp
// Apply the same significant‑digit rule to column B
ws.Cells.Columns[1].ApplyNumberFormatOptions(
    new NumberFormatOptions { SignificantDigits = 4 });
```

### नकारात्मक संख्याओं से निपटना

ग्लोबल `SignificantDigits` विकल्प सकारात्मक और नकारात्मक दोनों संख्याओं के लिए समान रूप से काम करता है। यदि आप नकारात्मक संख्याओं के लिए अलग डिस्प्ले चाहते हैं, तो इसे कस्टम फ़ॉर्मेट के साथ मिलाएँ:

```csharp
Style negStyle = wb.CreateStyle();
negStyle.Custom = "#,##0.###;[Red]-#,##0.###";
ws.Cells["E1"].PutValue(-9876.54321);
ws.Cells["E1"].SetStyle(negStyle);
```

## प्रो टिप्स और संभावित समस्याएँ

* **Pro tip:** डेटा लिखने से **पहले** नंबर‑फ़ॉर्मेट विकल्प सेट करें। सेल्स को भरने के बाद विकल्प बदलने से मौजूदा मानों को पुनः फ़ॉर्मेट नहीं किया जाता।
* **Watch out for:** `PutValue` के साथ **string** का उपयोग करना जो संख्या जैसा दिखता है (जैसे, `"123.45"`). Excel इसे टेक्स्ट मानता है, और कस्टम फ़ॉर्मेट लागू नहीं होगा।
* **Performance note:** ग्लोबल सेटिंग्स कम लागत वाली हैं, लेकिन लाखों सेल्स पर स्टाइल लागू करने से मेमोरी उपयोग बढ़ सकता है। संभव हो तो कॉलम‑लेवल फ़ॉर्मेटिंग का उपयोग करें।

## अगले कदम

अब जब आप महत्वपूर्ण अंकों के साथ **custom number format excel** फ़ाइलें बना सकते हैं, आप निम्नलिखित का अन्वेषण कर सकते हैं:

* **How to set number format** तिथियों और मुद्राओं के लिए `Style.Custom` का उपयोग करके।
* **Creating charts** जो आपके कस्टम फ़ॉर्मेट का सम्मान करते हैं।
* **Exporting to CSV** जबकि संख्यात्मक शुद्धता को बनाए रखें (`save workbook xlsx` → `wb.Save("file.csv", SaveFormat.Csv)`)।

ये विषय यहाँ प्रदर्शित `Workbook` और `Worksheet` अवधारणाओं पर आधारित हैं।

---

**Summary**

आपने **custom number format excel** को `NumberFormatOptions` को **set significant digits** करने के लिए कॉन्फ़िगर करके, C# में एक Excel वर्कबुक बनाकर, मान लिखकर, और **वर्कबुक को XLSX** फ़ाइल के रूप में **save** करके सीखा। ऊपर दिया गया पूर्ण, चलाने योग्य कोड हर चरण दिखाता है, प्रत्येक भाग की आवश्यकता समझाता है, और सामान्य विविधताओं के लिए टिप्स प्रदान करता है। अपने प्रोजेक्ट्स में स्निपेट्स को अनुकूलित करने और अन्य फ़ॉर्मेटिंग परिदृश्यों के साथ प्रयोग करने में संकोच न करें।

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [C# में कस्टम नंबर फ़ॉर्मेट एक्सेल – पूर्ण गाइड](/cells/english/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/)
- [C# में Excel वर्कबुक बनाएं – सीमित महत्वपूर्ण अंक Excel](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-c-limit-significant-digits-excel/)
- [Aspose.Cells के साथ number format excel कैसे लागू करें](/cells/english/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}