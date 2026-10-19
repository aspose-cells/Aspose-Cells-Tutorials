---
category: general
date: 2026-07-06
description: Python ile hücre arka plan rengini ayarlayan, hücre stilini programlı
  olarak belirleyen ve bugünün tarihini vurgulamak için koşullu biçimlendirme ekleyen
  bir Excel çalışma kitabı oluşturun.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: tr
lastmod: 2026-07-06
og_description: Python ile Excel çalışma kitabını anında oluşturun. Hücre arka plan
  rengini ayarlamayı, hücre stilini programlı olarak belirlemeyi ve bugünün tarihini
  vurgulamak için Python’da koşullu biçimlendirme eklemeyi öğrenin.
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Python ile Excel Çalışma Kitabı Oluştur – Hücreleri Stilize Et ve Bugünü
  Vurgula
schemas:
- author: Aspose
  dateModified: '2026-07-06'
  description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  headline: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  type: TechArticle
- description: Create Excel workbook Python with code to set cell background color,
    set cell style programmatically, and add conditional formatting python for highlighting
    today’s date.
  name: Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting
  steps:
  - name: Converting a range like `"A1:C3"` into a `CellArea`.
    text: Converting a range like `"A1:C3"` into a `CellArea`.
  - name: Filling every cell in that area with a sequential number (just for demo
      purposes).
    text: Filling every cell in that area with a sequential number (just for demo
      purposes).
  - name: Applying a solid **set cell background color**.
    text: Applying a solid **set cell background color**.
  - name: Adding a conditional rule that **highlight today date excel**.
    text: Adding a conditional rule that **highlight today date excel**.
  type: HowTo
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Python ile Excel Çalışma Kitabı Oluşturma – Stil ve Koşullu Biçimlendirme İçin
  Tam Kılavuz
url: /tr/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Çalışma Kitabı Python Oluşturma – Stil ve Koşullu Biçimlendirme Tam Kılavuzu

Hiç **create Excel workbook Python**'ı sıfırdan, Excel'i açmadan nasıl oluşturabileceğinizi merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici raporlar, panolar veya hatta basit veri günlükleri oluşturmak zorunda ve bunu programlı olarak yapmak saatlerce manuel çalışmayı tasarruf ettirir.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: yepyeni bir çalışma kitabı oluşturmak, **set cell background color** ayarlamak, **set cell style programmatically** ayarlamak ve sonunda **add conditional formatting python** kullanarak **highlight today date excel**. Sonunda saniyeler içinde şık bir .xlsx dosyası üreten hazır bir betiğe sahip olacaksınız.

---

## Oluşturacağınız Şey

- Birkaç doldurulmuş hücreye sahip yeni bir Excel dosyası.
- Özel bir arka plan rengiyle renklendirilmiş hücreler.
- Belirli bir sayı stiliyle biçimlendirilmiş sayısal ve tarih değerleri.
- Bugünün tarihini içeren hücreyi otomatik olarak vurgulayan bir koşullu kural.

Harici bir Excel kurulumuna gerek yok—Aspose.Cells for Python via .NET tüm ağır işleri yapar.

---

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| Python 3.8+ | Modern sözdizimi ve tip ipuçları |
| `aspose-cells` paketi | Çalışma kitabı manipülasyonu için temel kütüphane |
| `aspose-pydrawing` (Aspose.Cells ile kurulur) | `Color` sınıfını sağlar |
| Excel kavramlarına (hücreler, aralıklar, biçimlendirme) temel aşinalık | Öğreticinin akışını sorunsuz hâle getirir |

Install the library with:

```bash
pip install aspose-cells
```

---

## Adım 1: Çalışma Kitabı ve Çalışma Sayfasını Başlatma

İlk olarak **create excel workbook python** yaptığınızda bir `Workbook` nesnesi oluşturup varsayılan çalışma sayfasını alırsınız. Çalışma kitabını tüm Excel dosyası, çalışma sayfasını ise içindeki tek bir sekme olarak düşünün.

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Pro tip:** Birden fazla sayfa ihtiyacınız varsa, daha fazla sekme eklemek için `book.worksheets.add("MySheet")` kullanın.

---

## Adım 2: Stil ve Koşullu Biçimlendirme için Yardımcı Sınıf

Aşağıda, kompakt ama eksiksiz bir `ConditionalFormatting` sınıfı yer alıyor. Tekrarlayan görevleri şu şekilde sarar:

1. `"A1:C3"` gibi bir aralığı `CellArea`'ya dönüştürmek.
2. O alandaki her hücreyi sıralı bir sayı ile doldurmak (sadece demo amaçlı).
3. Katı bir **set cell background color** uygulamak.
4. **highlight today date excel** yapan bir koşullu kural eklemek.

```python
from aspose.cells import (
    CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """
    Utility class that demonstrates how to:
    • set cell background color
    • set cell style programmatically
    • add conditional formatting python
    """
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        """
        Creates a conditional formatting object for the given range
        and fills the range with a background color.
        """
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]

        # Convert "A1:C3" → CellArea object
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)

        # Paint the whole area with the supplied color
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        """
        Populates each cell in the range with an incrementing integer
        and applies the supplied background color.
        """
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)

                # Apply background only if a real color is supplied
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)

                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name: str) -> CellArea:
        """
        Parses an Excel‑style address (e.g. "B2:D4") into a CellArea.
        """
        area = CellArea()
        parts = name.replace("$", "").split(':')

        start_row, start_col = CellsHelper.cell_name_to_index(parts[0])
        area.start_row = start_row
        area.start_column = start_col

        if len(parts) == 2:
            end_row, end_col = CellsHelper.cell_name_to_index(parts[1])
            area.end_row = end_row
            area.end_column = end_col
        else:
            area.end_row = start_row
            area.end_column = start_col
        return area

    # -----------------------------------------------------------------
    # Step 2: Add conditional formatting for TODAY
    # -----------------------------------------------------------------
    def add_time_period_1(self):
        """
        Demonstrates add conditional formatting python that highlights
        cells containing today’s date.
        """
        # 1️⃣ Create a formatting range and give it a neutral background
        cf = self.get_format_condition("I1:K2", Color.light_slate_gray)

        # 2️⃣ Add a TIME_PERIOD condition (Today)
        idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
        cond = cf[idx]
        cond.time_period = TimePeriodType.TODAY
        cond.style.background_color = Color.pink
        cond.style.pattern = BackgroundType.SOLID

        # 3️⃣ Populate the cells with date values
        # Cell I1 – today’s date, formatted as a date
        cell = self._sheet.cells.get("I1")
        style = cell.get_style()
        style.number = 30               # 30 = “mm-dd-yy” style in Aspose
        cell.set_style(style)
        cell.put_value(datetime.today())

        # Cell K2 – an arbitrary past date for contrast
        self._sheet.cells.get("K2").put_value(datetime(2008, 7, 30))

        # Cell I2 – a label so the reader knows what’s being highlighted
        self._sheet.cells.get("I2").put_value("Today")
```

### Neden Yardımcı Sınıf?

- **Yeniden Kullanılabilirlik:** Herhangi bir çalışma sayfası için mantığı yeniden yazmadan `add_time_period_1()` çağırabilirsiniz.
- **Açıklık:** Her yöntem tek bir şey yapar – temiz kodun bir özelliği.
- **Genişletilebilirlik:** Daha fazla kural eklemek ister misiniz? Aynı deseni izleyen bir yöntem daha ekleyin.

---

## Adım 3: Biçimlendirmeyi Uygula ve Dosyayı Kaydet

Şimdi her şeyi birleştiriyoruz: yardımcı sınıfı örnekleyin, biçimlendirme rutinini çalıştırın ve sonunda çalışma kitabını diske yazın.

```python
# Instantiate the helper with our worksheet
formatter = ConditionalFormatting(sheet)

# Fill a demo range with numbers and a light blue background
formatter.get_format_condition("A1:C3", Color.light_sky_blue)

# Add the “today” conditional rule
formatter.add_time_period_1()

# Save the workbook – choose any location you like
output_path = "styled_workbook.xlsx"
book.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

When you open *styled_workbook.xlsx* you should see:

- **A1:C3** hücreleri 0‑8 ile numaralandırılmış ve açık gökyüzü mavisi dolgu rengine sahip.
- **I1** hücresi pembe arka planla bugünün tarihini gösterir (koşullu kural sayesinde).
- **K2** hücresi karşılaştırma için sabit tarih *2008‑07‑30* gösterir.
- **I2** hücresi “Today” metnini içerir.

Bu görsel ipucu, **highlight today date excel** gereksiniminin tam olarak istediği şeydir.

---

## Adım 4: Daha Derine İncele – Stilleri Özelleştirme

Yazı tiplerini, kenarlıkları veya sayı biçimlerini ayarlamanız gerekiyorsa, `fill_cell` yöntemini genişletebilir veya yeni bir yardımcı oluşturabilirsiniz:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

Daha sonra döngü içinde `apply_custom_style(cell, bold=True)` çağırarak bir aralıktaki her hücre için **set cell style programmatically** yapabilirsiniz.

---

## Yaygın Tuzaklar ve Nasıl Önlenir

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Hücreler `Color.light_sky_blue` despite beyaz kalıyor | Stil `foreground_color` ayarlandıktan sonra uygulanmadı | Stil nesnesini değiştirdikten sonra her zaman `cell.set_style(style)` çağırın. |
| Koşullu kural hiç tetiklenmiyor | Tarih hücreleri için `style.number` ayarlanmamış, bu yüzden Excel değeri string olarak kabul ediyor | `cell.put_value(datetime…)` öncesinde `style.number = 30` (veya herhangi bir tarih formatı) ayarlayın. |
| `SaveFormat.XLSX` kullanılmasına rağmen çalışma kitabı .xls olarak kaydediliyor | Varsayılan eski formatı kullanan eski Aspose sürümü | En son `aspose-cells` paketine yükseltin. |
| `"A1"` gibi bir aralık indeks hatası veriyor | Başlatılmamış bir sayfada `cells.get("A1")` kullanılması | Çalışma sayfasının var olduğundan emin olun (`Workbook()` sonrası vardır), ya da sıfır‑tabanlı indekslerle `cells.get(row, col)` kullanın. |

---

## Kopyala‑Yapıştır İçin Tam Betik

Aşağıda, `create_excel.py` adlı bir dosyaya koyup hemen çalıştırabileceğiniz **tam** betik bulunmaktadır.



## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Aspose.Cells .NET ile Excel Otomasyonu: Çalışma Kitabı Oluşturma ve Dış Bağlantılar Ayarlama](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Aspose.Cells for .NET ile Excel Hücre Biçimlendirme ve Çalışma Kitabı Yönetimini Öğrenin](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Otomasyonu: Aspose.Cells for .NET Kullanarak Çalışma Kitabı Oluşturma ve ListBox Ekleme](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}