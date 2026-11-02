---
category: general
date: 2026-09-27
description: Excel में प्रिंट एरिया सेट करें और चयनित सेल्स की PNG छवियों को निर्यात
  करना सीखें। यह गाइड रेंज को इमेज के रूप में सहेजने और वर्कशीट में चित्र जोड़ने को
  भी कवर करता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set print area excel
- how to export png
- save range as image
- add picture to worksheet
- export selected cells image
language: hi
lastmod: 2026-09-27
og_description: Excel में प्रिंट एरिया सेट करें और Aspose.Cells के साथ PNG निर्यात
  करें। इस चरण‑दर‑चरण गाइड का पालन करके रेंज को इमेज के रूप में सहेजें और वर्कशीट
  में चित्र जोड़ें।
og_image_alt: Screenshot showing set print area excel and exported PNG file
og_title: Excel में प्रिंट एरिया सेट करें – C# में PNG निर्यात करें
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Set print area in Excel and learn how to export PNG images of selected
    cells. This guide also covers saving range as image and adding picture to worksheet.
  headline: How to set print area in Excel and export PNG
  type: TechArticle
tags:
- Excel automation
- C#
- Aspose.Cells
title: Excel में प्रिंट एरिया कैसे सेट करें और PNG निर्यात करें
url: /hi/net/rendering-and-export/how-to-set-print-area-in-excel-and-export-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में प्रिंट एरिया कैसे सेट करें और PNG निर्यात करें

यदि आपको इमेज बनाने से पहले **set print area excel** सेट करने की आवश्यकता है, तो यह गाइड आपको ठीक-ठीक बताता है कि इसे कैसे करें। आप सीखेंगे **how to export png** फ़ाइलें एक विशिष्ट रेंज से, **save range as image**, और **add picture to worksheet** को एकल, दोहराने योग्य वर्कफ़्लो में।

Excel के साथ प्रोग्रामेटिकली काम करना अक्सर इसका मतलब होता है कि आप केवल कोशिकाओं का एक उपसमुच्चय—जैसे पिवट टेबल या चार्ट—को इमेज बनाना चाहते हैं। पहले प्रिंट एरिया निर्धारित करके, आप सुनिश्चित करते हैं कि निर्यात किया गया PNG बिल्कुल वही कोशिकाएँ रखे जो आप चाहते हैं, न अधिक न कम। यह ट्यूटोरियल आपको हर चरण से ले जाता है, वर्कबुक लोड करने से लेकर अंतिम PNG फ़ाइल सहेजने तक, और बताता है कि प्रत्येक सेटिंग क्यों महत्वपूर्ण है।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण स्थापित हो  
* Visual Studio 2022 (या कोई भी C# IDE)  
* The **Aspose.Cells for .NET** NuGet पैकेज (`Install-Package Aspose.Cells`)  
* एक Excel फ़ाइल (`input.xlsx`) जो ज्ञात डायरेक्टरी में स्थित हो  

इन आवश्यकताओं से सुनिश्चित होता है कि कोड अतिरिक्त कॉन्फ़िगरेशन के बिना चलेगा।

## चरण 1: वह वर्कबुक लोड करें जिसके साथ आप काम करना चाहते हैं

```csharp
using Aspose.Cells;
using System.Drawing.Imaging;

// Load the workbook from disk
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

`Workbook` क्लास पूरे Excel फ़ाइल का प्रतिनिधित्व करती है। इसे पहले लोड करने से आपको वर्कशीट्स, सेल्स, और पेज‑सेटअप विकल्पों तक पहुंच मिलती है।

## चरण 2: लक्ष्य रेंज के लिए **Set print area excel** सेट करें

```csharp
// Define the range you want to capture
string printArea = "A1:G20";

// Apply the range as the print area on the first worksheet
workbook.Worksheets[0].PageSetup.PrintArea = printArea;
```

**print area** सेट करने से Excel (और Aspose.Cells) को पता चलता है कि कौन से सेल्स प्रिंटेबल पेज में आते हैं। जब आप बाद में शीट को इमेज के रूप में निर्यात करते हैं, तो केवल यह क्षेत्र रेंडर होता है, जो एक साफ़ **export selected cells image** के लिए आवश्यक है।

## चरण 3: इमेज निर्यात विकल्प कॉन्फ़िगर करें – **how to export png**

```csharp
ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
{
    ImageFormat = ImageFormat.Png,   // PNG ensures lossless quality
    OnePagePerSheet = true           // Export the defined print area as a single page
};
```

`ImageOrPrintOptions` आउटपुट फ़ॉर्मेट को नियंत्रित करता है। `ImageFormat.Png` चुनने से आप एक हाई‑रेज़ोल्यूशन, ट्रांसपेरेंट‑बैकग्राउंड इमेज सुनिश्चित करते हैं जो वेब और डेस्कटॉप दोनों संदर्भों में अच्छी तरह काम करती है।

## चरण 4: परिभाषित रेंज से एक चित्र बनाएं और **add picture to worksheet**

```csharp
// Create a picture object from the selected range
Picture picture = workbook.Worksheets[0].Pictures.Add(
    0,                                     // top‑left row index where the picture will be placed
    0,                                     // top‑left column index where the picture will be placed
    workbook.Worksheets[0].Cells.CreateRange(printArea));
```

`Pictures.Add` मेथड एक नया चित्र वर्कशीट में डालता है। चरण 2 में बनाई गई रेंज पास करके, आप **save range as image** सीधे शीट पर सहेजते हैं, जो तब उपयोगी होता है जब आपको बाद में वर्कबुक के अन्य भागों में चित्र का संदर्भ देना हो।

## चरण 5: **Save the picture as an image file** – **export selected cells image** वर्कफ़्लो को पूरा करना

```csharp
// Save the picture to disk as a PNG file
picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);
```

`Save` को कॉल करने से चित्र फ़ाइल सिस्टम में Step 3 में परिभाषित विकल्पों का उपयोग करके लिखा जाता है। परिणामी `selected_range.png` बिल्कुल वही सेल्स रखता है जो **set print area excel** कमांड द्वारा परिभाषित किए गए थे।

## पूर्ण, चलाने योग्य उदाहरण

सभी भागों को एक साथ जोड़ने से आपको एक कॉम्पैक्ट प्रोग्राम मिलता है जिसे आप किसी भी कंसोल एप्लिकेशन में डाल सकते हैं:

```csharp
using System;
using Aspose.Cells;
using System.Drawing.Imaging;

class ExportExcelRangeAsPng
{
    static void Main()
    {
        // 1️⃣ Load the workbook
        Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

        // 2️⃣ Set print area excel
        string printArea = "A1:G20";
        workbook.Worksheets[0].PageSetup.PrintArea = printArea;

        // 3️⃣ Configure how to export png
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions
        {
            ImageFormat = ImageFormat.Png,
            OnePagePerSheet = true
        };

        // 4️⃣ Add picture to worksheet (save range as image)
        Picture picture = workbook.Worksheets[0].Pictures.Add(
            0,
            0,
            workbook.Worksheets[0].Cells.CreateRange(printArea));

        // 5️⃣ Export selected cells image
        picture.Save(@"YOUR_DIRECTORY\selected_range.png", imageOptions);

        Console.WriteLine("PNG exported successfully to YOUR_DIRECTORY\\selected_range.png");
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर यह प्रिंट करता है:

```
PNG exported successfully to YOUR_DIRECTORY\selected_range.png
```

और आपको एक `selected_range.png` फ़ाइल मिलेगी जिसमें केवल `input.xlsx` की कोशिकाएँ A1 से G20 तक दिखाए गए हैं।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| निर्यात की गई इमेज पूरी शीट को दिखाती है | कोई प्रिंट एरिया परिभाषित नहीं किया गया | सुनिश्चित करें कि चित्र बनाने से पहले **set print area excel** सुनिश्चित करें |
| PNG धुंधला है | डिफ़ॉल्ट DPI कम है | `imageOptions.DpiX` और `imageOptions.DpiY` को उच्च मान (जैसे 300) पर सेट करें |
| फ़ाइल नहीं मिली त्रुटि | गलत डायरेक्टरी पाथ | `Path.Combine` का उपयोग करें या फ़ोल्डर मौजूद है यह दोबारा जांचें |
| चित्र ऑफ़सेट दिखता है | गलत पंक्ति/स्तंभ इंडेक्स | `Pictures.Add` के पहले दो पैरामीटर वह टॉप‑लेफ़्ट सेल होते हैं जहाँ चित्र रखा जाता है; साफ़ निर्यात के लिए उन्हें `0,0` पर रखें |

## प्रो टिप: एक रन में कई रेंज निर्यात करें

यदि आपको कई क्षेत्रों के लिए **export selected cells image** चाहिए, तो लूप के अंदर चरण 2‑5 दोहराएँ, प्रत्येक इटरेशन में `printArea` बदलें। प्रत्येक चित्र को एक अनूठा फ़ाइल नाम दें, अन्यथा बाद का सेव पहले की फ़ाइल को ओवरराइट कर देगा।

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells का उपयोग करके **set print area excel**, **how to export png** कॉन्फ़िगर करना, **save range as image**, और **add picture to worksheet** कैसे किया जाता है। यह एंड‑टू‑एंड समाधान आपको किसी भी सेल ब्लॉक को कुछ ही C# कोड लाइनों से हाई‑क्वालिटी PNG में बदलने देता है।

आगे, आप खोज सकते हैं:

* निर्यात किए गए PNG में बॉर्डर या वॉटरमार्क जोड़ना (स्टाइलिंग के साथ *add picture to worksheet* खोजें)
* प्रिंटेबल रिपोर्ट के लिए सीधे PDF में निर्यात करना (*export selected cells image* → PDF वर्कफ़्लो)
* बैच जॉब में कई वर्कबुक्स के लिए प्रक्रिया को ऑटोमेट करना

विभिन्न रेंज, DPI सेटिंग्स, या इमेज फ़ॉर्मेट के साथ प्रयोग करने में संकोच न करें ताकि आपके प्रोजेक्ट की जरूरतों को पूरा किया जा सके। कोडिंग का आनंद लें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोचेज़ का अन्वेषण करने में मदद करती हैं।

- [Excel में प्रिंट एरिया सेट करें और PowerPoint में निर्यात करें – चरण‑दर‑चरण गाइड](/cells/english/net/converting-excel-files-to-other-formats/set-print-area-in-excel-and-export-to-powerpoint-step-by-ste/)
- [Aspose.Cells Java के साथ Excel प्रिंट एरिया को HTML में निर्यात करें](/cells/english/java/workbook-operations/export-excel-print-area-html-aspose-cells-java/)
- [Aspose.Cells for .NET का उपयोग करके Excel में प्रिंट एरिया कैसे सेट करें](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}