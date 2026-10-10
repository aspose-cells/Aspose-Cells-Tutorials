---
category: general
date: 2026-10-10
description: डेटा टेबल आयात करके, तिथि और मुद्रा फ़ॉर्मेट सेट करके, तथा हेडर पंक्ति
  को संरक्षित रखते हुए, एक्सेल में संख्या फ़ॉर्मेट को जल्दी लागू करें—सभी एक ही चरण
  में।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- set date format excel
- format excel cells date
- set currency format excel
- preserve header row excel
language: hi
lastmod: 2026-10-10
og_description: C# में Aspose.Cells का उपयोग करके Excel में संख्या स्वरूप लागू करें।
  Excel में तिथि स्वरूप सेट करना, मुद्रा स्वरूप सेट करना, और DataTable आयात करते समय
  हेडर पंक्ति को संरक्षित करना सीखें।
og_image_alt: Excel worksheet showing currency and date columns formatted after import
og_title: C# में एक्सेल संख्या स्वरूप लागू करें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: apply number format excel quickly by importing a DataTable, setting
    date and currency formats, and preserving header row excel in a single step.
  headline: How to apply number format excel with Aspose.Cells
  type: TechArticle
tags:
- excel
- aspnet
- csharp
- excel-formatting
title: Aspose.Cells के साथ Excel में नंबर फ़ॉर्मेट कैसे लागू करें
url: /hi/net/excel-custom-number-date-formatting/how-to-apply-number-format-excel-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ Excel में नंबर फ़ॉर्मेट कैसे लागू करें

यदि आपको `DataTable` से डेटा लोड करते समय **Excel में नंबर फ़ॉर्मेट लागू** करना है, तो यह गाइड आपको ठीक‑ठीक दिखाएगा। आप यह भी सीखेंगे कि **Excel में तिथि फ़ॉर्मेट सेट** कैसे करें, **Excel में मुद्रा फ़ॉर्मेट सेट** कैसे करें, और आयात के दौरान **हेडर पंक्ति को संरक्षित** कैसे रखें, ताकि परिणामी वर्कशीट पेशेवर दिखे बिना अतिरिक्त पोस्ट‑प्रोसेसिंग के।

हम लाइब्रेरी को इंस्टॉल करने से लेकर एक पूर्ण, चलाने योग्य स्निपेट लिखने तक सब कुछ कवर करेंगे। अंत तक आप किसी भी `DataTable` को Excel वर्कबुक में इम्पोर्ट कर पाएँगे, संख्यात्मक कॉलम को स्वचालित रूप से फ़ॉर्मेट कर पाएँगे, और हेडर पंक्ति को अपरिवर्तित रख पाएँगे—सिर्फ कुछ ही C# लाइनों में।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* .NET 6.0 या बाद का (कोड .NET Framework 4.6+ के साथ भी काम करता है)
* Visual Studio 2022 (या कोई भी C# IDE जो आप पसंद करते हैं)
* **Aspose.Cells for .NET** – NuGet के माध्यम से इंस्टॉल करें:

```bash
dotnet add package Aspose.Cells
```

* एक `DataTable` स्रोत – उदाहरण में एक हेल्पर मेथड `GetTable()` का उपयोग किया गया है जो सैंपल डेटा रिटर्न करता है।

> **Pro tip:** Aspose.Cells एक कमर्शियल लाइब्रेरी है, लेकिन यह एक फ्री इवैल्यूएशन मोड प्रदान करती है जो 30 दिनों तक वॉटरमार्क को डिसेबल कर देता है।

## Step 1: Create a workbook and access the first worksheet

वर्कबुक ऑब्जेक्ट सभी Excel ऑपरेशन्स का एंट्री पॉइंट है। नया वर्कबुक बनाते ही आपको इंडेक्स 0 पर एक डिफ़ॉल्ट वर्कशीट मिलती है।

```csharp
using Aspose.Cells;
using System;
using System.Data;

class Program
{
    static void Main()
    {
        // Create a new workbook
        Workbook wb = new Workbook();

        // Obtain reference to the first worksheet
        Worksheet sheet = wb.Worksheets[0];
```

*Why this step?*  
`Workbook` फ़ाइल फ़ॉर्मेट, कैलकुलेशन इंजन, और स्टाइल रिपॉज़िटरी को मैनेज करता है। `Worksheet` को जल्दी एक्सेस करने से बाद में इम्पोर्ट मेथड को टार्गेट शीट पास करना आसान हो जाता है।

## Step 2: Retrieve the source data as a DataTable

वास्तविक प्रोजेक्ट्स में डेटा अक्सर डेटाबेस क्वेरी, CSV पार्सर, या API रिस्पॉन्स से आता है। उदाहरण के लिए हम तीन कॉलम वाला एक सरल `DataTable` जेनरेट करते हैं: **Product**, **Price**, और **ReleaseDate**।

```csharp
        // Step 2: Retrieve the source data as a DataTable
        DataTable sourceTable = GetTable();
```

```csharp
        // Helper method that builds a sample DataTable
        static DataTable GetTable()
        {
            DataTable dt = new DataTable();
            dt.Columns.Add("Product", typeof(string));
            dt.Columns.Add("Price", typeof(decimal));
            dt.Columns.Add("ReleaseDate", typeof(DateTime));

            dt.Rows.Add("Widget A", 12.99m, new DateTime(2023, 5, 1));
            dt.Rows.Add("Widget B", 23.50m, new DateTime(2023, 6, 15));
            dt.Rows.Add("Widget C", 7.75m, new DateTime(2023, 7, 30));
            return dt;
        }
```

*Why this step?*  
`DataTable` एक टेबलर इन‑मेमोरी रिप्रेज़ेंटेशन देता है जिसे Aspose.Cells सीधे इम्पोर्ट कर सकता है, कॉलम ऑर्डर और डेटा टाइप्स को संरक्षित रखते हुए।

## Step 3: Prepare a `Style` array – one style per column

Aspose.Cells आपको इम्पोर्ट के दौरान प्रत्येक कॉलम के लिए एक अलग `Style` ऑब्जेक्ट पास करके अलग‑अलग स्टाइल लागू करने की सुविधा देता है। इस एरे की लंबाई स्रोत टेबल के कॉलम की संख्या के बराबर होनी चाहिए।

```csharp
        // Step 3: Prepare an array of Style objects – one for each column
        Style[] columnStyles = new Style[sourceTable.Columns.Count];
        for (int i = 0; i < columnStyles.Length; i++)
        {
            // Each entry must be instantiated before we can set properties
            columnStyles[i] = wb.CreateStyle();
        }
```

*Why this step?*  
यदि आप स्पष्ट रूप से `CreateStyle()` नहीं करते और `Number` सेट करने की कोशिश करते हैं, तो `NullReferenceException` फेंका जाएगा। प्रत्येक `Style` को इनिशियलाइज़ करने से बाद के असाइनमेंट सफल होते हैं।

## Step 4: Assign number formats – currency and date

Excel बिल्ट‑इन नंबर फ़ॉर्मेट को ID द्वारा पहचानता है।  
* **14** – Currency (उदाहरण: `$1,234.00`)  
* **22** – Short Date (`mm/dd/yyyy`)

```csharp
        // Step 4: Assign number formats to the desired columns
        // Column 0 – Product name (no format needed)
        // Column 1 – Currency format (Number format ID 14)
        columnStyles[1].Number = 14;   // set currency format excel

        // Column 2 – Date format (Number format ID 22)
        columnStyles[2].Number = 22;   // set date format excel
```

> **Note:** यदि आपको कस्टम फ़ॉर्मेट चाहिए (जैसे `"¥#,##0.00"`), तो बिल्ट‑इन ID की बजाय `Style.Custom = "¥#,##0.00"` उपयोग करें।

*Why this step?*  
इम्पोर्ट के समय सही **नंबर फ़ॉर्मेट** लागू करने से बाद में सेल्स पर लूप करके फ़ॉर्मेट बदलने की ज़रूरत नहीं रहती। यह सुनिश्चित करता है कि **फ़ॉर्मेट Excel cells date** और **set currency format excel** सभी पंक्तियों में सुसंगत रहें।

## Step 5: Import the DataTable while preserving the header row

`ImportDataTable` मेथड डेटा कॉपी कर सकता है, पहली पंक्ति को हेडर के रूप में रख सकता है, और हमने जो कॉलम स्टाइल तैयार किए हैं उन्हें लागू कर सकता है।

```csharp
        // Step 5: Import the DataTable into the worksheet
        // Parameters:
        //   sourceTable – the DataTable to import
        //   true        – preserve the header row (preserve header row excel)
        //   "A1"        – start cell
        //   columnStyles – array of styles for each column
        sheet.Cells.ImportDataTable(sourceTable, true, "A1", columnStyles);
```

```csharp
        // Save the workbook to disk
        wb.Save("FormattedReport.xlsx");
        Console.WriteLine("Workbook created successfully.");
    }
}
```

**Expected output** – `FormattedReport.xlsx` खोलें और आपको यह दिखेगा:

| उत्पाद | कीमत (मुद्रा) | रिलीज़ तिथि (तारीख) |
|--------|---------------|----------------------|
| Widget A| $12.99        | 05/01/2023           |
| Widget B| $23.50        | 06/15/2023           |
| Widget C| $7.75         | 07/30/2023           |

हेडर पंक्ति अपरिवर्तित है, **Price** कॉलम में मुद्रा सिंबल दिख रहा है, और **ReleaseDate** कॉलम में शॉर्ट डेट फ़ॉर्मेट दिख रहा है—बिना किसी अतिरिक्त स्टाइलिंग कोड के।

### Handling common edge cases

| स्थिति                                 | समाधान |
|----------------------------------------|----------|
| **More columns than styles**           | सुनिश्चित करें कि `columnStyles.Length` बराबर हो `sourceTable.Columns.Count` के। यदि एंट्री नहीं है तो वर्कबुक की डिफ़ॉल्ट स्टाइल उपयोग होगी। |
| **Null values in numeric columns**     | Excel `null` को खाली सेल मानता है; जब बाद में वैल्यू दर्ज होगी तो भी नंबर फ़ॉर्मेट लागू रहेगा। |
| **Custom locale‑specific currency**    | `columnStyles[i].Custom = "\"€\"#,##0.00"` सेट करें और `columnStyles[i].Number = -1` करके बिल्ट‑इन ID को डिसेबल करें। |
| **Large tables ( > 100 000 rows )**    | मेमोरी प्रेशर कम करने के लिए `ImportDataTable` ओवरलोड के साथ `ImportTableOptions` का उपयोग करके डेटा को स्ट्रीम करें। |
| **Applying the same style to multiple columns** | एरे में एक ही `Style` इंस्टेंस को पुनः उपयोग करें (जैसे, `columnStyles[1] = columnStyles[2] = dateStyle;`)। |

## Bonus: Using a custom format string

यदि बिल्ट‑इन ID आपकी ज़रूरतों को पूरा नहीं करती, तो आप एक कस्टम नंबर फ़ॉर्मेट परिभाषित कर सकते हैं:

```csharp
// Example: display Euro currency with no decimal places
Style euroStyle = wb.CreateStyle();
euroStyle.Custom = "\"€\"#,##0";
columnStyles[1] = euroStyle;   // replace the built‑in currency style
```

यह तरीका आपको **फ़ॉर्मेट Excel cells date** और **set currency format excel** पर पूरी नियंत्रण देता है, पूर्वनिर्धारित ID से आगे।

## Conclusion

अब आप जानते हैं कि `DataTable` को Aspose.Cells के साथ इम्पोर्ट करते समय **Excel में नंबर फ़ॉर्मेट लागू** करना कितना प्रभावी है। प्रति‑कॉलम `Style` एरे बनाकर, बिल्ट‑इन या कस्टम नंबर ID असाइन करके, और `ImportDataTable` ओवरलोड का उपयोग करके **हेडर पंक्ति को संरक्षित** करके, आप एक ही ऑपरेशन में तैयार‑टू‑पब्लिश वर्कशीट बना सकते हैं।

### What’s next?

* कस्टम पैटर्न जैसे `"dddd, mmmm dd, yyyy"` के साथ **Excel में तिथि फ़ॉर्मेट सेट** का अन्वेषण करें।  
* इस तकनीक को **कंडीशनल फ़ॉर्मेटिंग** के साथ मिलाकर आउट‑ऑफ़‑रेंज वैल्यूज़ को हाइलाइट करें।  
* पिवट टेबल या चार्ट में **फ़ॉर्मेट Excel cells date** का उपयोग करके डायनामिक रिपोर्टिंग बनाएँ।

विभिन्न नंबर ID या कस्टम स्ट्रिंग्स के साथ प्रयोग करें ताकि आपके संगठन की स्टाइल गाइड के अनुसार फ़ॉर्मेट मिल सके। Happy coding!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [apply number format excel – Step‑by‑Step Guide to Formatting Columns](/cells/english/net/number-and-display-formats-in-excel/apply-number-format-excel-step-by-step-guide-to-formatting-c/)
- [Create Excel Workbook C# – Apply Currency Format and Import DataTable](/cells/english/net/excel-data-import-export/create-excel-workbook-c-apply-currency-format-and-import-dat/)
- [Set date format in Excel with C# – Full Import Formatting Guide](/cells/english/net/excel-custom-number-date-formatting/set-date-format-in-excel-with-c-full-import-formatting-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}