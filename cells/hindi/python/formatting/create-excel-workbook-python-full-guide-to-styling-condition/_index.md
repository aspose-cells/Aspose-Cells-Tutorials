---
category: general
date: 2026-07-06
description: Python के साथ Excel वर्कबुक बनाएं, जिसमें कोड हो जो सेल की पृष्ठभूमि
  का रंग सेट करे, प्रोग्रामेटिक रूप से सेल स्टाइल सेट करे, और आज की तिथि को हाइलाइट
  करने के लिए कंडीशनल फ़ॉर्मेटिंग जोड़ता हो।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- set cell style programmatically
- highlight today date excel
- add conditional formatting python
language: hi
lastmod: 2026-07-06
og_description: Python का उपयोग करके तुरंत Excel वर्कबुक बनाएं। जानिए कैसे प्रोग्रामेटिक
  रूप से सेल की पृष्ठभूमि का रंग सेट करें, सेल शैली निर्धारित करें, और आज की तिथि
  को हाइलाइट करने के लिए Python में कंडीशनल फ़ॉर्मेटिंग जोड़ें।
og_image_alt: Screenshot of an Excel workbook created with Python showing colored
  cells and today’s date highlighted
og_title: Python से Excel वर्कबुक बनाएं – सेल्स को स्टाइल करें और आज को हाइलाइट करें
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
title: Python से Excel वर्कबुक बनाएं – स्टाइलिंग और कंडीशनल फ़ॉर्मेटिंग की पूरी गाइड
url: /hi/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting

क्या आपने कभी सोचा है कि **create Excel workbook Python** को बिना Excel खोले ही कैसे बनाया जाए? आप अकेले नहीं हैं। कई डेवलपर्स को रिपोर्ट, डैशबोर्ड या साधारण डेटा लॉग्स को तुरंत जेनरेट करना पड़ता है, और इसे प्रोग्रामेटिकली करने से मैन्युअल काम में कई घंटे बचते हैं।

इस ट्यूटोरियल में हम पूरी प्रक्रिया को कवर करेंगे: एक नई वर्कबुक बनाना, **set cell background color** सेट करना, **set cell style programmatically** लागू करना, और अंत में **highlight today date excel** को **add conditional formatting python** के साथ हाइलाइट करना। अंत तक आपके पास एक तैयार‑स्क्रिप्ट होगा जो सेकंडों में एक पॉलिश्ड .xlsx फ़ाइल बनाता है।

---

## What You’ll Build

- कुछ पॉप्युलेटेड सेल्स के साथ एक नई Excel फ़ाइल।
- कस्टम बैकग्राउंड के साथ रंगे हुए सेल्स।
- न्यूमेरिक और डेट वैल्यूज़ को एक विशिष्ट नंबर स्टाइल के साथ फॉर्मेट किया गया।
- एक कंडीशनल रूल जो स्वचालित रूप से आज की तारीख वाले सेल को हाइलाइट करता है।

कोई बाहरी Excel इंस्टॉलेशन आवश्यक नहीं—Aspose.Cells for Python via .NET सभी भारी काम करता है।

---

## Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | आधुनिक सिंटैक्स और टाइप हिंट्स |
| `aspose-cells` package | वर्कबुक मैनिपुलेशन के लिए कोर लाइब्रेरी |
| `aspose-pydrawing` (installed with Aspose.Cells) | `Color` क्लास प्रदान करता है |
| Basic familiarity with Excel concepts (cells, ranges, formatting) | ट्यूटोरियल को सुगमता से फॉलो करने में मदद करता है |

लाइब्रेरी को इस प्रकार इंस्टॉल करें:

```bash
pip install aspose-cells
```

---

## Step 1: Initialize the Workbook and Worksheet

जब आप **create excel workbook python** करते हैं, तो सबसे पहला कदम `Workbook` ऑब्जेक्ट को इंस्टैंशिएट करना और डिफ़ॉल्ट वर्कशीट को प्राप्त करना है। वर्कबुक को पूरे Excel फ़ाइल के रूप में सोचें, जबकि वर्कशीट एक सिंगल टैब है।

```python
from aspose.cells import Workbook

# Create a new workbook – this is our empty Excel file
book = Workbook()

# Grab the first (default) worksheet
sheet = book.worksheets[0]
```

> **Pro tip:** यदि आपको कई शीट्स चाहिए, तो `book.worksheets.add("MySheet")` का उपयोग करके और टैब जोड़ सकते हैं।

---

## Step 2: Helper Class for Styling & Conditional Formatting

नीचे एक कॉम्पैक्ट लेकिन पूर्ण `ConditionalFormatting` क्लास दिया गया है। यह दोहराव वाले कार्यों को रैप करता है:

1. `"A1:C3"` जैसे रेंज को `CellArea` में बदलना।
2. उस एरिया के हर सेल में क्रमिक नंबर भरना (सिर्फ डेमो के लिए)।
3. एक सॉलिड **set cell background color** लागू करना।
4. एक कंडीशनल रूल जोड़ना जो **highlight today date excel** करता है।

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

### Why a Helper Class?

- **Reusability:** आप `add_time_period_1()` को किसी भी वर्कशीट पर बिना लॉजिक दोबारा लिखे कॉल कर सकते हैं।
- **Clarity:** प्रत्येक मेथड एक काम करता है – क्लीन कोड की पहचान।
- **Extensibility:** और रूल जोड़ने हैं? बस वही पैटर्न फॉलो करके एक नया मेथड जोड़ें।

---

## Step 3: Apply the Formatting and Save the File

अब हम सब कुछ जोड़ते हैं: हेल्पर को इंस्टैंशिएट करें, फॉर्मेटिंग रूटीन चलाएँ, और अंत में वर्कबुक को डिस्क पर लिखें।

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

जब आप *styled_workbook.xlsx* खोलेंगे तो आपको दिखेगा:

- सेल्स **A1:C3** में 0‑8 तक नंबर होते हुए लाइट‑स्काई‑ब्लू फ़िल।
- सेल **I1** में आज की तारीख पिंक बैकग्राउंड के साथ (कंडीशनल रूल की वजह से)।
- सेल **K2** में तुलना के लिए स्थिर तिथि *2008‑07‑30*।
- सेल **I2** में टेक्स्ट “Today”।

यह विज़ुअल क्यू ठीक वही है जो **highlight today date excel** की आवश्यकता को पूरा करता है।

---

## Step 4: Dig Deeper – Customizing Styles

यदि आपको फ़ॉन्ट, बॉर्डर या नंबर फ़ॉर्मेट को कस्टमाइज़ करना है, तो आप `fill_cell` मेथड को एक्सटेंड कर सकते हैं या नया हेल्पर बना सकते हैं:

```python
def apply_custom_style(cell, font_name="Calibri", font_size=11, bold=False):
    style = cell.get_style()
    style.font.name = font_name
    style.font.size = font_size
    style.font.bold = bold
    cell.set_style(style)
```

फिर आप लूप के अंदर `apply_custom_style(cell, bold=True)` कॉल कर सकते हैं ताकि **set cell style programmatically** हर रेंज के सेल पर लागू हो सके।

---

## Common Pitfalls & How to Avoid Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Cells stay white despite `Color.light_sky_blue` | स्टाइल को `foreground_color` सेट करने के बाद लागू नहीं किया गया | स्टाइल ऑब्जेक्ट को मॉडिफ़ाई करने के बाद हमेशा `cell.set_style(style)` कॉल करें। |
| Conditional rule never fires | डेट सेल्स के लिए `style.number` सेट नहीं है, इसलिए Excel वैल्यू को स्ट्रिंग मानता है | `cell.put_value(datetime…)` से पहले `style.number = 30` (या कोई भी डेट फ़ॉर्मेट) सेट करें। |
| Workbook saves as .xls despite `SaveFormat.XLSX` | पुराना Aspose संस्करण जो डिफ़ॉल्ट रूप से लेगेसी फ़ॉर्मेट देता है | नवीनतम `aspose-cells` पैकेज में अपग्रेड करें। |
| Range like `"A1"` throws an index error | शीट को इनिशियलाइज़ नहीं किया गया और `cells.get("A1")` कॉल किया गया | सुनिश्चित करें कि वर्कशीट मौजूद है (`Workbook()` के तुरंत बाद), या ज़ीरो‑बेस्ड इंडेक्स के साथ `cells.get(row, col)` उपयोग करें। |

---

## Full Script for Copy‑Paste

नीचे वह **entire** स्क्रिप्ट है जिसे आप `create_excel.py` नाम की फ़ाइल में पेस्ट कर तुरंत चला सकते हैं।

```python
# create_excel.py
from aspose.cells import (
    Workbook, CellArea, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat, CellsHelper
)
from aspose.pydrawing import Color
from datetime import datetime

class ConditionalFormatting:
    """Utility for styling cells and adding conditional formatting."""
    def __init__(self, worksheet):
        self._sheet = worksheet

    def get_format_condition(self, cell_range: str, color: Color):
        index = self._sheet.conditional_formattings.add()
        cf = self._sheet.conditional_formattings[index]
        area = self.get_cell_area_by_name(cell_range)
        cf.add_area(area)
        self.fill_cell(cell_range, color)
        return cf

    def fill_cell(self, cell_range: str, color: Color):
        area = self.get_cell_area_by_name(cell_range)
        counter = 0
        for col in range(area.start_column, area.end_column + 1):
            for row in range(area.start_row, area.end_row + 1):
                cell = self._sheet.cells.get(row, col)
                if color != Color.empty:
                    style = cell.get_style()
                    style.foreground_color = color
                    style.pattern = BackgroundType.SOLID
                    cell.set_style(style)
                cell.put_value(counter)
                counter += 1

    @staticmethod
    def get_cell_area_by_name(name:


## What Should You Learn Next?

नीचे दिए गए ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक रिसोर्स में पूर्ण कार्यशील कोड उदाहरण और स्टेप‑बाय‑स्टेप एक्सप्लेनैशन शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Excel Automation with Aspose.Cells .NET: Create Workbook & Set External Links](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}