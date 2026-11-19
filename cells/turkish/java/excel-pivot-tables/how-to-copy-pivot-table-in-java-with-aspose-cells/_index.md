---
category: general
date: 2026-11-19
description: Java’da veri ve düzeni koruyarak pivot tabloyu nasıl kopyalayacağınızı
  öğrenin. Bu adım‑adım rehber, Excel pivot tablolarını da verimli bir şekilde nasıl
  kopyalayacağınızı gösterir.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table
- how to copy pivot
- how to preserve pivot
- preserve pivot table
- copy excel pivot
language: tr
lastmod: 2026-11-19
og_description: Aspose.Cells ile Java’da özet tablo kopyalama. Bu kılavuzu izleyerek
  özet tabloları korumayı ve Excel özet verilerini doğru bir şekilde kopyalamayı öğrenin.
og_image_alt: Illustration of the copy pivot table workflow in Java
og_title: Java'da Pivot Tablosunu Kopyalama – Tam Aspose.Cells Rehberi
schemas:
- author: Aspose
  dateModified: '2026-11-19'
  description: Learn how to copy pivot table in Java while preserving its data and
    layout. This step‑by‑step guide also shows how to copy excel pivot tables efficiently.
  headline: How to copy pivot table in Java with Aspose.Cells
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Pivot tables
title: Java'da Aspose.Cells ile Pivot Tablosunu Nasıl Kopyalarım
url: /tr/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java’da Aspose.Cells ile Pivot Tablosu Nasıl Kopyalanır

Bir çalışma kitabından diğerine **pivot tablo kopyalamak** istiyorsanız, bu rehber Java’da bunu tam olarak nasıl yapacağınızı gösterir. Raporlama motoru oluşturuyor ya da veri taşıma işlemi yapıyorsanız, pivot’un önbelleğini, alanlarını ve biçimlendirmesini korumanın güvenilir bir yolunu göreceksiniz.

Pivot tablo kopyalamak zor olabilir çünkü basit bir aralık kopyası genellikle temel veri kaynağını kaybeder. Bu öğreticide Aspose.Cells’i **pivot nasıl kopyalanır** sorusuna yanıt olarak kullanacağız ve hedef çalışma kitabı boş olduğunda **pivot nasıl korunur** konusunu da ele alacağız.

## Gereksinimler

Başlamadan önce şunların yüklü olduğundan emin olun:

* Java 17 veya daha yeni bir sürüm.
* Projenizin sınıf yoluna eklenmiş Aspose.Cells for Java (sürüm 23.9 veya sonrası).
* İki Excel dosyası: pivot tablosunu içeren bir kaynak çalışma kitabı ve boş bir hedef çalışma kitabı (veya birleştirmek istediğiniz bir çalışma kitabı).

Kod örneği için özel bir lisansa ihtiyacınız yoktur, ancak geçerli bir Aspose.Cells lisansı değerlendirme filigranlarını kaldırır.

## Adım 1: Pivot tablosunu içeren kaynak çalışma kitabını yükleyin

İlk adım, orijinal pivot’un bulunduğu çalışma kitabını açmaktır. Dosyayı yüklemek, çalışma sayfasına, hücrelere ve pivot önbelleğine erişim sağlar.

```java
// Step 1: Load the source workbook that contains the pivot table
Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Bu neden önemlidir*: Aspose.Cells, pivot’u besleyen gizli önbellek verileri dahil olmak üzere tüm çalışma kitabını okur. Dosyanın tamamı yüklenmezse, kopyalama işlemi pivot tanımını kaybeder.

## Adım 2: Hedef çalışma kitabını hazırlayın

Yeni bir çalışma kitabı oluşturun (veya mevcut bir tanesini açın) ve ilk çalışma sayfasını alın. Pivot burada yer alacak.

```java
// Step 2: Create a new destination workbook and get its first worksheet
Workbook destWb = new Workbook();                     // empty workbook
Worksheet destWs = destWb.getWorksheets().get(0);    // first sheet
```

*İpucu*: Zaten bir hedef çalışma kitabınız varsa, `new Workbook()` çağrısını `new Workbook("target.xlsx")` ile değiştirin. Bu, **excel pivot kopyala** işlemini önceden doldurulmuş bir çalışma kitabına yapmanızı sağlar.

## Adım 3: Pivot tablosunu çevreleyen hücre alanını tanımlayın

Pivot’u kapsayan tam aralığı belirtmeniz gerekir. Bu aralık, pivot tablosunu, alan listesini ve tutmak istediğiniz çevredeki verileri içerir.

```java
// Step 3: Define the cell area that covers the pivot table in the source sheet
CellArea area = CellArea.createCellArea("A1", "H30"); // adjust as needed
```

*Bu neden önemlidir*: `CellArea`, Aspose.Cells’e neyin kopyalanacağını söyler. Alan çok küçük olursa pivot kesilir; çok büyük olursa gereksiz veri kopyalanır. Koordinatları gerçek pivot boyutunuza göre ayarlayın.

## Adım 4: CopyOptions ile kopyalama işlemini gerçekleştirin

Kaynak çalışma sayfasının hücre koleksiyonunda `copy` metodunu kullanın. Yeni bir `CopyOptions()` nesnesi geçirerek tüm biçimlendirme, formüller ve pivot önbelleğinin aktarılması sağlanır.

```java
// Step 4: Copy the defined range (including the pivot table) to the destination worksheet
srcWb.getWorksheets().get(0).getCells().copy(area, destWs.getCells(), new CopyOptions());
```

### Neden `CopyOptions` pivotu korur

`CopyOptions`, Aspose.Cells’e aralığı düz bir değer kümesi yerine *bütün* bir nesne olarak ele almasını söyler. Bu, **pivot nasıl korunur** sorusunun anahtarıdır: temel pivot önbelleği çoğaltılır, böylece hedef çalışma kitabı pivotu manuel müdahale olmadan yeniden hesaplayabilir.

## Adım 5: Hedef çalışma kitabını kaydedin

Son olarak, hedef dosyayı diske yazın. Kaydedilen dosya, orijinal pivotun tam işlevsel bir kopyasını içerir.

```java
// Step 5: Save the destination workbook – the pivot table is preserved
destWb.save("YOUR_DIRECTORY/copied_with_pivot.xlsx");
```

*Beklenen sonuç*: `copied_with_pivot.xlsx` dosyasını Excel’de açtığınızda aynı pivot tablosu, dilimleyiciler, filtreler ve hesaplanmış alanlarla gösterilir. Pivotu yenileyebilir ve veri kaynağı aynı çalışma kitabındaki kopyalanan aralığa işaret eder.

---

![Diagram showing copy pivot table process](/images/copy-pivot-table-workflow.png){.align-center width=600 alt="Kaynak çalışma kitabından hedef çalışma kitabına pivot tablo kopyalama iş akışını gösteren diyagram"}

## Birden fazla çalışma sayfası arasında pivot tablolarını nasıl kopyalarsınız

Birden fazla sayfadan **excel pivot kopyala** tabloları kopyalamanız gerekiyorsa, Her kaynak çalışma sayfası için Adım 3‑4’ü tekrarlayın. Ayrıca `srcWb.getWorksheets()` üzerinden döngü kurarak her pivotu `destWb` içinde karşılık gelen sayfaya kopyalayabilirsiniz. İşte kısa bir döngü örneği:

```java
for (int i = 0; i < srcWb.getWorksheets().getCount(); i++) {
    Worksheet srcWs = srcWb.getWorksheets().get(i);
    Worksheet newDestWs = destWb.getWorksheets().add();
    // Assume each pivot occupies A1:H30 – adjust per sheet if needed
    CellArea area = CellArea.createCellArea("A1", "H30");
    srcWs.getCells().copy(area, newDestWs.getCells(), new CopyOptions());
}
destWb.save("YOUR_DIRECTORY/multi_sheet_copy.xlsx");
```

*Pro ipucu*: `srcWs.getPivotTables().getCount()` kullanarak bir sayfanın gerçekten pivot içerip içermediğini kontrol edin. Bu, alakasız verilerin kopyalanmasını önler.

## Yaygın tuzaklar ve nasıl önlenir

| Sorun | Neden olur | Çözüm |
|-------|------------|------|
| **Pivot önbelleğini kaybeder** | `Worksheet.copy()` `CopyOptions` olmadan sadece hücre değerlerini kopyalar. | Her zaman `srcWs.getCells().copy(..., new CopyOptions())` kullanın. |
| **Hedefte #REF! hataları gösterir** | Kopyalanan pivot hâlâ orijinal çalışma kitabının dış veri kaynağına referans verir. | Kopyalama sonrası `destWs.getPivotTables().get(0).refresh();` çağırarak önbelleği yeni aralığa bağlayın. |
| **Dilimleyiciler kaybolur** | Dilimleyiciler ana hücre alanının dışındadır. | `CellArea`yı dilimleyici aralıklarını kapsayacak şekilde genişletin veya tüm çalışma sayfasını (`srcWs.copy(destWs, new CopyOptions())`) kopyalayın. |
| **Büyük pivotlarda performans düşer** | Biçimlendirmeyle birlikte büyük aralıkların kopyalanması yavaş olabilir. | Biçimlendirme gerekmediğinde `CopyOptions.setOnlyData(true)` kullanın, ardından stilleri manuel olarak yeniden uygulayın. |

## Veri güncellenirken pivot tablo biçimlendirmesini nasıl korursunuz

Bazen kaynak veri değiştiğinde **pivot nasıl korunur** düzeni korumanız gerekir. Kopyalama sonrası pivotun stilini kilitleyebilirsiniz:

```java
PivotTable pt = destWs.getPivotTables().get(0);
pt.setPreserveFormatting(true);   // keeps colors, fonts, and layout
pt.refresh();                     // recalculates with new data
```

`PreserveFormatting` ayarı, kaynakta uyguladığınız özel stillerin kopyada da korunmasını sağlar.

## Kopyayı doğrulama

Kopyalamanın başarılı olduğunu hızlıca kontrol etmenin bir yolu, pivot tanımlarını karşılaştırmaktır:

```java
PivotTable srcPt = srcWb.getWorksheets().get(0).getPivotTables().get(0);
PivotTable destPt = destWs.getPivotTables().get(0);

System.out.println("Source fields: " + srcPt.getFields().size());
System.out.println("Destination fields: " + destPt.getFields().size());
// Both numbers should match
```

Sayım eşleşiyorsa ve hedef çalışma kitabı hatasız açılıyorsa, **pivot tablo kopyala** işlemini başarıyla tamamlamışsınız demektir.

## Sonuç

Artık Aspose.Cells for Java kullanarak bir Excel çalışma kitabından diğerine **pivot tablo kopyalama** yöntemini biliyorsunuz ve **pivot nasıl kopyalanır** sorusunun yanı sıra pivotun önbelleği, biçimlendirmesi ve dilimleyicilerinin korunmasını da sağladınız. Aynı desen, birden fazla sayfada **excel pivot kopyala** senaryoları için de geçerlidir; kodu, pivot biçimlendirmesini koruma veya büyük veri setleriyle çalışma gibi kenar durumlarına uyarlayabilirsiniz.

### Sonraki adımlar

* `setPreserveFormatting` ve `refresh` gibi **pivot tablo koruma** seçeneklerini keşfedin ve dinamik veri kaynaklarıyla çalışın.  
* Farklı sütun sıraları olan çalışma kitapları arasında pivot tablolarını kopyalamayı deneyin—`CellArea`yı buna göre ayarlayın.  
* Bu tekniği Aspose.Slides ile birleştirerek pivot anlık görüntülerini PowerPoint sunumlarına yerleştirin.

İyi kodlamalar, ve otomasyon hattınıza uygun varyasyonları denemekten çekinmeyin!

## Bir Sonraki Öğrenmeniz Gereken Konular

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve kendi projelerinizde ek API özelliklerini keşfetmenize yardımcı olur.

- [Java’da bir aralığı kopyala ve pivot tabloyu koru](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Java’da bir çalışma sayfası arasında pivot tabloyu kopyala](/cells/english/java/excel-pivot-tables/how-to-copy-a-pivot-table-between-worksheets-in-java/)
- [Java’da yeni bir çalışma kitabına pivot tablo kopyala](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-table-to-a-new-workbook-in-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}