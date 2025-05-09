---
"description": "Научитесь использовать ICellsDataTableDataSource с Aspose.Cells для .NET для динамического заполнения листов Excel. Идеально подходит для автоматизации данных клиентов в рабочих книгах."
"linktitle": "Используйте ICellsDataTableDataSource для конструктора рабочих книг"
"second_title": "API обработки Excel Aspose.Cells .NET"
"title": "Используйте ICellsDataTableDataSource для конструктора рабочих книг"
"url": "/ru/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Используйте ICellsDataTableDataSource для конструктора рабочих книг

## Введение
Создание расширенных электронных таблиц с автоматизированной интеграцией данных может стать переломным моментом, особенно в бизнес-приложениях. В этом руководстве мы рассмотрим, как использовать `ICellsDataTableDataSource` для дизайнера рабочих книг в Aspose.Cells для .NET. Мы проведем вас через создание простого, понятного человеку решения для динамической загрузки пользовательских данных в файл Excel. Итак, если вы работаете со списками клиентов, данными о продажах или чем-то подобным, это руководство для вас!
## Предпосылки
Для начала убедитесь, что у вас есть следующее:
- Библиотека Aspose.Cells for .NET – ее можно загрузить с сайта [здесь](https://releases.aspose.com/cells/net/) или получите бесплатную пробную версию.
- Среда разработки .NET – Visual Studio – отличный выбор.
- Базовые знания C# – знакомство с классами и обработкой данных поможет вам в дальнейшем изучении.
Прежде чем продолжить, убедитесь, что в вашей среде разработки установлены необходимые пакеты.
## Импортные пакеты
Для эффективного использования Aspose.Cells вам необходимо импортировать необходимые пакеты. Ниже приведен краткий справочник по требуемым пространствам имен:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Шаг 1: Определите класс данных клиента
Для начала создайте простой `Customer` класс. Этот класс будет содержать основные данные о клиенте, такие как `FullName` и `Address`. Думайте об этом как о способе определения «формы» ваших данных.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Шаг 2: Настройка класса списка клиентов
Далее, определите `CustomerList` класс, который расширяет `ArrayList`. Этот настраиваемый список будет содержать экземпляры `Customer` и разрешить индексированный доступ к каждой записи.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
На этом этапе мы преобразуем наши данные в формат, который Aspose.Cells может распознать и обработать.
## Шаг 3: Создание класса источника данных о клиентах
Вот тут-то и начинается самое интересное. Мы создадим `CustomerDataSource` класс реализующий `ICellsDataTable` чтобы сделать наши данные совместимыми с конструктором рабочих книг Aspose.Cells.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
Этот обычай `CustomerDataSource` класс позволяет Aspose.Cells интерпретировать каждый `Customer` объект в виде строки в файле Excel.
## Шаг 4: Инициализация данных клиента
Теперь давайте добавим несколько клиентов в наш список. Здесь мы загружаем данные для записи в рабочую книгу. Не стесняйтесь добавлять больше записей по мере необходимости.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
В этом примере мы работаем с небольшим набором данных. Однако вы можете легко расширить этот список, загрузив данные из базы данных или других источников.
## Шаг 5: Загрузите рабочую книгу
Теперь давайте откроем существующую книгу Excel, содержащую необходимые Smart Markers. Эта книга будет служить нашим шаблоном, а Aspose.Cells динамически заменит Smart Markers данными клиентов.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
Убедитесь, что `"SmartMarker1.xlsx"` содержит заполнители, такие как `&=Customer.FullName` и `&=Customer.Address` где необходимо заполнить данные.
## Шаг 6: Настройка конструктора рабочих книг
Теперь давайте настроим конструктор рабочей книги, чтобы связать наш источник данных о клиентах со смарт-маркерами рабочей книги.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
The `SetDataSource` метод связывает наш `CustomerDataSource` к Smart Markers в рабочей книге. Каждый маркер, помеченный `&=Customer` в Excel теперь будут заменены соответствующими данными о клиентах.
## Шаг 7: Обработка и сохранение рабочей книги
Наконец, давайте обработаем рабочую книгу, чтобы заполнить данные и сохранить результаты.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Этот код запускает обработку Smart Marker, заменяет все заполнители данными и сохраняет результат как `dest.xlsx`.
## Заключение
Поздравляем! Вы успешно внедрили `ICellsDataTableDataSource` для дизайнера рабочих книг, использующего Aspose.Cells для .NET. Этот подход идеально подходит для автоматизации заполнения данных в электронных таблицах, особенно при работе с динамическими данными, такими как списки клиентов или инвентаризации продуктов. С этими навыками вы на верном пути к созданию приложений, управляемых данными, которые делают отчетность на основе Excel легкой!
## Часто задаваемые вопросы
### Что такое `ICellsDataTable` в Aspose.Cells?  
Это интерфейс, позволяющий связывать пользовательские источники данных с интеллектуальными маркерами Aspose.Cells для динамического заполнения данных.
### Как настроить данные в шаблоне рабочей книги?  
Заполнители, называемые умными маркерами, например `&=Customer.FullName`, используются. Эти маркеры заменяются реальными данными в процессе обработки.
### Является ли Aspose.Cells для .NET бесплатным?  
Aspose.Cells предлагает бесплатную пробную версию, но для полного доступа требуется платная лицензия. Проверьте их [бесплатная пробная версия](https://releases.aspose.com/) или [купить](https://purchase.aspose.com/buy) параметры.
### Могу ли я динамически добавлять больше данных о клиентах?  
Конечно! Просто заполните `CustomerList` с дополнительными записями перед запуском программы.
### Где я могу получить помощь, если я застрял?  
У Aspose есть [форум поддержки](https://forum.aspose.com/c/cells/9) где пользователи могут задавать вопросы и получать помощь от сообщества и команды Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}