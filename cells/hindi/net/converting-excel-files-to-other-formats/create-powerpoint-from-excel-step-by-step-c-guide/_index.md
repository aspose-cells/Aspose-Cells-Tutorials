---
category: general
date: 2026-03-30
description: Aspose.Cells और Aspose.Slides का उपयोग करके Excel से जल्दी PowerPoint
  बनाएं। जानें कैसे वर्कशीट को इमेज के रूप में निर्यात करें और C# में प्रेजेंटेशन
  को PPTX के रूप में सहेजें।
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- export worksheet as image
- save presentation as pptx
- export excel chart as picture
language: hi
og_description: Aspose के साथ C# में Excel से PowerPoint बनाएं। वर्कशीट को इमेज के
  रूप में निर्यात करें, शैप्स को संपादन योग्य रखें, और परिणाम को PPTX के रूप में सहेजें।
og_title: Excel से PowerPoint बनाएं – पूर्ण C# ट्यूटोरियल
tags:
- Aspose
- C#
- Office Automation
title: एक्सेल से पॉवरपॉइंट बनाएं – चरण-दर-चरण C# गाइड
url: /hi/net/converting-excel-files-to-other-formats/create-powerpoint-from-excel-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel से PowerPoint बनाएं – पूर्ण C# ट्यूटोरियल

क्या आपको कभी **Excel से PowerPoint बनाना** पड़ा है लेकिन यह नहीं पता था कि कौन सी लाइब्रेरी आपके चार्ट्स को एडिटेबल रखेगी? आप अकेले नहीं हैं। कई रिपोर्टिंग परिदृश्यों में आप एक स्प्रेडशीट को स्लाइड डेक में बदलना चाहेंगे बिना बाद में टेक्स्ट बॉक्स को संशोधित करने की क्षमता खोए। यह गाइड आपको बिल्कुल दिखाता है कि **Excel को PowerPoint में कैसे बदलें** Aspose.Cells और Aspose.Slides का उपयोग करके, साथ ही **वर्कशीट को इमेज के रूप में एक्सपोर्ट** करने और अंत में **प्रेजेंटेशन को PPTX के रूप में सेव** करने का तरीका।

हम हर कोड लाइन को विस्तार से देखेंगे, *क्यों* प्रत्येक सेटिंग महत्वपूर्ण है समझाएंगे, और यह भी चर्चा करेंगे कि यदि आपके वर्कबुक में जटिल चार्ट्स हों जिन्हें आप चित्र के रूप में एक्सपोर्ट करना चाहें तो क्या करना है। अंत तक आपके पास एक तैयार‑चलाने‑योग्य C# कंसोल ऐप होगा जो `ShapesDemo.xlsx` को लेता है और `Result.pptx` आउटपुट करता है – सभी एडिटेबल टेक्स्ट बॉक्स और स्पष्ट इमेज के साथ।

## आपको क्या चाहिए

- .NET 6.0 या बाद का संस्करण (API .NET Framework के साथ भी काम करता है, लेकिन .NET 6 सबसे उपयुक्त है)।  
- **Aspose.Cells** और **Aspose.Slides** NuGet पैकेज (टेस्टिंग के लिए फ्री ट्रायल लाइसेंस काम करेंगे)।  
- C# सिंटैक्स की बुनियादी समझ – यदि आप `Console.WriteLine` लिख सकते हैं, तो आप तैयार हैं।  

कोई अतिरिक्त COM इंटरऑप नहीं, सर्वर पर Office इंस्टॉल नहीं होना चाहिए, और इमेज की मैन्युअल कॉपी‑पेस्ट की जरूरत नहीं। सब कुछ प्रोग्रामेटिकली संभाला जाता है।

## Excel से PowerPoint बनाएं – वर्कबुक लोड करें और एक्सपोर्ट विकल्प सेट करें

पहले हम Excel फ़ाइल खोलते हैं और Aspose.Cells को बताते हैं कि हम शीट को कैसे रेंडर करना चाहते हैं। `ImageOrPrintOptions` ऑब्जेक्ट वह जगह है जहाँ जादू होता है: हम `ExportShapes` और `ExportEditableTextBoxes` को सक्षम करते हैं ताकि कोई भी शैप (चार्ट सहित) स्लाइड का हिस्सा बन जाए **और** कन्वर्ज़न के बाद भी एडिटेबल रहे।

```csharp
using Aspose.Cells;
using Aspose.Slides;

// 1️⃣ Load the Excel workbook
string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
Workbook workbook = new Workbook(excelPath);
Worksheet worksheet = workbook.Worksheets[0];   // Grab the first sheet

// 2️⃣ Configure image export – keep shapes editable
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    OnePagePerSheet = true,          // Export the whole sheet as one slide
    ExportShapes = true,             // Include shapes (charts, drawings)
    ExportEditableTextBoxes = true   // Make text boxes editable in PPTX
};
```

**इन फ़्लैग्स का कारण क्या है?**  
- `OnePagePerSheet` शीट को कई स्लाइड्स में विभाजित होने से रोकता है – आपको एक ही पूर्ण‑साइज़ चित्र मिलता है।  
- `ExportShapes` Aspose.Cells को चार्ट्स *और* वेक्टर शैप्स को रास्टराइज़ करने के लिए कहता है, जिससे उनका लुक बरकरार रहता है।  
- `ExportEditableTextBoxes` वह गुप्त सॉस है जो आपको PowerPoint में टेक्स्टबॉक्स पर डबल‑क्लिक करके बिना Excel खोले टेक्स्ट एडिट करने देता है।

> **Pro tip:** यदि आपको केवल चार्ट की स्थिर तस्वीर चाहिए, तो `ExportShapes = false` सेट करें और बाद में `ExportExcelChartAsPicture` मेथड का उपयोग करें (अंतिम सेक्शन देखें)।

## Excel को PowerPoint में बदलें – वर्कशीट से इमेज जनरेट करें

ऑप्शन तैयार होने के बाद, हम अब वर्कशीट को `System.Drawing.Image` में बदलते हैं। `WorksheetToImageConverter` भारी काम करता है, हमने जो सेटिंग्स अभी परिभाषित की हैं उन्हें लागू करता है।

```csharp
// 3️⃣ Convert the worksheet to an image using the options above
WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
System.Drawing.Image sheetImage = converter.ConvertToImage(0, imageOptions);
```

`0` आर्ग्यूमेंट पहला पेज दर्शाता है (हमारे पास केवल एक ही पेज है क्योंकि `OnePagePerSheet` सेट है)। परिणामी `sheetImage` मूल DPI को बरकरार रखता है, इसलिए आपकी स्लाइड हाई‑रिज़ॉल्यूशन डिस्प्ले पर भी पिक्सेलेटेड नहीं दिखेगी।

## प्रेजेंटेशन को PPTX के रूप में सेव करें – स्लाइड में इमेज डालें

अब हम एक नई PowerPoint फ़ाइल बनाते हैं, एक स्लाइड जोड़ते हैं, और बिटमैप को उस पर ड्रॉप करते हैं। Aspose.Slides चित्र को *picture frame* शैप के रूप में ट्रीट करता है, जिसे आप बाद में किसी भी नेटिव PowerPoint ऑब्जेक्ट की तरह रिसाइज़ या मूव कर सकते हैं।

```csharp
// 4️⃣ Create a new PowerPoint presentation
Presentation presentation = new Presentation();
ISlide slide = presentation.Slides[0];   // The default blank slide

// Add the Excel‑derived image as a picture frame
slide.Shapes.AddPictureFrame(
    ShapeType.Rectangle,                 // Simple rectangle container
    0, 0,                                // Top‑left corner (0,0)
    sheetImage.Width,                    // Width of the picture
    sheetImage.Height,                   // Height of the picture
    sheetImage);                         // The bitmap we generated
```

> **अगर इमेज स्लाइड साइज से बड़ी हो तो क्या करें?**  
> PowerPoint स्वचालित रूप से स्लाइड डाइमेंशन से अधिक किसी भी चीज़ को क्लिप कर देगा। एक त्वरित समाधान है इमेज को इन्सर्ट करने से पहले स्केल करना:

```csharp
float scale = Math.Min(presentation.SlideSize.Size.Width / (float)sheetImage.Width,
                       presentation.SlideSize.Size.Height / (float)sheetImage.Height);
int newWidth  = (int)(sheetImage.Width * scale);
int newHeight = (int)(sheetImage.Height * scale);
```

फिर आप `newWidth` और `newHeight` को `AddPictureFrame` में पास कर सकते हैं।

## वर्कशीट को इमेज के रूप में एक्सपोर्ट करें – PPTX फ़ाइल सेव करें

अंत में हम प्रेजेंटेशन को डिस्क पर सेव करते हैं। `SaveFormat.Pptx` फ़्लैग आधुनिक OpenXML फ़ॉर्मेट को गारंटी देता है, जो सभी हालिया PowerPoint वर्ज़न में काम करता है।

```csharp
// 5️⃣ Save the presentation as a PPTX file
string pptxPath = "YOUR_DIRECTORY/Result.pptx";
presentation.Save(pptxPath, SaveFormat.Pptx);
```

जब आप `Result.pptx` खोलेंगे तो आपको एक ही स्लाइड दिखेगी जो आपके Excel शीट जैसी दिखती है, लेकिन आप अभी भी किसी भी टेक्स्टबॉक्स पर क्लिक करके उसका कंटेंट सीधे PowerPoint में एडिट कर सकते हैं।

## Excel चार्ट को चित्र के रूप में एक्सपोर्ट करें – जब रास्टर इमेज पसंद हों

कभी‑कभी आपको एडिटेबल शैप्स की ज़रूरत नहीं होती; एक हाई‑क्वालिटी PNG चार्ट की पर्याप्त होती है। Aspose.Cells पूरे शीट को बदलने के बिना किसी विशिष्ट चार्ट को इमेज में एक्सपोर्ट कर सकता है:

```csharp
// Example: Export the first chart on the sheet as a PNG
int chartIndex = 0; // Adjust if you have multiple charts
Chart chart = worksheet.Charts[chartIndex];
ImageOrPrintOptions chartOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,
    OnePagePerSheet = false
};
chart.ToImage("chart.png", chartOptions);
```

फिर आप `chart.png` को उसी तरह स्लाइड में एम्बेड कर सकते हैं जैसे हमने `sheetImage` डाली थी। यह तरीका PPTX फ़ाइल साइज को कम करता है और तब उपयोगी होता है जब स्लाइड पर आसपास का डेटा आवश्यक नहीं होता।

## सामान्य समस्याएँ और उनके समाधान

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Text looks blurry** | Exported at low DPI (default 96). | Set `imageOptions.Dpi = 300;` before conversion. |
| **Shapes disappear** | `ExportShapes` left `false`. | Ensure `ExportShapes = true` when you need editable graphics. |
| **Slide size mismatch** | Image larger than slide dimensions. | Scale the image (see code snippet) or change slide size via `presentation.SlideSize`. |
| **License exception** | Using trial version without proper activation. | Call `License license = new License(); license.SetLicense("Aspose.Total.lic");` early in `Main`. |

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है, जिसे आप नई कंसोल प्रोजेक्ट में डाल सकते हैं। `YOUR_DIRECTORY` को उस फ़ोल्डर से बदलें जहाँ आपका Excel फ़ाइल स्थित है।

```csharp
using System;
using Aspose.Cells;
using Aspose.Slides;
using System.Drawing;

namespace ExcelToPowerPointDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Load the Excel workbook
            // -----------------------------------------------------------------
            string excelPath = "YOUR_DIRECTORY/ShapesDemo.xlsx";
            Workbook workbook = new Workbook(excelPath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -----------------------------------------------------------------
            // 2️⃣ Set up export options – keep shapes editable
            // -----------------------------------------------------------------
            ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
            {
                OnePagePerSheet = true,
                ExportShapes = true,
                ExportEditableTextBoxes = true,
                Dpi = 300                 // High‑resolution output
            };

            // -----------------------------------------------------------------
            // 3️⃣ Convert worksheet to an image
            // -----------------------------------------------------------------
            WorksheetToImageConverter converter = new WorksheetToImageConverter(worksheet);
            Image sheetImage = converter.ConvertToImage(0, imageOptions);

            // -----------------------------------------------------------------
            // 4️⃣ Create PowerPoint and add the image as a slide
            // -----------------------------------------------------------------
            Presentation presentation = new Presentation();
            ISlide slide = presentation.Slides[0];
            slide.Shapes.AddPictureFrame(
                ShapeType.Rectangle,
                0, 0,
                sheetImage.Width,
                sheetImage.Height,
                sheetImage);

            // -----------------------------------------------------------------
            // 5️⃣ Save the PPTX file
            // -----------------------------------------------------------------
            string pptxPath = "YOUR_DIRECTORY/Result.pptx";
            presentation.Save(pptxPath, SaveFormat.Pptx);

            Console.WriteLine("✅ PowerPoint created successfully at: " + pptxPath);
        }
    }
}
```

**Expected output:**  
प्रोग्राम चलाने पर `✅ PowerPoint created successfully at: YOUR_DIRECTORY/Result.pptx` प्रिंट होगा। PPTX खोलने पर एक ही स्लाइड दिखेगी जो मूल Excel शीट को प्रतिबिंबित करती है, साथ ही एडिटेबल टेक्स्ट बॉक्स होंगे।

## सारांश और अगले कदम

अब आप जानते हैं कि Aspose की शक्तिशाली APIs का उपयोग करके **Excel से PowerPoint कैसे बनाएं**, **वर्कशीट को इमेज के रूप में एक्सपोर्ट करें**, और **प्रेजेंटेशन को PPTX के रूप में सेव करें** जबकि एडिटेबिलिटी बरकरार रहे। यही पैटर्न मल्टी‑शीट वर्कबुक्स पर भी काम करता है—सिर्फ `workbook.Worksheets` पर लूप करें और प्रत्येक के लिए नई स्लाइड जोड़ें।

**अगला क्या एक्सप्लोर करें?**  

- **Batch conversion:** फ़ोल्डर में मौजूद कई Excel फ़ाइलों पर लूप करके प्रत्येक फ़ाइल के लिए एक स्लाइड डेक जेनरेट करें।  
- **Dynamic layouts:** `slide.LayoutSlide` का उपयोग करके प्री‑डिज़ाइन किए गए PowerPoint टेम्प्लेट लागू करें।  
- **Chart‑only export:** “Export Excel chart as picture” स्निपेट को स्लाइड प्लेसहोल्डर्स के साथ मिलाकर एक हल्का डेक बनाएं।  
- **Advanced styling:** Aspose.Slides के माध्यम से कस्टम स्लाइड बैकग्राउंड, ट्रांज़िशन या एनीमेशन लागू करें।

बिना झिझक प्रयोग करें—DPI बदलें, `ShapeType.Ellipse` को सर्कुलर पिक्चर फ्रेम से बदलें, या एक स्लाइड में कई इमेज एम्बेड करें। जब आपके पास प्रोग्रामेटिक कंट्रोल हो तो संभावनाएँ असीमित हैं  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}