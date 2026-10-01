---
date: '2026-02-24'
description: Aspose.Cells for Java का उपयोग करके एक्सेल से हाइपरलिंक निकालना सीखें,
  जिसमें वर्कबुक लोड करना, एक्सेल हाइपरलिंक पढ़ना, और एक्सेल फ़ाइलों को बैच में प्रोसेस
  करना शामिल है।
keywords:
- Aspose.Cells Java
- Excel Hyperlink Management
- Aspose.Cells for Java setup
title: एक्सेल से हाइपरलिंक निकालें – Aspose Cells वर्कबुक लोडिंग
url: /hi/java/advanced-features/aspose-cells-java-excel-hyperlinks-processing/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# एक्सेल से हाइपरलिंक निकालें – उन्नत एक्सेल हाइपरलिंक प्रबंधन

आज के डेटा‑चालित विश्व में, **एक्सेल से हाइपरलिंक निकालना** तेज़ और भरोसेमंद होना हर उस व्यक्ति के लिए मुख्य आवश्यकता है जो एक्सेल रिपोर्टिंग को ऑटोमेट करता है। चाहे आप एक वित्तीय डैशबोर्ड, डेटा‑माइग्रेशन टूल, या दस्तावेज़‑जनरेशन सेवा बना रहे हों, हाइपरलिंक से भरपूर वर्कबुक को संभालना अक्सर एक चुनौती बन जाता है। इस ट्यूटोरियल में आप सीखेंगे कि कैसे एक Excel वर्कबुक लोड करें, उसकी वर्कशीट्स तक पहुँचें, और **Aspose.Cells for Java** का उपयोग करके **एक्सेल से हाइपरलिंक प्राप्त करें**। अंत तक, आप अपने स्वयं के एप्लिकेशन में हाइपरलिंक प्रोसेसिंग को इंटीग्रेट करने और बड़े‑पैमाने पर **एक्सेल फ़ाइलों को बैच प्रोसेस** करने के लिए तैयार होंगे।

## त्वरित उत्तर
- **वर्कबुक खोलने के लिए प्राथमिक क्लास कौन सी है?** `Workbook`
- **कौन सा मेथड रेंज में सभी हाइपरलिंक लौटाता है?** `Range.getHyperlinks()`
- **बुनियादी हाइपरलिंक एक्सट्रैक्शन के लिए लाइसेंस चाहिए?** एक फ्री ट्रायल काम करता है, लेकिन लाइसेंस मूल्यांकन सीमाओं को हटाता है।
- **क्या मैं बड़ी फ़ाइलों को कुशलता से प्रोसेस कर सकता हूँ?** हाँ—विशिष्ट वर्कशीट्स या रेंज पर फोकस करें।
- **कौन से Java संस्करण समर्थित हैं?** Java 8 और उसके बाद के संस्करण।

## “एक्सेल से हाइपरलिंक निकालें” क्या है?
एक्सेल से हाइपरलिंक निकालना का मतलब है सेल्स में संग्रहीत लिंक जानकारी पढ़ना, जैसे URLs, फ़ाइल पाथ, ईमेल एड्रेस, या आंतरिक सेल रेफ़रेंसेज़। Aspose.Cells एक सरल API प्रदान करता है जिससे इन लिंक को Excel खोले बिना ही सूचीबद्ध किया जा सकता है।

## एक्सेल से हाइपरलिंक क्यों प्राप्त करें?
हाइपरलिंक अक्सर बाहरी डेटा स्रोतों, दस्तावेज़ों, या आंतरिक रेफ़रेंसेज़ की ओर इशारा करते हैं। इन्हें निकालने से आप:
- लिंक हेल्थ को स्वचालित रूप से वैलिडेट कर सकते हैं।
- डेटा माइग्रेशन के दौरान URLs को माइग्रेट या री‑राइट कर सकते हैं।
- सभी लिंक्ड रिसोर्सेज की सारांश रिपोर्ट बना सकते हैं।
- नॉलेज‑बेस इंटीग्रेशन के लिए सर्चेबल इंडेक्स बना सकते हैं।

## आवश्यकताएँ

- **Aspose.Cells for Java** लाइब्रेरी (वर्ज़न 25.3 या नया)
- Java 8 + और एक IDE (IntelliJ IDEA, Eclipse, आदि)
- Maven या Gradle के माध्यम से डिपेंडेंसी मैनेजमेंट
- वैध Aspose.Cells लाइसेंस (ट्रायल के लिए वैकल्पिक)

### Aspose.Cells for Java सेटअप करना

लाइब्रेरी को अपने प्रोजेक्ट में Maven या Gradle के द्वारा जोड़ें।

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

> **प्रो टिप:** लाइब्रेरी का संस्करण हमेशा अपडेट रखें ताकि प्रदर्शन सुधार और नई हाइपरलिंक‑हैंडलिंग सुविधाओं का लाभ मिल सके।

#### बेसिक इनिशियलाइज़ेशन

डिपेंडेंसी जोड़ने के बाद, एक साधारण Java क्लास बनाएं ताकि वर्कबुक लोड हो रहा है या नहीं, यह सत्यापित किया जा सके।

```java
import com.aspose.cells.Workbook;

public class InitializeAsposeCells {
    public static void main(String[] args) throws Exception {
        // Set license if available
        // License license = new License();
        // license.setLicense("path/to/license/file");

        String dataDir = "YOUR_DATA_DIRECTORY";
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

### चरण‑दर‑चरण कार्यान्वयन

नीचे हम तीन मुख्य फीचर दिखाते हैं: वर्कबुक लोड करना, वर्कशीट और रेंज तक पहुँच, और अंत में हाइपरलिंक को प्राप्त व प्रोसेस करना।

## एक्सेल से हाइपरलिंक निकालें – वर्कबुक लोड करना

### वर्कबुक लोड करें (फ़ीचर 1)

```java
import com.aspose.cells.Workbook;

public class FeatureLoadWorkbook {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");
        
        System.out.println("Workbook loaded successfully!");
    }
}
```

## एक्सेल से हाइपरलिंक निकालें – वर्कशीट और रेंज तक पहुँच

### वर्कशीट और रेंज तक पहुँचें (फ़ीचर 2)

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
import com.aspose.cells.Range;

public class FeatureAccessWorksheetAndRange {
    public static void main(String[] args) throws Exception {
        String dataDir = "YOUR_DATA_DIRECTORY";
        
        // Load an existing workbook from the specified path.
        Workbook workbook = new Workbook(dataDir + "/LinkTypes.xlsx");

        // Access the first worksheet in the workbook (index 0).
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Create a range from cell A1 to A7 within the worksheet.
        Range range = worksheet.getCells().createRange("A1", "A7");
        
        System.out.println("Range created successfully!");
    }
}
```

## एक्सेल से हाइपरलिंक निकालें – हाइपरलिंक प्राप्त और प्रोसेस करें

### हाइपरलिंक प्राप्त और प्रोसेस करें (फ़ीचर 3)

```java
import com.aspose.cells.Range;
import com.aspose.cells.Hyperlink;
import com.aspose.cells.TargetModeType;

public class FeatureRetrieveAndProcessHyperlinks {
    public static void main(String[] args) throws Exception {
        // Assume 'range' is obtained as shown in previous examples.
        Range range = null;  // Placeholder, replace with actual range initialization

        // Retrieve all hyperlinks within the specified range.
        Hyperlink[] hyperlinks = range.getHyperlinks();

        // Iterate over each hyperlink and process it to determine its type.
        for (Hyperlink link : hyperlinks) {
            String displayText = link.getTextToDisplay();
            int linkType = link.getLinkType();
            System.out.println(displayText + ": " + getLinkTypeName(linkType));
        }
    }

    // Helper method to convert hyperlink type integer to a human‑readable string.
    private static String getLinkTypeName(int linkType) {
        switch (linkType) {
            case TargetModeType.EXTERNAL:
                return "EXTERNAL";
            case TargetModeType.FILE_PATH:
                return "FILE_PATH";
            case TargetModeType.EMAIL:
                return "EMAIL";
            default:
                return "CELL_REFERENCE";
        }
    }
}
```

### व्यावहारिक अनुप्रयोग

| उपयोग केस | लाभ |
|----------|-----|
| **डेटा वैलिडेशन** | रिपोर्ट प्रकाशित करने से पहले हर हाइपरलिंक के पहुँच योग्य होने की स्वचालित जाँच। |
| **ऑटोमेशन** | नई डेटा‑वेयरहाउस में माइग्रेशन के दौरान लिंक निकालें और रेफ़रेंसेज़ को रीयल‑टाइम अपडेट करें। |
| **रिपोर्टिंग** | एक सारांश शीट बनाएं जो वर्कबुक में सभी बाहरी रिसोर्सेज की सूची देती हो। |

### प्रदर्शन संबंधी विचार

- **केवल आवश्यक रेंज प्रोसेस करें** – स्कोप सीमित करने से मेमोरी खपत घटती है।
- **ऑब्जेक्ट्स को डिस्पोज़ करें** – उपयोग के बाद `workbook = null;` सेट करें और JVM के गैर्बेज कलेक्टर को मेमोरी मुक्त करने दें।
- **बैच प्रोसेसिंग** – कई फ़ाइलों को हैंडल करते समय संभव हो तो एक ही `Workbook` इंस्टेंस को पुनः उपयोग करें। इससे आप **एक्सेल फ़ाइलों को बैच प्रोसेस** प्रभावी ढंग से कर सकते हैं।

## सामान्य समस्याएँ और समाधान

| समस्या | समाधान |
|--------|--------|
| **Null `range`** | `getHyperlinks()` कॉल करने से पहले सुनिश्चित करें कि रेंज बनाया गया है। |
| **लाइसेंस नहीं है** | विकास के लिए ट्रायल काम करता है, लेकिन लाइसेंस मूल्यांकन सीमाओं को हटाता है और प्रदर्शन बेहतर करता है। |
| **असमर्थित हाइपरलिंक प्रकार** | नई प्रकारों को संभालने के लिए `TargetModeType` कॉन्स्टैंट्स का उपयोग करें जैसे ही Aspose अपडेट जारी करता है। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: Aspose.Cells के साथ कौन से Java संस्करण संगत हैं?**  
उत्तर: Aspose.Cells for Java Java 8 और उसके बाद के संस्करणों को सपोर्ट करता है। सुनिश्चित करें कि आपका JDK इस आवश्यकता को पूरा करता हो।

**प्रश्न: क्या मैं बहुत बड़ी Excel फ़ाइलों से हाइपरलिंक निकाल सकता हूँ बिना मेमोरी खत्म हुए?**  
उत्तर: हाँ। केवल आवश्यक वर्कशीट या रेंज लोड करें, और पूरी वर्कबुक को लोड करने से बचें जब संभव हो।

**प्रश्न: उत्पादन में हाइपरलिंक एक्सट्रैक्शन के लिए लाइसेंस आवश्यक है?**  
उत्तर: फ्री ट्रायल प्रयोग के लिए पर्याप्त है, लेकिन एक कमर्शियल लाइसेंस मूल्यांकन सीमाओं को हटाता है और पूर्ण सपोर्ट देता है।

**प्रश्न: ईमेल एड्रेस की ओर इशारा करने वाले हाइपरलिंक को कैसे हैंडल करें?**  
उत्तर: `TargetModeType.EMAIL` कॉन्स्टैंट ईमेल लिंक को पहचानता है; आप आवश्यकता अनुसार उन्हें अलग से प्रोसेस कर सकते हैं।

**प्रश्न: क्या Aspose.Cells वर्कबुक सेव करने पर हाइपरलिंक फ़ॉर्मेटिंग को बरकरार रखता है?**  
उत्तर: बिल्कुल। सभी हाइपरलिंक प्रॉपर्टीज़ (डिस्प्ले टेक्स्ट, टूलटिप, एड्रेस) को वर्कबुक सेव करने पर संरक्षित रखा जाता है।

**प्रश्न: क्या मैं Aspose.Cells का उपयोग करके **read excel hyperlinks** को बैच जॉब में कर सकता हूँ?**  
उत्तर: हाँ—API को फ़ाइलों की लूप के साथ मिलाकर कई वर्कबुक में एक्सेल हाइपरलिंक पढ़ सकते हैं।

**प्रश्न: हाई‑थ्रूपुट परिदृश्यों के लिए **load excel workbook java** का सबसे अच्छा तरीका क्या है?**  
उत्तर: जब संभव हो तो एक ही `Workbook` इंस्टेंस को पुनः उपयोग करें और संसाधन मुक्त करने के लिए स्ट्रीम्स को तुरंत बंद करें।

---

**अंतिम अपडेट:** 2026-02-24  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  

यदि आपके और प्रश्न हैं, तो कृपया [Aspose सपोर्ट फ़ोरम](https://forum.aspose.com/c/cells/9) पर जाएँ।

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}