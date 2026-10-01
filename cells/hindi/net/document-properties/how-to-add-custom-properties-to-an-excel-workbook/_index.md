---
category: general
date: 2026-10-01
description: Aspose.Cells का उपयोग करके Excel वर्कबुक में कस्टम प्रॉपर्टीज़ कैसे जोड़ें,
  सीखें। यह गाइड यह भी दिखाता है कि प्रोजेक्ट आईडी कैसे जोड़ें और कस्टम प्रॉपर्टीज़
  को कैसे पढ़ें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- add custom properties
- how to add custom
- excel custom properties
- add project id
- read custom properties
language: hi
lastmod: 2026-10-01
og_description: Aspose.Cells के साथ Excel वर्कबुक में कस्टम प्रॉपर्टीज़ जोड़ें। इस
  पूर्ण ट्यूटोरियल का पालन करके प्रोजेक्ट आईडी जोड़ें, रिव्यूअर जानकारी सेट करें,
  और प्रोग्रामेटिकली कस्टम प्रॉपर्टीज़ पढ़ें।
og_image_alt: Screenshot of an Excel worksheet displaying custom properties added
  via Aspose.Cells
og_title: Excel वर्कबुक में कस्टम प्रॉपर्टीज़ जोड़ें – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  headline: How to add custom properties to an Excel workbook
  type: TechArticle
- description: Learn how to add custom properties to an Excel workbook using Aspose.Cells.
    This guide also shows how to add project ID and read custom properties.
  name: How to add custom properties to an Excel workbook
  steps:
  - name: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
    text: Open the saved `DataWithProps.xlsb` file in Microsoft Excel.
  - name: Go to **File → Info → Properties → Advanced Properties**.
    text: Go to **File → Info → Properties → Advanced Properties**.
  - name: Select the **Custom** tab.
    text: Select the **Custom** tab.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Excel वर्कबुक में कस्टम प्रॉपर्टीज़ कैसे जोड़ें
url: /hi/net/document-properties/how-to-add-custom-properties-to-an-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel वर्कबुक में कस्टम प्रॉपर्टीज़ कैसे जोड़ें

यदि आपको Excel वर्कबुक में **कस्टम प्रॉपर्टीज़** जोड़नी हैं, तो यह गाइड Aspose.Cells for .NET के साथ इसे कैसे किया जाए, बिल्कुल दिखाता है। आप यह भी सीखेंगे कि प्रोजेक्ट आईडी कैसे जोड़ें, समीक्षक का नाम सेट करें, और बाद में फ़ाइल से **कस्टम प्रॉपर्टीज़ पढ़ें**।

कस्टम मेटाडेटा के साथ काम करने से आप व्यवसाय‑विशिष्ट जानकारी को सीधे स्प्रेडशीट में एम्बेड कर सकते हैं, जिससे स्वामित्व, संस्करण, या किसी भी अन्य संदर्भ को अलग डेटाबेस बनाए बिना ट्रैक करना आसान हो जाता है। नीचे दिए गए चरण पूरे एंड‑टू‑एंड वर्कफ़्लो को कवर करते हैं, वर्कबुक बनाने से लेकर नई प्रॉपर्टीज़ को स्थायी करने तक।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 या बाद का संस्करण स्थापित हो  
* एक वैध Aspose.Cells for .NET लाइसेंस (या फ्री ट्रायल)  
* Visual Studio 2022 (या कोई भी C# IDE)  

`Aspose.Cells` के अलावा कोई अतिरिक्त NuGet पैकेज आवश्यक नहीं है।

## Step 1: Set up the project and import namespaces

एक नया कंसोल एप्लिकेशन बनाएं और Aspose.Cells रेफ़रेंस जोड़ें:

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // The rest of the code lives here
        }
    }
}
```

`Aspose.Cells` नेमस्पेस में `Workbook`, `Worksheet`, और `CustomPropertyCollection` क्लासेज़ हैं जिन्हें हम उपयोग करेंगे।

## Step 2: Load an existing workbook (or create a new one)

आप मौजूदा `.xlsb` फ़ाइल से शुरू कर सकते हैं या नई वर्कबुक जेनरेट कर सकते हैं। नीचे का उदाहरण `YOUR_DIRECTORY` फ़ोल्डर में स्थित **Data.xlsb** नाम की फ़ाइल को लोड करता है।

```csharp
// Load the existing workbook
var workbookPath = @"YOUR_DIRECTORY\Data.xlsb";
var workbook = new Workbook(workbookPath);
```

यदि फ़ाइल मौजूद नहीं है, तो कोड को `new Workbook();` से बदलें ताकि एक खाली वर्कबुक बन सके।

## Step 3: Add custom properties to the first worksheet

मुख्य ऑपरेशन **कस्टम प्रॉपर्टीज़** को एक वर्कशीट में जोड़ना है। Aspose.Cells कस्टम प्रॉपर्टीज़ को एक कलेक्शन में स्टोर करता है जो डिक्शनरी जैसा व्यवहार करता है।

```csharp
// Get the first worksheet (index 0)
var worksheet = workbook.Worksheets[0];

// Add a numeric ProjectId property
worksheet.CustomProperties.Add("ProjectId", 12345);

// Add a string Reviewer property
worksheet.CustomProperties.Add("Reviewer", "John Doe");

// Optional: add a DateTime property for the creation timestamp
worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);
```

हम `CustomProperties.Add` का उपयोग `CustomProperties["Name"] = value` की बजाय इसलिए करते हैं क्योंकि `Add` मेथड एंट्री को बनाता है यदि वह मौजूद नहीं है और सही डेटा टाइप को स्टोर करने की गारंटी देता है। यह तरीका अनजाने टाइप मिसमैच को रोकता है, जो बाद में वैल्यू पढ़ते समय रन‑टाइम एरर का कारण बन सकता है।

## Step 4: Save the workbook with the new properties

मेटाडेटा इन्जेक्ट करने के बाद, बदलावों को नई फ़ाइल में सेव करें ताकि मूल फ़ाइल अपरिवर्तित रहे।

```csharp
// Save the workbook with the custom properties
var outputPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

इस चरण पर Excel फ़ाइल में वह कस्टम मेटाडेटा मौजूद है जो आपने परिभाषित किया था। आप अगली सेक्शन में बताए गए चरणों से प्रॉपर्टीज़ की पुष्टि कर सकते हैं।

## Step 5: Read custom properties from a workbook

**excel custom properties** पढ़ना वही कलेक्शन पैटर्न फॉलो करता है। यह स्निपेट दिखाता है कि हमने अभी जो वैल्यूज़ स्टोर की थीं, उन्हें कैसे प्राप्त करें।

```csharp
// Load the workbook that contains custom properties
var loadedWorkbook = new Workbook(outputPath);
var loadedWorksheet = loadedWorkbook.Worksheets[0];
var props = loadedWorksheet.CustomProperties;

// Retrieve each property safely
int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

Console.WriteLine($"ProjectId: {projectId}");
Console.WriteLine($"Reviewer: {reviewer}");
Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
```

`CustomPropertyCollection` इंडेक्सर एक `CustomProperty` ऑब्जेक्ट रिटर्न करता है; उसकी `Value` प्रॉपर्टी तक पहुँचने से आपको मूल टाइप में स्टोर किया गया डेटा मिलता है। `null` की जाँच करके कास्ट करने से `NullReferenceException` से बचा जा सकता है यदि कोई प्रॉपर्टी मौजूद नहीं है।

### Expected console output

```
ProjectId: 12345
Reviewer: John Doe
CreatedOn (UTC): 2026-10-01 12:34:56Z
```

टाइमस्टैम्प वह सटीक क्षण दर्शाएगा जब आपने चरण 3 में `Add` कॉल किया था।

## Pro tip: Updating an existing custom property

यदि आपको बाद में **how to add custom** जानकारी जोड़नी है (उदाहरण के लिए, समीक्षक बदलना), तो `CustomPropertyCollection` सेट्टर का उपयोग करें:

```csharp
// Change the reviewer name
if (props["Reviewer"] != null)
{
    props["Reviewer"].Value = "Jane Smith";
}
else
{
    // Property does not exist; add it
    props.Add("Reviewer", "Jane Smith");
}
```

यह पैटर्न सुनिश्चित करता है कि प्रॉपर्टी या तो अपडेट हो या बनाई जाए, जो इटरेटिव वर्कफ़्लो जैसे ऑटोमेटेड रिपोर्ट जेनरेशन में उपयोगी है।

## Step 6: Verify the properties inside Excel (optional)

आप कस्टम प्रॉपर्टीज़ को सीधे Excel में भी देख सकते हैं:

1. सेव की गई `DataWithProps.xlsb` फ़ाइल को Microsoft Excel में खोलें।  
2. **File → Info → Properties → Advanced Properties** पर जाएँ।  
3. **Custom** टैब चुनें।  

आपको `ProjectId`, `Reviewer`, और `CreatedOn` एंट्रीज़ उनके संबंधित वैल्यूज़ के साथ सूचीबद्ध दिखेंगी।

## Full working example

नीचे पूरा, स्व-निहित प्रोग्राम है जो सभी पिछले स्निपेट्स को मिलाता है। इसे `Program.cs` में कॉपी करें और चलाएँ; कंसोल में प्राप्त वैल्यूज़ दिखेंगे।

```csharp
using System;
using Aspose.Cells;

namespace ExcelCustomPropertiesDemo
{
    class Program
    {
        static void Main()
        {
            // Paths (adjust to your environment)
            var sourcePath = @"YOUR_DIRECTORY\Data.xlsb";
            var resultPath = @"YOUR_DIRECTORY\DataWithProps.xlsb";

            // Load or create workbook
            var workbook = new Workbook(sourcePath);
            var worksheet = workbook.Worksheets[0];

            // Add custom properties
            worksheet.CustomProperties.Add("ProjectId", 12345);
            worksheet.CustomProperties.Add("Reviewer", "John Doe");
            worksheet.CustomProperties.Add("CreatedOn", DateTime.UtcNow);

            // Save the workbook
            workbook.Save(resultPath);
            Console.WriteLine($"Saved workbook with custom properties to {resultPath}");

            // Load the saved workbook to read properties
            var loadedWorkbook = new Workbook(resultPath);
            var loadedWorksheet = loadedWorkbook.Worksheets[0];
            var props = loadedWorksheet.CustomProperties;

            // Read properties
            int projectId = props["ProjectId"] != null ? (int)props["ProjectId"].Value : -1;
            string reviewer = props["Reviewer"] != null ? props["Reviewer"].Value.ToString() : "Unknown";
            DateTime createdOn = props["CreatedOn"] != null ? (DateTime)props["CreatedOn"].Value : DateTime.MinValue;

            Console.WriteLine($"ProjectId: {projectId}");
            Console.WriteLine($"Reviewer: {reviewer}");
            Console.WriteLine($"CreatedOn (UTC): {createdOn:u}");
        }
    }
}
```

इस प्रोग्राम को चलाने से पहले दिखाया गया कंसोल आउटपुट मिलेगा और `DataWithProps.xlsb` बन जाएगा जिसमें एम्बेडेड मेटाडेटा होगा।

## Common questions and edge cases

| Question | Answer |
|---|---|
| **क्या मैं गैर‑प्रिमिटिव टाइप्स स्टोर कर सकता हूँ?** | Aspose.Cells `string`, `int`, `double`, `DateTime`, और `bool` को सपोर्ट करता है। जटिल ऑब्जेक्ट्स के लिए उन्हें पहले JSON या XML में सीरियलाइज़ करके स्ट्रिंग के रूप में स्टोर करें। |
| **अगर वर्कबुक पासवर्ड‑प्रोटेक्टेड हो तो क्या करें?** | `CustomProperties` तक पहुँचने से पहले पासवर्ड के साथ वर्कबुक खोलें (`new Workbook(path, password)`)। डिक्रिप्शन के बाद भी प्रॉपर्टीज़ उपलब्ध रहती हैं। |
| **क्या कस्टम प्रॉपर्टीज़ फॉर्मेट कन्वर्ज़न में बनी रहती हैं?** | जब आप फ़ाइल को किसी अलग फॉर्मेट (जैसे `.xlsx`) में सेव करते हैं, तो Aspose.Cells कस्टम प्रॉपर्टीज़ को तब तक रखता है जब तक लक्ष्य फॉर्मेट उन्हें सपोर्ट करता है। |
| **कस्टम प्रॉपर्टी को कैसे डिलीट करें?** | `worksheet.CustomProperties.Remove("PropertyName");` का उपयोग करें। यह एंट्री को कलेक्शन से हटा देता है। |

## Next steps

अब जब आप **add custom properties** जानते हैं, तो आप निम्न संबंधित विषयों का अन्वेषण कर सकते हैं:

* दस्तावेज़ संस्करणीकरण के लिए **excel custom properties**  
* एक ही वर्कबुक में कई वर्कशीट्स से **read custom properties** पढ़ना  
* **Aspose.Cells** का उपयोग करके पिवट टेबल बनाना जो कस्टम मेटाडेटा को संदर्भित करती हैं  
* वर्कबुक को PDF में निर्यात करना जबकि कस्टम प्रॉपर्टीज़ को संरक्षित रखना  

विभिन्न डेटा टाइप्स के साथ प्रयोग करें, कस्टम प्रॉपर्टीज़ को सेल कमेंट्स के साथ मिलाएँ, या मेटाडेटा को बड़े डॉक्यूमेंट‑मैनेजमेंट सिस्टम में इंटीग्रेट करें।

---

**क्या आप अपने Excel रिपोर्टिंग को ऑटोमेट करने के लिए तैयार हैं?** ऊपर दिया गया कोड अपने प्रोजेक्ट में जोड़ें, प्रॉपर्टी नामों को अपने बिज़नेस की ज़रूरतों के अनुसार एडजस्ट करें, और आपके पास एक सेल्फ‑डिस्क्राइबिंग स्प्रेडशीट तैयार होगा जो डाउनस्ट्रीम प्रोसेसिंग के लिए उपयुक्त है।

## What Should You Learn Next?

निम्न ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच का पता लगा सकें।

- [Create Excel Workbook – Add Custom Properties and Save as XLSB](/cells/english/net/document-properties/create-excel-workbook-add-custom-properties-and-save-as-xlsb/)
- [How to Access Custom Document Properties in Excel Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/access-custom-excel-properties-aspose-cells-net/)
- [Master Excel Custom Properties Using Aspose.Cells .NET for Enhanced Data Management](/cells/english/net/data-manipulation/excel-custom-properties-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}