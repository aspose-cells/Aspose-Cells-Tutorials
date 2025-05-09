---
"description": "Aspose.Cells for .NET kullanarak bir Excel çalışma sayfasına liste kutusu eklemeyi öğrenin. Kolay, adım adım kılavuzumuzu izleyin ve Excel sayfalarınızı etkileşimli hale getirin."
"linktitle": "Excel'de Çalışma Sayfasına Liste Kutusu Ekleme"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Çalışma Sayfasına Liste Kutusu Ekleme"
"url": "/tr/net/excel-shapes-controls/add-list-box-to-worksheet-excel/"
"weight": 20
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Çalışma Sayfasına Liste Kutusu Ekleme

## giriiş
Excel çalışma sayfalarınıza liste kutusu gibi etkileşimli öğeler eklemek, veri yönetimini ve sunumunu önemli ölçüde iyileştirebilir. İster etkileşimli bir form ister özel bir veri girişi aracı oluşturuyor olun, bir liste kutusuyla kullanıcı girdisini kontrol etme yeteneği paha biçilemezdir. Aspose.Cells for .NET, Excel dosyalarınıza bu kontrolleri eklemek ve yönetmek için etkili bir yol sağlar. Bu kılavuzda, Aspose.Cells for .NET kullanarak bir çalışma sayfasına liste kutusu ekleme sürecini adım adım anlatacağız.
## Ön koşullar
Kodlamaya başlamadan önce aşağıdaki araç ve kaynaklara sahip olduğunuzdan emin olun:
- Aspose.Cells for .NET Kütüphanesi: Bunu şu adresten indirebilirsiniz: [Aspose.Cells for .NET indirme sayfası](https://releases.aspose.com/cells/net/).
- Geliştirme Ortamı: Visual Studio gibi .NET geliştirmeyi destekleyen herhangi bir IDE.
- .NET Framework: Projenizin desteklenen bir .NET framework sürümünü hedeflediğinden emin olun.
Ayrıca, bir tane edinmeyi düşünün [geçici lisans](https://purchase.aspose.com/temporary-license/) Eğer tüm özellikleri sınırsızca keşfetmek istiyorsanız.
## Paketleri İçe Aktar
Başlamadan önce, gerekli Aspose.Cells ad alanlarını içe aktardığınızdan emin olun. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
Bu eğitimde, bir liste kutusu ekleme sürecini birden fazla basit adıma böleceğiz. Her şeyin beklendiği gibi çalıştığından emin olmak için her adımı yakından takip edin.
## Adım 1: Belge Dizininizi Ayarlama
Herhangi bir Excel dosyası oluşturmadan önce, onu kaydedeceğiniz bir konuma ihtiyacınız var. Dizini ayarlama yöntemi şu şekildedir:
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
Bu adımda, dosyanızın nerede saklanacağını tanımlıyorsunuz. Kod, dizinin var olup olmadığını kontrol eder ve yoksa sizin için bir tane oluşturur. Bu, daha sonra herhangi bir "dosya bulunamadı" hatasıyla karşılaşmamanızı sağlar.
## Adım 2: Yeni bir Çalışma Kitabı Oluşturun ve İlk Çalışma Sayfasına Erişin
Daha sonra yeni bir çalışma kitabı oluşturacağız ve liste kutumuzu ekleyeceğimiz ilk çalışma sayfasına ulaşacağız.
```csharp
// Yeni bir Çalışma Kitabı oluşturun.
Workbook workbook = new Workbook();
// İlk çalışma kağıdını al.
Worksheet sheet = workbook.Worksheets[0];
```
Bir çalışma kitabı esasen Excel dosyanızdır. Burada yeni bir çalışma kitabı oluşturuyoruz ve liste kutumuzu yerleştireceğimiz ilk çalışma sayfasına erişiyoruz. Bunu, kontrolleri boyayacağınız boş bir tuval oluşturmak olarak düşünün.
## Adım 3: Liste Kutusu için Veri Girişi
Liste kutusunu eklemeden önce, liste kutusunun referans alacağı bazı verileri doldurmamız gerekiyor.
```csharp
// Çalışma sayfası hücre koleksiyonunu alın.
Cells cells = sheet.Cells;
// Etiket için bir değer girin.
cells["B3"].PutValue("Choose Dept:");
// Etiketi kalın olarak ayarlayın.
cells["B3"].GetStyle().Font.IsBold = true;
// Liste kutusu için giriş değerleri.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
Burada, çalışma sayfasına biraz metin ekliyoruz. "Bölüm Seç:" etiketi B3 hücresine yerleştirilir ve yazı tipi kalın olarak ayarlanır. A sütununa, liste kutumuz için giriş aralığı olarak hizmet edecek ve farklı departmanları temsil edecek değerler ekliyoruz. Bu giriş aralığı, kullanıcıların liste kutusuyla etkileşime girerken seçecekleri şeydir.
## Adım 4: Liste Kutusunu Çalışma Sayfasına Ekleyin
Artık verileri ayarladığımıza göre, liste kutusu denetimini ekleyelim.
```csharp
// Yeni bir liste kutusu ekleyin.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
Bu kod liste kutusunu çalışma sayfasına ekler. Parametreler liste kutusunun konumunu ve boyutunu tanımlar. Liste kutusu satır 2, sütun 0'a 122 genişliğinde ve 100 yüksekliğinde yerleştirilir. Bunlar liste kutusunun çalışma sayfasında nerede görüneceğini belirleyen koordinatlar ve boyuttur.
## Adım 5: Liste Kutusu Özelliklerini Ayarlayın
Şimdi liste kutusunun tam işlevsel olabilmesi için çeşitli özellikler ayarlayacağız.
```csharp
// Yerleşim türünü ayarlayın.
listBox.Placement = PlacementType.FreeFloating;
// Bağlantılı hücreyi ayarla.
listBox.LinkedCell = "A1";
// Giriş aralığını ayarlayın.
listBox.InputRange = "A2:A7";
// Seçim türünü ayarlayın.
listBox.SelectionType = SelectionType.Single;
// Liste kutusunu 3 boyutlu gölgelendirme ile ayarlayın.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: Bu özellik, çalışma sayfası nasıl değiştirilirse değiştirilsin liste kutusunun konumunda kalmasını sağlar.
- LinkedCell: Bu, liste kutusundan seçilen değerin görüntüleneceği hücreyi (bu durumda A1) ayarlar.
- InputRange: Bu, liste kutusuna seçenekler listesinin nerede aranacağını söyler (daha önce belirlediğimiz A2'den A7'ye kadar).
- SelectionType.Single: Bu, kullanıcının liste kutusundan yalnızca bir öğe seçmesini sınırlar.
- Gölge: Gölge efekti, liste kutusuna daha üç boyutlu bir görünüm kazandırarak görsel olarak daha çekici hale getirir.
## Adım 6: Excel Dosyasını Kaydedin
Son olarak çalışma kitabımızı liste kutusu da dahil olacak şekilde kaydedelim.
```csharp
// Çalışma kitabını kaydedin.
workbook.Save(dataDir + "book1.out.xls");
```
Bu kod satırı çalışma kitabını daha önce kurduğumuz dizine kaydeder. Dosyanın adı "book1.out.xls"dir ancak projenize uygun herhangi bir adı seçebilirsiniz.
## Çözüm
İşte karşınızda! Aspose.Cells for .NET kullanarak bir Excel çalışma sayfasına başarıyla bir liste kutusu eklediniz. Sadece birkaç satır kodla, çalışma sayfasını daha etkileşimli ve dinamik hale getiren tam işlevli bir liste kutusu oluşturduk. Bu eğitim, Aspose.Cells for .NET'teki diğer denetimleri ve özellikleri keşfetmeniz için size sağlam bir temel sağlamalıdır. Denemeye devam edin ve yakında, kütüphanenin geniş işlevselliğinde ustalaşacaksınız!
## SSS
### Liste kutusunda birden fazla seçim yapılmasına izin verebilir miyim?  
Evet, değiştirebilirsiniz `SelectionType` ile `SelectionType.Multi` çoklu seçime izin vermek için.
### Liste kutusunun görünümünü değiştirebilir miyim?  
Kesinlikle! Aspose.Cells, liste kutusunun boyutunu, yazı tipini ve hatta rengini bile özelleştirmenize olanak tanır.
### Daha sonra liste kutusunu kaldırmam gerekirse ne olur?  
Liste kutusuna erişebilir ve onu kaldırabilirsiniz. `Shapes` koleksiyon kullanarak `sheet.Shapes.RemoveAt(index)`.
### Liste kutusunu başka bir hücreye bağlayabilir miyim?  
Evet, sadece şunu değiştirin: `LinkedCell` Seçili değeri görüntülemek istediğiniz herhangi bir hücreye özelliği ekleyin.
### Liste kutusuna nasıl daha fazla öğe ekleyebilirim?  
Belirtilen hücrelere daha fazla değer girerek giriş aralığını güncelleyin, liste kutusu otomatik olarak güncellenecektir.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}