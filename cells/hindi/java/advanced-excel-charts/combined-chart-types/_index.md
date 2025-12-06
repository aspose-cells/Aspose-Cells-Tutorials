---
date: 2025-12-06
description: Aspose.Cells for Java के साथ डेटा सीरीज़ जोड़ना, संयुक्त चार्ट प्रकार
  बनाना, वर्कबुक को Excel में सहेजना और चार्ट को PNG में निर्यात करना सीखें।
language: hi
linktitle: Add data series to create combined chart using Aspose.Cells
second_title: Aspose.Cells Java Excel Processing API
title: Aspose.Cells का उपयोग करके संयुक्त चार्ट बनाने के लिए डेटा सीरीज़ जोड़ें
url: /java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells का उपयोग करके संयुक्त चार्ट बनाने के लिए डेटा सीरीज़ जोड़ें

इस ट्यूटोरियल में आप **डेटा सीरीज़** को एक Excel वर्कबुक में जोड़ेंगे और Aspose.Cells for Java के साथ **संयुक्त चार्ट** प्रकार बनाना सीखेंगे। हम हर चरण को विस्तार से दिखाएंगे—वर्कबुक सेटअप करने से, सीरीज़ जोड़ने, लेजेंड को कस्टमाइज़ करने, **वर्कबुक Excel** फ़ाइलें सहेजने और **चार्ट को PNG** में निर्यात करने तक। अंत तक, आपके पास एक तैयार‑से‑उपयोग संयुक्त चार्ट होगा जिसे आप रिपोर्ट या डैशबोर्ड में एम्बेड कर सकते हैं।

## त्वरित उत्तर
- **कौन सा लाइब्रेरी संयुक्त चार्ट बनाता है?** Aspose.Cells for Java  
- **डेटा सीरीज़ कैसे जोड़ें?** Use `chart.getNSeries().add(...)`  
- **क्या मैं चार्ट को इमेज के रूप में निर्यात कर सकता हूँ?** Yes, with `chart.toImage(...)` (PNG)  
- **वर्कबुक को किस फ़ाइल फ़ॉर्मेट में सहेज सकते हैं?** Standard `.xlsx` (Excel)  
- **उत्पादन के लिए लाइसेंस आवश्यक है?** A valid Aspose.Cells license is required  

## Aspose.Cells में **add data series** क्या है?
डेटा सीरीज़ जोड़ने से चार्ट को पता चलता है कि कौन से सेल्स में वे मान हैं जिन्हें आप प्लॉट करना चाहते हैं। प्रत्येक सीरीज़ एक लाइन, कॉलम, या किसी अन्य चार्ट प्रकार का प्रतिनिधित्व कर सकती है, और आप उन्हें मिलाकर **संयुक्त चार्ट** बना सकते हैं।

## **संयुक्त चार्ट** क्यों बनाएं?
एक संयुक्त चार्ट आपको विभिन्न डेटा सेट्स को अलग-अलग दृश्य प्रतिनिधित्व (जैसे, कॉलम सीरीज़ के ऊपर एक लाइन सीरीज़) के साथ एक ही दृश्य में दिखाने देता है। यह कुलों के मुकाबले रुझानों की तुलना करने, सहसंबंधों को उजागर करने, या संक्षिप्त प्रारूप में अधिक समृद्ध अंतर्दृष्टि प्रदान करने के लिए आदर्श है।

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) 8 या उससे ऊपर  
- Aspose.Cells for Java लाइब्रेरी (नीचे दिए लिंक से डाउनलोड करें)  
- Java सिंटैक्स और Excel अवधारणाओं की बुनियादी परिचितता  

## शुरूआत

सबसे पहले, आधिकारिक साइट से Aspose.Cells for Java लाइब्रेरी डाउनलोड करें:

[Aspose.Cells for Java डाउनलोड करें](https://releases.aspose.com/cells/java/)

एक बार JAR को आपके प्रोजेक्ट की क्लासपाथ में जोड़ने के बाद, आप चार्ट बनाना शुरू कर सकते हैं।

### चरण 1: Aspose.Cells क्लासेस इम्पोर्ट करें
```java
import com.aspose.cells.*;
```

### चरण 2: नया वर्कबुक बनाएं
```java
Workbook workbook = new Workbook();
```

### चरण 3: पहली वर्कशीट तक पहुंचें
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### चरण 4: एक संयुक्त चार्ट ऑब्जेक्ट जोड़ें
हम एक लाइन चार्ट से शुरू करेंगे और बाद में अन्य सीरीज़ जोड़ेंगे ताकि **संयुक्त चार्ट** प्रभाव प्राप्त हो सके।
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## चार्ट में डेटा जोड़ना

अब जबकि चार्ट कंटेनर मौजूद है, हमें इसमें डेटा फीड करना होगा।

### चरण 5: डेटा रेंज निर्धारित करें और **डेटा सीरीज़ जोड़ें**
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **Pro tip:** पहला पैरामीटर (`"A1:A5"`) पहली सीरीज़ की रेंज है, और दूसरा (`"B1:B5"`) एक दूसरी सीरीज़ बनाता है जिसे पहली के साथ मिलाया जाएगा।

### चरण 6: श्रेणी (X‑axis) डेटा सेट करें
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## चार्ट को कस्टमाइज़ करना

एक अच्छा चार्ट कहानी बताता है। चलिए इसे शीर्षक, अक्ष लेबल और एक स्पष्ट लेजेंड देते हैं।

### चरण 7: चार्ट शीर्षक और अक्ष लेबल सेट करें
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### चरण 8: **लेजेंड चार्ट जोड़ें** और उसकी स्थिति समायोजित करें
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## चार्ट को सहेजना और निर्यात करना

कस्टमाइज़ करने के बाद, आप **वर्कबुक Excel** को सहेजना चाहेंगे और साथ ही एक इमेज जेनरेट करेंगे।

### चरण 9: वर्कबुक को Excel फ़ाइल के रूप में सहेजें
```java
workbook.save("CombinedChart.xlsx");
```

### चरण 10: **चार्ट को PNG** में निर्यात करें
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` मेथड **excel chart** इमेजेज़ जेनरेट करता है जिन्हें वेब पेज, रिपोर्ट या ईमेल में उपयोग किया जा सकता है।

## सामान्य समस्याएँ और ट्रबलशूटिंग

| समस्या | समाधान |
|-------|----------|
| **डेटा नहीं दिख रहा है** | चार्ट बनाने से पहले सुनिश्चित करें कि सेल रेंज (`A1:A5`, `B1:B5`, `C1:C5`) में वास्तव में डेटा मौजूद है। |
| **लेजेंड चार्ट के ऊपर ओवरलैप करता है** | `chart.getLegend().setOverlay(false)` सेट करें या लेजेंड को किसी अन्य स्थिति (जैसे, `RIGHT`) पर ले जाएँ। |
| **इमेज फ़ाइल खाली है** | सुनिश्चित करें कि चार्ट में कम से कम एक सीरीज़ हो और `chart.toImage` सभी कस्टमाइज़ेशन के बाद कॉल किया गया हो। |
| **सेव करते समय अपवाद आता है** | जाँचें कि आपके पास लक्ष्य डायरेक्टरी में लिखने की अनुमति है और फ़ाइल Excel में खुली नहीं है। |

## अक्सर पूछे जाने वाले प्रश्न

**Q: Aspose.Cells for Java को कैसे इंस्टॉल करें?**  
A: आधिकारिक साइट से JAR डाउनलोड करें और इसे अपने प्रोजेक्ट की क्लासपाथ में जोड़ें। डाउनलोड लिंक है: [Aspose.Cells for Java डाउनलोड करें](https://releases.aspose.com/cells/java/)

**Q: क्या मैं लाइन और कॉलम के अलावा अन्य चार्ट प्रकार बना सकता हूँ?**  
A: हाँ, Aspose.Cells बार, पाई, स्कैटर, एरिया और कई अन्य चार्ट प्रकारों को सपोर्ट करता है। पूरी सूची के लिए API डॉक्यूमेंटेशन देखें।

**Q: क्या उत्पादन उपयोग के लिए लाइसेंस आवश्यक है?**  
A: उत्पादन डिप्लॉयमेंट के लिए एक वैध Aspose.Cells लाइसेंस आवश्यक है। मूल्यांकन के लिए एक मुफ्त ट्रायल उपलब्ध है।

**Q: मैं प्रत्येक सीरीज़ के रंग कैसे बदल सकता हूँ?**  
A: `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (या समान) का उपयोग करके सीरीज़ जोड़ने के बाद रंग बदलें।

**Q: मैं अधिक कोड उदाहरण कहाँ पा सकता हूँ?**  
A: विस्तृत डॉक्यूमेंटेशन और अतिरिक्त सैंपल Aspose रेफ़रेंस साइट पर उपलब्ध हैं: [यहाँ](https://reference.aspose.com/cells/java/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

**अंतिम अपडेट:** 2025-12-06  
**परीक्षित संस्करण:** Aspose.Cells for Java 24.12  
**लेखक:** Aspose  

---