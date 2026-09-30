---
category: general
date: 2026-03-27
description: Aspose.Cells का उपयोग करके C# में डेटा बाइंड करना – सीखें कैसे वर्कबुक
  को XLSX के रूप में सहेजें, चार्ट जोड़ें, और मिनटों में चार्ट के साथ Excel निर्यात
  करें।
draft: false
keywords:
- how to bind data
- save workbook as xlsx
- create excel workbook c#
- how to add chart
- export excel with chart
language: hi
og_description: C# में Aspose.Cells के साथ डेटा बाइंड कैसे करें। यह गाइड आपको दिखाता
  है कि वर्कबुक को XLSX के रूप में कैसे सहेजें, चार्ट जोड़ें, और चार्ट के साथ Excel
  निर्यात करें।
og_title: C# में डेटा बाइंड कैसे करें – एक्सेल वर्कबुक बनाएं
tags:
- Aspose.Cells
- C#
- Excel Automation
title: C# में डेटा को बाइंड कैसे करें – एक्सेल वर्कबुक बनाएं
url: /hi/net/excel-data-import-export/how-to-bind-data-in-c-create-excel-workbook/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में डेटा बाइंड करना – Excel वर्कबुक बनाना

क्या आपने कभी **डेटा बाइंड करने** के बारे में सोचा है ताकि C# में चार्ट को बिना सिर दर्द के बनाया जा सके? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब उन्हें प्रोग्रामेटिकली ऐसे Excel फ़ाइलें जेनरेट करनी होती हैं जो वास्तव में *वही* दिखें जैसा कि वे मैन्युअली बनाते हैं।  

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने‑योग्य उदाहरण के माध्यम से चलते हैं जो एक Excel वर्कबुक बनाता है, उसमें डेटा भरता है, उस डेटा को एक Waterfall चार्ट से बाइंड करता है, और अंत में फ़ाइल को `.xlsx` के रूप में सेव करता है। अंत तक आप बिल्कुल जानेंगे कि **वर्कबुक को XLSX के रूप में कैसे सेव करें**, **वर्कशीट में चार्ट कैसे जोड़ें**, और **चार्ट के साथ Excel को कैसे एक्सपोर्ट करें**।

> **Prerequisites** – आपको Aspose.Cells for .NET (फ्री ट्रायल ठीक रहेगा) और एक .NET डेवलपमेंट एनवायरनमेंट जैसे Visual Studio 2022 चाहिए। कोई अन्य NuGet पैकेज आवश्यक नहीं है।

---

## इस गाइड में क्या कवर किया गया है

- **Create Excel workbook C#** – एक नया `Workbook` और एक वर्कशीट सेट अप करें।  
- **How to bind data** – अपने न्यूमेरिक सीरीज़ और कैटेगरी लेबल्स को चार्ट के डेटा सोर्स से मैप करें।  
- **How to add chart** – एक Waterfall चार्ट इन्सर्ट करें और उसका टाइटल कॉन्फ़िगर करें।  
- **Save workbook as XLSX** – फ़ाइल को डिस्क पर सहेजें ताकि कोई भी इसे Excel में खोल सके।  
- **Export Excel with chart** – अंतिम प्रोडक्ट एक पूरी‑फ़ंक्शनल वर्कबुक है जिसे आप शेयर कर सकते हैं।

यदि आप बेसिक C# सिंटैक्स से परिचित हैं, तो यह आपके लिए बहुत आसान रहेगा। चलिए शुरू करते हैं।

---

## Step 1: Create an Excel Workbook in C#  

सबसे पहले – हमें एक workbook ऑब्जेक्ट चाहिए जिससे हम काम कर सकें। `Workbook` क्लास को उस खाली नोटबुक की तरह समझें जिसे आप बाद में पेज़ (वर्कशीट) और कंटेंट से भरेंगे।

```csharp
using Aspose.Cells;
using Aspose.Cells.Charts;

class WaterfallDemo
{
    static void Main()
    {
        // Initialize a new workbook – this is your blank Excel file.
        Workbook workbook = new Workbook();

        // Grab the first worksheet (index 0). It’s already created for us.
        Worksheet worksheet = workbook.Worksheets[0];
```

> **Pro tip:** यदि आपको कई शीट्स चाहिए, तो बस `workbook.Worksheets.Add()` कॉल करें और प्रत्येक नई `Worksheet` का रेफ़रेंस रखें।

---

## Step 2: Populate the Worksheet with Categories and Values  

अब हम **create excel workbook c#**‑स्टाइल डेटा बनाएँगे। उदाहरण में एक क्लासिक Waterfall परिदृश्य है: start, revenue, cost, profit, और end।

```csharp
        // Add header labels.
        worksheet.Cells["A1"].PutValue("Category");
        worksheet.Cells["B1"].PutValue("Amount");

        // Sample data – you can replace these with your own source (database, API, etc.).
        string[] categoryLabels = { "Start", "Revenue", "Cost", "Profit", "End" };
        double[] values = { 0, 150, -70, 0, 80 };

        // Fill rows 2‑6 with the data.
        for (int i = 0; i < categoryLabels.Length; i++)
        {
            worksheet.Cells[i + 1, 0].PutValue(categoryLabels[i]); // Column A
            worksheet.Cells[i + 1, 1].PutValue(values[i]);       // Column B
        }
```

हम “Start” और “Profit” के लिए `0` क्यों रखते हैं? Waterfall चार्ट में ये ज़ीरो *कनेक्टर* की तरह काम करते हैं जिससे विज़ुअल फ्लो सही रहता है। यदि आप इन्हें छोड़ देंगे तो चार्ट टूटे‑हुए दिखेगा।

---

## Step 3: How to Add Chart – Insert a Waterfall Chart  

डेटा तैयार होने के बाद, अब **how to add chart** का समय है। Aspose.Cells इसे इतना आसान बना देता है कि आप सिर्फ `Charts.Add` कॉल करें।

```csharp
        // Insert a Waterfall chart starting at row 7, column 0 and spanning to row 25, column 10.
        int chartIndex = worksheet.Charts.Add(ChartType.Waterfall, 7, 0, 25, 10);
        Chart waterfallChart = worksheet.Charts[chartIndex];

        // Give the chart a meaningful title.
        waterfallChart.Title.Text = "Quarterly Waterfall";
```

कोऑर्डिनेट्स `(7,0,25,10)` चार्ट के बाउंडिंग बॉक्स के टॉप‑लेफ़्ट और बॉटम‑राइट सेल को परिभाषित करते हैं। अपने लेआउट के अनुसार इन्हें समायोजित करें।

---

## Step 4: How to Bind Data – Connect Series and Categories  

यह ट्यूटोरियल का मुख्य भाग है: **how to bind data** को चार्ट से कनेक्ट करना। `NSeries.Add` मेथड Y‑वैल्यूज़ की रेंज लेता है, जबकि `CategoryData` X‑अक्ष के लेबल्स की ओर इशारा करता है।

```csharp
        // Bind the numeric series (values) – the second parameter “true” tells Aspose to treat it as a series.
        waterfallChart.NSeries.Add("B2:B6", true);

        // Bind the category (X‑axis) labels.
        waterfallChart.NSeries.CategoryData = "A2:A6";
```

ध्यान दें कि हम वही सेल्स रेफ़रेंस कर रहे हैं जिन्हें हमने पहले भरा था (`A2:A6` कैटेगरी के लिए, `B2:B6` अमाउंट्स के लिए)। यदि आप डेटा लेआउट बदलते हैं, तो बस इन रेंजेज़ को अपडेट कर दें।

---

## Step 5: Save Workbook as XLSX – Persist the File  

अंत में, हम **save workbook as XLSX** करते हैं। `Save` मेथड फ़ाइल एक्सटेंशन के आधार पर सही फ़ॉर्मेट को स्वचालित रूप से चुन लेता है।

```csharp
        // Save the workbook to disk. Replace YOUR_DIRECTORY with an actual path.
        workbook.Save("YOUR_DIRECTORY/WaterfallChart.xlsx");
    }
}
```

जब आप `WaterfallChart.xlsx` को Excel में खोलेंगे तो आपको एक सुंदर रेंडर किया हुआ Waterfall चार्ट दिखेगा जो हमने दर्ज किया हुआ डेटा दर्शाता है। यही **export excel with chart** भाग पूरा होता है।

---

## Expected Result  

- **Excel फ़ाइल:** `WaterfallChart.xlsx` आपके द्वारा निर्दिष्ट फ़ोल्डर में स्थित होगी।  
- **वर्कशीट लेआउट:** कॉलम A में कैटेगरी, कॉलम B में अमाउंट्स, और चार्ट टेबल के नीचे स्थित होगा।  
- **चार्ट की उपस्थिति:** “Quarterly Waterfall” शीर्षक वाला Waterfall चार्ट जिसमें पाँच कॉलम हैं – Start, Revenue, Cost, Profit, और End।  

![डेटा बाइंड करने वाला Waterfall चार्ट उदाहरण](waterfall_chart.png "Aspose.Cells द्वारा उत्पन्न Waterfall चार्ट")

*Image alt text includes the primary keyword, helping both SEO and AI citation.*

---

## Common Questions & Edge Cases  

### What if my data source is dynamic?  
स्थैतिक एरेज़ को डेटाबेस या API से पढ़ने वाले लूप से बदलें। जब तक आप वही सेल रेंज में वैल्यूज़ लिखते हैं, बाइंडिंग कोड अपरिवर्तित रहेगा।

### Can I change the chart type?  
बिल्कुल। `ChartType.Waterfall` को `ChartType.Column`, `ChartType.Line` आदि से बदलें। बस नई चार्ट के अनुसार सीरीज़ डेटा को समायोजित करना याद रखें।

### How do I set the chart’s colors?  
`waterfallChart.NSeries[0].Format.Fill.ForeColor = Color.Yellow;` (या कोई भी `System.Drawing.Color`) का उपयोग करें। यह तब उपयोगी है जब आप “Profit” कॉलम को विशेष रूप से हाइलाइट करना चाहते हैं।

### What if I need to export to PDF instead of XLSX?  
`workbook.Save("Report.pdf", SaveFormat.Pdf);` कॉल करें। चार्ट स्वचालित रूप से PDF में रेंडर हो जाएगा।

---

## Tips for Production‑Ready Code  

- **Dispose objects** – यदि आप .NET Core पर हैं तो `Workbook` को `using` ब्लॉक में रखें ताकि संसाधन तुरंत मुक्त हो सकें।  
- **Path handling** – `Path.Combine(Environment.CurrentDirectory, "WaterfallChart.xlsx")` का उपयोग करें ताकि हार्ड‑कोडेड सेपरेटर से बचा जा सके।  
- **Error handling** – `Save` के आसपास `Exception` को कैच करें ताकि परमिशन या डिस्क‑स्पेस समस्याओं को जल्दी पता लगाया जा सके।  
- **Version check** – Aspose.Cells 23.10+ ने Waterfall सपोर्ट को बेहतर बनाया है; बेहतर परिणामों के लिए नवीनतम संस्करण उपयोग करें।

---

## Conclusion  

अब आपके पास एक पूर्ण, एंड‑टू‑एंड उदाहरण है जो **how to bind data** in C#, **create excel workbook c#**, **how to add chart**, **save workbook as xlsx**, और **export excel with chart** को दर्शाता है। कोड किसी भी .NET प्रोजेक्ट में डालने के लिए तैयार है, और अवधारणाएँ बड़े डेटा सेट और विभिन्न चार्ट प्रकारों तक स्केल करती हैं।

अगला कदम तैयार है? कई सीरीज़ जोड़ें, स्टैक्ड चार्ट के साथ प्रयोग करें, या मासिक रिपोर्ट्स को ऑटोमेट करें जो स्टेकहोल्डर्स को ईमेल की जाएँ। Excel ऑटोमेशन के बेसिक्स में महारत हासिल करने के बाद संभावनाएँ असीम हैं।

Happy coding, and may your spreadsheets always render perfectly!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}