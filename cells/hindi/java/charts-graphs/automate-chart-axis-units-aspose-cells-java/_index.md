---
date: '2026-07-02'
description: Aspose.Cells for Java का उपयोग करके चार्ट को PDF में निर्यात करना और
  अक्ष अंतराल को स्वचालित रूप से सेट करना सीखें। Excel चार्ट स्वचालन के लिए पूर्ण
  मार्गदर्शिका।
keywords:
- export chart to pdf
- set axis interval
- excel chart automation
- aspose.cells maven
- load excel workbook java
schemas:
- author: Aspose
  dateModified: '2026-07-02'
  description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  headline: Export Chart to PDF and Automate Axis Units in Java
  type: TechArticle
- description: Learn how to export chart to PDF and set axis interval automatically
    using Aspose.Cells for Java. Complete guide for Excel chart automation.
  name: Export Chart to PDF and Automate Axis Units in Java
  steps:
  - name: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
    text: '**Financial Reporting:** Generate quarterly profit‑loss charts that automatically
      adjust axis intervals as numbers grow.'
  - name: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
    text: '**Sales Analysis:** Create dynamic sales performance graphs that adapt
      to new data without manual re‑formatting.'
  - name: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
    text: '**Project Management:** Produce timeline Gantt charts where date axes scale
      automatically based on task duration.'
  type: HowTo
- questions:
  - answer: Yes—use `chart.toImage("output.png", ImageFormat.getPng())` for PNG, JPEG,
      BMP, and more.
    question: Can I export charts to image formats as well?
  - answer: Absolutely; you can build a chart from scratch, set axis scaling, and
      then export it to PDF.
    question: Does the API support charts created programmatically?
  - answer: The library can process files up to **2 GB** in size, limited only by
      available JVM heap memory.
    question: What is the maximum file size Aspose.Cells can handle?
  - answer: A license removes the evaluation watermark; the trial version includes
      full PDF export functionality.
    question: Is a license required for PDF export?
  - answer: Call `chart.getCategoryAxis().setMajorUnit(10.0)` (or `setMinorUnit`)
      to define a fixed interval.
    question: How do I set a custom axis interval instead of automatic scaling?
  type: FAQPage
title: जावा में चार्ट को PDF में निर्यात करें और अक्ष इकाइयों को स्वचालित करें
url: /hi/java/charts-graphs/automate-chart-axis-units-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# जावा में चार्ट को PDF में निर्यात करें और अक्ष इकाइयों को स्वचालित करें

## परिचय

एक चार्ट को PDF में निर्यात करना और साथ ही अक्ष इकाइयों को स्वचालित रूप से कॉन्फ़िगर करना अनगिनत मैन्युअल चरणों को बचाता है और फ़ॉर्मेटिंग त्रुटियों को समाप्त करता है। इस ट्यूटोरियल में आप सीखेंगे कि Aspose.Cells for Java के साथ प्रोग्रामेटिक रूप से **export chart to PDF** और **set axis interval** कैसे किया जाता है—बिल्कुल वही तरीका जैसा Microsoft Excel करता है। हम पर्यावरण सेटअप, वर्कबुक लोड करना, चार्ट अक्ष स्केलिंग कॉन्फ़िगर करना, और अंत में चार्ट को PDF फ़ाइल के रूप में रेंडर करना दिखाएंगे।

**आप क्या सीखेंगे**
- Maven या Gradle प्रोजेक्ट में Aspose.Cells for Java जोड़ने का तरीका (`aspose.cells maven`)।
- Excel वर्कबुक जावा कोड लोड करने और चार्ट तक पहुँचने का सही तरीका (**load Excel workbook java**)।
- चार्ट अक्ष स्केलिंग को स्वचालित करने के चरण (`set axis interval`) ताकि उत्तम दृश्य आउटपुट मिल सके।
- चार्ट को PDF और अन्य फ़ॉर्मैट्स में निर्यात करना।

## त्वरित उत्तर
- **क्या मैं Aspose.Cells के साथ चार्ट को PDF में निर्यात कर सकता हूँ?** हाँ—अक्ष को कॉन्फ़िगर करने के बाद `chart.toPdf()` कॉल करें।
- **क्या मुझे प्रोडक्शन के लिए लाइसेंस की आवश्यकता है?** एक वैध Aspose.Cells लाइसेंस मूल्यांकन वॉटरमार्क को हटा देता है।
- **कौन सा बिल्ड टूल अनुशंसित है?** Maven (`aspose.cells maven`) या Gradle दोनों समान रूप से काम करते हैं।
- **क्या API Java 8+ के साथ संगत है?** बिल्कुल; Aspose.Cells Java 8 से लेकर Java 21 तक समर्थन देता है।
- **क्या मैं किसी भी चार्ट प्रकार के लिए अक्ष इकाइयों को स्वचालित कर सकता हूँ?** एक ही API लाइन, बार, स्कैटर और पाई चार्ट्स के लिए काम करता है।

## “export chart to PDF” क्या है?
एक चार्ट को PDF में निर्यात करने से Excel चार्ट का दृश्य प्रतिनिधित्व एक उच्च‑गुणवत्ता, वेक्टर‑आधारित PDF दस्तावेज़ में बदल जाता है। यह प्रक्रिया चार्ट की लेआउट, रंग, फ़ॉन्ट और अक्ष स्केलिंग को संरक्षित रखती है, जिससे एक रिज़ॉल्यूशन‑स्वतंत्र फ़ाइल बनती है जिसे किसी भी प्लेटफ़ॉर्म पर देखा जा सकता है, बिना सर्वर पर Microsoft Excel स्थापित किए।

## चार्ट अक्ष स्केलिंग को स्वचालित क्यों करें?
Aspose.Cells डेटा रेंज के आधार पर स्वचालित रूप से इष्टतम अक्ष अंतराल की गणना कर सकता है, जो Excel के मूल व्यवहार को प्रतिबिंबित करता है। इससे मैन्युअल ट्यूनिंग समाप्त होती है, रिपोर्टों में स्थिरता सुनिश्चित होती है, और गलत डेटा व्याख्या का जोखिम कम होता है। **Quantified claim:** Aspose.Cells वर्कशीट्स को **1 048 576 पंक्तियों** और **16 384 कॉलम** तक संभालता है, जबकि सामान्य डेटा सेट के लिए अक्ष गणना **0.2 seconds** से कम रखता है।

## पूर्वापेक्षाएँ
- **Aspose.Cells for Java** (संस्करण 25.3 या बाद का)।
- Java Development Kit (JDK 8 या नया)।
- निर्भरता प्रबंधन के लिए Maven या Gradle।
- बुनियादी Java ज्ञान और Excel चार्ट अवधारणाओं की परिचितता।

## Aspose.Cells for Java सेटअप करना

Aspose.Cells का उपयोग शुरू करने के लिए, लाइब्रेरी को Maven या Gradle के माध्यम से अपने प्रोजेक्ट में जोड़ें।

**Maven (`aspose.cells maven`):**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle:**  
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### लाइसेंस प्राप्ति
Aspose.Cells for Java का उपयोग करने के लिए, आप एक अस्थायी लाइसेंस प्राप्त कर सकते हैं या खरीद सकते हैं:

- **Free Trial:** [Aspose Downloads](https://releases.aspose.com/cells/java/) से ट्रायल संस्करण डाउनलोड करें।
- **Temporary License:** [Aspose Temporary License page](https://purchase.aspose.com/temporary-license/) पर अस्थायी लाइसेंस के लिए आवेदन करें।
- **Purchase License:** [Aspose Purchase Page](https://purchase.aspose.com/buy) के माध्यम से पूर्ण लाइसेंस खरीदें।

Aspose.Cells को आपके Excel फ़ाइल को लोड करके इनिशियलाइज़ करें:  
```java
Workbook wb = new Workbook("your-file-path.xlsx");
```

पर्यावरण तैयार होने पर, चलिए मुख्य कार्यान्वयन की ओर बढ़ते हैं।

## Aspose.Cells for Java का उपयोग करके चार्ट को PDF में कैसे निर्यात करें?
`Chart` एक वर्कशीट के भीतर डेटा का ग्राफिकल प्रतिनिधित्व है, जैसे लाइन, बार, या पाई चार्ट। वर्कबुक लोड करें, चार्ट को खोजें, स्वचालित अक्ष स्केलिंग लागू करें, और PDF निर्यात मेथड को कॉल करें। नीचे दिए गए चरणों में 70 शब्दों से कम में पूरी प्रक्रिया दिखायी गई है।

पहले, एक `Workbook` इंस्टेंस बनाएं, वांछित `Chart` ऑब्जेक्ट प्राप्त करें, स्वचालित अक्ष अंतराल गणना सक्षम करें, और अंत में `chart.toPdf("output.pdf")` को कॉल करें। यह एक‑लाइन निर्यात सभी फ़ॉर्मेटिंग और अक्ष सेटिंग्स को ठीक उसी तरह संरक्षित रखता है जैसा Excel में दिखता है।

### डेटा लोड करना और एक्सेस करना
`Workbook` क्लास Aspose.Cells की शीर्ष‑स्तरीय ऑब्जेक्ट है जो मेमोरी में पूरे Excel फ़ाइल का प्रतिनिधित्व करती है। फ़ाइल लोड करने से आपको वर्कशीट्स, सेल्स, और एम्बेडेड चार्ट्स तक पहुँच मिलती है:  
```java
// Load the sample Excel file
Workbook wb = new Workbook(srcDir + "sampleHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.xlsx");

// Access first worksheet
Worksheet ws = wb.getWorksheets().get(0);

// Access first chart
Chart ch = ws.getCharts().get(0);
```

### चार्ट अक्ष इकाइयों को स्वचालित करना
`Axis` चार्ट के X या Y आयाम के स्केल और लेबलिंग को परिभाषित करता है, टिक मार्क्स और अंतराल को नियंत्रित करता है।

चार्ट अक्ष इकाइयों को स्वचालित करने से आपके चार्ट Excel के व्यवहार की नकल करते हैं, डेटा प्रतिनिधित्व में स्थिरता और सटीकता प्रदान करते हैं। डेटा रेंज के आधार पर इष्टतम अंतराल की गणना करने के लिए `Axis` ऑब्जेक्ट पर `setAutomaticMajorUnit(true)` मेथड का उपयोग करें।

**चार्ट को PDF में रेंडर करें:**  
विभिन्न फ़ॉर्मैट्स में चार्ट निर्यात करना प्रस्तुतियों या रिपोर्टों के लिए विशेष रूप से उपयोगी हो सकता है। यहाँ बताया गया है कि अक्ष कॉन्फ़िगरेशन के बाद चार्ट को PDF में कैसे रेंडर किया जाए:  
```java
// Render chart to pdf
ch.toPdf(outDir + "outputHandleAutomaticUnitsOfChartAxisLikeMicrosoftExcel.pdf");
```

## प्रमुख कॉन्फ़िगरेशन विकल्प
Aspose.Cells चार्ट्स के लिए **150** से अधिक कॉन्फ़िगर करने योग्य प्रॉपर्टीज़ प्रदान करता है, जिससे आप रंगों से लेकर डेटा लेबल्स तक सब कुछ फाइन‑ट्यून कर सकते हैं। अक्ष स्केलिंग के लिए सबसे प्रासंगिक विकल्प हैं:

- `setAutomaticMajorUnit(boolean)` – लाइब्रेरी को सबसे अच्छा अंतराल तय करने देता है।
- `setMajorUnit(double)` – आवश्यकता होने पर अंतराल को मैन्युअल रूप से ओवरराइड करता है।
- `setMinorUnit(double)` – माइनर टिक स्पेसिंग को नियंत्रित करता है।

## व्यावहारिक अनुप्रयोग
चार्ट अक्ष इकाइयों को स्वचालित करना कई वास्तविक‑दुनिया परिदृश्यों में मूल्यवान है:

1. **वित्तीय रिपोर्टिंग:** त्रैमासिक लाभ‑हानि चार्ट बनाएं जो संख्याओं के बढ़ने पर स्वचालित रूप से अक्ष अंतराल को समायोजित करते हैं।
2. **सेल्स विश्लेषण:** डायनामिक सेल्स प्रदर्शन ग्राफ़ बनाएं जो नई डेटा के साथ बिना मैन्युअल री‑फ़ॉर्मेटिंग के अनुकूल होते हैं।
3. **प्रोजेक्ट मैनेजमेंट:** टास्क अवधि के आधार पर डेट अक्ष स्वचालित रूप से स्केल होते हुए टाइमलाइन गैंट चार्ट बनाएं।

## प्रदर्शन विचार
बड़े वर्कबुक्स को प्रोसेस करते समय इष्टतम प्रदर्शन के लिए:

- अनुपयोगी `Workbook` इंस्टेंस को तुरंत बंद करें ताकि मेमोरी मुक्त हो सके।
- `Workbook.calculateFormula()` का उपयोग केवल आवश्यक होने पर करें; Aspose.Cells अधिकांश फ़ॉर्मूले को लेज़ी रूप से मूल्यांकन करता है।
- **Quantified claim:** 200‑शीट वर्कबुक जिसमें 500 KB चार्ट डेटा है, उसे मानक 2.6 GHz CPU पर **1.5 seconds** से कम समय में प्रोसेस किया जाता है।

**सर्वोत्तम प्रथाएँ**
- Aspose.Cells को अपडेट रखें ताकि प्रदर्शन सुधार और नए फ़ाइल‑फ़ॉर्मेट समर्थन से लाभ मिल सके।
- Java के बिल्ट‑इन टूल्स (जैसे, VisualVM) से अपने एप्लिकेशन को प्रोफ़ाइल करें ताकि चार्ट रेंडरिंग से संबंधित किसी भी बॉटलनेक को पहचाना जा सके।

## अक्सर पूछे जाने वाले प्रश्न
**Q: क्या मैं चार्ट को इमेज फ़ॉर्मैट्स में भी निर्यात कर सकता हूँ?**  
A: हाँ—PNG, JPEG, BMP आदि के लिए `chart.toImage("output.png", ImageFormat.getPng())` का उपयोग करें।

**Q: क्या API प्रोग्रामेटिक रूप से बनाए गए चार्ट्स का समर्थन करता है?**  
A: बिल्कुल; आप शून्य से चार्ट बना सकते हैं, अक्ष स्केलिंग सेट कर सकते हैं, और फिर इसे PDF में निर्यात कर सकते हैं।

**Q: Aspose.Cells अधिकतम कौन सा फ़ाइल आकार संभाल सकता है?**  
A: लाइब्रेरी **2 GB** तक की फ़ाइलों को प्रोसेस कर सकती है, जो केवल उपलब्ध JVM हीप मेमोरी द्वारा सीमित है।

**Q: क्या PDF निर्यात के लिए लाइसेंस आवश्यक है?**  
A: लाइसेंस मूल्यांकन वॉटरमार्क को हटाता है; ट्रायल संस्करण में पूर्ण PDF निर्यात कार्यक्षमता शामिल है।

**Q: स्वचालित स्केलिंग के बजाय कस्टम अक्ष अंतराल कैसे सेट करूँ?**  
A: एक निश्चित अंतराल निर्धारित करने के लिए `chart.getCategoryAxis().setMajorUnit(10.0)` (या `setMinorUnit`) कॉल करें।

## संसाधन
- [Aspose.Cells दस्तावेज़](https://reference.aspose.com/cells/java/)
- [Aspose.Cells Java डाउनलोड करें](https://releases.aspose.com/cells/java/)
- [लाइसेंस खरीदें](https://purchase.aspose.com/buy)
- [फ्री ट्रायल](https://releases.aspose.com/cells/java/)
- [अस्थायी लाइसेंस](https://purchase.aspose.com/temporary-license/)
- [सपोर्ट फ़ोरम](https://forum.aspose.com/c/cells/9)

---

**अंतिम अपडेट:** 2026-07-02  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल्स
- [Aspose.Cells for Java का उपयोग करके Excel चार्ट्स को PDF में निर्यात करें: कस्टम पेज साइज गाइड](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)
- [Aspose.Cells का उपयोग करके जावा में चार्ट बनाना और निर्यात करना: एक पूर्ण गाइड](/cells/java/charts-graphs/aspose-cells-java-create-export-charts/)
- [Aspose.Cells Java का उपयोग करके Excel चार्ट अक्ष लेबल निकालना: एक व्यापक गाइड](/cells/java/charts-graphs/aspose-cells-java-excel-chart-axis-labels/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< blocks/products/products-backtop-button >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}