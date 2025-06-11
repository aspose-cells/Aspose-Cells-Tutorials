---
"description": "Bu detaylı adım adım eğitimde Aspose.Cells for .NET kullanarak Excel çalışma kitaplarından gömülü MOL dosyalarının nasıl çıkarılacağını öğrenin."
"linktitle": "Çalışma Kitabından Gömülü Mol Dosyasını Çıkarın"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Çalışma Kitabından Gömülü Mol Dosyasını Çıkarın"
"url": "/tr/net/workbook-operations/extract-embedded-mol-file/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabından Gömülü Mol Dosyasını Çıkarın

## giriiş
Excel çalışma kitaplarındaki verileri yönetmeye gelince, bazen standart bir formatta olmayan çeşitli gömülü nesnelerle karşılaşırsınız. Bu formatlardan biri, kimyada moleküler bilgileri temsil etmek için yaygın olarak kullanılan MOL'dur (Moleküler Yapı Dosyası). Bu MOL dosyalarını .NET için Aspose.Cells kullanarak bir Excel çalışma kitabından çıkarmak istiyorsanız, doğru kılavuza ulaştınız. Bu makalede, her bir parçayı adım adım açıklayarak sizi süreçte yönlendireceğiz.
## Ön koşullar
Koda dalmadan önce, gerekli becerilere ve araçlara sahip olduğunuzdan emin olmanız önemlidir. İşte ihtiyacınız olacaklar:
1. .NET Programlamanın Temel Anlayışı: C# ve .NET framework'üne aşina olmalısınız.
2. .NET için Aspose.Cells: Aspose.Cells kütüphanesine sahip olduğunuzdan emin olun. [buradan indirin](https://releases.aspose.com/cells/net/).
3. Bir IDE: Visual Studio'yu veya herhangi bir .NET uyumlu IDE'yi kullanabilirsiniz.
4. Gömülü MOL Dosyaları İçeren Excel Çalışma Kitabı: Bu eğitim için, MOL nesneleri içeren bir Excel dosyasına ihtiyacınız var. Kendi dosyanızı oluşturabilir veya herhangi bir örnek dosyayı kullanabilirsiniz.
## Paketleri İçe Aktar
Başlamak için projenize gerekli ad alanlarını içe aktarmanız gerekir. Bu, Aspose.Cells işlevlerine erişmek için önemlidir. Bunu nasıl yapabileceğiniz aşağıda açıklanmıştır:

```csharp
using Aspose.Cells.Drawing;
using Aspose.Cells.WebExtensions;
using System;
using System.IO;
```

Bu ad alanları, çalışma kitaplarını değiştirmenize, çalışma sayfalarına erişmenize ve genel olarak dosyalarla çalışmanıza olanak tanır.
Artık ön koşullarımızı tamamladığımıza göre koda dalalım ve Excel çalışma kitabından gömülü MOL dosyalarını çıkarmada yer alan her adımı anlayalım. 
## Adım 1: Dizinlerinizi Ayarlama
İlk adım kaynak belgenizin nerede bulunduğunu ve çıkarılan MOL dosyalarını nereye kaydetmek istediğinizi tanımlamaktır. Bu dizinleri ayarlayalım.
```csharp
string SourceDir = "Your Document Directory"; // Dizin yolunuzla değiştirin
string outputDir = "Your Document Directory"; // Çıkış yolunuzla değiştirin
```
Burada, siz değiştirin `"Your Document Directory"` gerçek dizinlerinize giden yol ile. Hem kaynak hem de çıktı dizinlerinin uygulamanız tarafından erişilebilir olması önemlidir.
## Adım 2: Çalışma Kitabını Yükleme
Dizinlerinizi ayarladıktan sonra, bir sonraki görev Excel çalışma kitabını yüklemektir. Hadi şimdi bunu yapalım.

```csharp
Workbook workbook = new Workbook(SourceDir + "EmbeddedMolSample.xlsx");
```

Bir örneğini oluşturuyoruz `Workbook` sınıf ve Excel dosyamızın yolunu geçiriyoruz `EmbeddedMolSample.xlsx`Bu adım çalışma kitabını başlatır ve içeriğine erişmenizi sağlar.
## Adım 3: Çalışma Sayfaları Üzerinde Yineleme
Artık çalışma kitabınız yüklendiğine göre, çalışma kitabındaki her çalışma sayfasını dolaşmanız gerekir. Bu, her sayfayı gömülü nesneler açısından incelemenizi sağlar.

```csharp
var index = 1; // Çıkarılan MOL dosyalarını adlandırmak için kullanılır
foreach (Worksheet sheet in workbook.Worksheets)
{
    OleObjectCollection oles = sheet.OleObjects;
    // Daha fazla çıkarma mantığı buraya gelir
}
```

Burada, bir `foreach` çalışma sayfaları arasında gezinmek için döngü. Her çalışma sayfası için, `OleObjects` gömülü tüm nesneleri içeren koleksiyon.
## Adım 4: MOL Dosyalarını Çıkarma
Şimdi kritik kısım geliyor: OLE nesnelerinden MOL dosyalarını çıkarmak. Bu, çalışma sayfası döngüsünün içinde başka bir döngü gerektirir.

```csharp
foreach (OleObject ole in oles)
{
    string fileName = outputDir + "OleObject" + index + ".mol ";
    FileStream fs = File.Create(fileName);
    fs.Write(ole.ObjectData, 0, ole.ObjectData.Length);
    fs.Close();
    index++;
}
```

Bulduğunuz her OLE nesnesi için çıktı dizininde yeni bir dosya oluşturuyorsunuz. `ObjectData` mülkiyeti `OleObject` gömülü nesnenin verilerini tutar ve bunları yeni oluşturulan bir dosyaya bir `FileStream`Dosya sırayla adlandırılır (`OleObject1.mol`, `OleObject2.mol`, vb.) dayalı `index` değişken.
## Adım 5: İşlemin Tamamlandığının Onaylanması
Son olarak, tüm MOL dosyaları çıkarıldıktan sonra, işlemin başarıyla tamamlandığını kullanıcıya bildirmek iyi bir uygulamadır.

```csharp
Console.WriteLine("ExtractEmbeddedMolFile executed successfully.");
```

Bu satır, konsola basitçe çıkarma işleminin başarılı olduğunu bildiren bir mesaj yazdırır. Kullanıcı geri bildirimi için hoş bir dokunuştur.
## Çözüm
İşte karşınızda! Aspose.Cells for .NET kullanarak bir Excel çalışma kitabından gömülü MOL dosyalarını başarıyla çıkardınız. Bu süreç, gömülü nesneleri ele almak için yapılandırılmış bir yaklaşım sağlayan birkaç temel adımı birleştirir. İster bilimsel araştırma, ister kimyasal analiz veya sadece karmaşık veri kümeleriyle uğraşıyor olun, bu dosya türlerini çıkarabilmek ve işleyebilmek, bilgilerinizi yönetme şeklinizde önemli bir fark yaratabilir. 
## SSS
### Excel'den MOL dışında başka dosya türlerini de çıkarabilir miyim?
Evet, benzer tekniklerle çeşitli diğer gömülü dosya türlerini de çıkarabilirsiniz.
### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ticari bir kütüphanedir, ancak siz [sınırlı bir süre için ücretsiz deneyin](https://releases.aspose.com/).
### Bu yöntem tüm Excel versiyonlarında çalışıyor mu?
Evet, dosya biçimi Aspose.Cells tarafından desteklendiği sürece.
### Bu çıkarma işlemini otomatikleştirebilir miyim?
Kesinlikle! Bu süreci, kodu zamanlanmış bir göreve veya bir betiğe yerleştirerek otomatikleştirebilirsiniz.
### Aspose.Cells hakkında daha fazla dokümanı nerede bulabilirim?
Şunu kontrol edebilirsiniz: [Aspose.Cells belgeleri](https://reference.aspose.com/cells/net/) Daha fazla ayrıntı ve örnek için.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}