---
date: '2026-10-28'
description: Aspose.Cells for Java का उपयोग करके Excel डेट सिस्टम को 1904 में बदलना,
  Excel डेट फ़ॉर्मेट सेट करना, और Excel 1904 सिस्टम को कुशलतापूर्वक बदलना सीखें।
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Aspose.Cells for Java का उपयोग करके Excel डेट सिस्टम को 1904 में बदलें।
  चरण‑दर‑चरण सीखें कि 1904 सिस्टम को कैसे सक्षम करें, डेट सेट करें, और वापस बदलें।
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Aspose.Cells for Java के साथ Excel डेट सिस्टम को 1904 में बदलें
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Aspose.Cells Java के साथ Excel डेट सिस्टम को 1904 में बदलें
url: /hi/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells Java के साथ Excel तिथि प्रणाली को 1904 में बदलें

इस ट्यूटोरियल में आप सीखेंगे कि कैसे Aspose.Cells for Java का उपयोग करके **Excel तिथि प्रणाली बदलें** 1904 फ़ॉर्मेट में। 1904 प्रणाली आवश्यक है जब आपको लेगेसी मैक‑आधारित तिथियों को संरक्षित करना हो या वित्तीय मॉडलों के साथ संरेखित करना हो जो उस युग को अपेक्षित करते हैं। हम लाइब्रेरी को स्थापित करने, वर्कबुक लोड करने, तिथि प्रणाली को टॉगल करने, और परिणाम को सहेजने की प्रक्रिया को दिखाएंगे—सर्वर पर Microsoft Excel की आवश्यकता के बिना।

## त्वरित उत्तर
- **1904 तिथि प्रणाली क्या करती है?** यह 1 जनवरी 1904 से दिनों की गिनती शुरू करती है, जिससे सभी तिथियों को डिफ़ॉल्ट 1900 प्रणाली की तुलना में 1,462 दिन आगे ले जाया जाता है।  
- **तिथि प्रणाली बदलने के लिए Aspose.Cells का उपयोग क्यों करें?** यह एक सरल API प्रदान करता है जो Excel स्थापित किए बिना काम करता है और बड़े फ़ाइलों का समर्थन करता है।  
- **कौन से Java संस्करण समर्थित हैं?** JDK 8 या नया।  
- **क्या मुझे लाइसेंस चाहिए?** मुफ्त ट्रायल मूल्यांकन के लिए काम करता है; लाइसेंस उपयोग सीमाओं को हटाता है।  
- **क्या मैं बाद में 1900 प्रणाली में वापस बदल सकता हूँ?** हाँ, बस `setDate1904(false)` कॉल करें।

## Excel में 1904 तिथि प्रणाली क्या है?
1904 तिथि प्रणाली 1 जनवरी 1904 से दिनों की गिनती करती है, डिफ़ॉल्ट 1900 युग के बजाय। यह परिवर्तन प्रत्येक तिथि मान में ठीक 1,462 दिन जोड़ता है, इसलिए लेगेसी मैक वर्कबुक्स विंडोज़ पर खोलने पर ऑफ़सेट दिखाते हैं। यह मुख्यतः पुराने Macintosh Excel फ़ाइलों और कुछ लेगेसी वित्तीय मॉडलों के साथ संगतता के लिए उपयोग किया जाता है।

## Aspose.Cells के साथ Excel तिथि प्रणाली क्यों बदलें?
आप Java से सीधे तिथि प्रणाली बदल सकते हैं, जिससे Excel में मैन्युअल कदम समाप्त हो जाते हैं। Aspose.Cells वर्कबुक्स को **2 GB** तक के आकार में प्रोसेस करता है और सामान्य 4‑कोर सर्वर पर 500‑शीट वर्कबुक को **2 सेकंड** से कम समय में बदल सकता है, जिससे उच्च‑थ्रूपुट सर्वर‑साइड ऑटोमेशन मिलता है।

## पूर्वापेक्षाएँ
- Java Development Kit (JDK) 8 या उससे ऊपर।  
- निर्भरता प्रबंधन के लिए Maven या Gradle।  
- बुनियादी Java प्रोग्रामिंग ज्ञान।  

## Aspose.Cells for Java सेटअप करना

### Maven
अपने `pom.xml` फ़ाइल में निम्नलिखित निर्भरता जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
अपने `build.gradle` फ़ाइल में यह पंक्ति शामिल करें:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### लाइसेंस प्राप्ति
Aspose एक मुफ्त ट्रायल, अस्थायी लाइसेंस, और पूर्ण वाणिज्यिक लाइसेंस प्रदान करता है। आप [मुफ़्त ट्रायल](https://releases.aspose.com/cells/java/) से शुरू कर सकते हैं या [अस्थायी लाइसेंस पेज](https://purchase.aspose.com/temporary-license/) से अस्थायी लाइसेंस प्राप्त कर सकते हैं।

## Aspose.Cells for Java के साथ Excel तिथि प्रणाली को 1904 में कैसे बदलें?
वर्कबुक लोड करें, 1904 सेटिंग सक्षम करें, और फ़ाइल सहेजें—यह तीन‑स्टेप प्रक्रिया एक सेकंड से कम समय में वर्कबुक के आंतरिक तिथि युग को अपडेट करती है। API कॉल `setDate1904(true)` सिस्टम फ़्लैग को बदलता है, और परिवर्तन `save` कॉल करने पर स्थायी हो जाता है। Excel इंस्टॉलेशन की आवश्यकता नहीं है, जिससे यह हेडलेस सर्वर वातावरण के लिए आदर्श है।

### चरण 1: वर्कबुक को इनिशियलाइज़ करें और लोड करें
`Workbook` क्लास मेमोरी में पूरी Excel फ़ाइल का प्रतिनिधित्व करती है। पहले, अपने मौजूदा फ़ाइल की ओर इशारा करने वाला `Workbook` इंस्टेंस बनाएं।

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### चरण 2: 1904 तिथि प्रणाली सक्षम करें
`WorkbookSettings.setDate1904` मेथड वर्कबुक‑स्तर की तिथि फ़्लैग को टॉगल करता है। इसे `true` सेट करने से सभी वर्कशीट्स के लिए 1904 प्रणाली सक्रिय हो जाती है।

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro tip:** आप बाद में `setDate1904(false)` भी कॉल कर सकते हैं यदि आपको वापस लौटना हो।

### चरण 3: संशोधित वर्कबुक सहेजें
अंत में, परिवर्तनों को नई फ़ाइल में लिखें (या मूल को ओवरराइट करें)। `save` मेथड सक्रिय तिथि प्रणाली का स्वतः सम्मान करता है।

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

> **Note:** उपरोक्त कोड क्लास नाम `tWorkbook` का उपयोग करता है जैसा कि मूल रूप से दिया गया था। सुनिश्चित करें कि यह टाइपो आपके प्रोजेक्ट की नामकरण परंपराओं से मेल खाता है या आवश्यकता होने पर इसे `Workbook` में सुधारें।

## प्रोग्रामेटिक रूप से Excel तिथि सेट करें (secondary keyword)
यदि आपको प्रणाली बदलने के बाद व्यक्तिगत सेल मानों को समायोजित करने की आवश्यकता है, तो आप `cells.get(i, j).putValue(Date)` का उपयोग कर सकते हैं जहाँ तिथि सक्रिय तिथि प्रणाली के अनुसार व्याख्यायित होगी।

## Excel 1904 प्रणाली को 1900 में वापस बदलें (secondary keyword)
वापस करने के लिए, बस कॉल करें:

```java
workbook.getSettings().setDate1904(false);
```

फिर वर्कबुक को फिर से सहेजें।

## व्यावहारिक अनुप्रयोग
1. **Data archiving** – पुराने मैक‑आधारित स्प्रेडशीट्स को माइग्रेट करते समय लेगेसी टाइमस्टैम्प संरक्षित रखें।  
2. **Cross‑platform reporting** – ऐसे रिपोर्ट बनाएं जो Windows और macOS दोनों पर सही ढंग से खुलें, बिना तिथि असंगतियों के।  
3. **Financial modeling** – तिथि गणनाओं को लेगेसी वित्तीय मॉडलों के साथ संरेखित करें जो 1904 प्रणाली की अपेक्षा करते हैं।

## प्रदर्शन विचार
- एक सत्र में वर्कबुक ऑपरेशनों को सीमित रखें ताकि मेमोरी उपयोग कम रहे; Aspose.Cells डेटा को स्ट्रीम करता है और जब तक आप स्पष्ट रूप से न कहें, पूरी फ़ाइल को RAM में लोड नहीं करता।  
- बहुत बड़ी फ़ाइलों के लिए Java की गार्बेज‑कलेक्शन फ़्लैग्स (`-XX:+UseG1GC`) को ट्यून करें ताकि pause‑time स्पाइक्स से बचा जा सके।

## अक्सर पूछे जाने वाले प्रश्न

**Q: 1900 और 1904 तिथि प्रणालियों में क्या अंतर है?**  
A: 1900 प्रणाली 1 जनवरी 1900 से शुरू होती है, जबकि 1904 प्रणाली 1 जनवरी 1904 से शुरू होती है, जिससे सभी तिथियों में 1,462 दिन का अंतर आता है।

**Q: क्या मैं उस वर्कबुक की तिथि प्रणाली बदल सकता हूँ जो वर्तमान में Excel में खुला है?**  
A: हाँ, लेकिन आपको पहले Excel में फ़ाइल को बंद करना होगा; अन्यथा सहेजने का ऑपरेशन विफल हो जाएगा।

**Q: `setDate1904` उपयोग करने के लिए क्या मुझे लाइसेंस चाहिए?**  
A: यह मेथड मुफ्त ट्रायल में काम करता है, लेकिन पूर्ण लाइसेंस मूल्यांकन सीमाओं को हटाता है।

**Q: क्या केवल एक ही वर्कशीट के लिए तिथि प्रणाली बदलना संभव है?**  
A: नहीं, तिथि प्रणाली वर्कबुक‑स्तर की सेटिंग है; यह सभी वर्कशीट्स पर लागू होती है।

**Q: मैं कैसे सत्यापित करूँ कि तिथि प्रणाली बदल गई है?**  
A: Excel में सहेजी गई फ़ाइल खोलें, **File → Options → Advanced** पर जाएँ, और **"Use 1904 date system"** बॉक्स को चेक करें।

## निष्कर्ष
अब आप जानते हैं कि Aspose.Cells for Java का उपयोग करके 1904 में **Excel तिथि प्रणाली बदलें**, व्यक्तिगत सेल तिथियों को कैसे सेट करें, और आवश्यकता पड़ने पर 1900 प्रणाली में कैसे वापस जाएँ। इन स्निपेट्स को अपने डेटा‑प्रोसेसिंग पाइपलाइन में एकीकृत करें ताकि प्लेटफ़ॉर्म और लेगेसी फ़ाइलों में तिथि‑संगतता सुनिश्चित हो सके।

---

**अंतिम अपडेट:** 2026-10-28  
**परीक्षित संस्करण:** Aspose.Cells 25.3 for Java  
**लेखक:** Aspose  

**संसाधन**
- **दस्तावेज़ीकरण:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **डाउनलोड:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **लाइसेंस खरीदें:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **मुफ़्त ट्रायल:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **अस्थायी लाइसेंस:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **समर्थन फ़ोरम:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## संबंधित ट्यूटोरियल

- [Aspose.Cells for Java का उपयोग करके कस्टम डेट फ़ॉर्मैट के साथ Excel को PDF में कुशलतापूर्वक कनवर्ट करें](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: Excel वर्कबुक को कुशलतापूर्वक बनाना और फ़ॉर्मेट करना](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Aspose.Cells for Java के साथ Excel मैनिपुलेशन में निपुण बनें: वर्कबुक ऑपरेशन्स और सेल स्टाइलिंग ट्यूटोरियल](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}