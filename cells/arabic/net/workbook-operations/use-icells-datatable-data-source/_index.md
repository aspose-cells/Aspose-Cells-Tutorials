---
"description": "تعلم كيفية استخدام ICellsDataTableDataSource مع Aspose.Cells لـ .NET لتعبئة جداول بيانات Excel ديناميكيًا. مثالي لأتمتة بيانات العملاء في المصنفات."
"linktitle": "استخدم ICellsDataTableDataSource لمصمم المصنفات"
"second_title": "واجهة برمجة تطبيقات معالجة Excel Aspose.Cells .NET"
"title": "استخدم ICellsDataTableDataSource لمصمم المصنفات"
"url": "/ar/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# استخدم ICellsDataTableDataSource لمصمم المصنفات

## مقدمة
إنشاء جداول بيانات متقدمة مع تكامل بيانات آلي يُحدث نقلة نوعية، خاصةً في تطبيقات الأعمال. في هذا البرنامج التعليمي، سنتعمق في كيفية استخدام `ICellsDataTableDataSource` لمصمم مصنفات في Aspose.Cells لـ .NET. سنرشدك خلال بناء حل بسيط وسهل القراءة لتحميل بيانات مخصصة إلى ملف Excel ديناميكيًا. لذا، إذا كنت تعمل مع قوائم العملاء أو بيانات المبيعات أو أي شيء مشابه، فهذا الدليل مناسب لك!
## المتطلبات الأساسية
للبدء، تأكد من أن لديك ما يلي:
- مكتبة Aspose.Cells لـ .NET – يمكنك تنزيلها من [هنا](https://releases.aspose.com/cells/net/) أو احصل على نسخة تجريبية مجانية.
- بيئة تطوير .NET – Visual Studio هو خيار رائع.
- الفهم الأساسي لـ C# – إن الإلمام بالفئات ومعالجة البيانات سيساعدك على المتابعة.
قبل أن نستمر، تأكد من إعداد بيئة التطوير الخاصة بك بالحزم الضرورية.
## استيراد الحزم
لاستخدام Aspose.Cells بفعالية، عليك استيراد الحزم الأساسية. فيما يلي مرجع سريع لمساحات الأسماء المطلوبة:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## الخطوة 1: تحديد فئة بيانات العميل
للبدء، قم بإنشاء نموذج بسيط `Customer` الصف. سيحتوي هذا الصف على تفاصيل العملاء الأساسية مثل `FullName` و `Address`فكر في الأمر باعتباره طريقة لتحديد "شكل" بياناتك.
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
## الخطوة 2: إعداد فئة قائمة العملاء
بعد ذلك، قم بتعريف `CustomerList` الفئة التي تمتد `ArrayList`ستحتوي هذه القائمة المخصصة على حالات من `Customer` والسماح بالوصول المفهرس إلى كل إدخال.
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
في هذه الخطوة، نقوم بتغليف بياناتنا في تنسيق يمكن لـ Aspose.Cells التعرف عليه ومعالجته.
## الخطوة 3: إنشاء فئة مصدر بيانات العميل
هنا تصبح الأمور مثيرة للاهتمام. سننشئ `CustomerDataSource` تنفيذ الفصل `ICellsDataTable` لجعل بياناتنا متوافقة مع مصمم مصنف Aspose.Cells.
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
هذه العادة `CustomerDataSource` تتيح الفئة لـ Aspose.Cells تفسير كل `Customer` الكائن كصف في ملف Excel.
## الخطوة 4: تهيئة بيانات العميل
الآن، لنُضِف بعض العملاء إلى قائمتنا. هنا نُحمِّل البيانات المراد كتابتها في المصنف. لا تتردد في إضافة المزيد من الإدخالات حسب الحاجة.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
في هذا المثال، نعمل على مجموعة بيانات صغيرة. مع ذلك، يمكنك بسهولة توسيع هذه القائمة بتحميل البيانات من قاعدة بيانات أو مصادر أخرى.
## الخطوة 5: تحميل المصنف
الآن، لنفتح مصنف Excel موجودًا يحتوي على العلامات الذكية اللازمة. سيُستخدم هذا المصنف كقالب لنا، وسيستبدل Aspose.Cells العلامات الذكية ديناميكيًا ببيانات العميل.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
تأكد من ذلك `"SmartMarker1.xlsx"` يحتوي على عناصر نائبة مثل `&=Customer.FullName` و `&=Customer.Address` حيث يجب ملء البيانات.
## الخطوة 6: إعداد مصمم المصنف
الآن، دعنا نقوم بتكوين مصمم المصنف لربط مصدر بيانات العميل الخاص بنا بالعلامات الذكية الموجودة في المصنف.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
ال `SetDataSource` الطريقة تربطنا `CustomerDataSource` إلى العلامات الذكية في مصنف العمل. كل علامة مُسمّاة `&=Customer` سيتم الآن استبدال البيانات الموجودة في Excel ببيانات العميل المقابلة.
## الخطوة 7: معالجة المصنف وحفظه
وأخيرًا، دعنا نعالج المصنف لملء البيانات وحفظ النتائج.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
يؤدي هذا الكود إلى تشغيل معالجة العلامة الذكية، واستبدال جميع العناصر النائبة بالبيانات، وحفظ النتيجة باسم `dest.xlsx`.
## خاتمة
مبروك! لقد نجحت في التنفيذ `ICellsDataTableDataSource` لمصممي المصنفات باستخدام Aspose.Cells لـ .NET. يُعد هذا النهج مثاليًا لأتمتة تعبئة البيانات في جداول البيانات، خاصةً عند التعامل مع بيانات ديناميكية مثل قوائم العملاء أو مخزونات المنتجات. بفضل هذه المهارات، ستكون على الطريق الصحيح لبناء تطبيقات قائمة على البيانات تُسهّل إعداد التقارير باستخدام Excel!
## الأسئلة الشائعة
### ما هو `ICellsDataTable` في Aspose.Cells؟  
إنها واجهة تسمح بربط مصادر البيانات المخصصة مع علامات Aspose.Cells الذكية لتعبئة البيانات بشكل ديناميكي.
### كيف يمكنني تخصيص البيانات في قالب المصنف؟  
العناصر النائبة التي تسمى العلامات الذكية، مثل `&=Customer.FullName`يتم استخدام هذه العلامات. يتم استبدال هذه العلامات ببيانات حقيقية أثناء المعالجة.
### هل Aspose.Cells لـ .NET مجاني؟  
يقدم Aspose.Cells نسخة تجريبية مجانية، لكن الوصول الكامل يتطلب ترخيصًا مدفوعًا. تحقق من [نسخة تجريبية مجانية](https://releases.aspose.com/) أو [يشتري](https://purchase.aspose.com/buy) خيارات.
### هل يمكنني إضافة المزيد من بيانات العملاء بشكل ديناميكي؟  
بالتأكيد! ببساطة املأ الفراغات `CustomerList` مع إدخالات إضافية قبل تشغيل البرنامج.
### أين يمكنني الحصول على المساعدة إذا كنت عالقًا؟  
Aspose لديه [منتدى الدعم](https://forum.aspose.com/c/cells/9) حيث يمكن للمستخدمين طرح الأسئلة والحصول على المساعدة من المجتمع وفريق Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}