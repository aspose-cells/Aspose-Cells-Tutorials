---
date: '2026-09-27'
description: Aspose.Cells का उपयोग करके जावा में पाई चार्ट बनाना सीखें। Excel पाई
  चार्ट को कस्टमाइज़ करने, Maven डिपेंडेंसी सेट करने, और प्रोफेशनल चार्ट बनाने के
  लिए स्टेप‑बाय‑स्टेप गाइड।
keywords:
- create pie chart java
- customize excel pie chart
- maven dependency aspose cells
lastmod: '2026-09-27'
og_description: Aspose.Cells for Java का उपयोग करके जावा में पाई चार्ट बनाएं। Excel
  पाई चार्ट को कस्टमाइज़ करना सीखें, Maven डिपेंडेंसी जोड़ें, और मिनटों में प्रोफेशनल
  चार्ट जनरेट करें।
og_image_alt: Java code generating a customized pie chart in Excel with Aspose.Cells
og_title: Aspose.Cells के साथ जावा में पाई चार्ट बनाएं – पूर्ण जावा गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Learn how to create pie chart java using Aspose.Cells. Step‑by‑step
    guide to customize Excel pie chart, set up Maven dependency, and generate professional
    charts.
  headline: How to create pie chart java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes, repeat the chart‑creation steps for each data range; each chart is
      independent.
    question: Can I generate multiple pie charts in the same workbook?
  - answer: It does; set the chart type to `ChartType.PIE_3D` when adding the chart.
    question: Does Aspose.Cells support 3‑D pie charts?
  - answer: Use the `Workbook.setDefaultTheme` method before creating any charts.
    question: How do I apply a custom theme to all charts?
  - answer: Over 30 formats, including XLSX, CSV, PDF, and HTML.
    question: What file formats can I export the workbook to?
  - answer: Yes, a valid license removes evaluation watermarks and unlocks full functionality.
    question: Is a license required for commercial deployment?
  type: FAQPage
tags:
- Aspose.Cells
- Java charting
- Excel automation
- data visualization
title: Aspose.Cells के साथ जावा में पाई चार्ट कैसे बनाएं
url: /hi/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells के साथ जावा में पाई चार्ट कैसे बनाएं

## परिचय
प्रोग्रामेटिक रूप से **pie chart** बनाना अक्सर एक पहेली जैसा लगता है, विशेष रूप से जब आपको रंगों, लेजेंड और शीर्षकों पर सूक्ष्म नियंत्रण चाहिए। इस गाइड में आप Aspose.Cells का उपयोग करके **create pie chart java** कैसे बनाएं सीखेंगे, फिर अपने ब्रांड या रिपोर्टिंग शैली के अनुसार Excel पाई चार्ट को अनुकूलित करेंगे। हम पर्यावरण सेटअप, डेटा भरना, चार्ट जनरेशन और दृश्य समायोजन के चरणों से गुजरेंगे—बिना आपके Java IDE छोड़े।

**आप क्या सीखेंगे**
- अपने प्रोजेक्ट में **Maven dependency Aspose.Cells** जोड़ें।
- एक workbook बनाएं, डेटा के साथ सेल्स भरें, और एक pie chart उत्पन्न करें।
- चार्ट में कस्टम रंग, शीर्षक, और लेजेंड लागू करें।
- workbook को एक XLSX फ़ाइल में निर्यात करें जो साझा करने के लिए तैयार हो।

शुरू करने से पहले, आपको बुनियादी Java सिंटैक्स में सहज होना चाहिए और Maven या Gradle स्थापित होना चाहिए।

## त्वरित उत्तर
- **Java में पाई चार्ट बनाने वाली लाइब्रेरी कौन सी है?** Aspose.Cells for Java.
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक पेड लाइसेंस आवश्यक है।
- **कौन से Maven कोऑर्डिनेट्स आवश्यक हैं?** `com.aspose:aspose-cells:24.10`।
- **क्या मैं स्लाइस के रंग बदल सकता हूँ?** हाँ, प्रत्येक series पर `setAreaColor` मेथड के माध्यम से।
- **क्या चार्ट को XLSX में निर्यात किया जा सकता है?** बिल्कुल—सिर्फ `workbook.save("output.xlsx")` कॉल करें।

## Excel में पाई चार्ट क्या है?
एक पाई चार्ट एकल डेटा सीरीज़ को एक वृत्त के अनुपातिक स्लाइस के रूप में दर्शाता है, जिससे पूरे का भाग तुलना करना आसान हो जाता है। प्रत्येक स्लाइस का कोण उसके कुल के सापेक्ष मान के अनुरूप होता है, जिससे बाजार हिस्सेदारी, बजट आवंटन, या जनसांख्यिकीय प्रतिशत जैसी श्रेणियों में वितरण का त्वरित अंतर्दृष्टि मिलती है।

## जावा में पाई चार्ट बनाने के लिए Aspose.Cells क्यों उपयोग करें?
Aspose.Cells 50 से अधिक चार्ट प्रकारों को समर्थन देता है और पूरी फ़ाइल को मेमोरी में लोड किए बिना एक मिलियन पंक्तियों तक की वर्कशीट्स को संभाल सकता है। यह प्रदर्शन लाभ आपको सीमित हार्डवेयर पर बड़े रिपोर्ट बनाने की अनुमति देता है, साथ ही चार्ट की उपस्थिति, डेटा बाइंडिंग, और निर्यात फ़ॉर्मैट्स पर सूक्ष्म नियंत्रण प्रदान करता है, जिससे यह कई ओपन‑सोर्स लाइब्रेरीज़ की तुलना में श्रेष्ठ विकल्प बनता है।

## पूर्वापेक्षाएँ
- **Java Development Kit (JDK)** 8 या नया।
- **IDE** जैसे IntelliJ IDEA या Eclipse।
- **Maven** या **Gradle** निर्भरता प्रबंधन के लिए।
- एक **trial or purchased Aspose.Cells license**।

### आवश्यक लाइब्रेरी और निर्भरताएँ
अपने `pom.xml` में Aspose.Cells Maven आर्टिफैक्ट जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

या Gradle समकक्ष:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### लाइसेंस प्राप्ति चरण
Aspose.Cells for Java व्यावसायिक है, लेकिन आप एक मुफ्त ट्रायल से शुरू कर सकते हैं। अस्थायी लाइसेंस कुंजी प्राप्त करने के लिए [खरीद पृष्ठ](https://purchase.aspose.com/buy) पर जाएँ।

## Aspose.Cells for Java सेटअप करना
सबसे पहले, सुनिश्चित करें कि लाइब्रेरी आपके क्लासपाथ पर है। निर्भरता जोड़ने के बाद, आप नीचे दिखाए अनुसार API को इनिशियलाइज़ कर सकते हैं।

```java
import com.aspose.cells.Workbook;

// Initialize a new workbook instance
Workbook workbook = new Workbook();
```

## कार्यान्वयन गाइड

### एक workbook बनाएं और कॉन्फ़िगर करें
`Workbook` क्लास मेमोरी में एक पूरी Excel फ़ाइल का प्रतिनिधित्व करती है।

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Cells;
import com.aspose.cells.ChartType;
import com.aspose.cells.Chart;
import com.aspose.cells.Series;
import com.aspose.cells.Color;
import com.aspose.cells.LegendPositionType;
import com.aspose.cells.SaveFormat;
```

#### चरण 1: एक workbook इंस्टैंसिएट करें
```java
// Creates an empty workbook instance to work with.
Workbook workbook = new Workbook();
```  
यह एक नया, खाली workbook बनाता है जिसे आप तुरंत भरना शुरू कर सकते हैं।

### वर्कशीट सेल्स तक पहुँचें या संशोधित करें
`Worksheet` workbook के भीतर एक एकल शीट का प्रतिनिधित्व करता है, जिसमें सेल्स, पंक्तियाँ, और कॉलम होते हैं।  
आप वह डेटा लिखेंगे जो पाई चार्ट को संचालित करेगा, एक worksheet में।

#### चरण 2: पहली worksheet और उसके सेल्स प्राप्त करें
```java
// Access the first worksheet in the workbook.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// Put sample values used for a pie chart into specific cells.
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// Put percentage values for a pie chart into specific cells.
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```  
सेल्स को श्रेणी नामों और मानों से भरें जो चार्ट उपयोग करेगा।

### एक पाई चार्ट बनाएं
`Chart` ऑब्जेक्ट्स worksheet में डेटा को विज़ुअलाइज़ करते हैं और पाई, कॉलम, और लाइन जैसे विभिन्न प्रकारों का समर्थन करते हैं।

#### चरण 3: worksheet में एक पाई चार्ट जोड़ें
```java
// Create a pie chart in the worksheet.
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```  

### पाई चार्ट सीरीज़ और डेटा कॉन्फ़िगर करें
`Series` चार्ट के लिए डेटा रेंज और फ़ॉर्मेटिंग को परिभाषित करता है, worksheet के सेल्स को विज़ुअल तत्वों से जोड़ता है।

#### चरण 4: चार्ट के लिए सीरीज़ सेट करें
```java
// Configure the series data range for the chart.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// Link the pie chart title to a cell containing the title text.
pie.getTitle().setLinkedSource("D2");
```  

### चार्ट लेजेंड और शीर्षक की उपस्थिति कॉन्फ़िगर करें
एक चार्ट `Legend` सीरीज़ नाम और रंग दिखाता है, जिससे पाठकों को प्रत्येक स्लाइस पहचानने में मदद मिलती है।

#### चरण 5: चार्ट लेजेंड और शीर्षक को कस्टमाइज़ करें
```java
// Set legend position at bottom of the chart.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// Set font properties for the chart title.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```  

### चार्ट सीरीज़ रंग कस्टमाइज़ करें
`setAreaColor` एक चार्ट सीरीज़ स्लाइस के भरने का रंग RGB मान का उपयोग करके सेट करता है।

#### चरण 6: पाई सेगमेंट के रंग बदलें
```java
import com.aspose.cells.Color;

// Access and customize colors of individual pie chart segments.
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```  

### कॉलम ऑटोफिट करें और workbook सहेजें
`autoFitColumns` स्वचालित रूप से कॉलम की चौड़ाई को सेल सामग्री के अनुसार समायोजित करता है।

#### चरण 7: कॉलम चौड़ाई समायोजित करें और फ़ाइल सहेजें
```java
// Autofit all columns.
worksheet.autoFitColumns();

// Define output directory placeholder path for saving the workbook.
String outDir = "YOUR_OUTPUT_DIRECTORY";

// Save the modified workbook to an Excel file in the specified directory.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```  

## सामान्य उपयोग केस
- **Demographic analysis:** क्षेत्रों में जनसंख्या वितरण दिखाएँ।
- **Market‑share reporting:** एक नज़र में प्रत्येक प्रतिस्पर्धी का शेयर विज़ुअलाइज़ करें।
- **Budget allocation:** दिखाएँ कि फंड विभागों में कैसे विभाजित हैं।

## प्रदर्शन विचार
- जब ऑब्जेक्ट्स की अब आवश्यकता न हो तो (`workbook.dispose()`) रिलीज़ करें ताकि नेटिव मेमोरी मुक्त हो सके।
- बड़े डेटा सेट्स के लिए, सभी डेटा को एक बार लोड करने के बजाय `WorkbookDesigner` का उपयोग करके डेटा स्ट्रीम करें।
- चार्ट जनरेशन में किसी भी बॉटलनेक को पहचानने के लिए Java Flight Recorder के साथ प्रोफ़ाइल करें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं एक ही workbook में कई पाई चार्ट बना सकता हूँ?**  
A: हाँ, प्रत्येक डेटा रेंज के लिए चार्ट‑क्रिएशन चरण दोहराएँ; प्रत्येक चार्ट स्वतंत्र है।

**Q: क्या Aspose.Cells 3‑D पाई चार्ट सपोर्ट करता है?**  
A: हाँ; चार्ट जोड़ते समय चार्ट प्रकार को `ChartType.PIE_3D` सेट करें।

**Q: सभी चार्ट्स पर कस्टम थीम कैसे लागू करूँ?**  
A: कोई भी चार्ट बनाने से पहले `Workbook.setDefaultTheme` मेथड का उपयोग करें।

**Q: मैं workbook को किन फ़ाइल फ़ॉर्मैट्स में निर्यात कर सकता हूँ?**  
A: 30 से अधिक फ़ॉर्मैट्स, जैसे XLSX, CSV, PDF, और HTML।

**Q: व्यावसायिक उपयोग के लिए लाइसेंस आवश्यक है?**  
A: हाँ, एक वैध लाइसेंस मूल्यांकन वॉटरमार्क हटाता है और पूरी कार्यक्षमता अनलॉक करता है।

## निष्कर्ष
अब आपके पास Aspose.Cells के साथ **create pie chart java** के लिए एक पूर्ण, अंत‑से‑अंत रेसिपी है। ऊपर दिए गए चरणों का पालन करके आप परिष्कृत Excel पाई चार्ट बना सकते हैं, रंग और शीर्षक को अनुकूलित कर सकते हैं, और उन्हें किसी भी रिपोर्टिंग पाइपलाइन में एम्बेड कर सकते हैं। अन्य चार्ट प्रकार—कॉलम, लाइन, रडार—की खोज करें ताकि आपका डेटा‑विज़ुअलाइज़ेशन टूलकिट विस्तृत हो सके।

---

**अंतिम अपडेट:** 2026-09-27  
**परीक्षण किया गया:** Aspose.Cells 24.10 for Java  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose.Cells for Java का उपयोग करके Excel चार्ट डेटा लेबल कस्टमाइज़ करें&#58; एक चरण-दर-चरण गाइड](/cells/java/charts-graphs/customize-chart-data-labels-aspose-cells-java/)
- [Aspose.Cells Java के साथ डायनामिक Excel चार्ट बनाएं&#58; डेवलपर्स के लिए एक व्यापक गाइड](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Aspose.Cells Java का उपयोग करके Excel वर्कबुक बनाएं और कस्टमाइज़ करें&#58; एक चरण-दर-चरण गाइड](/cells/java/workbook-operations/create-customize-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}