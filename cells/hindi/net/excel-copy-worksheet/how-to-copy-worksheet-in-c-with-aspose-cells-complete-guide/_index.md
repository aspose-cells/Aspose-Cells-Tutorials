---
category: general
date: 2026-03-30
description: C# में Aspose.Cells का उपयोग करके वर्कशीट कैसे कॉपी करें – चरण‑दर‑चरण
  गाइड जिसमें सेल रेंज कॉपी करना, शीटों के बीच कॉलम कॉपी करना, वर्कशीट पिवट टेबल कॉपी
  करना और नई वर्कशीट जोड़ने का कोड शामिल है।
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: hi
og_description: Aspose.Cells के साथ C# में वर्कशीट कॉपी करना सीखें। यह गाइड सेल रेंज
  कॉपी करना, पिवट टेबल्स को संरक्षित रखना, शीट्स के बीच कॉलम कॉपी करना, और नई वर्कशीट
  जोड़ने का कोड दिखाता है।
og_title: C# में वर्कशीट कैसे कॉपी करें – पूर्ण Aspose.Cells ट्यूटोरियल
tags:
- Aspose.Cells
- C#
- Excel Automation
title: C# में Aspose.Cells के साथ वर्कशीट कैसे कॉपी करें – पूर्ण गाइड
url: /hi/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में Aspose.Cells के साथ Worksheet कैसे कॉपी करें – पूर्ण गाइड

क्या आपने कभी **how to copy worksheet** को C# में बिना किसी pivot table या formula को खोए कॉपी करने के बारे में सोचा है? आप अकेले नहीं हैं—कई डेवलपर्स को तब समस्या आती है जब उन्हें सभी सुविधाओं को बरकरार रखते हुए शीट को डुप्लिकेट करना पड़ता है। इस ट्यूटोरियल में हम एक व्यावहारिक, एंड‑टू‑एंड समाधान को देखेंगे जो न केवल डेटा को कॉपी करता है बल्कि **copy worksheet pivot table** को भी संरक्षित रखता है, **copy cell range** को संभालता है, और आपको आवश्यक **add new worksheet code** दिखाता है।

हम स्रोत वर्कबुक को लोड करने से लेकर डेस्टिनेशन फ़ाइल को सेव करने तक सब कुछ कवर करेंगे, ताकि आप शीट्स के बीच कॉलम कॉपी कर सकें, ऑब्जेक्ट्स को संरक्षित रख सकें, और अपना कोड साफ़ रख सकें। कोई अस्पष्ट रेफ़रेंस नहीं, सिर्फ एक पूर्ण, चलाने योग्य उदाहरण जिसे आप आज ही अपने प्रोजेक्ट में डाल सकते हैं।

## इस ट्यूटोरियल में क्या कवर किया गया है

- Aspose.Cells के साथ मौजूदा Excel फ़ाइल को लोड करना  
- लक्ष्य शीट बनाने के लिए **add new worksheet code** का उपयोग करना  
- **copy cell range** को परिभाषित करना जिसमें एक pivot table शामिल हो  
- **CopyOptions** को सेट करना ताकि चार्ट, फ़ॉर्मूले, और pivot tables बरकरार रहें  
- **copy columns between sheets** को पंक्ति‑दर‑पंक्ति सटीकता के साथ निष्पादित करना  
- परिणाम को सेव करना और यह सत्यापित करना कि worksheet सही ढंग से कॉपी हुआ है  

इस गाइड के अंत तक आप आत्मविश्वास के साथ “how to copy worksheet” प्रश्न का उत्तर दे पाएँगे, चाहे आप रिपोर्ट्स को ऑटोमेट कर रहे हों या स्प्रेडशीट‑ड्रिवेन UI बना रहे हों।

---

## How to Copy Worksheet – Overview

कोड में डुबने से पहले, चलिए हाई‑लेवल फ्लो को समझते हैं। इसे एक रेसिपी की तरह सोचें:

1. **Load** स्रोत वर्कबुक (`Source.xlsx`)।  
2. **Add** एक नई worksheet जो कॉपी को रखेगी (**add new worksheet code**)।  
3. **Define** वह क्षेत्र जिसे आप डुप्लिकेट करना चाहते हैं (**copy cell range**)।  
4. **Configure** कॉपी विकल्प ताकि pivot table जीवित रहे (**copy worksheet pivot table**)।  
5. **Copy** पंक्तियों और कॉलमों को (**copy columns between sheets**)।  
6. **Save** नई वर्कबुक (`Destination.xlsx`)।  

बस—छह कदम, कोई जादू नहीं। प्रत्येक कदम को नीचे कोड स्निपेट्स और उनके पीछे की तर्क के साथ समझाया गया है।

---

## Step 1 – Load the Source Workbook

सबसे पहले: आपको एक `Workbook` इंस्टेंस चाहिए जो उस फ़ाइल की ओर इशारा करे जिसे आप डुप्लिकेट करना चाहते हैं। यह कदम आवश्यक है क्योंकि Aspose.Cells सीधे फ़ाइल सिस्टम के साथ काम करता है, Office UI के साथ नहीं।

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*क्यों महत्वपूर्ण है:* फ़ाइल को लोड करने से प्रत्येक शीट, सेल, और ऑब्जेक्ट की इन‑मेमोरी प्रतिनिधित्व बनती है। इसके बिना कॉपी करने के लिए कुछ नहीं रहेगा, और बाद में `add new worksheet code` करने की कोशिश विफल होगी क्योंकि स्रोत डेटा मौजूद नहीं है।

---

## Step 2 – Add a New Worksheet (add new worksheet code)

अब हमें कॉपी किए गए डेटा को पेस्ट करने के लिए एक जगह चाहिए। यहीं **add new worksheet code** काम आता है। आप शीट का नाम कुछ भी रख सकते हैं; यहाँ हम इसे `"Copy"` कहते हैं।

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*प्रो टिप:* यदि आप कई शीट्स कॉपी करने की योजना बना रहे हैं, तो `Worksheets.Add` को लूप के अंदर कॉल करें और प्रत्येक शीट को एक अनोखा नाम दें। इससे नाम टकराव से बचेंगे और आपका वर्कबुक साफ़ रहेगा।

---

## Step 3 – Define the Copy Cell Range

एक **copy cell range** Aspose.Cells को ठीक‑ठीक बताता है कि कौन‑से पंक्तियों और कॉलमों को डुप्लिकेट करना है। कई वास्तविक परिदृश्यों में यह रेंज एक pivot table शामिल करती है, इसलिए हमें सटीक होना होगा।

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*क्यों आवश्यक है:* रेंज को स्पष्ट रूप से बताकर आप पूरे शीट को कॉपी करने से बचते हैं (जो संसाधन‑खर्चीला हो सकता है) और यह सुनिश्चित करते हैं कि pivot table कॉपी किए गए क्षेत्र के भीतर रहे। यह **how to copy worksheet** का मूल है जब आपको शीट का केवल एक हिस्सा चाहिए।

---

## Step 4 – Set Copy Options (preserve copy worksheet pivot table)

Aspose.Cells एक `CopyOptions` ऑब्जेक्ट प्रदान करता है जो यह नियंत्रित करता है कि क्या पेस्ट किया जाए। pivot table, चार्ट, और फ़ॉर्मूले को रखने के लिए हम `PasteType.All` सेट करते हैं और `PasteSpecial` को एनेबल करते हैं।

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*व्याख्या:* `PasteType.All` सबसे व्यापक विकल्प है, जबकि `PasteSpecial` इंजन को बताता है कि जटिल ऑब्जेक्ट्स—जैसे pivot tables—को सही ढंग से संभालना है। इस कदम को छोड़ देना एक आम गलती है; कॉपी किया गया शीट अपनी इंटरैक्टिव फीचर्स खो देगा।

---

## Step 5 – Copy Rows and Columns (copy columns between sheets)

अब असली काम: डेटा को वास्तव में मूव करना। हम **copy columns between sheets** को संभालने के लिए `CopyRows` और `CopyColumns` का उपयोग करेंगे। दोनों को चलाने से मर्ज्ड सेल्स और कॉलम चौड़ाई भी संरक्षित रहती है।

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*क्या हो रहा है:* `CopyRows` डेटा को पंक्ति‑दर‑पंक्ति ले जाता है, जबकि `CopyColumns` कॉलम‑दर‑कॉलम। दोनों को चलाने से सुनिश्चित होता है कि पूरा आयताकार ब्लॉक डुप्लिकेट हो गया है, जो तब आवश्यक होता है जब आपको विभिन्न कॉलम चौड़ाई या छिपे हुए कॉलम वाले शीट्स के बीच **copy columns between sheets** करना हो।

---

## Step 6 – Save the Workbook

अंत में, बदलावों को डिस्क पर लिखें। यह कदम **how to copy worksheet** प्रक्रिया को पूरा करता है।

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*सत्यापन टिप:* `Destination.xlsx` खोलें और देखें कि `"Copy"` शीट मूल के समान दिख रही है, pivot tables कार्यशील हैं, और कॉलम चौड़ाई मेल खाती है। यदि कुछ गड़बड़ दिखे, तो `CopyOptions` सेटिंग्स को फिर से देखें।

---

## Edge Cases & Common Variations

### Copying Multiple Worksheets

यदि आपको कई शीट्स डुप्लिकेट करनी हैं, तो ऊपर की लॉजिक को `foreach` लूप में रैप करें:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Preserving Formulas Across Different Workbooks

जब स्रोत और गंतव्य वर्कबुक में अलग‑अलग named ranges हों, तो `copyOptions` को `PasteType.Formulas` के साथ `All` सेट करें:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Large Ranges and Performance

बड़े डेटा सेट (सैकड़ों हज़ार पंक्तियों) के लिए, यदि कॉलम चौड़ाई महत्वपूर्ण नहीं है तो केवल `CopyRows` का उपयोग करें और `CopyColumns` को स्किप करें। इससे कुछ सेकंड बच सकते हैं।

---

## Full Working Example

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम दिया गया है जो हमने चर्चा किए सभी बिंदुओं को सम्मिलित करता है। इसे एक console app में पेस्ट करें, फ़ाइल पाथ को समायोजित करें, और **F5** दबाएँ।

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**अपेक्षित परिणाम:** `Destination.xlsx` खोलने पर एक शीट **Copy** दिखेगी जो `Source.xlsx` की पहली शीट की प्रतिलिपि होगी—जिसमें सभी pivot tables, फ़ॉर्मेटिंग, और कॉलम चौड़ाई शामिल हैं। मूल फ़ाइल अपरिवर्तित रहेगी।

---

## Frequently Asked Questions

**Q: क्या यह .xlsx फ़ाइलों के साथ काम करता है जो Excel 2019 द्वारा बनाई गई हैं?**  
A: बिल्कुल। Aspose.Cells सभी आधुनिक Excel फ़ॉर्मेट्स को सपोर्ट करता है, इसलिए वही कोड `.xlsx`, `.xlsm`, और यहाँ तक कि पुराने `.xls` फ़ाइलों के लिए भी काम करता है।

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}