---
"description": "Bu adım adım kılavuzla Aspose.Cells for .NET'i kullanarak Excel'de satır ve sütunları nasıl gruplayacağınızı öğrenin."
"linktitle": "Aspose.Cells ile Excel'de Satır ve Sütunları Gruplama"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Aspose.Cells ile Excel'de Satır ve Sütunları Gruplama"
"url": "/tr/net/row-and-column-management/grouping-rows-and-columns/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells ile Excel'de Satır ve Sütunları Gruplama

## giriiş
Büyük Excel sayfalarıyla çalışıyorsanız, her şeyi iyi organize edilmiş ve kullanıcı dostu tutmanın ne kadar önemli olduğunu biliyorsunuzdur. Satırları ve sütunları gruplamak, bölümler oluşturmanıza yardımcı olur ve veri gezinmesini çok daha akıcı hale getirir. .NET için Aspose.Cells ile Excel'de satırları ve sütunları programatik olarak kolayca gruplayabilir ve dosyalarınızın düzeni üzerinde tam kontrol sahibi olabilirsiniz.
Bu eğitimde, .NET için Aspose.Cells ile bir Excel sayfasında satırları ve sütunları ayarlamak, gruplamak ve gizlemek için bilmeniz gereken her şeyi ele alacağız. Sonunda, Excel'in kendisini açmadan bile Excel dosyalarını bir profesyonel gibi işleyebileceksiniz. Dalmaya hazır mısınız?
## Ön koşullar
Koda geçmeden önce her şeyin ayarlı ve hazır olduğundan emin olalım:
1. Aspose.Cells for .NET Kütüphanesi: Excel dosyalarıyla çalışmak için bu kütüphaneye ihtiyacınız olacak. İndirebilirsiniz [Burada](https://releases.aspose.com/cells/net/).
2. Visual Studio: Bu eğitimde kod örnekleri için Visual Studio kullanılıyor.
3. Temel C# Bilgisi: C# ve .NET'e aşinalık faydalıdır.
4. Aspose Lisansı: Değerlendirme sınırlamalarından kaçınmak için ücretli veya geçici bir lisans gereklidir. Geçici bir lisans edinin [Burada](https://purchase.aspose.com/temporary-license/).
## Paketleri İçe Aktar
Başlamak için, dosya işleme için gerekli .NET kitaplıklarıyla birlikte gerekli Aspose.Cells ad alanını içe aktarın. 
```csharp
using System.IO;
using Aspose.Cells;
```
Kodun her bir bölümünü, takip etmenizi ve anlamanızı kolaylaştırmak için parçalara ayıralım.
## Adım 1: Veri Dizininizi Ayarlayın
İlk önce, üzerinde çalışacağımız Excel dosyasının yolunu tanımlamamız gerekiyor. Bu genellikle yerel bir yoldur, ancak bir ağdaki yol da olabilir.
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
Burada, değiştirin `"Your Document Directory"` Excel dosyalarınıza giden gerçek yol ile. Bu kurulum, kodunuzun üzerinde çalışması gereken dosyaları bulmasına yardımcı olur.
## Adım 2: Excel Dosyasına Erişmek İçin Bir Dosya Akışı Oluşturun
Aspose.Cells, dosyayı bir dosya akışı aracılığıyla açmanızı gerektirir. Bu akış, işlenmek üzere dosyanın içeriğini okur ve yükler.
```csharp
// Açılacak Excel dosyasını içeren bir dosya akışı oluşturma
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
Yukarıdaki kod açılır `book1.xls` belirtilen dizinden. Dosya mevcut değilse, onu oluşturduğunuzdan veya dosya adını değiştirdiğinizden emin olun.
## Adım 3: Çalışma Kitabını Aspose.Cells ile yükleyin
Şimdi, çalışma kitabını Aspose.Cells aracılığıyla başlatalım. Bu adım bize Excel dosyasına erişim sağlar ve kolay düzenleme olanağı sağlar.
```csharp
// Excel dosyasını dosya akışı aracılığıyla açma
Workbook workbook = new Workbook(fstream);
```
Bu satırdan sonra, `workbook` nesnesi Excel dosyanızdaki tüm verileri ve yapıyı içerecektir. Bunu, tüm elektronik tablonun belleğe yüklenmesi gibi düşünün.
## Adım 4: Değiştirmek İstediğiniz Çalışma Sayfasına Erişin
Aspose.Cells, çalışma kitabındaki her çalışma sayfasını ayrı bir nesne olarak depolar. Burada, ilk çalışma sayfasını seçiyoruz.
```csharp
// Excel dosyasındaki ilk çalışma sayfasına erişim
Worksheet worksheet = workbook.Worksheets[0];
```
Belirli bir çalışma sayfasına ihtiyacınız varsa, adına veya dizinine göre erişmek için bu satırı değiştirebilirsiniz.
## Adım 5: Çalışma Sayfasındaki Satırları Gruplandırın
Şimdi eğlenceli kısma geldik: Satırları gruplandırma! İlk altı satırı gruplayıp gizleyelim.
```csharp
// İlk altı satırı (0'dan 5'e kadar) gruplandırıp true değerini geçirerek gizli hale getiriyoruz
worksheet.Cells.GroupRows(0, 5, true);
```
Her parametrenin işlevi şöyledir:
- 0, 5: Gruplamak istediğiniz satırların başlangıç ve bitiş dizinleri. Excel'de satır dizini 0'dan başlar.
- true: Bunu true olarak ayarlamak gruplanmış satırları gizler.
Çalıştırıldığında 0'dan 5'e kadar olan satırlar gruplandırılacak ve görünümden gizlenecektir.
## Adım 6: Çalışma Sayfasındaki Sütunları Gruplandırın
Tıpkı satırlarda olduğu gibi, daha temiz ve daha düzenli bir düzen oluşturmak için sütunları gruplayabilirsiniz. İlk üç sütunu nasıl gruplayacağınız aşağıda açıklanmıştır.
```csharp
// İlk üç sütunu (0'dan 2'ye kadar) gruplandırıp true değerini geçirerek gizli hale getiriyoruz
worksheet.Cells.GroupColumns(0, 2, true);
```
Bu fonksiyonun parametreleri şunlardır:
- 0, 2: Gruplanacak sütun aralığı, indeksleme 0'dan başlar.
- true: Bu parametre gruplanmış sütunları gizler.
Seçtiğiniz sütunlar (0 ila 2) artık Excel dosyasında gruplandırılmış ve gizli olarak görünecektir.
## Adım 7: Değiştirilen Excel Dosyasını Kaydedin
Değişiklikleri yaptıktan sonra orijinalinin üzerine yazılmasını önlemek için dosyayı yeni bir isimle kaydedelim.
```csharp
// Değiştirilen Excel dosyasını kaydetme
workbook.Save(dataDir + "output.xls");
```
Artık gruplanmış satırlarınızı ve sütunlarınızı başarıyla kaydettiniz `output.xls`. İhtiyacınıza göre dosya adını değiştirebilirsiniz.
## Adım 8: Kaynakları Serbest Bırakmak İçin Dosya Akışını Kapatın
Son olarak, kaynakları serbest bırakmak için dosya akışını kapatın. Bunu yapmamak, dosyaya tekrar erişmeniz veya dosyayı değiştirmeniz gerekirse sorunlara neden olabilir.
```csharp
// Tüm kaynakları serbest bırakmak için dosya akışını kapatıyorum
fstream.Close();
```
Ve işte bu kadar! Artık Aspose.Cells for .NET kullanarak bir Excel dosyasındaki satırları ve sütunları grupladınız.
## Çözüm
Excel'de .NET için Aspose.Cells ile satır ve sütunları gruplandırmak, elektronik tablolarınızı çok daha kullanıcı dostu ve düzenli hale getirebilecek basit bir işlemdir. Sadece birkaç satır kodla, Excel'de manuel olarak yapıldığında daha fazla adım gerektiren güçlü bir özelliği ustalıkla kullanmış olursunuz. Ayrıca, bu işlemi birçok dosyada otomatikleştirebilir, zamandan tasarruf edebilir ve hataları azaltabilirsiniz. Bu kılavuz, Excel dosyalarınızı programatik olarak kontrol altına almak için gereken tüm adımları size göstermiştir.
## SSS
### Satır ve sütunları gizlemeden gruplayabilir miyim?  
Evet! Sadece geç `false` üçüncü parametre olarak `GroupRows` veya `GroupColumns` yöntem.
### Satırları veya sütunları gruplandırmayı kaldırmak istersem ne olur?  
Kullanmak `wveyaksheet.Cells.UngroupRows(startRow, endRow)` or `worksheet.Cells.UngroupColumns(startColumn, endColumn)` onları gruplandırmak için.
### Aynı çalışma sayfasında birden fazla aralığı gruplayabilir miyim?  
Kesinlikle. Arayın `GroupRows` veya `GroupColumns` Gruplamak istediğiniz her aralık için yöntemi kullanın.
### Aspose.Cells for .NET'i kullanmak için lisansa ihtiyacım var mı?  
Evet, deneme sürümü mevcut olsa da, tam işlevselliğin kilidini açmak için bir lisansa ihtiyacınız olacak. Geçici bir lisans alabilirsiniz [Burada](https://purchase.aspose.com/temporary-license/).
### Koşullu mantıkla satır ve sütunları gruplayabilir miyim?  
Evet! Her satır veya sütundaki verilere bağlı olarak, gruplamadan önce kodunuza mantık ekleyerek koşullu gruplama oluşturabilirsiniz.


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}