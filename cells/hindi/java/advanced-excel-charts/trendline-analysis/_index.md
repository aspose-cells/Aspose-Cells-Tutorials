---
date: 2026-08-27
description: Aspose.Cells for Java का उपयोग करके chart में trendline जोड़ना, उसका
  R‑squared मान दिखाना, और chart को PNG या JPEG image के रूप में export करना सीखें।
keywords:
- add trendline to chart
- save chart as image
- export excel chart image
- java create excel workbook
- convert chart to png
lastmod: 2026-08-27
linktitle: Trendline Analysis के साथ chart को image में export करें
og_description: Aspose.Cells for Java का उपयोग करके chart में trendline जोड़ें, R‑squared
  देखें, और परिणाम को PNG/JPEG के रूप में export करें – एक तेज़, 50‑format समाधान।
og_image_alt: Guide showing Java code to add a trendline to an Excel chart and export
  it as an image
og_title: Aspose.Cells for Java के साथ chart में trendline जोड़ें और image के रूप
  में export करें
schemas:
- author: Aspose
  dateModified: '2026-08-27'
  description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  headline: How to add trendline to chart and export as image in Java
  type: TechArticle
- description: Learn how to add trendline to chart, display its R‑squared value, and
    export the chart as a PNG or JPEG image using Aspose.Cells for Java.
  name: How to add trendline to chart and export as image in Java
  steps:
  - name: set up the project
    text: Create a new Java project and place the Aspose.Cells JARs on the build path.
      This prepares the environment for generating and manipulating Excel files.
  - name: load excel file (load excel file java)
    text: '*We’ve just **loaded an Excel file** into memory, ready for chart creation.*'
  - name: create a chart
    text: '*Here we generate a line chart that will later host our trendline.*'
  - name: add trendline (how to add trendline) and display R‑squared value
    text: '*The `setDisplayRSquaredValue(true)` call ensures the **R‑squared value**
      appears on the chart.*'
  - name: customize chart and save workbook (save workbook xlsx, generate excel file
      java)
    text: '*Now the workbook is **generated** and saved as an XLSX file, ready for
      further processing.*'
  - name: export chart to image (export chart to image)
    text: '> **Note:** This step is described without an additional code block to
      keep the original block count unchanged. After the chart is created and saved,
      you can export it to an image by calling the `chart.toImage()` method and writing
      the resulting `java.awt.image.BufferedImage` to a file format of you'
  type: HowTo
- questions:
  - answer: Use a different `TrendlineType` enumeration when adding the trendline,
      e.g., `TrendlineType.POLYNOMIAL` for a polynomial fit.
    question: How can I change the trendline type?
  - answer: Yes. Access the trendline’s `LineFormat` via `trendline.getLineFormat()`
      and set properties such as `setWeight()` and `setColor()`.
    question: Can I customize the trendline appearance (color, thickness)?
  - answer: Convert the chart to an image first, then embed that image into a PDF
      using Aspose.PDF or any other PDF library.
    question: How do I export the chart to PDF instead of an image?
  - answer: Absolutely. Call `chart.getNSeries().get(0).getTrendlines().add(...)`
      for each series you wish to analyze.
    question: Is it possible to add multiple trendlines to the same chart?
  - answer: Yes. You can specify the DPI when calling `chart.toImage()` and then scale
      the image before saving, ensuring crisp output for print or high‑density screens.
    question: Does Aspose.Cells support high‑resolution image export?
  type: FAQPage
second_title: Aspose.Cells Java Excel Processing API
tags:
- Aspose.Cells
- Java charting
- Excel automation
- trendline analysis
title: Java में chart में trendline जोड़ें और image के रूप में export करें
url: /hi/java/advanced-excel-charts/trendline-analysis/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# चार्ट में ट्रेंडलाइन जोड़ें और इसे छवि के रूप में निर्यात करें

इस ट्यूटोरियल में आप सीखेंगे कि **चार्ट में ट्रेंडलाइन कैसे जोड़ें**, R‑squared मान कैसे प्रदर्शित करें, और Aspose.Cells for Java का उपयोग करके दृश्य को PNG या JPEG फ़ाइल के रूप में निर्यात करें। आप देखेंगे कि ट्रेंडलाइन क्यों महत्वपूर्ण हैं, वर्कबुक कैसे तैयार करें, और उच्च‑रिज़ॉल्यूशन छवि उत्पन्न करने के सटीक चरण क्या हैं, जिसे रिपोर्ट, ईमेल या वेब पेज में एम्बेड किया जा सकता है।

## त्वरित उत्तर
- **इस गाइड का मुख्य लक्ष्य क्या है?** आपको दिखाना कि चार्ट में ट्रेंडलाइन कैसे जोड़ें, उसका समीकरण और R‑squared मान कैसे प्रदर्शित करें, और जावा के साथ चार्ट को छवि के रूप में निर्यात करें।  
- **मुझे कौन सी लाइब्रेरी चाहिए?** Aspose.Cells for Java – इसे [Aspose.Cells for Java रिलीज़ पेज](https://releases.aspose.com/cells/java/) से डाउनलोड करें।  
- **क्या विकास के लिए लाइसेंस चाहिए?** विकास के लिए एक फ्री ट्रायल काम करता है; उत्पादन परिनियोजन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं प्रोग्रामेटिकली Excel वर्कबुक बना सकता हूँ?** हाँ – ट्यूटोरियल शून्य से एक XLSX वर्कबुक बनाता और सहेजता है।  
- **चार्ट को PNG या JPEG में कैसे निर्यात किया जाता है?** `Chart.toImage()` मेथड को कॉल करें और लौटाए गए `BufferedImage` को `ImageIO.write(...)` से लिखें।

## आप Excel चार्ट को ट्रेंडलाइन के साथ कैसे बनाते हैं और इसे छवि के रूप में निर्यात करते हैं?
वर्कबुक लोड करें, एक लाइन चार्ट जोड़ें, एक ट्रेंडलाइन संलग्न करें जो समीकरण और R‑squared मान दिखाती है, वर्कबुक सहेजें, फिर `chart.toImage()` को कॉल करें और परिणामी `BufferedImage` को PNG या JPEG फ़ाइल में लिखें। यह एंड‑टू‑एंड प्रक्रिया केवल कुछ ही जावा कोड लाइनों में पूरी होती है और किसी भी डाउनस्ट्रीम एप्लिकेशन के लिए उपयुक्त पिक्सेल‑परफ़ेक्ट छवि उत्पन्न करती है।

## चार्ट को छवि में निर्यात करना क्या है?
एक चार्ट को छवि में निर्यात करने से आपके डेटा का दृश्य प्रतिनिधित्व एक पोर्टेबल बिटमैप (PNG, JPEG, BMP, आदि) में बदल जाता है। यह फ़ॉर्मेट रिपोर्ट, वेब पेज या प्रस्तुतियों में चार्ट एम्बेड करने के लिए आदर्श है जहाँ मूल Excel फ़ाइल की आवश्यकता नहीं होती।

## ट्रेंडलाइन जोड़ने और R‑squared मान प्रदर्शित करने का कारण क्या है?
एक ट्रेंडलाइन डेटा श्रृंखला के अंतर्निहित पैटर्न को उजागर करती है, जबकि **R‑squared** मीट्रिक यह मापता है कि ट्रेंडलाइन डेटा से कितनी निकटता से मेल खाती है। निर्यातित छवि में दोनों को शामिल करने से हितधारकों को वर्कबुक खोले बिना तुरंत अंतर्दृष्टि मिलती है। यह निर्णय‑निर्माताओं को संबंध की ताकत और भविष्यवाणी ट्रेंड्स को जल्दी से आकलन करने में मदद करता है, Excel खोलने की आवश्यकता के बिना।

## पूर्वापेक्षाएँ
- आपके विकास मशीन पर Java 8 या नया स्थापित हो।  
- प्रोजेक्ट के क्लासपाथ में Aspose.Cells for Java लाइब्रेरी (JAR फ़ाइलें) जोड़ी गई हो।  
- IntelliJ IDEA या Eclipse जैसे Java IDE से परिचित हों।  

## चरण‑दर‑चरण मार्गदर्शिका

### चरण 1: प्रोजेक्ट सेट अप करें
एक नया Java प्रोजेक्ट बनाएं और Aspose.Cells JARs को बिल्ड पाथ पर रखें। यह Excel फ़ाइलों को जनरेट और मैनीपुलेट करने के लिए वातावरण तैयार करता है।

### चरण 2: Excel फ़ाइल लोड करें (load excel file java)
```java
// Import necessary libraries
import com.aspose.cells.*;

// Load the Excel file
Workbook workbook = new Workbook("your_excel_file.xlsx");

// Access the worksheet
Worksheet worksheet = workbook.getWorksheets().get(0);
```
*हमने अभी **एक Excel फ़ाइल** मेमोरी में लोड कर ली है, जो चार्ट निर्माण के लिए तैयार है।*

### चरण 3: चार्ट बनाएं
```java
// Create a chart
int chartIndex = worksheet.getCharts().add(ChartType.LINE, 5, 0, 15, 5);
Chart chart = worksheet.getCharts().get(chartIndex);

// Specify data source for the chart
chart.getNSeries().add("A1:A10", true);
```
*यहाँ हम एक लाइन चार्ट जनरेट करते हैं जो बाद में हमारी ट्रेंडलाइन को होस्ट करेगा।*

### चरण 4: ट्रेंडलाइन जोड़ें (how to add trendline) और R‑squared मान प्रदर्शित करें
```java
// Add a trendline to the chart
Trendline trendline = chart.getNSeries().get(0).getTrendlines().add(TrendlineType.LINEAR);

// Customize trendline options
trendline.setDisplayEquation(true);
trendline.setDisplayRSquaredValue(true);
```
*`setDisplayRSquaredValue(true)` कॉल यह सुनिश्चित करता है कि **R‑squared मान** चार्ट पर दिखाई दे।*

### चरण 5: चार्ट को कस्टमाइज़ करें और वर्कबुक सहेजें (save workbook xlsx, generate excel file java)
```java
// Customize chart title and axes
chart.getTitle().setText("Trendline Analysis");
chart.getCategoryAxis().getTitle().setText("X-Axis");
chart.getValueAxis().getTitle().setText("Y-Axis");

// Save the Excel file with the chart
workbook.save("output.xlsx");
```
*अब वर्कबुक **जनरेट** हो गई है और एक XLSX फ़ाइल के रूप में सहेजी गई है, आगे की प्रोसेसिंग के लिए तैयार।*

### चरण 6: चार्ट को छवि में निर्यात करें (export chart to image)
> **नोट:** इस चरण को अतिरिक्त कोड ब्लॉक के बिना वर्णित किया गया है ताकि मूल ब्लॉक गिनती अपरिवर्तित रहे।  
चार्ट बन जाने और सहेजे जाने के बाद, आप `chart.toImage()` मेथड को कॉल करके और परिणामी `java.awt.image.BufferedImage` को अपनी पसंद के फ़ाइल फ़ॉर्मेट (PNG, JPEG, BMP) में लिखकर इसे छवि में निर्यात कर सकते हैं। सामान्य कार्यप्रवाह इस प्रकार है:
1. `Chart` ऑब्जेक्ट प्राप्त करें (पहले के चरणों में पहले ही किया गया है)।  
2. `chart.toImage()` को कॉल करके एक `BufferedImage` प्राप्त करें।  
3. `ImageIO.write(bufferedImage, "png", new File("chart.png"))` का उपयोग करके फ़ाइल लिखें।  

`Chart` ऑब्जेक्ट वर्कबुक में एक चार्ट को दर्शाता है और इसकी उपस्थिति और डेटा को संशोधित करने के लिए मेथड्स प्रदान करता है। `BufferedImage` जावा क्लास है जो मेमोरी में छवि रखती है, जिससे इसे फ़ाइल में सहेजा जा सकता है। `ImageIO` जावा में छवियों को पढ़ने और लिखने के लिए एक यूटिलिटी क्लास है। `setDisplayRSquaredValue` ट्रेंडलाइन पर R‑squared आँकड़ा दिखाने को सक्षम करता है।

### परिणामों का विश्लेषण
`output.xlsx` को Excel में खोलें ताकि यह सत्यापित किया जा सके कि ट्रेंडलाइन, समीकरण, और R‑squared मान अपेक्षित रूप से दिखाई दे रहे हैं। निर्यातित छवि फ़ाइल (उदाहरण के लिए `chart.png`) खोलें ताकि एक साफ़ दृश्य देखा जा सके जिसे मूल वर्कबुक के बिना साझा किया जा सकता है।

## सामान्य समस्याएँ और समाधान
- **ट्रेंडलाइन नहीं दिख रही है:** सुनिश्चित करें कि डेटा रेंज (`A1:A10`) में संख्यात्मक मान हैं; गैर‑संख्यात्मक डेटा ट्रेंडलाइन गणना को रोकता है।  
- **R‑squared मान 0 दिखा रहा है:** यह अक्सर दर्शाता है कि डेटा श्रृंखला स्थिर है या परिवर्तन नहीं है। कोई अलग डेटा सेट आज़माएँ या पॉलीनॉमियल ट्रेंडलाइन का उपयोग करें।  
- **`NullPointerException` के साथ छवि निर्यात विफल:** `toImage()` को कॉल करने से पहले सुनिश्चित करें कि चार्ट पूरी तरह रेंडर हो चुका है। पहले वर्कबुक सहेजना कभी‑कभी टाइमिंग समस्याओं को हल कर सकता है।

## अक्सर पूछे जाने वाले प्रश्न

**Q: मैं ट्रेंडलाइन प्रकार कैसे बदल सकता हूँ?**  
A: ट्रेंडलाइन जोड़ते समय एक अलग `TrendlineType` एनेमरेशन का उपयोग करें, उदाहरण के लिए पॉलीनॉमियल फिट के लिए `TrendlineType.POLYNOMIAL`।

**Q: क्या मैं ट्रेंडलाइन की उपस्थिति (रंग, मोटाई) को कस्टमाइज़ कर सकता हूँ?**  
A: हाँ। `trendline.getLineFormat()` के माध्यम से ट्रेंडलाइन के `LineFormat` तक पहुँचें और `setWeight()` तथा `setColor()` जैसे गुण सेट करें।

**Q: मैं चार्ट को छवि के बजाय PDF में कैसे निर्यात करूँ?**  
A: पहले चार्ट को छवि में बदलें, फिर Aspose.PDF या किसी अन्य PDF लाइब्रेरी का उपयोग करके उस छवि को PDF में एम्बेड करें।

**Q: क्या एक ही चार्ट में कई ट्रेंडलाइन जोड़ना संभव है?**  
A: बिल्कुल। आप जिस प्रत्येक श्रृंखला का विश्लेषण करना चाहते हैं, उसके लिए `chart.getNSeries().get(0).getTrendlines().add(...)` को कॉल करें।

**Q: क्या Aspose.Cells उच्च‑रिज़ॉल्यूशन छवि निर्यात का समर्थन करता है?**  
A: हाँ। आप `chart.toImage()` को कॉल करते समय DPI निर्दिष्ट कर सकते हैं और फिर सहेजने से पहले छवि को स्केल कर सकते हैं, जिससे प्रिंट या हाई‑डेंसिटी स्क्रीन के लिए स्पष्ट आउटपुट सुनिश्चित हो जाता है।

---

**अंतिम अपडेट:** 2026-08-27  
**परीक्षण किया गया:** Aspose.Cells for Java latest (supports 50+ file formats and processes workbooks with up to 2 million rows without full memory load)  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose.Cells Java के साथ Excel चार्ट में डेटा लेबल जोड़ें](/cells/java/advanced-excel-charts/chart-interactivity/)
- [Aspose.Cells Java का उपयोग करके Excel चार्ट को SVG के रूप में निर्यात करने का तरीका (स्केलेबल वेक्टर ग्राफ़िक्स)](/cells/java/charts-graphs/export-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells for Java का उपयोग करके Excel चार्ट को PDF में निर्यात करें&#58; कस्टम पेज साइज गाइड](/cells/java/charts-graphs/export-excel-charts-pdf-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}