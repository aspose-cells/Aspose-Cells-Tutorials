---
category: general
date: 2026-03-30
description: Aspose.Cells kullanarak C#'ta Excel tarih‑saat değerlerini okurken tarihleri
  ISO formatına nasıl dönüştüreceğinizi ve Excel tarih‑saat verilerini nasıl çıkaracağınızı
  öğrenin.
draft: false
keywords:
- format date iso
- read excel datetime
- extract datetime excel
- Aspose.Cells date parsing
- Japanese era dates
language: tr
og_description: Aspose.Cells kullanarak Excel verilerinden ISO tarih formatı. Bu kılavuz,
  Excel tarih‑zamanını nasıl okuyacağınızı, tarih‑zaman Excel değerlerini nasıl çıkaracağınızı
  ve ISO tarihlerini nasıl çıktıya alacağınızı gösterir.
og_title: Excel'den ISO tarih biçimi – Adım Adım C# Öğreticisi
tags:
- C#
- Excel
- DateTime
- Aspose.Cells
title: Excel'den ISO tarih biçimlendirme – Tam C# Rehberi
url: /tr/net/excel-custom-number-date-formatting/format-date-iso-from-excel-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'den ISO tarih formatı – Tam C# Kılavuzu

Excel sayfasından tarihleri çekerken **format date iso** yapmanız gerektiğini hiç düşündünüz mü? Belki Japon dönemi tarihleriyle uğraşıyorsunuz ya da bir API yükü için temiz bir `yyyy‑MM‑dd` dizesi istiyorsunuz. Bu öğreticide **read Excel datetime** hücrelerini, **extract datetime Excel** değerlerini nasıl okuyacağınızı ve ISO‑8601 formatına nasıl dönüştüreceğinizi adım adım göreceksiniz—tahmin yürütmeye gerek yok.

Aspose.Cells kullanan gerçek bir örnek üzerinden ilerleyeceğiz, her satırın neden önemli olduğunu açıklayacağız ve projenize kopyalayıp yapıştırabileceğiniz son çıktıyı göstereceğiz. Sonuna geldiğinizde “令和3年5月1日” gibi garip dönem dizelerini işleyebilecek ve veritabanları, JSON veya ihtiyacınız olan herhangi bir yerde kullanabileceğiniz standart bir ISO tarih üretebileceksiniz.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework ile de çalışır)
- Aspose.Cells for .NET (ücretsiz deneme veya lisanslı sürüm)
- C# ve Excel kavramlarına temel aşinalık
- Visual Studio veya tercih ettiğiniz herhangi bir C# editörü

Aspose.Cells dışındaki ek NuGet paketlerine gerek yoktur, bu yüzden kurulum oldukça basittir.

---

## Adım 1: Bir Workbook Oluşturun ve İlk Çalışma Sayfasını Hedefleyin

İlk olarak yeni bir `Workbook` nesnesi oluşturursunuz. Bu, bir Excel dosyasının bellek içi temsilini sağlar; ardından bu nesneyi manipüle edebilir veya okuyabilirsiniz.

```csharp
using Aspose.Cells;
using System.Globalization;

// Step 1: Initialize a new workbook and grab the first worksheet
Workbook workbook = new Workbook();                 // creates an empty .xlsx
Worksheet worksheet = workbook.Worksheets[0];      // the default sheet is "Sheet1"
```

*Neden önemli:*  
Workbook'u programlı olarak oluşturmak, test sırasında fiziksel dosyalarla uğraşmanızı engeller. Ayrıca çalışma sayfası referansının her zaman geçerli olmasını sağlar—daha sonra **read Excel datetime** değerlerini okumaya çalıştığınızda null‑reference sürprizleri yaşamazsınız.

---

## Adım 2: Bir Hücreye Japon Dönemi Tarih Dizesi Yazın

Amacımız Gregoryen olmayan bir tarihi ayrıştırmayı göstermek. Dönem dizesini doğrudan **A1** hücresine yerleştireceğiz.

```csharp
// Step 2: Insert a Japanese era date string into cell A1
worksheet.Cells["A1"].PutValue("令和3年5月1日");
```

*İpucu:* Mevcut bir workbook'tan veri çekiyorsanız, `PutValue` çağrısını atlayıp zaten tarihi içeren hücreye başvurursunuz. Önemli olan, hücrenin Japon lunisolar takvimindeki bir tarihi temsil eden bir **string** tutmasıdır.

---

## Adım 3: Japon Lunisolar Takvimini Anlayan Bir Kültür Yapılandırın

.NET'in `CultureInfo` sınıfı, tarihlerin nasıl yorumlanacağını belirlemenizi sağlar. Varsayılan Gregoryen takvimi `JapaneseLunisolarCalendar` ile değiştirerek ayrıştırıcıya ihtiyaç duyduğu bağlamı sağlarsınız.

```csharp
// Step 3: Set up a culture using the Japanese lunisolar calendar
CultureInfo japaneseCulture = new CultureInfo("ja-JP");
japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();
```

*Neden bunu yapıyoruz:*  
Varsayılan kültürle “令和3年5月1日” ayrıştırmaya çalışırsanız, .NET bir `FormatException` fırlatır. Lunisolar takvimi kullanmak, çalışma zamanına “令和3年” (Reiwa döneminin 3. yılı) nasıl Gregorian yıl 2021'e eşleneceğini tam olarak söyler.

---

## Adım 4: Hücre Değerini Yapılandırılmış Kültür Kullanarak `DateTime` Olarak Ayrıştırın

Şimdi işlemin kalbine geliyoruz—bu dönem dizesini uygun bir `DateTime` nesnesine dönüştürmek. Aspose.Cells, bir `CultureInfo` kabul eden kullanışlı bir `GetDateTime` aşırı yüklemesi sunar.

```csharp
// Step 4: Retrieve the cell value as a DateTime, respecting the Japanese culture
DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);
```

*Arka planda neler oluyor:*  
`GetDateTime` ham dizeyi okur, sağlanan kültürün takvim kurallarını uygular ve aynı anı Gregorian takviminde temsil eden bir `DateTime` döndürür. İşte bu an, **extract datetime Excel** verilerini .NET içinde çalışabileceğiniz bir biçimde elde ettiğiniz zamandır.

---

## Adım 5: Ayrıştırılan Tarihi ISO 8601 Formatında Çıktılayın

Son olarak, `DateTime`'ı bir ISO dizesi olarak biçimlendiriyoruz—`yyyy‑MM‑dd`—ki bu, API'ler, veritabanları ve ön‑uç çerçeveler tarafından evrensel olarak kabul edilir.

```csharp
// Step 5: Print the date in ISO format (e.g., 2021-05-01)
Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // Output: 2021-05-01
```

*Neden ISO?*  
ISO 8601 belirsizliği ortadan kaldırır. “05/01/2021” yerel ayara bağlı olarak 1 Mayıs ya da 5 Ocak olabilir. `2021-05-01` ise tamamen açıktır; bu yüzden neredeyse her entegrasyon senaryosunda **format date iso** yaparız.

---

## Tam Çalışan Örnek

Aşağıda eksiksiz, çalıştırmaya hazır program bulunmaktadır. Bir console uygulaması projesine kopyalayın, Aspose.Cells referansını ekleyin ve **F5** tuşuna basın.

```csharp
using Aspose.Cells;
using System;
using System.Globalization;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and select the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date string into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // 3️⃣ Set up Japanese lunisolar culture
        CultureInfo japaneseCulture = new CultureInfo("ja-JP");
        japaneseCulture.DateTimeFormat.Calendar = new JapaneseLunisolarCalendar();

        // 4️⃣ Parse the cell value as DateTime using the culture
        DateTime parsedDate = worksheet.Cells["A1"].GetDateTime(japaneseCulture);

        // 5️⃣ Output the date in ISO format
        Console.WriteLine(parsedDate.ToString("yyyy-MM-dd")); // 2021-05-01
    }
}
```

**Beklenen çıktı**

```
2021-05-01
```

Bir kez çalıştırın, ISO‑formatlı tarihin konsola yazdırıldığını göreceksiniz. Bu, **read Excel datetime**'dan **format date iso**'ya kadar olan tüm işlem hattıdır.

---

## Yaygın Kenar Durumlarını Ele Alma

### 1. Gerçek Excel Tarih Sayılarını İçeren Hücreler

Bazen Excel tarihleri seri sayı olarak saklar (ör. `44204`). Bu durumda bir kültüre ihtiyacınız yoktur; sadece parametresiz `GetDateTime()` çağırın:

```csharp
DateTime serialDate = worksheet.Cells["B2"].GetDateTime(); // B2 holds a numeric date
Console.WriteLine(serialDate.ToString("yyyy-MM-dd"));
```

### 2. Boş veya Geçersiz Hücreler

Bir hücre boşsa veya ayrıştırılamayan bir dize içeriyorsa, `GetDateTime` bir istisna fırlatır. Çağrıyı bir `try/catch` bloğuna sarın veya önce `IsDateTime` kontrol edin:

```csharp
if (worksheet.Cells["C3"].Type == CellValueType.IsDateTime)
{
    DateTime safeDate = worksheet.Cells["C3"].GetDateTime();
    Console.WriteLine(safeDate.ToString("yyyy-MM-dd"));
}
else
{
    Console.WriteLine("Cell C3 does not contain a valid date.");
}
```

### 3. Farklı Dönem Biçimleri

Diğer Japon dönemleri (Heisei, Showa) aynı deseni izler. Aynı `JapaneseLunisolarCalendar` bunları otomatik olarak işler, bu yüzden ekstra mantığa gerek yoktur—sadece dizeyi besleyin.

---

## Profesyonel İpuçları ve Dikkat Edilmesi Gerekenler

- **Performance:** Büyük elektronik tabloları işlerken, bir döngü içinde yeni bir tane oluşturmak yerine tek bir `CultureInfo` örneğini yeniden kullanın.
- **Thread Safety:** `CultureInfo` nesneleri takvimi ayarladıktan sonra yalnızca‑okunur hâle gelir, bu yüzden çoklu iş parçacıkları arasında güvenle paylaşılabilir.
- **Aspose.Cells Licensing:** Ücretsiz deneme sürümünü kullanıyorsanız, deneme süresi dolduktan sonra bazı özelliklerin sınırlı olabileceğini unutmayın. Burada gösterilen tarih ayrıştırması hem deneme hem de lisanslı modda sorunsuz çalışır.
- **Time Zones:** Aldığınız `DateTime` **unspecified** (zaman dilimi belirtilmemiş) tipindedir. UTC'ye ihtiyacınız varsa, `DateTime.SpecifyKind(parsedDate, DateTimeKind.Utc)` çağırın veya `TimeZoneInfo` ile dönüştürün.

---

## Sonuç

Excel çalışma kitabından C# kullanarak **format date iso** yapmanız için gereken her şeyi ele aldık. Ham bir Japon dönemi dizesiyle başlayıp **read Excel datetime**, uygun kültürü ayarladık, **extract datetime excel** verilerini elde ettik ve sonunda temiz bir ISO‑8601 dizesi ürettik. Bu yaklaşım, Excel'in size sunabileceği herhangi bir tarih temsili—seri sayı, yerel‑özel dize ya da geleneksel bir dönem formatı—için çalışır.

Sonraki adımlar? Tüm bir tarih sütununu döngüye almayı, ISO sonuçlarını yeni bir sayfaya yazmayı ya da doğrudan bir web servisi için JSON yüküne eklemeyi deneyin. Diğer takvim sistemleri (İbrani, İslami) hakkında meraklıysanız, Aspose.Cells ve .NET'in `CultureInfo` bu deneyleri aynı kolaylıkla yapmanızı sağlar.

Sorularınız veya çözemediğiniz zor bir tarih formatı mı var? Aşağıya bir yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}