---
category: general
date: 2026-05-30
description: C# Excel ऑटोमेशन में AutoFilter का उपयोग कैसे करें। सीखें कि Excel वर्कबुक
  कैसे बनाएं, मान के आधार पर पंक्तियों को फ़िल्टर करें, और अपने स्प्रेडशीट कार्यों
  को सुव्यवस्थित करें।
draft: false
keywords:
- how to use autofilter
- create excel workbook
- filter rows by value
- filter column b
- excel automation c#
language: hi
og_description: C# Excel ऑटोमेशन में AutoFilter का उपयोग कैसे करें। Excel वर्कबुक
  बनाना, मान के आधार पर पंक्तियों को फ़िल्टर करना, और स्प्रेडशीट को आसानी से स्वचालित
  करना में निपुण बनें।
og_title: C# Excel ऑटोमेशन में ऑटोफ़िल्टर का उपयोग कैसे करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-05-30'
  description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  headline: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  type: TechArticle
- description: How to use AutoFilter in C# Excel automation. Learn how to create Excel
    workbook, filter rows by value, and streamline your spreadsheet tasks.
  name: How to Use AutoFilter in C# Excel Automation – Full Step‑by‑Step Guide
  steps:
  - name: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
    text: '**Creating the workbook** – `new Workbook()` gives you a clean file; `Worksheets[0]`
      grabs the default sheet.'
  - name: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
    text: '**Filling sample data** – We write a tiny dataset so you can see the filter
      in action.'
  - name: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
    text: '**Adding a table** – `ListObjects.Add` converts the range into an Excel
      table, which automatically supports filtering and styling.'
  - name: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
    text: '**Applying AutoFilter** – `table.AutoFilter.Filter(1, "Apple")` tells the
      engine: “Show only rows where the second column (B) equals *Apple*.”'
  - name: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
    text: '**Saving files** – Two files are written: one filtered, one with the filter
      removed, proving that `RemoveAutoFilter()` works as expected.'
  type: HowTo
- questions:
  - answer: Yes. Aspose.Cells can save to both `.xlsx` and `.xls` by changing the
      file extension or using `SaveOptions`.
    question: Does this work with older .xls files?
  - answer: Load the file with `new Workbook("path.xlsx")`, apply the filter, then
      `Save` again.
    question: What if I need to filter *after* the workbook is already saved?
  - answer: 'Absolutely. Use `worksheet.AutoFilter.Range = "A1:C5";` and then `worksheet.AutoFilter.ApplyFilter();`.
      However, tables give you built‑in styling and easier column referencing. ---
      ## Image – Visual Confirmation ![Screenshot showing AutoFilter applied to column
      B in an Excel workbook created with C#'
    question: Can I apply a filter to a *range* that isn’t a table?
  type: FAQPage
tags:
- C#
- Excel
- Automation
title: C# एक्सेल ऑटोमेशन में ऑटोफ़िल्टर का उपयोग कैसे करें – पूर्ण चरण‑दर‑चरण गाइड
url: /hi/net/excel-autofilter-validation/how-to-use-autofilter-in-c-excel-automation-full-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# Excel ऑटोमेशन में AutoFilter का उपयोग कैसे करें – पूर्ण गाइड

क्या आपने कभी **AutoFilter का उपयोग कैसे करें** इस बारे में सोचा है जब आप C# कोड से Excel फ़ाइलें बना रहे हों? आप अकेले नहीं हैं—कई डेवलपर्स को इस समस्या का सामना करना पड़ता है जब उन्हें उन पंक्तियों को छिपाना होता है जो किसी निश्चित मानदंड से मेल नहीं खातीं।  

इस ट्यूटोरियल में हम एक ठोस, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो **एक Excel वर्कबुक बनाता है**, एक टेबल जोड़ता है, और फिर **कॉलम B में मान के आधार पर पंक्तियों को फ़िल्टर करता है**। अंत तक आपके पास एक साफ़, पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी C# प्रोजेक्ट में डाल सकते हैं जिसे Excel ऑटोमेशन की आवश्यकता है।

## आप क्या सीखेंगे

- Aspose.Cells (या Microsoft.Office.Interop) लाइब्रेरी के साथ C# प्रोजेक्ट सेट अप करना।  
- प्रोग्रामेटिकली **Excel वर्कबुक बनाना** और एक स्टाइल्ड टेबल जोड़ना।  
- **AutoFilter** लागू करना ताकि केवल वे पंक्तियाँ दिखें जहाँ **कॉलम B** किसी विशिष्ट स्ट्रिंग के बराबर हो।  
- फ़िल्टर को पूरी तरह हटाना, जिससे पूरा डेटा सेट पुनः प्राप्त हो जाए।  
- गायब कॉलम या कई फ़िल्टर मानदंड जैसे एज केस को संभालने के टिप्स।

कोई पूर्व Excel‑VBA अनुभव आवश्यक नहीं; बस C# और NuGet पैकेजों की बुनियादी समझ चाहिए।

---

## पूर्वापेक्षाएँ

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0 या बाद का (या .NET Framework 4.7+) | आधुनिक रनटाइम बेहतर प्रदर्शन और आसान पैकेज प्रबंधन देते हैं। |
| Aspose.Cells for .NET (या Microsoft.Office.Interop.Excel) NuGet के माध्यम से स्थापित | यह लाइब्रेरी कोड में उपयोग किए जाने वाले `Workbook`, `Worksheet`, और `Table` ऑब्जेक्ट प्रदान करती है। |
| एक कोड एडिटर (Visual Studio, VS Code, Rider, आदि) | आपको उदाहरण को कंपाइल और चलाने की आवश्यकता होगी। |
| बेसिक C# ज्ञान | ट्यूटोरियल प्रत्येक लाइन के *क्यों* को समझाता है, न कि केवल *क्या* करता है। |

आप Aspose.Cells को इस प्रकार इंस्टॉल कर सकते हैं:

```bash
dotnet add package Aspose.Cells
```

---

## Aspose.Cells के साथ C# में AutoFilter का उपयोग कैसे करें

नीचे पूरा, स्व-समाहित प्रोग्राम दिया गया है। इसे एक कंसोल प्रोजेक्ट में `Program.cs` के रूप में सेव करें और चलाएँ – आपको आउटपुट फ़ोल्डर में `FilteredWorkbook.xlsx` मिलेगा।

```csharp
using System;
using Aspose.Cells;

namespace ExcelAutoFilterDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // Step 1: Create an Excel workbook and grab the first worksheet
            // -------------------------------------------------
            Workbook workbook = new Workbook();               // creates a new, empty workbook
            Worksheet sheet = workbook.Worksheets[0];         // the default sheet is named "Sheet1"

            // Populate the sheet with sample data (A‑C columns, 5 rows)
            sheet.Cells["A1"].PutValue("ID");
            sheet.Cells["B1"].PutValue("Fruit");
            sheet.Cells["C1"].PutValue("Quantity");

            sheet.Cells["A2"].PutValue(1);
            sheet.Cells["B2"].PutValue("Apple");
            sheet.Cells["C2"].PutValue(10);

            sheet.Cells["A3"].PutValue(2);
            sheet.Cells["B3"].PutValue("Banana");
            sheet.Cells["C3"].PutValue(15);

            sheet.Cells["A4"].PutValue(3);
            sheet.Cells["B4"].PutValue("Apple");
            sheet.Cells["C4"].PutValue(7);

            sheet.Cells["A5"].PutValue(4);
            sheet.Cells["B5"].PutValue("Cherry");
            sheet.Cells["C5"].PutValue(20);

            // -------------------------------------------------
            // Step 2: Convert the range into a ListObject (Excel table)
            // -------------------------------------------------
            // Parameters: firstRow, firstColumn, totalRows, totalColumns, hasHeaders
            int tableIdx = sheet.ListObjects.Add(0, 0, 5, 3, true);
            ListObject table = sheet.ListObjects[tableIdx];
            table.TableStyleType = TableStyleType.TableStyleMedium2; // nice built‑in styling

            // -------------------------------------------------
            // Step 3: Apply an AutoFilter to show only rows where column B = "Apple"
            // -------------------------------------------------
            // The AutoFilter is attached to the table’s range automatically.
            // We target column B (index 1) and set the criteria.
            table.AutoFilter.Filter(1, "Apple"); // 1 = zero‑based column index for B

            // -------------------------------------------------
            // Step 4: Save the filtered workbook to disk
            // -------------------------------------------------
            workbook.Save("FilteredWorkbook.xlsx");

            // -------------------------------------------------
            // Step 5: (Optional) Remove the AutoFilter completely
            // -------------------------------------------------
            // This demonstrates that you can revert to the full dataset without re‑loading.
            table.RemoveAutoFilter();   // clears the filter
            workbook.Save("UnfilteredWorkbook.xlsx");

            Console.WriteLine("Workbook created and filtered successfully.");
        }
    }
}
```

### कोड कैसे काम करता है

1. **वर्कबुक बनाना** – `new Workbook()` आपको एक साफ़ फ़ाइल देता है; `Worksheets[0]` डिफ़ॉल्ट शीट को पकड़ता है।  
2. **सैंपल डेटा भरना** – हम एक छोटा डेटा सेट लिखते हैं ताकि आप फ़िल्टर को कार्रवाई में देख सकें।  
3. **टेबल जोड़ना** – `ListObjects.Add` रेंज को एक Excel टेबल में बदलता है, जो स्वचालित रूप से फ़िल्टरिंग और स्टाइलिंग को सपोर्ट करता है।  
4. **AutoFilter लागू करना** – `table.AutoFilter.Filter(1, "Apple")` इंजन को बताता है: “केवल उन पंक्तियों को दिखाएँ जहाँ दूसरा कॉलम (B) *Apple* के बराबर हो।”  
5. **फ़ाइलें सेव करना** – दो फ़ाइलें लिखी जाती हैं: एक फ़िल्टर की हुई, एक फ़िल्टर हटाए हुए, जिससे यह प्रमाणित होता है कि `RemoveAutoFilter()` अपेक्षित रूप से काम करता है।

> **Pro tip:** यदि आपको कई मानदंडों (जैसे “Apple” *या* “Banana”) द्वारा फ़िल्टर करना है, तो ओवरलोड `Filter(int columnIndex, string criteria1, string criteria2)` या स्ट्रिंग्स की एरे पास करें।

---

## मान के आधार पर पंक्तियों को फ़िल्टर करना – सामान्य विविधताएँ

उपरोक्त उदाहरण **कॉलम B को फ़िल्टर करने** पर केंद्रित है, लेकिन आप अन्य कॉलम फ़िल्टर करना या संख्यात्मक मानदंड उपयोग करना चाह सकते हैं। यहाँ एक त्वरित चीट शीट है:

| Desired filter | Code snippet |
|----------------|--------------|
| कॉलम C में टेक्स्ट मिलान | `table.AutoFilter.Filter(2, "Cherry");` |
| कॉलम C में 10 से बड़े नंबर | `table.AutoFilter.CustomFilter(2, "10", OperatorType.GreaterThan);` |
| कॉलम B में कई मान | `table.AutoFilter.Filter(1, new[] { "Apple", "Banana" });` |

**Edge case:** यदि कॉलम हेडर गलत लिखा गया है या कॉलम इंडेक्स रेंज से बाहर है, तो Aspose.Cells `ArgumentException` फेंकेगा। फ़िल्टर लागू करने से पहले `table.ListColumns.Count` जाँच कर इसको रोकें।

---

## AutoFilter हटाना – कब रीसेट करें

कभी‑कभी आपको पूरा डेटा सेट फिर से प्रस्तुत करना पड़ता है (जैसे, उपयोगकर्ता ने सर्च बॉक्स साफ़ किया)। `table.RemoveAutoFilter()` एक ही लाइन में काम करता है। यदि आप Microsoft.Office.Interop उपयोग कर रहे हैं, तो `worksheet.AutoFilterMode = false;` कॉल करेंगे।

---

## पूर्ण कार्यशील उदाहरण पुनरावलोकन

नीचे *पूरा* प्रोग्राम फिर से दिया गया है, उन लोगों के लिए जो संक्षिप्त दृश्य चाहते हैं, टिप्पणी हटाकर:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        ws.Cells["A1"].PutValue("ID");
        ws.Cells["B1"].PutValue("Fruit");
        ws.Cells["C1"].PutValue("Quantity");

        ws.Cells["A2"].PutValue(1); ws.Cells["B2"].PutValue("Apple");  ws.Cells["C2"].PutValue(10);
        ws.Cells["A3"].PutValue(2); ws.Cells["B3"].PutValue("Banana"); ws.Cells["C3"].PutValue(15);
        ws.Cells["A4"].PutValue(3); ws.Cells["B4"].PutValue("Apple");  ws.Cells["C4"].PutValue(7);
        ws.Cells["A5"].PutValue(4); ws.Cells["B5"].PutValue("Cherry"); ws.Cells["C5"].PutValue(20);

        int idx = ws.ListObjects.Add(0, 0, 5, 3, true);
        ListObject tbl = ws.ListObjects[idx];
        tbl.TableStyleType = TableStyleType.TableStyleMedium2;

        tbl.AutoFilter.Filter(1, "Apple");
        wb.Save("FilteredWorkbook.xlsx");

        tbl.RemoveAutoFilter();
        wb.Save("UnfilteredWorkbook.xlsx");
    }
}
```

इसे चलाने पर दो फ़ाइलें बनेंगी:

- **FilteredWorkbook.xlsx** – केवल *Apple* वाली पंक्तियाँ दिखती हैं।  
- **UnfilteredWorkbook.xlsx** – मूल डेटा पुनर्स्थापित।

---

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या यह पुराने .xls फ़ाइलों के साथ काम करता है?**  
उत्तर: हाँ। Aspose.Cells फ़ाइल एक्सटेंशन बदलकर या `SaveOptions` उपयोग करके `.xlsx` और `.xls` दोनों में सेव कर सकता है।

**प्रश्न: यदि मुझे वर्कबुक पहले से सेव होने के बाद फ़िल्टर करना हो तो क्या करें?**  
उत्तर: `new Workbook("path.xlsx")` से फ़ाइल लोड करें, फ़िल्टर लागू करें, फिर फिर से `Save` करें।

**प्रश्न: क्या मैं टेबल नहीं होने वाले *रेंज* पर फ़िल्टर लगा सकता हूँ?**  
उत्तर: बिल्कुल। `worksheet.AutoFilter.Range = "A1:C5";` उपयोग करें और फिर `worksheet.AutoFilter.ApplyFilter();` कॉल करें। हालांकि, टेबल्स बिल्ट‑इन स्टाइलिंग और आसान कॉलम रेफ़रेंसिंग प्रदान करते हैं।

---

## इमेज – विज़ुअल पुष्टि

![C# से बनाई गई Excel वर्कबुक में कॉलम B पर AutoFilter लागू दिखाते हुए स्क्रीनशॉट](/images/autofilter-column-b.png "कॉलम B पर AutoFilter")

*(छवि फ़िल्टर किए हुए दृश्य को दर्शाती है जहाँ केवल “Apple” वाली पंक्तियाँ बची हैं।)*

---

## निष्कर्ष

हमने **C#‑ड्रिवेन Excel ऑटोमेशन** परिदृश्य में **AutoFilter का उपयोग कैसे करें** को कवर किया, **Excel वर्कबुक बनाना**, **कॉलम B में मान के आधार पर पंक्तियों को फ़िल्टर करना**, और अंत में **फ़िल्टर हटाना** जब इसकी आवश्यकता न रहे। मुख्य चरण—इनिशियलाइज़, टेबल जोड़ना, फ़िल्टर लागू करना, और क्लीन‑अप—किसी भी प्रोजेक्ट में पुन: उपयोग योग्य हैं जिसे **excel automation c#** चाहिए।

अगली चुनौती के लिए तैयार हैं? आज़माएँ:

- फ़िल्टर की गई पंक्तियों को हाइलाइट करने के लिए कंडीशनल फ़ॉर्मेटिंग जोड़ना।  
- फ़िल्टर किए हुए डेटा को CSV में एक्सपोर्ट करना ताकि डाउनस्ट्रीम प्रोसेसिंग हो सके।  
- कई फ़िल्टर संयोजित करना (जैसे “Apple” *और* मात्रा > 8)।

प्रयोग करें, चीज़ें तोड़ें, और फिर उन्हें ठीक करें—

## अगला आप क्या सीखें?

- [How to Implement AutoFilter in Excel using Aspose.Cells for .NET (Data Analysis Guide)](/cells/english/net/data-analysis/implement-autofilter-excel-aspose-cells-dotnet/)
- [How to Use Autofilter Not Contains in Aspose.Cells .NET for Excel Data Analysis](/cells/english/net/data-analysis/master-autofilter-not-contains-aspose-cells-net/)
- [How to Implement Excel Autofilter 'EndsWith' Using Aspose.Cells for .NET](/cells/english/net/data-analysis/implement-autofilter-endswith-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}