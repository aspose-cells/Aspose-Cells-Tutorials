---
title: Pivot Tablosunu .NET'te Programatik Olarak ODS Formatında Kaydetme
linktitle: Pivot Tablosunu .NET'te Programatik Olarak ODS Formatında Kaydetme
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu adım adım kılavuzla Aspose.Cells for .NET kullanarak Pivot Tablolarınızı ODS formatında nasıl kaydedeceğinizi öğrenin.
weight: 25
url: /tr/net/creating-and-configuring-pivot-tables/saving-in-ods-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pivot Tablosunu .NET'te Programatik Olarak ODS Formatında Kaydetme

## giriiş
Veriyi elektronik tablolarda yönetmeye gelince, Pivot Tabloların gücüyle hiçbir şey boy ölçüşemez. Karmaşık veri kümelerini özetlemek, analiz etmek ve sunmak için başvurulan bir araçtır. Bugün, Pivot Tabloyu ODS formatında kaydetmek için Aspose.Cells for .NET'i kullanmaya dalacağız. İster deneyimli bir geliştirici olun, ister .NET ile yeni tanışıyor olun, bu kılavuzun sizin için kolay olduğunu göreceksiniz. 
Hadi başlayalım!
## Ön koşullar
Koda geçmeden önce, ihtiyacınız olacak birkaç temel şey var:
### 1. .NET'in Temel Bilgileri
.NET ve programlama kavramları hakkında temel bir anlayışa sahip olmak, takip etmenizi kolaylaştıracaktır.
### 2. .NET için Aspose.Cells
 .NET için Aspose.Cells'in yüklü olması gerekir. Bunu şuradan indirebilirsiniz:[Aspose sürüm sayfası](https://releases.aspose.com/cells/net/) . Deneme sürümü de mevcuttur[Burada](https://releases.aspose.com/).
### 3. Geliştirme Ortamı
.NET kodlarınızı yazıp test edebileceğiniz Visual Studio gibi bir IDE'niz olduğundan emin olun.
### 4. Biraz Sabır
Herhangi bir kodlama çabasında olduğu gibi, sabır anahtardır. İlk seferde her şey mükemmel çalışmazsa endişelenmeyin; hata ayıklama sürecin bir parçasıdır.
## Paketleri İçe Aktar
Aspose.Cells ile çalışmak için gerekli ad alanlarını içe aktarmanız gerekir. Aşağıdaki using yönergesini kod dosyanızın başına ekleyin:
```csharp
using System;
using Aspose.Cells.Pivot;
```
Bu satır, Aspose.Cells kütüphanesindeki tüm işlevlere erişmenizi sağlayarak kodlama sürecinizi kolaylaştırır.
Şimdi süreci yönetilebilir adımlara bölelim.
## Adım 1: Çıktı Dizininizi Ayarlayın
Öncelikle ODS dosyanızı nereye kaydetmek istediğinizi tanımlamanız gerekir. Bu, basit bir dizin yolu atamasıdır.
```csharp
string outputDir = "Your Document Directory";
```
 Bu satırda şunu değiştirin:`"Your Document Directory"` dosyayı kaydetmek istediğiniz yolu yazın.
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun
Daha sonra Pivot Tablo da dahil olmak üzere tüm verilerinizi ve yapılarınızı tutacak yeni bir Çalışma Kitabı nesnesi oluşturacaksınız.
```csharp
Workbook workbook = new Workbook();
```
Burada temelde sıfırdan başlıyorsunuz; bunu başyapıtınızı yaratacağınız boş bir tuval olarak düşünün.
## Adım 3: Çalışma Sayfasına Erişim
Artık çalışma kitabımız olduğuna göre, çalışma sayfamız üzerinde çalışmaya başlamamız gerekiyor. Aspose.Cells, ilk kullanılabilir çalışma sayfasına kolayca erişmenizi sağlar.
```csharp
Worksheet sheet = workbook.Worksheets[0];
```
Bu satır bizi veri girişi için hazır olan ilk sayfaya götürür.
## Adım 4: Hücreleri Verilerle Doldurun
Çalışma sayfamızı biraz veriyle doldurmanın zamanı geldi. Spor satış verilerinin basit bir örneğini kullanacağız. 
Çeşitli hücrelere değerleri nasıl ayarlayabileceğiniz aşağıda açıklanmıştır:
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
Bu satırlarda başlıkları tanımlıyor ve satış verilerini dolduruyoruz. Bu adımı, bir yemek pişirmeden önce kilerinizi doldurmak gibi düşünün; malzemeleriniz (verileriniz) ne kadar iyiyse, yemeğiniz (analiz) de o kadar iyi olur.
## Adım 5: Pivot Tablo Oluşturun
Şimdi eğlenceli kısma geliyoruz: Pivot Tablo'yu oluşturmak! İşte onu çalışma sayfanıza nasıl ekleyeceğiniz:
```csharp
PivotTableCollection pivotTables = sheet.PivotTables;
// Çalışma sayfasına PivotTable ekleme
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```
 Bu kod parçacığında, Pivot Tablo için veri aralığını ve çalışma sayfasında nereye yerleştirileceğini belirtiyoruz. Veri aralığı`=A1:C8` verilerimizin bulunduğu alanı kapsar.
## Adım 6: Pivot Tablonuzu Özelleştirin
Sonra, Pivot Tablonuzu ihtiyaçlarınıza uyacak şekilde özelleştirmek isteyeceksiniz. Bu, gösterilenleri, nasıl kategorilendirildiğini ve verileri nasıl hesapladığını kontrol etmeyi içerir.
```csharp
PivotTable pivotTable = pivotTables[index];
// Satırlar için büyük toplamlar gösterilmiyor.
pivotTable.RowGrand = false;
// İlk alanı satır alanına sürüklüyoruz.
pivotTable.AddFieldToArea(PivotFieldType.Row, 0);
// İkinci alanı sütun alanına sürüklüyoruz.
pivotTable.AddFieldToArea(PivotFieldType.Column, 1);
// Üçüncü alanı veri alanına sürüklüyoruz.
pivotTable.AddFieldToArea(PivotFieldType.Data, 2);
pivotTable.CalculateData();
```
Burada, hangi veri alanlarının özetleneceğine ve nasıl temsil edileceğine karar veriyorsunuz. Akşam yemeği partiniz için masayı hazırlamak gibi; neyin en uygun olduğuna ve nasıl sunulacağına siz karar veriyorsunuz.
## Adım 7: Çalışma Kitabınızı Kaydedin
Son olarak, çalışmanızı istediğiniz ODS biçimine kaydetmeye hazırsınız. Bunu nasıl yapacağınız aşağıda açıklanmıştır:
```csharp
workbook.Save(outputDir + "PivotTableSaveInODS_out.ods");
```
Bu adımla projenizi tamamlayıp seçtiğiniz dizinde güvenceye almış oluyorsunuz; tatmin edici bir son!
## Adım 8: Çıktınızı Doğrulayın
Son olarak, işlemin başarıyla tamamlanıp tamamlanmadığını kontrol etmek her zaman iyi bir fikirdir. Basit bir konsol mesajı ekleyebilirsiniz:
```csharp
Console.WriteLine("PivotTableSaveInODS executed successfully.");
```
Bu mesaj, her şeyin sorunsuz bir şekilde gittiğini doğrulamak için konsolunuzda görünecektir. Tıpkı bir şefin servis etmeden önce her şeyin mükemmel şekilde pişip pişmediğini kontrol etmesi gibi!
## Çözüm 
Ve işte oldu! Sadece Aspose.Cells kullanarak bir Pivot Tablosu oluşturmakla kalmadınız, aynı zamanda onu ODS formatında da kaydettiniz. Bu kılavuz, gelecekte benzer görevleri üstlenmeniz için bilgi ve güvenle donatılmanızı sağlayarak sizi her adımda yönlendirdi.
## SSS
### Aspose.Cells Nedir?
Aspose.Cells, .NET uygulamalarında Excel dosyaları oluşturmanıza ve düzenlemenize olanak tanıyan gelişmiş bir kütüphanedir.
### Aspose.Cells'i ücretsiz kullanabilir miyim?
 Evet, ücretsiz deneme sürümünü şu adresten indirebilirsiniz:[Aspose web sitesi](https://releases.aspose.com/).
### Aspose.Cells hangi formatları destekliyor?
XLSX, XLS, ODS, PDF ve daha birçok formatı destekler.
### Aspose.Cells için desteği nasıl alabilirim?
 Yardımı şu adreste bulabilirsiniz:[Aspose Destek Forumu](https://forum.aspose.com/c/cells/9).
### Geçici lisans var mı?
 Evet, Aspose sitesi üzerinden geçici lisans başvurusunda bulunabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
