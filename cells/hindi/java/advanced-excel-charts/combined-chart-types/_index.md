---
date: 2026-09-02
description: Aspose.Cells for Java का उपयोग करके चार्ट को PNG में निर्यात करना, डेटा
  सीरीज़ जोड़ना, लाइन और कॉलम चार्ट को संयोजित करना, वर्कबुक को XLSX के रूप में सहेजना
  और लेजेंड चार्ट जोड़ना सीखें।
keywords:
- export chart to png
- combine line and column chart
- save workbook as xlsx
- generate chart image java
lastmod: 2026-09-02
linktitle: संयुक्त चार्ट के लिए चार्ट को PNG में निर्यात करें और डेटा सीरीज़ जोड़ें
og_description: Aspose.Cells for Java के साथ चार्ट को PNG में निर्यात करें, लाइन और
  कॉलम चार्ट को संयोजित करें, डेटा सीरीज़ जोड़ें, और एक ही ट्यूटोरियल में वर्कबुक
  को XLSX के रूप में सहेजें।
og_image_alt: Developer guide showing combined line‑column chart export to PNG using
  Aspose.Cells for Java
og_title: संयुक्त चार्ट के लिए चार्ट को PNG में निर्यात करें और डेटा सीरीज़ जोड़ें
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  headline: Export chart to PNG and add data series for combined chart
  type: TechArticle
- description: Learn how to export chart to PNG, add data series, combine line column
    chart, save workbook as XLSX and add legend chart using Aspose.Cells for Java.
  name: Export chart to PNG and add data series for combined chart
  steps:
  - name: import aspose.cells classes
    text: '`Workbook` is Aspose.Cells’ core object that represents an entire Excel
      file in memory.'
  - name: create a new workbook
    text: '`Worksheet` represents a single sheet inside a `Workbook` and provides
      access to cells, rows, and charts.'
  - name: access the first worksheet
    text: '`Chart` is the object that holds all chart‑related settings, series, and
      rendering options.'
  - name: add a combined chart object to the worksheet
    text: We’ll start with a line chart and later add a column series to achieve a
      **combined line column chart** effect.
  - name: define the data ranges and add data series
    text: '`NSeries` is the collection that stores each data series for a chart. Adding
      a series links a range of cells to the chart. > **Pro tip:** The first parameter
      (`"A1:A5"`) is the range for the first series, and the second (`"B1:B5"`) creates
      a second series that will be combined with the first.'
  - name: set the category (X‑axis) data
    text: '`CategoryAxis` represents the horizontal axis of the chart, controlling
      the labels displayed along the X‑axis.'
  - name: set chart axis labels and title
    text: '`Title` sets the main title of the chart, and `Axis` objects represent
      the X and Y axes.'
  - name: add legend chart and adjust its position
    text: '`Legend` controls the placement and appearance of the series legend in
      the chart.'
  - name: save the workbook as an Excel file (XLSX)
    text: '`Workbook.save` writes the in‑memory workbook to a file in the specified
      format.'
  - name: export chart to PNG
    text: '`Chart.toImage` renders the chart as an image file in the chosen format.
      > The `chart.toImage` method **generates Excel chart** images that can be used
      in web pages, reports, or emails.'
  type: HowTo
- questions:
  - answer: 'Download the JAR from the official site and add it to your project’s
      classpath. The download link is: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/).'
    question: How do I install Aspose.Cells for Java?
  - answer: Yes, Aspose.Cells supports bar, pie, scatter, area, and many more chart
      types. Refer to the API documentation for the full list.
    question: Can I create other chart types besides line and column?
  - answer: A valid Aspose.Cells license is required for production deployments. A
      free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Use `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (or similar)
      after adding the series.
    question: How can I change the colors of each series?
  - answer: 'Comprehensive documentation and additional samples are available at the
      Aspose reference site: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/).'
    question: Where can I find more code examples?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- export chart to png
- Aspose.Cells
- Java Excel charts
title: संयुक्त चार्ट के लिए चार्ट को PNG में निर्यात करें और डेटा सीरीज़ जोड़ें
url: /hi/java/advanced-excel-charts/combined-chart-types/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# चार्ट को PNG में निर्यात करें और संयुक्त चार्ट के लिए डेटा सीरीज़ जोड़ें

इस ट्यूटोरियल में आप **डेटा सीरीज़** को एक Excel वर्कबुक में जोड़ेंगे, **लाइन और कॉलम चार्ट** तत्वों को मिलाएंगे, और Aspose.Cells for Java का उपयोग करके **चार्ट को PNG में निर्यात** करना सीखेंगे। हम हर कदम से गुजरेंगे—वर्कबुक सेटअप करना, वर्कशीट में चार्ट जोड़ना, लेजेंड को कस्टमाइज़ करना, **वर्कबुक को XLSX के रूप में सहेजना** और चार्ट की PNG छवि बनाना। अंत में आपके पास एक तैयार‑उपयोगीय संयुक्त चार्ट होगा जिसे आप रिपोर्ट या डैशबोर्ड में एम्बेड कर सकते हैं।

## त्वरित उत्तर
- **कौन सी लाइब्रेरी संयुक्त चार्ट बनाती है?** Aspose.Cells for Java।  
- **डेटा सीरीज़ कैसे जोड़ें?** उपयुक्त रेंज के साथ `chart.getNSeries().add(...)` कॉल करें।  
- **चार्ट को PNG में कैसे निर्यात करें?** `chart.toImage("chart.png", ImageFormat.getPng())` का उपयोग करें।  
- **वर्कबुक को किस फ़ाइल फ़ॉर्मेट में सहेजा जा सकता है?** मानक `.xlsx` (वर्कबुक को XLSX के रूप में सहेजें)।  
- **उत्पादन के लिए लाइसेंस की आवश्यकता है?** हाँ – उत्पादन परिनियोजन के लिए एक वैध Aspose.Cells लाइसेंस आवश्यक है।

## Aspose.Cells में चार्ट को PNG में निर्यात करना क्या है?
चार्ट को PNG में निर्यात करने से Excel चार्ट की एक रास्टर छवि बनती है जिसे वेब पेज, रिपोर्ट या ईमेल में Excel एप्लिकेशन की आवश्यकता के बिना प्रदर्शित किया जा सकता है। यह विधि सटीक दृश्य लेआउट, रंग और डेटा मार्कर को कैप्चर करती है, जिससे एक पोर्टेबल इमेज फ़ाइल बनती है।

## संयुक्त लाइन‑कॉलम चार्ट क्यों बनाएं?
एक संयुक्त लाइन‑कॉलम चार्ट आपको विभिन्न डेटा सेटों को अलग-अलग दृश्य प्रतिनिधित्व (जैसे, कॉलम सीरीज़ के ऊपर एक लाइन सीरीज़) के साथ एक ही दृश्य में प्रदर्शित करने देता है। यह दृष्टिकोण कुल के मुकाबले रुझानों की तुलना, सहसंबंधों को उजागर करने, या छोटे दृश्य फुटप्रिंट के साथ अधिक समृद्ध अंतर्दृष्टि प्रदान करने के लिए आदर्श है।

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) 8 या उससे ऊपर  
- Aspose.Cells for Java लाइब्रेरी (नीचे दिए लिंक से डाउनलोड करें)  
- Java सिंटैक्स और Excel अवधारणाओं की बुनियादी परिचितता  

## शुरू करना

पहले, आधिकारिक साइट से Aspose.Cells for Java लाइब्रेरी डाउनलोड करें:

[Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)

एक बार JAR को अपने प्रोजेक्ट की क्लासपाथ में जोड़ने के बाद, आप चार्ट बनाना शुरू कर सकते हैं।

### चरण 1: aspose.cells क्लासेस आयात करें
`Workbook` Aspose.Cells का कोर ऑब्जेक्ट है जो मेमोरी में संपूर्ण Excel फ़ाइल का प्रतिनिधित्व करता है।  
```java
import com.aspose.cells.*;
```

### चरण 2: एक नया वर्कबुक बनाएं
`Worksheet` एक `Workbook` के भीतर एकल शीट का प्रतिनिधित्व करता है और सेल्स, पंक्तियों और चार्ट्स तक पहुँच प्रदान करता है।  
```java
Workbook workbook = new Workbook();
```

### चरण 3: पहली वर्कशीट तक पहुँचें
`Chart` वह ऑब्जेक्ट है जो सभी चार्ट‑संबंधित सेटिंग्स, सीरीज़ और रेंडरिंग विकल्प रखता है।  
```java
Worksheet worksheet = workbook.getWorksheets().get(0);
```

### चरण 4: वर्कशीट में एक संयुक्त चार्ट ऑब्जेक्ट जोड़ें  
हम पहले एक लाइन चार्ट बनाएँगे और बाद में एक कॉलम सीरीज़ जोड़कर **संयुक्त लाइन कॉलम चार्ट** प्रभाव प्राप्त करेंगे।  
```java
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 0, 0, 20, 10);
Chart chart = worksheet.getCharts().get(chartIndex);
```

## चार्ट में डेटा जोड़ना

अब जबकि चार्ट कंटेनर मौजूद है, हमें इसे डेटा से भरना है।

### चरण 5: डेटा रेंज निर्धारित करें और डेटा सीरीज़ जोड़ें
`NSeries` वह संग्रह है जो चार्ट के प्रत्येक डेटा सीरीज़ को संग्रहीत करता है। एक सीरीज़ जोड़ने से सेल रेंज को चार्ट से लिंक किया जाता है।  
```java
Cells cells = worksheet.getCells();
chart.getNSeries().add("A1:A5", true);
chart.getNSeries().add("B1:B5", true);
```
> **प्रो टिप:** पहला पैरामीटर (`"A1:A5"`) पहली सीरीज़ की रेंज है, और दूसरा (`"B1:B5"`) एक दूसरी सीरीज़ बनाता है जिसे पहली के साथ मिलाया जाएगा।

### चरण 6: श्रेणी (X‑axis) डेटा सेट करें
`CategoryAxis` चार्ट के क्षैतिज अक्ष का प्रतिनिधित्व करता है, जो X‑axis पर प्रदर्शित लेबल को नियंत्रित करता है।  
```java
chart.getNSeries().setCategoryData("C1:C5");
```

## चार्ट को अनुकूलित करना

एक अच्छा चार्ट कहानी बताता है। चलिए इसे शीर्षक, अक्ष लेबल और स्पष्ट लेजेंड देते हैं।

### चरण 7: चार्ट अक्ष लेबल और शीर्षक सेट करें
`Title` चार्ट का मुख्य शीर्षक सेट करता है, और `Axis` ऑब्जेक्ट्स X और Y अक्षों का प्रतिनिधित्व करते हैं।  
```java
chart.getTitle().setText("Combined Chart Example");
chart.getCategoryAxis().getTitle().setText("Categories");
chart.getValueAxis().getTitle().setText("Values");
```

### चरण 8: लेजेंड जोड़ें और उसकी स्थिति समायोजित करें
`Legend` चार्ट में सीरीज़ लेजेंड की स्थिति और स्वरूप को नियंत्रित करता है।  
```java
chart.getLegend().setPosition(LegendPositionType.BOTTOM);
chart.getLegend().setOverlay(true);
```

## चार्ट को सहेजना और निर्यात करना

कस्टमाइज़ करने के बाद, आप **वर्कबुक को XLSX के रूप में सहेजना** और साथ ही एक इमेज बनाना चाहेंगे।

### चरण 9: वर्कबुक को Excel फ़ाइल (XLSX) के रूप में सहेजें
`Workbook.save` मेमोरी में मौजूद वर्कबुक को निर्दिष्ट फ़ॉर्मेट में फ़ाइल में लिखता है।  
```java
workbook.save("CombinedChart.xlsx");
```

### चरण 10: चार्ट को PNG में निर्यात करें
`Chart.toImage` चयनित फ़ॉर्मेट में चार्ट को इमेज फ़ाइल के रूप में रेंडर करता है।  
```java
chart.toImage("CombinedChart.png", ImageFormat.getPng());
```
> `chart.toImage` मेथड **Excel चार्ट** इमेज बनाता है जिसे वेब पेज, रिपोर्ट या ईमेल में उपयोग किया जा सकता है।

## सामान्य समस्याएँ और समस्या निवारण

| समस्या | समाधान |
|-------|----------|
| **कोई डेटा नहीं दिख रहा** | सुनिश्चित करें कि सेल रेंज (`A1:A5`, `B1:B5`, `C1:C5`) में वास्तव में डेटा मौजूद है, फिर चार्ट बनाएं। |
| **लेजेंड चार्ट के ऊपर ओवरलैप हो रहा है** | `chart.getLegend().setOverlay(false)` सेट करें या लेजेंड को किसी अन्य स्थिति (जैसे, `RIGHT`) पर ले जाएँ। |
| **इमेज फ़ाइल खाली है** | यह सुनिश्चित करें कि चार्ट में कम से कम एक सीरीज़ हो और सभी कस्टमाइज़ेशन के बाद `chart.toImage` कॉल किया गया हो। |
| **सेव करते समय अपवाद फेंका जा रहा है** | लक्ष्य डायरेक्टरी में लिखने की अनुमति जांचें और सुनिश्चित करें कि फ़ाइल Excel में खुली नहीं है। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: Aspose.Cells for Java कैसे स्थापित करें?**  
उत्तर: आधिकारिक साइट से JAR डाउनलोड करें और उसे अपने प्रोजेक्ट की क्लासपाथ में जोड़ें। डाउनलोड लिंक है: [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)।

**प्रश्न: क्या मैं लाइन और कॉलम के अलावा अन्य चार्ट प्रकार बना सकता हूँ?**  
उत्तर: हाँ, Aspose.Cells बार, पाई, स्कैटर, एरिया और कई अन्य चार्ट प्रकारों का समर्थन करता है। पूर्ण सूची के लिए API दस्तावेज़ देखें।

**प्रश्न: उत्पादन उपयोग के लिए लाइसेंस आवश्यक है?**  
उत्तर: उत्पादन परिनियोजन के लिए एक वैध Aspose.Cells लाइसेंस आवश्यक है। मूल्यांकन के लिए एक मुफ्त ट्रायल उपलब्ध है।

**प्रश्न: प्रत्येक सीरीज़ के रंग कैसे बदलें?**  
उत्तर: सीरीज़ जोड़ने के बाद `chart.getNSeries().get(i).setAreaColor(Color.getRed())` (या समान) का उपयोग करें।

**प्रश्न: अधिक कोड उदाहरण कहाँ मिल सकते हैं?**  
उत्तर: व्यापक दस्तावेज़ीकरण और अतिरिक्त नमूने Aspose रेफ़रेंस साइट पर उपलब्ध हैं: [Aspose Cells Java reference documentation](https://reference.aspose.com/cells/java/)।

---

**अंतिम अपडेट:** 2026-09-02  
**परीक्षण किया गया:** Aspose.Cells for Java नवीनतम संस्करण  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [How to Add Labels to Excel Charts Using Aspose.Cells for Java](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel Charts to PDF Using Aspose.Cells for Java: Custom Page Sizes Guide](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}