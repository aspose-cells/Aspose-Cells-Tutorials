---
date: '2026-08-16'
description: Aspose.Cells का उपयोग करके Java में globalization कैसे जोड़ें, Excel
  त्रुटि संदेशों को अनुकूलित करना, और Maven dependency सेट अप करना सीखें।
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Aspose.Cells का उपयोग करके Java में globalization कैसे जोड़ें, Excel
  त्रुटि संदेशों को अनुकूलित करना, और Maven dependency सेट अप करना सीखें। step‑by‑step
  गाइड का पालन करें।
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Aspose.Cells के साथ Java में globalization कैसे जोड़ें
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Aspose.Cells के साथ Java में globalization कैसे जोड़ें
url: /hi/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# जावा में Aspose.Cells के साथ ग्लोबलाइज़ेशन कैसे जोड़ें

## परिचय

अपने जावा वर्कबुक में ग्लोबलाइज़ेशन जोड़ने से आप त्रुटि संदेश, बूलियन मान और अन्य स्थानीय‑विशिष्ट स्ट्रिंग्स को उपयोगकर्ताओं की अपेक्षित भाषा में प्रस्तुत कर सकते हैं। इस ट्यूटोरियल में आप **रूसी के लिए ग्लोबलाइज़ेशन कैसे जोड़ें** सीखेंगे, लेकिन यही पैटर्न किसी भी भाषा के लिए काम करता है। गाइड के अंत तक आप सक्षम होंगे:

- डिफ़ॉल्ट त्रुटि टेक्स्ट और बूलियन प्रतिनिधित्व को ओवरराइड करना।
- अपनी कस्टम सेटिंग्स को किसी भी `Workbook` इंस्टेंस पर लागू करना।
- समाधान को सामान्य Maven‑आधारित जावा प्रोजेक्ट में एकीकृत करना।

क्या आप अपने Excel फ़ाइलों को वास्तव में बहुभाषी बनाना चाहते हैं? पहले यह सुनिश्चित करें कि आपका विकास वातावरण आवश्यकताओं को पूरा करता है।

## त्वरित उत्तर
- **Aspose.Cells में ग्लोबलाइज़ेशन क्या है?** यह स्थानीय‑सचेत स्ट्रिंग्स (त्रुटियां, बूलियन आदि) का सेट है जिसे आप कस्टम टेक्स्ट से बदल सकते हैं।  
- **कौन सा Maven आर्टिफैक्ट आवश्यक है?** `com.aspose:aspose-cells:25.3`।  
- **क्या मैं रूसी के अलावा अन्य भाषाओं को लक्षित कर सकता हूँ?** हाँ – `GlobalizationSettings` को विस्तारित करें और प्रत्येक स्थानीय के लिए आवश्यक मेथड्स को ओवरराइड करें।  
- **क्या विकास के लिए लाइसेंस चाहिए?** परीक्षण के लिए एक फ्री ट्रायल काम करता है; एक स्थायी लाइसेंस मूल्यांकन वॉटरमार्क हटाता है।  
- **क्या समाधान थ्रेड‑सेफ़ है?** प्रति‑वर्कबुक सेटिंग्स लागू करें; `GlobalizationSettings` ऑब्जेक्ट निर्माण के बाद अपरिवर्तनीय रहता है।

## Aspose.Cells में ग्लोबलाइज़ेशन क्या है?

`GlobalizationSettings` Aspose.Cells का कॉन्फ़िगरेशन ऑब्जेक्ट है जो त्रुटि संदेश, बूलियन मान, मुद्रा प्रतीक और तिथि पैटर्न जैसी स्थानीय‑विशिष्ट स्ट्रिंग्स को नियंत्रित करता है। अपना स्वयं का सबक्लास प्रदान करके आप लाइब्रेरी को बताते हैं कि प्रत्येक संस्कृति के लिए कौन सा टेक्स्ट दिखाना है, जिससे आप डिफ़ॉल्ट अंग्रेज़ी स्ट्रिंग्स को ऐसे अनुवादों से बदल सकते हैं जो अंतिम‑उपयोगकर्ता की भाषा और क्षेत्रीय मानकों से मेल खाते हों।

## कस्टम ग्लोबलाइज़ेशन क्यों जोड़ें?

Aspose.Cells **50+ इनपुट और आउटपुट फ़ॉर्मैट** को सपोर्ट करता है – जिसमें XLSX, CSV, PDF और ODS शामिल हैं – और **200 000 पंक्तियों** तक के वर्कबुक को पूरी फ़ाइल को मेमोरी में लोड किए बिना प्रोसेस कर सकता है। ग्लोबलाइज़ेशन को कस्टमाइज़ करने से अंतिम‑उपयोगकर्ता अपनी मातृभाषा में संदेश देखता है, जिससे बहु‑राष्ट्रीय डिप्लॉयमेंट में समर्थन टिकटों में अनुमानित **30 %** की कमी आती है।

## पूर्वापेक्षाएँ

- **Java Development Kit** 8 या नया।
- **IDE** जैसे IntelliJ IDEA या Eclipse।
- **Aspose.Cells for Java** संस्करण 25.3 (या बाद का) Maven या Gradle के माध्यम से जोड़ा गया।

### Aspose.Cells for Java सेटअप करना

अपने `pom.xml` में Maven डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

या, यदि आप Gradle पसंद करते हैं, तो `build.gradle` में निम्नलिखित जोड़ें:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### लाइसेंस प्राप्त करना

Aspose कई लाइसेंस विकल्प प्रदान करता है:

- **Free trial** – 30 दिनों के लिए पूर्ण‑फ़ीचर मूल्यांकन।  
- **Temporary license** – वॉटरमार्क के बिना अनलिमिटेड मूल्यांकन।  
- **Commercial license** – प्रोडक्शन‑रेडी, प्रायोरिटी सपोर्ट के साथ।

लाइसेंस फ़ाइल प्राप्त करने के बाद, एप्लिकेशन स्टार्टअप पर इसे एक बार सेट करें:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## रूसी के लिए ग्लोबलाइज़ेशन कैसे जोड़ें?

`Workbook` ऑब्जेक्ट एक Excel फ़ाइल का प्रतिनिधित्व करता है जो मेमोरी में लोड होती है, और आपको उसकी शीट्स, सेल्स और सेटिंग्स तक पहुंच प्रदान करती है। अपना वर्कबुक लोड करें, `GlobalizationSettings` का एक सबक्लास बनाएं, और उसे वर्कबुक से जोड़ें। सीधा उत्तर है: **एक कस्टम `GlobalizationSettings` क्लास को इंस्टैंशिएट करें, `getErrorValueString` और `getBooleanValueString` को ओवरराइड करें, फिर `workbook.setGlobalizationSettings(customSettings)` को कॉल करें**। यह दो‑स्टेप दृष्टिकोण डिफ़ॉल्ट रूसी स्ट्रिंग्स को आपके अपने स्ट्रिंग्स से बदल देता है।

### कस्टम सेटिंग्स परिभाषित करना

इस गाइड में पहली बार जब आप `GlobalizationSettings` का उल्लेख करते हैं, तो परिभाषा नोट करें:

`GlobalizationSettings` वह बेस क्लास है जिसे Aspose.Cells स्थानीय‑विशिष्ट स्ट्रिंग्स प्राप्त करने के लिए उपयोग करता है।  

अब एक सबक्लास बनाएं जो रूसी‑विशिष्ट टेक्स्ट रिटर्न करे:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### सेटिंग्स को वर्कबुक पर लागू करना

सबक्लास परिभाषित करने के बाद, इसे किसी भी `Workbook` इंस्टेंस से जोड़ें:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## व्यावहारिक उपयोग

- **वित्तीय रिपोर्टिंग** – लेखाकार की मातृभाषा में त्रुटि कोड दिखाएँ, जिससे गलतफ़हमी कम हो।  
- **एंटरप्राइज़‑व्यापी टूल्स** – कई आंतरिक Excel‑आधारित यूटिलिटीज़ में समान ग्लोबलाइज़ेशन लॉजिक एम्बेड करें।  
- **स्वचालित डेटा पाइपलाइन** – सुनिश्चित करें कि डाउनस्ट्रीम सिस्टम स्थानीय‑सचेत मान प्राप्त करें बिना अतिरिक्त अनुवाद चरणों के।

## प्रदर्शन संबंधी विचार

जब आप कस्टम ग्लोबलाइज़ेशन सक्षम करते हैं, तब भी Aspose.Cells फ़ॉर्मूला और I/O को समान उच्च प्रदर्शन के साथ प्रोसेस करता है। मेमोरी उपयोग कम रखने के लिए:

- सहेजने के बाद वर्कबुक रेफ़रेंसेज़ को रिलीज़ करें (`wb.dispose()`)।  
- केवल आवश्यक होने पर `CalculationOptions.setEnableIterativeCalculation(true)` का उपयोग करें।  
- 100 MB से बड़े वर्कबुक के लिए JVM हीप (`-Xmx2g`) को ट्यून करें।

## अक्सर पूछे जाने वाले प्रश्न

**प्रश्न: क्या मैं एक ही ग्लोबलाइज़ेशन सेटिंग्स को कई वर्कबुक पर एक साथ लागू कर सकता हूँ?**  
उत्तर: हाँ। एक `RussianGlobalization` इंस्टेंस बनाएं और `setGlobalizationSettings` के माध्यम से प्रत्येक वर्कबुक को पास करें।

**प्रश्न: यदि मुझे ऐसी भाषा का समर्थन करना है जो दाएँ‑से‑बाएँ स्क्रिप्ट उपयोग करती है तो क्या करें?**  
उत्तर: अपने सबक्लास में अतिरिक्त मेथड्स जैसे `getCurrencySymbol` और `getDatePattern` को ओवरराइड करके उपयुक्त RTL प्रतीक रिटर्न करें।

**प्रश्न: क्या कस्टम ग्लोबलाइज़ेशन उपयोग करने के लिए ट्रायल संस्करण में लाइसेंस आवश्यक है?**  
उत्तर: नहीं। ट्रायल संस्करण पूरी तरह `GlobalizationSettings` को सपोर्ट करता है; केवल कुछ आउटपुट फ़ॉर्मैट्स पर मूल्यांकन वॉटरमार्क दिखते हैं।

**प्रश्न: गलत त्रुटि स्ट्रिंग्स को कैसे डिबग करें?**  
उत्तर: अपने ओवरराइडेड मेथड्स के अंदर `System.out.println` स्टेटमेंट डालें ताकि इनपुट `err` वैल्यू आपके स्विच केस से मेल खाती हो यह सत्यापित किया जा सके।

**प्रश्न: क्या इससे फ़ॉर्मूला कैलकुलेशन गति प्रभावित होती है?**  
उत्तर: नगण्य रूप से। लाइब्रेरी स्ट्रिंग को केवल सेल वैल्यू रेंडर करते समय लुक अप करती है, न कि मध्यवर्ती कैलकुलेशन चरणों में।

## अतिरिक्त संसाधन

- **डॉक्यूमेंटेशन**: विस्तृत गाइड्स के लिए देखें [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **डाउनलोड**: नवीनतम रिलीज़ के लिए जाएँ [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **खरीदें**: व्यावसायिक उपयोग के लिए लाइसेंस खरीदें [Aspose Purchase](https://purchase.aspose.com/buy)  
- **फ्री ट्रायल**: शुरू करने के लिए फ्री ट्रायल प्राप्त करें [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **टेम्पररी लाइसेंस**: टेम्पररी लाइसेंस प्राप्त करें [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **सपोर्ट**: समुदाय से मदद लें [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**अंतिम अपडेट:** 2026-08-16  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose

## संबंधित ट्यूटोरियल

- [Aspose.Cells Java: Custom Calculation Engine Guide](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [How to Use Aspose Cells – Excel Engine Tutorials for Java](/cells/java/calculation-engine/)
- [Aspose Cells Maven Dependency – Manage Excel Data Connections with Aspose.Cells in Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}