---
category: general
date: 2026-07-20
description: Aspose.Cells के साथ Python में Excel वर्कबुक बनाएं, सेल की पृष्ठभूमि
  रंग सेट करें, और तिथि के आधार पर सेल को स्टाइल करने के लिए कंडीशनल फ़ॉर्मेटिंग जोड़ें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- aspose cells conditional formatting
- add conditional formatting python
language: hi
lastmod: 2026-07-20
og_description: Aspose.Cells का उपयोग करके Python में Excel वर्कबुक बनाएं। सेल की
  पृष्ठभूमि रंग सेट करना और तिथि के आधार पर सेल को फॉर्मेट करने के लिए Python में
  कंडीशनल फॉर्मेटिंग जोड़ना सीखें।
og_image_alt: Screenshot of an Excel workbook created with Python showing conditional
  formatting applied to date cells
og_title: Python में Excel वर्कबुक बनाएं – कंडीशनल फ़ॉर्मेटिंग जोड़ें
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Create Excel workbook Python with Aspose.Cells, set cell background
    color, and add conditional formatting python to style cells by date.
  headline: Create Excel Workbook Python – Conditional Formatting Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Change `"I19:K20"` to any A1‑style range, and adjust the sample
      dates accordingly.
    question: Can I target a different date range?
  - answer: Use `FormatConditionType.FORMULA` and set `condition.formula1 = "YOUR_FORMULA"`—for
      example, `=TODAY()-A1=1` to mimic yesterday.
    question: What if I need a custom formula instead of `YESTERDAY`?
  - answer: Call `conditions.add_condition` again with a different `FormatConditionType`.
      The order matters; later rules can override earlier ones.
    question: How do I apply multiple rules to the same range?
  - answer: Yes—modify `condition.style.font.color = Color.white` (or any other `Color`).
    question: Is there a way to set font colour together with background?
  type: FAQPage
tags:
- Aspose.Cells
- Python
- Excel Automation
title: Python के साथ Excel वर्कबुक बनाएं – कंडीशनल फ़ॉर्मेटिंग गाइड
url: /hi/python/formatting/create-excel-workbook-python-conditional-formatting-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel वर्कबुक Python बनाएं – कंडीशनल फ़ॉर्मेटिंग गाइड

क्या आपने कभी सोचा है कि **create Excel workbook Python** को शुरू से कैसे बनाएं और UI खोले बिना इसे परिपूर्ण दिखाएँ? आप अकेले नहीं हैं। कई डेवलपर्स को तब रुकावट आती है जब उन्हें **set cell background color** या प्रोग्रामेटिकली डेट‑आधारित स्टाइल लागू करनी होती है।  

इस ट्यूटोरियल में हम एक पूर्ण, चलाने योग्य उदाहरण के माध्यम से चलते हैं जो Aspose.Cells का उपयोग करके **add conditional formatting python** नियम जोड़ता है, डेट के आधार पर सेल्स को फ़ॉर्मेट करता है, और परिणाम को आधुनिक XLSX फ़ाइल के रूप में सहेजता है। अंत तक आपके पास एक स्व-समाहित स्क्रिप्ट होगी जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## आप क्या सीखेंगे

- वर्कबुक को इनिशियलाइज़ करना और पहली वर्कशीट को प्राप्त करना।  
- पूरे रेंज के लिए **set cell background color** कैसे सेट करें।  
- **aspose cells conditional formatting** का उपयोग करके “Yesterday” डेट को हाइलाइट करना।  
- कॉलम्स को ऑटो‑फ़िट करना और फ़ाइल को डिस्क पर सहेजना।  

कोई बाहरी कॉन्फ़िगरेशन आवश्यक नहीं—सिर्फ Python 3 और Aspose.Cells पैकेज। यदि आपने पहले से `aspose-cells` इंस्टॉल किया है, तो आप तैयार हैं; अन्यथा एक तेज़ `pip install aspose-cells` कर लें।

## आवश्यकताएँ

- Python 3.8+ (कोड 3.9, 3.10 और नए संस्करणों पर काम करता है)।  
- Aspose.Cells for Python via .NET (`aspose-cells` NuGet wrapper)।  
- Excel की बुनियादी अवधारणाओं (सेल्स, रेंजेज, फ़ॉर्मेटिंग) की परिचितता।  

इन सबके पास हैं? बढ़िया—चलते हैं आगे।

## Create Excel Workbook Python – सेटअप और वर्कशीट

सबसे पहले हमें एक नया वर्कबुक ऑब्जेक्ट और डिफ़ॉल्ट वर्कशीट का रेफ़रेंस चाहिए। यही वह कैनवास है जहाँ बाद के सभी ऑपरेशन होंगे।

```python
# Import the necessary Aspose.Cells classes
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and grab the first sheet
workbook = Workbook()                     # create excel workbook python
worksheet = workbook.worksheets[0]        # default is the first worksheet
```

> **यह क्यों महत्वपूर्ण है:** `Workbook()` एक इन‑मेमोरी Excel फ़ाइल बनाता है, जिससे किसी भी टेम्पररी फ़ाइल की ज़रूरत नहीं पड़ती। `worksheet` वेरिएबल हमारे सेल‑लेवल एक्शन का एंट्री पॉइंट है।

## Set Cell Background Color

कोई भी नियम जोड़ने से पहले, टार्गेट रेंज को बेस कलर देना अच्छा रहता है ताकि कंडीशनल फ़ॉर्मेटिंग उभर कर दिखे। नीचे दिया गया हेल्पर एक `FormatConditionCollection` को (यदि मौजूद नहीं है तो बनाकर) प्राप्त करता है और सेल्स को सॉलिड बैकग्राउंड से पेंट करता है।

```python
def get_format_condition(cell_range: str, base_color: Color):
    """
    Obtain (or create) a FormatConditionCollection for `cell_range`.
    Also set a base background colour for the whole range.
    """
    # Retrieve or add a conditional formatting entry for the range
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    # Apply the base colour to every cell in the range
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color          # set cell background color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection
```

> **प्रो टिप:** यदि आप एक ही रेंज को कई नियमों के साथ पुनः उपयोग करने वाले हैं, तो इस हेल्पर को एक बार कॉल करें और रिटर्नेड कलेक्शन को रखें; इससे कुछ API कॉल्स बचते हैं।

## Add Conditional Formatting Python for Date Ranges

अब मज़ेदार हिस्सा: हम एक **time‑period conditional formatting** नियम बनाएँगे जो कल की डेट वाले सेल्स को हाइलाइट करेगा। यह Aspose.Cells का उपयोग करके **format cells by date** की शक्ति को दर्शाता है।

```python
def apply_yesterday_rule():
    """
    Apply a “Yesterday” conditional formatting rule to the range I19:K20.
    Cells that match will turn pink; others stay with the base colour.
    """
    # Obtain the condition collection for the target range
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)

    # Create a TIME_PERIOD condition (this is the aspose cells conditional formatting type we need)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]

    # Define the appearance for cells that meet the condition
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Set the time period to “Yesterday”
    condition.time_period = TimePeriodType.YESTERDAY

    # Populate sample dates to demonstrate the rule
    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))   # matches “Yesterday”
    cell_i19.style.number = 30                 # Excel number format for dates
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))    # does NOT match
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    # Add a label for clarity
    worksheet.cells.get("I20").put_value("Yesterday")
```

> **`TIME_PERIOD` क्यों उपयोग करें?** यह कस्टम फ़ॉर्मूले लिखने की ज़रूरत को हटाता है। Aspose.Cells डेट को वर्तमान सिस्टम डेट के खिलाफ एवाल्यूएट करता है, इसलिए नियम हमेशा प्रासंगिक रहता है।

### Running the Rule

```python
apply_yesterday_rule()
```

जब आप परिणामी फ़ाइल खोलेंगे, तो सेल `I19` पिंक (क्योंकि वह “Yesterday” है) चमकेगा, जबकि `K20` बेस ग्रीन कलर में रहेगा।

## Auto‑Fit Columns and Save Workbook

एक साफ़-सुथरी स्प्रेडशीट प्रोफ़ेशनल दिखती है। ऑटो‑फ़िटिंग सुनिश्चित करता है कि हमारा डेटा भीड़भाड़ वाला न लगे।

```python
# Step 4: Auto‑fit the column width for a tidy appearance
worksheet.auto_fit_column(12)   # column index is zero‑based; 12 corresponds to column M

# Step 5: Save the workbook to disk
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **एज केस:** यदि आप किसी ऐसे डायरेक्टरी को टार्गेट करते हैं जो मौजूद नहीं है, तो `workbook.save` एक एरर उठाएगा। यदि आपको ग्रेसफ़ुल हैंडलिंग चाहिए तो `try/except` ब्लॉक में सेव कॉल को रैप करें।

### Full Script (Copy‑Paste Ready)

नीचे पूरा स्क्रिप्ट दिया गया है, जो चलाने के लिए तैयार है। बस `YOUR_DIRECTORY` को अपने मशीन पर वैध फ़ोल्डर से बदलें।

```python
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create the workbook and worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

def get_format_condition(cell_range: str, base_color: Color):
    condition_collection = worksheet.conditional_formattings.get(
        worksheet.conditional_formattings.add(cell_range)
    )
    for cell_name in cell_range.split(":"):
        cell = worksheet.cells.get(cell_name)
        cell.style.background_color = base_color
        cell.style.pattern = BackgroundType.SOLID
    return condition_collection

def apply_yesterday_rule():
    conditions = get_format_condition("I19:K20", Color.medium_sea_green)
    index = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[index]
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = TimePeriodType.YESTERDAY

    cell_i19 = worksheet.cells.get("I19")
    cell_i19.put_value(datetime(2008, 7, 30))
    cell_i19.style.number = 30
    cell_i19.set_style(cell_i19.style)

    cell_k20 = worksheet.cells.get("K20")
    cell_k20.put_value(datetime(2008, 8, 3))
    cell_k20.style.number = 30
    cell_k20.set_style(cell_k20.style)

    worksheet.cells.get("I20").put_value("Yesterday")

apply_yesterday_rule()
worksheet.auto_fit_column(12)

output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

इस स्क्रिप्ट को चलाने पर `TimePeriodExample.xlsx` बन जाएगा जिसमें हमने वर्णित कंडीशनल फ़ॉर्मेटिंग होगी।

## Common Questions & Tips

- **क्या मैं किसी अलग डेट रेंज को टार्गेट कर सकता हूँ?**  
  बिल्कुल। `"I19:K20"` को किसी भी A1‑स्टाइल रेंज में बदलें, और सैंपल डेट्स को उसी अनुसार एडजस्ट करें।

- **यदि मुझे `YESTERDAY` के बजाय कस्टम फ़ॉर्मूला चाहिए तो?**  
  `FormatConditionType.FORMULA` उपयोग करें और `condition.formula1 = "YOUR_FORMULA"` सेट करें—उदाहरण के लिए, `=TODAY()-A1=1` ताकि कल की डेट का सिमुलेशन हो सके।

- **मैं एक ही रेंज पर कई नियम कैसे लागू करूँ?**  
  `conditions.add_condition` को फिर से कॉल करें लेकिन अलग `FormatConditionType` के साथ। क्रम मायने रखता है; बाद के नियम पहले वाले को ओवरराइड कर सकते हैं।

- **क्या बैकग्राउंड के साथ फ़ॉन्ट कलर भी सेट कर सकते हैं?**  
  हाँ—`condition.style.font.color = Color.white` (या कोई अन्य `Color`) को मॉडिफ़ाई करें।

## निष्कर्ष

अब आप जानते हैं कि **create Excel workbook Python** को Aspose.Cells के साथ कैसे बनाएं, **set cell background color** कैसे सेट करें, और **add conditional formatting python** का उपयोग करके डेट के आधार पर सेल्स को फ़ॉर्मेट करें। स्क्रिप्ट पूरी तरह फ़ंक्शनल है, मिसिंग डायरेक्टरी जैसे एज केस को हैंडल करती है, और इसे मल्टी‑रूल कंडीशनल लॉजिक या डायनामिक रेंज डिटेक्शन जैसे अधिक उन्नत परिदृश्यों के लिए विस्तारित किया जा सकता है।

अगला कदम तैयार है? “Yesterday” नियम को “Last Week” से बदलें, ग्रेडिएंट फ़िल्स के साथ प्रयोग करें, या दर्जनों फ़ॉर्मेटेड टेबल्स वाले पूर्ण रिपोर्ट जेनरेट करें। बिल्डिंग ब्लॉक्स यहाँ सब हैं, और आपने **aspose cells conditional formatting** को Python में मास्टर कर लिया है।

हैप्पी कोडिंग, और अपने वैरिएशन्स को कमेंट्स में शेयर करना न भूलें!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Master Excel Cell Formatting and Workbook Management with Aspose.Cells for .NET](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [How to Create and Save an Excel Workbook as ODS Using Aspose.Cells for .NET](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)
- [How to Create Workbook Scoped Named Ranges in Excel Using Aspose.Cells .NET](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}