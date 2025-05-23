---
"description": "Узнайте, как отключить ленту сводной таблицы в .NET с помощью Aspose.Cells. Это пошаговое руководство позволяет легко настроить взаимодействие с Excel."
"linktitle": "Отключить ленту сводной таблицы программно в .NET"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Отключить ленту сводной таблицы программно в .NET"
"url": "/ru/net/creating-and-configuring-pivot-tables/disabling-pivot-table-ribbon/"
"weight": 15
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Отключить ленту сводной таблицы программно в .NET

## Введение
Вы когда-нибудь хотели контролировать видимость сводных таблиц в файлах Excel при работе с .NET? Что ж, вы попали по адресу! В этом уроке мы научимся программно отключать ленту сводных таблиц с помощью библиотеки Aspose.Cells для .NET. Эта функция может быть исключительно полезна разработчикам, желающим настроить взаимодействие пользователей с документами Excel. Итак, пристегните ремни безопасности и давайте нырнем прямо сейчас!
## Предпосылки
Прежде чем мы начнем, вам необходимо иметь под рукой несколько вещей:
1. Библиотека Aspose.Cells: Убедитесь, что у вас установлена библиотека Aspose.Cells. Если вы еще этого не сделали, вы можете загрузить ее с [здесь](https://releases.aspose.com/cells/net/).
2. Среда разработки .NET: рабочая среда разработки .NET (настоятельно рекомендуется Visual Studio).
3. Базовые знания C#: Определенно пригодятся некоторые базовые знания о том, как писать и запускать код C#.
4. Пример файла Excel: для тестирования вам понадобится файл Excel, содержащий сводную таблицу.
Как только вы выполните все эти предварительные требования, вы будете готовы приступить к изучению программирования!
## Импортные пакеты
Прежде чем перейти к основной задаче, крайне важно импортировать необходимые пакеты в ваш проект C#. Обязательно включите следующие пространства имен для доступа к функциональности Aspose.Cells:
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
using System;
```
Эти пространства имен содержат все классы и методы, которые мы будем использовать в этом руководстве.
Давайте разобьем нашу задачу на выполнимые шаги. Выполнив эти шаги, вы сможете отключить мастер сводных таблиц, не напрягаясь!
## Шаг 1: Инициализируйте свою среду
Для начала давайте убедимся, что ваша среда разработки готова. Откройте IDE и создайте новый проект C#. Если вы используете Visual Studio, это должно быть просто.
## Шаг 2: Настройте документ Excel
Теперь давайте определим исходный и выходной каталоги для нашего файла Excel. Это то место, куда вы поместите исходный документ, содержащий сводную таблицу, и где будет сохранен измененный документ.
```csharp
// Исходный каталог
string sourceDir = "Your Document Directory";
// Выходной каталог
string outputDir = "Your Document Directory";
```
Обязательно замените `"Your Document Directory"` с фактическим путем к вашим каталогам на вашем компьютере.
## Шаг 3: Загрузите рабочую книгу
Теперь, когда у нас определены наши каталоги, давайте загрузим файл Excel, содержащий сводную таблицу. Мы будем использовать `Workbook` класс из Aspose.Cells для этого.
```csharp
// Откройте файл шаблона, содержащий сводную таблицу.
Workbook wb = new Workbook(sourceDir + "samplePivotTableTest.xlsx");
```
В этой строке мы создаем новый экземпляр `Workbook` класс, который загрузит наш файл Excel. Не забудьте убедиться, что `samplePivotTableTest.xlsx` действительно находится в указанном исходном каталоге.
## Шаг 4: Доступ к сводной таблице
После загрузки рабочей книги нам нужно получить доступ к сводной таблице, которую мы хотим изменить. В большинстве случаев мы будем работать с первым листом (index0), но если ваша сводная таблица находится в другом месте, вы можете соответствующим образом настроить индекс.
```csharp
// Доступ к сводной таблице на первом листе
PivotTable pt = wb.Worksheets[0].PivotTables[0];
```
Этот фрагмент извлекает сводную таблицу из первого рабочего листа. Это как найти книгу, которую вы хотите прочитать в библиотеке!
## Шаг 5: Отключите Мастер сводных таблиц
А теперь самое интересное! Мы отключим мастер для сводной таблицы, установив `EnableWizard` к `false`.
```csharp
// Отключить ленту для этой сводной таблицы
pt.EnableWizard = false;
```
Эта единственная строка кода не позволяет пользователям взаимодействовать с интерфейсом мастера сводной таблицы, обеспечивая более понятный интерфейс при использовании таблицы Excel.
## Шаг 6: Сохраните измененную рабочую книгу.
После внесения изменений пришло время сохранить обновленную книгу. Для этого мы используем следующую строку кода.
```csharp
// Сохранить выходной файл
wb.Save(outputDir + "outputSamplePivotTableTest.xlsx");
```
Эта команда сохранит измененную книгу в указанном выходном каталоге. Теперь у вас есть новый файл Excel без мастера сводных таблиц!
## Шаг 7: Подтвердите изменения
Наконец, давайте сообщим пользователю, что все выполнено успешно. Простое сообщение на консоли сделает свое дело!
```csharp
Console.WriteLine("DisablePivotTableRibbon executed successfully.\r\n");
```
Запуск этого кода даст вам положительный отзыв о том, что ваша задача была успешно выполнена. В конце концов, кто не любит хорошего похлопывания по спине после завершения проекта?
## Заключение
Поздравляем! Вы успешно научились программно отключать ленту сводной таблицы в .NET с помощью библиотеки Aspose.Cells. Этот мощный инструмент не только позволяет вам настраивать функциональность ваших файлов Excel, но и улучшает пользовательский опыт, контролируя, с чем пользователи могут и не могут взаимодействовать. Так что вперед, экспериментируйте с настройками и настраивайте свои файлы Excel как профессионал! Для получения дополнительной информации об Aspose.Cells не забудьте проверить их [документация](https://reference.aspose.com/cells/net/) для более глубокого понимания, поддержки или приобретения лицензии.
## Часто задаваемые вопросы
### Что такое Aspose.Cells?
Aspose.Cells — это библиотека .NET, предназначенная для управления файлами Excel и предлагающая разнообразные функции для работы с файлами Excel.
### Могу ли я использовать Aspose.Cells бесплатно?
Да, вы можете использовать [Бесплатная пробная версия](https://releases.aspose.com/) изучить его особенности, прежде чем принимать решение о покупке.
### Есть ли способ получить поддержку по вопросам Aspose.Cells?
Конечно! Вы можете задать вопросы и получить совет на Aspose [форум](https://forum.aspose.com/c/cells/9).
### Какие типы форматов файлов поддерживает Aspose.Cells?
Aspose.Cells поддерживает множество форматов, включая XLS, XLSX, ODS и многие другие.
### Как я могу получить временную лицензию на Aspose.Cells?
Вы можете получить временную лицензию, посетив [временная страница лицензии](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}