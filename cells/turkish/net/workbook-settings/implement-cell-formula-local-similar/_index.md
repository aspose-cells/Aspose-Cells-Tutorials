---
title: Hücre Formülünü Yerel Olarak Uygulayın Aralık Formülüne Benzer Yerel
linktitle: Hücre Formülünü Yerel Olarak Uygulayın Aralık Formülüne Benzer Yerel
second_title: Aspose.Cells .NET Excel İşleme API'si
description: Aspose.Cells for .NET'teki aralık formülü yerel işlevselliğine benzer bir hücre formülünün nasıl uygulanacağını keşfedin. Yerleşik Excel işlev adlarını ve daha fazlasını özelleştirmeyi öğrenin.
weight: 13
url: /tr/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hücre Formülünü Yerel Olarak Uygulayın Aralık Formülüne Benzer Yerel

## giriiş
Aspose.Cells for .NET, Excel dosyalarını programlı olarak oluşturmanıza, düzenlemenize ve dönüştürmenize olanak tanıyan güçlü ve esnek bir elektronik tablo düzenleme API'sidir. Aspose.Cells tarafından sunulan birçok özellikten biri, kendi yerel işlev adlarınızı oluşturma yeteneği de dahil olmak üzere yerleşik Excel işlevlerinin davranışını özelleştirme yeteneğidir. Bu eğitimde, Aspose.Cells for .NET'teki aralık formülü yerel işlevselliğine benzer bir hücre formülü uygulamak için gereken adımlarda size yol göstereceğiz.
## Ön koşullar
Başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:
1. Sisteminizde Microsoft Visual Studio 2010 veya üzeri yüklü olmalıdır.
2.  Projenize yüklenen Aspose.Cells for .NET kütüphanesinin en son sürümü. Kütüphaneyi şuradan indirebilirsiniz:[Aspose.Cells for .NET indirme sayfası](https://releases.aspose.com/cells/net/).
## Paketleri İçe Aktar
Başlamak için, gerekli paketleri C# projenize aktarmanız gerekir. Aşağıdaki using ifadelerini kod dosyanızın en üstüne ekleyin:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## Adım 1: Özel Küreselleştirme Ayarları Sınıfı Oluşturun
 İlk adım, özel bir tane oluşturmaktır`GlobalizationSettings`Excel işlevlerinin varsayılan davranışını geçersiz kılmanıza izin verecek sınıf. Bu örnekte, adlarını değiştireceğiz`SUM` Ve`AVERAGE` işlevleri`UserFormulaLocal_SUM` Ve`UserFormulaLocal_AVERAGE`Sırasıyla.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //SUM fonksiyonunun adını ihtiyaçlarınıza göre değiştirin.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //AVERAGE fonksiyonunun adını ihtiyaçlarınıza göre değiştirin.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## Adım 2: Yeni Bir Çalışma Kitabı Oluşturun ve Özel Küreselleştirme Ayarlarını Atayın
 Sonra, yeni bir Çalışma Kitabı örneği oluşturun ve özel`GlobalizationSettings` Çalışma Kitabının uygulama sınıfı`Settings.GlobalizationSettings` mülk.
```csharp
//Çalışma kitabı oluştur
Workbook wb = new Workbook();
//GlobalizationSettings uygulama sınıfını atayın
wb.Settings.GlobalizationSettings = new GS();
```
## Adım 3: İlk Çalışma Sayfasına ve Bir Hücreye Erişim
Şimdi çalışma kitabındaki ilk çalışma sayfasına ve o çalışma sayfasındaki belirli bir hücreye erişelim.
```csharp
//İlk çalışma sayfasına erişin
Worksheet ws = wb.Worksheets[0];
//Bazı hücrelere erişim
Cell cell = ws.Cells["C4"];
```
## Adım 4: Formülleri Ata ve FormulaLocal'ı Yazdır
 Son olarak, şunu atayalım:`SUM` Ve`AVERAGE` formülleri hücreye yazın ve sonucu yazdırın`FormulaLocal` değerler.
```csharp
//SUM formülünü atayın ve FormulaLocal'ını yazdırın
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//AVERAGE formülünü atayın ve FormulaLocal'ını yazdırın
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## Çözüm
Bu eğitimde, Aspose.Cells for .NET'teki aralık formülü yerel işlevselliğine benzer bir hücre formülünün nasıl uygulanacağını öğrendiniz. Özel bir`GlobalizationSettings` sınıfı, Excel işlevlerinin varsayılan davranışını geçersiz kılabilir ve yerel işlev adlarını ihtiyaçlarınıza uyacak şekilde özelleştirebilirsiniz. Bu, özellikle yerelleştirilmiş veya uluslararasılaştırılmış Excel belgeleriyle çalışırken yararlı olabilir.
## SSS
###  Amacı nedir?`GlobalizationSettings` class in Aspose.Cells?
 The`GlobalizationSettings` Aspose.Cells'deki sınıf, yerel fonksiyon adlarını değiştirme yeteneği de dahil olmak üzere yerleşik Excel fonksiyonlarının davranışlarını özelleştirmenize olanak tanır.
###  Diğer fonksiyonların davranışlarını geçersiz kılabilir miyim?`SUM` and `AVERAGE`?
 Evet, herhangi bir yerleşik Excel işlevinin davranışını,`GetLocalFunctionName` özel yönteminizde`GlobalizationSettings` sınıf.
### Fonksiyon adlarını varsayılan değerlerine sıfırlamanın bir yolu var mı?
 Evet, özel adları kaldırarak işlev adlarını sıfırlayabilirsiniz.`GlobalizationSettings` sınıftan veya boş bir dize döndürerek`GetLocalFunctionName` yöntem.
### Bu özelliği Aspose.Cells'de özel fonksiyonlar oluşturmak için kullanabilir miyim?
 Hayır,`GlobalizationSettings`sınıf, özel işlevler oluşturmak için değil, yerleşik Excel işlevlerinin davranışını geçersiz kılmak için tasarlanmıştır. Özel işlevler oluşturmanız gerekiyorsa, şunu kullanabilirsiniz:`UserDefinedFunction` Aspose.Cells'deki sınıf.
### Bu özellik Aspose.Cells for .NET'in tüm sürümlerinde mevcut mu?
 Evet,`GlobalizationSettings` Sınıf ve fonksiyon adlarını özelleştirme yeteneği Aspose.Cells for .NET'in tüm sürümlerinde mevcuttur.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
