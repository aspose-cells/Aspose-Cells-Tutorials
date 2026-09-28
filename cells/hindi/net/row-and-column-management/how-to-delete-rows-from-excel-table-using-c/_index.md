---
category: general
date: 2026-09-27
description: C# में Excel तालिका से पंक्तियों को हटाने का तरीका सीखें, एक चरण‑दर‑चरण
  मार्गदर्शिका के साथ जो यह भी दिखाती है कि C# में Excel वर्कबुक को जल्दी कैसे लोड
  किया जाए।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- delete rows from Excel table
- load Excel workbook C#
language: hi
lastmod: 2026-09-27
og_description: C# में Excel तालिका से पंक्तियों को हटाएँ, एक स्पष्ट उदाहरण के साथ।
  यह ट्यूटोरियल यह भी बताता है कि C# में Excel वर्कबुक कैसे लोड करें और सामान्य किनारी
  मामलों को कैसे संभालें।
og_image_alt: Screenshot illustrating delete rows from Excel table using C# code
og_title: C# में Excel तालिका से पंक्तियों को हटाएँ – पूर्ण कोड गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  headline: How to delete rows from Excel table using C#
  type: TechArticle
- description: Learn how to delete rows from Excel table in C# with a step‑by‑step
    guide that also shows how to load Excel workbook C# quickly.
  name: How to delete rows from Excel table using C#
  steps:
  - name: What if the table has a different name or position?
    text: '* **Named table:** Use `ws.ListObjects["MyTableName"]` instead of the index.
      * **Multiple tables:** Loop through `ws.ListObjects` and pick the one that matches
      a condition (e.g., column header names). * **Dynamic row count:** You can compute
      `rowCount` at runtime by inspecting `ws.ListObjects[0].Dat'
  - name: Edge‑case handling
    text: '| Situation | Recommended code change | |----------------------------------------|--------------------------------------------------------------|
      | Table is empty or has fewer rows | Check `ws.ListObjects[0].DataRange.RowCount`
      before deleting. | | Rows to delete exceed table size | Clamp `rowCount`'
  - name: How do I delete rows from **all** tables in a workbook?
    text: '```csharp foreach (Worksheet sheet in workbook.Worksheets) { foreach (ListObject
      tbl in sheet.ListObjects) { // Example: delete the first data row of each table
      if (tbl.DataRange.RowCount > 1) tbl.DeleteRows(1, 1); } } ```'
  - name: Can I delete rows based on a **cell value**?
    text: 'Yes. Scan the `DataRange` for matching cells, collect their zero‑based
      indices, then delete in descending order:'
  - name: What if I need to **preserve formatting**?
    text: '`DeleteRows` removes the entire row from the table but retains the table’s
      style for remaining rows. If you need to keep specific formatting on a row you’re
      deleting, copy the style to another row before deletion.'
  - name: Does this work with **.xls** (Excel 97‑2003) files?
    text: Yes. Aspose.Cells automatically detects the file format, so the same code
      works with `.xls`. Just change the file extension in the `Workbook` constructor.
  - name: Next steps
    text: '* Explore **ClosedXML** or **EPPlus** if you prefer a fully open‑source
      stack. * Combine row deletion with **data validation** to clean spreadsheets
      before importing into a database. * Automate the process for a folder of workbooks
      using `Directory.GetFiles` and a loop.'
  type: HowTo
tags:
- Excel
- C#
- .NET
title: C# का उपयोग करके Excel तालिका से पंक्तियों को कैसे हटाएँ
url: /hi/net/row-and-column-management/how-to-delete-rows-from-excel-table-using-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Excel तालिका से पंक्तियों को हटाएँ – पूर्ण प्रोग्रामिंग गाइड

यदि आपको .xlsx फ़ाइल में **Excel तालिका से पंक्तियों को हटाना** है, तो यह ट्यूटोरियल आपको C# के साथ इसे कैसे करना है, बिल्कुल दिखाता है। आप एक संक्षिप्त, चलाने योग्य उदाहरण देखेंगे जो एक Excel वर्कबुक लोड करता है, पहली तालिका से विशिष्ट पंक्तियों को हटाता है, और परिणाम को सहेजता है। यह तरीका लोकप्रिय Aspose.Cells लाइब्रेरी के साथ काम करता है और अन्य .NET Excel APIs के लिए अनुकूलित किया जा सकता है।

तालिका से पंक्तियों को हटाना आयातित डेटा को साफ़ करने, रिपोर्ट सेक्शन को छोटा करने, या स्प्रेडशीट अपडेट को स्वचालित करने के सामान्य कार्यों में से एक है। इस गाइड के अंत तक आप **C# में Excel वर्कबुक लोड** कर पाएँगे, एक तालिका (ListObject) को ढूँढ़ेंगे, अपनी पसंद की कोई भी पंक्तियाँ हटाएँगे, और संशोधित फ़ाइल को डिस्क पर वापस लिखेंगे।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण स्थापित हो (कोड .NET Framework 4.7+ के साथ भी काम करता है)।
* **Aspose.Cells** NuGet पैकेज का रेफ़रेंस (या कोई भी संगत लाइब्रेरी जो `Workbook`, `Worksheet`, और `ListObject` टाइप्स प्रदान करती हो)।
* `input.xlsx` नाम की इनपुट फ़ाइल को ऐसे फ़ोल्डर में रखें जिसे आप अपने प्रोजेक्ट से रेफ़र कर सकें।
* C# सिंटैक्स और Visual Studio (या आपका पसंदीदा IDE) की बुनियादी समझ।

> **Pro tip:** यदि आप ओपन‑सोर्स विकल्प पसंद करते हैं, तो वही लॉजिक **ClosedXML** के साथ लागू किया जा सकता है – बस Aspose‑विशिष्ट क्लासेज़ को `XLWorkbook`, `IXLWorksheet`, और `IXLTable` से बदल दें।

## चरण 1: C# में Excel वर्कबुक लोड करें

पहला कार्य स्रोत फ़ाइल को मेमोरी में पढ़ना है। सामान्य स्प्रेडशीट आकारों के लिए वर्कबुक लोड करना हल्का होता है और आपको worksheets, tables, और cell values तक पूर्ण पहुँच देता है।

```csharp
using Aspose.Cells;

// Step 1: Load the workbook
// Replace YOUR_DIRECTORY with the actual folder path, e.g. @"C:\Data"
Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");
```

*Why this matters:* `Workbook` .xlsx फ़ाइल की Open XML संरचना को पार्स करता है, जिससे `Worksheet` ऑब्जेक्ट्स का संग्रह उपलब्ध होता है। यदि फ़ाइल नहीं मिलती, तो Aspose `FileNotFoundException` फेंकता है, इसलिए पथ सही रखें।

## चरण 2: लक्ष्य कार्यपत्रक (worksheet) तक पहुँचें

अधिकांश स्प्रेडशीट में कई शीट्स होते हैं; आपको वह शीट चुननी होगी जिसमें वह तालिका हो जिसे आप संशोधित करना चाहते हैं। यहाँ हम पहली शीट (`Worksheets[0]`) का उपयोग करते हैं, जो साधारण फ़ाइलों के लिए सुरक्षित डिफ़ॉल्ट है।

```csharp
// Step 2: Access the first worksheet
Worksheet ws = workbook.Worksheets[0];
```

*Why this matters:* `Worksheet` तालिकाओं (`ListObjects`) का कंटेनर है। सही शीट तक पहुँचने से अनजाने में अन्य डेटा में बदलाव होने से बचा जा सकता है।

## चरण 3: Excel तालिका से पंक्तियों को हटाएँ

Excel तालिकाओं को `ListObject` ऑब्जेक्ट्स द्वारा दर्शाया जाता है। शीट पर पहली तालिका `ListObjects[0]` है। `DeleteRows(startIndex, rowCount)` मेथड **तालिका के डेटा एरिया के सापेक्ष** पंक्तियों को हटाता है, न कि कार्यपत्रक की पूर्ण पंक्ति संख्याओं को।

इस उदाहरण में हम तालिका की दूसरी और तीसरी पंक्तियों को हटाते हैं (हेडर पंक्ति 0 है, इसलिए हम इंडेक्स 1 से शुरू करते हैं)।

```csharp
// Step 3: Delete rows 1 and 2 from the first table (ListObject)
// The first row (index 0) is the header, so we start at index 1
ws.ListObjects[0].DeleteRows(1, 2);
```

### यदि तालिका का नाम या स्थिति अलग हो तो क्या करें?

* **नामित तालिका:** इंडेक्स के बजाय `ws.ListObjects["MyTableName"]` उपयोग करें।
* **एकाधिक तालिकाएँ:** `ws.ListObjects` पर लूप चलाएँ और वह तालिका चुनें जो किसी शर्त (जैसे, कॉलम हेडर नाम) से मेल खाती हो।
* **डायनामिक पंक्ति संख्या:** रन‑टाइम पर `ws.ListObjects[0].DataRange.RowCount` की जाँच करके `rowCount` की गणना कर सकते हैं।

### किनारे‑केस (Edge‑case) संभालना

| स्थिति                              | सिफ़ारिश किया गया कोड परिवर्तन                                      |
|----------------------------------------|--------------------------------------------------------------|
| तालिका खाली है या पंक्तियों की संख्या कम है      | हटाने से पहले `ws.ListObjects[0].DataRange.RowCount` जाँचें। |
| हटाने के लिए पंक्तियों की संख्या तालिका आकार से अधिक है       | `rowCount` को `DataRange.RowCount - startIndex` तक सीमित करें।       |
| किसी शर्त (जैसे, कॉलम C में मान) के आधार पर पंक्तियाँ हटानी हों | `DataRange.Rows` को इटररेट करें, मिलते हुए इंडेक्स एकत्र करें, फिर इंडेक्स स्थिर रखने के लिए उल्टे क्रम में हटाएँ। |

## चरण 4: संशोधित वर्कबुक को सहेजें

हटाने के बाद, वर्कबुक को नई फ़ाइल में (या यदि आप चाहें तो मूल फ़ाइल को ओवरराइट करके) लिखें। सहेजने से एक नया .xlsx बनता है जो अपडेटेड तालिका को दर्शाता है।

```csharp
// Step 4: Save the modified workbook
workbook.Save(@"YOUR_DIRECTORY\output.xlsx");
```

*Why this matters:* `Save` मेमोरी में मौजूद प्रतिनिधित्व को डिस्क पर सीरियलाइज़ करता है। यदि आपको मूल फ़ाइल को संरक्षित रखना है, तो हमेशा अलग पथ पर लिखें।

## पूर्ण, चलाने योग्य उदाहरण

सभी चरणों को मिलाकर आपको एक स्व-निहित प्रोग्राम मिलता है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं।

```csharp
using System;
using Aspose.Cells;

class ExcelRowDeletion
{
    static void Main()
    {
        // Adjust the folder path as needed
        const string folder = @"YOUR_DIRECTORY";

        // Load the workbook (load Excel workbook C#)
        Workbook workbook = new Workbook($"{folder}\\input.xlsx");

        // Access the first worksheet
        Worksheet ws = workbook.Worksheets[0];

        // Ensure the worksheet contains at least one table
        if (ws.ListObjects.Count == 0)
        {
            Console.WriteLine("No tables found on the first worksheet.");
            return;
        }

        // Delete rows 1 and 2 from the first table (skip header)
        ListObject table = ws.ListObjects[0];
        int rowsToDelete = Math.Min(2, table.DataRange.RowCount - 1); // guard against short tables
        if (rowsToDelete > 0)
        {
            table.DeleteRows(1, rowsToDelete);
            Console.WriteLine($"Deleted {rowsToDelete} row(s) from table \"{table.Name}\".");
        }
        else
        {
            Console.WriteLine("Table does not have enough rows to delete.");
        }

        // Save the result
        workbook.Save($"{folder}\\output.xlsx");
        Console.WriteLine("Workbook saved as output.xlsx");
    }
}
```

**अपेक्षित आउटपुट** (कंसोल):

```
Deleted 2 row(s) from table "Table1".
Workbook saved as output.xlsx
```

`output.xlsx` खोलें – पहली तालिका अब उन पंक्तियों को नहीं दिखाती जिन्हें आपने हटाया है, जबकि हेडर पंक्ति बरकरार रहती है।

## सामान्य प्रश्न और विविधताएँ

### मैं वर्कबुक में **सभी** तालिकाओं से पंक्तियों को कैसे हटाऊँ?

```csharp
foreach (Worksheet sheet in workbook.Worksheets)
{
    foreach (ListObject tbl in sheet.ListObjects)
    {
        // Example: delete the first data row of each table
        if (tbl.DataRange.RowCount > 1)
            tbl.DeleteRows(1, 1);
    }
}
```

### क्या मैं **सेल मान** के आधार पर पंक्तियों को हटाएँ?

हाँ। `DataRange` को स्कैन करके मिलते हुए सेल्स खोजें, उनके शून्य‑आधारित इंडेक्स एकत्र करें, फिर इंडेक्स स्थिर रखने के लिए अवरोही क्रम में हटाएँ:

```csharp
var rowsToRemove = new List<int>();
for (int i = 0; i < table.DataRange.RowCount; i++)
{
    var cell = table.DataRange[i, 2]; // column C (zero‑based)
    if (cell.StringValue == "Obsolete")
        rowsToRemove.Add(i);
}

// Delete rows from bottom to top to keep indices valid
rowsToRemove.Sort((a, b) => b.CompareTo(a));
foreach (int rowIdx in rowsToRemove)
    table.DeleteRows(rowIdx, 1);
```

### यदि मुझे **फ़ॉर्मेटिंग बनाए रखना** हो तो क्या करें?

`DeleteRows` तालिका से पूरी पंक्ति हटाता है लेकिन शेष पंक्तियों के लिए तालिका की शैली बरकरार रखता है। यदि आप हटाई जा रही पंक्ति की विशिष्ट फ़ॉर्मेटिंग रखना चाहते हैं, तो हटाने से पहले शैली को किसी अन्य पंक्ति में कॉपी कर लें।

### क्या यह **.xls** (Excel 97‑2003) फ़ाइलों के साथ काम करता है?

हाँ। Aspose.Cells फ़ाइल फ़ॉर्मेट को स्वतः पहचान लेता है, इसलिए वही कोड `.xls` के साथ भी काम करता है। केवल `Workbook` कंस्ट्रक्टर में फ़ाइल एक्सटेंशन बदलें।

## प्रदर्शन सुझाव

* **बैच डिलीशन:** कई पंक्तियों को एक‑एक करके हटाना धीमा हो सकता है। संभव हो तो एक ही `DeleteRows(start, count)` कॉल का उपयोग करें।
* **UI थ्रेड ब्लॉकिंग से बचें:** यदि आप इसे डेस्कटॉप ऐप में इंटीग्रेट कर रहे हैं, तो UI को रिस्पॉन्सिव रखने के लिए वर्कबुक मैनिपुलेशन को बैकग्राउंड थ्रेड पर चलाएँ।
* **सही ढंग से डिस्पोज़ करें:** यद्यपि Aspose.Cells मैनेज्ड मेमोरी उपयोग करता है, बड़े फ़ाइलों के साथ काम करते समय `Workbook` को `using` ब्लॉक में रैप करें ताकि संसाधन तुरंत मुक्त हो सकें।

## निष्कर्ष

आपके पास अब एक पूर्ण, प्रोडक्शन‑रेडी उदाहरण है जो **C# के साथ Excel तालिका से पंक्तियों को हटाता** है। इस गाइड में हमने **C# में Excel वर्कबुक लोड** करना, इच्छित `ListObject` को ढूँढ़ना, सुरक्षित रूप से पंक्तियों को हटाना, और अपडेटेड फ़ाइल को सहेजना कवर किया। किनारे‑केस हैंडलिंग और प्रदर्शन सलाह के साथ, आप इस पैटर्न को अधिक जटिल परिदृश्यों जैसे शर्तीय डिलीशन, कई तालिकाएँ, या वैकल्पिक .NET Excel लाइब्रेरीज़ में अनुकूलित कर सकते हैं।

### अगले कदम

* यदि आप पूरी तरह ओपन‑सोर्स स्टैक पसंद करते हैं तो **ClosedXML** या **EPPlus** को एक्सप्लोर करें।
* डेटाबेस में आयात करने से पहले स्प्रेडशीट को साफ़ करने के लिए **डेटा वैलिडेशन** के साथ पंक्ति डिलीशन को संयोजित करें।
* `Directory.GetFiles` और लूप का उपयोग करके वर्कबुक फ़ोल्डर के लिए प्रक्रिया को ऑटोमेट करें।

विभिन्न पंक्ति रेंज, तालिका नाम, और शर्तीय लॉजिक के साथ प्रयोग करने में संकोच न करें। Happy coding!

## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच का अन्वेषण कर सकें।

- [Load Excel File C# – How to Delete Rows and Remove Specific Rows](/cells/english/net/row-and-column-management/load-excel-file-c-how-to-delete-rows-and-remove-specific-row/)
- [How to Insert and Delete Rows in Excel with Aspose.Cells for .NET: A Comprehensive Guide](/cells/english/net/data-manipulation/aspose-cells-net-insert-delete-excel-rows/)
- [How to Delete Blank Rows in Excel Using Aspose.Cells .NET for Data Cleanup](/cells/english/net/data-manipulation/delete-blank-rows-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}