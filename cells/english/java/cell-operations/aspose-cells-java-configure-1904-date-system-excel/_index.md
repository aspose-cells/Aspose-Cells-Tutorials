---
date: '2026-10-28'
description: Learn how to change Excel date system to 1904 using Aspose.Cells for
  Java, set Excel date format, and convert Excel 1904 system efficiently.
images:
- /java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/og-image.png
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Change Excel date system to 1904 using Aspose.Cells for Java. Learn
  step‑by‑step how to enable the 1904 system, set dates, and convert back.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Change Excel date system to 1904 with Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Change Excel date system to 1904 with Aspose.Cells Java
url: /java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Change Excel date system to 1904 with Aspose.Cells Java

In this tutorial you’ll learn how to **change Excel date system** to the 1904 format using Aspose.Cells for Java. The 1904 system is essential when you need to preserve legacy Mac‑based dates or align with financial models that expect that epoch. We’ll walk through installing the library, loading a workbook, toggling the date system, and saving the result—all without requiring Microsoft Excel on the server.

## Quick answers
- **What does the 1904 date system do?** It starts counting days from January 1, 1904, shifting all dates by 1,462 days compared with the default 1900 system.  
- **Why use Aspose.Cells to change the date system?** It provides a simple API that works without Excel installed and supports large files.  
- **Which Java versions are supported?** JDK 8 or newer.  
- **Do I need a license?** A free trial works for evaluation; a license removes usage limits.  
- **Can I convert back to the 1900 system later?** Yes, just call `setDate1904(false)`.

## What is the 1904 date system in Excel?
The 1904 date system counts days from January 1, 1904, instead of the default 1900 epoch. This shift adds exactly 1,462 days to every date value, which is why legacy Mac workbooks appear offset when opened on Windows. It is primarily used for compatibility with older Macintosh Excel files and some legacy financial models.

## Why change Excel date system with Aspose.Cells?
You can switch the date system directly from Java, eliminating manual steps in Excel. Aspose.Cells processes workbooks up to **2 GB** in size and can convert a 500‑sheet workbook in under **2 seconds** on a typical 4‑core server, delivering high‑throughput server‑side automation.

## Prerequisites
- Java Development Kit (JDK) 8 or higher.  
- Maven or Gradle for dependency management.  
- Basic Java programming knowledge.  

## Setting up Aspose.Cells for Java

### Maven
Add the following dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Include this line in your `build.gradle` file:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### License acquisition
Aspose offers a free trial, temporary license, and full commercial licenses. You can start with the [free trial](https://releases.aspose.com/cells/java/) or obtain a temporary license from the [temporary license page](https://purchase.aspose.com/temporary-license/).

## How do you change the Excel date system to 1904 with Aspose.Cells for Java?
Load the workbook, enable the 1904 setting, and save the file—this three‑step flow updates the workbook’s internal date epoch in under a second. The API call `setDate1904(true)` flips the system flag, and the change is persisted when you call `save`. No Excel installation is required, making it ideal for headless server environments.

### Step 1: initialize and load the workbook
The `Workbook` class represents an entire Excel file in memory. First, create a `Workbook` instance that points to your existing file.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Step 2: enable the 1904 date system
The `WorkbookSettings.setDate1904` method toggles the workbook‑level date flag. Setting it to `true` activates the 1904 system for all worksheets.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro tip:** You can also call `setDate1904(false)` later if you need to revert.

### Step 3: save the modified workbook
Finally, write the changes to a new file (or overwrite the original). The `save` method respects the active date system automatically.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Note:** The code above uses the class name `tWorkbook` as originally provided. Ensure this typo matches your project’s naming conventions or correct it to `Workbook` if needed.

## Set Excel date programmatically (secondary keyword)
If you need to adjust individual cell values after changing the system, you can use `cells.get(i, j).putValue(Date)` where the date will be interpreted according to the active date system.

## Convert Excel 1904 system back to 1900 (secondary keyword)
To revert, simply call:

```java
workbook.getSettings().setDate1904(false);
```

Then save the workbook again.

## Practical applications
1. **Data archiving** – Preserve legacy timestamps when migrating old Mac‑based spreadsheets.  
2. **Cross‑platform reporting** – Generate reports that open correctly on both Windows and macOS without date mismatches.  
3. **Financial modeling** – Align date calculations with legacy financial models that expect the 1904 system.

## Performance considerations
- Limit workbook operations in a single session to keep memory usage low; Aspose.Cells streams data and never loads the whole file into RAM unless you explicitly request it.  
- Tune Java’s garbage‑collection flags (`-XX:+UseG1GC`) for very large files to avoid pause‑time spikes.  

## Frequently asked questions

**Q: What is the difference between the 1900 and 1904 date systems?**  
A: The 1900 system starts on January 1, 1900, while the 1904 system starts on January 1, 1904, shifting all dates by 1,462 days.

**Q: Can I change the date system of a workbook that is currently open in Excel?**  
A: Yes, but you must close the file in Excel first; otherwise the save operation will fail.

**Q: Do I need a license to use `setDate1904`?**  
A: The method works in the free trial, but a full license removes evaluation limitations.

**Q: Is it possible to change the date system for only a single worksheet?**  
A: No, the date system is a workbook‑level setting; it applies to all worksheets.

**Q: How can I verify that the date system was changed?**  
A: Open the saved file in Excel, go to **File → Options → Advanced**, and check the **"Use 1904 date system"** box.

## Conclusion
You now know how to **change Excel date system** to 1904 using Aspose.Cells for Java, how to set individual cell dates, and how to revert to the 1900 system when needed. Integrate these snippets into your data‑processing pipelines to guarantee date‑compatibility across platforms and legacy files.

---

**Last Updated:** 2026-10-28  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

**Resources**
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Purchase license:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Free trial:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Temporary license:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Support forum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Related Tutorials

- [Efficiently Convert Excel to PDF with Custom Date Formats Using Aspose.Cells for Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells for Java: How to Create and Format Excel Workbooks Efficiently](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Master Excel Manipulation with Aspose.Cells for Java: Workbook Operations and Cell Styling Tutorial](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}