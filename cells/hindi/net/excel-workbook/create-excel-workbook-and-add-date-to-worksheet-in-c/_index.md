---
category: general
date: 2026-10-13
description: C# में Excel वर्कबुक बनाएं और Aspose.Cells का उपयोग करके Excel में तिथि
  लिखें। सीखें कि Excel फ़ाइल को xlsx के रूप में कैसे सहेजें और पूर्ण कोड के साथ वर्कशीट
  में तिथि जोड़ें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- save excel file
- write date to excel
- save workbook as xlsx
- add date to worksheet
language: hi
lastmod: 2026-10-13
og_description: C# में एक्सेल वर्कबुक बनाएं और एक्सेल में तारीख लिखें। इस पूर्ण गाइड
  का पालन करके एक्सेल फ़ाइल को xlsx के रूप में सहेजें और Aspose.Cells के साथ वर्कशीट
  में तारीख जोड़ें।
og_image_alt: Excel workbook screenshot showing a Japanese imperial date in cell A1
og_title: एक्सेल वर्कबुक बनाएं और वर्कशीट में तिथि जोड़ें – C# चरण‑दर‑चरण
schemas:
- author: Aspose
  dateModified: '2026-10-13'
  description: Create excel workbook in C# and write date to excel using Aspose.Cells.
    Learn to save excel file as xlsx and add date to worksheet with full code.
  headline: Create excel workbook and add date to worksheet in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में एक्सेल वर्कबुक बनाएं और वर्कशीट में तारीख जोड़ें
url: /hi/net/excel-workbook/create-excel-workbook-and-add-date-to-worksheet-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Excel वर्कबुक बनाएं और वर्कशीट में तिथि जोड़ें

यदि आपको प्रोग्रामेटिक रूप से **create excel workbook** करने की आवश्यकता है, तो यह गाइड आपको **write date to excel** और **save excel file** को *.xlsx* वर्कबुक के रूप में कैसे करना है दिखाता है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो एक जापानी साम्राज्य युग स्ट्रिंग को पार्स करता है और परिणामी `DateTime` को सेल A1 में संग्रहीत करता है।

C# से Excel के साथ काम करने में अक्सर तीन चरणों की आवश्यकता होती है: वर्कबुक को instantiate करना, डेटा को वर्कशीट पर रखना, और अंत में फ़ाइल को persist करना। यह ट्यूटोरियल प्रत्येक चरण को कवर करता है, बताता है कि कोड इस तरह लिखा गया है, और सामान्य pitfalls जैसे culture‑specific parsing और file‑system permissions को उजागर करता है। अंत तक आप **add date to worksheet**, **save workbook as xlsx**, और इस पैटर्न को किसी भी डेटा प्रकार के लिए अनुकूलित कर सकते हैं।

> **Prerequisite** – नमूना **Aspose.Cells for .NET** लाइब्रेरी (संस्करण 23.10 या बाद) का उपयोग करता है। इसे NuGet के माध्यम से स्थापित करें:

```bash
dotnet add package Aspose.Cells
```

आपको एक .NET 6+ SDK और आउटपुट फ़ाइल के लिए एक लिखने योग्य डायरेक्टरी की भी आवश्यकता है।

---

## Excel वर्कबुक बनाएं और वर्कशीट कॉन्फ़िगर करें

पहला चरण एक खाली वर्कबुक को instantiate करना और उसकी डिफ़ॉल्ट वर्कशीट को प्राप्त करना है। Aspose.Cells स्वचालित रूप से “Sheet1” नाम की एक शीट के साथ वर्कबुक बनाता है।

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

// Step 1: Create a new workbook
Workbook workbook = new Workbook();

// Step 2: Get the first worksheet (index 0)
Worksheet sheet = workbook.Worksheets[0];
```

**Why this matters** – `Workbook` सभी Excel ऑपरेशन्स का एंट्री पॉइंट है। इसे बिना पैरामीटर के बनाकर आप एक साफ़ वर्कबुक प्राप्त करते हैं जिसे आप बाद में किसी भी फ़ॉर्मेट में **save excel file** कर सकते हैं।

---

## जापानी साम्राज्य तिथि को पार्स करें

जापानी साम्राज्य तिथियों में एक युग प्रतीक (जैसे, “R” रीवा के लिए) के बाद दो-अंकीय वर्ष होता है। .NET `DateTime.ParseExact` मेथड इस फ़ॉर्मेट को संभाल सकता है जब आप एक कस्टम `DateTimeParseOptions` ऑब्जेक्ट प्रदान करते हैं जो पार्सर को जापानी सम्राट कैलेंडर उपयोग करने के लिए बताता है।

```csharp
// Step 3: Define a date string in the Japanese imperial era
string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

// Step 4: Configure parsing options for the Japanese Emperor calendar
var parseOptions = new DateTimeParseOptions
{
    Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
};

// Step 5: Parse the string into a .NET DateTime
DateTime parsedDate = DateTime.ParseExact(
    imperialDate,
    "ggyy/MM/dd",
    CultureInfo.InvariantCulture,
    DateTimeStyles.None,
    parseOptions);
```

**Explanation** –  
* `gg` युग डिज़ाइनटर (`R` रीवा के लिए) पढ़ता है।  
* `yy` उस युग के भीतर दो-अंकीय वर्ष पढ़ता है।  
* `MM/dd` माह और दिन पढ़ता है।  

यदि आप `parseOptions` को छोड़ देते हैं, तो पार्सर ग्रेगोरियन कैलेंडर मान लेता है और `FormatException` फेंकता है। यह गैर‑ग्रेगोरियन कैलेंडरों से निपटते समय एक सामान्य एज केस है।

---

## तिथि को वर्कशीट में लिखें

अब जब आपके पास एक `DateTime` मान है, आप इसे एक सेल में रख सकते हैं। Aspose.Cells स्वचालित रूप से सेल को मान के प्रकार के आधार पर फ़ॉर्मेट करता है।

```csharp
// Step 6: Write the parsed date into cell A1
sheet.Cells["A1"].PutValue(parsedDate);

// Optional: Apply a date format for better readability
Style style = workbook.CreateStyle();
style.Custom = "yyyy-mm-dd";
sheet.Cells["A1"].SetStyle(style);
```

**Why set a style?** – बिना स्टाइल के, Excel तिथि को सिस्टम की डिफ़ॉल्ट फ़ॉर्मेट में दिखा सकता है, जो अन्य लोकेल के उपयोगकर्ताओं के लिए भ्रमित कर सकता है। स्पष्ट रूप से `"yyyy-mm-dd"` परिभाषित करने से एक सुसंगत रूप सुनिश्चित होता है।

---

## Excel फ़ाइल को xlsx के रूप में सहेजें

अंत में, वर्कबुक को डिस्क पर persist करें। `Save` मेथड फ़ाइल एक्सटेंशन से आउटपुट फ़ॉर्मेट निर्धारित करता है, इसलिए “.xlsx” का उपयोग करने से स्वचालित रूप से Office Open XML फ़ॉर्मेट सक्रिय हो जाता है।

```csharp
// Step 7: Define the output path (adjust to your environment)
string outputPath = Path.Combine(
    Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
    "JapaneseDate.xlsx");

// Step 8: Save the workbook
workbook.Save(outputPath, SaveFormat.Xlsx);
```

**Tip** – यदि लक्ष्य डायरेक्टरी मौजूद नहीं है या आपके पास लिखने की अनुमति नहीं है, तो `Save` `IOException` फेंकता है। `Save` को कॉल करने से पहले हमेशा पाथ की जाँच करें।

---

## पूर्ण चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी, पेस्ट और चलाएँ। इसमें सभी `using` निर्देश, त्रुटि संभालना, और टिप्पणियाँ शामिल हैं जो प्रत्येक ऑपरेशन को स्पष्ट करती हैं।

```csharp
using Aspose.Cells;
using System;
using System.Globalization;
using System.IO;

class Program
{
    static void Main()
    {
        try
        {
            // 1️⃣ Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.Worksheets[0];

            // 2️⃣ Define the Japanese imperial date string
            string imperialDate = "R3/04/01"; // Reiwa 3, April 1st

            // 3️⃣ Set up parsing options for the Japanese Emperor calendar
            var parseOptions = new DateTimeParseOptions
            {
                Calendar = DateTimeParseOptions.CalendarType.JapaneseEmperor
            };

            // 4️⃣ Parse the string into a .NET DateTime
            DateTime parsedDate = DateTime.ParseExact(
                imperialDate,
                "ggyy/MM/dd",
                CultureInfo.InvariantCulture,
                DateTimeStyles.None,
                parseOptions);

            // 5️⃣ Write the date to cell A1
            sheet.Cells["A1"].PutValue(parsedDate);

            // Apply a consistent date format
            Style dateStyle = workbook.CreateStyle();
            dateStyle.Custom = "yyyy-mm-dd";
            sheet.Cells["A1"].SetStyle(dateStyle);

            // 6️⃣ Determine the output file location
            string outputPath = Path.Combine(
                Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
                "JapaneseDate.xlsx");

            // 7️⃣ Save the workbook as an .xlsx file
            workbook.Save(outputPath, SaveFormat.Xlsx);

            Console.WriteLine($"Workbook saved successfully to: {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

**Expected result**

जब आप `JapaneseDate.xlsx` खोलते हैं, तो सेल A1 में तिथि **2021‑04‑01** (Reiwa 3 / 04 / 01 का ग्रेगोरियन समकक्ष) `yyyy‑mm‑dd` फ़ॉर्मेट में प्रदर्शित होती है।

![Excel workbook with date in cell A1](excel-date-screenshot.png){alt="एक Excel वर्कबुक का स्क्रीनशॉट जिसमें सेल A1 में जापानी साम्राज्य तिथि दिख रही है"}

---

## सामान्य प्रश्न और किनारे के मामलों

| Question | Answer |
|----------|--------|
| *यदि युग बदलता है (उदाहरण के लिए, हेइसेई से रीवा) तो क्या होगा?* | `JapaneseEmperor` कैलेंडर स्वचालित रूप से युग प्रतीकों (`H`, `R`, आदि) को सही ग्रेगोरियन रेंज से मैप करता है, इसलिए आपको केवल इनपुट स्ट्रिंग को अपडेट करने की आवश्यकता है। |
| *क्या मैं एक कॉलम में कई तिथियाँ लिख सकता हूँ?* | हां। अपने डेटा पर लूप करें और प्रत्येक पंक्ति के लिए `sheet.Cells[row, column].PutValue(dateValue)` कॉल करें। |
| *यदि मुझे अलग तिथि फ़ॉर्मेट चाहिए तो क्या करें?* | `dateStyle.Custom` को किसी भी Excel तिथि फ़ॉर्मेट स्ट्रिंग जैसे `"dd-mmm-yyyy"` या `"mm/dd/yyyy"` में बदलें। |
| *तिथि लिखने के बाद शीट को सुरक्षित करने का कोई तरीका है?* | सेव करने से पहले `sheet.Protect(ProtectOptions.All, "password")` का उपयोग करें। |
| *मैं टाइम ज़ोन को कैसे संभालूँ?* | `DateTime` UTC या स्थानीय समय संग्रहीत करता है। `PutValue` कॉल करने से पहले `DateTime.SpecifyKind` या `TimeZoneInfo.ConvertTime` का उपयोग करके बदलें। |

---

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells का उपयोग करके C# में **create excel workbook**, **write date to excel**, **add date to worksheet**, और **save workbook as xlsx** कैसे किया जाता है। पूर्ण उदाहरण एक जापानी साम्राज्य कैलेंडर स्ट्रिंग को पार्स करना, एक सुसंगत शैली लागू करना, और फ़ाइल‑सिस्टम संबंधी चिंताओं को संभालना दर्शाता है।  

यहाँ से आप

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Excel वर्कबुक बनाएं C# – टिप्पणी जोड़ें और XLSX के रूप में सहेजें](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)
- [C# में नया वर्कबुक बनाएं – फ़ॉर्मूला जोड़ें और Excel फ़ाइल सहेजें](/cells/english/net/excel-workbook/create-new-workbook-in-c-add-formula-and-save-excel-file/)
- [Excel वर्कबुक बनाएं – कॉलम रैप करें और XLSX के रूप में सहेजें](/cells/english/net/formatting-rows-and-columns-in-excel/create-excel-workbook-wrap-columns-and-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}