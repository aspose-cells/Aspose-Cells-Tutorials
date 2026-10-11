---
category: general
date: 2026-10-10
description: Aspose.Cells का उपयोग करके जावा में Excel रेंज को इमेज के रूप में निर्यात
  करना सीखें। गाइड में चयनित सेल्स को इमेज के रूप में निर्यात करना और Excel वर्कशीट
  को चित्र के रूप में सहेजना भी शामिल है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel range as image
- export selected cells as image
- save excel worksheet as picture
language: hi
lastmod: 2026-10-10
og_description: जावा में एक्सेल रेंज को इमेज के रूप में निर्यात करें, चरण‑दर‑चरण समाधान
  के साथ। इसमें चयनित कोशिकाओं को इमेज के रूप में निर्यात करना और एक्सेल वर्कशीट को
  चित्र के रूप में सहेजना शामिल है।
og_image_alt: Diagram showing export Excel range as image using Java and Aspose.Cells
og_title: जावा में एक्सेल रेंज को इमेज के रूप में निर्यात करें – Aspose.Cells की संपूर्ण
  गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-10'
  description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  headline: How to export Excel range as image in Java with Aspose.Cells
  type: TechArticle
- description: Learn how to export Excel range as image in Java using Aspose.Cells.
    The guide also covers export selected cells as image and save Excel worksheet
    as picture.
  name: How to export Excel range as image in Java with Aspose.Cells
  steps:
  - name: Why this method matters
    text: '* **Separation of concerns:** Loading, option configuration, and exporting
      are clearly divided. * **Flexibility:** You can change the image format or DPI
      without touching the core logic. * **Error handling:** Throwing `Exception`
      lets the caller decide whether to log, retry, or abort.'
  - name: 1. Merged cells
    text: Aspose.Cells automatically preserves merged cell appearance, but if you
      need to control the rendering, set `options.setOnePagePerSheet(true)` to force
      the whole sheet onto a single page before exporting.
  - name: 2. Hidden rows or columns
    text: 'By default, hidden rows/columns are not rendered. To include them, enable:'
  - name: 3. Large ranges and memory consumption
    text: 'Exporting very large ranges can consume significant memory. If you encounter
      `OutOfMemoryError`, consider:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel
- Image export
title: Java में Aspose.Cells के साथ Excel रेंज को इमेज के रूप में कैसे एक्सपोर्ट करें
url: /hi/java/images-shapes/how-to-export-excel-range-as-image-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java में Aspose.Cells के साथ Excel रेंज को इमेज के रूप में एक्सपोर्ट कैसे करें

यदि आपको **Excel रेंज को इमेज के रूप में एक्सपोर्ट** करना है, तो यह ट्यूटोरियल Aspose.Cells लाइब्रेरी का उपयोग करके एक पूर्ण Java समाधान दिखाता है। आप यह भी सीखेंगे कि **सेलेक्टेड सेल्स को इमेज के रूप में एक्सपोर्ट** कैसे करें और **Excel वर्कशीट को पिक्चर के रूप में सेव** कैसे करें, रिपोर्टिंग या डॉक्यूमेंटेशन उद्देश्यों के लिए।

वर्कबुक के किसी भाग को पिक्चर में एक्सपोर्ट करने से थर्ड‑पार्टी स्क्रीनशॉट टूल्स की आवश्यकता समाप्त हो जाती है और पिक्सेल‑परफेक्ट परिणाम सुनिश्चित होते हैं। इस गाइड के अंत तक आपके पास एक रीयूज़ेबल मेथड होगा जो PNG (या किसी भी सपोर्टेड फॉर्मेट) को सीधे डिस्क पर लिखता है, जिसे PDFs, ईमेल या वेब पेज में शामिल किया जा सकता है।

## Prerequisites

शुरू करने से पहले सुनिश्चित करें कि आपके पास निम्नलिखित हैं:

* Java 17 या उससे नया इंस्टॉल हो।
* Maven 3.8+ (या कोई अन्य बिल्ड टूल जो Maven डिपेंडेंसीज़ को हैंडल कर सके)।
* Aspose.Cells for Java लाइसेंस (फ्री इवैल्यूएशन काम करता है लेकिन वॉटरमार्क जोड़ता है)।
* एक सैंपल Excel फ़ाइल (`input.xlsx`) जिसे आप किसी ज्ञात डायरेक्टरी में रखें।

अगले सेक्शन मानते हैं कि आप बेसिक Java डेवलपमेंट और Maven प्रोजेक्ट सेटअप से परिचित हैं।

## Step 1: Add Aspose.Cells to your project

अपने `pom.xml` में Aspose.Cells Maven डिपेंडेंसी जोड़ें। यह लाइब्रेरी कोड उदाहरण में उपयोग किए गए `Workbook`, `Worksheet`, और `ImageOrPrintOptions` क्लासेज़ प्रदान करती है।

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Use the latest stable version -->
</dependency>
```

> **Pro tip:** संस्करण संख्या को अपडेट रखें; नए रिलीज़ फॉर्मेट सपोर्ट और परफ़ॉर्मेंस सुधार जोड़ते हैं।

## Step 2: Create a utility method to export a range

एक्सपोर्ट लॉजिक को मेथड में एन्कैप्सुलेट करने से इसे प्रोजेक्ट्स में री‑यूज़ करना आसान हो जाता है और मर्ज्ड सेल्स या हिडन रोज़ जैसे एज केस को हैंडल किया जा सकता है।

```java
import com.aspose.cells.*;

import java.io.File;

/**
 * Exports a specific cell range from an Excel worksheet to an image file.
 *
 * @param workbookPath   Full path to the source .xlsx file.
 * @param sheetIndex     Zero‑based index of the worksheet (0 = first sheet).
 * @param range          A‑style range string, e.g. "A1:G20".
 * @param outputPath     Full path where the image will be saved.
 * @param imageFormat    Desired image format (PNG, JPEG, BMP, etc.).
 * @throws Exception if the file cannot be read or written.
 */
public static void exportRangeAsImage(
        String workbookPath,
        int sheetIndex,
        String range,
        String outputPath,
        ImageFormat imageFormat) throws Exception {

    // Load the workbook
    Workbook wb = new Workbook(workbookPath);

    // Obtain the requested worksheet
    Worksheet ws = wb.getWorksheets().get(sheetIndex);

    // Configure image export options
    ImageOrPrintOptions options = new ImageOrPrintOptions();
    options.setImageFormat(imageFormat);
    // Optional: increase DPI for higher‑resolution output
    options.setHorizontalResolution(300);
    options.setVerticalResolution(300);

    // Export the defined range as an image file
    ws.getCells().exportRangeAsImage(range, outputPath, options);
}
```

### Why this method matters

* **Separation of concerns:** लोडिंग, ऑप्शन कॉन्फ़िगरेशन, और एक्सपोर्ट स्पष्ट रूप से विभाजित हैं।
* **Flexibility:** आप इमेज फॉर्मेट या DPI को कोर लॉजिक को छुए बिना बदल सकते हैं।
* **Error handling:** `Exception` थ्रो करने से कॉलर तय कर सकता है कि लॉग करना है, री‑ट्राई करना है या एबॉर्ट करना है।

## Step 3: Call the method with real parameters

नीचे एक न्यूनतम `main` मेथड दिया गया है जो दिखाता है कि **सेलेक्टेड सेल्स को इमेज के रूप में एक्सपोर्ट** कैसे किया जाए और साथ ही **Excel वर्कशीट को पिक्चर के रूप में सेव** कैसे किया जाए, पूरे शीट रेंज का उपयोग करके।

```java
public class ExcelImageExporter {
    public static void main(String[] args) {
        try {
            String inputFile   = "C:/Data/input.xlsx";
            String outputFile1 = "C:/Data/range.png";
            String outputFile2 = "C:/Data/full_sheet.png";

            // Export a specific range (A1:G20)
            exportRangeAsImage(
                    inputFile,
                    0,                  // first worksheet
                    "A1:G20",
                    outputFile1,
                    ImageFormat.PNG);   // primary format for lossless quality

            // Export the entire first worksheet – effectively saving the worksheet as picture
            exportRangeAsImage(
                    inputFile,
                    0,
                    "A1:" + getLastCellAddress(inputFile, 0), // compute last used cell
                    outputFile2,
                    ImageFormat.PNG);

            System.out.println("Images generated successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    /**
     * Helper that returns the address of the last used cell in a worksheet.
     */
    private static String getLastCellAddress(String workbookPath, int sheetIdx) throws Exception {
        Workbook wb = new Workbook(workbookPath);
        Worksheet ws = wb.getWorksheets().get(sheetIdx);
        // Find the maximum row and column that contain data
        int maxRow = ws.getCells().getMaxDataRow();
        int maxCol = ws.getCells().getMaxDataColumn();
        // Convert column index to A‑style letter (0 -> A)
        String colLetter = CellReference.convertNumToColString(maxCol);
        return colLetter + (maxRow + 1);
    }
}
```

#### Expected output

प्रोग्राम चलाने पर दो PNG फ़ाइलें बनती हैं:

* `range.png` – एक इमेज जिसमें केवल सेल्स **A1:G20** शामिल हैं।
* `full_sheet.png` – पहले वर्कशीट के पूरे उपयोग किए गए एरिया की इमेज, प्रभावी रूप से **Excel वर्कशीट को पिक्चर के रूप में सेव**।

आप इन फ़ाइलों को किसी भी इमेज व्यूअर से खोलकर देख सकते हैं कि विज़ुअल लेआउट Excel व्यू के समान है या नहीं, जिसमें सेल बॉर्डर, रंग, और मर्ज्ड सेल्स शामिल हैं।

## Step 4: Handle common edge cases

### 1. Merged cells

Aspose.Cells स्वचालित रूप से मर्ज्ड सेल्स की उपस्थिति को बरकरार रखता है, लेकिन यदि आपको रेंडरिंग को कंट्रोल करना है, तो `options.setOnePagePerSheet(true)` सेट करके पूरे शीट को एक सिंगल पेज पर फोर्स कर सकते हैं।

### 2. Hidden rows or columns

डिफ़ॉल्ट रूप से, हिडन रोज़/कॉलम रेंडर नहीं होते। उन्हें शामिल करने के लिए सक्षम करें:

```java
options.setSkipEmptyRows(false);
options.setSkipEmptyColumns(false);
```

### 3. Large ranges and memory consumption

बहुत बड़े रेंज को एक्सपोर्ट करने से मेमोरी का काफी उपयोग हो सकता है। यदि आपको `OutOfMemoryError` मिलता है, तो विचार करें:

* DPI कम करें (`options.setHorizontalResolution(150)`)।
* रेंज को छोटे‑छोटे चंक्स में एक्सपोर्ट करें और इमेजेज़ को ग्राफ़िक्स लाइब्रेरी से जोड़ें।

## Step 5: Verify the result programmatically (optional)

यदि आपका डाउनस्ट्रीम प्रोसेस यह पुष्टि करना चाहता है कि इमेज सही ढंग से जेनरेट हुई है, तो आप `javax.imageio.ImageIO` का उपयोग करके PNG लोड कर सकते हैं और उसकी डाइमेंशन्स चेक कर सकते हैं:

```java
import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;

BufferedImage img = ImageIO.read(new File(outputFile1));
System.out.println("Image width: " + img.getWidth() + " px");
System.out.println("Image height: " + img.getHeight() + " px");
```

शून्य‑से‑बड़ी चौड़ाई और ऊँचाई सफल एक्सपोर्ट को दर्शाती है।

## Conclusion

अब आप जानते हैं कि Java में **Excel रेंज को इमेज के रूप में एक्सपोर्ट** कैसे किया जाता है, **सेलेक्टेड सेल्स को इमेज के रूप में एक्सपोर्ट** कैसे किया जाता है, और Aspose.Cells का उपयोग करके **Excel वर्कशीट को पिक्चर के रूप में सेव** कैसे किया जाता है। री‑यूज़ेबल `exportRangeAsImage` मेथड जटिलता को एब्स्ट्रैक्ट करता है, इमेज क्वालिटी को कंट्रोल करने देता है, और किसी भी वर्कशीट इंडेक्स या सेल रेंज के साथ काम करता है।

आगे आप ये कर सकते हैं:

* रिपोर्टिंग के लिए PNG को Aspose.PDF के साथ PDF में कन्वर्ट करें।
* किसी डायरेक्टरी में कई वर्कबुक्स को बैच‑प्रोसेस करें।
* इमेज एक्सपोर्ट को Spring Boot REST एंडपॉइंट में इंटीग्रेट करें ताकि क्लाइंट्स इमेज ऑन‑डिमांड रिक्वेस्ट कर सकें।

विभिन्न इमेज फॉर्मेट (`ImageFormat.JPEG`, `ImageFormat.BMP`) और DPI सेटिंग्स के साथ प्रयोग करें ताकि आपके प्रोजेक्ट की विज़ुअल आवश्यकताओं को पूरा किया जा सके। Happy coding!

## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप एक्सप्लैनेशन्स हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ एक्सप्लोर कर सकते हैं।

- [Export Excel Workbook as Image Using Aspose.Cells for Java: A Step‑By‑Step Guide](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [How to Create Excel Chart with Trendline and Export to Image using Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/trendline-analysis/)
- [Export Excel Cells to Image Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/import-export/export-excel-cells-to-image-aspose-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}