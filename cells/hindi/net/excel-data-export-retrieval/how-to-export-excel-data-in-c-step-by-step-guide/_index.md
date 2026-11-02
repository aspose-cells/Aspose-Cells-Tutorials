---
category: general
date: 2026-03-21
description: कैसे Aspose.Cells का उपयोग करके C# में कॉलम नामों के साथ Excel डेटा निर्यात
  करें, संख्या स्वरूप को बनाए रखें, और विशिष्ट पंक्तियों को पढ़ें। Excel वर्कशीट को
  पढ़ना और विशिष्ट पंक्तियों को प्रभावी ढंग से निर्यात करना सीखें।
draft: false
keywords:
- how to export excel
- preserve number format
- export with column names
- read excel worksheet
- export specific rows
language: hi
og_description: Aspose.Cells का उपयोग करके कॉलम नामों के साथ Excel डेटा निर्यात करना,
  संख्या स्वरूप को बनाए रखना, और विशिष्ट पंक्तियों को पढ़ना। C# डेवलपर्स के लिए पूर्ण,
  चलाने योग्य उदाहरण।
og_title: C# में Excel डेटा निर्यात कैसे करें – पूर्ण प्रोग्रामिंग गाइड
tags:
- C#
- Aspose.Cells
- Excel
- DataTable
title: C# में Excel डेटा निर्यात कैसे करें – चरण‑दर‑चरण गाइड
url: /hi/net/excel-data-export-retrieval/how-to-export-excel-data-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Excel डेटा निर्यात करने का तरीका – पूर्ण प्रोग्रामिंग गाइड

क्या आप कभी सोचते हैं **how to export excel** डेटा को मूल फ़ॉर्मेटिंग खोए बिना कैसे निर्यात करें? शायद आपने जल्दी‑से कॉपी‑पेस्ट किया और तिथियाँ “44728” जैसी दिखने लगीं या कॉलम हेडर गायब हो गए। यह निराशाजनक है, है ना? इस ट्यूटोरियल में आप देखेंगे एक साफ़, एंड‑टू‑एंड तरीका Excel वर्कशीट पढ़ने का, नंबर फ़ॉर्मेट बनाए रखने का, कॉलम नामों के साथ निर्यात करने का, और यहाँ तक कि केवल आवश्यक पंक्तियों को चुनने का।

हम Aspose.Cells लाइब्रेरी का उपयोग करेंगे क्योंकि यह निर्यात विकल्पों पर सूक्ष्म नियंत्रण देती है। इस गाइड के अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे किसी भी .NET प्रोजेक्ट में डाला जा सकता है, और आप समझ पाएँगे कि प्रत्येक विकल्प क्यों महत्वपूर्ण है। कोई बाहरी दस्तावेज़ आवश्यक नहीं—सब कुछ यहाँ उपलब्ध है।

---

## आप क्या सीखेंगे

- **Read Excel worksheet** को मेमोरी में Aspose.Cells के साथ पढ़ना।
- **Export specific rows** (उदाहरण : rows 0‑49) को कॉलम नाम रखते हुए निर्यात करना।
- **Preserve number format** ताकि मुद्रा, तिथियाँ और प्रतिशत अपरिवर्तित रहें।
- कैसे **export with column names** करें और यदि आवश्यक हो तो सेल कमेंट्स भी शामिल करें।
- एक पूर्ण, तैयार‑चलाने‑योग्य C# उदाहरण और सामान्य समस्याओं के टिप्स।

### पूर्वापेक्षाएँ

- .NET 6.0 या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)।
- NuGet के माध्यम से Aspose.Cells for .NET स्थापित (`Install-Package Aspose.Cells`)।
- एक Excel फ़ाइल (`input.xlsx`) जिसे आप संदर्भित कर सकें।

> **Pro tip:** यदि आप CI पाइपलाइन पर हैं, तो लाइसेंसिंग आश्चर्यों से बचने के लिए निजी फ़ीड से NuGet पैकेज खींचने पर विचार करें।

---

## चरण 1 – Aspose.Cells स्थापित करें और नेमस्पेस जोड़ें

पहले, सुनिश्चित करें कि Aspose.Cells पैकेज आपके प्रोजेक्ट में है। पैकेज मैनेजर कंसोल खोलें और चलाएँ:

```powershell
Install-Package Aspose.Cells
```

फिर अपने C# फ़ाइल के शीर्ष पर आवश्यक `using` निर्देश जोड़ें:

```csharp
using Aspose.Cells;
using System.Data;
using System;
```

इन इम्पोर्ट्स से आपको `Workbook`, `Worksheet`, `ExportTableOptions`, और `DataTable` तक पहुँच मिलती है—जो **reading an Excel worksheet** और डेटा निर्यात करने के मुख्य घटक हैं।

---

## चरण 2 – वर्कबुक लोड करें (Excel फ़ाइल पढ़ें)

अब हम वास्तव में **read the Excel worksheet**। `Workbook` कंस्ट्रक्टर फ़ाइल का पाथ लेता है, और Aspose.Cells दोनों `.xlsx` और पुराने `.xls` फ़ॉर्मेट को संभाल लेगा।

```csharp
// Step 2: Load the workbook containing the data
string filePath = @"YOUR_DIRECTORY\input.xlsx";
Workbook workbook = new Workbook(filePath);
```

> **Why this matters:** वर्कबुक को एक बार लोड करके उसी `Worksheet` ऑब्जेक्ट को पुनः‑उपयोग करना बड़े स्प्रेडशीट्स के लिए फ़ाइल को बार‑बार खोलने की तुलना में बहुत अधिक कुशल है।

---

## चरण 3 – निर्यात विकल्प कॉन्फ़िगर करें (Preserve Number Format & Column Names)

यहाँ हम Aspose.Cells को बताते हैं *कैसे* निर्यात करना है। `ExportTableOptions` क्लास हमें आउटपुट को सूक्ष्म‑तरीके से ट्यून करने की सुविधा देती है। हम तीन फ़्लैग्स को सक्षम करेंगे:

1. `ExportAsString = true` – हर सेल को स्ट्रिंग बनाता है, जिससे नंबर अपना दृश्य प्रतिनिधित्व बनाए रखते हैं।
2. `IncludeCellComments = true` – सेल्स से जुड़े किसी भी कमेंट को कॉपी करता है (डॉक्यूमेंटेशन के लिए उपयोगी)।
3. `PreserveNumberFormat = true` – मूल नंबर फ़ॉर्मेट (करेंसी सिंबल, डेट पैटर्न आदि) को बरकरार रखता है।

```csharp
// Step 3: Configure export options to control how the table is exported
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,          // Export all values as strings
    IncludeCellComments = true,     // Preserve any cell comments
    PreserveNumberFormat = true     // Keep the original number formatting
};
```

> **Edge case:** यदि आप `ExportAsString` को `false` रखते हैं लेकिन फिर भी नंबर फ़ॉर्मेट रखना चाहते हैं, तो आपको कच्चे संख्यात्मक मान (जैसे, तिथि के लिए 44728) मिल सकते हैं। दोनों फ़्लैग्स को ऑन रखने से यह आश्चर्य टल जाता है।

---

## चरण 4 – पहली वर्कशीट प्राप्त करें (Read Excel Worksheet)

अधिकांश सरल फ़ाइलों में आवश्यक डेटा पहली शीट पर होता है, इसलिए हम इसे इंडेक्स द्वारा प्राप्त करेंगे। यदि आपको कोई अलग शीट चाहिए, तो `0` को उपयुक्त शून्य‑आधारित इंडेक्स से बदलें या `workbook.Worksheets["SheetName"]` का उपयोग करें।

```csharp
// Step 4: Get the first worksheet from the workbook
Worksheet firstWorksheet = workbook.Worksheets[0];
```

> **Why it’s useful:** वर्कशीट ऑब्जेक्ट तक सीधे पहुँचने से आपको उसके `Cells` कलेक्शन पर पूर्ण नियंत्रण मिलता है, जो बाद में **export specific rows** करने के लिए आवश्यक है।

---

## चरण 5 – सेल रेंज निर्यात करें (Export Specific Rows)

अब ट्यूटोरियल का मुख्य भाग: rows 0‑49 और columns 0‑4 (अर्थात पहले 50 पंक्तियाँ और पहले पाँच कॉलम) को `DataTable` में निर्यात करना। हम Aspose.Cells को `DataTable` की पहली पंक्ति में कॉलम नाम शामिल करने के लिए भी कहेंगे।

```csharp
// Step 5: Export a range of cells (rows 0‑49, columns 0‑4) to a DataTable using the options
DataTable exportedTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: 50,
    totalColumns: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

### यह क्या करता है

- **`startRow: 0`** – शीट के सबसे ऊपर से शुरू करता है।
- **`totalRows: 50`** – पहले 50 पंक्तियों को लेता है (**export specific rows**)।
- **`totalColumns: 5`** – निर्यात को पहले पाँच कॉलम तक सीमित करता है।
- **`includeColumnNames: true`** – सुनिश्चित करता है कि `DataTable` के कॉलम हेडर Excel की हेडर पंक्ति से मेल खाते हों, जिससे **export with column names** की आवश्यकता पूरी होती है।
- **`exportOptions`** – चरण 3 की सेटिंग्स लागू करता है, इसलिए आपका नंबर “$1,234.56” जैसा दिखेगा, “1234.56” नहीं।

---

## चरण 6 – निर्यात की पुष्टि करें (What the Result Looks Like)

पहली कुछ पंक्तियों को कंसोल में प्रिंट करें ताकि आप देख सकें कि फ़ॉर्मेटिंग बनी रही।

```csharp
// Step 6: Display a few rows to verify the export
Console.WriteLine("=== Exported DataTable Preview ===");
foreach (DataRow row in exportedTable.Rows)
{
    // Join each column with a tab for readability
    Console.WriteLine(string.Join("\t", row.ItemArray));
}
```

**Expected output (example):**

```
=== Exported DataTable Preview ===
Date        Description    Amount   Tax   Total
01/02/2024  Widget A       $120.00  $12  $132.00
01/03/2024  Widget B       $200.00  $20  $220.00
...
```

ध्यान दें कि तिथियाँ `MM/dd/yyyy` फ़ॉर्मेट में दिख रही हैं और मुद्रा में `$` सिंबल बना हुआ है—धन्यवाद **preserve number format** को लागू करने के लिए।

---

## सामान्य समस्याएँ एवं समाधान

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| तिथियाँ बड़े संख्याओं में बदल जाती हैं | `ExportAsString` को `false` रखा गया | `ExportAsString = true` रखें या सेल्स को मैन्युअली बदलें |
| कॉलम हेडर गायब हैं | `includeColumnNames` को `false` सेट किया गया | जब **export with column names** चाहिए तो इसे `true` सेट करें |
| कमेंट्स नहीं दिख रहे | `IncludeCellComments` सक्षम नहीं है | `ExportTableOptions` में `IncludeCellComments` को ऑन करें |
| गलत शीट निर्यात हो रही है | मल्टी‑शीट फ़ाइल में `Worksheets[0]` उपयोग किया गया | शीट नाम निर्दिष्ट करें: `workbook.Worksheets["Data"]` |
| आउट‑ऑफ़‑रेंज एक्सेप्शन | `totalRows` वास्तविक पंक्तियों से अधिक है | `Math.Min(totalRows, worksheet.Cells.MaxDataRow + 1)` का उपयोग करें |

---

## बोनस: पूरे शीट को निर्यात करना जबकि फ़ॉर्मेट्स बरकरार रखें

यदि बाद में आपको पूरी शीट चाहिए, तो `totalRows` और `totalColumns` को शीट के अधिकतम आयामों से बदल दें:

```csharp
int maxRows = firstWorksheet.Cells.MaxDataRow + 1;      // +1 because rows are zero‑based
int maxCols = firstWorksheet.Cells.MaxDataColumn + 1;

DataTable fullTable = firstWorksheet.Cells.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    totalRows: maxRows,
    totalColumns: maxCols,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

अब आपके पास एक **read excel worksheet** रूटीन है जो किसी भी आकार की शीट के लिए काम करता है, जबकि **preserving number format** और **exporting with column names** को बनाए रखता है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है जिसे आप किसी भी कंसोल ऐप में डाल सकते हैं। इसमें सभी चरण, इम्पोर्ट्स, और एक सरल सत्यापन प्रिंटआउट शामिल है।

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the workbook
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);

            // 2️⃣ Set export options (preserve number format, include comments, export as strings)
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                IncludeCellComments = true,
                PreserveNumberFormat = true
            };

            // 3️⃣ Grab the first worksheet (read excel worksheet)
            Worksheet sheet = workbook.Worksheets[0];

            // 4️⃣ Export rows 0‑49, columns 0‑4 (export specific rows) with column headers
            DataTable table = sheet.Cells.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                totalRows: 50,
                totalColumns: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // 5️⃣ Show a preview
            Console.WriteLine("=== Exported DataTable Preview ===");
            foreach (DataRow row in table.Rows)
            {
                Console.WriteLine(string.Join("\t", row.ItemArray));
            }

            // Keep console open
            Console.WriteLine("\nExport complete. Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

इसे `Program.cs` के रूप में सेव करें, `dotnet run` चलाएँ, और आपको टर्मिनल में फ़ॉर्मेटेड प्रीव्यू दिखना चाहिए।

---

## निष्कर्ष

हमने अभी **how to export excel** डेटा को Aspose.Cells का उपयोग करके कैसे निर्यात किया, इस पर पूरी walkthrough की, जिसमें वर्कबुक लोड करना, नंबर फ़ॉर्मेट बनाए रखना, कॉलम नामों के साथ निर्यात करना, और निर्यात को विशिष्ट पंक्तियों तक सीमित करना शामिल है। कोड स्व-निहित, पूरी तरह चलने योग्य, और सबसे सामान्य किनारी मामलों के लिए व्यावहारिक सुरक्षा उपायों के साथ है।

अगली चुनौती के लिए तैयार हैं? मूल नंबर फ़ॉर्मेट को बनाए रखते हुए सीधे CSV में निर्यात करने की कोशिश करें, या `DataTable` को Entity Framework Core कॉन्टेक्स्ट में बैच डेटाबेस इन्सर्ट्स के लिए पुश करें। दोनों परिदृश्य वही मूलभूत सिद्धांतों पर आधारित हैं जो हमने यहाँ कवर किए हैं।

यदि आपको यह गाइड उपयोगी लगा

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}