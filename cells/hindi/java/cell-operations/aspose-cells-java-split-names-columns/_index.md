---
date: '2026-03-15'
description: Aspose Cells Java का उपयोग करके नामों को अलग-अलग कॉलम में विभाजित करना
  और वर्कबुक (xlsx) को सहेजना सीखें, एक चरण‑दर‑चरण ट्यूटोरियल में।
keywords:
- Aspose.Cells Java
- split names columns
- Excel manipulation
- text to columns Java
- Java Excel processing
title: aspose cells java – नामों को कॉलम में विभाजित करें
url: /hi/java/cell-operations/aspose-cells-java-split-names-columns/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# **aspose cells java** में महारत: नामों को कॉलम में विभाजित करना

हमारे व्यापक **aspose cells java** ट्यूटोरियल में आपका स्वागत है। इस गाइड में आप सीखेंगे **नामों को कैसे विभाजित करें** जो एक ही Excel कॉलम में संग्रहीत हैं, और उन्हें दो अलग-अलग कॉलम—पहला नाम और अंतिम नाम—में बदलें, शक्तिशाली टेक्स्ट‑टू‑कॉलम्स फीचर का उपयोग करके। चाहे आप संपर्क सूची को साफ़ कर रहे हों, CRM इम्पोर्ट के लिए डेटा तैयार कर रहे हों, या बस स्प्रेडशीट को पुनर्संरचना करने का तेज़ तरीका चाहिए, यह ट्यूटोरियल आपको दिखाएगा कि परिवर्तन के बाद **workbook xlsx को कैसे सहेजें**।

## त्वरित उत्तर
- **इस ट्यूटोरियल में क्या कवर किया गया है?** Aspose.Cells for Java के साथ पूर्ण‑नाम स्ट्रिंग्स को प्रथम‑और‑अंतिम‑नाम कॉलम में विभाजित करना।  
- **कौन सा लाइब्रेरी संस्करण उपयोग किया गया है?** नवीनतम स्थिर रिलीज़ (2026 तक)।  
- **क्या मुझे लाइसेंस चाहिए?** विकास के लिए एक मुफ्त ट्रायल काम करता है; उत्पादन के लिए एक व्यावसायिक लाइसेंस आवश्यक है।  
- **क्या मैं अन्य डिलिमिटर पर विभाजित कर सकता हूँ?** हाँ—सिर्फ `TxtLoadOptions` में सेपरेटर बदलें।  
- **क्या आउटपुट .xlsx फ़ाइल है?** बिल्कुल, वर्कबुक XLSX फ़ॉर्मेट में सहेजी जाती है।

## **aspose cells java** क्या है?
**Aspose.Cells java** एक उच्च‑प्रदर्शन Java API है जो डेवलपर्स को Microsoft Office की आवश्यकता के बिना Excel फ़ाइलें बनाने, संशोधित करने, परिवर्तित करने और रेंडर करने की अनुमति देता है। यह सभी प्रमुख Excel फ़ॉर्मेट्स को सपोर्ट करता है और फ़ॉर्मूले, चार्ट, और डेटा मैनिपुलेशन जैसी उन्नत सुविधाएँ प्रदान करता है।

## नाम विभाजन के लिए **aspose cells java** क्यों उपयोग करें?
- **Zero‑install**: किसी भी सर्वर‑साइड Java वातावरण में काम करता है।  
- **Speed**: बड़े स्प्रेडशीट्स को नेटिव Excel इंटरऑप से तेज़ी से संभालता है।  
- **Precision**: डिलिमिटर, कॉलम रेंज, और आउटपुट फ़ॉर्मेट पर पूर्ण नियंत्रण।  
- **Reliability**: कोई COM या Office निर्भरताएँ नहीं, जिससे क्लाउड या कंटेनर डिप्लॉयमेंट के लिए आदर्श बनता है।

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) 8 या नया।  
- IntelliJ IDEA या Eclipse जैसा IDE (वैकल्पिक लेकिन अनुशंसित)।  
- निर्भरताओं के प्रबंधन के लिए Maven या Gradle।  

### Maven सेटअप
अपने `pom.xml` में Aspose.Cells निर्भरता जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle सेटअप
अपने `build.gradle` में लाइब्रेरी जोड़ें:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

> **Pro tip:** विकास के दौरान पूरी कार्यक्षमता अनलॉक करने के लिए Aspose पोर्टल से एक अस्थायी लाइसेंस उपयोग करें।

## चरण‑दर‑चरण कार्यान्वयन

### चरण 1: एक वर्कबुक बनाएं और पहली वर्कशीट तक पहुँचें
पहले, कोर क्लासेज़ इम्पोर्ट करें और एक नई वर्कबुक इंस्टैंसिएट करें। यह आपको डेटा इन्सर्शन के लिए तैयार एक साफ़ Excel फ़ाइल देता है।

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;
```

```java
String dataDir = "YOUR_DATA_DIRECTORY"; // Define your directory path here

Workbook wb = new Workbook();
Worksheet ws = wb.getWorksheets().get(0);
```

### चरण 2: वर्कशीट में नमूना नाम भरें
अगले, कॉलम **A** में कुछ पूर्ण‑नाम स्ट्रिंग्स जोड़ें। वास्तविक प्रोजेक्ट में आप इन्हें डेटाबेस या CSV फ़ाइल से पढ़ेंगे।

```java
import com.aspose.cells.Cell;

String outDir = "YOUR_OUTPUT_DIRECTORY"; // Define your output directory path here

ws.getCells().get("A1").putValue("John Teal");
ws.getCells().get("A2").putValue("Peter Graham");
ws.getCells().get("A3").putValue("Brady Cortez");
ws.getCells().get("A4").putValue("Mack Nick");
ws.getCells().get("A5").putValue("Hsu Lee");
```

### चरण 3: कॉलम विभाजन के लिए टेक्स्ट लोड विकल्प कॉन्फ़िगर करें
`TxtLoadOptions` क्लास Aspose.Cells को बताता है कि टेक्स्ट को कैसे इंटरप्रेट किया जाए। यहाँ हम स्पेस (`' '`) को डिलिमिटर के रूप में उपयोग कर रहे हैं।

```java
import com.aspose.cells.TxtLoadOptions;

TxtLoadOptions opts = new TxtLoadOptions();
opts.setSeparator(' ');
```

### चरण 4: टेक्स्ट को दो कॉलम में विभाजित करें
अब `textToColumns()` को उस सेल एरिया पर कॉल करें जिसमें नाम हैं। पैरामीटर `(0, 0, 5, opts)` का अर्थ है *पंक्ति 0, कॉलम 0 से शुरू करें, 5 पंक्तियों को प्रोसेस करें, और हमने अभी जो विकल्प परिभाषित किए हैं उनका उपयोग करें*।

```java
ws.getCells().textToColumns(0, 0, 5, opts);
```

इस कॉल के बाद, कॉलम A में प्रथम नाम और कॉलम B में अंतिम नाम रहेगा।

### चरण 5: वर्कबुक को XLSX फ़ाइल के रूप में सहेजें
अंत में, संशोधित वर्कबुक को डिस्क पर लिखें। `SaveFormat` एन्नुम फ़ाइल को आधुनिक XLSX फ़ॉर्मेट में स्टोर करना सुनिश्चित करता है।

```java
import com.aspose.cells.SaveFormat;

wb.save(outDir + "outputTextToColumns.xlsx");
```

> **यह क्यों महत्वपूर्ण है:** **save workbook xlsx** का उपयोग करके आप सुनिश्चित करते हैं कि फ़ाइल नवीनतम संस्करणों के Excel, Google Sheets, और अन्य स्प्रेडशीट टूल्स के साथ संगत है।

## व्यावहारिक अनुप्रयोग
- **डेटा क्लीनिंग:** एनालिटिक्स पाइपलाइन में लोड करने से पहले जुड़े हुए फ़ील्ड्स को जल्दी से अलग करें।  
- **CRM इंटीग्रेशन:** फ्लैट संपर्क सूची को इम्पोर्ट के लिए संरचित तालिका में बदलें।  
- **HR सिस्टम:** पेरोल या लाभ प्रोसेसिंग के लिए कर्मचारी पूर्ण नाम को विभाजित करें।

## प्रदर्शन विचार
हजारों पंक्तियों के साथ काम करते समय:

1. **बैच अपडेट्स:** `ws.getCells().setRowHeight()` या समान बैच मेथड्स का उपयोग करके ओवरहेड कम करें।  
2. **मेमोरी मैनेजमेंट:** `wb.calculateFormula()` को केवल आवश्यक होने पर कॉल करें, और बड़े ऑब्जेक्ट्स को तुरंत डिस्पोज़ करें।  
3. **गार्बेज कलेक्शन:** बड़े फ़ाइलों के लिए `-Xmx2g` जैसे उचित हीप सेटिंग्स के साथ JVM चलाएँ ताकि OutOfMemory त्रुटियों से बचा जा सके।

## सामान्य समस्याएँ और समाधान
| समस्या | समाधान |
|-------|----------|
| **नामों में मध्य अक्षर होते हैं** (जैसे “John A. Doe”) | सेपरेटर को समायोजित करें या दूसरे कॉलम को पोस्ट‑प्रोसेस करके अंतिम नाम निकालें। |
| **अनपेक्षित खाली सेल्स** | सुनिश्चित करें कि स्रोत रेंज (`textToColumns` पैरामीटर) वास्तविक डेटा पंक्तियों से मेल खाती है। |
| **लाइसेंस नहीं मिला** | अस्थायी लाइसेंस फ़ाइल (`Aspose.Cells.lic`) को प्रोजेक्ट रूट में रखें या लाइसेंस को प्रोग्रामेटिकली सेट करें। |

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: Aspose.Cells Java क्या है?**  
**उत्तर:** एक शक्तिशाली लाइब्रेरी जो आपको Java का उपयोग करके प्रोग्रामेटिक रूप से Excel फ़ाइलें बनाने, संशोधित करने और परिवर्तित करने की अनुमति देती है।

**प्रश्न: क्या मैं स्पेस के अलावा अन्य डिलिमिटर पर कॉलम विभाजित कर सकता हूँ?**  
**उत्तर:** हाँ, अपनी डेटा के अनुसार `TxtLoadOptions` सेपरेटर को कस्टमाइज़ करें।

**प्रश्न: बड़े डेटासेट्स को Aspose.Cells के साथ कैसे संभालूँ?**  
**उत्तर:** मेमोरी प्रबंधन और वर्कबुक ऑपरेशन्स को न्यूनतम करके प्रदर्शन को ऑप्टिमाइज़ करें, जैसा कि ऊपर बताया गया है।

**प्रश्न: यदि मुझे समस्याएँ आती हैं तो क्या सहायता उपलब्ध है?**  
**उत्तर:** समुदाय सहायता के लिए [Aspose Forum](https://forum.aspose.com/c/cells/9) देखें या सीधे Aspose सपोर्ट टीम से संपर्क करें।

**प्रश्न: Aspose.Cells किन फ़ॉर्मेट्स में वर्कबुक सहेज सकता है?**  
**उत्तर:** XLSX, XLS, CSV आदि सहित कई Excel फ़ाइल फ़ॉर्मेट्स को सपोर्ट करता है।

## संसाधन

- **डॉक्यूमेंटेशन**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **डाउनलोड**: [Aspose.Cells Java Releases](https://releases.aspose.com/cells/java/)
- **खरीदें**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **फ़्री ट्रायल**: [Try Aspose.Cells for Free](https://releases.aspose.com/cells/java/)
- **अस्थायी लाइसेंस**: [Request a Temporary License](https://purchase.aspose.com/temporary-license/)

कोडिंग का आनंद लें, और अपने प्रोजेक्ट्स में **aspose cells java** की पूरी शक्ति का उपयोग करें!

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2026-03-15  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose