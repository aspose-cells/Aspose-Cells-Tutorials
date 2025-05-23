---
"description": "Узнайте, как сохранять сводные таблицы в формате ODS с помощью Aspose.Cells для .NET, следуя этому пошаговому руководству."
"linktitle": "Сохранение сводной таблицы в формате ODS программным способом в .NET"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Сохранение сводной таблицы в формате ODS программным способом в .NET"
"url": "/ru/net/creating-and-configuring-pivot-tables/saving-in-ods-format/"
"weight": 25
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Сохранение сводной таблицы в формате ODS программным способом в .NET

## Введение
Когда дело доходит до управления данными в электронных таблицах, ничто не сравнится с мощью сводных таблиц. Это инструмент для обобщения, анализа и представления сложных наборов данных. Сегодня мы углубимся в использование Aspose.Cells для .NET для сохранения сводной таблицы в формате ODS. Независимо от того, являетесь ли вы опытным разработчиком или только знакомитесь с .NET, это руководство покажется вам простым. 
Давайте начнем!
## Предпосылки
Прежде чем мы перейдем к коду, вам понадобится несколько основных вещей:
### 1. Базовые знания .NET
Базовые знания .NET и концепций программирования помогут вам легко усвоить материал.
### 2. Aspose.Cells для .NET
Вам понадобится установленный Aspose.Cells for .NET. Вы можете скачать его с сайта [Страница релизов Aspose](https://releases.aspose.com/cells/net/). Также доступна пробная версия. [здесь](https://releases.aspose.com/).
### 3. Среда разработки
Убедитесь, что у вас есть IDE, например Visual Studio, в которой вы можете писать и тестировать свой код .NET.
### 4. Немного терпения
Как и в любом деле кодирования, терпение — ключ. Не волнуйтесь, если что-то не получится идеально с первого раза; отладка — часть процесса.
## Импортные пакеты
Для работы с Aspose.Cells вам нужно будет импортировать необходимые пространства имен. Добавьте следующую директиву using в начало вашего файла кода:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Эта строка позволяет получить доступ ко всем функциям библиотеки Aspose.Cells, что упрощает процесс кодирования.
Теперь давайте разобьем процесс на управляемые этапы.
## Шаг 1: Настройте выходной каталог
Сначала вам нужно определить, где вы хотите сохранить свой ODS-файл. Это простое назначение пути к каталогу.
```csharp
string outputDir = "Your Document Directory";
```
В этой строке замените `"Your Document Directory"` на путь, по которому вы хотите сохранить файл.
## Шаг 2: Создайте новую рабочую книгу
Далее вы создадите новый объект Workbook, который будет содержать все ваши данные и структуры, включая сводную таблицу.
```csharp
Workbook workbook = new Workbook();
```
Здесь вы, по сути, начинаете с чистого листа — представьте себе чистый холст, на котором вы создадите свой шедевр.
## Шаг 3: Доступ к рабочему листу
Теперь, когда у нас есть рабочая книга, нам нужно приступить к работе над нашим рабочим листом. Aspose.Cells позволяет вам легко получить доступ к первому доступному рабочему листу.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
Эта строка переносит нас на самый первый лист, готовый к вводу данных.
## Шаг 4: Заполнение ячеек данными
Пришло время заполнить наш рабочий лист данными. Мы будем использовать простой пример данных о продажах в спорте. 
Вот как можно задать значения в различных ячейках:
```csharp
Cells cells = sheet.Cells;
cells["A1"].PutValue("Sport");
cells["B1"].PutValue("Quarter");
cells["C1"].PutValue("Sales");
cells["A2"].PutValue("Golf");
cells["A3"].PutValue("Golf");
cells["A4"].PutValue("Tennis");
cells["A5"].PutValue("Tennis");
cells["A6"].PutValue("Tennis");
cells["A7"].PutValue("Tennis");
cells["A8"].PutValue("Golf");
cells["B2"].PutValue("Qtr3");
cells["B3"].PutValue("Qtr4");
cells["B4"].PutValue("Qtr3");
cells["B5"].PutValue("Qtr4");
cells["B6"].PutValue("Qtr3");
cells["B7"].PutValue("Qtr4");
cells["B8"].PutValue("Qtr3");
cells["C2"].PutValue(1500);
cells["C3"].PutValue(2000);
cells["C4"].PutValue(600);
cells["C5"].PutValue(1500);
cells["C6"].PutValue(4070);
cells["C7"].PutValue(5000);
cells["C8"].PutValue(6430);
```
В этих строках мы определяем заголовки и заполняем данные о продажах. Подумайте об этом шаге как о заполнении кладовой перед приготовлением еды: чем лучше ваши ингредиенты (данные), тем лучше ваша еда (анализ).
## Шаг 5: Создайте сводную таблицу
Теперь самое интересное — создание сводной таблицы! Вот как добавить ее на свой рабочий лист:
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
// Добавление сводной таблицы на рабочий лист
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
В этом фрагменте мы указываем диапазон данных для сводной таблицы и место ее размещения на рабочем листе. Диапазон данных `=A1:C8` охватывает область, где существуют наши данные.
## Шаг 6: Настройте сводную таблицу
Далее вам нужно настроить сводную таблицу в соответствии с вашими потребностями. Это включает в себя контроль того, что отображается, как это категоризируется и как она вычисляет данные.
```csharp
PivotTable pivotTable = pivotTables[index];
// Скрытие общих итогов по строкам.
pivotTable.RowGrand = false;
// Перетаскиваем первое поле в область строки.
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// Перетаскиваем второе поле в область столбцов.
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// Перетаскиваем третье поле в область данных.
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
Здесь вы решаете, какие поля данных суммировать и как их следует представлять. Это как сервировка стола для званого ужина: вы решаете, что лучше всего подходит и как это представить.
## Шаг 7: Сохраните свою рабочую книгу
Наконец, вы готовы сохранить свою работу в желаемом формате ODS. Вот как это сделать:
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
На этом этапе вы завершаете свой проект и сохраняете его в выбранном вами каталоге — это приятное завершение!
## Шаг 8: Проверьте вывод
Наконец, всегда полезно проверить, успешно ли завершился процесс. Вы можете добавить простое сообщение в консоль:
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
Это сообщение появится на вашей консоли, чтобы подтвердить, что все прошло без сучка и задоринки. Прямо как шеф-повар, проверяющий, все ли приготовлено идеально перед подачей!
## Заключение 
И вот оно! Вы не только создали сводную таблицу с помощью Aspose.Cells, но и сохранили ее в формате ODS. Это руководство провело вас через каждый шаг, гарантируя, что вы вооружены знаниями и уверенностью для решения подобных задач в будущем.
## Часто задаваемые вопросы
### Что такое Aspose.Cells?
Aspose.Cells — это сложная библиотека, позволяющая создавать и обрабатывать файлы Excel в приложениях .NET.
### Могу ли я использовать Aspose.Cells бесплатно?
Да, вы можете загрузить бесплатную пробную версию с сайта [Сайт Aspose](https://releases.aspose.com/).
### Какие форматы поддерживает Aspose.Cells?
Поддерживает множество форматов, включая XLSX, XLS, ODS, PDF и многие другие.
### Как получить поддержку по Aspose.Cells?
Помощь вы можете найти на [Форум поддержки Aspose](https://forum.aspose.com/c/cells/9).
### Есть ли временная лицензия?
Да, вы можете подать заявку на временную лицензию через сайт Aspose. [здесь](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}