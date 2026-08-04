---
date: 2026-02-09
description: Aspose.Cells for Java का उपयोग करके Excel चार्ट में डेटा लेबल जोड़ना
  और चार्ट प्रकार बदलना सीखें, साथ ही टूलटिप्स और ड्रिल‑डाउन इंटरैक्टिविटी।
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells Java के साथ Excel चार्ट में डेटा लेबल जोड़ें
url: /hi/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

 प्रकार बदलें – Aspose.Cells Java". Keep dash.

Paragraph: "Interactive charts give your Excel reports a new level ...". Translate.

We'll produce Hindi sentences.

Need to translate bullet points, tables, etc.

Make sure markdown formatting unchanged.

Let's craft translation.

Be careful with code snippets inside backticks like `ChartType`. Keep as is.

Also keep URLs unchanged.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel चार्ट में डेटा लेबल जोड़ें और चार्ट प्रकार बदलें – Aspose.Cells Java

इंटरैक्टिव चार्ट आपके Excel रिपोर्ट को नई अंतर्दृष्टि प्रदान करते हैं, और **Excel चार्ट में डेटा लेबल जोड़ना** जानकारी को तुरंत पढ़ने योग्य बनाता है। इस ट्यूटोरियल में आप सीखेंगे कि **Excel चार्ट में डेटा लेबल कैसे जोड़ें**, चार्ट प्रकार कैसे बदलें, और Aspose.Cells के साथ इंटरैक्टिव Java समाधान कैसे बनाएं। हम यह भी दिखाएंगे कि टूलटिप्स कैसे जोड़ें और एक सरल ड्रिल‑डाउन हाइपरलिंक कैसे बनाएं ताकि आपका दर्शक डेटा को गहराई से एक्सप्लोर कर सके।

## त्वरित उत्तर
- **कौन सी लाइब्रेरी उपयोग की जाती है?** Aspose.Cells for Java  
- **क्या मैं चार्ट प्रकार बदल सकता हूँ?** हाँ – जब आप चार्ट बनाते हैं तो `ChartType` enum को बदलें।  
- **चार्ट में टूलटिप्स कैसे जोड़ें?** डेटा‑लेबल API (`setHasDataLabels(true)`) का उपयोग करें और वैल्यू डिस्प्ले सक्षम करें।  
- **क्या ड्रिल‑डाउन समर्थित है?** आप डेटा पॉइंट्स पर हाइपरलिंक जोड़कर बेसिक ड्रिल‑डाउन व्यवहार प्राप्त कर सकते हैं।  
- **पूर्वापेक्षाएँ?** Java IDE, Aspose.Cells JAR, और एक Excel फ़ाइल जिसमें नमूना डेटा हो।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

- Java Development Environment (JDK 8+ अनुशंसित)  
- Aspose.Cells for Java लाइब्रेरी (डाउनलोड करें [here](https://releases.aspose.com/cells/java/))  
- एक नमूना वर्कबुक (`data.xlsx`) जिसमें वह डेटा हो जिसे आप विज़ुअलाइज़ करना चाहते हैं  

## चरण 1: अपना Java प्रोजेक्ट सेट अप करना

1. अपने पसंदीदा IDE (IntelliJ IDEA, Eclipse, आदि) में एक नया Java प्रोजेक्ट बनाएं।  
2. Aspose.Cells JAR को अपने प्रोजेक्ट के बिल्ड पाथ या Maven/Gradle डिपेंडेंसीज़ में जोड़ें।

## चरण 2: डेटा लोड करना

चार्ट के साथ काम करने के लिए पहले एक वर्कबुक को मेमोरी में लोड करना आवश्यक है।

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## चरण 3: चार्ट बनाना (और उसका प्रकार बदलना)

आप अपनी विश्लेषण के अनुसार कोई भी चार्ट प्रकार चुन सकते हैं। नीचे हम एक **कॉलम चार्ट** बनाते हैं, लेकिन आप `ChartType` enum को बदलकर आसानी से लाइन, पाई, या बार चार्ट में स्विच कर सकते हैं।

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **प्रो टिप:** Excel चार्ट प्रकार बदलने के लिए, `ChartType.COLUMN` को `ChartType.LINE`, `ChartType.PIE` आदि से बदलें।

## चरण 4: इंटरैक्टिविटी जोड़ना

### 4.1. टूलटिप्स जोड़ना (Add Tooltips to Chart)

टूलटिप्स तब दिखते हैं जब उपयोगकर्ता डेटा पॉइंट पर होवर करता है। निम्नलिखित कोड डेटा लेबल्स को सक्षम करता है और वैल्यू को टूलटिप के रूप में दिखाता है।

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. डेटा लेबल्स जोड़ना – **add data labels to excel chart**

डेटा लेबल्स चार्ट पर स्थायी विज़ुअल संकेत प्रदान करते हैं। आप बेहतर पठनीयता के लिए उन्हें कॉलआउट के रूप में प्रदर्शित कर सकते हैं।

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

> **डेटा लेबल्स क्यों जोड़ें?** चार्ट पर सीधे डेटा लेबल्स होने से उपयोगकर्ताओं को होवर या अनुमान लगाने की आवश्यकता नहीं रहती, जिससे रिपोर्ट की स्पष्टता बढ़ती है।

### 4.3. ड्रिल‑डाउन लागू करना (डेटा पॉइंट पर हाइपरलिंक)

ड्रिल‑डाउन क्षमता जोड़ने का एक सरल तरीका है कि किसी विशिष्ट पॉइंट पर हाइपरलिंक संलग्न करें। पॉइंट पर क्लिक करने से विस्तृत जानकारी वाला वेब पेज खुलता है।

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## चरण 5: वर्कबुक को सहेजना

चार्ट को कॉन्फ़िगर करने के बाद, वर्कबुक को सहेजें ताकि इंटरैक्टिव फीचर्स आउटपुट फ़ाइल में स्टोर हो जाएँ।

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## सामान्य समस्याएँ और समाधान

| समस्या | समाधान |
|-------|----------|
| **टूलटिप्स नहीं दिख रहे** | `setHasDataLabels(true)` को `setShowValue(true)` कॉन्फ़िगर करने से पहले कॉल करना सुनिश्चित करें। |
| **हाइपरलिंक क्लिक नहीं हो रहा** | आउटपुट फ़ॉर्मेट हाइपरलिंक को सपोर्ट करता है (जैसे XLSX, CSV नहीं) यह जाँचें। |
| **चार्ट प्रकार नहीं बदल रहा** | चार्ट जोड़ते समय सही `ChartType` enum को संशोधित किया है या नहीं, दोबारा जांचें। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: चार्ट बन जाने के बाद उसका प्रकार कैसे बदलूँ?**  
**उत्तर:** आपको इच्छित `ChartType` के साथ एक नया चार्ट बनाना होगा। Aspose.Cells इन‑प्लेस टाइप कन्वर्ज़न प्रदान नहीं करता, इसलिए पुराने चार्ट को हटाकर नया जोड़ें।

**प्रश्न: क्या मैं टूलटिप्स की उपस्थिति को कस्टमाइज़ कर सकता हूँ?**  
**उत्तर:** हाँ। `DataLabel` प्रॉपर्टीज़ जैसे `setFontSize`, `setFontColor`, और `setBackgroundColor` का उपयोग करके टूलटिप टेक्स्ट को स्टाइल कर सकते हैं।

**प्रश्न: वेब एप्लिकेशन में उपयोगकर्ता इंटरैक्शन कैसे हैंडल करूँ?**  
**उत्तर:** वर्कबुक को HTML या XLSX फ़ाइल में एक्सपोर्ट करें और क्लाइंट साइड पर चार्ट एलिमेंट्स पर क्लिक इवेंट कैप्चर करने के लिए JavaScript उपयोग करें।

**प्रश्न: अधिक उदाहरण और दस्तावेज़ कहाँ मिलेंगे?**  
**उत्तर:** पूर्ण चार्ट‑संबंधित क्लासेज़ और मेथड्स की सूची के लिए [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) देखें।

## निष्कर्ष

अब आप जानते हैं कि **Excel चार्ट में डेटा लेबल कैसे जोड़ें**, **Excel चार्ट प्रकार कैसे बदलें**, **इंटरैक्टिव चार्ट Java** समाधान कैसे बनाएं, और Aspose.Cells for Java का उपयोग करके टूलटिप्स, डेटा लेबल्स, और ड्रिल‑डाउन हाइपरलिंक्स के साथ उन्हें कैसे समृद्ध करें। ये सुधार आपके Excel रिपोर्ट को अंतिम उपयोगकर्ताओं के लिए अधिक आकर्षक और अंतर्दृष्टिपूर्ण बनाते हैं।

---

**अंतिम अपडेट:** 2026-02-09  
**परीक्षित संस्करण:** Aspose.Cells for Java 24.12  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}