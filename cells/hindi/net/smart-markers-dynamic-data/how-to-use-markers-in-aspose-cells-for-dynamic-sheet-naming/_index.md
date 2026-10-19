---
category: general
date: 2026-05-23
description: Aspose.Cells के साथ मार्कर्स का उपयोग करके डायनेमिक शीट नामकरण एक्सेल
  ऑटोमेशन कैसे प्राप्त करें। स्मार्ट मार्कर्स, JSON डेटा बाइंडिंग, और शीट निर्माण
  को मिनटों में सीखें।
draft: false
keywords:
- how to use markers
- dynamic sheet naming excel
- aspose.cells smart markers
language: hi
og_description: Aspose.Cells में मार्कर्स का उपयोग करके डायनामिक शीट नामकरण के साथ
  Excel फ़ाइलें बनाने का तरीका। पूर्ण चरण‑दर‑चरण गाइड जिसमें पूरा C# उदाहरण शामिल
  है।
og_title: मार्कर्स का उपयोग कैसे करें – Aspose.Cells के साथ एक्सेल में डायनेमिक शीट
  नामकरण
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  headline: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  type: TechArticle
- description: How to use markers with Aspose.Cells to achieve dynamic sheet naming
    Excel automation. Learn smart markers, JSON data binding, and sheet creation in
    minutes.
  name: How to Use Markers in Aspose.Cells for Dynamic Sheet Naming in Excel
  steps:
  - name: What Happens Under the Hood?
    text: 1. The processor reads the `Orders` array. 2. For each order it creates
      a **master sheet** (using `${Orders.MasterSheetName}`) and a **detail sheet**
      (using the `DetailSheetNewName` pattern). 3. Cell values are replaced with the
      corresponding JSON fields, so the master sheet’s first cell ends up con
  - name: What if I need more than two levels of hierarchy?
    text: You can nest markers inside the newly created detail sheets. Just place
      additional `${...}` tags in the template sheet before processing. The processor
      will cascade through each level automatically.
  - name: Can I use a DataTable instead of JSON?
    text: Absolutely. `SmartMarkerProcessor` has overloads for `DataSet`, `DataTable`,
      and even custom objects. The only change is the call to `ApplyJson` – you’d
      use `ApplyDataSet(myDataSet)` instead.
  - name: How do I control the order of sheet creation?
    text: The order follows the sequence of the source collection. If you need a custom
      sort, simply sort the JSON array (or DataTable) before passing it to the processor.
  - name: Is there a way to hide the template sheet after processing?
    text: Yes. Set `sm.Options.RemoveTemplateSheets = true;` before calling `ApplyJson`.
      The original sheet (index 0) will be removed from the final workbook.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells में मार्कर्स का उपयोग करके एक्सेल में डायनेमिक शीट नामकरण कैसे
  करें
url: /hi/net/smart-markers-dynamic-data/how-to-use-markers-in-aspose-cells-for-dynamic-sheet-naming/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells में मार्कर्स का उपयोग करके Excel में डायनेमिक शीट नामकरण कैसे करें

क्या आपने कभी सोचा है **मार्कर्स का उपयोग कैसे करें** एक स्थिर Excel टेम्पलेट को पूरी‑फ्लेज़्ड मास्टर‑डिटेल वर्कबुक में बदलने के लिए? आप अकेले नहीं हैं। कई डेवलपर्स को *डायनेमिक शीट नामकरण excel* क्षमताओं की आवश्यकता होने पर रुकावट आती है, विशेषकर जब शीट नामों को JSON या डेटाबेस से आने वाले डेटा मानों को दर्शाना हो।  

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य C# उदाहरण के माध्यम से चलेंगे जो दिखाता है **मार्कर्स का उपयोग कैसे करें** **Aspose.Cells** स्मार्ट मार्कर्स के साथ, JSON डेटा बाइंड करें, और प्रोसेसर को ऐसे शीट बनाने दें जिनके नाम रन‑टाइम पर बदलते हैं। कोई फालतू नहीं, बस वही कोड जो आप Visual Studio में पेस्ट करके तुरंत परिणाम देख सकते हैं।

## आप क्या सीखेंगे

- **स्मार्ट मार्कर्स** की अवधारणा और क्यों वे मास्टर‑डिटेल परिदृश्यों के लिए परफेक्ट हैं।  
- वर्कबुक में मार्कर टैग एम्बेड करना जो बाद में वास्तविक शीट नामों से बदलेंगे।  
- `DetailSheetNewName` विकल्प का उपयोग करके **डायनेमिक शीट नामकरण excel** सेट करना।  
- JSON डेटा के खिलाफ `SmartMarkerProcessor` चलाना ताकि कई शीटें ऑटोमैटिकली जेनरेट हो सकें।  
- आउटपुट की वैरिफिकेशन और सामान्य पिटफ़ॉल्स से बचने के लिए कुछ उपयोगी टिप्स।

> **Prerequisites** – आपको एक हालिया .NET रनटाइम (≥ .NET 6 ठीक है), Aspose.Cells for .NET लाइब्रेरी (आप Aspose से फ्री ट्रायल ले सकते हैं), और C# की बुनियादी जानकारी चाहिए।  

---

![Aspose.Cells में मार्कर्स के उपयोग का उदाहरण](example.png "Aspose.Cells में मार्कर्स के उपयोग का उदाहरण")

## मार्कर्स का उपयोग करके डायनेमिक शीट नामकरण कैसे बनाएं (Step 1)

सबसे पहले हमें एक खाली वर्कबुक चाहिए जो हमारे टेम्पलेट के रूप में काम करेगा। वास्तविक प्रोजेक्ट में आप संभवतः मौजूदा `.xlsx` फ़ाइल से शुरू करेंगे जिसमें लेआउट, फॉर्मेटिंग और प्लेसहोल्डर सेल्स पहले से मौजूद हों। स्पष्टता के लिए हम सब कुछ प्रोग्रामैटिकली बनाएँगे।

```csharp
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

// Step 1: Create a new workbook and get the first worksheet
Workbook wb = new Workbook();                // fresh workbook, no sheets yet
Worksheet ws = wb.Worksheets[0];             // default first sheet
```

*Why this matters*: `Worksheet` ऑब्जेक्ट वह जगह है जहाँ हम अपने **smart marker** टैग्स डालेंगे। टैग्स को छोटे प्लेसहोल्डर की तरह समझें जो प्रोसेसर बाद में JSON से वास्तविक मानों से बदल देगा।  

## स्मार्ट मार्कर टैग्स डालें (Step 2)

अब हम मार्कर टैग्स को सीधे सेल्स में रखेंगे। `${...}` सिंटैक्स Aspose.Cells को बताता है “यह एक मार्कर है”। हमारे उदाहरण में हमें दो मार्कर्स चाहिए: एक मास्टर शीट नाम के लिए और दूसरा डिटेल शीट नाम के लिए।

```csharp
// Step 2: Insert Smart Marker tags that will be replaced with sheet names
ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");   // master sheet placeholder
ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");   // detail sheet placeholder
```

> **Pro tip** – मार्कर नाम छोटे और अर्थपूर्ण रखें; ये वही कीज़ बनेंगे जिन्हें आप अपने JSON पेलोड में उपयोग करेंगे।

## JSON डेटा तैयार करें (Step 3)

प्रोसेसर किसी भी डेटा सोर्स के साथ काम करता है जिसे JSON, `DataSet`, या यहाँ तक कि साधारण ऑब्जेक्ट के रूप में प्रस्तुत किया जा सके। यहाँ एक न्यूनतम JSON स्ट्रिंग है जिसमें मास्टर‑डिटेल कलेक्शन है। ध्यान दें कि प्रत्येक ऑर्डर में `MasterSheetName` और `DetailSheetName` दोनों होते हैं।

```csharp
// Step 3: Prepare the JSON data that contains the master‑detail information
string jsonOrders = @"{
    ""Orders"": [
        {
            ""OrderId"": 1,
            ""MasterSheetName"": ""Master_1"",
            ""DetailSheetName"": ""Detail_1""
        },
        {
            ""OrderId"": 2,
            ""MasterSheetName"": ""Master_2"",
            ""DetailSheetName"": ""Detail_2""
        }
    ]
}";
```

*Why JSON?* यह हल्का, मानव‑पठनीय, और वेब APIs के साथ बेहतरीन काम करता है। आप इसे आसानी से एक SQL क्वेरी से निकाल कर `Newtonsoft.Json` के साथ सीरियलाइज़ भी कर सकते हैं।

## SmartMarkerProcessor को इनिशियलाइज़ करें (Step 4)

`SmartMarkerProcessor` वह इंजन है जो वर्कबुक को स्कैन करता है, मार्कर्स खोजता है, और डेटा बाइंडिंग करता है। इसे इंस्टैंशिएट करना एक‑लाइनर है।

```csharp
// Step 4: Initialise the SmartMarkerProcessor with the workbook
SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);
```

## डायनेमिक शीट नामकरण परिभाषित करें (Step 5)

यहीं पर **डायनेमिक शीट नामकरण excel** असली चमक दिखाता है। `DetailSheetNewName` सेट करके हम प्रोसेसर को प्रत्येक ऑर्डर के लिए एक नया डिटेल शीट बनाने और उसे `OrderId` के आधार पर नाम देने को कहते हैं। `${OrderId}` प्लेसहोल्डर प्रोसेसिंग के दौरान वर्तमान रिकॉर्ड से हल हो जाता है।

```csharp
// Step 5: Define how new detail sheets should be named during processing
sm.Options.DetailSheetNewName = "Detail_${OrderId}";
```

> **Watch out** – यदि आप `${}` सिंटैक्स को भूल जाते हैं, तो शीट का नाम वास्तव में “Detail_${OrderId}” रहेगा, न कि “Detail_1”, “Detail_2” आदि।

## JSON लागू करें और शीट्स जेनरेट करें (Step 6)

अब हम प्रोसेसर को भारी काम करने देते हैं। यह JSON पढ़ेगा, मार्कर्स को बदल देगा, और आवश्यकतानुसार नई वर्कशीट्स बनाएगा।

```csharp
// Step 6: Apply the JSON data to populate the smart markers and generate sheets
sm.ApplyJson(jsonOrders);
```

### पर्दे के पीछे क्या हो रहा है?

1. प्रोसेसर `Orders` एरे को पढ़ता है।  
2. प्रत्येक ऑर्डर के लिए वह **मास्टर शीट** (`${Orders.MasterSheetName}`) और **डिटेल शीट** (`DetailSheetNewName` पैटर्न) बनाता है।  
3. सेल वैल्यूज़ को संबंधित JSON फ़ील्ड्स से बदल दिया जाता है, इसलिए मास्टर शीट की पहली सेल में “Master_1”, “Master_2” आदि आ जाता है।  

## परिणाम को सेव और वैरिफ़ाई करें (वैकल्पिक)

अंत में, वर्कबुक को डिस्क पर लिखें। फ़ाइल को Excel में खोलें और आपको दो मास्टर शीट्स (`Master_1`, `Master_2`) और दो डायनेमिकली नेम्ड डिटेल शीट्स (`Detail_1`, `Detail_2`) दिखेंगे।  

```csharp
// (Optional) Save the result to verify the output
wb.Save("output.xlsx");
```

**Expected output** – `output.xlsx` खोलने के बाद आप देखेंगे:

- शीट **Master_1** जिसमें सेल A1 = “Master_1”。  
- शीट **Detail_1** जिसमें सेल A1 = “Detail_1”。  
- शीट **Master_2** जिसमें सेल A1 = “Master_2”。  
- शीट **Detail_2** जिसमें सेल A1 = “Detail_2”。  

यही है **मार्कर्स का उपयोग करके** **डायनेमिक शीट नामकरण excel** को **Aspose.Cells स्मार्ट मार्कर्स** के साथ हासिल करने का पूरा चक्र।

---

## सामान्य प्रश्न और एज केस

### यदि मुझे दो से अधिक लेवल की हाइरार्की चाहिए तो क्या करें?

आप नई बनाई गई डिटेल शीट्स के अंदर भी मार्कर्स नेस्ट कर सकते हैं। प्रोसेसिंग से पहले टेम्पलेट शीट में अतिरिक्त `${...}` टैग्स रखें। प्रोसेसर प्रत्येक लेवल को ऑटोमैटिकली हैंडल करेगा।

### क्या मैं JSON की बजाय DataTable उपयोग कर सकता हूँ?

बिल्कुल। `SmartMarkerProcessor` के पास `DataSet`, `DataTable`, और कस्टम ऑब्जेक्ट्स के लिए ओवरलोड्स हैं। केवल कॉल बदलनी होगी: `ApplyJson` की जगह `ApplyDataSet(myDataSet)` उपयोग करें।

### शीट निर्माण के क्रम को कैसे नियंत्रित करूँ?

क्रम स्रोत कलेक्शन की सीक्वेंस पर निर्भर करता है। यदि आपको कस्टम सॉर्ट चाहिए, तो प्रोसेसर को पास करने से पहले JSON एरे (या DataTable) को सॉर्ट कर दें।

### प्रोसेसिंग के बाद टेम्पलेट शीट को छुपाने का कोई तरीका है?

हां। `sm.Options.RemoveTemplateSheets = true;` को `ApplyJson` कॉल से पहले सेट करें। मूल शीट (इंडेक्स 0) अंतिम वर्कबुक से हटा दी जाएगी।

---

## पूर्ण कार्यशील उदाहरण (सभी स्टेप्स एक साथ)

नीचे पूरा प्रोग्राम है जिसे आप एक नए C# कंसोल प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं। सुनिश्चित करें कि आपने `Aspose.Cells` NuGet पैकेज रेफ़रेंस किया हुआ है।

```csharp
using System;
using Aspose.Cells;
using Aspose.Cells.SmartMarker;

namespace DynamicSheetNamingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook wb = new Workbook();
            Worksheet ws = wb.Worksheets[0];

            // Step 2: Insert Smart Marker tags that will be replaced with sheet names
            ws.Cells[0, 0].PutValue("${Orders.MasterSheetName}");
            ws.Cells[1, 0].PutValue("${Orders.DetailSheetName}");

            // Step 3: Prepare the JSON data that contains the master‑detail information
            string jsonOrders = @"{
                ""Orders"": [
                    {
                        ""OrderId"": 1,
                        ""MasterSheetName"": ""Master_1"",
                        ""DetailSheetName"": ""Detail_1""
                    },
                    {
                        ""OrderId"": 2,
                        ""MasterSheetName"": ""Master_2"",
                        ""DetailSheetName"": ""Detail_2""
                    }
                ]
            }";

            // Step 4: Initialise the SmartMarkerProcessor with the workbook
            SmartMarkerProcessor sm = new SmartMarkerProcessor(wb);

            // Step 5: Define how new detail sheets should be named during processing
            sm.Options.DetailSheetNewName = "Detail_${OrderId}";

            // (Optional) Remove the original template sheet after processing
            // sm.Options.RemoveTemplateSheets = true;

            // Step 6: Apply the JSON data to populate the smart markers and generate sheets
            sm.ApplyJson(jsonOrders);

            // Save the result
            wb.Save("output.xlsx");
            Console.WriteLine("Workbook generated successfully. Check output.xlsx.");
        }
    }
}
```

प्रोग्राम चलाएँ, `output.xlsx` खोलें, और आप वही डायनेमिक शीट्स देखेंगे जैसा ऊपर बताया गया है।

---

## समापन

हमने अभी-अभी **मार्कर्स का उपयोग करके** Aspose.Cells में एक साधारण वर्कबुक को **डायनेमिक शीट नामकरण excel** के साथ मास्टर‑डिटेल समाधान में बदलना कवर किया। मुख्य बिंदु हैं:

1. जहाँ डेटा चाहिए वहाँ `${...}` स्मार्ट मार्कर्स रखें।  
2. `SmartMarkerProcessor` को JSON (या कोई भी सपोर्टेड डेटा सोर्स) फ़ीड करें।  
3. `DetailSheetNewName` का उपयोग करके प्रोसेसर को नई शीट्स को रन‑टाइम पर नाम देने दें।  

अब आप अधिक उन्नत परिदृश्यों की खोज कर सकते हैं—टेबल्स जोड़ना, सेल्स को स्टाइल करना, या चार्ट एम्बेड करना—सब कुछ डेटा‑ड्रिवेन।

## संबंधित ट्यूटोरियल

- [डायनेमिक Excel रिपोर्टिंग के लिए C# में Aspose.Cells स्मार्ट मार्कर्स को कैसे लागू करें](/cells/english/net/automation-batch-processing/implement-aspose-cells-smart-markers-with-csharp/)
- [Aspose.Cells .NET स्मार्ट मार्कर्स का उपयोग करके डायनेमिक Excel रिपोर्ट बनाएं](/cells/english/net/templates-reporting/generate-excel-reports-aspose-cells-net-smart-markers/)
- [Aspose.Cells .NET में महारत: डायनेमिक Excel रिपोर्टों के लिए स्मार्ट मार्कर्स और कस्टम लेबल लागू करें](/cells/english/net/advanced-features/aspose-cells-net-smart-markers-custom-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}