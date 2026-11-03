---
category: general
date: 2026-10-16
description: Aspose.Cells जावा में EXPAND फ़ंक्शन का उपयोग करके फ़ॉर्मूला सेट करता
  है। चरण‑दर‑चरण उदाहरण सीखें और देखें कि डायनेमिक रेंज के लिए EXPAND का उपयोग कैसे
  किया जाता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- aspose cells set formula
- how to use expand
- expand function example
- Java Excel automation
- dynamic range formula
language: hi
lastmod: 2026-10-16
og_description: Aspose.Cells जावा में EXPAND फ़ंक्शन का उपयोग करके फ़ॉर्मूला सेट करता
  है। एक्सेल वर्कबुक में रेंज को गतिशील रूप से विस्तारित करने के लिए एक पूर्ण उदाहरण
  देखें।
og_image_alt: Spreadsheet screenshot showing the EXPAND formula applied to cell B2
  via Aspose.Cells
og_title: Aspose.Cells में EXPAND के साथ फ़ॉर्मूला सेट करना – Java ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-10-16'
  description: Aspose.Cells set formula in Java using the EXPAND function. Learn a
    step‑by‑step example and see how to use expand for dynamic ranges.
  headline: Aspose.Cells set formula with EXPAND function – complete Java guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel formulas
- Spreadsheet automation
title: Aspose.Cells में EXPAND फ़ंक्शन के साथ फ़ॉर्मूला सेट करना – पूर्ण Java गाइड
url: /hi/java/formulas-functions/aspose-cells-set-formula-with-expand-function-complete-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells set formula with EXPAND function – पूर्ण Java गाइड

यदि आपको प्रोग्रामेटिक रूप से **aspose cells set formula** करने की आवश्यकता है, तो यह ट्यूटोरियल आपको बिल्कुल सही तरीका दिखाता है। आप सीखेंगे कि कैसे EXPAND फ़ंक्शन का उपयोग करके एक डायनेमिक रेंज बनाई जाए जो प्रारंभिक सेल से पाँच पंक्तियों और पाँच कॉलम तक विस्तारित हो, वह भी पूरी तरह से Java कोड से।

Java से Excel फ़ॉर्मूले के साथ काम करना अक्सर जटिल लगता है, लेकिन Aspose.Cells जटिलता को सरल बनाता है। नीचे दिए गए सेक्शन में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे, प्रत्येक लाइन का महत्व समझाएंगे, और सामान्य वैरिएशन जैसे विभिन्न प्रारंभिक सेल या वैरिएबल एक्सपैंशन साइज को भी देखेंगे।

## इस ट्यूटोरियल में क्या कवर किया गया है

* Aspose.Cells के साथ मौजूदा वर्कबुक लोड करना  
* वर्कशीट और उसकी सेल्स कलेक्शन तक पहुंचना  
* `EXPAND` फ़ंक्शन का उपयोग करके **aspose cells set formula** करना  
* फ़ॉर्मूला के मूल्यांकन के लिए वर्कबुक को पुनः‑गणना करना  
* परिणाम को सेव करना और आउटपुट की पुष्टि करना  

Aspose.Cells के अलावा कोई बाहरी लाइब्रेरी आवश्यक नहीं है, और कोड किसी भी Java 8+ रनटाइम पर चलता है। अंत तक आप इस पैटर्न को अन्य डायनेमिक फ़ॉर्मूले के लिए अनुकूलित कर पाएँगे।

## पूर्वापेक्षाएँ

* Java Development Kit (JDK) 8 या नया  
* Aspose.Cells for Java (डाउनलोड करें [official site](https://downloads.aspose.com/cells/java) से)  
* एक इनपुट Excel फ़ाइल (`input.xlsx`) जिसे ज्ञात डायरेक्टरी में रखें  
* Java सिंटैक्स और Maven/Gradle के बेसिक ज्ञान  

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose.Cells जोड़ें

यदि आप Maven उपयोग कर रहे हैं, तो अपने `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

Gradle के लिए समकक्ष है:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** हमेशा नवीनतम स्थिर संस्करण का उपयोग करें; नए रिलीज़ में फ़ॉर्मूला कैलकुलेशन के लिए प्रदर्शन सुधार शामिल होते हैं।

## चरण 2: वर्कबुक लोड करें

हमारे समाधान की पहली लाइन मौजूदा वर्कबुक को खोलती है। `YOUR_DIRECTORY` को उस पूर्ण पाथ से बदलें जहाँ `input.xlsx` स्थित है।

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*यह क्यों महत्वपूर्ण है*: वर्कबुक को लोड करने से मेमोरी में एक प्रतिनिधित्व बनता है जिससे आप फ़ाइल सिस्टम को फिर से छुए बिना वर्कशीट, सेल और फ़ॉर्मूले को बदल सकते हैं।

## चरण 3: लक्ष्य वर्कशीट और सेल्स कलेक्शन तक पहुंचें

हम पहली वर्कशीट (इंडेक्स 0) के साथ काम करेंगे। `Cells` ऑब्जेक्ट आपको एड्रेस द्वारा व्यक्तिगत सेल्स तक सीधे पहुंच देता है।

```java
        // Access the first worksheet
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();
```

यदि आपको किसी अलग शीट की जरूरत है, तो इंडेक्स बदलें या `get("SheetName")` का उपयोग करें।

## चरण 4: **aspose cells set formula** – EXPAND फ़ंक्शन लागू करें

अब हम सेल **B2** में फ़ॉर्मूला सेट करेंगे। `EXPAND` फ़ंक्शन तीन आर्ग्यूमेंट लेता है: रेफ़रेंस सेल, विस्तारित करने के लिए पंक्तियों की संख्या, और विस्तारित करने के लिए कॉलम की संख्या।

```java
        // Apply the EXPAND function to B2, expanding 5 rows and 5 columns from A2
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");
```

### EXPAND का उपयोग कैसे करें

* **रेफ़रेंस सेल (`A2`)** – डायनेमिक रेंज का प्रारंभिक बिंदु।  
* **Rows (`5`)** – रेंज को नीचे की ओर कितनी पंक्तियों तक बढ़ाना है।  
* **Columns (`5`)** – रेंज को दाईं ओर कितनी कॉलम तक बढ़ाना है।

यदि आपको लचीला समाधान चाहिए तो इन मानों को वैरिएबल्स से बदल सकते हैं:

```java
int rows = 10;
int cols = 3;
cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));
```

## चरण 5: वर्कबुक को पुनः‑गणना करें

फ़ॉर्मूला सेट करने के बाद, आपको Aspose.Cells को इसे मूल्यांकन करने के लिए कहना होगा। `calculateFormula()` मेथड वर्कबुक में सभी फ़ॉर्मूले को प्रोसेस करता है।

```java
        // Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();
```

> **पुनः‑गणना क्यों?**  
> इस कॉल के बिना फ़ॉर्मूला अनइवैल्यूएटेड रहता है और आउटपुट फ़ाइल में केवल कच्चा `=EXPAND(...)` स्ट्रिंग दिखेगा, विस्तारित एरे नहीं।

## चरण 6: अपडेटेड वर्कबुक को सेव करें

अंत में, बदलावों को नई फ़ाइल में लिखें। इससे मूल वर्कबुक तुलना के लिए सुरक्षित रहता है।

```java
        // Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

जब आप `output.xlsx` को Excel में खोलेंगे, तो सेल **B2** में 5 × 5 ब्लॉक वैल्यूज़ दिखेंगे जो **A2** से शुरू होने वाले क्षेत्र से कॉपी किए गए हैं। यदि **A2** में संख्या `1` थी, तो ब्लॉक के सभी सेल में `1` दिखेगा क्योंकि `EXPAND` स्रोत वैल्यू को विस्तारित रेंज में दोहराता है।

## पूर्ण, चलाने योग्य स्रोत कोड

```java
import com.aspose.cells.*;

public class ExpandFunctionDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Load an existing workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Step 2: Access the first worksheet and its cells collection
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Step 3: Apply the EXPAND function to cell B2, referencing A2 and expanding 5 rows and 5 columns
        cells.get("B2").setFormula("=EXPAND(A2,5,5)");

        // Step 4: Recalculate the workbook so the formula is evaluated
        workbook.calculateFormula();

        // Step 5: Save the updated workbook
        workbook.save("YOUR_DIRECTORY/output.xlsx");
    }
}
```

### अपेक्षित आउटपुट

| B2 | C2 | D2 | E2 | F2 |
|----|----|----|----|----|
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |
| 1  | 1  | 1  | 1  | 1  |

(वास्तविक मान आपके स्रोत फ़ाइल में `A2` में मौजूद डेटा पर निर्भर करेंगे।)

## सामान्य वैरिएशन और एज केस

| परिदृश्य | कोड परिवर्तन | कारण |
|----------|-------------|--------|
| **विभिन्न प्रारंभिक सेल** | `cells.get("C3").setFormula("=EXPAND(D3,3,2)");` | कोई भी सेल रेफ़रेंस उपयोग किया जा सकता है; फ़ॉर्मूला उस सेल के सापेक्ष विस्तारित होता है। |
| **वैरिएबल एक्सपैंशन साइज** | `int rows = 8; int cols = 4; cells.get("B2").setFormula(String.format("=EXPAND(A2,%d,%d)", rows, cols));` | रन‑टाइम पर निर्धारित रेंज की अनुमति देता है, डेटा‑ड्रिवन रिपोर्ट्स में उपयोगी। |
| **शून्य‑साइज़ एक्सपैंशन** | `=EXPAND(A2,0,0)` | केवल मूल सेल वैल्यू लौटाता है; तब उपयोगी जब बाद में साइज बढ़ाने की योजना हो। |
| **नामित रेंज का उपयोग** | `cells.get("B2").setFormula("=EXPAND(MyRange,5,5)");` | जब वर्कबुक में `MyRange` परिभाषित हो तो काम करता है; फ़ॉर्मूले को पढ़ने योग्य बनाता है। |

> **ध्यान रखें:** Excel की अधिकतम एरे साइज (16,384 कॉलम × 1,048,576 पंक्तियाँ) है। इन सीमाओं से अधिक विस्तार करने पर कैलकुलेशन एरर आता है।

## डिबगिंग टिप्स

* **फ़ॉर्मूला इवैल्युएट नहीं हो रहा?** प्रत्येक `setFormula` के बाद `workbook.calculateFormula();` कॉल करना सुनिश्चित करें।  
* **अनपेक्षित मान?** रेफ़रेंस सेल (`A2` इस उदाहरण में) में वह डेटा है जिसे आप प्रसारित करना चाहते हैं, इसकी जाँच करें।  
* **परफ़ॉर्मेंस चिंता** – बड़े एक्सपैंशन महंगे हो सकते हैं। यदि आपको केवल उप‑सेट चाहिए, तो पंक्तियों/कॉलम के आर्ग्यूमेंट को घटाएँ।

## निष्कर्ष

अब आपके पास एक पूर्ण **aspose cells set formula** उदाहरण है जो Java में **EXPAND** का उपयोग दिखाता है। वर्कबुक लोड करके, `EXPAND` फ़ॉर्मूला सेट करके, पुनः‑गणना करके और सेव करके, आप मैन्युअल Excel इंटरैक्शन के बिना डायनेमिक रेंज बना सकते हैं।  

आगे आप यह कर सकते हैं:

* `FILTER` या `SEQUENCE` जैसे अन्य डायनेमिक फ़ंक्शन को Aspose.Cells के साथ उपयोग करना।  
* लॉजिक को वेब सर्विस में एम्बेड करना जिससे ऑन‑डिमांड रिपोर्ट जेनरेट हो सके।  
* `EXPAND` को कंडीशनल फ़ॉर्मेटिंग के साथ Aspose.Cells API के माध्यम से संयोजित करना।

विभिन्न प्रारंभिक सेल, वैरिएबल साइज या नामित रेंज के साथ प्रयोग करें ताकि आपका ऑटोमेशन परिदृश्य पूरी तरह फिट हो। यदि आपको यह **expand function example** उपयोगी लगा, तो इसे अपनी टीम के साथ शेयर करें या GitHub पर सुधार योगदान दें। Happy coding!


## अगला क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दर्शाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Mastering Aspose.Cells Java: How to interrupt formula calculation in Excel](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Convert Excel Tables to Ranges Using Aspose.Cells Java&#58; A Step-by-Step Guide](/cells/english/java/tables-structured-references/convert-excel-tables-ranges-aspose-cells-java/)
- [How to Set Excel Document Version Using Aspose.Cells for Java](/cells/english/java/workbook-operations/set-excel-version-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}