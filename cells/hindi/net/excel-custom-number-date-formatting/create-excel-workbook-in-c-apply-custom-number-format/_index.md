---
category: general
date: 2026-05-23
description: C# में एक्सेल वर्कबुक बनाएं और कस्टम नंबर फ़ॉर्मेट लागू करना, प्रोग्रामेटिकली
  सेल स्टाइल सेट करना, सेल को वैज्ञानिक नोटेशन में फ़ॉर्मेट करना, फिर वर्कबुक को xlsx
  में सहेजना सीखें।
draft: false
keywords:
- create excel workbook
- apply custom number format
- format cell scientific notation
- set cell style programmatically
- save workbook to xlsx
language: hi
og_description: C# में जल्दी से एक्सेल वर्कबुक बनाएं। कस्टम नंबर फ़ॉर्मेट लागू करना,
  प्रोग्रामेटिकली सेल्स को स्टाइल करना, वैज्ञानिक संकेतन को फ़ॉर्मेट करना, और xlsx
  में सहेजना सीखें।
og_title: C# में Excel वर्कबुक बनाएं – कस्टम नंबर फ़ॉर्मेट लागू करें
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Create excel workbook in C# and learn how to apply custom number format,
    set cell style programmatically, format cell scientific notation, then save workbook
    to xlsx.
  headline: Create Excel Workbook in C# – Apply Custom Number Format
  type: TechArticle
tags:
- C#
- Excel
- Aspose.Cells
- Automation
title: C# में Excel वर्कबुक बनाएं – कस्टम नंबर फ़ॉर्मेट लागू करें
url: /hi/net/excel-custom-number-date-formatting/create-excel-workbook-in-c-apply-custom-number-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Excel वर्कबुक बनाएं – कस्टम नंबर फ़ॉर्मेट लागू करें

C# में Excel वर्कबुक बनाना आपके सोच से आसान है। इस गाइड में हम आपको कस्टम नंबर फ़ॉर्मेट लागू करने, एक सेल को वैज्ञानिक नोटेशन में फ़ॉर्मेट करने, प्रोग्रामेटिकली सेल स्टाइल सेट करने, और अंत में वर्कबुक को xlsx फ़ाइल में सहेजने की प्रक्रिया दिखाएंगे।

यदि आपने कभी खाली स्प्रेडशीट को देखा है और सोचा है कि पूरे काम को कैसे ऑटोमेट किया जाए—डेटा भरने से लेकर नंबरों को बिल्कुल उसी तरह दिखाने तक—तो यह ट्यूटोरियल आपके लिए है। अंत तक आप एक पूरी‑फ़ंक्शनल Excel फ़ाइल बना पाएँगे जिसे आप किसी भी स्प्रेडशीट प्रोग्राम में खोल सकते हैं, और आप समझेंगे **क्यों** प्रत्येक कदम महत्वपूर्ण है, न कि सिर्फ **कैसे** कोड लिखना है।

## आपको क्या चाहिए

- **.NET 6+** (या कोई भी हालिया .NET Framework जो लाइब्रेरी को सपोर्ट करता हो)  
- **Aspose.Cells for .NET** (या कोई अन्य API जो `Workbook`, `Cell`, और `CellFormat` क्लासेज़ को एक्सपोज़ करता हो)  
- थोड़ा‑बहुत C# का अनुभव – यदि आप `Console.WriteLine` लिख सकते हैं, तो आप तैयार हैं।  

कोई अतिरिक्त कॉन्फ़िगरेशन फ़ाइलें नहीं, कोई COM इंटरऑप नहीं, और बिल्कुल भी मैन्युअल Excel इंस्टॉलेशन की ज़रूरत नहीं।

---

## Excel वर्कबुक बनाएं – वर्कबुक ऑब्जेक्ट को इनिशियलाइज़ करें

सबसे पहले हमें एक खाली वर्कबुक बनानी होगी। `Workbook` क्लास को आप एक खाली कैनवास की तरह समझें, जिस पर आप पंक्तियाँ, कॉलम और स्टाइल पेंट करेंगे।

```csharp
using Aspose.Cells;   // Make sure the Aspose.Cells namespace is referenced

// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

बस इतना ही—एक लाइन और आपके पास मेमोरी में एक नई Excel फ़ाइल है। `Workbook` कंस्ट्रक्टर डिफ़ॉल्ट वर्कशीट कलेक्शन बनाता है, इसलिए आप तुरंत डेटा जोड़ना शुरू कर सकते हैं।

> **Pro tip:** यदि आपको कई शीट्स चाहिए, तो आप सेल्स भरना शुरू करने से पहले `workbook.Worksheets.Add()` कॉल कर सकते हैं।

![Excel वर्कबुक बनाने का उदाहरण](image-placeholder.png "Excel वर्कबुक स्क्रीनशॉट")

*Image alt text: Excel वर्कबुक बनाने का उदाहरण दिखाता है कि IDE में एक खाली Excel शीट है।*

## सेल पर कस्टम नंबर फ़ॉर्मेट लागू करें

अब वर्कबुक मौजूद है, चलिए **A1** सेल में एक नंबर डालते हैं और उसे कस्टम फ़ॉर्मेट देते हैं। कस्टम नंबर फ़ॉर्मेट आपको यह नियंत्रित करने देते हैं कि नंबर कैसे दिखेंगे—करेंसी, प्रतिशत, डेट, या हमारे मामले में वैज्ञानिक नोटेशन।

```csharp
// Step 2: Grab the first worksheet and the cell at A1 (row 0, column 0)
Worksheet sheet = workbook.Worksheets[0];
Cell cell = sheet.Cells[0, 0];

// Step 3: Insert a numeric value
cell.PutValue(12345.6789);

// Step 4: Retrieve the current style so we can modify its Number format
Style style = cell.GetStyle();

// Step 5: Define a custom scientific notation format with two decimal places
style.Custom = "0.00E+00";   // This is the “apply custom number format” part

// Step 6: Push the modified style back onto the cell
cell.SetStyle(style);
```

पहले स्टाइल को क्यों खींचते हैं? क्योंकि `Cell` ऑब्जेक्ट एक **Style** ऑब्जेक्ट रखता है जिसमें फ़ॉन्ट, बॉर्डर, अलाइनमेंट और नंबर फ़ॉर्मेटिंग सभी एक जगह होते हैं। `Custom` प्रॉपर्टी को एडिट करके हम Excel को बताते हैं, “इस वैल्यू को दो दशमलव के साथ वैज्ञानिक नोटेशन में दिखाओ।”

> **Common question:** *क्या मैं कस्टम फ़ॉर्मेट की बजाय बिल्ट‑इन फ़ॉर्मेट इस्तेमाल कर सकता हूँ?*  
> हाँ—बिल्ट‑इन वैज्ञानिक फ़ॉर्मेट के लिए `style.Number = 10` सेट करें, लेकिन कस्टम स्ट्रिंग आपको दशमलव स्थानों पर सटीक नियंत्रण देती है।

## प्रोग्रामेटिकली सेल स्टाइल सेट करें (नंबर फ़ॉर्मेट से आगे)

अक्सर आपको सिर्फ नंबर फ़ॉर्मेट से अधिक चाहिए। चलिए सेल को बोल्ड फ़ॉन्ट और हल्के ग्रे बैकग्राउंड के साथ हाइलाइट करते हैं।

```csharp
// Optional: Enhance the cell appearance
style.Font.IsBold = true;
style.ForegroundColor = System.Drawing.Color.LightGray;
style.Pattern = BackgroundType.Solid;

// Re‑apply the enriched style
cell.SetStyle(style);
```

ध्यान दें कि हम वही `style` ऑब्जेक्ट फिर से उपयोग कर रहे हैं जिसे हमने पहले ट्यून किया था। यही है **प्रोग्रामेटिकली सेल स्टाइल सेट करने** की खूबी—आप स्टाइल को एक बार फ़ेच करते हैं, ज़रूरी प्रॉपर्टीज़ बदलते हैं, और फिर वापस लिखते हैं। ऑब्जेक्ट को फिर से बनाने या पहले सेट किए गए नंबर फ़ॉर्मेट को खोने की ज़रूरत नहीं।

## सेल को वैज्ञानिक नोटेशन में फ़ॉर्मेट करें (एज‑केस हैंडलिंग)

यदि आप बहुत बड़े या बहुत छोटे नंबरों से निपट रहे हैं, तो वैज्ञानिक नोटेशन एक लाइफ़सेवर है। हमने जो कस्टम फ़ॉर्मेट (`0.00E+00`) इस्तेमाल किया है, वह दशमलव के बाद दो अंक सुनिश्चित करता है और एक्सपोनेंट के लिए प्लस साइन फोर्स करता है। यहाँ एक त्वरित चेक है:

```csharp
// Verify the format by inserting another extreme value
Cell extraCell = sheet.Cells[1, 0]; // B2
extraCell.PutValue(0.00001234);
extraCell.SetStyle(style); // Reuse the same style with scientific notation
```

जब आप परिणामी फ़ाइल खोलेंगे, तो B2 `1.23E-05` के रूप में दिखेगा, जिससे पुष्टि होती है कि **सेल को वैज्ञानिक नोटेशन में फ़ॉर्मेट** निर्देश बड़े और छोटे दोनों नंबरों के लिए काम करता है।

## वर्कबुक को XLSX में सहेजें

सारा मज़ा तब रुक जाता है जब आप वास्तव में फ़ाइल को डिस्क पर लिखते हैं। `Save` मेथड भारी काम संभालता है, इन‑मेमोरी प्रतिनिधित्व को एक सही `.xlsx` पैकेज में बदलता है।

```csharp
// Step 7: Persist the workbook
string outputPath = @"C:\Temp\CustomFormatted.xlsx";
workbook.Save(outputPath, SaveFormat.Xlsx);
```

यह लाइन **वर्कबुक को XLSX में सहेजने** का लक्ष्य पूरा करती है। यदि डायरेक्टरी मौजूद नहीं है, तो `Save` एक एक्सेप्शन फेंकेगा—इसलिए फ़ोल्डर को पहले बना लें या कॉल को try/catch ब्लॉक में रैप करें।

```csharp
try
{
    workbook.Save(outputPath, SaveFormat.Xlsx);
    Console.WriteLine($"Workbook saved successfully to {outputPath}");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
}
```

अब आपके पास एक तैयार‑शेयर करने योग्य Excel फ़ाइल है जिसमें सुंदर फ़ॉर्मेट किया गया वैज्ञानिक नंबर, बोल्ड स्टाइल, और हल्का ग्रे बैकग्राउंड है।

## पूर्ण कार्यशील उदाहरण

नीचे पूरा, कॉपी‑पेस्ट‑रेडी प्रोग्राम है जो हर हिस्से को जोड़ता है। यह एक कंसोल ऐप के रूप में कंपाइल होता है, लेकिन आप इस लॉजिक को किसी भी C# प्रोजेक्ट में डाल सकते हैं।

```csharp
using System;
using Aspose.Cells;
using System.Drawing;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // 2️⃣ Access the first worksheet and target cell A1
        Worksheet sheet = workbook.Worksheets[0];
        Cell cell = sheet.Cells[0, 0];

        // 3️⃣ Insert a numeric value
        cell.PutValue(12345.6789);

        // 4️⃣ Retrieve and customize the cell style
        Style style = cell.GetStyle();
        style.Custom = "0.00E+00";               // apply custom number format (scientific)
        style.Font.IsBold = true;               // set cell style programmatically
        style.ForegroundColor = Color.LightGray;
        style.Pattern = BackgroundType.Solid;

        // 5️⃣ Apply the style back to the cell
        cell.SetStyle(style);

        // 6️⃣ Add another example to prove scientific notation works for tiny numbers
        Cell tinyCell = sheet.Cells[1, 0]; // B2
        tinyCell.PutValue(0.00001234);
        tinyCell.SetStyle(style);

        // 7️⃣ Save the workbook to an XLSX file
        string outputPath = @"C:\Temp\CustomFormatted.xlsx";
        try
        {
            workbook.Save(outputPath, SaveFormat.Xlsx);
            Console.WriteLine($"Workbook saved successfully to {outputPath}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Failed to save workbook: {ex.Message}");
        }
    }
}
```

**Expected outcome:** `CustomFormatted.xlsx` खोलें और आप देखेंगे:

| A1               | B2            |
|------------------|---------------|
| 1.23E+04         | 1.23E-05      |

दोनों सेल्स बोल्ड हैं, हल्का ग्रे फ़िल है, और नंबर दो दशमलव स्थानों के साथ वैज्ञानिक नोटेशन में दिखते हैं।

---

## समापन

हमने अभी **C# से Excel वर्कबुक बनाना**, **कस्टम नंबर फ़ॉर्मेट लागू करना**, **सेल को वैज्ञानिक नोटेशन में फ़ॉर्मेट करना**, **प्रोग्रामेटिकली सेल स्टाइल सेट करना**, और **वर्कबुक को XLSX में सहेजना**—सभी कुछ लाइनों के कोड में किया। यह तरीका स्केलेबल है: बस पंक्तियों पर लूप लगाएँ, `style` ऑब्जेक्ट को क्लोन करें, और आप सेकंडों में पूरी‑स्टाइल्ड रिपोर्ट बना लेंगे।

### आगे क्या?

- **डायनामिक फ़ॉर्मेटिंग:** वैल्यू की माप के आधार पर फ़ॉर्मेट बदलें (जैसे, करंसी बनाम प्रतिशत)।  
- **एकाधिक शीट्स:** `workbook.Worksheets.Add("Summary")` का उपयोग करके डैशबोर्ड बनाएं।  
- **एडवांस्ड स्टाइलिंग:** बॉर्डर, कंडीशनल फ़ॉर्मेटिंग, और डेटा वैलिडेशन

## संबंधित ट्यूटोरियल

- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [Create Save Excel Workbook Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)
- [Create Save Excel Workbook Pdf Aspnet Aspose Cells](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}