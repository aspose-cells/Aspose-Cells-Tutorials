---
category: general
date: 2026-08-14
description: Aspose.Cells का उपयोग करके Excel को SVG में निर्यात करते समय SVG में
  फ़ॉन्ट एम्बेड करें। प्रिंट एरिया सेट करना, प्रिंट विकल्प सेट करना, और WRAPCOLS फ़ंक्शन
  का उपयोग करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: hi
lastmod: 2026-08-14
og_description: Aspose.Cells के साथ Excel को SVG में निर्यात करते समय SVG में फ़ॉन्ट
  एम्बेड करें। यह गाइड आपको दिखाता है कि प्रिंट एरिया कैसे सेट करें, प्रिंट विकल्प
  कैसे कॉन्फ़िगर करें, और WRAPCOLS फ़ंक्शन कैसे लागू करें।
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Excel को SVG में निर्यात करते समय SVG में फ़ॉन्ट एम्बेड करें – चरण‑दर‑चरण
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: एक्सेल को SVG में निर्यात करते समय SVG में फ़ॉन्ट एम्बेड करें
url: /hi/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel को SVG में निर्यात करते समय SVG में फ़ॉन्ट एम्बेड करें

यदि आपको **Excel को SVG में निर्यात करते समय SVG में फ़ॉन्ट एम्बेड** करने की आवश्यकता है, तो यह ट्यूटोरियल Aspose.Cells for Java के साथ इसे कैसे करें, बिल्कुल दिखाता है। हम यह भी कवर करेंगे कि **print area सेट करें**, **print options सेट करें**, और **WRAPCOLS फ़ंक्शन का उपयोग** करके डेटा को लेआउट खोए बिना फॉर्मेट कैसे करें।

आप एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलेंगे जो मौजूदा वर्कबुक को लोड करता है, `WRAPCOLS` फ़ॉर्मूला लागू करता है, SVG‑विशिष्ट इमेज विकल्प कॉन्फ़िगर करता है, प्रिंट रेज़ियन को परिभाषित करता है, और अंत में फ़ाइल को एम्बेडेड फ़ॉन्ट्स के साथ SVG के रूप में सहेजता है। कोई बाहरी दस्तावेज़ आवश्यक नहीं—सिर्फ कोड कॉपी करें, चलाएँ, और उत्पन्न SVG की जाँच करें।

## SVG में फ़ॉन्ट एम्बेड करना – ImageOrPrintOptions को कॉन्फ़िगर करना

फ़ॉन्ट एम्बेड करने से यह सुनिश्चित होता है कि SVG Excel में जैसा दिखता है, वैसा ही रेंडर हो, भले ही मशीन पर मूल टाइपफ़ेस स्थापित न हों।

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*यह क्यों महत्वपूर्ण है*: जब `setEmbedFonts(true)` सक्षम किया जाता है, तो Aspose.Cells फ़ॉन्ट डेटा को सीधे SVG के `<defs>` सेक्शन में लिखता है। परिणामस्वरूप एक स्व‑निहित फ़ाइल बनती है जो ब्राउज़र और प्लेटफ़ॉर्म में समान दिखती है।

## Excel को SVG में निर्यात – पूर्ण वर्कफ़्लो

निम्नलिखित चरण अंत‑से‑अंत प्रक्रिया को दर्शाते हैं, वर्कबुक लोड करने से लेकर SVG फ़ाइल सहेजने तक।

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**अपेक्षित आउटपुट**: `output.svg` `YOUR_DIRECTORY` में दिखाई देता है। इसे ब्राउज़र में खोलने पर वर्कशीट सभी फ़ॉन्ट एम्बेडेड के साथ दिखती है, डेटा `WRAPCOLS` की वजह से तीन कॉलम में रैप किया गया है, और केवल `A1:H30` के भीतर के सेल्स रेंडर होते हैं।

## वर्कशीट के लिए प्रिंट एरिया सेट करें

प्रिंट एरिया को परिभाषित करने से निर्यात किया गया SVG एक विशिष्ट रेंज तक सीमित हो जाता है, जिससे फ़ाइल आकार घटता है और दर्शक संबंधित डेटा पर केंद्रित रहता है।

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*टिप*: रेंज Excel की A1 नोटेशन का पालन करती है। यदि आपको डायनामिक रेंज चाहिए, तो आप इसे प्रोग्रामेटिकली `ws.getCells().getMaxDisplayRange()` से गणना कर सकते हैं।

## SVG आउटपुट के लिए प्रिंट विकल्प सेट करें

प्रिंट विकल्प नियंत्रित करते हैं कि Aspose.Cells वर्कशीट को इमेज में कैसे बदलता है। फ़ॉन्ट एम्बेड करने के अलावा, आप रिज़ॉल्यूशन, स्केलिंग, और पेज लेआउट को भी समायोजित कर सकते हैं।

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*आपको प्रिंट विकल्प सेट क्यों करने चाहिए*: स्पष्ट विकल्पों के बिना, Aspose.Cells डिफ़ॉल्ट्स का उपयोग करता है जो फ़ॉन्ट एम्बेडिंग को छोड़ सकते हैं या अनचाहा स्केलिंग फ़ैक्टर लागू कर सकते हैं, जिससे ब्लरी या गलत शैली वाले SVG बनते हैं।

## कॉलम डेटा को रैप करने के लिए WRAPCOLS फ़ंक्शन का उपयोग करें

`WRAPCOLS` एक Excel फ़ॉर्मूला है जो एक वर्टिकल रेंज को निर्दिष्ट संख्या में कॉलम में वितरित करता है। यह तब उपयोगी होता है जब आप लंबी सूची को कॉम्पैक्ट ग्रिड में दिखाना चाहते हैं।

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

जब वर्कबुक सहेजी जाती है, तो Aspose.Cells फ़ॉर्मूला का मूल्यांकन करता है, परिभाषित प्रिंट एरिया के भीतर तीन‑कॉलम लेआउट बनाता है। यह तकनीक किसी भी आकार की रेंज के लिए काम करती है—सिर्फ दूसरे आर्ग्यूमेंट को इच्छित कॉलम संख्या के अनुसार समायोजित करें।

## पूर्ण चलाने योग्य उदाहरण

नीचे पूरा Java प्रोग्राम है जिसे आप किसी भी IDE में पेस्ट कर सकते हैं। सुनिश्चित करें कि आपके क्लासपाथ में Aspose.Cells for Java लाइब्रेरी मौजूद है।

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**सत्यापन चरण**

1. प्रोग्राम चलाएँ।  
2. `output.svg` को वेब ब्राउज़र में खोलें।  
3. पुष्टि करें कि टेक्स्ट मूल Excel फ़ाइल के समान टाइपफ़ेस का उपयोग करता है (फ़ॉन्ट एम्बेडेड हैं)।  
4. यह सत्यापित करें कि केवल `A1:H30` के भीतर के सेल्स दिख रहे हैं और `A2:A10` का डेटा तीन कॉलम में प्रदर्शित हो रहा है।

## सामान्य समस्याएँ और उन्हें कैसे टालें

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| SVG में फ़ॉन्ट नहीं दिख रहे हैं | `setEmbedFonts(false)` या फ़ॉन्ट फ़ाइल उपलब्ध नहीं है | `setEmbedFonts(true)` सुनिश्चित करें और कोड चलाने वाली मशीन पर फ़ॉन्ट इंस्टॉल हो |
| WRAPCOLS मूल्यांकन नहीं करता | कैलकुलेशन इंजन डिसेबल है | निर्यात से पहले `workbook.calculateFormula()` कॉल करें, या सेव के दौरान Aspose.Cells को मूल्यांकन करने दें |
| निर्यात किया गया SVG खाली है | प्रिंट एरिया में कोई डेटा नहीं है | `setPrintArea` को पास किए गए रेंज को दोबारा जांचें |
| SVG फ़ाइल बहुत बड़ी है | स्केलिंग नहीं लागू, बड़ी इमेज रेज़ोल्यूशन | DPI नियंत्रित करने के लिए `imgOptions.setResolution(96)` या समान सेट करें |

## प्रो टिप: कई वर्कशीट्स के लिए ImageOrPrintOptions को पुनः उपयोग करें

यदि आपके वर्कबुक में कई शीट्स हैं जिन्हें समान SVG सेटिंग्स की आवश्यकता है, तो एक ही `ImageOrPrintOptions` इंस्टेंस बनाएं और इसे प्रत्येक वर्कशीट के `PageSetup` को असाइन करें। इससे मेमोरी खपत कम होती है और सभी निर्यातित फ़ाइलों में फ़ॉन्ट एम्बेडिंग सुसंगत रहती है।

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## अगले कदम

* **अन्य वेक्टर फ़ॉर्मेट में निर्यात** – उच्च‑गुणवत्ता वाले PDF के लिए `ImageFormat.SVG` को `ImageFormat.PDF` में बदलें।  
* **बैच प्रोसेसिंग** – `.xlsx` फ़ाइलों के फ़ोल्डर को लूप करके स्वचालित रूप से SVG उत्पन्न करें।  
* **कस्टम फ़ॉन्ट हैंडलिंग** – जब सिस्टम फ़ॉन्ट अपर्याप्त हों, तो विशिष्ट डायरेक्टरी से फ़ॉन्ट लोड करने के लिए `FontSettings` का उपयोग करें।  

**embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options**, और **use WRAPCOLS function** में निपुण होकर आप रिपोर्ट, डैशबोर्ड, और वेब विज़ुअलाइज़ेशन के लिए उच्च‑फ़िडेलिटी SVG जेनरेशन को सीधे Excel डेटा से स्वचालित कर सकते हैं। हैप्पी कोडिंग!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का पता लगाने में मदद करेंगे।

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}