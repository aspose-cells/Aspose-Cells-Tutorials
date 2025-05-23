---
"description": "Автоматизируйте форматирование чисел в Excel с помощью Aspose.Cells для .NET. Узнайте, как применять форматы даты, процентов и валюты программно."
"linktitle": "Использование встроенных числовых форматов в Excel программным способом"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Использование встроенных числовых форматов в Excel программным способом"
"url": "/ru/net/number-and-display-formats-in-excel/using-built-in-number-formats/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Использование встроенных числовых форматов в Excel программным способом

## Введение
В этом руководстве мы покажем вам, как использовать встроенные числовые форматы в Excel с помощью Aspose.Cells для .NET. Мы рассмотрим все, от настройки среды до применения различных форматов, таких как даты, проценты и валюты. Независимо от того, являетесь ли вы опытным профессионалом или только начинаете изучать экосистему .NET, это руководство поможет вам форматировать ячейки Excel с легкостью.
## Предпосылки
Прежде чем приступить к работе, убедитесь, что у вас есть следующее:
- Установлена библиотека Aspose.Cells for .NET. Вы можете [скачать здесь](https://releases.aspose.com/cells/net/).
- Практические знания C# и основ программирования .NET.
- Visual Studio или любая .NET IDE, установленная на вашем компьютере.
- Действующая лицензия Aspose или [временная лицензия](https://purchase.aspose.com/temporary-license/).
- Установлен .NET Framework (версии 4.0 или выше).
  
Если вам не хватает чего-либо из вышеперечисленного, перейдите по предоставленным ссылкам, чтобы все настроить. Готовы? Давайте перейдем к самой интересной части!
## Импортные пакеты
Прежде чем приступить к изучению руководства, обязательно импортируйте необходимые пространства имен для работы с Aspose.Cells для .NET:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
После импорта вы готовы к программной обработке файлов Excel. Теперь давайте перейдем к пошаговому руководству!
## Шаг 1: Создайте или откройте свою книгу Excel
На этом этапе вы создадите новую книгу. Думайте об этом как об открытии нового файла Excel, только вы делаете это через код!
```csharp
// Путь к каталогу документов.
string dataDir = "Your Document Directory";
// Создайте каталог, если его еще нет.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
	System.IO.Directory.CreateDirectory(dataDir);
// Создание объекта Workbook
Workbook workbook = new Workbook();
```
Здесь мы просто создаем новый экземпляр `Workbook` объект. Это действует как ваш файл Excel, готовый к обработке данных. Вы также можете загрузить существующий файл, указав его путь.
## Шаг 2: Доступ к рабочему листу
Книги Excel могут содержать несколько листов. На этом этапе мы получим доступ к первому листу в вашей книге:
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
Теперь мы получаем доступ к первому листу в рабочей книге. Если вам нужно манипулировать дополнительными листами, вы можете ссылаться на них, используя их индекс или имя.
## Шаг 3: Добавьте данные в ячейки
Давайте начнем добавлять некоторые данные в определенные ячейки. Сначала мы вставим текущую системную дату в ячейку "A1":
```csharp
worksheet.Cells["A1"].PutValue(DateTime.Now);
```
Эта строка вставляет текущую дату в ячейку A1. Круто, правда? Представьте, что вы делаете это вручную для сотен ячеек — это был бы кошмар. Теперь перейдем к форматированию!
## Шаг 4: Форматирование даты в ячейке «A1»
Далее, давайте отформатируем эту дату в более читаемом формате, например "15-Oct-24". Вот где Aspose.Cells действительно блистает:
1. Получить стиль ячейки:
```csharp
Style style = worksheet.Cells["A1"].GetStyle();
```
Здесь мы захватываем стиль ячейки A1. Думайте об этом как о захвате «моды» ячейки перед внесением каких-либо изменений.
2. Установите формат даты:
```csharp
style.Number = 15;
```
Установка `Number` свойство 15 применяет желаемый формат даты. Это встроенный код числового формата для отображения дат в формате "д-ммм-гг".
3. Примените стиль к ячейке:
```csharp
worksheet.Cells["A1"].SetStyle(style);
```
Эта строка применяет изменения стиля к ячейке. Теперь вместо формата даты по умолчанию вы увидите что-то гораздо более удобное, например "15-Oct-24".
## Шаг 5: Добавьте и отформатируйте процент в ячейке «A2»
Давайте перейдем к форматированию процентов. Представьте, что вы хотите вставить значение и отобразить его в виде процентов. На этом этапе мы добавим числовое значение в ячейку "A2" и отформатируем его как процент:
1. Вставьте числовое значение:
```csharp
worksheet.Cells["A2"].PutValue(20);
```
Это вставит число 20 в ячейку A2. Вы можете подумать: «Это просто число — как мне превратить его в процент?» Что ж, мы как раз к этому и переходим.
2. Получите стиль и установите процентный формат:
```csharp
style = worksheet.Cells["A2"].GetStyle();
style.Number = 9;  // Форматировать как процент
worksheet.Cells["A2"].SetStyle(style);
    ```
Setting the `Number` property to 9 applies the built-in percentage format. Now the value in A2 will be displayed as "2000%." (Yes, 20 is treated as 2000% in percentage formatting).
## Step 6: Add and Format Currency in Cell "A3"
Now, let’s add a numeric value in cell A3 and format it as currency. This is a common use case for financial reports.
1. Insert Numeric Value:
```csharp
worksheet.Cells["A3"].PutValue(2546);
```
Здесь мы добавляем 2546 к ячейке A3. Далее мы отформатируем это число так, чтобы оно отображалось как денежная единица.
2. Получите стиль и установите формат валюты:
```csharp
style = worksheet.Cells["A3"].GetStyle();
style.Number = 6;  // Форматировать как валюту
worksheet.Cells["A3"].SetStyle(style);
```
Установка `Number` свойство 6 применяет формат валюты. Теперь значение в ячейке A3 будет отображаться как "2,546.00", с запятыми и двумя десятичными знаками.
## Шаг 7: Сохраните файл Excel.
Теперь, когда мы применили всю магию форматирования, пришло время сохранить файл:
```csharp
// Сохранение файла Excel
workbook.Save(dataDir + "book1.out.xls", SaveFormat.Excel97To2003);
```
Эта строка сохраняет файл Excel в формате Excel 97-2003. Вы можете изменить `SaveFormat` в соответствии с вашими потребностями. И вот так вы создали и отформатировали файл Excel программным способом!
## Заключение
Поздравляем! Вы успешно научились использовать Aspose.Cells для .NET для применения встроенных числовых форматов к ячейкам в файле Excel. От дат до процентов и валют — мы рассмотрели некоторые из наиболее распространенных потребностей в форматировании для обработки данных Excel. Теперь вместо ручного форматирования ячеек вы можете автоматизировать весь процесс, что сэкономит вам время и сократит количество ошибок.
## Часто задаваемые вопросы
### Можно ли применять пользовательские числовые форматы с помощью Aspose.Cells для .NET?
Да! В дополнение к встроенным форматам, Aspose.Cells также поддерживает пользовательские числовые форматы. Вы можете создавать узкоспециализированные форматы с помощью `Custom` недвижимость в `Style` сорт.
### Как отформатировать ячейку как валюту с определенным символом?
Чтобы применить определенный символ валюты, вы можете использовать пользовательское форматирование, установив `Style.Custom` свойство.
### Могу ли я форматировать целые строки или столбцы?
Конечно! Вы можете применять стили ко всем строкам или столбцам, используя `Rows` или `Columns` коллекции в `Worksheet` объект.
### Как отформатировать несколько ячеек одновременно?
Вы можете использовать `Range` объект, позволяющий выбрать несколько ячеек и применить стили ко всем ним одновременно.
### Нужно ли устанавливать Microsoft Excel для использования Aspose.Cells?
Нет, Aspose.Cells работает независимо от Microsoft Excel, поэтому вам не нужно устанавливать Excel на вашем компьютере.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}