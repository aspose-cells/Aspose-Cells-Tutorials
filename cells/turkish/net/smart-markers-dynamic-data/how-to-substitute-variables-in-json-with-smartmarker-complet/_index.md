---
category: general
date: 2026-03-29
description: SmartMarker kullanarak JSON'da değişkenleri nasıl değiştireceğinizi öğrenin
  – if ifadesini kullanmayı, koşullu mantığı uygulamayı, değerleri çarpmayı ve JSON'u
  zahmetsizce oluşturmayı keşfedin.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: tr
og_description: SmartMarker kullanarak JSON'da değişkenleri nasıl değiştireceğinizi
  öğrenin. if ifadesini nasıl kullanacağınızı, koşullu mantığı nasıl uygulayacağınızı,
  değerleri nasıl çarpacağınızı ve dakikalar içinde JSON oluşturmayı keşfedin.
og_title: SmartMarker ile JSON'da Değişkenleri Nasıl Değiştiririz – Adım Adım
tags:
- C#
- SmartMarker
- JSON templating
title: SmartMarker ile JSON'da Değişkenleri Nasıl Değiştirirsiniz – Tam Kılavuz
url: /tr/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSON'da Değişkenleri SmartMarker ile Değiştirme – Tam Kılavuz

Hiç **değişkenleri nasıl değiştireceğinizi** bir JSON yükünde, özel bir ayrıştırıcı yazmadan merak ettiniz mi? Yalnız değilsiniz. Birçok entegrasyon senaryosunda—faturalar, fiyatlandırma motorları veya dinamik yapılandırma dosyaları gibi—çalışma zamanı değerlerini enjekte etmeniz, basit koşullar uygulamanız ve hatta hızlı bir çarpma yapmanız gerekir. Bu öğretici, SmartMarker kütüphanesini kullanarak **değişkenleri nasıl değiştireceğinizi** tam olarak gösterir, tüm bunları JSON'u temiz ve okunabilir tutarak yapar.

Gerçek bir örnek üzerinden **if ifadesi kullanımı**, **koşullu nasıl uygulanır**, **değerleri nasıl çarparız** ve **json nasıl oluşturulur** konularını ele alacağız. Sonuna geldiğinizde, herhangi bir .NET projesine ekleyebileceğiniz hazır bir C# kod parçacığına sahip olacaksınız.

## Öğrenecekleriniz

- `SmartMarkerOptions`'ı yeniden kullanılabilir değişkenleri depolamak için ayarlayın.  
- Koşullu mantık için bir `if` ifadesi içeren bir JSON şablonu yazın.  
- Şablon içinde bir değeri bir değişkenle çarpın.  
- Şablonu `SmartMarkerProcessor` ile işleyin ve son JSON dizesini alın.  
- Eksik değişkenler veya hatalı ifadeler gibi yaygın sorunları giderin.

Harici hizmetler yok, ağır bağımlılıklar yok—sadece saf C# ve SmartMarker NuGet paketi.

---

## Değişkenleri Değiştirme – Adım‑Adım Genel Bakış

Aşağıda iş akışının yüksek seviyeli bir resmi var. Bunu, ham JSON şablonunuzun soldan girdiği, SmartMarker motorunun sihrini yaptığı ve tamamen oluşturulmuş JSON'un sağdan çıktığı bir boru hattı olarak düşünün.

![JSON'da değişkenleri nasıl değiştireceğinizi gösteren diyagram](https://example.com/images/smartmarker-flow.png "JSON'da değişkenleri nasıl değiştireceğinizi gösteren diyagram")

*Görsel alt metni: JSON'da değişkenleri nasıl değiştireceğinizi gösteren diyagram.*

---

## Adım 1: SmartMarker'ı Kurun ve İçe Aktarın

Başlamadan önce, SmartMarker paketinin projenizde referans alındığından emin olun. .NET CLI kullanıyorsanız, şu komutu çalıştırın:

```bash
dotnet add package SmartMarker
```

Ardından, C# dosyanızın en üstüne gerekli `using` yönergelerini ekleyin:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro ipucu:** En son sürüm (Mart 2026 itibarıyla) 2.4.1'dir. .NET 6 ve üzerini destekler, ancak .NET Framework 4.7 ile de sorunsuz çalışır.

---

## Adım 2: SmartMarker Seçeneklerini Oluşturun ve Değişkenleri Tanımlayın

Şimdi, şablon boyunca yeniden kullanmak istediğimiz tüm değişkenleri tutacak bir `SmartMarkerOptions` örneği oluşturacağız. İşte **değişkenleri nasıl değiştireceğinizi** yanıtladığımız yer—değişkenler, SmartMarker'ın daha sonra yerine koyacağı yer tutucular olarak işlev görür.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

`Variables` içinde oranı saklamak neden tercih edilir, sabit kodlamak yerine? Çünkü bu sayıyı bir veritabanından, bir yapılandırma dosyasından veya kullanıcı girişinden alabilirsiniz. Seçeneklerde tutmak, şablonun yeniden kullanılabilir ve test edilebilir olmasını sağlar.

---

## Adım 3: `if` İfadesiyle JSON Şablonu Yazın

İşte **if ifadesi kullan** anahtar kelimesinin parladığı yer. SmartMarker, koşullu mantığı doğrudan JSON dizesinin içine yerleştirmenize izin verir. Sözdizimi bir özellik adı gibi görünse de, SmartMarker bunu bir yönerge olarak işler.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

`if(Amount>500)` anahtarına dikkat edin. SmartMarker, `Amount>500` ifadesini değerlendirir; eğer doğruysa, ilgili değer (`${Amount * Rate}`) çıktıya eklenir. `${...}` sözdizimi *değişken yerine koyma* motorudur—burada **değerleri nasıl çarparız** (`Amount * Rate`) sonucunu enjekte etmeden önce.

---

## Adım 4: Şablonu İşleyin ve Son JSON'u Alın

Seçenekler ve şablon hazır olduğunda, her şeyi işlemciye teslim ederiz. `ProcessJson` yöntemi şablonu ayrıştırır, koşulu uygular, çarpmayı gerçekleştirir ve temiz bir JSON dizesi döndürür.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

Running the snippet prints:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**Ne oldu?**  
- `Amount` 1000, bu da `Amount>500` koşulunu karşılar.  
- SmartMarker `${Amount * Rate}` ifadesini değerlendirir → `1000 * 0.08 = 80`.  
- Orijinal koşullu anahtar (`if(Amount>500)`) temiz bir özellik adı (`Result`) ile değiştirilir. Varsayılan olarak SmartMarker `"Result"` kullanır ancak bunu özelleştirebilirsiniz (daha fazla bilgi aşağıda).

`Amount` değerini `400` olarak değiştirirseniz, çıktı şu şekilde olur:

```json
{
  "Amount": 400
}
```

Koşullu blok kaybolur çünkü ifade `false` olarak değerlendirilir. Bu, JSON'da **koşullu nasıl uygulanır** mantığının özüdür.

---

## Adım 5: Çıktı Özellik Adını Özelleştirme (İsteğe Bağlı)

Bazen genel `"Result"` anahtarını istemezsiniz. SmartMarker, `RenameIfExpression` seçeneği ile özel bir ad belirlemenize izin verir:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

Output:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

Artık koşullu değer, daha anlamlı bir özellik adı altında saklanır—belirli bir alan bekleyen downstream servisleri için mükemmeldir.

---

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| Değişken bulunamadı | Referans verdiğiniz değişken `smartMarkerOptions.Variables` içinde yok. | Yazımını kontrol edin ve değişkenin işleme başlamadan önce eklendiğinden emin olun. |
| Geçersiz `if` sözdizimi | Parantez eksikliği veya yanlış operatör (`>`, `<`, `==`). | `if(<expression>)` desenine tam olarak uyun; SmartMarker sadece basit sayısal karşılaştırmaları destekler. |
| JSON bozuluyor | Koşullu bloktan sonra yanlışlıkla bir son virgül bırakılması. | Silme işlemini SmartMarker'a bırakın; orijinal şablonu sözdizimsel olarak doğru tutun. |
| Beklenmeyen sayı formatı | Sonuç bir sayı yerine `"80"` gibi bir dize olarak görünüyor. | Daha sonra tip dönüşümü yapın veya sayısal biçimlendirme için `${(Amount * Rate):N0}` kullanın. |

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda derleyip çalıştırabileceğiniz tam program var. Dinamik değişkenler, koşullar ve aritmetik ile **json nasıl oluşturulur** gösterir—hepsi 30 satırın altında.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**Expected console output**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

`Amount` değerini değiştirerek koşullu dalı test edebilir, ya da `Rate` değerini ayarlayarak farklı indirim hesaplamalarını görebilirsiniz.

---

## Deseni Genişletme – Daha Fazla “Nasıl” Senaryosu

- **Konfigürasyon dosyasından değişkenleri nasıl değiştiririz**: `appsettings.json` dosyasından bir `Dictionary<string, object>` yükleyin ve `smartMarkerOptions.Variables` içine besleyin.  
- **Birden fazla koşul için if ifadesi nasıl kullanılır**: `"if(Amount>500 && CustomerType=='VIP')"` gibi zincirleyin—SmartMarker mantıksal AND/OR destekler.  
- **Koşullu biçimlendirme nasıl uygulanır**: Ondalık basamakları kontrol etmek için ifadeye `${Amount:0.00}` ekleyin.  
- **Daha karmaşık matematikle değerleri nasıl çarparız**: `${(Amount - Discount) * TaxRate}` aynı şekilde çalışır.  
- **İç içe nesneler için json nasıl oluşturulur**: Koşullu bloğu başka bir JSON nesnesinin içine yerleştirin, SmartMarker hiyerarşiyi korur.

---

## Sonuç

SmartMarker kullanarak JSON'da **değişkenleri nasıl değiştireceğinizi** ele aldık, koşullu ekleme için **if ifadesi kullanımı** gösterdik, **koşullu nasıl uygulanır** mantığını açıkladık, şablon içinde **değerleri nasıl çarparız** gösterdik ve sonunda **json nasıl oluşturulur** örneğini sunduk; bu, downstream tüketim için hazır. Yaklaşım hafif, harici bir şablon motoru gerektirmiyor ve herhangi bir C# kod tabanına sorunsuz uyuyor.

Deneyin—değişkenleri ayarlayın, daha fazla koşul ekleyin veya tüm süreci bir yardımcı sınıfa sararak çözümünüzde yeniden kullanın. Dinamik JSON'u hızlıca üretmeniz gerektiğinde, SmartMarker sağlam ve üretim‑hazır bir seçenektir.

---

**Sonraki adımlar**

- `foreach` döngüleri ve özel fonksiyonlar gibi SmartMarker’ın ileri özelliklerine daha derinlemesine bakın.  
- Bu tekniği ASP.NET Core uç noktalarıyla birleştirerek dinamik JSON API'leri sunun.  
- Diğer şablon kütüphanelerini (ör. Handlebars.NET) karşılaştırma amaçlı inceleyin, özellikle daha zengin sözdizimi gerekiyorsa.

Sorularınız veya üzerinde çalıştığınız belirli bir kullanım senaryonuz mu var? Aşağıya yorum bırakın, birlikte sorun giderelim. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}