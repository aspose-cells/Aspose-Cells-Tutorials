---
category: general
date: 2026-03-01
description: GridJs'te satır ekleme kolaylaştırıldı—100 satır eklemeyi, boş satırlar
  oluşturmayı ve toplam satır sayısını sadece birkaç C# satırıyla öğrenin.
draft: false
keywords:
- how to insert rows
- add multiple rows
- add 100 rows
- create empty rows
- check total rows
language: tr
og_description: GridJs'de satırları hızlı bir şekilde ekleme. Bu rehber, birden fazla
  satır eklemeyi, boş satırlar oluşturmayı ve temiz C# kodu ile toplam satır sayısını
  kontrol etmeyi gösterir.
og_title: GridJs'te Satır Ekleme – Hızlı Rehber
tags:
- C#
- GridJs
- data‑grid
title: GridJs'te Satır Ekleme – Birden Fazla Satırı Hızlıca Ekleyin
url: /tr/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GridJs'de Satır Ekleme – Birden Fazla Satırı Hızlıca Ekleyin

Hiç **satır eklemenin** bir GridJs veri‑ızgarasına, sonsuza kadar süren bir döngü yazmadan nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz. Birçok kurumsal uygulamada, toplu bir içe aktarma, bir şablon ya da gelecekteki veriler için bir yer tutucu oluşturmanız gerektiğinde bu noktaya gelirsiniz. İyi haber? GridJs, sizin için ağır işi yapan tek bir yöntem sunar.

Bu öğreticide, **100 satır ekleme**, **boş satırlar oluşturma** ve işlem sonrası **toplam satır sayısını kontrol etme** konularını gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda, GridJs kullanan herhangi bir C# projesine ekleyebileceğiniz sağlam bir desen elde edeceksiniz.

## Önkoşullar

İlerlemeye başlamadan önce şunların kurulu olduğundan emin olun:

- .NET 6.0 veya üzeri (API, .NET Framework 4.8'de de aynı şekilde çalışır, ancak yeni SDK daha güzel araçlar sağlar).
- `GridJs` NuGet paketine ya da `GridJs` sınıfını içeren derlenmiş DLL'e bir referans.
- C# sözdizimine temel aşinalık – egzotik bir şey yok, sadece standart `using` ifadeleri ve nesne‑yönelimli temeller.

Bu maddelerden herhangi biri bir sorun oluşturuyorsa, bir dakikalık ara verin ve eksikleri giderin. Takip eden adımlar, ızgara nesnesinin zaten örneklenmiş ve satır kabul etmeye hazır olduğunu varsayar.

![satır ekleme illüstrasyonu](gridjs-insert-rows.png)

## Adım 1: Izgara Örneğini Oluşturma

İlk olarak bir `GridJs` nesnesine ihtiyacınız var. Gerçek bir uygulamada bu muhtemelen bir servis katmanından gelir ya da bağımlılık enjeksiyonu ile sağlanır, ancak açıklık açısından yerel olarak oluşturacağız.

```csharp
using System;
using GridJsLibrary;   // <-- replace with the actual namespace of GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create or obtain the grid you want to modify
            GridJs gridJs = new GridJs();   // replace with your actual grid initialization
```

> **Neden önemli:** Izgarayı örneklemek, temiz bir başlangıç sağlar; böylece satır‑ekleme mantığı önceki çalışmalardan kalan durumla çakışmaz.

## Adım 2: Belirli Bir İndekste 100 Satır Ekleme

Şimdi **satır eklemenin** özüne geliyoruz. `InsertRows` metodu iki argüman alır: sıfır‑tabanlı başlangıç indeksi ve eklemek istediğiniz satır sayısı. 5. satırdan başlayarak 100 satır ekleyelim.

```csharp
            // Step 2: Insert 100 rows starting at row index 5 (zero‑based)
            // This pushes existing rows down and creates space for new data.
            gridJs.InsertRows(5, 100);
```

> **İpucu:** Satırları ızgaranın en sonuna eklemek isterseniz, başlangıç indeksi olarak `gridJs.RowCount` kullanabilirsiniz. Böylece etkili bir şekilde “ekleme” (append) yapmış olursunuz, ekleme (insert) değil.

### Arkada Ne Olur?

- **Bellek Tahsisi:** `InsertRows`, içsel olarak boş satır nesnelerinin bir bloğunu tahsis eder, böylece her birini manuel olarak örneklemeniz gerekmez.
- **İndeks Kaydırma:** İndeks 5 ve sonrasındaki tüm satırlar 100 konum aşağı kayar, orijinal verileri korunur.
- **Performans:** İşlem tek bir çağrıda gerçekleştiği için, `InsertRow` 100 kez döngüyle çağırmaktan genellikle daha hızlıdır.

## Adım 3: Eklemeyi Doğrulama (Toplam Satır Sayısını Kontrol Etme)

Satırları ekledikten sonra, **toplam satır sayısını** kontrol etmek iyi bir alışkanlıktır; böylece işlemin başarılı olduğunu teyit edersiniz. `RowCount` özelliği, ızgaradaki mevcut satır sayısını verir.

```csharp
            // Step 3: (Optional) Verify the insertion or continue processing
            int newRowCount = gridJs.RowCount; // example property to check total rows
            Console.WriteLine($"Grid now contains {newRowCount} rows.");
```

Örneğin, başlangıçta 20 satırınız varsa, konsolda `120` çıktısını görmelisiniz. Bu basit doğrulama adımı, ileride saatlerce sürebilecek hata ayıklamayı önleyebilir.

## Adım 4: Yeni Oluşturulan Boş Satırları Doldurma (İsteğe Bağlı)

Çoğu zaman, yeni oluşturulan satırları yer tutucu veri ya da varsayılan nesnelerle doldurmak istersiniz. `InsertRows` size bir blok boş satır sağladığından, bu aralıkta döngü kurup değer atayabilirsiniz.

```csharp
            // Optional: Fill the newly created rows with default values
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i); // assume GetRow returns a mutable row object
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Verify a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

> **Neden yapabilirsiniz:** Boş satır oluşturmak, kullanıcı girişi için bir şablon, toplu yükleme yer tutucu veya gelecekteki hesaplamalar için alan ayırma gibi durumlarda kullanışlıdır.

## Yaygın Varyasyonlar ve Kenar Durumları

### 100'den Az Satır Eklemek

Eğer **birden fazla satır** eklemeniz gerekiyorsa—örneğin 10 veya 25—aynı `InsertRows` çağrısını kullanın; sadece `100` yerine istediğiniz sayıyı yazın.

```csharp
gridJs.InsertRows(startIndex, 25); // adds 25 rows
```

### Izgaranın En Üstüne Ekleme

Satırları başa eklemek mi istiyorsunuz? Başlangıç indeksi olarak `0` kullanın:

```csharp
gridJs.InsertRows(0, 5); // adds 5 rows at the very beginning
```

### Kapsam Dışı İndekslerle Baş Etme

`RowCount` değerinden büyük bir indeks vermek `ArgumentOutOfRangeException` fırlatır. Bunun önüne geçmek için kontrol ekleyin:

```csharp
int safeIndex = Math.Min(requestedIndex, gridJs.RowCount);
gridJs.InsertRows(safeIndex, 100);
```

### Salt Okunur Izgaralarla Çalışma

Bazı GridJs yapılandırmaları salt‑okunur bir görünüm sunar. Bu durumda, `InsertRows` çağrısı öncesinde yazılabilir bir örneğe geçiş yapmalı veya geçici olarak salt‑okunur bayrağını devre dışı bırakmalısınız.

## Performans İpuçları

- **Toplu İşlemler:** Satırları bir döngü içinde tekrar tekrar ekliyorsanız, mümkün olduğunca tek bir `InsertRows` çağrısına toplamak daha iyidir. Bu, iç liste yeniden tahsislerini azaltır.
- **UI Yenilemelerinden Kaçınma:** UI‑bağlı ızgaralarda, satır eklemeden önce renderlamayı durdurun (`gridJs.BeginUpdate()`) ve sonrasında yeniden başlatın (`gridJs.EndUpdate()`); böylece titremeyi önlersiniz.
- **Bellek Profili:** Büyük eklemeler (ör. >10.000 satır) bellek kullanımını artırabilir. Tek bir devasa ekleme yerine sayfalama ya da akış (streaming) veri kullanmayı düşünün.

## Tam Çalışan Örnek Özeti

Her şeyi bir araya getirdiğimizde, kopyala‑yapıştır yapmaya hazır tam program aşağıdadır:

```csharp
using System;
using GridJsLibrary;   // replace with the actual namespace

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create the grid instance
            GridJs gridJs = new GridJs();

            // Insert 100 rows starting at index 5
            gridJs.InsertRows(5, 100);

            // Verify insertion
            int newRowCount = gridJs.RowCount;
            Console.WriteLine($"Grid now contains {newRowCount} rows.");

            // Optional: Fill new rows with placeholder data
            for (int i = 5; i < 5 + 100; i++)
            {
                var row = gridJs.GetRow(i);
                row["Name"] = $"Placeholder {i - 4}";
                row["CreatedOn"] = DateTime.UtcNow;
            }

            // Show a sample row
            var sample = gridJs.GetRow(5);
            Console.WriteLine($"First inserted row name: {sample["Name"]}");
        }
    }
}
```

Bu programı çalıştırdığınızda, konsolda satır sayısını ve ilk yer tutucu satırın adını göreceksiniz. İşte GridJs'de **satır eklemenin** tüm cevabı; doğrulama ve isteğe bağlı veri doldurma adımlarıyla birlikte.

## Sonuç

**GridJs'de satır ekleme** için net, uçtan uca bir çözüm sunduk; **100 satır ekleme**, **boş satır oluşturma** ve işlem sonrası **toplam satır sayısını kontrol etme** konularını kapsadık. Desen ölçeklenebilir—başlangıç indeksi ve sayıyı değiştirerek ihtiyacınız olan yerde **birden fazla satır ekleyebilirsiniz**.

Sonraki adımlar? Bu tekniği CSV dosyalarından toplu veri içe aktarmalarıyla birleştirin ya da kullanıcı girdisine dayalı koşullu satır oluşturmayı deneyin. Satır silme, sıralama veya koşullu biçimlendirme gibi konular, aynı API yüzeyinin doğal uzantılarıdır.

İyi kodlamalar, ve ızgaralarınız her zaman mükemmel boyutta olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}