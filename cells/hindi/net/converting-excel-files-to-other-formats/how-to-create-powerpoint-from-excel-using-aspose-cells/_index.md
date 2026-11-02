---
category: general
date: 2026-09-18
description: Aspose.Cells के साथ Excel से PowerPoint बनाएं – पिवट टेबल्स कॉपी करें,
  रेंज निर्यात करें, और कुछ ही C# कोड लाइनों में PPTX के रूप में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create powerpoint from excel
- how to copy pivot table
- copy range between workbooks
- how to export excel to pptx
- save workbook as pptx
language: hi
lastmod: 2026-09-18
og_description: Excel से जल्दी PowerPoint बनाएं। सीखें कैसे पिवट टेबल्स को कॉपी करें,
  रेंजेज़ को एक्सपोर्ट करें, और Aspose.Cells का उपयोग करके वर्कबुक को PPTX के रूप
  में सहेजें।
og_image_alt: Screenshot of a PowerPoint slide generated from Excel data
og_title: Aspose.Cells के साथ Excel से PowerPoint बनाएं – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-09-18'
  description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  headline: How to create PowerPoint from Excel using Aspose.Cells
  type: TechArticle
- description: Create PowerPoint from Excel with Aspose.Cells – copy pivot tables,
    export ranges, and save as PPTX in a few lines of C# code.
  name: How to create PowerPoint from Excel using Aspose.Cells
  steps:
  - name: Load the source workbook and define the range
    text: You must load the workbook that holds the source data and the pivot table.
      Selecting a precise range ensures that only the needed cells are transferred,
      which keeps the resulting slide lightweight.
  - name: Prepare the destination workbook
    text: Aspose.Cells treats a PowerPoint slide as a workbook when you save it in
      PPTX format. Creating a fresh workbook gives you a clean canvas for the copied
      range.
  - name: Copy the range while preserving the pivot table
    text: The `CopyRange` method accepts a `PasteOptions` object. Setting `CopyPivotTables
      = true` tells Aspose.Cells to keep the pivot table structure intact, not just
      the rendered values.
  - name: Save the workbook as a PowerPoint file
    text: Finally, export the workbook to PPTX format. The `SaveFormat.Pptx` flag
      tells Aspose.Cells to write the worksheet as a PowerPoint slide.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel to PowerPoint
title: Aspose.Cells का उपयोग करके Excel से PowerPoint कैसे बनाएं
url: /hi/net/converting-excel-files-to-other-formats/how-to-create-powerpoint-from-excel-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel से PowerPoint बनाने का तरीका Aspose.Cells का उपयोग करके

यदि आपको Excel से PowerPoint बनाना है, तो यह गाइड आपको एक संक्षिप्त, अंत‑से‑अंत समाधान दिखाता है। आप देखेंगे कि कैसे एक पिवट टेबल को कॉपी किया जाए, चयनित रेंज को एक्सपोर्ट किया जाए, और परिणाम को कुछ ही C# लाइनों के साथ PPTX फ़ाइल के रूप में सहेजा जाए।

स्प्रेडशीट डेटा से सीधे स्लाइड डेक जेनरेट करने से वह मैन्युअल कॉपी‑पेस्ट चरण हट जाता है जो रिपोर्टिंग वर्कफ़्लो को धीमा करता है। ट्यूटोरियल में आपको प्रोजेक्ट सेटअप से लेकर अंतिम PPTX फ़ाइल तक सब कुछ बताया गया है, और यह नवीनतम Aspose.Cells for .NET के साथ काम करता है।

## आवश्यकताएँ

* **Aspose.Cells for .NET** (संस्करण 23.12 या नया)। इसे NuGet के माध्यम से इंस्टॉल करें: `Install-Package Aspose.Cells`।
* **.NET 6+** विकास वातावरण (Visual Studio 2022 या VS Code काम करता है)।
* एक Excel वर्कबुक (`Source.xlsx`) जिसमें वह डेटा और पिवट टेबल है जिसे आप पुनः उपयोग करना चाहते हैं।
* आउटपुट फ़ोल्डर में लिखने की अनुमति।

कोई अतिरिक्त थर्ड‑पार्टी लाइब्रेरी आवश्यक नहीं है।

## Excel से PowerPoint बनाना – चरण‑दर‑चरण

यह प्रक्रिया चार तार्किक चरणों में विभाजित है जो बाद में दिखाए गए कोड उदाहरण से सीधे मेल खाते हैं।

### चरण 1: स्रोत वर्कबुक लोड करें और रेंज निर्धारित करें

आपको वह वर्कबुक लोड करनी होगी जिसमें स्रोत डेटा और पिवट टेबल है। सटीक रेंज चुनने से केवल आवश्यक सेल्स ट्रांसफ़र होते हैं, जिससे परिणामी स्लाइड हल्की रहती है।

```csharp
using Aspose.Cells;
using System;

// Load the source workbook
Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// Select the first worksheet (index 0)
Worksheet sourceSheet = sourceWorkbook.Worksheets[0];

// Define the range that contains the pivot table and surrounding data
Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");
```

**यह क्यों महत्वपूर्ण है:**  
`CreateRange` एक `Range` ऑब्जेक्ट बनाता है जिसे एक साथ कॉपी किया जा सकता है। रेंज को `A1:G20` तक सीमित करके आप अनावश्यक सेल्स को लाने से बचते हैं, जो अन्यथा PowerPoint फ़ाइल को बड़ा बना सकते हैं।

### चरण 2: गंतव्य वर्कबुक तैयार करें

Aspose.Cells PPTX फ़ॉर्मेट में सहेजते समय PowerPoint स्लाइड को वर्कबुक के रूप में मानता है। एक नई वर्कबुक बनाने से आपको कॉपी की गई रेंज के लिए एक साफ़ कैनवास मिलता है।

```csharp
// Create a new empty workbook that will become the PowerPoint slide
Workbook destinationWorkbook = new Workbook();

// Use the first worksheet of the new workbook
Worksheet destinationSheet = destinationWorkbook.Worksheets[0];
```

**टिप:** यदि आपको कई स्लाइड्स चाहिए, तो आप अतिरिक्त वर्कशीट्स जोड़ सकते हैं और बाद में प्रत्येक को अलग PPTX फ़ाइल के रूप में सहेज सकते हैं।

### चरण 3: रेंज को कॉपी करें जबकि पिवट टेबल को संरक्षित रखें

`CopyRange` मेथड एक `PasteOptions` ऑब्जेक्ट स्वीकार करता है। `CopyPivotTables = true` सेट करने से Aspose.Cells को पिवट टेबल की संरचना को अपरिवर्तित रखने को कहा जाता है, न कि केवल रेंडर किए गए मानों को।

```csharp
// Copy the defined range, preserving the pivot table definition
destinationSheet.Cells.CopyRange(
    sourceRange,
    new PasteOptions { CopyPivotTables = true });
```

**यह कैसे काम करता है:**  
जब `CopyPivotTables` true होता है, तो गंतव्य शीट को स्रोत डेटा और पिवट कैश दोनों मिलते हैं। इसका मतलब है कि पिवट टेबल पूरी तरह कार्यशील रहती है और यदि स्रोत डेटा बदलता है तो बाद में रिफ्रेश की जा सकती है।

### चरण 4: वर्कबुक को PowerPoint फ़ाइल के रूप में सहेजें

अंत में, वर्कबुक को PPTX फ़ॉर्मेट में एक्सपोर्ट करें। `SaveFormat.Pptx` फ़्लैग Aspose.Cells को बताता है कि वर्कशीट को PowerPoint स्लाइड के रूप में लिखे।

```csharp
// Save the destination workbook as a PowerPoint presentation
destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);
```

**परिणाम:**  
`CopyWithPivot.pptx` Microsoft PowerPoint (या किसी भी संगत व्यूअर) में खुलता है, जिसमें एक सिंगल स्लाइड पर कॉपी की गई रेंज दिखती है, जिसमें एक लाइव पिवट टेबल भी शामिल है जिसे PowerPoint में इंटरैक्ट किया जा सकता है।

## पूर्ण चलाने योग्य उदाहरण

नीचे पूरा प्रोग्राम दिया गया है जिसे आप नई कंसोल प्रोजेक्ट में पेस्ट करके तुरंत चला सकते हैं।

```csharp
using Aspose.Cells;
using System;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook and select the range containing the pivot table
            Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");
            Worksheet sourceSheet = sourceWorkbook.Worksheets[0];
            Range sourceRange = sourceSheet.Cells.CreateRange("A1:G20");

            // 2️⃣ Create a fresh workbook that will become the PowerPoint slide
            Workbook destinationWorkbook = new Workbook();
            Worksheet destinationSheet = destinationWorkbook.Worksheets[0];

            // 3️⃣ Copy the range, preserving the pivot table definition
            destinationSheet.Cells.CopyRange(
                sourceRange,
                new PasteOptions { CopyPivotTables = true });

            // 4️⃣ Export the workbook as a PPTX file
            destinationWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.pptx", SaveFormat.Pptx);

            Console.WriteLine("PowerPoint file created successfully.");
        }
    }
}
```

**अपेक्षित आउटपुट:**  
प्रोग्राम चलाने पर “PowerPoint file created successfully.” प्रिंट होता है और `CopyWithPivot.pptx` नाम की फ़ाइल बनती है। PowerPoint में फ़ाइल खोलने पर एक सिंगल स्लाइड दिखती है जहाँ कॉपी किया गया Excel रेंज स्रोत वर्कशीट जैसा ही दिखता है, साथ ही एक सक्रिय पिवट टेबल भी होती है जिसे PowerPoint के भीतर रिफ्रेश किया जा सकता है।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | क्या बदलें |
|-----------|----------------|
| **Multiple pivot tables** | प्रत्येक टेबल के लिए अलग `Range` ऑब्जेक्ट परिभाषित करें और प्रत्येक के लिए `CopyRange` कॉल करें, या यदि वे एक ही डेटा स्रोत साझा करते हैं तो पूरी शीट कॉपी करें। |
| **Large data sets** | रेंज बढ़ाएँ (उदा., `"A1:Z5000"`). PPTX आकार कम करने के लिए `PasteOptions.CompressData = true` सक्षम करने पर विचार करें। |
| **Different slide layouts** | PPTX के रूप में सहेजने के बाद, फ़ाइल को PowerPoint में खोलें और कस्टम लेआउट या थीम लागू करें; डेटा संपादन योग्य रहता है। |
| **Saving to a stream** | जब आपको वेब API के माध्यम से PPTX लौटाना हो, तो `destinationWorkbook.Save(stream, SaveFormat.Pptx)` उपयोग करें। |
| **Preserving cell formatting** | फ़ॉन्ट, रंग और बॉर्डर रखने के लिए `PasteOptions.PasteType = PasteType.All` सेट करें। |

**प्रो टिप:**  
सेव करने से पहले हमेशा सुनिश्चित करें कि गंतव्य फ़ोल्डर मौजूद है। यदि फ़ोल्डर नहीं है, तो `Save` `DirectoryNotFoundException` फेंकता है।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells का उपयोग करके Excel से PowerPoint कैसे बनाएं, पिवट टेबल को कॉपी करें, और परिणाम को PPTX फ़ाइल के रूप में एक्सपोर्ट करें। चरण—स्रोत वर्कबुक लोड करना, रेंज निर्धारित करना, `CopyPivotTables` के साथ कॉपी करना, और PPTX के रूप में सहेजना—पूरे वर्कफ़्लो को विश्वसनीय, प्रोडक्शन‑रेडी तरीके से कवर करते हैं।

अगला, कई वर्कशीट्स के लिए **Excel को PPTX में एक्सपोर्ट करने** का पता लगाएँ, या **वर्कबुक्स के बीच रेंज कॉपी करने** के बारे में सीखें जब आपको स्लाइड डेक जेनरेट करने से पहले कई स्रोतों से डेटा मर्ज करना हो। दोनों विषय एक ही API सतह पर आधारित हैं और जटिल रिपोर्टिंग पाइपलाइन को ऑटोमेट करने के लिए संयोजित किए जा सकते हैं।

कोडिंग का आनंद लें, और अपनी स्प्रेडशीट्स को शानदार प्रस्तुतियों में बदलने का मज़ा उठाएँ!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करती हैं।

- [C# में पिवट टेबल कॉपी कैसे करें – Excel को PPTX में बदलें, रेंज कॉपी करें और टेक्स्टबॉक्स बनाएं](/cells/english/net/pivot-tables/how-to-copy-pivot-table-in-c-convert-excel-to-pptx-copy-rang/)
- [नई वर्कबुक बनाएं – पिवट टेबल वाली वर्कशीट को कैसे कॉपी करें](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [Aspose.Cells for .NET के साथ Excel फ़ाइलें कैसे बनाएं और सहेजें: एक पूर्ण गाइड](/cells/english/net/workbook-operations/create-save-excel-file-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}