---
category: general
date: 2026-03-18
description: C# में Excel डेटा को DataTable में निर्यात करने का तरीका, जिसमें विशिष्ट
  कोशिकाओं को संभालने वाला कोड, Excel को DataTable में बदलना, और संख्याओं का स्वरूपण
  शामिल है। विशिष्ट कोशिकाओं को निर्यात करना और अधिक जानें।
draft: false
keywords:
- how to export excel
- convert excel to datatable
- export specific cells
- excel to datatable c#
- excel range to datatable
language: hi
og_description: C# में Excel डेटा को DataTable में कैसे निर्यात करें। यह ट्यूटोरियल
  दिखाता है कि विशिष्ट सेल्स को कैसे निर्यात करें, Excel को DataTable में कैसे बदलें,
  और आसानी से संख्याओं को कैसे फ़ॉर्मेट करें।
og_title: C# में Excel को DataTable में निर्यात कैसे करें – पूर्ण मार्गदर्शिका
tags:
- C#
- Excel
- DataTable
- Aspose.Cells
title: C# में Excel को DataTable में निर्यात करने का तरीका – चरण‑दर‑चरण गाइड
url: /hi/net/excel-data-import-export/how-to-export-excel-to-a-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को C# में DataTable में निर्यात कैसे करें – चरण‑दर‑चरण गाइड

क्या आप कभी सोचते रहे हैं **Excel को निर्यात** करने के बारे में `DataTable` में बिना फ़ॉर्मेट खोए? आप अकेले नहीं हैं—डेवलपर्स को लगातार एक स्प्रेडशीट का हिस्सा मेमोरी में लाना पड़ता है रिपोर्टिंग, वैधता, या बल्क‑इंसर्ट ऑपरेशन्स के लिए। अच्छी खबर? कुछ ही पंक्तियों के C# कोड से आप एक सटीक रेंज (जैसे *A1:F11*) निर्यात कर सकते हैं, हर सेल को स्ट्रिंग के रूप में ट्रीट कर सकते हैं, और एक कस्टम नंबर फ़ॉर्मेट भी लागू कर सकते हैं।

इस ट्यूटोरियल में हम वह सब कवर करेंगे जो आपको जानना आवश्यक है: वर्कबुक लोड करना, **विशिष्ट सेल निर्यात** को कॉन्फ़िगर करना, रेंज को `DataTable` में बदलना, और खाली पंक्तियों या लोकल‑निर्भर संख्याओं जैसे एज केस को संभालना। अंत तक आपके पास एक पुन: उपयोग योग्य मेथड होगा जो **excel to datatable c#** परिदृश्यों में प्रोडक्शन कोड के साथ काम करता है।

> **आवश्यकताएँ** – आपको Aspose.Cells for .NET लाइब्रेरी की जरूरत पड़ेगी (या कोई समान API जो `ExportDataTable` प्रदान करता हो)। उदाहरण .NET 6+ मानता है, लेकिन अवधारणाएँ पहले के संस्करणों पर भी लागू होती हैं।

---

## आप क्या सीखेंगे

- Aspose.Cells का उपयोग करके **Excel को DataTable में बदलना**।
- सभी मानों को स्ट्रिंग के रूप में ट्रीट करते हुए एक कस्टम रेंज (`excel range to datatable`) निर्यात करना।
- निर्यात के दौरान दो दशमलव स्थान वाला नंबर फ़ॉर्मेट (`#,#00.00`) लागू करना।
- सामान्य समस्याएँ (null पंक्तियाँ, छिपे कॉलम) और उन्हें कैसे टालें।
- एक तैयार‑कॉपी, पूरी तरह चलने योग्य कोड नमूना।

---

## आवश्यकताएँ और सेटअप

कोड में डुबकी लगाने से पहले सुनिश्चित करें कि आपके पास ये हैं:

1. **Aspose.Cells for .NET** NuGet के माध्यम से इंस्टॉल किया हुआ:

   ```bash
   dotnet add package Aspose.Cells
   ```

2. एक Excel फ़ाइल (`input.xlsx`) जिसे आप किसी फ़ोल्डर में रख सकते हैं, उदाहरण के लिए `YOUR_DIRECTORY/input.xlsx`।
3. एक प्रोजेक्ट जो .NET 6 या बाद के संस्करण को टार्गेट करता हो (नीचे दिखाए गए `using` स्टेटमेंट्स बॉक्स से बाहर काम करेंगे)।

> **प्रो टिप:** यदि आप कोई अलग लाइब्रेरी (जैसे EPPlus या ClosedXML) उपयोग कर रहे हैं, तो अवधारणा वही रहती है—वर्कबुक लोड करें, रेंज चुनें, और वह मेथड कॉल करें जो `DataTable` लौटाता है।

---

## चरण 1: वर्कबुक लोड करें और पहली वर्कशीट प्राप्त करें

सबसे पहले आपको एक `Workbook` ऑब्जेक्ट चाहिए जो आपकी Excel फ़ाइल का प्रतिनिधित्व करता है। एक बार मिलने के बाद आप इंडेक्स या नाम से किसी भी वर्कशीट तक पहुँच सकते हैं।

```csharp
using Aspose.Cells;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // Load the workbook from disk
            Workbook workbook = new Workbook(@"YOUR_DIRECTORY\input.xlsx");

            // Grab the first worksheet (index 0)
            Worksheet worksheet = workbook.Worksheets[0];

            // Continue with export options...
        }
    }
}
```

**क्यों महत्वपूर्ण है:** वर्कबुक को जल्दी लोड करने से आप उसकी संरचना (छिपी शीट्स, प्रोटेक्शन) का निरीक्षण कर सकते हैं, इससे पहले कि आप तय करें कि कौन से सेल निर्यात करने हैं। यदि फ़ाइल बड़ी है, तो केवल आवश्यक भागों को स्ट्रीम करने के लिए `LoadOptions` का उपयोग करने पर विचार करें।

---

## चरण 2: निर्यात विकल्प कॉन्फ़िगर करें – सभी मानों को स्ट्रिंग के रूप में ट्रीट करें

जब आप डेटा को डाउनस्ट्रीम प्रोसेसिंग (जैसे SQL में बल्क इन्सर्ट) के लिए निर्यात करते हैं, तो अक्सर आप **सुसंगत स्ट्रिंग प्रतिनिधित्व** चाहते हैं। यह बाद में टाइप‑मिसमैच त्रुटियों से बचाता है।

```csharp
// Configure export behavior
ExportTableOptions exportOptions = new ExportTableOptions
{
    // Force every cell to be returned as a string, regardless of its original type
    ExportAsString = true,

    // Apply a two‑decimal‑place format to numeric cells
    NumberFormat = "#,##0.00"
};
```

**व्याख्या:**  
- `ExportAsString = true` Aspose.Cells को मूल सेल टाइप को अनदेखा करके फ़ॉर्मेटेड टेक्स्ट लौटाने को कहता है।  
- `NumberFormat = "#,##0.00"` सुनिश्चित करता है कि `1234.5` जैसे नंबर `"1,234.50"` बन जाएँ—वित्तीय रिपोर्टों के लिए उपयोगी।

यदि आपको मूल डेटा टाइप चाहिए, तो बस `ExportAsString` को `false` सेट करें और स्वयं रूपांतरण संभालें।

---

## चरण 3: विशिष्ट रेंज (A1:F11) को DataTable में निर्यात करें

अब **विशिष्ट सेल निर्यात** का मुख्य भाग आता है। `ExportDataTable` मेथड शुरू/समाप्त पंक्ति/कॉलम इंडेक्स (शून्य‑आधारित) लेता है और हेडर शामिल करने का फ़्लैग भी लेता है।

```csharp
// Export cells A1:F11 (rows 0‑10, columns 0‑5) including the header row
DataTable table = worksheet.ExportDataTable(
    startRow: 0,
    startColumn: 0,
    endRow: 10,
    endColumn: 5,
    includeColumnNames: true,
    exportOptions: exportOptions);
```

**आपको क्या मिलेगा:** एक `DataTable` जिसमें 11 पंक्तियाँ (हेडर सहित) और 6 कॉलम (`A`‑`F`) होंगे। सभी मान `exportOptions` के अनुसार स्ट्रिंग के रूप में फ़ॉर्मेटेड होंगे।

---

## चरण 4: परिणाम सत्यापित करें – कंसोल में प्रिंट करें

टेबल को किसी अन्य कॉम्पोनेन्ट को सौंपने से पहले आउटपुट की जाँच करना हमेशा अच्छा विचार है।

```csharp
// Simple console dump
foreach (DataRow row in table.Rows)
{
    foreach (var item in row.ItemArray)
    {
        Console.Write($"{item}\t");
    }
    Console.WriteLine();
}
```

आपको कुछ इस तरह दिखना चाहिए:

```
Id      Name        Qty     Price   Total   Date
1       Widget A    10      2.50    25.00   2026-01-01
2       Widget B    5       3.75    18.75   2026-01-02
...
```

ध्यान दें कि संख्यात्मक कॉलम दो दशमलव स्थान के साथ दिखाए जा रहे हैं, बिल्कुल जैसा हमने निर्दिष्ट किया था।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

नीचे पूरा प्रोग्राम दिया गया है जो सभी भागों को जोड़ता है। इसे एक नए कंसोल प्रोजेक्ट में डालें, फ़ाइल पाथ समायोजित करें, और चलाएँ—कोई अतिरिक्त कॉन्फ़िगरेशन नहीं चाहिए।

```csharp
using Aspose.Cells;
using System;
using System.Data;

namespace ExcelExportDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // 1️⃣ Load workbook and select worksheet
            // -------------------------------------------------
            string filePath = @"YOUR_DIRECTORY\input.xlsx";
            Workbook workbook = new Workbook(filePath);
            Worksheet worksheet = workbook.Worksheets[0];

            // -------------------------------------------------
            // 2️⃣ Set export options – strings + number format
            // -------------------------------------------------
            ExportTableOptions exportOptions = new ExportTableOptions
            {
                ExportAsString = true,
                NumberFormat = "#,##0.00"
            };

            // -------------------------------------------------
            // 3️⃣ Export range A1:F11 (rows 0‑10, cols 0‑5)
            // -------------------------------------------------
            DataTable table = worksheet.ExportDataTable(
                startRow: 0,
                startColumn: 0,
                endRow: 10,
                endColumn: 5,
                includeColumnNames: true,
                exportOptions: exportOptions);

            // -------------------------------------------------
            // 4️⃣ Output to console for verification
            // -------------------------------------------------
            Console.WriteLine("=== Exported DataTable ===");
            foreach (DataRow row in table.Rows)
            {
                foreach (var cell in row.ItemArray)
                {
                    Console.Write($"{cell}\t");
                }
                Console.WriteLine();
            }

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**कोड से मुख्य निष्कर्ष:**  

- `ExportTableOptions` ऑब्जेक्ट पुन: उपयोग योग्य है; यदि आपको कई रेंज निर्यात करनी हों तो आप इसे कई `ExportDataTable` कॉल्स में पास कर सकते हैं।  
- इंडेक्सिंग **0** से शुरू होती है, इसलिए `A1` का मान `(0,0)` है।  
- `includeColumnNames` को `true` सेट करने से पहली पंक्ति स्वचालित रूप से कॉलम हेडर बन जाती है—डेटा‑टेबल के बाद के ऑपरेशन्स के लिए बहुत उपयोगी।

---

## एज केस और सामान्य प्रश्नों का समाधान

### यदि वर्कशीट में छिपी पंक्तियाँ या कॉलम हों तो क्या करें?

Aspose.Cells डिफ़ॉल्ट रूप से विज़िबिलिटी का सम्मान करता है। यदि आपको छिपा डेटा निर्यात करना है, तो `exportOptions.ExportHiddenRows = true` और `ExportHiddenColumns = true` सेट करें।

### मेरी Excel फ़ाइल में फ़ॉर्मूले हैं—क्या मुझे गणना किए हुए मान मिलेंगे?

हां। डिफ़ॉल्ट रूप से `ExportDataTable` **दिखाए गए मान** (फ़ॉर्मूले का परिणाम) लौटाता है। यदि आप कच्चा फ़ॉर्मूला टेक्स्ट चाहते हैं, तो `exportOptions.ExportFormulas = true` सेट करें।

### पूरी तरह खाली पंक्तियों को कैसे छोड़ें?

निर्यात के बाद आप `DataTable` को इस तरह साफ़ कर सकते हैं:

```csharp
foreach (DataRow row in table.Rows.Cast<DataRow>()
                                   .Where(r => r.ItemArray.All(c => c == DBNull.Value || string.IsNullOrWhiteSpace(c.ToString()))).ToList())
{
    table.Rows.Remove(row);
}
```

### क्या मैं गैर‑सतत रेंज (जैसे A1:B5 और D1:E5) निर्यात कर सकता हूँ?

Aspose.Cells एक ही कॉल में डिसजॉइंट रेंज को सपोर्ट नहीं करता। इसके बजाय प्रत्येक ब्लॉक को अलग‑अलग निर्यात करें और फिर प्राप्त `DataTable` को मैन्युअल रूप से मर्ज करें।

---

## प्रदर्शन टिप्स

- **`ExportTableOptions` को पुन: उपयोग करें** कई निर्यातों के लिए; हर बार नया इंस्टेंस बनाना अतिरिक्त ओवरहेड जोड़ता है लेकिन कोड को गंदा नहीं करता।  
- **`LoadOptions` के साथ बड़े फ़ाइलों को स्ट्रीम करें** ताकि पूरी वर्कबुक मेमोरी में लोड न हो।  
- यदि आपको केवल तेज़ CSV निर्यात चाहिए, तो `ExportDataTable` के बजाय सीधे CSV लिखना मेमोरी‑कुशल हो सकता है।

---

## निष्कर्ष

हमने यह दिखाया कि **Excel डेटा को `DataTable` में निर्यात** कैसे किया जाए, फ़ॉर्मेटिंग को नियंत्रित किया जाए, विशिष्ट सेल रेंज को संभाला जाए, और सभी मान स्ट्रिंग के रूप में प्राप्त हों। पूरा उदाहरण एक साफ़, प्रोडक्शन‑रेडी दृष्टिकोण प्रस्तुत करता है जिसे आप **convert excel to datatable**, **export specific cells**, या किसी भी **excel range to datatable** परिदृश्य में अनुकूलित कर सकते हैं।

इसे आज़माएँ: रेंज बदलें, `ExportAsString` टॉगल करें, या `DataTable` को सीधे Entity Framework में बल्क इन्सर्ट के लिए पाइप करें। इस ठोस नींव के साथ संभावनाएँ असीमित हैं।

---

### अगले कदम और संबंधित विषय

- **DataTable को फिर से Excel में इम्पोर्ट करना** – `ImportDataTable` के साथ रिवर्स ऑपरेशन सीखें।  
- **DataTable को SQL Server में बल्क इन्सर्ट करना** – तेज़ लोड के लिए `SqlBulkCopy` का उपयोग करें।  
- **EPPlus या ClosedXML के साथ काम करना** – वैकल्पिक लाइब्रेरीज़ के साथ वही कार्य कैसे दिखता है, देखें।  
- **निर्यात पर सेल फ़ॉर्मेटिंग** – तिथि फ़ॉर्मेट, कस्टम कल्चर सेटिंग्स आदि के लिए `ExportTableOptions` को और एक्सप्लोर करें।

कोई प्रश्न या अलग उपयोग‑केस है? टिप्पणी करें, और चर्चा जारी रखें। हैप्पी कोडिंग!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}