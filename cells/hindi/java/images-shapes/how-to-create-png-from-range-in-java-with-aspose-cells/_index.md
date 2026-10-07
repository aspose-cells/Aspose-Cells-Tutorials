---
category: general
date: 2026-10-07
description: जावा में रेंज से PNG बनाना और डेटा को PNG के रूप में निर्यात करना सीखें।
  यह गाइड आपको Aspose.Cells का उपयोग करके Excel रेंज इमेज को सहेजना दिखाता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create png from range
- export data as png
- save excel range image
- convert worksheet to png
- save cells as png
language: hi
lastmod: 2026-10-07
og_description: जावा में रेंज से PNG बनाएं और Aspose.Cells के साथ डेटा को PNG के रूप
  में निर्यात करें। इस पूर्ण ट्यूटोरियल का पालन करके एक्सेल रेंज इमेज को तुरंत सहेजें।
og_image_alt: Screenshot of Java code that creates a PNG from an Excel range
og_title: जावा में रेंज से PNG बनाएं – चरण‑दर‑चरण Aspose.Cells गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  headline: How to create PNG from range in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to create PNG from range and export data as PNG in Java.
    This guide shows you how to save Excel range image using Aspose.Cells.
  name: How to create PNG from range in Java with Aspose.Cells
  steps:
  - name: Maven dependency
    text: '```xml <dependency> <groupId>com.aspose</groupId> <artifactId>aspose-cells</artifactId>
      <version>23.12</version> </dependency> ```'
  - name: Expected output
    text: '* A file named `PivotImage.png` located in `YOUR_DIRECTORY`. * The image
      shows the exact layout, fonts, colors, and borders from the selected range.
      * If the source range contains a pivot table, the rendered image includes the
      same styling and calculated values as displayed in Excel.'
  - name: Exporting a non‑contiguous range
    text: Aspose.Cells does not render disjoint ranges in a single image. To export
      multiple areas, create separate images for each range and combine them later
      with an image‑processing library (e.g., ImageIO).
  - name: Saving a large worksheet as PNG
    text: 'Rendering an entire sheet that spans thousands of rows can consume significant
      memory. Mitigate this by:'
  - name: Preserving cell formulas
    text: A PNG image is a raster format; formulas are not retained. If downstream
      consumers need the raw data, also export the range as CSV or JSON using `Range.exportDataTable()`.
  - name: Next steps
    text: '* Experiment with different `Resolution` values to balance quality and
      file size. * Use `ImageOrPrintOptions.setTransparent(true)` if you need a PNG
      with a transparent background. * Combine multiple range images into a single
      PDF using `PdfSaveOptions` for multi‑page reports. * Explore exporting to '
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Aspose.Cells के साथ जावा में रेंज से PNG कैसे बनाएं
url: /hi/java/images-shapes/how-to-create-png-from-range-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में Aspose.Cells के साथ रेंज से PNG कैसे बनाएं

यदि आपको Excel वर्कबुक में **रेंज से PNG बनाना** है, तो यह ट्यूटोरियल आपको ठीक-ठीक बताता है कि कैसे करना है। गाइड के अंत तक आप **डेटा को PNG के रूप में एक्सपोर्ट** कर सकेंगे, Excel रेंज इमेज को सहेज सकेंगे, और रिपोर्ट या वेब पेजों में फ़ाइल को पुनः उपयोग कर सकेंगे।

आप एक पूर्ण, चलाने योग्य Java प्रोग्राम देखेंगे जो वर्कबुक को लोड करता है, इच्छित सेल्स को चुनता है, उन्हें PNG के रूप में रेंडर करता है, और परिणाम को डिस्क पर सहेजता है। कोई बाहरी टूल आवश्यक नहीं है—Aspose.Cells सभी काम आंतरिक रूप से संभालता है।

## इस ट्यूटोरियल में क्या कवर किया गया है

* Aspose.Cells के लिए प्रीरेक्विज़िट्स और Maven सेटअप
* पिवट टेबल या किसी भी डेटा रेंज वाले वर्कबुक को लोड करना
* वह सटीक सेल रेंज निर्धारित करना जिसे आप कनवर्ट करना चाहते हैं
* PNG आउटपुट के लिए इमेज ऑप्शन्स कॉन्फ़िगर करना
* रेंज को रेंडर करके PNG फ़ाइल सहेजना
* सामान्य समस्याएँ और हाई‑क्वालिटी इमेज के टिप्स

इन चरणों को पूरा करने के बाद आप **वर्कशीट को PNG में कनवर्ट** कर सकेंगे, चाहे वह एक साधारण टेबल हो या जटिल पिवट चार्ट।

## प्रीरेक्विज़िट्स

* Java 17 या बाद का (कोड JDK 11+ के साथ कम्पाइल होता है)
* Maven 3.6+ (या यदि आप चाहें तो Gradle)
* Aspose.Cells for Java 23.12 या नया – नीचे दिखाए गए डिपेंडेंसी को जोड़ें
* एक मौजूदा Excel फ़ाइल (`PivotWithStyle.xlsx`) जिसमें वह रेंज हो जिसे आप कैप्चर करना चाहते हैं

> **Pro tip:** यदि आपके पास लाइसेंस नहीं है, तो आप Aspose से एक टेम्पररी इवैल्यूएशन की प्राप्त कर सकते हैं। लाइब्रेरी इवैल्यूएशन मोड में अतिरिक्त कॉन्फ़िगरेशन के बिना काम करती है।

### Maven dependency

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

## चरण 1: वह वर्कबुक लोड करें जिसमें लक्ष्य रेंज हो

पहला ऑपरेशन Excel फ़ाइल को खोलना है। Aspose.Cells फ़ाइल को मेमोरी में पढ़ता है बिना Microsoft Office की आवश्यकता के।

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the data you want to export
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");
```

*यह क्यों महत्वपूर्ण है*: वर्कबुक को लोड करने से आपको वर्कशीट्स, सेल्स और पेज‑सेटअप प्रॉपर्टीज़ तक पहुंच मिलती है जो रेंडरिंग के लिए आवश्यक हैं।

## चरण 2: वह वर्कशीट एक्सेस करें जिसमें रेंज हो

अधिकांश वर्कबुक में डिफ़ॉल्ट शीट इंडेक्स 0 पर होती है, लेकिन आप शीट नाम का भी उपयोग कर सकते हैं।

```java
        // Retrieve the first worksheet (index 0)
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

यदि आपका डेटा किसी अलग शीट पर है, तो `0` को उपयुक्त इंडेक्स से बदलें या `workbook.getWorksheets().get("SheetName")` का उपयोग करें।

## चरण 3: वह सेल रेंज परिभाषित करें जिसे आप कनवर्ट करना चाहते हैं

आप A1 नोटेशन का उपयोग करके कोई भी आयताकार क्षेत्र निर्दिष्ट कर सकते हैं। इस उदाहरण में हम `A1:D15` को कैप्चर कर रहे हैं, जो पिवट टेबल या सामान्य डेटा ब्लॉक हो सकता है।

```java
        // Create a range object for cells A1:D15
        Range pivotRange = worksheet.getCells().createRange("A1:D15");
```

*एज केस*: जब रेंज में मर्ज्ड सेल्स शामिल हों, तो Aspose.Cells स्वचालित रूप से इमेज को मर्ज्ड एरिया सहित विस्तारित कर देता है।

## चरण 4: PNG इमेज ऑप्शन्स तैयार करें

`ImageOrPrintOptions` आपको फॉर्मेट, रिज़ॉल्यूशन और अन्य रेंडरिंग विवरणों को नियंत्रित करने देता है। सेव फॉर्मेट को PNG सेट करने से लॉसलेस क्वालिटी सुनिश्चित होती है।

```java
        // Configure image options – we want a PNG file
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        // Optional: increase DPI for sharper output (default is 96)
        imageOptions.setImageFormat(ImageFormat.getPng());
        imageOptions.setResolution(150); // 150 DPI for clearer text
```

छोटी फ़ॉन्ट या विस्तृत चार्ट वाले स्रोत सेल्स के लिए DPI बढ़ाना उपयोगी होता है।

## चरण 5: चयनित रेंज को प्रिंट एरिया के रूप में सेट करके रेंडर एरिया सीमित करें

रेंज को प्रिंट एरिया के रूप में असाइन करने से Aspose.Cells केवल उन सेल्स को रेंडर करता है और शीट के बाकी हिस्से को अनदेखा करता है।

```java
        // Set the print area so only the defined range is rendered
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());
```

यदि आप इस चरण को छोड़ देते हैं, तो पूरी वर्कशीट रास्टराइज़ हो जाएगी, जिससे मेमोरी बर्बाद होगी और बड़ी इमेज बन सकती है।

## चरण 6: रेंज को रेंडर करें और वर्कशीट में चित्र जोड़ें (वैकल्पिक)

यदि आप जेनरेटेड PNG को वापस वर्कबुक में एम्बेड करना चाहते हैं (प्रिव्यू के लिए), तो आप इसे चित्र के रूप में जोड़ सकते हैं। यह चरण शुद्ध एक्सपोर्ट परिदृश्यों के लिए वैकल्पिक है।

```java
        // Add the rendered image back to the worksheet at cell (0,0) – optional
        worksheet.getPictures().add(0, 0, imageOptions);
```

*आप इसे क्यों करेंगे*: कुछ वर्कफ़्लो में इमेज को वितरण से पहले वर्कबुक का हिस्सा बनाना आवश्यक होता है, जैसे कि नेटीव सेल्स और इमेज दोनों को मिलाकर प्रिंटेबल रिपोर्ट बनाना।

## चरण 7: PNG फ़ाइल को डिस्क पर सहेजें

अंत में, इमेज को फ़ाइल में लिखें। `save` मेथड `imageOptions` में निर्दिष्ट फॉर्मेट का सम्मान करता है।

```java
        // Save the rendered PNG image to the specified path
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

जब प्रोग्राम समाप्त होगा, `PivotImage.png` में `A1:D15` सेल्स का पिक्सेल‑परफेक्ट स्नैपशॉट होगा।

### अपेक्षित आउटपुट

* `YOUR_DIRECTORY` में स्थित `PivotImage.png` नाम की फ़ाइल।
* इमेज में चयनित रेंज का सटीक लेआउट, फ़ॉन्ट, रंग और बॉर्डर दिखेगा।
* यदि स्रोत रेंज में पिवट टेबल है, तो रेंडर की गई इमेज में वही स्टाइलिंग और गणना किए गए मान Excel में दिखाए गए अनुसार शामिल होंगे।

## सामान्य परिदृश्यों का प्रबंधन

### गैर‑सतत रेंज को एक्सपोर्ट करना

Aspose.Cells एक ही इमेज में डिसजॉइंट रेंज को रेंडर नहीं करता। कई क्षेत्रों को एक्सपोर्ट करने के लिए प्रत्येक रेंज के लिए अलग‑अलग इमेज बनाएं और बाद में किसी इमेज‑प्रोसेसिंग लाइब्रेरी (जैसे ImageIO) से उन्हें संयोजित करें।

```java
Range first = worksheet.getCells().createRange("A1:B10");
Range second = worksheet.getCells().createRange("D1:E10");
// Render each range individually using the same ImageOrPrintOptions
```

### बड़े वर्कशीट को PNG के रूप में सहेजना

हज़ारों पंक्तियों तक फैली पूरी शीट को रेंडर करने में काफी मेमोरी लग सकती है। इसे कम करने के लिए:

* छोटे फ़ाइल के लिए DPI घटाएँ (`imageOptions.setResolution(72)`)।
* `setPageCount` का उपयोग करके रेंडर किए जाने वाले पेजों की संख्या सीमित करें।
* `worksheet.getPageSetup().setPrintArea(...)` के माध्यम से एक समय में एक प्रिंटेबल पेज एक्सपोर्ट करें।

### सेल फ़ॉर्मूले को संरक्षित करना

PNG एक रास्टर फॉर्मेट है; फ़ॉर्मूले संरक्षित नहीं रहते। यदि डाउनस्ट्रीम कंज्यूमर्स को कच्चा डेटा चाहिए, तो रेंज को CSV या JSON के रूप में भी एक्सपोर्ट करें `Range.exportDataTable()` का उपयोग करके।

## पूर्ण, चलाने योग्य उदाहरण

नीचे पूरा Java क्लास दिया गया है जिसे आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं। `YOUR_DIRECTORY` को अपने मशीन पर एक एब्सोल्यूट या रिलेटिव पाथ से बदलें।

```java
import com.aspose.cells.*;

public class PivotRangeToPng {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the workbook containing the data
        Workbook workbook = new Workbook("YOUR_DIRECTORY/PivotWithStyle.xlsx");

        // 2️⃣ Access the first worksheet (adjust index or name as needed)
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Define the exact cell range you want to convert (A1:D15 in this case)
        Range pivotRange = worksheet.getCells().createRange("A1:D15");

        // 4️⃣ Prepare PNG image options – set format and optional resolution
        ImageOrPrintOptions imageOptions = new ImageOrPrintOptions();
        imageOptions.setSaveFormat(SaveFormat.PNG);
        imageOptions.setResolution(150); // sharper output

        // 5️⃣ Restrict rendering to the selected range
        worksheet.getPageSetup().setPrintArea(pivotRange.getRefersTo());

        // 6️⃣ (Optional) Add the rendered image back to the worksheet for preview
        worksheet.getPictures().add(0, 0, imageOptions);

        // 7️⃣ Save the PNG file – this creates the final image on disk
        workbook.save("YOUR_DIRECTORY/PivotImage.png", SaveFormat.PNG);
    }
}
```

प्रोग्राम को `mvn compile exec:java` (या अपनी पसंद के बिल्ड टूल) से चलाएँ। निष्पादन के बाद, परिणाम की पुष्टि के लिए `PivotImage.png` खोलें।

## निष्कर्ष

अब आप Java में Aspose.Cells का उपयोग करके **रेंज से PNG बनाना**, प्रभावी रूप से **डेटा को PNG के रूप में एक्सपोर्ट** करना और **Excel रेंज इमेज को सहेजना** जानते हैं। वर्कबुक लोड करना, रेंज परिभाषित करना, इमेज ऑप्शन्स कॉन्फ़िगर करना, प्रिंट एरिया सेट करना, और फ़ाइल सहेजना—इन चरणों से **वर्कशीट को PNG में कनवर्ट** और **सेल्स को PNG के रूप में सहेजना** का पूरा वर्कफ़्लो कवर होता है।

### अगले कदम

* गुणवत्ता और फ़ाइल आकार के बीच संतुलन के लिए विभिन्न `Resolution` मानों के साथ प्रयोग करें।
* यदि आपको ट्रांसपेरेंट बैकग्राउंड वाला PNG चाहिए तो `ImageOrPrintOptions.setTransparent(true)` का उपयोग करें।
* मल्टी‑पेज रिपोर्ट के लिए कई रेंज इमेज को `PdfSaveOptions` के साथ एक ही PDF में संयोजित करें।
* `setSaveFormat` बदलकर JPEG, BMP जैसे अन्य रास्टर फॉर्मेट में एक्सपोर्ट करने का अन्वेषण करें।

इस पैटर्न को चार्ट, टेबल या पूरी वर्कशीट के लिए भी अनुकूलित करें। हैप्पी कोडिंग!

## आप आगे क्या सीखें?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Convert Excel to PNG Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/workbook-operations/convert-excel-to-png-aspose-cells-java/)
- [Create Union Range in Excel using Aspose.Cells Java: A Comprehensive Guide](/cells/english/java/range-management/create-union-range-excel-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}