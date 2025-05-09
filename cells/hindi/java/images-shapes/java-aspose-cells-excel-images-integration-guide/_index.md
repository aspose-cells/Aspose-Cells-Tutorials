---
"date": "2025-04-08"
"description": "जानें कि जावा और Aspose.Cells का उपयोग करके अपनी एक्सेल रिपोर्ट में छवियों को कैसे सहजता से एकीकृत किया जाए। यह गाइड छवि फ़ाइलों को पढ़ने से लेकर गतिशील कार्यपुस्तिकाएँ बनाने तक सब कुछ कवर करती है।"
"title": "जावा और Aspose.Cells का उपयोग करके एक्सेल वर्कबुक में छवियों को कैसे एकीकृत करें"
"url": "/hi/java/images-shapes/java-aspose-cells-excel-images-integration-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# जावा में Aspose.Cells और इमेजेस के साथ Excel वर्कबुक कैसे बनाएं

## परिचय

क्या आप जावा का उपयोग करके अपनी एक्सेल रिपोर्ट में छवियों को एकीकृत करने के लिए संघर्ष कर रहे हैं? यह व्यापक गाइड आपको दिखाएगा कि छवियों से भरी गतिशील एक्सेल वर्कबुक बनाने के लिए जावा के लिए Aspose.Cells की शक्ति का लाभ कैसे उठाया जाए। चाहे आप एक अनुभवी डेवलपर हों या Aspose.Cells के लिए नए हों, यह ट्यूटोरियल आपको अपने डेटा प्रस्तुतियों को प्रभावी ढंग से बढ़ाने के लिए आवश्यक कौशल से लैस करेगा।

**आप क्या सीखेंगे:**
- जावा में छवि फ़ाइलें कैसे पढ़ें?
- Aspose.Cells का उपयोग करके Excel कार्यपुस्तिका बनाना और संशोधित करना।
- गतिशील डेटा प्रविष्टि के लिए स्मार्ट मार्कर का उपयोग करना।
- संरचित डेटा प्रबंधन के लिए कस्टम डेटा वर्ग परिभाषित करना।

क्या आप अपनी एक्सेल रिपोर्ट्स को रूपांतरित करने के लिए तैयार हैं? आइये सबसे पहले आवश्यक शर्तों पर नज़र डालें!

## आवश्यक शर्तें

शुरू करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

- **जावा डेवलपमेंट किट (JDK):** संस्करण 8 या उच्चतर अनुशंसित है।
- **जावा के लिए Aspose.Cells:** हम इस ट्यूटोरियल में संस्करण 25.3 का उपयोग करेंगे।
- **आईडीई:** कोई भी जावा आईडीई जैसे कि इंटेलीज आईडिया या एक्लिप्स काम करेगा।

आपको बुनियादी जावा प्रोग्रामिंग से परिचित होना चाहिए और फाइलों और डेटा संरचनाओं को संभालने की कुछ समझ होनी चाहिए।

## Java के लिए Aspose.Cells सेट अप करना

आरंभ करने के लिए, आपको अपने प्रोजेक्ट में Aspose.Cells लाइब्रेरी को शामिल करना होगा। Maven या Gradle का उपयोग करके इसे करने का तरीका यहां बताया गया है:

### मावेन
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### ग्रैडल
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

निर्भरता स्थापित करने के बाद, आप Aspose.Cells के लिए लाइसेंस प्राप्त कर सकते हैं:

- **मुफ्त परीक्षण:** कुछ सीमाओं के साथ लाइब्रेरी को डाउनलोड करें और आज़माएँ।
- **अस्थायी लाइसेंस:** बिना किसी प्रतिबंध के सम्पूर्ण सुविधाओं का आनंद लेने के लिए अस्थायी लाइसेंस प्राप्त करें।
- **खरीदना:** यदि आपको दीर्घकालिक पहुंच की आवश्यकता है तो इसे खरीदने पर विचार करें।

अपनी जावा क्लास फ़ाइलों में आवश्यक आयात सेट करके अपने प्रोजेक्ट को आरंभ करें, जैसा कि नीचे दिखाया गया है। यह सेटअप छवियों को पढ़ने और Aspose.Cells के साथ Excel वर्कबुक बनाने के लिए आवश्यक होगा।

## कार्यान्वयन मार्गदर्शिका

इस अनुभाग में, हम आपको Aspose.Cells का उपयोग करके छवियों वाली एक Excel कार्यपुस्तिका बनाने में मदद करने के लिए प्रत्येक सुविधा के बारे में चरण-दर-चरण बताएंगे।

### फ़ीचर 1: छवि फ़ाइलें पढ़ना

सबसे पहले, आइए समझते हैं कि किसी डायरेक्टरी से इमेज फाइल को कैसे पढ़ा जाए। यह बाद में हमारी वर्कबुक में इमेज जोड़ने के लिए महत्वपूर्ण है।

#### अवलोकन
हम इमेज फ़ाइलों को बाइट ऐरे में पढ़ने के लिए जावा के NIO पैकेज का उपयोग करेंगे। यह दृष्टिकोण हमें विभिन्न इमेज प्रारूपों को सहजता से संभालने की अनुमति देता है।

```java
import java.nio.file.*;
import java.io.IOException;

public class ReadImageFiles {
    public static void main(String[] args) throws IOException {
        String dataDir = "YOUR_DATA_DIRECTORY"; // अपना निर्देशिका पथ सेट करें

        Path imagePath1 = Paths.get(dataDir + "sample1.png");
        byte[] photo1 = Files.readAllBytes(imagePath1);

        Path imagePath2 = Paths.get(dataDir + "sample2.jpg");
        byte[] photo2 = Files.readAllBytes(imagePath2);
    }
}
```

- **पैरामीटर और वापसी मान:** The `Paths.get()` विधि एक पथ का निर्माण करती है, और `Files.readAllBytes()` फ़ाइल को बाइट सरणी में पढ़ता है.
- **यह दृष्टिकोण क्यों?** NIO का उपयोग करने से बड़ी फ़ाइलों को संभालना सरल हो जाता है और यह विभिन्न छवि प्रारूपों का समर्थन करता है।

### फ़ीचर 2: Aspose.Cells के साथ वर्कबुक बनाना और संशोधित करना

अब जबकि हमारी छवियां तैयार हैं, आइए एक एक्सेल वर्कबुक बनाएं और उन्हें स्मार्ट मार्करों का उपयोग करके सम्मिलित करें।

#### अवलोकन
हम कार्यपुस्तिका बनाने, उसके स्वरूप को अनुकूलित करने, तथा डेटा के आधार पर गतिशील रूप से चित्र सम्मिलित करने के लिए Aspose.Cells का उपयोग करेंगे।

```java
import com.aspose.cells.*;
import java.util.ArrayList;

public class CreateAndModifyWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        String outDir = "YOUR_OUTPUT_DIRECTORY";

        Path path1 = Paths.get(dataDir + "sample1.png");
        byte[] photo1 = Files.readAllBytes(path1);
        
        Path path2 = Paths.get(dataDir + "sample2.jpg");
        byte[] photo2 = Files.readAllBytes(path2);

        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        worksheet.getCells().setStandardHeight(35);
        worksheet.getCells().setColumnWidth(3, 20); // स्तंभ डी
        worksheet.getCells().setColumnWidth(4, 20); // स्तंभ ई
        worksheet.getCells().setColumnWidth(5, 40); // स्तंभ एफ

        Style st = worksheet.getCells().get("D1").getStyle();
        st.getFont().setBold(true);
        
        worksheet.getCells().get("D1").putValue("Name");
        worksheet.getCells().get("E1").putValue("City");
        worksheet.getCells().get("F1").putValue("Photo");

        worksheet.getCells().get("D1").setStyle(st);
        worksheet.getCells().get("E1").setStyle(st);
        worksheet.getCells().get("F1").setStyle(st);

        worksheet.getCells().get("D2").putValue("&=Person.Name(group:normal,skip:1)");
        worksheet.getCells().get("E2").putValue("&=Person.City");
        worksheet.getCells().get("F2").putValue("&=Person.Photo(Picture:FitToCell)");

        ArrayList<Person> persons = new ArrayList<>();
        persons.add(new Person("George", "New York", photo1));
        persons.add(new Person("George", "New York", photo2));
        persons.add(new Person("Johnson", "London", photo2));
        persons.add(new Person("Simon", "Paris", photo1));
        persons.add(new Person("Henry", "Sydney", photo2));

        WorkbookDesigner designer = new WorkbookDesigner(workbook);
        designer.setDataSource("Person", persons);
        designer.process();

        workbook.save(outDir + "output.xlsx", SaveFormat.XLSX);
    }
}
```

- **स्मार्ट मार्कर:** ये मार्कर (`&=`) डेटा को गतिशील रूप से सम्मिलित करने की अनुमति देते हैं, जिससे प्रक्रिया कुशल और मापनीय बन जाती है।
- **कस्टम डेटा वर्ग:** हम परिभाषित करते हैं `Person` नाम, शहर और फोटो जैसे गुणों के साथ संरचित डेटा को प्रबंधित करने के लिए क्लास।

### फ़ीचर 3: कस्टम डेटा क्लास को परिभाषित करना और उसका उपयोग करना

हमारे इमेज डेटा को संभालने के लिए, हमें एक कस्टम क्लास की आवश्यकता है। आप इसे इस तरह परिभाषित कर सकते हैं:

```java
class Person {
    private String m_Name;
    private String m_City;
    private byte[] m_Photo;

    public Person(String name, String city, byte[] photo) {
        this.m_Name = name;
        this.m_City = city;
        this.m_Photo = photo;
    }

    public String getName() { return m_Name; }
    public void setName(String name) { this.m_Name = name; }

    public String getCity() { return m_City; }
    public void setCity(String city) { this.m_City = city; }

    public byte[] getPhoto() { return m_Photo; }
    public void setPhoto(byte[] photo) { this.m_Photo = photo; }
}
```

- **कस्टम क्लास का उपयोग क्यों करें?** यह डेटा को कुशलतापूर्वक व्यवस्थित करता है, जिससे बड़े अनुप्रयोगों में प्रबंधन और विस्तार करना आसान हो जाता है।

## व्यावहारिक अनुप्रयोगों

यहां कुछ वास्तविक दुनिया परिदृश्य दिए गए हैं जहां आप इन तकनीकों को लागू कर सकते हैं:

1. **व्यावसायिक रिपोर्ट:** कर्मचारियों की तस्वीरों के साथ स्वचालित रूप से व्यक्तिगत रिपोर्ट तैयार करें।
2. **ई-कॉमर्स कैटलॉग:** ऑनलाइन स्टोर के लिए छवियों के साथ उत्पाद कैटलॉग बनाएं।
3. **ईवेंट की योजना बनाना:** आयोजनों के लिए प्रोफ़ाइल चित्रों के साथ सहभागियों की सूची संकलित करें।
4. **शैक्षिक सामग्री:** एक्सेल शीट में एकीकृत दृश्य सहायता के साथ अध्ययन मार्गदर्शिकाएँ विकसित करें।

## प्रदर्शन संबंधी विचार

Aspose.Cells के साथ काम करते समय और बड़े डेटासेट या कई छवियों को संभालते समय, इन सुझावों पर विचार करें:

- जावा में डेटा को कुशलतापूर्वक प्रबंधित करके मेमोरी उपयोग को अनुकूलित करें।
- यदि आवश्यक हो तो छवियों को संपीड़ित करने के लिए Aspose की अंतर्निहित सुविधाओं का उपयोग करें।
- मापनीयता सुनिश्चित करने के लिए अलग-अलग डेटासेट आकारों के साथ प्रदर्शन का परीक्षण करें।

## निष्कर्ष

इस गाइड का पालन करके, आपने सीखा है कि जावा और Aspose.Cells का उपयोग करके एक्सेल वर्कबुक में छवियों को कैसे एकीकृत किया जाए। यह तकनीक विज़ुअल कंटेंट के साथ रिपोर्ट और प्रेजेंटेशन को बेहतर बनाने के लिए अमूल्य है।


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}