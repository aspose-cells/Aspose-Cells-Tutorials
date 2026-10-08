---
category: general
date: 2026-03-22
description: कस्टम नंबर फ़ॉर्मेट एक्सेल ट्यूटोरियल जिसमें दिखाया गया है कि डेटाटेबल
  को एक्सेल में कैसे इम्पोर्ट करें, कॉलम की पृष्ठभूमि का रंग सेट करें, कॉलम को मुद्रा
  के रूप में फ़ॉर्मेट करें और वर्कबुक को xlsx के रूप में सहेजें।
draft: false
keywords:
- custom number format excel
- import datatable to excel
- set column background color
- format column as currency
- save workbook as xlsx
language: hi
og_description: कस्टम नंबर फ़ॉर्मेट एक्सेल ट्यूटोरियल जो आपको डेटा टेबल आयात करने,
  कॉलम की पृष्ठभूमि रंग सेट करने, कॉलम को मुद्रा के रूप में फ़ॉर्मेट करने, और वर्कबुक
  को xlsx के रूप में सहेजने के माध्यम से मार्गदर्शन करता है।
og_title: C# में Excel के लिए कस्टम नंबर फ़ॉर्मेट – चरण‑दर‑चरण गाइड
tags:
- C#
- Excel automation
- Aspose.Cells
- Data export
title: C# में एक्सेल के कस्टम नंबर फ़ॉर्मेट – पूर्ण गाइड
url: /hi/net/excel-custom-number-date-formatting/custom-number-format-excel-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कस्टम नंबर फ़ॉर्मेट एक्सेल – फुल‑स्टैक C# ट्यूटोरियल

क्या आपने कभी सोचा है कि C# से सीधे **custom number format excel** शैली कैसे लागू करें? शायद आपने DataTable को स्प्रेडशीट में डंप करने की कोशिश की होगी, लेकिन केवल साधारण संख्याएँ, कोई रंग नहीं, और कोई मुद्रा फ़ॉर्मेट नहीं देखी। यह एक सामान्य समस्या है—विशेषकर जब आपको स्टेकहोल्डर्स के लिए एक पॉलिश्ड रिपोर्ट चाहिए।

इस गाइड में हम मिलकर इस समस्या को हल करेंगे: आप सीखेंगे कि कैसे **import datatable to excel**, **set column background color**, **format column as currency**, और अंत में **save workbook as xlsx** को एक कस्टम नंबर फ़ॉर्मेट के साथ सहेजें जो आपके आंकड़ों को आकर्षक बनाता है। कोई अस्पष्ट संदर्भ नहीं, सिर्फ एक पूर्ण, चलाने योग्य समाधान जिसे आप अपने प्रोजेक्ट में कॉपी‑पेस्ट कर सकते हैं।

---

## आप क्या बनाएँगे

1. एक `DataTable` प्राप्त करता है (आप स्टब को अपनी क्वेरी से बदल सकते हैं)।  
2. Aspose.Cells (या कोई भी संगत लाइब्रेरी) का उपयोग करके एक नया Excel वर्कबुक बनाता है।  
3. पहले कॉलम पर नीला, बोल्ड फ़ॉन्ट, दूसरे कॉलम पर हल्का‑पीला बैकग्राउंड, और तीसरे कॉलम पर मुद्रा फ़ॉर्मेट (`$#,##0.00`) लागू करता है।  
4. फ़ाइल को `DataTableWithStyleArray.xlsx` के रूप में उस फ़ोल्डर में सहेजता है जिसे आप चुनते हैं।

आप देखेंगे कि प्रत्येक पंक्ति अंतिम Excel फ़ाइल में कैसे योगदान देती है, और हम चर्चा करेंगे कि ये विकल्प रखरखाव और प्रदर्शन के लिए क्यों महत्वपूर्ण हैं।

---

## पूर्वापेक्षाएँ

- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)।  
- Aspose.Cells for .NET (फ्री ट्रायल या लाइसेंस्ड संस्करण)। NuGet के माध्यम से इंस्टॉल करें:

```bash
dotnet add package Aspose.Cells
```

- `DataTable` और C# कंसोल एप्लिकेशन की बुनियादी परिचितता।

---

## चरण 1: स्रोत डेटा को DataTable के रूप में प्राप्त करें

सबसे पहले, हमें निर्यात करने के लिए कुछ डेटा चाहिए। वास्तविक दुनिया के परिदृश्य में आप संभवतः एक रिपॉज़िटरी को कॉल करेंगे या SQL क्वेरी चलाएंगे। उदाहरण के लिए हम एक सरल इन‑मेमोरी टेबल बनाएँगे।

```csharp
using System;
using System.Data;
using Aspose.Cells;

static DataTable GetSampleData()
{
    var table = new DataTable("Sales");
    table.Columns.Add("Product", typeof(string));
    table.Columns.Add("Quantity", typeof(int));
    table.Columns.Add("Revenue", typeof(decimal));

    table.Rows.Add("Widget A", 120, 3450.75m);
    table.Rows.Add("Widget B", 85, 2190.00m);
    table.Rows.Add("Widget C", 60, 1580.40m);

    return table;
}
```

> **यह क्यों महत्वपूर्ण है:** `DataTable` का उपयोग करने से आपको एक तालिका‑आधारित, स्कीमा‑जागरूक स्रोत मिलता है जो Excel पंक्तियों और कॉलमों में साफ़-साफ़ मैप होता है। यह आपको किसी भी डेटासेट के लिए वही एक्सपोर्ट लॉजिक पुनः उपयोग करने देता है बिना कोड को फिर से लिखे।

---

## चरण 2: नया वर्कबुक बनाएं और पहली वर्कशीट प्राप्त करें

अब हम एक Excel वर्कबुक बनाते हैं। `Workbook` क्लास पूरी फ़ाइल का प्रतिनिधित्व करती है; इसका `Worksheets[0]` डिफ़ॉल्ट शीट है जहाँ हम अपना डेटा डालेंगे।

```csharp
// Initialize a fresh workbook
Workbook workbook = new Workbook();

// Grab the first (and only) worksheet
Worksheet worksheet = workbook.Worksheets[0];
```

> **प्रो टिप:** यदि आपको कई शीट्स चाहिए, तो बस `workbook.Worksheets.Add("SheetName")` कॉल करें और प्रत्येक के लिए स्टाइलिंग चरण दोहराएँ।

---

## चरण 3: कॉलम शैलियों को परिभाषित करें – फ़ॉन्ट, बैकग्राउंड, और नंबर फ़ॉर्मेट

Aspose.Cells में स्टाइलिंग `Style` ऑब्जेक्ट्स के माध्यम से की जाती है। हम एक एरे बनाएँगे जहाँ प्रत्येक तत्व DataTable के एक कॉलम से मेल खाता है।

```csharp
// Prepare an array to hold three distinct styles
Style[] columnStyles = new Style[3];

// 1️⃣ First column – blue, bold font
columnStyles[0] = workbook.CreateStyle();
columnStyles[0].Font.Color = System.Drawing.Color.Blue;
columnStyles[0].Font.IsBold = true;

// 2️⃣ Second column – light‑yellow background
columnStyles[1] = workbook.CreateStyle();
columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
columnStyles[1].Pattern = BackgroundType.Solid;

// 3️⃣ Third column – custom currency format (custom number format excel)
columnStyles[2] = workbook.CreateStyle();
columnStyles[2].Custom = "$#,##0.00";
```

> **स्टाइल एरे क्यों?** `ImportDataTable` को एरे पास करने से आप एक ही कॉल में प्रत्येक कॉलम पर अलग शैली लागू कर सकते हैं, जो संक्षिप्त और प्रदर्शन‑उपयुक्त दोनों है। यह यह भी सुनिश्चित करता है कि फ़ॉर्मेटिंग डेटा क्रम के साथ सिंक में रहे।

---

## चरण 4: शैलियों को लागू करते हुए DataTable आयात करें

यह ऑपरेशन का मुख्य भाग है: हम `DataTable` को वर्कशीट में फीड करते हैं, Aspose को हेडर रो शामिल करने के लिए कहते हैं, और अपना `columnStyles` एरे सौंपते हैं।

```csharp
// Import data starting at cell A1 (row 0, column 0)
worksheet.Cells.ImportDataTable(
    GetSampleData(),   // source DataTable
    true,              // include column names as header
    0, 0,              // start row, start column
    columnStyles);     // apply the style array
```

> **आंतरिक रूप से क्या होता है?** Aspose प्रत्येक कॉलम के माध्यम से इटरेट करता है, हेडर लिखता है, फिर प्रत्येक पंक्ति का मान लिखता है। इस दौरान यह एरे से संबंधित `Style` लागू करता है, इसलिए आपको “Product” के लिए नीला हेडर, “Quantity” के लिए पीले‑शेडेड, और “Revenue” कॉलम के लिए सुंदर फ़ॉर्मेटेड मिलता है।

---

## चरण 5: वर्कबुक को XLSX फ़ाइल के रूप में सहेजें

अंत में, हम वर्कबुक को डिस्क पर सहेजते हैं। `Save` मेथड फ़ाइल एक्सटेंशन के आधार पर स्वचालित रूप से XLSX फ़ॉर्मेट चुनता है।

```csharp
// Choose a folder that exists on your machine
string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";

// Ensure the directory exists (optional safety check)
System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);

// Save the workbook
workbook.Save(outputPath);
Console.WriteLine($"Workbook saved to {outputPath}");
```

> **टिप:** यदि आपको फ़ाइल को स्ट्रीम करना है (जैसे वेब API के लिए), तो फ़ाइल पाथ के बजाय `workbook.Save(stream, SaveFormat.Xlsx)` का उपयोग करें।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा प्रोग्राम है जिसे आप एक नए कंसोल प्रोजेक्ट में पेस्ट कर सकते हैं। यह जैसा है वैसा ही कंपाइल और रन होता है, और एक स्टाइल्ड Excel फ़ाइल बनाता है।

```csharp
using System;
using System.Data;
using Aspose.Cells;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Get data
            DataTable dataTable = GetSampleData();

            // Step 2 – Create workbook & worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Step 3 – Prepare column styles
            Style[] columnStyles = new Style[3];

            // Font style for first column (blue, bold)
            columnStyles[0] = workbook.CreateStyle();
            columnStyles[0].Font.Color = System.Drawing.Color.Blue;
            columnStyles[0].Font.IsBold = true;

            // Background style for second column (light yellow)
            columnStyles[1] = workbook.CreateStyle();
            columnStyles[1].ForegroundColor = System.Drawing.Color.LightYellow;
            columnStyles[1].Pattern = BackgroundType.Solid;

            // Currency format for third column (custom number format excel)
            columnStyles[2] = workbook.CreateStyle();
            columnStyles[2].Custom = "$#,##0.00";

            // Step 4 – Import data with styles
            worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, columnStyles);

            // Step 5 – Save as XLSX
            string outputPath = @"C:\Temp\DataTableWithStyleArray.xlsx";
            System.IO.Directory.CreateDirectory(System.IO.Path.GetDirectoryName(outputPath)!);
            workbook.Save(outputPath);

            Console.WriteLine($"Workbook saved to {outputPath}");
        }

        // Helper method to build a demo DataTable
        static DataTable GetSampleData()
        {
            var table = new DataTable("Sales");
            table.Columns.Add("Product", typeof(string));
            table.Columns.Add("Quantity", typeof(int));
            table.Columns.Add("Revenue", typeof(decimal));

            table.Rows.Add("Widget A", 120, 3450.75m);
            table.Rows.Add("Widget B", 85, 2190.00m);
            table.Rows.Add("Widget C", 60, 1580.40m);

            return table;
        }
    }
}
```

### अपेक्षित परिणाम

`DataTableWithStyleArray.xlsx` खोलने पर आपको दिखेगा:

| **Product** (नीला, बोल्ड) | **Quantity** (हल्का‑पीला) | **Revenue** (मुद्रा) |
|----------------------------|----------------------------|----------------------|
| Widget A                   | 120                        | $3,450.75            |
| Widget B                   | 85                         | $2,190.00            |
| Widget C                   | 60                         | $1,580.40            |

आपके द्वारा निर्दिष्ट **custom number format excel** (`$#,##0.00`) सुनिश्चित करता है कि प्रत्येक revenue सेल में डॉलर साइन, हजारों विभाजक, और दो दशमलव स्थान दिखें—बिल्कुल वही जो फाइनेंस टीमें अपेक्षा करती हैं।

---

## अक्सर पूछे जाने वाले प्रश्न और किनारे के मामले

### क्या मैं इसे किसी अलग Excel लाइब्रेरी के साथ उपयोग कर सकता हूँ?

बिल्कुल। अवधारणा—प्रति कॉलम एक शैली बनाना और आयात के दौरान लागू करना—EPPlus, ClosedXML, या NPOI में भी लागू होती है। API कॉल्स अलग हो सकते हैं, लेकिन पैटर्न वही रहता है।

### यदि मेरे DataTable में शैलियों से अधिक कॉलम हैं तो क्या होगा?

Aspose उन सभी कॉलमों पर डिफ़ॉल्ट शैली लागू करेगा जिनके लिए `columnStyles` एरे में मेल खाने वाला एंट्री नहीं है। आश्चर्य से बचने के लिए, एरे का आकार `dataTable.Columns.Count` के बराबर रखें या लूप में डायनामिक रूप से शैलियाँ जेनरेट करें।

### तिथियों के लिए कस्टम नंबर फ़ॉर्मेट कैसे सेट करें?

सिर्फ `style.Custom = "dd‑mm‑yyyy"` सेट करें (या कोई भी वैध Excel फ़ॉर्मेट स्ट्रिंग)। वही एरे‑आधारित तरीका तिथियों, प्रतिशत या वैज्ञानिक नोटेशन के लिए भी काम करता है।

### आयात के बाद कॉलमों को ऑटो‑साइज़ करने का तरीका है क्या?

हाँ—आयात के बाद `worksheet.AutoFitColumns();` कॉल करें। यह सेल सामग्री के आधार पर तेज़ चौड़ाई गणना करता है।

### बड़े डेटा सेट (100k+ पंक्तियाँ) के बारे में क्या?

`ImportDataTable` बल्क ऑपरेशन्स के लिए ऑप्टिमाइज़्ड है, लेकिन आप मेमोरी लिमिट तक पहुँच सकते हैं। ऐसे में, पंक्तियों को मैन्युअली `Cells[i, j].PutValue(...)` से स्ट्रीम करने और ओवरहेड कम करने के लिए एक ही `Style` ऑब्जेक्ट को पुनः उपयोग करने पर विचार करें।

---

## प्रो टिप्स और सामान्य गलतियाँ

- **हर्ड‑कोडिंग पाथ्स** से बचें उत्पादन कोड में; `Environment.GetFolderPath` या कॉन्फ़िगरेशन सेटिंग्स का उपयोग करें।  
- **वर्कबुक को डिस्पोज़ करें** यदि आप एक लंबी‑चलने वाली सेवा में हैं—नेटीव रिसोर्सेज़ को मुक्त करने के लिए इसे `using` ब्लॉक में रखें।  
- **कल्चर‑स्पेसिफिक सेपरेटर** पर ध्यान दें। कस्टम फ़ॉर्मेट `$#,##0.00` OS लोकेल की परवाह किए बिना दशमलव सेपरेटर के रूप में पीरियड लागू करता है, जो आमतौर पर वित्तीय रिपोर्टों के लिए वांछित होता है।  
- **System.Drawing** (या .NET Core पर `System.Drawing.Common`) को संदर्भित करना याद रखें, जो स्टाइलिंग में उपयोग किए गए कलर स्ट्रक्ट्स के लिए आवश्यक है।  
- **विभिन्न Excel संस्करणों पर आउटपुट का परीक्षण करें**; पुराने संस्करण कुछ कस्टम फ़ॉर्मेट को थोड़ा अलग तरीके से व्याख्या कर सकते हैं।

---

## निष्कर्ष

हमने वह सब कवर किया है जो आपको C# से **custom number format excel** फ़ाइलें बनाने के लिए चाहिए: `DataTable` से डेटा निकालना, **import datatable to excel**, **set column background color** लागू करना, **format column as currency** का उपयोग करना, और अंत में **save workbook as x

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}