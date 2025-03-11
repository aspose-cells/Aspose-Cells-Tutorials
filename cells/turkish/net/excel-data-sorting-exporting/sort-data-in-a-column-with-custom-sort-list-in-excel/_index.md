---
title: Excel'de Özel Sıralama Listesiyle Bir Sütundaki Verileri Sıralama
linktitle: Excel'de Özel Sıralama Listesiyle Bir Sütundaki Verileri Sıralama
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Bu kapsamlı eğitimde, Aspose.Cells for .NET ile özel sıralama listesi kullanarak Excel'de verileri nasıl sıralayacağınızı öğrenin.
weight: 10
url: /tr/net/excel-data-sorting-exporting/sort-data-in-a-column-with-custom-sort-list-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Özel Sıralama Listesiyle Bir Sütundaki Verileri Sıralama

## giriiş

Bu eğitim, projenizi kurma, bir Excel dosyası yükleme ve özel bir sıralama düzeni kullanarak belirli bir aralıktaki verileri sıralama sürecinde size rehberlik edecektir. Bu kılavuzu izleyerek, veri yönetimi becerilerinizi ve Aspose.Cells kitaplığının kullanılabilirliğini artırabilecek uygulamalı deneyim kazanacaksınız.

## Ön koşullar

Eğitime başlamadan önce, sorunsuz bir öğrenme deneyimi için bazı ön koşulları ana hatlarıyla açıklayalım.

### C# Temel Bilgisi

Eğitim, sizi her adımda yönlendirmek için tasarlanmış olsa da, C# hakkında temel bir anlayışa sahip olmak, sunulan kavramları kavramanızı kolaylaştıracaktır.

### .NET Geliştirme Ortamı

Çalışan bir .NET geliştirme ortamı kurduğunuzdan emin olun. Visual Studio veya .NET geliştirmeyi destekleyen herhangi bir IDE kullanabilirsiniz.

### Aspose.Cells for .NET NuGet Paketi

Projenizde .NET için Aspose.Cells kütüphanesinin yüklü olması gerekir. Bunu NuGet Paket Yöneticisi aracılığıyla kolayca ekleyebilirsiniz. 

İşte bunu nasıl yapacağınız:

1. Projenizi Visual Studio’da açın.
2. "Araçlar" > "NuGet Paket Yöneticisi" > "Çözüm için NuGet Paketlerini Yönet" seçeneğine gidin.
3.  Arama`Aspose.Cells` ve en son sürümü yükleyin.

### Test için Temel Excel Dosyası

Çalışmak için bir örnek Excel dosyasına ihtiyacınız olacak. Rastgele ülke adları ve kodlarıyla basit bir Excel dosyası oluşturabilirsiniz.

## Paketleri İçe Aktar

Başlamak için gerekli paketleri projenize aktaralım. İşte kodunuzu nasıl kuracağınıza dair bir kesit:

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

Paketleri içeri aktardıktan sonra artık ilerlemeye hazırız.

## Adım 1: Kaynak ve Çıktı Dizinlerini Tanımlayın 

İlk adım, giriş dosyanızın nerede bulunduğunu ve çıktının (sıralanmış dosya) nerede kaydedilmesini istediğinizi tanımlamaktır. İki yol belirtmeniz gerekir: biri kaynak Excel dosyası için ve diğeri de sıralandıktan sonra çıktının kaydedilmesi için.

```csharp
string sourceDir = "Your Document Directory\\";
string outputDir = "Your Document Directory\\";
```

## Adım 2: Kaynak Excel Dosyasını Yükleyin

Sonra, sıralamak istediğiniz verileri içeren Excel dosyasını yükleyeceğiz. Bu, bir örneğin oluşturulmasıyla yapılır`Workbook` sınıf ve kaynak dosyanızın yolunu geçiriyoruz.

```csharp
Workbook wb = new Workbook(sourceDir + "sampleSortData_CustomSortList.xlsx");
```

## Adım 3: İlk Çalışma Sayfasına Erişim 

Dosya yüklendikten sonra, sıralamayı amaçladığımız verileri içeren belirli çalışma sayfasına erişmemiz gerekir. Bu durumda, ilk çalışma sayfasını hedefliyoruz.

```csharp
Worksheet ws = wb.Worksheets[0];
```

## Adım 4: Sıralanacak Hücre Alanını Belirleyin

 Sıralayacağımız hücre aralığını belirlememiz gerekiyor. Bu örnekte hücreleri A1'den A40'a kadar sıralayacağız.`CellArea.CreateCellArea` hücre alanını tanımlama yöntemi.

```csharp
CellArea ca = CellArea.CreateCellArea("A1", "A40");
```

## Adım 5: Özel Sıralama Listesi Oluşturun

Sıralamadan önce, özel sıralamamız için kullanacağımız ölçütleri belirlememiz gerekir. Sıralama listesini dizelerden oluşan bir dizi olarak tanımlayabilirsiniz. Özel sıralama listesi sıralamanın sırasını belirleyecektir.

```csharp
string[] customSortList = new string[] { "USA,US", "Brazil,BR", "China,CN", "Russia,RU", "Canada,CA" };
```

## Adım 6: Sıralama Anahtarını Ekleyin ve Sıralamayı Gerçekleştirin

Şimdi sıralama zamanı! Bunun için DataSorter sınıfını kullanacağız. Özel listemize göre sıralama için bir anahtar oluşturun ve sıralama işlemini yürütün.

```csharp
wb.DataSorter.AddKey(0, SortOrder.Ascending, customSortList);
wb.DataSorter.Sort(ws.Cells, ca);
```

## Adım 7: Çıktı Excel Dosyasını Kaydedin

Sıralama tamamlandıktan sonra son adım değişiklikleri yeni bir Excel dosyasına kaydetmektir. Çıktı dosya adını belirtin ve çalışma kitabını kaydedin.

```csharp
wb.Save(outputDir + "outputSortData_CustomSortList.xlsx");
```

## Adım 8: Başarılı Yürütmeyi Onaylayın

Her şeyin düzgün çalıştığından emin olmak için konsola bir onay mesajı yazdırabilirsiniz. Bu hata ayıklamada yardımcı olur ve işlemin başarılı olduğuna dair size memnuniyet verir.

```csharp
Console.WriteLine("SortDataInColumnWithCustomSortList executed successfully.\r\n");
```

## Çözüm

Ve işte oldu! Aspose.Cells for .NET ile özel bir sıralama listesi kullanarak Excel sütunundaki verileri başarıyla sıraladınız. Sıralama, verilerinize yapı ve netlik kazandırmaya yardımcı olarak analiz etmeyi ve yorumlamayı kolaylaştırır. Umarım bu kılavuz becerilerinizi bir üst seviyeye taşır ve Aspose.Cells'in Excel ile ilgili görevleriniz için ne kadar güçlü olabileceğini anlamanıza yardımcı olur.

## SSS

### Aspose.Cells for .NET nedir?
Aspose.Cells for .NET, Excel dosyalarını .NET uygulamaları içerisinde oluşturmanıza, düzenlemenize ve dönüştürmenize olanak tanıyan kapsamlı bir kütüphanedir.

### Özel sıralama listesini kullanarak birden fazla sütunu sıralayabilir miyim?
Evet! Gerekirse birden fazla sütuna göre sıralama yapmak için ek anahtarlar ekleyebilirsiniz, her anahtar için aynı prosedürü izlemeniz yeterlidir.

### Aspose.Cells'i kullanmak için C# hakkında ön bilgiye sahip olmam gerekir mi?
Yararlı olsa da, bu eğitimi takip edebilir ve ilerledikçe öğrenebilirsiniz! C# hakkında temel bir anlayışa sahip olmak öğrenme deneyiminizi geliştirecektir.

### Aspose.Cells için geçici lisans kullanmak mümkün müdür?
Kesinlikle! Kütüphanenin tüm özelliklerini kısıtlama olmadan test etmek istiyorsanız geçici bir lisans satın alabilirsiniz.

### Aspose.Cells için örnekleri veya dokümanları indirebilir miyim?
 Evet! Aspose, size büyük ölçüde yardımcı olabilecek kapsamlı belgeler ve örnek projeler sunar. Şuraya göz atın:[Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
