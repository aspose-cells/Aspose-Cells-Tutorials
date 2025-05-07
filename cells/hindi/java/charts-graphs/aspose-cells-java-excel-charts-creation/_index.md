---
"date": "2025-04-07"
"description": "Java के लिए Aspose.Cells का उपयोग करके Excel में चार्ट बनाना और उन्हें कस्टमाइज़ करना सीखें। इस विस्तृत गाइड के साथ चार्ट निर्माण को स्वचालित करें, डेटा विज़ुअलाइज़ेशन को बेहतर बनाएँ और समय बचाएँ।"
"title": "Aspose.Cells Java के साथ Excel चार्ट बनाना और स्टाइल करना एक व्यापक गाइड"
"url": "/hi/java/charts-graphs/aspose-cells-java-excel-charts-creation/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells Java के साथ Excel चार्ट बनाना और स्टाइल करना

## परिचय

आज की डेटा-संचालित दुनिया में, विश्लेषण और निर्णय लेने के लिए प्रभावी सूचना विज़ुअलाइज़ेशन महत्वपूर्ण है। अक्सर, एक्सेल वर्कबुक में प्रोग्रामेटिक रूप से गतिशील चार्ट बनाने की आवश्यकता होती है - खासकर जब बड़े डेटासेट या स्वचालित रिपोर्टिंग सिस्टम से निपटना होता है। यह ट्यूटोरियल प्रदर्शित करता है कि एक्सेल में चार्ट को सहजता से बनाने और कस्टमाइज़ करने के लिए जावा के लिए Aspose.Cells का उपयोग कैसे करें। अपने जावा अनुप्रयोगों में Aspose.Cells को एकीकृत करके, आप चार्ट निर्माण को स्वचालित कर सकते हैं, डेटा प्रस्तुति को बढ़ा सकते हैं और समय बचा सकते हैं।

**आप क्या सीखेंगे:**
- Aspose.Cells का उपयोग करके कार्यपुस्तिका को आरंभ करना और उसमें डेटा भरना।
- डेटा मार्करों के साथ लाइन चार्ट बनाना और कॉन्फ़िगर करना।
- बेहतर दृश्य के लिए श्रृंखला के स्वरूप और रंगों को अनुकूलित करना।
- नव निर्मित चार्ट के साथ कार्यपुस्तिका को एक्सेल प्रारूप में सहेजना।

आइये, आरंभ करने के लिए आवश्यक पूर्वापेक्षाओं पर चर्चा से शुरुआत करें।

## आवश्यक शर्तें

Aspose.Cells for Java का उपयोग करके चार्ट बनाने और स्टाइल करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित सेटअप है:

### आवश्यक पुस्तकालय
अपने प्रोजेक्ट में निर्भरता के रूप में Aspose.Cells को शामिल करें। यहाँ Maven और Gradle दोनों उपयोगकर्ताओं के लिए निर्देश दिए गए हैं:

**मावेन:**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**ग्रेडेल:**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### पर्यावरण सेटअप आवश्यकताएँ
- आपके सिस्टम पर जावा डेवलपमेंट किट (JDK) स्थापित है।
- कोडिंग और परीक्षण के लिए एक एकीकृत विकास वातावरण (आईडीई) जैसे कि इंटेलीज आईडिया या एक्लिप्स।

### ज्ञान पूर्वापेक्षाएँ
जावा प्रोग्रामिंग की बुनियादी समझ के साथ-साथ एक्सेल वर्कबुक और चार्टिंग अवधारणाओं से परिचित होना आवश्यक है। 

### लाइसेंस अधिग्रहण
Aspose.Cells एक व्यावसायिक उत्पाद है जिसे पूर्ण कार्यक्षमता के लिए लाइसेंस की आवश्यकता होती है। आप इसकी विशेषताओं का मूल्यांकन करने के लिए एक निःशुल्क परीक्षण प्राप्त कर सकते हैं, विस्तारित परीक्षण के लिए एक अस्थायी लाइसेंस का अनुरोध कर सकते हैं, या दीर्घकालिक उपयोग के लिए उत्पाद खरीद सकते हैं।

- **मुफ्त परीक्षण:** [निःशुल्क परीक्षण डाउनलोड करें](https://releases.aspose.com/cells/java/)
- **अस्थायी लाइसेंस:** [अस्थायी लाइसेंस का अनुरोध करें](https://purchase.aspose.com/temporary-license/)
- **खरीदना:** [Aspose.Cells खरीदें](https://purchase.aspose.com/buy)

## Java के लिए Aspose.Cells सेट अप करना

एक बार जब आप आवश्यक निर्भरताएँ स्थापित कर लें, तो Aspose.Cells का उपयोग करने के लिए अपने विकास वातावरण को सेट करें। लाइब्रेरी को आयात करके और अपने जावा एप्लिकेशन में वर्कबुक ऑब्जेक्ट को आरंभ करके शुरू करें:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // एक नई कार्यपुस्तिका इंस्टैंस आरंभ करें
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## कार्यान्वयन मार्गदर्शिका

इस अनुभाग में, हम कार्यान्वयन को अलग-अलग विशेषताओं में विभाजित करेंगे: कार्यपुस्तिका आरंभीकरण और डेटा जनसंख्या, चार्ट निर्माण और कॉन्फ़िगरेशन, श्रृंखला अनुकूलन, और कार्यपुस्तिका सहेजना।

### विशेषता 1: कार्यपुस्तिका आरंभीकरण और डेटा जनसंख्या

**अवलोकन:** यह सुविधा एक नई कार्यपुस्तिका बनाने, उसकी पहली कार्यपत्रक तक पहुंचने और चार्ट निर्माण के लिए उसमें डेटा भरने पर केंद्रित है।

#### चरण 1: कार्यपुस्तिका को आरंभ करें
एक उदाहरण बनाकर शुरू करें `Workbook` वस्तु:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // कार्यपुस्तिका को इंस्टैंसिएट करें
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुंचें
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### चरण 2: कॉलम शीर्षक सेट करें और डेटा भरें
स्तंभ शीर्षलेख परिभाषित करें और पंक्तियों को नमूना डेटा से भरें:

```java
        // कॉलम शीर्षक सेट करें 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // श्रृंखला 1 के लिए यादृच्छिक डेटा बनाएँ
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // श्रृंखला 2 के लिए यादृच्छिक डेटा बनाएँ
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### विशेषता 2: चार्ट निर्माण और कॉन्फ़िगरेशन

**अवलोकन:** यह सुविधा दर्शाती है कि कार्यपुस्तिका की वर्कशीट में चार्ट कैसे जोड़ें, इसकी शैली कैसे सेट करें, तथा बुनियादी गुणों को कैसे कॉन्फ़िगर करें।

#### चरण 3: वर्कशीट में चार्ट जोड़ें
डेटा मार्कर के साथ लाइन चार्ट जोड़ें:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // कार्यपुस्तिका को इंस्टैंसिएट करें
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुंचें
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // वर्कशीट में चार्ट जोड़ें
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // चार्ट तक पहुँचें और उसे कॉन्फ़िगर करें
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // पूर्वनिर्धारित शैली सेट करें
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### विशेषता 3: श्रृंखला कॉन्फ़िगरेशन और अनुकूलन

**अवलोकन:** विभिन्न रंगों और मार्कर शैलियों जैसी श्रृंखला सेटिंग्स को अनुकूलित करके अपने चार्ट के दृश्य आकर्षण को बढ़ाएं।

#### चरण 4: श्रृंखला सेटिंग अनुकूलित करें
श्रृंखला डेटा कॉन्फ़िगर करें, कस्टम फ़ॉर्मेटिंग लागू करें, और मार्कर समायोजित करें:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // कार्यपुस्तिका को इंस्टैंसिएट करें
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुंचें
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // चार्ट में श्रृंखला जोड़ें
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // श्रृंखला बिंदुओं के लिए विविध रंग सक्षम करें
        chart.getNSeries().setColorVaried(true);

        // पहली श्रृंखला मार्कर शैलियों और रंगों को अनुकूलित करें
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // पहली श्रृंखला के लिए X और Y मान सेट करें
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // दूसरी श्रृंखला मार्कर शैलियों और रंगों को अनुकूलित करें
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // दूसरी श्रृंखला के लिए X और Y मान सेट करें
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### विशेषता 4: कार्यपुस्तिका सहेजना

**अवलोकन:** अंत में, अपने परिवर्तनों को बनाए रखने के लिए कार्यपुस्तिका को सहेजें और सुनिश्चित करें कि चार्ट एक्सेल फ़ाइल में शामिल है।

#### चरण 5: कार्यपुस्तिका सहेजें
अपनी कार्यपुस्तिका को नए बनाए गए चार्ट के साथ सहेजें:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // कार्यपुस्तिका को इंस्टैंसिएट करें
        Workbook workbook = new Workbook();
        
        // पहले वर्कशीट तक पहुंचें और पिछले चरणों के अनुसार डेटा, चार्ट कॉन्फ़िगरेशन जोड़ें...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (डेटा जोड़ने और चार्ट को कॉन्फ़िगर करने का कार्यान्वयन यहां होगा)

        // कार्यपुस्तिका को Excel फ़ाइल में सहेजें
        workbook.save("StyledChart.xlsx");
    }
}
```

**कीवर्ड अनुशंसाएँ:**
- "Aspose.Cells for Java"
- "जावा के साथ एक्सेल चार्ट निर्माण"
- "एक्सेल स्वचालन के लिए जावा प्रोग्रामिंग"

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}