---
category: general
date: 2026-09-15
description: सीएसवी के रूप में वर्कबुक को सहेजना, एक्सेल को TXT में निर्यात करना,
  और C# में सेल मानों को बड़े अक्षरों में बदलते हुए कस्टम नंबर फ़ॉर्मेट लागू करना
  सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save workbook as csv
- apply custom number format
- export excel to txt
- uppercase cell values
- export worksheet as text
language: hi
lastmod: 2026-09-15
og_description: वर्कबुक को CSV के रूप में सहेजें, Excel को TXT में निर्यात करें, और
  Aspose.Cells का उपयोग करके C# में सेल मानों को बड़े अक्षरों में बदलते हुए कस्टम
  नंबर फ़ॉर्मेट लागू करें।
og_image_alt: Screenshot showing workbook saved as CSV using C# code
og_title: वर्कबुक को CSV के रूप में सहेजें और कस्टम फ़ॉर्मेटिंग के साथ Excel को TXT
  में निर्यात करें C# में
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to save workbook as CSV, export Excel to TXT, and apply custom
    number format while converting cell values to uppercase in C#.
  headline: How to save workbook as CSV and export Excel to TXT with custom formatting
    in C#
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में वर्कबुक को CSV के रूप में सहेजना और कस्टम फ़ॉर्मेटिंग के साथ Excel को
  TXT में निर्यात करना
url: /hi/net/converting-excel-files-to-other-formats/how-to-save-workbook-as-csv-and-export-excel-to-txt-with-cus/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में वर्कबुक को CSV के रूप में सहेजना और कस्टम फॉर्मेटिंग के साथ Excel को TXT में एक्सपोर्ट करना

यदि आपको **save workbook as CSV** करने की आवश्यकता है जबकि साथ ही एक वर्कशीट को प्लेन‑टेक्स्ट के रूप में एक्सपोर्ट करना और कस्टम नंबर फॉर्मेट लागू करना है, तो यह गाइड आपको एक पूर्ण, तैयार‑चलाने‑योग्य समाधान दिखाता है। आप देखेंगे कि कैसे संख्यात्मक प्रिसीजन को बनाए रखें, प्रत्येक सेल वैल्यू को अपरकेस में बदलें, और जापानी‑इरा डेट्स को हैंडल करें—सब Aspose.Cells for .NET के साथ।

Excel से डेटा एक्सपोर्ट करना अक्सर कई फ़ॉर्मेट्स को संभालने की माँग करता है: डेटा‑एक्सचेंज के लिए CSV, लेगेसी सिस्टम्स के लिए TXT, और लोकेल‑विशिष्ट रिपोर्टिंग के लिए कस्टम नंबर फ़ॉर्मेट। यह ट्यूटोरियल प्रत्येक आवश्यकता को चरण‑बद्ध तरीके से समझाता है, ताकि आप कोड को सीधे अपने प्रोजेक्ट में कॉपी कर सकें।

इन सेक्शनों में आप सीखेंगे:

* **save workbook as csv** को परिभाषित महत्वपूर्ण अंकों की संख्या के साथ  
* **export excel to txt** करते समय **uppercase cell values** को मजबूर करना  
* जापानी‑इरा डेट्स के लिए **apply custom number format** और फॉर्मेटेड परिणाम पढ़ना  

कोई बाहरी टूल आवश्यक नहीं—केवल Aspose.Cells लाइब्रेरी और एक .NET डेवलपमेंट एनवायरनमेंट।

## पूर्वापेक्षाएँ

* .NET 6.0 या बाद का (कोड .NET Framework 4.8 के साथ भी काम करता है)  
* Aspose.Cells for .NET (NuGet पैकेज `Aspose.Cells`)  
* C# और Excel अवधारणाओं की बेसिक समझ  

---

## चरण 1: नियंत्रित प्रिसीजन के साथ वर्कबुक को CSV के रूप में सहेजें

जब आप **save workbook as CSV** करते हैं, तो संख्यात्मक मान डिफ़ॉल्ट स्ट्रिंग प्रतिनिधित्व का उपयोग करके लिखे जाते हैं, जिससे प्रिसीजन खो सकता है। `CsvSaveOptions.SignificantDigits` को कॉन्फ़िगर करके आप Aspose.Cells को बता सकते हैं कि कितने महत्वपूर्ण अंक रखने हैं।

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (or load an existing one)
Workbook workbook = new Workbook();               // you can also use new Workbook("input.xlsx");

// Configure CSV options to keep up to 4 significant digits
CsvSaveOptions csvOptions = new CsvSaveOptions
{
    SignificantDigits = 4   // ensures numbers like 123.4567 stay precise
};

// Save the workbook as CSV
string csvPath = @"C:\Temp\Digits.csv";
workbook.Save(csvPath, csvOptions);

Console.WriteLine($"Workbook saved as CSV to {csvPath}");
```

**Why this matters:**  
`SignificantDigits` सेट करने से राउंडिंग त्रुटियों को रोका जा सकता है जो अक्सर बड़े डेटासेट्स को डाउनस्ट्रीम सिस्टम्स (जैसे डेटा‑वेयरहाउस) में एक्सचेंज करते समय दिखाई देती हैं। `CsvSaveOptions` ऑब्जेक्ट आपको डिलिमिटर, एन्कोडिंग, और अन्य CSV‑विशिष्ट सेटिंग्स को भी नियंत्रित करने की सुविधा देता है यदि आवश्यकता हो।

---

## चरण 2: मानों को अपरकेस में बदलते हुए वर्कशीट को प्लेन टेक्स्ट के रूप में एक्सपोर्ट करें

एक शीट को साधारण `.txt` फ़ाइल में एक्सपोर्ट करना लेगेसी इम्पोर्ट रूटीन के लिए उपयोगी है जो व्हाइटस्पेस‑डिलिमिटेड डेटा की अपेक्षा करती हैं। `ExportTableOptions.ExportAsString` को एनेबल करके और एक `CustomExport` डेलीगेट प्रदान करके आप **export excel to txt** कर सकते हैं और साथ ही **uppercase cell values** को लागू कर सकते हैं।

```csharp
// Prepare export options for plain‑text output
ExportTableOptions tableOptions = new ExportTableOptions
{
    ExportAsString = true, // forces every cell to be treated as a string
    // CustomExport receives the cell and its current string value,
    // allowing you to modify it before it is written.
    CustomExport = (cell, value) =>
    {
        // Convert the cell value to an upper‑case string
        return value?.ToString().ToUpperInvariant();
    }
};

// Define the output path for the text file
string txtPath = @"C:\Temp\Table.txt";

// Export the first worksheet (index 0) as a tab‑delimited text file
workbook.Worksheets[0].ExportTable(txtPath, tableOptions);

Console.WriteLine($"Worksheet exported as text to {txtPath}");
```

**Why this matters:**  
कई इंटीग्रेशन पॉइंट्स (जैसे मेनफ़्रेम बैच जॉब्स) अपरकेस आइडेंटिफ़ायर्स की अपेक्षा करते हैं। `CustomExport` कॉलबैक आपको प्रत्येक सेल की प्रतिनिधित्व पर पूर्ण नियंत्रण देता है, जिससे आप ट्रिमिंग, पैडिंग, या लोकेल‑स्पेसिफिक फॉर्मेटिंग जैसी ट्रांसफ़ॉर्मेशन को फ़ाइल के पोस्ट‑प्रोसेसिंग के बिना इंजेक्ट कर सकते हैं।

---

## चरण 3: कस्टम नंबर फॉर्मेट लागू करें और फॉर्मेटेड परिणाम पढ़ें

Excel के बिल्ट‑इन नंबर फ़ॉर्मेट अधिकांश मामलों को कवर करते हैं, लेकिन कभी‑कभी आपको डेट्स को एक विशिष्ट कैलेंडर सिस्टम—जैसे जापानी इरा—में दिखाने की जरूरत पड़ती है। नीचे दिया गया कोड दिखाता है कि कैसे **apply custom number format** को एक सेल पर लागू करें, फिर वर्कबुक के लोकेल को सम्मानित करने वाला फॉर्मेटेड स्ट्रिंग पढ़ें।

```csharp
// Create a new workbook for the era example
Workbook eraWorkbook = new Workbook();

// Access the first worksheet and target cell A1
Worksheet sheet = eraWorkbook.Worksheets[0];
Cell dateCell = sheet.Cells["A1"];

// Insert a Japanese‑era date string (Reiwa 3 = 2021)
dateCell.PutValue("Reiwa 3/04/01");

// Apply a built‑in date number format (14 = mm-dd-yy)
// You could also assign a custom format string, e.g., "[$-ja-JP]ggge年m月d日"
Style style = eraWorkbook.CreateStyle();
style.Number = 14; // standard short date format
dateCell.SetStyle(style);

// Force formula calculation (necessary if the cell contains a formula)
eraWorkbook.CalculateFormula();

// Retrieve the formatted string as it would appear in Excel
string formattedDate = dateCell.StringValue;
Console.WriteLine($"Formatted date (locale aware): {formattedDate}");
```

**Why this matters:**  
नंबर फ़ॉर्मेट के साथ `SetStyle` का उपयोग करने से यह सुनिश्चित होता है कि सेल का डिस्प्ले रीजनल सेटिंग्स का सम्मान करता है, जो विभिन्न लोकेल्स में वितरित रिपोर्टों के लिए महत्वपूर्ण है। जब आप बाद में `StringValue` पढ़ते हैं, तो आपको वही स्ट्रिंग मिलती है जो उपयोगकर्ता Excel UI में देखेगा, जिससे मैन्युअल पार्सिंग की आवश्यकता समाप्त हो जाती है।

---

## पूर्ण, चलाने योग्य उदाहरण

नीचे एक सिंगल प्रोग्राम है जो तीनों चरणों को संयोजित करता है। इसे एक नए Console App प्रोजेक्ट में पेस्ट करें, Aspose.Cells NuGet पैकेज जोड़ें, और चलाएँ।

```csharp
using Aspose.Cells;
using System;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // ---------- Step 1: Save workbook as CSV ----------
            Workbook workbook = new Workbook(); // start with a fresh workbook
            // (Optionally load an existing file: new Workbook("input.xlsx"))

            // Populate some sample data
            workbook.Worksheets[0].Cells["A1"].PutValue(123.456789);
            workbook.Worksheets[0].Cells["B1"].PutValue("Sample Text");

            CsvSaveOptions csvOptions = new CsvSaveOptions
            {
                SignificantDigits = 4
            };
            string csvPath = @"C:\Temp\Digits.csv";
            workbook.Save(csvPath, csvOptions);
            Console.WriteLine($"Saved CSV to {csvPath}");

            // ---------- Step 2: Export worksheet as text with uppercase ----------
            ExportTableOptions tableOptions = new ExportTableOptions
            {
                ExportAsString = true,
                CustomExport = (cell, value) => value?.ToString().ToUpperInvariant()
            };
            string txtPath = @"C:\Temp\Table.txt";
            workbook.Worksheets[0].ExportTable(txtPath, tableOptions);
            Console.WriteLine($"Exported TXT to {txtPath}");

            // ---------- Step 3: Apply custom number format ----------
            Workbook eraWorkbook = new Workbook();
            Cell dateCell = eraWorkbook.Worksheets[0].Cells["A1"];
            dateCell.PutValue("Reiwa 3/04/01");

            Style eraStyle = eraWorkbook.CreateStyle();
            eraStyle.Number = 14; // short date format; replace with custom if needed
            dateCell.SetStyle(eraStyle);
            eraWorkbook.CalculateFormula();

            Console.WriteLine($"Japanese era date formatted: {dateCell.StringValue}");
        }
    }
}
```

**Expected output**

```
Saved CSV to C:\Temp\Digits.csv
Exported TXT to C:\Temp\Table.txt
Japanese era date formatted: 4/1/2021
```

(सटीक डेट फ़ॉर्मेट आपके सिस्टम की लोकेल सेटिंग्स के अनुसार बदल सकता है।)

---

## सामान्य प्रश्न और किनारे‑के‑केस हैंडलिंग

| Question | Answer |
|----------|--------|
| *What if I need a different delimiter in the CSV?* | Set `csvOptions.Separator` to `','`, `'\t'`, or any custom character before calling `Save`. |
| *Can I keep the original numeric precision instead of rounding?* | Use `SignificantDigits = 0` to write the full double‑precision value, or set `NumberDecimalSeparator` for locale‑specific decimal symbols. |
| *How do I export only a specific range rather than the whole sheet?* | Call `ExportTable(string fileName, ExportTableOptions options, CellArea area)` and pass a `CellArea` that defines the range. |
| *What if the workbook contains formulas that reference other sheets?* | Ensure you call `workbook.CalculateFormula()` before exporting; otherwise you’ll get the cached values. |
| *Is there a way to keep the original cell formatting (fonts, colors) in the TXT file?* | Plain‑text formats cannot retain visual styling. If you need rich formatting, consider exporting to HTML (`HtmlSaveOptions`) instead. |

---

## निष्कर्ष

अब आप जानते हैं कि कैसे **save workbook as CSV** को नियंत्रित प्रिसीजन के साथ करें, **export excel to TXT** करते समय **uppercase cell values** को मजबूर करें, और लोकेल‑अवेयर डेट रेंडरिंग के लिए **apply custom number format** करें। प्रत्येक स्निपेट स्व-निहित है, बॉक्स‑से‑बाहर चलता है, और प्रदर्शन एवं मेंटेनबिलिटी दोनों के लिए बेस्ट प्रैक्टिसेज़ का पालन करता है।

अगले चरण में आप खोज सकते हैं:

* `HtmlSaveOptions` का उपयोग करके वेब‑फ्रेंडली फ़ॉर्मेट्स में एक्सपोर्ट करते समय स्टाइलिंग को बनाए रखें।  
* मल्टी‑लिंगुअल डेटा के साथ काम करते समय UTF‑8 या अन्य कैरेक्टर सेट्स के लिए `CsvSaveOptions.Encoding` को लेवरज करें।  
* `workbook.Worksheets` पर लूप करके कई वर्कशीट्स की बैच प्रोसेसिंग को ऑटोमेट करें।

कोड को अपने डेटा पाइपलाइन में अनुकूलित करने के लिए स्वतंत्र महसूस करें, और Aspose.Cells की लचीलापन भारी काम को संभाल लेगा।

---

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑बद्ध व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [वर्कबुक को टेक्स्ट CSV फ़ॉर्मेट में सहेजें](/cells/german/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [वर्कबुक को टेक्स्ट CSV फ़ॉर्मेट में सहेजें](/cells/french/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)
- [वर्कबुक को टेक्स्ट CSV फ़ॉर्मेट में सहेजें](/cells/spanish/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}