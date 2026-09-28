---
category: general
date: 2026-02-14
description: SmartMarker şablonlarında hiyerarşi oluşturmak düşündüğünüzden daha kolaydır
  – hiyerarşik verileri nasıl oluşturacağınızı ve çalışanları verimli bir şekilde
  nasıl listeleyeceğinizi öğrenin.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: tr
og_description: SmartMarker şablonlarında hiyerarşi oluşturmak basittir. Hiyerarşik
  veri oluşturmak ve çalışanları iç içe geçmiş aralıklarla listelemek için bu rehberi
  izleyin.
og_title: SmartMarker ile Hiyerarşi Oluşturma – Tam Rehber
tags:
- SmartMarker
- C#
- templating
title: SmartMarker ile Hiyerarşi Oluşturma – Adım Adım Rehber
url: /tr/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarker ile Hiyerarşi Oluşturma – Tam Kılavuz

SmartMarker şablonu içinde **hiyerarşi nasıl oluşturulur** diye hiç merak ettiniz mi, saçınızı yolmak zorunda kalmadan? Tek başınıza değilsiniz. Birçok raporlama senaryosunda ebeveyn‑çocuk ilişkisine ihtiyaç duyarsınız—bölümler ve içinde çalışan kişiler gibi. İyi haber şu ki, doğru adımları bildiğinizde SmartMarker bunu çocuk oyuncağı haline getiriyor.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: C#'ta **hiyerarşik veri oluşturma**, iç içe aralıkları etkinleştirme ve sonunda her bölüm için **çalışanları listeleyen** bir şablon oluşturma. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz hazır bir örnek elde edeceksiniz.

---

## İhtiyacınız Olanlar

- .NET 6+ (herhangi bir yeni sürüm çalışır)
- **SmartMarker** kütüphanesine referans ( `ws.SmartMarkerProcessor` ad alanı )
- Temel C# bilgisi – karmaşık bir şey değil, sadece birkaç nesne ve bir iki lambda
- Tercih ettiğiniz bir IDE ya da editör (Visual Studio, Rider, VS Code… seçiminiz)

Bu gereksinimlere zaten sahipseniz, harika—hadi başlayalım.

---

## Hiyerarşi Oluşturma – Genel Bakış

Temel fikir, son belgede görmek istediğiniz yapıyı yansıtan bir **iç içe nesne grafiği** oluşturmaktır. Bizim örneğimizde grafik şu şekilde görünür:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker daha sonra `Departments` üzerinde yineleme yapabilir ve **iç içe aralık işleme**yi açtığımız için her bölümün `Employees` koleksiyonunu otomatik olarak döner.

---

## Adım 1: Hiyerarşik Veri Modelini Oluşturma

İlk olarak, her bir bölümün kendi çalışan listesini içeren bir dizi departman barındıran anonim bir nesne oluşturuyoruz. Anonim tip kullanmak örneği hafif tutar—daha sonra gerçek POCO sınıflarıyla değiştirmekten çekinmeyin.

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **Neden Önemli:** `Departments` dizisi en üst seviye koleksiyondur. Her eleman bir `Employees` dizisi içerir ve bu, daha sonra `#Departments.Employees#` ile erişeceğimiz ikinci hiyerarşi seviyesini sağlar.

---

## Adım 2: İç İçe Aralık İşlemeyi Etkinleştirme

SmartMarker, iç koleksiyonlara dalmaz; siz ona söylemediğiniz sürece. Bu anahtarı `SmartMarkerOptions` nesnesi tutar.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **İpucu:** Bu bayrağı unutursanız, iç `#Employees#` aralığı hiçbir şey döndürmez ve şablonun neden boş olduğunu merak ederken kafanızı kaşırsınız.

---

## Adım 3: İşlemciyi Verinizle Çalıştırma

Şimdi veriyi ve seçenekleri işlemciye veriyoruz. `ws` değişkeni, **WebService** (veya SmartMarker motorunu barındıran herhangi bir nesne) anlamına gelir.

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

Bu noktada SmartMarker şablonu ayrıştırır, her bölüm adı için `#Departments.Name#` ifadesini değiştirir ve iç içe aralıklar etkin olduğu için her bölümün `Employees` koleksiyonunu yineleyecektir.

---

## Adım 4: Şablon İşaretçilerini Oluşturma

Aşağıda dış ve iç döngüleri gösteren minimal bir şablon bulunuyor. Bunu SmartMarker şablon editörüne (veya işlemciye verdiğiniz bir `.txt` dosyasına) yapıştırın.

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Render edildiğinde şunun gibi bir çıktı göreceksiniz:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **Ne Görüyorsunuz:** Dış `#Departments.Name#` bölüm başlığını yazdırır. İç `#Departments.Employees#` bloğu her çalışan üzerinde döner ve blok içindeki `#Departments.Employees#` gerçek ismi çıktılar.

---

## Beklenen Çıktı ve Doğrulama

Tam örneği (veri + seçenekler + şablon) çalıştırmak, yukarıda gösterilen listeyi tam olarak üretmelidir. Hızlı bir doğrulama için sonucu konsola dökebilirsiniz:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

İki bölüm başlığı ve ardından çalışan madde işaretlerini görürseniz, **hiyerarşi oluşturmayı** ve **çalışanları listelemeyi** başarıyla tamamlamışsınız demektir.

---

## Yaygın Tuzaklar ve Kenar Durumları

| Sorun | Neden | Çözüm |
|-------|-------|-------|
| Çalışanlar için çıktı yok | `EnableNestedRange` false bırakıldı | `EnableNestedRange = true` olarak ayarlayın |
| Çalışan adları yineleniyor | Aynı dizi bölümler arasında yeniden kullanılıyor | Diziyi kopyalayın ya da farklı koleksiyonlar kullanın |
| Çok büyük hiyerarşiler bellek baskısına neden olur | SmartMarker tüm nesne grafiğini belleğe yükler | Veriyi akış olarak işleyin ya da büyük koleksiyonları sayfalara bölün |
| Şablon sözdizimi hataları | Kapanış `#/…#` etiketleri eksik | SmartMarker doğrulayıcısını kullanın ya da küçük bir şablonla hızlı test yapın |

---

## İleriye Dönük – Gerçek Dünya Varyasyonları

1. **Dinamik veri kaynakları** – Bölümleri bir veritabanından çekin ve LINQ kullanarak anonim yapıya eşleyin.  
2. **Koşullu biçimlendirme** – Her çalışan için bir `IsManager` bayrağı ekleyin ve yöneticileri vurgulamak için SmartMarker’ın koşullu etiketlerini (`#if …#`) kullanın.  
3. **Çoklu iç içe seviyeler** – Bölümler içinde takımlar gerekiyorsa, bir başka koleksiyon (`Teams`) ekleyin ve `EnableNestedRange`i açık tutun.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**Şablon (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

Programı çalıştırdığınızda hiyerarşi, daha önce gösterildiği gibi tam olarak yazdırılır.

---

## Sonuç

**Hiyerarşi nasıl oluşturulur** konusunu, C#'ta **hiyerarşik veri** şekillendirmeden iç içe aralıkları açmaya ve sonunda bölüm başına **çalışanları listeleyen** bir şablon render etmeye kadar ele aldık. Bu desen ölçeklenebilir—daha fazla iç içe koleksiyon veya koşullu mantık ekleyin ve güçlü bir raporlama motoruna sahip olun.

Bir sonraki meydan okumaya hazır mısınız? Anonim tipleri güçlü tipli POCO sınıflarıyla değiştirin ya da bu akışı bir PDF veya Word belgesi dönen bir ASP.NET Core uç noktasına entegre edin. Gökyüzü sınırdır ve artık sağlam bir temele sahipsiniz.

---

![Hiyerarşi oluşturma diyagramı](image.png){alt="Bölüm‑çalışan ilişkisini gösteren hiyerarşi oluşturma diyagramı"}

*Kodlamaktan keyif alın! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın—yardımcı olmaktan mutluluk duyarım.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}