---
category: general
date: 2026-09-21
description: C# में SmartMarkerOptions ArrayAsSingle को कॉन्फ़िगर करें ताकि JSON एरेज़
  को Excel वर्कबुक में एक ही सेल मान के रूप में निर्यात किया जा सके।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- configure smartmarkeroptions arrayassingle
- Aspose.Cells smart markers
- export JSON array
- C# DataTable
- Workbook ProcessSmartMarkers
language: hi
lastmod: 2026-09-21
og_description: C# में SmartMarkerOptions ArrayAsSingle को कॉन्फ़िगर करके JSON एरेज़
  को एकल सेल मान के रूप में निर्यात करें। पूर्ण चरण‑दर‑चरण समाधान सीखें।
og_image_alt: Screenshot of an Excel sheet showing a JSON array stored in a single
  cell after using SmartMarkerOptions
og_title: C# में SmartMarkerOptions ArrayAsSingle को कॉन्फ़िगर करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Configure SmartMarkerOptions ArrayAsSingle in C# to export JSON arrays
    as a single cell value in an Excel workbook.
  headline: Configure SmartMarkerOptions ArrayAsSingle in C# for JSON arrays
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में JSON एरेज़ के लिए SmartMarkerOptions ArrayAsSingle को कॉन्फ़िगर करें
url: /hi/net/smart-markers-dynamic-data/configure-smartmarkeroptions-arrayassingle-in-c-for-json-arr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में JSON एरेज़ के लिए SmartMarkerOptions ArrayAsSingle को कॉन्फ़िगर करें

यदि आपको Aspose.Cells के साथ Excel फ़ाइलें जनरेट करते समय **SmartMarkerOptions ArrayAsSingle** को कॉन्फ़िगर करने की आवश्यकता है, तो यह गाइड आपको बिल्कुल बताता है कि इसे कैसे करें। आप देखेंगे कि कैसे एक JSON एरे को एक ही सेल में अपरिवर्तित रखा जा सकता है, बजाय इसके कि उसके तत्व कई पंक्तियों में बिखर जाएँ।

स्प्रेडशीट में JSON डेटा के साथ काम करना अक्सर फ्लैटेड व्यू और कॉम्पैक्ट प्रतिनिधित्व के बीच चयन करने का मतलब होता है। कई रिपोर्टिंग परिदृश्यों में—जैसे टैग की सूची या पहचानकर्ताओं का सेट संग्रहीत करना—आप चाहते हैं कि पूरा JSON स्ट्रिंग एक ही सेल में रहे। `SmartMarkerOptions` में **ArrayAsSingle** फ़्लैग इसे संभव बनाता है।

इस ट्यूटोरियल में आप करेंगे:

* एक `DataTable` बनाएँ जिसमें एक कॉलम में JSON एरे हो।
* Excel वर्कशीट में Smart Markers रखें।
* **SmartMarkerOptions ArrayAsSingle** को कॉन्फ़िगर करें ताकि JSON एरे को एकल सेल वैल्यू के रूप में माना जाए।
* मार्कर्स को प्रोसेस करें और वर्कबुक को सेव करें।
* आउटपुट की पुष्टि करें।

> **Prerequisites** – आपको Aspose.Cells for .NET लाइब्रेरी (v23.12 या बाद का) और एक .NET डेवलपमेंट एनवायरनमेंट (Visual Studio 2022 अनुशंसित) चाहिए। C# और DataTables का बुनियादी ज्ञान मान लिया गया है।

---

## Step 1: Prepare the data source with a JSON array

पहले, एक `DataTable` बनाएँ जो उस डेटा की नकल करता है जिसे आप किसी सर्विस या डेटाबेस से प्राप्त करेंगे। **Names** कॉलम में एक JSON‑एन्कोडेड स्ट्रिंग होती है जो नामों की एरे को दर्शाती है।

```csharp
using System;
using System.Data;
using Aspose.Cells;

DataTable dataTable = new DataTable();
dataTable.Columns.Add("Id", typeof(int));
dataTable.Columns.Add("Names", typeof(string));

// Store the JSON array as a plain string
dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");
```

*इस चरण का उद्देश्य क्या है?*  
Smart Markers .NET ऑब्जेक्ट्स से सीधे डेटा पढ़ते हैं। JSON एरे को स्ट्रिंग कॉलम में रखने से आप सटीक JSON सिंटैक्स को संरक्षित रखते हैं, जिसे बाद में बिना बदले एक सेल में लिखा जा सकता है।

## Step 2: Insert Smart Markers into a new workbook

एक नई वर्कबुक बनाएँ, पहली वर्कशीट चुनें, और Smart Markers लिखें जो पूरी टेबल और विशेष **Names** कॉलम को रेफ़र करते हैं।

```csharp
// Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Smart marker for the entire table (optional, shown for completeness)
worksheet.Cells["A1"].PutValue("&=dataTable");

// Smart marker that targets only the Names column
worksheet.Cells["A2"].PutValue("&=dataTable.Names");
```

मार्कर `&=dataTable.Names` Aspose.Cells को बताता है कि सेल को `dataTable` की प्रत्येक पंक्ति के **Names** कॉलम के मान से बदल दें। चूँकि हमारे पास केवल एक पंक्ति है, मार्कर एक बार प्रोसेस होगा।

## Step 3: **Configure SmartMarkerOptions ArrayAsSingle**

डिफ़ॉल्ट रूप से, Aspose.Cells एक एरे‑जैसी स्ट्रिंग को अलग‑अलग पंक्तियों में विस्तारित कर देता है। `ArrayAsSingle` को `true` सेट करने से यह व्यवहार ओवरराइड हो जाता है, और पूरी JSON स्ट्रिंग एक ही सेल में रहती है।

```csharp
SmartMarkerOptions smartMarkerOptions = new SmartMarkerOptions
{
    // Export the JSON array as a single cell value
    ArrayAsSingle = true
};
```

*`ArrayAsSingle` क्यों सक्षम करें?*  
जब `ArrayAsSingle` `false` होता है, तो इंजन `["Alice","Bob"]` को दो अलग मानों के रूप में समझता है और उन्हें क्रमिक पंक्तियों में लिखता है। इसे `true` करने से स्ट्रिंग को एक एटॉमिक वैल्यू माना जाता है, जो Excel में JSON फ़ॉर्मेट को संरक्षित रखने के लिए आवश्यक है।

## Step 4: Process the Smart Markers with the configured options

अब Smart Marker इंजन को चलाएँ, और वह विकल्प ऑब्जेक्ट पास करें जिसे आपने अभी कॉन्फ़िगर किया है।

```csharp
// Process smart markers using the custom options
workbook.ProcessSmartMarkers(smartMarkerOptions);
```

प्रोसेसिंग के दौरान, Aspose.Cells `dataTable` को पढ़ता है, मार्कर्स लागू करता है, और `ArrayAsSingle` फ़्लैग का सम्मान करता है, जिससे JSON एरे अपरिवर्तित रहता है।

## Step 5: Save the workbook and verify the result

अंत में, वर्कबुक को डिस्क पर लिखें। उत्पन्न फ़ाइल को Excel या किसी भी स्प्रेडशीट व्यूअर में खोलें और पुष्टि करें कि सेल **A2** में सटीक JSON स्ट्रिंग है।

```csharp
// Save the resulting workbook
string outputPath = @"C:\Temp\SmartMarkerJson.xlsx";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

### Expected output

| A   |
|-----|
| **["Alice","Bob"]** |

सेल **A2** JSON एरे को एकल टेक्स्ट वैल्यू के रूप में दिखाता है, बिल्कुल उसी तरह जैसा `DataTable` में संग्रहीत है। कोई अतिरिक्त पंक्तियाँ नहीं बनाई गईं।

## Common variations and edge‑case handling

| Situation | How to adapt |
|-----------|--------------|
| **Multiple rows with JSON arrays** | वही `ArrayAsSingle` सेटिंग काम करती है; प्रत्येक पंक्ति का JSON एरे अपने स्वयं के सेल में रहता है। |
| **Different JSON structures (objects, nested arrays)** | जब तक JSON एक स्ट्रिंग है, `ArrayAsSingle` इसे अपरिवर्तित रखेगा। जटिल ऑब्जेक्ट्स के लिए आपको कोट्स को एस्केप करना पड़ सकता है। |
| **Using a different data source (e.g., List\<T\>)** | `DataTable` को किसी भी एनेरेबल कलेक्शन से बदलें; मार्कर सिंटैक्स (`&=myList.Property`) वही रहता है। |
| **Exporting to CSV instead of XLSX** | `ArrayAsSingle` अभी भी लागू होता है, लेकिन याद रखें कि CSV सेल फ़ॉर्मेटिंग को संरक्षित नहीं करता; आपको JSON को कोट्स में रैप करना पड़ सकता है। |

**Pro tip:** हमेशा `ArrayAsSingle` को *ProcessSmartMarkers* को कॉल करने से पहले सेट करें। प्रोसेसिंग के बाद फ़्लैग बदलने से पहले से जेनरेट हुए सेल्स पर कोई असर नहीं पड़ेगा।

## Full, runnable example

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी‑पेस्ट करके एक कंसोल एप्लिकेशन में चला सकते हैं। इसमें सभी `using` निर्देश और स्पष्टता के लिए कमेंट्स शामिल हैं।

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Create the data source with a JSON array
            DataTable dataTable = new DataTable();
            dataTable.Columns.Add("Id", typeof(int));
            dataTable.Columns.Add("Names", typeof(string));
            dataTable.Rows.Add(1, "[\"Alice\",\"Bob\"]");

            // 2️⃣ Build a workbook and place smart markers
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Cells["A1"].PutValue("&=dataTable");          // whole table (optional)
            worksheet.Cells["A2"].PutValue("&=dataTable.Names");   // Names column

            // 3️⃣ Configure SmartMarkerOptions to treat arrays as single values
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                ArrayAsSingle = true
            };

            // 4️⃣ Process the markers with the custom options
            workbook.ProcessSmartMarkers(options);

            // 5️⃣ Save the file
            string path = @"C:\Temp\SmartMarkerJson.xlsx";
            workbook.Save(path);
            Console.WriteLine($"Workbook saved to {path}");
        }
    }
}
```

प्रोग्राम चलाएँ, `SmartMarkerJson.xlsx` खोलें, और आप देखेंगे कि JSON एरे सेल **A2** में संरक्षित है।

## Conclusion

अब आप जानते हैं कि C# में **SmartMarkerOptions ArrayAsSingle** को कैसे **कॉन्फ़िगर** किया जाता है ताकि Aspose.Cells स्मार्ट मार्कर्स का उपयोग करते समय JSON एरे को एकल सेल वैल्यू के रूप में रखा जा सके। चरण—`DataTable` तैयार करना, मार्कर्स डालना, `ArrayAsSingle` फ़्लैग सेट करना, प्रोसेस करना, और सेव करना—एक दोहराने योग्य पैटर्न बनाते हैं जिसे आप किसी भी ऐसे परिदृश्य में लागू कर सकते हैं जहाँ Excel में कॉम्पैक्ट JSON प्रतिनिधित्व आवश्यक हो।

आगे आप खोज सकते हैं:

* कलेक्शन्स पर लूपिंग के लिए **Aspose.Cells smart markers**।
* सेल फ़ॉर्मेटिंग को कस्टमाइज़ करके **nested JSON objects** का एक्सपोर्ट करना।
* अधिक समृद्ध रिपोर्ट्स के लिए स्मार्ट मार्कर्स के साथ **conditional formatting** को संयोजित करना।

विभिन्न डेटा स्ट्रक्चर्स के साथ प्रयोग करने और अपने निष्कर्ष साझा करने में संकोच न करें। Happy coding!

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [JSON से Excel वर्कबुक बनाएं – पूर्ण Aspose.Cells गाइड](/cells/english/net/data-loading-and-parsing/create-excel-workbook-from-json-complete-aspose-cells-guide/)
- [Excel वर्कबुक बनाएं और कॉन्फ़िगर करें Aspose Cells Net](/cells/hindi/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Excel वर्कबुक बनाएं और कॉन्फ़िगर करें Aspose Cells Net](/cells/german/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}