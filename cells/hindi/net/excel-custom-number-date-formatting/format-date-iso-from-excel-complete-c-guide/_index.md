---
category: general
date: 2026-03-30
description: Aspose.Cells का उपयोग करके C# में Excel datetime मान पढ़ते समय ISO तिथि
  को फ़ॉर्मेट करना सीखें और datetime Excel डेटा निकालें।
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: hi
og_description: Aspose.Cells का उपयोग करके Excel डेटा से ISO तिथि को फॉर्मेट करें।
  यह गाइड दिखाता है कि Excel datetime को कैसे पढ़ें, datetime Excel मानों को निकालें,
  और ISO तिथियों को आउटपुट करें।
og_title: Excel से ISO तिथि फ़ॉर्मेट – चरण‑दर‑चरण C# ट्यूटोरियल
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Excel से ISO तिथि फ़ॉर्मेट – पूर्ण C# गाइड
url: /hi/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel से तिथि को iso फ़ॉर्मेट करें – पूर्ण C# गाइड

क्या आपको कभी Excel शीट से तिथियों को निकालते समय **format date iso** करने की ज़रूरत पड़ी है? शायद आप जापानी युग तिथियों से निपट रहे हैं, या आप सिर्फ API पेलोड के लिए एक साफ़ `yyyy‑MM‑dd` स्ट्रिंग चाहते हैं। इस ट्यूटोरियल में आप देखेंगे कि कैसे **read Excel datetime** सेल्स, **extract datetime Excel** वैल्यूज़ को पढ़ें, और उन्हें ISO‑8601 फ़ॉर्मेट में बदलें—बिना किसी अनुमान के।

हम एक वास्तविक‑दुनिया उदाहरण के माध्यम से चलेंगे जो Aspose.Cells का उपयोग करता है, बताता है कि प्रत्येक पंक्ति क्यों महत्वपूर्ण है, और आपको अंतिम आउटपुट दिखाता है जिसे आप अपने प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। अंत तक, आप “令和3年5月1日” जैसी विचित्र युग स्ट्रिंग्स को संभाल सकेंगे और एक मानक ISO तिथि उत्पन्न कर सकेंगे, जो डेटाबेस, JSON, या जहाँ भी आपको चाहिए, के लिए तैयार है।

## आवश्यकताएँ

- .NET 6.0 या बाद का (कोड .NET Framework के साथ भी काम करता है)
- Aspose.Cells for .NET (फ्री ट्रायल या लाइसेंस्ड संस्करण)
- C# और Excel अवधारणाओं की बुनियादी परिचितता
- Visual Studio या कोई भी C# एडिटर जो आपको पसंद हो

Aspose.Cells के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है, इसलिए सेटअप काफी सरल है।

---

## चरण 1: एक Workbook बनाएं और पहली Worksheet को लक्ष्य बनाएं

सबसे पहला काम आप एक नया `Workbook` ऑब्जेक्ट बनाते हैं। यह आपको Excel फ़ाइल का इन‑मेमोरी प्रतिनिधित्व देता है, जिसे आप फिर बदल या पढ़ सकते हैं।

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*यह क्यों महत्वपूर्ण है:*  
प्रोग्रामेटिकली workbook बनाने से आप परीक्षण के दौरान फिजिकल फ़ाइलों से निपटने से बचते हैं। यह यह भी सुनिश्चित करता है कि worksheet रेफ़रेंस हमेशा वैध रहे—बाद में जब आप **read Excel datetime** वैल्यूज़ पढ़ने की कोशिश करेंगे तो कोई null‑reference आश्चर्य नहीं होगा।

---

## चरण 2: एक Japanese Era तिथि स्ट्रिंग को सेल में लिखें

हमारा लक्ष्य एक गैर‑ग्रेगोरियन तिथि को पार्स करने का प्रदर्शन करना है। हम युग स्ट्रिंग को सीधे सेल **A1** में रखेंगे।

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*प्रो टिप:* यदि आप किसी मौजूदा workbook से डेटा खींच रहे हैं, तो आप `PutValue` कॉल को छोड़ देंगे और बस उस सेल को रेफ़र करेंगे जिसमें पहले से ही तिथि मौजूद है। मुख्य बात यह है कि सेल एक **string** रखता है जो Japanese lunisolar calendar में तिथि को दर्शाता है।

---

## चरण 3: एक Culture कॉन्फ़िगर करें जो Japanese Lunisolar Calendar को समझता हो

.NET की `CultureInfo` क्लास आपको यह निर्दिष्ट करने देती है कि तिथियों को कैसे व्याख्या किया जाए। डिफ़ॉल्ट Gregorian calendar को `JapaneseLunisolarCalendar` से बदलकर, आप parser को आवश्यक संदर्भ प्रदान करते हैं।

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*हम यह क्यों करते हैं:*  
यदि आप डिफ़ॉल्ट culture के साथ “令和3年5月1日” को पार्स करने की कोशिश करेंगे, तो .NET एक `FormatException` फेंकेगा। lunisolar calendar को स्वैप करने से runtime को ठीक‑ठीक बताता है कि “令和3年” (Reiwa युग का 3rd वर्ष) को Gregorian वर्ष 2021 में कैसे मैप किया जाए।

---

## चरण 4: कॉन्फ़िगर किए गए Culture का उपयोग करके सेल वैल्यू को `DateTime` के रूप में पार्स करें

अब ऑपरेशन का मुख्य भाग आता है—उस युग स्ट्रिंग को एक उचित `DateTime` ऑब्जेक्ट में बदलना। Aspose.Cells एक सुविधाजनक `GetDateTime` ओवरलोड प्रदान करता है जो एक `CultureInfo` स्वीकार करता है।

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*अंदर क्या हो रहा है:*  
`GetDateTime` कच्ची स्ट्रिंग पढ़ता है, प्रदान किए गए culture के कैलेंडर नियम लागू करता है, और एक `DateTime` लौटाता है जो Gregorian कैलेंडर में उसी क्षण को दर्शाता है। यही वह क्षण है जहाँ आप **extract datetime Excel** डेटा को .NET में काम करने योग्य रूप में प्राप्त करते हैं।

---

## चरण 5: पार्स की गई तिथि को ISO 8601 फ़ॉर्मेट में आउटपुट करें

अंत में, हम `DateTime` को ISO स्ट्रिंग—`yyyy‑MM‑dd`—के रूप में फ़ॉर्मेट करते हैं—जो APIs, डेटाबेस, और फ्रंट‑एंड फ्रेमवर्क्स द्वारा सार्वभौमिक रूप से स्वीकार किया जाता है।

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*ISO क्यों?*  
ISO 8601 अस्पष्टता को समाप्त करता है। “05/01/2021” लोकैल के आधार पर मई 1 या जनवरी 5 हो सकता है। `2021-05-01` स्पष्ट है, इसलिए हम लगभग हर इंटीग्रेशन परिदृश्य में **format date iso** करते हैं।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, तैयार‑चलाने योग्य प्रोग्राम दिया गया है। इसे एक कंसोल ऐप प्रोजेक्ट में कॉपी करें, Aspose.Cells रेफ़रेंस जोड़ें, और **F5** दबाएँ।

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**अपेक्षित आउटपुट**

```
2021-05-01
```

इसे एक बार चलाएँ, और आप कंसोल में ISO‑फ़ॉर्मेटेड तिथि प्रिंट होते देखेंगे। यही पूरी पाइपलाइन है **read Excel datetime** से **format date iso** तक।

---

## सामान्य किनारे के मामलों को संभालना

### 1. वास्तविक Excel तिथि संख्याएँ रखने वाले सेल्स

कभी‑कभी Excel तिथियों को सीरियल नंबरों (जैसे, `44204`) के रूप में संग्रहीत करता है। ऐसे में आपको culture की आवश्यकता नहीं है; बस `GetDateTime()` को बिना पैरामीटर के कॉल करें:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. खाली या अमान्य सेल्स

यदि कोई सेल खाली है या उसमें एक अपरसिबल स्ट्रिंग है, तो `GetDateTime` फेंकेगा। कॉल को `try/catch` में रैप करें या पहले `IsDateTime` जांचें:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. विभिन्न युग फ़ॉर्मेट्स

अन्य Japanese युग (Heisei, Showa) भी समान पैटर्न का पालन करते हैं। वही `JapaneseLunisolarCalendar` उन्हें स्वतः संभालेगा, इसलिए आपको अतिरिक्त लॉजिक की जरूरत नहीं—सिर्फ स्ट्रिंग दें।

---

## प्रो टिप्स और गॉटचाज़

- **Performance:** बड़े स्प्रेडशीट्स को प्रोसेस करते समय, लूप के अंदर नया `CultureInfo` बनाने के बजाय एक ही `CultureInfo` इंस्टेंस को पुनः उपयोग करें।
- **Thread Safety:** `CultureInfo` ऑब्जेक्ट्स कैलेंडर सेट करने के बाद पढ़ने‑के‑लिए‑केवल (read‑only) होते हैं, इसलिए उन्हें थ्रेड्स के बीच सुरक्षित रूप से साझा किया जा सकता है।
- **Aspose.Cells Licensing:** यदि आप फ्री ट्रायल उपयोग कर रहे हैं, तो याद रखें कि ट्रायल अवधि समाप्त होने के बाद कुछ फीचर्स सीमित हो सकते हैं। यहाँ दिखाया गया डेट पार्सिंग ट्रायल और लाइसेंस्ड दोनों मोड में ठीक काम करता है।
- **Time Zones:** आपके द्वारा प्राप्त `DateTime` **unspecified** (कोई टाइमज़ोन नहीं) है। यदि आपको UTC चाहिए, तो `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` कॉल करें या `TimeZoneInfo` का उपयोग करके कनवर्ट करें।

---

## निष्कर्ष

हमने C# का उपयोग करके Excel वर्कबुक से **format date iso** करने के लिए आवश्यक सभी चीज़ें कवर कर ली हैं। एक कच्ची Japanese era स्ट्रिंग से शुरू करके, हमने **read Excel datetime**, उचित culture सेट किया, **extract datetime Excel** डेटा प्राप्त किया, और अंत में एक साफ़ ISO‑8601 स्ट्रिंग आउटपुट की। यह तरीका किसी भी तिथि प्रतिनिधित्व के लिए काम करता है जो Excel आपके सामने रख सकता है, चाहे वह सीरियल नंबर हो, लोकैल‑विशिष्ट स्ट्रिंग, या पारंपरिक युग फ़ॉर्मेट।

अगले कदम? पूरी कॉलम की तिथियों पर लूप चलाने की कोशिश करें, ISO परिणामों को नई शीट में लिखें, या उन्हें सीधे वेब सर्विस के लिए JSON पेलोड में फीड करें। यदि आप अन्य कैलेंडर सिस्टम (Hebrew, Islamic) के बारे में जिज्ञासु हैं, तो Aspose.Cells और .NET की `CultureInfo` इन प्रयोगों को भी उतना ही आसान बनाते हैं।

कोई प्रश्न या कठिन तिथि फ़ॉर्मेट है जिसे आप नहीं सुलझा पा रहे? नीचे टिप्पणी छोड़ें, और खुश कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}