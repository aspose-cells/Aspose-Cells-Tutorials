---
category: general
date: 2026-07-26
description: Excel वर्कशीट से PowerPoint में आकृतियों को कुछ ही चरणों में निर्यात
  कैसे करें – डेवलपर्स के लिए एक तेज़ एक्सेल‑से‑PPTX ट्यूटोरियल।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to export shapes
- convert worksheet to powerpoint
- export excel to pptx
- excel to powerpoint tutorial
- export excel workbook powerpoint
language: hi
lastmod: 2026-07-26
og_description: Excel से PowerPoint में शैप्स को चरण‑दर‑चरण कैसे निर्यात करें। इस
  Excel से PPTX निर्यात ट्यूटोरियल का पालन करें और देखें कि आपकी वर्कशीट्स संपादन
  योग्य स्लाइड्स में बदल जाती हैं।
og_image_alt: Screenshot showing how to export shapes from Excel to PowerPoint using
  Aspose.Cells
og_title: Excel से PowerPoint में आकृतियों को निर्यात कैसे करें – तेज़ और आसान
schemas:
- author: Aspose
  dateModified: '2026-07-26'
  description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  headline: How to Export Shapes from Excel to PowerPoint – Complete Guide
  type: TechArticle
- description: How to export shapes from an Excel worksheet to PowerPoint in just
    a few steps – a quick export excel to pptx tutorial for developers.
  name: How to Export Shapes from Excel to PowerPoint – Complete Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code also works on .NET Framework 4.7+). - A valid
      license for **Aspose.Cells for .NET** (the free trial works for testing). -
      An Excel workbook (e.g., `ShapesDemo.xlsx`) that contains at least one text
      box or shape. - A development environment—Visual Studio, Rider, or VS Co'
  - name: Multiple Worksheets
    text: If you need to export several sheets into a single PPTX, loop through `workbook.Worksheets`
      and call `worksheet.Save` with the same `pptxOptions`. Aspose.Cells will automatically
      add a new slide for each sheet.
  - name: Custom Slide Layouts
    text: You can specify `pptxOptions.SlideSize` (e.g., `SlideSizeType.Widescreen`)
      to match your corporate deck dimensions.
  - name: Missing Files or Permissions
    text: 'Wrap the whole `Main` method in a `try` block:'
  type: HowTo
- questions:
  - answer: Yes. `Workbook` can open `.xls`, `.xlsx`, and even CSV files. The shape
      export works the same way.
    question: Does this work with older Excel formats (.xls)?
  - answer: Charts are already exported as native PowerPoint charts; you don’t need
      extra flags.
    question: What if I need to keep charts editable?
  - answer: Absolutely—just replace `SaveFormat.Pptx` with `SaveFormat.Pdf` and omit
      the `PptxSaveOptions`.
    question: Can I export to PDF instead of PPTX?
  type: FAQPage
tags:
- Aspose.Cells
- C#
- Office Automation
title: Excel से PowerPoint में आकृतियों को निर्यात करने की पूरी गाइड
url: /hi/net/drawing-objects/how-to-export-shapes-from-excel-to-powerpoint-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel से PowerPoint में Shapes को निर्यात कैसे करें – पूर्ण गाइड

क्या आपने कभी सोचा है कि Excel फ़ाइल से **shapes को कैसे निर्यात करें** और उन्हें PowerPoint डेक में संपादन योग्य रखें? आप अकेले नहीं हैं। चाहे आप रिपोर्टिंग पाइपलाइन बना रहे हों या सिर्फ एक शीट को प्रस्तुति में बदलने का तेज़ तरीका चाहिए, **worksheet को PowerPoint में बदलने** की क्षमता, बिना shape की संपादन योग्यता खोए, आपके कई घंटे का मैन्युअल काम बचा सकती है।

इस **excel to powerpoint tutorial** में हम एक पूरी‑कार्यशील C# उदाहरण के माध्यम से चलेंगे जो एक workbook लोड करता है, सही निर्यात विकल्पों को कॉन्फ़िगर करता है, और एक PPTX फ़ाइल लिखता है जहाँ टेक्स्ट बॉक्स और अन्य ड्राइंग ऑब्जेक्ट्स संपादन योग्य रहते हैं। कोई अस्पष्ट संदर्भ नहीं—सिर्फ वह कोड जिसे आप आज ही कॉपी, पेस्ट और चलाएँ।

## आप क्या सीखेंगे

- shape editability को बनाए रखते हुए **export excel to pptx** के सटीक चरण।  
- `Aspose.Cells` लाइब्रेरी के `PptxSaveOptions` निर्यात व्यवहार को कैसे नियंत्रित करते हैं।  
- एकाधिक worksheets, गायब फ़ाइलों, और कस्टम shape सेटिंग्स को संभालने के टिप्स।  
- एक पूर्ण, चलाने योग्य प्रोग्राम जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।  

### पूर्वापेक्षाएँ

- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ पर भी काम करता है)।  
- **Aspose.Cells for .NET** के लिए एक वैध लाइसेंस (फ़्री ट्रायल परीक्षण के लिए काम करता है)।  
- एक Excel workbook (जैसे `ShapesDemo.xlsx`) जिसमें कम से कम एक टेक्स्ट बॉक्स या shape हो।  
- एक विकास पर्यावरण—Visual Studio, Rider, या VS Code पर्याप्त है।  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं।

## चरण 1: Workbook लोड करें – How to Export Shapes का शुरुआती बिंदु

पहले हमें उस Excel फ़ाइल को खोलना होगा जिसमें वे shapes हैं जिन्हें हम संपादन योग्य रखना चाहते हैं।

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        // Load the Excel workbook that contains text boxes and other shapes
        Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
        Worksheet worksheet = workbook.Worksheets[0];
```

**यह क्यों महत्वपूर्ण है:**  
`Workbook` ऑब्जेक्ट फ़ाइल के भीतर प्रत्येक सेल, चार्ट, और ड्राइंग ऑब्जेक्ट का द्वार है। पहले worksheet (`Worksheets[0]`) को पकड़कर हम सुनिश्चित करते हैं कि हम एक ज्ञात शीट पर काम कर रहे हैं, लेकिन यदि आपको किसी विशिष्ट टैब की आवश्यकता है तो आप इंडेक्स को नाम (`workbook.Worksheets["Sheet2"]`) से बदल सकते हैं।

> **Pro tip:** यदि फ़ाइल पथ गलत हो तो एक मित्रवत त्रुटि देने के लिए लोड कॉल को `try / catch` ब्लॉक में घेरें।

## चरण 2: PPTX निर्यात विकल्प कॉन्फ़िगर करें – How to Export Shapes का मूल

अब हम Aspose.Cells को बताते हैं कि परिणामस्वरूप PPTX में shapes को संपादन योग्य रखें।

```csharp
        // Configure PPTX export options to keep shapes editable
        var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
        {
            ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
            ExportEditableShapes = true     // makes other shapes editable in the PPTX
        };
```

**इन फ़्लैग्स का कारण क्या है?**  
- `ExportEditableTextBoxes` Excel के टेक्स्ट बॉक्स को PowerPoint के टेक्स्ट प्लेसहोल्डर में बदलता है जिसे आप डबल‑क्लिक करके संपादित कर सकते हैं।  
- `ExportEditableShapes` वही काम arrows, rectangles, और SmartArt जैसे shapes के लिए करता है। इनके बिना, ऑब्जेक्ट्स स्थिर छवियों में बदल जाते हैं, जिससे **convert worksheet to powerpoint** वर्कफ़्लो का उद्देश्य विफल हो जाता है।  

आप `PptxSaveOptions` को स्लाइड आकार, थीम, या फ़ॉन्ट एम्बेड करने के लिए भी समायोजित कर सकते हैं—जब आपकी प्रस्तुति को कॉर्पोरेट ब्रांडिंग से मेल खाना हो तो यह उपयोगी है।

## चरण 3: Worksheet को PPTX के रूप में सहेजें – Export Excel Workbook PowerPoint का अंतिम भाग

विकल्प सेट होने के बाद, सहेजना सीधा है।

```csharp
        // Save the worksheet as a PPTX file with the editable shapes option
        worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);
```

**आंतरिक रूप से क्या होता है?**  
Aspose.Cells शीट पर प्रत्येक ड्राइंग ऑब्जेक्ट पर इटररेट करता है, उसे संबंधित PowerPoint shape क्लास में मैप करता है, और वह XML लिखता है जिसे PowerPoint पढ़ता है। क्योंकि हमने संपादन योग्य फ़्लैग्स को सक्षम किया है, XML प्रत्येक shape को `Picture` के बजाय `Shape` के रूप में चिह्नित करता है, इसलिए PowerPoint इसे एक लाइव ऑब्जेक्ट मानता है।

## चरण 4: निर्यात की पुष्टि करें – उपयोगकर्ता के लिए त्वरित प्रतिक्रिया

एक छोटा कंसोल संदेश आपको बताता है कि प्रक्रिया सफल रही।

```csharp
        // Inform the user that the export is complete
        Console.WriteLine("Exported worksheet with editable shapes.");
    }
}
```

यदि आप प्रोग्राम चलाते हैं और संदेश देखते हैं, तो PowerPoint में `ShapesEditable.pptx` खोलें। किसी भी टेक्स्ट बॉक्स पर क्लिक करें—आपको सीधे टेक्स्ट संपादित करने में सक्षम होना चाहिए, और shape को ड्रैग करने से वह मूल PowerPoint ऑब्जेक्ट की तरह ही मूव होगा।

## चरण 5: वास्तविक‑दुनिया के परिदृश्यों को संभालना

नीचे कुछ सामान्य विविधताएँ दी गई हैं जो आप **excel to powerpoint tutorial** पर काम करते समय सामना कर सकते हैं।

### कई Worksheets

यदि आपको कई शीट्स को एक ही PPTX में निर्यात करना है, तो `workbook.Worksheets` पर लूप करें और समान `pptxOptions` के साथ `worksheet.Save` कॉल करें। Aspose.Cells प्रत्येक शीट के लिए स्वचालित रूप से एक नई स्लाइड जोड़ देगा।

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    ws.Save($"YOUR_DIRECTORY/{ws.Name}.pptx", SaveFormat.Pptx, pptxOptions);
}
```

### कस्टम स्लाइड लेआउट्स

आप `pptxOptions.SlideSize` (जैसे `SlideSizeType.Widescreen`) निर्दिष्ट कर सकते हैं ताकि यह आपके कॉर्पोरेट डेक के आयामों से मेल खाए।

```csharp
pptxOptions.SlideSize = SlideSizeType.Widescreen;
```

### गायब फ़ाइलें या अनुमतियाँ

`Main` मेथड को पूरी तरह `try` ब्लॉक में घेरें:

```csharp
try
{
    // ... existing code ...
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error: {ex.Message}");
}
```

यह **export excel workbook powerpoint** प्रक्रिया को प्रोडक्शन पाइपलाइन के लिए मजबूत बनाता है।

## पूर्ण कार्यशील उदाहरण

यहाँ वह पूर्ण प्रोग्राम है जिसे आप अभी संकलित कर सकते हैं। इसे `ExportEditableShapes.cs` के रूप में सहेजें, फ़ाइल पथ समायोजित करें, और `dotnet run` चलाएँ।

```csharp
using Aspose.Cells;
using System;

class ExportEditableShapes
{
    static void Main()
    {
        try
        {
            // Step 1: Load the Excel workbook that contains text boxes and other shapes
            Workbook workbook = new Workbook("YOUR_DIRECTORY/ShapesDemo.xlsx");
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 2: Configure PPTX export options to keep shapes editable
            var pptxOptions = new Aspose.Cells.Export.PptxSaveOptions
            {
                ExportEditableTextBoxes = true, // makes text boxes editable in the PPTX
                ExportEditableShapes = true,    // makes other shapes editable in the PPTX
                SlideSize = SlideSizeType.Widescreen // optional: set slide size
            };

            // Step 3: Save the worksheet as a PPTX file with the editable shapes option
            worksheet.Save("YOUR_DIRECTORY/ShapesEditable.pptx", SaveFormat.Pptx, pptxOptions);

            // Step 4: Inform the user that the export is complete
            Console.WriteLine("Exported worksheet with editable shapes.");
        }
        catch (Exception ex)
        {
            // Step 5: Handle errors gracefully
            Console.Error.WriteLine($"Export failed: {ex.Message}");
        }
    }
}
```

**अपेक्षित आउटपुट** जब आप प्रोग्राम चलाते हैं:

```
Exported worksheet with editable shapes.
```

जनरेट किए गए `ShapesEditable.pptx` को खोलें और आप प्रत्येक Excel shape को एक पूरी तरह संपादन योग्य PowerPoint ऑब्जेक्ट के रूप में देखेंगे—बिल्कुल वही जो आपने **how to export shapes** खोजते समय माँगा था।

## अक्सर पूछे जाने वाले प्रश्न

- **क्या यह पुराने Excel फ़ॉर्मेट्स (.xls) के साथ काम करता है?**  
  हाँ। `Workbook` `.xls`, `.xlsx`, और यहाँ तक कि CSV फ़ाइलें भी खोल सकता है। shape निर्यात उसी तरह काम करता है।

- **यदि मुझे चार्ट्स को भी संपादन योग्य रखना हो तो क्या करें?**  
  चार्ट्स पहले से ही मूल PowerPoint चार्ट्स के रूप में निर्यात होते हैं; आपको अतिरिक्त फ़्लैग्स की आवश्यकता नहीं है।

- **क्या मैं PPTX के बजाय PDF में निर्यात कर सकता हूँ?**  
  बिल्कुल—सिर्फ `SaveFormat.Pptx` को `SaveFormat.Pdf` से बदलें और `PptxSaveOptions` को छोड़ दें।

## निष्कर्ष

अब आपके पास Excel से एक संपादन योग्य PowerPoint डेक में **how to export shapes** का एक ठोस, अंत‑से‑अंत उत्तर है। `Aspose.Cells` के `PptxSaveOptions` का उपयोग करके, आप प्रत्येक टेक्स्ट बॉक्स और ड्राइंग ऑब्जेक्ट को संरक्षित रखते हैं, जिससे एक स्थिर स्प्रेडशीट को न्यूनतम प्रयास से एक गतिशील प्रस्तुति में बदल दिया जाता है।

अगली चुनौती के लिए तैयार हैं? कस्टम स्लाइड मास्टर्स जोड़ने, प्रोग्रामेटिकली इमेजेज डालने, या इस निर्यात को CI/CD पाइपलाइन में जोड़ने की कोशिश करें जो स्वचालित रूप से साप्ताहिक सेल्स डेक जनरेट करे। **export excel workbook powerpoint** की दुनिया अब खुली है—जाएँ और खोजें!

--- 

*यदि आपको यह **excel to powerpoint tutorial** उपयोगी लगा, तो इसे GitHub पर स्टार दें या किसी सहयोगी के साथ साझा करें जो अभी भी स्प्रेडशीट को स्लाइड्स में कॉपी‑पेस्ट करता है। कोडिंग का आनंद लें!*

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [How to Export Excel Cells as Images Using Aspose.Cells for Java](/cells/english/java/import-export/export-excel-cells-as-image-aspose-cells-java/)
- [How to Export Excel Charts as SVG Using Aspose.Cells Java for Scalable Vector Graphics](/cells/english/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}