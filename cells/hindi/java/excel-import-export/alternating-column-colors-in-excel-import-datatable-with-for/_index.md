---
category: general
date: 2026-06-27
description: डेटा टेबल को एक्सेल में वैकल्पिक कॉलम रंगों के साथ इम्पोर्ट करना सीखें।
  फॉर्मेटिंग के साथ डेटा इम्पोर्ट करने और जावा का उपयोग करके कॉलम फ़ॉन्ट रंग सेट करने
  की चरण‑दर‑चरण गाइड।
draft: false
keywords:
- alternating column colors
- import data with formatting
- import datatable to excel
- set column font color
- how to import datatable
language: hi
og_description: डेटा टेबल को एक्सेल में इम्पोर्ट करते समय वैकल्पिक कॉलम रंगों में
  महारत हासिल करें। यह गाइड दिखाता है कि फॉर्मेटिंग के साथ डेटा कैसे इम्पोर्ट करें
  और जावा में कॉलम फ़ॉन्ट रंग कैसे सेट करें।
og_title: एक्सेल में वैकल्पिक कॉलम रंग – फ़ॉर्मेटिंग के साथ डेटा टेबल आयात
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  headline: Alternating Column Colors in Excel – Import DataTable with Formatting
  type: TechArticle
- description: Learn how to import DataTable to Excel with alternating column colors.
    Step‑by‑step guide on import data with formatting and set column font color using
    Java.
  name: Alternating Column Colors in Excel – Import DataTable with Formatting
  steps:
  - name: Prerequisites
    text: '- Java 8+ (the code works with newer releases as well). - Apache POI 5.x
      on your classpath – the library that talks to Excel files. - A `DataTable` implementation
      that offers `getColumns()` and `size()` (or adapt the example to a `ResultSet`).'
  - name: – Obtain the DataTable You Want to Export
    text: First, you need a source of rows and columns. In real projects this might
      be a database query, a CSV parser, or an in‑memory collection. The example assumes
      a helper method `getDataTable()` that returns a ready‑to‑use `DataTable`.
  - name: – Prepare a Style for Each Column
    text: We create a `Style[]` whose length matches the number of columns. Each entry
      will hold a font color that alternates between blue and green.
  - name: – Create Styles with Alternating Font Colors
    text: 'Now the fun part: loop through the array and assign a blue font to even‑indexed
      columns and a green font to odd‑indexed ones. This is where **alternating column
      colors** is implemented.'
  - name: – Import the DataTable with the Style Array
    text: Finally, we hand the `DataTable` and the `columnStyles` array to POI’s `importDataTable`
      method. The `true` flag tells POI to treat the first row as column headers.
  - name: – Save the Workbook (Optional but Recommended)
    text: After the import, you’ll probably want to write the workbook to disk or
      stream it to a client.
  type: HowTo
- questions:
  - answer: Replace `setFontColor` with `setPatternForegroundColor` and call `setPattern(BackgroundType.SOLID)`
      on the style.
    question: What if I need background colors instead of font colors?
  - answer: 'Absolutely—just swap the loop logic: iterate over rows and assign a style
      per row index.'
    question: Can I apply the same color scheme to rows instead of columns?
  - answer: Excel caps at 16,384 columns (XFD). The code will throw an exception once
      you exceed that limit. Guard against it by checking `columnCount` against `SpreadsheetVersion.EXCEL2007.getMaxColumns()`.
    question: What if the DataTable has more columns than the worksheet can handle?
  - answer: Yes, POI abstracts the format. However, the older binary format supports
      fewer colors, so you might see a fallback to the nearest palette entry.
    question: Does this work with .xls (Excel 97‑2003) files?
  type: FAQPage
tags:
- excel
- java
- datatable
- formatting
- apache-poi
title: एक्सेल में वैकल्पिक कॉलम रंग – फ़ॉर्मेटिंग के साथ डेटा टेबल आयात
url: /hi/java/excel-import-export/alternating-column-colors-in-excel-import-datatable-with-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में वैकल्पिक कॉलम रंग – फ़ॉर्मेटिंग के साथ DataTable आयात करें

क्या आपने कभी सोचा है कि कोड से बाहर निकले बिना अपने Excel निर्यात को दृश्य रूप से आकर्षक कैसे बनाएं? **Alternating column colors** बड़े तालिकाओं को पढ़ने योग्य बनाने का एक तेज़ तरीका है, और आप इसे **import datatable to excel** करते समय कर सकते हैं। इस ट्यूटोरियल में हम एक पूर्ण Java समाधान के माध्यम से चलेंगे जो न केवल आपके डेटा को एक वर्कशीट में लाता है बल्कि प्रत्येक कॉलम पर नीले‑हरे फ़ॉन्ट पैटर्न को भी लागू करता है।

## आप क्या बनाएँगे

इस गाइड के अंत तक आपके पास एक चलाने योग्य Java स्निपेट होगा जो:

1. `DataTable` (या किसी भी `ResultSet`‑जैसे संग्रह) को प्राप्त करता है।  
2. एक `Style` एरे बनाता है जहाँ सम कॉलम नीले और विषम कॉलम हरे होते हैं।  
3. `importDataTable` को कॉल करता है ताकि डेटा को सेल **A1** में डालते समय शैलियों को लागू किया जा सके।  

यह सब कुछ कुछ लाइनों में हो जाता है, फिर भी परिणाम एक हाथ से तैयार रिपोर्ट जैसा दिखता है।

### पूर्वापेक्षाएँ

- Java 8+ (कोड नए रिलीज़ के साथ भी काम करता है)।  
- आपके क्लासपाथ पर Apache POI 5.x – वह लाइब्रेरी जो Excel फ़ाइलों से बात करती है।  
- `DataTable` कार्यान्वयन जो `getColumns()` और `size()` प्रदान करता है (या उदाहरण को `ResultSet` के अनुसार अनुकूलित करें)।  

यदि आप पहले से ही अन्य Excel कार्यों के लिए POI का उपयोग कर रहे हैं, तो आप इसे सीधे उपयोग कर सकते हैं।  

---

## Excel में DataTable आयात करते समय वैकल्पिक कॉलम रंग

समाधान का मूल चार संक्षिप्त चरणों में निहित है। आइए इन्हें विभाजित करें।

### चरण 1 – वह DataTable प्राप्त करें जिसे आप निर्यात करना चाहते हैं

सबसे पहले, आपको पंक्तियों और कॉलमों का स्रोत चाहिए। वास्तविक प्रोजेक्ट्स में यह एक डेटाबेस क्वेरी, CSV पार्सर, या मेमोरी में संग्रह हो सकता है। उदाहरण मानता है कि एक हेल्पर मेथड `getDataTable()` एक तैयार‑उपयोग `DataTable` लौटाता है।

```java
// Step 1: Obtain the data to be imported
DataTable dataTable = getDataTable();   // your own method that fills the table
```

> **यह क्यों महत्वपूर्ण है:**  
> डेटा पहले प्राप्त करने से आप कॉलम गिनती देख सकते हैं, जो बाद में शैली एरे के आकार को निर्धारित करता है। यह यह भी सुनिश्चित करता है कि आयात चरण के पास काम करने के लिए एक ठोस ऑब्जेक्ट हो।

### चरण 2 – प्रत्येक कॉलम के लिए एक Style तैयार करें

हम एक `Style[]` बनाते हैं जिसकी लंबाई कॉलमों की संख्या के बराबर होती है। प्रत्येक प्रविष्टि में एक फ़ॉन्ट रंग होगा जो नीले और हरे के बीच बदलता रहेगा।

```java
// Step 2: Prepare a style for each column (same count as the number of columns)
int columnCount = dataTable.getColumns().size();
Style[] columnStyles = new Style[columnCount];
```

> **प्रो टिप:** यदि आपका `DataTable` रनटाइम पर आकार बदल सकता है, तो प्रत्येक निर्यात पर `columnCount` को पुनः गणना करें। इससे `ArrayIndexOutOfBoundsException` से बचा जा सकता है।

### चरण 3 – वैकल्पिक फ़ॉन्ट रंगों के साथ शैलियाँ बनाएं

अब मज़ेदार भाग: एरे पर लूप करें और सम‑इंडेक्स वाले कॉलमों को नीला फ़ॉन्ट और विषम‑इंडेक्स वाले कॉलमों को हरा फ़ॉन्ट असाइन करें। यही वह जगह है जहाँ **alternating column colors** लागू किया जाता है।

```java
// Step 3: Create styles with alternating font colors for visual distinction
for (int i = 0; i < columnStyles.length; i++) {
    columnStyles[i] = workbook.createStyle();               // create a fresh style
    // Even columns → blue, odd columns → green
    columnStyles[i].setFontColor(
        (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
    );
}
```

> **वैकल्पिक रंग क्यों?**  
> जब पास के कॉलम अलग दिखते हैं तो मानव आँखें पंक्तियों को अधिक आसानी से स्कैन करती हैं। नीला‑हरा लय दृश्य थकान को कम करती है, विशेष रूप से विस्तृत तालिकाओं में।

### चरण 4 – Style एरे के साथ DataTable आयात करें

अंत में, हम `DataTable` और `columnStyles` एरे को POI की `importDataTable` मेथड को देते हैं। `true` फ़्लैग POI को बताता है कि पहली पंक्ति को कॉलम हेडर मानें।

```java
// Step 4: Import the data table into the worksheet starting at cell A1, applying the styles
worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);
```

> **आंतरिक रूप से क्या होता है?**  
> POI प्रत्येक कॉलम पर इटररेट करता है, एरे से मिलते‑जुलते `Style` को लेता है, और प्रत्येक सेल को उस शैली के साथ लिखता है। क्योंकि हमने केवल फ़ॉन्ट रंग सेट किया है, अन्य पहलू (बॉर्डर, बैकग्राउंड) डिफ़ॉल्ट रहते हैं—यदि आपको अधिक सजावट चाहिए तो शैली को विस्तारित करने में संकोच न करें।

### चरण 5 – वर्कबुक सहेजें (वैकल्पिक लेकिन अनुशंसित)

आयात के बाद, आप संभवतः वर्कबुक को डिस्क पर लिखना या क्लाइंट को स्ट्रीम करना चाहेंगे।

```java
// Optional: write the workbook to a file
try (FileOutputStream fos = new FileOutputStream("ExportedReport.xlsx")) {
    workbook.save(fos);
}
```

> **एज केस:** यदि लक्ष्य फ़ाइल पहले से मौजूद है, तो `FileOutputStream` उसे ओवरराइट कर देगा। कॉल को एक जाँच में लपेटें या UI संदर्भ में उपयोगकर्ता से पुष्टि पूछें।

---

## सामान्य प्रश्न और समस्याएँ

- **यदि मुझे फ़ॉन्ट रंगों के बजाय बैकग्राउंड रंग चाहिए तो?**  
  `setFontColor` को `setPatternForegroundColor` से बदलें और शैली पर `setPattern(BackgroundType.SOLID)` कॉल करें।

- **क्या मैं वही रंग योजना कॉलम के बजाय पंक्तियों पर लागू कर सकता हूँ?**  
  बिल्कुल—सिर्फ लूप लॉजिक बदलें: पंक्तियों पर इटररेट करें और प्रत्येक पंक्ति इंडेक्स के लिए एक शैली असाइन करें।

- **यदि DataTable में वर्कशीट से अधिक कॉलम हों तो?**  
  Excel अधिकतम 16,384 कॉलम (XFD) तक सीमित है। इस सीमा से अधिक होने पर कोड एक अपवाद फेंकेगा। `columnCount` को `SpreadsheetVersion.EXCEL2007.getMaxColumns()` के विरुद्ध जाँच कर इसे रोकें।

- **क्या यह .xls (Excel 97‑2003) फ़ाइलों के साथ काम करता है?**  
  हाँ, POI फ़ॉर्मेट को एब्स्ट्रैक्ट करता है। हालांकि, पुराने बाइनरी फ़ॉर्मेट में कम रंग होते हैं, इसलिए आप निकटतम पैलेट एंट्री पर फॉलबैक देख सकते हैं।

## पूर्ण कार्यशील उदाहरण

नीचे एक स्व-निहित क्लास है जिसे आप एक Maven प्रोजेक्ट में पेस्ट कर सकते हैं जिसमें पहले से `org.apache.poi:poi-ooxml:5.2.3` शामिल है। `getDataTable()` को अपने वास्तविक डेटा स्रोत को लौटाने के लिए समायोजित करें।

```java
import com.aspose.cells.*;
import java.io.FileOutputStream;

public class ExcelAlternatingColorsExport {

    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 1️⃣ Obtain the data to be imported
        DataTable dataTable = getDataTable(); // implement this method

        // 2️⃣ Prepare a style for each column
        int columnCount = dataTable.getColumns().size();
        Style[] columnStyles = new Style[columnCount];

        // 3️⃣ Create alternating font colors (blue for even, green for odd)
        for (int i = 0; i < columnStyles.length; i++) {
            columnStyles[i] = workbook.createStyle();
            columnStyles[i].setFontColor(
                (i % 2 == 0) ? Color.getBlue() : Color.getGreen()
            );
        }

        // 4️⃣ Import the data with formatting
        worksheet.getCells().importDataTable(dataTable, true, "A1", columnStyles);

        // 5️⃣ Save the file
        try (FileOutputStream fos = new FileOutputStream("AlternatingColorsReport.xlsx")) {
            workbook.save(fos);
        }

        System.out.println("Export complete – open AlternatingColorsReport.xlsx to see the result.");
    }

    // Dummy implementation – replace with real data retrieval
    private static DataTable getDataTable() {
        DataTable dt = new DataTable();
        dt.getColumns().add("ID");
        dt.getColumns().add("Name");
        dt.getColumns().add("Score");
        dt.getRows().add(new DataRow(new Object[]{1, "Alice", 85}));
        dt.getRows().add(new DataRow(new Object[]{2, "Bob", 92}));
        dt.getRows().add(new DataRow(new Object[]{3, "Carol", 78}));
        return dt;
    }
}
```

**अपेक्षित आउटपुट:** `AlternatingColorsReport.xlsx` खोलें। कॉलम A और C (सम इंडेक्स) अपना टेक्स्ट नीले रंग में दिखाते हैं, जबकि कॉलम B (विषम इंडेक्स) हरे फ़ॉन्ट में दिखाता है। पहली पंक्ति हेडर के रूप में बोल्ड है क्योंकि `importDataTable` इसे ऐसा मानता है।

## निष्कर्ष

हमने अभी वह सब कवर किया है जो आपको प्रोग्रामेटिक रूप से **import datatable to excel** करते समय **alternating column colors** और **set column font color** लागू करने के लिए चाहिए। यह तरीका हल्का है, केवल Apache POI पर निर्भर करता है, और बॉर्डर या सेल बैकग्राउंड जैसे अन्य स्टाइलिंग आवश्यकताओं के लिए विस्तारित किया जा सकता है।

अगला, प्रयोग करने पर विचार करें:

- **Import data with formatting** पंक्तियों के लिए (वैकल्पिक पंक्ति रंग)।  
- उच्च स्कोर को हाइलाइट करने के लिए **conditional formatting** जोड़ना।  
- वेब ऐप्स के लिए सीधे HTTP प्रतिक्रिया में निर्यात करना।

अपने रिपोर्टिंग पाइपलाइन में इस पैटर्न को अनुकूलित करने में संकोच न करें—एक बार जब आप बुनियादों में निपुण हो जाएँ, तो संभावनाएँ असीमित हैं। कोडिंग का आनंद लें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [How to Sort Excel Data by Column Color Using Aspose.Cells Java: A Complete Guide](/cells/english/java/formatting/sort-excel-data-by-column-color-aspose-cells-java/)
- [Master Excel Column Protection Using Aspose.Cells for Java: A Comprehensive Guide](/cells/english/java/security-protection/excel-column-protection-aspose-cells-java/)
- [How to Insert a Column in Excel Using Aspose.Cells for Java - A Comprehensive Guide](/cells/english/java/worksheet-management/aspose-cells-java-insert-column-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}