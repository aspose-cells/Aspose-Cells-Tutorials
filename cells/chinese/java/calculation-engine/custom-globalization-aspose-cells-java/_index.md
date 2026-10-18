---
date: '2026-08-16'
description: 了解如何在 Java 中使用 Aspose.Cells 添加全球化、自定义 Excel 错误消息以及设置 Maven 依赖。
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: 了解如何在 Java 中使用 Aspose.Cells 添加全球化、自定义 Excel 错误消息以及设置 Maven 依赖。请按照分步指南操作。
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: 如何在 Java 中使用 Aspose.Cells 添加全球化
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: 如何在 Java 中使用 Aspose.Cells 添加全球化
url: /zh/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 Java 中使用 Aspose.Cells 添加全球化

## 简介

将全球化添加到您的 Java 工作簿，可让您以用户期望的语言显示错误信息、布尔值以及其他特定地区的字符串。在本教程中，您将学习**如何添加全球化**为俄语，但相同的模式适用于任何语言。完成本指南后，您将能够：

- 覆盖默认错误文本和布尔值表示。
- 将自定义设置应用于任何 `Workbook` 实例。
- 将解决方案集成到典型的基于 Maven 的 Java 项目中。

准备好让您的 Excel 文件真正实现多语言吗？让我们先确认您的开发环境满足前提条件。

## 快速答案

- **什么是 Aspose.Cells 中的全球化？** 它是一组区域感知的字符串（错误、布尔值等），您可以用自定义文本替换。  
- **需要哪个 Maven 构件？** `com.aspose:aspose-cells:25.3`。  
- **我可以针对除俄语之外的语言吗？** 可以——扩展 `GlobalizationSettings` 并覆盖每个地区所需的方法。  
- **开发是否需要许可证？** 免费试用可用于测试；永久许可证可去除评估水印。  
- **该解决方案是线程安全的吗？** 对每个工作簿应用设置；`GlobalizationSettings` 对象在创建后是不可变的。

## Aspose.Cells 中的全球化是什么？

`GlobalizationSettings` 是 Aspose.Cells 的配置对象，用于控制区域特定的字符串，如错误信息、布尔值、货币符号和日期模式。通过提供自己的子类，您可以告诉库在每种文化下显示哪些文本，从而用匹配终端用户语言和地区惯例的翻译替换默认的英文字符串。

## 为什么添加自定义全球化？

Aspose.Cells 支持 **50 多种输入和输出格式**——包括 XLSX、CSV、PDF 和 ODS——并且能够在不将整个文件加载到内存的情况下处理 **多达 200 000 行** 的工作簿。自定义全球化可确保终端用户以母语看到信息，预计可为跨国部署减少约 **30 %** 的支持工单。

## 前提条件

- **Java Development Kit** 8 或更高版本。
- **IDE** 如 IntelliJ IDEA 或 Eclipse。
- **Aspose.Cells for Java** 版本 25.3（或更高），通过 Maven 或 Gradle 添加。

### 设置 Aspose.Cells for Java

在您的 `pom.xml` 中添加 Maven 依赖：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

或者，如果您更喜欢 Gradle，请将以下内容插入 `build.gradle`：

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 获取许可证

Aspose 提供多种授权选项：

- **免费试用** – 30 天完整功能评估。  
- **临时许可证** – 无限评估且无水印。  
- **商业许可证** – 生产就绪，提供优先支持。

获取许可证文件后，在应用程序启动时设置一次：

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## 如何为俄语添加全球化？

`Workbook` 对象表示加载到内存中的 Excel 文件，提供对其工作表、单元格和设置的访问。加载工作簿，创建 `GlobalizationSettings` 的子类，并将其附加到工作簿。直接答案是：**实例化自定义的 `GlobalizationSettings` 类，覆盖 `getErrorValueString` 和 `getBooleanValueString`，然后调用 `workbook.setGlobalizationSettings(customSettings)`**。这种两步方法将默认的俄语字符串替换为您自己的。

### 定义自定义设置

在本指南中首次引用 `GlobalizationSettings` 时，请注意其定义：

`GlobalizationSettings` 是 Aspose.Cells 用于检索区域特定字符串的基类。

现在创建一个返回俄语特定文本的子类：

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### 将设置应用于工作簿

定义子类后，将其附加到任何 `Workbook` 实例：

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## 实际应用

- **财务报告** – 以会计人员的母语显示错误代码，减少误解。  
- **全企业工具** – 在数十个内部基于 Excel 的实用程序中嵌入相同的全球化逻辑。  
- **自动化数据管道** – 确保下游系统接收带有区域感知的值，无需额外翻译步骤。

## 性能考虑

启用自定义全球化后，Aspose.Cells 仍以相同的高性能处理公式和 I/O。为保持低内存使用：

- 在保存后释放工作簿引用（`wb.dispose()`）。  
- 仅在必要时使用 `CalculationOptions.setEnableIterativeCalculation(true)`。  
- 为大于 100 MB 的工作簿调优 JVM 堆（`-Xmx2g`）。

## 常见问题

**问：我可以一次将相同的全球化设置应用于多个工作簿吗？**  
答：可以。创建一个 `RussianGlobalization` 实例，并通过 `setGlobalizationSettings` 将其传递给每个工作簿。

**问：如果需要支持使用从右到左书写的语言怎么办？**  
答：在子类中覆盖额外的方法，如 `getCurrencySymbol` 和 `getDatePattern`，返回适当的 RTL 符号。

**问：试用版使用自定义全球化是否需要许可证？**  
答：不需要。试用版完全支持 `GlobalizationSettings`；仅在某些输出格式上出现评估水印。

**问：如何调试错误的错误字符串？**  
答：在覆盖的方法内部插入 `System.out.println` 语句，以验证输入的 `err` 值是否匹配您的 switch case。

**问：这会影响公式计算速度吗？**  
答：几乎没有影响。库仅在渲染单元格值时查找字符串，而不是在中间计算步骤中。

## 其他资源

- **文档**：在 [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/) 查看详细指南  
- **下载**：在 [Aspose Downloads](https://releases.aspose.com/cells/java/) 获取最新发布  
- **购买**：在 [Aspose Purchase](https://purchase.aspose.com/buy) 购买商业许可证  
- **免费试用**：从 [Aspose Free Trial](https://releases.aspose.com/cells/java/) 开始免费试用  
- **临时许可证**：通过 [Aspose Temporary License](https://purchase.aspose.com/temporary-license/) 获取临时许可证  
- **支持**：在 [Aspose Support Forum](https://forum.aspose.com/c/cells/9) 获取社区帮助

---

**最后更新：** 2026-08-16  
**测试环境：** Aspose.Cells 25.3 for Java  
**作者：** Aspose

## 相关教程

- [Aspose.Cells Java：自定义计算引擎指南](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [如何使用 Aspose Cells – Java Excel 引擎教程](/cells/java/calculation-engine/)
- [Aspose Cells Maven 依赖 – 在 Java 中使用 Aspose.Cells 管理 Excel 数据连接](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}