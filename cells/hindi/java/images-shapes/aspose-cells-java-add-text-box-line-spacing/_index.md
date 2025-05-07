---
"date": "2025-04-08"
"description": "Excel कार्यपुस्तिकाओं में टेक्स्ट बॉक्स जोड़ने और लाइन स्पेसिंग सेट करने के लिए Java के लिए Aspose.Cells का उपयोग करना सीखें। स्टाइल किए गए टेक्स्ट आकृतियों के साथ अपनी कार्यपुस्तिका प्रस्तुतियों को बेहतर बनाएँ।"
"title": "जावा के लिए Aspose.Cells का उपयोग करके Excel में टेक्स्ट बॉक्स जोड़ें और लाइन स्पेसिंग सेट करें"
"url": "/hi/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# जावा के लिए Aspose.Cells का उपयोग करके Excel में टेक्स्ट बॉक्स जोड़ें और लाइन स्पेसिंग सेट करें

## परिचय

डायनेमिक एक्सेल रिपोर्ट बनाने के लिए अक्सर कस्टम टेक्स्ट फ़ॉर्मेटिंग की आवश्यकता होती है, जैसे कि विशिष्ट लाइन स्पेसिंग के साथ टेक्स्ट बॉक्स जोड़ना। Aspose.Cells for Java के साथ, यह सरल और कुशल हो जाता है। यह ट्यूटोरियल आपको स्टाइल किए गए टेक्स्ट शेप जोड़ने के लिए Aspose.Cells for Java का उपयोग करके अपनी वर्कबुक प्रेजेंटेशन को बेहतर बनाने के बारे में मार्गदर्शन करेगा।

इस गाइड के अंत तक आप सीखेंगे कि कैसे:
- एक नई Excel कार्यपुस्तिका बनाएँ और उसकी कार्यपत्रिकाओं तक पहुँचें
- वर्कशीट में टेक्स्ट बॉक्स आकार जोड़ें
- टेक्स्ट आकृति के अंदर कस्टम लाइन स्पेसिंग सेट करें
- अपनी स्वरूपित कार्यपुस्तिका को XLSX प्रारूप में सहेजें

आइये, अपने परिवेश की स्थापना से शुरुआत करें।

### आवश्यक शर्तें

आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
- आपकी मशीन पर जावा डेवलपमेंट किट (JDK) स्थापित है
- जावा कोड लिखने के लिए एक IDE या संपादक
- निर्भरताओं को प्रबंधित करने के लिए कॉन्फ़िगर किया गया Maven या Gradle बिल्ड सिस्टम

जावा प्रोग्रामिंग की बुनियादी समझ और एक्सेल फ़ाइल संरचनाओं से परिचित होना लाभदायक होगा।

## Java के लिए Aspose.Cells सेट अप करना

Maven या Gradle का उपयोग करके अपने प्रोजेक्ट के निर्भरता प्रबंधन में Aspose.Cells को शामिल करें:

**मावेन**

अपने में निम्नलिखित निर्भरता ब्लॉक जोड़ें `pom.xml` फ़ाइल:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**ग्रैडल**

इसे अपने में शामिल करें `build.gradle` फ़ाइल:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

इसके बाद, निःशुल्क परीक्षण का विकल्प चुनकर, अस्थायी लाइसेंस का अनुरोध करके, या पूर्ण लाइसेंस खरीदकर Aspose.Cells के लिए लाइसेंस प्राप्त करें।

### Aspose.Cells आरंभ करना

एक बार जब लाइब्रेरी आपके प्रोजेक्ट में शामिल हो जाए, तो इसे अपने जावा एप्लिकेशन में आरंभ करें:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // वर्कबुक का एक उदाहरण आरंभ करें (यह एक एक्सेल फ़ाइल को दर्शाता है)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## कार्यान्वयन मार्गदर्शिका

### कार्यपुस्तिका और एक्सेस वर्कशीट बनाएं

एक नई एक्सेल वर्कबुक बनाकर और उसकी पहली वर्कशीट एक्सेस करके शुरुआत करें। यहीं पर आप अपना टेक्स्ट बॉक्स जोड़ेंगे।

#### अवलोकन

नई कार्यपुस्तिका बनाने से आवश्यकतानुसार डेटा, आकृतियाँ और स्वरूपण जोड़ने के लिए एक खाली स्लेट उपलब्ध हो जाती है।

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // एक नई कार्यपुस्तिका (एक्सेल फ़ाइल) बनाएँ
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुँचें
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### वर्कशीट में टेक्स्ट बॉक्स जोड़ें

इसके बाद, अपनी चुनी हुई वर्कशीट में एक टेक्स्ट बॉक्स आकार जोड़ें। इस आकार में आप अपनी ज़रूरत के हिसाब से कोई भी टेक्स्ट रख सकते हैं।

#### अवलोकन

टेक्स्ट बॉक्स एक बहुमुखी उपकरण है, जिसके द्वारा कस्टम टेक्स्ट, जैसे नोट्स या निर्देश, को सीधे एक्सेल शीट में शामिल किया जा सकता है।

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // एक नई कार्यपुस्तिका (एक्सेल फ़ाइल) बनाएँ
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुँचें
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // वर्कशीट में टेक्स्ट बॉक्स आकार जोड़ें
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### टेक्स्ट को आकार में सेट करें

एक बार आपका टेक्स्ट बॉक्स तैयार हो जाए, तो उसकी सामग्री सेट करें और उसके अंदर के टेक्स्ट को फॉर्मेट करें।

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // एक नई कार्यपुस्तिका (एक्सेल फ़ाइल) बनाएँ
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुँचें
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // वर्कशीट में टेक्स्ट बॉक्स आकार जोड़ें
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // आकृति के अंदर पाठ सामग्री सेट करें
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### आकार में पाठ पैराग्राफ तक पहुंचें

आप विशिष्ट स्वरूपण लागू करने के लिए टेक्स्ट बॉक्स के भीतर अलग-अलग पैराग्राफ तक पहुंच सकते हैं।

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // एक नई कार्यपुस्तिका (एक्सेल फ़ाइल) बनाएँ
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुँचें
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // वर्कशीट में टेक्स्ट बॉक्स आकार जोड़ें
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // आकृति के अंदर पाठ सामग्री सेट करें
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // आकृति में दूसरे पैराग्राफ तक पहुंचें
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### पैराग्राफ की लाइन स्पेसिंग सेट करें

लाइन स्पेसिंग को कस्टमाइज़ करने से पठनीयता बढ़ सकती है। इसे सेट करने का तरीका यहां बताया गया है:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // एक नई कार्यपुस्तिका (एक्सेल फ़ाइल) बनाएँ
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुँचें
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // वर्कशीट में टेक्स्ट बॉक्स आकार जोड़ें
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // आकृति के अंदर पाठ सामग्री सेट करें
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // आकृति में दूसरे पैराग्राफ तक पहुंचें
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // पंक्ति अंतरण 20 पॉइंट पर सेट करें
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // पैराग्राफ़ से पहले और बाद में स्थान कॉन्फ़िगर करें
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### कार्यपुस्तिका सहेजें

अंत में, अपनी कार्यपुस्तिका को नए जोड़े गए और स्वरूपित टेक्स्ट बॉक्स के साथ सहेजें।

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // एक नई कार्यपुस्तिका (एक्सेल फ़ाइल) बनाएँ
        Workbook workbook = new Workbook();
        
        // पहली वर्कशीट तक पहुँचें
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // वर्कशीट में टेक्स्ट बॉक्स आकार जोड़ें
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // आकृति के अंदर पाठ सामग्री सेट करें
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // आकृति में दूसरे पैराग्राफ तक पहुंचें
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // पंक्ति अंतरण 20 पॉइंट पर सेट करें
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // पैराग्राफ़ से पहले और बाद में स्थान कॉन्फ़िगर करें
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // कार्यपुस्तिका सहेजें
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## निष्कर्ष

आपने सफलतापूर्वक सीख लिया है कि जावा के लिए Aspose.Cells का उपयोग करके Excel वर्कबुक में टेक्स्ट बॉक्स कैसे जोड़ें और लाइन स्पेसिंग कैसे सेट करें। यह गतिशील, दृश्यमान रूप से आकर्षक रिपोर्ट बनाने की आपकी क्षमता को बढ़ाता है।

## कीवर्ड अनुशंसाएँ
- "Aspose.Cells for Java"
- "एक्सेल में टेक्स्ट बॉक्स जोड़ें"
- "एक्सेल में लाइन स्पेसिंग सेट करें"
- "स्टाइल्ड टेक्स्ट के साथ एक्सेल वर्कबुक"
- "जावा और Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}