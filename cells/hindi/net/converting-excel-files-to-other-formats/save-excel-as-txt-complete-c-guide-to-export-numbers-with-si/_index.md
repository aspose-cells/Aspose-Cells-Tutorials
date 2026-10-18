---
category: general
date: 2026-02-21
description: Excel को txt के रूप में सहेजें, महत्वपूर्ण अंकों पर सटीक नियंत्रण के
  साथ। C# में Excel को txt में निर्यात करें और महत्वपूर्ण अंकों को आसानी से सेट करें।
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: hi
og_description: Excel को जल्दी से txt में सहेजें। सीखें कि Excel को txt में कैसे निर्यात
  करें, महत्वपूर्ण अंकों को सेट करें, और C# का उपयोग करके टेक्स्ट आउटपुट को नियंत्रित
  करें।
og_title: Excel को txt के रूप में सहेजें – C# में महत्वपूर्ण अंकों के साथ संख्याएँ
  निर्यात करें
tags:
- C#
- Aspose.Cells
- Excel automation
title: Excel को txt के रूप में सहेजें – महत्वपूर्ण अंकों के साथ संख्याओं को निर्यात
  करने के लिए पूर्ण C# गाइड
url: /hi/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को txt के रूप में सहेजें – महत्वपूर्ण अंकों के साथ संख्याओं को निर्यात करने के लिए पूर्ण C# गाइड

क्या आपको कभी **Excel को txt के रूप में सहेजने** की ज़रूरत पड़ी है लेकिन संख्याओं की सटीकता खोने की चिंता रही है? आप अकेले नहीं हैं। कई डेवलपर्स को Excel को txt में निर्यात करने पर या तो बहुत अधिक दशमलव स्थान या गोलाई की गड़बड़ी का सामना करना पड़ता है।  

इस ट्यूटोरियल में हम आपको एक सीधा‑सरल तरीका दिखाएंगे जिससे आप **Excel को txt में निर्यात** कर सकते हैं जबकि **महत्वपूर्ण अंकों** को सेट कर सकते हैं, ताकि आउटपुट बिल्कुल वही दिखे जैसा आप चाहते हैं। अंत तक आपके पास एक तैयार‑चलाने‑योग्य C# स्निपेट होगा जो वर्कबुक को टेक्स्ट के रूप में सहेजता है, संख्याओं को txt में निर्यात करता है, और संख्यात्मक फ़ॉर्मेट पर पूरी नियंत्रण देता है।

## आप क्या सीखेंगे

- नई वर्कबुक बनाना और संख्यात्मक डेटा लिखना।
- `TxtSaveOptions` का उपयोग करके **महत्वपूर्ण अंकों** को सही तरीके से सेट करना।
- **वर्कबुक को टेक्स्ट के रूप में सहेजना** और परिणाम की पुष्टि करना।
- एज‑केस हैंडलिंग (बड़ी संख्याएँ, नकारात्मक मान, लोकेल समस्याएँ)।
- आउटपुट को आगे ट्यून करने के त्वरित टिप्स (डिलिमिटर परिवर्तन, एन्कोडिंग)।

### पूर्वापेक्षाएँ

- .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.6+ पर भी काम करता है)।
- **Aspose.Cells** NuGet पैकेज (`Install-Package Aspose.Cells`)।
- C# सिंटैक्स की बुनियादी समझ—गहरी Excel इंटरऑप ज्ञान की आवश्यकता नहीं।

> **प्रो टिप:** यदि आप Visual Studio का उपयोग कर रहे हैं, तो *nullable reference types* (`<Nullable>enable</Nullable>`) को सक्षम करें ताकि संभावित null बग्स जल्दी पकड़े जा सकें।

---

## चरण 1: वर्कबुक को इनिशियलाइज़ करें और एक संख्या लिखें

सबसे पहले, हमें एक वर्कबुक ऑब्जेक्ट चाहिए। इसे Excel फ़ाइल की इन‑मेमोरी प्रतिनिधित्व के रूप में सोचें।  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**यह क्यों महत्वपूर्ण है:**  
प्रोग्रामेटिक रूप से वर्कबुक बनाना COM इंटरऑप के ओवरहेड से बचाता है, और `PutValue` स्वचालित रूप से डेटा टाइप का पता लगाता है, जिससे सेल को संख्या के रूप में माना जाता है—not a string.

---

## चरण 2: TxtSaveOptions को कॉन्फ़िगर करें ताकि महत्वपूर्ण अंक नियंत्रित हो सकें

`TxtSaveOptions` क्लास वह जगह है जहाँ जादू होता है। `SignificantDigits` सेट करके आप Aspose.Cells को बताते हैं कि फ़ाइल लिखते समय कितने अर्थपूर्ण अंक रखने हैं।

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**आपको यह सेट क्यों करना चाहिए:**  
जब आप **संख्याओं को txt में निर्यात** करते हैं, तो अक्सर एक संक्षिप्त प्रतिनिधित्व चाहिए (जैसे रिपोर्टिंग सिस्टम जो केवल निश्चित प्रिसीजन स्वीकार करता है)। `SignificantDigits` प्रॉपर्टी मूल संख्या की लंबाई की परवाह किए बिना सुसंगत राउंडिंग सुनिश्चित करती है।

---

## चरण 3: वर्कबुक को टेक्स्ट फ़ाइल के रूप में सहेजें

अब हम वही विकल्पों का उपयोग करके वर्कबुक को डिस्क पर लिखते हैं।

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**आपको क्या दिखेगा:**  
`Numbers.txt` खोलें और आपको एक ही लाइन मिलेगी:

```
12350
```

मूल `12345.6789` को **चार महत्वपूर्ण अंकों** तक राउंड किया गया है, बिल्कुल वही जैसा माँगा गया था।

---

## चरण 4: आउटपुट की पुष्टि करें (वैकल्पिक लेकिन अनुशंसित)

ऑटोमेटेड टेस्ट एक अच्छी आदत है। यहाँ एक त्वरित चेक है जिसे आप सहेजने के तुरंत बाद चला सकते हैं:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

इस ब्लॉक को चलाने पर यदि सब कुछ सही है तो हरा चेकमार्क प्रिंट होगा, जिससे आपको यह भरोसा मिलेगा कि **save excel as txt** ऑपरेशन इच्छित रूप से काम किया।

---

## सामान्य विविधताएँ और एज केस

### कई सेल या रेंज निर्यात करना

यदि आपको पूरी रेंज के लिए **excel को txt में निर्यात** करना है, तो सहेजने से पहले अधिक सेल भरें:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

उसी `TxtSaveOptions` से प्रत्येक मान पर 4‑अंकीय नियम लागू होगा, जिससे परिणाम मिलेगा:

```
12350
0.0001235
-98800
```

### डिलिमिटर बदलना

कुछ डाउनस्ट्रीम सिस्टम टैब‑सेपरेटेड वैल्यूज़ की अपेक्षा करते हैं। डिलिमिटर को इस तरह बदलें:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

अब प्रत्येक रो में सेल टैब से अलग दिखेंगे।

### लोकेल‑विशिष्ट दशमलव विभाजक संभालना

यदि आपके उपयोगकर्ता दशमलव के लिए कॉमा प्रयोग करते हैं, तो कल्चर सेट करें:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

आउटपुट लोकेल का सम्मान करेगा, `12350` को `12 350` (फ़्रेंच में थाउज़ेंड सेपरेटर के रूप में स्पेस) में बदल देगा।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**अपेक्षित `Numbers.txt` सामग्री (डिफ़ॉल्ट डिलिमिटर, 4 महत्वपूर्ण अंक):**

```
12350	0.0001235	-98800
```

टैब (`\t`) दिखाई देता है क्योंकि हमने उदाहरण में डिलिमिटर को डिफ़ॉल्ट (टैब) ही रखा है; यदि आप CSV चाहते हैं तो इसे कॉमा में बदल सकते हैं।

---

## निष्कर्ष

अब आप बिल्कुल जानते हैं कि **Excel को txt के रूप में कैसे सहेजें** जबकि महत्वपूर्ण अंकों की संख्या को नियंत्रित करें। चरण—वर्कबुक बनाना, `TxtSaveOptions.SignificantDigits` सेट करना, और सहेजना—इनसे आप **excel को txt में निर्यात** भरोसेमंद रूप से कर सकते हैं।  

अब आप कर सकते हैं:

- बड़े डेटा सेट के लिए **संख्याओं को txt में निर्यात** करें।
- डिलिमिटर, एन्कोडिंग, या कल्चर सेटिंग्स को किसी भी डाउनस्ट्रीम सिस्टम के अनुसार ट्यून करें।
- निर्यात से पहले अन्य Aspose.Cells सुविधाओं (स्टाइल्स, फॉर्मूले) को जोड़ें।

इसे चलाएँ, `SignificantDigits` को 2 या 6 में बदलें, और देखें आउटपुट कैसे बदलता है। **save workbook as text** की लचीलापन इसे किसी भी डेटा‑एक्सचेंज पाइपलाइन में उपयोगी बनाता है।

---

### अगले संभावित विषय

- कस्टम कॉलम ऑर्डरिंग के साथ **Excel को CSV में निर्यात** करना।
- **txt फ़ाइलों को वापस वर्कबुक में पढ़ना** (`Workbook.Load` with `LoadOptions`)।
- कई वर्कशीट्स को बैच‑प्रोसेस करके एक txt फ़ाइल में समेकित करना।
- बड़े‑पैमाने पर निर्यात के लिए **परफ़ॉर्मेंस ट्यूनिंग** (स्ट्रीमिंग बनाम इन‑मेमोरी)।

यदि आपको कोई समस्या आती है तो टिप्पणी छोड़ें, या अपने प्रोजेक्ट में आपने कैसे कस्टमाइज़ किया, साझा करें। हैप्पी कोडिंग!  

---  

*Image: एक स्क्रीनशॉट जिसमें जनरेटेड `Numbers.txt` फ़ाइल दिख रही है और राउंडेड वैल्यूज़ दिखाए गए हैं।*  
*Alt text: “Numbers.txt फ़ाइल में 12350, 0.0001235, और -98800 दिख रहे हैं, जो 4 महत्वपूर्ण अंकों के साथ Excel को txt में सहेजने के बाद हैं।”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}