---
category: general
date: 2026-02-14
description: 'Автоматизируйте создание счетов с помощью SmartMarker: узнайте, как
  дублировать листы, динамически их именовать и освоить динамическое именование листов
  за считанные минуты.'
draft: false
keywords:
- automate invoice generation
- how to name worksheets
- how to repeat worksheet
- dynamic worksheet naming
language: ru
og_description: Автоматизируйте создание счетов с помощью SmartMarker. Это руководство
  показывает, как дублировать листы, динамически их именовать и освоить динамическое
  именование листов.
og_title: Автоматизация генерации счетов – динамическое именование листов и их повторение
tags:
- C#
- SmartMarker
- Excel Automation
title: Автоматизация создания счетов – динамическое именование листов и повторение
  в C#
url: /ru/net/smart-markers-dynamic-data/automate-invoice-generation-dynamic-worksheet-naming-repeati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Автоматизация создания счетов – динамическое именование листов и их повторение в C#

Ever wondered how to **автоматизировать создание счетов** without manually copying sheets for each order? You're not alone. Many developers hit a wall when they need a separate worksheet per invoice but also want the sheet name to reflect the order number. In this tutorial we’ll solve that problem using SmartMarker’s `SmartMarkerProcessor` and show you **how to name worksheets** dynamically while also covering **how to repeat worksheet** for each record. By the end you’ll have a ready‑to‑run C# sample that produces a workbook where each invoice lives on its own, nicely‑named tab.

We’ll walk through every step—from pulling orders from a data source to configuring `SmartMarkerOptions` for dynamic worksheet naming. No external docs required; everything you need is right here. A little prerequisite knowledge of C# and a reference to the Aspose.Cells library (or any SmartMarker‑compatible engine) will do.

---

## Что вы построите

- Retrieve a collection of order objects. → Получить коллекцию объектов заказа.
- Configure SmartMarker to **repeat a worksheet** for each order. → Настроить SmartMarker для **повторения листа** для каждого заказа.
- Apply **dynamic worksheet naming** using the `{OrderId}` placeholder. → Применить **динамическое именование листов** с использованием заполнителя `{OrderId}`.
- Generate an Excel file where each tab is named `Invoice_12345`, `Invoice_67890`, etc. → Сгенерировать файл Excel, где каждая вкладка называется `Invoice_12345`, `Invoice_67890` и т.д.
- Verify the output by opening the workbook. → Проверить результат, открыв книгу.

---

## Требования

- .NET 6.0 или новее (the code compiles with .NET 5+ as well). → (the code compiles with .NET 5+ as well).
- Aspose.Cells for .NET (or any library that implements SmartMarker). Install via NuGet:

```bash
dotnet add package Aspose.Cells
```

- A basic `Order` class (you can replace it with your own DTO). → Базовый класс `Order` (можете заменить его своим DTO).

---

## Шаг 1: Настройка проекта и модели

First, create a new console app and define the data model that represents an order. → Сначала создайте новое консольное приложение и определите модель данных, представляющую заказ.

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    // Simple POCO representing an order – replace fields as needed
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }
    }

    class Program
    {
        static void Main()
        {
            // Retrieve orders (in real life this could be a DB call)
            var orders = GetOrders();

            // The rest of the tutorial continues here...
        }

        // Mock method – in production pull from EF Core, Dapper, etc.
        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

> **Совет:** Keep the model lightweight for the demo; you can always enrich it later with line items, tax details, etc. → Сделайте модель лёгкой для демонстрации; позже её всегда можно расширить позициями, деталями налогов и т.д.

---

## Шаг 2: Подготовка шаблона Excel

SmartMarker works against a template workbook. Create a file called `InvoiceTemplate.xlsx` with a single worksheet named `InvoiceTemplate`. In cell **A1** place a SmartMarker placeholder like:

```
{{OrderId}} – {{Customer}} – {{Date}} – ${{Total}}
```

You can format the cells any way you like—bold headers, currency formatting, etc. Save the file in the project’s root folder. → Вы можете форматировать ячейки как угодно — жирные заголовки, формат валюты и т.д. Сохраните файл в корневой папке проекта.

> **Зачем нужен шаблон?** It separates layout from code, letting designers tweak the look without touching the logic. → Он отделяет макет от кода, позволяя дизайнерам менять внешний вид без вмешательства в логику.

---

## Шаг 3: Настройка параметров SmartMarker – повтор и именование листов

Now we’ll tell SmartMarker to *repeat* the template worksheet for every order and to give each copy a name that includes the order ID. This is the core of **dynamic worksheet naming**. → Это основа **динамического именования листов**.

```csharp
// Inside Main() after retrieving orders
// Load the template workbook
Workbook wb = new Workbook("InvoiceTemplate.xlsx");

// Set up SmartMarker options
var smartMarkerOptions = new SmartMarkerOptions
{
    // Instructs SmartMarker to create a new worksheet per data item
    RepeatWorksheet = true,

    // Naming pattern – {OrderId} will be replaced with the actual value
    RepeatWorksheetName = "Invoice_{OrderId}"
};

// Run the processor
wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

// Save the result
string outputPath = "GeneratedInvoices.xlsx";
wb.Save(outputPath);

Console.WriteLine($"✅ Invoices generated: {outputPath}");
```

### Как это работает

- **`RepeatWorksheet = true`** tells the engine to duplicate the source sheet for each element in the `orders` collection. This satisfies the **how to repeat worksheet** requirement. → **`RepeatWorksheet = true`** указывает движку дублировать исходный лист для каждого элемента в коллекции `orders`. Это удовлетворяет требование **как повторять лист**.

- **`RepeatWorksheetName = "Invoice_{OrderId}"`** is a template string where `{OrderId}` is a placeholder that SmartMarker replaces with the current order’s ID. That’s the answer to **how to name worksheets** and **dynamic worksheet naming**. → **`RepeatWorksheetName = "Invoice_{OrderId}"`** — строка‑шаблон, где `{OrderId}` является заполнителем, который SmartMarker заменяет текущим идентификатором заказа. Это ответ на **как назвать листы** и **динамическое именование листов**.

- The processor merges each order’s fields (`{{OrderId}}`, `{{Customer}}`, etc.) into the duplicated sheet, producing a fully‑filled invoice. → Процессор объединяет поля каждого заказа (`{{OrderId}}`, `{{Customer}}` и т.д.) с дублированным листом, создавая полностью заполненный счёт.

---

## Шаг 4: Запуск приложения и проверка результата

Compile and run the console app: → Скомпилируйте и запустите консольное приложение:

```bash
dotnet run
```

You should see the success message in the console. Open `GeneratedInvoices.xlsx` and you’ll find three tabs: → Вы должны увидеть сообщение об успехе в консоли. Откройте `GeneratedInvoices.xlsx`, и вы найдете три вкладки:

- **Invoice_1001**
- **Invoice_1002**
- **Invoice_1003**

Each sheet contains the order data substituted into the placeholders. The layout you designed in the template is preserved, proving that **automate invoice generation** works end‑to‑end. → Каждый лист содержит данные заказа, подставленные в заполнители. Макет, который вы разработали в шаблоне, сохраняется, подтверждая, что **автоматизация создания счетов** работает от начала до конца.

### Ожидаемый скриншот (alt‑текст для SEO)

![пример автоматизации создания счетов, показывающий три динамически именованных листа](/images/invoice-automation.png)

> *Текст alt изображения включает основной ключевой запрос для удовлетворения требований SEO.*

---

## Шаг 5: Пограничные случаи и распространённые варианты

### Что если OrderId содержит недопустимые символы?

Excel sheet names can’t contain `\ / ? * [ ] :`. If your IDs might include those, sanitize them: → Имена листов Excel не могут содержать `\ / ? * [ ] :`. Если ваши идентификаторы могут включать эти символы, очистите их:

```csharp
RepeatWorksheetName = "Invoice_{SanitizedOrderId}"
```

Add a computed property to `Order`: → Добавьте вычисляемое свойство в `Order`:

```csharp
public string SanitizedOrderId => OrderId.ToString().Replace("/", "-").Replace("\\", "-");
```

### Нужно оставить оригинальный лист‑шаблон?

Set `smartMarkerOptions.RemoveTemplate = false;` (default is `true`). This leaves the original `InvoiceTemplate` untouched as a reference. → Установите `smartMarkerOptions.RemoveTemplate = false;` (по умолчанию `true`). Это оставит оригинальный `InvoiceTemplate` нетронутым в качестве ссылки.

### Хотите группировать счета по клиенту?

You can nest **repeat groups**. First repeat by customer, then by orders inside each customer worksheet. The syntax gets a bit more involved, but the principle stays the same—use `RepeatWorksheet` and a naming pattern that reflects the hierarchy. → Можно вложить **repeat groups**. Сначала повторить по клиенту, затем по заказам внутри листа каждого клиента. Синтаксис становится чуть сложнее, но принцип остаётся тем же — используйте `RepeatWorksheet` и шаблон именования, отражающий иерархию.

---

## Полный рабочий пример (весь код в одном месте)

```csharp
using System;
using System.Collections.Generic;
using Aspose.Cells;
using Aspose.Cells.SmartMarkers;

namespace InvoiceAutomation
{
    public class Order
    {
        public int OrderId { get; set; }
        public string Customer { get; set; }
        public DateTime Date { get; set; }
        public decimal Total { get; set; }

        // Helper for safe sheet names
        public string SanitizedOrderId => OrderId.ToString();
    }

    class Program
    {
        static void Main()
        {
            var orders = GetOrders();

            // Load template
            Workbook wb = new Workbook("InvoiceTemplate.xlsx");

            // Configure SmartMarker for repeating and naming worksheets
            var smartMarkerOptions = new SmartMarkerOptions
            {
                RepeatWorksheet = true,
                RepeatWorksheetName = "Invoice_{OrderId}" // dynamic worksheet naming
                // RemoveTemplate = true; // default behavior
            };

            // Process the data
            wb.SmartMarkerProcessor.StartSmartMarkerProcessing(orders, smartMarkerOptions);

            // Save the final workbook
            string outputPath = "GeneratedInvoices.xlsx";
            wb.Save(outputPath);

            Console.WriteLine($"✅ Invoices generated: {outputPath}");
        }

        private static List<Order> GetOrders()
        {
            return new List<Order>
            {
                new Order { OrderId = 1001, Customer = "Acme Corp", Date = DateTime.Today, Total = 1234.56m },
                new Order { OrderId = 1002, Customer = "Beta Ltd.", Date = DateTime.Today.AddDays(-1), Total = 789.00m },
                new Order { OrderId = 1003, Customer = "Gamma LLC", Date = DateTime.Today.AddDays(-2), Total = 456.78m }
            };
        }
    }
}
```

Copy‑paste this into `Program.cs`, place `InvoiceTemplate.xlsx` beside it, and you’re good to go. → Скопируйте‑вставьте это в `Program.cs`, разместите `InvoiceTemplate.xlsx` рядом с ним, и вы готовы к работе.

---

## Часто задаваемые вопросы

**Q: Работает ли этот подход с большими наборами данных (тысячами счетов)?**  
**A:** Да. SmartMarker эффективно потоково обрабатывает данные, но следите за использованием памяти. Если достигнуты ограничения, рассмотрите обработку пакетами и запись каждого пакета в отдельную книгу.

**Q: Могу ли я автоматически добавить логотип к каждому счету?**  
**A:** Конечно. Разместите изображение логотипа на листе шаблона. Поскольку лист дублируется, логотип появляется в каждом сгенерированном счёте без дополнительного кода.

**Q: Что если нужно защитить листы?**  
**A:** После обработки пройдитесь по `wb.Worksheets` и вызовите `ws.Protect(Password, ProtectionType.All)`.

---

## Заключение

We’ve just **автоматизировали создание счетов** by leveraging SmartMarker’s repeat‑worksheet feature and a clever naming pattern. The tutorial covered **how to name worksheets**, demonstrated **how to repeat worksheet** for each order, and showcased **dynamic worksheet naming** that keeps your workbook tidy and searchable.  

From pulling data, setting up a template, configuring `SmartMarkerOptions`, to handling edge cases, you now have a complete, runnable solution. Next, try adding line‑item tables, applying conditional formatting, or exporting the same data to PDF for a fully‑automated billing pipeline.  

Ready to level up? Explore related topics such as “bulk Excel export with Aspose.Cells”, “PDF conversion of worksheets”, or “emailing generated invoices directly from C#”. The sky’s the limit—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}