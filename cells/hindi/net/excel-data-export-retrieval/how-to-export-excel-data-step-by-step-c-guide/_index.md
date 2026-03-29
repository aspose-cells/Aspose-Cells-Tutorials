---
category: general
date: 2026-03-29
description: सी# का उपयोग करके एक्सेल टेबल को प्लेन टेक्स्ट में निर्यात करना, स्ट्रिंग
  को फ़ाइल में लिखना, और एक्सेल टेबल को CSV या TXT में बदलना सीखें। इसमें पूरा कोड
  और टिप्स शामिल हैं।
draft: false
keywords:
- how to export excel
- write string to file
- convert excel table
- export table as csv
- save txt file c#
language: hi
og_description: C# में Excel तालिकाओं को टेक्स्ट फ़ाइलों में निर्यात करने का तरीका।
  Excel तालिकाओं को परिवर्तित करने और TXT फ़ाइलें सहेजने के लिए पूर्ण समाधान, कोड
  और सर्वोत्तम प्रथाएँ प्राप्त करें।
og_title: एक्सेल डेटा निर्यात कैसे करें – पूर्ण C# ट्यूटोरियल
tags:
- C#
- Excel
- File I/O
title: एक्सेल डेटा को निर्यात कैसे करें – चरण‑दर‑चरण C# गाइड
url: /hi/net/excel-data-export-retrieval/how-to-export-excel-data-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel डेटा निर्यात करने का तरीका – पूर्ण C# गाइड

क्या आपने कभी सोचा है **how to export Excel** डेटा को मैन्युअली स्प्रेडशीट खोले बिना? शायद आपको एक लेगेसी सिस्टम के लिए टेबल को साधारण टेक्स्ट फ़ाइल में डंप करना पड़े, या आप डेटा‑एनालिसिस पाइपलाइन के लिए तेज़ CSV निर्यात चाहते हैं। इस ट्यूटोरियल में हम एक व्यावहारिक, एंड‑टू‑एंड समाधान पर चलेंगे जो **writes a string to file** करता है और आपको बिल्कुल दिखाएगा कि **convert Excel table** डेटा को C# का उपयोग करके डिलीमिटेड टेक्स्ट फॉर्मेट में कैसे बदलें।

हम सभी चीज़ों को कवर करेंगे—वर्कबुक लोड करना, सही टेबल चुनना, एक्सपोर्ट विकल्प कॉन्फ़िगर करना, और अंत में परिणाम को `.txt` फ़ाइल के रूप में सहेजना। अंत तक आप **export table as CSV** (या कोई भी डिलीमीटर जो आप चुनें) कर पाएँगे और साथ ही **saving txt file C#** प्रोजेक्ट्स के लिए कुछ उपयोगी ट्रिक्स देखेंगे। कोई बाहरी टूल्स आवश्यक नहीं—सिर्फ कुछ NuGet पैकेज और थोड़ा कोड।

---

## आप को क्या चाहिए

- **.NET 6.0+** (या यदि आप क्लासिक पसंद करते हैं तो .NET Framework 4.7.2)
- **Syncfusion.XlsIO** NuGet पैकेज (`ExportTableOptions` क्लास यहाँ स्थित है)
- एक बेसिक C# IDE (Visual Studio, VS Code, Rider—कोई भी चलेगा)
- एक Excel वर्कबुक जिसमें कम से कम एक टेबल हो (उदाहरण में हम `ws.Tables[0]` का उपयोग करेंगे)

> Pro tip: यदि आपके पास पहले से Syncfusion लाइब्रेरी नहीं है, तो कमांड लाइन से चलाएँ  
> `dotnet add package Syncfusion.XlsIO.Net.Core`

## चरण 1 – वर्कबुक खोलें और पहली टेबल प्राप्त करें  

पहला काम है Excel फ़ाइल को लोड करना और उस वर्कशीट का रेफ़रेंस प्राप्त करना जिसमें टेबल है। यह चरण महत्वपूर्ण है क्योंकि **convert excel table** ऑपरेशन `ITable` ऑब्जेक्ट पर काम करता है, न कि कच्ची सेल रेंज पर।

```csharp
using Syncfusion.XlsIO;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        // Load the workbook (replace with your actual file path)
        using (ExcelEngine excelEngine = new ExcelEngine())
        {
            IApplication application = excelEngine.Excel;
            application.DefaultVersion = ExcelVersion.Xlsx;

            // Open the file
            FileStream stream = new FileStream(@"C:\Data\Sample.xlsx", FileMode.Open, FileAccess.Read);
            IWorkbook workbook = application.Workbooks.Open(stream);
            IWorksheet ws = workbook.Worksheets[0];   // First worksheet
```

*Why this matters:* `using` के साथ वर्कबुक खोलने से सभी अनमैनेज्ड रिसोर्स रिलीज़ हो जाते हैं, जिससे बाद में **write string to file** करने पर फ़ाइल‑लॉक समस्याएँ नहीं आतीं।

## चरण 2 – एक्सपोर्ट विकल्प कॉन्फ़िगर करें (सादा टेक्स्ट, हेडर नहीं, सेमीकोलन डिलीमीटर)  

अब हम Syncfusion को बताते हैं कि हम टेबल को कैसे सीरियलाइज़ करना चाहते हैं। `ExportTableOptions` आपको हेडर शामिल करने को टॉगल करने, डिलीमीटर चुनने, और यह तय करने की सुविधा देता है कि आपको स्ट्रिंग चाहिए या बाइट एरे।

```csharp
            // Step 2: Configure export options – plain text, omit headers, ';' delimiter
            var exportOptions = new ExportTableOptions
            {
                ExportAsString = true,      // Returns a string we can write directly
                IncludeHeaders = false,     // Skip column headers if you don’t need them
                Delimiter = ";"             // Change to ',' for classic CSV
            };
```

*Why this matters:* `IncludeHeaders = false` सेट करने से अक्सर डाउनस्ट्रीम सिस्टम की अपेक्षाओं से मेल खाता है जो पहले से कॉलम क्रम जानते हैं। डिलीमीटर बदलना वह तरीका है जिससे आप **export table as CSV** को कस्टम सेपरेटर के साथ कर सकते हैं।

## चरण 3 – टेबल को स्ट्रिंग में एक्सपोर्ट करें  

विकल्प तैयार होने पर, हम `ExportToString` को कॉल करते हैं। यह मेथड पूरी टेबल (सभी पंक्तियों सहित) को लेता है और फ़ाइल आउटपुट के लिए तैयार एकल स्ट्रिंग लौटाता है।

```csharp
            // Step 3: Export the first table to a string using the configured options
            ITable firstTable = ws.Tables[0];               // Access the first table
            string tableText = firstTable.ExportToString(exportOptions);
```

*Why this matters:* `ExportToString` कॉल Excel ग्रिड को डिलीमिटेड फॉर्मेट में बदलने का भारी काम करती है। यह आपके द्वारा सेट किए गए `Delimiter` का सम्मान करती है, इसलिए आपको अतिरिक्त प्रोसेसिंग के बिना एक साफ़ **export table as csv** परिणाम मिलता है।

## चरण 4 – एक्सपोर्टेड टेक्स्ट को फ़ाइल में लिखें  

अंत में, हम स्ट्रिंग को डिस्क पर सहेजते हैं। `File.WriteAllText` **save txt file C#** का सबसे सरल तरीका है; यह फ़ाइल को स्वचालित रूप से बनाता है यदि वह मौजूद नहीं है और अन्यथा उसे ओवरराइट कर देता है।

```csharp
            // Step 4: Write the exported text to a file
            string outputPath = @"C:\Data\ExportedTable.txt";
            File.WriteAllText(outputPath, tableText);
            System.Console.WriteLine($"Table exported successfully to {outputPath}");
        }
    }
}
```

*Why this matters:* स्ट्रिंग को सीधे लिखने से आप अतिरिक्त कन्वर्ज़न स्टेप से बचते हैं। फ़ाइल अब `Value1;Value2;Value3` जैसी पंक्तियों को रखती है, जो किसी भी डाउनस्ट्रीम पार्सर के लिए तैयार है।

## पूर्ण कार्यशील उदाहरण (सभी चरण एक ही जगह)  

नीचे पूर्ण, कॉपी‑पेस्ट‑तैयार प्रोग्राम है जो हमने चर्चा किए सभी चीज़ों को मिलाता है। इसमें एरर हैंडलिंग और स्पष्टता के लिए टिप्पणियाँ शामिल हैं।

```csharp
using Syncfusion.XlsIO;
using System;
using System.IO;

class ExcelExporter
{
    static void Main()
    {
        try
        {
            // 1️⃣ Load workbook and get first worksheet
            using (ExcelEngine excelEngine = new ExcelEngine())
            {
                IApplication app = excelEngine.Excel;
                app.DefaultVersion = ExcelVersion.Xlsx;

                string sourcePath = @"C:\Data\Sample.xlsx";
                using (FileStream fs = new FileStream(sourcePath, FileMode.Open, FileAccess.Read))
                {
                    IWorkbook wb = app.Workbooks.Open(fs);
                    IWorksheet ws = wb.Worksheets[0]; // first sheet

                    // 2️⃣ Set export options (plain text, no headers, ';' delimiter)
                    var opts = new ExportTableOptions
                    {
                        ExportAsString = true,
                        IncludeHeaders = false,
                        Delimiter = ";"
                    };

                    // 3️⃣ Export the first table to a string
                    ITable table = ws.Tables[0];
                    string csvText = table.ExportToString(opts);

                    // 4️⃣ Save the string to a .txt file
                    string destPath = @"C:\Data\ExportedTable.txt";
                    File.WriteAllText(destPath, csvText);

                    Console.WriteLine($"✅ Export complete! File saved at: {destPath}");
                }
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Something went wrong: {ex.Message}");
        }
    }
}
```

**Expected output** (`ExportedTable.txt` की सामग्री):

```
John;Doe;35
Jane;Smith;28
Bob;Brown;42
```

प्रत्येक पंक्ति मूल Excel टेबल की एक पंक्ति से मेल खाती है, जिसमें मान सेमीकोलन से अलग किए गए हैं। यदि आप `Delimiter = ","` बदलते हैं तो आपको एक क्लासिक CSV फ़ाइल मिलेगी।

## आम प्रश्न और किनारे के मामले  

### यदि मेरी वर्कबुक में कई टेबल हैं तो क्या?  
आप बस `ws.Tables[0]` को उचित इंडेक्स में बदल सकते हैं, या `ws.Tables` पर लूप चला सकते हैं:

```csharp
foreach (var tbl in ws.Tables)
{
    string txt = tbl.ExportToString(opts);
    // Save each table to a separate file or concatenate as needed
}
```

### मैं कॉलम हेडर कैसे शामिल करूँ?  
`ExportTableOptions` में `IncludeHeaders = true` सेट करें। यह तब उपयोगी है जब डाउनस्ट्रीम सिस्टम हेडर रो की अपेक्षा करता है।

### क्या मैं डायनामिक रूप से किसी अलग फ़ोल्डर में एक्सपोर्ट कर सकता हूँ?  
बिल्कुल। `Path.Combine` को `Environment.GetFolderPath(Environment.SpecialFolder.Desktop)` या किसी भी यूज़र‑प्रोवाइडेड पाथ के साथ उपयोग करें ताकि समाधान अधिक लचीला बन सके।

### बड़ी फ़ाइलों के बारे में क्या?  
बड़े टेबलों के लिए, पूरी स्ट्रिंग को मेमोरी में लोड करने के बजाय आउटपुट को स्ट्रीम करने पर विचार करें:

```csharp
using (StreamWriter writer = new StreamWriter(outputPath))
{
    writer.Write(table.ExportToString(opts));
}
```

### क्या यह .NET Core पर काम करता है?  
हां—Syncfusion.XlsIO .NET 5/6/7 को सपोर्ट करता है। बस उचित NuGet पैकेज को रेफ़रेंस करें और आप तैयार हैं।

## विश्वसनीय एक्सपोर्ट के लिए प्रो टिप्स  

- **Validate the file path** लिखने से पहले सत्यापित करें। एक गायब डायरेक्टरी `DirectoryNotFoundException` फेंकेगी।  
- **Check `ExportAsString`** केवल तभी करें जब टेबल मेमोरी में आराम से फिट हो; अन्यथा, बड़े डेटा सेट के लिए `ExportToStream` उपयोग करें।  
- **Mind the culture**: यदि आपके डेटा में दशमलव विभाजक के रूप में कॉमा है, तो CSV पार्सिंग त्रुटियों से बचने के लिए सेमीकोलन (`;`) या टैब (`\t`) डिलीमीटर चुनें।  
- **Version lock**: Syncfusion कभी‑कभी API सिग्नेचर बदलता है। अपने बिल्ड को पुनरुत्पादित रखने के लिए NuGet संस्करण को पिन करें (`<PackageReference Include="Syncfusion.XlsIO.Net.Core" Version="21.2.0.44" />`)।

## निष्कर्ष  

इस गाइड में हमने C# का उपयोग करके Excel टेबल को प्लेन‑टेक्स्ट फ़ाइलों में **how to export Excel** करने का प्रदर्शन किया। वर्कबुक लोड करके, `ExportTableOptions` कॉन्फ़िगर करके, टेबल को स्ट्रिंग में एक्सपोर्ट करके, और अंत में **writing the string to file** करके, अब आपके पास **convert excel table** डेटा, **export table as csv**, और **save txt file C#** कार्यों के लिए एक मजबूत पैटर्न है।

बिना झिझक प्रयोग करें—डिलीमीटर बदलें, हेडर शामिल करें, या कई टेबलों पर लूप चलाएँ। वही तरीका CSV रिपोर्ट बनाने, डेटा को लेगेसी पार्सर में फीड करने, या बस स्प्रेडशीट सामग्री को हल्की टेक्स्ट फ़ाइलों के रूप में आर्काइव करने में काम आता है।

क्या आपके पास और परिदृश्य हैं जिन्हें आप हल करना चाहते हैं? शायद आपको **write string to file** असिंक्रोनस रूप से चाहिए, या आप आउटपुट को तुरंत ज़िप करना चाहते हैं। हमारे अगले ट्यूटोरियल देखें *asynchronous file I/O in C#* और *zipping files with .NET* ताकि गति बनी रहे।

कोडिंग का आनंद लें! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}