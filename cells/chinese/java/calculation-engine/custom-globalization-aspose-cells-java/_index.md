---
date: '2026-02-01'
description: 了解如何在 Java 中使用 Aspose.Cells 设置 Aspose 许可证、覆盖 Excel 错误文本以及自定义错误消息和布尔值。
keywords:
- custom globalization aspose cells java
- localization with aspose.cells
- java internationalization aspose.cells
title: 在 Java 中使用 Aspose.Cells 自定义错误消息：实现全球化
url: /zh/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/products-backtop-button >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/main-wrap-class >}}

# 在 Java 中使用 Aspose.Cells 实现自定义错误消息

## 介绍

当您为全球布尔值变得至关重要局化**文本**，甚至 **设置 Aspose 许可证**，使工作簿显示正确的语言特定信息——这里以俄语为实际示例。

阅读完本指南后，这些设置无缝应用到工作簿开始了吗？让我们先速回答
- **主要目的是什么？** 在 Excel 工作簿中自定义错误消息和布尔值。  
- **需要哪个库？** Aspose.Cells for Java（最新版本）。  
- **需要许可证吗？** 是的，生产环境应 **设置 Aspose 许可证**。  
- **可以针对其他语言吗？** 当然——只需为每个语言在 30 分钟以内完成。

## 前置条件

要在 Java 中使用 Asp：

- **Java 开发环境**：JDK  **IDE**：IntelliJ IDEA、Eclipse 或任意 Java 兼容编辑器。  
- **Aspose.Cells 库**：版本 25.3（或更新） via Maven将库添加到项目中。

**Maven**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 许可证获取

Aspose 提供多种授权选项：

- **免费试用** – 在没有许可证密钥的合大量测试。  
- **正式购买需品。

下面是一段最小的 Java 示例，**设置 Aspose 许可证** 并创建工作簿实例。

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

## 什么是 Aspose.Cells 中的自换默认的 Excel 消息（例如 `#DIV/0!`、`#NAME?`TRUE`、`FALSE`）。这就是 **覆盖 Excel 错误文本** 并消息？

- **提升终端用户的可读性** – 用户看到自己语言的提示。  
- **符合法规要求**使 Excel 输出与应用 UI 语言保持统一。

## 实施指南

### 功能 1：俄语全局化

本示例展示如何为俄语创建自定义全局化类。

#### 自定义错误消息

创建 `GlobalizationSettings` 的子类，返回俄语特定的字符串。

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

**说明**

- `getErrorValueString` 拦截 Excel 错 `getBooleanValueString` 将 `TRUE`/`FALSE` 替换为俄语重新计算公式并保存结果。

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

### 实际应用场景

- **财务报告** – 为跨国财务团队提供本地化错误处理。  
- 以用户母语显示布尔结果。  
- **自动化数据管道** –

- 及时释放工作簿对象以释放内存。  
- 仅在必要时使用 `Workbook.calculateFormula()`。  
- 为大工作簿调优 JVM因 | 解决方案 |
|------|------|----------|
| 许可证未被识别 | 路径错误或缺少文件 | 核实 `.lic` 文件位置并使用绝对路径。 |
| 错误未被翻译之前** 设置全局化。 |
| 内存激增 | 未Options` 并调用 `set 常见问答

**问：如何为除俄语之外的其他语言创建自定义错误消息？**  
Settings`，并在 `getErrorValueString` 与 `getBooleanValueString` 中提供相应语言的翻译。

**问：开发阶段是否必须使用许可证？**  
答：可以使用免费试用，但在生产部署时必须 **设置 Aspose 许可证**。

**问：能否在运行时更改全局化设置？**  
答：可以——在需要时调用 `Workbook.getSettings().setGlobalizationSettings()` 并传入新实例。

**问：这会影响已有公式吗？**  
答：不会。自定义设置仅影响计算后错误和布尔值的显示方式。

**问：Aspose.Cells 是否支持其他文件格式（如 CSV、PDF）的自定义全局化？**  
答：自定义全局化适用于基于 Excel 的格式；导出为 PDF 或 CSV 时，已翻译的字符串会被保留。

## 资源
- **文档**：在 [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/) 查看详细指南  
- **下载**：前往 [Aspose Downloads](https://releases.aspose.com/cells/java/) 获取最新发行版  
- **购买**：在 [Aspose Purchase](https://purchase.aspose.com/buy) 购买商业许可证  
- **免费试用**：通过 [Aspose Free Trial](https://releases.aspose.com/cells/java/) 开始试用  
- **临时许可证**：在 [Aspose Temporary License](https://purchase.aspose.com/temporary-license/) 获取临时授权  
- **支持**：在 [Aspose Support Forum](https://forum.aspose.com/c/cells/9) 与社区交流获取帮助  

---

**最后更新：** 2026-02-01  
**测试环境：** Aspose.Cells 25.3 (Java)  
**作者：** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/tutorial-page-section >}}