---
category: general
date: 2026-03-30
description: C#'ta Aspose.Cells kullanarak çalışma sayfasını kopyalama – hücre aralığını
  kopyalama, sayfalar arasında sütunları kopyalama, çalışma sayfası pivot tablosunu
  kopyalama ve yeni çalışma sayfası ekleme kodunu kapsayan adım adım rehber.
draft: false
keywords:
- how to copy worksheet
- copy cell range
- copy columns between sheets
- copy worksheet pivot table
- add new worksheet code
language: tr
og_description: Aspose.Cells ile C#'ta çalışma sayfasını nasıl kopyalayacağınızı öğrenin.
  Bu rehber, hücre aralığını kopyalamayı, pivot tablolarını korumayı, sayfalar arasında
  sütunları kopyalamayı ve yeni çalışma sayfası ekleme kodunu gösterir.
og_title: C#'ta Çalışma Sayfasını Kopyalama – Tam Aspose.Cells Öğreticisi
tags:
- Aspose.Cells
- C#
- Excel Automation
title: C#'ta Aspose.Cells ile Çalışma Sayfası Nasıl Kopyalanır – Tam Rehber
url: /tr/net/excel-copy-worksheet/how-to-copy-worksheet-in-c-with-aspose-cells-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose.Cells Kullanarak Çalışma Sayfası Nasıl Kopyalanır – Tam Kılavuz

Hiç **çalışma sayfası nasıl kopyalanır** sorusunu, bir pivot tablo ya da formülü kaybetmeden C# içinde merak ettiniz mi? Yalnız değilsiniz—birçok geliştirici, tüm özellikleri koruyarak bir sayfayı çoğaltmak zorunda kaldığında takılıp kalıyor. Bu öğreticide, veriyi kopyalamanın yanı sıra **çalışma sayfası pivot tablosunu kopyalama**, **hücre aralığını kopyalama** ve ihtiyacınız olacak **yeni çalışma sayfası ekleme kodu** gibi konuları kapsayan pratik, uçtan uca bir çözümü adım adım göstereceğiz.

Kaynak çalışma kitabını yüklemekten hedef dosyayı kaydetmeye kadar her şeyi ele alacağız; böylece sayfalar arasında sütunları kopyalayabilir, nesneleri koruyabilir ve kodunuzu temiz tutabilirsiniz. Belirsiz referanslar yok, sadece projenize hemen ekleyebileceğiniz tam, çalıştırılabilir bir örnek.

## Bu Öğreticide Neler Ele Alınacak

- Aspose.Cells ile mevcut bir Excel dosyasını yükleme  
- **yeni çalışma sayfası ekleme kodu** kullanarak hedef sayfa oluşturma  
- Pivot tablo içeren bir **hücre aralığını kopyalama** tanımlama  
- Grafikler, formüller ve pivot tabloların korunması için **CopyOptions** ayarlama  
- **Sayfalar arasında sütunları kopyalama** işlemini satır‑satır hassasiyetle gerçekleştirme  
- Sonucu kaydetme ve çalışma sayfasının doğru kopyalandığını doğrulama  

Bu rehberin sonunda, “çalışma sayfası nasıl kopyalanır” sorusuna güvenle cevap verebilecek, raporları otomatikleştirirken ya da elektronik tablo‑tabanlı bir UI oluştururken bu yöntemi kullanabileceksiniz.

---

## Çalışma Sayfası Nasıl Kopyalanır – Genel Bakış

Kodlamaya geçmeden önce yüksek‑seviye akışı özetleyelim. Bunu bir tarif gibi düşünün:

1. **Kaynak çalışma kitabını yükle** (`Source.xlsx`).  
2. **Kopya için yeni bir çalışma sayfası ekle** (`yeni çalışma sayfası ekleme kodu`).  
3. **Kopyalanacak alanı tanımla** (`hücre aralığını kopyalama`).  
4. **Pivot tablonun korunması için kopya seçeneklerini yapılandır** (`çalışma sayfası pivot tablosunu kopyalama`).  
5. **Satır ve sütunları kopyala** (`sayfalar arasında sütunları kopyalama`).  
6. **Yeni çalışma kitabını kaydet** (`Destination.xlsx`).  

Hepsi bu—altı adım, sihir yok. Her adım aşağıda kod parçacıkları ve mantığıyla birlikte açıklanmıştır.

---

## Adım 1 – Kaynak Çalışma Kitabını Yükle

İlk iş: kopyalamak istediğiniz dosyaya işaret eden bir `Workbook` örneği oluşturmanız gerekir. Bu adım kritiktir çünkü Aspose.Cells doğrudan dosya sistemiyle çalışır, Office UI ile değil.

```csharp
using Aspose.Cells;

// Path to the original file
string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";

// Load the workbook – this is the starting point for how to copy worksheet
Workbook workbook = new Workbook(sourcePath);
```

*Neden önemli:* Dosyanın yüklenmesi, her sayfa, hücre ve nesnenin bellek içinde bir temsilini oluşturur. Bu olmadan kopyalanacak bir şey yoktur ve daha sonra `yeni çalışma sayfası ekleme kodu` kullanmak başarısız olur çünkü kaynak veri mevcut değildir.

---

## Adım 2 – Yeni Bir Çalışma Sayfası Ekle (yeni çalışma sayfası ekleme kodu)

Şimdi kopyalanan veriyi yapıştıracağımız bir yere ihtiyacımız var. İşte **yeni çalışma sayfası ekleme kodu** devreye giriyor. Sayfayı istediğiniz gibi adlandırabilirsiniz; burada `"Copy"` adını verdik.

```csharp
// Grab the first worksheet (the one we want to copy)
Worksheet sourceSheet = workbook.Worksheets[0];

// Add a fresh worksheet to receive the copy
Worksheet copySheet = workbook.Worksheets.Add("Copy");
```

*İpucu:* Birden fazla sayfa kopyalamayı planlıyorsanız, `Worksheets.Add` çağrısını bir döngü içinde yapın ve her sayfaya benzersiz bir ad verin. Böylece ad çakışmalarını önler ve çalışma kitabınızı düzenli tutarsınız.

---

## Adım 3 – Kopyalanacak Hücre Aralığını Tanımla

Bir **hücre aralığını kopyalama**, Aspose.Cells’e hangi satır ve sütunların çoğaltılacağını tam olarak söyler. Gerçek dünyada bu aralık çoğu zaman bir pivot tablo içerir, bu yüzden kesin olmak gerekir.

```csharp
// Define the area that contains the pivot table (A1:G20)
CellArea sourceRange = new CellArea
{
    StartRow = 0,      // Row 1 (zero‑based)
    StartColumn = 0,   // Column A
    EndRow = 19,       // Row 20
    EndColumn = 6      // Column G
};

// Destination range – we start at the same top‑left corner
CellArea destinationRange = new CellArea
{
    StartRow = 0,
    StartColumn = 0,
    EndRow = 19,
    EndColumn = 6
};
```

*Neden gerekli:* Aralığı açıkça belirterek tüm sayfayı (gereksiz yere) kopyalamaktan kaçınırsınız ve pivot tablonun kopyalanan alanda yer almasını garantilersiniz. Bu, **çalışma sayfası nasıl kopyalanır** sorusunun sadece bir kısmını ihtiyaç duyduğunuzda temel yaklaşımdır.

---

## Adım 4 – Kopya Seçeneklerini Ayarla (çalışma sayfası pivot tablosunu koruma)

Aspose.Cells, neyin yapıştırılacağını kontrol eden bir `CopyOptions` nesnesi sunar. Pivot tablo, grafik ve formülleri korumak için `PasteType.All` ayarlayıp `PasteSpecial` özelliğini etkinleştiririz.

```csharp
CopyOptions copyOptions = new CopyOptions
{
    PasteType = PasteType.All,   // Copy everything: values, formats, objects
    PasteSpecial = true          // Enable special paste to retain pivot tables
};
```

*Açıklama:* `PasteType.All` en kapsayıcı seçenektir, `PasteSpecial` ise motorun pivot tablolar gibi karmaşık nesneleri doğru şekilde işlemesini sağlar. Bu adımı atlamak yaygın bir tuzaktır; kopyalanan sayfa etkileşimli özelliklerini kaybeder.

---

## Adım 5 – Satır ve Sütunları Kopyala (sayfalar arasında sütunları kopyalama)

Şimdi asıl işi yapıyoruz: veriyi gerçekten taşıyoruz. **Sayfalar arasında sütunları kopyalama** için `CopyRows` ve `CopyColumns` kullanacağız. İkisini birlikte çalıştırmak, birleştirilmiş hücrelerin ve sütun genişliklerinin korunmasını sağlar.

```csharp
// Copy rows from the source to the destination sheet
sourceSheet.Cells.CopyRows(
    sourceRange.StartRow,
    sourceRange.EndRow,
    copySheet.Cells,
    destinationRange.StartRow,
    copyOptions);

// Copy columns from the source to the destination sheet
sourceSheet.Cells.CopyColumns(
    sourceRange.StartColumn,
    sourceRange.EndColumn,
    copySheet.Cells,
    destinationRange.StartColumn,
    copyOptions);
```

*Ne oluyor:* `CopyRows` veriyi satır satır taşırken, `CopyColumns` aynı işlemi sütun bazında yapar. İkisini de çalıştırmak, farklı sütun genişliklerine ya da gizli sütunlara sahip sayfalarda tam bir dikdörtgen bloğun kopyalanmasını garantiler.

---

## Adım 6 – Çalışma Kitabını Kaydet

Son olarak değişiklikleri diske yazın. Bu adım **çalışma sayfası nasıl kopyalanır** sürecini tamamlar.

```csharp
// Save the workbook with the newly copied sheet
workbook.Save(destinationPath);
```

*Doğrulama ipucu:* `Destination.xlsx` dosyasını açın ve `"Copy"` sayfasının orijinaliyle aynı göründüğünden, pivot tabloların çalıştığından ve sütun genişliklerinin eşleştiğinden emin olun. Bir şeyler eksikse, `CopyOptions` ayarlarını yeniden gözden geçirin.

---

## Kenar Durumları ve Yaygın Varyasyonlar

### Birden Çok Çalışma Sayfası Kopyalama

Birden fazla sayfayı çoğaltmanız gerekiyorsa, yukarıdaki mantığı bir `foreach` döngüsü içine alın:

```csharp
foreach (Worksheet ws in workbook.Worksheets)
{
    Worksheet newWs = workbook.Worksheets.Add(ws.Name + "_Copy");
    // Re‑use sourceRange/destinationRange or calculate per sheet
    // Then call CopyRows/CopyColumns as shown earlier
}
```

### Farklı Çalışma Kitapları Arasında Formülleri Koruma

Kaynak ve hedef çalışma kitaplarında farklı adlandırılmış aralıklar varsa, `copyOptions`’a `PasteType.Formulas` ekleyin:

```csharp
copyOptions.PasteType = PasteType.All | PasteType.Formulas;
```

### Büyük Aralıklar ve Performans

Yüzbinlerce satır gibi devasa veri setleri için, sütun genişlikleri kritik değilse sadece `CopyRows` kullanıp `CopyColumns`’ı atlayabilirsiniz. Bu, birkaç saniyelik tasarruf sağlar.

---

## Tam Çalışan Örnek

Aşağıda, tartıştığımız her şeyi içeren, doğrudan çalıştırılabilir bir program yer alıyor. Konsol uygulamasına yapıştırın, dosya yollarını ayarlayın ve **F5** tuşuna basın.

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // ---------- Step 1: Load the source workbook ----------
        string sourcePath = "YOUR_DIRECTORY/Source.xlsx";
        string destinationPath = "YOUR_DIRECTORY/Destination.xlsx";
        Workbook workbook = new Workbook(sourcePath);

        // ---------- Step 2: Add a new worksheet (add new worksheet code) ----------
        Worksheet sourceSheet = workbook.Worksheets[0];
        Worksheet copySheet = workbook.Worksheets.Add("Copy");

        // ---------- Step 3: Define the copy cell range ----------
        CellArea sourceRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };
        CellArea destinationRange = new CellArea
        {
            StartRow = 0,
            StartColumn = 0,
            EndRow = 19,
            EndColumn = 6
        };

        // ---------- Step 4: Set copy options (preserve copy worksheet pivot table) ----------
        CopyOptions copyOptions = new CopyOptions
        {
            PasteType = PasteType.All,
            PasteSpecial = true
        };

        // ---------- Step 5: Copy rows and columns (copy columns between sheets) ----------
        sourceSheet.Cells.CopyRows(
            sourceRange.StartRow,
            sourceRange.EndRow,
            copySheet.Cells,
            destinationRange.StartRow,
            copyOptions);

        sourceSheet.Cells.CopyColumns(
            sourceRange.StartColumn,
            sourceRange.EndColumn,
            copySheet.Cells,
            destinationRange.StartColumn,
            copyOptions);

        // ---------- Step 6: Save the workbook ----------
        workbook.Save(destinationPath);
    }
}
```

**Beklenen sonuç:** `Destination.xlsx` dosyasını açtığınızda, **Copy** adlı bir sayfanın `Source.xlsx`’in ilk sayfasını (pivot tablolar, biçimlendirme ve sütun genişlikleri dahil) yansıttığını görürsünüz. Orijinal dosya hiç değişmez.

---

## Sık Sorulan Sorular

**S: Bu kod .xlsx dosyaları Excel 2019 ile oluşturulmuş dosyalarla çalışır mı?**  
C: Kesinlikle. Aspose.Cells tüm modern Excel formatlarını destekler; aynı kod `.xlsx`, `.xlsm` ve hatta eski `.xls` dosyaları için de geçerlidir.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}