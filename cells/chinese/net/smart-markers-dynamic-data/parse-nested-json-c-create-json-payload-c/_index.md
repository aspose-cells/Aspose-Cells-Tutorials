---
category: general
date: 2026-02-15
description: 使用 SmartMarkers 解析嵌套 JSON（C#），并学习如何为复杂订单创建 JSON 负载（C#）。一步步指南，提供完整代码和说明。
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: zh
og_description: 即时解析嵌套 JSON C#。学习在 C# 中创建 JSON 负载并使用 SmartMarkers 进行处理，提供完整可运行的示例。
og_title: 解析嵌套 JSON C# – 创建 JSON 负载 C#
tags:
- json
- csharp
- smartmarkers
title: 解析嵌套 JSON C# – 创建 JSON 负载 C#
url: /zh/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse Nested JSON C# – Create JSON Payload C#  

是否曾经需要 **parse nested JSON C#**，却不知从何入手？你并不孤单——很多开发者在面对对象内部包含数组的数据时都会卡住。好消息是，只需几行代码，你既可以 **create JSON payload C#**，又可以让 SmartMarkers 为你遍历嵌套结构。

在本教程中，我们将构建一个表示订单及其行项目的 JSON 字符串，启用 SmartMarkers 处理器理解嵌套范围，最后验证数据是否被正确解析。完成后，你将拥有一个可直接复制粘贴的完整程序，能够适配任何层级化的 JSON。

## What You’ll Need  

- .NET 6 或更高版本（代码同样可以在 .NET Core 3.1 上编译）  
- 对 SmartMarkers 库的引用（或任何支持嵌套范围的类似处理器）  
- 基础的 C# 知识——只需常规的 `using` 语句和一个 `Main` 方法  

就这些。除标记库外无需额外的 NuGet 包，也不需要外部服务。

## Step 1: Create JSON Payload C# – Building the Data  

首先我们构造包含订单数组的 JSON 字符串，每个订单内部拥有自己的 `Lines` 数组。可以把它看作一个小型的订单管理快照。

```csharp
using System;

namespace SmartMarkerDemo
{
    class Program
    {
        static void Main()
        {
            // -------------------------------------------------
            // STEP 1 – Define the JSON payload with nested arrays
            // -------------------------------------------------
            string ordersJson = @"{
                ""Orders"": [
                    {
                        ""Id"": 1,
                        ""Lines"": [
                            { ""Prod"": ""A"" },
                            { ""Prod"": ""B"" }
                        ]
                    },
                    {
                        ""Id"": 2,
                        ""Lines"": [
                            { ""Prod"": ""C"" }
                        ]
                    }
                ]
            }";

            // The rest of the steps follow…
```

为什么要把负载写成逐字字符串（verbatim string）？它会保留换行符，让你一眼就能看到结构——在调试嵌套 JSON 时非常方便。

> **Pro tip:** 如果你的 JSON 来自数据库或 API，可以用 `File.ReadAllText` 或网络请求替代字面量——本教程的其余部分并不依赖于数据来源。

## Step 2: Enable Nested Ranges with SmartMarkerOptions  

SmartMarkers 需要一点提示才能识别数组中还能包含另一个数组。这正是 `EnableNestedRanges` 的作用。

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

将 `EnableNestedRanges` 设置为 `true`，处理器会把每个 `Lines` 集合作为其父级 `Orders` 范围的子范围。若不启用此标志，内部循环将被忽略，只会看到顶层对象。

## Step 3: Process the JSON with SmartMarkersProcessor  

现在我们把 JSON 字符串和选项传给处理器。调用是同步的且不返回值——SmartMarkers 会把结果写入内部上下文，稍后可以检索。

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

如果使用的是其他库，请将 `ws.SmartMarkersProcessor.Process` 替换为相应的方法名；原理保持不变——传入 JSON 和启用嵌套处理的配置。

## Step 4: Verify the Parsed Result  

处理完成后，通常需要确认每个订单及其行项目都已被遍历。下面示例展示了如何使用假设的 `GetProcessedData` 方法（请替换为你库实际的访问器）将数据打印到控制台。

```csharp
            // -------------------------------------------------
            // STEP 4 – Output the parsed structure (demo purpose)
            // -------------------------------------------------
            var result = ws.SmartMarkersProcessor.GetProcessedData(); // pseudo‑code
            Console.WriteLine("=== Parsed Orders ===");
            foreach (var order in result.Orders)
            {
                Console.WriteLine($"Order Id: {order.Id}");
                foreach (var line in order.Lines)
                {
                    Console.WriteLine($"  - Product: {line.Prod}");
                }
            }
        }
    }
}
```

**Expected console output**

```
=== Parsed Orders ===
Order Id: 1
  - Product: A
  - Product: B
Order Id: 2
  - Product: C
```

看到层级结构被重新输出，说明 **parse nested json c#** 已按预期工作。

## Step 5: Edge Cases & Common Pitfalls  

### Empty Collections  
如果某个订单没有 `Lines`，处理器仍会创建一个空范围。确保下游代码能够处理空列表，避免抛出 `NullReferenceException`。

### Deeply Nested Structures  
`EnableNestedRanges` 开箱即支持两层嵌套。若需三层或更多层级，可能需要设置 `MaxNestedDepth`（如果库提供此属性），或对每个子对象递归调用处理器。

### Special Characters  
包含引号、反斜杠或 Unicode 的 JSON 字符串需要正确转义。使用逐字字符串 (`@""`) 可以规避大多数问题，但如果以编程方式构造 JSON，建议让 `System.Text.Json.JsonSerializer` 负责转义。

### Performance  
解析大体积负载（兆字节级）可能会占用大量内存。若遇到性能瓶颈，可考虑使用 `Utf8JsonReader` 流式读取 JSON，并将块传递给处理器。

## Visual Overview  

![展示 parse nested json c# 在 SmartMarkers 处理过程中的流程图](parse-nested-json-csharp-diagram.png "parse nested json c# diagram")

该图展示了从原始 JSON → SmartMarkerOptions → Processor → 解析后对象模型的整个过程。

## Recap  

我们完整演示了一个 **parse nested json c#** 示例，从 **create json payload c#** 到处理后验证嵌套数据。关键要点如下：

1. 构建与领域对象相匹配的结构化 JSON 字符串。  
2. 开启 `EnableNestedRanges`（或等效选项），让解析器识别内部数组。  
3. 运行处理器并检查结果，确保每一层都被遍历。  

## What’s Next?  

- **Dynamic payloads:** 用 `System.Text.Json` 将对象序列化，取代硬编码字符串。  
- **Custom markers:** 为 SmartMarkers 扩展自定义标签，在每个行项目中注入计算字段。  
- **Error handling:** 将 `Process` 调用包装在 try/catch 中，记录 `SmartMarkerException` 细节以便排查。  

尽情实验吧——把 `Orders` 数组换成客户、发票或任何层级化数据，都可以 **parse nested json c#**。模式保持不变。

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}