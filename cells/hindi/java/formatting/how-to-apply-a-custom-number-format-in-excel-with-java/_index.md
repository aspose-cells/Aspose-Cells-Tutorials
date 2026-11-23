---
category: general
date: 2026-11-22
description: जावा का उपयोग करके एक्सेल में एक कॉलम को मुद्रा के रूप में स्वरूपित करने
  के लिए कस्टम नंबर फ़ॉर्मेट का उपयोग करना सीखें। एक सरल शैली के साथ एक्सेल नंबर फ़ॉर्मेट
  को जल्दी सेट करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: hi
lastmod: 2026-11-22
og_description: जावा के साथ एक्सेल में कस्टम नंबर फ़ॉर्मेट लागू करें। यह ट्यूटोरियल
  दिखाता है कि एक्सेल नंबर फ़ॉर्मेट कैसे सेट करें और पहली कॉलम को मुद्रा के रूप में
  स्टाइल करें।
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: जावा के साथ एक्सेल में कस्टम नंबर फ़ॉर्मेट लागू करें – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: जावा के साथ एक्सेल में कस्टम नंबर फ़ॉर्मेट कैसे लागू करें
url: /hi/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java के साथ Excel में कस्टम नंबर फ़ॉर्मेट कैसे लागू करें

यदि आपको Excel वर्कशीट में किसी कॉलम को **कस्टम नंबर फ़ॉर्मेट** करना है, तो यह गाइड आपको Java का उपयोग करके इसे बिल्कुल कैसे करना है दिखाएगा। चाहे आप वित्तीय रिपोर्ट बना रहे हों या अकाउंटिंग डेटा एक्सपोर्ट कर रहे हों, पहले कॉलम को मुद्रा (currency) के रूप में फ़ॉर्मेट करने से आउटपुट तुरंत पढ़ने योग्य हो जाता है।

नीचे के उदाहरण में हम **कॉलम को मुद्रा के रूप में फ़ॉर्मेट** करेंगे, इस स्टाइल को पहले कॉलम पर लागू करेंगे, और फिर एक `DataTable` को वर्कशीट में इम्पोर्ट करेंगे। वही तरीका किसी भी संख्यात्मक फ़ॉर्मेट के लिए काम करता है जिसे आप दिखाना चाहते हैं।

## आप क्या सीखेंगे

* Apache POI के `Style` ऑब्जेक्ट के साथ **कस्टम नंबर फ़ॉर्मेट** कैसे बनाएं।  
* किसी विशिष्ट कॉलम के लिए **Excel नंबर फ़ॉर्मेट सेट** करना, जिसमें **set currency format** केस भी शामिल है।  
* `DataTable` इम्पोर्ट करते समय **पहले कॉलम को स्टाइल** कैसे करें।  
* वर्कबुक को सेव करें और सत्यापित करें कि फ़ॉर्मेट सही ढंग से दिख रहा है।

### पूर्वापेक्षाएँ

* Java 17 या उससे नया संस्करण।  
* Apache POI 5.x (लाइब्रेरी जो `Workbook`, `Worksheet`, और `Style` प्रदान करती है)।  
* एक `DataTable` इम्प्लीमेंटेशन जो कोड सैंपल में दिखाए अनुसार इटरटेबल हो।  
* Java और Excel अवधारणाओं की बुनियादी समझ।

---

## चरण 1: प्रोजेक्ट सेट अप करें और डेटा इम्पोर्ट करें

सबसे पहले, अपने प्रोजेक्ट में Apache POI जोड़ें। यदि आप Maven उपयोग कर रहे हैं, तो निम्न डिपेंडेंसी शामिल करें:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

अगला, स्रोत डेटा को `DataTable` के रूप में प्राप्त करें। वास्तविक दुनिया में यह डेटाबेस क्वेरी, CSV फ़ाइल, या API रिस्पॉन्स से आ सकता है।

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **प्रो टिप:** सुनिश्चित करें कि `DataTable` कॉलम्स के पास सही Java टाइप्स (`Integer`, `Double`, आदि) हों, क्योंकि नंबर फ़ॉर्मेट केवल संख्यात्मक सेल्स को प्रभावित करता है।

---

## चरण 2: पहले कॉलम के लिए **कस्टम नंबर फ़ॉर्मेट** बनाएं

एक **कस्टम नंबर फ़ॉर्मेट** Excel को बताता है कि संख्यात्मक मानों को कैसे प्रदर्शित किया जाए। मानों को मुद्रा के रूप में दिखाने के लिए हम बिल्ट‑इन `CURRENCY` फ़ॉर्मेट का उपयोग करते हैं, लेकिन आप `"$#,##0.00"` जैसे पैटर्न भी परिभाषित कर सकते हैं।

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**यह क्यों काम करता है:**  
* `createCellStyle()` एक पुन: उपयोग योग्य स्टाइल ऑब्जेक्ट लौटाता है।  
* `setDataFormat()` **set currency format** को स्टाइल से जोड़ता है, जिसे Excel प्रत्येक सेल पर लागू करता है जो इस स्टाइल का उपयोग करता है।  
* स्टाइल को `columnStyles[0]` में स्टोर करके हम सुनिश्चित करते हैं कि केवल पहला कॉलम ही मुद्रा फ़ॉर्मेट प्राप्त करे।

---

## चरण 3: कॉलम स्टाइल्स लागू करते हुए `DataTable` इम्पोर्ट करें

अब हम डेटा को वर्कशीट में इम्पोर्ट करते हैं। `importDataTable` मेथड स्टाइल एरे को स्वीकार करता है, जिससे हम **पहले कॉलम को स्टाइल** कर सकते हैं और बाकी कॉलम्स को डिफ़ॉल्ट फ़ॉर्मेट पर छोड़ सकते हैं।

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

ऊपर दिया गया कॉल **पहले कॉलम के लिए Excel नंबर फ़ॉर्मेट सेट** करता है। सभी अन्य कॉलम वर्कबुक की डिफ़ॉल्ट स्टाइल को विरासत में लेते हैं, जिससे कोड सरल और कुशल रहता है।

---

## चरण 4: वर्कबुक को सेव करें और परिणाम सत्यापित करें

अंत में, वर्कबुक को फ़ाइल में लिखें और Excel में खोलें यह पुष्टि करने के लिए कि पहला कॉलम मुद्रा प्रतीक दिखा रहा है।

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**अपेक्षित आउटपुट:**  
जब आप *FormattedReport.xlsx* खोलते हैं, तो कॉलम A में मान उचित मुद्रा प्रतीक (जैसे `$1,234.00`) के साथ दिखाई देंगे। सभी अन्य कॉलम अपने मूल संख्यात्मक प्रतिनिधित्व को बरकरार रखते हैं।

---

## सामान्य विविधताएँ और किनारे के केस

| स्थिति | समायोजन |
|-----------|------------|
| **विभिन्न मुद्रा** (जैसे यूरो) | `Style.CustomNumberFormat.CURRENCY` को एक कस्टम पैटर्न से बदलें: <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **एक से अधिक स्टाइल्ड कॉलम** | `columnStyles[]` में अतिरिक्त एंट्रीज़ जोड़ें और उनके अपने `CellStyle` ऑब्जेक्ट्स असाइन करें। |
| **बड़ी डेटा सेट्स** | `importDataTable` को बैच में या स्ट्रीम रोज़ में उपयोग करें ताकि `OutOfMemoryError` से बचा जा सके। |
| **लोकैल‑विशिष्ट विभाजक** | `java.text.NumberFormat` का उपयोग करके लोकैल‑अवेयर पैटर्न जनरेट करें और उसे `setDataFormat` को पास करें। |

> **ध्यान रखें:** कई कॉलम्स में एक ही `CellStyle` ऑब्जेक्ट को पुन: उपयोग करने से अप्रत्याशित फ़ॉर्मेटिंग हो सकती है क्योंकि Excel प्रत्येक वर्कबुक में अलग-अलग स्टाइल्स की संख्या पर सीमा लगाता है। प्रत्येक अनोखे फ़ॉर्मेट के लिए अलग स्टाइल बनाएं।

---

## पूर्ण चलाने योग्य उदाहरण

नीचे एक स्व-समाहित प्रोग्राम दिया गया है जो पूरे वर्कफ़्लो को दर्शाता है, डेटा निर्माण से लेकर फ़ॉर्मेटेड वर्कबुक को सेव करने तक।

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

प्रोग्राम चलाने पर **FormattedReport.xlsx** बनता है जहाँ कॉलम A ( “Amount” कॉलम) **कस्टम नंबर फ़ॉर्मेट** के साथ डॉलर साइन और दो दशमलव स्थान दिखाता है।

---

## निष्कर्ष

अब आप Java से Excel वर्कशीट में **कस्टम नंबर फ़ॉर्मेट** कैसे लागू करें, **कॉलम को मुद्रा के रूप में फ़ॉर्मेट** करें, और डेटा इम्पोर्ट करते समय **पहले कॉलम को स्टाइल** करें, यह जानते हैं। एक पुन: उपयोग योग्य `CellStyle` बनाकर और उसे `importDataTable` को पास करके आप किसी भी कॉलम के लिए **Excel नंबर फ़ॉर्मेट सेट** कर सकते हैं बिना प्रत्येक सेल को मैन्युअली लूप किए।

अगला प्रयास करें:

* `setDataFormat` को लोकैल‑विशिष्ट पैटर्न के साथ उपयोग करके **set currency format** को और कस्टमाइज़ करें

## आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में निपुण हो सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकें।

- [Set Number Format Excel in Java – Complete Guide](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Apply Number Format Excel in Java – Complete Aspose.Cells Guide](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [How to create excel workbook with currency format and bold font in Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}