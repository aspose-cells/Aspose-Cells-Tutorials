---
category: general
date: 2026-02-26
description: एम्बेडेड फ़ॉन्ट्स के साथ वर्कबुक को PDF में निर्यात करें और C# में चार्ट्स
  को PowerPoint में भी निर्यात करें। पिवट टेबल वर्कशीट को कॉपी करना सीखें और वर्कबुक
  को PPTX के रूप में सहेजें।
draft: false
keywords:
- export workbook to pdf
- export charts to powerpoint
- copy pivot table worksheet
- embed fonts pdf export
- save workbook as pptx
language: hi
og_description: वर्कबुक को एम्बेडेड फ़ॉन्ट्स के साथ PDF में निर्यात करें और C# में
  चार्ट्स को PowerPoint में भी निर्यात करें। पिवट टेबल्स को कॉपी करने और उन्हें PPTX
  के रूप में सहेजने के लिए चरण‑दर‑चरण गाइड का पालन करें।
og_title: वर्कबुक को पीडीएफ में निर्यात करें – पूर्ण C# गाइड
tags:
- Aspose.Cells
- Aspose.Slides
- C#
- Reporting
title: वर्कबुक को PDF में निर्यात करें – पूर्ण C# गाइड
url: /hi/net/conversion-to-pdf/export-workbook-to-pdf-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# वर्कबुक को PDF में निर्यात करें – पूर्ण C# गाइड

Export workbook to PDF एक सामान्य आवश्यकता है जब आपको रिपोर्ट्स को उन हितधारकों के साथ साझा करना होता है जिनके पास Excel स्थापित नहीं हो सकता। इस ट्यूटोरियल में हम आपको दिखाएंगे कि कैसे **export charts to PowerPoint**, **pivot table worksheet** को कॉपी करें, और फ़ॉन्ट एम्बेड करें ताकि PDF आपके स्क्रीन पर दिखने वाले डिज़ाइन के बिल्कुल समान दिखे।  

क्या आपने कभी सोचा है कि कुछ PDFs मूल लेआउट क्यों खो देते हैं या PowerPoint स्लाइड्स में आकृतियाँ क्यों गायब हो जाती हैं? इसका कारण अक्सर निर्यात प्रक्रिया के दौरान विकल्पों की कमी होता है। इस गाइड के अंत तक आपके पास एक ही, पुन: उपयोग योग्य C# मेथड होगा जो इन सभी समस्याओं को हल करता है—अब मैन्युअल कॉपी‑पेस्ट या निर्यात सेटिंग्स के साथ झंझट नहीं।

## आप क्या सीखेंगे

- कैसे एक workbook बनाएं, Smart Marker एक्सप्रेशन जोड़ें, और उन्हें प्रोसेस करें।  
- कैसे **copy a pivot table worksheet** को डेटा स्रोत को तोड़े बिना कॉपी करें।  
- कैसे **export charts, shapes, and text boxes** को PowerPoint प्रेजेंटेशन में निर्यात करें जबकि उन्हें संपादन योग्य रखें।  
- कैसे **embed standard fonts** को PDF निर्यात के दौरान एम्बेड करें ताकि किसी भी मशीन पर समान रेंडरिंग मिले।  
- कैसे **save the workbook as PPTX** `save workbook as pptx` एप्रोच का उपयोग करके करें।  

यह सब नवीनतम Aspose.Cells और Aspose.Slides .NET लाइब्रेरीज़ (लेखन के समय संस्करण 23.11) के साथ काम करता है। कोई बाहरी टूल नहीं, कोई पोस्ट‑प्रोसेसिंग स्क्रिप्ट नहीं—सिर्फ शुद्ध C#।

> **Pro tip:** यदि आप पहले से ही अपने प्रोजेक्ट में Aspose का उपयोग कर रहे हैं, तो आप कोड स्निपेट्स को जैसा है वैसा ही डाल सकते हैं; अन्यथा, पहले NuGet पैकेज `Aspose.Cells` और `Aspose.Slides` जोड़ें।

## पूर्वापेक्षाएँ

- .NET 6.0 या बाद वाला (कोड .NET Framework 4.7.2 पर भी चलता है)।  
- Visual Studio 2022 (या आपका पसंदीदा कोई भी IDE)।  
- NuGet के माध्यम से स्थापित Aspose.Cells .NET और Aspose.Slides .NET।  
- C# और Excel अवधारणाओं जैसे Smart Markers और PivotTables की बुनियादी समझ।

---

![Export workbook to PDF diagram](export-workbook-to-pdf.png "Export workbook to PDF workflow showing PDF and PPTX outputs")

## वर्कबुक को PDF में निर्यात करें – चरण‑दर‑चरण कार्यान्वयन

नीचे पूर्ण, तैयार‑चलाने‑योग्य उदाहरण दिया गया है। यह एक workbook बनाता है, Smart Marker एक्सप्रेशन इन्जेक्ट करता है, उन्हें प्रोसेस करता है, पिवट टेबल रेंज को कॉपी करता है, और अंत में PDF तथा PowerPoint दोनों फ़ाइलें सहेजता है।

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides.Export;

namespace ReportExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Build the workbook and add Smart Markers
            // -------------------------------------------------
            var reportWorkbook = new Workbook();
            Worksheet dataSheet = reportWorkbook.Worksheets[0];

            // Header with a variable department name
            dataSheet.Cells["A1"].PutValue("Report for ${$dept=Department}");

            // Conditional text based on department
            dataSheet.Cells["A2"].PutValue("${if $dept == \"Sales\"}Sales Summary${else}Other Summary${/if}");

            // Table header for orders – this will be repeated for each order
            dataSheet.Cells["A5:D5"].PutValue("${Orders.Product}|${Orders.Quantity}|${Orders.Price}");

            // -------------------------------------------------
            // Step 2: Process Smart Markers and name the detail sheet
            // -------------------------------------------------
            reportWorkbook.SmartMarkerProcessor.Options.DetailSheetNewName = "Orders_${$dept}";
            reportWorkbook.SmartMarkerProcessor.Process();

            // -------------------------------------------------
            // Step 3: Copy the range that contains the pivot table
            // -------------------------------------------------
            // Assume the pivot table lives in A1:G30 on the original sheet
            Range sourceRange = dataSheet.Cells.CreateRange("A1", "G30");
            Worksheet copySheet = reportWorkbook.Worksheets.Add("Copy");
            sourceRange.Copy(copySheet.Cells["A1"]);   // Pivot table is duplicated intact

            // -------------------------------------------------
            // Step 4: Export to PowerPoint (keep charts, shapes, text boxes)
            // -------------------------------------------------
            var pptOptions = new PresentationOptions
            {
                ExportCharts = true,
                ExportShapes = true,
                ExportTextBoxes = true
            };
            string pptPath = @"C:\Temp\FinalPresentation.pptx";
            reportWorkbook.Save(pptPath, SaveFormat.Pptx, pptOptions);

            // -------------------------------------------------
            // Step 5: Export to PDF and embed standard fonts
            // -------------------------------------------------
            var pdfOptions = new PdfSaveOptions { EmbedStandardFonts = true };
            string pdfPath = @"C:\Temp\FinalReport.pdf";
            reportWorkbook.Save(pdfPath, pdfOptions);

            Console.WriteLine("Export completed:");
            Console.WriteLine($" • PDF saved to {pdfPath}");
            Console.WriteLine($" • PowerPoint saved to {pptPath}");
        }
    }
}
```

### यह क्यों काम करता है

1. **Smart Marker processing** आपको किसी भी डेटा स्रोत (JSON, DataTables, आदि) से workbook को लूप लिखे बिना भरने देता है।  
2. **DetailSheetNewName** प्रत्येक विभाग के लिए एक अलग शीट बनाता है, जिससे आपको एक साफ़, प्रति‑विभाग टैब मिलता है।  
3. **Copying the range** (`sourceRange.Copy`) पिवट टेबल *सहित* उसकी कैश को डुप्लिकेट करता है, इसलिए कॉपी की गई शीट मूल की तरह ही व्यवहार करती है।  
4. **PresentationOptions** के साथ `ExportCharts`, `ExportShapes`, और `ExportTextBoxes` Aspose को इन ऑब्जेक्ट्स को नेटिव PowerPoint एलिमेंट्स के रूप में रेंडर करने के लिए कहता है, जिससे एडिटेबिलिटी बनी रहती है।  
5. **PdfSaveOptions.EmbedStandardFonts** सुनिश्चित करता है कि PDF उन मशीनों पर भी मूल फ़ॉन्ट्स के बिना समान दिखे जहाँ फ़ॉन्ट्स इंस्टॉल नहीं हैं।

परिणाम दो फ़ाइलें—`FinalReport.pdf` और `FinalPresentation.pptx`—हैं जिन्हें ईमेल किया जा सकता है, आर्काइव किया जा सकता है, या किसी भी व्यूअर में खोले बिना फ़िडेलिटी खोए।

## चार्ट्स को PowerPoint में निर्यात करें (वर्कबुक को PPTX के रूप में सहेजें)

यदि आपके रिपोर्ट में चार्ट्स हैं, तो आप संभवतः उन्हें PowerPoint में संपादन योग्य चाहते हैं। `PresentationOptions` क्लास यही कुंजी है। यहाँ एक केंद्रित स्निपेट है जो केवल चार्ट‑निर्यात भाग को दिखाता है:

```csharp
// Assuming reportWorkbook already contains charts
var pptExportOptions = new PresentationOptions
{
    ExportCharts = true,      // Convert Excel charts to PowerPoint chart objects
    ExportShapes = false,    // Skip shapes if you don’t need them
    ExportTextBoxes = true   // Keep any text boxes editable
};

string pptFile = @"C:\Temp\ChartsOnly.pptx";
reportWorkbook.Save(pptFile, SaveFormat.Pptx, pptExportOptions);
```

**What happens under the hood?** Aspose प्रत्येक Excel चार्ट को एक नेटिव PowerPoint चार्ट में परिवर्तित करता है, सीरीज़, एक्सिस टाइटल, और फ़ॉर्मेटिंग को संरक्षित रखते हुए। यह स्थिर इमेज के रूप में निर्यात करने से कहीं बेहतर है, क्योंकि आपका दर्शक बाद में डेटा पॉइंट्स को समायोजित कर सकता है।

## डेटा खोए बिना पिवट टेबल वर्कशीट कॉपी करें

पिवट टेबल अक्सर निर्यात का सबसे कठिन हिस्सा होते हैं क्योंकि वे एक छिपी हुई कैश पर निर्भर करते हैं। सरल `Copy` मेथड काम करता है क्योंकि Aspose दृश्य रेंज **और** अंतर्निहित कैश ऑब्जेक्ट दोनों को कॉपी करता है।

```csharp
// Copy the whole sheet (including pivot table) to a new workbook
Workbook clone = new Workbook();
reportWorkbook.Worksheets[0].CopyTo(clone.Worksheets[0]);
clone.Save(@"C:\Temp\PivotCopy.xlsx", SaveFormat.Xlsx);
```

> **Note:** यदि आपको केवल उसी workbook के भीतर नई शीट पर पिवट टेबल चाहिए, तो पहले का `sourceRange.Copy` एप्रोच हल्का है और पूरे नए workbook को बनाने से बचाता है।

## PDF निर्यात के लिए फ़ॉन्ट एम्बेड करें – क्यों महत्वपूर्ण है

जब आप किसी ऐसी मशीन पर PDF खोलते हैं जहाँ मूल फ़ॉन्ट्स नहीं हैं, तो टेक्स्ट शिफ्ट हो सकता है, लाइन ब्रेक बदल सकते हैं, या अक्षर गायब हो सकते हैं। `EmbedStandardFonts = true` सेट करने से Aspose सबसे सामान्य फ़ॉन्ट्स (Arial, Times New Roman, आदि) को सीधे PDF स्ट्रीम में एम्बेड कर देता है।

यदि आप कस्टम फ़ॉन्ट्स का उपयोग करते हैं, तो `PdfSaveOptions.FontEmbeddingMode = FontEmbeddingMode.EmbedAll` पर स्विच करें। यहाँ एक उदाहरण है:

```csharp
var pdfOpts = new PdfSaveOptions
{
    EmbedStandardFonts = true,
    FontEmbeddingMode = FontEmbeddingMode.EmbedAll   // For custom fonts
};
reportWorkbook.Save(@"C:\Temp\CustomFontReport.pdf", pdfOpts);
```

अब हर प्राप्तकर्ता वही लेआउट देखेगा जो आपने डिज़ाइन किया था—कोई आश्चर्य नहीं।

## पूर्ण कार्यशील उदाहरण सारांश

सब कुछ मिलाकर, पूरा प्रोग्राम (पहले दिखाया गया) निम्नलिखित करता है:

1. **Creates** एक workbook जिसमें Smart Marker प्लेसहोल्डर होते हैं।  
2. **Processes** मार्कर्स, जिससे विभाग के नाम पर एक डिटेल शीट बनती है।  
3. **Copies** पिवट टेबल वाली रेंज को नई वर्कशीट में, उसकी कार्यक्षमता को संरक्षित रखते हुए।  
4. **Exports** workbook को PowerPoint में, चार्ट्स, शैप्स, और टेक्स्ट बॉक्स को संपादन योग्य रखते हुए।  
5. **Exports** वही workbook को PDF में, विश्वसनीय रेंडरिंग के लिए मानक फ़ॉन्ट्स एम्बेड करते हुए।

प्रोग्राम चलाएँ, जेनरेट की गई फ़ाइलें खोलें, और आप देखेंगे:

- **PDF**: स्पष्ट टेबल्स, एम्बेडेड फ़ॉन्ट्स, और Excel स्रोत के समान विज़ुअल स्टाइल।  
- **PowerPoint**: संपादन योग्य चार्ट्स जिन्हें आप राइट‑क्लिक → *Edit Data* कर सकते हैं, और शैप्स जो पूरी तरह से मैनिपुलेटेबल रहते हैं।

---

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**Q: क्या यह .NET Core के साथ काम करता है?**  
हाँ—Aspose.Cells और Aspose.Slides क्रॉस‑प्लेटफ़ॉर्म हैं। बस .NET 6 या बाद वाला टार्गेट करें और वही कोड Windows, Linux, या macOS पर चलता है।

**Q: यदि मुझे केवल कुछ शीट्स को निर्यात करना हो तो क्या करें?**  
`Workbook.Save` को `SaveOptions` के साथ उपयोग करें जो आपको `SheetNames` निर्दिष्ट करने की अनुमति देता है। उदाहरण: `new PresentationOptions { SheetNames = new[] { "Copy" } }`।

**Q: क्या मैं PDF को एन्क्रिप्ट कर सकता हूँ?**  
बिल्कुल। `PdfSaveOptions.EncryptionDetails` को पासवर्ड के साथ सेट करें और फिर `Save` कॉल करें।

**Q: मेरी पिवट टेबल एक बाहरी डेटा स्रोत का उपयोग करती है—क्या कॉपी करने से लिंक टूट जाएगा?**  
कॉपी ऑपरेशन कैश को शामिल करता है, न कि बाहरी कनेक्शन को। पिवट ऑफ़लाइन काम करेगा, लेकिन मूल स्रोत के खिलाफ रिफ्रेश नहीं होगा। यदि आपको लाइव रिफ्रेश चाहिए, तो स्रोत डेटा को workbook के साथ निर्यात करें।

## अगले कदम और संबंधित विषय

- **Dynamic Data Sources** – सीखें कैसे JSON या DataTable को Smart Markers में फ़ीड करें रीयल‑टाइम रिपोर्टिंग के लिए।  
- **Advanced PDF Styling** – Explore `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}