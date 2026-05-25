---
date: '2026-04-08'
description: Aspose.Cells का उपयोग करके जावा में कॉलम चार्ट बनाना सीखें, जिसमें चार्ट
  जावा बनाना, चार्ट शीट जोड़ना और वर्कबुक एक्सेल निर्यात करना शामिल है।
keywords:
- generate column chart
- create chart java
- add chart sheet
- populate excel cells
- set chart title
- export workbook excel
title: Aspose.Cells जावा ट्यूटोरियल के साथ कॉलम चार्ट बनाएं
url: /hi/java/charts-graphs/aspose-cells-java-create-customize-charts/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java के साथ कॉलम चार्ट बनाएं

आज के डेटा‑चालित अनुप्रयोगों में, **कॉलम चार्ट बनाना** तेज़ी से और प्रोग्रामेटिक रूप से कच्चे नंबरों को स्पष्ट दृश्य अंतर्दृष्टियों में बदल सकता है। चाहे आप रिपोर्टिंग डैशबोर्ड, एनालिटिक्स टूल, या एक साधारण एक्सपोर्ट फीचर बना रहे हों, Aspose.Cells for Java आपको एक सहज API प्रदान करता है जिससे आप **create chart java** प्रोजेक्ट्स को Excel UI के बिना बना सकते हैं। इस ट्यूटोरियल में आप सीखेंगे कि लाइब्रेरी कैसे सेट अप करें, **Excel सेल्स भरें**, एक **चार्ट शीट** जोड़ें, **चार्ट शीर्षक** को कस्टमाइज़ करें, और अंत में **वर्कबुक एक्सेल निर्यात** को फ़ाइल में करें।

## त्वरित उत्तर
- **“generate column chart” क्या मतलब है?** यह टेबल डेटा से एक ऊर्ध्वर बार‑प्रकार का विज़ुअलाइज़ेशन बनाता है।  
- **कौनसी लाइब्रेरी आवश्यक है?** Aspose.Cells for Java (free trial उपलब्ध)।  
- **क्या मुझे Excel इंस्टॉल करना आवश्यक है?** नहीं, लाइब्रेरी Microsoft Excel से स्वतंत्र रूप से काम करती है।  
- **क्या मैं XLS के अलावा अन्य फ़ॉर्मेट में निर्यात कर सकता हूँ?** हाँ – PDF, PNG, SVG आदि, `workbook.save()` के माध्यम से।  
- **क्या उत्पादन के लिए लाइसेंस अनिवार्य है?** हाँ, खरीदा गया या अस्थायी लाइसेंस आवश्यक है।

## generate column chart क्या है?
कॉलम चार्ट डेटा श्रृंखलाओं को ऊर्ध्वर बार के रूप में प्रदर्शित करता है, जिससे क्षेत्रों, महीनों, या उत्पाद लाइनों जैसी श्रेणियों में मानों की तुलना आसान हो जाती है। Aspose.Cells आपको यह चार्ट पूरी तरह कोड में बनाने की सुविधा देता है, जिससे आप डेटा, स्टाइलिंग, और आउटपुट फ़ॉर्मेट पर पूर्ण नियंत्रण रख सकते हैं।

## Aspose.Cells का उपयोग करके chart java क्यों बनाएं?
- **No COM interop** – किसी भी OS पर JVM के साथ काम करता है।  
- **Rich styling options** – इमेजेज़, ग्रेडिएंट्स, लेजेंड्स, और कस्टम फ़ॉन्ट्स।  
- **High performance** – बड़े डेटा सेट्स के लिए उपयुक्त।  
- **Multiple export formats** – XLS, XLSX, PDF, PNG, और अधिक।

## आवश्यकताएँ
- **Java Development Kit (JDK) 8+** स्थापित है।  
- बुनियादी Java ज्ञान और Excel अवधारणाओं की परिचितता।

### आवश्यक लाइब्रेरीज़
नीचे दिए गए स्निपेट्स में से एक का उपयोग करके अपने प्रोजेक्ट में Aspose.Cells जोड़ें।

#### Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

#### Gradle
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### लाइसेंस प्राप्ति
Aspose व्यापक परीक्षण के लिए एक फ्री ट्रायल और एक अस्थायी लाइसेंस प्रदान करता है।
- **फ़्री ट्रायल**: [फ़्री डाउनलोड](https://releases.aspose.com/cells/java/)  
- **अस्थायी लाइसेंस**: [यहाँ अनुरोध करें](https://purchase.aspose.com/temporary-license/)

## Aspose.Cells for Java सेट अप करना

पहले, एक `Workbook` इंस्टेंस बनाएं – यह हमारे डेटा और चार्ट के लिए कैनवास होगा।

```java
import com.aspose.cells.Workbook;

// Initialize a new Workbook
Workbook workbook = new Workbook();
```

## चरण‑दर‑चरण गाइड

### 1. वर्कशीट बनाएं और नाम दें
हम कच्चा डेटा **Data** नामक शीट में रखेंगे।

```java
import com.aspose.cells.Worksheet;

// Create a new Workbook instance
Workbook workbook = new Workbook();
```

```java
// Access the first worksheet and set its name to "Data"
Worksheet sheet = workbook.getWorksheets().get(0);
sheet.setName("Data");
```

### 2. Excel सेल्स भरें
ऐसे क्षेत्र नाम और बिक्री आंकड़े डालें जिन्हें कॉलम चार्ट विज़ुअलाइज़ करेगा।

```java
import com.aspose.cells.Cells;

// Get the cells collection from the "Data" sheet
Cells cells = sheet.getCells();
```

```java
// Insert region names and sales figures
cells.get("A1").putValue("Region");
cells.get("B1").putValue("Sale");

String[] regions = {"France", "Germany", "England", "Sweden", "Italy", "Spain", "Portugal"};
int[] sales = {70000, 55000, 30000, 40000, 35000, 32000, 10000};

for (int i = 0; i < regions.length; i++) {
    cells.get("A" + (i+2)).putValue(regions[i]);
    cells.get("B" + (i+2)).putValue(sales[i]);
}
```

### 3. चार्ट शीट जोड़ें
चार्ट को कच्चे डेटा से अलग रखने से वर्कबुक साफ़-सुथरा रहता है।

```java
import com.aspose.cells.SheetType;

// Add a new chart sheet
int sheetIndex = workbook.getWorksheets().add(SheetType.CHART);
Worksheet chartSheet = workbook.getWorksheets().get(sheetIndex);

// Name the worksheet "Chart"
chartSheet.setName("Chart");
```

### 4. कॉलम चार्ट बनाएं
अब हम वास्तव में **कॉलम चार्ट बनाते** हैं।

```java
import com.aspose.cells.Chart;
import com.aspose.cells.ChartType;

// Add a new column chart to the "Chart" sheet
int chartIndex = chartSheet.getCharts().add(ChartType.COLUMN, 1, 1, 25, 10);
Chart chart = chartSheet.getCharts().get(chartIndex);
```

### 5. प्लॉट एरिया में पृष्ठभूमि भरने के लिए चित्र सेट करें
एक पृष्ठभूमि छवि चार्ट को अधिक आकर्षक बना सकती है।

```java
import java.io.FileInputStream;
import com.aspose.cells.Color;

String dataDir = "YOUR_DATA_DIRECTORY";
File file = new FileInputStream(dataDir + "aspose-logo.png");
byte[] data = new byte[(int)file.length()];
file.read(data);

chart.getPlotArea().getArea().getFillFormat().setImageData(data);
chart.getPlotArea().getBorder().setVisible(false);
```

### 6. चार्ट शीर्षक सेट करें
**चार्ट शीर्षक सेट करें** को कस्टमाइज़ करने से पठनीयता बढ़ती है।

```java
// Configure the chart's title properties
chart.getTitle().setText("Sales By Region");
chart.getTitle().getFont().setColor(Color.getBlue());
chart.getTitle().getFont().setBold(true);
chart.getTitle().getFont().setSize(12);
```

### 7. सीरीज़ डेटा और लेजेंड कॉन्फ़िगर करें
डेटा रेंज को चार्ट से लिंक करें और लेजेंड की स्थिति निर्धारित करें।

```java
// Set series and category data for the chart
chart.getNSeries().add("Data!B2:B8", true);
chart.getNSeries().setCategoryData("Data!A2:A8");
chart.getNSeries().setColorVaried(true);

// Position the legend at the top of the chart
import com.aspose.cells.Legend;
import com.aspose.cells.LegendPositionType;

Legend legend = chart.getLegend();
legend.setPosition(LegendPositionType.TOP);
```

### 8. वर्कबुक एक्सेल निर्यात करें
अंत में, **वर्कबुक एक्सेल निर्यात** को एक XLS फ़ाइल (या किसी भी समर्थित फ़ॉर्मेट) में करें।

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
workbook.save(outDir + "SPAsBFillInChart_out.xls");
```

## व्यावहारिक अनुप्रयोग
- **Business Reports** – मासिक PDFs के लिए बिक्री चार्ट स्वचालित रूप से बनाएं।  
- **Data Analysis Tools** – कस्टम एनालिटिक्स डैशबोर्ड में डायनामिक चार्ट एम्बेड करें।  
- **Enterprise Dashboards** – रियल‑टाइम मॉनिटरिंग के लिए चार्ट इमेजेज़ को तुरंत रिफ्रेश करें।

## प्रदर्शन संबंधी विचार
- बड़े डेटा सेट्स के साथ काम करते समय बैच सेल अपडेट करें ताकि ओवरहेड कम हो।  
- यदि आप लूप में कई वर्कबुक प्रोसेस कर रहे हैं तो संसाधन रिलीज़ करें (`workbook.dispose()`)।

## सामान्य समस्याएँ और समाधान
- **Image not showing** – फ़ाइल पाथ और इमेज फ़ॉर्मेट (PNG, JPEG) सपोर्टेड है या नहीं, जांचें।  
- **Chart appears blank** – सुनिश्चित करें कि डेटा रेंज रेफ़रेंसेज़ (`Data!B2:B8`) भरें गए सेल्स से मेल खाते हैं।  
- **Out‑of‑memory errors** – डेटा को हिस्सों में प्रोसेस करें और बड़े सेव्स के बाद `System.gc()` कॉल करें।

## अक्सर पूछे जाने वाले प्रश्न

**Q: कॉलम चार्ट में कई सीरीज़ कैसे जोड़ें?**  
A: विभिन्न डेटा रेंज के साथ `chart.getNSeries().add()` को बार‑बार कॉल करें, उदाहरण के लिए, दूसरे सीरीज़ के लिए `"Data!C2:C8"`।

**Q: क्या मैं एक्सिस लेबल बदल सकता हूँ?**  
A: हाँ। `chart.getCategoryAxis().setTitle("Regions")` और `chart.getValueAxis().setTitle("Sales")` का उपयोग करें।

**Q: XLS के अलावा कौन‑से फ़ॉर्मेट में निर्यात कर सकता हूँ?**  
A: PDF के लिए `workbook.save("chart.pdf")`, PNG के लिए `workbook.save("chart.png")`, या XLSX के लिए `workbook.save("chart.xlsx")` का उपयोग करें।

**Q: विकास बिल्ड्स के लिए लाइसेंस आवश्यक है?**  
A: मूल्यांकन के लिए फ्री ट्रायल काम करता है, लेकिन उत्पादन डिप्लॉयमेंट के लिए स्थायी या अस्थायी लाइसेंस आवश्यक है।

**Q: हजारों पंक्तियों के लिए रेंडरिंग स्पीड कैसे बढ़ाएँ?**  
A: `cells.importArray()` का उपयोग करके सेल्स भरें और सभी डेटा लोड होने के बाद चार्ट बनाकर चार्ट री‑ड्रॉ को कम करें।

---

**अंतिम अपडेट:** 2026-04-08  
**परीक्षण किया गया:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  

## संसाधन

- [Aspose.Cells दस्तावेज़ीकरण](https://reference.aspose.com/cells/java/)  
- [Aspose.Cells डाउनलोड करें](https://releases.aspose.com/cells/java/)  
- [लाइसेंस खरीदें](https://purchase.aspose.com/buy)  
- [फ़्री ट्रायल](https://releases.aspose.com/cells/java/)  
- [अस्थायी लाइसेंस अनुरोध](https://purchase.aspose.com/temporary-license/)  
- [सपोर्ट फ़ोरम](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}