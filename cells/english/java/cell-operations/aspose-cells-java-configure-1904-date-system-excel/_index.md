---
title: "Change Excel date system to 1904 with Aspose.Cells Java"
description: "Learn how to change Excel date system to 1904 using Aspose.Cells for Java, set Excel date format, and convert Excel 1904 system efficiently."
date: "2026-02-22"
weight: 1
url: "/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/"
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Change Excel date system to 1904 with Aspose.Cells Java

Managing historical data in Excel can be challenging because Excel supports two different date systems. **In this tutorial you'll learn how to change Excel date system to the 1904 format using Aspose.Cells for Java**, which makes handling legacy dates painless. We'll walk through initializing a workbook, enabling the 1904 date system, and persisting the change.

## Quick Answers
- **What does the 1904 date system do?** It starts counting days from January 1, 1904, shifting all dates by 1462 days compared with the default 1900 system.  
- **Why use Aspose.Cells to change the date system?** It provides a simple API that works without Excel installed and supports large files.  
- **Which Java versions are supported?** JDK 8 or newer.  
- **Do I need a license?** A free trial works for evaluation; a license removes usage limits.  
- **Can I convert back to the 1900 system later?** Yes, just set `setDate1904(false)`.

## What is the 1904 date system in Excel?
The 1904 date system was originally used by early Macintosh versions of Excel. It counts days from January 1, 1904, which is useful for compatibility with older spreadsheets and some financial models.

## Why change Excel date system with Aspose.Cells?
- **Cross‑platform compatibility** – works on Windows, Linux, and macOS.  
- **No Excel installation required** – ideal for server‑side processing.  
- **High performance** – handles large workbooks with minimal memory overhead.  

## Prerequisites
- Java Development Kit (JDK) 8 or higher.  
- Maven or Gradle for dependency management.  
- Basic Java programming knowledge.  

## Setting Up Aspose.Cells for Java

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

#### License Acquisition
Aspose offers a free trial, temporary license, and full commercial licenses. You can start with the [free trial](https://releases.aspose.com/cells/java/) or obtain a temporary license from the [temporary license page](https://purchase.aspose.com/temporary-license/).

## Change Excel date system using Aspose.Cells Java

Below is the step‑by‑step guide that actually **changes the Excel date system**. Each step includes a short explanation followed by the exact code you need.

### Step 1: Initialize and load the workbook
First, create a `Workbook` instance that points to your existing Excel file.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Step 2: Enable the 1904 date system
Use the workbook settings to switch the date system.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Pro tip:** You can also call `setDate1904(false)` later if you need to revert.

### Step 3: Save the modified workbook
Finally, write the changes to a new file (or overwrite the original).

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
If you need to adjust individual cell values after changing the system, you can use `Cells.get(i, j).putValue(Date)` where the date will be interpreted according to the active date system.

## Convert Excel 1904 system back to 1900 (secondary keyword)
To revert, simply call:

```java
workbook.getSettings().setDate1904(false);
```

Then save the workbook again.

## Practical Applications
1. **Data Archiving** – Preserve legacy timestamps when migrating old Mac‑based spreadsheets.  
2. **Cross‑Platform Reporting** – Generate reports that can be opened on both Windows and macOS without date mismatches.  
3. **Financial Modeling** – Align date calculations with legacy financial models that expect the 1904 system.

## Performance Considerations
- Limit workbook operations in a single session to keep memory usage low.  
- Use Java’s garbage‑collection tuning for very large files.  

## Frequently Asked Questions

**Q: What is the difference between the 1900 and 1904 date systems?**  
A: The 1900 system starts on January 1, 1900, while the 1904 system starts on January 1, 1904, shifting all dates by 1462 days.

**Q: Can I change the date system of a workbook that is currently open in Excel?**  
A: Yes, but you must close the file in Excel first; otherwise the save operation will fail.

**Q: Do I need a license to use `setDate1904`?**  
A: The method works in the free trial, but a full license removes evaluation limitations.

**Q: Is it possible to change the date system for only a single worksheet?**  
A: No, the date system is a workbook‑level setting; it applies to all worksheets.

**Q: How can I verify that the date system was changed?**  
A: Open the saved file in Excel, go to **File → Options → Advanced**, and check the **"Use 1904 date system"** box.

## Conclusion
You now know how to **change Excel date system** to 1904 using Aspose.Cells for Java, how to set Excel date formats, and how to convert back if needed. Incorporate these snippets into your data‑processing pipelines to guarantee date‑compatibility across platforms.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

**Resources**
- **Documentation:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Download:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Purchase License:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Free Trial:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Temporary License:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Support Forum:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}