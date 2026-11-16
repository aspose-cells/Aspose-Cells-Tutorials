---
category: general
date: 2026-11-16
description: जावा में एक्सेल वर्कबुक्स के बीच सेल्स कैसे कॉपी करें – एक वर्कबुक लोड
  करें, वर्कबुक्स के बीच रेंज कॉपी करें (पिवट टेबल सहित), और वर्कबुक फ़ाइल को सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: hi
lastmod: 2026-11-16
og_description: जावा में एक्सेल वर्कबुक्स के बीच सेल्स कैसे कॉपी करें। एक एक्सेल वर्कबुक
  लोड करना, रेंज (पिवट टेबल सहित) को वर्कबुक्स के बीच कॉपी करना, और वर्कबुक फ़ाइल
  को सहेजना सीखें।
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: जावा में Excel वर्कबुक्स के बीच सेल्स कैसे कॉपी करें – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: जावा में एक्सेल वर्कबुक्स के बीच सेल्स कैसे कॉपी करें
url: /hi/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel कार्यपुस्तिकाओं के बीच Java में सेल्स कॉपी कैसे करें

यदि आपको Java का उपयोग करके एक Excel कार्यपुस्तिका से दूसरी में **सेल्स कॉपी** करने की आवश्यकता है, तो यह गाइड आपको एक विश्वसनीय तरीका दिखाता है। आप सीखेंगे कि **load Excel workbook Java** कैसे किया जाता है, एक ऐसा रेंज कॉपी करें जिसमें पिवट टेबल हो सकती है, और अंत में **save workbook file** को कॉपी किए गए डेटा के साथ कैसे सहेजा जाता है।

यह ट्यूटोरियल शामिल करता है:

* स्रोत कार्यपुस्तिका लोड करना और एक वर्कशीट चुनना।  
* वह सटीक रेंज परिभाषित करना जिसे आप स्थानांतरित करना चाहते हैं (पिवट टेबल सहित)।  
* गंतव्य कार्यपुस्तिका बनाना और रेंज कॉपी करना।  
* गंतव्य फ़ाइल को सहेजना।  

उदाहरण में Aspose.Cells for Java लाइब्रेरी का उपयोग किया गया है, जो Microsoft Office की आवश्यकता के बिना Excel फ़ाइलों के साथ काम करती है। कोड Java 8+ और किसी भी आधुनिक IDE (IntelliJ IDEA, Eclipse, VS Code, आदि) पर चलता है।

---

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

| आवश्यकता | कारण |
|-------------|--------|
| Java Development Kit (JDK) 8 या नया | कोड को संकलित और चलाने के लिए आवश्यक। |
| Maven या Gradle बिल्ड टूल | Aspose.Cells निर्भरता जोड़ना आसान बनाता है। |
| Aspose.Cells for Java लाइब्रेरी (नवीनतम संस्करण) | उदाहरण में उपयोग किए गए `Workbook`, `Worksheet`, और `Range` क्लासेज़ प्रदान करती है। |
| दो Excel फ़ाइलें (`source.xlsx` और `dest.xlsx` के लिए एक खाली फ़ोल्डर) | स्रोत फ़ाइल में वह डेटा और वैकल्पिक रूप से पिवट टेबल होना चाहिए जिसे आप कॉपी करना चाहते हैं। |

अपने `pom.xml` (Maven) या `build.gradle` (Gradle) में Aspose.Cells निर्भरता जोड़ें। Maven के लिए उदाहरण:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## How to copy cells with Aspose.Cells

निम्नलिखित चरण पूरी प्रक्रिया को चरण‑दर‑चरण दिखाते हैं। प्रत्येक चरण में Java कोड, **क्यों** यह चरण महत्वपूर्ण है इसका स्पष्टीकरण, और सामान्य त्रुटियों से बचने के लिए एक टिप शामिल है।

### चरण 1: स्रोत कार्यपुस्तिका लोड करें

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**क्यों?**  
`Workbook` पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। इसे लोड करने से आपको सभी वर्कशीट्स, सेल्स, और पिवट टेबल जैसे ऑब्जेक्ट्स तक पहुंच मिलती है। पहली वर्कशीट का उपयोग आम है, लेकिन आप किसी भी शीट को नाम से चुन सकते हैं (`srcWb.getWorksheets().get("Sheet2")`)।

**प्रो टिप:**  
यदि स्रोत फ़ाइल बड़ी है, तो *memory‑efficient* मोड में लोड करने पर विचार करें: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }})`

### चरण 2: पिवट टेबल सहित रेंज परिभाषित करें

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**क्यों?**  
`Range` ऑब्जेक्ट एक आयताकार सेल ब्लॉक को एब्स्ट्रैक्ट करता है। `"A1:G20"` निर्दिष्ट करके आप Aspose.Cells को ठीक वही सेल्स—जिसमें एम्बेडेड पिवट टेबल भी शामिल है—कॉपी करने के लिए कहते हैं। लाइब्रेरी स्वचालित रूप से डेटा, स्टाइल, और पिवट परिभाषाएँ कॉपी कर देती है।

**एज केस:**  
यदि पिवट टेबल परिभाषित रेंज से बाहर तक फैली है, तो पता बढ़ाएँ (जैसे `"A1:Z100"`). आप `srcWs.getCells().getMaxDataColumn()` और `getMaxDataRow()` का उपयोग करके उपयोग किए गए क्षेत्र को गतिशील रूप से गणना भी कर सकते हैं।

### चरण 3: गंतव्य कार्यपुस्तिका बनाएं

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**क्यों?**  
एक नई कार्यपुस्तिका सुनिश्चित करती है कि कोई अनचाहा फॉर्मेटिंग या छिपी शीट्स कॉपी किए गए कंटेंट में हस्तक्षेप न करें। डिफ़ॉल्ट कार्यपुस्तिका में पहले से ही एक वर्कशीट होती है, जिसे हम लक्ष्य के रूप में उपयोग करेंगे।

### चरण 4: रेंज को गंतव्य कार्यपुस्तिका में कॉपी करें

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**क्यों?**  
`copyRange` सभी सेल एट्रिब्यूट्स—मान, फ़ॉर्मूले, फॉर्मेटिंग, और पिवट कैशेज़—को संभालता है। `"A1"` पर कॉपी करके आप रेंज को गंतव्य शीट के टॉप‑लेफ़्ट कोने में रख देते हैं, जिससे मूल लेआउट बना रहता है।

**सामान्य प्रश्न:** *क्या पिवट टेबल कार्यशील रहेगी?*  
हाँ। Aspose.Cells पिवट टेबल की परिभाषा और उसका कैश कॉपी करता है, इसलिए पिवट स्रोत कार्यपुस्तिका की तरह ही काम करता है।

### चरण 5: गंतव्य कार्यपुस्तिका सहेजें

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**क्यों?**  
`save` को कॉल करने से मेमोरी में मौजूद कार्यपुस्तिका एक वास्तविक `.xlsx` फ़ाइल में लिखी जाती है। आप फ़ाइल एक्सटेंशन बदलकर या `SaveOptions` का उपयोग करके अन्य फ़ॉर्मेट्स (`.xls`, `.csv`, `.pdf`) में भी सहेज सकते हैं।

**टिप:**  
यदि आपको फ़ाइल को वेब रिस्पॉन्स में स्ट्रीम करना है, तो फ़ाइल पाथ की बजाय `destWb.save(OutputStream, SaveFormat.XLSX);` का उपयोग करें।

---

## Copy range between workbooks – पूर्ण स्रोत कोड

नीचे पूरी, तैयार‑चलाने योग्य Java क्लास दी गई है। `YOUR_DIRECTORY` को अपने मशीन पर वास्तविक फ़ोल्डर पाथ से बदलें।

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**अपेक्षित परिणाम:**  
`dest.xlsx` में `source.xlsx` की रेंज `A1:G20` की बिल्कुल समान प्रतिलिपि होगी। यदि स्रोत रेंज में पिवट टेबल थी, तो गंतव्य फ़ाइल में वही पिवट दिखेगा और उसका डेटा स्रोत कॉपी किए गए सेल्स से सही ढंग से जुड़ा होगा।

आप `dest.xlsx` को Excel, LibreOffice, या किसी भी `.xlsx` समर्थित व्यूअर में खोलकर मान, फॉर्मेटिंग, और पिवट कार्यक्षमता की पुष्टि कर सकते हैं।

---

## Copy pivot table workbook – आपको क्या जानना चाहिए

* **पिवट कैश स्वचालित रूप से कॉपी हो जाता है।** लाइब्रेरी अंतर्निहित कैश ट्रांसफ़र करती है, इसलिए पिवट को मैन्युअल रूप से रीफ़्रेश करने की आवश्यकता नहीं होती।
* **बाहरी डेटा स्रोत ट्रांसफ़र नहीं होते।** यदि पिवट किसी बाहरी डेटाबेस से डेटा लेता है, तो आपको सुनिश्चित करना होगा कि गंतव्य कार्यपुस्तिका उसी स्रोत तक पहुंच सके, या कैश को स्थानीय रूप से पुनः बनाएं।
* **बड़ी पिवट टेबल्स मेमोरी उपयोग बढ़ा सकती हैं।** बहुत बड़े कार्यपुस्तिकाओं के लिए JVM हीप (`-Xmx2g`) बढ़ाने पर विचार करें ताकि `OutOfMemoryError` से बचा जा सके।

---

## Save workbook file in different formats

Aspose.Cells आपको कई फ़ॉर्मेट्स में परिणाम सहेजने की सुविधा देता है, बिना अतिरिक्त कोड परिवर्तन के:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

अपनी डाउनस्ट्रीम प्रक्रिया के अनुसार फ़ॉर्मेट चुनें। वही `copyRange` लॉजिक अंतिम फ़ॉर्मेट चाहे जो भी हो, समान रूप से काम करता है।

---

## Load Excel workbook Java – अतिरिक्त टिप्स

* **एन्क्रिप्टेड फ़ाइलें लोड करना:** पासवर्ड के साथ `LoadOptions` का उपयोग करें:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **केवल विशिष्ट शीट्स पढ़ना:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

ये विकल्प **load excel workbook java** चरण को तेज़ बना सकते हैं, विशेषकर बड़े फ़ाइलों के लिए।

---

## Conclusion

अब आप **सेल्स को Excel कार्यपुस्तिकाओं के बीच Java में कॉपी** करना, **पिवट टेबल वाली रेंज को कार्यपुस्तिकाओं के बीच कॉपी** करना, और आवश्यक फ़ॉर्मेट में **वर्कबुक फ़ाइल सहेजना** जानते हैं। ऊपर दिए गए चरणों का पालन करके आप किसी भी Java एप्लिकेशन में Excel डेटा मैनिपुलेशन को एकीकृत कर सकते हैं—चाहे आप रिपोर्टिंग इंजन, ETL पाइपलाइन, या साधारण फ़ाइल‑कन्वर्ज़न यूटिलिटी बना रहे हों।

**अगले कदम** आप खोज सकते हैं:

* **copy range between workbooks** का उपयोग करके कई रिपोर्ट्स को मिलाना

## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Save New Workbook in Java – Copy Range Between Workbooks Tutorial](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [How to copy pivot tables between Excel workbooks in Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [How to copy range in Java – Copy Pivot Table with Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}