---
category: general
date: 2026-04-07
description: Bir elektronik tablo hücresine özel sayı biçimi uygulayın ve C# ile hücre
  değerini dışa aktarırken elektronik tabloda sayıyı nasıl biçimlendireceğinizi öğrenin.
  Hızlı, eksiksiz rehber.
draft: false
keywords:
- apply custom number format
- format number in spreadsheet
- how to format numeric cell
- how to export cell value
language: tr
og_description: Bir elektronik tablo hücresine özel sayı biçimi uygulayın ve bunu
  biçimlendirilmiş bir dize olarak dışa aktarın. Elektronik tabloda sayıyı nasıl biçimlendireceğinizi
  ve hücre değerini nasıl dışa aktaracağınızı öğrenin.
og_title: Özel Sayı Formatı Uygulama – Tam C# Dışa Aktarma Öğreticisi
tags:
- C#
- Spreadsheet
- Number Formatting
title: C# Elektronik Tablo Dışa Aktarımında Özel Sayı Formatı Uygulama – Adım Adım
  Kılavuz
url: /tr/net/excel-custom-number-date-formatting/apply-custom-number-format-in-c-spreadsheet-export-step-by-s/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# Spreadsheet Export’inde Özel Sayı Biçimi Uygulama – Tam Kılavuz

Hiç bir hücreye **özel sayı biçimi** uygulayıp ardından bu biçimlendirilmiş dizeyi bir elektronik tablodan çıkarmak zorunda kaldınız mı? Yalnız değilsiniz. Birçok geliştirici, bekledikleri güzel, yerel ayar‑duyarlı dize yerine ham değerin çıktığını gördüklerinde takılıp kalıyor. Bu rehberde, elektronik tablo hücrelerinde sayıyı nasıl biçimlendireceğinizi ve popüler bir C# elektronik tablo kütüphanesi kullanarak hücre değerini biçimlendirilmiş bir dize olarak nasıl dışa aktaracağınızı adım adım göstereceğiz.

Bu adımları tamamladığınızda, **özel sayı biçimi**ni herhangi bir sayısal hücreye uygulayabilecek, sonucu `ExportTable` ile dışa aktarabilecek ve bir UI ya da raporda göstermek istediğiniz tam çıktıyı elde edebileceksiniz. Harici belgelere ihtiyaç yok—her şey burada.

## Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır)
- `Workbook`, `Worksheet` ve `ExportTableOptions` sağlayan bir elektronik tablo kütüphanesine referans (ör. **Aspose.Cells** veya **GemBox.Spreadsheet**; gösterilen API Aspose.Cells ile eşleşir)
- Temel C# bilgisi—eğer bir `Console.WriteLine` yazabiliyorsanız, hazırsınız

> **Pro tip:** Farklı bir kütüphane kullanıyorsanız, özellik adları genellikle benzer olur (`NumberFormat`, `ExportAsString`). Sadece buna göre eşleştirin.

## Eğitimde Neler Kapsanıyor

1. Bir çalışma kitabı oluşturma ve ilk çalışma sayfasını seçme.  
2. Bir hücreye sayısal bir değer ekleme.  
3. `ExportTableOptions`ı **özel sayı biçimi** uygulayacak ve bir dize döndürecek şekilde yapılandırma.  
4. Hücreyi dışa aktarma ve biçimlendirilmiş sonucu yazdırma.  
5. Kenar‑durum yönetimi – hücre bir formül ya da null değer içerirse ne olur?

Haydi başlayalım.

![apply custom number format example](https://example.com/image.png "apply custom number format")

## Adım 1 – Bir çalışma kitabı oluşturun ve ilk çalışma sayfasını alın

İlk olarak bir çalışma kitabı nesnesine ihtiyacınız var. Bunu, Office uygulamasında açtığınız Excel dosyası gibi düşünün. Elinize geçince, çoğu öğreticinin örneği kısa tutmak için ilk sayfayı kullandığını göreceksiniz, bu yüzden ilk sayfayı alın.

```csharp
// Step 1: Initialize the workbook and fetch the first worksheet
Workbook workbook = new Workbook();                 // creates an in‑memory workbook
Worksheet worksheet = workbook.Worksheets[0];      // first sheet (index 0)
```

**Neden önemli:** Yeni bir çalışma kitabı temiz bir sayfa sağlar, böylece daha sonra uygulayacağımız özel sayı biçimini etkileyebilecek gizli biçimlendirmeler olmaz.

## Adım 2 – B2 hücresine sayısal bir değer koyun (dışa aktaracağımız hücre)

Şimdi biçimlendirecek bir şeye ihtiyacımız var. **B2** hücresi, referans alması kolay ve varsayılan A1 köşesinden yeterince uzakta olduğu için kazara üzerine yazılma riskini azaltan uygun bir konumdur.

```csharp
// Step 2: Insert a raw numeric value
worksheet.Cells["B2"].Value = 1234.56;   // raw double, no formatting yet
```

**Değer bir formül olsaydı ne olur?**  
Daha sonra ham değeri bir formülle (ör. `=SUM(A1:A10)`) değiştirirseniz, dışa aktarma rutini bir sonraki adımda uyguladığımız sayı biçimini hâlâ dikkate alır; çünkü biçimlendirme hücreye, değer tipine değil, eklenir.

## Adım 3 – Değeri biçimlendirilmiş bir dize olarak almak için dışa aktarma seçeneklerini yapılandırın

İşte eğitimin kalbi: Kütüphaneye dışa aktarırken **özel sayı biçimi**ni uygulamasını söylüyoruz. `NumberFormat` dizesi, Excel’in “Custom” kategorisinde kullandığınız aynı desenle çalışır.

```csharp
// Step 3: Set up options for exporting as a formatted string
ExportTableOptions exportOptions = new ExportTableOptions
{
    ExportAsString = true,                         // forces string output
    NumberFormat = "#,##0.00;(#,##0.00)"           // custom format: 1,234.56 or (1,234.56) for negatives
};
```

- `ExportAsString = true` yöntemin bir `string` döndürmesini, ham bir double yerine sağlar.  
- `NumberFormat = "#,##0.00;(#,##0.00)"` Excel desenini yansıtır: binlik ayırıcı olarak virgül, iki ondalık basamak ve negatif sayılar için parantez.

> **Neden özel bir format kullanmalı?** Kültürler arasında tutarlılık sağlar (ör. ABD vs. Avrupa sayı ayırıcıları) ve muhasebe parantezleri gibi iş‑özel stil eklemenize olanak tanır.

## Adım 4 – Yapılandırılmış seçenekleri kullanarak hücreyi dışa aktarın

Şimdi değeri çalışma sayfasından gerçekten çekiyoruz ve kütüphanenin tanımladığımız biçimi uygulama işini üstlenmesine izin veriyoruz.

```csharp
// Step 4: Export the formatted value from B2
string formattedResult = worksheet.Cells.ExportTable(
    worksheet.Cells["B2"],   // the source cell
    exportOptions);         // our custom options
```

**Kenar durumu – boş hücre:** `B2` boş olsaydı, `formattedResult` `null` olurdu. Yazdırmadan önce basit bir null‑kontrolü ile bunu önleyebilirsiniz.

## Adım 5 – Biçimlendirilmiş dizeyi göster

Son olarak sonucu konsola yazdırıyoruz. Gerçek bir uygulamada bu dizeyi bir PDF, e‑posta ya da UI etiketi içine yerleştirebilirsiniz.

```csharp
// Step 5: Show the result
Console.WriteLine(formattedResult);   // Expected output: 1,234.56
```

**Beklenen çıktı**

```
1,234.56
```

Ham değeri `-9876.54` olarak değiştirirseniz, aynı format size `(9,876.54)` verir—birçok muhasebe raporunun tam olarak ihtiyaç duyduğu biçim.

## Tam, çalıştırılabilir örnek

Aşağıda yeni bir konsol projesine kopyalayıp‑yapıştırabileceğiniz tam program yer alıyor. Uygun NuGet paketini eklediğiniz sürece olduğu gibi derlenir ve çalışır.

```csharp
using System;
using Aspose.Cells;   // Replace with your library’s namespace if different

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Insert numeric value into B2
        worksheet.Cells["B2"].Value = 1234.56;

        // 3️⃣ Set export options – apply custom number format
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true,
            NumberFormat = "#,##0.00;(#,##0.00)"   // custom format
        };

        // 4️⃣ Export the cell as a formatted string
        string formattedResult = worksheet.Cells.ExportTable(
            worksheet.Cells["B2"], exportOptions);

        // 5️⃣ Output the result
        Console.WriteLine(formattedResult);   // → 1,234.56
    }
}
```

### Hızlı doğrulama kontrolü

- **Derleniyor mu?** Evet—sadece `Aspose.Cells` (veya eşdeğeri) DLL'inin referans edildiğinden emin olun.  
- **Diğer kültürlerde çalışır mı?** Format dizesi kültür‑bağımsızdır; kütüphane verdiğiniz deseni uygular. Yerel ayırıcılar gerekirse, dışa aktarmadan önce `CultureInfo` işleme ekleyebilirsiniz.

## Yaygın sorular ve varyasyonlar

### Farklı bir desen kullanarak **format number in spreadsheet** nasıl yapılır?

`NumberFormat` dizesini değiştirin. Örneğin, bir ondalık basamaklı yüzde göstermek için:

```csharp
NumberFormat = "0.0%";
```

### **how to export cell value**'ı HTML olarak düz metin yerine nasıl alabilirim?

Çoğu kütüphane bir dışa aktarma türü kabul eden bir aşırı yükleme sunar. `ExportAsString = true` ayarlayıp `ExportHtml = true` (veya benzeri) ekleyebilirsiniz. İlke aynı kalır: formatı tanımlayın, ardından çıktı temsilini seçin.

### Formatı sadece bir hücreye değil, tüm bir aralığa uygulayabilir miyim?

Kesinlikle. `NumberFormat`ı bir `Style` nesnesine atayabilir ve ardından bu stili bir `Range`e uygulayabilirsiniz. Dışa aktarma çağrısı değişmez; stil otomatik olarak alınır.

```csharp
Style style = workbook.CreateStyle();
style.Custom = "#,##0.00;(#,##0.00)";
Range range = worksheet.Cells.CreateRange("A1:C10");
range.ApplyStyle(style, new StyleFlag { NumberFormat = true });
```

### Hücre bir formül içerdiğinde ne olur?

Dışa aktarma rutini önce formülü değerlendirir, ardından ortaya çıkan sayısal değeri biçimlendirir. Ek bir kod gerekmez—otomatik hesaplamayı devre dışı bıraktıysanız `Calculate` metodunun çağrıldığından emin olun.

```csharp
worksheet.Cells["B2"].Formula = "=SUM(A1:A5)";
worksheet.Calculate();   // forces evaluation
```

## Sonuç

Artık bir elektronik tablo hücresine **özel sayı biçimi** uygulamayı, **format number in spreadsheet** bağlamlarında biçimlendirmeyi ve **how to export cell value**'ı doğrudan gösterilebilir bir dize olarak dışa aktarmayı biliyorsunuz. Yukarıdaki özlü kod örneği, çalışma kitabı oluşturulmasından son çıktıya kadar her adımı kapsar; böylece doğrudan üretim projenize ekleyebilirsiniz.

Bir sonraki meydan okumaya hazır mısınız? Bu tekniği tarih, para birimi simgeleri veya koşullu biçimlendirme için **how to format numeric cell** ile birleştirmeyi deneyin. Ya da her hücrenin özel biçimini koruyarak birden fazla hücreyi CSV olarak dışa aktarmayı keşfedin. Ufkunuz sınırsız ve bu temellerle sağlam bir altyapıya sahipsiniz.

Keyifli kodlamalar, ve denemeyi unutmayın—bazen en iyi cevaplar, format dizesini birazcık ayarladığınızda ortaya çıkar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}