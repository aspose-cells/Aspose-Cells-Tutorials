---
category: general
date: 2026-06-30
description: C# के साथ Excel में लाइन स्पार्कलाइन जल्दी बनाएं। सीखें कैसे स्पार्कलाइन
  जोड़ें, C# में Excel वर्कबुक बनाएं, और कुछ ही चरणों में सेल में स्पार्कलाइन जोड़ें।
draft: false
keywords:
- create line sparkline
- how to add sparkline
- add line sparkline
- create excel workbook c#
- add sparkline to cell
language: hi
og_description: C# के साथ Excel में लाइन स्पार्कलाइन बनाएं। यह ट्यूटोरियल दिखाता है
  कि स्पार्कलाइन कैसे जोड़ें, C# में Excel वर्कबुक कैसे बनाएं, और स्पार्कलाइन को एक
  सेल में कैसे एम्बेड करें।
og_title: C# के साथ Excel में लाइन स्पार्कलाइन बनाएं – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Create line sparkline in Excel with C# quickly. Learn how to add sparkline,
    create Excel workbook C#, and add sparkline to cell in a few steps.
  headline: Create line sparkline in Excel with C# – Complete Programming Guide
  type: TechArticle
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# के साथ Excel में लाइन स्पार्कलाइन बनाएं – पूर्ण प्रोग्रामिंग गाइड
url: /hi/net/charts/create-line-sparkline-in-excel-with-c-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# के साथ Excel में लाइन स्पार्कलाइन बनाएं – पूर्ण प्रोग्रामिंग गाइड

क्या आपने कभी सोचा है कि **लाइन स्पार्कलाइन** को Excel फ़ाइल में C# का उपयोग करके कैसे बनाया जाए? आप अकेले नहीं हैं—डेवलपर्स अक्सर पूछते हैं, “मैं रिपोर्ट में स्पार्कलाइन कैसे जोड़ूँ बिना Excel को मैन्युअली खोले?” अच्छी खबर यह है कि कुछ ही लाइनों के कोड से आप वर्कबुक के अंदर ही एक स्टाइलिश लाइन स्पार्कलाइन जेनरेट कर सकते हैं, बिना किसी UI के।

इस ट्यूटोरियल में हम वह सब कवर करेंगे जो आपको जानना जरूरी है: **create Excel workbook C#** की बुनियादें, डेटा भरना, और **add line sparkline** तथा **add sparkline to cell** के सटीक चरण। अंत में आपके पास एक तैयार *.xlsx* फ़ाइल होगी जो मासिक बिक्री रुझानों को एक नज़र में दिखाएगी। कोई फालतू बात नहीं, सिर्फ एक व्यावहारिक, चलाने योग्य समाधान।

---

## आप क्या बनाएँगे

- *KPI_Sparklines.xlsx* नाम की एक नई Excel वर्कबुक  
- **KPI** नाम का एक वर्कशीट जिसमें नमूना बिक्री आँकड़े होंगे  
- **लाइन स्पार्कलाइन** जो सेल **D2** में रखी होगी और डेटा रेंज **B2:B13** को रेफ़र करेगी  
- बेसिक फ़ॉर्मेटिंग (रंग, लाइन वेट) जिससे स्पार्कलाइन आकर्षक दिखे  

पूर्वापेक्षाएँ? बस .NET SDK (3.1+ या .NET 6) और मुफ्त Aspose.Cells for .NET लाइब्रेरी (NuGet के माध्यम से उपलब्ध)। यदि आपने पहले Aspose.Cells नहीं इस्तेमाल किया है, तो इसे एक शक्तिशाली Excel इंजन समझें जिसे आप कोड से कॉल कर सकते हैं—कोई COM इंटरऑप नहीं, कोई Excel इंस्टॉलेशन नहीं चाहिए।

---

![Create line sparkline in Excel using C#](https://example.com/images/create-line-sparkline.png "C# के साथ Excel में लाइन स्पार्कलाइन बनाएं")

*छवि वैकल्पिक पाठ: C# कोड उदाहरण के साथ Excel में लाइन स्पार्कलाइन बनाना*

---

## चरण 1: **Create Excel workbook C#** – फ़ाइल और वर्कशीट सेटअप करें

सबसे पहले हमें एक वर्कबुक ऑब्जेक्ट और एक वर्कशीट चाहिए जहाँ डेटा रहेगा। यह किसी भी Excel ऑटोमेशन की बुनियाद है, चाहे आप बाद में **add line sparkline** करें या फ़ॉर्मूले लिखें।

```csharp
using Aspose.Cells;
using System.Drawing;

// Initialize a new workbook
Workbook workbook = new Workbook();

// Grab the first worksheet (index 0) and give it a meaningful name
Worksheet worksheet = workbook.Worksheets[0];
worksheet.Name = "KPI";   // “KPI” will hold our key performance indicators
```

> **यह क्यों महत्वपूर्ण है:** `Workbook` क्लास पूरी फ़ाइल को दर्शाता है, जबकि `Worksheet` पंक्तियों, कॉलमों और अंततः हमारे स्पार्कलाइन के लिए कैनवास है। शीट का नाम पहले से सेट करने से फ़ाइल साफ‑सुथरी और स्वयं‑दस्तावेज़ी बनती है।

---

## चरण 2: डेटा भरें – स्पार्कलाइन के लिए स्रोत रेंज

स्पार्कलाइन को प्लॉट करने के लिए डेटा चाहिए। चलिए 12 महीनों की बिक्री संख्याएँ सिम्युलेट करते हैं। आप इन्हें डेटाबेस से भी ले सकते हैं, लेकिन स्पष्टता के लिए हम इन्हें ऑन‑द‑फ्लाई जनरेट करेंगे।

```csharp
// Fill column B (index 1) with monthly sales numbers
for (int month = 0; month < 12; month++)
{
    // Example pattern: start at 5,000 and increase by 750 each month
    worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
}
```

> **टिप:** `PutValue` डेटा टाइप को स्वचालित रूप से पहचान लेता है, इसलिए आपको `double` या `int` में कास्ट करने की ज़रूरत नहीं। यदि आपको सेल्स को फ़ॉर्मेट करना है (करेंसी, हजारों का विभाजन), तो बाद में `Style` ऑब्जेक्ट लागू कर सकते हैं।

---

## चरण 3: **Create line sparkline** – स्पार्कलाइन को विशिष्ट सेल में जोड़ें

अब आती है मुख्य बात: **लाइन स्पार्कलाइन**। Aspose.Cells स्पार्कलाइन को समूहित करता है, इसलिए हम पहले `Line` प्रकार की `SparklineGroup` बनाते हैं, फिर उसे बताते हैं कि विज़ुअल कहाँ रखनी है।

```csharp
// Add a new SparklineGroup of type Line
int groupIndex = worksheet.SparklineGroups.Add(SparklineType.Line);
SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIndex];

// Add a sparkline that lives in D2 (row 1, column 3) and reads data from B2:B13
// Parameters: firstRow, firstColumn, lastRow, lastColumn, firstDataRow, lastDataRow
sparklineGroup.Add(1, 3, 1, 3, 1, 12);   // D2 ↔ B2:B13
```

> **कैसे काम करता है:**  
> - `firstRow/firstColumn` और `lastRow/lastColumn` *टार्गेट सेल* (जहाँ स्पार्कलाइन दिखाई देगी) को परिभाषित करते हैं।  
> - `firstDataRow/lastDataRow` स्रोत रेंज की ओर इशारा करते हैं।  
> क्योंकि हम **लाइन स्पार्कलाइन** उपयोग कर रहे हैं, विज़ुअल एक साधी पतली लाइन होगी जो संख्याओं के ट्रेंड को दर्शाएगी।

### वैकल्पिक: कस्टम स्टाइलिंग के साथ **How to add sparkline**

यदि आप स्पार्कलाइन को अधिक प्रमुख बनाना चाहते हैं, तो कुछ प्रॉपर्टीज़ को समायोजित करें:

```csharp
sparklineGroup.LineWeight = 1.0;               // Thickness of the line
sparklineGroup.SeriesColor = Color.DarkBlue;  // Color of the sparkline line
sparklineGroup.ShowMarkers = true;             // Show data markers (optional)
sparklineGroup.MarkerColor = Color.OrangeRed;  // Marker color
```

> **स्टाइल क्यों?** सफ़ेद बैकग्राउंड पर डार्क ब्लू लाइन आँखों के लिए आरामदायक होती है, जबकि मार्कर्स व्यक्तिगत डेटा पॉइंट्स का त्वरित संकेत देते हैं—प्रेज़ेंटेशन में उपयोगी।

---

## चरण 4: वर्कबुक सहेजें – परिणाम की पुष्टि करें

स्पार्कलाइन जोड़ने के बाद, हमें फ़ाइल को डिस्क पर लिखना है। वह फ़ोल्डर चुनें जहाँ आपके पास लिखने की अनुमति हो; उदाहरण में प्लेसहोल्डर पाथ है जिसे आपको बदलना चाहिए।

```csharp
// Save the workbook as an .xlsx file
string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
workbook.Save(outputPath);
```

> **वेरिफिकेशन:** उत्पन्न फ़ाइल को Excel (या कोई भी .xlsx सपोर्ट करने वाला व्यूअर) में खोलें। आपको सेल **D2** में एक **लाइन स्पार्कलाइन** दिखनी चाहिए जो कॉलम **B** में बढ़ती बिक्री संख्याओं को प्रतिबिंबित करती है। स्पार्कलाइन पर होवर करने से मूल मानों के साथ एक टूलटिप दिखेगा।

---

## चरण 5: **add sparkline to cell** के दौरान आम समस्याएँ

भले ही उदाहरण सरल हो, नए उपयोगकर्ताओं को कुछ अड़चनें मिल सकती हैं। यहाँ कुछ चीज़ें हैं जिन पर ध्यान देना चाहिए:

| Issue | Why it happens | Fix |
|-------|----------------|-----|
| Wrong cell coordinates | Sparkline target uses zero‑based column index but one‑based row index. | Remember `Cells[row, column]` where `row` is zero‑based, `column` is zero‑based as well. In `SparklineGroup.Add`, rows and columns are **1‑based**. |
| No data displayed | Source range is empty or contains non‑numeric values. | Ensure the range (e.g., `B2:B13`) holds numbers. Use `PutValue` with numeric types. |
| Sparkline disappears after saving | Library version mismatch or missing license. | Use the latest Aspose.Cells package and provide a valid license if you’re beyond the evaluation limits. |
| Formatting not applied | Style changes made before adding the sparkline. | Set styling **after** you create the group, as shown above. |

---

## पूरा सोर्स कोड – एक‑बार में कॉपी‑पेस्ट

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम दिया गया है। इसे एक नए कंसोल प्रोजेक्ट में पेस्ट करें, Aspose.Cells NuGet पैकेज जोड़ें, और **F5** दबाएँ।

```csharp
using Aspose.Cells;
using System.Drawing;

namespace SparklineDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create Excel workbook C#
            // -------------------------------------------------
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];
            worksheet.Name = "KPI";

            // -------------------------------------------------
            // Step 2: Populate monthly sales data (B2:B13)
            // -------------------------------------------------
            for (int month = 0; month < 12; month++)
            {
                worksheet.Cells[month + 1, 1].PutValue(5000 + month * 750);
            }

            // -------------------------------------------------
            // Step 3: Create line sparkline and add it to D2
            // -------------------------------------------------
            int groupIdx = worksheet.SparklineGroups.Add(SparklineType.Line);
            SparklineGroup sparklineGroup = worksheet.SparklineGroups[groupIdx];
            sparklineGroup.Add(1, 3, 1, 3, 1, 12); // D2 ↔ B2:B13

            // -------------------------------------------------
            // Step 4: Optional formatting (how to add sparkline with style)
            // -------------------------------------------------
            sparklineGroup.LineWeight = 1.0;
            sparklineGroup.SeriesColor = Color.DarkBlue;
            sparklineGroup.ShowMarkers = true;
            sparklineGroup.MarkerColor = Color.OrangeRed;

            // -------------------------------------------------
            // Step 5: Save the workbook
            // -------------------------------------------------
            string outputPath = @"C:\Temp\KPI_Sparklines.xlsx";
            workbook.Save(outputPath);

            System.Console.WriteLine($"Workbook saved to {outputPath}");
        }
    }
}
```

**अपेक्षित आउटपुट:** जब आप *KPI_Sparklines.xlsx* खोलेंगे, तो कॉलम **B** में बारह संख्याएँ (5,000 → 13,250) दिखेंगी और सेल **D2** में एक स्मूद डार्क‑ब्लू लाइन स्पार्कलाइन होगी जो लगातार ऊपर की ओर बढ़ती दिखेगी। यदि आपने `ShowMarkers` सक्षम किया है तो मार्कर्स छोटे ऑरेंज‑रेड डॉट्स के रूप में दिखाई देंगे।

---

## आगे क्या? अपने स्पार्कलाइन कौशल को विस्तारित करें

अब जब आप Aspose.Cells के साथ **create line sparkline** में निपुण हो गए हैं, तो इन संबंधित विषयों को देखें:

- **Add column sparkline** – स्टैक्ड डेटा दिखाने के लिए परफेक्ट।  
- **Create multi‑sparkline groups** – एक ही शीट पर साइड‑बाय‑साइड तुलना के लिए।  
- **Export to PDF** – स्पार्कलाइन को बरकरार रखते हुए PDF में बदलें (Aspose.Cells PDF कन्वर्ज़न सपोर्ट करता है)।  
- **Dynamic data sources** – हार्ड‑कोडेड वैल्यूज़ की बजाय SQL डेटाबेस से वास्तविक बिक्री आंकड़े लाएँ।  

इनमें से प्रत्येक ऊपर बताए गए कोर कॉन्सेप्ट्स पर आधारित है: **create Excel workbook C#**, डेटा भरें, और **add sparkline to cell** को इच्छित स्टाइल में जोड़ें।

---

### TL;DR

हमने दिखाया कि C# का उपयोग करके Excel वर्कबुक में **लाइन स्पार्कलाइन** कैसे बनाई जाए। चरण—*वर्कबुक बनाना, डेटा भरना, स्पार्कलाइन जोड़ना, स्टाइल करना, और सहेजना*—एक ही स्व-निहित प्रोग्राम में समाहित हैं। रंग, लाइन वेट, या स्रोत रेंज को अपनी रिपोर्टिंग जरूरतों के अनुसार बदलने के लिए स्वतंत्र रहें।

क्या आपके पास कोई नया आइडिया है? नीचे कमेंट करें, और कोडिंग का आनंद लें!

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Excel Automation Create Workbook Add Listbox Aspose Cells](/cells/french/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}