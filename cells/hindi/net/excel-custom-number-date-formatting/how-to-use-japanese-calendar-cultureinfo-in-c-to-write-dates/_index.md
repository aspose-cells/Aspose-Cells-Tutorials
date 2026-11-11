---
category: general
date: 2026-10-26
description: C# में जापानी कैलेंडर CultureInfo का उपयोग करके युग तिथियों को पार्स
  करने और उन्हें NPOI के साथ Excel वर्कशीट में डालने के तरीके सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- use japanese calendar cultureinfo
- japanese era date parsing
- cultureinfo with japanese calendar
- datetime parse with cultureinfo
- npoi excel cultureinfo
language: hi
lastmod: 2026-10-26
og_description: C# में Japanese calendar CultureInfo का उपयोग करके रैवा युग की तिथियों
  को पार्स करें और उन्हें Excel वर्कशीट में लिखें। पूर्ण, चलाने योग्य कोड के साथ व्याख्याएँ।
og_image_alt: Screenshot of C# code parsing a Japanese era date and inserting it into
  an Excel cell
og_title: C# में जापानी कैलेंडर CultureInfo का उपयोग करें – पूर्ण Excel उदाहरण
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use Japanese calendar CultureInfo in C# when parsing era
    dates and inserting them into an Excel worksheet with NPOI.
  headline: How to use Japanese calendar CultureInfo in C# to write dates to Excel
  type: TechArticle
tags:
- C#
- CultureInfo
- Excel
- NPOI
- Internationalization
title: C# में जापानी कैलेंडर CultureInfo का उपयोग करके Excel में तिथियों को लिखना
  कैसे करें
url: /hi/net/excel-custom-number-date-formatting/how-to-use-japanese-calendar-cultureinfo-in-c-to-write-dates/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Japanese calendar CultureInfo का उपयोग करके Excel में तिथियों को लिखना कैसे करें

यदि आपको C# में तिथियों के साथ काम करते समय **Japanese calendar CultureInfo** का उपयोग करना है, तो यह गाइड आपको बिल्कुल बताता है कि कैसे करना है। आप सीखेंगे कि कैसे एक तिथि स्ट्रिंग को पार्स करें जिसमें Japanese era name हो (उदाहरण के लिए, *Reiwa 2/5/1*) और फिर NPOI लाइब्रेरी का उपयोग करके `DateTime` को Excel वर्कशीट की पहली सेल में लिखें।

सही `CultureInfo` के बिना era‑आधारित तिथियों को पार्स करने से `FormatException` या गलत माह/दिन मान प्राप्त हो सकते हैं। `CultureInfo` को Japanese calendar पर सेट करके, आप सुनिश्चित करते हैं कि .NET रनटाइम era को सही ढंग से समझे और Excel में संग्रहीत मान मूल Japanese नोटेशन से मेल खाए।

इस ट्यूटोरियल में आप करेंगे:

* एक `CultureInfo` ऑब्जेक्ट बनाना जो Japanese calendar का उपयोग करता है।
* `DateTime.Parse` के साथ Japanese era तिथि स्ट्रिंग को पार्स करना।
* पार्स किए गए `DateTime` को NPOI वर्कशीट सेल में डालना।
* पूर्ण, चलाने योग्य प्रोग्राम और अपेक्षित आउटपुट देखना।

> **Prerequisites** – .NET 6.0+ (या .NET Core 3.1+), **NPOI** NuGet पैकेज, और C# तथा Excel फ़ाइल हैंडलिंग की बुनियादी समझ।

---

## आप क्या चाहिए

| आइटम | कारण |
|------|--------|
| **.NET SDK** (6.0 या बाद का) | `CultureInfo` के लिए रनटाइम और लाइब्रेरी प्रदान करता है। |
| **NPOI** (`NPOI` NuGet पैकेज) | Office स्थापित किए बिना Excel फ़ाइलें बनाने और संशोधित करने की अनुमति देता है। |
| **Visual Studio Code**, **Visual Studio**, या कोई भी C# IDE | सैंपल को संकलित और चलाने के लिए। |
| **Japanese era date string** (उदा., `"Reiwa 2/5/1"`) | Japanese calendar के उपयोग को दर्शाता है। |

---

## चरण 1: NPOI स्थापित करें

अपने प्रोजेक्ट फ़ोल्डर में एक टर्मिनल खोलें और चलाएँ:

```bash
dotnet add package NPOI --version 2.6.1
```

यह पैकेज बाद में उपयोग किए जाने वाले `IWorkbook`, `ISheet`, और `ICell` टाइप्स प्रदान करता है।

---

## चरण 2: एक CultureInfo बनाएं जो Japanese calendar का उपयोग करता है

Japanese calendar एक era‑आधारित कैलेंडर है। आपको `ja-JP` लोकैल के *Japanese* वैरिएंट का अनुरोध करना होगा और स्पष्ट रूप से कैलेंडर को `JapaneseCalendar` पर सेट करना होगा।

```csharp
using System;
using System.Globalization;

// Create a CultureInfo based on Japanese locale and switch its calendar.
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();
```

> **Why this matters** – डिफ़ॉल्ट `ja-JP` संस्कृति Gregorian कैलेंडर का उपयोग करती है। `Calendar` प्रॉपर्टी को पुनः असाइन करने से *Reiwa* जैसे era नाम पार्सिंग के दौरान पहचाने जाते हैं।

---

## चरण 3: एक Japanese era तिथि स्ट्रिंग को पार्स करें

अब जब `CultureInfo` कॉन्फ़िगर हो गया है, आप सुरक्षित रूप से एक ऐसी स्ट्रिंग को पार्स कर सकते हैं जिसमें era नाम हो।

```csharp
// Example Japanese era date: Reiwa 2 (2020) year, May 1st.
string eraDate = "Reiwa 2/5/1";

// Parse using the Japanese CultureInfo created earlier.
DateTime reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
Console.WriteLine($"Parsed DateTime (UTC): {reiwaDate:u}");
```

**Output**

```
Parsed DateTime (UTC): 2020-05-01 00:00:00Z
```

`Parse` मेथड *Reiwa 2* को Gregorian वर्ष 2020, माह 5, दिन 1 के रूप में व्याख्या करता है।

### किनारे का मामला: अमान्य युगों को संभालना

यदि कोई उपयोगकर्ता असमर्थित era प्रदान करता है (उदा., Heisei युग समाप्त होने के बाद `"Heisei 31/4/30"`), तो `DateTime.Parse` `FormatException` फेंकेगा। एक दोस्ताना त्रुटि संदेश देने के लिए कॉल को try‑catch ब्लॉक में लपेटें:

```csharp
try
{
    DateTime parsed = DateTime.Parse(input, japaneseCulture);
}
catch (FormatException)
{
    Console.Error.WriteLine($"'{input}' is not a valid Japanese era date.");
}
```

---

## चरण 4: पार्स किए गए DateTime को Excel वर्कशीट में लिखें

`DateTime` ऑब्जेक्ट तैयार होने पर, आप इसे Excel सेल में संग्रहीत कर सकते हैं। NPOI स्वचालित रूप से `DateTime` मानों को Excel तिथियों के रूप में फॉर्मेट करता है।

```csharp
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;
using System.IO;

// Create a new workbook and a sheet.
IWorkbook workbook = new XSSFWorkbook();
ISheet sheet = workbook.CreateSheet("Japanese Dates");

// Write the DateTime into cell A1 (row 0, column 0).
IRow row = sheet.CreateRow(0);
ICell cell = row.CreateCell(0);
cell.SetCellValue(reiwaDate);

// Optionally apply a date style that shows the era (Excel does not have a built‑in era format,
// so we keep the Gregorian representation).
ICellStyle dateStyle = workbook.CreateCellStyle();
short dateFormatId = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
dateStyle.DataFormat = dateFormatId;
cell.CellStyle = dateStyle;

// Save the workbook to a file.
using (FileStream fs = new FileStream("JapaneseEraDate.xlsx", FileMode.Create, FileAccess.Write))
{
    workbook.Write(fs);
}
Console.WriteLine("Excel file 'JapaneseEraDate.xlsx' created successfully.");
```

**Result** – *JapaneseEraDate.xlsx* खोलने पर सेल A1 में तिथि **2020‑05‑01** दिखती है।

### NPOI का उपयोग क्यों करें?

*Works on any platform* (Windows, Linux, macOS) और Microsoft Office की आवश्यकता **नहीं** होती। यह समाधान CI पाइपलाइनों, Docker कंटेनरों, या सर्वर‑साइड प्रोसेसिंग के लिए उपयुक्त बनाता है।

---

## चरण 5: पूर्ण, चलाने योग्य प्रोग्राम

सब कुछ एक साथ रखते हुए, यहाँ एक पूर्ण कंसोल एप्लिकेशन है जो पूरे फ्लो को दर्शाता है:

```csharp
// File: Program.cs
using System;
using System.Globalization;
using System.IO;
using NPOI.SS.UserModel;
using NPOI.XSSF.UserModel;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure CultureInfo for the Japanese calendar.
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseCalendar();

        // 2️⃣ Parse a Japanese era date string.
        string eraDate = "Reiwa 2/5/1";
        DateTime reiwaDate;
        try
        {
            reiwaDate = DateTime.Parse(eraDate, japaneseCulture);
            Console.WriteLine($"Parsed DateTime: {reiwaDate:u}");
        }
        catch (FormatException)
        {
            Console.Error.WriteLine($"'{eraDate}' is not a valid Japanese era date.");
            return;
        }

        // 3️⃣ Create an Excel workbook and write the date.
        IWorkbook workbook = new XSSFWorkbook();
        ISheet sheet = workbook.CreateSheet("Japanese Dates");
        IRow row = sheet.CreateRow(0);
        ICell cell = row.CreateCell(0);
        cell.SetCellValue(reiwaDate);

        // Apply a simple Gregorian date format.
        ICellStyle style = workbook.CreateCellStyle();
        short fmt = workbook.CreateDataFormat().GetFormat("yyyy-mm-dd");
        style.DataFormat = fmt;
        cell.CellStyle = style;

        // 4️⃣ Save the workbook.
        const string fileName = "JapaneseEraDate.xlsx";
        using (FileStream fs = new FileStream(fileName, FileMode.Create, FileAccess.Write))
        {
            workbook.Write(fs);
        }

        Console.WriteLine($"Excel file '{fileName}' created successfully.");
    }
}
```

**How to run**

```bash
dotnet run
```

चलाने के बाद, आप प्रोजेक्ट फ़ोल्डर में `JapaneseEraDate.xlsx` पाएँगे जिसमें सही ढंग से पार्स की गई तिथि होगी।

---

## सामान्य pitfalls और सर्वोत्तम‑प्रैक्टिस टिप्स

| समस्या | समाधान / सिफारिश |
|---------|----------------------|
| `japaneseCulture.DateTimeFormat.Calendar` सेट करना भूल जाना | हमेशा एक `JapaneseCalendar` इंस्टेंस असाइन करें; अन्यथा era नाम पहचाना नहीं जाएगा। |
| कस्टम `CultureInfo` के बिना `DateTime.TryParse` का उपयोग करना | समान व्यवहार बनाए रखने के लिए `TryParse` को वही `japaneseCulture` पास करें। |
| Excel से era नाम दिखाने की उम्मीद करना | Excel के बिल्ट‑इन तिथि फ़ॉर्मेट केवल Gregorian हैं। यदि आपको era दिखाना है, तो मूल स्ट्रिंग को अलग कॉलम में रखें या कस्टम टेक्स्ट फ़ॉर्मेट बनाएं। |
| `FileStream` को डिस्पोज़ न करना | जैसा दिखाया गया है, फ़ाइल हैंडल को तुरंत रिलीज़ करने के लिए `using` ब्लॉक का उपयोग करें। |
| थ्रेड्स के बीच `CultureInfo` ऑब्जेक्ट्स को मिलाना | `CultureInfo` पढ़ने‑के‑लिए थ्रेड‑सेफ़ है, लेकिन प्रारंभिक सेटअप के बाद उसके `Calendar` प्रॉपर्टी को बदलने से बचें। |

---

## निष्कर्ष

अब आप जानते हैं कि **Japanese calendar CultureInfo** को C# में कैसे उपयोग करके Japanese era तिथियों को सही ढंग से पार्स करें और NPOI के साथ Excel वर्कशीट में परिणामी `DateTime` लिखें। यह पूर्ण उदाहरण कॉन्फ़िगरेशन, पार्सिंग, त्रुटि संभालना, और Excel आउटपुट को कवर करता है, जिससे आप किसी भी अंतर्राष्ट्रीय रिपोर्टिंग या डेटा‑एक्सचेंज परिदृश्य के लिए एक ठोस आधार प्राप्त करते हैं।

आगे, आप खोज सकते हैं:

* **कस्टम टेक्स्ट के साथ तिथियों को फॉर्मेट करना** ताकि Excel में era नाम बना रहे।
* **Excel से तिथियों को पढ़ना** `cell.DateCellValue` का उपयोग करके और Japanese calendar का सम्मान करना।
* **इसी तकनीक को अन्य era‑आधारित कैलेंडरों** (जैसे Thai Buddhist calendar) के लिए लागू करना, `JapaneseCalendar` को उपयुक्त `Calendar` सबक्लास से बदलकर।

विभिन्न era स्ट्रिंग्स, बड़े डेटा सेट, या इस लॉजिक को ASP.NET Core APIs में एकीकृत करके Excel रिपोर्ट्स को ऑन‑द‑फ़्लाई जनरेट करने के साथ प्रयोग करने में संकोच न करें। Happy coding!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Create Excel Workbook with Japanese Calendar Dates – Full Guide](/cells/english/net/excel-custom-number-date-formatting/create-excel-workbook-with-japanese-calendar-dates-full-guid/)
- [Parse Japanese Era Dates in Excel – Full Guide for C# Developers](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [How to create Excel workbook and parse Japanese dates in C#](/cells/english/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-and-parse-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}