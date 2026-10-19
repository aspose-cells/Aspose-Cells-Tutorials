---
category: general
date: 2026-06-30
description: Aspose.Cells का उपयोग करके Excel वर्कबुक में कंडीशनल फॉर्मेटिंग बनाएं।
  सीखें कि कैसे सेल बैकग्राउंड सेट करें, सेल्स को रैंक करें, और प्रोग्रामेटिकली फ़ाइल
  बनाएं।
draft: false
keywords:
- create conditional formatting
- create excel workbook
- set cell background
- how to rank cells
- how to use aspose
language: hi
og_description: Aspose.Cells का उपयोग करके Excel वर्कबुक में कंडीशनल फॉर्मेटिंग बनाएं।
  सेल बैकग्राउंड सेट करने, सेल्स को रैंक करने और Excel को ऑटोमेट करने के लिए इस पूर्ण
  ट्यूटोरियल का पालन करें।
og_title: Aspose.Cells के साथ Excel में कंडीशनल फ़ॉर्मेटिंग बनाएं
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create conditional formatting in an Excel workbook using Aspose.Cells.
    Learn how to set cell background, rank cells, and build the file programmatically.
  headline: Create Conditional Formatting in Excel with Aspose.Cells – Step‑by‑Step
    Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: Aspose.Cells के साथ Excel में कंडीशनल फॉर्मेटिंग बनाएं – चरण‑दर‑चरण गाइड
url: /hi/net/excel-conditional-formatting/create-conditional-formatting-in-excel-with-aspose-cells-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में Conditional Formatting बनाएं Aspose.Cells के साथ – चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है कि UI खोले बिना Excel फ़ाइल में **conditional formatting** कैसे बनाएं? आप अकेले नहीं हैं। कई डेवलपर्स को तुरंत **excel workbook** फ़ाइलें बनानी होती हैं, और इसे प्रोग्रामेटिकली करने से मैन्युअल काम में कई घंटे बचते हैं। इस ट्यूटोरियल में हम आपको बिल्कुल दिखाएंगे कि **conditional formatting** कैसे बनाएं, सेल्स को स्टाइल करें, और शीर्ष मानों को रैंक भी करें—सब कुछ शक्तिशाली Aspose.Cells लाइब्रेरी for .NET के साथ।

हम एक वास्तविक‑दुनिया का उदाहरण देखेंगे: एक स्कोर शीट जेनरेट करना, हाई स्कोर को हल्के‑हरा रंग में हाइलाइट करना, और टॉप‑3 परफ़ॉर्मर्स को गोल्ड बैकग्राउंड देना। अंत तक आप जानेंगे **how to set cell background**, **how to rank cells**, और **how to use Aspose** के साथ उन्नत Excel ऑटोमेशन कैसे करें। कोई फालतू बातें नहीं, सिर्फ एक पूर्ण, रन‑एबल सॉल्यूशन जिसे आप किसी भी C# प्रोजेक्ट में डाल सकते हैं।

## आप क्या सीखेंगे

- Aspose.Cells का उपयोग करके **create excel workbook** कैसे करें  
- रैंडम डेटा (स्कोर) के साथ एक रेंज को कैसे भरें  
- सॉलिड रंगों के साथ **set cell background** कैसे सेट करें  
- फ़ॉर्मूला‑आधारित नियम लागू करके **rank cells** कैसे करें और टॉप तीन को हाइलाइट करें  
- परिणाम को .xlsx फ़ाइल के रूप में कैसे सेव करें  

Prerequisites: .NET 6+ (या .NET Framework 4.6+), Visual Studio (या कोई भी C# IDE), और Aspose.Cells NuGet पैकेज का रेफ़रेंस। अगर आपने पहले कभी Aspose का उपयोग नहीं किया है, तो चिंता न करें—हम **how to use Aspose** को शुरुआती स्तर से कवर करेंगे।

---

![Conditional Formatting का उदाहरण बनाएं](https://example.com/images/create-conditional-formatting.png "जनरेट किए गए Excel फ़ाइल में Conditional Formatting दिखाने वाला स्क्रीनशॉट")

*Image alt text: Aspose.Cells से जनरेट किए गए Excel वर्कबुक में conditional formatting का उदाहरण*.

## Aspose.Cells के साथ Excel Workbook कैसे बनाएं

पहले बात यह है कि आपको एक workbook ऑब्जेक्ट चाहिए जिससे आप काम कर सकें। Aspose.Cells इसे एक‑लाइनर बना देता है।

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Instantiate a new workbook and give the first sheet a friendly name
    Workbook workbook = new Workbook();                 // creates an empty workbook
    Worksheet sheet = workbook.Worksheets[0];           // grab the default worksheet
    sheet.Name = "Scores";                              // rename it to something meaningful
```

हम शीट का नाम क्यों बदलते हैं? एक स्पष्ट नाम (जैसे **Scores**) बाद में रेफ़रेंस करना आसान बनाता है, खासकर जब आप फ़ाइल को गैर‑तकनीकी उपयोगकर्ताओं के साथ शेयर करते हैं।  

अब workbook मौजूद है, चलिए कॉलम A को रैंडम स्कोर से भरते हैं।

## डेटा भरें – रैंडम स्कोर बनाना

```csharp
    // Step 2: Populate A2:A21 with random values between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)               // 20 rows of data
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }
```

एक त्वरित नोट: `PutValue` डेटा टाइप को स्वतः पहचान लेता है, इसलिए आपको `int` में कास्ट करने की ज़रूरत नहीं है। लूप `i = 0` से शुरू होता है लेकिन `i + 1` पंक्ति में लिखता है क्योंकि Excel पंक्तियाँ 1‑आधारित होती हैं जबकि `Cells` कलेक्शन 0‑आधारित है।

## हाई स्कोर के लिए Cell Background कैसे सेट करें

अब हम **create conditional formatting** करेंगे जो किसी भी स्कोर ≥ 80 को हल्के‑हरा रंग में पेंट करेगा।

```csharp
    // Step 3: Define a conditional formatting range (A2:A21)
    int firstRow = 1, lastRow = 20;                     // zero‑based indices for rows 2‑21
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];

    // Add a rule: cell value >= 80 → light‑green background
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");

    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;
```

`ForegroundColor` प्रॉपर्टी फ़िल रंग को नियंत्रित करती है, जबकि `Pattern = BackgroundType.Solid` Excel को ग्रेडिएंट या पैटर्न के बजाय सॉलिड फ़िल उपयोग करने को कहता है। यह **how to set cell background** का मुख्य हिस्सा है, जो संख्यात्मक थ्रेशहोल्ड पर आधारित है।

## Cells को Rank करें और Top‑3 को हाइलाइट करें

रैंकिंग थोड़ा जटिल है क्योंकि हमें एक फ़ॉर्मूला चाहिए जो प्रत्येक सेल को पूरी रेंज के मुकाबले मूल्यांकन करे। Aspose.Cells आपको वही Excel फ़ॉर्मूला सिंटैक्स उपयोग करने देता है जो आप UI में टाइप करेंगे।

```csharp
    // Step 4: Add a formula‑based rule to color the top‑3 scores gold
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);

    // The formula uses the RANK function; note the absolute references ($) lock the range
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";

    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;
```

फ़ॉर्मूला में `A2` क्यों है? Aspose फ़ॉर्मूला को रेंज के प्रत्येक सेल के सापेक्ष मूल्यांकन करता है, इसलिए `A2` स्वचालित रूप से `A3`, `A4` आदि में शिफ्ट हो जाता है जब नियम पंक्ति‑दर‑पंक्ति लागू होता है। `RANK` फ़ंक्शन निर्दिष्ट रेंज में मान की स्थिति लौटाता है, और `<=3` भाग सुनिश्चित करता है कि केवल तीन सबसे उच्च स्कोर को गोल्ड फ़िल मिले।

## Workbook को कैसे Save करें

```csharp
    // Step 5: Persist the workbook to disk
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

`YOUR_DIRECTORY` को उस पूर्ण या रिलेटिव पाथ से बदलें जहाँ आपका एप्लिकेशन लिख सकता है। मेथड चलाने के बाद, फ़ाइल को Excel में खोलें और आप देखेंगे:

- कोई भी स्कोर ≥ 80 के लिए हल्के‑हरा सेल  
- टॉप‑3 सबसे उच्च स्कोर के लिए गोल्ड सेल, चाहे वे ≥ 80 हों या नहीं  

यह पूरी **create conditional formatting** पाइपलाइन है।

---

## पूरा, Runnable Example

यहाँ पूरा मेथड फिर से दिया गया है, जिसे आप कॉपी‑पेस्ट करके किसी भी कंसोल ऐप या C# क्लास में उपयोग कर सकते हैं:

```csharp
using Aspose.Cells;
using System.Drawing;

void CreateConditionalFormattingWorkbook()
{
    // Step 1: Create a new workbook and name the first worksheet
    Workbook workbook = new Workbook();
    Worksheet sheet = workbook.Worksheets[0];
    sheet.Name = "Scores";

    // Step 2: Fill column A (A2:A21) with random scores between 40 and 99
    Random random = new Random();
    for (int i = 0; i < 20; i++)
    {
        sheet.Cells[i + 1, 0].PutValue(random.Next(40, 100));
    }

    // Step 3: Highlight scores >= 80 with a light‑green background
    int firstRow = 1, lastRow = 20;
    int cfIndex = sheet.ConditionalFormattings.Add(firstRow, 0, lastRow, 0);
    ConditionalFormatting cf = sheet.ConditionalFormattings[cfIndex];
    FormatCondition highScoreCondition = cf.AddCondition(
        FormatConditionType.CellValue,
        OperatorType.GreaterOrEqual,
        "80");
    highScoreCondition.Style.ForegroundColor = Color.LightGreen;
    highScoreCondition.Style.Pattern = BackgroundType.Solid;

    // Step 4: Color the top‑3 scores with a gold background using a formula rule
    FormatCondition topThreeCondition = cf.AddCondition(
        FormatConditionType.Formula,
        null,
        null);
    topThreeCondition.Formula1 = "=RANK(A2,$A$2:$A$21)<=3";
    topThreeCondition.Style.ForegroundColor = Color.Gold;
    topThreeCondition.Style.Pattern = BackgroundType.Solid;

    // Step 5: Save the workbook
    workbook.Save("YOUR_DIRECTORY/Scores_ConditionalFormatting.xlsx");
}
```

### अपेक्षित परिणाम

जब आप `Scores_ConditionalFormatting.xlsx` खोलते हैं:

- **80** या उससे अधिक मान वाले सेल हल्के‑हरा चमकेंगे।  
- तीन सबसे बड़े नंबर (भले ही वे 80 से नीचे हों) **gold** बैकग्राउंड के साथ दिखेंगे।  
- बाकी सभी सेल डिफ़ॉल्ट सफ़ेद बैकग्राउंड रखेंगे।

यह विज़ुअल क्यू तुरंत मैनेजर को बताता है कि टॉप परफ़ॉर्मर्स कौन हैं, बिना किसी मैन्युअल सॉर्टिंग के।

---

## सामान्य प्रश्न और किनारे के मामलों

**यदि मुझे तीन से अधिक टॉप स्कोर चाहिए तो क्या करें?**  
बस फ़ॉर्मूला के `<=3` भाग को `<=5` (या कोई भी संख्या) में बदल दें। नियम स्वतः अनुकूल हो जाएगा।

**क्या मैं कई फ़ॉर्मेटिंग रेंज लागू कर सकता हूँ?**  
बिल्कुल। `sheet.ConditionalFormattings.Add` को फिर से एक अलग रेंज के साथ कॉल करें, फिर उस नए `ConditionalFormatting` ऑब्जेक्ट में कंडीशन जोड़ें।

**पुराने Excel संस्करणों के बारे में क्या?**  
Aspose.Cells डिफ़ॉल्ट रूप से आधुनिक `.xlsx` फ़ॉर्मेट में सेव करता है, जो Excel 2007 और बाद के संस्करणों के साथ संगत है। यदि आपको `.xls` चाहिए, तो `Save` मेथड में `SaveFormat.Excel97To2003` पास करें।

**बड़ी शीट्स के लिए प्रदर्शन पर असर पड़ता है क्या?**  
Conditional formatting मेटाडेटा के रूप में स्टोर होता है, इसलिए फ़ाइल आकार पर बड़ा असर नहीं पड़ता। हालांकि, सैकड़ों हज़ार पंक्तियों को जेनरेट करने से मेमोरी उपयोग बढ़ सकता है—बैच में प्रोसेस करने पर विचार करें।

---

## अगले कदम

अब जब आप **how to create conditional formatting** में निपुण हो गए हैं, तो आप आगे खोज सकते हैं:

- **How to create Excel charts** प्रोग्रामेटिकली (Aspose.Cells का एक और ख़ज़ाना)  
- **How to set cell background** टेक्स्ट वैल्यूज़ (जैसे “Pass/Fail”) के आधार पर  
- **How to use Aspose.Cells for data validation** और ड्रॉप‑डाउन लिस्ट्स  

इनमें से प्रत्येक विषय वही मूलभूत सिद्धांतों पर आधारित है जो आपने अभी सीखे हैं, इसलिए आप तुरंत काम में लगा सकते हैं।

---

## समापन

हमने Aspose.Cells का उपयोग करके Excel वर्कबुक में **create conditional formatting** का एक पूर्ण, एंड‑टू‑एंड उदाहरण दिखाया। workbook को इनिशियलाइज़ करने, डेटा भरने, **setting cell background**, टॉप परफ़ॉर्मर्स को रैंक करने, और अंत में फ़ाइल को सेव करने तक हर कदम को **how to rank cells** और **how to use Aspose** को ध्यान में रखकर कवर किया गया।  

कोड को चलाएँ, थ्रेशहोल्ड को बदलें, और देखें कि आप कितनी जल्दी किसी भी बिज़नेस परिदृश्य के लिए पॉलिश्ड रिपोर्ट जेनरेट कर सकते हैं। कोई ट्विस्ट शेयर करना चाहते हैं? नीचे कमेंट डालें—हैप्पी कोडिंग!

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Java के लिए Aspose.Cells का उपयोग करके Excel Conditional Formatting को स्वचालित करें: एक पूर्ण गाइड](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Java के लिए Aspose.Cells का उपयोग करके Excel Cells को बनाना और फ़ॉर्मेट करना: चरण‑दर‑चरण गाइड](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Java में Aspose.Cells का उपयोग करके Excel Workbook बनाना: चरण‑दर‑चरण गाइड](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}