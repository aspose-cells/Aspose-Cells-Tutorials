---
category: general
date: 2026-10-01
description: Aspose.Cells का उपयोग करके C# में जापानी युग की तिथि को ग्रेगोरियन DateTime
  में बदलें। जल्दी से जापानी कैलेंडर को कैसे बदलें, सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert japanese era date
- how to convert japanese calendar
language: hi
lastmod: 2026-10-01
og_description: C# में जापानी युग की तिथि को ग्रेगोरियन DateTime में बदलें। यह ट्यूटोरियल
  Aspose.Cells के साथ जापानी कैलेंडर को सटीक रूप से बदलने की विधि समझाता है।
og_image_alt: Code example converting a Japanese era date string to a Gregorian DateTime
  in a C# console app
og_title: C# में जापानी युग तिथि को ग्रेगोरियन में बदलें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  headline: How to convert Japanese era date to Gregorian in C#
  type: TechArticle
- description: convert japanese era date to a Gregorian DateTime using Aspose.Cells
    in C#. Learn how to convert japanese calendar quickly.
  name: How to convert Japanese era date to Gregorian in C#
  steps:
  - name: Why each step matters
    text: '| Step | Purpose | How it helps the conversion | |------|---------|-----------------------------|
      | **Create workbook** | Provides a container that understands Excel formulas
      and date systems. | The library’s internal date engine is activated only inside
      a workbook. | | **Insert era string** | Suppl'
  - name: Handling invalid or ambiguous strings
    text: '* **Invalid era name** – Aspose.Cells throws a `FormatException`. Wrap
      the conversion in `try/catch` to provide a friendly error message. * **Missing
      year/month/day** – The library expects a full “Era Year/Month/Day” pattern.
      If you receive partial data, prepend missing parts or reject the input ear'
  - name: Next steps
    text: '* Explore **formatting options** to write the Gregorian date back into
      the worksheet with a custom number format. * Combine this conversion with **data
      import pipelines** (e.g., reading CSV files that contain era dates). * Review
      other Aspose.Cells features such as **date arithmetic** and **regional'
  type: HowTo
tags:
- Aspose.Cells
- C#
- date conversion
title: C# में जापानी युग की तिथि को ग्रेगोरियन में कैसे परिवर्तित करें
url: /hi/net/excel-custom-number-date-formatting/how-to-convert-japanese-era-date-to-gregorian-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में जापानी युग तिथि को ग्रेगोरियन में कैसे बदलें

यदि आपको C# में **जापानी युग तिथि** स्ट्रिंग्स को ग्रेगोरियन तिथियों में बदलने की आवश्यकता है, तो यह गाइड आपको बिल्कुल सही तरीका दिखाता है। चाहे आप लेगेसी डेटा प्रोसेस कर रहे हों, उपयोगकर्ता इनपुट पढ़ रहे हों, या रिपोर्ट बना रहे हों, Aspose.Cells लाइब्रेरी परिवर्तन को सरल बनाती है। इसके अतिरिक्त, आप स्प्रेडशीट्स के साथ काम करते समय **जापानी कैलेंडर को कैसे बदलें** के सर्वोत्तम तरीके की खोज करेंगे।

यह ट्यूटोरियल हर चरण को कवर करता है—वर्कबुक बनाने से लेकर `DateTime` वैल्यू प्राप्त करने तक—ताकि आप एक पूर्ण, चलने योग्य प्रोग्राम को कॉपी‑पेस्ट कर सकें। कोई बाहरी दस्तावेज़ आवश्यक नहीं है; बस नीचे दिए गए कोड और व्याख्याओं का पालन करें।

## पूर्वापेक्षाएँ

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.6+ के साथ भी काम करता है)
* Aspose.Cells के लिए एक लाइसेंस (**Aspose.Cells**) (नि:शुल्क ट्रायल परीक्षण के लिए काम करता है)
* Visual Studio 2022 या VS Code जैसे विकास पर्यावरण
* C# कंसोल एप्लिकेशन की बुनियादी जानकारी

## Aspose.Cells के साथ जापानी युग तिथि को बदलें

परिवर्तन का मूल कुछ सरल API कॉल्स में निहित है। Aspose.Cells स्वचालित रूप से जापानी युग स्ट्रिंग्स (जैसे “Reiwa 2/04/01”) को व्याख्या करता है और वर्कशीट के पुनः गणना होने पर परिणाम को `DateTime` ऑब्जेक्ट के रूप में प्रदान करता है।

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        var workbook = new Workbook();                // creates an empty Excel file in memory
        var worksheet = workbook.Worksheets[0];       // the default sheet is at index 0

        // Step 2: Insert a Japanese era date string into cell A1
        // The string follows the Japanese calendar format: Era Year/Month/Day
        worksheet.Cells[0, 0].PutValue("Reiwa 2/04/01");

        // Step 3: Apply a default style to the cell (required for proper calculation)
        // Without a style, Aspose.Cells may treat the content as plain text and skip conversion.
        worksheet.Cells[0, 0].SetStyle(workbook.CreateStyle());

        // Step 4: Recalculate the worksheet so the date string is converted to a Gregorian date
        // The Calculate method parses the era string and updates the cell's internal value.
        worksheet.Calculate();

        // Step 5: Retrieve and display the converted DateTime value (2020‑04‑01)
        DateTime gregorian = worksheet.Cells[0, 0].DateTimeValue;
        Console.WriteLine($"Gregorian date: {gregorian:yyyy-MM-dd}");
    }
}
```

### प्रत्येक चरण का महत्व

| चरण | उद्देश्य | यह परिवर्तन में कैसे मदद करता है |
|------|---------|-----------------------------|
| **वर्कबुक बनाएं** | एक कंटेनर प्रदान करता है जो Excel फ़ॉर्मूले और तिथि प्रणालियों को समझता है। | लाइब्रेरी का आंतरिक डेट इंजन केवल वर्कबुक के भीतर सक्रिय होता है। |
| **युग स्ट्रिंग डालें** | कच्चा जापानी कैलेंडर टेक्स्ट प्रदान करता है जिसे आप अनुवाद करना चाहते हैं। | Aspose.Cells *Reiwa*, *Heisei*, *Showa* आदि जैसे युग नामों को पहचानता है। |
| **स्टाइल सेट करें** | सेल को लिटरल स्ट्रिंग की बजाय वैल्यू सेल के रूप में ट्रीट करने के लिए मजबूर करता है। | स्टाइल के बिना, `Calculate` मेथड सेल को अनदेखा कर सकता है, जिससे टेक्स्ट अपरिवर्तित रहता है। |
| **कैल्कुलेट** | युग स्ट्रिंग के पार्सिंग और आंतरिक सीरियल डेट नंबर में परिवर्तन को ट्रिगर करता है। | लाइब्रेरी “Reiwa 2/04/01” → सीरियल नंबर → ग्रेगोरियन `DateTime` में बदलती है। |
| **`DateTimeValue` पढ़ें** | परिवर्तित .NET `DateTime` ऑब्जेक्ट लौटाता है। | अब आपके पास एक मानक `DateTime` है जिसे आप किसी भी .NET API में उपयोग कर सकते हैं। |

## अन्य परिदृश्यों में जापानी कैलेंडर को कैसे बदलें

उपरोक्त समान दृष्टिकोण Aspose.Cells द्वारा समर्थित किसी भी जापानी युग नाम के लिए काम करता है:

```csharp
// Example: converting a Heisei era date
worksheet.Cells[0, 0].PutValue("Heisei 30/12/31"); // corresponds to 2018‑12‑31
worksheet.Calculate();
Console.WriteLine(worksheet.Cells[0, 0].DateTimeValue); // 2018-12-31
```

### अमान्य या अस्पष्ट स्ट्रिंग्स को संभालना

* **अमान्य युग नाम** – Aspose.Cells `FormatException` फेंकता है। परिवर्तन को `try/catch` में रैप करें ताकि एक मित्रवत त्रुटि संदेश प्रदान किया जा सके।
* **वर्ष/माह/दिन गायब** – लाइब्रेरी पूर्ण “Era Year/Month/Day” पैटर्न की अपेक्षा करती है। यदि आपको आंशिक डेटा मिलता है, तो गायब हिस्से जोड़ें या इनपुट को जल्दी अस्वीकार करें।
* **विभिन्न लोकेल सेटिंग्स** – परिवर्तन वर्तमान थ्रेड कल्चर पर **निर्भर नहीं** करता; यह हमेशा Aspose.Cells में निर्मित जापानी युग मानचित्र का उपयोग करता है। यह मेथड सर्वर‑साइड प्रोसेसिंग के लिए सुरक्षित बनाता है।

```csharp
try
{
    worksheet.Cells[0, 0].PutValue(userInput);
    worksheet.Calculate();
    DateTime result = worksheet.Cells[0, 0].DateTimeValue;
    // Use result...
}
catch (FormatException ex)
{
    Console.WriteLine($"Unable to parse Japanese era date: {ex.Message}");
}
```

## व्यावहारिक टिप्स और सामान्य pitfalls

* **`Calculate` से पहले हमेशा `SetStyle` कॉल करें**। इस चरण को छोड़ना बग्स का सामान्य स्रोत है क्योंकि सेल साधारण टेक्स्ट होल्डर बना रहता है।
* यदि आपको कई तिथियों को बदलना है तो **एक ही वर्कबुक को पुन: उपयोग करें**। प्रत्येक परिवर्तन के लिए नई वर्कबुक बनाना अनावश्यक ओवरहेड जोड़ता है।
* **बैच परिवर्तन** – एक कॉलम को युग स्ट्रिंग्स से भरें, एक बार `worksheet.Calculate()` कॉल करें, फिर `DateTimeValue`s की पूरी कॉलम पढ़ें। यह प्रति सेल पुनः गणना करने की तुलना में बहुत अधिक कुशल है।
* **संस्करण संगतता** – युग परिवर्तन लॉजिक Aspose.Cells 22.9 में पेश किया गया था। सुनिश्चित करें कि आप उस संस्करण या बाद के संस्करण पर हैं; पुराने रिलीज़ स्ट्रिंग को साधारण टेक्स्ट मानते हैं।

## पूर्ण कार्यशील उदाहरण (कंसोल ऐप)

नीचे एक स्व-समाहित प्रोग्राम है जिसे आप तुरंत कंपाइल और चलाकर देख सकते हैं। यह Reiwa और Heisei दोनों परिवर्तन को दर्शाता है, तथा त्रुटियों को सहजता से संभालता है।

```csharp
using System;
using Aspose.Cells;

class JapaneseEraConverter
{
    static void Main()
    {
        // Initialize workbook once
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        var style = workbook.CreateStyle();
        sheet.Cells[0, 0].SetStyle(style);
        sheet.Cells[1, 0].SetStyle(style);

        // Sample inputs
        string[] eraDates = { "Reiwa 2/04/01", "Heisei 30/12/31", "InvalidEra 1/01/01" };

        for (int i = 0; i < eraDates.Length; i++)
        {
            sheet.Cells[i, 0].PutValue(eraDates[i]);
        }

        // Perform conversion for all populated cells
        sheet.Calculate();

        // Output results
        for (int i = 0; i < eraDates.Length; i++)
        {
            try
            {
                DateTime dt = sheet.Cells[i, 0].DateTimeValue;
                Console.WriteLine($"{eraDates[i]} → {dt:yyyy-MM-dd}");
            }
            catch (Exception)
            {
                Console.WriteLine($"{eraDates[i]} → conversion failed");
            }
        }
    }
}
```

**अपेक्षित कंसोल आउटपुट**

```
Reiwa 2/04/01 → 2020-04-01
Heisei 30/12/31 → 2018-12-31
InvalidEra 1/01/01 → conversion failed
```

इस प्रोग्राम को चलाने से पुष्टि होती है कि लाइब्रेरी सही ढंग से **जापानी युग तिथि** स्ट्रिंग्स को बदलती है और असमर्थित मानों को सहजता से रिपोर्ट करती है।

## निष्कर्ष

आप अब जानते हैं कि Aspose.Cells का उपयोग करके C# में **जापानी युग तिथि** स्ट्रिंग्स को मानक ग्रेगोरियन `DateTime` ऑब्जेक्ट में कैसे बदलें। प्रक्रिया युग टेक्स्ट डालने, स्टाइल लागू करने, वर्कशीट को पुनः गणना करने, और `DateTimeValue` पढ़ने तक सीमित है। ऊपर दिए गए चरणों का पालन करके आप बड़े पैमाने पर **जापानी कैलेंडर** डेटा को बदलने, त्रुटियों को संभालने, और प्रदर्शन को अनुकूलित करने का व्यापक प्रश्न भी हल कर सकते हैं।

### अगले चरण

* **फ़ॉर्मेटिंग विकल्प** का अन्वेषण करें ताकि कस्टम नंबर फ़ॉर्मेट के साथ ग्रेगोरियन तिथि को वर्कशीट में वापस लिखा जा सके।
* इस परिवर्तन को **डेटा इम्पोर्ट पाइपलाइन** के साथ संयोजित करें (जैसे, युग तिथियों वाले CSV फ़ाइलों को पढ़ना)।
* अधिक जटिल कैलेंडर परिदृश्यों के लिए **डेट अरीथमेटिक** और **रीजनल सेटिंग्स** जैसे अन्य Aspose.Cells फीचर्स की समीक्षा करें।

कोडिंग का आनंद लें, और इस नमूने को अपने डेटा‑प्रोसेसिंग वर्कफ़्लो के अनुसार अनुकूलित करने में संकोच न करें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [C# में Aspose.Cells के साथ जापानी युग तिथि को पार्स करें – पूर्ण गाइड](/cells/english/net/excel-custom-number-date-formatting/parse-japanese-era-date-in-c-with-aspose-cells-full-guide/)
- [C# में Aspose.Cells के साथ जापानी युग पार्सिंग सक्षम करें](/cells/english/net/workbook-settings/enable-japanese-era-parsing-in-c-with-aspose-cells/)
- [C# में वर्कबुक बनाना और स्ट्रिंग को तिथि में बदलना](/cells/english/net/excel-custom-number-date-formatting/how-to-create-workbook-and-convert-string-to-date-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}