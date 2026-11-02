---
category: general
date: 2026-09-27
description: Java में Excel वर्कबुक बनाएं, SQL डेटा आयात करें, कॉलम का नंबर फ़ॉर्मेट
  सेट करें, और Aspose.Cells का उपयोग करके वर्कबुक को XLSX के रूप में सहेजें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: hi
lastmod: 2026-09-27
og_description: जावा में एक्सेल वर्कबुक बनाएं, SQL डेटा आयात करें, कॉलम का नंबर फ़ॉर्मेट
  सेट करें, और पूरी तरह कार्यशील जावा उदाहरण के साथ वर्कबुक को XLSX के रूप में सहेजें।
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: जावा में एक्सेल वर्कबुक बनाएं – SQL डेटा आयात करें और कॉलम नंबर फ़ॉर्मेट
  सेट करें
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: जावा में एक्सेल वर्कबुक बनाएं और कॉलम नंबर फ़ॉर्मेट लागू करें
url: /hi/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel वर्कबुक जावा बनाएं और कॉलम नंबर फ़ॉर्मेट लागू करें

यदि आपको **create Excel workbook java** बनाना है और संख्यात्मक कॉलम को स्टाइल करना है, तो यह गाइड आपको ठीक-ठीक दिखाएगा। आप सीखेंगे कि SQL डेटा को Excel में कैसे इम्पोर्ट करें, प्रत्येक कॉलम के लिए नंबर फ़ॉर्मेट कैसे सेट करें, और Aspose.Cells लाइब्रेरी का उपयोग करके **save workbook as XLSX** कैसे करें।

Java से स्प्रेडशीट्स के साथ काम करना अक्सर टुकड़े‑टुकड़े जैसा लगता है—डेवलपर्स स्निपेट्स को कॉपी‑पेस्ट करते हैं, नंबर फ़ॉर्मेट करना भूल जाते हैं, या वास्तविक Excel फ़ाइलों के बजाय CSV फ़ाइलें बनाते हैं। यह ट्यूटोरियल इस झंझट को दूर करता है एक एकल, एंड‑टू‑एंड समाधान प्रदान करके जिसे आप किसी भी Java प्रोजेक्ट में जोड़ सकते हैं।

लेख के अंत तक आप सक्षम होंगे:

* डेटाबेस से कनेक्ट होकर `DataTable` (या `ResultSet`) प्राप्त करना  
* Aspose.Cells के साथ एक नया वर्कबुक बनाना  
* प्रत्येक कॉलम पर एक समान **add number format excel** स्टाइल लागू करना  
* अपनी पसंद के स्थान पर **Save workbook as XLSX** करना  

एकमात्र पूर्वापेक्षा एक Java विकास वातावरण (JDK 8+ अनुशंसित) और आपके क्लासपाथ में Aspose.Cells for Java JAR है।

## आवश्यकताएँ

| आवश्यकता | क्यों महत्वपूर्ण है |
|-------------|----------------|
| JDK 8 or newer | उदाहरण में उपयोग किए गए भाषा फीचर्स प्रदान करता है। |
| Aspose.Cells for Java (latest version) | Office स्थापित किए बिना Excel निर्माण, स्टाइलिंग और सहेजने को संभालता है। |
| A JDBC‑compatible database (e.g., MySQL, PostgreSQL) | SQL डेटा प्रदान करता है जिसे हम इम्पोर्ट करेंगे। |
| Maven or Gradle (optional) | डिपेंडेंसी प्रबंधन को सरल बनाता है। |

Add Aspose.Cells to your Maven `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Or download the JAR directly from the Aspose website and add it to your project’s classpath.

## चरण 1: Excel वर्कबुक जावा बनाएं

पहला तार्किक ब्लॉक एक नया `Workbook` इंस्टैंसिएट करना है। यह ऑब्जेक्ट मेमोरी में पूरी Excel फ़ाइल का प्रतिनिधित्व करता है और आपको वर्कशीट्स, सेल्स और स्टाइल्स तक पहुंच देता है।

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

वर्कबुक को पहले से बनाना हमें एक `Style` फ़ैक्ट्री भी देता है जिसकी हमें बाद में **set number format column** करने के लिए आवश्यकता होगी।

## चरण 2: SQL से डेटा प्राप्त करें (import sql data excel)

नीचे हम एक JDBC कनेक्शन खोलते हैं, एक सरल `SELECT` स्टेटमेंट चलाते हैं, और परिणाम सेट को Aspose `DataTable` में लोड करते हैं। `DataTable` क्लास .NET `DataTable` की नकल करता है और `importDataTable` मेथड के साथ सहजता से काम करता है।

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **टिप:** यदि आपके पास पहले से किसी अन्य स्रोत (जैसे CSV पार्सिंग) से `DataTable` है, तो आप JDBC कोड को छोड़ सकते हैं और सीधे वह टेबल रिटर्न कर सकते हैं।

## चरण 3: पुन: उपयोग योग्य स्टाइल तैयार करें (add number format excel)

हम चाहते हैं कि प्रत्येक संख्यात्मक कॉलम दो दशमलव स्थान और हजारों विभाजक के साथ संख्या दिखाए। प्रत्येक सेल को अलग‑अलग स्टाइल करने के बजाय, हम प्रत्येक कॉलम के लिए एक बार `Style` ऑब्जेक्ट बनाते हैं और इम्पोर्ट के दौरान उसे पुन: उपयोग करते हैं। यह **add number format excel** करने का सबसे कुशल तरीका है।

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

आप फ़ॉर्मेट स्ट्रिंग (`"#,##0.00"`) को अपनी आवश्यकता के अनुसार किसी भी Excel नंबर फ़ॉर्मेट में बदल सकते हैं। तिथियों के लिए, `styles[i].setCustom("mm-dd-yyyy")` आदि का उपयोग करें।

## चरण 4: DataTable को इम्पोर्ट करें और कॉलम स्टाइल लागू करें

अब हम सब कुछ एक साथ लाते हैं। `importDataTable` ओवरलोड हमें `DataTable` पास करने, यह निर्दिष्ट करने देता है कि पहली पंक्ति को कॉलम हेडर माना जाए या नहीं, और स्टाइल एरे प्रदान करता है। यह स्वचालित रूप से संबंधित कॉलम में प्रत्येक सेल के लिए **set number format column** करता है।

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

चूंकि हमने `importColumnNames` फ़्लैग के लिए `true` पास किया है, वर्कशीट की पहली पंक्ति में `DataTable` से कॉलम नाम होते हैं। प्रत्येक अगली पंक्ति डेटा प्राप्त करती है, जो पहले से ही हमने परिभाषित स्टाइल के अनुसार फ़ॉर्मेट किया हुआ है।

## चरण 5: वर्कबुक को xlsx के रूप में सहेजें

अंतिम चरण इन‑मेमोरी वर्कबुक को एक भौतिक फ़ाइल में सहेजना है। Aspose.Cells कई फ़ॉर्मेट्स को सपोर्ट करता है; हम आधुनिक XLSX फ़ॉर्मेट का उपयोग करेंगे, जो आज अधिकांश एप्लिकेशन अपेक्षित करते हैं।

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

`filePath` को अपने सिस्टम पर किसी भी वैध स्थान पर बदल सकते हैं। यदि डायरेक्टरी मौजूद नहीं है या आपके पास लिखने की अनुमति नहीं है तो यह मेथड `IOException` थ्रो करेगा।

## पूर्ण, चलाने योग्य उदाहरण

सभी हिस्सों को एक साथ जोड़ने से एक स्व-निहित प्रोग्राम बनता है जिसे आप तुरंत कम्पाइल और रन कर सकते हैं।

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### अपेक्षित परिणाम

प्रोग्राम चलाने से कार्य निर्देशिका में **DataTableWithNumberFormat.xlsx** नाम की फ़ाइल बनती है। इसे Microsoft Excel, LibreOffice Calc, या किसी भी XLSX‑संगत व्यूअर से खोलें और आप देखेंगे:

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1,234.56 | 2023‑01‑15 |
| 2  | 78,900.00 | 2023‑02‑20 |
| …  | … | … |

***Amount** कॉलम दो दशमलव स्थान और हजारों विभाजक के साथ संख्याएँ दिखाता है, यह सब **add number format excel** स्टाइल के लागू करने के कारण है।*

## सामान्य प्रश्न और किनारे‑केस हैंडलिंग

| प्रश्न | उत्तर |
|----------|--------|
| **यदि मेरा क्वेरी कोई पंक्तियाँ नहीं लौटाता है तो क्या होगा?** | `DataTable` खाली रहेगा लेकिन फिर भी कॉलम परिभाषाएँ रखेगा। वर्कबुक में केवल हेडर पंक्ति होगी, जो अक्सर डाउनस्ट्रीम प्रोसेस के लिए पर्याप्त होती है। |
| **मैं प्रत्येक कॉलम पर अलग-अलग फ़ॉर्मेट कैसे लागू करूँ?** | `buildColumnStyles` को बदलें ताकि वह कॉलम नाम या डेटा टाइप को जांचे और कस्टम फ़ॉर्मेट असाइन करे (जैसे, तिथियाँ, प्रतिशत)। |
| **क्या मैं सीधे `ByteArrayOutputStream` में लिख सकता हूँ?** | हाँ। `workbook.save(filePath, SaveFormat.XLSX);` को इस प्रकार बदलें |

## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells for Java का उपयोग करके Excel वर्कबुक को SVG के रूप में बनाना और सहेजना कैसे करें](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Excel वर्कबुक बनाएं और सहेजें Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel वर्कबुक बनाएं और सहेजें Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}