---
date: '2026-04-08'
description: Aspose.Cells for Java का उपयोग करके मार्कर्स के साथ लाइन चार्ट बनाना
  सीखें, चार्ट को वर्कशीट में जोड़ें, और स्वचालित रिपोर्टिंग के लिए Excel चार्ट को
  कस्टमाइज़ करें।
keywords:
- line chart with markers
- add chart to worksheet
- automate excel chart creation
- populate data for chart
- export styled chart excel
title: Aspose.Cells for Java का उपयोग करके मार्कर्स के साथ लाइन चार्ट बनाएं
url: /hi/java/charts-graphs/aspose-cells-java-excel-charts-creation/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java के साथ Excel चार्ट बनाना और स्टाइल करना

## परिचय

आज के डेटा‑चालित विश्व में, एक **line chart with markers** प्रवृत्तियों और अपवादों को दृश्य रूप में प्रस्तुत करने के सबसे प्रभावी तरीकों में से एक है। चाहे आप स्वचालित रिपोर्ट बना रहे हों या दैनिक रूप से अपडेट होने वाला डैशबोर्ड, एक worksheet में प्रोग्रामेटिक रूप से line chart with markers जोड़ना अनगिनत मैन्युअल चरणों को बचाता है। यह ट्यूटोरियल आपको Aspose.Cells for Java का उपयोग करके ऐसे चार्ट बनाने, स्टाइल करने और एक्सपोर्ट करने की प्रक्रिया दिखाता है, ताकि आप थकाऊ Excel कार्यों के बजाय अंतर्दृष्टियों पर ध्यान केंद्रित कर सकें।

**आप क्या सीखेंगे**
- Aspose.Cells का उपयोग करके एक workbook को इनिशियलाइज़ करना और डेटा से भरना।  
- **एक worksheet में line chart with markers जोड़ना** और उसकी उपस्थिति को कॉन्फ़िगर करना।  
- सीरीज़ के रंग, मार्कर्स और अन्य स्टाइलिंग विकल्पों को कस्टमाइज़ करना।  
- workbook को एक Excel फ़ाइल के रूप में सहेजना जिसमें आपका स्टाइल किया हुआ चार्ट शामिल हो।

## त्वरित उत्तर
- **शुरू करने के लिए मुख्य क्लास कौन सी है?** `Workbook` एक नई Excel फ़ाइल इनिशियलाइज़ करता है।  
- **कौन सा चार्ट प्रकार line chart with markers बनाता है?** `ChartType.LINE_WITH_DATA_MARKERS`.  
- **सीरीज़ पॉइंट्स के लिए कस्टम रंग कैसे सेट करें?** `chart.getNSeries().setColorVaried(true)` का उपयोग करें और मार्कर एरिया के रंग सेट करें।  
- **पूरा फ़ंक्शनलिटी के लिए लाइसेंस चाहिए?** हाँ, एक पेड या टेम्पररी Aspose.Cells लाइसेंस इवैल्यूएशन लिमिट्स को हटाता है।  
- **क्या मैं परिणाम को XLSX के रूप में एक्सपोर्ट कर सकता हूँ?** बिल्कुल—`workbook.save("StyledChart.xlsx")` एक XLSX फ़ाइल बनाता है।

## पूर्वापेक्षाएँ

Aspose.Cells for Java का उपयोग करके चार्ट बनाने और स्टाइल करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित सेटअप है:

### आवश्यक लाइब्रेरीज़

अपने प्रोजेक्ट में Aspose.Cells को एक डिपेंडेंसी के रूप में शामिल करें। यहाँ Maven और Gradle उपयोगकर्ताओं के लिए निर्देश दिए गए हैं:

**Maven:**
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

### पर्यावरण सेटअप आवश्यकताएँ
- आपके सिस्टम पर Java Development Kit (JDK) स्थापित होना चाहिए।  
- कोडिंग और टेस्टिंग के लिए IntelliJ IDEA या Eclipse जैसे Integrated Development Environment (IDE) का उपयोग।

### ज्ञान पूर्वापेक्षाएँ
Java प्रोग्रामिंग की बुनियादी समझ आवश्यक है, साथ ही Excel वर्कबुक और चार्टिंग अवधारणाओं की परिचितता भी।

### लाइसेंस प्राप्ति
Aspose.Cells एक व्यावसायिक उत्पाद है जिसके लिए पूर्ण कार्यक्षमता हेतु लाइसेंस आवश्यक है। आप इसकी सुविधाओं का मूल्यांकन करने के लिए मुफ्त ट्रायल प्राप्त कर सकते हैं, विस्तारित परीक्षण के लिए टेम्पररी लाइसेंस का अनुरोध कर सकते हैं, या दीर्घकालिक उपयोग के लिए उत्पाद खरीद सकते हैं।

- **फ्री ट्रायल:** [Download Free Trial](https://releases.aspose.com/cells/java/)  
- **टेम्पररी लाइसेंस:** [Request Temporary License](https://purchase.aspose.com/temporary-license/)  
- **खरीदें:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)

## Aspose.Cells for Java सेटअप

आवश्यक डिपेंडेंसीज़ स्थापित करने के बाद, Aspose.Cells का उपयोग करने के लिए अपने विकास पर्यावरण को सेटअप करें। लाइब्रेरी को इम्पोर्ट करके और अपने Java एप्लिकेशन में एक `Workbook` ऑब्जेक्ट इनिशियलाइज़ करके शुरू करें:

```java
import com.aspose.cells.*;

public class SetupAsposeCells {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook instance
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook initialized successfully!");
    }
}
```

## कार्यान्वयन गाइड

इस सेक्शन में, हम कार्यान्वयन को विभिन्न फीचर्स में विभाजित करेंगे: Workbook Initialization और Data Population, Chart Creation और Configuration, Series Customization, तथा Workbook Saving।

### फीचर 1: Workbook Initialization और Data Population

**Overview:** यह फीचर एक नया workbook बनाने, उसकी पहली worksheet तक पहुँचने, और चार्ट निर्माण के लिए डेटा से भरने पर केंद्रित है।

#### चरण 1: Workbook को इनिशियलाइज़ करें
`Workbook` ऑब्जेक्ट को इंस्टैंसिएट करके शुरू करें:

```java
import com.aspose.cells.*;

public class FeatureWorkbookInitialization {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

#### चरण 2: कॉलम शीर्षक सेट करें और डेटा भरें
कॉलम हेडर को परिभाषित करें और नमूना डेटा के साथ पंक्तियों को भरें:

```java
        // Set columns title 
        worksheet.getCells().get(0, 0).setValue("X");
        worksheet.getCells().get(0, 1).setValue("Y");

        // Create random data for series 1
        for (int i = 1; i < 21; i++) {
            worksheet.getCells().get(i, 0).setValue(i);
            worksheet.getCells().get(i, 1).setValue(0.8);
        }

        // Create random data for series 2
        for (int i = 21; i < 41; i++) {
            worksheet.getCells().get(i, 0).setValue(i - 20);
            worksheet.getCells().get(i, 1).setValue(0.9);
        }
    }
}
```

### फीचर 2: Chart Creation और Configuration

**Overview:** यह फीचर दिखाता है कि workbook की worksheet में चार्ट कैसे जोड़ें, उसकी शैली सेट करें, और बुनियादी प्रॉपर्टीज़ को कॉन्फ़िगर करें।

#### चरण 3: Worksheet में चार्ट जोड़ें
डेटा मार्कर्स के साथ एक line chart जोड़ें:

```java
import com.aspose.cells.*;

public class FeatureChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add chart to the worksheet
        int idx = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20);

        // Access and configure the chart
        Chart chart = worksheet.getCharts().get(idx);
        chart.setStyle(3); // Set a predefined style
        chart.setAutoScaling(true);
        chart.getTitle().setText("Sample Chart");
        chart.getCategoryAxis().getTitle().setText("Units");
    }
}
```

### फीचर 3: Series Configuration और Customization

**Overview:** विभिन्न रंगों और मार्कर शैलियों जैसी सीरीज़ सेटिंग्स को कस्टमाइज़ करके अपने चार्ट की दृश्य आकर्षण बढ़ाएँ।

#### चरण 4: Series सेटिंग्स को कस्टमाइज़ करें
सीरीज़ डेटा को कॉन्फ़िगर करें, कस्टम फॉर्मेटिंग लागू करें, और मार्कर्स को समायोजित करें:

```java
import com.aspose.cells.*;

public class FeatureSeriesConfiguration {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        
        // Add series to the chart
        Chart chart = worksheet.getCharts().add(ChartType.LINE_WITH_DATA_MARKERS, 1, 3, 20, 20).get(0);

        int s2_idx = chart.getNSeries().add("A2: A21", true);
        int s3_idx = chart.getNSeries().add("A22: A41", true);

        // Enable varied colors for series points
        chart.getNSeries().setColorVaried(true);

        // Customize first series marker styles and colors
        chart.getNSeries().get(s2_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s2_idx).getMarker().getArea().setForegroundColor(Color.getYellow());
        chart.getNSeries().get(s2_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the first series
        chart.getNSeries().get(s2_idx).setXValues("A2: A21");
        chart.getNSeries().get(s2_idx).setValues("B2: B21");

        // Customize second series marker styles and colors
        chart.getNSeries().get(s3_idx).getArea().setFormatting(FormattingType.CUSTOM);
        chart.getNSeries().get(s3_idx).getMarker().getArea().setForegroundColor(Color.getGreen());
        chart.getNSeries().get(s3_idx).getMarker().getBorder().setVisible(false);

        // Set X and Y values for the second series
        chart.getNSeries().get(s3_idx).setXValues("A22: A41");
        chart.getNSeries().get(s3_idx).setValues("B22: B41");
    }
}
```

### फीचर 4: Workbook Saving

**Overview:** अंत में, workbook को सहेजें ताकि आपके बदलाव संरक्षित रहें और चार्ट Excel फ़ाइल में शामिल हो।

#### चरण 5: Workbook को सहेजें
नए बनाए गए चार्ट्स के साथ अपना workbook सहेजें:

```java
import com.aspose.cells.*;

public class FeatureWorkbookSaving {
    public static void main(String[] args) throws Exception {
        // Instantiate a workbook
        Workbook workbook = new Workbook();
        
        // Access first worksheet and add data, chart configuration as per previous steps...
        Worksheet worksheet = workbook.getWorksheets().get(0);
        // (Implementation of adding data and configuring the chart would be here)

        // Save the workbook to an Excel file
        workbook.save("StyledChart.xlsx");
    }
}
```

### सामान्य समस्याएँ और ट्रबलशूटिंग
- **Chart खाली दिख रहा है:** सुनिश्चित करें कि `setXValues` और `setValues` में उपयोग किए गए सेल रेंज सही ढंग से भरे हुए सेल्स को संदर्भित कर रहे हैं।  
- **रंग लागू नहीं हो रहे:** व्यक्तिगत सीरीज़ को कस्टमाइज़ करने से पहले `chart.getNSeries().setColorVaried(true)` को कॉल किया गया है यह सुनिश्चित करें।  
- **License त्रुटियाँ:** ट्रायल लाइसेंस चार्ट की संख्या को सीमित कर सकता है; प्रतिबंध हटाने के लिए पूर्ण लाइसेंस इंस्टॉल करें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं Aspose.Cells के साथ अन्य चार्ट प्रकार (जैसे, बार, पाई) बना सकता हूँ?**  
A: हाँ, Aspose.Cells विभिन्न प्रकार के चार्ट सपोर्ट करता है; बस `ChartType.LINE_WITH_DATA_MARKERS` को इच्छित enum वैल्यू से बदल दें।

**Q: क्या मुझे workbook को बंद करने या रिसोर्सेज़ रिलीज़ करने की जरूरत है?**  
A: `Workbook` क्लास रिसोर्सेज़ को ऑटोमैटिकली मैनेज करती है, लेकिन आप लंबी अवधि चलने वाले एप्लिकेशन में मेमोरी मुक्त करने के लिए `workbook.dispose()` कॉल कर सकते हैं।

**Q: क्या एक ही worksheet में कई चार्ट जोड़ना संभव है?**  
A: बिल्कुल—जिस चार्ट को आप जोड़ना चाहते हैं, उसके लिए `worksheet.getCharts().add(...)` कॉल करें।

**Q: फ़ाइल को पुराने Excel फ़ॉर्मेट (XLS) में कैसे एक्सपोर्ट करें?**  
A: `workbook.save("StyledChart.xls", SaveFormat.EXCEL_97_TO_2003);` का उपयोग करें।

**Q: क्या चार्ट Microsoft Excel में खोलने पर अपनी स्टाइलिंग बरकरार रखेगा?**  
A: हाँ, Aspose.Cells नेटिव Excel चार्ट ऑब्जेक्ट लिखता है, इसलिए सभी स्टाइल, रंग और मार्कर ठीक वैसा ही दिखेंगे जैसा परिभाषित किया गया है।

---

**अंतिम अपडेट:** 2026-04-08  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}