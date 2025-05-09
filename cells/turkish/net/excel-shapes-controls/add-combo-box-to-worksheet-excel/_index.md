---
"description": "Aspose.Cells for .NET kullanarak Excel çalışma sayfasına programatik olarak birleşik kutu eklemeyi öğrenin. Bu adım adım kılavuz, her ayrıntıda size yol gösterir."
"linktitle": "Excel'de Çalışma Sayfasına Birleşik Kutu Ekleme"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Çalışma Sayfasına Birleşik Kutu Ekleme"
"url": "/tr/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Çalışma Sayfasına Birleşik Kutu Ekleme

## giriiş
Etkileşimli Excel elektronik tabloları oluşturmak, özellikle birleşik kutular gibi form öğeleri eklediğinizde kullanıcı deneyimini büyük ölçüde iyileştirebilir. Birleşik kutular, kullanıcıların önceden tanımlanmış bir listeden seçenekleri seçmesine olanak tanır ve veri girişine kolaylık ve verimlilik katar. Aspose.Cells for .NET ile Excel'i doğrudan kullanmadan Excel sayfalarında birleşik kutular programatik olarak oluşturabilirsiniz. Bu güçlü kitaplık, geliştiricilerin Excel dosyalarını çeşitli şekillerde düzenlemesine olanak tanır; bunlara form denetimlerini otomatikleştirme yeteneği de dahildir.
Bu eğitimde, Aspose.Cells for .NET kullanarak Excel'de bir çalışma sayfasına birleşik kutu ekleme sürecini adım adım anlatacağız. Dinamik, kullanıcı dostu elektronik tablolar oluşturmak istiyorsanız, bu kılavuz başlamanıza yardımcı olacaktır.
## Ön koşullar
Koda dalmadan önce ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
- Aspose.Cells for .NET: Aspose.Cells for .NET kitaplığını şu adresten indirin ve yükleyin: [indirme sayfası](https://releases.aspose.com/cells/net/).
- .NET Framework: Makinenizde .NET Framework'ün yüklü olduğundan emin olun. Aspose.Cells tarafından desteklenen herhangi bir sürüm çalışacaktır.
- Geliştirme Ortamı: Projenizi yönetmek ve kod yazmak için Visual Studio gibi bir IDE kullanın.
- Aspose Lisansı: Değerlendirme modunda lisans olmadan çalışabilirsiniz, ancak tam sürüm için bir lisans uygulamanız gerekir. [geçici lisans](https://purchase.aspose.com/temporary-license/) eğer gerekirse.
## Paketleri İçe Aktar
Başlamak için gerekli ad alanlarını projenize aktarmanız gerekir. İhtiyacınız olanlar şunlardır:
```csharp
using System.IO;
using Aspose.Cells;
```
Bunlar Excel dosyalarıyla etkileşim kurmak ve çalışma kitabındaki birleşik kutular gibi form öğelerini düzenlemek için gereklidir.
Kolay anlaşılması için, birleşik kutu ekleme sürecini birden fazla basit adıma bölelim.
## Adım 1: Belge Dizinini Ayarlayın
İlk adım Excel dosyalarınızın kaydedileceği bir dizin oluşturmaktır. Zaten mevcut değilse yeni bir klasör oluşturabilirsiniz.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Eğer mevcut değilse dizin oluşturun.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: Çıktı dosyasının kaydedileceği konumu belirtir.
- System.IO.Directory.Exists: Dizinin zaten var olup olmadığını kontrol eder.
- System.IO.Directory.CreateDirectory: Dizin yoksa oluşturur.
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun
Şimdi, birleşik kutuyu ekleyeceğiniz yeni bir Excel çalışma kitabı oluşturun.

```csharp
// Yeni bir Çalışma Kitabı oluşturun.
Workbook workbook = new Workbook();
```

- Çalışma kitabı çalışma kitabı: Excel dosyasını temsil eden Çalışma Kitabı sınıfının yeni bir örneğini başlatır.
## Adım 3: Çalışma Sayfasını ve Hücreleri Alın
Daha sonra çalışma kitabından ilk çalışma sayfasına erişin ve veri girişi yapacağınız hücre koleksiyonunu alın.

```csharp
// İlk çalışma kağıdını al.
Worksheet sheet = workbook.Worksheets[0];
// Çalışma sayfası hücre koleksiyonunu alın.
Cells cells = sheet.Cells;
```

- Çalışma sayfası: Çalışma kitabından ilk çalışma sayfasını getirir.
- Hücreler hücreler: Çalışma sayfasındaki hücre koleksiyonunu alır.
## Adım 4: Combo Box için Giriş Değerleri
Şimdi hücrelere bazı değerler girmemiz gerekiyor. Bu değerler, birleşik kutu için seçenekler olarak hizmet edecek.

```csharp
// Bir değer girin.
cells["B3"].PutValue("Employee:");
// Kalın olarak ayarlayın.
cells["B3"].GetStyle().Font.IsBold = true;
// Combobox için giriş aralığını belirten bazı değerleri girin.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- hücreler["B3"].PutValue: "Çalışan" etiketini B3 hücresine yerleştirir.
- Font.IsBold = true: Metni öne çıkarmak için kalınlaştırır.
- Giriş aralığı: A2 ila A7 hücrelerine birkaç çalışan kimliği girer. Bunlar açılır menüde görünecektir.
## Adım 5: Çalışma Sayfasına Combo Box'ı Ekleyin
Bir sonraki adım, birleşik kutu denetimini çalışma sayfanıza eklemektir. Bu birleşik kutu, kullanıcıların daha önce girdiğiniz çalışan kimliklerinden birini seçmesine izin verecektir.

```csharp
// Yeni bir açılır kutu ekleyin.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Çalışma sayfasına yeni bir birleşik kutu ekler. Sayılar (2, 0, 2, 0, 22, 100) birleşik kutunun konumunu ve boyutlarını temsil eder.
## Adım 6: Combo Box'ı bir Hücreye Bağlayın ve Giriş Aralığını Ayarlayın
Combobox'ı işlevsel hale getirmek için onu belirli bir hücreye bağlamamız ve seçeneklerini çekeceği hücre aralığını tanımlamamız gerekiyor.

```csharp
// Bağlantılı hücreyi ayarla.
comboBox.LinkedCell = "A1";
// Giriş aralığını ayarlayın.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Birleşik kutunun seçimini A1 hücresine bağlar. Birleşik kutudan seçilen değer bu hücrede görünecektir.
- InputRange: Birleşik kutu seçeneklerini dolduracak değerleri içeren hücre aralığını (A2:A7) tanımlar.
## Adım 7: Combo Box Görünümünü Özelleştirin
Daha estetik bir görünüm için açılır satır sayısını belirleyerek ve 3D gölgelendirmeyi etkinleştirerek birleşik kutuyu daha da özelleştirebilirsiniz.

```csharp
// Açılır kutunun liste bölümünde görüntülenecek liste satırı sayısını ayarlayın.
comboBox.DropDownLines = 5;
// 3 boyutlu gölgelendirme ile combo box'ı ayarlayın.
comboBox.Shadow = true;
```

- DropDownLines: Birleşik açılır listede aynı anda kaç seçeneğin görüneceğini kontrol eder.
- Gölge: Combo box'a 3 boyutlu gölgelendirme efekti ekler.
## Adım 8: Sütunları Otomatik Olarak Sığdır ve Çalışma Kitabını Kaydet
Son olarak, temiz bir düzen için sütunları otomatik olarak sığdıralım ve çalışma kitabını kaydedelim.

```csharp
// Otomatik Uyum Sütunları
sheet.AutoFitColumns();
// Dosyayı kaydeder.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: İçeriğe uyacak şekilde sütun genişliklerini otomatik olarak ayarlar.
- Kaydet: Çalışma kitabını belirtilen dizine Excel dosyası olarak kaydeder.

## Çözüm
.NET için Aspose.Cells kullanarak Excel çalışma sayfalarınıza bir birleşik kutu eklemek, veri girişi esnekliğini büyük ölçüde artıran basit bir işlemdir. Programatik olarak form denetimleri oluşturarak, etkileşimli elektronik tabloları kolaylıkla oluşturabilirsiniz. Bu eğitim, bir birleşik kutunun nasıl ekleneceğini, bir hücreye nasıl bağlanacağını ve giriş aralığının nasıl yapılandırılacağını Aspose.Cells kullanarak gösterdi.
Aspose.Cells, Excel dosya düzenleme için geniş bir özellik yelpazesi sunarak, elektronik tablo görevlerini otomatikleştirmek isteyen geliştiriciler için ideal bir seçim haline getirir. Bunu bir [ücretsiz deneme](https://releases.aspose.com/).
## SSS
### Excel yüklü olmadan Aspose.Cells'i kullanabilir miyim?
Evet, Aspose.Cells Excel'den bağımsız olarak çalışır ve Excel'in kurulu olmasını gerektirmez.
### Aspose.Cells'te lisans başvurusunu nasıl yapabilirim?
Lisansınızı şu adresten alarak başvurabilirsiniz: [Burada](https://purchase.aspose.com/buy) ve çağrı `License.SetLicense()` kodunuzda.
### Aspose.Cells dosyaları kaydetmek için hangi formatları destekler?
Aspose.Cells, dosyaların XLSX, XLS, CSV, PDF ve daha birçok formatta kaydedilmesini destekler.
### Ekleyebileceğim kombo kutularının sayısında bir sınırlama var mı?
Hayır, kesin bir sınır yoktur; projenizin gerektirdiği kadar çok kombo kutusu ekleyebilirsiniz.
### Aspose.Cells için desteği nasıl alabilirim?
Destek alabilirsiniz [Aspose forumu](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}