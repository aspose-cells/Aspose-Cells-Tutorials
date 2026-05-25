---
date: 2026-02-16
description: जाने कैसे सेट करें चार्ट डेटा रेंज और जावा में Aspose.Cells का उपयोग
  करके वाटरफ़ॉल चार्ट बनाएं। डेटा सीरीज़ चार्ट जोड़ने, उसे कस्टमाइज़ करने और XLSX
  में निर्यात करने के लिए चरण‑दर‑चरण गाइड।
linktitle: Waterfall Charts
second_title: Aspose.Cells Java Excel Processing API
title: चार्ट डेटा रेंज सेट करें – Aspose.Cells for Java वाटरफ़ॉल चार्ट
url: /hi/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

Chart.pdf", SaveFormat.PDF);` to **export excel pdf java**‑compatible output.

**Q: What if I need ...** (continue)

We need translate all.

Let's translate.

Be careful with bold formatting **text** remains same but text inside should be Hindi.

Also preserve code blocks placeholders.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Waterfall Charts

## Introduction to Waterfall Charts using Aspose.Cells for Java

इस ट्यूटोरियल में आप सीखेंगे कि **set chart data range** कैसे सेट करें और Aspose.Cells for Java के साथ **waterfall chart** कैसे बनाएं। Waterfall चार्ट डेटा विज़ुअलाइज़ेशन में एक आवश्यक टूल है क्योंकि यह आपको सकारात्मक और नकारात्मक मानों की श्रृंखला के संचयी प्रभाव को देखने देता है। चाहे आप वित्तीय विवरण, बिक्री प्रदर्शन रिपोर्ट, या कोई अन्य डेटा‑ड्रिवेन विश्लेषण तैयार कर रहे हों, एक waterfall चार्ट कच्चे आंकड़ों को स्पष्ट, कार्रवाई योग्य अंतर्दृष्टियों में बदल सकता है।

## Quick Answers
- **What is a waterfall chart?** एक विज़ुअल जो दिखाता है कि प्रारंभिक मान को मध्यवर्ती मानों की श्रृंखला द्वारा कैसे बढ़ाया और घटाया जाता है, अंत में एक अंतिम कुल के साथ।  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** विकास के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **Can I save the file as XLSX?** हाँ – `workbook.save("FileName.xlsx")` का उपयोग करें।  
- **Is it suitable for Java data visualization?** बिल्कुल; Aspose.Cells बिना Office स्थापित किए समृद्ध चार्टिंग सुविधाएँ प्रदान करता है।

## What is a Waterfall Chart?
एक waterfall चार्ट प्रारंभिक मान में क्रमिक सकारात्मक और नकारात्मक योगदान को प्रदर्शित करता है, जिससे आप समझ सकते हैं कि प्रत्येक घटक समग्र परिणाम को कैसे प्रभावित करता है।

## Why Use Aspose.Cells for Java to Add a Waterfall Chart?
- **No Microsoft Excel required** – किसी भी सर्वर या CI पाइपलाइन पर चार्ट जनरेट करें।  
- **Full control over formatting** – रंग, डेटा लेबल और अक्षों को प्रोग्रामेटिकली कस्टमाइज़ किया जा सकता है।  
- **Supports multiple output formats** – XLSX, PDF, HTML, और अधिक।  
- **High performance** – बड़े वर्कबुक और स्वचालित रिपोर्टिंग के लिए आदर्श।

## Prerequisites

कोड में डुबकी लगाने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित आवश्यकताएँ मौजूद हैं:

- Aspose.Cells for Java: आपको Aspose.Cells for Java स्थापित होना चाहिए। आप इसे [here](https://releases.aspose.com/cells/java/) से डाउनलोड कर सकते हैं।

- Java Development Environment: सुनिश्चित करें कि आपके सिस्टम पर Java स्थापित है।

अब चलिए चरण-दर-चरण waterfall चार्ट बनाना शुरू करते हैं।

## How to Set Chart Data Range for a Waterfall Chart in Java

### Step 1: Import Aspose.Cells

```java
import com.aspose.cells.*;
```

सबसे पहले, आपको अपने Java प्रोजेक्ट में Aspose.Cells लाइब्रेरी इम्पोर्ट करनी होगी। यह लाइब्रेरी Excel फ़ाइलों के साथ काम करने के लिए विस्तृत कार्यक्षमता प्रदान करती है, जिसमें चार्ट निर्माण भी शामिल है।

### Step 2: Initialize Workbook and Worksheet

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

एक नया वर्कबुक बनाएं और उसमें एक वर्कशीट जोड़ें। हम इस वर्कशीट का उपयोग अपने डेटा को दर्ज करने और **add chart to worksheet** करने के लिए करेंगे।

### Step 3: Enter Data

अब, चलिए वर्कशीट को उन डेटा से भरते हैं जिन्हें हम waterfall चार्ट में दर्शाना चाहते हैं।

```java
Cells cells = worksheet.getCells();

// Insert data
cells.get("A1").putValue("Categories");
cells.get("A2").putValue("Start");
cells.get("A3").putValue("Positive Value 1");
cells.get("A4").putValue("Negative Value 1");
cells.get("A5").putValue("Positive Value 2");
cells.get("A6").putValue("End");

cells.get("B1").putValue("Values");
cells.get("B2").putValue(0);
cells.get("B3").putValue(20);
cells.get("B4").putValue(-10);
cells.get("B5").putValue(15);
cells.get("B6").putValue(25);
```

इस उदाहरण में, हमारे पास कॉलम A में श्रेणियाँ और कॉलम B में संबंधित मान हैं। आप इस डेटा को अपने स्वयं के डेटासेट से बदल सकते हैं।

### Step 4: Create the Waterfall Chart

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

हमने अपनी वर्कशीट में एक waterfall चार्ट जोड़ा है, डेटा सीरीज़ और श्रेणी डेटा निर्दिष्ट किया है। यह वह मुख्य चरण है जो **adds waterfall chart** आपके शीट में जोड़ता है। ध्यान दें कि `add` मेथड रेंज `"B2:B6"` का उपयोग करता है – यही वह जगह है जहाँ हम **set chart data range** सीरीज़ के लिए सेट करते हैं। आप `Chart` ऑब्जेक्ट की प्रॉपर्टीज़ का उपयोग करके चार्ट की उपस्थिति (रंग, डेटा लेबल आदि) को और कस्टमाइज़ कर सकते हैं।

### Step 5: Save the Workbook

```java
workbook.save("WaterfallChart.xlsx");
```

वर्कबुक को फ़ाइल में सहेजें। उदाहरण XLSX फॉर्मेट का उपयोग करता है, लेकिन Aspose.Cells आपको **export excel pdf java**‑compatible फ़ाइलें जैसे PDF, CSV, और कई अन्य फॉर्मेट भी एक्सपोर्ट करने की सुविधा देता है। यह **save workbook xlsx** आवश्यकता को पूरा करता है।

## Common Issues and Solutions

- **Chart appears blank** – सुनिश्चित करें कि डेटा रेंज रेफ़रेंसेज़ (`B2:B6` और `A2:A6`) उन वास्तविक सेल्स से मेल खाती हैं जिनमें आपके मान और श्रेणियाँ हैं।  
- **Negative values not displayed correctly** – यह सुनिश्चित करें कि सीरीज़ प्रकार `ChartType.WATERFALL` पर सेट है; अन्य चार्ट प्रकार नकारात्मक मानों को अलग तरीके से संभालते हैं।  
- **File not opening in Excel** – यह सुनिश्चित करें कि आप Aspose.Cells का नवीनतम संस्करण उपयोग कर रहे हैं और फ़ाइल एक्सटेंशन फॉर्मेट से मेल खाता है (`.xlsx` Excel के लिए)।

## Frequently Asked Questions

### How can I customize the appearance of my waterfall chart?

आप अपने waterfall चार्ट की उपस्थिति को रंग, डेटा लेबल और अक्ष लेबल जैसी प्रॉपर्टीज़ को संशोधित करके कस्टमाइज़ कर सकते हैं। विस्तृत मार्गदर्शन के लिए Aspose.Cells दस्तावेज़ देखें।

### Can I create multiple waterfall charts in the same worksheet?

हाँ, आप एक ही वर्कशीट में विभिन्न डेटा रेंज के साथ समान चरणों का पालन करके कई waterfall चार्ट बना सकते हैं।

### Is Aspose.Cells compatible with different Java development environments?

हाँ, Aspose.Cells for Java विभिन्न Java विकास वातावरणों जैसे Eclipse, IntelliJ IDEA, और NetBeans के साथ संगत है।

### Can I add additional data series to my waterfall chart?

बिल्कुल, आप प्रोग्रामेटिकली **add data series chart** करके अपने waterfall चार्ट में अतिरिक्त डेटा सीरीज़ जोड़ सकते हैं।

### Where can I find more resources and examples for Aspose.Cells for Java?

आप Aspose.Cells for Java की दस्तावेज़ीकरण यहाँ देख सकते हैं: [reference.aspose.com/cells/java/](https://reference.aspose.com/cells/java/) जिसमें विस्तृत जानकारी और कोड उदाहरण उपलब्ध हैं।

## FAQ

**Q: How do I set the chart data range for a financial waterfall chart?**  
A: चार्ट की सीरीज़ पर `add` मेथड का उपयोग करें, जिसमें वह सेल रेंज पास करें जिसमें आपके मान हैं, जैसे `"B2:B6"`।

**Q: Can I export the workbook to PDF instead of XLSX?**  
A: हाँ, `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` को कॉल करके **export excel pdf java**‑compatible आउटपुट प्राप्त करें।

**Q: What if I need to create a financial waterfall chart with more categories?**  
A: मान और श्रेणी कॉलम दोनों में डेटा रेंज को विस्तारित करें, फिर `add` और `setCategoryData` कॉल्स को उसी अनुसार अपडेट करें।

**Q: Is there a way to automatically format positive and negative bars?**  
A: आप `Series` कलेक्शन के माध्यम से इटरेट करके प्रत्येक मान के संकेत के आधार पर `FillFormat` रंग सेट कर सकते हैं।

**Q: Does Aspose.Cells support dynamic data updates for charts?**  
A: हाँ, आप चार्ट बन जाने के बाद सेल मानों को संशोधित कर सकते हैं; वर्कबुक सहेजने पर चार्ट इन बदलावों को दर्शाएगा।

---

**Last Updated:** 2026-02-16  
**Tested With:** Aspose.Cells for Java (latest)  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}