---
category: general
date: 2026-06-30
description: जावा का उपयोग करके एक्सेल में कस्टम नंबर फ़ॉर्मेट सेट करें। जावा में
  एक्सेल वर्कबुक बनाना, सेल से डेट‑टाइम प्राप्त करना, वर्कबुक फ़ॉर्मूले की गणना करना
  और डेट‑टाइम मान आउटपुट करना सीखें।
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: hi
og_description: जावा का उपयोग करके एक्सेल में कस्टम नंबर फ़ॉर्मेट सेट करें। यह गाइड
  दिखाता है कि जावा से एक्सेल वर्कबुक कैसे बनाएं, सेल से डेट‑टाइम प्राप्त करें, वर्कबुक
  फ़ॉर्मूले की गणना करें और डेट‑टाइम मान आउटपुट करें।
og_title: जावा के साथ एक्सेल में कस्टम नंबर फ़ॉर्मेट सेट करें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: जावा के साथ एक्सेल में कस्टम नंबर फ़ॉर्मेट सेट करें – पूर्ण गाइड
url: /hi/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में Java के साथ कस्टम नंबर फ़ॉर्मेट सेट करें – पूर्ण गाइड

क्या आपको Java में काम करते हुए Excel शीट में **कस्टम नंबर फ़ॉर्मेट सेट** करने की ज़रूरत पड़ी है? आप अकेले नहीं हैं। चाहे आप रिपोर्टिंग इंजन बना रहे हों या सिर्फ़ जापानी युग की तिथियों को सही ढंग से दिखाना चाहते हों, इस ट्रिक में महारत हासिल करने से पोस्ट‑प्रोसेसिंग में अनगिनत घंटे बचते हैं। इस ट्यूटोरियल में हम एक वास्तविक उदाहरण के माध्यम से चलेंगे जिसमें **Excel workbook Java बनाता है**, एक लोकैल‑विशिष्ट फ़ॉर्मेट लागू करता है, फ़ॉर्मूले पुनः गणना करता है, और अंत में **सेल से DateTime प्राप्त करता है** ताकि **datetime मान आउटपुट किया जा सके**।

हम लोकप्रिय Aspose.Cells for Java लाइब्रेरी का उपयोग करेंगे क्योंकि यह बॉक्स से ही नंबर फ़ॉर्मेट और संस्कृति‑सचेत तिथियों को संभालती है। गाइड के अंत तक आपके पास एक स्व-निहित, चलाने योग्य प्रोग्राम होगा जिसे आप किसी भी Maven या Gradle प्रोजेक्ट में डाल सकते हैं। कोई अस्पष्ट “डॉक्यूमेंट देखें” शॉर्टकट नहीं—सिर्फ ठोस कोड और स्पष्ट व्याख्याएँ।

---

## आप क्या सीखेंगे

- कैसे **Excel workbook Java** को प्रोग्रामेटिकली बनाएं।
- जापानी युग की तिथियों के लिए **कस्टम नंबर फ़ॉर्मेट सेट** करने के सटीक चरण।
- मूल्य निकालने से पहले **calculate workbook formulas** को कॉल करना क्यों आवश्यक है।
- सेल से **datetime प्राप्त करने** और **datetime मान आउटपुट करने** का सही तरीका।
- सामान्य गड़बड़ियां (लोकैल गायब, पुरानी फ़ॉर्मूले) और त्वरित समाधान।

---

## पूर्वापेक्षाएँ

- आपके मशीन पर Java 8 या उससे नया स्थापित हो।  
- Aspose.Cells for Java 23.11 (या कोई भी नवीनतम संस्करण)।  
- एक बेसिक IDE या टेक्स्ट एडिटर—IntelliJ IDEA, Eclipse, VS Code, जो भी आपको पसंद हो।  

यदि आपने अभी तक अपने प्रोजेक्ट में Aspose.Cells नहीं जोड़ा है, तो नीचे दिया गया Maven स्निपेट अपने `pom.xml` में पेस्ट करें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Gradle उपयोगकर्ता जोड़ सकते हैं:

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

अब जब पर्यावरण तैयार है, चलिए कोड में डुबकी लगाते हैं।

---

## चरण 1: कस्टम नंबर फ़ॉर्मेट सेट करें – अवलोकन

कोई भी Java कोड लिखने से पहले यह देखना उपयोगी है कि हम क्या चाहते हैं। कल्पना करें कि एक Excel सेल को **“令和2年4月1日”** दिखाना चाहिए, न कि ISO‑8601 स्ट्रिंग “2020‑04‑01”। अंतर्निहित मान एक वास्तविक तिथि बना रहता है (ताकि फ़ॉर्मूले अभी भी काम करें), लेकिन *प्रदर्शन* जापानी युग फ़ॉर्मेट का पालन करता है। यही **set custom number format** ऑपरेशन करता है।

नीचे पूरा स्रोत फ़ाइल दिया गया है। इसे `src/main/java/SetCustomNumberFormatDemo.java` में कॉपी‑पेस्ट करने में संकोच न करें।

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### यह क्यों काम करता है

- **`setNumberFormat`** Excel को बताता है कि अंतर्निहित संख्यात्मक मान को *कैसे दिखाया* जाए। फ़ॉर्मेट स्ट्रिंग `[$-ja-JP]ggge年m月d日` मुख्य है; `ggg` युग का नाम चुनता है, `e` युग के भीतर वर्ष, उसके बाद महीने और दिन के लिटरल।
- **`calculateFormula`** Aspose.Cells को “R02-04-01” टेक्स्ट को जापानी कैलेंडर के आधार पर तिथि के रूप में व्याख्या करने के लिए मजबूर करता है। इस चरण को छोड़ने पर सेल साधारण टेक्स्ट रह जाता है, और `getDateTime()` एक अपवाद फेंकेगा।
- **`getDateTime`** अंततः *वास्तविक* `java.util.Calendar` ऑब्जेक्ट निकालता है, जिसे आप आगे बदल, फ़ॉर्मेट या कहीं और संग्रहीत कर सकते हैं।

---

## चरण 2: Excel Workbook Java बनाएं – गहरी झलक

जब आप **create Excel workbook Java** करते हैं, तो आप केवल मेमोरी आवंटित नहीं कर रहे होते; आप डिफ़ॉल्ट स्टाइल, एक डिफ़ॉल्ट वर्कशीट, और एक डिफ़ॉल्ट संस्कृति (आमतौर पर सिस्टम लोकैल) भी स्थापित कर रहे होते हैं। यदि आपको अलग डिफ़ॉल्ट लोकैल चाहिए, तो आप `LoadOptions` ऑब्जेक्ट पास कर सकते हैं:

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

अधिकांश परिदृश्यों में साधारण कंस्ट्रक्टर पर्याप्त है, लेकिन विकल्प को जानना अच्छा है—विशेषकर जब आप एक ही एप्लिकेशन में कई लोकैल्स के साथ काम कर रहे हों।

*Pro tip:* फ़ॉर्मेटिंग पूरी होने तक वर्कबुक को मेमोरी में रखें। प्रत्येक परिवर्तन के बाद डिस्क पर लिखने से अनावश्यक I/O ओवरहेड बढ़ता है।

---

## चरण 3: सेल से DateTime प्राप्त करें – परिणाम को संभालना

लाइन `java.util.Calendar dt = cellA1.getDateTime();` भारी काम करती है। पर्दे के पीछे Aspose.Cells आंतरिक सीरियल नंबर (1899‑12‑31 से दिनों की संख्या) को `Calendar` में बदल देता है। यह रूपांतरण वर्कबुक की लोकैल का सम्मान करता है, इसलिए आपको सही ग्रेगोरियन तिथि मिलती है जबकि डिस्प्ले जापानी युग में रहता है।

यदि आपको `java.time.LocalDate` (नया API) चाहिए, तो इस तरह बदलें:

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

इससे **output datetime value** की आवश्यकता पूरी होती है और कोड आधुनिक रहता है।

---

## चरण 4: Workbook फ़ॉर्मूले गणना करें – जब यह महत्वपूर्ण हो

आप सोच सकते हैं: *“क्या मुझे वास्तव में `calculateFormula()` को कॉल करना ज़रूरी है?”* उत्तर स्पष्ट हाँ है, जब तक आप शुरू से ही सेल को नेटिव Java `Date` ऑब्जेक्ट से नहीं भर रहे हैं। जब आप **set custom number format** को टेक्स्ट स्ट्रिंग पर लागू करते हैं, तो Excel (और Aspose.Cells) इसे एक फ़ॉर्मूला‑समान अभिव्यक्ति मानते हैं जिसे मूल्यांकन की आवश्यकता होती है। पुनर्गणना के बिना, `getDateTime()` डिफ़ॉल्ट `1900‑01‑00` लौटाएगा या `CellValueException` फेंकेगा।

यदि आपका वर्कबुक पहले से ही जटिल फ़ॉर्मूले रखता है जो नए फ़ॉर्मेट किए गए सेल को संदर्भित करते हैं, तो सभी बदलावों के बाद **एक बार** `calculateFormula()` कॉल करें। बार‑बार कॉल करना महंगा पड़ता है।

---

## चरण 5: DateTime मान आउटपुट करें – परिणाम की पुष्टि

डेमो चलाने पर कुछ इस तरह प्रिंट होगा:

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

यह लाइन तीन बातें पुष्टि करती है:

1. **set custom number format** लागू किया गया (आप उत्पन्न `.xlsx` को Excel में खोलकर “令和2年4月1日” देख सकते हैं)।
2. **calculate workbook formulas** चरण सफल रहा, जिससे युग स्ट्रिंग वास्तविक तिथि में बदल गई।
3. **get datetime from cell** कॉल ने एक उचित `Calendar` लौटाया, जिसे हमने फिर **output datetime value** कंसोल पर प्रिंट किया।

यदि आप वर्कबुक को किसी स्प्रेडशीट प्रोग्राम में खोलते हैं, तो फ़ॉर्मेटेड टेक्स्ट दिखेगा, लेकिन अंतर्निहित सेल मान सीरियल नंबर `43831` (Excel में 2020‑04‑01 का प्रतिनिधित्व) ही रहेगा। यही द्वैतता Excel को शक्तिशाली बनाती है।

---

## सामान्य गड़बड़ियां और किनारे के मामले

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| `cellA1.getDateTime()` `CellValueException` फेंकता है | `calculateFormula()` न बुलाने के कारण सेल अभी भी स्ट्रिंग है। | टेक्स्ट तिथि को रूपांतरित करने के बाद हमेशा `workbook.calculateFormula()` को कॉल करें। |
| जापानी युग सही ढंग से नहीं दिख रहा है | लोकैल कोड गायब या गलत है। | फ़ॉर्मेट स्ट्रिंग में `[$-ja-JP]` उपयोग करें, या `LoadOptions` के माध्यम से वर्कबुक लोकैल सेट करें। |
| फ़ॉर्मेट Excel में “#VALUE!” दिखा रहा है | फ़ॉर्मेट स्ट्रिंग खराब है। | कोष्ठक और अक्षरों की दोबारा जाँच करें; युग वर्ष के लिए `ggge年m月d日` आवश्यक है। |
| समय घटक दिखाई देता है (जैसे “00:00:00”) | स्रोत स्ट्रिंग में समय शामिल है या सेल की शैली इसे जोड़ रही है। | स्रोत स्ट्रिंग को ट्रिम करें या फ़ॉर्मेट को `ggge年m月d日;@` में बदलें। |

---

## पूर्ण कार्यशील उदाहरण – एक‑क्लिक चलाएँ

यदि आप अतिरिक्त टिप्पणियों के बिना एकल फ़ाइल पसंद करते हैं, तो यहाँ न्यूनतम संस्करण है:



## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकटतम संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API सुविधाओं में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Aspose.Cells का उपयोग करके जावा में Excel वर्कबुक बनाना&#58; चरण‑दर‑चरण गाइड](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Excel में डेटा प्रस्तुति में महारत&#58; संख्या और कस्टम डेट फ़ॉर्मेटिंग Aspose.Cells for Java के साथ](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Aspose.Cells for Java के साथ Excel सेल्स बनाना और फ़ॉर्मेट करना&#58; चरण‑दर‑चरण गाइड](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}