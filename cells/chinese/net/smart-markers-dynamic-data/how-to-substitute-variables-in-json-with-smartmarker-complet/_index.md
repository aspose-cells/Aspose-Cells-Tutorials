---
category: general
date: 2026-03-29
description: 如何使用 SmartMarker 在 JSON 中替换变量——学习使用 if 表达式、应用条件逻辑、进行数值乘法，并轻松生成 JSON。
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: zh
og_description: 如何使用 SmartMarker 在 JSON 中替换变量。了解如何使用 if 表达式、应用条件逻辑、进行数值乘法，并在几分钟内生成
  JSON。
og_title: 如何使用 SmartMarker 在 JSON 中替换变量 – 步骤详解
tags:
- C#
- SmartMarker
- JSON templating
title: 使用 SmartMarker 在 JSON 中替换变量 – 完整指南
url: /zh/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在 JSON 中使用 SmartMarker 替换变量 – 完整指南

是否曾想过 **如何在 JSON 负载中替换变量** 而无需编写自定义解析器？你并不孤单。在许多集成场景——比如发票、定价引擎或动态配置文件——中，你需要注入运行时值、应用简单的条件判断，甚至进行一次快速的乘法运算。本教程将向你展示 **如何使用 SmartMarker 库替换变量**，同时保持 JSON 的整洁可读。

我们将通过一个真实案例，涵盖 **使用 if 表达式**、**如何应用条件**、**如何进行乘法运算**，以及 **如何动态生成 json**。完成后，你将拥有一段可直接运行的 C# 代码片段，能够放入任意 .NET 项目中使用。

## 你将学到的内容

- 设置 `SmartMarkerOptions` 以存储可复用的变量。  
- 编写包含 `if` 表达式的 JSON 模板，实现条件逻辑。  
- 在模板中使用变量进行乘法运算。  
- 使用 `SmartMarkerProcessor` 处理模板并获取最终的 JSON 字符串。  
- 排查常见问题，如变量缺失或表达式格式错误。

无需外部服务，无需沉重依赖——只需纯 C# 与 SmartMarker NuGet 包。

---

## 替换变量的步骤概览

下面是一张工作流的高层示意图。可以把它想象成一个管道：左侧是原始 JSON 模板，SmartMarker 引擎在中间处理，右侧输出完整渲染后的 JSON。

![Diagram showing how to substitute variables in JSON](https://example.com/images/smartmarker-flow.png "如何在 JSON 中替换变量的示意图")

*图片替代文字：展示如何在 JSON 中替换变量的示意图。*

---

## 步骤 1：安装并导入 SmartMarker

在开始之前，请确保项目已引用 SmartMarker 包。如果使用 .NET CLI，运行：

```bash
dotnet add package SmartMarker
```

然后，在 C# 文件顶部添加必要的 `using` 指令：

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **小技巧：**截至 2026 年 3 月的最新版本是 2.4.1。它支持 .NET 6 及更高版本，同时在 .NET Framework 4.7 上也能正常工作。

---

## 步骤 2：创建 SmartMarker 选项并定义变量

现在我们创建一个 `SmartMarkerOptions` 实例，用来保存模板中需要复用的变量。这正是回答 **如何替换变量** 的关键——这些变量充当占位符，稍后由 SmartMarker 替换。

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

为什么把费率存放在 `Variables` 中而不是硬编码？因为你可能会从数据库、配置文件或用户输入中获取该数值。将其放在选项中，使模板更具可复用性和可测试性。

---

## 步骤 3：编写带有 `if` 表达式的 JSON 模板

这一步展示 **使用 if 表达式** 的威力。SmartMarker 允许你直接在 JSON 字符串中嵌入条件逻辑。语法看起来像属性名，但 SmartMarker 会将其视为指令。

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

注意键名 `if(Amount>500)`。SmartMarker 会求值表达式 `Amount>500`；若为真，则对应的值（`${Amount * Rate}`）会被插入输出。`${...}` 语法是 *变量替换* 引擎——这里我们 **如何进行乘法运算**（`Amount * Rate`）后再注入结果。

---

## 步骤 4：处理模板并获取最终 JSON

准备好选项和模板后，将它们交给处理器。`ProcessJson` 方法会解析模板、应用条件、执行乘法，并返回整洁的 JSON 字符串。

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

运行代码片段后会打印：

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**发生了什么？**  
- `Amount` 为 1000，满足 `Amount>500`。  
- SmartMarker 计算 `${Amount * Rate}` → `1000 * 0.08 = 80`。  
- 原始的条件键 (`if(Amount>500)`) 被替换为干净的属性名 (`Result`)。默认情况下 SmartMarker 使用 `"Result"`，但你可以自行定制（后文会介绍）。

如果将 `Amount` 改为 `400`，输出将变为：

```json
{
  "Amount": 400
}
```

条件块会消失，因为表达式求值为 `false`。这正是 **如何在 JSON 中应用条件** 的核心。

---

## 步骤 5：自定义输出属性名（可选）

有时你不想使用通用的 `"Result"` 键。SmartMarker 允许通过 `RenameIfExpression` 选项指定自定义名称：

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

输出：

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

现在条件值会存放在更具意义的属性名下——这对于下游服务需要特定字段的场景非常友好。

---

## 常见陷阱及规避方法

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 变量未找到 | 代码中引用了 `smartMarkerOptions.Variables` 中不存在的变量。 | 检查拼写并确保在处理前已添加该变量。 |
| `if` 语法无效 | 缺少括号或使用了错误的运算符（`>`、`<`、`==`）。 | 严格遵循 `if(<expression>)` 形式；SmartMarker 仅支持简单的数值比较。 |
| JSON 结构损坏 | 条件块后不小心留下了多余的逗号。 | 让 SmartMarker 负责移除；保持原始模板的语法正确。 |
| 数字格式异常 | 结果以字符串 `"80"` 而非数值出现。 | 后续自行转换或使用 `${(Amount * Rate):N0}` 进行数值格式化。 |

---

## 完整可运行示例（复制粘贴即用）

下面是完整程序代码，可直接编译运行。它演示了 **如何生成 json**，包括动态变量、条件判断和算术运算，代码行数不足 30 行。

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**预期的控制台输出**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

随意修改 `Amount` 以测试条件分支，或调整 `Rate` 观察不同的折扣计算效果。

---

## 拓展模式 – 更多 “如何” 场景

- **如何从配置文件替换变量**：从 `appsettings.json` 加载 `Dictionary<string, object>` 并填入 `smartMarkerOptions.Variables`。  
- **如何使用 if 表达式处理多重条件**：可写成 `"if(Amount>500 && CustomerType=='VIP')"`——SmartMarker 支持逻辑 AND/OR。  
- **如何应用条件格式化**：在表达式中使用 `${Amount:0.00}` 控制小数位数。  
- **如何进行更复杂的乘法运算**：`${(Amount - Discount) * TaxRate}` 同样适用。  
- **如何生成嵌套对象的 json**：将条件块放入另一个 JSON 对象内部，SmartMarker 会保留层级结构。

---

## 结论

我们已经完整演示了 **如何在 JSON 中使用 SmartMarker 替换变量**，展示了 **使用 if 表达式** 实现条件包含，解释了 **如何应用条件** 逻辑，说明了 **如何进行乘法运算**，并最终实现了 **如何生成 json**，以供下游使用。该方法轻量、无需外部模板引擎，且可无缝融入任何 C# 代码库。

不妨动手尝试——调节变量、添加更多条件，或将整个流程封装成帮助类，以在整个解决方案中复用。当你需要快速生成动态 JSON 时，SmartMarker 是一个可靠、可投入生产的选项。

---

**后续步骤**

- 深入了解 SmartMarker 的高级特性，如循环 (`foreach`) 和自定义函数。  
- 将此技术与 ASP.NET Core 端点结合，提供动态 JSON API。  
- 探索其他模板库（如 Handlebars.NET），进行对比，特别是当你需要更丰富的语法时。

有任何问题或特定使用场景想要讨论？在下方留言，我们一起排查。祝编码愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}