---
category: general
date: 2026-09-21
description: Aspose.Cells in Java के साथ Excel को PowerPoint में बदलें – सीखें कि
  चार्ट को PPTX में कैसे निर्यात करें और केवल कुछ लाइनों के कोड से वर्कबुक को PPTX
  के रूप में कैसे सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- save workbook as pptx
- how to export chart to pptx
- create powerpoint from excel chart
language: hi
lastmod: 2026-09-21
og_description: Java में Aspose.Cells का उपयोग करके Excel को PowerPoint में बदलें।
  यह ट्यूटोरियल दिखाता है कि कैसे एक चार्ट को PPTX में निर्यात किया जाए और वर्कबुक
  को संपादन योग्य टेक्स्ट बॉक्स के साथ PPTX के रूप में सहेजा जाए।
og_image_alt: Screenshot of Java code converting an Excel workbook to a PowerPoint
  presentation
og_title: Aspose.Cells के साथ Excel को PowerPoint में बदलें – Java गाइड
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Convert Excel to PowerPoint with Aspose.Cells in Java – learn how to
    export chart to PPTX and save workbook as PPTX in just a few lines of code.
  headline: Convert Excel to PowerPoint with Aspose.Cells in Java
  type: TechArticle
- questions:
  - answer: Yes. Loop through each worksheet, export its chart to a new slide using
      `PdfSaveOptions`, and then save the workbook once after processing all sheets.
    question: Can I convert multiple worksheets into separate PowerPoint slides?
  - answer: Only chart and textbox objects are transferred to PowerPoint. Cell formatting
      stays in the Excel file; it does not appear in the PPTX.
    question: Does this method preserve cell formatting?
  - answer: 'Use `SaveFormat.PDF` and the same `PdfSaveOptions`. The `setExportEditableTextBoxes`
      flag works for PDF as well. ## Next steps Now that you know how to **save workbook
      as PPTX** and **export chart to PPTX**, you might explore: * Adding multiple
      charts to different slides (`create powerpoint from exc'
    question: What if I need to export to PDF instead of PPTX?
  type: FAQPage
tags:
- Excel
- PowerPoint
- Aspose.Cells
- Java
title: Aspose.Cells का उपयोग करके जावा में एक्सेल को पावरपॉइंट में बदलें
url: /hi/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells in Java के साथ Excel को PowerPoint में बदलें

यदि आपको **Excel को PowerPoint में बदलना** है, तो यह गाइड आपको एक संक्षिप्त, उत्पादन‑तैयार तरीका दिखाता है। आप देखेंगे कि चार्ट को PPTX में कैसे निर्यात करें, टेक्स्ट बॉक्स को संपादन योग्य रखें, और **वर्कबुक को PPTX के रूप में सहेजें** केवल तीन पंक्तियों के Java कोड में।

बहुत से डेवलपर्स डेटा को PDFs में निर्यात करते हैं, लेकिन PowerPoint अक्सर उन प्रस्तुतियों के लिए बेहतर होता है जिन्हें लाइव चार्ट और संपादन योग्य तत्वों की आवश्यकता होती है। यह ट्यूटोरियल सब कुछ कवर करता है—प्रोजेक्ट सेटअप से लेकर सामान्य समस्याओं को संभालने तक—ताकि आप अपने Java IDE को छोड़े बिना Excel चार्ट से PowerPoint बना सकें।

## आवश्यकताएँ

* Java 17 या उससे नया स्थापित हो।
* Maven (या Gradle) निर्भरताओं को प्रबंधित करने के लिए।
* Aspose.Cells for Java लाइसेंस (मुफ़्त ट्रायल मूल्यांकन के लिए काम करता है)।
* एक Excel फ़ाइल (`ChartAndTextbox.xlsx`) जिसमें कम से कम एक चार्ट और एक टेक्स्टबॉक्स हो।

## चरण 1: अपने प्रोजेक्ट में Aspose.Cells जोड़ें

पहला कदम Aspose.Cells लाइब्रेरी को शामिल करना है। Maven का उपयोग करके, अपने `pom.xml` में निम्नलिखित डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** यदि आप Gradle का उपयोग करते हैं, तो समकक्ष है:
> ```groovy
> implementation 'com.aspose:aspose-cells:24.9'
> ```

लाइब्रेरी को शामिल करने से आपको `Workbook`, `PdfSaveOptions`, और `SaveFormat` enum तक पहुंच मिलती है, जो रूपांतरण के लिए आवश्यक हैं।

## चरण 2: उस वर्कबुक को लोड करें जिसमें चार्ट और टेक्स्टबॉक्स हो

अब Excel फ़ाइल लोड करें। `Workbook` क्लास पूरी वर्कबुक को मेमोरी में पढ़ता है, चार्ट, फ़ॉर्मूले और टेक्स्टबॉक्स को संरक्षित रखता है।

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        // Adjust the path to point to your Excel file
        String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";

        // Load the workbook
        Workbook workbook = new Workbook(sourcePath);
        
        // Continue with conversion...
    }
}
```

**Why this matters:** वर्कबुक को पहले लोड करने से यह सुनिश्चित होता है कि सभी एम्बेडेड ऑब्जेक्ट्स (चार्ट, इमेज, टेक्स्टबॉक्स) निर्यात प्रक्रिया के लिए उपलब्ध हों। यदि फ़ाइल नहीं मिलती है, तो Aspose.Cells एक स्पष्ट `FileNotFoundException` फेंकता है, जिसे आप बेहतर उपयोगकर्ता अनुभव के लिए पकड़ सकते हैं।

## चरण 3: टेक्स्टबॉक्स को संपादन योग्य रखने के लिए निर्यात विकल्प कॉन्फ़िगर करें

Aspose.Cells `PdfSaveOptions` का उपयोग करता है यह नियंत्रित करने के लिए कि लक्ष्य फ़ॉर्मेट PowerPoint होने पर ऑब्जेक्ट्स कैसे लिखे जाएँ। `setExportEditableTextBoxes(true)` को सक्षम करके, Excel शीट में कोई भी टेक्स्टबॉक्स रूपांतरण के बाद संपादन योग्य रहता है।

```java
import com.aspose.cells.PdfSaveOptions;

PdfSaveOptions saveOptions = new PdfSaveOptions();
saveOptions.setExportEditableTextBoxes(true); // Text boxes stay editable in the PPTX
```

> **Why use `PdfSaveOptions` for PPTX?**  
> आंतरिक रूप से, Aspose.Cells PowerPoint आउटपुट के लिए PDF रेंडरिंग पाइपलाइन को पुन: उपयोग करता है, जिससे संपादन योग्य तत्वों पर सूक्ष्म नियंत्रण मिलता है। इस फ़्लैग को सेट करना टेक्स्टबॉक्स की संपादन योग्यता को बनाए रखने का अनुशंसित तरीका है।

## चरण 4: वर्कबुक को PowerPoint प्रस्तुति के रूप में सहेजें

अंत में, `workbook.save` को `SaveFormat.PPTX` के साथ कॉल करें। यह कदम **Excel चार्ट से PowerPoint बनाना** वर्कफ़्लो को पूरा करता है।

```java
import com.aspose.cells.SaveFormat;

String targetPath = "YOUR_DIRECTORY/Result.pptx";
workbook.save(targetPath, SaveFormat.PPTX, saveOptions);
System.out.println("Conversion successful! PPTX saved to " + targetPath);
```

सब कुछ एक साथ मिलाकर, पूर्ण प्रोग्राम इस प्रकार दिखता है:

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.PdfSaveOptions;
import com.aspose.cells.SaveFormat;

public class ExcelToPowerPoint {
    public static void main(String[] args) {
        try {
            // 1. Load the workbook containing the chart and textbox
            String sourcePath = "YOUR_DIRECTORY/ChartAndTextbox.xlsx";
            Workbook workbook = new Workbook(sourcePath);

            // 2. Create PDF save options and enable editable text boxes for PPTX output
            PdfSaveOptions saveOptions = new PdfSaveOptions();
            saveOptions.setExportEditableTextBoxes(true); // text boxes will remain editable in the PPTX

            // 3. Save the workbook as a PowerPoint presentation using the configured options
            String targetPath = "YOUR_DIRECTORY/Result.pptx";
            workbook.save(targetPath, SaveFormat.PPTX, saveOptions);

            System.out.println("Conversion successful! PPTX saved to " + targetPath);
        } catch (Exception e) {
            System.err.println("Error during conversion: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

### अपेक्षित आउटपुट

प्रोग्राम चलाने पर यह प्रिंट करता है:

```
Conversion successful! PPTX saved to YOUR_DIRECTORY/Result.pptx
```

जब आप `Result.pptx` को Microsoft PowerPoint में खोलते हैं, तो आप देखेंगे:

* मूल Excel चार्ट को एक मूल PowerPoint चार्ट के रूप में रेंडर किया गया है (PowerPoint के चार्ट एडिटर में संपादन योग्य)।
* Excel से आया टेक्स्टबॉक्स एक संपादन योग्य शेप के रूप में दिखाई देता है, जिससे आप स्लाइड पर सीधे उसका टेक्स्ट बदल सकते हैं।

## सामान्य किनारे के मामलों को संभालना

| स्थिति | सिफ़ारिश किया गया तरीका |
|-----------|----------------------|
| **फ़ाइल नहीं मिली** | `Workbook` कन्स्ट्रक्टर को `try‑catch` ब्लॉक में लपेटें और एक स्पष्ट संदेश दिखाएँ। |
| **वर्कबुक में कोई चार्ट नहीं है** | रूपांतरण से पहले जांचें कि शीट में चार्ट है (`worksheet.getCharts().getCount() > 0`); यदि नहीं, तो चरण को छोड़ दें या एक प्लेसहोल्डर जोड़ें। |
| **बड़ी Excel फ़ाइलें** | `OutOfMemoryError` से बचने के लिए रेंडरिंग के दौरान JVM हीप साइज (`-Xmx2g`) बढ़ाएँ। |
| **लाइसेंस सेट नहीं है** | वर्कबुक लोड करने से पहले `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` कॉल करें ताकि मूल्यांकन वॉटरमार्क हट सके। |

## अक्सर पूछे जाने वाले प्रश्न

**Q: क्या मैं कई वर्कशीट्स को अलग-अलग PowerPoint स्लाइड्स में बदल सकता हूँ?**  
A: हाँ। प्रत्येक वर्कशीट के माध्यम से लूप करें, उसके चार्ट को `PdfSaveOptions` का उपयोग करके नई स्लाइड में निर्यात करें, और सभी शीट्स को प्रोसेस करने के बाद वर्कबुक को एक बार सहेजें।

**Q: क्या यह विधि सेल फ़ॉर्मेटिंग को संरक्षित रखती है?**  
A: केवल चार्ट और टेक्स्टबॉक्स ऑब्जेक्ट्स PowerPoint में ट्रांसफ़र होते हैं। सेल फ़ॉर्मेटिंग Excel फ़ाइल में रहती है; यह PPTX में नहीं दिखती।

**Q: यदि मुझे PPTX के बजाय PDF में निर्यात करना हो तो क्या करें?**  
A: `SaveFormat.PDF` और वही `PdfSaveOptions` उपयोग करें। `setExportEditableTextBoxes` फ़्लैग PDF के लिए भी काम करता है।

## अगले कदम

अब जब आप जानते हैं कि **वर्कबुक को PPTX के रूप में सहेजें** और **चार्ट को PPTX में निर्यात करें**, आप निम्नलिखित का अन्वेषण कर सकते हैं:

* विभिन्न स्लाइड्स में कई चार्ट जोड़ना (`create powerpoint from excel chart` लूप के साथ)।
* अधिक समृद्ध प्रस्तुति शैली के लिए Aspose.Slides for Java का उपयोग करके स्लाइड लेआउट को कस्टमाइज़ करना।
* `Picture` क्लास का उपयोग करके Excel सेल्स से इमेज को PowerPoint में एम्बेड करना।

ये विस्तार आपको पूरी तरह स्वचालित रिपोर्टिंग पाइपलाइन बनाने की अनुमति देते हैं जो Excel डेटा से सीधे परिष्कृत प्रस्तुतियों को जनरेट करती हैं।

---

**सारांश:** इस ट्यूटोरियल ने Aspose.Cells for Java का उपयोग करके **Excel को PowerPoint में बदलने** का एक विश्वसनीय तरीका दिखाया। वर्कबुक को लोड करके, `PdfSaveOptions` को टेक्स्टबॉक्स को संपादन योग्य रखने के लिए कॉन्फ़िगर करके, और `SaveFormat.PPTX` के साथ सहेजकर, आप एक PowerPoint फ़ाइल प्राप्त करते हैं जिसमें लाइव चार्ट और संपादन योग्य शेप्स होते हैं—डायनामिक बिज़नेस प्रस्तुतियों के लिए उत्तम। बैच प्रोसेसिंग के लिए कोड को अनुकूलित करने या बड़े रिपोर्टिंग समाधान में एकीकृत करने में संकोच न करें।

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दर्शाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells for Java का उपयोग करके ट्रेंडलाइन के साथ Excel चार्ट बनाना और इमेज में निर्यात करना](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Aspose.Cells in Java का उपयोग करके Excel चार्ट को SVG में बदलना](/cells/english/java/charts-graphs/convert-excel-charts-svg-aspose-cells-java/)
- [Aspose.Cells&#58; एक चरण-दर-चरण गाइड का उपयोग करके Java में Excel को PDF में बदलना](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}