---
category: general
date: 2026-08-20
description: Aspose.Cells का उपयोग करके जावा में एक्सेल वर्कबुक बनाएं, मुद्रा फ़ॉर्मेट
  सेट करें, बोल्ड फ़ॉन्ट जोड़ें, और स्टाइल्ड सेल्स के लिए स्टाइल एरे आयात करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook
- set currency format
- format cells currency
- how to import style
- add bold font
language: hi
lastmod: 2026-08-20
og_description: जावा में एक्सेल वर्कबुक बनाएं, मुद्रा स्वरूप सेट करें, बोल्ड फ़ॉन्ट
  जोड़ें, और Aspose.Cells का उपयोग करके शैली आयात करना सीखें।
og_image_alt: Screenshot of an excel workbook created with currency format and bold
  font using Aspose.Cells
og_title: जावा में स्टाइल किए गए मुद्रा सेल्स के साथ एक्सेल वर्कबुक बनाएं
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  headline: How to create excel workbook with currency format and bold font in Java
  type: TechArticle
- description: Create excel workbook in Java using Aspose.Cells, set currency format,
    add bold font, and import style array for styled cells.
  name: How to create excel workbook with currency format and bold font in Java
  steps:
  - name: Initialise the workbook and worksheet
    text: Creating a fresh workbook gives you a clean container for all subsequent
      formatting.
  - name: Build a DataTable with numeric data
    text: A `DataTable` mimics a database table, making it easy to import rows in
      bulk.
  - name: Define a style – currency format and bold font
    text: Here we **set currency format** and **add bold font** to a `Style` object.
  - name: Configure import options to use the style array
    text: Aspose.Cells lets you pass a `Style[]` via `ImportTableOptions`. This is
      the official **how to import style** method.
  - name: Import the DataTable into the worksheet
    text: Now we bring the data into the sheet at cell `A1`, applying the style array
      automatically.
  - name: Save the workbook to disk
    text: Finally, write the in‑memory workbook to a physical file.
  - name: Expected output
    text: 'When you open `DataTableWithStyleArray.xlsx` in Microsoft Excel, you should
      see:'
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Formatting
title: Java में मुद्रा प्रारूप और बोल्ड फ़ॉन्ट के साथ एक्सेल वर्कबुक कैसे बनाएं
url: /hi/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# जावा में मुद्रा फ़ॉर्मेट और बोल्ड फ़ॉन्ट के साथ एक्सेल वर्कबुक कैसे बनाएं

यदि आपको प्रोग्रामेटिक रूप से **create excel workbook** बनाने की आवश्यकता है, तो यह गाइड आपको ठीक-ठीक दिखाएगा। हम वर्कबुक बनाने, मुद्रा फ़ॉर्मेट लागू करने, बोल्ड फ़ॉन्ट जोड़ने, और Aspose.Cells की **how to import style** सुविधा का उपयोग करने के चरणों से गुजरेंगे ताकि प्रत्येक आयातित सेल सुसंगत दिखे।

आप एक तैयार‑उपयोग `DataTableWithStyleArray.xlsx` फ़ाइल के साथ समाप्त करेंगे जो संख्याओं को डॉलर के रूप में दिखाती है और उन्हें बोल्ड में हाइलाइट करती है। एक्सेल में कोई मैनुअल फ़ॉर्मेटिंग आवश्यक नहीं है।

## आवश्यकताएँ

- Java 17 या बाद का संस्करण स्थापित हो।
- Aspose.Cells for Java लाइसेंस (या एक मुफ्त इवैल्यूएशन की)।
- `aspose-cells` निर्भरता को प्रबंधित करने के लिए Maven या Gradle।
- Java कलेक्शन्स और `DataTable` की बुनियादी जानकारी।

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pro tip:** यदि आपको `LicenseException` मिलती है, तो अपनी लाइसेंस फ़ाइल को क्लासपाथ में रखें और वर्कबुक बनाने से पहले `License license = new License(); license.setLicense("Aspose.Total.Java.lic");` को कॉल करें।

## शैलीबद्ध मुद्रा सेल्स के साथ एक्सेल वर्कबुक कैसे बनाएं

यह अनुभाग मुख्य चरणों को सम्मिलित करता है। प्रत्येक चरण यह बताता है कि यह **क्यों** महत्वपूर्ण है, न कि केवल **क्या** टाइप करना है।

### चरण 1: वर्कबुक और वर्कशीट को इनिशियलाइज़ करें

एक नई वर्कबुक बनाना आपको सभी आगे के फ़ॉर्मेटिंग के लिए एक साफ़ कंटेनर प्रदान करता है।

```java
// Step 1: Create a new workbook and get the first worksheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
Cells cells = worksheet.getCells();                     // shortcut to work with cells
```

> **Why:** `Workbook` ऑब्जेक्ट पूरे Excel फ़ाइल का प्रतिनिधित्व करता है। पहले `Worksheet` तक पहुंचने से आप तुरंत डेटा भरना शुरू कर सकते हैं।

### चरण 2: संख्यात्मक डेटा के साथ DataTable बनाएं

`DataTable` एक डेटाबेस टेबल की नकल करता है, जिससे पंक्तियों को बल्क में आयात करना आसान हो जाता है।

```java
// Step 2: Build a DataTable with sample numeric data
DataTable dataTable = new DataTable();
dataTable.getColumns().add("Amount", DataType.DOUBLE); // column type DOUBLE ensures numeric handling
dataTable.getRows().add(new Object[]{1234.56});
dataTable.getRows().add(new Object[]{7890.12});
```

> **Why:** `DOUBLE` का उपयोग यह सुनिश्चित करता है कि मान अपनी दशमलव सटीकता बनाए रखें, जो बाद में **format cells currency** करने के लिए आवश्यक है।

### चरण 3: एक शैली परिभाषित करें – मुद्रा फ़ॉर्मेट और बोल्ड फ़ॉन्ट

यहाँ हम `Style` ऑब्जेक्ट में **currency format सेट** करते हैं और **bold फ़ॉन्ट जोड़ते** हैं।

```java
// Step 3: Define a style (currency format and bold font) for the imported cells
Style currencyStyle = workbook.createStyle();                // create a reusable style instance
currencyStyle.getNumber().setFormat("$#,##0.00");            // set currency format (e.g., $1,234.56)
currencyStyle.getFont().setBold(true);                      // make the font bold
Style[] styleArray = new Style[] { currencyStyle };          // style array required by ImportTableOptions
```

> **Why:** `Number` फ़ॉर्मेट स्ट्रिंग `$#,##0.00` Excel को बताती है कि सेल को मौद्रिक मान के रूप में माना जाए, जबकि `setBold(true)` संख्याओं पर ध्यान आकर्षित करता है। शैली को एक एरे में रखकर हम **how to import style** चरण के लिए तैयार होते हैं।

### चरण 4: शैली एरे का उपयोग करने के लिए इम्पोर्ट विकल्प कॉन्फ़िगर करें

Aspose.Cells आपको `ImportTableOptions` के माध्यम से `Style[]` पास करने देता है। यह आधिकारिक **how to import style** विधि है।

```java
// Step 4: Set up import options to use the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(styleArray); // tells the importer to apply our currencyStyle to every column
```

> **Why:** `ImportTableOptions` के बिना, आयातित सेल्स डिफ़ॉल्ट शैली को विरासत में ले लेंगे, जिससे हमने परिभाषित मुद्रा फ़ॉर्मेट और बोल्डनेस खो जाएगी।

### चरण 5: DataTable को वर्कशीट में आयात करें

अब हम डेटा को शीट में `A1` सेल पर लाते हैं, और शैली एरे को स्वचालित रूप से लागू करते हैं।

```java
// Step 5: Import the DataTable into the worksheet at A1, applying the style
cells.importDataTable(dataTable, true, "A1", importOptions);
```

- `true` दर्शाता है कि `DataTable` की पहली पंक्ति में कॉलम हेडर हैं।
- `"A1"` वह शीर्ष‑बाएँ कोना है जहाँ आयात शुरू होता है।

> **Why:** शैली एरे के साथ आयात करने से यह सुनिश्चित होता है कि प्रत्येक आयातित सेल को हमने पहले तैयार किया हुआ **format cells currency** शैली प्राप्त हो।

### चरण 6: वर्कबुक को डिस्क पर सहेजें

अंत में, मेमोरी में मौजूद वर्कबुक को एक भौतिक फ़ाइल में लिखें।

```java
// Step 6: Save the workbook to a file
String outputPath = "YOUR_DIRECTORY/DataTableWithStyleArray.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to: " + outputPath);
```

> **Why:** सहेजने से फ़ॉर्मेटिंग स्थायी हो जाती है, जिससे आप या डाउनस्ट्रीम प्रक्रियाएँ फ़ाइल को इच्छित रूप में Excel में खोल सकते हैं।

## पूर्ण स्रोत कोड

नीचे पूर्ण, तैयार‑चलाने योग्य Java क्लास दिया गया है। इसे अपने IDE में कॉपी करें, `YOUR_DIRECTORY` को मौजूदा फ़ोल्डर से बदलें, और चलाएँ।

```java
import com.aspose.cells.*;

public class StyleArrayImportTutorial {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Step 2: Build a DataTable with sample numeric data
        DataTable dataTable = new DataTable();
        dataTable.getColumns().add("Amount", DataType.DOUBLE);
        dataTable.getRows().add(new Object[]{1234.56});
        dataTable.getRows().add(new Object[]{7890.12});

        // Step 3: Define a style (currency format and bold font) for the imported cells
        Style currencyStyle = workbook.createStyle();
        currencyStyle.getNumber().setFormat("$#,##0.00");   // set currency format
        currencyStyle.getFont().setBold(true);             // add bold font
        Style[] styleArray = new Style[] { currencyStyle };

        // Step 4: Set up import options to use the style array
        ImportTableOptions importOptions = new ImportTableOptions();
        importOptions.setStyleArray(styleArray);           // how to import style

        // Step 5: Import the DataTable into the worksheet at A1, applying the style
        cells.importDataTable(dataTable, true, "A1", importOptions);

        // Step 6: Save the workbook to a file
        workbook.save("YOUR_DIRECTORY/DataTableWithStyleArray.xlsx");
        System.out.println("Workbook created successfully.");
    }
}
```

### अपेक्षित आउटपुट

जब आप Microsoft Excel में `DataTableWithStyleArray.xlsx` खोलते हैं, तो आपको यह दिखना चाहिए:

| राशि |
|------|
| **$1,234.56** |
| **$7,890.12** |

- संख्याएँ **currency format** (`$` चिह्न, दो दशमलव स्थान) के साथ प्रदर्शित होती हैं।
- दोनों सेल्स का फ़ॉन्ट **bold** है, जिससे वे उभरे हुए दिखते हैं।

## सामान्य विविधताएँ और किनारे के मामले

| परिदृश्य | क्या बदलें | कारण |
|----------|------------|------|
| **विभिन्न मुद्रा** | `currencyStyle.getNumber().setFormat("€#,##0.00");` | यूरो प्रतीक या किसी भी स्थानीय‑विशिष्ट फ़ॉर्मेट का उपयोग करें। |
| **विभिन्न शैलियों के साथ कई कॉलम** | Create multiple `Style` objects, populate `styleArray` in the same order as columns. | प्रत्येक कॉलम का अपना नंबर फ़ॉर्मेट, फ़ॉन्ट, बैकग्राउंड आदि हो सकता है। |
| **बड़े डेटा सेट** | Use `cells.importDataTable(dataTable, false, "A1", importOptions);` and set `importOptions.setImportDataOptions(ImportDataOptions.DATA_ONLY);` | हेडर पंक्तियों या अनावश्यक मेटाडेटा को छोड़कर प्रदर्शन में सुधार करता है। |
| **आयात के बाद शैली लागू करना** | Call `cells.get("A2").setStyle(currencyStyle);` for individual cells. | जब केवल कुछ पंक्तियों को विशेष फ़ॉर्मेटिंग की आवश्यकता हो तो उपयोगी। |

## उत्पादन उपयोग के लिए टिप्स

- **License early**: वर्कबुक बनाने से पहले अपनी Aspose.Cells लाइसेंस रजिस्टर करें ताकि इवैल्यूएशन वॉटरमार्क न आए।
- **Thread safety**: `Workbook` इंस्टेंस **थ्रेड‑सेफ़** नहीं हैं। यदि आप एक साथ कई फ़ाइलें बनाते हैं तो प्रत्येक थ्रेड के लिए अलग इंस्टेंस बनाएं।
- **Memory management**: बहुत बड़े शीट्स के लिए, मेमोरी उपयोग कम रखने हेतु `Workbook` की स्ट्रीमिंग API (`Workbook` → `WorkbookDesigner`) उपयोग करने पर विचार करें।
- **Testing**: एक यूनिट टेस्ट शामिल करें जो सहेजी गई फ़ाइल को Apache POI से खोलता है और सुनिश्चित करता है कि सेल शैली का नंबर फ़ॉर्मेट `"$#,##0.00"` से मेल खाता है।

## निष्कर्ष

अब आप जानते हैं कि जावा में **create excel workbook** कैसे करें, **currency format सेट** करें, **bold फ़ॉन्ट जोड़ें**, और Aspose.Cells के `ImportTableOptions` का उपयोग करके सही ढंग से **how to import style** कैसे करें। यह एंड‑टू‑एंड समाधान मैनुअल Excel चरणों को समाप्त करता है और सुनिश्चित करता है कि प्रत्येक आयातित सेल समान **format cells currency** शैली का पालन करे।

अगली चुनौती के लिए तैयार हैं? कंडीशनल फ़ॉर्मेटिंग जोड़ने, चार्ट एम्बेड करने, या वर्कबुक को PDF में एक्सपोर्ट करने का प्रयास करें—सभी एक ही style‑array तकनीक का पुनः उपयोग करते हुए। कोडिंग का आनंद लें!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [जावा में Aspose.Cells का उपयोग करके Excel वर्कबुक बनाना: चरण‑दर‑चरण गाइड](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java का उपयोग करके Excel सेल्स को बनाना और फ़ॉर्मेट करना: चरण‑दर‑चरण गाइड](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)
- [Aspose.Cells for Java का उपयोग करके Excel सेल्स को स्टाइल करना और हाइपरलिंक जोड़ना](/cells/english/java/formatting/style-excel-cells-hyperlinks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}