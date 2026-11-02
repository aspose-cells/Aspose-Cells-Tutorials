---
category: general
date: 2026-09-15
description: Aspose.Cells के साथ Python में समय अवधि की कंडीशनल फ़ॉर्मेटिंग लागू करना
  और वर्कबुक को XLSX के रूप में सहेजना सीखें। इसमें चरण‑दर‑चरण कोड शामिल है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- time period conditional formatting
- save workbook as xlsx
- how to create excel workbook python
- how to highlight yesterday in excel
- add conditional formatting python
language: hi
lastmod: 2026-09-15
og_description: Python का उपयोग करके Excel में समय अवधि के आधार पर कंडीशनल फॉर्मेटिंग
  लागू करें और वर्कबुक को XLSX के रूप में सहेजें। Aspose.Cells के लिए इस पूर्ण गाइड
  का पालन करें।
og_image_alt: Screenshot of an Excel sheet where the cells for yesterday are highlighted
  in pink
og_title: Python के साथ Excel में समय अवधि के लिए सशर्त स्वरूपण लागू करें
schemas:
- author: Aspose
  dateModified: '2026-09-15'
  description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  headline: How to apply time period conditional formatting in Excel using Python
  type: TechArticle
- description: Learn how to apply time period conditional formatting and save workbook
    as XLSX with Aspose.Cells in Python. Includes step‑by‑step code.
  name: How to apply time period conditional formatting in Excel using Python
  steps:
  - name: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
    text: '**Creating the workbook** gives you an in‑memory Excel file you can manipulate
      without opening Excel.'
  - name: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
    text: '**Defining the range** (`I19:K20`) tells Aspose.Cells where the rule applies,
      keeping the logic isolated.'
  - name: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
    text: '**Adding a TIME_PERIOD condition** uses Aspose’s built‑in enumeration `TimePeriodType.YESTERDAY`.
      This avoids manual date calculations and automatically updates when the file
      is opened on a different day.'
  - name: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
    text: '**Setting the style** (`background_color` and `pattern`) determines how
      the highlighted cells appear. Using `Color.pink` makes the rule easy to spot.'
  - name: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
    text: '**Writing sample dates** with number format 30 ensures Excel displays them
      as short dates rather than serial numbers.'
  - name: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
    text: '**Auto‑fitting the column** improves readability for anyone opening the
      file later.'
  - name: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
    text: '**Saving as XLSX** produces a widely compatible file that can be opened
      in Excel, Google Sheets, or any modern spreadsheet program.'
  - name: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
    text: Cells `I19` and `K20` contain the dates `30‑07‑2008` and `03‑08‑2008`.
  - name: The cell `I20` shows the text “Yesterday”.
    text: The cell `I20` shows the text “Yesterday”.
  - name: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
    text: If you change your system date to **July 30 2008** and reopen the file,
      the cells with matching dates are automatically filled with pink.
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: Python का उपयोग करके Excel में समय अवधि की शर्तीय स्वरूपण कैसे लागू करें
url: /hi/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में Python का उपयोग करके टाइम पीरियड कंडीशनल फॉर्मेटिंग कैसे लागू करें

यदि आपको Excel फ़ाइल में **time period conditional formatting** चाहिए, तो यह ट्यूटोरियल आपको Python के साथ इसे कैसे करना है, बिल्कुल दिखाता है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो एक वर्कबुक बनाता है, कल की तिथियों को हाइलाइट करता है, और **save workbook as XLSX** केवल कुछ लाइनों के कोड में।

कंडीशनल फॉर्मेटिंग एक शक्तिशाली तरीका है जिससे आप उन डेटा पर ध्यान आकर्षित कर सकते हैं जो किसी विशिष्ट नियम को पूरा करता है। इस गाइड में हम “Yesterday” टाइम पीरियड पर ध्यान केंद्रित करते हैं, लेकिन यही पैटर्न अन्य बिल्ट‑इन पीरियड्स जैसे Today, LastWeek, और NextMonth के लिए भी काम करता है। ट्यूटोरियल के अंत तक आप **how to create excel workbook python**‑स्टाइल स्क्रिप्ट्स बना पाएँगे जो प्रोडक्शन के लिए तैयार होंगी।

## पूर्वापेक्षाएँ

- Python 3.8+ स्थापित हो  
- `aspose-cells` और `aspose-pydrawing` पैकेज (`pip install aspose-cells aspose-pydrawing`)  
- Python सिंटैक्स की बुनियादी परिचितता  

कोई अतिरिक्त Office इंस्टॉलेशन आवश्यक नहीं है क्योंकि Aspose.Cells फ़ाइल जनरेशन को आंतरिक रूप से संभालता है।

## Aspose.Cells के साथ Python में टाइम पीरियड कंडीशनल फॉर्मेटिंग

यह सेक्शन मुख्य कार्य के लिए आवश्यक प्रत्येक कोड लाइन को समझाता है। नीचे दिया गया कोड ब्लॉक पूर्ण स्क्रिप्ट है; टिप्पणियाँ प्रत्येक चरण के उद्देश्य को समझाती हैं।

```python
# -*- coding: utf-8 -*-
"""
Apply time period conditional formatting to highlight yesterday's dates
and save the workbook as XLSX using Aspose.Cells for Python.
"""

from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the range that will receive the conditional formatting rule
cell_range = "I19:K20"
cond_format = worksheet.conditional_formattings.add(cell_range)

# Step 3: Add a TIME_PERIOD condition for “Yesterday” and style it
condition_index = cond_format.add_condition(FormatConditionType.TIME_PERIOD)
condition = cond_format[condition_index]
condition.style.background_color = Color.pink          # Highlight colour
condition.style.pattern = BackgroundType.SOLID        # Solid fill
condition.time_period = TimePeriodType.YESTERDAY      # Built‑in “Yesterday” period

# Step 4: Populate the range with sample dates (Excel number format 30 = short date)
date_cells = ["I19", "K20"]                           # Cells that will contain dates
sample_dates = [datetime(2008, 7, 30), datetime(2008, 8, 3)]
for cell_ref, date_val in zip(date_cells, sample_dates):
    cell = worksheet.cells.get(cell_ref)
    cell.put_value(date_val)                         # Write the Python datetime
    style = cell.get_style()
    style.number = 30                                 # Excel short date format
    cell.set_style(style)

# Step 5: Add a label so the user knows what the rule represents
worksheet.cells.get("I20").put_value("Yesterday")

# Step 6: Auto‑fit the column for better readability (column L is index 12)
worksheet.auto_fit_column(12)

# Step 7: Save the workbook – this demonstrates “save workbook as xlsx”
output_path = "TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

### प्रत्येक चरण क्यों महत्वपूर्ण है

1. **Creating the workbook** आपको एक इन‑मेमोरी Excel फ़ाइल देता है जिसे आप Excel खोले बिना ही संशोधित कर सकते हैं।  
2. **Defining the range** (`I19:K20`) Aspose.Cells को बताता है कि नियम कहाँ लागू होता है, जिससे लॉजिक अलग रहता है।  
3. **Adding a TIME_PERIOD condition** Aspose की बिल्ट‑इन एन्यूमरेशन `TimePeriodType.YESTERDAY` का उपयोग करता है। इससे मैन्युअल डेट कैलकुलेशन से बचा जाता है और फ़ाइल किसी अन्य दिन खुले तो स्वचालित रूप से अपडेट हो जाता है।  
4. **Setting the style** (`background_color` और `pattern`) निर्धारित करता है कि हाइलाइटेड सेल्स कैसे दिखेंगी। `Color.pink` का उपयोग करने से नियम आसानी से दिखाई देता है।  
5. **Writing sample dates** संख्या फ़ॉर्मेट 30 के साथ यह सुनिश्चित करता है कि Excel उन्हें शॉर्ट डेट के रूप में दिखाए, न कि सीरियल नंबरों के रूप में।  
6. **Auto‑fitting the column** फ़ाइल को बाद में खोलने वाले किसी भी व्यक्ति के लिए पठनीयता बढ़ाता है।  
7. **Saving as XLSX** एक व्यापक रूप से संगत फ़ाइल बनाता है जिसे Excel, Google Sheets, या किसी भी आधुनिक स्प्रेडशीट प्रोग्राम में खोला जा सकता है।

## Aspose.Cells के साथ Excel वर्कबुक Python‑स्टाइल कैसे बनाएं

ऊपर दिया गया स्क्रिप्ट पहले से ही **how to create excel workbook python** के न्यूनतम चरण दिखाता है। वास्तविक उपयोग में आप चाह सकते हैं:

- एकाधिक वर्कशीट्स जोड़ें (`workbook.worksheets.add("Report")`)।  
- लूप या pandas DataFrames (`worksheet.cells.import_data_table`) के साथ बड़े डेटा टेबल भरें।  
- अतिरिक्त फॉर्मेटिंग (फ़ॉन्ट, बॉर्डर) `cell.get_style()` का उपयोग करके लागू करें।  

इन सभी कार्यों में वही पैटर्न अपनाया जाता है: ऑब्जेक्ट प्राप्त करें, उसकी प्रॉपर्टीज़ बदलें, और `set_style` या `save` को कॉल करें।

## Python में कंडीशनल फॉर्मेटिंग जोड़ें – अन्य उपयोगी पैटर्न

“Yesterday” उदाहरण के अलावा, Aspose.Cells कई कंडीशनल‑फ़ॉर्मेटिंग प्रकारों का समर्थन करता है:

| FormatConditionType | Typical use case |
|---------------------|------------------|
| `FORMAT_CONDITION_TYPE_EXPRESSION` | कस्टम फ़ॉर्मूले (`=A1>100`) |
| `FORMAT_CONDITION_TYPE_CELL_VALUE` | सरल तुलना (`>`, `<`, `=`) |
| `FORMAT_CONDITION_TYPE_COLOR_SCALE` | ग्रेडिएंट कलर स्केल्स |
| `FORMAT_CONDITION_TYPE_DATA_BAR`   | इन‑सेल बार विज़ुअलाइज़ेशन |

संख्यात्मक थ्रेशोल्ड के लिए **add conditional formatting python** करने हेतु, आप `FormatConditionType.TIME_PERIOD` को `FormatConditionType.CELL_VALUE` से बदलेंगे और `condition.operator_type` तथा `condition.formula1` सेट करेंगे।

```python
# Example: highlight values greater than 500
idx = cond_format.add_condition(FormatConditionType.CELL_VALUE)
cond = cond_format[idx]
cond.operator_type = ConditionOperatorType.GREATER_THAN
cond.formula1 = "500"
cond.style.background_color = Color.light_green
```

## XLSX के रूप में वर्कबुक सहेजें – सर्वोत्तम प्रैक्टिसेज

जब आप **save workbook as xlsx** करते हैं, तो विचार करें:

- **सही `SaveFormat` निर्दिष्ट करना** (`SaveFormat.XLSX`) ताकि लेगेसी फ़ॉर्मेट्स से बचा जा सके।  
- यदि स्क्रिप्ट लूप में चलती है तो **निर्धारित फ़ाइल नाम** उपयोग करें (`f"report_{datetime.now():%Y%m%d}.xlsx"`)।  
- लॉन्ग‑रनिंग सर्विसेज़ में **संसाधनों को बंद करना** (`workbook.dispose()`) ताकि नेटिव मेमोरी मुक्त हो सके।  

उदाहरण में पहले से ही `SaveFormat.XLSX` का उपयोग किया गया है, जो एक आधुनिक, ज़िप‑आधारित वर्कबुक बनाता है जो सभी कंडीशनल‑फ़ॉर्मेटिंग नियमों को बनाए रखता है।

## Excel में कल को हाइलाइट करें – सत्यापन चरण

स्क्रिप्ट चलाने के बाद, `TimePeriodExample.xlsx` खोलें:

1. सेल्स `I19` और `K20` में तिथियाँ `30‑07‑2008` और `03‑08‑2008` हैं।  
2. सेल `I20` में टेक्स्ट “Yesterday” दिखता है।  
3. यदि आप अपना सिस्टम डेट **July 30 2008** में बदलते हैं और फ़ाइल को पुनः खोलते हैं, तो मिलती‑जुलती तिथियों वाले सेल्स स्वचालित रूप से पिंक से भर जाएंगे।  
4. सिस्टम डेट को किसी अन्य दिन में बदलने से पिंक फ़िल हट जाता है, जिससे पुष्टि होती है कि नियम **time period conditional formatting** लॉजिक पर प्रतिक्रिया करता है।  

## सामान्य गलतियाँ और उन्हें कैसे टालें

- **Missing `aspose-pydrawing`** – `Color` क्लास इस पैकेज में रहती है; इसे इंस्टॉल करना भूलने पर `ImportError` उत्पन्न होता है।  
- **Incorrect number format** – डिफ़ॉल्ट General फ़ॉर्मेट का उपयोग करने से सीरियल नंबर (जैसे 39822) दिखते हैं। शॉर्ट डेट्स के लिए हमेशा `style.number = 30` सेट करें।  
- **Range mismatch** – कंडीशनल फ़ॉर्मेटिंग रेंज में उन सेल्स को शामिल होना चाहिए जिन्हें आप हाइलाइट करना चाहते हैं; अन्यथा नियम का कोई प्रभाव नहीं पड़ेगा।  

## प्रो टिप: फॉर्मेटिंग रूटीन को पुनः उपयोग करें

यदि आपको कई वर्कबुक में वही “Yesterday” नियम चाहिए, तो लॉजिक को एक हेल्पर फ़ंक्शन में रैप करें:

```python
def apply_yesterday_highlight(worksheet, address):
    cf = worksheet.conditional_formattings.add(address)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    cond = cf[idx]
    cond.style.background_color = Color.pink
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

जहाँ भी आवश्यक हो, `apply_yesterday_highlight(worksheet, "A1:A10")` को कॉल करें।

## निष्कर्ष

इस गाइड ने आपको दिखाया कि Python का उपयोग करके Excel में **time period conditional formatting** कैसे लागू करें, **save workbook as XLSX** कैसे करें, और एक ही पुन: उपयोग योग्य स्क्रिप्ट से **highlight yesterday in Excel** कैसे करें। अब आपके पास किसी भी ऑटोमेशन प्रोजेक्ट में **add conditional formatting python** कोड जोड़ने की ठोस नींव है, चाहे आप दैनिक रिपोर्ट बना रहे हों, डैशबोर्ड तैयार कर रहे हों, या डेटा एक्सपोर्ट तैयार कर रहे हों।

**अगले कदम**

- `TimePeriodType` के अन्य मान जैसे `TODAY` या `LAST_WEEK` का अन्वेषण करें।  
- एक ही रेंज पर कई कंडीशनल नियमों को मिलाकर अधिक समृद्ध विज़ुअल संकेत बनाएं।  
- वर्कबुक जनरेशन को वेब सर्विस या शेड्यूल्ड जॉब में इंटीग्रेट करें।  

कोडिंग का आनंद लें, और कंडीशनल फॉर्मेटिंग द्वारा आपके Excel ऑटोमेशन में लाई गई विज़ुअल स्पष्टता का आनंद उठाएँ!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर करने में मदद करेंगे।

- [Master Conditional Formatting in Excel Using Aspose.Cells .NET : A Comprehensive Guide](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Master Aspose.Cells .NET : Apply Conditional Formatting to Alternate Rows in Excel](/cells/english/net/formatting/aspose-cells-net-conditional-formatting-alternate-rows/)
- [Master Conditional Formatting with Custom Fonts in Excel using Aspose.Cells for .NET and C#](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}