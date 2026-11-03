---
category: general
date: 2026-10-01
description: जावा में ShapeExportOptions का उपयोग करके आकार को निर्यात करना सीखें,
  Aspose.Cells के साथ PPTX में परिवर्तित करते समय आकार को संपादन योग्य रखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: hi
lastmod: 2026-10-01
og_description: जावा में ShapeExportOptions का उपयोग करके आकार को निर्यात करें और
  संपादन योग्य PPTX फ़ाइलें बनाएं। यह ट्यूटोरियल Aspose.Cells का उपयोग करके पूरी प्रक्रिया
  को आपके सामने लाता है।
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: जावा में ShapeExportOptions के साथ शेप निर्यात – चरण-दर-चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Java में ShapeExportOptions के साथ shape को कैसे निर्यात करें
url: /hi/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to export shape with ShapeExportOptions in Java

यदि आपको Excel वर्कबुक से **ShapeExportOptions के साथ shape को एक्सपोर्ट** करना है, तो यह गाइड आपको सटीक चरण दिखाता है। आप देखेंगे कि PPTX फ़ाइल में बदलते समय shape को कैसे संपादन योग्य रखा जाए, जो PowerPoint में आगे की संपादन के लिए आवश्यक है।

शेप्स को एक्सपोर्ट करना एक सामान्य कार्य है जब आप स्प्रेडशीट से स्लाइड डेक बनाते हैं—चाहे आप सेल्स डेक, रिपोर्टिंग डैशबोर्ड या ऑटोमेटेड प्रेजेंटेशन बना रहे हों। यह ट्यूटोरियल सब कुछ कवर करता है, प्रोजेक्ट सेटअप से लेकर एक्सपोर्टेड फ़ाइल की पुष्टि तक, और यह **Aspose.Cells for Java** लाइब्रेरी का उपयोग करता है।

## What you’ll need

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

- Java 17 या नया (कोड किसी भी हालिया JDK के साथ कम्पाइल होता है)
- Maven या Gradle डिपेंडेंसी मैनेजमेंट के लिए
- एक Excel फ़ाइल (`Shapes.xlsx`) जिसमें कम से कम एक टेक्स्टबॉक्स या अन्य shape हो
- Aspose.Cells APIs की बुनियादी समझ

## Step 1: Add Aspose.Cells to your project (Aspose Cells export shape)

यदि आप Maven उपयोग कर रहे हैं, तो अपने `pom.xml` में निम्न डिपेंडेंसी जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Gradle के लिए, इसे `build.gradle` में रखें:

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** लाइसेंस को जल्दी रजिस्टर करें ताकि इवैल्यूएशन वाटरमार्क से बचा जा सके।  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Step 2: Load the workbook that contains the shape

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

`Workbook` ऑब्जेक्ट पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। इसे लोड करना किसी भी shape मैनिपुलेशन की पहली पूर्वशर्त है।

## Step 3: Access the worksheet and retrieve the desired shape (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Why this matters:** Shapes प्रत्येक‑वर्कशीट में संग्रहीत होते हैं, इसलिए आपको सही शीट पर नेविगेट करना होगा इससे पहले कि आप किसी विशिष्ट shape को एक्सपोर्ट कर सकें।

## Step 4: Configure **ShapeExportOptions** to keep the shape editable (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

`ExportAsEditable` को `true` सेट करने से Aspose.Cells shape के वेक्टर डेटा को संरक्षित रखता है, जिससे PowerPoint उपयोगकर्ता इम्पोर्ट के बाद shape को संशोधित कर सकते हैं।

## Step 5: Export the shape directly to a PPTX file (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

`exportToImage` मेथड कई इमेज फ़ॉर्मेट्स के लिए काम करता है; जब टार्गेट फ़ाइल नाम `.pptx` पर समाप्त होता है, तो Aspose.Cells एक PowerPoint स्लाइड लिखता है जिसमें वह shape शामिल होती है।

### Expected result

- निर्दिष्ट डायरेक्टरी में `textbox.pptx` बनता है।
- PowerPoint में फ़ाइल खोलने पर एक ही स्लाइड में मूल टेक्स्टबॉक्स दिखता है।
- टेक्स्टबॉक्स पूरी तरह से संपादन योग्य है (आप टेक्स्ट, फ़ॉन्ट, आकार आदि बदल सकते हैं)।

## Step 6: Verify the output and handle common edge cases

### Verify programmatically

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

यदि `slideCount` `1` के बराबर है, तो एक्सपोर्ट सफल रहा।

### Edge case: Multiple shapes

यदि वर्कशीट में कई shapes हैं और आप केवल एक विशिष्ट shape चाहते हैं, तो उसे नाम से खोजें:

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Edge case: Shape not found

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Edge case: Export to other formats

`ShapeExportOptions` PNG, JPEG, SVG, और EMF को भी सपोर्ट करता है। फ़ाइल एक्सटेंशन बदलें और वैकल्पिक रूप से `exportOptions.setImageFormat(ImageFormat.PNG)` सेट करें।

## Full, runnable example

सभी हिस्सों को मिलाकर आपको एक स्व-निहित प्रोग्राम मिलता है जिसे आप अपने IDE में कॉपी‑पेस्ट कर सकते हैं:

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

प्रोग्राम चलाने से `textbox.pptx` बनता है। इसे PowerPoint में खोलें, टेक्स्टबॉक्स पर राइट‑क्लिक करें, और आप सामान्य एडिटिंग हैंडल्स देखेंगे—जिससे पुष्टि होती है कि **export shape with ShapeExportOptions** ने संपादन क्षमता को संरक्षित किया है।

## Frequently asked questions

| Question | Answer |
|----------|--------|
| *क्या मैं chart shape को एक्सपोर्ट कर सकता हूँ?* | हाँ। वही `exportToImage` कॉल चार्ट, इमेज और SmartArt के लिए भी काम करती है। |
| *यदि मुझे उच्च रिज़ॉल्यूशन PNG चाहिए तो क्या करें?* | `options.setImageFormat(ImageFormat.PNG)` सेट करें और एक्सपोर्ट से पहले `options.setResolution(300)` समायोजित करें। |
| *क्या एक्सपोर्टेड PPTX पुराने PowerPoint संस्करणों के साथ संगत है?* | लाइब्रेरी Office Open XML (PPTX) लिखती है, जो PowerPoint 2007 और बाद के संस्करणों द्वारा समर्थित है। |
| *क्या इसको काम करने के लिए लाइसेंस चाहिए?* | फ्री इवैल्यूएशन काम करता है लेकिन वाटरमार्क जोड़ता है। लाइसेंस रजिस्टर करने से वह हट जाता है। |

## Next steps

- यदि आपको कई एक्सपोर्टेड shapes को एक ही स्लाइड डेक में संयोजित करना है, तो **Aspose.Slides for Java** का अन्वेषण करें।
- जब आप रास्टर इमेज (PNG/JPEG) चाहते हैं तेज़ रेंडरिंग के लिए, तो **ShapeExportOptions.setExportAsEditable(false)** उपयोग करें।
- बैच प्रोसेसिंग को ऑटोमेट करें: सभी वर्कशीट्स पर लूप करें और प्रत्येक shape को अलग‑अलग PPTX फ़ाइलों में एक्सपोर्ट करें।

---

### Conclusion

अब आप जानते हैं कि Java में **ShapeExportOptions के साथ shape को एक्सपोर्ट** कैसे किया जाता है, और कैसे टेक्स्टबॉक्स (या कोई भी अन्य shape) को PPTX फ़ाइल में बदलते समय संपादन योग्य रखा जाता है। ऊपर दिए गए चरणों—लाइब्रेरी सेटअप, वर्कबुक लोड करना, `ShapeExportOptions` कॉन्फ़िगर करना, और `exportToImage` को कॉल करना—को फॉलो करके आप किसी भी ऑटोमेटेड रिपोर्टिंग पाइपलाइन में shape एक्सपोर्ट को इंटीग्रेट कर सकते हैं।

विभिन्न shapes, आउटपुट फ़ॉर्मेट्स और रिज़ॉल्यूशन सेटिंग्स के साथ प्रयोग करने में संकोच न करें। यदि यह गाइड आपके काम आया, तो इसे टीम के साथ शेयर करें या भविष्य के संदर्भ के लिए बुकमार्क करें। हैप्पी कोडिंग!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर कर सकते हैं।

- [How to Adjust Shape Margins in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [How to Apply 3D Shape Formatting in Excel Using Aspose.Cells for Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Aspose Cells Java Workbook Shape Copying Guide](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}