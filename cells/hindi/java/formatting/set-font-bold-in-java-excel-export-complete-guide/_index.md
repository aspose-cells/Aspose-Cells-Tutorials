---
category: general
date: 2026-06-30
description: जावा का उपयोग करके डेटा टेबल को एक्सेल में इम्पोर्ट करते समय फ़ॉन्ट को
  बोल्ड सेट करें। कंडीशनल फॉर्मेटिंग कोड सीखें, डेटा टेबल को एक्सेल में इम्पोर्ट करें
  और टेबल्स को आसानी से स्टाइल करें।
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: hi
og_description: जावा में डेटा टेबल को एक्सेल में निर्यात करते समय फ़ॉन्ट को बोल्ड
  सेट करें। यह गाइड कंडीशनल फ़ॉर्मेटिंग कोड, डेटा टेबल एक्सेल इम्पोर्ट, और टेबल को
  स्टाइल करने को कवर करता है।
og_title: जावा एक्सेल एक्सपोर्ट में फ़ॉन्ट बोल्ड सेट करें – चरण‑दर‑चरण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: जावा एक्सेल निर्यात में फ़ॉन्ट को बोल्ड सेट करें – पूर्ण गाइड
url: /hi/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Set Font Bold in Java Excel Export – Complete Guide

क्या आपने कभी सोचा है **how to set font bold** विशेष कॉलम के लिए जबकि आप **import datatable excel** फ़ाइलें आयात करते हैं? आप अकेले नहीं हैं। कई डेवलपर्स को एक सुंदर‑स्टाइल्ड स्प्रेडशीट की आवश्यकता होने पर हर सेल को मैन्युअल रूप से बदलने में कठिनाई होती है। अच्छी खबर? कुछ ही Java लाइनों के साथ आप एक `DataTable` आयात कर सकते हैं, बोल्ड फ़ॉन्ट लागू कर सकते हैं, और यहाँ तक कि कुछ **conditional formatting code** भी जोड़ सकते हैं—सब प्रोग्रामेटिक रूप से।

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से दिखाएंगे **how to import datatable** को Excel वर्कबुक में कैसे इम्पोर्ट करें, हर सम‑इंडेक्स्ड कॉलम पर **set font bold** लागू करें, और वैकल्पिक रूप से एक सरल कंडीशनल फ़ॉर्मेट जोड़ें। अंत तक आपके पास एक तैयार‑चलाने योग्य स्निपेट और **import table with styles** को समझने के लिए स्पष्ट समझ होगी।

## Prerequisites

- Java 8 या नया (कोड Java 17 पर भी काम करता है)  
- Aspose.Cells for Java (फ़्री ट्रायल संस्करण ठीक है) – Maven डिपेंडेंसी या JAR को अपने क्लासपाथ में जोड़ें।  
- `java.sql` `ResultSet` → `DataTable` रूपांतरण की बुनियादी जानकारी (सरलता के लिए हम एक टेबल को मॉक करेंगे)।  
- एक IDE या Maven/Gradle जैसे बिल्ड टूल।

> **Pro tip:** यदि आप Maven का उपयोग कर रहे हैं, तो इसे अपने `pom.xml` में जोड़ें:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Overview of the Solution

1. **Create a mock `DataTable`** जो उस डेटा की नकल करता है जिसे आप सामान्यतः डेटाबेस से लाते हैं।  
2. **Generate a `CellStyle` array** जहाँ हर सम कॉलम को बोल्ड फ़ॉन्ट मिलती है – यही **set font bold** का मूल है।  
3. **Grab the first worksheet** वर्कबुक से।  
4. **Import the `DataTable`** कॉलम हेडर के साथ, सेल `A1` से शुरू करके, और तैयार शैलियों को लागू करें।  
5. (वैकल्पिक) **Add a conditional formatting rule** ताकि **conditional formatting code** कीवर्ड को दर्शाया जा सके।

हर चरण को सरल अंग्रेज़ी में समझाया गया है, और कोड ब्लॉक्स पूरी तरह से स्व-समाहित हैं ताकि आप तुरंत कॉपी‑पेस्ट करके चला सकें।

---

## Step 1: Retrieve or Build the DataTable to Import

वास्तविक‑दुनिया के ऐप्स में आप संभवतः `ResultSet` → `DataTable` रूपांतरण यूटिलिटीज़ को कॉल करेंगे। इस गाइड के लिए हम एक साधारण `DataTable` मैन्युअली बनाते हैं ताकि आप Excel भाग पर ध्यान केंद्रित कर सकें।

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Why this matters:** `DataTable` तैयार होने से हम **import datatable excel** API और शैली लॉजिक पर ध्यान केंद्रित कर सकते हैं। ऊपर दिया गया मेथड पुन: उपयोग योग्य है—प्रोडक्शन में केवल हार्ड‑कोडेड पंक्तियों को डेटाबेस क्वेरी से बदल दें।

## Step 2: Prepare Styles – This Is Where We **Set Font Bold**

अब हम `CellStyle` ऑब्जेक्ट्स की एक एरे बनाएँगे, प्रत्येक कॉलम के लिए एक। नियम सरल है: **set font bold** हर सम‑इंडेक्स्ड कॉलम (0, 2, 4,…) के लिए। विषम कॉलम सामान्य रहेंगे।

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Why Use an Array of Styles?

- **Performance:** प्रत्येक कॉलम के लिए एक शैली लागू करना प्रत्येक सेल को अलग‑अलग स्टाइल करने से तेज़ होता है।  
- **Consistency:** कॉलम के सभी सेल एक ही फ़ॉर्मेटिंग को विरासत में लेते हैं, जिससे समान रूप मिलता है।  
- **Scalability:** बाद में अधिक कॉलम जोड़ने के लिए केवल एरे को विस्तारित करना पड़ता है—कोड को फिर से लिखने की जरूरत नहीं।

## Step 3: Access the First Worksheet in the Workbook

Aspose.Cells हमारे लिए एक डिफ़ॉल्ट वर्कशीट बनाता है, लेकिन इसे स्पष्ट रूप से प्राप्त करना अच्छा अभ्यास है। यह यह भी दर्शाता है कि **how to import datatable** को किसी विशिष्ट शीट में कैसे किया जाए।

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

## Step 4: Import the DataTable with Styles – The Core **Import Table With Styles** Operation

`importDataTable` मेथड भारी काम करता है। यह डेटा कॉपी करता है, कॉलम हेडर जोड़ता है, और पहले बनाई गई शैली एरे को लागू करता है।

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

जब आप उदाहरण चलाएँगे, तो आप देखेंगे कि **set font bold** कॉलम `ID` और `Score` पर लागू हो गया है, जबकि `Name` सामान्य रहता है।

## Step 5 (Optional): Add Conditional Formatting – A Quick **Conditional Formatting Code** Example

यदि आप उन पंक्तियों को हाइलाइट करना चाहते हैं जहाँ स्कोर 90 से अधिक है, तो कुछ अतिरिक्त लाइनों से यह संभव है। यह **conditional formatting code** कीवर्ड को मुख्य प्रवाह को बाधित किए बिना दर्शाता है।

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Note:** ऊपर दिया गया स्निपेट वैकल्पिक है लेकिन यह दिखाता है कि आप पहले से स्टाइल किए गए टेबल के ऊपर **conditional formatting code** कैसे लेयर कर सकते हैं।

## Putting It All Together – Full, Runnable Example

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण कर सकें।

- [Aspose.Cells for Java का उपयोग करके Excel कंडीशनल फ़ॉर्मेटिंग को स्वचालित करें: एक पूर्ण गाइड](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Aspose.Cells Java में कस्टम फ़ॉन्ट सेटिंग्स को लागू करना Excel फ़ॉर्मेटिंग के लिए](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Aspose.Cells Java का उपयोग करके Excel में फ़ॉन्ट आकार सेट करें - व्यापक गाइड](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}