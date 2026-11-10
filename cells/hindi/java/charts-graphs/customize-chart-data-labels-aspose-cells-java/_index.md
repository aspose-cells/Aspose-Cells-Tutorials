---
date: '2026-10-17'
description: Aspose.Cells का उपयोग करके Java में Excel चार्ट डेटा लेबल्स का आकार कैसे
  सेट करें, सीखें। यह गाइड आपको Excel चार्ट लेबल्स को तेज़ी और प्रभावी ढंग से संशोधित
  करने का तरीका दिखाता है।
keywords:
- how to set shape
- modify excel chart labels
- customize chart data labels
- add data label shape
lastmod: '2026-10-17'
og_description: Aspose.Cells का उपयोग करके Java में Excel चार्ट डेटा लेबल्स का आकार
  कैसे सेट करें, सीखें। यह चरण‑दर‑चरण गाइड आपको Excel चार्ट लेबल्स को जल्दी संशोधित
  करने में मदद करता है।
og_image_alt: Guide showing how to set shape of Excel chart data labels using Aspose.Cells
  for Java
og_title: Java में Excel चार्ट डेटा लेबल्स का आकार कैसे सेट करें
schemas:
- author: Aspose
  dateModified: '2026-10-17'
  description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  headline: How to set shape of Excel chart data labels in Java
  type: TechArticle
- description: Learn how to set shape of Excel chart data labels in Java using Aspose.Cells.
    This guide shows you how to modify Excel chart labels quickly and efficiently.
  name: How to set shape of Excel chart data labels in Java
  steps:
  - name: load your workbook
    text: The `Workbook` class is Aspose.Cells' top‑level object that represents a
      single Excel file in memory. Use `new Workbook("input.xlsx")` to load the file
      you want to modify.
  - name: access the chart
    text: '`Worksheet` represents a single sheet within a workbook. `Worksheet ws
      = workbook.getWorksheets().get(0);` retrieves the first worksheet. `Chart` is
      an object that represents a chart embedded in a worksheet. `Chart chart = ws.getCharts().get(0);`
      obtains the first chart on that sheet.'
  - name: retrieve series and modify data labels
    text: '`Series` represents a data series plotted on a chart. Each `Series` object
      contains a `DataLabel` collection. `DataLabel` controls the appearance of a
      data label for a series. `DataLabelShapeType` is an enumeration of possible
      shapes for data labels. Call `series.getDataLabels().setShapeType(DataLab'
  - name: save your workbook
    text: After applying the shape, invoke `workbook.save("output.xlsx");` to write
      the changes back to disk.
  type: HowTo
- questions:
  - answer: Loop through each series in the chart and call `setShapeType` on the series’
      `DataLabel` object.
    question: How do I change the shape of multiple data labels at once?
  - answer: Yes. With proper memory management, it processes workbooks containing
      hundreds of thousands of rows without loading the entire file into memory.
    question: Can Aspose.Cells for Java handle large Excel files efficiently?
  - answer: Missing Maven dependencies, using an outdated library version, or providing
      an invalid license file are typical pitfalls.
    question: What are common issues when setting up Aspose.Cells?
  - answer: Set the shape type to `DataLabelShapeType.DEFAULT` to restore the original
      appearance.
    question: Is there a way to revert data label shapes to default?
  - answer: Iterate over `ws.getCharts()` and apply the same `setShapeType` logic
      to each chart’s series collection.
    question: How can I apply this customization to multiple charts in a workbook?
  type: FAQPage
tags:
- excel chart
- aspose.cells
- java chart customization
- data label shape
title: Java में Excel चार्ट डेटा लेबल्स का आकार कैसे सेट करें
url: /hi/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में Aspose.Cells के साथ चार्ट कस्टमाइज़ेशन में महारत: डेटा लेबल शैप्स को संशोधित करें

## परिचय

रिपोर्ट या डैशबोर्ड तैयार करते समय Excel चार्ट की दृश्य आकर्षण को बढ़ाना अत्यंत महत्वपूर्ण है, विशेष रूप से जब आप जावा का उपयोग कर रहे हों। Aspose.Cells—स्प्रेडशीट प्रबंधन और हेरफेर के लिए एक शक्तिशाली लाइब्रेरी—के साथ आप कुछ ही कोड लाइनों में चार्ट डेटा लेबल **how to set shape** कर सकते हैं। यह ट्यूटोरियल आपको Aspose.Cells for Java का उपयोग करके Excel चार्ट में डेटा लेबल के आकार को बदलने की प्रक्रिया दिखाएगा। अंत तक, आप जानेंगे कैसे:

- चार्ट डेटा लेबल तक पहुंचें और उन्हें संशोधित करें
- डेटा लेबल के लिए कस्टम शैप सेट करें
- अपनी वर्कबुक में बदलाव सहेजें

## त्वरित उत्तर
- **Excel फ़ाइलों के साथ काम करने के लिए मुख्य क्लास कौन सी है?** `Workbook` मेमोरी में पूरी Excel फ़ाइल का प्रतिनिधित्व करता है।  
- **लेबल शैप सेट करने वाला मेथड कौन सा है?** `setShapeType(DataLabelShapeType shape)` `DataLabel` ऑब्जेक्ट पर।  
- **क्या विकास के लिए लाइसेंस की आवश्यकता है?** मूल्यांकन के लिए एक मुफ्त अस्थायी लाइसेंस काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या मैं शैप को कई सीरीज़ पर लागू कर सकता हूँ?** हाँ—प्रत्येक सीरीज़ पर इटरेट करके `setShapeType` कॉल करें।  
- **क्या यह तरीका बड़े वर्कबुक्स के साथ संगत है?** Aspose.Cells कई‑सौ‑पृष्ठ वाले वर्कबुक को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस करता है।

## 'how to set shape' क्या है?
वाक्यांश **how to set shape** का अर्थ है चार्ट के डेटा लेबल की दृश्य रूपरेखा को कॉन्फ़िगर करना, जैसे साधारण आयत को कॉलआउट या एलिप्स में बदलना। शैप बदलने से पठनीयता बढ़ती है और प्रमुख डेटा पॉइंट्स उजागर होते हैं। उपयुक्त शैप चुनकर आप लेबल को प्रमुख बना सकते हैं, संबंधित पॉइंट्स को समूहित कर सकते हैं, या कॉर्पोरेट ब्रांडिंग दिशानिर्देशों के साथ मेल करा सकते हैं, जिससे चार्ट की समग्र पठनीयता में सुधार होता है।

## चार्ट लेबल कस्टमाइज़ेशन के लिए Aspose.Cells क्यों उपयोग करें?
Aspose.Cells **50+ इनपुट और आउटपुट फ़ॉर्मेट**—जैसे XLSX, CSV, ODS, और PDF—को सपोर्ट करता है और **1 मिलियन पंक्तियों** तक वाली वर्कबुक को मेमोरी समाप्त किए बिना हेरफेर कर सकता है। इसका API आपको प्रोग्रामेटिक रूप से चार्ट को संशोधित करने की अनुमति देता है, जिससे मैन्युअल Excel संपादन की आवश्यकता नहीं रहती और स्वचालित रिपोर्टों में शैली में निरंतरता बनी रहती है।

## पूर्वापेक्षाएँ

- **Aspose.Cells for Java लाइब्रेरी**: संस्करण 25.3 या बाद का आवश्यक है।  
- **Java विकास वातावरण**: आपके मशीन पर JDK स्थापित होना चाहिए।  
- **IDE सेटअप**: कोड लिखने और चलाने के लिए IntelliJ IDEA या Eclipse जैसे IDE का उपयोग करें।

### आवश्यक लाइब्रेरीज़ और निर्भरताएँ

Maven उपयोगकर्ताओं के लिए, अपने `pom.xml` में निम्नलिखित निर्भरता शामिल करें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Gradle उपयोगकर्ता इसे अपने `build.gradle` फ़ाइल में जोड़ें:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### लाइसेंस प्राप्ति

Aspose.Cells एक मुफ्त ट्रायल लाइसेंस प्रदान करता है, जिसे आप [Aspose temporary license page](https://purchase.aspose.com/temporary-license/) से प्राप्त कर सकते हैं। यह सीमित समय के लिए सभी सुविधाओं तक पूर्ण पहुंच देता है।

## जावा के लिए Aspose.Cells सेटअप करना

एक बार आपका वातावरण तैयार हो जाने पर, चलिए Aspose.Cells सेटअप करते हैं। शुरू करने का तरीका यहाँ है:

### इंस्टॉलेशन चरण

1. **लाइब्रेरी डाउनलोड करें**: ऊपर दिखाए अनुसार Maven या Gradle का उपयोग करें।  
2. **लाइसेंस कॉन्फ़िगरेशन**:  
   - `License` एक क्लास है जो आपके Aspose.Cells लाइसेंस फ़ाइल को लागू करके पूर्ण कार्यक्षमता सक्षम करता है।  
   - `Workbook` ऑब्जेक्ट को इनिशियलाइज़ करने के बाद इस कोड स्निपेट का उपयोग करके अस्थायी लाइसेंस डाउनलोड और लागू करें:

    ```java
    License license = new License();
    license.setLicense("path/to/your/license/file");
    ```
3. **बेसिक इनिशियलाइज़ेशन**: Excel फ़ाइलों के साथ काम शुरू करने के लिए एक `Workbook` इंस्टेंस बनाएं।

## चार्ट में डेटा लेबल के शैप को कैसे सेट करें?

अपनी वर्कबुक लोड करें, लक्ष्य चार्ट खोजें, और उसके डेटा लेबल पर इच्छित शैप लागू करें। नीचे दिए गए सीधे चरण एक मिनट से कम समय में यह कार्य पूरा करेंगे।

### चरण‑दर‑चरण मार्गदर्शन

#### चरण 1: अपनी वर्कबुक लोड करें

`Workbook` क्लास Aspose.Cells की टॉप‑लेवल ऑब्जेक्ट है जो मेमोरी में एकल Excel फ़ाइल का प्रतिनिधित्व करती है। `new Workbook("input.xlsx")` का उपयोग करके वह फ़ाइल लोड करें जिसे आप संशोधित करना चाहते हैं।

#### चरण 2: चार्ट तक पहुंचें

`Worksheet` वर्कबुक के भीतर एकल शीट का प्रतिनिधित्व करता है।  
`Worksheet ws = workbook.getWorksheets().get(0);` पहला वर्कशीट प्राप्त करता है।  
`Chart` वह ऑब्जेक्ट है जो वर्कशीट में एम्बेडेड चार्ट को दर्शाता है।  
`Chart chart = ws.getCharts().get(0);` उस शीट पर पहला चार्ट प्राप्त करता है।

#### चरण 3: सीरीज़ प्राप्त करें और डेटा लेबल संशोधित करें

`Series` चार्ट पर प्लॉट की गई डेटा सीरीज़ को दर्शाता है।  
प्रत्येक `Series` ऑब्जेक्ट में एक `DataLabel` कलेक्शन होता है।  
`DataLabel` सीरीज़ के डेटा लेबल की उपस्थिति को नियंत्रित करता है।  
`DataLabelShapeType` डेटा लेबल के संभावित शैप्स का एनेमरेशन है।  
`series.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);` का उपयोग करके शैप सेट करें। एनेमरेशन में `RECTANGLE`, `CLOUD`, `WEDGE_ELLIPSE_CALLOUT` आदि कई विकल्प उपलब्ध हैं।

#### चरण 4: अपनी वर्कबुक सहेजें

शैप लागू करने के बाद `workbook.save("output.xlsx");` को कॉल करके बदलाव डिस्क पर लिखें।

## समस्या निवारण टिप्स

- **फ़ाइल पाथ समस्याएँ**: सुनिश्चित करें कि फ़ाइल पाथ पूर्ण (absolute) है या आपके प्रोजेक्ट की कार्य निर्देशिका के सापेक्ष सही है।  
- **लाइब्रेरी संस्करण असंगतता**: Aspose.Cells संस्करण 25.3 या बाद का उपयोग करें; पुराने संस्करणों में `setShapeType` मेथड नहीं होता।  
- **असमर्थित चार्ट प्रकार**: कुछ लेगेसी चार्ट प्रकार (जैसे radar) डेटा लेबल शैप प्रॉपर्टी नहीं दिखा सकते; कॉलम या लाइन जैसे समर्थित चार्ट प्रकार पर स्विच करें।

## व्यावहारिक उपयोग

1. **वित्तीय रिपोर्टिंग** – कॉलआउट‑स्टाइल लेबल के साथ प्रमुख लाभ मार्जिन को उजागर करें।  
2. **शैक्षिक सामग्री** – क्लाउड‑शेप्ड लेबल का उपयोग करके शिक्षण सामग्री में महत्वपूर्ण डेटा पॉइंट्स पर ध्यान आकर्षित करें।  
3. **मार्केटिंग एनालिटिक्स** – डैशबोर्ड में अभियान प्रदर्शन मीट्रिक्स को अलग दिखाने के लिए कस्टम शैप लागू करें।

Aspose.Cells को डेटा पाइपलाइन या CRM सिस्टम के साथ एकीकृत करके आप पूरी तरह स्टाइल्ड रिपोर्ट स्वचालित रूप से जनरेट कर सकते हैं, जिससे मैन्युअल प्रयास कम होता है और ब्रांड‑संगत विज़ुअल्स सुनिश्चित होते हैं।

## प्रदर्शन विचार

बड़े Excel फ़ाइलों के साथ काम करते समय:

- **मेमोरी उपयोग को अनुकूलित करें**: सहेजने के बाद `workbook.dispose();` कॉल करके नेटिव रिसोर्सेज़ को तुरंत रिलीज़ करें।  
- **बैच प्रोसेसिंग**: चार्ट को एक‑एक करके प्रोसेस करने के बजाय समूह में प्रोसेस करें ताकि ऑब्जेक्ट निर्माण ओवरहेड कम हो।  
- **कुशल डेटा हैंडलिंग**: हजारों पंक्तियों पर इटररेट करने वाले लूप्स के भीतर भारी गणनाओं से बचें; मानों को पहले से गणना करें।

## निष्कर्ष

आप अब जावा में Aspose.Cells का उपयोग करके Excel चार्ट डेटा लेबल के **how to set shape** को जानते हैं। यह क्षमता न केवल चार्ट की सौंदर्यशास्त्र को बढ़ाती है बल्कि अंतिम‑उपयोगकर्ताओं के लिए डेटा समझ को भी सुधारती है। लेबल रंग, फ़ॉन्ट, और लीडर लाइन्स जैसी अतिरिक्त कस्टमाइज़ेशन विकल्पों का अन्वेषण करें ताकि अपनी विज़ुअलाइज़ेशन को और भी परिष्कृत किया जा सके।

किसी भी प्रश्न या सहायता के लिए, [Aspose support forum](https://forum.aspose.com/c/cells/9) देखें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: कई डेटा लेबल्स का शैप एक साथ कैसे बदलें?**  
उत्तर: चार्ट में प्रत्येक सीरीज़ पर लूप करें और सीरीज़ के `DataLabel` ऑब्जेक्ट पर `setShapeType` कॉल करें।

**प्रश्न: क्या Aspose.Cells for Java बड़े Excel फ़ाइलों को कुशलता से संभाल सकता है?**  
उत्तर: हाँ। उचित मेमोरी प्रबंधन के साथ यह सैकड़ों हज़ार पंक्तियों वाली वर्कबुक को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस करता है।

**प्रश्न: Aspose.Cells सेटअप करते समय आम समस्याएँ क्या हैं?**  
उत्तर: Maven निर्भरताएँ गायब होना, पुराना लाइब्रेरी संस्करण उपयोग करना, या अवैध लाइसेंस फ़ाइल प्रदान करना सामान्य समस्याएँ हैं।

**प्रश्न: डेटा लेबल शैप को डिफ़ॉल्ट पर कैसे रीसेट करें?**  
उत्तर: शैप टाइप को `DataLabelShapeType.DEFAULT` सेट करके मूल रूप पुनर्स्थापित करें।

**प्रश्न: वर्कबुक में कई चार्ट्स पर यह कस्टमाइज़ेशन कैसे लागू करें?**  
उत्तर: `ws.getCharts()` पर इटररेट करें और प्रत्येक चार्ट की सीरीज़ कलेक्शन पर समान `setShapeType` लॉजिक लागू करें।

## संसाधन

- [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- [Download Aspose.Cells for Java](https://releases.aspose.com/cells/java/)  
- [Purchase a License](https://purchase.aspose.com/buy)  
- [Free Trial License](https://releases.aspose.com/cells/java/)  
- [Temporary License](https://purchase.aspose.com/temporary-license/)

---  

**अंतिम अपडेट:** 2026-10-17  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  



```java
Workbook wb = new Workbook("YOUR_DATA_DIRECTORY/sampleSetShapeTypeOfDataLabelsOfChart.xlsx");
```
```java
Worksheet ws = wb.getWorksheets().get(0);
Chart ch = ws.getCharts().get(0);
```
```java
Series srs = ch.getNSeries().get(0);
srs.getDataLabels().setShapeType(DataLabelShapeType.WEDGE_ELLIPSE_CALLOUT);
```
```java
wb.save("YOUR_OUTPUT_DIRECTORY/outputSetShapeTypeOfDataLabelsOfChart.xlsx");
```

## संबंधित ट्यूटोरियल

- [Aspose.Cells Java का उपयोग करके Excel चार्ट डेटा लेबल संशोधित करें](/cells/java/charts-graphs/modify-excel-chart-data-labels-aspose-cells-java/)
- [Aspose.Cells for Java के साथ Excel चार्ट लेबल का आकार बदलें](/cells/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/)
- [Aspose Cells for Java के साथ Excel चार्ट में लेबल जोड़ें](/cells/java/charts-graphs/adding-labels-to-charts-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}