---
"date": "2025-04-05"
"description": "Узнайте, как автоматизировать и освоить Excel PivotTables с помощью Aspose.Cells для .NET. Это руководство охватывает загрузку рабочих книг, настройку итогов, параметры сортировки и эффективное сохранение изменений."
"title": "Мастер сводных таблиц Excel с помощью Aspose.Cells в .NET&#58; загрузка, сортировка и сохранение"
"url": "/ru/net/data-analysis/excel-pivottable-aspose-cells-net-tutorial/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Освоение сводных таблиц Excel с помощью Aspose.Cells в .NET: загрузка, сортировка и сохранение

## Введение
Боретесь со сложным управлением данными в Excel? Автоматизируйте и оптимизируйте свои задачи анализа данных с помощью Aspose.Cells для .NET. Это руководство идеально подходит для разработчиков, улучшающих приложения, или бизнес-аналитиков, ищущих точные сведения. Узнайте, как загружать рабочие книги, настраивать расширенные функции PivotTable, такие как общие и промежуточные итоги строк, автоматическая сортировка и сохранение изменений.

**Что вы узнаете:**
- Загрузка и доступ к сводным таблицам Excel с помощью Aspose.Cells
- Настройте общие и промежуточные итоги по строкам для расширенных сводок данных
- Настройте параметры автоматической сортировки и автоматического показа для лучшего отображения данных
- Эффективное сохранение изменений на диске

Давайте погрузимся в эти мощные функции!

## Предпосылки
Перед началом убедитесь, что у вас есть:

1. **Библиотеки и версии:** Используйте Aspose.Cells для .NET версии 23.x или более поздней.
2. **Требования к настройке среды:** Настройте среду разработки с установленной платформой .NET (версии 6 или новее).
3. **Необходимые знания:** Знакомство с программированием на языке C# и базовые знания рабочих книг Excel будут преимуществом.

## Настройка Aspose.Cells для .NET
Для начала установите библиотеку Aspose.Cells:

- **Использование .NET CLI:**
  ```bash
  dotnet add package Aspose.Cells
  ```

- **Использование менеджера пакетов:**
  ```plaintext
  PM> NuGet\Install-Package Aspose.Cells
  ```

### Приобретение лицензии
Aspose предлагает различные варианты лицензирования, включая бесплатную пробную версию и временные лицензии. Чтобы изучить их:

- Посетите [бесплатная пробная версия](https://releases.aspose.com/cells/net/) для оценки.
- Получить [временная лицензия](https://purchase.aspose.com/temporary-license/) для тестирования функций без ограничений.
- Для полного доступа рассмотрите возможность покупки у [Страница покупки Aspose](https://purchase.aspose.com/buy).

### Базовая инициализация
Начните с создания экземпляра `Workbook` класс и загрузка вашего файла Excel:

```csharp
string sourceDir = "YOUR_SOURCE_DIRECTORY";
string outputDir = "YOUR_OUTPUT_DIRECTORY";

// Загрузить книгу с диска
Workbook workbook = new Workbook(sourceDir + "Book1.xls");
```

## Руководство по внедрению
Подробно изучите каждую функцию ниже.

### Загрузка и доступ к сводной таблице
#### Обзор
Доступ к сводной таблице необходим для манипулирования данными. Вот как загрузить файл Excel и получить определенную сводную таблицу.

#### Шаг за шагом
**1. Загрузите рабочую книгу:**
   ```csharp
   using Aspose.Cells;
   using Aspose.Cells.Pivot;
   
   string sourceDir = "YOUR_SOURCE_DIRECTORY";
   Workbook workbook = new Workbook(sourceDir + "Book1.xls");
   ```
**2. Доступ к рабочему листу и сводной таблице:**
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   int pivotIndex = 0;
   PivotTable pivotTable = worksheet.PivotTables[pivotIndex];
   ```
### Установить строки общих и промежуточных итогов
#### Обзор
Настройка общих и промежуточных итогов по строкам обеспечивает эффективное суммирование данных.

#### Шаг за шагом
**1. Доступ к полям строк:**
   ```csharp
   PivotFieldCollection pivotFields = pivotTable.RowFields;
   PivotField pivotField = pivotFields[0];
   ```
**2. Настройте итоги и промежуточные итоги:**
   ```csharp
   // Включить общие итоги
   pivotTable.RowGrand = true;

   // Установить промежуточные итоги для суммы и количества
   pivotField.SetSubtotals(PivotFieldSubtotalType.Sum, true);
   pivotField.SetSubtotals(PivotFieldSubtotalType.Count, true);
   ```
### Настройте параметры автосортировки
#### Обзор
Автосортировка организует данные динамически. Вот как настроить эту функцию.

#### Шаг за шагом
**1. Включить автосортировку:**
   ```csharp
   PivotField pivotField = pivotTable.RowFields[0];
   pivotField.IsAutoSort = true;
   pivotField.IsAscendSort = true; // Установить порядок сортировки по возрастанию
   ```
**2. Определите индекс поля сортировки:**
   ```csharp
   pivotField.AutoSortField = -5;
   ```
### Настройте параметры автопоказа
#### Обзор
Функция автопоказа автоматически отображает только релевантные данные.

#### Шаг за шагом
**1. Включите настройки автопоказа:**
   ```csharp
   PivotField pivotField = pivotTable.RowFields[0];
   pivotField.IsAutoShow = true;
   ```
**2. Настройте условия показа:**
   ```csharp
   pivotField.AutoShowField = 0; // На основе определенного индекса поля данных
   ```
### Сохраните файл Excel
#### Обзор
После внесения изменений сохраните книгу обратно на диск.

#### Шаг за шагом
**1. Сохранить рабочую книгу:**
   ```csharp
   string outputDir = "YOUR_OUTPUT_DIRECTORY";
   workbook.Save(outputDir + "output.xls");
   ```
## Практические применения
Освоение сводных таблиц с помощью Aspose.Cells приносит пользу в различных сценариях:

1. **Финансовая отчетность:** Автоматизируйте квартальные отчеты для подведения итогов финансового состояния.
2. **Управление запасами:** Сортируйте и фильтруйте данные по запасам, чтобы определить товары с низким запасом.
3. **Анализ продаж:** Выделите наиболее эффективные продукты или регионы с помощью автоматической сортировки и промежуточных итогов.
4. **Аналитика кадрового делопроизводства:** Создавайте сводки по эффективности работы сотрудников по отделам или ролям.

## Соображения производительности
Обеспечьте оптимальную производительность с помощью Aspose.Cells:
- **Управление памятью:** Распоряжаться `Workbook` объекты, когда это делается для освобождения ресурсов.
- **Эффективная обработка данных:** Обрабатывайте только необходимые поля данных, чтобы сократить время загрузки.
- **Пакетная обработка:** При работе с несколькими файлами обрабатывайте их пакетами, а не последовательно.

## Заключение
Вы узнали, как использовать Aspose.Cells для .NET для эффективного управления сводными таблицами. От загрузки таблиц и настройки параметров сортировки до сохранения изменений, эти навыки значительно расширяют ваши возможности обработки данных.

**Следующие шаги:**
- Поэкспериментируйте с различными конфигурациями на выборочных наборах данных.
- Изучите дополнительные возможности Aspose.Cells, чтобы максимально использовать его возможности.

**Призыв к действию:** Внедрите это решение в свой следующий проект и трансформируйте свои рабочие процессы Excel!

## Раздел часто задаваемых вопросов
1. **Как установить Aspose.Cells для .NET?**
   - Используйте менеджер пакетов NuGet или команду .NET CLI, как описано выше.
2. **Могу ли я использовать Aspose.Cells без лицензии?**
   - Да, начните с бесплатной пробной версии, чтобы оценить возможности.
3. **В чем разница между общими итогами и промежуточными итогами в сводных таблицах?**
   - Общие итоги предоставляют общую сводку по всем строкам данных, тогда как промежуточные итоги предлагают сводки на разных уровнях иерархии данных.
4. **Можно ли автоматизировать задачи Excel с помощью Aspose.Cells?**
   - Конечно! Aspose.Cells предоставляет обширные возможности автоматизации в книгах Excel.
5. **Где я могу найти больше ресурсов по Aspose.Cells?**
   - Исследуйте [официальная документация](https://reference.aspose.com/cells/net/) и форумы поддержки сообщества для получения дальнейших рекомендаций.

## Ресурсы
- Документация: [Справочник API Aspose.Cells .NET](https://reference.aspose.com/cells/net/)
- Скачать: [Страница релизов](https://releases.aspose.com/cells/net/)
- Покупка: [Купить лицензию](https://purchase.aspose.com/buy)
- Бесплатная пробная версия: [Попробуйте Aspose.Cells](https://releases.aspose.com/cells/net/)
- Временная лицензия: [Запросить здесь](https://purchase.aspose.com/temporary-license/)
- Поддерживать: [Форум Aspose](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}