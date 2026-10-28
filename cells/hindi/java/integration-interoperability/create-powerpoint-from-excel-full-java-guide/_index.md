---
category: general
date: 2026-06-21
description: जावा का उपयोग करके एक्सेल से जल्दी पावरपॉइंट बनाएं। Aspose.Cells के साथ
  XLSX को PPTX में बदलना सीखें, चरण‑दर‑चरण ट्यूटोरियल में।
draft: false
keywords:
- create powerpoint from excel
- convert excel to powerpoint
- how to convert xlsx
- how to export excel
- excel workbook to powerpoint
language: hi
og_description: जावा का उपयोग करके एक्सेल से पावरपॉइंट बनाएं। यह ट्यूटोरियल Aspose.Cells
  के साथ XLSX को PPTX में कैसे बदलें, कोड, संभावित समस्याओं और टिप्स सहित, बिल्कुल
  दिखाता है।
og_title: एक्सेल से पावरपॉइंट बनाएं – जावा रूपांतरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create PowerPoint from Excel quickly using Java. Learn how to convert
    XLSX to PPTX with Aspose.Cells in a step‑by‑step tutorial.
  headline: Create PowerPoint from Excel – Full Java Guide
  type: TechArticle
- description: Create PowerPoint from Excel quickly using Java. Learn how to convert
    XLSX to PPTX with Aspose.Cells in a step‑by‑step tutorial.
  name: Create PowerPoint from Excel – Full Java Guide
  steps:
  - name: Expected Output
    text: '- A file named `shapes.pptx` appears in `YOUR_DIRECTORY`. - Opening the
      PPTX in Microsoft PowerPoint shows one slide per worksheet, with all cell formatting,
      charts, and shapes preserved as raster images. - No manual copy‑pasting required—your
      data is now presentation‑ready.'
  - name: 5.1 Large Workbooks or High‑Resolution Slides
    text: 'If your Excel file contains many rows, charts, or high‑resolution graphics,
      the generated PPTX can become bulky. You can reduce file size by:'
  - name: 5.2 Preserving Vector Graphics
    text: If you need vector‑based charts (so they stay crisp when zoomed), Aspose.Cells
      also supports `SaveFormat.SVG` for each slide, then you can assemble an SVG‑based
      PPTX manually. This is more advanced and beyond the scope of this quick guide,
      but worth exploring for design‑heavy decks.
  - name: 5.3 Multiple Worksheets per Slide
    text: Sometimes you want two related worksheets side‑by‑side on a single slide.
      Set `options.setOnePagePerSheet(false);` and use `WorksheetCollection` to control
      the range you render per slide.
  - name: 5.4 Automating Batch Conversions
    text: If you have a folder full of Excel files, wrap the conversion logic inside
      a loop that iterates over `File[] files = new File("YOUR_DIRECTORY").listFiles((dir,
      name) -> name.endsWith(".xlsx"));`. This way you can **convert excel to powerpoint**
      en masse.
  - name: Expected Result Screenshot
    text: '![create powerpoint from excel example](https://example.com/images/create-powerpoint-from-excel.png
      "create powerpoint from excel")'
  type: HowTo
- questions:
  - answer: Absolutely. Aspose.Cells supports both `.xls` and `.xlsx`. Just point
      `Workbook` at the old file; the rest of the code stays identical.
    question: Can I convert an `.xls` (old Excel) file?
  - answer: No. The conversion rasterizes the sheet, so formulas become static values
      on the slide. If you need editable data in PowerPoint, consider exporting to
      CSV and using PowerPoint’s table insertion APIs instead.
    question: Does this method retain formulas?
  - answer: Load the workbook with `loadOptions.setPassword("yourPassword");` before
      creating the `Workbook` object.
    question: What about password‑protected workbooks?
  - answer: 'Not directly via `ImageOrPrintOptions`. You’d need to post‑process the
      generated PPTX with Aspose.Slides for Java, adding notes to each slide programmatically.
      ## Full Working Example – Paste and Run Below is the complete, ready‑to‑run
      program. Copy it into a file named `ExcelToPowerPoint.java`, adj'
    question: Is there a way to add speaker notes automatically?
  type: FAQPage
tags:
- java
- excel
- powerpoint
- file-conversion
title: एक्सेल से पावरपॉइंट बनाएं – पूर्ण जावा गाइड
url: /hi/java/integration-interoperability/create-powerpoint-from-excel-full-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel से PowerPoint बनाएं – पूर्ण Java गाइड

क्या आपने कभी सोचा है कि **Excel से PowerPoint कैसे बनाएं** बिना ऐप्स को मैन्युअल रूप से खोले? आप अकेले नहीं हैं। हममें से कई को डेटा‑समृद्ध स्प्रेडशीट्स को प्रेजेंटेशन‑तैयार डेक्स में बदलना पड़ता है, चाहे वह साप्ताहिक बिक्री समीक्षाएँ हों या त्वरित स्टेकहोल्डर अपडेट। अच्छी खबर? कुछ ही Java कोड लाइनों के साथ आप पूरे प्रोसेस को ऑटोमेट कर सकते हैं—कोई कॉपी‑पेस्ट नहीं, कोई मैन्युअल फॉर्मेटिंग नहीं।

इस ट्यूटोरियल में हम Aspose.Cells for Java का उपयोग करके **Excel workbook को PowerPoint** में बदलने की प्रक्रिया को चरण‑दर‑चरण देखेंगे। अंत तक आपके पास एक चलाने योग्य प्रोग्राम होगा जो `.xlsx` फ़ाइल लेता है और एक पॉलिश्ड `.pptx` फ़ाइल आउटपुट करता है, जो आपके अगले मीटिंग के लिए तैयार है। हम **Excel डेटा को कुशलतापूर्वक एक्सपोर्ट करने** के टिप्स भी देंगे, ताकि आप इस समाधान को अपने प्रोजेक्ट्स में अनुकूलित कर सकें।

## आवश्यकताएँ – आपको क्या चाहिए

- **Java Development Kit (JDK) 8 या नया** – कोड किसी भी हालिया JDK पर चलता है।
- **Aspose.Cells for Java** लाइब्रेरी (फ्री ट्रायल परीक्षण के लिए ठीक काम करती है)। आप इसे Maven Central से प्राप्त कर सकते हैं या JAR सीधे डाउनलोड कर सकते हैं।
- एक **Excel workbook** (`shapes.xlsx` हमारे उदाहरण में) को ऐसी डायरेक्टरी में रखें जिसे आप रेफ़र कर सकें।
- एक **development environment** – IntelliJ IDEA, Eclipse, या यहाँ तक कि साधारण टेक्स्ट एडिटर के साथ कमांड‑लाइन कंपाइलेशन भी चलेगा।

इन सबके पास है? बढ़िया, चलिए शुरू करते हैं।

## चरण 1: प्रोजेक्ट सेट अप करें और डिपेंडेंसी इम्पोर्ट करें

पहले, एक नया Maven (या Gradle) प्रोजेक्ट बनाएं और Aspose.Cells को डिपेंडेंसी के रूप में जोड़ें। यदि आप मैन्युअल JAR तरीका पसंद करते हैं, तो बस `aspose-cells-xx.x.jar` को अपने `libs` फ़ोल्डर में डालें और क्लासपाथ में जोड़ें।

```xml
<!-- Maven pom.xml snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest version -->
</dependency>
```

क्यों यह कदम महत्वपूर्ण है: लाइब्रेरी के बिना, Java के पास **excel को powerpoint में बदलने** का कोई नेटिव तरीका नहीं है। Aspose.Cells भारी काम संभालता है, प्रत्येक worksheet को बैकग्राउंड में एक स्लाइड इमेज में बदलता है।

## चरण 2: Excel Workbook लोड करें

अब हम स्रोत workbook को लोड करेंगे। यह मूल स्निपेट की पहली लाइन को दर्शाता है, लेकिन हम इसे मजबूती के लिए try‑catch ब्लॉक में लपेटेंगे।

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Define paths – adjust as needed
        String inputPath = "YOUR_DIRECTORY/shapes.xlsx";
        String outputPath = "YOUR_DIRECTORY/shapes.pptx";

        try {
            // Step 1: Load the Excel workbook
            Workbook workbook = new Workbook(inputPath);
            System.out.println("Workbook loaded successfully.");
```

ध्यान दें हमने `Workbook workbook = new Workbook(inputPath);` का उपयोग किया। यह लाइन **xlsx को कैसे कन्वर्ट करें** का दिल है—यह पूरी स्प्रेडशीट को मेमोरी में लाता है, आगे की प्रोसेसिंग के लिए तैयार।

## चरण 3: PowerPoint आउटपुट के लिए ImageOrPrintOptions कॉन्फ़िगर करें

Aspose.Cells PowerPoint कन्वर्ज़न को एक image‑or‑print ऑपरेशन मानता है। हम एक `ImageOrPrintOptions` ऑब्जेक्ट बनाते हैं, टार्गेट फॉर्मेट को PPTX सेट करते हैं, और वैकल्पिक रूप से रिज़ॉल्यूशन या स्लाइड साइज को ट्यून करते हैं।

```java
            // Step 2: Create options for image/print conversion and set the target format to PPTX
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.PPTX);      // PPTX is the modern PowerPoint format
            options.setOnePagePerSheet(true);           // Each worksheet becomes a separate slide
            options.setImageFormat(ImageFormat.Png);    // Use PNG for crisp slide graphics
            options.setQuality(100);                    // Max quality for clearer images
```

`OnePagePerSheet` क्यों सेट करें? क्योंकि अधिकांश प्रेजेंटेशन एक **single slide per worksheet** चाहते हैं, जिससे Excel में डिज़ाइन किया गया लेआउट बरकरार रहता है। यदि आपको एक शीट में कई स्लाइड चाहिए, तो आप बाद में इस फ़्लैग को टॉगल कर सकते हैं।

## चरण 4: Workbook को PowerPoint प्रेजेंटेशन के रूप में सेव करें

ऑप्शन तैयार होने के बाद, अंतिम लाइन PPTX फ़ाइल को डिस्क पर लिखती है।

```java
            // Step 3: Save the workbook as a PowerPoint presentation
            workbook.save(outputPath, options);
            System.out.println("Conversion complete! PowerPoint saved at: " + outputPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

बस—**excel workbook to powerpoint** तीन संक्षिप्त चरणों में। जब आप प्रोग्राम चलाते हैं, Aspose.Cells प्रत्येक शीट को स्लाइड इमेज के रूप में रेंडर करता है, उसे नई PPTX फ़ाइल में एम्बेड करता है, और निर्दिष्ट स्थान पर सेव करता है।

### अपेक्षित आउटपुट

- `YOUR_DIRECTORY` में `shapes.pptx` नाम की फ़ाइल बनती है।
- Microsoft PowerPoint में PPTX खोलने पर प्रत्येक worksheet के लिए एक स्लाइड दिखती है, जिसमें सभी सेल फॉर्मेटिंग, चार्ट और शैप्स रास्टर इमेज के रूप में संरक्षित रहते हैं।
- कोई मैन्युअल कॉपी‑पेस्ट आवश्यक नहीं—आपका डेटा अब प्रेजेंटेशन‑तैयार है।

## चरण 5: सामान्य परिदृश्यों और किनारी मामलों को संभालना

भले ही मूल कन्वर्ज़न सीधा है, वास्तविक प्रोजेक्ट्स अक्सर कुछ समस्याओं से जूझते हैं। नीचे कुछ व्यावहारिक टिप्स हैं जो आपके सिरदर्द को कम करेंगे।

### 5.1 बड़े Workbook या हाई‑रेज़ॉल्यूशन स्लाइड्स

यदि आपका Excel फ़ाइल कई पंक्तियों, चार्ट्स या हाई‑रेज़ॉल्यूशन ग्राफ़िक्स रखती है, तो उत्पन्न PPTX भारी हो सकता है। फ़ाइल आकार कम करने के लिए आप:

- `options.setResolution(150);` को कम करके (डिफ़ॉल्ट 220 DPI है)।
- `options.setImageFormat(ImageFormat.Jpeg);` में बदलकर और कंप्रेशन क्वालिटी को समायोजित करके।
- कन्वर्ज़न से पहले workbook को छोटे फ़ाइलों में विभाजित करके।

```java
options.setResolution(150);          // Reduce DPI to shrink image size
options.setImageFormat(ImageFormat.Jpeg);
options.setQuality(80);              // JPEG quality (0‑100)
```

### 5.2 वेक्टर ग्राफ़िक्स को संरक्षित करना

यदि आपको वेक्टर‑आधारित चार्ट्स चाहिए (ताकि ज़ूम करने पर भी तेज़ रहें), तो Aspose.Cells प्रत्येक स्लाइड के लिए `SaveFormat.SVG` को सपोर्ट करता है, फिर आप मैन्युअली SVG‑आधारित PPTX असेंबल कर सकते हैं। यह अधिक उन्नत है और इस त्वरित गाइड के दायरे से बाहर है, लेकिन डिज़ाइन‑भारी डेक्स के लिए उपयोगी है।

### 5.3 एक स्लाइड में कई Worksheet

कभी‑कभी आप दो संबंधित worksheets को एक ही स्लाइड पर साइड‑बाय‑साइड दिखाना चाहते हैं। `options.setOnePagePerSheet(false);` सेट करें और `WorksheetCollection` का उपयोग करके प्रत्येक स्लाइड में रेंडर करने की रेंज को नियंत्रित करें।

```java
options.setOnePagePerSheet(false);
Worksheet sheet1 = workbook.getWorksheets().get(0);
Worksheet sheet2 = workbook.getWorksheets().get(1);
// Render both sheets onto a single slide using custom positioning logic.
```

### 5.4 बैच कन्वर्ज़न को ऑटोमेट करना

यदि आपके पास Excel फ़ाइलों का एक फ़ोल्डर है, तो कन्वर्ज़न लॉजिक को लूप में लपेटें जो `File[] files = new File("YOUR_DIRECTORY").listFiles((dir, name) -> name.endsWith(".xlsx"));` पर इटरेट करता है। इस तरह आप **excel को powerpoint में** बड़े पैमाने पर कन्वर्ट कर सकते हैं।

```java
File dir = new File("YOUR_DIRECTORY");
File[] excelFiles = dir.listFiles((d, n) -> n.toLowerCase().endsWith(".xlsx"));
for (File excel : excelFiles) {
    String pptxPath = excel.getAbsolutePath().replace(".xlsx", ".pptx");
    Workbook wb = new Workbook(excel.getAbsolutePath());
    wb.save(pptxPath, options);
    System.out.println("Converted: " + excel.getName());
}
```

## अक्सर पूछे जाने वाले प्रश्न (FAQ)

**प्रश्न: क्या मैं `.xls` (पुराना Excel) फ़ाइल को कन्वर्ट कर सकता हूँ?**  
**उत्तर:** बिल्कुल। Aspose.Cells दोनों `.xls` और `.xlsx` को सपोर्ट करता है। बस `Workbook` को पुराने फ़ाइल पर पॉइंट करें; बाकी कोड समान रहता है।

**प्रश्न: क्या यह विधि फ़ॉर्मूले रखती है?**  
**उत्तर:** नहीं। कन्वर्ज़न शीट को रास्टराइज़ करता है, इसलिए फ़ॉर्मूले स्लाइड पर स्थैतिक मान बन जाते हैं। यदि आपको PowerPoint में एडिटेबल डेटा चाहिए, तो CSV एक्सपोर्ट करके PowerPoint की टेबल इन्सर्शन API का उपयोग करें।

**प्रश्न: पासवर्ड‑सुरक्षित workbook के बारे में क्या?**  
**उत्तर:** `loadOptions.setPassword("yourPassword");` को `Workbook` ऑब्जेक्ट बनाने से पहले सेट करें।

**प्रश्न: क्या स्पीकर नोट्स को स्वचालित रूप से जोड़ने का कोई तरीका है?**  
**उत्तर:** सीधे `ImageOrPrintOptions` से नहीं। आपको उत्पन्न PPTX को Aspose.Slides for Java के साथ पोस्ट‑प्रोसेस करना पड़ेगा, जिससे प्रत्येक स्लाइड पर प्रोग्रामेटिक रूप से नोट्स जोड़े जा सकें।

## पूर्ण कार्यशील उदाहरण – कॉपी करें और चलाएँ

नीचे पूरा, तैयार‑चलाने‑योग्य प्रोग्राम दिया गया है। इसे `ExcelToPowerPoint.java` नाम की फ़ाइल में कॉपी करें, पाथ्स को समायोजित करें, और `javac` + `java` से कंपाइल‑रन करें या अपने IDE से चलाएँ।

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust these paths to match your environment
        String inputPath = "YOUR_DIRECTORY/shapes.xlsx";
        String outputPath = "YOUR_DIRECTORY/shapes.pptx";

        try {
            // Load the workbook (how to export excel)
            Workbook workbook = new Workbook(inputPath);
            System.out.println("Workbook loaded.");

            // Configure conversion options (convert excel to powerpoint)
            ImageOrPrintOptions options = new ImageOrPrintOptions();
            options.setSaveFormat(SaveFormat.PPTX);
            options.setOnePagePerSheet(true);
            options.setImageFormat(ImageFormat.Png);
            options.setQuality(100);
            options.setResolution(220); // default DPI

            // Perform the conversion
            workbook.save(outputPath, options);
            System.out.println("PowerPoint created at: " + outputPath);
        } catch (Exception e) {
            System.err.println("Conversion failed: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### अपेक्षित परिणाम स्क्रीनशॉट

![Excel से PowerPoint बनाने का उदाहरण](https://example.com/images/create-powerpoint-from-excel.png "Excel से PowerPoint बनाने का उदाहरण")

*(छवि में एक PowerPoint स्लाइड दिखती है जो Excel शीट से जेनरेट हुई है, जिसमें सेल बॉर्डर्स और चार्ट संरक्षित दिख रहे हैं।)*

## निष्कर्ष

बस इतना ही—Java का उपयोग करके **Excel से PowerPoint बनाना** का एक साफ़, एंड‑टू‑एंड समाधान। हमने आवश्यक कोड को कवर किया, **excel को pptx स्लाइड्स में कैसे एक्सपोर्ट करें** समझाया, और बड़े फ़ाइल आकार व बैच प्रोसेसिंग जैसे सामान्य मुद्दों को हल किया। अब आप साप्ताहिक डेक अपडेट्स को ऑटोमेट कर सकते हैं, क्लाइंट‑रेडी प्रेजेंटेशन तुरंत जेनरेट कर सकते हैं, या इस कन्वर्ज़न को बड़े रिपोर्टिंग पाइपलाइन में इंटीग्रेट कर सकते हैं। आगे बढ़ना चाहते हैं? कस्टम स्लाइड टाइटल जोड़ें, हाइपरलिंक एम्बेड करें, या आउटपुट को Aspose.Slides के साथ मर्ज करें।

## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकें।

- [Java में Aspose.Cells का उपयोग करके Excel को PDF में कैसे कन्वर्ट करें: चरण‑दर‑चरण गाइड](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Aspose.Cells Java का उपयोग करके Excel शीट्स को XPS फ़ॉर्मेट में कैसे कन्वर्ट करें](/cells/english/java/workbook-operations/render-excel-to-xps-aspose-cells-java/)
- [Aspose.Cells for .NET का उपयोग करके Excel को PowerPoint में कैसे कन्वर्ट करें: पूर्ण गाइड](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}