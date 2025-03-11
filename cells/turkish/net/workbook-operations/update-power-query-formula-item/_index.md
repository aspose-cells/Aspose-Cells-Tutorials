---
title: Çalışma Kitabında Power Query Formül Öğesini Güncelle
linktitle: Çalışma Kitabında Power Query Formül Öğesini Güncelle
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu kapsamlı adım adım kılavuzda Aspose.Cells for .NET ile Excel'de Power Query formüllerinin nasıl güncelleneceğini öğrenin.
weight: 27
url: /tr/net/workbook-operations/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Çalışma Kitabında Power Query Formül Öğesini Güncelle

## giriiş
Excel'de Power Query kullanarak verileri verimli bir şekilde nasıl yöneteceğinizi anlamak, herhangi bir veri analisti veya Excel tutkunu için çok önemlidir. Power Query çalışma kitabınızdaki formül öğelerini güncellemeniz gerektiyse, doğru yerdesiniz. Bu kılavuz, bir Excel çalışma kitabındaki Power Query formüllerini sorunsuz bir şekilde güncellemek için Aspose.Cells for .NET'i nasıl kullanacağınızı öğrenmenize yardımcı olmak için tasarlanmıştır. Birkaç basit adımla verilerinizi düzenleyebilir ve düzene sokabilir, çalışma kitaplarınızın dinamik ve merkezi kalmasını sağlayabilirsiniz.
## Ön koşullar
Örnek kod ve adımlara dalmadan önce, neye ihtiyacınız olacağını gözden geçirelim:
1. C# ve .NET'in Temel Anlayışı: Biraz kod yazacağımız için C# programlama kavramlarına aşina olmanız faydalı olacaktır.
2.  .NET için Aspose.Cells'i yükleyin: .NET projenize Aspose.Cells kütüphanesinin entegre olması gerekir. İndirebilirsiniz[Burada](https://releases.aspose.com/cells/net/).
3. Değişikliğe Hazır Bir Excel Dosyası: Güncellemek istediğiniz bir Power Query içeren bir Excel dosyanız olduğundan emin olun. Aşağıdaki gibi bir örnek çalışma kitabına sahip olmanız gerekir:`SamplePowerQueryFormula.xlsx` Emrinizde.
## Paketleri İçe Aktar
Başlamak için, C# dosyanızda aşağıdaki ad alanlarının bulunduğundan emin olun:
```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```
Bu, özellikle çalışma kitapları ve Power Query verileriyle çalışmak için Aspose.Cells kitaplığının sağladığı işlevlere erişmenizi sağlayacaktır.
## Adım 1: Çalışma Dizinlerinizi Ayarlayın
İlk önce kaynak ve çıktı dosyalarınızın nerede bulunacağını tanımlamanız gerekir. 
```csharp
string SourceDir = "Your Document Directory";
string outputDir = "Your Document Directory";
```
 Bu adımda dizin yollarını belirtirsiniz. Değiştir`"Your Document Directory"` Excel dosyalarınızın kaydedildiği gerçek yol ile. Bu, programa kaynak dosyanızı nerede arayacağını ve güncellenmiş olanı nereye kaydedeceğini söyler.
## Adım 2: Çalışma Kitabını Yükleyin
Artık çalışma dizinlerinizi ayarladığınıza göre, bir sonraki adım Excel dosyanızı programa yüklemektir.
```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 Burada bir tane yaratıyorsunuz`Workbook` belirtilen Excel dosyasını yükleyen nesne.`Workbook`sınıfı, Aspose.Cells kütüphanesinin bir parçasıdır ve Excel dosyası üzerinde gerçekleştireceğiniz tüm işlemler için gereklidir.
## Adım 3: Power Query Verilerine Erişim
Çalışma kitabı yüklendikten sonra, içinde saklanan Power Query formüllerine erişmenin zamanı geldi.
```csharp
DataMashup mashupData = workbook.DataMashup;
```
 Bu satırda,`DataMashup` özellik, çalışma kitabındaki Power Query veri yapılarına erişmenize yardımcı olur. Bu özellik, Excel dosyanızda bulunan Power Query verilerinin çeşitli yönleriyle etkileşim kurma yeteneği sağlar.
## Adım 4: Power Query Formüllerinde Döngü
Power Query verilerine erişildikten sonraki adım, mevcut formüllerin her birini yinelemektir.
```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```
 İşte sihrin gerçekleştiği yer burası. Her bir döngüde`PowerQueryFormula` ve sonra her biri aracılığıyla`PowerQueryFormulaItem` .`if` ifadesi "Kaynak" adlı formül öğesini arar ve değerini Power Query'nin başvurmasını istediğiniz kaynak dosyasının yolu olacak şekilde günceller. Bu, Power Query'nin verileri hangi dosyadan çektiğini dinamik olarak değiştirmenize olanak tanır.
## Adım 5: Güncellenen Çalışma Kitabını Kaydedin
Gerekli formül öğelerini güncelledikten sonra son adımınız Çalışma Kitabını kaydetmektir.
```csharp
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
```
Bu satır, değiştirilen çalışma kitabını yeni bir dosyaya kaydeder, böylece orijinali korurken güncellenmiş sürümle çalışmanıza olanak tanır.
## Adım 6: Onay Mesajı
Son olarak, kodunuzun düzgün çalışıp çalışmadığını kontrol etmek iyi bir uygulamadır.
```csharp
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
Bu basit mesaj konsolda işleminizin başarılı olduğunu teyit edecek ve sürecin güven verici bir şekilde sonlanmasını sağlayacaktır.
## Çözüm
İşte karşınızda! Aspose.Cells for .NET kullanarak Excel'deki Power Query formül öğelerini güncellemek sadece birkaç basit adımda yapılabilir. Bu kılavuzu izleyerek Excel veri bağlantılarınızı etkili bir şekilde yönetebilir ve çalışma kitaplarınızın sorunsuz çalışmasını sağlayabilirsiniz. İster deneyimli bir profesyonel olun ister veri işlemede yeni başlıyor olun, Aspose.Cells Excel iş akışlarını otomatikleştirmek ve geliştirmek için güçlü bir yol sunar. 
## SSS
### Aspose.Cells'i herhangi bir .NET sürümüyle kullanabilir miyim?
Aspose.Cells, .NET Framework ve .NET Core dahil olmak üzere .NET'in birden fazla sürümüyle uyumludur.
### Aspose.Cells'i kullanmak ücretsiz mi?
 Aspose.Cells ücretsiz deneme sunuyor ancak sürekli kullanım için lisans gerekiyor. Geçici bir lisans alabilirsiniz[Burada](https://purchase.aspose.com/temporary-license/).
### Mevcut Excel dosyamda Power Query yoksa ne olur?
Açıklanan işlem Power Query öğelerinin güncellenmesine odaklanır, bu nedenle dosyanızda bunlar yoksa öncelikle Power Query'yi eklemeniz gerekir.
### Aspose.Cells hakkında daha fazla bilgiyi nerede bulabilirim?
 Kapsamlı rehberlik ve örnekler için belgeleri kontrol edin. Ziyaret edin[belgeleme](https://reference.aspose.com/cells/net/).
### Aspose.Cells ile ilgili hataları veya sorunları nasıl bildirebilirim?
Karşılaştığınız herhangi bir sorunla ilgili yardım almak için desteklenen forumlarına ulaşabilirsiniz.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
