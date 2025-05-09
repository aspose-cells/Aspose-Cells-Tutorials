---
"description": "Aspose.Cells kullanarak .NET'te Pivot Tablolarını programatik olarak nasıl sıralayacağınızı öğrenin. Kurulum, yapılandırma, sıralama ve sonuçları Excel ve PDF dosyaları olarak kaydetmeyi kapsayan adım adım bir kılavuz."
"linktitle": ".NET'te Pivot Tablo Özel Sıralama Programlama"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": ".NET'te Pivot Tablo Özel Sıralama Programlama"
"url": "/tr/net/creating-and-configuring-pivot-tables/pivot-table-custom-sort/"
"weight": 29
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Pivot Tablo Özel Sıralama Programlama

## giriiş
.NET ortamında Excel ile çalışmaya gelince, bir kütüphane diğerlerinden sıyrılıyor: Aspose.Cells. Şimdi, bir araç elektronik tabloları programatik olarak düzenlemenize izin verdiğinde bunu sevmiyor musunuz? Aspose.Cells tam olarak bunu yapıyor! Bugünkü eğitimde, Pivot Tablolar dünyasına derinlemesine dalıyoruz ve bu çok yönlü kütüphaneyi kullanarak özel sıralamayı programatik olarak nasıl uygulayacağınızı gösteriyoruz.
## Ön koşullar
Kolları sıvayıp kodlara dalmadan önce birkaç şeyin yerinde olduğundan emin olun:
1. Visual Studio: Çalışan bir Visual Studio sürümüne ihtiyacınız olacak. Tüm sihrin gerçekleştiği oyun alanı burası.
2. .NET Framework: .NET programlamaya aşinalık şarttır. .NET Core veya .NET Framework meraklısı olun, hazırsınız.
3. Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesini yüklemeniz gerekir. Bunu şuradan alabilirsiniz: [İndirme bağlantısı](https://releases.aspose.com/cells/net/) ve projenize ekleyin.
4. Pivot Tablolar Hakkında Temel Bilgi: Uzman olmanıza gerek yok ancak bu eğitimi alırken Pivot Tabloların nasıl çalıştığı hakkında biraz bilgi sahibi olmanız faydalı olacaktır.
5. Örnek Excel Dosyası: Aşağıdaki adlı bir örnek Excel dosyanız var: `SamplePivotSort.xlsx` test için çalışma dizininizde hazır.
## Paketleri İçe Aktar
Tüm önkoşullarınızı hallettikten sonra, ilk adım gerekli paketleri içe aktarmaktır. Bunu yapmak için, kodunuzun en üstüne şu satırları ekleyin:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using Aspose.Cells;
using Aspose.Cells.Pivot;
```
Bu paket, Aspose.Cells kullanarak Excel dosyalarını düzenlemek için ihtiyaç duyduğunuz tüm işlevselliği sağlar.

Tamam, eğlenceli kısma geçelim! Pivot Tablo oluşturma ve özel sıralamayı yönetilebilir adımlara uygulama sürecini parçalara ayıracağız.
## Adım 1: Çalışma Kitabını Ayarlayın
Başlamak için çalışma kitabımızı ayarlamamız gerekiyor. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
string sourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
Workbook wb = new Workbook(sourceDir + "SamplePivotSort.xlsx");
```
Bu adımda yeni bir başlangıç yapıyoruz `Workbook` Excel dosyamıza giden yol ile örnek. Bu, Pivot Tablomuzun canlanacağı tuval görevi görür.
## Adım 2: Çalışma Sayfasına Erişim
Daha sonra Pivot Tablomuzu ekleyeceğimiz çalışma sayfasına erişmemiz gerekiyor.
```csharp
Worksheet sheet = wb.Worksheets[0];
PivotTableCollection pivotTables = sheet.PivotTables;
```
Burada, çalışma kitabımızdaki ilk çalışma sayfasını alıyoruz ve `PivotTableCollection`Bu koleksiyon, bu çalışma sayfasındaki tüm Pivot Tabloları yönetmemizi sağlar.
## Adım 3: İlk Pivot Tablonuzu Oluşturun
Şimdi Pivot Tablomuzu oluşturmanın zamanı geldi.
```csharp
int index = pivotTables.Add("=Sheet1!A1:C10", "E3", "PivotTable1");
PivotTable pivotTable = pivotTables[index];
```
Çalışma sayfamıza yeni bir Pivot Tablo ekliyoruz, veri aralığını ve konumunu belirtiyoruz. "E3" Pivot Tablomuzun nerede başlamasını istediğimizi gösterir. Daha sonra bu yeni Pivot Tabloya dizinini kullanarak başvuruyoruz.
## Adım 4: Pivot Tablo Ayarlarını Yapılandırın
Pivot Tablomuzu yapılandıralım! Bu, büyük toplamlar ve alan düzenlemeleri gibi yönleri kontrol etmek anlamına gelir.
```csharp
pivotTable.RowGrand = false;
pivotTable.ColumnGrand = false;
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
PivotField rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
Satır ve sütunlar için genel toplamların görüntülenmediğinden emin oluyoruz, bu da verileri daha temiz hale getirebilir. Ardından, satır alanına ilk alanı ekleyerek otomatik sıralamayı ve artan sıralamayı etkinleştiriyoruz.
## Adım 5: Sütun ve Veri Alanlarını Ekleyin
Satırlar ayarlandıktan sonra sütun ve veri alanlarını ekleyelim.
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Column,0);
PivotField colField = pivotTable.ColumnFields[0];
colField.NumberFormat = "dd/mm/yyyy";
colField.IsAutoSort = true;
colField.IsAscendSort = true;
```
İkinci alanı bir sütun olarak ekliyoruz ve tarih olarak biçimlendiriyoruz. Tekrar, her şeyi düzenli tutmak için otomatik sıralamayı ve artan düzeni etkinleştiriyoruz. Son olarak, veri alanımıza üçüncü alanı eklememiz gerekiyor:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Data,2);
```
## Adım 6: Pivot Tablosunu Yenileyin ve Hesaplayın
Gerekli tüm alanları ekledikten sonra Pivot Tablomuzun güncel ve hazır olduğundan emin olalım.
```csharp
pivotTable.RefreshData();
pivotTable.CalculateData();
```
Bu yöntemler verileri yeniler ve yeniden hesaplar, böylece Pivot Tablomuzda her şeyin güncel olmasını ve doğru şekilde görüntülenmesini sağlar.
## Adım 7: Satır Alanı Değerlerine Göre Özel Sıralama
Pivot Tablosunu "Deniz Ürünleri" gibi belirli değerlere göre sıralayarak biraz gösteriş katalım.
```csharp
index = pivotTables.Add("=Sheet1!A1:C10", "E10", "PivotTable2");
pivotTable = pivotTables[index];
```
Başka bir Pivot Tablo oluşturarak ve onu birincisine benzer şekilde ayarlayarak işlemi tekrarlıyoruz. Şimdi onu daha da özelleştirebiliriz:
```csharp
pivotTable.AddFieldToArea(PivotFieldType.Row,1);
rowField = pivotTable.RowFields[0];
rowField.IsAutoSort = true;
rowField.IsAscendSort = true;
```
## Adım 8: Ek Sıralama ÖzelleştirmesiBelirli bir tarihe dayalı başka bir sıralama yöntemini deneyelim:
```csharp
// Tarihe göre sıralama için başka bir Pivot Tablo ekleme
index = pivotTables.Add("=Sheet1!A1:C10", "E18", "PivotTable3");
pivotTable = pivotTables[index];
// Önceki adımlara benzer şekilde satır ve sütun ayarlarını tekrarlayın
```
Aynı işlemi tekrarlayarak ihtiyaçlarınıza göre sıralanmış sıralama ölçütlerine sahip üçüncü bir Pivot Tablo oluşturursunuz.
## Adım 9: Çalışma Kitabını Kaydedin Tüm emeklerimizi kaydetme zamanı!
```csharp
wb.Save(outputDir + "out.xlsx");
PdfSaveOptions options = new PdfSaveOptions();
options.OnePagePerSheet = true;
wb.Save(outputDir + "out.pdf", options);
```
Burada çalışma kitabını Excel dosyası ve PDF olarak kaydedersiniz. `PdfSaveOptions` dönüştürüldüğünde her sayfanın ayrı bir sayfada görünmesini sağlayarak daha iyi biçimlendirmeye olanak tanır.
## Adım 10: BitirinKullanıcıya her şeyin yolunda olduğunu bildirerek işlemi tamamlayın.
```csharp
Console.WriteLine("PivotTableCustomSort executed successfully.");
```
## Çözüm
Artık, .NET uygulamalarınızda Pivot Tablolar oluşturmak ve özelleştirmek için Aspose.Cells'in gücünden nasıl yararlanacağınızı öğrendiniz. İlk kurulumdan özel sıralamaya kadar her adım, kusursuz bir deneyim sunmak için bir araya geliyor. Yıllık satış verilerini sunmanız veya envanter istatistiklerini takip etmeniz gerekip gerekmediğine bakılmaksızın, bu beceriler size çok yardımcı olacak!
## SSS
### Pivot Tablo Nedir?
Pivot Tablo, Excel'de verileri özetlemenize ve analiz etmenize olanak tanıyan, esnek bir şekilde içgörüler çıkarmanıza olanak tanıyan bir veri işleme aracıdır.
### Aspose.Cells'i nasıl kurarım?
NuGet aracılığıyla Visual Studio'da kurabilir veya doğrudan şu adresten indirebilirsiniz: [İndirme bağlantısı](https://releases.aspose.com/cells/net/).
### Aspose.Cells'in deneme sürümü var mı?
Evet! Ücretsiz olarak denemek için şu adresi ziyaret edebilirsiniz: [Ücretsiz deneme bağlantısı](https://releases.aspose.com/).
### Pivot Tablo'da birden fazla alanı sıralayabilir miyim?
Kesinlikle! İhtiyaçlarınıza göre birden fazla alan ekleyebilir ve sıralayabilirsiniz.
### Aspose.Cells için desteği nereden bulabilirim?
Topluluk oldukça aktiftir ve forumlarında soru sorabilirsiniz [Burada](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}