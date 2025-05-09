---
"description": "Aspose.Cells for .NET'i adım adım talimatlarla kullanarak Excel dosyasında sürüm, yazar ve başlık gibi belge özelliklerinin programlı olarak nasıl belirleneceğini öğrenin."
"linktitle": "Excel Dosyasının Belge Sürümünün .NET'te Programatik Olarak Belirlenmesi"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel Dosyasının Belge Sürümünün .NET'te Programatik Olarak Belirlenmesi"
"url": "/tr/net/saving-and-exporting-excel-files-with-options/specifying-document-version-of-excel-file/"
"weight": 12
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel Dosyasının Belge Sürümünün .NET'te Programatik Olarak Belirlenmesi

## giriiş
Aspose.Cells for .NET, geliştiricilerin Excel dosyalarını kolaylıkla programatik olarak düzenlemelerine olanak tanıyan güçlü bir kütüphanedir. İster sıfırdan Excel dosyaları oluşturmak, ister mevcut olanları değiştirmek isteyin, Aspose.Cells hedeflerinize ulaşmanız için kapsamlı bir API sunar. Bu özelliklerden biri de sürüm, yazar veya başlık gibi belge özelliklerini belirtmektir. Bu eğitim, Aspose.Cells for .NET kullanarak bir Excel dosyasının belge sürümünü programatik olarak nasıl belirteceğinizi gösterecektir.
## Ön koşullar
Ayrıntılara dalmadan önce, bu eğitimi takip etmek için ihtiyacınız olan her şeye sahip olduğunuzdan emin olalım:
1. Aspose.Cells for .NET: En son sürümü indirebilirsiniz [Burada](https://releases.aspose.com/cells/net/)Henüz bir lisans satın almadıysanız, bir lisans satın alabilirsiniz. [geçici lisans](https://purchase.aspose.com/temporary-license/) Özellikleri keşfetmek için.
2. .NET Geliştirme Ortamı: Visual Studio veya herhangi bir .NET uyumlu IDE'yi kullanabilirsiniz.
3. Temel C# Bilgisi: C# programlamayı anlamak, takip etmeyi kolaylaştıracaktır.
## Paketleri İçe Aktar
Kodlamaya başlamadan önce, Aspose.Cells kütüphanesinden gerekli ad alanlarını içe aktarmanız gerekir. Bu, Excel dosya düzenlemesi için gereken sınıflara ve yöntemlere erişmenizi sağlayacaktır.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
Bu iki ad alanı, çalışma kitabı ve yerleşik belge özellikleriyle etkileşim kurmak için önemli olacaktır.
Şimdi, bir Excel dosyasında sürüm, başlık ve yazar gibi belge özelliklerini belirtme sürecini parçalara ayıralım.
## Adım 1: Çalışma Kitabı Nesnesini Başlatın
İlk adım, yeni bir örnek oluşturmaktır `Workbook` nesne. Bu nesne, üzerinde çalışacağınız tüm Excel dosyasını temsil eder.
```csharp
Workbook wb = new Workbook();
```
The `Workbook` sınıfı bir Excel dosyasının bir gösterimini sağlar. Bunu örnekleyerek, üzerinde değişiklik yapabileceğimiz boş bir Excel çalışma kitabı oluştururuz.
## Adım 2: Yerleşik Belge Özelliklerine Erişim
Aspose.Cells, başlık, yazar ve belge sürümü gibi alanları içeren yerleşik belge özellikleri sunar. Bu özelliklere şuradan erişebilirsiniz: `BuiltInDocumentProperties` koleksiyon.
```csharp
Aspose.Cells.Properties.BuiltInDocumentPropertyCollection bdpc = wb.BuiltInDocumentProperties;
```
The `BuiltInDocumentPropertyCollection` sınıf, başlık, yazar ve genellikle belgeyle ilişkilendirilen diğer meta veriler gibi yerleşik belge özelliklerinin bir koleksiyonuna erişim sağlar.
## Adım 3: Excel Belgesinin Başlığını Ayarlayın
Sonra, Excel belgesinin başlığını ayarlayacağız. Bu meta veriler, dosyanın daha sonra tanımlanmasına ve yönetilmesine yardımcı olur.
```csharp
bdpc.Title = "Aspose File Format APIs";
```
Başlığı ayarlamak belge organizasyonu için önemlidir. Bu meta veriler dosya özelliklerinde görülebilir ve harici sistemler tarafından belgeyi daha etkili bir şekilde kataloglamak veya tanımlamak için kullanılabilir.
## Adım 4: Yazarı Belirleyin
Belgenin yazarı, dosyayı kimin oluşturduğunu veya değiştirdiğini yansıtacak şekilde de belirtilebilir.
```csharp
bdpc.Author = "Aspose APIs Developers";
```
Bu adım, belgenin yaratıcısına atanmasına yardımcı olur ve belge yönetimi veya iş birliği senaryoları için ek meta veri sağlar.
## Adım 5: Belge Sürümünü Belirleyin
Bu eğitimde ele aldığımız en önemli özelliklerden biri belge sürümüdür. Bu adım, sürüm denetimi gerektiren ortamlarda çalışırken faydalı olan belgenin sürümünü belirtmenize olanak tanır.
```csharp
bdpc.DocumentVersion = "Aspose.Cells Version - 18.3";
```
Belge sürümünün ayarlanması, dosyayı oluşturmak için belgenin veya kitaplığın hangi sürümünün kullanıldığına ilişkin netlik sağlar. Bu, özellikle dosya revizyonlarını veya farklı kitaplık sürümleriyle uyumluluğu izlemesi gereken ortamlarda önemlidir.
## Adım 6: Excel Dosyasını Kaydedin
Son olarak, Excel dosyasını az önce ayarladığınız tüm özelliklerle kaydedebilirsiniz. Aspose.Cells dosyayı çeşitli biçimlerde kaydetmenize olanak tanır, ancak bu örnek için, `.xlsx` Biçim.
```csharp
wb.Save("outputSpecifyDocumentVersionOfExcelFile.xlsx", SaveFormat.Xlsx);
```
The `Save` yöntemi dosyayı belirtilen dizine kaydetmek için kullanılır. Burada, dosyayı bir Excel dosyası olarak kaydediyoruz `.xlsx` biçimi. Gerekirse, Aspose.Cells ayrıca şu biçimleri de destekler: `.xls`, `.csv`, Ve `.pdf`Projenizin ihtiyaçlarına göre esneklik sağlar.
## Çözüm
Bu eğitimde, .NET için Aspose.Cells kullanarak bir Excel dosyasında belge özelliklerinin, özellikle de belge sürümünün nasıl belirleneceğini ele aldık. Aspose.Cells, Excel dosyalarını programatik olarak düzenlemenize olanak tanıyan son derece esnek ve güçlü bir araçtır ve bu da onu elektronik tablolarla çalışan herhangi bir .NET geliştiricisi için harika bir varlık haline getirir.
## SSS
### Aspose.Cells'i kullanarak diğer yerleşik özellikleri değiştirebilir miyim?  
Evet, konu, anahtar sözcükler, yorumlar gibi diğer yerleşik özellikleri de değiştirebilirsiniz.
### Aspose.Cells hangi dosya formatlarını destekliyor?  
Aspose.Cells, aşağıdakiler de dahil olmak üzere çok çeşitli biçimleri destekler: `.xls`, `.xlsx`, `.csv`, `.pdf`ve daha fazlası.
### Aspose.Cells for .NET'i kullanmak için lisansa ihtiyacım var mı?  
Aspose.Cells'i şu şekilde keşfedebilirsiniz: [ücretsiz deneme](https://releases.aspose.com/) veya başvuruda bulunun [geçici lisans](https://purchase.aspose.com/temporary-license/) Genişletilmiş testler için.
### Aspose.Cells'i bir web uygulamasında kullanabilir miyim?  
Evet, Aspose.Cells hem masaüstü hem de web uygulamalarında kullanılabilir. Oldukça çok yönlüdür ve .NET web çerçeveleriyle iyi entegre olur.
### Aspose.Cells için desteği nereden alabilirim?  
Topluluğa ve desteğe şu şekilde erişebilirsiniz: [Aspose.Cells destek forumu](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}