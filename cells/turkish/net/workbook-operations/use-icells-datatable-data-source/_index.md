---
title: Çalışma Kitabı Tasarımcısı için ICellsDataTableDataSource'u kullanın
linktitle: Çalışma Kitabı Tasarımcısı için ICellsDataTableDataSource'u kullanın
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Excel sayfalarını dinamik olarak doldurmak için ICellsDataTableDataSource'u Aspose.Cells for .NET ile kullanmayı öğrenin. Çalışma kitaplarındaki müşteri verilerini otomatikleştirmek için mükemmeldir.
weight: 21
url: /tr/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabı Tasarımcısı için ICellsDataTableDataSource'u kullanın

## giriiş
 Otomatik veri entegrasyonuyla gelişmiş elektronik tablolar oluşturmak, özellikle iş uygulamalarında oyunun kurallarını değiştirebilir. Bu eğitimde, nasıl kullanılacağına derinlemesine ineceğiz`ICellsDataTableDataSource`Aspose.Cells for .NET'te bir çalışma kitabı tasarımcısı için. Özel verileri bir Excel dosyasına dinamik olarak yüklemek için basit, insan tarafından okunabilir bir çözüm oluşturma konusunda size yol göstereceğiz. Yani, müşteri listeleri, satış verileri veya benzeri bir şeyle çalışıyorsanız, bu kılavuz tam size göre!
## Ön koşullar
Başlamak için aşağıdakilere sahip olduğunuzdan emin olun:
-  Aspose.Cells for .NET Kütüphanesi – Buradan indirebilirsiniz[Burada](https://releases.aspose.com/cells/net/) veya ücretsiz deneme sürümünü edinin.
- .NET Geliştirme Ortamı – Visual Studio harika bir seçimdir.
- C# Temel Anlayışı – Sınıflar ve veri işleme konusunda bilgi sahibi olmak, takip etmenize yardımcı olacaktır.
Devam etmeden önce, geliştirme ortamınızın gerekli paketlerle kurulduğundan emin olun.
## Paketleri İçe Aktar
Aspose.Cells'i etkili bir şekilde kullanmak için, temel paketleri içe aktarmanız gerekir. Aşağıda gerekli ad alanları için hızlı bir referans verilmiştir:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Adım 1: Müşteri Veri Sınıfını Tanımlayın
 Başlamak için basit bir tane oluşturun`Customer` sınıf. Bu sınıf, aşağıdaki gibi temel müşteri ayrıntılarını içerecektir:`FullName` Ve`Address`Bunu verilerinizin "şeklini" tanımlamanın bir yolu olarak düşünün.
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
## Adım 2: Müşteri Listesi Sınıfını Ayarlayın
 Sonra, bir tanımlayın`CustomerList` genişleyen sınıf`ArrayList` Bu özelleştirilmiş liste, şu örnekleri tutacaktır:`Customer` ve her girdiye indeksli erişime izin verin.
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
Bu adımda, verilerimizi Aspose.Cells'in tanıyabileceği ve işleyebileceği bir biçime dönüştürüyoruz.
## Adım 3: Müşteri Veri Kaynağı Sınıfını Oluşturun
 İşte işler burada ilginçleşiyor. Bir tane yaratacağız`CustomerDataSource` sınıf uygulaması`ICellsDataTable` Verilerimizi Aspose.Cells'in çalışma kitabı tasarımcısıyla uyumlu hale getirmek.
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
 Bu gelenek`CustomerDataSource` sınıf, Aspose.Cells'in her bir hücreyi yorumlamasını mümkün kılar`Customer` Excel dosyasında bir satır olarak nesne.
## Adım 4: Müşteri Verilerini Başlatın
Şimdi listemize birkaç müşteri ekleyelim. İşte çalışma kitabına yazılacak verileri yüklediğimiz yer. Gerektiğinde daha fazla girdi eklemekten çekinmeyin.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Bu örnekte küçük bir veri kümesiyle çalışıyoruz. Ancak, bir veritabanından veya diğer kaynaklardan veri yükleyerek bu listeyi kolayca genişletebilirsiniz.
## Adım 5: Çalışma Kitabını Yükleyin
Şimdi, gerekli Akıllı İşaretleyicileri içeren mevcut bir Excel çalışma kitabını açalım. Bu çalışma kitabı şablonumuz olarak hizmet edecek ve Aspose.Cells, Akıllı İşaretleyicileri dinamik olarak müşteri verileriyle değiştirecek.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Emin olun ki`"SmartMarker1.xlsx"` gibi yer tutucular içerir`&=Customer.FullName` Ve`&=Customer.Address` verilerin doldurulacağı yer.
## Adım 6: Çalışma Kitabı Tasarımcısını Ayarlayın
Şimdi, çalışma kitabı tasarımcısını müşteri veri kaynağımızı çalışma kitabının Akıllı İşaretleyicileriyle bağlayacak şekilde yapılandıralım.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 The`SetDataSource` yöntem bizim`CustomerDataSource` çalışma kitabındaki Akıllı İşaretleyicilere. Her işaretleyici etiketlendi`&=Customer` Excel'deki veriler artık ilgili müşteri verileriyle değiştirilecek.
## Adım 7: Çalışma Kitabını İşleyin ve Kaydedin
Son olarak çalışma kitabını işleyip verileri dolduralım ve sonuçları kaydedelim.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Bu kod Akıllı İşaretleyici işlemini tetikler, tüm yer tutucuları verilerle değiştirir ve sonucu şu şekilde kaydeder:`dest.xlsx`.
## Çözüm
 Tebrikler! Başarıyla uyguladınız`ICellsDataTableDataSource` Aspose.Cells for .NET kullanan bir çalışma kitabı tasarımcısı için. Bu yaklaşım, özellikle müşteri listeleri veya ürün envanterleri gibi dinamik verilerle uğraşırken, elektronik tablolardaki veri doldurmayı otomatikleştirmek için idealdir. Bu becerilerle, Excel tabanlı raporlamayı çocuk oyuncağı haline getiren veri odaklı uygulamalar oluşturma yolunda iyi bir mesafe kat etmiş olursunuz!
## SSS
###  Nedir?`ICellsDataTable` in Aspose.Cells?  
Dinamik veri popülasyonu için özel veri kaynaklarının Aspose.Cells Akıllı İşaretleyicileri ile bağlanmasına olanak tanıyan bir arayüzdür.
### Çalışma kitabı şablonundaki verileri nasıl özelleştirebilirim?  
 Akıllı İşaretleyiciler adı verilen yer tutucular, örneğin:`&=Customer.FullName`, kullanılır. Bu işaretleyiciler işleme sırasında gerçek verilerle değiştirilir.
### Aspose.Cells for .NET ücretsiz mi?  
 Aspose.Cells ücretsiz deneme sunuyor ancak tam erişim için ücretli lisans gerekiyor. Kontrol edin[ücretsiz deneme](https://releases.aspose.com/) veya[satın almak](https://purchase.aspose.com/buy) seçenekler.
### Daha fazla müşteri verisini dinamik olarak ekleyebilir miyim?  
 Kesinlikle! Sadece doldurun`CustomerList`Programı çalıştırmadan önce ek girdilerle.
### Sıkışırsam nereden yardım alabilirim?  
 Aspose'un bir[destek forumu](https://forum.aspose.com/c/cells/9) Kullanıcıların soru sorabilecekleri ve topluluktan ve Aspose ekibinden yardım alabilecekleri bir yer.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
