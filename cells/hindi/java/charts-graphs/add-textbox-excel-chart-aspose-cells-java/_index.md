---
date: '2026-04-05'
description: Aspose.Cells for Java के साथ Excel चार्ट में टेक्स्टबॉक्स जोड़ना सीखें,
  जिसमें वर्कबुक लोड करना और Java में Excel फ़ाइल सहेजना शामिल है।
keywords:
- how to add textbox
- save excel file java
- excel chart textbox
- load excel workbook java
- Aspose.Cells Java
title: Aspose.Cells Java का उपयोग करके Excel चार्ट में टेक्स्टबॉक्स कैसे जोड़ें
url: /hi/java/charts-graphs/add-textbox-excel-chart-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel चार्ट में TextBox जोड़ने के लिए Aspose.Cells Java का उपयोग कैसे करें

## परिचय

डेटा विज़ुअलाइज़ेशन की दुनिया में नेविगेट करना चुनौतीपूर्ण हो सकता है, विशेष रूप से जब आपको अपने Excel स्प्रेडशीट्स के चार्ट्स पर सीधे कस्टम टेक्स्ट एनोटेशन या लेबल जोड़ने की आवश्यकता हो। यह ट्यूटोरियल आपको Aspose.Cells for Java—एक मजबूत लाइब्रेरी जो इन कार्यों को सरल बनाती है—का उपयोग करके Excel चार्ट में एक TextBox को सहजता से एकीकृत करने में मार्गदर्शन करेगा।

**आप क्या सीखेंगे:**
- Aspose.Cells for Java के साथ Excel फ़ाइलों को लोड और संशोधित करना।
- Excel वर्कबुक में चार्ट ऑब्जेक्ट्स तक पहुंचना और उन्हें संशोधित करना।
- चार्ट पर एक TextBox कंट्रोल जोड़ना और कस्टमाइज़ करना।
- अपने बदलावों को वापस एक Excel फ़ाइल में सहेजना।

### त्वरित उत्तर
- **वर्कबुक लोड करने के लिए प्रमुख क्लास कौन सी है?** `Workbook` from `com.aspose.cells`.
- **कौन सा मेथड चार्ट में TextBox जोड़ता है?** `addTextBoxInChart` on the chart's shape collection.
- **क्या मैं TextBox का फ़िल रंग बदल सकता हूँ?** हाँ, `FillFormat` और `SolidFill` के माध्यम से।
- **संशोधित फ़ाइल को कैसे सहेजें?** चुने हुए `SaveFormat` के साथ `workbook.save` का उपयोग करें।
- **उत्पादन के लिए लाइसेंस की आवश्यकता है?** हाँ, एक व्यावसायिक लाइसेंस मूल्यांकन सीमाओं को हटा देता है।

## Excel चार्ट में TextBox कैसे जोड़ें

अब जब आप समग्र कार्यप्रवाह को समझते हैं, चलिए चरण‑दर‑चरण कार्यान्वयन में गहराई से उतरते हैं। प्रत्येक चरण में एक छोटा कोड स्निपेट (अपरिवर्तित) और यह क्या करता है, इसका स्पष्ट स्पष्टीकरण शामिल है।

## पूर्वापेक्षाएँ

- **आवश्यक लाइब्रेरीज़:** Aspose.Cells for Java संस्करण 25.3 या बाद का। यह ट्यूटोरियल Maven और Gradle सेटअप का उपयोग करता है।
- **पर्यावरण सेटअप:** आपके मशीन पर स्थापित एक संगत Java Development Kit (JDK)।
- **ज्ञान पूर्वापेक्षाएँ:** Java प्रोग्रामिंग की बुनियादी समझ और Excel फ़ाइल संरचनाओं की परिचितता।

## Aspose.Cells for Java सेटअप करना

अपने प्रोजेक्ट में Aspose.Cells का उपयोग करने के लिए, आपको इसे एक निर्भरता के रूप में जोड़ना होगा। Maven या Gradle का उपयोग करके इसे करने का तरीका यहाँ दिया गया है:

### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### लाइसेंस प्राप्ति

Aspose.Cells एक मुफ्त ट्रायल, विस्तारित परीक्षण के लिए अस्थायी लाइसेंस, और व्यावसायिक खरीद विकल्प प्रदान करता है:

- **फ़्री ट्रायल:** लाइब्रेरी डाउनलोड करके इसकी सुविधाओं के साथ प्रयोग शुरू करें।
- **अस्थायी लाइसेंस:** सीमाओं के बिना पूरी क्षमताओं का मूल्यांकन करने के लिए [यहाँ](https://purchase.aspose.com/temporary-license/) से प्राप्त करें।
- **खरीद:** उत्पादन वातावरण में निरंतर उपयोग के लिए, [Aspose Purchase](https://purchase.aspose.com/buy) पर लाइसेंस खरीदें।

### बुनियादी इनिशियलाइज़ेशन और सेटअप

लाइब्रेरी जोड़ने के बाद, यदि उपलब्ध हो तो अपने लाइसेंस के साथ इसे इनिशियलाइज़ करें:
```java
License license = new License();
license.setLicense("path/to/your/license/file.lic");
```

## कार्यान्वयन गाइड

अब हम Aspose.Cells for Java का उपयोग करके Excel चार्ट में TextBox जोड़ने की प्रक्रिया को समझेंगे। इस गाइड में प्रत्येक फीचर का विवरण दिया गया है।

### Excel फ़ाइल लोड करना

**सारांश:** हम अपने एप्लिकेशन में एक मौजूदा Excel फ़ाइल लोड करके शुरू करते हैं, जिससे हम प्रोग्रामेटिक रूप से उसकी सामग्री को संशोधित कर सकते हैं।

#### Step 1: Import Required Classes
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

#### Step 2: Load the Workbook
```java
String dataDir = "YOUR_DATA_DIRECTORY";
String filePath = dataDir + "/chart.xls";
Workbook workbook = new Workbook(filePath);
Worksheet worksheet = workbook.getWorksheets().get(0);
```
**व्याख्या:** `Workbook` क्लास एक Excel फ़ाइल को दर्शाता है। इसे लोड करने से सभी शीट्स और सामग्री तक पहुंच मिलती है।

### चार्ट ऑब्जेक्ट तक पहुंचना

**सारांश:** फ़ाइल लोड होने के बाद, हमें निर्दिष्ट वर्कशीट से चार्ट ऑब्जेक्ट प्राप्त करना होता है।

#### Step 3: Import Chart Class
```java
import com.aspose.cells.Chart;
```

#### Step 4: Access the First Chart
```java
Chart chart = worksheet.getCharts().get(0);
```
**व्याख्या:** यह आपके सक्रिय वर्कशीट में पहला चार्ट प्राप्त करता है जिससे आगे संशोधन किया जा सके।

### चार्ट में TextBox कंट्रोल जोड़ना

**सारांश:** अब, चलिए अपने चार्ट में एक कस्टमाइज़्ड TextBox जोड़ते हैं ताकि हम कोई भी टेक्स्ट एनोटेशन प्रदर्शित कर सकें।

#### Step 5: Import Required Classes
```java
import com.aspose.cells.TextBox;
import com.aspose.cells.FillFormat;
import com.aspose.cells.LineFormat;
import java.awt.Color;
import com.aspose.cells.MsoLineDashStyle;
```

#### Step 6: Add and Customize the TextBox
```java
TextBox txt = chart.getShapes().addTextBoxInChart(100, 100, 850, 2500);
txt.setText("Aspose");
txt.getFont().setItalic(true);
txt.getFont().setSize(20);
txt.getFont().setBold(true);

// Set Fill Format
FillFormat fillformat = txt.getFill();
fillformat.setFillType(FillFormat.FillType.SOLID);
fillformat.getSolidFill().setColor(Color.getSilver());

// Configure Line Format
LineFormat lineformat = txt.getLine();
lineformat.setWeight(2);
lineformat.setDashStyle(MsoLineDashStyle.SOLID);
```
**व्याख्या:** यह निर्दिष्ट कॉर्डिनेट्स पर एक TextBox जोड़ता है, उसके टेक्स्ट रूप को कस्टमाइज़ करता है, और फ़िल और लाइन स्टाइल लागू करता है।

### Excel फ़ाइल सहेजना

**सारांश:** अंत में, संशोधित वर्कबुक को वापस Excel फ़ाइल फ़ॉर्मेट में सहेजें।

#### Step 7: Import SaveFormat Class
```java
import com.aspose.cells.SaveFormat;
```

#### Step 8: Save the Workbook
```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "/ATBoxControl_out.xls", SaveFormat.EXCEL_97_TO_2003);
```
**व्याख्या:** वर्कबुक निर्दिष्ट डायरेक्टरी में सहेजा जाता है, जिससे निष्पादन के दौरान किए गए बदलाव संरक्षित रहते हैं।

## व्यावहारिक अनुप्रयोग

यहाँ कुछ वास्तविक‑दुनिया के परिदृश्य हैं जहाँ Excel चार्ट में TextBox जोड़ना लाभदायक हो सकता है:

1. **रिपोर्ट के लिए एनोटेशन:** चार्ट्स पर सीधे संदर्भ प्रदान करने या प्रमुख निष्कर्षों को उजागर करने के लिए टेक्स्ट बॉक्स का उपयोग करें।
2. **कस्टम लीजेंड और लेबल:** अतिरिक्त जानकारी या स्पष्टीकरण के साथ समझ को बढ़ाएँ जो मानक लीजेंड नहीं कवर कर सकते।
3. **ब्रांडिंग:** प्रस्तुतियों के लिए चार्ट्स में कंपनी लोगो या ब्रांडिंग स्टेटमेंट जोड़ें।

## प्रदर्शन संबंधी विचार

बड़े Excel फ़ाइलों के साथ काम करते समय, इन टिप्स पर विचार करें:

- **संसाधन उपयोग को अनुकूलित करें:** मेमोरी फुटप्रिंट को कम करने के लिए चार्ट संशोधनों और ऑब्जेक्ट निर्माण की संख्या को न्यूनतम रखें।
- **Java मेमोरी प्रबंधन:** उपयोग के बाद `Workbook` ऑब्जेक्ट्स को बंद करके संसाधनों को तुरंत मुक्त करने को सुनिश्चित करें।
- **कुशल डेटा हैंडलिंग:** बड़े डेटासेट्स से निपटते समय केवल आवश्यक भागों को ही वर्कबुक में लोड करें।

## Excel फ़ाइल को Java में कैसे सहेजें

अंतिम चरण—वर्कबुक सहेजना—**save excel file java** कार्यप्रवाह को दर्शाता है। वांछित `SaveFormat` निर्दिष्ट करके, आप लेगेसी `.xls`, आधुनिक `.xlsx`, या यहाँ तक कि CSV फ़ॉर्मेट में आउटपुट कर सकते हैं, जिससे आपको फ़ाइल प्रकार पर पूर्ण नियंत्रण मिलता है जो आपके डाउनस्ट्रीम प्रोसेस के लिए सबसे उपयुक्त हो।

## Excel वर्कबुक को Java में कैसे लोड करें

पहले `Workbook` इनिशियलाइज़ेशन में **load excel workbook java** पैटर्न दिखाया गया है। Aspose.Cells बाइनरी Excel संरचनाओं के पार्सिंग की जटिलता को सारांशित करता है, जिससे आप फ़ाइल I/O की जटिलताओं के बजाय बिज़नेस लॉजिक पर ध्यान केंद्रित कर सकते हैं।

## निष्कर्ष

हमने Aspose.Cells for Java का उपयोग करके Excel चार्ट में TextBox जोड़ने की प्रक्रिया को समझा। इस गाइड में पर्यावरण सेटअप, फ़ाइल लोड करना, चार्ट ऑब्जेक्ट्स तक पहुंचना, टेक्स्ट बॉक्स को कस्टमाइज़ करना, और अंतिम दस्तावेज़ सहेजना शामिल था।

**अगले कदम:** विभिन्न स्टाइल लागू करके या Aspose.Cells में उपलब्ध अन्य चार्ट प्रकारों को एक्सप्लोर करके आगे प्रयोग करें। अधिक उन्नत कार्यक्षमताओं के लिए उनकी डॉक्यूमेंटेशन देखें: [Aspose Reference](https://reference.aspose.com/cells/java/)।

## अक्सर पूछे जाने वाले प्रश्न

1. **क्या मैं चार्ट में कई TextBoxes जोड़ सकता हूँ?**
   - हाँ, आप विभिन्न कॉर्डिनेट्स के साथ आवश्यकतानुसार `addTextBoxInChart` मेथड को दोहरा सकते हैं।

2. **यदि मेरी Excel फ़ाइल में कोई चार्ट नहीं है तो क्या होगा?**
   - गैर‑मौजूद चार्ट तक पहुंचने का प्रयास करने पर एक एक्सेप्शन होगा। आगे बढ़ने से पहले सुनिश्चित करें कि आपके वर्कबुक में कम से कम एक चार्ट हो।

3. **क्या .xls के अलावा अन्य फ़ॉर्मेट में फ़ाइलें सहेजना संभव है?**
   - हाँ, आप अपनी आवश्यकता के अनुसार `XLSX` जैसे विभिन्न `SaveFormat` विकल्पों का उपयोग कर सकते हैं।

4. **फ़ाइल ऑपरेशन्स के दौरान एक्सेप्शन को कैसे संभालें?**
   - फ़ाइल लोडिंग और सहेजने के ऑपरेशन्स के आसपास try‑catch ब्लॉक्स लागू करके त्रुटियों को सुगमता से संभालें।

5. **क्या Aspose.Cells for Java को अन्य प्रोग्रामिंग भाषाओं के साथ उपयोग किया जा सकता है?**
   - जबकि यह गाइड Java पर केंद्रित है, Aspose.Cells .NET, C++, और अन्य के लिए भी उपलब्ध है। भाषा‑विशिष्ट गाइड्स के लिए उनकी [डॉक्यूमेंटेशन](https://reference.aspose.com/cells/java/) देखें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या TextBox जोड़ने से चार्ट के प्रदर्शन पर असर पड़ता है?**  
**उत्तर:** प्रभाव न्यूनतम है; हालांकि, बहुत बड़े वर्कबुक के लिए मेमोरी उपयोग कम रखने हेतु शेप ऑब्जेक्ट्स की संख्या सीमित रखें।

**प्रश्न: क्या मैं TextBox को पिक्सेल के बजाय सेल रेफ़रेंसेज़ से पोज़िशन कर सकता हूँ?**  
**उत्तर:** हाँ, आप सेल इंडेक्स से पिक्सेल कॉर्डिनेट्स की गणना कर सकते हैं या सेल‑आधारित पोज़िशनिंग के लिए वर्कशीट पर `addTextBox` मेथड का उपयोग कर सकते हैं।

**प्रश्न: क्या TextBox के टेक्स्ट को सेल वैल्यू से बाइंड करने का कोई तरीका है?**  
**उत्तर:** Aspose.Cells शेप्स के लिए सीधे डेटा बाइंडिंग प्रदान नहीं करता, लेकिन आप सेल वैल्यू पढ़ने के बाद प्रोग्रामेटिक रूप से TextBox टेक्स्ट को अपडेट कर सकते हैं।

**प्रश्न: व्यावसायिक डिप्लॉयमेंट के लिए कौन से लाइसेंस आवश्यक हैं?**  
**उत्तर:** खरीदा गया Aspose.Cells लाइसेंस सभी मूल्यांकन प्रतिबंधों को हटाता है और उत्पादन उपयोग के लिए आवश्यक है।

**प्रश्न: चार्ट मैनिपुलेशन के अधिक उदाहरण कहाँ मिल सकते हैं?**  
**उत्तर:** आधिकारिक Aspose.Cells डॉक्यूमेंटेशन और सैंपल रिपोजिटरी में कई परिदृश्य शामिल हैं, जैसे डायनामिक सीरीज़, चार्ट प्रकार, और स्टाइलिंग।

## संसाधन

- **डॉक्यूमेंटेशन:** व्यापक गाइड्स के लिए देखें: [Aspose Reference](https://reference.aspose.com/cells/java/)।
- **डाउनलोड:** नवीनतम लाइब्रेरी संस्करण प्राप्त करें: [Releases](https://releases.aspose.com/cells/java/)।
- **खरीद और ट्रायल विकल्प:** लाइसेंस प्राप्त करें या मुफ्त ट्रायल से शुरू करें: [Purchase Aspose](https://purchase.aspose.com/buy) और [Free Trial](https://releases.aspose.com/cells/java/)।
- **सपोर्ट:** सहायता के लिए समुदाय में जुड़ें: [Aspose Forum](https://forum.aspose.com/c/cells/9)।

इस गाइड का पालन करके, आप अपने Java प्रोजेक्ट्स में Aspose.Cells को कुशलता से इंटीग्रेट कर सकते हैं और कस्टम टेक्स्ट एनोटेशन के साथ Excel चार्ट कार्यक्षमताओं को बढ़ा सकते हैं। कोडिंग का आनंद लें!

---

**अंतिम अपडेट:** 2026-04-05  
**परीक्षित संस्करण:** Aspose.Cells Java 25.3  
**लेखक:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}