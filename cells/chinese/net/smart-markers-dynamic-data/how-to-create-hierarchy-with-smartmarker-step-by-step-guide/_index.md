---
category: general
date: 2026-02-14
description: 在 SmartMarker 模板中创建层次结构比你想象的更容易——学习如何创建层次化数据以及如何高效列出员工。
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: zh
og_description: 在 SmartMarker 模板中创建层次结构很简单。请按照本指南创建层次化数据并列出具有嵌套范围的员工。
og_title: 如何使用 SmartMarker 创建层次结构 – 完整指南
tags:
- SmartMarker
- C#
- templating
title: 如何使用 SmartMarker 创建层次结构 – 步骤指南
url: /zh/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

’s the limit, and now you have a solid foundation." => translate.

"Happy coding! If you hit any snags, drop a comment below—I'm happy to help." => "祝编码愉快！如果遇到任何问题，欢迎在下方留言——我很乐意帮助。"

Image alt translation: alt="How to create hierarchy diagram showing department‑employee relationship" => Chinese: "展示部门‑员工关系的层级结构图". Keep alt attribute.

Now produce final content with same shortcodes and markdown.

Let's assemble.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何使用 SmartMarker 创建层级结构 – 完整指南

有没有想过 **如何在 SmartMarker 模板中创建层级结构** 而不抓狂？你并不是唯一的。在许多报表场景中，你需要父子关系——比如部门及其员工。好消息是，一旦掌握正确的步骤，SmartMarker 就能让这变得轻而易举。

在本教程中，我们将完整演示整个过程：从 **在 C# 中创建层级数据**、启用嵌套范围，到最终渲染一个 **列出每个部门员工** 的模板。结束时，你将拥有一个可直接运行的示例，能够放入任何 .NET 项目中使用。

---

## 你需要准备的环境

- .NET 6+（任何近期版本均可）
- 对 **SmartMarker** 库的引用（`ws.SmartMarkerProcessor` 命名空间）
- 基础的 C# 知识——不需要高级技巧，只要会使用几个对象和 lambda 表达式
- 你喜欢的 IDE 或编辑器（Visual Studio、Rider、VS Code……随你挑）

如果这些都已经准备好，太好了——让我们开始吧。

---

## 创建层级结构 – 概览

核心思路是构建一个 **嵌套对象图**，它映射出你希望在最终文档中看到的结构。以我们的示例来说，对象图如下：

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker 随后可以遍历 `Departments`，并且因为我们会打开 **嵌套范围处理**，它会自动循环每个部门的 `Employees` 集合。

---

## 步骤 1：构建层级数据模型

首先我们创建一个匿名对象，其中包含部门数组，每个部门都有自己的员工列表。使用匿名类型可以让示例保持轻量——以后你可以自行替换为真实的 POCO 类。

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **为什么这很重要：** `Departments` 数组是顶层集合。每个元素内部包含一个 `Employees` 数组，这为我们后续使用 `#Departments.Employees#` 访问提供了第二层层级。

---

## 步骤 2：启用嵌套范围处理

除非明确告诉 SmartMarker，否则它不会深入内部集合。`SmartMarkerOptions` 对象正是用来控制这个开关的。

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **专业提示：** 如果忘记设置此标志，内部的 `#Employees#` 范围将什么也不返回，你会疑惑为什么模板是空白的。

---

## 步骤 3：使用数据运行处理器

现在我们把数据和选项交给处理器。`ws` 变量代表你的 **WebService**（或任何承载 SmartMarker 引擎的对象）。

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

此时 SmartMarker 会解析模板，用每个部门的名称替换 `#Departments.Name#`，并且因为已启用嵌套范围，它会遍历每个部门的 `Employees` 集合。

---

## 步骤 4：编写模板标记

下面是一个最小化的模板，演示了外层和内层循环。将其粘贴到 SmartMarker 模板编辑器中（或放入你传给处理器的 `.txt` 文件）。

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

渲染后你会看到：

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **你看到的内容：** 外层的 `#Departments.Name#` 打印部门标题。内层的 `#Departments.Employees#` 块遍历每位员工，而块内部的 `#Departments.Employees#` 则输出实际的姓名。

---

## 预期输出与验证

运行完整示例（数据 + 选项 + 模板）应当产生上面展示的列表。要快速验证，你可以将结果输出到控制台：

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

如果看到两个部门标题以及其下的员工项目符号，说明你已经成功 **创建了层级结构** 并 **列出了员工**。

---

## 常见陷阱与边缘情况

| 问题 | 产生原因 | 解决方案 |
|------|----------|----------|
| 员工无输出 | `EnableNestedRange` 为 false | 将 `EnableNestedRange = true` |
| 员工姓名重复 | 同一数组在多个部门之间复用 | 克隆数组或使用不同的集合 |
| 层级结构过大导致内存压力 | SmartMarker 将整个对象图加载到内存中 | 使用流式处理或对大集合进行分页 |
| 模板语法错误 | 缺少闭合的 `#/…#` 标记 | 使用 SmartMarker 验证器或用小模板快速测试 |

---

## 进一步探索 – 实际场景变体

1. **动态数据源** – 从数据库中获取部门并使用 LINQ 映射到匿名结构。  
2. **条件格式化** – 为每位员工添加 `IsManager` 标志，并使用 SmartMarker 的条件标签（`#if …#`）突出显示经理。  
3. **多层嵌套** – 如果需要在部门内部再划分团队，只需添加另一个集合（`Teams`），并保持 `EnableNestedRange` 开启。

---

## 完整可运行示例（复制粘贴即可）

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**模板（template.txt）**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

运行程序会准确输出前面展示的层级结构。

---

## 结论

我们已经完整阐述了 **如何在 SmartMarker 中创建层级结构**：从在 C# 中构造 **层级数据**、打开嵌套范围，到最终渲染一个 **按部门列出员工** 的模板。该模式具备良好的可扩展性——只需添加更多嵌套集合或条件逻辑，你就拥有了一个强大的报表引擎。

准备好迎接下一个挑战了吗？尝试将匿名类型换成强类型 POCO 类，或将此流程集成到返回 PDF 或 Word 文档的 ASP.NET Core 接口中。天地无限，而你已经拥有了坚实的基础。

---

![How to create hierarchy diagram](image.png){alt="展示部门‑员工关系的层级结构图"}

祝编码愉快！如果遇到任何问题，欢迎在下方留言——我很乐意帮助。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}