---
category: general
date: 2026-02-28
description: Aspose.Cells का उपयोग करके C# में एक्सेल डेट फ़ॉर्मेट सेट करना, एक्सेल
  डेटटाइम पढ़ना, एक्सेल से तारीख निकालना और वर्कबुक फ़ॉर्मूले की गणना करना सीखें।
  पूर्ण चलाने योग्य उदाहरण।
draft: false
keywords:
- set excel date format
- read excel datetime
- extract date from excel
- calculate workbook formulas
- get datetime cell
language: hi
og_description: एक्सेल की तिथि फ़ॉर्मेट सेट करने, एक्सेल डेटटाइम पढ़ने, तिथियों को
  निकालने और पूरी C# उदाहरण के साथ वर्कबुक फ़ॉर्मूले की गणना में निपुण बनें।
og_title: C# में एक्सेल डेट फ़ॉर्मेट सेट करें – पूर्ण चरण‑दर‑चरण गाइड
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में एक्सेल की तिथि फ़ॉर्मेट सेट करें – पूर्ण चरण‑दर‑चरण गाइड
url: /hi/net/excel-custom-number-date-formatting/set-excel-date-format-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# excel तिथि प्रारूप सेट करें – पूर्ण C# गाइड

क्या आप स्प्रेडशीट्स को तुरंत जनरेट करते समय **excel तिथि प्रारूप सेट करने** में संघर्ष कर रहे हैं? आप अकेले नहीं हैं। कई डेवलपर्स को तब समस्या आती है जब सेल में उचित तिथि के बजाय कच्चा स्ट्रिंग दिखता है, विशेषकर जापानी युग तिथियों या कस्टम लोकैल स्ट्रिंग्स के साथ।  

इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से **Excel तिथि प्रारूप सेट** करेंगे, फिर **excel datetime पढ़ेंगे**, **excel से तिथि निकालेंगे**, और यहाँ तक कि **workbook फ़ॉर्मूले की गणना** करेंगे ताकि आप अंततः **datetime सेल** मानों को नेटिव .NET `DateTime` ऑब्जेक्ट्स के रूप में प्राप्त कर सकें। कोई बाहरी रेफ़रेंसेज़ नहीं, सिर्फ एक स्व-निहित, चलाने योग्य स्निपेट जिसे आप Visual Studio में पेस्ट करके तुरंत काम करता देख सकते हैं।

## आपको क्या चाहिए

- **Aspose.Cells for .NET** (कोई भी हालिया संस्करण; यहाँ उपयोग किया गया API 23.x और उसके बाद के संस्करणों के साथ काम करता है)  
- .NET 6 या बाद का (कोड .NET Framework 4.6+ के साथ भी कम्पाइल होता है)  
- C# सिंटैक्स की बुनियादी समझ – यदि आप `Console.WriteLine` लिख सकते हैं, तो आप तैयार हैं।

बस इतना ही। Aspose.Cells के अलावा कोई अतिरिक्त NuGet पैकेज नहीं, Excel इंस्टॉलेशन की भी ज़रूरत नहीं।

## C# में excel तिथि प्रारूप कैसे सेट करें  

पहला कदम यह है कि हम Excel को बताएं कि सेल में टेक्स्ट नहीं, बल्कि तिथि है। Aspose.Cells एक बिल्ट‑इन नंबर फ़ॉर्मेट ID (`14`) प्रदान करता है जो वर्तमान लोकैल के शॉर्ट डेट पैटर्न से मेल खाती है।

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // Step 2: Write a Japanese era date string into cell A1
        sheet.Cells["A1"].PutValue("Reiwa 2-04-01");

        // Step 3: Apply the standard date number format (ID 14) to A1
        // This tells Excel to treat the cell as a date.
        sheet.Cells["A1"].Style.Number = 14;

        // Step 4: Force Excel to recalculate formulas so the value is parsed
        workbook.CalculateFormula();

        // Step 5: Retrieve the parsed value as a .NET DateTime
        DateTime parsedDate = sheet.Cells["A1"].GetDateTime();

        // Step 6: Show the result – should be 2020‑04‑01
        Console.WriteLine($"Parsed DateTime: {parsedDate:yyyy-MM-dd}");
    }
}
```

> **Pro tip:** `CalculateFormula()` कॉल अत्यंत महत्वपूर्ण है। इसके बिना, सेल अभी भी कच्चा स्ट्रिंग रखता है, और `GetDateTime()` एक एक्सेप्शन फेंकेगा। यह लाइन Aspose.Cells को उसका इंटरनल पार्सर चलाने के लिए मजबूर करती है, जिससे प्रभावी रूप से **workbook फ़ॉर्मूले की गणना** हमारे लिए हो जाती है।

जब आप प्रोग्राम चलाएंगे तो आपको यह आउटपुट दिखाई देगा:

```
Parsed DateTime: 2020-04-01
```

यह पुष्टि करता है कि हमने सफलतापूर्वक **excel तिथि प्रारूप सेट** किया, और हम एक उचित `DateTime` के रूप में **datetime सेल** प्राप्त करने में सक्षम रहे।

## excel datetime मान पढ़ना  

अब जब तिथि सही ढंग से संग्रहीत है, आप सोच सकते हैं कि बाद में इसे कैसे पुनः प्राप्त करें, शायद किसी मौजूदा फ़ाइल से। वही `GetDateTime()` मेथड किसी भी सेल पर काम करता है जिसमें पहले से ही तिथि फ़ॉर्मेट हो।

```csharp
// Assuming 'sheet' is already loaded from an existing workbook
DateTime existingDate = sheet.Cells["B5"].GetDateTime();
Console.WriteLine($"Cell B5 contains: {existingDate:d}");
```

यदि सेल को तिथि के रूप में फ़ॉर्मेट नहीं किया गया है, तो `GetDateTime()` `DateTime.MinValue` लौटाता है। इसलिए हम हमेशा पहले **excel तिथि प्रारूप सेट** करते हैं।

## excel सेल्स से तिथि निकालना  

कभी‑कभी सेल में पूर्ण टाइमस्टैम्प (तिथि + समय) होता है लेकिन आपको केवल तिथि भाग चाहिए। आप लौटाए गए `DateTime` पर `.Date` का उपयोग करके समय घटक को ट्रंकेट कर सकते हैं।

```csharp
DateTime fullStamp = sheet.Cells["C3"].GetDateTime(); // e.g., 2023-07-15 14:30:00
DateTime onlyDate = fullStamp.Date;                  // 2023-07-15 00:00:00
Console.WriteLine($"Date only: {onlyDate:yyyy-MM-dd}");
```

यह तरीका अंतर्निहित Excel नंबर फ़ॉर्मेट की परवाह किए बिना काम करता है, बशर्ते सेल को तिथि के रूप में पहचाना गया हो।

## workbook फ़ॉर्मूले की गणना  

क्या होगा अगर तिथि किसी फ़ॉर्मूले का परिणाम हो, जैसे `=TODAY()` या `=DATE(2022,5,10)`? Aspose.Cells `CalculateFormula()` कॉल करने पर फ़ॉर्मूले का मूल्यांकन करेगा। उसके बाद सेल बिल्कुल उसी तरह व्यवहार करता है जैसे मैन्युअली दर्ज की गई तिथि।

```csharp
sheet.Cells["D2"].Formula = "=TODAY()";
workbook.CalculateFormula(); // Re‑evaluate the sheet
DateTime today = sheet.Cells["D2"].GetDateTime();
Console.WriteLine($"Today is: {today:yyyy-MM-dd}");
```

ध्यान दें कि हमें सेल स्टाइल बदलने की जरूरत नहीं पड़ी; जब फ़ॉर्मूला एक सीरियल नंबर लौटाता है जो तिथि में मैप होता है, तो Excel स्वचालित रूप से परिणाम को तिथि के रूप में मानता है।

## मौजूदा workbook से datetime सेल प्राप्त करना  

सब कुछ एक साथ रखते हुए, यहाँ एक कॉम्पैक्ट रूटीन है जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं ताकि Excel फ़ाइल खोलें, सभी तिथि सेल्स को सही ढंग से इंटरप्रेट करें, और `DateTime` ऑब्जेक्ट्स की सूची लौटाएँ।

```csharp
using System.Collections.Generic;
using Aspose.Cells;

static List<DateTime> ExtractAllDates(string filePath)
{
    Workbook wb = new Workbook(filePath);
    Worksheet ws = wb.Worksheets[0];
    wb.CalculateFormula(); // Make sure formulas are evaluated

    var dates = new List<DateTime>();
    foreach (Cell cell in ws.Cells)
    {
        // Check if the cell has a date number format (ID 14‑22 are common date formats)
        if (cell.GetStyle().Number >= 14 && cell.GetStyle().Number <= 22)
        {
            dates.Add(cell.GetDateTime());
        }
    }
    return dates;
}
```

`ExtractAllDates("Sample.xlsx")` चलाने पर आपको पहली शीट में **excel तिथि प्रारूप सेट** की गई सभी तिथियाँ मिलेंगी।

## सामान्य समस्याएँ और उन्हें कैसे टालें  

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| `GetDateTime()` throws `ArgumentException` | Cell isn’t recognized as a date (missing number format) | Apply `Style.Number = 14` **before** calling `CalculateFormula()` |
| Date appears as `1900‑01‑00` | Excel’s serial number 0 is interpreted as the epoch | Ensure the cell actually contains a valid serial (>0) |
| Japanese era strings don’t parse | Aspose.Cells only parses era strings after `CalculateFormula()` | Keep the raw string, set a date format, then call `CalculateFormula()` |
| Time zone shifts | `DateTime` is stored without zone info, but your app may display in a different locale | Use `DateTimeKind.Utc` or convert explicitly if needed |

## छवि – दृश्य सारांश  

![excel तिथि प्रारूप उदाहरण](excel-date-format.png "excel तिथि प्रारूप उदाहरण")

डायग्राम यह प्रवाह दर्शाता है: **स्ट्रिंग लिखें → नंबर फ़ॉर्मेट लागू करें → पुनः गणना करें → DateTime प्राप्त करें**।

## सारांश  

हमने वह सब कवर किया जो आपको **excel तिथि प्रारूप सेट** करने, **excel datetime पढ़ने**, **excel से तिथि निकालने**, **workbook फ़ॉर्मूले की गणना** करने, और अंत में **datetime सेल** मानों को नेटिव .NET ऑब्जेक्ट्स के रूप में प्राप्त करने के लिए चाहिए। पूर्ण, चलाने योग्य कोड कॉपी‑पेस्ट के लिए तैयार है, और व्याख्याएँ प्रत्येक चरण के “क्यों” को समझाती हैं, ताकि आप इस पैटर्न को अधिक जटिल परिदृश्यों में अनुकूलित कर सकें।

### आगे क्या?

- **Bulk import/export:** बड़े रिपोर्टों को बैच‑प्रोसेस करने के लिए `ExtractAllDates` हेल्पर का उपयोग करें।  
- **Custom date formats:** लोकैल‑स्वतंत्र फ़ॉर्मेटिंग के लिए `Style.Number = 14` को `Style.Custom = "yyyy/mm/dd"` से बदलें।  
- **Time‑zone aware dates:** ग्लोबल एप्लिकेशन्स के लिए `DateTimeOffset` को Excel के सीरियल नंबरों के साथ संयोजित करें।

बिना झिझक प्रयोग करें, कंडीशनल फ़ॉर्मेटिंग जोड़ें, या तिथियों को डेटाबेस में पुश करें। यदि आपको कोई समस्या आती है, तो कमेंट छोड़ें — हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}