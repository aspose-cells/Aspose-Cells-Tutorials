---
date: 2026-02-14
description: Aspose.Cells for Java का उपयोग करके चार्ट को PNG में निर्यात करना, डेटा
  सीरीज़ जोड़ना, लाइन‑कॉलम चार्ट को संयोजित करना, वर्कबुक को XLSX के रूप में सहेजना
  और लेजेंड चार्ट जोड़ना सीखें।
linktitle: Export chart to PNG and add data series for combined chart
second_title: Aspose.Cells Java Excel Processing API
title: चार्ट को PNG में निर्यात करें और संयुक्त चार्ट के लिए डेटा श्रृंखला जोड़ें
url: /hi/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# चार्ट को PNG में निर्यात करें और संयुक्त चार्ट के लिए डेटा सीरीज़ जोड़ें

इस ट्यूटोरियल में आप **डेटा सीरीज़** को एक Excel वर्कबुक में **लाइन और कॉलम चार्ट** तत्वों को मिलाकर जोड़ेंगे, और Aspose.Cells for Java का उपयोग करके **चार्ट को PNG में निर्यात** करना सीखेंगे। हम हर कदम पर चलेंगे—वर्कबुक सेट अप करना, वर्कशीट में चार्ट जोड़ना, लेजेंड को कस्टमाइज़ करना, **वर्कबुक को xlsx के रूप में सहेजना** और चार्ट की PNG इमेज बनाना। अंत में आपके पास एक तैयार‑उपयोगी संयुक्त चार्ट होगा जिसे आप रिपोर्ट या डैशबोर्ड में एम्बेड कर सकते हैं।

## त्वरित उत्तर
- **कौन सा लाइब्रेरी संयुक्त चार्ट बनाता है?** Aspose.Cells for Java  
- **डेटा सीरीज़ कैसे जोड़ें?** `chart.getNSeries().add(...)` का उपयोग करें  
- **चार्ट को PNG में कैसे निर्यात करें?** `chart.toImage("file.png", ImageFormat.getPng())` को कॉल करें  
- **वर्कबुक को किस फ़ाइल फ़ॉर्मेट में सहेजा जा सकता है?** स्टैंडर्ड `.xlsx` (वर्कबुक को xlsx के रूप में सहेजें)  
- **प्रोडक्शन के लिए लाइसेंस चाहिए?** एक वैध Aspose.Cells लाइसेंस आवश्यक है  

## Aspose.Cells में **export chart to PNG** क्या है?
एक चार्ट को PNG में निर्यात करने से Excel चार्ट की रास्टर इमेज बनती है जिसे वेब पेज, रिपोर्ट या ईमेल में Excel एप्लिकेशन की आवश्यकता के बिना प्रदर्शित किया जा सकता है।

## **combined line column chart** क्यों बनाएं?
एक संयुक्त चार्ट आपको विभिन्न डेटा सेट्स को अलग-अलग दृश्य प्रतिनिधित्व (जैसे, कॉलम सीरीज़ के ऊपर एक लाइन सीरीज़) के साथ एक ही दृश्य में दिखाने की अनुमति देता है। यह कुल के मुकाबले रुझानों की तुलना करने, सहसंबंधों को उजागर करने, या एक कॉम्पैक्ट फ़ॉर्मेट में समृद्ध अंतर्दृष्टि प्रदान करने के लिए आदर्श है।

## पूर्व आवश्यकताएँ
- Java Development Kit (JDK) 8 या उससे ऊपर  
- Aspose.Cells for Java लाइब्रेरी (नीचे दिए लिंक से डाउनलोड करें)  
- Java सिंटैक्स और Excel अवधारणाओं की बुनियादी समझ  

## शुरूआत

सबसे पहले, आधिकारिक साइट से Aspose.Cells for Java लाइब्रेरी डाउनलोड करें:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

एक बार JAR को अपने प्रोजेक्ट के क्लासपाथ में जोड़ने के बाद, आप चार्ट बनाना शुरू कर सकते हैं।

### चरण 1: Aspose.Cells क्लासेस इम्पोर्ट करें
```java
import com.aspose.cells.*;
```

### चरण 2: नई वर्कबुक बनाएं
```java
Workbook workbook = new Workbook();
```

### चरण 3: पहली वर्कशीट तक पहुँचें
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### चरण 4: वर्कशीट में एक संयुक्त चार्ट ऑब्जेक्ट जोड़ें  
हम पहले एक लाइन चार्ट बनाएँगे और बाद में एक कॉलम सीरीज़ जोड़कर **combined line column chart** प्रभाव प्राप्त करेंगे।
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## चार्ट में डेटा जोड़ना

अब जब चार्ट कंटेनर मौजूद है, हमें इसमें डेटा फीड करना होगा।

### चरण 5: डेटा रेंज निर्धारित करें और **डेटा सीरीज़ जोड़ें**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **प्रो टिप:** पहला पैरामीटर (`"A1:A5"`) पहली सीरीज़ की रेंज है, और दूसरा (`"B1:B5"`) दूसरी सीरीज़ बनाता है जिसे पहली के साथ मिलाया जाएगा।

### चरण 6: कैटेगरी (X‑axis) डेटा सेट करें
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## चार्ट को कस्टमाइज़ करना

एक अच्छा चार्ट कहानी बताता है। चलिए इसे शीर्षक, एक्सिस लेबल और स्पष्ट लेजेंड देते हैं।

### चरण 7: **चार्ट एक्सिस लेबल** और शीर्षक सेट करें
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### चरण 8: **लेजेंड चार्ट** जोड़ें और उसकी स्थिति समायोजित करें
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## चार्ट को सहेजना और निर्यात करना

कस्टमाइज़ करने के बाद, आप **वर्कबुक को xlsx के रूप में सहेजना** चाहेंगे और साथ ही एक इमेज भी बनाना चाहेंगे।

### चरण 9: वर्कबुक को Excel फ़ाइल (xlsx) के रूप में सहेजें
```java
workbook.save("CombinedChart.xlsx");
```

### चरण 10: **चार्ट को PNG में निर्यात करें**
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` मेथड **Excel चार्ट** की इमेज बनाता है जिसे वेब पेज, रिपोर्ट या ईमेल में उपयोग किया जा सकता है।

## सामान्य समस्याएँ और ट्रबलशूटिंग

| समस्या | समाधान |
|-------|----------|
| **डेटा नहीं दिख रहा** | सुनिश्चित करें कि सेल रेंज (`A1:A5`, `B1:B5`, `C1:C5`) में वास्तव में डेटा मौजूद है चार्ट बनाने से पहले। |
| **लेजेंड चार्ट के ऊपर ओवरलैप हो रहा है** | `chart.getLegend().setOverlay(false)` सेट करें या लेजेंड को किसी अन्य पोज़िशन (जैसे, `RIGHT`) पर ले जाएँ। |
| **इमेज फ़ाइल खाली है** | यह सुनिश्चित करें कि चार्ट में कम से कम एक सीरीज़ हो और सभी कस्टमाइज़ेशन के बाद `chart.toImage` कॉल किया गया हो। |
| **सेव करते समय एक्सेप्शन आता है** | लक्ष्य डायरेक्टरी में लिखने की अनुमति जांचें और फ़ाइल Excel में खुली न हो। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: Aspose.Cells for Java को कैसे इंस्टॉल करें?**  
उत्तर: आधिकारिक साइट से JAR डाउनलोड करें और उसे अपने प्रोजेक्ट के क्लासपाथ में जोड़ें। डाउनलोड लिंक है: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)।

**प्रश्न: क्या मैं लाइन और कॉलम के अलावा अन्य चार्ट प्रकार बना सकता हूँ?**  
उत्तर: हाँ, Aspose.Cells बार, पाई, स्कैटर, एरिया और कई अन्य चार्ट प्रकारों को सपोर्ट करता है। पूरी सूची के लिए API डॉक्यूमेंटेशन देखें।

**प्रश्न: प्रोडक्शन उपयोग के लिए लाइसेंस आवश्यक है?**  
उत्तर: प्रोडक्शन डिप्लॉयमेंट के लिए एक वैध Aspose.Cells लाइसेंस आवश्यक है। मूल्यांकन के लिए एक फ्री ट्रायल उपलब्ध है।

**प्रश्न: प्रत्येक सीरीज़ के रंग कैसे बदलें?**  
उत्तर: सीरीज़ जोड़ने के बाद `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (या समान) का उपयोग करें।

**प्रश्न: अधिक कोड उदाहरण कहाँ मिलेंगे?**  
उत्तर: व्यापक डॉक्यूमेंटेशन और अतिरिक्त सैंपल Aspose रेफ़रेंस साइट पर उपलब्ध हैं: [here](https://reference.aspose.com/cells/java/)।

---

**अंतिम अपडेट:** 2026-02-14  
**टेस्टेड विद:** Aspose.Cells for Java नवीनतम संस्करण  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}