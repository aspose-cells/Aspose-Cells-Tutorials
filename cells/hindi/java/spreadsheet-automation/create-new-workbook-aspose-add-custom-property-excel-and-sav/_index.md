---
category: general
date: 2026-08-11
description: Java में Aspose का उपयोग करके नया वर्कबुक बनाएं, Excel में एक कस्टम प्रॉपर्टी
  जोड़ें, फिर पूर्ण चरण‑दर‑चरण उदाहरण के साथ वर्कबुक को XLSB के रूप में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: hi
lastmod: 2026-08-11
og_description: Java में Aspose के साथ नया वर्कबुक बनाएं, Excel में एक कस्टम प्रॉपर्टी
  जोड़ें, और वर्कबुक को XLSB के रूप में सहेजें, साथ ही एक पूर्ण, तुरंत चलाने योग्य
  उदाहरण प्रदान करें।
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Aspose के साथ नया वर्कबुक बनाएं – Excel में कस्टम प्रॉपर्टी जोड़ें
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: नया वर्कबुक बनाएं Aspose – Excel में कस्टम प्रॉपर्टी जोड़ें और इसे XLSB के
  रूप में सहेजें
url: /hi/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# नया workbook Aspose बनाएं – कस्टम प्रॉपर्टी Excel जोड़ें और XLSB के रूप में सहेजें

यदि आपको Java एप्लिकेशन में **create new workbook Aspose** करने की आवश्यकता है, तो यह गाइड आपको ठीक-ठीक बताता है कि कैसे करना है। आप **add custom property Excel** करना, मान प्राप्त करना, और **save workbook as XLSB** बिना किसी मेटाडेटा को खोए सीखेंगे।

यह ट्यूटोरियल प्रोजेक्ट सेटअप से लेकर सहेजी गई फ़ाइल की पुष्टि तक सब कुछ कवर करता है। कोई बाहरी दस्तावेज़ीकरण आवश्यक नहीं है; बस चरणों का पालन करें और कोड चलाएँ।

## पूर्वापेक्षाएँ

- Java Development Kit (JDK) 8 या उससे ऊपर स्थापित हो।
- निर्भरताओं को प्रबंधित करने के लिए Maven या Gradle (उदाहरण में Maven उपयोग किया गया है)।
- एक सक्रिय Aspose.Cells for Java लाइसेंस (या परीक्षण के लिए मुफ्त इवैल्यूएशन मोड का उपयोग करें)।

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

`pom.xml` में Aspose.Cells Maven आर्टिफैक्ट जोड़ें। यह डिपेंडेंसी **create new workbook Aspose** ऑब्जेक्ट बनाने के लिए आवश्यक क्लासेज़ प्रदान करती है।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** यदि आप Gradle पसंद करते हैं, तो Maven स्निपेट को समकक्ष `implementation "com.aspose:aspose-cells:23.12"` लाइन से बदल दें।

## चरण 2: नया workbook Aspose बनाएं

पहला कार्यात्मक कदम `Workbook` ऑब्जेक्ट को इंस्टैंशिएट करना है। यह ऑब्जेक्ट मेमोरी में एक Excel फ़ाइल का प्रतिनिधित्व करता है और आगे की सभी ऑपरेशन्स का एंट्री पॉइंट है।

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

नया workbook Aspose बनाने से आपको एक साफ़ workbook मिलता है जिसमें डिफ़ॉल्ट वर्कशीट होती है, जो कस्टमाइज़ेशन के लिए तैयार है।

## चरण 3: कस्टम प्रॉपर्टी Excel जोड़ें

कस्टम प्रॉपर्टीज़ आपको Excel फ़ाइल के अंदर मनमाना मेटाडेटा स्टोर करने देती हैं। यहाँ हम `ProjectId` नाम की **add custom property Excel** को एक संख्यात्मक मान के साथ जोड़ते हैं।

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

`add` मेथड प्रॉपर्टी का नाम और किसी भी समर्थित प्रकार (string, number, date आदि) का मान स्वीकार करता है। यह मेटाडेटा फ़ाइल के साथ कहीं भी कॉपी करने पर साथ रहता है।

## चरण 4: कस्टम प्रॉपर्टी को प्राप्त करें और प्रदर्शित करें

प्रॉपर्टी को पढ़ना यह सत्यापित करता है कि वह सही ढंग से संग्रहीत हुई है। आप प्राप्त मान को अपने बिज़नेस लॉजिक में भी उपयोग कर सकते हैं।

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

`int` में कास्ट करना काम करता है क्योंकि हमने संख्यात्मक मान स्टोर किया था। यदि आप स्ट्रिंग स्टोर करते हैं, तो `(String)` का उपयोग करें।

## चरण 5: workbook को XLSB के रूप में सहेजें

अब आप **save workbook as XLSB** करेंगे। XLSB फ़ॉर्मेट workbook को बाइनरी प्रतिनिधित्व में स्टोर करता है, जिससे खोलना तेज़ और डिस्क पर आकार छोटा रहता है। सभी कस्टम प्रॉपर्टीज़ स्वचालित रूप से संरक्षित रहती हैं।

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

यदि आपको फ़ाइल किसी विशिष्ट डायरेक्टरी में चाहिए तो `"WithCustomProps.xlsb"` को पूर्ण पाथ से बदलें। `SaveFormat.XLSB` एनेम Aspose.Cells को बाइनरी फ़ॉर्मेट लिखने के लिए बताता है।

## चरण 6: आउटपुट को सत्यापित करें

IDE या कमांड लाइन से प्रोग्राम चलाएँ:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

आपको यह दिखना चाहिए:

```
ProjectId = 12345
```

Excel में `WithCustomProps.xlsb` खोलें। **File → Info → Properties → Advanced Properties → Custom** पर जाएँ। `ProjectId` एंट्री जिसका मान `12345` है, सूचीबद्ध होगी, जिससे यह पुष्टि होगी कि **add custom property excel** चरण सफल रहा और **save workbook as xlsb** ऑपरेशन ने मेटाडेटा को बरकरार रखा।

## सामान्य प्रश्न और किनारे के मामले

### यदि मुझे स्ट्रिंग प्रॉपर्टी स्टोर करनी हो तो क्या करें?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

इसे इस प्रकार प्राप्त करें:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### क्या मैं एक साथ कई कस्टम प्रॉपर्टीज़ जोड़ सकता हूँ?

हाँ। प्रत्येक नाम/मान जोड़े के लिए `add` को बार‑बार कॉल करें। Aspose.Cells कस्टम प्रॉपर्टीज़ की संख्या पर कोई सीमा नहीं लगाता, लेकिन फ़ाइल को बloat होने से बचाने के लिए कुल आकार को यथोचित रखें।

### बाइनरी फ़ॉर्मेट प्रदर्शन को कैसे प्रभावित करता है?

XLSB फ़ाइलें तेज़ लोड होती हैं क्योंकि वे XML पार्सिंग से बचती हैं। यह विशेष रूप से उन workbooks के लिए स्पष्ट होता है जिनमें कई पंक्तियाँ, फ़ॉर्मूले या एम्बेडेड इमेज़ होते हैं।

### यदि मुझे मौजूदा XLSX फ़ाइल के साथ काम करना हो तो क्या करें?

`new Workbook()` कन्स्ट्रक्टर को `new Workbook("ExistingFile.xlsx")` से बदलें। बाकी चरण (प्रॉपर्टीज़ जोड़ना, XLSB के रूप में सहेजना) समान रहते हैं।

## पूरा स्रोत कोड

नीचे पूर्ण, तैयार‑चलाने‑योग्य उदाहरण दिया गया है। इसे `CustomPropertiesXlsb.java` नाम की फ़ाइल में कॉपी करें और अपने `src/main/java` फ़ोल्डर में रखें।

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

इस क्लास को चलाने से एक XLSB फ़ाइल बनती है जिसमें कस्टम प्रॉपर्टी होती है और इसे किसी भी आधुनिक Microsoft Excel संस्करण में खोला जा सकता है।

## निष्कर्ष

अब आप Java का उपयोग करके **create new workbook Aspose**, **add custom property Excel**, और **save workbook as XLSB** करना जानते हैं। यह उदाहरण पूरी लाइफ़साइकल दिखाता है: इनिशियलाइज़ेशन, मेटाडेटा इन्जेक्शन, वैरिफिकेशन, और बाइनरी सीरियलाइज़ेशन।

अगले चरण में **setting document properties**, **working with Excel formulas**, या **converting between XLSX and XLSB** जैसे संबंधित विषयों को एक्सप्लोर करें। ये सभी वही Aspose.Cells API पर आधारित हैं जिसे आपने अभी इस्तेमाल किया, इसलिए आप नई लाइब्रेरी सीखे बिना समाधान को विस्तारित कर सकते हैं।

विभिन्न डेटा टाइप्स, कई वर्कशीट्स, या पासवर्ड प्रोटेक्शन के साथ प्रयोग करने में संकोच न करें—Aspose.Cells इन सभी परिदृश्यों को बॉक्स से बाहर सपोर्ट करता है। Happy coding!

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Excel Workbook Aspose Cells Java बनाएं और सहेजें](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java का उपयोग करके Excel Workbook को SVG के रूप में कैसे बनाएं और सहेजें](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Aspose.Cells for Java के साथ Excel Workbook बनाएं और लेबल जोड़ें](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}