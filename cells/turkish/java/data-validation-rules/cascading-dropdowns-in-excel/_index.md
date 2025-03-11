---
title: Excel'de Basamaklı Açılır Listeler
linktitle: Excel'de Basamaklı Açılır Listeler
second_title: Aspose.Cells Java Excel İşleme API'si
description: Aspose.Cells for Java kullanarak Excel'de basamaklı açılır listelerin nasıl oluşturulacağını öğrenin. Bu adım adım kılavuz, verimli Excel elektronik tablosu düzenlemesi için kaynak kodu ve uzman ipuçları sağlar.
weight: 13
url: /tr/java/data-validation-rules/cascading-dropdowns-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'de Basamaklı Açılır Listeler


## Excel'de Basamaklı Açılır Listelere Giriş

Elektronik tablo düzenleme dünyasında, Java için Aspose.Cells, geliştiricilerin Excel dosyalarıyla verimli bir şekilde çalışmasını sağlayan güçlü bir araç takımı olarak öne çıkıyor. Sunduğu ilgi çekici özelliklerden biri, Excel'de basamaklı açılır listeler oluşturma yeteneğidir ve kullanıcıların önceki bir seçime göre seçenekleri dinamik olarak seçmelerine olanak tanır. Bu adım adım kılavuzda, Java için Aspose.Cells kullanarak basamaklı açılır listeler uygulama sürecine dalacağız. Hadi başlayalım!

## Ön koşullar

Bu yolculuğa çıkmadan önce aşağıdaki ön koşulların mevcut olduğundan emin olun:

-  Java için Aspose.Cells: İndirin ve kurun[Burada](https://releases.aspose.com/cells/java/).
- Java Geliştirme Ortamı: Makinenizde bir Java geliştirme ortamının kurulu olması gerekir.
- Excel'in Temel Anlayışı: Excel'e ve temel kavramlarına aşinalık faydalı olacaktır.

## Sahneyi Hazırlamak

Amacımız, basamaklı açılır listeler içeren bir Excel sayfası oluşturmaktır. Ülkelerin bir listesinin olduğu ve bir ülke seçtiğinizde, o ülkedeki şehirlerin bir listesinin seçilebileceği bir senaryoyu hayal edin. Bunu başarmak için gereken adımları parçalayalım.

## Adım 1: Excel Çalışma Kitabını Oluşturma

Öncelikle Java için Aspose.Cells kullanarak bir Excel çalışma kitabı oluşturalım. İki sayfa ekleyeceğiz: biri ülke listesi için, diğeri şehir listesi için.

```java
// Excel çalışma kitabı oluşturmak için Java kodu
Workbook workbook = new Workbook();
Worksheet countrySheet = workbook.getWorksheets().get(0);
countrySheet.setName("Countries");
Worksheet citySheet = workbook.getWorksheets().add("Cities");
```

## Adım 2: Verilerin Doldurulması

Şimdi, çalışma sayfalarımızı verilerle doldurmamız gerekiyor. "Ülkeler" sayfasında ülkeleri listeleyeceğiz ve "Şehirler" sayfasında başlangıçta boş bırakacağız çünkü daha sonra dinamik olarak dolduracağız.

```java
//"Ülkeler" sayfasını doldurmak için Java kodu
countrySheet.getCells().get("A1").putValue("Country");
countrySheet.getCells().get("A2").putValue("USA");
countrySheet.getCells().get("A3").putValue("Canada");
countrySheet.getCells().get("A4").putValue("UK");
// Gerektiğinde daha fazla ülke ekleyin
```

## Adım 3: Açılır Listeleri Oluşturma

Sonra, ülke ve şehir sütunları için açılır listeler oluşturacağız. Bu açılır listeler, bir ülke seçildiğinde şehir açılır listesinin buna göre güncelleneceği şekilde birbirine bağlanacak.

```java
// Açılır listeler oluşturmak için Java kodu
DataValidationCollection validations = countrySheet.getDataValidations();
DataValidation validation = validations.get(validations.add(1, 1, countrySheet.getCells().getMaxDataRow(), 1));
validation.setType(DataValidationType.LIST);
validation.setFormula1("Countries!$A$2:$A$4"); // Ülke listesine referans
```

## Adım 4: Basamaklı Açılır Listeleri Uygulama

Şimdi heyecan verici kısım geliyor: basamaklı açılır menüleri uygulama. Şehir açılır menüsünü seçili ülkeye göre dinamik olarak güncellemek için Java için Aspose.Cells kullanacağız.

```java
// Basamaklı açılır menüleri uygulamak için Java kodu
countrySheet.getCells().setCellObserver(new ICellObserver() {
    @Override
    public void cellChanged(Cell cell) {
        if (cell.getName().equals("B2")) {
            // Önceki şehir açılır menüsünü temizle
            citySheet.getCells().get("B2").setValue("");
            
            // Seçilen ülkeyi belirleyin
            String selectedCountry = cell.getStringValue();
            
            // Seçilen ülkeye göre şehir açılır listesini doldurun
            switch (selectedCountry) {
                case "USA":
                    validation.setFormula1("Cities!$A$2:$A$4"); // ABD şehirleriyle doldurun
                    break;
                case "Canada":
                    validation.setFormula1("Cities!$B$2:$B$4"); // Kanada şehirlerini doldurun
                    break;
                case "UK":
                    validation.setFormula1("Cities!$C$2:$C$4"); // İngiltere şehirleriyle doldurun
                    break;
                // Diğer ülkeler için daha fazla vaka ekleyin
            }
        }
    }
});
```

## Çözüm

Bu kapsamlı kılavuzda, Aspose.Cells for Java kullanarak Excel'de basamaklı açılır listelerin nasıl oluşturulacağını inceledik. Ön koşulları ayarlayarak, Excel çalışma kitabını oluşturarak, verileri doldurarak başladık ve ardından açılır listeler oluşturmanın ve dinamik basamaklı davranışı uygulamanın inceliklerine daldık. Bir geliştirici olarak artık Excel dosyalarınızı etkileşimli açılır listelerle zenginleştirmek ve sorunsuz bir kullanıcı deneyimi sağlamak için gereken bilgi ve araçlara sahipsiniz.

## SSS

### Açılır listelere daha fazla ülke ve şehir nasıl ekleyebilirim?

Daha fazla ülke ve şehir eklemek için Excel çalışma kitabınızdaki ilgili sayfaları güncellemeniz gerekir. "Ülkeler" ve "Şehirler" sayfalarındaki listeleri genişletmeniz yeterlidir ve açılır listeler otomatik olarak yeni girdileri içerecektir.

### Bu tekniği diğer Excel özellikleriyle birlikte kullanabilir miyim?

Kesinlikle! Koşullu biçimlendirme, formüller ve grafikler gibi çeşitli Excel özelliklerini basamaklı açılır listelerle birleştirerek özel ihtiyaçlarınıza göre uyarlanmış güçlü ve etkileşimli elektronik tablolar oluşturabilirsiniz.

### Aspose.Cells for Java hem küçük hem de büyük ölçekli projeler için uygun mudur?

Evet, Aspose.Cells for Java çok yönlüdür ve her boyuttaki projede kullanılabilir. İster küçük bir yardımcı program, ister karmaşık bir kurumsal uygulama üzerinde çalışıyor olun, Aspose.Cells for Java Excel ile ilgili görevlerinizi kolaylaştırabilir.

### Aspose.Cells for Java ile basamaklı açılır menüleri uygulamak için gelişmiş programlama becerilerine ihtiyacım var mı?

Java'ya dair temel bir anlayış faydalı olsa da, Aspose.Cells for Java, süreçte size rehberlik etmek için kapsamlı belgeler ve örnekler sunar. Biraz özveri ve pratik ile bu özelliği ustalıkla kullanabilirsiniz.

### Aspose.Cells for Java için daha fazla kaynak ve belgeyi nerede bulabilirim?

 Java için Aspose.Cells'e ilişkin kapsamlı belgelere ve kaynaklara şu adresten erişebilirsiniz:[Burada](https://reference.aspose.com/cells/java/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
