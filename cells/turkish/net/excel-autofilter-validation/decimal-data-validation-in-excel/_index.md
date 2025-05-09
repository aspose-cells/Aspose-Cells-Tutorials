---
"description": "Kolay takip edilebilir kılavuzumuzla Aspose.Cells for .NET kullanarak Excel'de ondalık veri doğrulamasını nasıl uygulayacağınızı keşfedin. Veri bütünlüğünü zahmetsizce geliştirin."
"linktitle": "Excel'de Ondalık Veri Doğrulaması"
"second_title": "Aspose.Cells .NET Excel İşleme API'si"
"title": "Excel'de Ondalık Veri Doğrulaması"
"url": "/tr/net/excel-autofilter-validation/decimal-data-validation-in-excel/"
"weight": 11
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Ondalık Veri Doğrulaması

## giriiş

Herhangi bir işte net iletişim için doğru verilerle elektronik tablolar oluşturmak esastır. Veri doğruluğunu sağlamanın bir yolu Excel'de veri doğrulamanın kullanılmasıdır. Bu eğitimde, verilerinizi güvenilir ve temiz tutan bir ondalık veri doğrulama mekanizması oluşturmak için Aspose.Cells for .NET'in gücünden yararlanacağız. Excel oyununuzu geliştirmek istiyorsanız, doğru yerdesiniz!

## Ön koşullar

Koda dalmadan önce, sorunsuz bir yolculuk deneyimi için her şeyin ayarlandığından emin olun:

1. Visual Studio: Henüz yapmadıysanız Visual Studio'yu indirin ve kurun. .NET uygulamaları geliştirmek için mükemmel bir ortamdır.
2. .NET için Aspose.Cells: Projenize Aspose.Cells kütüphanesinin eklenmesi gerekir. Bunu şuradan indirebilirsiniz: [bu bağlantı](https://releases.aspose.com/cells/net/).
3. Temel C# Bilgisi: Her ne kadar her şeyi adım adım açıklasak da, C# programlamanın temellerine dair bir anlayışa sahip olmak, kavramları daha iyi kavramanızı sağlayacaktır.
4. .NET Framework: Aspose.Cells ile uyumlu gerekli .NET Framework'ün yüklü olduğundan emin olun.
5. Kütüphaneler: Derleme hatalarından kaçınmak için projenizde Aspose.Cells kütüphanesine başvurun.

Temelleri ele aldığımıza göre, şimdi heyecan verici kısma, yani kodlamaya geçebiliriz.

## Paketleri İçe Aktar

Başlamak için, gerekli paketleri C# dosyanıza aktarmanız gerekir. Bu, Aspose.Cells işlevlerine erişmenizi sağlar.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Dosyanızın en üstüne bu satırı ekleyerek, C#'a Excel dosyalarını düzenlemenize olanak tanıyan Aspose.Cells işlevselliğini aramasını söylüyorsunuz.

Artık ortamı hazırladığımıza göre, Excel çalışma sayfasında ondalık veri doğrulaması oluşturmak için gereken adımları inceleyelim.

## Adım 1: Belge Dizininizi Ayarlayın

Herhangi bir dosyayı kaydedebilmeniz için, belge dizininizin doğru şekilde ayarlandığından emin olmanız gerekir:

```csharp
string dataDir = "Your Document Directory";
```

Yer değiştirmek `"Your Document Directory"` Excel dosyalarınızı kaydetmek istediğiniz yolu yazın.

## Adım 2: Dizin Varlığını Kontrol Edin

Bu kod parçası dizinin var olup olmadığını kontrol eder ve yoksa oluşturur:

```csharp
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```

Bu adım, yeni bir projeye başlamadan önce çalışma alanınızın hazır olduğundan emin olmak gibidir. Dağınıklık yok, stres yok!

## Adım 3: Bir Çalışma Kitabı Nesnesi Oluşturun

Şimdi, özünde bir Excel dosyası olan yeni bir çalışma kitabı nesnesi oluşturalım:

```csharp
Workbook workbook = new Workbook();
```

Bir çalışma kitabını verileriniz için boş bir tuval olarak düşünün. Bu noktada, içeriği yoktur ancak boyanmaya hazırdır.

## Adım 4: Çalışma Sayfasını Oluşturun ve Erişim Sağlayın


Şimdi bir çalışma sayfası oluşturalım ve çalışma kitabındaki ilk sayfaya erişelim:

```csharp
Worksheet ExcelWorkSheet = workbook.Worksheets[0];
```

Bir kitabın birden fazla sayfası olduğu gibi, bir çalışma kitabının da birden fazla çalışma sayfası olabilir. Şu anda birincisine odaklanıyoruz.

## Adım 5: Doğrulama Koleksiyonunu Edinin

Şimdi, veri doğrulama kurallarımızı yöneteceğimiz yer burası olduğundan, çalışma sayfasından doğrulama koleksiyonunu çekelim:

```csharp
ValidationCollection validations = ExcelWorkSheet.Validations;
```

Bu adım, bir projeye başlamadan önce araç kutunuzu kontrol etmeye benzer.

## Adım 6: Doğrulama için Hücre Alanını Tanımlayın

Doğrulamanın uygulanacağı alanı tanımlamamız gerekiyor:

```csharp
CellArea ca = new CellArea();
ca.StartRow = 0;
ca.EndRow = 0;
ca.StartColumn = 0;
ca.EndColumn = 0;
```

Burada, veri doğrulamasının tek bir hücreye, özellikle çalışma sayfasındaki ilk hücreye (A1) uygulanmasını şart koşuyoruz.

## Adım 7: Doğrulama Oluşturun ve Ekleyin

Doğrulama nesnemizi oluşturalım ve doğrulamalar koleksiyonuna ekleyelim:

```csharp
Validation validation = validations[validations.Add(ca)];
```

Şimdi ondalık koşullarımızı zorunlu kılmak için yapılandıracağımız bir doğrulama nesnemiz var.

## Adım 8: Doğrulama Türünü Ayarlayın

Daha sonra, istediğimiz doğrulama türünü belirteceğiz:

```csharp
validation.Type = ValidationType.Decimal;
```

Türü Ondalık olarak ayarlayarak Excel'e doğrulanan hücrede ondalık değerleri beklemesini söylüyoruz.

## Adım 9: Operatörü Belirleyin

Şimdi, izin verilen değerler için koşulu belirteceğiz. Girilen verilerin iki aralık arasında olduğundan emin olmak istiyoruz:

```csharp
validation.Operator = OperatorType.Between;
```

Bunu bir sınır çizgisi çizmek olarak düşünün. Bu aralığın dışındaki herhangi bir sayı reddedilecek ve verileriniz temiz kalacaktır!

## Adım 10: Doğrulama için Sınırları Belirleyin

Şimdi doğrulamamız için alt ve üst limitleri belirleyeceğiz:

```csharp
validation.Formula1 = Decimal.MinValue.ToString();
validation.Formula2 = Decimal.MaxValue.ToString();
```

Bu sınırlamalarla, geçerli olduğu sürece, ne kadar büyük veya küçük olursa olsun her ondalık sayı kabul edilir!

## Adım 11: Hata Mesajını Özelleştirme

Kullanıcıların girdilerinin neden reddedildiğini bir hata mesajı ekleyerek bilmelerini sağlayalım:

```csharp
validation.ErrorMessage = "Please enter a valid integer or decimal number";
```

Bu, ne girileceği konusunda rehberlik sağladığı için kullanıcı dostu bir deneyime yol açar.

## Adım 12: Doğrulama Alanını Tanımlayın

Şimdi bu doğrulamayı yapacak hücreleri belirleyelim:

```csharp
CellArea area;
area.StartRow = 0;
area.EndRow = 9;
area.StartColumn = 0;
area.EndColumn = 0;
```

Bu yapılandırmada doğrulamanın A1 hücresinden A10'a kadar uygulandığını söylüyoruz.

## Adım 13: Doğrulama Alanını Ekleyin

Doğrulama alanımızı tanımladığımıza göre şimdi uygulayalım:

```csharp
validation.AddArea(area);
```

Doğrulamanız artık yerinde ve uygunsuz girdileri yakalamaya hazır!

## Adım 14: Çalışma Kitabını Kaydedin

Son olarak, çalışma kitabını ondalık veri doğrulamamızı kullanarak kaydedelim:

```csharp
workbook.Save(dataDir + "output.out.xls");
```

Ve işte karşınızda! Aspose.Cells for .NET kullanarak ondalık veri doğrulaması içeren bir çalışma kitabını başarıyla oluşturdunuz.

## Çözüm

Bu basit adımları takip ettiğinizde, Aspose.Cells for .NET kullanarak Excel'de ondalık veri doğrulamasını uygulamak çocuk oyuncağıdır. Sadece verilerin temiz ve yapılandırılmış kalmasını sağlamakla kalmaz, aynı zamanda elektronik tablolarınızdaki genel veri bütünlüğünü de iyileştirerek güvenilir ve kullanıcı dostu hale getirirsiniz.
Finans, proje yönetimi veya veri raporlamasını kullanan herhangi bir alanda olun, bu becerilerde ustalaşmak üretkenliğinizi önemli ölçüde artıracaktır. O halde devam edin, deneyin! Elektronik tablolarınız size teşekkür edecek.

## SSS

### Excel'de veri doğrulama nedir?
Excel'de veri doğrulama, belirli bir hücreye veya aralığa girilebilecek veri türünü kısıtlayarak veri bütünlüğünü sağlayan bir özelliktir.

### Veri doğrulamada hata mesajını özelleştirebilir miyim?
Evet! Yanlış veri girişleri yapıldığında kullanıcıları yönlendirmek için özel hata mesajları sağlayabilirsiniz.

### Aspose.Cells'i kullanmak ücretsiz mi?
Aspose.Cells ücretsiz deneme sunuyor ancak uzun süreli kullanım için bir lisansa ihtiyacınız olacak. Geçici bir lisans edinme hakkında daha fazla bilgi bulabilirsiniz [Burada](https://purchase.aspose.com/temporary-license/).

### Excel'de hangi veri türlerini doğrulayabilirim?
Aspose.Cells ile tam sayılar, ondalıklar, tarihler, listeler ve özel formüller dahil olmak üzere çeşitli veri türlerini doğrulayabilirsiniz.

### Aspose.Cells hakkında daha fazla dokümanı nerede bulabilirim?
Kapsamlı belgeleri inceleyebilirsiniz [Burada](https://reference.aspose.com/cells/net/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}