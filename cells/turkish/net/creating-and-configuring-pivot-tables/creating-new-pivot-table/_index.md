---
title: .NET'te Programatik Olarak Yeni Bir Pivot Tablo Oluşturma
linktitle: .NET'te Programatik Olarak Yeni Bir Pivot Tablo Oluşturma
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells'i kullanarak .NET'te programatik olarak pivot tablo oluşturmayı adım adım kılavuzumuzla öğrenin. Verilerinizi verimli bir şekilde analiz edin.
weight: 13
url: /tr/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# .NET'te Programatik Olarak Yeni Bir Pivot Tablo Oluşturma

## giriiş
Pivot tablo oluşturmak, özellikle bunu programatik olarak yapıyorsanız, göz korkutucu bir görev gibi görünebilir. Ancak korkmayın! .NET için Aspose.Cells ile bir pivot tablo oluşturmak yalnızca basit değil, aynı zamanda veri analizi için de oldukça güçlüdür. Bu eğitimde, .NET uygulamasında yeni bir pivot tablonun nasıl oluşturulacağı konusunda adım adım size rehberlik edeceğiz. İster satış, ister spor veya başka bir iş metriği için veri ekliyor olun, bu kılavuz pivot tablolarınızı kısa sürede çalışır hale getirmenize yardımcı olacaktır.

## Ön koşullar
Dalmadan önce, her şeyin hazır olduğundan emin olalım. Yapmanız gerekenler şunlardır:

1. .NET Framework'ü yükleyin: Makinenizde .NET Framework'ün yüklü olduğundan emin olun. Aspose.Cells çeşitli sürümleri destekler, ancak en son sürüme bağlı kalmak en iyisidir.
2.  Aspose.Cells Kütüphanesi: Aspose.Cells kütüphanesine sahip olmanız gerekir.[buradan indirin](https://releases.aspose.com/cells/net/)veya bir tane al[geçici lisans](https://purchase.aspose.com/temporary-license/) Değerlendirme için.
3. IDE Kurulumu: Yeni bir projeye başlayabileceğiniz Visual Studio gibi C# uyumlu bir IDE'niz olsun.
4. Temel C# Bilgisi: C# programlamaya aşina olmak, çok fazla kafanızın karışmadan konuyu takip etmenize yardımcı olacaktır.

Tamam mı? Harika! Gerekli paketleri içe aktarmaya başlayalım.

## Paketleri İçe Aktar
İlk önce, gerekli ad alanlarını C# projenize aktarmanız gerekir. C# dosyanızı açın ve aşağıdaki using yönergelerini ekleyin:

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Bu ad alanları, bu eğitim boyunca kullanacağımız çalışma kitabı, çalışma sayfası ve pivot tablo işlevlerine erişmenizi sağlar.

## Adım 1: Bir Çalışma Kitabı Nesnesi Oluşturun
Bir çalışma kitabı oluşturmak yolculuğunuzun başlangıcıdır. Yeni bir çalışma kitabı örneği oluşturarak ve ilk çalışma sayfasına erişerek başlayalım.

```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
// Bir Çalışma Kitabı nesnesini örnekleme
Workbook workbook = new Workbook();

// Yeni eklenen çalışma sayfasının referansını edinme
Worksheet sheet = workbook.Worksheets[0];
```

 Bu adımda bir tane oluşturuyoruz`Workbook`Excel dosyamızı temsil eden örneği seçip pivot tablomuz için oyun alanımız olacak ilk çalışma sayfasını alalım.

## Adım 2: Hücrelere Veri Ekleme
Şimdi, çalışma sayfamızı bazı örnek verilerle dolduralım. Pivot tablomuza özetleyecek bir şey vermek için farklı sporlar, çeyrekler ve satış rakamları için satırlar gireceğiz.

```csharp
Cells cells = sheet.Cells;

// Hücrelere değer ayarlama
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// Veri hücresi dolduruluyor = hücreler["A2"];
cell.PutValue("Golf");
// ... Daha fazla veri girişi
```

Burada, sütun başlıklarımızı tanımlıyoruz ve her başlığın altına değerler ekliyoruz. Bu veriler pivot tablomuz için kaynak görevi görecek, bu yüzden düzenli olduğundan emin olun! Bu bloğu takip edin ve kapsamlı bir veri kümesi oluşturacaksınız.

## Adım 3: Pivot Tablo Ekleme
Verilerimiz hazır olduğunda, pivot tabloyu oluşturmanın zamanı geldi. Yeni pivot tablomuzu eklemek için çalışma sayfasındaki pivot tablo koleksiyonunu kullanacağız.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// Çalışma sayfasına PivotTable ekleme
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

Bu kod parçasında, veri aralığımıza (bu durumda A1 ila C8 hücreleri) başvuran bir pivot tabloyu çalışma sayfasına ekliyoruz. Pivot tabloyu E3 hücresinden başlayarak yerleştiriyoruz ve "PivotTable2" olarak adlandırıyoruz. Oldukça basit, değil mi?

## Adım 4: Pivot Tablosunu Özelleştirin
Artık pivot tablomuz olduğuna göre, anlamlı özetler göstermesi için özelleştirelim. Pivot tablonun satırlarında, sütunlarında ve veri alanlarında neyin görüneceğini kontrol edebiliriz.

```csharp
// Yeni eklenen PivotTable örneğine erişim
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// Satırlar için büyük toplamlar gösterilmiyor.
pivotTable.RowGrand = false;

// İlk alanı satır alanına sürüklüyoruz.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// İkinci alanı sütun alanına sürüklüyoruz.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// Üçüncü alanı veri alanına sürüklüyoruz.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

Bu adımda, pivot tabloya satırlar için genel toplamları gizlemesini ve ardından satır, sütun ve veri alanlarına hangi alanların gireceğini belirtmesini söyleriz. Spor adları satırları dolduracak, çeyrekler sütunları dolduracak ve satış rakamları özetleri sağlayacaktır.

## Adım 5: Çalışma Kitabını Kaydedin
Son olarak emeğimizin meyvelerini görmek için yeni oluşturduğumuz çalışma kitabımızı kaydetmek istiyoruz.

```csharp
// Excel dosyasını kaydetme
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

Sadece uygun bir yol sağlayın, böylece pivot tablo çıktınız açıp inceleyebileceğiniz bir Excel dosyasına kaydedilecektir.

## Çözüm
Aspose.Cells for .NET kullanarak programatik olarak pivot tabloları oluşturmak, özellikle büyük veri kümeleriyle uğraşırken size önemli ölçüde zaman kazandırabilir. Projenizi nasıl kuracağınızı, gerekli paketleri nasıl içe aktaracağınızı, verileri nasıl dolduracağınızı ve sıfırdan özelleştirilebilir bir pivot tablo nasıl oluşturacağınızı öğrendiniz. Yani, bir dahaki sefere sayılar içinde boğulduğunuzda, bu öğreticiyi hatırlayın ve Aspose.Cells'in sizin için ağır işi yapmasına izin verin.

## SSS
### Aspose.Cells Nedir?
Aspose.Cells, Excel elektronik tablolarını programlı olarak oluşturmak ve yönetmek için güçlü bir .NET kütüphanesidir.

### Aspose.Cells için ücretsiz deneme sürümü var mı?
 Evet, ücretsiz deneme alabilirsiniz[Burada](https://releases.aspose.com/).

### Pivot tablonun görünümünü özelleştirebilir miyim?
Kesinlikle! Pivot tablonun biçimlendirmesini, düzenini ve hatta stillerini ihtiyaçlarınıza göre özelleştirebilirsiniz.

### Aspose.Cells hakkında daha fazla örnek ve dokümanı nerede bulabilirim?
 Kontrol edebilirsiniz[belgeleme](https://reference.aspose.com/cells/net/) Kapsamlı kılavuzlar ve örnekler için.

### Aspose.Cells için desteği nasıl alabilirim?
 Destek almak için:[Aspose forumu](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
