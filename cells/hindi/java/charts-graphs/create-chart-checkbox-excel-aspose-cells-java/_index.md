---
"date": "2025-04-07"
"description": "जानें कि Aspose.Cells for Java का उपयोग करके चेकबॉक्स के साथ इंटरैक्टिव चार्ट बनाकर अपनी Excel फ़ाइलों को कैसे बेहतर बनाया जाए। डेटा विज़ुअलाइज़ेशन को बेहतर बनाने के लिए इस चरण-दर-चरण मार्गदर्शिका का पालन करें।"
"title": "जावा के लिए Aspose.Cells का उपयोग करके चेकबॉक्स के साथ Excel में इंटरैक्टिव चार्ट बनाएं"
"url": "/hi/java/charts-graphs/create-chart-checkbox-excel-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# जावा के लिए Aspose.Cells का उपयोग करके चेकबॉक्स के साथ Excel में इंटरैक्टिव चार्ट बनाएं

## परिचय

एक्सेल में डेटा विज़ुअलाइज़ेशन और इंटरएक्टिविटी को बेहतर बनाने के लिए चार्ट में चेकबॉक्स जैसे डायनामिक एलिमेंट को शामिल किया जा सकता है। यह ट्यूटोरियल आपको जावा के लिए Aspose.Cells का उपयोग करके इंटरेक्टिव चार्ट बनाने में मार्गदर्शन करेगा, जो आपकी एक्सेल फ़ाइलों में कार्यक्षमता जोड़ने के लिए एकदम सही है।

**आप क्या सीखेंगे:**
- Java के लिए Aspose.Cells को कैसे सेट अप और उपयोग करें
- एक्सेल वर्कबुक बनाने और चार्ट सम्मिलित करने के चरण
- अपने चार्ट क्षेत्र में चेकबॉक्स जोड़ने के तरीके
- अपने संशोधनों को एक्सेल फ़ाइल में सहेजने की तकनीकें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास आवश्यक उपकरण और ज्ञान है।

## आवश्यक शर्तें

इस ट्यूटोरियल का अनुसरण करने के लिए, सुनिश्चित करें कि आपके पास ये हैं:
- **जावा डेवलपमेंट किट (JDK):** आपकी मशीन पर संस्करण 8 या उच्चतर स्थापित है।
- **जावा के लिए Aspose.Cells:** Aspose.Cells लाइब्रेरी का नवीनतम संस्करण। इस गाइड के लिए, हम संस्करण 25.3 का उपयोग करेंगे।
- **मावेन या ग्रेडेल:** निर्भरताओं को प्रबंधित करने के लिए अपने विकास परिवेश में सेटअप करें।

### ज्ञान पूर्वापेक्षाएँ

यद्यपि जावा प्रोग्रामिंग की बुनियादी समझ और एक्सेल फ़ाइल संरचनाओं से परिचित होना उपयोगी होगा, यह मार्गदर्शिका शुरुआती लोगों के लिए सभी आवश्यक विवरणों को शामिल करती है।

## Java के लिए Aspose.Cells सेट अप करना

Aspose.Cells को अपने प्रोजेक्ट में एकीकृत करना सरल है। आइए Maven या Gradle का उपयोग करके लाइब्रेरी सेट अप करके शुरू करें।

### मावेन का उपयोग करना

अपने में निम्नलिखित निर्भरता जोड़ें `pom.xml` फ़ाइल:

```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

### ग्रेडेल का उपयोग करना

इस पंक्ति को अपने में शामिल करें `build.gradle` फ़ाइल:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### लाइसेंस प्राप्ति चरण

Aspose.Cells की पूरी क्षमता का पता लगाने के लिए, एक अस्थायी या स्थायी लाइसेंस प्राप्त करने पर विचार करें। आप इसे यहाँ से डाउनलोड करके निःशुल्क परीक्षण के साथ शुरू कर सकते हैं [Aspose की वेबसाइट](https://releases.aspose.com/cells/java/)उत्पादन उपयोग के लिए, आप लाइसेंस खरीदना चाह सकते हैं या मूल्यांकन प्रयोजनों के लिए अस्थायी लाइसेंस का अनुरोध कर सकते हैं।

#### मूल आरंभीकरण

एक बार जब Aspose.Cells आपके प्रोजेक्ट में जुड़ जाए, तो इसे अपने जावा अनुप्रयोग में निम्न प्रकार से आरंभ करें:

```java
import com.aspose.cells.Workbook;

public class AsposeSetup {
    public static void main(String[] args) throws Exception {
        // वर्कबुक ऑब्जेक्ट को आरम्भ करें.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## कार्यान्वयन मार्गदर्शिका

अपने परिवेश को सेट अप करने के बाद, आइए Excel में एक चेकबॉक्स के साथ एक चार्ट बनाएं।

### कार्यपुस्तिका को इंस्टेंशिएट करें और चार्ट जोड़ें

#### अवलोकन

यह अनुभाग बताता है कि जावा के लिए Aspose.Cells का उपयोग करके Excel कार्यपुस्तिका कैसे बनाई जाए और कॉलम-प्रकार चार्ट कैसे जोड़ा जाए। चार्ट डेटा को प्रभावी ढंग से विज़ुअलाइज़ करने में मदद करते हैं, जिससे वे रिपोर्ट और डैशबोर्ड के लिए महत्वपूर्ण बन जाते हैं।

##### चरण 1: नई कार्यपुस्तिका बनाएँ

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SheetType;

public class ChartCreation {
    public static void main(String[] args) throws Exception {
        // एक Excel फ़ाइल का प्रतिनिधित्व करने वाले नए Workbook ऑब्जेक्ट को इन्स्टेन्शिएट करें.
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
        
        // कार्यपुस्तिका में चार्ट वर्कशीट जोड़ना.
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

        // नए जोड़े गए चार्ट वर्कशीट में COLUMN प्रकार का एक फ्लोटिंग चार्ट जोड़ें।
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        System.out.println("Column chart inserted.");
    }
}
```

##### चरण 4: श्रृंखला डेटा जोड़ें

```java
public class ChartCreation {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // COLUMN प्रकार का एक फ़्लोटिंग चार्ट जोड़ें.
        sheet.getCharts().addFloatingChart(ChartType.COLUMN, 0, 0, 1024, 960);

        // चार्ट के लिए श्रृंखला डेटा जोड़ना.
        sheet.getCharts().get(0).getNSeries().add("{1,2,3}", false);
        
        System.out.println("Series data added to the chart.");
    }
}
```

### चार्ट में चेकबॉक्स जोड़ें

#### अवलोकन

अपने एक्सेल चार्ट क्षेत्र में चेकबॉक्स एम्बेड करने से दृश्यता या अन्य सुविधाओं को गतिशील रूप से टॉगल करने की सुविधा मिलती है। यह अनुभाग आपको चार्ट में चेकबॉक्स एम्बेड करने के बारे में मार्गदर्शन करता है।

##### चरण 1: चेकबॉक्स आकार एम्बेड करें

```java
import com.aspose.cells.MsoDrawingType;
import com.aspose.cells.PlacementType;

public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // वर्कशीट के पहले चार्ट पर चार्ट क्षेत्र के भीतर एक चेकबॉक्स आकार जोड़ें।
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        
        System.out.println("Checkbox added to the chart.");
    }
}
```

##### चरण 2: चेकबॉक्स टेक्स्ट सेट करें

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // चार्ट के भीतर चेकबॉक्स आकार जोड़ें.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);

        // नये जोड़े गए चेकबॉक्स आकार के लिए पाठ सेट करना.
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        System.out.println("Checkbox labeled successfully.");
    }
}
```

### कार्यपुस्तिका को एक्सेल फ़ाइल के रूप में सहेजें

#### अवलोकन

एक बार जब आपका चार्ट और चेकबॉक्स कॉन्फ़िगर हो जाएं, तो अपने परिवर्तनों को बनाए रखने के लिए कार्यपुस्तिका को सहेजें।

```java
public class ChartWithCheckbox {
    public static void main(String[] args) throws Exception {
        Workbook workbook = new Workbook();
        int index = workbook.getWorksheets().add(SheetType.CHART);
        Worksheet sheet = workbook.getWorksheets().get(index);

        // चेकबॉक्स आकार जोड़ें और इसे लेबल करें.
        sheet.getCharts().get(0).getShapes().addShapeInChart(MsoDrawingType.CHECK_BOX, PlacementType.MOVE, 400, 400, 1000, 600);
        sheet.getCharts().get(0).getShapes().get(0).setText("CheckBox 1");

        // कार्यपुस्तिका सहेजें
        String outDir = "YOUR_OUTPUT_DIRECTORY"; // अपने वास्तविक आउटपुट निर्देशिका पथ से प्रतिस्थापित करें।
        workbook.save(outDir + "/InsertCheckboxInChartSheet_out.xlsx");
        
        System.out.println("Workbook saved successfully.");
    }
}
```

## व्यावहारिक अनुप्रयोगों

यहां कुछ वास्तविक दुनिया परिदृश्य दिए गए हैं जहां आप इस ट्यूटोरियल से प्राप्त ज्ञान को लागू कर सकते हैं:
1. **इंटरैक्टिव रिपोर्ट:** रिपोर्ट में डेटा श्रृंखला की दृश्यता को टॉगल करने के लिए चेकबॉक्स का उपयोग करें, जिससे उपयोगकर्ता इंटरैक्शन और अनुकूलन में वृद्धि हो।
2. **डेटा विश्लेषण:** तुलनात्मक विश्लेषण के लिए चार्ट में कुछ डेटा सेट को सक्षम या अक्षम करें, जिससे आपके डेटा के विशिष्ट पहलुओं पर ध्यान केंद्रित करना आसान हो जाएगा।
3. **शैक्षिक उपकरण:** गतिशील शिक्षण सामग्री बनाएं जहां छात्र चार्ट में विभिन्न विकल्पों का चयन करके सामग्री के साथ बातचीत कर सकें।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}