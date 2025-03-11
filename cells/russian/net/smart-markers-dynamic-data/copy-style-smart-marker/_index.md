---
title: Копировать стиль с помощью смарт-маркера в Aspose.Cells .NET
linktitle: Копировать стиль с помощью смарт-маркера в Aspose.Cells .NET
second_title: API обработки Excel Aspose.Cells .NET
description: Легко копируйте стили и форматы из файла шаблона в сгенерированный вами вывод Excel. Это всеобъемлющее руководство проведет вас через пошаговый процесс.
weight: 12
url: /ru/net/smart-markers-dynamic-data/copy-style-smart-marker/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Копировать стиль с помощью смарт-маркера в Aspose.Cells .NET

## Введение
В мире управления данными и обработки электронных таблиц Aspose.Cells для .NET — это мощный инструмент, позволяющий разработчикам создавать, изменять и экспортировать файлы Excel программным способом. Одной из выдающихся особенностей Aspose.Cells является его способность работать с интеллектуальными маркерами, что позволяет разработчикам легко копировать стили и форматы из файла шаблона в сгенерированный вывод. Это руководство проведет вас через процесс использования Aspose.Cells для копирования стилей из файла шаблона и применения их к сгенерированному файлу Excel.
## Предпосылки
Прежде чем начать, убедитесь, что выполнены следующие требования:
1.  Aspose.Cells для .NET: Вы можете загрузить последнюю версию Aspose.Cells для .NET с сайта[Сайт Aspose](https://releases.aspose.com/cells/net/).
2. Microsoft Visual Studio: для написания и запуска кода C# вам понадобится версия Microsoft Visual Studio.
3. Базовые знания C# и .NET: у вас должно быть базовое понимание языка программирования C# и платформы .NET.
## Импортные пакеты
Для начала вам нужно импортировать необходимые пакеты из Aspose.Cells for .NET. Добавьте следующие операторы using в начало вашего файла C#:
```csharp
using System.IO;
using Aspose.Cells;
using System.Data;
```
## Создать источник данных
 Давайте начнем с создания образца источника данных, который мы будем использовать для заполнения нашего файла Excel. В этом примере мы создадим`DataTable` называется`dtStudent` с двумя столбцами: «Имя» и «Возраст».
```csharp
// Путь к каталогу документов.
string dataDir = "Your Document Directory";
// Создать таблицу данных студентов
DataTable dtStudent = new DataTable("Student");
// Определите поле в нем
DataColumn dcName = new DataColumn("Name", typeof(string));
dtStudent.Columns.Add(dcName);
dtStudent.Columns.Add(new DataColumn("Age", typeof(int)));
// Добавьте к нему три строки.
DataRow drName1 = dtStudent.NewRow();
DataRow drName2 = dtStudent.NewRow();
DataRow drName3 = dtStudent.NewRow();
drName1["Name"] = "John";
drName1["Age"] = 23;
drName2["Name"] = "Jack";
drName2["Age"] = 24;
drName3["Name"] = "James";
drName3["Age"] = 32;
dtStudent.Rows.Add(drName1);
dtStudent.Rows.Add(drName2);
dtStudent.Rows.Add(drName3);
```
## Загрузить файл шаблона
 Далее мы загрузим файл шаблона Excel, содержащий стили, которые мы хотим скопировать. В этом примере мы предположим, что файл шаблона называется "Template.xlsx" и находится в`dataDir` каталог.
```csharp
string filePath = dataDir + "Template.xlsx";
// Создайте рабочую книгу из файла шаблона Smart Markers
Workbook workbook = new Workbook(filePath);
```
## Создать экземпляр WorkbookDesigner
 Теперь мы создадим`WorkbookDesigner` экземпляр, который будет использоваться для обработки смарт-маркеров в файле шаблона.
```csharp
// Создать новый экземпляр WorkbookDesigner
WorkbookDesigner designer = new WorkbookDesigner();
// Укажите рабочую книгу
designer.Workbook = workbook;
```
## Установить источник данных
 Затем мы установим источник данных для`WorkbookDesigner` пример, который является`dtStudent` `DataTable` мы создали ранее.
```csharp
// Установить источник данных
designer.SetDataSource(dtStudent);
```
## Обработка смарт-маркеров
 Далее мы позвоним`Process()` метод обработки смарт-маркеров в файле шаблона.
```csharp
// Обработка смарт-маркеров
designer.Process();
```
## Сохраните файл Excel
Наконец, сохраним созданный файл Excel со скопированными стилями.
```csharp
// Сохраните файл Excel.
workbook.Save(dataDir + "output.xlsx", SaveFormat.Xlsx);
```
Вот и все! Вы успешно использовали Aspose.Cells для .NET для копирования стилей из файла шаблона и применили их к сгенерированному вами файлу Excel.
## Заключение
В этом уроке вы узнали, как использовать Aspose.Cells для .NET для копирования стилей из файла шаблона и применения их к сгенерированному файлу Excel. Используя возможности интеллектуальных маркеров, вы можете оптимизировать процесс генерации Excel и обеспечить единообразный вид и восприятие во всех ваших электронных таблицах.
## Часто задаваемые вопросы
###  Какова цель`WorkbookDesigner` class in Aspose.Cells for .NET?
 The`WorkbookDesigner` класс в Aspose.Cells для .NET используется для обработки смарт-маркеров в файле шаблона и их применения к сгенерированному файлу Excel. Он позволяет разработчикам легко копировать стили, форматы и другие атрибуты из шаблона в вывод.
###  Могу ли я использовать Aspose.Cells для .NET с другими источниками данных, кроме`DataTable`?
 Да, вы можете использовать Aspose.Cells для .NET с различными источниками данных, такими как`DataSet`, `IEnumerable`или пользовательские объекты данных.`SetDataSource()` Метод`WorkbookDesigner` класс может принимать различные типы источников данных.
### Как настроить стили и форматы в файле шаблона?
Вы можете настроить стили и форматы в файле шаблона с помощью Microsoft Excel или других инструментов. Aspose.Cells for .NET затем скопирует эти стили и форматы в сгенерированный файл Excel, что позволит вам поддерживать единообразный вид и стиль во всех ваших электронных таблицах.
### Есть ли способ обработки ошибок или исключений, которые могут возникнуть в ходе процесса?
Да, вы можете использовать блоки try-catch для обработки любых исключений, которые могут возникнуть во время процесса. Aspose.Cells для .NET предоставляет подробные сообщения об исключениях, которые могут помочь вам устранить любые проблемы.
### Могу ли я использовать Aspose.Cells для .NET в производственной среде?
 Да, Aspose.Cells for .NET — это коммерческий продукт, который широко используется в производственных средах. Он обеспечивает надежное и прочное решение для программной работы с файлами Excel. Вы можете приобрести[лицензия](https://purchase.aspose.com/buy)или попробуйте[бесплатная пробная версия](https://releases.aspose.com/) для оценки возможностей продукта.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
