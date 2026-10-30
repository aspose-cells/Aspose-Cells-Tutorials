---
category: general
date: 2026-07-16
description: Aspose.Cells का उपयोग करके जावा में एक्सेल को TXT में निर्यात करें। सीखें
  कि महत्वपूर्ण अंकों को कैसे सेट करें, एक्सेल को टेक्स्ट फ़ाइल के रूप में सहेजें,
  और आउटपुट फ़ॉर्मेट को नियंत्रित करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set significant digits
- save excel as text file
- save workbook as txt
language: hi
lastmod: 2026-07-16
og_description: Aspose.Cells के साथ जावा में एक्सेल को TXT में निर्यात करें। यह ट्यूटोरियल
  आपको दिखाता है कि महत्वपूर्ण अंकों को कैसे सेट करें, एक्सेल को टेक्स्ट फ़ाइल के
  रूप में कैसे सहेजें, और विश्वसनीय परिणाम कैसे प्राप्त करें।
og_image_alt: Screenshot of Java code exporting an Excel workbook to a TXT file with
  4 significant digits
og_title: जावा में एक्सेल को TXT में निर्यात करें – चरण‑दर‑चरण मार्गदर्शिका
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  headline: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Export Excel to TXT using Aspose.Cells in Java. Learn how to set significant
    digits, save Excel as text file, and control the output format.
  name: Export Excel to TXT with Java – Complete Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '- Java Development Kit (JDK) 8 or newer. - Maven or Gradle to manage the
      Aspose.Cells dependency (we’ll show the Maven snippet). - A basic understanding
      of Java syntax (if you’ve written a “Hello World”, you’re good).'
  - name: Understanding `setSignificantDigits`
    text: '- **Definition:** The number of digits that remain after the decimal point,
      *including* leading digits. For `123.456789` with `4` significant digits, the
      output becomes `123.5`. - **When to use:** If the downstream system expects
      a fixed precision (e.g., scientific data files), or you need to trunca'
  - name: Folder Considerations
    text: '- The `output` folder must exist, or you’ll get an `IOException`. You can
      create it programmatically:'
  - name: 1️⃣ What if I need a different delimiter?
    text: "`TxtSaveOptions` also offers `setSeparator('\t')` for tabs or `setSeparator(',')`
      for CSV‑style output. Example:"
  - name: 2️⃣ How does locale affect decimal separators?
    text: 'By default Aspose uses the system locale. If you need a period (`.`) regardless
      of locale, set:'
  - name: 3️⃣ Large worksheets – memory concerns?
    text: Aspose.Cells streams data to disk when working with worksheets larger than
      1 GB, so you usually won’t hit an `OutOfMemoryError`. Still, avoid loading massive
      sheets into memory if you only need a subset; use `Workbook.getWorksheets().get(index)`
      to target a specific sheet.
  - name: 4️⃣ Can I export only a range?
    text: Yes. Use `txtOptions.setExportRange("A1:B10")` to restrict the output to
      a specific area. This reduces file size and speeds up the export.
  - name: 5️⃣ What if I don’t have a license?
    text: The evaluation mode adds a watermark line (`"Aspose.Cells for Java Evaluation
      Version"`). For production you’ll need a license; otherwise the watermark may
      break downstream parsers.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: जावा के साथ एक्सेल को TXT में निर्यात करें – पूर्ण चरण-दर-चरण गाइड
url: /hi/java/excel-import-export/export-excel-to-txt-with-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा के साथ Excel को TXT में निर्यात करें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपने कभी सोचा है **Excel को TXT में कैसे निर्यात करें** बिना संख्यात्मक सटीकता खोए? शायद आपको लेगेसी सिस्टम के लिए एक साधारण‑टेक्स्ट डंप चाहिए, या आप डेटा को किसी वैज्ञानिक पाइपलाइन में फीड कर रहे हैं जो विशिष्ट महत्वपूर्ण अंकों की संख्या की अपेक्षा करता है। इस ट्यूटोरियल में हम एक **पूर्ण, चलाने योग्य जावा उदाहरण** के माध्यम से यह दिखाएंगे—साथ ही **महत्वपूर्ण अंकों को सेट करने**, **Excel को टेक्स्ट फ़ाइल के रूप में सहेजने**, और **वर्कबुक को txt के रूप में सहेजने** के बारे में Aspose.Cells का उपयोग करके।

हम प्रोजेक्ट सेटअप से लेकर अंतिम सत्यापन चरण तक सब कुछ कवर करेंगे, ताकि आप कोड को कॉपी‑पेस्ट कर सकें, चलाएँ, और तुरंत परिणाम देख सकें। कोई रहस्यमयी निर्भरताएँ नहीं, कोई “डॉक्यूमेंट देखें” शॉर्टकट नहीं—सिर्फ एक स्पष्ट, अंत‑से‑अंत समाधान।

---

## आप क्या सीखेंगे

- Aspose.Cells के साथ प्रोग्रामेटिक रूप से वर्कबुक बनाना।
- **TXT निर्यात** के लिए **महत्वपूर्ण अंकों को सेट करने** की सटीक API कॉल।
- `TxtSaveOptions` और अन्य सेव विकल्पों के बीच अंतर।
- किसी भी OS (Windows, macOS, Linux) पर **Excel को टेक्स्ट फ़ाइल के रूप में सहेजना**।
- सामान्य जाल (लोकल‑विशिष्ट दशमलव विभाजक, बड़े वर्कशीट) और उन्हें कैसे टालें।
- एक पूर्ण, तैयार‑चलाने‑योग्य जावा क्लास जिसे आप अपने प्रोजेक्ट में अनुकूलित कर सकते हैं।

### पूर्वापेक्षाएँ

- जावा डेवलपमेंट किट (JDK) 8 या नया।
- Maven या Gradle ताकि Aspose.Cells निर्भरता प्रबंधित की जा सके (हम Maven स्निपेट दिखाएंगे)।
- जावा सिंटैक्स की बुनियादी समझ (यदि आपने “Hello World” लिखा है, तो आप तैयार हैं)।

---

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose.Cells जोड़ें

सबसे पहले, लाइब्रेरी को अपने बिल्ड में जोड़ें। यदि आप Maven उपयोग कर रहे हैं, तो यह `pom.xml` में जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** Aspose एक मुफ्त 30‑दिन की इवैल्यूएशन लाइसेंस देता है। `Aspose.Total.lic` फ़ाइल को प्रोजेक्ट रूट में रखें, या किसी भी API उपयोग से पहले `License.setLicense("path/to/license")` कॉल करें।

एक बार निर्भरता हल हो जाने पर, आप कोड लिखना शुरू कर सकते हैं। यदि आप Gradle पसंद करते हैं, तो समकक्ष इस प्रकार है:

```gradle
implementation 'com.aspose:aspose-cells:24.9'
```

---

## चरण 2: Excel को TXT में निर्यात – वर्कबुक बनाएं

अब हम एक नई वर्कबुक बनाएँगे, एक संख्यात्मक मान जोड़ेंगे, और निर्यात के लिए तैयार करेंगे। यह **export excel to txt** का मुख्य भाग है।

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a fresh workbook (in‑memory Excel file)
        Workbook workbook = new Workbook();

        // 2️⃣ Grab the first worksheet – it's created by default
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 3️⃣ Put a numeric value into cell A1
        Cell cell = sheet.getCells().get("A1");
        cell.putValue(123.456789); // Example number with many decimals
```

**यह क्यों महत्वपूर्ण है:** कोड में वर्कबुक बनाकर हम किसी भी छिपे हुए फ़ॉर्मेटिंग से बचते हैं जो टेम्पलेट फ़ाइल से आ सकता है। `putValue` मेथड स्वचालित रूप से डेटा टाइप का पता लगाता है, इसलिए सेल **संख्यात्मक** बन जाता है—स्ट्रिंग नहीं।

---

## चरण 3: TXT आउटपुट के लिए महत्वपूर्ण अंकों को कैसे सेट करें

जब आप प्लेन टेक्स्ट में निर्यात करते हैं, तो Aspose.Cells डिफ़ॉल्ट रूप से कच्चा संख्यात्मक मान लिखता है। आउटपुट को, उदाहरण के लिए, **4 महत्वपूर्ण अंकों** तक सीमित करने के लिए आपको `TxtSaveOptions` को समायोजित करना होगा।

```java
        // 4️⃣ Configure TXT save options – this is where we set the precision
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4); // <-- controls significant digits
```

### `setSignificantDigits` को समझना

- **परिभाषा:** दशमलव बिंदु के बाद बचे हुए अंकों की संख्या, *सहित* अग्रणी अंकों के। `123.456789` को `4` महत्वपूर्ण अंकों के साथ सेट करने पर आउटपुट `123.5` बन जाता है।
- **कब उपयोग करें:** यदि डाउनस्ट्रीम सिस्टम एक निश्चित प्रिसीजन की अपेक्षा करता है (जैसे वैज्ञानिक डेटा फ़ाइलें), या आप फ़्लोटिंग‑पॉइंट शोर को हटाना चाहते हैं।
- **एज केस:** यदि संख्या में निर्दिष्ट गिनती से कम अंक हैं, तो Aspose मूल मान को जैसा है वैसा ही रखेगा (शून्य से पैड नहीं करेगा)।

> **`setDecimalPlaces` क्यों नहीं?** यह प्रॉपर्टी केवल दशमलव बिंदु के बाद के अंकों को नियंत्रित करती है, अग्रणी अंकों को अनदेखा करती है। वैज्ञानिक डेटा के लिए `significantDigits` आमतौर पर सही विकल्प है।

---

## चरण 4: Excel को टेक्स्ट फ़ाइल (TXT) के रूप में सहेजें

विकल्प तैयार होने के बाद, हम अंततः वर्कबुक को `.txt` फ़ाइल में लिखते हैं। यही **save workbook as txt** चरण है।

```java
        // 5️⃣ Persist the workbook as a TXT file
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Excel exported to TXT at: " + outputPath);
    }
}
```

### फ़ोल्डर विचार

- `output` फ़ोल्डर मौजूद होना चाहिए, अन्यथा आपको `IOException` मिलेगा। आप इसे प्रोग्रामेटिक रूप से बना सकते हैं:

```java
new java.io.File("output").mkdirs();
```

- Linux/macOS पर पाथ केस‑सेंसिटिव होते हैं; Windows पर नहीं। क्रॉस‑प्लेटफ़ॉर्म सुरक्षा के लिए लोअर‑केस फ़ोल्डर नाम रखें।

---

## चरण 5: परिणाम सत्यापित करें

प्रोग्राम चलाएँ (`mvn compile exec:java -Dexec.mainClass=ExportExcelToTxtDemo`) और `output/SignificantDigits.txt` खोलें। आपको यह दिखना चाहिए:

```
123.5
```

यह एकल पंक्ति पुष्टि करती है:

- वर्कबुक सफलतापूर्वक **टेक्स्ट फ़ाइल के रूप में सहेजी गई**।
- संख्यात्मक मान ने वह **4 महत्वपूर्ण अंक** लागू किए हैं जो हमने सेट किए थे।
- फ़ाइल में कोई अतिरिक्त कॉमा, टैब, या Excel‑विशिष्ट मेटाडेटा नहीं आया।

यदि आपको कई कॉलम के लिए टैब‑डिलिमिटेड लेआउट चाहिए, तो बस अधिक सेल भरें और Aspose स्वचालित रूप से टैब डाल देगा।

---

## सामान्य प्रश्न एवं एज केस

### 1️⃣ यदि मुझे अलग डिलीमीटर चाहिए तो?

`TxtSaveOptions` `setSeparator('\t')` के साथ टैब या `setSeparator(',')` के साथ CSV‑स्टाइल आउटपुट भी प्रदान करता है। उदाहरण:

```java
txtOptions.setSeparator('\t'); // Tab delimiter
```

### 2️⃣ लोकल कैसे दशमलव विभाजक को प्रभावित करता है?

डिफ़ॉल्ट रूप से Aspose सिस्टम लोकल का उपयोग करता है। यदि आप लोकल की परवाह किए बिना हमेशा डॉट (`.`) चाहते हैं, तो सेट करें:

```java
txtOptions.setCultureInfo(java.util.Locale.US);
```

### 3️⃣ बड़े वर्कशीट – मेमोरी की चिंता?

Aspose.Cells 1 GB से बड़े वर्कशीट के लिए डेटा को डिस्क पर स्ट्रीम करता है, इसलिए आमतौर पर `OutOfMemoryError` नहीं आएगा। फिर भी, यदि आपको केवल एक उपसमुच्चय चाहिए, तो मेमोरी बचाने के लिए `Workbook.getWorksheets().get(index)` से विशिष्ट शीट को टार्गेट करें।

### 4️⃣ क्या मैं केवल एक रेंज निर्यात कर सकता हूँ?

हाँ। `txtOptions.setExportRange("A1:B10")` का उपयोग करके आउटपुट को किसी विशेष क्षेत्र तक सीमित कर सकते हैं। इससे फ़ाइल आकार घटेगा और निर्यात तेज़ होगा।

### 5️⃣ यदि मेरे पास लाइसेंस नहीं है तो?

इवैल्यूएशन मोड एक वॉटरमार्क लाइन (`"Aspose.Cells for Java Evaluation Version"`) जोड़ता है। प्रोडक्शन के लिए आपको लाइसेंस चाहिए; अन्यथा वॉटरमार्क डाउनस्ट्रीम पार्सर को बाधित कर सकता है।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```java
import com.aspose.cells.*;

import java.io.File;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Ensure output directory exists
        new File("output").mkdirs();

        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // 2️⃣ Put several numbers to illustrate formatting
        sheet.getCells().get("A1").putValue(123.456789);
        sheet.getCells().get("A2").putValue(0.0012345);
        sheet.getCells().get("A3").putValue(98765.4321);

        // 3️⃣ Configure TXT options – 4 significant digits, tab delimiter
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(4);
        txtOptions.setSeparator('\t'); // optional, defaults to tab
        txtOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator

        // 4️⃣ Save as TXT
        String outPath = "output/SignificantDigits.txt";
        workbook.save(outPath, txtOptions);

        System.out.println("Export completed: " + outPath);
    }
}
```

ऊपर का कोड चलाने पर `output/SignificantDigits.txt` मिलेगा जिसमें:

```
123.5
0.001235
98770
```

ध्यान दें कि प्रत्येक संख्या **4 महत्वपूर्ण अंकों** नियम का पालन करती है, चाहे वह बहुत छोटी हो या बहुत बड़ी।

---

## निष्कर्ष

हमने जावा और Aspose.Cells का उपयोग करके **Excel को TXT में निर्यात करने** का **पूरा, स्व-समाहित तरीका** दिखाया, जिसमें **महत्वपूर्ण अंकों को सेट करना**, **Excel को टेक्स्ट फ़ाइल के रूप में सहेजना**, और **वर्कबुक को txt के रूप में सहेजना** शामिल है। मुख्य बिंदु:

- संख्यात्मक प्रिसीजन को नियंत्रित करने के लिए `TxtSaveOptions.setSignificantDigits` का उपयोग करें।
- आवश्यकतानुसार डिलीमीटर, संस्कृति, और निर्यात रेंज को समायोजित करें।
- कोड किसी भी प्लेटफ़ॉर्म पर काम करता है, केवल एक लाइब्रेरी की आवश्यकता है, और साफ़, व्हाइटस्पेस‑डिलिमिटेड टेक्स्ट उत्पन्न करता है जो डाउनस्ट्रीम प्रोसेसिंग के लिए तैयार है।

अगला कदम तैयार है? कई कॉलम जोड़ें, विभिन्न डिलीमीटर के साथ प्रयोग करें, या निर्यात को बड़े ETL पाइपलाइन में एकीकृत करें। यदि कोई अजीब बात आती है—शायद लोकल समस्या या बहुत बड़ी शीट—तो ऊपर के “सामान्य प्रश्न एवं एज केस” सेक्शन को फिर से देखें।

कोई उपयोग‑केस साझा करना चाहते हैं? टिप्पणी दें, या रिपॉज़िटरी फ़ोर्क करके पुल‑रिक्वेस्ट खोलें। कोडिंग का आनंद लें, और स्प्रेडशीट को साधारण टेक्स्ट में बदलने की सरलता का मज़ा उठाएँ!


## आगे आप क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में महारत हासिल कर सकें और अपने प्रोजेक्ट में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [How to Save Excel Files in Various Formats Using Aspose.Cells Java](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)
- [How to Load and Save Excel as CSV Using Aspose.Cells for Java&#58; A Comprehensive Guide](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}