---
date: '2026-03-31'
description: Aspose.Cells for Java का उपयोग करके Excel चार्ट में लेबल्स को री‑साइज़
  करना सीखें, जिससे Excel चार्ट लेबल्स स्वचालित रूप से समायोजित हो जाएँ और परिपूर्ण
  फिट व पठनीयता प्राप्त हो।
keywords:
- auto-resize chart data labels
- Aspose.Cells for Java
- Excel charts customization
title: Aspose.Cells for Java के साथ Excel चार्ट में लेबल का आकार बदलने का तरीका
url: /hi/java/charts-graphs/aspose-cells-java-auto-resize-chart-data-labels/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for Java के साथ Excel चार्ट में लेबल का आकार कैसे बदलें

## परिचय

यदि आप **लेबल का आकार कैसे बदलें** Excel चार्ट में खोज रहे हैं, तो आप सही जगह पर आए हैं। यह ट्यूटोरियल आपको Aspose.Cells for Java का उपयोग करके चार्ट डेटा लेबल शैप्स को स्वचालित रूप से री‑साइज़ करने के माध्यम से लेबल को उनके कंटेनर में पूरी तरह फिट करने का तरीका दिखाता है। इस गाइड के अंत तक आप Excel चार्ट लेबल को जल्दी से समायोजित कर पाएँगे, पठनीयता में सुधार करेंगे, और मैन्युअल ट्यूनिंग के बिना परिष्कृत रिपोर्ट बना पाएँगे।

**आप क्या सीखेंगे**
- अपने प्रोजेक्ट में Aspose.Cells for Java को सेट अप कैसे करें।
- Excel चार्ट लेबल को स्वचालित रूप से **resize excel chart labels** करने के सटीक चरण।
- वास्तविक दुनिया के परिदृश्य जहाँ ऑटो‑रिसाइज़िंग समय बचाता है।
- बड़े वर्कबुक या जटिल चार्ट्स के लिए प्रदर्शन टिप्स।

## त्वरित उत्तर
- **“लेबल का आकार कैसे बदलें” का क्या अर्थ है?** यह चार्ट डेटा लेबल के आकार को स्वचालित रूप से समायोजित करने को दर्शाता है ताकि टेक्स्ट बिना कटे फिट हो सके।  
- **कौन सी लाइब्रेरी इसे संभालती है?** Aspose.Cells for Java `setResizeShapeToFitText` प्रॉपर्टी प्रदान करता है।  
- **क्या मुझे लाइसेंस चाहिए?** परीक्षण के लिए ट्रायल काम करता है; उत्पादन के लिए पूर्ण लाइसेंस आवश्यक है।  
- **क्या यह सभी चार्ट प्रकारों पर काम करेगा?** हाँ—कॉलम, बार, पाई, लाइन और अधिक समर्थित हैं।  
- **क्या इसका प्रदर्शन पर प्रभाव पड़ेगा?** न्यूनतम; बदलाव के बाद बस `chart.calculate()` कॉल करें।

## ऑटो‑रिसाइज़िंग चार्ट डेटा लेबल क्या है?
ऑटो‑रिसाइज़िंग चार्ट डेटा लेबल एक फीचर है जो लेबल के बाउंडिंग बॉक्स को डायनामिक रूप से विस्तारित या संकुचित करता है ताकि उसमें मौजूद टेक्स्ट की लंबाई के अनुसार फिट हो सके। यह ट्रंकेटेड या ओवरलैपिंग लेबल की सामान्य समस्या को समाप्त करता है, विशेषकर जब विभिन्न संख्यात्मक फ़ॉर्मेट या लंबे कैटेगरी नाम हों।

## Excel चार्ट लेबल को क्यों समायोजित करें?
- **पठनीयता:** कटे हुए नंबरों को रोकता है और सुनिश्चित करता है कि हर डेटा पॉइंट दिखे।  
- **पेशेवर लुक:** डैशबोर्ड और रिपोर्ट को मैन्युअल एडिट के बिना परिष्कृत बनाता है।  
- **समय बचत:** एक दोहरावदार फ़ॉर्मेटिंग कार्य को स्वचालित करता है, विशेषकर बैच‑जनरेटेड रिपोर्ट में उपयोगी।

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) 8 या उससे ऊपर।  
- IntelliJ IDEA, Eclipse, या VS Code जैसे IDE।  
- बेसिक Java ज्ञान और Excel फ़ाइल हैंडलिंग की परिचितता।  

## Aspose.Cells for Java सेट अप करना

### स्थापना जानकारी

Maven या Gradle के माध्यम से अपने प्रोजेक्ट में Aspose.Cells जोड़ें।

**Maven**
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### लाइसेंस प्राप्ति

Aspose अपनी लाइब्रेरीज़ की क्षमताओं को परीक्षण करने के लिए एक मुफ्त ट्रायल प्रदान करता है:
1. **Free Trial**: 30 दिनों के लिए [this link](https://releases.aspose.com/cells/java/) से एक टेम्पररी लाइसेंस डाउनलोड करें।  
2. **Temporary License**: अधिक समय के लिए एक्सेस अनुरोध करें [purchase page](https://purchase.aspose.com/temporary-license/) के माध्यम से।  
3. **Purchase**: निरंतर उपयोग के लिए, [Aspose purchase page](https://purchase.aspose.com/buy) से पूर्ण लाइसेंस खरीदने पर विचार करें।

### बेसिक इनिशियलाइज़ेशन और सेटअप

एक बार Aspose.Cells आपके प्रोजेक्ट में जोड़ दिया गया, तो इसे अपने Java एप्लिकेशन में इनिशियलाइज़ करें:

```java
import com.aspose.cells.Workbook;

public class InitializeAspose {
    public static void main(String[] args) throws Exception {
        // Create a new Workbook instance or open an existing one
        Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
        
        // Save the modified Excel file
        workbook.save("output/path/output_file.xlsx");
    }
}
```

## इम्प्लीमेंटेशन गाइड

### ऑटो‑रिसाइज़िंग चार्ट डेटा लेबल

नीचे वह स्टेप‑बाय‑स्टेप कोड है जिसकी आपको **resize excel chart labels** स्वचालित रूप से करने के लिए आवश्यकता है।

#### 1️⃣ वर्कबुक लोड करें

```java
import com.aspose.cells.Workbook;
import AsposeCellsExamples.Utils;

public class ResizeChartDataLabelShapeToFitText {
    public static void main(String[] args) throws Exception {
        // Define the directory of your document
        String dataDir = Utils.getSharedDataDir(ResizeChartDataLabelShapeToFitText.class) + "TechnicalArticles/";
        
        // Load an existing workbook containing charts
        Workbook book = new Workbook(dataDir + "report.xlsx");
    }
}
```

#### 2️⃣ चार्ट्स और डेटा लेबल्स तक पहुंचें

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartCollection;

public class ResizeChartDataLabelShapeToFitText {
    public static void main(String[] args) throws Exception {
        // (Load workbook code here...)
        
        // Access the first worksheet in the workbook
        Worksheet sheet = book.getWorksheets().get(0);
        
        // Get all charts from the worksheet
        ChartCollection charts = sheet.getCharts();

        for (int chartIndex = 0; chartIndex < charts.getCount(); chartIndex++) {
            com.aspose.cells.Chart chart = charts.get(chartIndex);
            
            // Process each series in the chart
            for (int seriesIndex = 0; seriesIndex < chart.getNSeries().getCount(); seriesIndex++) {
                DataLabels labels = chart.getNSeries().get(seriesIndex).getDataLabels();
                
                // Enable auto‑resizing of data label shape to fit text
                labels.setResizeShapeToFitText(true);
            }
            
            // Recalculate the chart after changes
            chart.calculate();
        }
    }
}
```

#### 3️⃣ संशोधित वर्कबुक सहेजें

```java
public class ResizeChartDataLabelShapeToFitText {
    public static void main(String[] args) throws Exception {
        // (Previous code...)
        
        // Save the workbook to a new file
        book.save(dataDir + "RCDLabelShapeToFitText_out.xlsx");
    }
}
```

### समस्या निवारण टिप्स
- **Chart Not Updating:** लेबल प्रॉपर्टीज़ बदलने के बाद `chart.calculate()` कॉल किया है यह सुनिश्चित करें।  
- **License Limitations:** यदि आप फीचर प्रतिबंधों का सामना करते हैं, तो अपने लाइसेंस फ़ाइल को सही से लोड किया है या पूर्ण एक्सेस के लिए टेम्पररी लाइसेंस पर स्विच किया है, यह दोबारा जांचें।

## व्यावहारिक अनुप्रयोग

यहाँ सामान्य परिदृश्य हैं जहाँ **लेबल का आकार कैसे बदलें** आवश्यक हो जाता है:

1. **Financial Reports** – मुद्रा मान और प्रतिशत लंबाई में भिन्न होते हैं; ऑटो‑रिसाइज़िंग लेआउट को साफ़ रखता है।  
2. **Sales Dashboards** – प्रोडक्ट नाम लंबे हो सकते हैं; यह फीचर सुनिश्चित करता है कि हर लेबल पठनीय रहे।  
3. **Academic Research** – जटिल डेटासेट अक्सर असमान लेबल लंबाई उत्पन्न करते हैं; स्वचालित समायोजन मैन्युअल फ़ॉर्मेटिंग में घंटों बचाता है।

## प्रदर्शन विचार

बड़े वर्कबुक के साथ काम करते समय:

- **Memory Management:** जब ऑब्जेक्ट्स की आवश्यकता न रहे तो (`workbook.dispose()`) उन्हें डिस्पोज़ करें।  
- **Batch Processing:** हीप उपयोग को अत्यधिक बढ़ने से बचाने के लिए चार्ट्स को छोटे समूहों में प्रोसेस करें।  
- **Stay Updated:** नवीनतम Aspose.Cells संस्करण का उपयोग करें ताकि प्रदर्शन सुधार और बग फिक्सेस मिल सकें।

## सामान्य समस्याएँ और समाधान

| समस्या | कारण | समाधान |
|-------|-------|----------|
| लेबल का आकार वही रहता है | `setResizeShapeToFitText` नहीं बुलाया गया | प्रत्येक सीरीज़ के लिए प्रॉपर्टी `true` पर सेट है, यह सुनिश्चित करें। |
| सहेजने के बाद चार्ट खाली दिखाई देता है | लाइसेंस लागू नहीं किया गया | वर्कबुक खोलने से पहले वैध लाइसेंस लोड करें। |
| बड़े फाइलों पर प्रोसेसिंग धीमी | सभी चार्ट्स को एक साथ प्रोसेस करना | चार्ट्स को बैच में प्रोसेस करें या JVM हीप साइज बढ़ाएँ। |

## अक्सर पूछे जाने वाले प्रश्न

**Q: चार्ट डेटा लेबल का आकार बदलने का मुख्य उपयोग केस क्या है?**  
A: उन चार्ट्स में पठनीयता बढ़ाने के लिए जहाँ लेबल की लंबाई अलग‑अलग होती है, जिससे ट्रंकेशन या ओवरलैपिंग रोका जा सके।

**Q: क्या मैं इसे हर चार्ट प्रकार पर लागू कर सकता हूँ?**  
A: हाँ, Aspose.Cells कॉलम, बार, पाई, लाइन और कई अन्य चार्ट प्रकारों को सपोर्ट करता है।

**Q: क्या ऑटो‑रिसाइज़िंग का प्रदर्शन पर महत्वपूर्ण प्रभाव पड़ता है?**  
A: प्रभाव न्यूनतम है; मुख्य ओवरहेड `chart.calculate()` कॉल है, जो किसी भी चार्ट संशोधन के लिए आवश्यक है।

**Q: उत्पादन के लिए लाइसेंस अनिवार्य है क्या?**  
A: हाँ, ट्रायल अवधि के बाद उत्पादन डिप्लॉयमेंट के लिए पूर्ण Aspose.Cells लाइसेंस आवश्यक है।

**Q: क्या मैं इस फीचर को प्रोग्रामेटिकली बनाए गए चार्ट्स पर उपयोग कर सकता हूँ?**  
A: बिल्कुल। चार्ट जनरेट करने के बाद वही `setResizeShapeToFitText(true)` कॉल लागू करें।

## संसाधन

- [Aspose.Cells दस्तावेज़ीकरण](https://reference.aspose.com/cells/java/)  
- [Aspose.Cells for Java डाउनलोड करें](https://releases.aspose.com/cells/java/)  
- [लाइसेंस खरीदें](https://purchase.aspose.com/buy)  
- [Free Trial](https://releases.aspose.com/cells/java/)  
- [Temporary License Request](https://purchase.aspose.com/temporary-license/)  
- [Aspose सपोर्ट फ़ोरम](https://forum.aspose.com/c/cells/9)

---

**अंतिम अपडेट:** 2026-03-31  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}