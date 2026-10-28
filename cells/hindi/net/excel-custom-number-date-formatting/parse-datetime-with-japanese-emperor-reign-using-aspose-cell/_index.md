---
category: general
date: 2026-09-24
description: Aspose.Cells का उपयोग करके C# में जापानी सम्राट के राजकाल के साथ DateTime
  को पार्स करें। जापानी युग कैलेंडर को सक्षम करें, युग स्ट्रिंग लिखें, और सटीक DateTime
  मान प्राप्त करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- Parse DateTime with Japanese Emperor Reign
- Aspose.Cells
- C# date parsing
- Japanese era calendar
- Workbook Settings
- DateTimeValue
language: hi
lastmod: 2026-09-24
og_description: C# में Aspose.Cells का उपयोग करके जापानी सम्राट के राजकाल के साथ DateTime
  को पार्स करें। यह ट्यूटोरियल दिखाता है कि कैसे जापानी युग कैलेंडर को सक्षम किया
  जाए, युग स्ट्रिंग्स लिखी जाएँ, और सही DateTime को पुनः पढ़ा जाए।
og_image_alt: Screenshot of C# code parsing a Japanese era date with Aspose.Cells
og_title: Aspose.Cells का उपयोग करके जापानी सम्राट के राजकाल के साथ DateTime पार्स
  करें – C# गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-24'
  description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  headline: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  type: TechArticle
- description: Parse DateTime with Japanese Emperor Reign using Aspose.Cells in C#.
    Enable the Japanese era calendar, write era strings, and retrieve accurate DateTime
    values.
  name: Parse DateTime with Japanese Emperor Reign using Aspose.Cells
  steps:
  - name: Multiple era formats
    text: 'Aspose.Cells recognises several era representations:'
  - name: Invalid strings
    text: 'When the string cannot be parsed (e.g., `"令和99年13月40日"`), `DateTimeValue`
      returns `DateTime.MinValue`. You can check for this condition:'
  - name: Disabling the feature
    text: 'If you later need to store raw era strings without conversion, set the
      flag back to `false`:'
  - name: Performance tip
    text: Enabling the era calendar adds a small overhead to every `PutValue` call
      that involves strings. If you only parse a handful of cells, enable the flag
      right before the operation and disable it afterward to minimise impact.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DateTime
- Japanese era
- .NET
title: Aspose.Cells का उपयोग करके जापानी सम्राट के राजकाल के साथ DateTime पार्स करें
url: /hi/net/excel-custom-number-date-formatting/parse-datetime-with-japanese-emperor-reign-using-aspose-cell/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells का उपयोग करके जापानी सम्राट के राजकाल के साथ DateTime पार्स करें

यदि आपको .NET एप्लिकेशन में **जापानी सम्राट के राजकाल के साथ DateTime पार्स** करने की आवश्यकता है, तो यह गाइड Aspose.Cells के साथ इसे कैसे करना है, बिल्कुल दिखाता है। जापानी युग कैलेंडर को सक्षम करके, युग‑आधारित स्ट्रिंग लिखकर, और परिणामी `DateTime` मान को पढ़कर, आप मैन्युअल स्ट्रिंग हेरफेर के बिना विश्वसनीय, संस्कृति‑सचेत तिथियां प्राप्त करते हैं।

जापानी युग तिथियों के साथ काम करना वित्त, सरकार, और लेगेसी सिस्टम में सामान्य है जो अभी भी “令和3年5月10日” जैसी तिथियां संग्रहीत करते हैं। यह ट्यूटोरियल पूर्ण कार्यप्रवाह को कवर करता है, प्रोजेक्ट सेटअप से लेकर एक `DateTime` ऑब्जेक्ट प्राप्त करने तक, जिसे आप गणनाओं, लॉगिंग, या UI डिस्प्ले में उपयोग कर सकते हैं।

## आप क्या सीखेंगे

- C# प्रोजेक्ट में Aspose.Cells NuGet पैकेज कैसे जोड़ें।  
- `Workbook.Settings` के माध्यम से **Japanese era calendar** को कैसे चालू करें।  
- एक सेल में जापानी युग तिथि स्ट्रिंग कैसे लिखें और Aspose.Cells को इसे स्वचालित रूप से पार्स करने दें।  
- `DateTimeValue` प्रॉपर्टी का उपयोग करके पार्स किया गया `DateTime` कैसे पढ़ें।  

**Prerequisites**  
- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)।  
- C# और Visual Studio (या किसी भी IDE) की बुनियादी परिचितता।  
- Aspose.Cells पैकेज डाउनलोड करने के लिए इंटरनेट एक्सेस।

---

## चरण 1: Aspose.Cells स्थापित करें

टर्मिनल या NuGet पैकेज मैनेजर कंसोल में अपने प्रोजेक्ट फ़ोल्डर को खोलें और चलाएँ:

```bash
dotnet add package Aspose.Cells
```

या, Visual Studio में, प्रोजेक्ट पर राइट‑क्लिक करें → **Manage NuGet Packages** → **Aspose.Cells** खोजें और **Install** पर क्लिक करें। यह `Aspose.Cells` असेंबली जोड़ता है, जो हमें आवश्यक `Workbook`, `Worksheet`, और पार्सिंग क्षमताएँ प्रदान करता है।

## चरण 2: Japanese era calendar सक्षम करें

Aspose.Cells डिफ़ॉल्ट रूप से Japanese era पार्सिंग को अक्षम करता है। आपको इसे `Workbook.Settings.UseJapaneseEraCalendar` फ़्लैग के माध्यम से चालू करना होगा।

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // Create a new workbook instance
        Workbook workbook = new Workbook();

        // Enable parsing of Japanese era dates (e.g., 令和, 平成)
        workbook.Settings.UseJapaneseEraCalendar = true;
```

`UseJapaneseEraCalendar` को `true` सेट करने से लाइब्रेरी को उन स्ट्रिंग्स को व्याख्या करने के लिए कहा जाता है जिनमें युग नाम (`令和`, `平成`, `昭和`, आदि) होते हैं, आधिकारिक जापानी कैलेंडर नियमों के अनुसार।

## चरण 3: एक सेल में जापानी युग तिथि स्ट्रिंग लिखें

अब, पहले वर्कशीट को प्राप्त करें और सेल **A1** में एक जापानी युग तिथि स्ट्रिंग रखें।

```csharp
        // Access the first worksheet (index 0)
        Worksheet sheet = workbook.Worksheets[0];

        // Write the era‑based date string into cell A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");
```

**यह क्यों काम करता है:**  
जब `UseJapaneseEraCalendar` सक्रिय होता है, तो `PutValue` स्ट्रिंग की जांच करता है, युग उपसर्ग (`令和`) को पहचानता है, और आंतरिक रूप से इसे संबंधित ग्रेगोरियन वर्ष (2021) में बदल देता है। लाइब्रेरी फिर इस मान को एक वास्तविक `DateTime` ऑब्जेक्ट के रूप में संग्रहीत करती है, न कि केवल टेक्स्ट के रूप में।

## चरण 4: पार्स किया गया `DateTime` मान प्राप्त करें

अब सेल के `DateTimeValue` को पढ़ें। Aspose.Cells स्वचालित रूप से ग्रेगोरियन तिथि लौटाता है।

```csharp
        // Retrieve the parsed DateTime from cell A1
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Output the result to the console
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
    }
}
```

Running the program prints:

```
Parsed Gregorian date: 2021-05-10
```

आउटपुट पुष्टि करता है कि **Parse DateTime with Japanese Emperor Reign** ने “令和3年5月10日” को सही ढंग से 10 May 2021 में परिवर्तित किया।

## चरण 5: किनारे के मामलों और सामान्य विविधताओं को संभालें

### कई युग स्वरूप

Aspose.Cells कई युग प्रतिनिधित्वों को पहचानता है:

| युग (Japanese) | Gregorian वर्ष सीमा |
|----------------|----------------------|
| 明治 (Meiji)   | 1868‑1912            |
| 大正 (Taishō)  | 1912‑1926            |
| 昭和 (Shōwa)   | 1926‑1989            |
| 平成 (Heisei)  | 1989‑2019            |
| 令和 (Reiwa)   | 2019‑present         |

यदि आपका स्रोत डेटा पूर्ण‑चौड़ाई अक्षरों, स्पेस, या कंजी “年”, “月”, “日” का उपयोग करता है, तो भी पार्सर सफल होता है। उदाहरण के लिए, `"平成31年4月30日"` `2019-04-30` बन जाता है।

### अमान्य स्ट्रिंग्स
जब स्ट्रिंग पार्स नहीं की जा सकती (जैसे, `"令和99年13月40日"`), तो `DateTimeValue` `DateTime.MinValue` लौटाता है। आप इस स्थिति की जाँच कर सकते हैं:

```csharp
if (parsedDate == DateTime.MinValue)
{
    Console.WriteLine("The cell does not contain a valid Japanese era date.");
}
```

### फीचर को अक्षम करना
यदि बाद में आपको रूपांतरण के बिना कच्ची युग स्ट्रिंग्स संग्रहीत करनी हों, तो फ़्लैग को `false` पर सेट करें:

```csharp
workbook.Settings.UseJapaneseEraCalendar = false;
```

### प्रदर्शन टिप
युग कैलेंडर को सक्षम करने से प्रत्येक `PutValue` कॉल में जो स्ट्रिंग्स शामिल करती है, थोड़ा ओवरहेड जुड़ता है। यदि आप केवल कुछ ही सेल्स को पार्स कर रहे हैं, तो ऑपरेशन से ठीक पहले फ़्लैग को सक्षम करें और बाद में इसे अक्षम करें ताकि प्रभाव कम हो।

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम है जिसे आप कॉपी, पेस्ट और तुरंत चला सकते हैं।

```csharp
using Aspose.Cells;
using System;

class ParseJapaneseEraDemo
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Turn on Japanese era parsing
        workbook.Settings.UseJapaneseEraCalendar = true;

        // 3️⃣ Access the first worksheet
        Worksheet sheet = workbook.Worksheets[0];

        // 4️⃣ Write an era date string into A1
        sheet.Cells["A1"].PutValue("令和3年5月10日");

        // 5️⃣ Retrieve the parsed DateTime
        DateTime parsedDate = sheet.Cells["A1"].DateTimeValue;

        // Verify the result
        Console.WriteLine($"Parsed Gregorian date: {parsedDate:yyyy-MM-dd}");
        // Expected output: Parsed Gregorian date: 2021-05-10
    }
}
```

**अपेक्षित आउटपुट**

```
Parsed Gregorian date: 2021-05-10
```

यह प्रोग्राम Aspose.Cells का उपयोग करके **Parse DateTime with Japanese Emperor Reign** के लिए अंत‑से‑अंत प्रवाह दिखाता है, वर्कबुक निर्माण से लेकर उपयोगी `DateTime` ऑब्जेक्ट प्राप्त करने तक।

---

## निष्कर्ष

अब आप जानते हैं कि C# में **Parse DateTime with Japanese Emperor Reign** कैसे करें:

1. **Aspose.Cells** स्थापित करना।  
2. `Workbook.Settings` के माध्यम से **Japanese era calendar** को सक्षम करना।  
3. युग‑आधारित स्ट्रिंग्स को सेल्स में लिखना।  
4. परिणामी `DateTimeValue` को पढ़ना।  

यह तरीका मैन्युअल पार्सिंग लॉजिक को समाप्त करता है, आधिकारिक युग सीमाओं का सम्मान करता है, और मौजूदा .NET तिथि‑हैंडलिंग कोड के साथ सहजता से एकीकृत होता है।  

**अगले कदम**  
- Aspose.Cells की अन्य संस्कृति‑विशिष्ट सुविधाओं का अन्वेषण करें, जैसे Hijri या Thai Buddhist कैलेंडर के लिए **C# date parsing**।  
- इस तकनीक को **Workbook Settings** जैसे `CalcEngine` के साथ मिलाकर युग तिथियों को संदर्भित करने वाले फ़ॉर्मूले का मूल्यांकन करें।  
- पार्स किए गए `DateTime` को रिपोर्टिंग, डेटाबेस स्टोरेज, या UI कंपोनेंट्स में उपयोग करें जिन्हें ग्रेगोरियन तिथियों की आवश्यकता है।  

विभिन्न युग स्ट्रिंग्स के साथ प्रयोग करने, अमान्य इनपुट को संभालने, और समाधान को बड़े डेटा‑इम्पोर्ट पाइपलाइन में एकीकृत करने में स्वतंत्र महसूस करें। कोडिंग का आनंद लें!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Excel में जापानी युग तिथियों को पार्स करें – C# डेवलपर्स के लिए पूर्ण गाइड](/cells/english/net/data-loading-and-parsing/parse-japanese-era-dates-in-excel-full-guide-for-c-developer/)
- [C# में जापानी तिथियों को कैसे पार्स करें – पूर्ण गाइड](/cells/english/net/data-loading-and-parsing/how-to-parse-japanese-dates-in-c-complete-guide/)
- [.NET में Aspose.Cells का उपयोग करके तिथि वैधता कैसे लागू करें: एक व्यापक गाइड](/cells/english/net/data-validation/implement-date-validation-net-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}