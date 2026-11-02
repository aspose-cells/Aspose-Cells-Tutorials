---
category: general
date: 2026-08-08
description: Python का उपयोग करके Excel वर्कबुक बनाएं और तिथि के आधार पर कंडीशनल फ़ॉर्मेटिंग
  जोड़ें। Aspose.Cells का उपयोग करके कल की कोशिकाओं को हाइलाइट करने के लिए चरण‑दर‑चरण
  गाइड।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- conditional formatting based on date
- Aspose.Cells Python example
- Excel date formatting Python
- Python Excel automation
language: hi
lastmod: 2026-08-08
og_description: Aspose.Cells के साथ Python में Excel वर्कबुक बनाएं और गतिशील स्प्रेडशीट्स
  के लिए तिथि के आधार पर कंडीशनल फ़ॉर्मेटिंग लागू करें।
og_image_alt: Screenshot of an Excel sheet created with Python showing cells highlighted
  by date conditional formatting
og_title: Python के साथ Excel वर्कबुक बनाएं – तिथि शर्तीय स्वरूपण
schemas:
- author: Aspose
  dateModified: '2026-08-08'
  description: Create Excel workbook Python and add conditional formatting based on
    date. Step‑by‑step guide using Aspose.Cells to highlight yesterday’s cells.
  headline: Create Excel workbook Python date conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: एक्सेल वर्कबुक बनाएं पायथन तिथि सशर्त स्वरूपण
url: /hi/python/formatting/create-excel-workbook-python-date-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में Excel वर्कबुक बनाना और तिथि के आधार पर कंडीशनल फॉर्मेटिंग

यदि आपको **create Excel workbook Python** बनाना है और स्वचालित रूप से उन सेल्स को हाइलाइट करना है जो किसी विशिष्ट तिथि से मेल खाते हैं, तो यह ट्यूटोरियल आपको बिल्कुल वही दिखाता है। आप **conditional formatting based on date** लागू करना सीखेंगे ताकि कल की तिथियों का पिंक रंग में प्रकाशन हो, Aspose.Cells लाइब्रेरी का उपयोग करके।

यह गाइड हर चरण को विस्तार से बताता है—SDK को इंस्टॉल करने से लेकर अंतिम .xlsx फ़ाइल को सेव करने तक—ताकि आप एक कार्यशील उदाहरण को अपने प्रोजेक्ट में कॉपी‑पेस्ट कर सकें। बाहरी दस्तावेज़ीकरण की आवश्यकता नहीं है; सभी कोड और व्याख्याएँ स्वयं में पूर्ण हैं।

## पूर्वापेक्षाएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास है:

* Python 3.8 या उससे नया संस्करण स्थापित हो।
* `aspose-cells` पैकेज (Aspose.Cells का Python रैपर)। इसे इस प्रकार इंस्टॉल करें:
  ```bash
  pip install aspose-cells
  ```
* Python और Excel की बुनियादी अवधारणाओं की समझ, जैसे वर्कशीट्स और सेल स्टाइल्स।

> **Pro tip:** Aspose.Cells माइक्रोसॉफ्ट Excel के बिना भी काम करता है, जिससे यह सर्वर‑साइड ऑटोमेशन के लिए आदर्श बन जाता है।

## चरण 1: Python में Excel वर्कबुक बनाएं

पहला कार्य एक नई वर्कबुक को इंस्टैंशिएट करना और डिफ़ॉल्ट वर्कशीट को प्राप्त करना है। यह ऑब्जेक्ट पूरी Excel फ़ाइल का प्रतिनिधित्व करता है और पंक्तियों, स्तंभों और फॉर्मेटिंग API तक पहुँच प्रदान करता है।

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook – this automatically adds one worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]   # reference to the first (default) sheet
```

वर्कबुक बनाना आगे की किसी भी मैनिपुलेशन की नींव है, चाहे आप डेटा, फ़ॉर्मूले या फॉर्मेटिंग नियम जोड़ रहे हों।

## चरण 2: तिथि‑आधारित कंडीशनल फॉर्मेट परिभाषित करें

अब हम **conditional formatting based on date** जोड़ते हैं। `FormatConditionType.TIME_PERIOD` एन्‍युम हमें बिल्ट‑इन टाइम पीरियड्स जैसे Yesterday, Today, या LastWeek निर्दिष्ट करने की अनुमति देता है।

```python
from aspose.cells import FormatConditionType, BackgroundType, TimePeriodType
from aspose.pydrawing import Color

# Target range I19:K20 – three columns by two rows
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions

# Add a new time‑period condition (e.g., Yesterday)
condition_index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[condition_index]

# Set the visual style: pink solid background
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Specify that the condition should trigger for "Yesterday"
condition.time_period = TimePeriodType.YESTERDAY
```

यह चरण क्यों महत्वपूर्ण है: Excel रेंज में प्रत्येक सेल के लिए शर्त का मूल्यांकन करता है। जब किसी सेल का मान परिभाषित अवधि (कल) में आता है, तो हमने जो स्टाइल असाइन किया है वह स्वचालित रूप से लागू हो जाता है।

## चरण 3: नमूना तिथियों के साथ रेंज को भरें

नियम को कार्य में देखाने के लिए, हम लक्ष्य सेल्स में कुछ `datetime` ऑब्जेक्ट लिखते हैं। इनमें से एक को जानबूझकर वर्कबुक की आंतरिक तिथि प्रणाली के सापेक्ष कल की तिथि पर सेट किया गया है।

```python
from datetime import datetime

# Cell I19 – yesterday’s date (will be highlighted)
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # This date matches the "Yesterday" rule
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel’s built‑in date format
cell_i19.set_style(style_i19)

# Cell K20 – a random later date (no highlight)
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Not yesterday, so no formatting
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

`number = 30` पंक्ति Excel को मान को उसके मानक शॉर्ट‑डेट फ़ॉर्मेट में दिखाने के लिए कहती है। यदि आप अलग प्रस्तुति चाहते हैं तो इस इंडेक्स को किसी भी बिल्ट‑इन नंबर फ़ॉर्मेट में बदल सकते हैं।

## चरण 4: पठनीयता के लिए कॉलम की चौड़ाई समायोजित करें

तिथियों वाले कॉलम को ऑटो‑फ़िट करने से आउटपुट पढ़ने में आसान हो जाता है, विशेषकर जब वर्कबुक को Excel या किसी व्यूअर में खोला जाता है।

```python
# Column 12 corresponds to column L (zero‑based indexing)
worksheet.auto_fit_column(12)
```

## चरण 5: वर्कबुक को डिस्क पर सेव करें

अंत में, वर्कबुक को .xlsx फ़ाइल के रूप में सहेजें। `"YOUR_DIRECTORY"` को अपने मशीन पर वास्तविक पथ से बदलें।

```python
import os

output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

जब आप `TimePeriodDemo.out.xlsx` को Excel में खोलते हैं, तो सेल **I19** पिंक बैकग्राउंड के साथ दिखेगा क्योंकि उसका मान “Yesterday” नियम से मेल खाता है, जबकि **K20** अपरिवर्तित रहेगा।

### अपेक्षित आउटपुट

| I19 (date) | I20 (label) | J19 | J20 | K19 | K20 (date) |
|------------|-------------|-----|-----|-----|------------|
| *2008‑07‑30* (पिंक बैकग्राउंड) | Yesterday | – | – | – | *2008‑08‑03* (कोई फॉर्मेटिंग नहीं) |

पिंक शेडिंग पुष्टि करती है कि **conditional formatting based on date** इच्छित रूप से काम कर रहा है।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | कोड को कैसे अनुकूलित करें |
|-----------|-----------------------|
| **“Yesterday” के बजाय “Today” को हाइलाइट करना** | `condition.time_period = TimePeriodType.TODAY` को बदलें |
| **पूरे कॉलम पर नियम लागू करना** | `worksheet.get_range("A:A").format_conditions` का उपयोग करें |
| **कस्टम तिथि रेंज (जैसे, पिछले 7 दिन) का उपयोग करना** | टाइम‑पीरियड शर्त को फ़ॉर्मूला शर्त से बदलें: <br>```python<br>condition = conditions.add_condition(FormatConditionType.FORMULA)<br>condition.formula1 = 'AND(A1>=TODAY()-7, A1<=TODAY())'<br>``` |
| **विभिन्न बैकग्राउंड रंग** | `condition.style.background_color = Color.light_green` सेट करें (या कोई भी `Color` जो आप पसंद करें) |
| **डिस्प्ले के बिना Linux पर चलाना** | Aspose.Cells पूरी तरह हेडलेस है; अतिरिक्त कॉन्फ़िगरेशन की आवश्यकता नहीं। |

## पूर्ण, चलाने योग्य उदाहरण

नीचे वह संपूर्ण स्क्रिप्ट है जिसे आप जैसा है वैसा ही चलाकर देख सकते हैं (आउटपुट डायरेक्टरी को अपडेट करने के बाद)। सभी इम्पोर्ट्स, टिप्पणियाँ, और बुनियादी एरर‑हैंडलिंग शामिल हैं।

```python
# -*- coding: utf-8 -*-
"""
Create Excel workbook Python with date conditional formatting.
Demonstrates how to highlight yesterday’s dates using Aspose.Cells.
"""

import os
from datetime import datetime
from aspose.cells import (
    Workbook, SaveFormat,
    FormatConditionType, BackgroundType,
    TimePeriodType
)
from aspose.pydrawing import Color

# ----------------------------------------------------------------------
# 1️⃣ Initialize workbook
# ----------------------------------------------------------------------
workbook = Workbook()
worksheet = workbook.worksheets[0]

# ----------------------------------------------------------------------
# 2️⃣ Add conditional formatting for "Yesterday"
# ----------------------------------------------------------------------
range_obj = worksheet.get_range("I19:K20")
conditions = range_obj.format_conditions
cond_idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
condition = conditions[cond_idx]

# Visual style: pink solid fill
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
condition.time_period = TimePeriodType.YESTERDAY

# ----------------------------------------------------------------------
# 3️⃣ Populate sample dates
# ----------------------------------------------------------------------
# Cell that should match the condition
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Yesterday relative to demo data
style_i19 = cell_i19.get_style()
style_i19.number = 30                       # Excel short‑date format
cell_i19.set_style(style_i19)

# Cell that does NOT match
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))
style_k20 = cell_k20.get_style()
style_k20.number = 30
cell_k20.set_style(style_k20)

# Optional label
worksheet.cells.get("I20").put_value("Yesterday")

# ----------------------------------------------------------------------
# 4️⃣ Auto‑fit column for better visibility
# ----------------------------------------------------------------------
worksheet.auto_fit_column(12)   # Column L (0‑based index)

# ----------------------------------------------------------------------
# 5️⃣ Save workbook
# ----------------------------------------------------------------------
output_dir = "YOUR_DIRECTORY"   # <-- replace with a real folder
os.makedirs(output_dir, exist_ok=True)
output_path = os.path.join(output_dir, "TimePeriodDemo.out.xlsx")
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

स्क्रिप्ट चलाने से एक Excel फ़ाइल बनती है जहाँ “Yesterday” सेल स्वचालित रूप से हाइलाइट हो जाता है, जिससे **create Excel workbook Python** को **conditional formatting based on date** के साथ संयोजित करने का प्रदर्शन होता है।

## निष्कर्ष

अब आप जानते हैं कि **create Excel workbook Python** ऑब्जेक्ट्स कैसे बनाते हैं, **date‑based conditional formatting** को कैसे परिभाषित करते हैं


## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Create an Excel Workbook using Aspose.Cells in Java: A Step‑By‑Step Guide](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Create Excel Workbook with Charts Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/charts-graphs/create-excel-workbook-charts-aspose-cells-net/)
- [Excel Automation: Create a Workbook and Add a ListBox Using Aspose.Cells for .NET](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}