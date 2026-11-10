---
category: general
date: 2026-10-01
description: एक्सेल वर्कबुक C# में बनाना, कस्टम नंबर फ़ॉर्मेट लागू करना, सेल के दशमलव
  स्थान सेट करना, और वर्कबुक को XLSX के रूप में सहेजना सीखें—एक पूर्ण चरण‑दर‑चरण गाइड
  में।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook c#
- apply custom number format
- how to format numbers excel
- set cell decimal places
- save workbook as xlsx
language: hi
lastmod: 2026-10-01
og_description: C# के साथ कस्टम नंबर फ़ॉर्मेट के साथ Excel वर्कबुक बनाएं, सेल के दशमलव
  स्थान सेट करें, और वर्कबुक को XLSX के रूप में सहेजें। सटीक संख्यात्मक आउटपुट के
  लिए इस पूर्ण गाइड का पालन करें।
og_image_alt: Screenshot of an Excel sheet showing numbers rounded to four significant
  digits
og_title: Excel वर्कबुक बनाएं C# – कस्टम नंबर फ़ॉर्मेट और XLSX निर्यात
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  headline: How to create Excel workbook C# with custom number formatting
  type: TechArticle
- description: Learn how to create Excel workbook C# and apply custom number format,
    set cell decimal places, and save workbook as XLSX in a complete step‑by‑step
    guide.
  name: How to create Excel workbook C# with custom number formatting
  steps:
  - name: Run the program (`dotnet run`).
    text: Run the program (`dotnet run`).
  - name: Open `SigDigits.xlsx`.
    text: Open `SigDigits.xlsx`.
  - name: Confirm that **A1** reads `123.5`.
    text: Confirm that **A1** reads `123.5`.
  - name: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
    text: If you open the file’s XML (`.xlsx` is a zip archive), you’ll see the custom
      format `"0.######"` stored in the `<c>` element’s `s` attribute.
  type: HowTo
tags:
- Excel
- C#
- Aspose.Cells
title: कस्टम नंबर फ़ॉर्मेटिंग के साथ C# में Excel वर्कबुक कैसे बनाएं
url: /hi/net/excel-custom-number-date-formatting/how-to-create-excel-workbook-c-with-custom-number-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to create Excel workbook C# with custom number formatting

यदि आपको **create excel workbook c#** बनाना है जो संख्याओं को बिल्कुल उसी तरह दिखाए जैसा आप चाहते हैं, तो यह गाइड आपको कुछ स्पष्ट चरणों में यह करने का तरीका दिखाता है। आप कस्टम नंबर फ़ॉर्मेट लागू करना, सेल दशमलव स्थान सेट करना, और अंत में **save workbook as xlsx** करना सीखेंगे।

संख्यात्मक डेटा के साथ काम करना अक्सर सटीकता और पठनीयता के बीच संतुलन बनाता है। इस ट्यूटोरियल के अंत तक आपके पास एक पुन: उपयोग योग्य पैटर्न होगा जो प्रदर्शित अंकों को एक विशिष्ट महत्वपूर्ण अंकों की संख्या तक सीमित करता है जबकि फ़ाइल में मूल मान को बरकरार रखता है। कोई बाहरी स्क्रिप्ट आवश्यक नहीं—सिर्फ C# और Aspose.Cells लाइब्रेरी।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 SDK या बाद का संस्करण स्थापित  
* Visual Studio 2022 (या कोई भी C# IDE)  
* **Aspose.Cells for .NET** NuGet पैकेज (`Install-Package Aspose.Cells`) – यह लाइब्रेरी उन `Workbook`, `Worksheet`, और `ExportTableOptions` क्लासों को प्रदान करती है जो उदाहरणों में उपयोग होते हैं।  

ये आवश्यकताएँ न्यूनतम हैं; वही कोड .NET Core, .NET Framework, और यहाँ तक कि Azure Functions में भी काम करता है।

## Step 1: Create Excel workbook C# – initialize the file

पहला ऑपरेशन एक नया `Workbook` ऑब्जेक्ट बनाना है। यह ऑब्जेक्ट मेमोरी में पूरे Excel फ़ाइल का प्रतिनिधित्व करता है और स्वचालित रूप से एक डिफ़ॉल्ट वर्कशीट शामिल करता है।

```csharp
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();               // creates an empty .xlsx container
            Worksheet sheet = workbook.Worksheets[0];         // reference to the default sheet
```

**Why this matters:**  
वर्कबुक को पहले बनाकर रखने से आपको एक साफ़ कैनवास मिलता है। डिफ़ॉल्ट वर्कशीट (`Worksheets[0]`) डेटा एंट्री के लिए तैयार है, इसलिए जब तक आपका परिदृश्य कई टैब की आवश्यकता नहीं रखता, आपको नई शीट जोड़ने की ज़रूरत नहीं है।

## Step 2: Write a numeric value to a cell

अब नमूना संख्या को सेल **A1** में रखें। हम जो मान उपयोग करते हैं (`123.456789`) में उन दशमलव स्थानों की संख्या अधिक है जितनी हम अंत में दिखाना चाहते हैं, जिससे बाद में राउंडिंग दिखाने में मदद मिलती है।

```csharp
            // Step 2: Write a numeric value to cell A1
            sheet.Cells[0, 0].PutValue(123.456789); // row 0, column 0 = A1
```

**Tip:** `PutValue` स्वचालित रूप से डेटा टाइप का पता लगा लेता है, इसलिए आपको संख्या को स्ट्रिंग में बदलने की ज़रूरत नहीं है।

## Step 3: Apply custom number format – limit visible decimals

Excel को संख्या कैसे दिखानी है, इसे नियंत्रित करने के लिए हम एक `Style` बनाते हैं जिसमें **custom number format** हो। पैटर्न `"0.######"` Excel को अधिकतम छह दशमलव स्थान दिखाने को कहता है, लेकिन अंत के शून्य को हटाता है।

```csharp
            // Step 3: Define a custom number format (up to 6 decimal places) and apply it
            Style customStyle = workbook.CreateStyle();
            customStyle.Custom = "0.######";               // up to 6 decimals, no trailing zeros
            sheet.Cells[0, 0].SetStyle(customStyle);
```

**How this works:**  
फ़ॉर्मेट स्ट्रिंग Excel के कस्टम‑फ़ॉर्मेट सिंटैक्स का पालन करती है। `0` अंक को अनिवार्य बनाता है, जबकि `#` केवल तब अंक दिखाता है जब वह महत्वपूर्ण हो। इन्हें मिलाकर आप एक लचीला डिस्प्ले प्राप्त करते हैं जो मूल सटीकता को बरकरार रखता है।

## Step 4: Set cell decimal places – using ExportTableOptions

यदि आपको निर्यातित डेटा के लिए **set cell decimal places** (जैसे DataTable में बदलते समय) की आवश्यकता है, तो Aspose.Cells आपको **significant digits** की संख्या निर्दिष्ट करने देता है। यह चरण सुनिश्चित करता है कि निर्यातित CSV या DataTable वही राउंडिंग नियम अपनाए जो आपने वर्कबुक में लागू किए हैं।

```csharp
            // Step 4: Configure export options to limit the output to 4 significant digits
            ExportTableOptions exportOptions = new ExportTableOptions();
            exportOptions.SignificantDigits = 4;           // round to 4 significant figures
```

**Why use `SignificantDigits`?**  
एक निश्चित दशमलव गिनती के विपरीत, महत्वपूर्ण अंक संख्या के परिमाण को बरकरार रखते हैं जबकि सटीकता को सीमित करते हैं, जो अक्सर विश्लेषकों को डेटा सारांशित करते समय चाहिए होता है।

## Step 5: Export the worksheet data and **save workbook as xlsx**

अंत में, डेटा निर्यात करें (यदि आपको DataTable चाहिए) और वर्कबुक को डिस्क पर सहेजें। `ExportDataTable` कॉल हमारे द्वारा कॉन्फ़िगर किए गए `ExportTableOptions` को मानता है, और `workbook.Save` एक मानक XLSX फ़ाइल लिखता है।

```csharp
            // Step 5: Export the worksheet data using the configured options and save the workbook
            sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
            workbook.Save("SigDigits.xlsx");               // saves to the application’s working folder
        }
    }
}
```

**Expected result:**  
जब आप *SigDigits.xlsx* को Excel में खोलते हैं, तो सेल **A1** में `123.5` दिखेगा। मूल मान `123.456789` बना रहता है, लेकिन प्रदर्शित संख्या 4‑significant‑digit नियम का पालन करती है। यदि आप शीट को DataTable में निर्यात करते हैं, तो तालिका में मान भी `123.5` तक राउंड हो जाएगा।

---

## Apply custom number format to additional cells

यदि आपको एकल सेल के बजाय रेंज को फ़ॉर्मेट करना है, तो `Style` ऑब्जेक्ट को पुन: उपयोग करें:

```csharp
// Apply the same custom style to B2:C5
Range range = sheet.Cells.CreateRange("B2:C5");
range.ApplyStyle(customStyle, new StyleFlag { NumberFormat = true });
```

**Pro tip:** एक ही स्टाइल ऑब्जेक्ट को पुन: उपयोग करने से मेमोरी ओवरहेड कम होता है और शीट भर में फ़ॉर्मेटिंग समान रहती है।

## How to format numbers Excel using C# – common variations

| Scenario | Format string | Result |
|----------|---------------|--------|
| दो दशमलव स्थान निश्चित | `"0.00"` | `123.46` |
| मुद्रा (US) | `"$#,##0.00"` | `$123.46` |
| एक दशमलव के साथ प्रतिशत | `"0.0%"` | `12,346.0%` |
| वैज्ञानिक संकेतन | `"0.00E+00"` | `1.23E+02` |

अपनी रिपोर्टिंग आवश्यकताओं के अनुसार उपयुक्त पैटर्न चुनें। सभी पैटर्न `Style.Custom` प्रॉपर्टी के साथ संगत हैं जैसा कि पहले दिखाया गया था।

## Set cell decimal places dynamically based on user input

कभी‑कभी आवश्यक सटीकता कंपाइल टाइम पर ज्ञात नहीं होती। आप रन‑टाइम पर फ़ॉर्मेट स्ट्रिंग बना सकते हैं:

```csharp
int decimals = 3; // could come from a UI textbox
string format = "0." + new string('#', decimals);
customStyle.Custom = format;
sheet.Cells["A2"].PutValue(987.654321);
sheet.Cells["A2"].SetStyle(customStyle);
```

**Edge case:** यदि `decimals` शून्य है, तो फ़ॉर्मेट `"0"` (पूर्णांक डिस्प्ले) बन जाता है। हमेशा उपयोगकर्ता इनपुट को वैध करें ताकि गलत फ़ॉर्मेट स्ट्रिंग न बनें।

## Save workbook as XLSX – best practices

* **Use absolute paths** जब आप किसी ज्ञात डायरेक्टरी में लिख रहे हों (`Path.Combine(Environment.CurrentDirectory, "output.xlsx")`)।  
* **Dispose** `Workbook` को `using` स्टेटमेंट में रैप करके अनमैनेज्ड रिसोर्सेज़ को तुरंत मुक्त करें:

```csharp
using (Workbook wb = new Workbook())
{
    // ...populate workbook...
    wb.Save(Path.Combine(@"C:\Exports", "Report.xlsx"));
}
```

* **Version compatibility:** Aspose.Cells फ़ाइलें Excel 2010‑2023 के साथ संगत लिखता है, इसलिए डाउनस्ट्रीम उपयोगकर्ताओं को फ़ॉर्मेट समस्याओं का सामना नहीं करना पड़ेगा।

---

## Full working example

नीचे पूरा प्रोग्राम दिया गया है जिसे आप कॉपी, पेस्ट और तुरंत चला सकते हैं। इसमें सभी आवश्यक `using` निर्देश, टिप्पणियाँ, और एरर हैंडलिंग शामिल हैं।

```csharp
using System;
using System.IO;
using Aspose.Cells;

namespace ExcelDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Create workbook and get the first worksheet
                Workbook workbook = new Workbook();
                Worksheet sheet = workbook.Worksheets[0];

                // 2️⃣ Write a high‑precision number to A1
                sheet.Cells[0, 0].PutValue(123.456789);

                // 3️⃣ Apply a custom number format (up to 6 decimals)
                Style customStyle = workbook.CreateStyle();
                customStyle.Custom = "0.######";
                sheet.Cells[0, 0].SetStyle(customStyle);

                // 4️⃣ Configure export options for 4 significant digits
                ExportTableOptions exportOptions = new ExportTableOptions
                {
                    SignificantDigits = 4
                };

                // 5️⃣ Export data (optional) and save the workbook as XLSX
                sheet.ExportDataTable(sheet.Cells.MaxDisplayRange, true, exportOptions);
                string outputPath = Path.Combine(Environment.CurrentDirectory, "SigDigits.xlsx");
                workbook.Save(outputPath);

                Console.WriteLine($"Workbook saved successfully at: {outputPath}");
                Console.WriteLine("Cell A1 displays: " + sheet.Cells["A1"].StringValue);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error creating workbook: {ex.Message}");
            }
        }
    }
}
```

**Verification steps**

1. प्रोग्राम चलाएँ (`dotnet run`)।  
2. `SigDigits.xlsx` खोलें।  
3. पुष्टि करें कि **A1** में `123.5` लिखा है।  
4. यदि आप फ़ाइल का XML देखें (`.xlsx` एक ज़िप आर्काइव है), तो आप `<c>` एलिमेंट के `s` एट्रिब्यूट में कस्टम फ़ॉर्मेट `"0.######"` देखेंगे।

---

## Conclusion

इस ट्यूटोरियल में आपने **create excel workbook c#**, **apply custom number format**, **set cell decimal places**, और **save workbook as xlsx** को Aspose.Cells की मदद से करना सीखा। समाधान दोनों—Excel में दृश्य फ़ॉर्मेटिंग और `ExportTableOptions` के माध्यम से डेटा‑निर्यात राउंडिंग—को प्रदर्शित करता है।

अब आप कर सकते हैं:

* इस दृष्टिकोण को पूरी रेंज या टेबल पर विस्तारित करें।  
* `StyleFlag` के साथ कई स्टाइल (फ़ॉन्ट, बॉर्डर) को मिलाएँ।  
* डेटा स्रोतों पर लूप करके और समान फ़ॉर्मेटिंग लॉजिक लागू करके रिपोर्ट जेनरेशन को स्वचालित करें।  

विभिन्न फ़ॉर्मेट स्ट्रिंग, दशमलव गिनती, या निर्यात विकल्पों के साथ प्रयोग करें ताकि आपकी विशिष्ट रिपोर्टिंग जरूरतें पूरी हों। हैप्पी कोडिंग!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Create Excel Workbook C# – Step‑by‑Step Guide with Conditional Formatting](/cells/english/net/excel-conditional-formatting/create-excel-workbook-c-step-by-step-guide-with-conditional/)
- [Create Excel Workbook C# – Add Comment & Save as XLSX](/cells/english/net/excel-comment-annotation/create-excel-workbook-c-add-comment-save-as-xlsx/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}