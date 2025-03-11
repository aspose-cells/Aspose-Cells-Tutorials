---
title: Çalışma Kitabını CSV Formatında Metne Kaydet
linktitle: Çalışma Kitabını CSV Formatında Metne Kaydet
second_title: Aspose.Cells .NET Excel İşleme API'si
description: .NET geliştiricileri için tasarlanmış bu kapsamlı, adım adım eğitimde, Aspose.Cells ile Excel çalışma kitaplarını CSV formatına nasıl zahmetsizce dönüştüreceğinizi öğrenin.
weight: 17
url: /tr/net/saving-files-in-different-formats/save-workbook-to-text-csv-format/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabını CSV Formatında Metne Kaydet

## giriiş
Verilerle uğraşırken, seçtiğiniz biçim, onunla ne kadar kolay çalışabileceğinizi gerçekten belirleyebilir. Tablo verileri işlemek için en yaygın biçimlerden biri CSV'dir (Virgülle Ayrılmış Değerler). Excel dosyalarıyla çalışan bir geliştiriciyseniz ve çalışma kitaplarını CSV biçimine dönüştürmeniz gerekiyorsa, .NET için Aspose.Cells bu görevi basitleştiren harika bir kütüphanedir. Bu eğitimde, bir Excel çalışma kitabını sorunsuz bir şekilde metin CSV biçimine dönüştürme adımlarını açıklayacağız.
## Ön koşullar
Başlamadan önce, başlamak için her şeyin yerinde olduğundan emin olalım:
1. Temel C# ve .NET Bilgisi: C# dilinde kod yazacağımız için dil ve .NET framework'üne aşinalık şarttır.
2. Aspose.Cells Kütüphanesi: Geliştirme ortamınızda Aspose.Cells for .NET kütüphanesinin yüklü olduğundan emin olun. Bunu indirebilirsiniz[Burada](https://releases.aspose.com/cells/net/).
3. Visual Studio veya Herhangi Bir C# IDE: Kodunuzu yazmak ve yürütmek için entegre bir geliştirme ortamına (IDE) ihtiyacınız olacak. Visual Studio popüler bir seçimdir.
4. Excel Çalışma Kitabı: Dönüşümü test etmek için bazı veriler içeren bir örnek Excel çalışma kitabı hazırlayın (örneğin, "book1.xls").
## Paketleri İçe Aktar
Artık ön koşullarımızı tamamladığımıza göre, süreçteki ilk adım gerekli paketleri içe aktarmaktır. C# projenizde, kod dosyanızın en üstüne aşağıdaki ad alanını eklemeniz gerekir:
```csharp
using System.IO;
using Aspose.Cells;
using System;
```
Bu ad alanları, Excel dosyalarıyla çalışmak ve bellek akışlarını yönetmek için gereken sınıflara ve yöntemlere erişmenizi sağlayacaktır.
## Adım 1: Belgeler Dizinine Giden Yolu Tanımlayın
Sürecimizdeki ilk adım, belgelerimizin (Excel çalışma kitapları) nerede saklandığını tanımlamaktır. Bu önemlidir çünkü programımızın işlemesi gereken dosyaları nerede bulacağını bilmesini sağlar. 
```csharp
// Belgeler dizinine giden yol.
string dataDir = "Your Document Directory";
```
 Değiştirdiğinizden emin olun`"Your Document Directory"` "book1.xls" dosyanızın bulunduğu gerçek yol ile. Bu, bilgisayarınızdaki bir dizin veya bir sunucuya giden bir yol olabilir.
## Adım 2: Kaynak Çalışma Kitabınızı Yükleyin
Daha sonra CSV formatına dönüştürülecek Excel çalışma kitabını yüklememiz gerekiyor.
```csharp
// Kaynak çalışma kitabınızı yükleyin
Workbook workbook = new Workbook(dataDir + "book1.xls");
```
 The`Workbook` Aspose.Cells kütüphanesinden sınıf, Excel çalışma kitaplarının işlenmesine ve erişilmesine olanak tanır. Dosya yolunu geçirerek, belirtilen çalışma kitabını işleme için yüklüyoruz.
## Adım 3: Çalışma Kitabı Verileri için Bir Bayt Dizisi Başlatın
Çalışma kitabını CSV'ye dönüştürmeye başlamadan önce, sonunda tüm çalışma sayfası verilerini tutacak boş bir bayt dizisi başlatmamız gerekiyor.
```csharp
// 0 baytlık dizi
byte[] workbookData = new byte[0];
```
Bu bayt dizisi, her çalışma sayfasındaki verileri daha sonra bir dosyaya yazabileceğimiz tek bir yapıda birleştirecektir.
## Adım 4: Metin Kaydetme Seçeneklerini Ayarlayın
Şimdi, metin biçimini nasıl kaydetmek istediğimize dair seçenekleri ayarlayalım. Özel sınırlayıcıları seçebilir veya sekmelerde kalabilirsiniz.
```csharp
// Metin kaydetme seçenekleri. Herhangi bir ayırıcı türünü kullanabilirsiniz
TxtSaveOptions opts = new TxtSaveOptions();
opts.Separator = '\t'; // Sekmeyi ayırıcı olarak ayarlama
```
 Bu örnekte ayırıcı olarak bir sekme karakteri kullanıyoruz. Bunu değiştirebilirsiniz`'\t'` istediğiniz herhangi bir karakterle, örneğin virgülle (`,`), CSV dosyanızın nasıl biçimlendirilmesini istediğinize bağlı olarak.
## Adım 5: Her Çalışma Sayfasını Tekrarlayın
 Daha sonra, çalışma kitabındaki tüm çalışma sayfalarını yineleyerek her birini kendimize kaydedeceğiz.`workbookData` dizi, ancak öncelikle hangi çalışma sayfası üzerinde çalışacağınızı seçmelisiniz.
```csharp
// Her çalışma sayfası verisini çalışma kitabı veri dizisinin içine metin biçiminde kopyala
for (int idx = 0; idx < workbook.Worksheets.Count; idx++)
{
    // Etkin çalışma sayfasını metin biçimine kaydedin
    MemoryStream ms = new MemoryStream();
    workbook.Worksheets.ActiveSheetIndex = idx;
    workbook.Save(ms, opts);
```
 Döngü çalışma kitabındaki her çalışma sayfasından geçer.`ActiveSheetIndex` döngü boyunca her seferinde geçerli çalışma sayfasını kaydedecek şekilde ayarlanmıştır. Sonuçlar bir`MemoryStream`.
## Adım 6: Çalışma Sayfası Verilerini Alın
 Bir çalışma sayfasını bellek akışına kaydettikten sonraki adım, bu verileri almak ve bunları çalışma sayfamıza eklemektir.`workbookData` sıralamak.
```csharp
    // Çalışma sayfası verilerini sayfa veri dizisine kaydedin
    ms.Position = 0; // Bellek akışının konumunu sıfırla
    byte[] sheetData = ms.ToArray(); // Bayt dizisini al
```
`ms.Position = 0;` yazmadan sonra okuma pozisyonunu sıfırlar. Sonra, kullanırız`ToArray()` bellek akışını çalışma sayfası verilerini tutan bir bayt dizisine dönüştürmek için.
## Adım 7: Çalışma Sayfası Verilerini Birleştirin
 Şimdi, her çalışma sayfasındaki verileri tek bir çalışma sayfasında birleştireceğiz.`workbookData` dizi daha önce başlatıldı.
```csharp
    // Bu çalışma sayfası verilerini çalışma kitabı veri dizisine birleştirin
    byte[] combinedArray = new byte[workbookData.Length + sheetData.Length];
    Array.Copy(workbookData, 0, combinedArray, 0, workbookData.Length);
    Array.Copy(sheetData, 0, combinedArray, workbookData.Length, sheetData.Length);
    workbookData = combinedArray;
}
```
Hem mevcut çalışma kitabı verilerini hem de yeni çalışma sayfası verilerini tutabilecek kadar büyük yeni bir dizi oluşturuyoruz. Daha sonra mevcut ve yeni verileri daha sonra kullanmak üzere bu birleşik diziye kopyalıyoruz.
## Adım 8: Tüm Çalışma Kitabı Verilerini Dosyaya Kaydet
 Son olarak, tüm veriler bir araya getirildiğinde`workbookData` dizi, bu diziyi belirtilen bir dosya yoluna kaydedebiliriz.
```csharp
//Tüm çalışma kitabı verilerini dosyaya kaydet
File.WriteAllBytes(dataDir + "out.txt", workbookData);
```
`WriteAllBytes` Birleştirilmiş bayt dizisini alır ve belirtilen dizindeki "out.txt" adlı bir metin dosyasına yazar.
## Çözüm
Ve işte oldu! Aspose.Cells for .NET kullanarak bir Excel çalışma kitabını CSV formatına başarıyla dönüştürdünüz. Bu işlem yalnızca verimli olmakla kalmaz, aynı zamanda Excel verilerinin daha fazla analiz veya raporlama için kolayca işlenmesine olanak tanır. Artık veri işleme görevlerinizi otomatikleştirebilir veya bu işlevselliği daha büyük uygulamalara entegre edebilirsiniz.
## SSS
### CSV dosyası için farklı ayraçlar kullanabilir miyim?
 Evet, değiştirebilirsiniz`opts.Separator` virgül veya boru gibi istediğiniz herhangi bir karaktere.
### Aspose.Cells'i kullanmak ücretsiz mi?
 Aspose.Cells ücretsiz değildir, ancak ücretsiz deneme alabilirsiniz[Burada](https://releases.aspose.com/).
### CSV dışında hangi formatlarda kaydedebilirim?
Aspose.Cells, XLSX, PDF ve daha fazlası dahil olmak üzere birden fazla formatta kaydetmenize olanak tanır.
### Aspose.Cells kullanarak büyük Excel dosyalarını işleyebilir miyim?
Evet, Aspose.Cells büyük dosyaları verimli bir şekilde işlemek için tasarlanmıştır, ancak performans sistem kaynaklarına bağlı olabilir.
### Daha detaylı dokümanları nerede bulabilirim?
Kapsamlı dokümanları ve örnekleri şu adreste bulabilirsiniz:[referans sitesi](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
