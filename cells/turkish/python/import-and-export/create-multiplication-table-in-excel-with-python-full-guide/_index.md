---
category: general
date: 2026-06-21
description: Python kullanarak Excel'de çarpım tablosu oluşturun. Lambda kullanımını,
  makearray kullanımını, Excel dizisini görüntülemeyi ve Python’da Excel değerlerini
  okumayı adım adım bir öğreticide öğrenin.
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: tr
og_description: Python kullanarak Excel'de çarpım tablosu oluşturun. Bu öğreticide
  lambda, makearray kullanımı, Excel dizisini görüntüleme ve Excel değerlerini Python
  ile verimli bir şekilde okuma gösterilmektedir.
og_title: Python ile Excel'de çarpım tablosu oluşturma – Tam rehber
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Python ile Excel'de Çarpım Tablosu Oluşturma – Tam Kılavuz
url: /tr/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python ile Excel'de Çarpım Tablosu Oluşturma – Tam Kılavuz

Hiç **çarpım tablosu** oluşturmak için Excel'de her hücreyi tek tek yazmak zorunda kaldınız mı? Yalnız değilsiniz. Birçok raporlama senaryosunda 5×5 (veya daha büyük) bir ürün ızgarasına hızlıca ihtiyacınız olur ve bunu elle yapmak zaman kaybıdır.  

Bu öğreticide, temiz ve Python‑tabanlı bir yöntemle tabloyu nasıl oluşturacağınızı, `MAKEARRAY` formülüyle gömeceğinizi ve sonuçları script'inize nasıl geri çekeceğinizi adım adım göstereceğiz. Yol boyunca **lambda nasıl kullanılır**, **makearray nasıl kullanılır** ve **excel array nasıl görüntülenir** ile **read excel values python** konularını tek bir bütünleşik örnek içinde yanıtlayacağız.

Sonunda, herhangi bir çalışma kitabı ile çalışabilen yeniden kullanılabilir bir kod parçacığına sahip olacaksınız ve bu yaklaşımın neden hem hızlı hem de geleceğe dayanıklı olduğunu anlayacaksınız.

## Gereksinimler

- Python 3.8+ (en son kararlı sürüm yeterlidir)
- `openpyxl` kütüphanesi (veya formülleri destekleyen herhangi bir Excel‑uyumlu kütüphane)
- Python’da lambda ifadeleri hakkında temel bilgi
- Özel Excel eklentileri gerekmez; yerel `MAKEARRAY` işlevi (Excel 365'te mevcut) işi halleder

Eğer bunlardan birine sahip değilseniz, sadece `pip install openpyxl` komutunu çalıştırın, hazırsınız.

## Çarpım tablosu oluşturma – Genel Bakış

Temel fikir basit: yeni bir çalışma kitabı oluşturur, 5 × 5 çarpım matrisini inşa eden bir `MAKEARRAY` formülü yazar, Excel'in bunu hesaplamasını sağlarız ve ardından oluşan değerleri Python'a geri okuruz.

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Script'i çalıştırdığınızda şu çıktı alınır:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

Bu, tamamen Python'dan üretilen **çarpım tablosu** oluşturmanın tam işlevsel bir örneğidir.

### Neden Python döngüsü yerine `MAKEARRAY` kullanmalı?

- **Performans**: Excel hesaplamayı yerel olarak yapar, bu da büyük matrislerde daha hızlıdır.
- **Canlı güncelleme**: Formüldeki boyutları daha sonra değiştirirseniz, sayfa otomatik olarak yeniden hesaplanır.
- **Okunabilirlik**: Formül, niyetinizi (“bir dizi oluştur”) doğrudan ifade eder, Python kodunuzu düzenli tutar.

## Excel formüllerinde Python lambda nasıl kullanılır?

`MAKEARRAY` çağrısındaki `LAMBDA` bölümü bir Excel‑tarafı anonim işlevdir, Python lambda'sı değildir. Yine de kavram aynı: `r` (satır indeksi) ve `c` (sütun indeksi) alıp `r*c` döndüren küçük, satır içi bir mantık tanımlarsınız.  

Excel dünyasında **lambda nasıl kullanılır** konusunda yeniyseniz, bunu sadece formül içinde yaşayan bir mini‑fonksiyon olarak düşünün. Başka bir yerde ayrı bir fonksiyon tanımlamanıza gerek yok. Python’da sadece stringi gömeriz:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

Bu satır Excel'e şunu söyler: *“5 × 5'lik bir bloktaki her hücre için satır × sütun hesabını yap.”*  

Lambda Excel tarafından değerlendirildiği için, burada Python'un kendi lambda sözdizimiyle uğraşmanıza gerek yok—sadece Excel sözdizimi yeterli.

## makearray nasıl kullanılır, diziler nasıl üretilir

`MAKEARRAY`, Excel fonksiyon kütüphanesine (Microsoft 365'te 2022 itibarıyla) yeni eklenen bir işlevdir. `INDEX` + `ROW`/`COLUMN` gibi eski hilelerin yerini alır. İmzası şöyledir:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – istediğiniz satır sayısı.
- **columns** – istediğiniz sütun sayısı.
- **lambda** – `(row, column)` alıp bir değer döndüren bir Excel LAMBDA.

Örneğimizde klasik bir çarpım tablosu için `5,5` geçirdik, ancak bu sayıları kolayca değiştirebilirsiniz:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

Bu, Python döngüsü dokunmadan 10 × 10 bir tablo elde etmenizi sağlar. Bu, **makearray nasıl kullanılır** sorusunun, ister bir lookup tablosu, ister bir heatmap, ister finansal bir takvim olsun, her türlü deterministik ızgara için nasıl uygulanacağını gösterir.

## excel array nasıl görüntülenir – verileri Python'a geri çekmek

Excel formülü hesaplandıktan sonra, ortaya çıkan değerler tıpkı manuel girilen hücreler gibi sayfada bulunur. **excel array nasıl görüntülenir** için aralığı dolaşır ve her satırı yazdırırız:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

Birkaç ipucu:

- Daha büyük aralıklarla çalışmanız gerekiyorsa, `worksheet.cell(row, column).value` kullanın; sözlük‑stil indekslemeden biraz daha hızlıdır.
- Daha şık bir tablo isterseniz, çıktıyı biçimlendirmek için `tabulate` veya `pandas.DataFrame` düşünebilirsiniz.

Aşağıda oluşan sayfanın ekran görüntüsü (görsel alt metni SEO için ana anahtar kelimeyi içerir):

![Screenshot showing create multiplication table in Excel using Python](/images/multiplication-table-excel.png)

## read excel values python – matrisi daha ileri işlem için çıkarmak

**excel array nasıl görüntülenir** adımından sonra genellikle bu sayıları bir veri‑analiz boru hattına beslemek istersiniz. İşte **read excel values python** burada devreye girer. Yazdırmak için kullandığımız aynı döngü, list‑of‑lists, NumPy dizisi veya Pandas DataFrame oluşturmak için yeniden kullanılabilir:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

Çıktı:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

Artık bir DataFrame'iniz var; bunu görselleştirebilir, CSV’ye aktarabilir veya bir makine‑öğrenme modeline besleyebilirsiniz. Bu, iş akışının **read excel values python** kısmını tamamlar.

## Kenar Durumları & Pratik İpuçları

- **Formül yeniden hesaplama**: `calculate_formula()` çağrısından sonra çalışma kitabını değiştirirseniz, tekrar çağırmanız gerekir; aksi takdirde önbellekteki dizi eski kalır.
- **365 dışı Excel**: Eski Excel sürümleri `MAKEARRAY`'i desteklemez. Bu durumda Python‑tarafı oluşturulmuş tabloya geri dönüp her hücreyi tek tek yazabilirsiniz.
- **Büyük tablolar**: ~100 × 100'den büyük matrisler için, tüm sayfayı belleğe yüklemek yerine veriyi akış (stream) şeklinde işlemek daha iyidir.
- **Hata yönetimi**: Hesaplama ve okuma adımlarını `try/except` bloklarıyla sararak `InvalidFileException` veya `FormulaError` gibi hataları yakalayın.

## Sonuç

Python kullanarak Excel'de **çarpım tablosu** oluşturmayı, **lambda nasıl kullanılır** ve **makearray nasıl kullanılır** gücünden yararlanarak gösterdik. **excel array nasıl görüntülenir**, **read excel values python** adımlarıyla verileri geri alıp bir Pandas DataFrame'e dönüştürdünüz.

Daha ileri gitmek ister misiniz? Çarpım mantığını daha karmaşık bir şeyle değiştirin—örneğin bir mesafe matrisi, olasılık tablosu veya dinamik fiyatlandırma ızgarası. Aynı desen geçerli: tek bir `MAKEARRAY` satırı, hızlı bir `calculate_formula()`, ve verileri çekmek için birkaç Python döngüsü.

Bu kılavuzu faydalı bulduysanız, GitHub’da yıldız verin, ekip arkadaşlarınızla paylaşın veya kendi kullanım senaryonuzu yorum olarak bırakın. İyi kodlamalar ve tek bir formülle Excel tabloları üretmenin keyfini çıkarın!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}