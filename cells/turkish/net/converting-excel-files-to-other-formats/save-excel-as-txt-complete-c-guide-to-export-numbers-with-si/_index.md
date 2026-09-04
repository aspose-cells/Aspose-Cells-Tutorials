---
category: general
date: 2026-02-21
description: Excel dosyasını txt olarak kaydedin ve anlamlı basamaklar üzerinde hassas
  kontrol sağlayın. C# ile Excel'i txt'ye dışa aktarın ve anlamlı basamakları kolayca
  ayarlayın.
draft: false
keywords:
- save excel as txt
- export excel to txt
- set significant digits
- save workbook as text
- export numbers to txt
language: tr
og_description: Excel'i hızlıca txt olarak kaydedin. Excel'i txt'ye nasıl dışa aktaracağınızı,
  anlamlı basamakları nasıl ayarlayacağınızı ve C# kullanarak metin çıktısını nasıl
  kontrol edeceğinizi öğrenin.
og_title: Excel'i txt olarak kaydet – C#'ta Anlamlı Basamaklarla Sayıları Dışa Aktar
tags:
- C#
- Aspose.Cells
- Excel automation
title: Excel'i txt olarak kaydet – Önemli Basamaklarıyla Sayıları Dışa Aktarmak için
  Tam C# Rehberi
url: /tr/net/converting-excel-files-to-other-formats/save-excel-as-txt-complete-c-guide-to-export-numbers-with-si/
---

translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel'i txt olarak kaydet – Anlamlı Rakamlarla Sayıları Dışa Aktarmak için Tam C# Rehberi

Excel'i **txt olarak kaydet**meniz gerektiğinde ama sayıların hassasiyetini kaybedeceğinden endişe ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, Excel'i txt'ye dışa aktarmaya çalıştığında ya çok fazla ondalık basamak ya da yuvarlanmış bir karmaşa ile karşılaşıyor.  

Bu öğreticide, **Excel'i txt olarak dışa aktarmanın** ve **anlamlı rakamları ayarlamanın** basit bir yolunu göstereceğiz, böylece çıktı tam istediğiniz gibi olur. Sonunda, bir çalışma kitabını metin olarak kaydeden, sayıları txt'ye dışa aktaran ve sayısal format üzerinde tam kontrol sağlayan çalıştırmaya hazır bir C# kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- Yeni bir çalışma kitabı oluşturma ve sayısal veri yazma.
- `TxtSaveOptions` kullanarak **anlamlı rakamları ayarlama** yöntemi.
- **Çalışma kitabını metin olarak kaydetme** ve sonucu doğrulama.
- Kenar‑durumları ele alma (büyük sayılar, negatif değerler, yerel ayar sorunları).
- Çıktıyı daha da özelleştirmek için hızlı ipuçları (ayırıcı değişiklikleri, kodlama).

### Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Framework 4.6+ üzerinde de çalışır).
- **Aspose.Cells** NuGet paketi (`Install-Package Aspose.Cells`).
- C# sözdizimi hakkında temel bir anlayış — derin Excel interop bilgisi gerekmez.

> **Pro ipucu:** Visual Studio kullanıyorsanız, *nullable reference types* (`<Nullable>enable</Nullable>`) özelliğini etkinleştirerek olası null hatalarını erken yakalayabilirsiniz.

---

## Adım 1: Çalışma Kitabını Başlatma ve Bir Sayı Yazma

İlk olarak bir çalışma kitabı nesnesine ihtiyacımız var. Bunu, bir Excel dosyasının bellek içi temsili olarak düşünün.  

```csharp
using Aspose.Cells;
using System;

// Create a new workbook (starts with one worksheet by default)
var workbook = new Workbook();
var worksheet = workbook.Worksheets[0];

// Write a numeric value into cell A1 (row 0, column 0)
worksheet.Cells[0, 0].PutValue(12345.6789);
```

**Neden önemli:**  
Çalışma kitabını programlı olarak oluşturmak, COM interop yükünden kaçınmanızı sağlar ve `PutValue` veri tipini otomatik olarak algılar, hücrenin bir sayı olarak işlenmesini, metin olarak değil, garantiler.

---

## Adım 2: Anlamlı Rakamları Kontrol Etmek İçin TxtSaveOptions Ayarlama

`TxtSaveOptions` sınıfı, sihrin gerçekleştiği yerdir. `SignificantDigits` özelliğini ayarlayarak, dosya yazıldığında kaç anlamlı rakamın korunacağını Aspose.Cells'e bildirirsiniz.

```csharp
// Configure text save options – keep only 4 significant digits
var txtSaveOptions = new TxtSaveOptions
{
    // 4 significant digits means 12345.6789 becomes 12350
    SignificantDigits = 4,

    // Optional: change delimiter if you need CSV‑style output
    // Delimiter = ',',

    // Optional: force UTF‑8 encoding for broader character support
    // Encoding = System.Text.Encoding.UTF8
};
```

**Bunu ayarlamanızın nedeni:**  
**Sayıları txt'ye dışa aktarırken**, genellikle kısa bir temsil gerekir (ör. yalnızca belirli bir hassasiyeti kabul eden raporlama sistemleri için). `SignificantDigits` özelliği, orijinal sayının uzunluğundan bağımsız olarak tutarlı bir yuvarlama sağlar.

---

## Adım 3: Çalışma Kitabını Metin Dosyası Olarak Kaydetme

Şimdi, az önce tanımladığımız seçenekleri kullanarak çalışma kitabını diske yazıyoruz.

```csharp
// Define the output path – adjust to your environment
string outputPath = @"C:\Temp\Numbers.txt";

// Save the workbook as a .txt file with the configured options
workbook.Save(outputPath, txtSaveOptions);

Console.WriteLine($"Workbook saved as txt at: {outputPath}");
```

**Gördükleriniz:**  
`Numbers.txt` dosyasını açtığınızda tek bir satır göreceksiniz:

```
12350
```

Orijinal `12345.6789` **dört anlamlı rakama** yuvarlanmış ve tam olarak istenildiği gibi elde edilmiştir.

---

## Adım 4: Çıktıyı Doğrulama (Opsiyonel ama Önerilir)

Otomatik testler iyi bir alışkanlıktır. Kaydetme işleminden hemen sonra çalıştırabileceğiniz hızlı bir kontrol burada:

```csharp
// Read back the file to confirm the content
string fileContent = System.IO.File.ReadAllText(outputPath).Trim();

if (fileContent == "12350")
{
    Console.WriteLine("✅ Export succeeded – significant digits applied correctly.");
}
else
{
    Console.WriteLine($"⚠️ Unexpected output: {fileContent}");
}
```

Bu bloğu çalıştırdığınızda her şey uyuyorsa yeşil bir onay işareti basar ve **excel'i txt olarak kaydet** işleminin beklendiği gibi davrandığından emin olursunuz.

---

## Yaygın Varyasyonlar ve Kenar Durumları

### Birden Çok Hücre veya Aralığı Dışa Aktarma

Bir bütün aralık için **excel'i txt olarak dışa aktarmanız** gerekiyorsa, kaydetmeden önce daha fazla hücre doldurun:

```csharp
worksheet.Cells[0, 1].PutValue(0.000123456);
worksheet.Cells[0, 2].PutValue(-98765.4321);
```

Aynı `TxtSaveOptions` her değere 4‑rakam kuralını uygular ve şu çıktıyı üretir:

```
12350
0.0001235
-98800
```

### Ayırıcıyı Değiştirme

Bazı alt sistemler sekme‑ayırılmış değerler bekler. Ayırıcıyı şu şekilde ayarlayın:

```csharp
txtSaveOptions.Delimiter = '\t'; // Tab character
```

Artık bir satırdaki her hücre sekme ile ayrılmış olur.

### Yerel Ayara Özel Ondalık Ayırıcıları

Kullanıcılar ondalık ayırıcı olarak virgül kullanıyorsa, kültürü şu şekilde ayarlayın:

```csharp
txtSaveOptions.CultureInfo = new System.Globalization.CultureInfo("fr-FR");
```

Çıktı, `12350` sayısını `12 350` (Fransızca’da binlik ayırıcı olarak boşluk) olarak gösterir.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.Cells;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create workbook and write numbers
        var workbook = new Workbook();
        var sheet = workbook.Worksheets[0];
        sheet.Cells[0, 0].PutValue(12345.6789);
        sheet.Cells[0, 1].PutValue(0.000123456);
        sheet.Cells[0, 2].PutValue(-98765.4321);

        // 2️⃣ Configure save options – 4 significant digits
        var txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 4,
            // Delimiter = '\t',               // Uncomment for TSV
            // Encoding = System.Text.Encoding.UTF8,
            // CultureInfo = new System.Globalization.CultureInfo("en-US")
        };

        // 3️⃣ Save to text file
        string path = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.Desktop), "Numbers.txt");
        workbook.Save(path, txtOptions);
        Console.WriteLine($"File saved to {path}");

        // 4️⃣ Verify result (optional)
        string result = File.ReadAllText(path).Trim();
        Console.WriteLine($"File content: {result}");
    }
}
```

**Beklenen `Numbers.txt` içeriği (varsayılan ayırıcı, 4 anlamlı rakam):**

```
12350	0.0001235	-98800
```

Sekme (`\t`) görünür çünkü örnekte ayırıcı varsayılan (sekme) olarak bırakılmıştır; CSV tercih ediyorsanız virgül olarak değiştirebilirsiniz.

---

## Sonuç

Artık **Excel'i txt olarak kaydet**irken anlamlı rakam sayısını kontrol etmenin tam yolunu biliyorsunuz. Çalışma kitabı oluşturma, `TxtSaveOptions.SignificantDigits` ayarlama ve kaydetme adımları, **excel'i txt'ye dışa aktarmak** için güvenilir bir yöntem sunar.  

Bundan sonra şunları yapabilirsiniz:

- **Sayıları txt'ye dışa aktar** daha büyük veri setleri için.
- Ayırıcıları, kodlamayı veya kültür ayarlarını, herhangi bir alt sistemle uyumlu olacak şekilde özelleştir.
- Dışa aktarmadan önce stil, formül gibi diğer Aspose.Cells özellikleriyle bu yaklaşımı birleştir.

Bir deneme yapın, `SignificantDigits` değerini 2 ya da 6'ya değiştirin ve çıktının nasıl değiştiğini görün. **Metin olarak çalışma kitabını kaydet** esnekliği, her veri‑değişim hattında kullanışlı bir araç haline getirir.

---

### Bir Sonraki Kez Keşfedebileceğiniz İlgili Konular

- **Excel'i CSV'ye dışa aktar** ve özel sütun sıralaması belirle.
- **txt dosyalarını tekrar bir çalışma kitabına oku** (`Workbook.Load` ile `LoadOptions`).
- **Toplu işleme** birden çok çalışma sayfasını bir txt dosyasında birleştirme.
- **Performans ayarı** büyük ölçekli dışa aktarmalar için (akış vs. bellek içi).

Herhangi bir sorunla karşılaşırsanız yorum bırakmaktan ya da kendi projelerinizde nasıl özelleştirdiğinizi paylaşmaktan çekinmeyin. Mutlu kodlamalar!  

---  

*Image: Oluşturulan `Numbers.txt` dosyasının yuvarlanmış değerleri gösteren bir ekran görüntüsü.*  
*Alt metin: “Numbers.txt dosyası, Excel'i txt olarak kaydetme işlemi sonrası 4 anlamlı rakamla 12350, 0.0001235 ve -98800 değerlerini gösteriyor.”*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}