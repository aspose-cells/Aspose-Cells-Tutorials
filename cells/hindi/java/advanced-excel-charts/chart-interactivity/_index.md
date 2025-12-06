---
date: 2025-12-06
description: Aspose.Cells का उपयोग करके जावा में Excel चार्ट प्रकार कैसे बदलें और
  इंटरैक्टिव चार्ट बनाएं, सीखें। चार्ट में टूलटिप्स, डेटा लेबल्स जोड़ें, और समृद्ध
  डेटा विज़ुअलाइज़ेशन के लिए ड्रिल‑डाउन लागू करें।
language: hi
linktitle: Change Excel Chart Type
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells Java के साथ Excel चार्ट प्रकार बदलें
url: /java/advanced-excel-charts/chart-interactivity/
weight: 19
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel चार्ट प्रकार बदलें और इंटरैक्टिविटी जोड़ें

## परिचय

इंटरैक्टिव चार्ट आपके Excel रिपोर्ट्स को नई अंतर्दृष्टि का स्तर प्रदान करते हैं, जिससे उपयोगकर्ता डेटा पॉइंट्स पर होवर, क्लिक और सीधे अन्वेषण कर सकते हैं। इस ट्यूटोरियल में आप **Excel चार्ट प्रकार बदलेंगे** और Aspose.Cells for Java के साथ **इंटरैक्टिव चार्ट Java** समाधान बनाएँगे। हम चार्ट में टूलटिप्स, डेटा लेबल्स, और एक सरल ड्रिल‑डाउन हाइपरलिंक जोड़ने की प्रक्रिया को कवर करेंगे ताकि आपका दर्शक संख्याओं में गहराई से जा सके।

## त्वरित उत्तर
- **क्या लाइब्रेरी उपयोग की गई है?** Aspose.Cells for Java  
- **क्या मैं चार्ट प्रकार बदल सकता हूँ?** हाँ – जब आप चार्ट बनाते हैं तो `ChartType` enum को संशोधित करें।  
- **चार्ट में टूलटिप्स कैसे जोड़ें?** डेटा‑लेबल API (`setHasDataLabels(true)`) का उपयोग करें और वैल्यू डिस्प्ले सक्षम करें।  
- **क्या ड्रिल‑डाउन समर्थित है?** आप डेटा पॉइंट्स पर हाइपरलिंक संलग्न करके बेसिक ड्रिल‑डाउन व्यवहार प्राप्त कर सकते हैं।  
- **पूर्वापेक्षाएँ?** Java IDE, Aspose.Cells JAR, और एक Excel फ़ाइल जिसमें नमूना डेटा हो।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

- Java Development Environment (JDK 8+ अनुशंसित)  
- Aspose.Cells for Java लाइब्रेरी (डाउनलोड करें [here](https://releases.aspose.com/cells/java/))  
- एक नमूना वर्कबुक (`data.xlsx`) जिसमें वह डेटा हो जिसे आप विज़ुअलाइज़ करना चाहते हैं  

## चरण 1: अपना Java प्रोजेक्ट सेटअप करना

1. अपने पसंदीदा IDE (IntelliJ IDEA, Eclipse, आदि) में एक नया Java प्रोजेक्ट बनाएँ।  
2. Aspose.Cells JAR को अपने प्रोजेक्ट के बिल्ड पाथ या Maven/Gradle डिपेंडेंसीज़ में जोड़ें।

## चरण 2: डेटा लोड करना

चार्ट्स के साथ काम करने के लिए आपको पहले मेमोरी में एक वर्कबुक लोड करनी होगी।

```java
// Load the Excel file
Workbook workbook = new Workbook("data.xlsx");
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## चरण 3: चार्ट बनाना (और उसका प्रकार बदलना)

आप अपनी विश्लेषण के अनुसार कोई भी चार्ट प्रकार चुन सकते हैं। नीचे हम एक **column chart** बनाते हैं, लेकिन आप `ChartType` enum को बदलकर आसानी से लाइन, पाई, या बार चार्ट में स्विच कर सकते हैं।

```java
// Create a column chart
int chartIndex = worksheet.getCharts().add(ChartType.COLUMN, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);
```

> **Pro tip:** **Excel चार्ट प्रकार बदलने** के लिए, `ChartType.COLUMN` को `ChartType.LINE`, `ChartType.PIE` आदि से बदलें।

## चरण 4: इंटरैक्टिविटी जोड़ना

### 4.1. टूलटिप्स जोड़ना (Add Tooltips to Chart)

जब उपयोगकर्ता डेटा पॉइंट पर होवर करता है तो टूलटिप्स दिखाई देते हैं। निम्नलिखित कोड डेटा लेबल्स को सक्षम करता है और वैल्यू को टूलटिप के रूप में दिखाता है।

```java
// Enable tooltips for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowValue(true);
```

### 4.2. डेटा लेबल्स जोड़ना

डेटा लेबल्स चार्ट पर एक स्थायी विज़ुअल संकेत प्रदान करते हैं। आप बेहतर पठनीयता के लिए उन्हें कॉलआउट के रूप में प्रदर्शित कर सकते हैं।

```java
// Enable data labels for data points
chart.getNSeries().get(0).getPoints().setHasDataLabels(true);
chart.getNSeries().get(0).getPoints().getDataLabels().setShowLabelAsDataCallout(true);
```

### 4.3. ड्रिल‑डाउन लागू करना (डेटा पॉइंट पर हाइपरलिंक)

ड्रिल‑डाउन क्षमता जोड़ने का एक सरल तरीका है किसी विशिष्ट पॉइंट पर हाइपरलिंक संलग्न करना। पॉइंट पर क्लिक करने से विस्तृत जानकारी वाला वेब पेज खुलता है।

```java
// Add a hyperlink to a data point
String url = "https://example.com/data-details";
chart.getNSeries().get(0).getPoints().get(0).getHyperlinks().add(url);
```

## चरण 5: वर्कबुक सहेजना

चार्ट को कॉन्फ़िगर करने के बाद, वर्कबुक को स्थायी बनाएं ताकि इंटरैक्टिव फीचर्स आउटपुट फ़ाइल में संग्रहीत हों।

```java
// Save the workbook
workbook.save("interactive_chart_output.xlsx");
```

## सामान्य समस्याएँ और समाधान

| समस्या | समाधान |
|-------|----------|
| **टूलटिप्स नहीं दिख रहे** | सुनिश्चित करें कि `setHasDataLabels(true)` को `setShowValue(true)` कॉन्फ़िगर करने से पहले कॉल किया गया है। |
| **हाइपरलिंक क्लिक नहीं हो रहा** | जांचें कि आउटपुट फ़ॉर्मेट हाइपरलिंक को सपोर्ट करता है (जैसे XLSX, CSV नहीं)। |
| **चार्ट प्रकार नहीं बदल रहा** | जब आप चार्ट जोड़ते हैं, तो सही `ChartType` enum को संशोधित किया है या नहीं, दोबारा जांचें। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: चार्ट बन जाने के बाद मैं उसका प्रकार कैसे बदल सकता हूँ?**  
**उत्तर:** आपको इच्छित `ChartType` के साथ एक नया चार्ट बनाना होगा। Aspose.Cells इन‑प्लेस प्रकार परिवर्तन प्रदान नहीं करता, इसलिए पुराने चार्ट को हटाएँ और नया जोड़ें।

**प्रश्न: क्या मैं टूलटिप्स की उपस्थिति को कस्टमाइज़ कर सकता हूँ?**  
**उत्तर:** हाँ। `DataLabel` प्रॉपर्टीज़ जैसे `setFontSize`, `setFontColor`, और `setBackgroundColor` का उपयोग करके टूलटिप टेक्स्ट को स्टाइल कर सकते हैं।

**प्रश्न: वेब एप्लिकेशन में उपयोगकर्ता इंटरैक्शन कैसे संभालें?**  
**उत्तर:** वर्कबुक को HTML या XLSX फ़ाइल में एक्सपोर्ट करें और क्लाइंट साइड पर चार्ट एलिमेंट्स पर क्लिक इवेंट कैप्चर करने के लिए JavaScript का उपयोग करें।

**प्रश्न: अधिक उदाहरण और दस्तावेज़ कहाँ मिलेंगे?**  
**उत्तर:** पूरी चार्ट‑संबंधित क्लासेस और मेथड्स की सूची के लिए [Aspose.Cells Java API Reference](https://reference.aspose.com/cells/java/) देखें।

## निष्कर्ष

अब आप जानते हैं कि **Excel चार्ट प्रकार कैसे बदलें**, **इंटरैक्टिव चार्ट Java** समाधान कैसे बनाएं, और Aspose.Cells for Java का उपयोग करके टूलटिप्स, डेटा लेबल्स, और ड्रिल‑डाउन हाइपरलिंक्स के साथ उन्हें कैसे समृद्ध करें। ये सुधार आपके Excel रिपोर्ट्स को अंतिम उपयोगकर्ताओं के लिए अधिक आकर्षक और अंतर्दृष्टिपूर्ण बनाते हैं।

---

**अंतिम अपडेट:** 2025-12-06  
**परीक्षण किया गया:** Aspose.Cells for Java 24.12  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}