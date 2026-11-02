---
date: 2026-09-02
description: जानेँ कि Java में Aspose.Cells के साथ एक्सेल वॉटरफ़ॉल चार्ट कैसे बनाएं,
  चार्ट डेटा रेंज सेट करें, लेबल कस्टमाइज़ करें और XLSX में एक्सपोर्ट करें।
keywords:
- create excel waterfall chart
- waterfall chart data labels
- Aspose.Cells Java chart
lastmod: 2026-09-02
linktitle: वॉटरफ़ॉल चार्ट्स
og_description: Aspose.Cells for Java का उपयोग करके एक्सेल वॉटरफ़ॉल चार्ट बनाएं –
  चार्ट डेटा रेंज सेट करें, डेटा लेबल जोड़ें, और कुछ ही चरणों में XLSX में एक्सपोर्ट
  करें।
og_image_alt: 'Tutorial: create excel waterfall chart with Aspose.Cells Java'
og_title: Aspose.Cells for Java के साथ एक्सेल वॉटरफ़ॉल चार्ट बनाएं
schemas:
- author: Aspose
  dateModified: '2026-09-02'
  description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  headline: Create excel waterfall chart with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create excel waterfall chart in Java with Aspose.Cells,
    set the chart data range, customize labels and export to XLSX.
  name: Create excel waterfall chart with Aspose.Cells for Java
  steps:
  - name: import Aspose.Cells
    text: The `com.aspose.cells` package contains all classes required for Excel manipulation,
      including workbook creation, worksheet handling, and chart generation.
  - name: initialize workbook and worksheet
    text: A **Workbook** represents an Excel file, and a **Worksheet** is a single
      sheet within that file. Creating these objects provides the canvas for both
      raw data and the chart.
  - name: enter data
    text: Column A holds category labels, while column B contains the numeric values
      for the waterfall. This layout matches the typical profit‑and‑loss flow used
      in financial analysis.
  - name: create the waterfall chart
    text: The **Chart** object creates a visual representation; setting its type to
      `ChartType.WATERFALL` configures it as a waterfall chart. Use the `add` method
      to set the chart data range for the series (`"B2:B6"`), and link the category
      axis to `"A2:A6"`.
  - name: save the workbook
    text: Saving the workbook writes the chart and data to the specified file format.
      Call `workbook.save("WaterfallChart.xlsx")` to generate an XLSX file, or change
      the format parameter to export to PDF, CSV, or HTML.
  type: HowTo
- questions:
  - answer: Use the `add` method on the chart’s series, passing the cell range that
      contains your values, e.g., `"B2:B6"`.
    question: How do I set the chart data range for a financial waterfall chart?
  - answer: Yes, call `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` to generate
      a PDF version.
    question: Can I export the workbook to PDF instead of XLSX?
  - answer: Extend the data range in both the values column and the category column,
      then update the `add` and `setCategoryData` calls accordingly.
    question: What if I need to create a waterfall chart with more categories?
  - answer: Iterate through the `Series` collection and set the `FillFormat` color
      based on each value’s sign; Aspose.Cells lets you apply conditional formatting
      programmatically.
    question: Is there a way to automatically format positive and negative bars?
  - answer: Yes. After modifying cell values, simply re‑save the workbook—the chart
      will reflect the new data automatically.
    question: Does Aspose.Cells support dynamic data updates for charts?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- waterfall chart
- Aspose.Cells
- java excel charts
- excel automation
title: Aspose.Cells for Java के साथ एक्सेल वॉटरफ़ॉल चार्ट बनाएं
url: /hi/java/advanced-excel-charts/waterfall-charts/
weight: 18
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# वॉटरफ़ॉल चार्ट

## Aspose.Cells for Java का उपयोग करके वॉटरफ़ॉल चार्ट का परिचय

इस ट्यूटोरियल में आप सीखेंगे कि Aspose.Cells for Java के साथ **create excel waterfall chart** और **set chart data range** कैसे बनाएं। वॉटरफ़ॉल चार्ट सकारात्मक और नकारात्मक संख्याओं की श्रृंखला को एक स्पष्ट दृश्य कहानी में बदलते हैं, जिससे वे वित्तीय विवरणों, बिक्री प्रदर्शन समीक्षाओं, और किसी भी स्थिति में आदर्श होते हैं जहाँ आपको देखना हो कि व्यक्तिगत आइटम कुल में कैसे योगदान देते हैं।

## त्वरित उत्तर
- **What is a waterfall chart?** एक दृश्य जो दिखाता है कि प्रारंभिक मान को मध्यवर्ती मानों की श्रृंखला द्वारा कैसे बढ़ाया और घटाया जाता है, अंत में अंतिम कुल के साथ।  
- **Which library is used?** Aspose.Cells for Java.  
- **Do I need a license?** विकास के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **Can I save the file as XLSX?** हाँ – `workbook.save("FileName.xlsx")` का उपयोग करें।  
- **Is it suitable for Java data visualization?** बिल्कुल; Aspose.Cells बिना Office स्थापित किए समृद्ध चार्टिंग सुविधाएँ प्रदान करता है।

## वॉटरफ़ॉल चार्ट क्या है?
वॉटरफ़ॉल चार्ट प्रारंभिक मान में क्रमिक सकारात्मक और नकारात्मक योगदान को प्रदर्शित करता है, जिससे आप समझ सकते हैं कि प्रत्येक घटक समग्र परिणाम को कैसे प्रभावित करता है। लाभ और हानि को साथ‑साथ दृश्य रूप में दिखाकर, यह जटिल वित्तीय प्रवाह को तुरंत पढ़ने योग्य बनाता है।

## वॉटरफ़ॉल चार्ट जोड़ने के लिए Aspose.Cells for Java का उपयोग क्यों करें?
Aspose.Cells आपको किसी भी सर्वर, CI पाइपलाइन, या डेस्कटॉप पर Microsoft Excel की आवश्यकता के बिना Excel चार्ट बनाने देता है। यह **15+ आउटपुट फ़ॉर्मेट** (XLSX, PDF, HTML, CSV, आदि) का समर्थन करता है, **500+ पंक्तियों** वाले वर्कबुक को एक सेकंड से कम समय में प्रोसेस करता है, और प्रत्येक चार्ट तत्व पर प्रोग्रामेटिक नियंत्रण प्रदान करता है—रंगों से लेकर डेटा लेबल तक।

## पूर्वापेक्षाएँ

कोड में डुबकी लगाने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ मौजूद हैं:

- Aspose.Cells for Java: आपको Aspose.Cells for Java स्थापित होना चाहिए। आप इसे Aspose.Cells for Java रिलीज़ पेज से डाउनलोड कर सकते हैं: [Aspose.Cells for Java releases](https://releases.aspose.com/cells/java/).
- Java विकास पर्यावरण: सुनिश्चित करें कि आपके सिस्टम पर Java स्थापित है और एक बिल्ड टूल (Maven/Gradle) तैयार है।

अब, चलिए चरण-दर-चरण वॉटरफ़ॉल चार्ट बनाना शुरू करते हैं।

## Java में वॉटरफ़ॉल चार्ट के लिए चार्ट डेटा रेंज कैसे सेट करें
एक नया वर्कबुक लोड करें, उसे डेटा से भरें, एक `Chart` ऑब्जेक्ट जोड़ें, सीरीज़ रेंज निर्धारित करें, और अंत में फ़ाइल सहेजें। यह प्रक्रिया सीधी है: आप एक वर्कबुक बनाते हैं, श्रेणियों और मानों के साथ सेल भरते हैं, एक चार्ट बनाते हैं, डेटा रेंज को बाइंड करते हैं, और फिर वर्कबुक को निर्यात करते हैं। परिणाम एक पूर्ण कार्यात्मक वॉटरफ़ॉल चार्ट है जो रिपोर्ट या डैशबोर्ड में उपयोग के लिए तैयार है।

### चरण 1: Aspose.Cells आयात करें
`com.aspose.cells` पैकेज में Excel हेरफेर के लिए आवश्यक सभी क्लासेस शामिल हैं, जिसमें वर्कबुक निर्माण, वर्कशीट हैंडलिंग, और चार्ट जनरेशन शामिल है।

### चरण 2: वर्कबुक और वर्कशीट को प्रारंभ करें
एक **Workbook** Excel फ़ाइल का प्रतिनिधित्व करता है, और एक **Worksheet** उस फ़ाइल के भीतर एकल शीट है। इन ऑब्जेक्ट्स को बनाना कच्चे डेटा और चार्ट दोनों के लिए कैनवास प्रदान करता है।

### चरण 3: डेटा दर्ज करें
कॉलम A में श्रेणी लेबल होते हैं, जबकि कॉलम B में वॉटरफ़ॉल के लिए संख्यात्मक मान होते हैं। यह लेआउट वित्तीय विश्लेषण में उपयोग किए जाने वाले सामान्य लाभ‑और‑हानि प्रवाह से मेल खाता है।

### चरण 4: वॉटरफ़ॉल चार्ट बनाएं
**Chart** ऑब्जेक्ट एक दृश्य प्रतिनिधित्व बनाता है; इसका प्रकार `ChartType.WATERFALL` सेट करने से यह वॉटरफ़ॉल चार्ट बन जाता है। सीरीज़ के लिए चार्ट डेटा रेंज सेट करने हेतु `add` मेथड का उपयोग करें (`"B2:B6"`), और श्रेणी अक्ष को `"A2:A6"` से लिंक करें।

### चरण 5: वर्कबुक सहेजें
वर्कबुक को सहेजने से चार्ट और डेटा निर्दिष्ट फ़ाइल फ़ॉर्मेट में लिखे जाते हैं। `workbook.save("WaterfallChart.xlsx")` को कॉल करके एक XLSX फ़ाइल बनाएं, या फ़ॉर्मेट पैरामीटर बदलकर PDF, CSV, या HTML में निर्यात करें।

## सामान्य समस्याएँ और समाधान
- **Chart appears blank** – सुनिश्चित करें कि डेटा रेंज रेफ़रेंसेज़ (`B2:B6` और `A2:A6`) आपके मानों और श्रेणियों वाले वास्तविक सेल्स से मेल खाते हैं।  
- **Negative values not displayed correctly** – सुनिश्चित करें कि सीरीज़ प्रकार `ChartType.WATERFALL` पर सेट है; अन्य चार्ट प्रकार नकारात्मक मानों को अलग तरीके से दिखाते हैं।  
- **File not opening in Excel** – नवीनतम Aspose.Cells रिलीज़ का उपयोग करें और पुष्टि करें कि फ़ाइल एक्सटेंशन फ़ॉर्मेट से मेल खाता है (`.xlsx` Excel के लिए)।

## अक्सर पूछे जाने वाले प्रश्न

### मैं अपने वॉटरफ़ॉल चार्ट की उपस्थिति को कैसे अनुकूलित कर सकता हूँ?
आप `Chart.getSeries().get(0).getFillFormat().setColor(Color.getRed())` जैसी प्रॉपर्टीज़ को बदलकर बार के रंग बदल सकते हैं, `setShowDataLabels(true)` के साथ डेटा लेबल सक्षम कर सकते हैं, और `getCategoryAxis().setTitle("Stage")` के माध्यम से अक्ष शीर्षक समायोजित कर सकते हैं। Aspose.Cells API रेफ़रेंस अनुकूलन योग्य विकल्पों की पूरी सूची प्रदान करता है।

### क्या मैं उसी वर्कशीट में कई वॉटरफ़ॉल चार्ट बना सकता हूँ?
हाँ। पहला चार्ट जोड़ने के बाद, अलग डेटा रेंज और एक नया `Chart` ऑब्जेक्ट के साथ चार्ट‑निर्माण चरणों को दोहराएँ। प्रत्येक चार्ट स्वतंत्र होता है और शीट पर कहीं भी स्थित किया जा सकता है।

### क्या Aspose.Cells विभिन्न Java विकास पर्यावरणों के साथ संगत है?
बिल्कुल। लाइब्रेरी Eclipse, IntelliJ IDEA, NetBeans, और किसी भी बिल्ड सिस्टम के साथ काम करती है जो Maven या Gradle का समर्थन करता है। अतिरिक्त प्लगइन्स की आवश्यकता नहीं है।

### क्या मैं अपने वॉटरफ़ॉल चार्ट में अतिरिक्त डेटा सीरीज़ जोड़ सकता हूँ?
आप `chart.getNSeries().add("C2:C6", true)` को कॉल करके और प्रत्येक सीरीज़ को अलग से कॉन्फ़िगर करके अधिक सीरीज़ जोड़ सकते हैं। यह आपको कई परिदृश्यों की तुलना साइड‑बाय‑साइड करने देता है।

### Aspose.Cells for Java के लिए अधिक संसाधन और उदाहरण मैं कहाँ पा सकता हूँ?
पूरा दस्तावेज़ Aspose.Cells Java API रेफ़रेंस पर देखें: [Aspose.Cells Java API reference](https://reference.aspose.com/cells/java/).

## FAQ

**Q: वित्तीय वॉटरफ़ॉल चार्ट के लिए चार्ट डेटा रेंज कैसे सेट करें?**  
A: चार्ट की सीरीज़ पर `add` मेथड का उपयोग करें, जिसमें आपके मानों वाली सेल रेंज पास करें, उदाहरण के लिए, "B2:B6"।

**Q: क्या मैं वर्कबुक को XLSX के बजाय PDF में निर्यात कर सकता हूँ?**  
A: हाँ, `workbook.save("WaterfallChart.pdf", SaveFormat.PDF);` को कॉल करके PDF संस्करण बनाएं।

**Q: यदि मुझे अधिक श्रेणियों के साथ वॉटरफ़ॉल चार्ट बनाना हो तो क्या करें?**  
A: मान कॉलम और श्रेणी कॉलम दोनों में डेटा रेंज को विस्तारित करें, फिर `add` और `setCategoryData` कॉल्स को उसी अनुसार अपडेट करें।

**Q: क्या सकारात्मक और नकारात्मक बार को स्वचालित रूप से फॉर्मेट करने का कोई तरीका है?**  
A: `Series` कलेक्शन पर इटररेट करें और प्रत्येक मान के संकेत के आधार पर `FillFormat` रंग सेट करें; Aspose.Cells आपको प्रोग्रामेटिक रूप से कंडीशनल फॉर्मेटिंग लागू करने देता है।

**Q: क्या Aspose.Cells चार्ट्स के लिए डायनेमिक डेटा अपडेट का समर्थन करता है?**  
A: हाँ। सेल मानों को संशोधित करने के बाद, बस वर्कबुक को फिर से सहेजें—चार्ट स्वचालित रूप से नए डेटा को दर्शाएगा।

---

**अंतिम अपडेट:** 2026-09-02  
**परीक्षण किया गया:** Aspose.Cells for Java (latest)  
**लेखक:** Aspose  









```java
import com.aspose.cells.*;
```

```java
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
```

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

```java
int chartIndex = worksheet.getCharts().add(ChartType.WATERFALL, 5, 0, 15, 5);
Chart waterfallChart = worksheet.getCharts().get(chartIndex);
waterfallChart.getNSeries().add("B2:B6", true);
waterfallChart.getNSeries().setCategoryData("A2:A6");
```

```java
workbook.save("WaterfallChart.xlsx");
```

## संबंधित ट्यूटोरियल

- [Aspose.Cells for Java का उपयोग करके Excel चार्ट डेटा लेबल को कस्टमाइज़ करें: चरण-दर-चरण गाइड](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Aspose.Cells Java के साथ Excel चार्ट में डेटा लेबल जोड़ें](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Aspose.Cells का उपयोग करके Java में चार्ट बनाना और निर्यात करना: एक पूर्ण गाइड](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}