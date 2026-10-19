---
category: general
date: 2026-02-15
description: Yeni bir çalışma kitabı oluşturun ve sayısal hassasiyeti ayarlayarak
  Excel'i TXT'ye dışa aktarın. C#'ta anlamlı basamakları ayarlamayı ve sınırlamayı
  öğrenin.
draft: false
keywords:
- create new workbook
- export excel to txt
- set significant digits
- limit significant digits
- set numeric precision
language: tr
og_description: Yeni bir çalışma kitabı oluşturun ve Excel'i TXT'ye aktarın, sayısal
  hassasiyet için anlamlı basamakları ayarlayın. Adım adım C# rehberi.
og_title: Yeni Çalışma Kitabı Oluştur – Excel'i Hassasiyetle TXT'ye Dışa Aktar
tags:
- C#
- Aspose.Cells
- Excel automation
title: Yeni Çalışma Kitabı Oluştur ve Excel'i Hassasiyetle TXT'ye Dışa Aktar
url: /tr/net/excel-data-export-retrieval/create-new-workbook-and-export-excel-to-txt-with-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Yeni Çalışma Kitabı Oluştur – Excel’i TXT’ye Kesin Sayısal Formatlama ile Dışa Aktarma

Hiç **yeni çalışma kitabı** (workbook) nesnelerini C#’ta oluşturup anında düz metin dosyasına dökmeyi düşündünüz mü? Tek başınıza değilsiniz. Birçok veri‑akışı senaryosunda **Excel’i TXT’ye dışa aktarmamız** gerekir ve sayıları okunabilir tutmak, yani ondalık noktadan sonra görünen basamak sayısını sınırlamak önemlidir.  

Bu öğreticide tüm süreci adım adım inceleyeceğiz: temiz bir çalışma kitabı oluşturmak, dışa aktarımı **önemli basamakları ayarlayacak** (yani önemli basamakları sınırlayacak) şekilde yapılandırmak ve son olarak dosyayı diske yazmak. Sonunda **sayısal hassasiyet** gereksinimlerinizi karşılayan, çalıştırılmaya hazır bir kod parçacığı elde edeceksiniz—ekstra kütüphane, sihir yok.

> **Pro ipucu:** Zaten Aspose.Cells kullanıyorsanız, aşağıda gösterilen sınıflar bu kütüphanenin bir parçasıdır. Farklı bir platformda iseniz, kavramlar hâlâ geçerlidir; sadece API çağrılarını değiştirin.

---

## Gerekenler

- .NET 6+ (kod .NET Core ve .NET Framework’te de derlenir)  
- Aspose.Cells for .NET (ücretsiz deneme ya da lisanslı sürüm) – NuGet ile kurun: `dotnet add package Aspose.Cells`  
- İstediğiniz IDE (Visual Studio, Rider, VS Code)  

Hepsi bu. Ekstra yapılandırma dosyası, gizli adım yok.

---

## Adım 1: Yeni Bir Çalışma Kitabı Oluşturma

İlk iş **yeni çalışma kitabı** (new workbook) oluşturmaktır. `Workbook` sınıfını, sayfalar, hücreler ve veri bekleyen boş bir Excel dosyası olarak düşünün.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate a fresh workbook – this is the core of create new workbook logic
        Workbook workbook = new Workbook();

        // (Optional) Add some sample data so you can see the effect of numeric precision later
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);
```

> **Neden önemli:** Temiz bir çalışma kitabıyla başlayarak, daha sonra hassasiyet ayarlarını etkileyebilecek gizli biçimlendirmelerden kaçınmış olursunuz.

---

## Adım 2: Metin Kaydetme Seçeneklerini Yapılandırma – Önemli Basamakları Ayarlama

Şimdi Aspose.Cells’e `.txt` dosyasına yazarken kaç **önemli basamak** (significant digits) istediğimizi söylüyoruz. `TxtSaveOptions` sınıfı, tam da bunu yapan bir `SignificantDigits` özelliği sunar.

```csharp
        // Step 2: Prepare save options – limit numeric precision to 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            // This limits the output to 5 digits that matter, rounding the rest
            SignificantDigits = 5
        };
```

> **Açıklama:** `SignificantDigits = 5` demek, dışa aktarıcının herhangi bir sayının en önemli beş basamağını, ondalık noktanın konumundan bağımsız olarak tutacağı anlamına gelir. Her hücreyi manuel biçimlendirmeden **sayısal hassasiyeti** ayarlamanın pratik bir yoludur.

---

## Adım 3: Çalışma Kitabını Düz Metin Dosyası Olarak Kaydetme

Çalışma kitabı ve seçenekler hazır olduğunda, nihayet **Excel’i txt’ye dışa aktar**. `Save` metodu, dosya yolunu ve az önce yapılandırdığımız seçenek nesnesini alır.

```csharp
        // Step 3: Write the workbook out as a TXT file using our precision settings
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        System.Console.WriteLine($"Workbook exported to {outputPath} with 5 significant digits.");
    }
}
```

Programı çalıştırdığınızda aşağıdaki gibi bir dosya oluşur:

```
12346
0.00012346
3.1416
```

Her sayının, daha önce belirlediğimiz **önemli basamakları sınırlama** kuralına uyduğunu görebilirsiniz.

---

## Adım 4: Sonucu Doğrulama (Opsiyonel ama Tavsiye Edilir)

Oluşturulan `numbers.txt` dosyasını herhangi bir editörde açmak kolaydır, ancak CI pipeline’larında doğrulama adımını otomatikleştirmek isteyebilirsiniz.

```csharp
        // Quick verification – read back the file and print each line
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            System.Console.WriteLine($"Line: {line}");
        }
```

Konsolda yukarıdaki üç satır görüntüleniyorsa, **önemli basamakları ayarladınız** ve dışa aktarım istediğiniz gibi çalışıyor demektir.

---

## Yaygın Tuzaklar ve Çözümleri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| Sayılar çok fazla ondalık basamakla gösterilir | `SignificantDigits` varsayılan (0) bırakılmış | `SignificantDigits` değerini istediğiniz sayıya açıkça ayarlayın |
| Boş dosya oluşturulur | Kaydetmeden önce çalışma kitabına veri eklenmemiş | **Save** çağrısından **önce** hücreleri doldurun |
| Dosya yolu `UnauthorizedAccessException` verir | Korunan bir klasöre yazmaya çalışılıyor | Yazma izniniz olan bir klasör kullanın (ör. `C:\Temp` veya `%USERPROFILE%\Documents`) |
| Çok küçük sayılarda hassasiyet hatalı görünür | Önemli basamak sayısı, ondalıktan sonraki önde gelen sıfırları da sayar | “Önemli” basamakların önde gelen sıfırları saymadığını unutmayın; 0.000123456 ve 5 basamak `0.00012346` olur |

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda eksiksiz, bağımsız bir program yer alıyor. Yeni bir console projesine yapıştırın ve **Run** tuşuna basın.

```csharp
using Aspose.Cells;
using System;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a new workbook
        Workbook workbook = new Workbook();

        // Populate with sample numbers
        Worksheet sheet = workbook.Worksheets[0];
        sheet.Cells["A1"].PutValue(12345.678901);
        sheet.Cells["A2"].PutValue(0.000123456);
        sheet.Cells["A3"].PutValue(Math.PI);

        // 2️⃣ Set up export options – limit significant digits to 5
        TxtSaveOptions txtOptions = new TxtSaveOptions
        {
            SignificantDigits = 5
        };

        // 3️⃣ Export to TXT
        string outputPath = @"C:\Temp\numbers.txt";
        workbook.Save(outputPath, txtOptions);

        Console.WriteLine($"✅ Export completed: {outputPath}");
        Console.WriteLine("🔎 Verifying content:");
        foreach (var line in System.IO.File.ReadAllLines(outputPath))
        {
            Console.WriteLine($"   {line}");
        }
    }
}
```

**Beklenen konsol çıktısı**

```
✅ Export completed: C:\Temp\numbers.txt
🔎 Verifying content:
   12346
   0.00012346
   3.1416
```

Ve `numbers.txt` dosyası, yukarıda gösterilen üç satırı içerecek.

---

## Sonraki Adımlar: Temelin Ötesine Geçmek

- **Diğer formatları dışa aktar** – Aspose.Cells ayrıca CSV, HTML ve PDF destekler. Gerektiğinde `TxtSaveOptions` yerine `CsvSaveOptions` ya da `PdfSaveOptions` kullanın.  
- **Dinamik hassasiyet** – `SignificantDigits` değerini, kullanıcı girişi ya da yapılandırma dosyalarına göre çalışma zamanında hesaplayabilirsiniz.  
- **Birden çok çalışma sayfası** – `workbook.Worksheets` üzerinde döngü kurarak her birini ayrı bir `.txt` dosyasına dışa aktarın.  
- **Yerelleştirme** – Bölgesel ayarlarla uyumlu olması için ondalık ayırıcıyı (`.` vs `,`) `CultureInfo` üzerinden kontrol edin.  

Tüm bu uzantılar, ele aldığımız temel fikri kullanır: **yeni çalışma kitabı oluştur**, dışa aktarmayı yapılandır ve **sayısal hassasiyeti** raporlama gereksinimlerine göre ayarla.

---

## Özet

Temiz bir **yeni çalışma kitabı** (create new workbook) örneği oluşturduk, verileri doldurduk ve **Excel’i TXT’ye dışa aktar**ırken **önemli basamakları ayarlayarak** çıktının hassasiyetini sınırladık. Tam örnek kutudan çıkar çıkmaz çalışır ve her satırın *neden* olduğu açıklanmıştır, böylece kendi projelerinize kolayca uyarlayabilirsiniz.

Denemeler yapın—`SignificantDigits` değerini değiştirin, daha fazla sayfa ekleyin ya da çıktı formatını değiştirin. Bir sorunla karşılaşırsanız Aspose.Cells belgelerine bakın ya da aşağıya yorum bırakın. Kodlamanın tadını çıkarın!

---

![Create new workbook example](/images/create-new-workbook.png "Screenshot showing a C# IDE with the create new workbook code")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}