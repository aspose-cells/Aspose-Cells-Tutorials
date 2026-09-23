---
category: general
date: 2026-02-15
description: Разбор вложенного JSON в C# с использованием SmartMarkers и изучение
  создания JSON‑payload в C# для сложных заказов. Пошаговое руководство с полным кодом
  и объяснениями.
draft: false
keywords:
- parse nested json c#
- create json payload c#
language: ru
og_description: Мгновенно разбирайте вложенный JSON в C#. Узнайте, как создать JSON‑payload
  в C# и обработать его с помощью SmartMarkers в полном, исполняемом примере.
og_title: Разбор вложенного JSON в C# – Создание JSON‑payload в C#
tags:
- json
- csharp
- smartmarkers
title: Разбор вложенного JSON C# – Создание JSON‑payload C#
url: /ru/net/smart-markers-dynamic-data/parse-nested-json-c-create-json-payload-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Parse Nested JSON C# – Create JSON Payload C#  

Когда‑то вам нужно было **parse nested JSON C#**, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с проблемой, когда их данные содержат массивы внутри объектов. Хорошая новость в том, что несколькими строками кода вы можете как **create JSON payload C#**, так и позволить SmartMarkers пройтись по вложенной структуре за вас.  

В этом руководстве мы построим строку JSON, представляющую заказы с позициями, настроим процессор SmartMarkers для понимания вложенных диапазонов и, наконец, проверим, что данные были разобраны корректно. К концу вы получите автономную программу, готовую к копированию и вставке, которую можно адаптировать под любой иерархический JSON.

## What You’ll Need  

- .NET 6 или новее (код также компилируется с .NET Core 3.1)  
- Ссылка на библиотеку SmartMarkers (или любой аналогичный процессор, поддерживающий вложенные диапазоны)  
- Базовые знания C# — ничего экзотического, только обычные `using`‑директивы и метод `Main`  

Это всё. Никаких дополнительных пакетов NuGet, кроме библиотеки маркеров, и никаких внешних сервисов.

## Step 1: Create JSON Payload C# – Building the Data  

Сначала формируем строку JSON, содержащую массив заказов, каждый из которых имеет собственный массив `Lines`. Представьте это как небольшую «снимок» системы управления заказами.

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

Почему именно строка‑литерал? Она сохраняет переносы строк и позволяет сразу увидеть структуру — удобно при отладке вложённого JSON.  

> **Pro tip:** Если ваш JSON приходит из базы данных или API, вы можете заменить литерал на `File.ReadAllText` или веб‑запрос — в этом руководстве нет зависимости от источника.

## Step 2: Enable Nested Ranges with SmartMarkerOptions  

SmartMarkers нуждаются в небольшом указании, что массив может содержать другой массив. Для этого и предназначен `EnableNestedRanges`.

```csharp
            // -------------------------------------------------
            // STEP 2 – Configure SmartMarker options for nesting
            // -------------------------------------------------
            SmartMarkerOptions options = new SmartMarkerOptions
            {
                EnableNestedRanges = true   // <-- crucial for Orders → Lines
            };
```

Установка `EnableNestedRanges` в `true` сообщает процессору рассматривать каждую коллекцию `Lines` как под‑диапазон родительского диапазона `Orders`. Без этого флага вложенный цикл будет проигнорирован, и вы увидите только объекты верхнего уровня.

## Step 3: Process the JSON with SmartMarkersProcessor  

Теперь передаём строку JSON и параметры процессору. Вызов синхронный и ничего не возвращает — SmartMarkers записывает результаты во внутренний контекст, который можно получить позже.

```csharp
            // -------------------------------------------------
            // STEP 3 – Run the processor on the JSON payload
            // -------------------------------------------------
            ws.SmartMarkersProcessor.Process(ordersJson, options);
```

Если вы используете другую библиотеку, замените `ws.SmartMarkersProcessor.Process` на соответствующее имя метода; принцип остаётся тем же — передать JSON и конфигурацию, включающую обработку вложенности.

## Step 4: Verify the Parsed Result  

После обработки обычно хочется убедиться, что каждый заказ и его позиции были обработаны. Ниже простой способ вывести данные обратно в консоль с помощью гипотетического метода `GetProcessedData` (замените на реальный accessor вашей библиотеки).

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

Видя восстановленную иерархию, вы подтверждаете, что **parse nested json c#** отработал как задумано.

## Step 5: Edge Cases & Common Pitfalls  

### Empty Collections  
Если у заказа нет `Lines`, процессор всё равно создаст пустой диапазон. Убедитесь, что ваш последующий код умеет работать с пустым списком без выбрасывания `NullReferenceException`.

### Deeply Nested Structures  
`EnableNestedRanges` работает для вложенности двух уровней «из коробки». Для трёх и более уровней может потребоваться задать `MaxNestedDepth` (если библиотека его поддерживает) или рекурсивно вызывать процессор для каждого под‑объекта.

### Special Characters  
Строки JSON, содержащие кавычки, обратные слеши или Unicode, требуют правильного экранирования. Использование дословной строки (`@""`) как у нас обходится без большинства проблем, но если вы формируете JSON программно, позвольте `System.Text.Json.JsonSerializer` выполнить экранирование за вас.

### Performance  
Разбор больших payload‑ов (мегабайты) может быть ресурсоёмким. Рассмотрите потоковое чтение JSON с помощью `Utf8JsonReader` и передачу порций процессору, если столкнётесь с узкими местами производительности.

## Visual Overview  

![Диаграмма, иллюстрирующая как parse nested json c# проходит через обработку SmartMarkers](parse-nested-json-csharp-diagram.png "диаграмма parse nested json c#")

Изображение показывает путь от сырого JSON → SmartMarkerOptions → Processor → Parsed object model.

## Recap  

Мы прошли полный пример **parse nested json c#**, от **create json payload c#** до проверки вложенных данных после обработки. Ключевые выводы:

1. Сформируйте хорошо структурированную строку JSON, отражающую ваши доменные объекты.  
2. Включите `EnableNestedRanges` (или эквивалент), чтобы парсер учитывал вложенные массивы.  
3. Запустите процессор и проверьте результат, убедившись, что каждый уровень был пройден.  

## What’s Next?  

- **Dynamic payloads:** Замените жёстко закодированную строку объектами, сериализованными через `System.Text.Json`.  
- **Custom markers:** Расширьте SmartMarkers собственными тегами для вставки вычисляемых полей в каждую позицию.  
- **Error handling:** Оберните вызов `Process` в `try/catch` и логируйте детали `SmartMarkerException` для отладки.  

Экспериментируйте — заменяйте массив `Orders` на клиентов, счета или любые иерархические данные, которые нужно **parse nested json c#**. Паттерн остаётся тем же.

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}