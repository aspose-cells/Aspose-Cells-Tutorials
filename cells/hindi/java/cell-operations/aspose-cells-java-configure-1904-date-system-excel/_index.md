---
date: '2026-02-22'
description: Aspose.Cells for Java का उपयोग करके Excel की तिथि प्रणाली को 1904 में
  बदलना, Excel तिथि प्रारूप सेट करना, और Excel 1904 प्रणाली को कुशलतापूर्वक परिवर्तित
  करना सीखें।
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Aspose.Cells Java के साथ Excel तिथि प्रणाली को 1904 में बदलें
url: /hi/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

 keep markdown formatting.

Let's produce final content.

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java के साथ Excel डेट सिस्टम को 1904 में बदलें

Excel में ऐतिहासिक डेटा को संभालना चुनौतीपूर्ण हो सकता है क्योंकि Excel दो अलग-अलग डेट सिस्टम को सपोर्ट करता है। **इस ट्यूटोरियल में आप सीखेंगे कि Aspose.Cells for Java का उपयोग करके Excel डेट सिस्टम को 1904 फॉर्मेट में कैसे बदलें**, जिससे लेगेसी डेट्स को संभालना आसान हो जाता है। हम वर्कबुक को इनिशियलाइज़ करने, 1904 डेट सिस्टम को एनेबल करने, और परिवर्तन को सहेजने की प्रक्रिया को चरण‑बद्ध तरीके से दिखाएंगे।

## त्वरित उत्तर
- **1904 डेट सिस्टम क्या करता है?** यह January 1, 1904 से दिनों की गिनती शुरू करता है, जिससे डिफ़ॉल्ट 1900 सिस्टम की तुलना में सभी डेट्स 1462 दिन आगे शिफ्ट हो जाती हैं।  
- **डेट सिस्टम बदलने के लिए Aspose.Cells क्यों उपयोग करें?** यह एक सरल API प्रदान करता है जो बिना Excel इंस्टॉल किए काम करता है और बड़े फ़ाइलों को सपोर्ट करता है।  
- **कौन से Java संस्करण समर्थित हैं?** JDK 8 या नया।  
- **क्या मुझे लाइसेंस चाहिए?** मूल्यांकन के लिए एक फ्री ट्रायल काम करता है; लाइसेंस उपयोग सीमाओं को हटाता है।  
- **क्या बाद में 1900 सिस्टम में वापस बदल सकते हैं?** हाँ, सिर्फ `setDate1904(false)` सेट करें।

## Excel में 1904 डेट सिस्टम क्या है?
1904 डेट सिस्टम मूल रूप से शुरुआती Macintosh संस्करणों के Excel में उपयोग किया जाता था। यह January 1, 1904 से दिनों की गिनती करता है, जो पुराने स्प्रेडशीट्स और कुछ वित्तीय मॉडलों के साथ संगतता के लिए उपयोगी है।

## Aspose.Cells के साथ Excel डेट सिस्टम क्यों बदलें?
- **क्रॉस‑प्लेटफ़ॉर्म संगतता** – Windows, Linux, और macOS पर काम करता है।  
- **Excel इंस्टॉलेशन की आवश्यकता नहीं** – सर्वर‑साइड प्रोसेसिंग के लिए आदर्श।  
- **उच्च प्रदर्शन** – न्यूनतम मेमोरी ओवरहेड के साथ बड़े वर्कबुक को संभालता है।  

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) 8 या उससे ऊपर।  
- डिपेंडेंसी मैनेजमेंट के लिए Maven या Gradle।  
- बुनियादी Java प्रोग्रामिंग ज्ञान।  

## Aspose.Cells for Java सेटअप करना

### Maven
अपने `pom.xml` फ़ाइल में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
अपने `build.gradle` फ़ाइल में यह लाइन शामिल करें:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### लाइसेंस प्राप्त करना
Aspose एक फ्री ट्रायल, टेम्पररी लाइसेंस, और पूर्ण कमर्शियल लाइसेंस प्रदान करता है। आप [फ्री ट्रायल](https://releases.aspose.com/cells/java/) से शुरू कर सकते हैं या [टेम्पररी लाइसेंस पेज](https://purchase.aspose.com/temporary-license/) से टेम्पररी लाइसेंस प्राप्त कर सकते हैं।

## Aspose.Cells Java के साथ Excel डेट सिस्टम बदलें

नीचे चरण‑बद्ध गाइड है जो वास्तव में **Excel डेट सिस्टम को बदलता** है। प्रत्येक चरण में एक छोटा व्याख्यान और आवश्यक कोड दिया गया है।

### चरण 1: वर्कबुक को इनिशियलाइज़ और लोड करें
सबसे पहले, एक `Workbook` इंस्टेंस बनाएं जो आपके मौजूदा Excel फ़ाइल की ओर इशारा करता हो।

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### चरण 2: 1904 डेट सिस्टम एनेबल करें
डेट सिस्टम को स्विच करने के लिए वर्कबुक सेटिंग्स का उपयोग करें।

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**प्रो टिप:** यदि बाद में रिवर्ट करना हो तो आप `setDate1904(false)` भी कॉल कर सकते हैं।

### चरण 3: संशोधित वर्कबुक को सेव करें
अंत में, बदलावों को नई फ़ाइल में लिखें (या मूल फ़ाइल को ओवरराइट करें)।

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **नोट:** ऊपर दिया गया कोड क्लास नाम `tWorkbook` का उपयोग करता है जैसा कि मूल रूप से प्रदान किया गया था। सुनिश्चित करें कि यह टाइपो आपके प्रोजेक्ट की नेमिंग कन्वेंशन से मेल खाता है या आवश्यक होने पर इसे `Workbook` में बदलें।

## प्रोग्रामेटिकली Excel डेट सेट करना (सेकेंडरी कीवर्ड)
यदि सिस्टम बदलने के बाद आपको व्यक्तिगत सेल वैल्यूज़ को एडजस्ट करना है, तो आप `Cells.get(i, j).putValue(Date)` का उपयोग कर सकते हैं जहाँ डेट सक्रिय डेट सिस्टम के अनुसार इंटरप्रेट होगी।

## Excel 1904 सिस्टम को 1900 में वापस बदलना (सेकेंडरी कीवर्ड)
रिवर्ट करने के लिए, बस कॉल करें:

```java
workbook.getSettings().setDate1904(false);
```

फिर वर्कबुक को फिर से सेव करें।

## व्यावहारिक उपयोग
1. **डेटा आर्काइविंग** – पुराने Mac‑आधारित स्प्रेडशीट्स को माइग्रेट करते समय लेगेसी टाइमस्टैम्प्स को संरक्षित रखें।  
2. **क्रॉस‑प्लेटफ़ॉर्म रिपोर्टिंग** – ऐसी रिपोर्ट्स जनरेट करें जो Windows और macOS दोनों पर बिना डेट मismatch के खुल सकें।  
3. **वित्तीय मॉडलिंग** – डेट कैलकुलेशन को लेगेसी वित्तीय मॉडलों के साथ संरेखित करें जो 1904 सिस्टम की अपेक्षा रखते हैं।

## प्रदर्शन संबंधी विचार
- मेमोरी उपयोग को कम रखने के लिए एक सिंगल सत्र में वर्कबुक ऑपरेशन्स की संख्या सीमित रखें।  
- बहुत बड़ी फ़ाइलों के लिए Java की गार्बेज‑कलेक्शन ट्यूनिंग का उपयोग करें।  

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: 1900 और 1904 डेट सिस्टम में क्या अंतर है?**  
उत्तर: 1900 सिस्टम January 1, 1900 से शुरू होता है, जबकि 1904 सिस्टम January 1, 1904 से, जिससे सभी डेट्स 1462 दिन शिफ्ट हो जाती हैं।

**प्रश्न: क्या मैं किसी वर्कबुक का डेट सिस्टम बदल सकता हूँ जो वर्तमान में Excel में खुला है?**  
उत्तर: हाँ, लेकिन पहले Excel में फ़ाइल को बंद करें; अन्यथा सेव ऑपरेशन फेल हो जाएगा।

**प्रश्न: `setDate1904` उपयोग करने के लिए क्या लाइसेंस चाहिए?**  
उत्तर: यह मेथड फ्री ट्रायल में काम करता है, लेकिन पूर्ण लाइसेंस मूल्यांकन सीमाओं को हटाता है।

**प्रश्न: क्या केवल एक ही वर्कशीट के लिए डेट सिस्टम बदलना संभव है?**  
उत्तर: नहीं, डेट सिस्टम वर्कबुक‑लेवल सेटिंग है; यह सभी वर्कशीट्स पर लागू होता है।

**प्रश्न: कैसे पुष्टि करूँ कि डेट सिस्टम बदल गया है?**  
उत्तर: सेव्ड फ़ाइल को Excel में खोलें, **File → Options → Advanced** पर जाएँ, और **"Use 1904 date system"** बॉक्स को चेक करें।

## निष्कर्ष
अब आप जानते हैं कि **Aspose.Cells for Java** का उपयोग करके Excel डेट सिस्टम को 1904 में कैसे बदलें, Excel डेट फ़ॉर्मेट कैसे सेट करें, और आवश्यकता पड़ने पर कैसे वापस बदलें। इन स्निपेट्स को अपने डेटा‑प्रोसेसिंग पाइपलाइन में शामिल करें ताकि प्लेटफ़ॉर्म्स के बीच डेट‑संगतता सुनिश्चित हो सके।

---

**अंतिम अपडेट:** 2026-02-22  
**टेस्टेड विथ:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  

**संसाधन**
- **डॉक्यूमेंटेशन:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **डाउनलोड:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **लाइसेंस खरीदें:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **फ्री ट्रायल:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **टेम्पररी लाइसेंस:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **सपोर्ट फ़ोरम:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}