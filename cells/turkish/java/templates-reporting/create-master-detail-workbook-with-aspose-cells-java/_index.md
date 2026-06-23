---
category: general
date: 2026-06-08
description: Aspose.Cells Smart Marker kullanarak Java’da master‑detail çalışma kitabı
  oluşturun. Master verileri bir detay sayfasına bağlamayı ve Excel’i dışa aktarmayı
  adım adım öğrenin.
draft: false
keywords:
- create master detail workbook
- Aspose.Cells Smart Marker
- Java Excel export
- master‑detail relationship
- Smart Marker data source
language: tr
og_description: Aspose.Cells Smart Marker kullanarak Java'da ana‑detay çalışma kitabı
  oluşturun. Ana verileri bir detay sayfasına bağlamak ve Excel dosyaları üretmek
  için bu kapsamlı rehberi izleyin.
og_title: Aspose.Cells (Java) ile ana‑detay çalışma kitabı oluştur.
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create master detail workbook in Java using Aspose.Cells Smart Marker.
    Learn step‑by‑step how to bind master data to a detail sheet and export Excel.
  headline: Create master detail workbook with Aspose.Cells (Java)
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
title: Aspose.Cells (Java) ile ana detay çalışma kitabı oluştur
url: /tr/java/templates-reporting/create-master-detail-workbook-with-aspose-cells-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells (Java) ile master‑detail çalışma kitabı oluşturma

Java’da **master‑detail çalışma kitabı oluşturma** ihtiyacınız varsa doğru yerdesiniz. Satış panosu, fatura oluşturucu veya master‑detail görünümü gerektiren herhangi bir raporlama aracı oluşturuyorsanız, bu kılavuz size tüm süreci adım adım gösterecek—süsleme yok, sadece çalıştırılabilir kod.

Bu öğreticide **Aspose.Cells Smart Marker** özelliğini kullanacağız; bu özellik, bir Excel şablonuna doğrudan veri yer tutucuları eklemenizi sağlar. Sonunda, master‑detail ilişkiyi nasıl kuracağınızı, POJO listesini veri kaynağı olarak nasıl bağlayacağınızı ve temiz bir .xlsx dosyasını nasıl dışa aktaracağınızı anlayacaksınız.

## Öğrenecekleriniz

- Bir çalışma kitabı başlatma ve bir detay çalışma sayfası ekleme.  
- Master satırlarını detay sayfasına bağlayan bir Smart Marker ekleme.  
- `Order` nesnelerinden oluşan bir listeyi Smart Marker veri kaynağı olarak sağlama.  
- Eklenen verilere bağlı formülleri yeniden hesaplama.  
- Master‑detail ilişkiyi koruyarak son dosyayı kaydetme.  

**Önkoşullar:** Java 17 (veya daha yeni), Maven veya Gradle ve geçerli bir Aspose.Cells for Java lisansı (ücretsiz deneme testi için yeterlidir). Aspose.Cells ile hiç çalışmadıysanız endişelenmeyin—bu kılavuz sadece temel Java bilgisi gerektirir.

---

![master‑detail çalışma kitabı diyagramı](create_master_detail_workbook.png "master‑detail çalışma kitabı akışını gösteren diyagram")

## Master‑detail çalışma kitabı oluşturma – Adım 1: Çalışma kitabını başlatma

İlk olarak yeni bir `Workbook` örneğine ihtiyacımız var. Çalışma kitabını, master ve detail sayfalarının yaşayacağı bir tuval olarak düşünün.

```java
import com.aspose.cells.*;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and add the master and detail worksheets
        Workbook workbook = new Workbook();                 // empty workbook with a default sheet
        Worksheet masterSheet = workbook.getWorksheets().get(0); // the first sheet becomes the master
        Worksheet detailSheet = workbook.getWorksheets().add("Details"); // add a detail sheet
```

*Bu neden önemli:* Aspose.Cells her zaman bir varsayılan sayfa oluşturur, bu yüzden onu master olarak yeniden kullanıyoruz. Adlandırılmış bir detay sayfası (`"Details"`) eklemek, sonraki Smart Marker referansını netleştirir ve dosyayı düzenli tutar.

> **Pro tip:** Zaten bir şablon dosyanız varsa, `new Workbook()` yerine `new Workbook("template.xlsx")` kullanın. Diğer adımlar aynı kalır.

## Smart Marker ekleme – Adım 2: Master satırlarını detay sayfasına bağlama

Smart Marker’lar, Aspose.Cells’in çalışma zamanında veri ile değiştirdiği yer tutuculardır. `${DataSource,DetailSheet=SheetName}` sözdizimi, motorun hangi veriyi çekeceğini ve detay satırlarını nereye dökeceğini belirtir.

```java
        // Step 2: Insert the Smart Marker that links the master data to the detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");
```

*Bu neden önemli:* Marker’ı `A2` hücresine koymak, master satırının başlık satırının hemen altında (genellikle `A1`) başlamasını sağlar. `DetailSheet=Details` kısmı, **master‑detail ilişki**yi otomatik olarak oluşturur—her master satırı, `Details` sayfasında bir satır bloğu oluşturur.

> **Sık sorulan soru:** *Marker’ı farklı bir sütunda koyabilir miyim?* Kesinlikle. Hücre referansını (`B2`, `C2` vb.) ayarlayın ve şablonunuzun düzeninin buna uygun olduğundan emin olun.

## Veri kaynağı sağlama – Adım 3: POJO’ları Smart Marker’a bağlama

Şimdi Smart Marker’a gerçek veri veriyoruz. Bu örnekte, yardımcı bir sınıf olan `DataFactory` tarafından döndürülen `Order` POJO’larından oluşan bir liste kullanıyoruz.

```java
        // Step 3: Provide the data source for the Smart Marker (a list of Order objects)
        List<Order> orders = DataFactory.getOrders();   // your POJO list
        workbook.getSmartMarkers().setDataSource("Orders", orders);
```

*Bu neden önemli:* `"Orders"` anahtarı, `${...}` yer tutucusunda kullanılan isimle aynı olmalıdır. Aspose.Cells listeyi iterasyonla dolaşır, her `Order` için bir master satırı oluşturur ve ilgili alt verileri (varsa) detay sayfasına çeker.

> **Köşe durum:** Listeniz boşsa, Smart Marker master alanını boş bırakır—herhangi bir istisna atılmaz. Ancak dosya üretip üretmeyeceğinize karar vermek için `orders.isEmpty()` kontrolü yapabilirsiniz.

## Formülleri yeniden hesaplama – Adım 4: Hesaplamaları güncel tutma

Master‑detail sayfalarında genellikle miktarları toplama, toplamları hesaplama veya vergileri uygulama gibi formüller bulunur. Smart Marker veri ekledikten sonra bu formülleri yeniden hesaplamamız gerekir.

```java
        // Step 4: Recalculate any formulas that may depend on the inserted data
        workbook.calculateFormula();
```

*Bu neden önemli:* Bu çağrı olmadan, yeni eklenen satırları referans alan hücreler eski (veya #DIV/0!) değerleri gösterir. `calculateFormula()` tüm çalışma kitabını dolaşır, her bağımlı hücrenin yeni veriyi yansıtmasını sağlar.

> **Performans notu:** Çok büyük çalışma kitapları için yeniden hesaplamayı belirli bir sayfaya sınırlayabilirsiniz: `worksheet.calculateFormula()`. Çoğu master‑detail senaryosunda tüm çalışma kitabı çağrısı yeterlidir.

## Dosyayı kaydetme – Adım 5: Master‑detail çalışma kitabını dışa aktarma

Son olarak, çalışma kitabını diske yazın. Herhangi bir desteklenen formatı (`.xlsx`, `.xls`, `.csv` vb.) seçebilirsiniz—burada modern `.xlsx` formatını kullanıyoruz.

```java
        // Step 5: Save the workbook with the master‑detail relationship applied
        workbook.save("output/master-detail.xlsx"); // adjust path as needed
    }
}
```

*Bu neden önemli:* Kaydedilen dosya artık iki sayfa içerir: **Sheet1** (master) ve **Details** (detail). Excel’de açtığınızda, formüllerinizin yeniden hesaplandığı güzel biçimlendirilmiş bir master‑detail görünümü göreceksiniz.

> **Dikkat edilmesi gerekenler:** `calculateFormula()` çağrısını kaydetmeden önce atlamanız durumunda, Excel dosyayı açtığında yeniden hesaplama yapar; bu daha yavaş olabilir ve çalışma kitabı volatil fonksiyonlar içeriyorsa farklı sonuçlar doğurabilir.

---

## Tam kaynak kodu (çalıştırılabilir)

Tüm parçaları bir araya getirdiğimizde, IDE’nize kopyalayıp yapıştırabileceğiniz eksiksiz program aşağıdadır:

```java
import com.aspose.cells.*;
import java.util.List;

public class MasterDetailExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize workbook and worksheets
        Workbook workbook = new Workbook();
        Worksheet masterSheet = workbook.getWorksheets().get(0);
        Worksheet detailSheet = workbook.getWorksheets().add("Details");

        // Optional: Add headers to master sheet
        masterSheet.getCells().get("A1").putValue("Order ID");
        masterSheet.getCells().get("B1").putValue("Customer");
        masterSheet.getCells().get("C1").putValue("Total");

        // Step 2: Insert Smart Marker linking to detail sheet
        masterSheet.getCells().get("A2").putValue("${Orders,DetailSheet=Details}");

        // Step 3: Supply data source (list of Order POJOs)
        List<Order> orders = DataFactory.getOrders(); // assume this returns a populated list
        workbook.getSmartMarkers().setDataSource("Orders", orders);

        // Step 4: Recalculate formulas (if any)
        workbook.calculateFormula();

        // Step 5: Save the resulting workbook
        workbook.save("output/master-detail.xlsx");
    }
}
```

**Beklenen çıktı:** `master-detail.xlsx` dosyasını açın ve şunları göreceksiniz:

- **Sheet1** (master) her sipariş ID’si, müşteri adı ve toplamı listeler.  
- **Details** sayfası her siparişe ait satırları (ör. satır kalemleri) içerir.  
- Tüm toplam veya vergi formülleri doğru şekilde doldurulmuş olur.

---

## Sık sorulan varyasyonlar

| Soru | Cevap |
|----------|--------|
| *Boş bir çalışma kitabı yerine bir şablon kullanabilir miyim?* | Evet. `new Workbook("template.xlsx")` ile yükleyin ve Smart Marker’ı uygun hücreye yerleştirin. |
| *Detay verilerim ayrı bir listede olsaydı ne olur?* | Smart Marker’ları iç içe kullanabilirsiniz: `${Orders.Details,DetailSheet=Details}` burada `Details`, her `Order` nesnesinin satır kalemleri listesini dönen bir özelliktir. |
| *Detay satırlarını nasıl biçimlendirebilirim?* | Şablondaki ilk detay satırına bir stil uygulayın; Aspose.Cells bu stili her oluşturulan satır için kopyalar. |
| *Bir master satırı genişletilene kadar detay sayfasını gizlemenin bir yolu var mı?* | Smart Marker’lar aracılığıyla doğrudan mümkün değil, ancak sayfanın `Visible` özelliğini `false` yapabilir ve açıldıktan sonra VBA ile görünür hâle getirebilirsiniz. |

---

## Sonuç

Artık Java’da Aspose.Cells Smart Marker kullanarak **master‑detail çalışma kitabı oluşturma** konusunda bilgi sahibisiniz. Çalışma kitabını başlatma, Smart Marker ekleme, POJO listesini bağlama, formülleri yeniden hesaplama ve dosyayı kaydetme adımlarının her birini *neden* gerektiğini açıklayarak gösterdik; böylece bu deseni kendi projelerinize uyarlayabilirsiniz.

Şimdi bu örneği genişletin:

- Yüksek değerli siparişleri vurgulamak için koşullu biçimlendirme ekleyin.  
- `workbook.save("report.pdf", SaveFormat.PDF)` ile çalışma kitabını PDF olarak dışa aktarın.  
- Farklı Smart Marker adları kullanarak tek bir dosyada birden fazla master‑detail bölümü birleştirin.

**master‑

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve ek API özelliklerini keşfetmenize yardımcı olacak tam çalışan kod örnekleri içerir.

- [Java'da Aspose.Cells ile Excel Çalışma Kitabı Oluşturma: Adım Adım Kılavuz](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Aspose.Cells for Java ile Master Excel Dosyası Manipülasyonu | Çalışma Kitabı İşlemleri Kılavuzu](/cells/english/java/workbook-operations/master-excel-manipulation-aspose-cells-java/)
- [Aspose.Cells Java ile Excel'i HTML Olarak Oluşturma ve Dışa Aktarma | Çalışma Kitabı İşlemleri Kılavuzu](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}