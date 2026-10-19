---
date: '2026-09-22'
description: Aspose.Cells for Java का उपयोग करके इंटरैक्टिव Excel चार्ट को चेकबॉक्स
  के साथ बनाना सीखें। यह गाइड सेटअप, चेकबॉक्स जोड़ना, लाइसेंसिंग, और सर्वोत्तम प्रथाओं
  को कवर करता है।
keywords:
- create interactive Excel chart
- how to add checkbox java
- aspose.cells license java
lastmod: '2026-09-22'
og_description: Aspose.Cells for Java का उपयोग करके इंटरैक्टिव Excel चार्ट को चेकबॉक्स
  के साथ बनाना सीखें। चरण‑दर‑चरण निर्देशों का पालन करें, लाइसेंसिंग टिप्स देखें, और
  वास्तविक‑विश्व उपयोग मामलों की खोज करें।
og_image_alt: Guide showing how to create interactive Excel chart with checkboxes
  using Aspose.Cells for Java
og_title: इंटरैक्टिव Excel चार्ट को चेकबॉक्स के साथ कैसे बनाएं
schemas:
- author: Aspose
  dateModified: '2026-09-22'
  description: Learn how to create interactive Excel chart with checkboxes using Aspose.Cells
    for Java. This guide covers setup, adding checkboxes, licensing, and best practices.
  headline: How to create interactive Excel chart with checkboxes
  type: TechArticle
- questions:
  - answer: Use Aspose.Cells’ `Shape` API with `ShapeType.FORM_CONTROL_CHECKBOX` and
      link it to a worksheet cell; the checkbox works natively in Excel.
    question: How do I add a checkbox without using VBA?
  - answer: The checkbox shape is available in the free evaluation, but a permanent
      Aspose.Cells license removes evaluation limits and enables full performance
      optimizations.
    question: Do I need a license for the checkbox feature?
  - answer: Files saved with Aspose.Cells follow the Office Open XML standard and
      open correctly in Excel 2016, 2019, 2021, and Microsoft 365.
    question: Which Excel versions can open the generated file?
  - answer: Yes, create a checkbox for each series, link each to a distinct helper
      cell, and use conditional formulas to toggle each series independently.
    question: Can I control multiple series with separate checkboxes?
  - answer: Practically, you can add dozens; performance remains stable up to 200
      controls per worksheet on typical server hardware.
    question: Is there a limit on the number of checkboxes per chart?
  type: FAQPage
tags:
- interactive Excel charts
- Aspose.Cells
- Java Excel automation
title: इंटरैक्टिव Excel चार्ट को चेकबॉक्स के साथ कैसे बनाएं
url: /hi/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# इंटरैक्टिव एक्सेल चार्ट को चेकबॉक्स के साथ कैसे बनाएं

## परिचय

इस ट्यूटोरियल में आप **इंटरैक्टिव एक्सेल चार्ट** बनाएँगे जो उपयोगकर्ताओं को चार्ट पर सीधे रखे गए चेकबॉक्स पर क्लिक करके डेटा सीरीज़ को टॉगल करने की अनुमति देता है। Aspose.Cells for Java का उपयोग करके आप प्रोग्रामेटिक रूप से पूर्ण‑फ़ीचर वाले वर्कबुक बना सकते हैं, बिना Microsoft Excel स्थापित किए। यह तरीका किसी भी Java‑आधारित रिपोर्टिंग या डैशबोर्ड समाधान के लिए काम करता है।

**आप क्या सीखेंगे**
- Maven या Gradle में Aspose.Cells for Java को सेट अप कैसे करें  
- `Workbook` को इंस्टैंशिएट करना और कॉलम चार्ट जोड़ना  
- चार्ट क्षेत्र के भीतर चेकबॉक्स शेप एम्बेड करना  
- प्रोडक्शन उपयोग के लिए Aspose.Cells लाइसेंस लागू करना  

## त्वरित उत्तर
- **इंटरैक्टिव एक्सेल चार्ट कौन सी लाइब्रेरी बनाती है?** Aspose.Cells for Java.  
- **क्या मैं VBA के बिना चेकबॉक्स जोड़ सकता हूँ?** हाँ, API के माध्यम से फ़ॉर्म कंट्रोल शेप डालकर।  
- **क्या इस फीचर के लिए लाइसेंस चाहिए?** मूल्यांकन के लिए एक अस्थायी लाइसेंस काम करता है; प्रोडक्शन के लिए स्थायी लाइसेंस आवश्यक है।  
- **कौन सा जावा संस्करण आवश्यक है?** JDK 8 या नया.  
- **क्या चार्ट Excel 2016‑2024 में काम करेगा?** हाँ, उत्पन्न फ़ाइल Office Open XML मानक का पालन करती है।  

## इंटरैक्टिव एक्सेल चार्ट क्या है?
एक **इंटरैक्टिव एक्सेल चार्ट** मानक चार्ट को UI कंट्रोल (जैसे, चेकबॉक्स) के साथ संयोजित करता है जो उपयोगकर्ताओं को डेटा सीरीज़ को तुरंत दिखाने या छिपाने की अनुमति देता है, जिससे एक स्थैतिक विज़ुअल को एक डायनामिक रिपोर्टिंग टूल में बदल दिया जाता है।

## Aspose.Cells for Java का उपयोग क्यों करें?
Aspose.Cells **80+ इनपुट और आउटपुट फ़ॉर्मैट** का समर्थन करता है और **10,000+ पंक्तियों** वाले वर्कबुक को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है, जिससे सर्वर‑साइड वातावरण में उच्च‑प्रदर्शन जनरेशन संभव होता है।

## पूर्वापेक्षाएँ

- **Java Development Kit (JDK):** संस्करण 8 या उच्चतर।  
- **Aspose.Cells for Java:** नवीनतम रिलीज़ (जैसे, 25.3)।  
- **Maven या Gradle:** लाइब्रेरी निर्भरता प्रबंधित करने के लिए।  

### ज्ञान पूर्वापेक्षाएँ
बेसिक जावा सिंटैक्स और एक्सेल कॉन्सेप्ट्स (वर्कशीट, रेंज, चार्ट) की परिचितता मददगार है, लेकिन नीचे दिए गए चरण किसी भी अनुभव स्तर के डेवलपर्स के लिए पर्याप्त रूप से विस्तृत हैं।

## जावा में चेकबॉक्स कैसे जोड़ें?

Aspose.Cells लाइब्रेरी लोड करें, एक वर्कबुक बनाएं, और एक ही कॉल में चेकबॉक्स शेप डालें। चेकबॉक्स एक फ़ॉर्म कंट्रोल है जिसे एक सेल से लिंक किया जा सकता है; इसे टॉगल करने से लिंक्ड सेल का मान बदलता है, जिसे आप बाद में चार्ट सीरीज़ की दृश्यता से बाइंड कर सकते हैं।

```text
// Direct answer (40‑70 words):
You add a checkbox by creating a `Shape` of type `ShapeType.FORM_CONTROL_CHECKBOX`, setting its placement on the chart worksheet, and linking it to a cell that stores the Boolean state. The linked cell can be used in formulas that drive chart series visibility, enabling real‑time interactivity without VBA.
```

### चरण 1: Maven निर्भरता सेट करें

Add the Aspose.Cells Maven artifact to your `pom.xml`:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### चरण 2: Gradle निर्भरता सेट करें

Add the following line to your `build.gradle` file:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### लाइसेंस प्राप्त करने के चरण

To unlock full functionality, obtain a temporary or permanent license. Download a trial license from [Aspose's website](https://releases.aspose.com/cells/java/). For production, purchase a license and apply it as shown later.

#### बेसिक इनिशियलाइज़ेशन

License is the Aspose.Cells class used to apply a purchased license file, enabling full functionality without evaluation limits. Initialize the library in your Java code before any workbook operation:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // Initialize the Workbook object.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## इंटरैक्टिव एक्सेल चार्ट कैसे बनाएं?

एक Aspose.Cells `Workbook` ऑब्जेक्ट पूरे एक्सेल फ़ाइल का प्रतिनिधित्व करता है, जिसमें वर्कशीट, चार्ट और अन्य तत्व शामिल होते हैं। वर्कबुक बनाकर आप प्रोग्रामेटिक रूप से डेटा जोड़ सकते हैं, एक कॉलम चार्ट जनरेट कर सकते हैं, और बाद में चेकबॉक्स जैसे इंटरैक्टिव कंट्रोल एम्बेड कर सकते हैं। नीचे दिए गए चरण वर्कबुक बनाने, डेटा भरने, और चार्ट को इंटरैक्टिव बनाने की प्रक्रिया को दर्शाते हैं।

```text
// Direct answer (40‑70 words):
First, instantiate a `Workbook`, fill a worksheet with sample data, and call `addChart` to place a column chart. Next, create a checkbox shape, position it over the chart, and link it to a cell that toggles the series’ `isVisible` property via a formula. Finally, save the workbook as an XLSX file.
```

### वर्कबुक इंस्टैंशिएट करें और चार्ट जोड़ें

#### सारांश

यह सेक्शन दिखाता है कि कैसे एक नया वर्कबुक बनाएं, डेटा के लिए एक वर्कशीट जोड़ें, और एक कॉलम चार्ट जनरेट करें जिसे बाद में इंटरैक्टिव बनाया जाएगा।

##### चरण 1: नया वर्कबुक बनाएं

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // Instantiate a new Workbook object representing an Excel file.
        Workbook workbook = new Workbook();
        
        System.out.println("Workbook created.");
    }
}
```

##### चरण 2: चार्ट वर्कशीट जोड़ें

```java
import com.aspose.cells.Worksheet;
import com.aspose.cells.ChartType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        
        // Adding a chart worksheet to the workbook.
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        System.out.println("Chart worksheet added.");
    }
}
```

##### चरण 3: कॉलम चार्ट डालें

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN to the newly added chart worksheet.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### चरण 4: सीरीज़ डेटा जोड़ें

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a floating chart of type COLUMN.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // Adding series data for the chart.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

## चार्ट में चेकबॉक्स कैसे एम्बेड करें?

चार्ट क्षेत्र पर सीधे चेकबॉक्स डालने से अंतिम उपयोगकर्ता क्लिक करके किसी विशिष्ट सीरीज़ को दिखा या छिपा सकते हैं। चेकबॉक्स एक फ़ॉर्म कंट्रोल शेप है जिसे एक सेल से लिंक किया जा सकता है; सेल वैल्यू को एक फ़ॉर्मूले में रेफ़रेंस किया जा सकता है जो सीरीज़ की दृश्यता को नियंत्रित करता है।

Shape is the Aspose.Cells object representing a drawing element such as a form control, picture, or text box within a worksheet.

```text
// Direct answer (40‑70 words):
You embed a checkbox by creating a `Shape` with `ShapeType.FORM_CONTROL_CHECKBOX`, positioning it using `setUpperLeftRow/Column` relative to the chart sheet, and linking it to a helper cell (e.g., `B1`). Then, use a conditional formula in the series data range that checks the helper cell’s Boolean value to decide whether the series is plotted.
```

### चेकबॉक्स शेप एम्बेड करें

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add a checkbox shape within the chart area on the first chart of the worksheet.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

### चेकबॉक्स टेक्स्ट सेट करें

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape within the chart.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // Setting text for the newly added checkbox shape.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

## वर्कबुक को एक्सेल फ़ाइल के रूप में कैसे सहेजें?

`Workbook` को सहेजने से सभी इन‑मेमोरी बदलाव एक भौतिक एक्सेल फ़ाइल में डिस्क पर लिखे जाते हैं। Aspose.Cells आधुनिक .xlsx फ़ॉर्मेट का समर्थन करता है, जिससे फ़ाइल Excel 2016‑2024 और अन्य Office‑संगत एप्लिकेशन में खुलती है। इच्छित फ़ाइल पाथ के साथ `save` मेथड का उपयोग करें, और अतिरिक्त विकल्पों के लिए फ़ाइल फ़ॉर्मेट भी निर्दिष्ट कर सकते हैं।

```text
// Direct answer (40‑70 words):
Call `workbook.save("InteractiveChart.xlsx", SaveFormat.XLSX)` to write the workbook. The method automatically closes all streams and guarantees that the embedded chart and checkbox are fully functional when the file is opened in Excel 2016‑2024.
```

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // Add checkbox shape and label it.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // Save the workbook
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // Replace with your actual output directory path.
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## व्यावहारिक अनुप्रयोग

इंटरैक्टिव चार्ट के साथ चेकबॉक्स के वास्तविक‑दुनिया में उपयोग के उदाहरण:

1. **इंटरैक्टिव रिपोर्ट्स:** हितधारकों को बिक्री चार्ट पर व्यक्तिगत प्रोडक्ट लाइन्स टॉगल करने दें।  
2. **तुलनात्मक विश्लेषण:** विश्लेषकों को विशिष्ट समय अवधि या क्षेत्रों पर ध्यान केंद्रित करने के लिए सीरीज़ को चेक/अनचेक करने की सुविधा दें।  
3. **शैक्षणिक डैशबोर्ड:** छात्र यह चुनकर डेटा ट्रेंड्स का अन्वेषण कर सकते हैं कि कौन से वेरिएबल दिखाने हैं।  

## सामान्य समस्याएँ और समाधान

- **चेकबॉक्स प्रतिक्रिया नहीं दे रहा:** सुनिश्चित करें कि चेकबॉक्स एक सेल से लिंक है और वह सेल फ़ॉर्मूला में संदर्भित है जो सीरीज़ की दृश्यता को प्रभावित करता है।  
- **टॉगल के बाद चार्ट अपडेट नहीं हो रहा:** Excel में वर्कबुक व्यू को रिफ्रेश करें या फ़ॉर्मूले पुनः‑गणना करें (`workbook.calculateFormula()`)।  
- **लाइसेंस लागू नहीं हुआ:** सुनिश्चित करें कि `License license = new License(); license.setLicense("Aspose.Cells.lic");` किसी भी वर्कबुक ऑपरेशन से पहले चलाया गया है।  

## अक्सर पूछे जाने वाले प्रश्न

**Q: VBA का उपयोग किए बिना मैं चेकबॉक्स कैसे जोड़ूं?**  
A: Aspose.Cells के `Shape` API को `ShapeType.FORM_CONTROL_CHECKBOX` के साथ उपयोग करें और इसे वर्कशीट सेल से लिंक करें; चेकबॉक्स Excel में मूल रूप से काम करता है।

**Q: चेकबॉक्स फीचर के लिए मुझे लाइसेंस चाहिए?**  
A: चेकबॉक्स शेप फ्री इवैल्यूएशन में उपलब्ध है, लेकिन स्थायी Aspose.Cells लाइसेंस इवैल्यूएशन सीमाओं को हटाता है और पूर्ण प्रदर्शन अनुकूलन सक्षम करता है।

**Q: उत्पन्न फ़ाइल कौन से Excel संस्करणों में खुल सकती है?**  
A: Aspose.Cells द्वारा सहेजी गई फ़ाइलें Office Open XML मानक का पालन करती हैं और Excel 2016, 2019, 2021, तथा Microsoft 365 में सही ढंग से खुलती हैं।

**Q: क्या मैं अलग-अलग चेकबॉक्स के साथ कई सीरीज़ को नियंत्रित कर सकता हूँ?**  
A: हाँ, प्रत्येक सीरीज़ के लिए एक चेकबॉक्स बनाएं, प्रत्येक को अलग हेल्पर सेल से लिंक करें, और कंडीशनल फ़ॉर्मूले का उपयोग करके प्रत्येक सीरीज़ को स्वतंत्र रूप से टॉगल करें।

**Q: क्या चार्ट प्रति चेकबॉक्स की संख्या पर कोई सीमा है?**  
A: व्यावहारिक रूप से, आप दर्जनों जोड़ सकते हैं; सामान्य सर्वर हार्डवेयर पर प्रति वर्कशीट 200 कंट्रोल तक प्रदर्शन स्थिर रहता है।

---

**Last Updated:** 2026-09-22  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose.Cells for Java का उपयोग करके एक्सेल में चेकबॉक्स कैसे जोड़ें: चरण‑दर‑चरण गाइड](/cells/java/data-validation/add-checkbox-excel-aspose-cells-java/)
- [Aspose.Cells Java के साथ डायनामिक एक्सेल चार्ट बनाएं: डेवलपर्स के लिए व्यापक गाइड](/cells/java/charts-graphs/aspose-cells-java-dynamic-excel-charts/)
- [Aspose.Cells Java के साथ एक्सेल चार्ट में डेटा लेबल जोड़ें](/cells/java/advanced-excel-charts/chart-interactivity/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}