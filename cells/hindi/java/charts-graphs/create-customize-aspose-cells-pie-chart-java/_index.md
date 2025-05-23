---
"date": "2025-04-08"
"description": "जावा के लिए Aspose.Cells का उपयोग करके पाई चार्ट बनाना और कस्टमाइज़ करना सीखें। डेवलपर्स के लिए कोड उदाहरणों के साथ चरण-दर-चरण मार्गदर्शिका।"
"title": "Aspose.Cells में महारत हासिल करना, जावा में पाई चार्ट बनाना और अनुकूलित करना"
"url": "/hi/java/charts-graphs/create-customize-aspose-cells-pie-chart-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells में महारत हासिल करना: जावा में पाई चार्ट बनाना और अनुकूलित करना

## परिचय
Excel में डेटा विज़ुअलाइज़ेशन से निपटने के दौरान आकर्षक चार्ट बनाना एक सामान्य आवश्यकता है। चाहे आप जनसांख्यिकीय जानकारी प्रस्तुत कर रहे हों या बाज़ार के रुझानों का विश्लेषण कर रहे हों, पाई चार्ट आनुपातिक डेटा को दर्शाने का एक स्पष्ट तरीका प्रदान करते हैं। हालाँकि, इन चार्ट को प्रोग्रामेटिक रूप से सेट करना जटिल हो सकता है। यह ट्यूटोरियल आपको जावा का उपयोग करके Aspose.Cells पाई चार्ट बनाने और उसे कस्टमाइज़ करने के बारे में मार्गदर्शन करता है, जिससे डेवलपर्स के लिए प्रक्रिया सरल हो जाती है।

**आप क्या सीखेंगे:**
- Java के लिए Aspose.Cells के साथ अपना वातावरण सेट करें।
- एक नई कार्यपुस्तिका बनाएं और कार्यपत्रक कक्षों तक पहुंचें.
- चार्ट निर्माण की तैयारी के लिए विशिष्ट कक्षों में डेटा भरें।
- इस डेटा से एक पाई चार्ट बनाएं।
- अपने पाई चार्ट के स्वरूप को अनुकूलित करें, जिसमें रंग, शीर्षक और लेजेंड शामिल हैं।

शुरू करने से पहले, सुनिश्चित करें कि आपको जावा प्रोग्रामिंग और मावेन या ग्रेडेल निर्भरता प्रबंधन की कुछ बुनियादी समझ है। चलिए अपना वातावरण सेट करते हैं!

## आवश्यक शर्तें
इस ट्यूटोरियल का अनुसरण करने के लिए आपको निम्न की आवश्यकता होगी:
- **जावा डेवलपमेंट किट (JDK)**: संस्करण 8 या उच्चतर.
- **एकीकृत विकास वातावरण (आईडीई)**जैसे कि इंटेलीज आईडिया या एक्लिप्स।
- **निर्भरता प्रबंधन**: अपनी निर्भरताओं को प्रबंधित करने के लिए Maven या Gradle का उपयोग करें।

### आवश्यक लाइब्रेरी और निर्भरताएँ
Maven या Gradle का उपयोग करके अपने प्रोजेक्ट में Java के लिए Aspose.Cells को शामिल करना सुनिश्चित करें।

**मावेन**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**ग्रैडल**
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### लाइसेंस प्राप्ति चरण
Aspose.Cells for Java एक व्यावसायिक लाइब्रेरी है, लेकिन आप इसे निःशुल्क परीक्षण के साथ शुरू कर सकते हैं या अस्थायी लाइसेंस के लिए आवेदन कर सकते हैं। [खरीद पृष्ठ](https://purchase.aspose.com/buy) लाइसेंसिंग विकल्पों का पता लगाने के लिए।

## Java के लिए Aspose.Cells सेट अप करना
सबसे पहले, सुनिश्चित करें कि आपके प्रोजेक्ट वातावरण में आवश्यक लाइब्रेरीज़ शामिल हैं, उन्हें ऊपर दिखाए अनुसार Maven या Gradle के माध्यम से जोड़कर। एक बार शामिल होने के बाद, आप Aspose.Cells को आरंभ कर सकते हैं:

```java
import com.aspose.cells.Workbook;

// एक नई कार्यपुस्तिका इंस्टैंस आरंभ करें
Workbook workbook = new Workbook();
```

## कार्यान्वयन मार्गदर्शिका

### कार्यपुस्तिका बनाएं और कॉन्फ़िगर करें
कार्यपुस्तिका बनाना प्रारंभिक चरण है जहां आप अपना डेटा सेट करेंगे।

#### लाइब्रेरीज़ आयात करें
सुनिश्चित करें कि ये आयात आपकी फ़ाइल के शीर्ष पर शामिल हैं:

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

#### चरण 1: कार्यपुस्तिका इंस्टेंस बनाएँ
```java
// कार्य करने के लिए एक रिक्त कार्यपुस्तिका इंस्टैंस बनाता है.
Workbook workbook = new Workbook();
```
यह चरण आपकी Excel फ़ाइल को प्रोग्रामेटिक रूप से आरंभीकृत करता है, जिससे आप Aspose.Cells कार्यक्षमताओं का उपयोग करके उसमें परिवर्तन कर सकते हैं।

### वर्कशीट कक्षों तक पहुँचें या उन्हें संशोधित करें
इसके बाद, वर्कशीट कक्षों में डेटा भरें जिसका उपयोग पाई चार्ट के लिए किया जाएगा।

#### चरण 2: वर्कशीट और उसके कक्षों तक पहुँचें
```java
// कार्यपुस्तिका में प्रथम कार्यपत्रक तक पहुँचें.
Worksheet worksheet = workbook.getWorksheets().get(0);
Cells cells = worksheet.getCells();

// पाई चार्ट के लिए प्रयुक्त नमूना मानों को विशिष्ट कक्षों में रखें।
cells.get("C3").putValue("India");
cells.get("C4").putValue("China");
cells.get("C5").parseNumber("United States", true, null);
cells.get("C6").setValue("Russia");
cells.get("C7").setValue("United Kingdom");
cells.get("C8").setValue("Others");

// पाई चार्ट के लिए प्रतिशत मानों को विशिष्ट कक्षों में रखें।
cells.get("D2").putValue("% of world population");
cells.get("D3").putValue(25);
cells.get("D4").putValue(30);
cells.get("D5").putValue(10);
cells.get("D6").putValue(13);
cells.get("D7").putValue(9);
cells.get("D8").putValue(13);
```
यहां, आप वर्कशीट को डेटा से भरते हैं जो पाई चार्ट के विभिन्न खंडों का प्रतिनिधित्व करेगा।

### पाई चार्ट बनाएं

#### चरण 3: वर्कशीट में पाई चार्ट जोड़ें
```java
// वर्कशीट में एक पाई चार्ट बनाएं।
int pieIdx = worksheet.getCharts().add(ChartType.PIE, 1, 6, 15, 14);
Chart pie = worksheet.getCharts().get(pieIdx);
```
यह चरण आपके वर्कशीट में निर्दिष्ट स्थानों और आयामों पर एक नया पाई चार्ट जोड़ता है।

### पाई चार्ट श्रृंखला और डेटा कॉन्फ़िगर करें

#### चरण 4: चार्ट के लिए श्रृंखला निर्धारित करें
```java
// चार्ट के लिए श्रृंखला डेटा श्रेणी कॉन्फ़िगर करें.
pie.getNSeries().add("D3:D8", true);
pie.getNSeries().setCategoryData("=Sheet1!$C$3:$C$8");

// पाई चार्ट शीर्षक को शीर्षक पाठ वाले सेल से लिंक करें।
pie.getTitle().setLinkedSource("D2");
```
यह कोड आपकी डेटा रेंज को लिंक करता है और पाई चार्ट के लिए श्रृंखला सेट करता है।

### चार्ट लेजेंड और शीर्षक उपस्थिति कॉन्फ़िगर करें

#### चरण 5: चार्ट लेजेंड और शीर्षक को अनुकूलित करें
```java
// चार्ट के नीचे लेजेंड स्थिति सेट करें.
pie.getLegend().setPosition(LegendPositionType.BOTTOM);

// चार्ट शीर्षक के लिए फ़ॉन्ट गुण सेट करें.
pie.getTitle().getFont().setName("Calibri");
pie.getTitle().getFont().setSize(18);
```
स्वरूप को अनुकूलित करने से पठनीयता और दृश्य अपील बढ़ जाती है।

### चार्ट श्रृंखला रंग अनुकूलित करें

#### चरण 6: पाई सेगमेंट का रंग बदलें
```java
import com.aspose.cells.Color;

// व्यक्तिगत पाई चार्ट खंडों के रंगों तक पहुंच और उन्हें अनुकूलित करें।
Series srs = pie.getNSeries().get(0);
srs.getPoints().get(0).getArea().setForegroundColor(Color.fromArgb(0, 246, 22, 219));
srs.getPoints().get(1).getArea().setForegroundColor(Color.fromArgb(0, 51, 34, 84));
srs.getPoints().get(2).getArea().setForegroundColor(Color.fromArgb(0, 46, 74, 44));
srs.getPoints().get(3).getArea().setForegroundColor(Color.fromArgb(0, 19, 99, 44));
srs.getPoints().get(4).getArea().setForegroundColor(Color.fromArgb(0, 208, 223, 7));
srs.getPoints().get(5).getArea().setForegroundColor(Color.fromArgb(0, 222, 69, 8));
```
ये सेटिंग्स आपके चार्ट को विशिष्ट रंग योजनाओं के अनुरूप वैयक्तिकृत करती हैं।

### कॉलम को ऑटोफिट करें और कार्यपुस्तिका सहेजें

#### चरण 7: कॉलम की चौड़ाई समायोजित करें और फ़ाइल सहेजें
```java
// सभी कॉलम स्वतः फिट करें.
worksheet.autoFitColumns();

// कार्यपुस्तिका को सहेजने के लिए आउटपुट निर्देशिका प्लेसहोल्डर पथ परिभाषित करें।
String outDir = "YOUR_OUTPUT_DIRECTORY";

// संशोधित कार्यपुस्तिका को निर्दिष्ट निर्देशिका में Excel फ़ाइल में सहेजें.
workbook.save(outDir + "/CSOrSColorsPieChart_out.xlsx", SaveFormat.XLSX);
```
अंत में, कॉलम को ऑटोफिट करें और अपनी कार्यपुस्तिका को सेव करें।

## व्यावहारिक अनुप्रयोगों
1. **जनसांख्यिकीय विश्लेषण**विभिन्न देशों या क्षेत्रों में जनसंख्या वितरण प्रदर्शित करने के लिए पाई चार्ट का उपयोग करें।
2. **बाजार हिस्सेदारी रिपोर्ट**किसी क्षेत्र में विभिन्न कंपनियों की बाजार हिस्सेदारी को चित्रित करें।
3. **बजट आवंटन**कल्पना करें कि किसी संगठन के विभिन्न विभागों में बजट किस प्रकार आवंटित किया जाता है।

ये अनुप्रयोग वास्तविक दुनिया परिदृश्यों में Aspose.Cells की बहुमुखी प्रतिभा और उपयोगिता को प्रदर्शित करते हैं।

## प्रदर्शन संबंधी विचार
Aspose.Cells का उपयोग करते समय प्रदर्शन को अनुकूलित करने के लिए:
- अब अनावश्यक वस्तुओं को हटाकर मेमोरी उपयोग को न्यूनतम करें।
- बड़े डेटासेट के प्रसंस्करण के लिए कुशल डेटा संरचनाओं का उपयोग करें।
- बाधाओं की पहचान करने के लिए अपने एप्लिकेशन का प्रोफाइल बनाएं।

सर्वोत्तम प्रथाओं का पालन करने से सुचारू और उत्तरदायी अनुप्रयोग सुनिश्चित होते हैं।

## निष्कर्ष
इस ट्यूटोरियल में आपको जावा में Aspose.Cells का उपयोग करके पाई चार्ट बनाने और उसे कस्टमाइज़ करने के चरणों के बारे में बताया गया है। इस ज्ञान के साथ, अब आप इन तकनीकों को अपने प्रोजेक्ट में विभिन्न डेटा विज़ुअलाइज़ेशन कार्यों पर लागू कर सकते हैं। आगे की खोज के लिए, Aspose.Cells के साथ उपलब्ध अतिरिक्त चार्ट प्रकारों और उन्नत अनुकूलन विकल्पों पर विचार करें।


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}