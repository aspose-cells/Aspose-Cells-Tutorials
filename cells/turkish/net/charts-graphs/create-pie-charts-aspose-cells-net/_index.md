---
"date": "2025-04-05"
"description": "Aspose.Cells for .NET kullanarak lider çizgileriyle dinamik pasta grafikleri oluşturmayı öğrenin. Veri görselleştirme becerilerinizi geliştirmek için bu kılavuzu izleyin."
"title": "Aspose.Cells .NET&#58;te Lider Çizgileriyle Pasta Grafikleri Oluşturma Kapsamlı Bir Kılavuz"
"url": "/tr/net/charts-graphs/create-pie-charts-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Aspose.Cells .NET Kullanarak Lider Çizgileriyle Pasta Grafikleri Oluşturma

## giriiş
Aspose.Cells for .NET ile daha bilgilendirici pasta grafikleri oluşturarak veri görselleştirmenizi geliştirin. Bu adım adım kılavuz, pasta grafik segmentlerine lider çizgileri eklemeyi ve karşılık gelen veri kategorilerini tek bakışta tanımlamayı nasıl kolaylaştıracağınızı gösterir. Bu öğreticiyi takip ederek görselleştirmeleriniz hem görsel olarak çekici hem de oldukça işlevsel olacaktır.

**Ne Öğreneceksiniz:**
- Ortamınızda .NET için Aspose.Cells'i kurma
- C# kullanarak özel lider çizgi pasta grafikleri oluşturma
- Tabloyu resim olarak veya Excel çalışma kitabına kaydetme

Etkili bir şekilde takip edebilmek için her şeyin hazır olduğundan emin olun.

## Ön koşullar
Başlamadan önce şu ön koşulları karşıladığınızdan emin olun:

- **Kütüphaneler ve Sürümler**: .NET için Aspose.Cells'i yükleyin. Projenizin en son sürümle kurulduğundan emin olun.
- **Çevre Kurulumu**: Bu kılavuz Aspose.Cells için uyumlu bir .NET ortamının olduğunu varsayar.
- **Bilgi Önkoşulları**:C# programlama ve Excel işlemlerine dair temel bilgiye sahip olmak faydalıdır.

## Aspose.Cells'i .NET için Kurma
Başlamak için Aspose.Cells'i projenize şu şekilde yükleyin:

**.NET Komut Satırı Arayüzü**
```bash
dotnet add package Aspose.Cells
```

**Paket Yöneticisi**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

Aşağıdaki seçeneklerden birini seçerek tam işlevsellik için bir lisans edinin:
- **Ücretsiz Deneme**: Ücretsiz denemenize başlayın [Aspose indirme sayfası](https://releases.aspose.com/cells/net/).
- **Geçici Lisans**: Geçici bir lisans alın [Burada](https://purchase.aspose.com/temporary-license/).
- **Satın almak**: Tüm özellikler için bir lisans satın alın [Burada](https://purchase.aspose.com/buy).

Projenizde Aspose.Cells'i, örneğini oluşturarak başlatın `Workbook` sınıf.

## Uygulama Kılavuzu

### Çalışma Kitabı ve Çalışma Sayfası Oluşturma
1. **Çalışma Kitabını Başlat**
   XLSX formatında yeni bir çalışma kitabı oluşturun:
   ```csharp
   Workbook workbook = new Workbook(FileFormatType.Xlsx);
   ```

2. **İlk Çalışma Sayfasına Erişim**
   Veri girişi için ilk çalışma sayfasını kullanın:
   ```csharp
   Worksheet worksheet = workbook.Worksheets[0];
   ```

3. **Pasta Grafiği için Veri Ekleme**
   Çalışma sayfanızı kategoriler ve değerlerle doldurun:
   ```csharp
   worksheet.Cells["A1"].PutValue("Retail");
   // Kalan kategori adlarını ekle...
   worksheet.Cells["B1"].PutValue(10.4);
   // İlgili değerleri ekleyin...
   ```

### Çalışma Sayfasına Pasta Grafiği Ekleme
1. **Pasta Grafiğini Oluşturun**
   Bir pasta grafiği oluşturun ve bunu çalışma sayfanızın grafik koleksiyonuna ekleyin:
   ```csharp
   int id = worksheet.Charts.Add(ChartType.Pie, 3, 3, 23, 13);
   ```

2. **Seri ve Kategori Verilerini Yapılandırın**
   Seri ve kategorilere ait verileri birbirine bağlayın:
   ```csharp
   Chart chart = worksheet.Charts[id];
   chart.NSeries.Add("B1:B16", true);
   chart.NSeries.CategoryData = "A1:A16";
   ```

3. **Veri Etiketlerini Özelleştir**
   Efsane gösterimini kapatın, veri etiketlerini kategori adlarını ve yüzdeleri gösterecek şekilde ayarlayın:
   ```csharp
   chart.ShowLegend = false;
   DataLabels dataLabels = chart.NSeries[0].DataLabels;
   dataLabels.ShowCategoryName = true;
   dataLabels.ShowPercentage = true;
   dataLabels.Position = LabelPositionType.OutsideEnd;
   ```

### Lider Hatların Uygulanması
1. **Lider Hatlarını Açın**
   Daha net görsel bağlantılar için lider çizgilerini etkinleştirin:
   ```csharp
   chart.NSeries[0].HasLeaderLines = true;
   ```

2. **Veri Etiketleri Pozisyonunu Ayarla**
   Etiket konumlarını ayarlayarak görünürlüğü sağlayın:
   ```csharp
   int DELTA = 100;
   foreach (var point in chart.NSeries[0].Points)
   {
       int X = point.DataLabels.X;
       if (X > 2000) 
           point.DataLabels.X += DELTA;
       else 
           point.DataLabels.X -= DELTA;
   }
   ```

### Tablo ve Çalışma Kitabını Kaydetme
1. **Resim olarak kaydet**
   Tabloyu bir resim dosyasına dönüştürün:
   ```csharp
   ImageOrPrintOptions options = new ImageOrPrintOptions { ImageType = Drawing.ImageType.Png, HorizontalResolution = 200, VerticalResolution = 200 };
   chart.ToImage("output_out.png", options);
   ```

2. **Çalışma Kitabını Kaydet**
   Tabloyu Excel'de görüntülemek için çalışma kitabını kaydedin:
   ```csharp
   workbook.Save("output_out.xlsx");
   ```

## Pratik Uygulamalar
- **Finansal Raporlar**: Bütçe dağılımlarını açıkça gösterin.
- **Pazarlama Analitiği**:Pazar payı verilerini sunumlarınızda veya raporlarınızda etkili bir şekilde görselleştirin.
- **Satış Analizi**Satışların farklı bölgeler/ürünler arasındaki dağılımını kolaylıkla görüntüleyin.

Entegrasyon olanakları arasında bu görselleştirmelerin web uygulamalarına aktarılması veya otomatik raporlama araçlarına gömülmesi yer almaktadır.

## Performans Hususları
Aspose.Cells kullanırken optimum performans için aşağıdakileri göz önünde bulundurun:
- Belleğe aynı anda yüklenen büyük veri kümelerini en aza indirin.
- Verimli döngüler kullanın ve döngüler içinde gereksiz hesaplamalardan kaçının.
- Bellek sızıntılarını önlemek için çalışma kitabı nesneleri gibi kaynakları düzenli olarak temizleyin.

## Çözüm
Aspose.Cells for .NET kullanarak lider çizgileriyle pasta grafikleri oluşturmayı öğrendiniz. Bu işlevsellik, veri görselleştirmelerinizin netliğini artırarak bunları daha erişilebilir ve etkili hale getirir. 

**Sonraki Adımlar:**
Grafik görünümlerinde daha fazla özelleştirmeyi keşfedin veya Aspose.Cells'te bulunan diğer grafik türlerini deneyin.

## SSS Bölümü
1. **Pasta grafiğinde lider çizgisi nedir?**
   Lider çizgiler, veri etiketlerini ilgili segmentlere bağlayarak okunabilirliği artırır.

2. **Aspose.Cells'i ücretsiz kullanabilir miyim?**
   Evet, ücretsiz denemeyle başlayabilirsiniz, ancak tüm özellikleri kullanabilmek için lisansa ihtiyacınız var.

3. **Grafikleri resim olarak dışarı aktarmak mümkün müdür?**
   Kesinlikle! Kullan `ImageOrPrintOptions` Grafiklerinizi PNG veya JPEG gibi resim formatlarında kaydetmek için.

4. **Veri etiketi konumlarını manuel olarak nasıl ayarlarım?**
   Seri noktaları döngüsü içindeki veri etiketlerinin X ve Y koordinatlarını değiştirin.

5. **Aspose.Cells diğer sistemlerle entegre olabilir mi?**
   Evet, otomatik raporlama çözümleri için veritabanları, web servisleri ve daha fazlasıyla birlikte kullanılabilir.

## Kaynaklar
- [Aspose.Cells Belgeleri](https://reference.aspose.com/cells/net/)
- [Aspose.Cells'i indirin](https://releases.aspose.com/cells/net/)
- [Lisans Satın Al](https://purchase.aspose.com/buy)
- [Ücretsiz Deneme](https://releases.aspose.com/cells/net/)
- [Geçici Lisans](https://purchase.aspose.com/temporary-license/)
- [Destek Forumu](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}