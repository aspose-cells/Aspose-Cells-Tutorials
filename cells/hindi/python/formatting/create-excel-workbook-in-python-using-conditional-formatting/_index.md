---
category: general
date: 2026-09-21
description: Python में Excel वर्कबुक बनाना, सेल की पृष्ठभूमि रंग सेट करना, और Aspose.Cells
  के साथ तिथि-आधारित कंडीशनल फ़ॉर्मेटिंग लागू करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- format cells by date
- excel conditional formatting python
- date based conditional formatting
language: hi
lastmod: 2026-09-21
og_description: Python में Excel वर्कबुक बनाएं, सेल की पृष्ठभूमि रंग सेट करें, और
  Aspose.Cells का उपयोग करके तिथि-आधारित कंडीशनल फ़ॉर्मेटिंग लागू करें। चरण‑दर‑चरण
  गाइड का पालन करें।
og_image_alt: Screenshot of an Excel sheet showing a yellow‑green cell background
  for yesterday's dates
og_title: पायथन में कंडीशनल फ़ॉर्मेटिंग के साथ एक्सेल वर्कबुक बनाएं
schemas:
- author: Aspose
  dateModified: '2026-09-21'
  description: Learn how to create Excel workbook in Python, set cell background color,
    and apply date based conditional formatting with Aspose.Cells.
  headline: Create Excel workbook in Python using conditional formatting
  type: TechArticle
tags:
- Python
- Excel
- Aspose.Cells
title: Python में कंडीशनल फ़ॉर्मेटिंग का उपयोग करके Excel वर्कबुक बनाएं
url: /hi/python/formatting/create-excel-workbook-in-python-using-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में कंडीशनल फॉर्मेटिंग का उपयोग करके Excel वर्कबुक बनाएं

यदि आपको **create Excel workbook python** स्क्रिप्ट्स चाहिए जो तिथियों को स्वचालित रूप से हाइलाइट करें, तो यह गाइड आपको बिल्कुल बताता है कि कैसे। आप देखेंगे कि कैसे **set cell background color** सेट करें, “Yesterday” नियम जोड़ें, और फ़ाइल सहेजें—सब Aspose.Cells for Python के साथ।

प्रोग्रामेटिक रूप से Excel फ़ाइलों के साथ काम करना अक्सर कई शीट्स में समान फॉर्मेटिंग लॉजिक को दोहराने का मतलब होता है। इस ट्यूटोरियल के अंत तक आपके पास **excel conditional formatting python** के लिए एक पुन: उपयोग योग्य पैटर्न होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं।

## आवश्यकताएँ

- Python 3.8+ स्थापित है  
- `aspose-cells` पैकेज (`pip install aspose-cells`)  
- Python फ़ंक्शन्स और datetime मॉड्यूल की बुनियादी परिचितता  

कोई अतिरिक्त लाइब्रेरी आवश्यक नहीं है; Aspose.Cells सभी Excel ऑपरेशन्स को संभालता है।

## चरण 1: वर्कबुक बनाएं और पहली वर्कशीट तक पहुँचें

पहला चरण **create excel workbook python** ऑब्जेक्ट्स बनाना और डिफ़ॉल्ट वर्कशीट को प्राप्त करना है। यह आपको आगे की स्टाइलिंग के लिए एक साफ़ कैनवास देता है।

```python
# Import required Aspose.Cells classes
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# Create a new workbook; the first worksheet is at index 0
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*Why this matters:* `Workbook()` एक इन‑मे्मोरी Excel फ़ाइल बनाता है। `worksheets[0]` तक पहुँचने से शीट नामों को हार्ड‑कोड करने से बचा जाता है और यह तब भी काम करता है जब डिफ़ॉल्ट नाम बदल जाता है।

## चरण 2: TIME_PERIOD कंडीशनल फॉर्मेट जोड़ने के लिए हेल्पर

कोड को व्यवस्थित रखने के लिए, हम कंडीशनल‑फ़ॉर्मेट निर्माण को एक हेल्पर में लपेटते हैं। यह एक सेल रेंज, बैकग्राउंड रंग, और इच्छित टाइम‑पिरियड नियम प्राप्त करता है।

```python
def add_time_period(sheet, cell_range, bg_color, period_type):
    """
    Adds a TIME_PERIOD conditional formatting rule to `cell_range`.
    The rule paints the cells with `bg_color` when the date matches `period_type`.
    """
    # Retrieve (or create) the ConditionalFormatting collection for the range
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)

    # Insert a TIME_PERIOD condition and configure its style
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color          # set cell background color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type                # e.g., TimePeriodType.YESTERDAY
```

*Why this matters:* हेल्पर कंडीशनल फ़ॉर्मेट बनाने के दोहराव वाले चरणों को सारांशित करता है, जिससे इसे “Today” या “Last Week” जैसे अन्य डेट‑आधारित नियमों के लिए आसानी से पुन: उपयोग किया जा सकता है।

## चरण 3: “Yesterday” नियम को एक रेंज पर लागू करें

अब हम हेल्पर का उपयोग करके उन सेल्स को हाइलाइट करते हैं जिनमें कल की तिथि है। रेंज `I19:K20` शर्त पूरी होने पर **medium sea green** रंग में बदल जाएगी।

```python
add_time_period(
    worksheet,
    "I19:K20",                # range to format
    Color.medium_sea_green,  # set cell background color
    TimePeriodType.YESTERDAY # date based conditional formatting
)
```

*Why this matters:* `TimePeriodType.YESTERDAY` Aspose.Cells की बिल्ट‑इन एनेमरेशन का हिस्सा है, इसलिए आपको तिथियों की मैन्युअल गणना करने की आवश्यकता नहीं है। लाइब्रेरी हर बार वर्कबुक खोलने पर नियम का मूल्यांकन करती है।

## चरण 4: रेंज को नमूना तिथियों से भरें

नियम को क्रिया में देखने के लिए, हम दो तिथियां लिखते हैं—एक जो “Yesterday” से मेल खाती है और एक जो नहीं। `number` स्टाइल `30` एक बिल्ट‑इन डेट फ़ॉर्मेट से मेल खाता है।

```python
# Cell I19 gets a date that is exactly yesterday (relative to the sample data)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))   # 30 July 2008
cell.style.number = 30                # date format

# Cell K20 gets a date that is outside the rule
cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))    # 3 August 2008
cell.style.number = 30
```

*Why this matters:* ठोस तिथियों को डालकर आप सत्यापित कर सकते हैं कि कंडीशनल फॉर्मेटिंग काम कर रही है बिना किसी विशिष्ट दिन फ़ाइल खोलने की आवश्यकता के।

## चरण 5: एक वर्णनात्मक लेबल जोड़ें और कॉलम को ऑटो‑फ़िट करें

एक छोटा लेबल फॉर्मेटेड रेंज के उद्देश्य को स्पष्ट करता है, और `auto_fit_column` शीट को पढ़ने योग्य बनाता है।

```python
# Add a label under the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Adjust column width for better visibility (column 12 = L)
worksheet.auto_fit_column(12)
```

## चरण 6: वर्कबुक सहेजें

अंत में, वर्कबुक को डिस्क पर लिखें। `os.makedirs` कॉल यह सुनिश्चित करता है कि लक्ष्य फ़ोल्डर मौजूद हो।

```python
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)

# Save as XLSX – the most widely supported Excel format
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

जब आप *TimePeriodDemo.xlsx* खोलेंगे तो आप देखेंगे:

- सेल **I19** **medium sea green** रंग में शेडेड है क्योंकि इसका मान “Yesterday” नियम से मेल खाता है।  
- सेल **K20** डिफ़ॉल्ट बैकग्राउंड रखता है क्योंकि उसकी तिथि शर्त को पूरा नहीं करती।  

यह **format cells by date** को एक ही पंक्ति के Python कोड से दर्शाता है।

## पूरा, चलाने योग्य उदाहरण

सभी हिस्सों को मिलाकर, यहाँ पूर्ण स्क्रिप्ट है जिसे आप कॉपी‑पेस्ट करके चला सकते हैं:

```python
from aspose.cells import (
    Workbook, FormatConditionType, TimePeriodType,
    BackgroundType, Color, SaveFormat
)
from datetime import datetime
import os

# 1️⃣ Create workbook and get first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# 2️⃣ Helper to add TIME_PERIOD conditional formatting
def add_time_period(sheet, cell_range, bg_color, period_type):
    cf = sheet.conditional_formattings.get(cell_range)
    if cf is None:
        cf = sheet.conditional_formattings.add(cell_range)
    idx = cf.add_condition(FormatConditionType.TIME_PERIOD)
    condition = cf[idx]
    condition.style.background_color = bg_color
    condition.style.pattern = BackgroundType.SOLID
    condition.time_period = period_type

# 3️⃣ Apply “Yesterday” rule (set cell background color)
add_time_period(
    worksheet,
    "I19:K20",
    Color.medium_sea_green,
    TimePeriodType.YESTERDAY
)

# 4️⃣ Fill sample dates (format cells by date)
cell = worksheet.cells.get("I19")
cell.put_value(datetime(2008, 7, 30))
cell.style.number = 30

cell = worksheet.cells.get("K20")
cell.put_value(datetime(2008, 8, 3))
cell.style.number = 30

# 5️⃣ Add label and auto‑fit column
worksheet.cells.get("I20").put_value("Yesterday")
worksheet.auto_fit_column(12)

# 6️⃣ Save the workbook
output_path = os.path.join("YOUR_DIRECTORY", "TimePeriodDemo.xlsx")
os.makedirs(os.path.dirname(output_path), exist_ok=True)
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

स्क्रिप्ट चलाएँ, परिणामी फ़ाइल खोलें, और आप कंडीशनल फॉर्मेटिंग को क्रिया में देखेंगे।

## सामान्य विविधताएँ और किनारे के मामले

| विविधता | कैसे लागू करें | कब उपयोग करें |
|-----------|------------------|-------------|
| **“Today” को हाइलाइट करें** | `TimePeriodType.YESTERDAY` को `TimePeriodType.TODAY` से बदलें | रियल‑टाइम डैशबोर्ड्स |
| **एकाधिक रेंज** | प्रत्येक रेंज के लिए `add_time_period` को कॉल करें, विभिन्न रंग पास करते हुए | जटिल रिपोर्ट्स |
| **डायनेमिक डेट रेंज** | `TimePeriodType.LAST_7_DAYS` या `TimePeriodType.NEXT_MONTH` का उपयोग करें | रोलिंग रिपोर्ट्स |
| **कस्टम रंग** | किसी भी शेड बनाने के लिए `Color.from_argb(255, r, g, b)` का उपयोग करें | ब्रांड‑संगत स्टाइलिंग |

**Pro tip:** जब आप सॉलिड फ़िल चाहते हैं तो हमेशा `condition.style.pattern = BackgroundType.SOLID` सेट करें; अन्यथा Excel एक ग्रेडिएंट दिखा सकता है जो विभिन्न संस्करणों में असंगत दिखता है।

## निष्कर्ष

अब आप जानते हैं कि कैसे **create Excel workbook python** स्क्रिप्ट्स बनाएं जो **set cell background color** सेट करती हैं, **excel conditional formatting python** लागू करती हैं, और Aspose.Cells का उपयोग करके **format cells by date** करती हैं। यह उदाहरण एक **date based conditional formatting** परिदृश्य को कवर करता है, लेकिन वही पैटर्न किसी भी टाइम‑पिरियड नियम के लिए काम करता है।

अगले, आप अन्वेषण कर सकते हैं:

- डेटा बार या आइकन सेट जोड़ना (`FormatConditionType.DATA_BAR`)  
- एक ही रेंज पर कई कंडीशनल नियमों को संयोजित करना  
- रिपोर्टिंग के लिए वर्कबुक को PDF (`SaveFormat.PDF`) में एक्सपोर्ट करना  

विभिन्न रंगों, रेंजों, और टाइम‑पिरियड प्रकारों के साथ प्रयोग करने में संकोच न करें ताकि आपके विशिष्ट रिपोर्टिंग आवश्यकताओं के अनुरूप हो सके। कोडिंग का आनंद लें!

## आप को आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API सुविधाओं में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells for .NET के साथ Excel सेल फॉर्मेटिंग और वर्कबुक प्रबंधन में महारत हासिल करें](/cells/english/net/formatting/excel-formatting-aspose-cells-net/)
- [Aspose.Cells .NET के साथ Excel ऑटोमेशन&#58; वर्कबुक बनाएं और एक्सटर्नल लिंक सेट करें](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Aspose.Cells .NET का उपयोग करके Excel में वर्कबुक-स्कोप्ड नेम्ड रेंजेज कैसे बनाएं](/cells/english/net/range-management/excel-workbook-scoped-named-ranges-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}