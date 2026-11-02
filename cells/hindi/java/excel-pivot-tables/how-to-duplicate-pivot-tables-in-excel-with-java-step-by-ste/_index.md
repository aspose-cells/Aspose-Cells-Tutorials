---
category: general
date: 2026-10-07
description: जावा और Aspose.Cells का उपयोग करके एक्सेल में पिवट टेबल को डुप्लिकेट
  करना सीखें। पिवट टेबल को उसके रेंज को वर्कबुक्स के बीच तेज़ी से कॉपी करके कॉपी करें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to duplicate pivot
- copy pivot table
- copy excel range
- copy range between workbooks
- how to copy pivot table
language: hi
lastmod: 2026-10-07
og_description: जावा और Aspose.Cells का उपयोग करके एक्सेल में पिवट टेबल को डुप्लिकेट
  करने का तरीका। इस गाइड का पालन करके पिवट टेबल को उसकी रेंज को वर्कबुक्स के बीच कॉपी
  करके कॉपी करें।
og_image_alt: Illustration of copying an Excel pivot table from one workbook to another
og_title: जावा के साथ एक्सेल में पिवट टेबल्स को डुप्लिकेट कैसे करें – पूर्ण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  headline: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  type: TechArticle
- description: Learn how to duplicate pivot tables in Excel using Java and Aspose.Cells.
    Copy a pivot table by copying its range between workbooks quickly.
  name: How to duplicate pivot tables in Excel with Java – step‑by‑step guide
  steps:
  - name: Explanation of each step
    text: '| Step | What the code does | Why it matters for **copy pivot table** |
      |------|-------------------|----------------------------------------| | **1️⃣
      Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | The
      source file is the only place where the original pivot exists. | | **2️⃣ D'
  - name: 1️⃣ Copying a pivot that spans multiple sheets
    text: 'If the pivot’s source data lives on a different sheet than the pivot itself,
      include both sheets in the copy operation. The simplest approach is to copy
      the entire source sheet first, then copy the pivot sheet:'
  - name: 2️⃣ Dealing with named ranges
    text: 'Aspose.Cells preserves named ranges when you copy a range. However, if
      the destination workbook already contains a name with the same identifier, a
      `CellsException` is thrown. Resolve this by renaming the conflicting name before
      the copy:'
  - name: 3️⃣ Large workbooks and performance
    text: 'Copying very large ranges (hundreds of thousands of rows) can be memory‑intensive.
      Enable **memory optimization**:'
  - name: 4️⃣ Keeping formulas intact
    text: If the source range contains formulas that reference cells outside the copied
      area, those references become broken after the copy. To avoid this, expand the
      range to include all dependent cells, or use `copyRange` with the `CopyOptions`
      flag `CopyOptions.COPY_FORMULA`.
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- PivotTable
- Data manipulation
title: जावा के साथ एक्सेल में पिवट टेबल्स को डुप्लिकेट करने का चरण‑दर‑चरण मार्गदर्शक
url: /hi/java/excel-pivot-tables/how-to-duplicate-pivot-tables-in-excel-with-java-step-by-ste/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में Java के साथ पिवट टेबल्स को डुप्लिकेट कैसे करें – चरण‑दर‑चरण गाइड

यदि आपको Excel वर्कबुक में **पिवट को डुप्लिकेट करने का तरीका** टेबल्स की आवश्यकता है, तो यह ट्यूटोरियल आपको एक पूर्ण, तैयार‑चलाने योग्य समाधान दिखाता है। Aspose.Cells for Java का उपयोग करके आप पिवट टेबल को उसके स्रोत डेटा के साथ नीचे के रेंज को कॉपी करके कॉपी कर सकते हैं, फिर परिणाम को नई वर्कबुक के रूप में सहेज सकते हैं।

पिवट टेबल को डुप्लिकेट करना अक्सर कठिन लगता है क्योंकि पिवट कैश शीट के अंदर छिपा होता है। पिवट को शामिल करने वाले पूरे रेंज को कॉपी करके, Aspose.Cells स्वचालित रूप से लक्ष्य वर्कबुक में कैश को पुनः बनाता है, इसलिए आपको मैन्युअल XML हेरफेर के बिना एक पूरी तरह कार्यशील कॉपी मिलती है।

इस गाइड में आप करेंगे:

* पिवट टेबल वाली स्रोत वर्कबुक लोड करेंगे।  
* पिवट को धारण करने वाले सटीक रेंज को परिभाषित करेंगे।  
* उस रेंज को नई वर्कबुक में कॉपी करेंगे, पिवट परिभाषा को संरक्षित रखते हुए।  
* नई फ़ाइल सहेजेंगे और पिवट के काम करने की पुष्टि करेंगे।  

ये चरण Aspose.Cells द्वारा समर्थित किसी भी Excel संस्करण (2007‑2024) के साथ काम करते हैं और केवल कुछ ही Java पंक्तियों की आवश्यकता होती है।

## आवश्यकताएँ

| Requirement | क्यों महत्वपूर्ण है |
|-------------|-------------------|
| **Java 8 or newer** | Aspose.Cells Java 8+ के लिए बनाया गया है। |
| **Aspose.Cells for Java** (latest version) | उदाहरण में उपयोग किए गए `Workbook`, `Range`, और `CopyRange` APIs प्रदान करता है। |
| **Source workbook** with a pivot table (e.g., `Source.xlsx`) | वह पिवट जिसे आप डुप्लिकेट करना चाहते हैं। |
| **Write permission** to the target directory | `CopyWithPivot.xlsx` को सहेजने के लिए आवश्यक है। |

Add the Aspose.Cells Maven dependency to your `pom.xml` (or download the JAR manually):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>   <!-- use the latest stable version -->
</dependency>
```

## पिवट टेबल्स को डुप्लिकेट करने का तरीका – पूर्ण कार्यान्वयन

Below is a self‑contained Java program that demonstrates **पिवट को डुप्लिकेट करने का तरीका** tables by copying the range that contains the pivot. The code includes error handling, comments, and a verification step.

```java
// File: DuplicatePivot.java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // 1️⃣ Load the source workbook that holds the pivot table.
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // 2️⃣ Identify the range that encloses the pivot table.
        // Adjust the sheet index (0‑based) and address as needed.
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        // Example address "A1:G20" – includes the pivot and its data source.
        String pivotRangeAddress = "A1:G20";
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // 3️⃣ Create a destination workbook and copy the identified range.
        Workbook destWb = new Workbook(); // starts with a blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            // copyRange copies both values and the internal pivot cache.
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // 4️⃣ (Optional) Refresh the pivot so it reflects the copied data.
        // Aspose.Cells automatically rebuilds the cache, but calling refresh
        // guarantees up‑to‑date results if the source data has changed.
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet.getPivotTables().get(i).refresh();
        }

        // 5️⃣ Save the new workbook that now contains the duplicated pivot.
        String destPath = "YOUR_DIRECTORY/CopyWithPivot.xlsx";
        try {
            destWb.save(destPath);
            System.out.println("Pivot table duplicated successfully to: " + destPath);
        } catch (Exception e) {
            System.err.println("Failed to save destination workbook: " + e.getMessage());
        }
    }
}
```

### प्रत्येक चरण की व्याख्या

| Step | कोड क्या करता है | क्यों महत्वपूर्ण है **copy pivot table** के लिए |
|------|-------------------|----------------------------------------|
| **1️⃣ Load source workbook** | `new Workbook(srcPath)` reads `Source.xlsx`. | स्रोत फ़ाइल वह एकमात्र जगह है जहाँ मूल पिवट मौजूद है। |
| **2️⃣ Define the range** | `createRange("A1:G20")` creates a `Range` object that covers the pivot and its data. | पिवट टेबल अपने कैश के साथ संग्रहीत होती है; पूरे रेंज को कॉपी करने से कैश भी स्थानांतरित हो जाता है। |
| **3️⃣ Copy the range** | `copyRange(srcRange, "A1")` writes the range into the destination sheet. | यह **copy range between workbooks** का मुख्य भाग है – API स्वचालित रूप से छिपे हुए ऑब्जेक्ट्स को संभालता है। |
| **4️⃣ Refresh pivot** | `pivotTable.refresh()` forces the pivot to recalculate. | डुप्लिकेट पिवट को मूल के समान मान दिखाने की गारंटी देता है, विशेषकर संशोधनों के बाद। |
| **5️⃣ Save workbook** | `destWb.save(destPath)` writes the file to disk. | अंतिम **copy excel range** परिणाम उत्पन्न करता है जिसे आप Excel में खोल सकते हैं। |

#### अपेक्षित आउटपुट

प्रोग्राम चलाने के बाद, `CopyWithPivot.xlsx` खोलें। आपको एक वर्कशीट दिखेगी जो स्रोत शीट के समान दिखती है, और पिवट टेबल बिल्कुल मूल की तरह काम करती है – आप पंक्तियों का विस्तार कर सकते हैं, फ़ील्ड फ़िल्टर कर सकते हैं, और डेटा को बिना त्रुटियों के रीफ़्रेश कर सकते हैं।

## सामान्य विविधताएँ और किनारे के मामले

### 1️⃣ कई शीट्स में फैले पिवट को कॉपी करना

यदि पिवट का स्रोत डेटा पिवट स्वयं से अलग शीट पर स्थित है, तो कॉपी ऑपरेशन में दोनों शीट्स को शामिल करें। सबसे सरल तरीका है पहले पूरी स्रोत शीट को कॉपी करना, फिर पिवट शीट को कॉपी करना:

```java
// Copy source data sheet
Workbook temp = new Workbook(); // temporary workbook for the data sheet
temp.getWorksheets().addCopy(srcWb.getWorksheets().get(0));
Workbook dest = new Workbook();
dest.getWorksheets().addCopy(temp.getWorksheets().get(0));

// Then copy the pivot sheet as shown earlier
```

### 2️⃣ नामित रेंजेज़ से निपटना

Aspose.Cells रेंज को कॉपी करने पर नामित रेंजेज़ को संरक्षित रखता है। हालांकि, यदि लक्ष्य वर्कबुक में पहले से ही वही पहचानकर्ता वाला नाम मौजूद है, तो `CellsException` फेंका जाता है। कॉपी से पहले टकराव वाले नाम को पुनः नामकरण करके इसे हल करें:

```java
if (destWb.getWorksheets().get(0).getNames().containsKey("MyRange")) {
    destWb.getWorksheets().get(0).getNames().remove("MyRange");
}
```

### 3️⃣ बड़े वर्कबुक और प्रदर्शन

बहुत बड़े रेंजेज़ (सैकड़ों हजारों पंक्तियों) को कॉपी करना मेमोरी‑गहन हो सकता है। **memory optimization** सक्षम करें:

```java
LoadOptions loadOptions = new LoadOptions(LoadFormat.XLSX);
loadOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
Workbook largeSrc = new Workbook(srcPath, loadOptions);
```

### 4️⃣ सूत्रों को अपरिवर्तित रखना

यदि स्रोत रेंज में ऐसे सूत्र हैं जो कॉपी किए गए क्षेत्र के बाहर की कोशिकाओं को संदर्भित करते हैं, तो कॉपी के बाद वे संदर्भ टूट जाते हैं। इसे रोकने के लिए, रेंज को सभी निर्भर कोशिकाओं को शामिल करने के लिए विस्तारित करें, या `copyRange` को `CopyOptions` फ़्लैग `CopyOptions.COPY_FORMULA` के साथ उपयोग करें।

```java
CopyOptions options = new CopyOptions();
options.setCopyFormula(true);
destSheet.getCells().copyRange(srcRange, "A1", options);
```

## विश्वसनीय **copy range between workbooks** के लिए प्रो टिप्स

* **Always use absolute addresses** (`$A$1:$G$20`) when the source sheet may be renamed.  
* **Refresh after copy** – even though Aspose.Cells rebuilds the cache, calling `refresh()` eliminates occasional stale‑cache warnings in Excel.  
* **Validate the pivot**: after saving, open the file programmatically and call `pivotTable.validate()` to ensure no broken references.  
* **Version compatibility**: the code works with Excel 2007‑2024 files (`.xlsx`, `.xlsm`). For legacy `.xls` files, set `LoadOptions.setLoadFormat(LoadFormat.XLS)`.

## पूर्ण स्रोत सूची (कम्पाइल करने के लिए तैयार)

```java
import com.aspose.cells.*;

public class DuplicatePivot {
    public static void main(String[] args) {
        // --------------------------------------------------------------------
        // 1️⃣ Load source workbook
        // --------------------------------------------------------------------
        String srcPath = "YOUR_DIRECTORY/Source.xlsx";
        Workbook srcWb;
        try {
            srcWb = new Workbook(srcPath);
        } catch (Exception e) {
            System.err.println("Failed to load source workbook: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 2️⃣ Define the range that contains the pivot table
        // --------------------------------------------------------------------
        Worksheet srcSheet = srcWb.getWorksheets().get(0);
        String pivotRangeAddress = "A1:G20"; // adjust to your pivot's actual area
        Range srcRange = srcSheet.getCells().createRange(pivotRangeAddress);

        // --------------------------------------------------------------------
        // 3️⃣ Copy the range (including the pivot) to a new workbook
        // --------------------------------------------------------------------
        Workbook destWb = new Workbook(); // blank workbook
        Worksheet destSheet = destWb.getWorksheets().get(0);
        try {
            destSheet.getCells().copyRange(srcRange, "A1");
        } catch (Exception e) {
            System.err.println("Failed to copy range: " + e.getMessage());
            return;
        }

        // --------------------------------------------------------------------
        // 4️⃣ Refresh the duplicated pivot (ensures correct values)
        // --------------------------------------------------------------------
        for (int i = 0; i < destSheet.getPivotTables().getCount(); i++) {
            destSheet


## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकटता से संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण, चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में निपुण होने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Java में पिवट टेबल कॉपी करने का तरीका – पूर्ण Aspose.Cells गाइड](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-complete-aspose-cells-guide/)
- [Java के लिए Aspose.Cells का उपयोग करके Excel में पिवट टेबल बनाना: एक व्यापक गाइड](/cells/english/java/data-analysis/create-pivot-tables-excel-aspose-cells-java/)
- [Java के लिए Aspose.Cells के साथ Excel पिवट टेबल स्रोत को अपडेट करना: एक व्यापक गाइड](/cells/english/java/data-analysis/update-excel-pivot-table-source-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}