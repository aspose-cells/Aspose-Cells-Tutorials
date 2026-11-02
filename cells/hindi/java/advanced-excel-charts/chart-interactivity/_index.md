---
date: 2026-08-21
description: Aspose.Cells for Java का उपयोग करके Excel चार्ट्स में टूलटिप्स, डेटा
  लेबल जोड़ना और चार्ट टाइप बदलना सीखें – चरण‑दर‑चरण गाइड इंटरैक्टिव उदाहरणों के साथ।
keywords:
- how to add tooltips
- how to change chart type
- how to add data labels
lastmod: 2026-08-21
linktitle: Excel चार्ट टाइप बदलें
og_description: Aspose.Cells for Java का उपयोग करके Excel चार्ट्स में टूलटिप्स, डेटा
  लेबल जोड़ना और चार्ट टाइप बदलना सीखें – चरण‑दर‑चरण गाइड इंटरैक्टिव उदाहरणों के साथ।
og_image_alt: 'Developer guide: Adding tooltips and data labels to Excel charts with
  Aspose.Cells for Java'
og_title: Java में Excel चार्ट्स में टूलटिप्स और डेटा लेबल जोड़ने का तरीका
schemas:
- author: Aspose
  dateModified: '2026-08-21'
  description: Learn how to add tooltips, data labels, and change chart type in Excel
    charts using Aspose.Cells for Java – step‑by‑step guide with interactive examples.
  headline: How to add tooltips and data labels to Excel charts in Java
  type: TechArticle
- questions:
  - answer: You need to create a new chart with the desired `ChartType`. Aspose.Cells
      does not provide an in‑place type conversion, so remove the old chart and add
      a new one.
    question: How can I change the chart type after it’s created?
  - answer: Yes. Use the `DataLabel` properties such as `setFontSize`, `setFontColor`,
      and `setBackgroundColor` to style the tooltip text.
    question: Can I customize the appearance of tooltips?
  - answer: Export the workbook to an HTML or XLSX file and use JavaScript on the
      client side to capture click events on chart elements.
    question: How do I handle user interactions in a web application?
  - answer: Visit the [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/)
      for a full list of chart‑related classes and methods.
    question: Where can I find more examples and documentation?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java chart
- Excel interactivity
- tooltips
- data labels
title: Java में Excel चार्ट्स में टूलटिप्स और डेटा लेबल जोड़ने का तरीका
url: /hi/java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel चार्ट में डेटा लेबल जोड़ें और चार्ट प्रकार बदलें – Aspose.Cells Java

इंटरैक्टिव चार्ट्स आपके Excel रिपोर्ट्स को नई अंतर्दृष्टि प्रदान करते हैं, और **टूलटिप्स कैसे जोड़ें** जानकारी को तुरंत पढ़ने योग्य बनाता है। इस ट्यूटोरियल में आप सीखेंगे कैसे **Excel चार्ट में डेटा लेबल जोड़ें**, **चार्ट प्रकार बदलें**, और Aspose.Cells के साथ इंटरैक्टिव Java समाधान बनाएं। हम आपको टूलटिप्स और एक सरल ड्रिल‑डाउन हाइपरलिंक जोड़ने का तरीका भी दिखाएंगे ताकि आपका दर्शक डेटा को गहराई से एक्सप्लोर कर सके।

## त्वरित उत्तर
- **क्या लाइब्रेरी उपयोग की गई है?** Aspose.Cells for Java  
- **क्या मैं चार्ट प्रकार बदल सकता हूँ?** हाँ – जब आप चार्ट बनाते हैं तो `ChartType` enum को संशोधित करें।  
- **चार्ट में टूलटिप्स कैसे जोड़ें?** डेटा‑लेबल API (`setHasDataLabels(true)`) का उपयोग करें और वैल्यू डिस्प्ले सक्षम करें।  
- **क्या ड्रिल‑डाउन समर्थित है?** आप डेटा पॉइंट्स पर हाइपरलिंक संलग्न करके बुनियादी ड्रिल‑डाउन व्यवहार प्राप्त कर सकते हैं।  
- **पूर्वापेक्षाएँ?** Java IDE, Aspose.Cells JAR, और नमूना डेटा वाली एक Excel फ़ाइल।  

## टूलटिप्स कैसे जोड़ें क्या है?
**टूलटिप्स कैसे जोड़ें** वह प्रक्रिया है जो Excel चार्ट पर होवर‑ओवर टेक्स्ट को सक्षम करती है, जो डेटा पॉइंट का मान या कस्टम जानकारी प्रदर्शित करती है। Aspose.Cells में यह चार्ट की डेटा‑लेबल सेटिंग्स के माध्यम से प्राप्त किया जाता है। टूलटिप्स उपयोगकर्ताओं को चार्ट को अव्यवस्थित किए बिना डेटा को जल्दी समझने में मदद करती हैं, और इन्हें फ़ॉन्ट, रंग, और फ़ॉर्मेट के लिए कस्टमाइज़ किया जा सकता है।

## Aspose.Cells के साथ इंटरैक्टिव चार्ट्स क्यों उपयोग करें?
Aspose.Cells **50+ इनपुट और आउटपुट फ़ॉर्मेट** को सपोर्ट करता है—जैसे XLSX, CSV, PDF, और HTML—और **1 000 से अधिक शीट्स** वाले वर्कबुक को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, जिससे एंटरप्राइज़ रिपोर्टिंग के लिए तेज़, सर्वर‑साइड चार्ट जेनरेशन मिलता है। इंटरैक्टिव चार्ट्स हाइपरलिंक एम्बेडिंग, डायनामिक डेटा अपडेट, और वेब‑फ्रेंडली फ़ॉर्मेट में एक्सपोर्ट की सुविधा भी देते हैं, जिससे वे डैशबोर्ड और रिपोर्टिंग पोर्टल्स के लिए आदर्श बनते हैं।

## पूर्वापेक्षाएँ

- Java डेवलपमेंट एनवायरनमेंट (JDK 8+ अनुशंसित)  
- Aspose.Cells for Java लाइब्रेरी (डाउनलोड करें [Aspose.Cells for Java download page](https://releases.aspose.com/cells/java/))  
- एक नमूना वर्कबुक (`data.xlsx`) जिसमें वह डेटा हो जिसे आप विज़ुअलाइज़ करना चाहते हैं  

## चरण 1: अपना Java प्रोजेक्ट सेटअप करना

1. अपने पसंदीदा IDE (IntelliJ IDEA, Eclipse, आदि) में एक नया Java प्रोजेक्ट बनाएं।  
2. Aspose.Cells JAR को अपने प्रोजेक्ट के बिल्ड पाथ या Maven/Gradle डिपेंडेंसीज़ में जोड़ें।

## चरण 2: डेटा लोड करना

चार्ट्स के साथ काम करने के लिए आपको पहले एक वर्कबुक को मेमोरी में लोड करना होगा।

`Workbook` क्लास एक Excel फ़ाइल को दर्शाता है, और `Worksheet` उस फ़ाइल के भीतर एक सिंगल शीट को दर्शाता है।

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## Aspose.Cells में चार्ट प्रकार कैसे बदलें?

इच्छित `ChartType` enum के साथ एक नया चार्ट बनाएं; Aspose.Cells मौजूदा चार्ट के प्रकार को इन‑प्लेस संशोधित नहीं करता, इसलिए आपको सही प्रकार का नया चार्ट जोड़ना होगा और वैकल्पिक रूप से पुराने को हटाना होगा। यह तरीका सुनिश्चित करता है कि सभी सीरीज़ और एक्सिस नई विज़ुअल रिप्रेजेंटेशन के लिए सही ढंग से पुनर्निर्मित हों।

## चरण 3: चार्ट बनाना (और उसका प्रकार बदलना)

आप अपनी विश्लेषण के अनुसार कोई भी चार्ट प्रकार चुन सकते हैं। नीचे हम एक **कॉलम चार्ट** बनाते हैं, लेकिन आप `ChartType` enum को बदलकर आसानी से लाइन, पाई, या बार चार्ट में स्विच कर सकते हैं।

`Chart` ऑब्जेक्ट वर्कशीट में डेटा की विज़ुअल रिप्रेजेंटेशन को कॉन्फ़िगर करने के मेथड्स प्रदान करता है।

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

**Pro tip:** **Excel चार्ट प्रकार बदलने** के लिए, `ChartType.COLUMN` को `ChartType.LINE`, `ChartType.PIE` आदि से बदलें।

## Excel चार्ट में टूलटिप्स कैसे जोड़ें?

अपने चार्ट को लोड करें, डेटा लेबल सक्षम करें, और `showValue` फ़्लैग सेट करें। तब टूलटिप उपयोगकर्ता के डेटा पॉइंट पर होवर करने पर अंतर्निहित सेल वैल्यू प्रदर्शित करेगा, चाहे वह रेंडर किया गया Excel फ़ाइल हो या HTML व्यू। आप टूलटिप के फ़ॉन्ट, रंग, और बैकग्राउंड को अपनी रिपोर्ट की शैली के अनुसार कस्टमाइज़ भी कर सकते हैं।

`DataLabel` क्लास डेटा लेबल की उपस्थिति और सामग्री को नियंत्रित करती है, जो टूलटिप के रूप में भी कार्य करती है।

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

## चरण 4: इंटरैक्टिविटी जोड़ना

### 4.1. टूलटिप्स जोड़ना (चार्ट में टूलटिप्स जोड़ें)

जब उपयोगकर्ता डेटा पॉइंट पर होवर करता है तो टूलटिप्स दिखाई देते हैं। नीचे दिया गया कोड डेटा लेबल सक्षम करता है और वैल्यू को टूलटिप के रूप में दिखाता है।

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.2. डेटा लेबल जोड़ना – **Excel चार्ट में डेटा लेबल जोड़ें**

डेटा लेबल चार्ट पर एक स्थायी विज़ुअल संकेत प्रदान करते हैं। आप उन्हें बेहतर पठनीयता के लिए कॉलआउट के रूप में प्रदर्शित कर सकते हैं।

`DataLabel` क्लास प्रत्येक सीरीज़ पर लेबल की उपस्थिति को नियंत्रित करती है। `setHasDataLabels(true)` को कॉल करके और `setShowValue(true)` जैसे प्रॉपर्टीज़ को कॉन्फ़िगर करके, आप संख्यात्मक वैल्यू को सीधे चार्ट पर एम्बेड करते हैं, जिससे यह बिना किसी इंटरैक्शन के तुरंत दिखाई देता है। अतिरिक्त विकल्प आपको सीरीज़ नाम, प्रतिशत, या कस्टम टेक्स्ट दिखाने की अनुमति देते हैं जिससे अधिक संदर्भ मिलता है।

> **डेटा लेबल क्यों जोड़ें?** चार्ट पर सीधे डेटा लेबल शामिल करने से उपयोगकर्ताओं को होवर या वैल्यू अनुमान करने की आवश्यकता नहीं रहती, जिससे रिपोर्ट की स्पष्टता बढ़ती है।

### 4.3. ड्रिल‑डाउन लागू करना (डेटा पॉइंट पर हाइपरलिंक)

ड्रिल‑डाउन क्षमता जोड़ने का एक सरल तरीका है किसी विशिष्ट पॉइंट पर हाइपरलिंक संलग्न करना। पॉइंट पर क्लिक करने से विस्तृत जानकारी वाला वेब पेज खुलता है।

`Hyperlink` क्लास चार्ट एलिमेंट पर एक क्लिकेबल लिंक संलग्न करती है, जिससे ड्रिल‑डाउन नेविगेशन सक्षम होता है।

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## Excel चार्ट में डेटा लेबल कैसे जोड़ें?

`DataLabel` क्लास प्रत्येक सीरीज़ पर लेबल की उपस्थिति को नियंत्रित करती है। `setHasDataLabels(true)` को कॉल करके और `setShowValue(true)` जैसे प्रॉपर्टीज़ को कॉन्फ़िगर करके, आप संख्यात्मक वैल्यू को सीधे चार्ट पर एम्बेड करते हैं, जिससे यह बिना किसी इंटरैक्शन के तुरंत दिखाई देता है। अतिरिक्त विकल्प आपको सीरीज़ नाम, प्रतिशत, या कस्टम टेक्स्ट दिखाने की अनुमति देते हैं जिससे अधिक संदर्भ मिलता है।

## चरण 5: वर्कबुक सहेजना

चार्ट को कॉन्फ़िगर करने के बाद, वर्कबुक को सहेजें ताकि इंटरैक्टिव फीचर्स आउटपुट फ़ाइल में स्टोर हो जाएँ।

`workbook.save` को कॉल करने से संशोधित वर्कबुक चुने गए फ़ॉर्मेट में फ़ाइल में लिखी जाती है।

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## सामान्य समस्याएँ और समाधान

| समस्या | समाधान |
|-------|----------|
| **टूलटिप्स नहीं दिख रहे** | `setHasDataLabels(true)` को `setShowValue(true)` कॉन्फ़िगर करने से पहले कॉल किया गया है, यह सुनिश्चित करें। |
| **हाइपरलिंक क्लिक नहीं हो रहा** | जाँचें कि आउटपुट फ़ॉर्मेट हाइपरलिंक को सपोर्ट करता है (जैसे XLSX, CSV नहीं)। |
| **चार्ट प्रकार नहीं बदल रहा** | जब चार्ट जोड़ रहे हों तो सही `ChartType` enum को संशोधित किया है, यह दोबारा जांचें। |

## अक्सर पूछे जाने वाले प्रश्न

**मैं चार्ट बन जाने के बाद उसका प्रकार कैसे बदल सकता हूँ?**  
आपको इच्छित `ChartType` के साथ एक नया चार्ट बनाना होगा। Aspose.Cells इन‑प्लेस टाइप कन्वर्ज़न प्रदान नहीं करता, इसलिए पुराने चार्ट को हटाएँ और नया जोड़ें।

**क्या मैं टूलटिप्स की उपस्थिति कस्टमाइज़ कर सकता हूँ?**  
हाँ। `DataLabel` प्रॉपर्टीज़ जैसे `setFontSize`, `setFontColor`, और `setBackgroundColor` का उपयोग करके टूलटिप टेक्स्ट को स्टाइल कर सकते हैं।

**मैं वेब एप्लिकेशन में उपयोगकर्ता इंटरैक्शन कैसे संभालूँ?**  
वर्कबुक को HTML या XLSX फ़ाइल में एक्सपोर्ट करें और क्लाइंट साइड पर जावास्क्रिप्ट का उपयोग करके चार्ट एलिमेंट्स पर क्लिक इवेंट्स को कैप्चर करें।

**मैं अधिक उदाहरण और दस्तावेज़ कहाँ पा सकता हूँ?**  
चार्ट‑संबंधित क्लासेज़ और मेथड्स की पूरी सूची के लिए [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) पर जाएँ।

## निष्कर्ष

अब आप जानते हैं कि **Excel चार्ट में डेटा लेबल कैसे जोड़ें**, **Excel चार्ट प्रकार कैसे बदलें**, **इंटरैक्टिव चार्ट Java** समाधान कैसे बनाएं, और Aspose.Cells for Java का उपयोग करके उन्हें टूलटिप्स, डेटा लेबल, और ड्रिल‑डाउन हाइपरलिंक से कैसे समृद्ध करें। ये सुधार आपके Excel रिपोर्ट को अंतिम उपयोगकर्ताओं के लिए अधिक आकर्षक और अंतर्दृष्टिपूर्ण बनाते हैं।

---

**अंतिम अपडेट:** 2026-08-21  
**परीक्षण किया गया:** Aspose.Cells for Java 24.12  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose.Cells for Java का उपयोग करके Excel चार्ट और डेटा लेबल कैसे संशोधित करें](/cells/java/charts-graphs/aspose-cells-java-modify-excel-charts-data-labels/)
- [Aspose.Cells Java का उपयोग करके Excel चार्ट एक्सिस लेबल निकालें: एक व्यापक गाइड](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)
- [Aspose.Cells for Java का उपयोग करके Excel में बबल चार्ट बनाएं: चरण‑दर‑चरण गाइड](/cells/java/charts-graphs/aspose-cells-java-create-bubble-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}