---
title: استخدم ICellsDataTableDataSource لمصمم المصنفات
linktitle: استخدم ICellsDataTableDataSource لمصمم المصنفات
second_title: واجهة برمجة تطبيقات معالجة Excel الخاصة بـ Aspose.Cells .NET
description: تعلم كيفية استخدام ICellsDataTableDataSource مع Aspose.Cells for .NET لتعبئة جداول Excel بشكل ديناميكي. مثالي لأتمتة بيانات العملاء في المصنفات.
weight: 21
url: /ar/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخدم ICellsDataTableDataSource لمصمم المصنفات

## مقدمة
 إن إنشاء جداول بيانات متقدمة مع تكامل البيانات الآلي يمكن أن يكون بمثابة تغيير كبير، وخاصة في تطبيقات الأعمال. في هذا البرنامج التعليمي، سنتعمق في كيفية استخدام`ICellsDataTableDataSource`لمصمم المصنفات في Aspose.Cells لـ .NET. سنرشدك خلال بناء حل بسيط وسهل القراءة من قبل البشر لتحميل البيانات المخصصة في ملف Excel بشكل ديناميكي. لذا، إذا كنت تعمل مع قوائم العملاء أو بيانات المبيعات أو أي شيء مماثل، فهذا الدليل مناسب لك!
## المتطلبات الأساسية
للبدء، تأكد من توفر ما يلي:
-  مكتبة Aspose.Cells لـ .NET – يمكنك تنزيلها من[هنا](https://releases.aspose.com/cells/net/) أو احصل على نسخة تجريبية مجانية.
- بيئة تطوير .NET – Visual Studio هو خيار رائع.
- الفهم الأساسي لـ C# – التعرف على الفئات ومعالجة البيانات سيساعدك على المتابعة.
قبل أن نستمر، تأكد من إعداد بيئة التطوير الخاصة بك بالحزم اللازمة.
## استيراد الحزم
لاستخدام Aspose.Cells بشكل فعال، تحتاج إلى استيراد الحزم الأساسية. فيما يلي مرجع سريع للمساحات المطلوبة:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## الخطوة 1: تحديد فئة بيانات العميل
 للبدء، قم بإنشاء نموذج بسيط`Customer` الصف. سيحتوي هذا الصف على تفاصيل أساسية عن العملاء مثل`FullName` و`Address`فكر في الأمر باعتباره طريقة لتحديد "شكل" بياناتك.
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
 بعد ذلك، قم بتحديد`CustomerList` الصف الذي يمتد`ArrayList` ستحتوي هذه القائمة المخصصة على حالات`Customer` والسماح بالوصول المفهرس إلى كل إدخال.
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
 وهنا تصبح الأمور مثيرة للاهتمام. سننشئ`CustomerDataSource` تنفيذ الفصل`ICellsDataTable` لجعل بياناتنا متوافقة مع مصمم مصنف Aspose.Cells.
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
 هذه العادة`CustomerDataSource` تتيح الفئة لـ Aspose.Cells تفسير كل`Customer` الكائن كصف في ملف Excel.
## الخطوة 4: تهيئة بيانات العميل
الآن، دعنا نضيف بعض العملاء إلى قائمتنا. هنا نقوم بتحميل البيانات التي سيتم كتابتها في المصنف. لا تتردد في إضافة المزيد من الإدخالات حسب الحاجة.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
في هذا المثال، نعمل على مجموعة بيانات صغيرة. ومع ذلك، يمكنك بسهولة توسيع هذه القائمة عن طريق تحميل البيانات من قاعدة بيانات أو مصادر أخرى.
## الخطوة 5: تحميل المصنف
الآن، لنفتح مصنف Excel موجودًا يحتوي على العلامات الذكية اللازمة. سيعمل هذا المصنف كقالب لنا، وسيقوم Aspose.Cells باستبدال العلامات الذكية ديناميكيًا ببيانات العميل.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 تأكد من ذلك`"SmartMarker1.xlsx"` يحتوي على عناصر نائبة مثل`&=Customer.FullName` و`&=Customer.Address` حيث يجب ملء البيانات.
## الخطوة 6: إعداد مصمم المصنف
الآن، دعنا نقوم بتكوين مصمم المصنف لربط مصدر بيانات العميل الخاص بنا مع العلامات الذكية الموجودة في المصنف.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 ال`SetDataSource` الطريقة تربطنا`CustomerDataSource` إلى العلامات الذكية في المصنف. كل علامة تحمل علامة`&=Customer` سيتم الآن استبدال البيانات الموجودة في Excel ببيانات العميل المقابلة.
## الخطوة 7: معالجة المصنف وحفظه
وأخيرًا، دعنا نعالج المصنف لملء البيانات وحفظ النتائج.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
يؤدي هذا الكود إلى تشغيل معالجة العلامة الذكية، واستبدال جميع العناصر النائبة بالبيانات، وحفظ النتيجة كـ`dest.xlsx`.
## خاتمة
 مبروك! لقد قمت بالتنفيذ بنجاح`ICellsDataTableDataSource` لمصممي المصنفات باستخدام Aspose.Cells لـ .NET. هذا النهج مثالي لأتمتة تعبئة البيانات في جداول البيانات، وخاصة عند التعامل مع البيانات الديناميكية مثل قوائم العملاء أو مخزونات المنتجات. بفضل هذه المهارات، ستكون على الطريق الصحيح لبناء تطبيقات تعتمد على البيانات تجعل إعداد التقارير المستندة إلى Excel أمرًا سهلاً!
## الأسئلة الشائعة
###  ما هو`ICellsDataTable` in Aspose.Cells?  
إنها واجهة تسمح بربط مصادر البيانات المخصصة مع علامات Aspose.Cells الذكية لتعبئة البيانات بشكل ديناميكي.
### كيف يمكنني تخصيص البيانات في قالب المصنف؟  
 العناصر النائبة التي تسمى العلامات الذكية، مثل`&=Customer.FullName`يتم استخدام هذه العلامات، ويتم استبدالها ببيانات حقيقية أثناء المعالجة.
### هل Aspose.Cells لـ .NET مجاني؟  
 يقدم Aspose.Cells نسخة تجريبية مجانية، لكن الوصول الكامل يتطلب ترخيصًا مدفوع الأجر. تحقق من[نسخة تجريبية مجانية](https://releases.aspose.com/) أو[يشتري](https://purchase.aspose.com/buy) خيارات.
### هل يمكنني إضافة المزيد من بيانات العملاء بشكل ديناميكي؟  
 بالتأكيد! ما عليك سوى ملء النموذج`CustomerList`مع إدخالات إضافية قبل تشغيل البرنامج.
### أين يمكنني الحصول على المساعدة إذا واجهت مشكلة؟  
 Aspose لديه[منتدى الدعم](https://forum.aspose.com/c/cells/9) حيث يمكن للمستخدمين طرح الأسئلة والحصول على المساعدة من المجتمع وفريق Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
