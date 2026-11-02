---
category: general
date: 2026-02-28
description: C# में Excel तालिका की पंक्तियों को जल्दी हटाएँ। सीखें कि Excel में नामित
  रेंज कैसे जोड़ें, नाम से वर्कशीट तक कैसे पहुँचें, और डुप्लिकेट नाम त्रुटियों से
  बचें।
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: hi
og_description: C# का उपयोग करके एक्सेल टेबल की पंक्तियों को हटाएँ। यह ट्यूटोरियल
  यह भी दिखाता है कि कैसे नामित रेंज जोड़ें और नाम से वर्कशीट तक पहुँचें।
og_title: C# के साथ Excel तालिका में पंक्तियों को हटाएँ – पूर्ण गाइड
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: C# के साथ Excel टेबल की पंक्तियों को हटाएँ – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ Excel तालिका की पंक्तियों को हटाना – पूर्ण प्रोग्रामिंग ट्यूटोरियल

क्या आपको कभी वर्कबुक से **delete rows excel table** करने की ज़रूरत पड़ी है लेकिन यह नहीं पता था कि कौन सा API कॉल उपयोग करना है? आप अकेले नहीं हैं—ज्यादातर डेवलपर्स को पहली बार प्रोग्रामेटिक रूप से तालिका को छोटा करने की कोशिश में यही समस्या आती है।  

इस गाइड में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो न केवल Excel तालिका से पंक्तियों को हटाता है, बल्कि **how to add defined name** (जिसे *named range* भी कहा जाता है) को भी दिखाता है, **access worksheet by name** कैसे किया जाता है, और क्यों किसी अन्य शीट पर डुप्लिकेट नाम जोड़ने से `InvalidOperationException` उत्पन्न होता है।  

लेख के अंत तक आप सक्षम होंगे:

* टैब नाम का उपयोग करके एक वर्कशीट प्राप्त करें।  
* उस शीट की पहली तालिका से डेटा पंक्तियों को सुरक्षित रूप से हटाएँ।  
* एक नामित रेंज बनाएँ जो एक विशिष्ट पते की ओर संकेत करता हो।  
* शीट्स के बीच डुप्लिकेट नामों की समस्याओं को समझें।  

कोई बाहरी दस्तावेज़ीकरण आवश्यक नहीं—आपको जो कुछ भी चाहिए वह यहाँ ही है।

---

## आपको क्या चाहिए

* **DevExpress Spreadsheet** (या कोई भी लाइब्रेरी जो `Workbook`, `Worksheet`, `ListObject` और `Names` ऑब्जेक्ट्स प्रदान करती है)।  
* .NET प्रोजेक्ट जो **.NET 6** या बाद के संस्करण को टार्गेट करता है (कोड .NET Framework 4.8 के साथ भी कम्पाइल होता है)।  
* C# की बुनियादी समझ—यदि आप `foreach` लूप लिख सकते हैं, तो आप तैयार हैं।  

> **Pro tip:** यदि आप DevExpress के मुफ्त Community Edition का उपयोग कर रहे हैं, तो नीचे उपयोग किए गए API व्यावसायिक संस्करण के समान हैं।

---

## चरण 1 – नाम से वर्कशीट तक पहुँचें

सबसे पहला काम यह है कि आप उस शीट को खोजें जिसमें वह तालिका है जिसे आप संशोधित करना चाहते हैं।  
अधिकांश डेवलपर्स आदत से `Worksheets[0]` का उपयोग करते हैं, लेकिन यह आपके कोड को शीट क्रम से बाँध देता है और जैसे ही कोई टैब का नाम बदलता है, यह टूट जाता है।

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Why this matters:* शीट के **name** का उपयोग करके, न कि उसके इंडेक्स से, आप वर्कबुक बदलने पर गलत शीट में अनजाने में बदलाव करने से बचते हैं।  

यदि आप द्वारा दिया गया नाम मौजूद नहीं है, तो लाइब्रेरी `KeyNotFoundException` फेंकती है, जिसे आप पकड़ कर एक उपयोगकर्ता‑मित्र त्रुटि संदेश दिखा सकते हैं।

---

## चरण 2 – Delete Rows Excel Table (सुरक्षित तरीका)

अब जब आपके पास सही वर्कशीट है, चलिए पहली तालिका से डेटा पंक्तियों को हटाते हैं।  
एक सामान्य गलती `DeleteRows(1, rowCount‑1)` को कॉल करना है। **DevExpress 22.2** से यह ओवरलोड **निषिद्ध** है और `InvalidOperationException` फेंकता है। लाइब्रेरी अपेक्षा करती है कि आप पंक्तियों को **तालिका के डेटा रेंज के भीतर** हटाएँ, न कि हेडर पंक्ति को।

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **What if the table is empty?** `if` गार्ड `rowCount = 0` के साथ कॉल को रोकता है, जिससे अन्यथा एक अपवाद उत्पन्न होता।

### दृश्य अवलोकन  

![delete rows excel table example](image.png "Excel तालिका से पंक्तियों को हटाते हुए स्क्रीनशॉट")  

*Alt text: C# कोड में delete rows excel table example*

---

## चरण 3 – How to Add Defined Name (नामित रेंज बनाना)

तालिका को साफ़ करने के बाद आप बाद में किसी विशिष्ट रेंज का संदर्भ देना चाह सकते हैं—जैसे चार्ट या डेटा वैलिडेशन लिस्ट के लिए। यही वह जगह है जहाँ **add named range excel** काम आता है।

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

`Names.Add` मेथड दो पैरामीटर लेता है: पहचानकर्ता और A1‑स्टाइल पता।  
क्योंकि हमने पहले **access worksheet by name** का उपयोग किया था, पता स्ट्रिंग सुरक्षित रूप से किसी भी शीट को संदर्भित कर सकता है बिना इंडेक्स परिवर्तन की चिंता के।

---

## चरण 4 – Named Range on Another Sheet – Duplicate Name Errors से बचें

आप सोच सकते हैं कि आप अलग शीट पर वही पहचानकर्ता पुनः उपयोग कर सकते हैं, जैसे:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

दुर्भाग्यवश, Excel की नामकरण सीमा **वर्कबुक‑व्यापी** है, शीट‑प्रति नहीं। ऊपर दिया गया कॉल `InvalidOperationException` उत्पन्न करता है जिसमें संदेश *“A name with the same identifier already exists.”* होता है।  

### इसे कैसे हल करें

1. **एक अद्वितीय नाम चुनें** (`MyTable_Sheet2`)।  
2. **मौजूदा नाम को हटाएँ** फिर से जोड़ने से पहले (सिर्फ तभी जब आप वास्तव में उसे बदलना चाहते हों)।

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## पूर्ण, चलाने योग्य उदाहरण

सब कुछ मिलाकर, यहाँ एक स्व-निहित कंसोल ऐप है जिसे आप Visual Studio में डाल सकते हैं और `sample.xlsx` फ़ाइल के खिलाफ चला सकते हैं।

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**अपेक्षित परिणाम**

* **Sheet1** की पहली तालिका की सभी डेटा पंक्तियाँ हट जाती हैं, केवल हेडर पंक्ति बचती है।  
* नाम **MyTable** अब `Sheet1!$A$1:$C$5` की ओर संकेत करता है।  
* दूसरा नाम **MyTable_Sheet2** सुरक्षित रूप से **Sheet2** पर एक रेंज को संदर्भित करता है बिना किसी अपवाद के।

---

## सामान्य प्रश्न और किनारे के मामलों

| प्रश्न | उत्तर |
|----------|--------|
| *यदि वर्कबुक में कई तालिकाएँ हों तो क्या होगा?* | इंडेक्स (`worksheet.ListObjects[1]`) या नाम (`worksheet.ListObjects["MyTable"]`) द्वारा सही `ListObject` प्राप्त करें। |
| *क्या मैं कई वर्कशीट्स में फैली तालिका की पंक्तियों को हटा सकता हूँ?* | नहीं—तालिकाएँ केवल एक शीट तक सीमित होती हैं। आपको प्रत्येक शीट के लिए हटाने की लॉजिक दोहरानी होगी। |
| *क्या केवल कुछ पंक्तियों को हटाने का तरीका है?* | हाँ—`table.DeleteRows(startRow, count)` का उपयोग करें जहाँ `startRow` तालिका के डेटा क्षेत्र के भीतर शून्य‑आधारित है। |
| *क्या नामित रेंजें सहेजने के बाद भी बनी रहती हैं?* | बिल्कुल। एक बार जब आप `SaveDocument` कॉल करते हैं, तो नाम वर्कबुक के XML का हिस्सा बन जाते हैं। |
| *मैं वर्कबुक में सभी परिभाषित नामों की सूची कैसे बना सकता हूँ?* | `foreach (var name in workbook.Names) Console.WriteLine(name.Name);` को इटररेट करें। |

---

## निष्कर्ष

हमने C# का उपयोग करके **delete rows excel table** को कवर किया, **add named range excel** को प्रदर्शित किया, और **access worksheet by name** का सही तरीका दिखाया जबकि डरावनी डुप्लिकेट‑नाम अपवाद से बचा।  

पूरा समाधान ऊपर दिए गए कोड स्निपेट में मौजूद है—इसे कॉपी, पेस्ट करें और अपनी फ़ाइलों पर चलाएँ। यहाँ से आप लॉजिक को कई तालिकाओं, डायनामिक रेंज गणनाओं को संभालने, या यहाँ तक कि UI के साथ एकीकृत करने के लिए विस्तारित कर सकते हैं।  

**अगले कदम** आप खोज सकते हैं:

* **named range on another sheet** का उपयोग करके चार्ट सीरीज़ चलाएँ।  
* हटाने की लॉजिक को **ExcelDataReader** के साथ मिलाएँ ताकि डेटा को साफ़ करने से पहले आयात किया जा सके।  
* सरल `foreach (var file in Directory.GetFiles(...))` लूप का उपयोग करके दर्जनों वर्कबुक्स में बड़े पैमाने पर अपडेट को स्वचालित करें।  

C# में Excel ऑटोमेशन के बारे में और प्रश्न हैं? टिप्पणी छोड़ें, और चलिए बातचीत जारी रखें। कोडिंग का आनंद लें!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}