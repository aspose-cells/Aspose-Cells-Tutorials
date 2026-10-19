---
category: general
date: 2026-09-05
description: Python में Excel वर्कबुक बनाएं और कल की कोशिकाओं को हाइलाइट करने के लिए
  कंडीशनल फॉर्मेटिंग जोड़ें। पूरा कोड सीखें और प्रत्येक चरण क्यों महत्वपूर्ण है, यह
  समझें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- add conditional formatting excel
- highlight cells based on date
- add conditional formatting range
- how to highlight yesterday cells
language: hi
lastmod: 2026-09-05
og_description: Python में Excel वर्कबुक बनाएं और कल की कोशिकाओं को हाइलाइट करने के
  लिए कंडीशनल फॉर्मेटिंग जोड़ें। पूर्ण समाधान के लिए इस चरण‑दर‑चरण गाइड का पालन करें।
og_image_alt: Screenshot of an Excel sheet where cells are highlighted after creating
  Excel workbook in Python
og_title: Python में Excel वर्कबुक बनाएं – कंडीशनल फ़ॉर्मेटिंग जोड़ें
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Create Excel workbook in Python and add conditional formatting to highlight
    yesterday cells. Learn the full code and why each step matters.
  headline: Create Excel workbook in Python with conditional formatting
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Python में कंडीशनल फॉर्मेटिंग के साथ Excel वर्कबुक बनाएं
url: /hi/python/formatting/create-excel-workbook-in-python-with-conditional-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में Conditional Formatting के साथ Excel वर्कबुक बनाएं

यदि आपको रिपोर्टिंग कार्य के लिए **create Excel workbook python** की आवश्यकता है, तो यह गाइड आपको दिखाएगा कि कैसे एक वर्कबुक जनरेट करें और एक conditional formatting नियम लागू करें जो कल की तिथियों को हाइलाइट करे। आप सटीक कोड, प्रत्येक पंक्ति का उद्देश्य, और अन्य तिथि रेंज के लिए समाधान को कैसे अनुकूलित करें, देखेंगे।

Conditional formatting एक शक्तिशाली तरीका है जिससे आप उन डेटा पर ध्यान आकर्षित कर सकते हैं जो किसी विशिष्ट शर्त को पूरा करता है। इस ट्यूटोरियल में हम Aspose.Cells लाइब्रेरी for Python via .NET का उपयोग करते हैं, जो Microsoft Office की आवश्यकता के बिना पूरी Excel फीचर सपोर्ट प्रदान करती है। गाइड के अंत तक आपके पास एक फ़ाइल होगी जहाँ रेंज *I19:K20* के सेल्स में यदि कल की तिथि होगी तो पिंक हो जाएंगे।

## आवश्यकताएँ

शुरू करने से पहले सुनिश्चित करें कि आपके पास हैं:

* Python 3.9+ स्थापित हो
* `aspose-cells` पैकेज (`pip install aspose-cells` के साथ स्थापित करें)
* Python सिंटैक्स का बुनियादी परिचय
* जिस डायरेक्टरी में वर्कबुक सहेजी जाएगी, वहाँ लिखने की अनुमति

कोड Windows, macOS, और Linux पर काम करता है जब तक .NET runtime उपलब्ध हो।

## Python में Excel वर्कबुक बनाएं

पहला कदम `Workbook` ऑब्जेक्ट को इंस्टैंशिएट करना और डिफ़ॉल्ट वर्कशीट को प्राप्त करना है। यह ऑब्जेक्ट मेमोरी में पूरी Excel फ़ाइल का प्रतिनिधित्व करता है।

```python
from aspose.cells import Workbook, SaveFormat

# Create a new workbook and select the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]
```

*यह क्यों महत्वपूर्ण है*: `Workbook()` एक खाली वर्कबुक बनाता है जिसमें एक ही वर्कशीट होती है। `worksheets[0]` तक पहुँचने से आपको बाद में डेटा, स्टाइल और फॉर्मेटिंग जोड़ने का हैंडल मिलता है।

## Conditional Formatting रेंज जोड़ें

अब हम उस क्षेत्र को परिभाषित करते हैं जिसे conditional rule द्वारा मूल्यांकित किया जाएगा। रेंज `I19:K20` दो पंक्तियों में छह सेल्स को कवर करती है।

```python
# Define the range that will receive the conditional formatting rule
condition_collection = worksheet.conditional_formattings.add("I19:K20")
```

*यह क्यों महत्वपूर्ण है*: किसी विशिष्ट रेंज में conditional formatting कलेक्शन जोड़ने से नियम अलग रहता है, जिससे यह अनावश्यक सेल्स को प्रभावित नहीं करता। यह **add conditional formatting range** की आवश्यकता को पूरा करता है।

## नियम परिभाषित करें: तिथि के आधार पर सेल्स को हाइलाइट करें

अब हम `TIME_PERIOD` प्रकार की एक शर्त बनाते हैं। यह Excel को प्रत्येक सेल के मान की तुलना एक पूर्वनिर्धारित समय विंडो से करने को कहता है।

```python
from aspose.cells import FormatConditionType, TimePeriodType

# Add a TIME_PERIOD condition to the collection
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Set the time period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY
```

*यह क्यों महत्वपूर्ण है*: `TIME_PERIOD` वह एकमात्र बिल्ट‑इन प्रकार है जो सीधे “Yesterday”, “Today”, “Last Week” आदि को सपोर्ट करता है। `condition.time_period` को `YESTERDAY` सेट करने से नियम स्वचालित रूप से प्रत्येक सेल की तिथि को वर्तमान तिथि से एक दिन पहले की तिथि से तुलना करता है।

## शर्त को पूरा करने वाले सेल्स की शैली निर्धारित करें

Conditional formatting को एक विज़ुअल स्टाइल की भी आवश्यकता होती है। यहाँ हम मेल खाने वाले सेल्स को पिंक सॉलिड फ़िल के साथ हाइलाइट करते हैं।

```python
from aspose.pydrawing import Color as DrawingColor
from aspose.cells import BackgroundType

# Apply a pink solid background to cells that satisfy the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID
```

*यह क्यों महत्वपूर्ण है*: स्टाइल ऑब्जेक्ट यह निर्धारित करता है कि Excel उन सेल्स को कैसे रेंडर करेगा जो शर्त को पूरा करते हैं। पिंक सॉलिड फ़िल का उपयोग **highlight cells based on date** की आवश्यकता को पूरा करता है और परिणाम को आसानी से सत्यापित करने योग्य बनाता है।

## मूल्यांकन के लिए नमूना तिथियां भरें

नियम को क्रियान्वित होते देखना है तो हम दो तिथियां डालते हैं—एक जो कल की तिथि पर आती है और एक जो नहीं आती। `number` फ़ॉर्मेट `30` बिल्ट‑इन तिथि फ़ॉर्मेट `mm-dd-yy` के अनुरूप है।

```python
from datetime import datetime

# Cell I19: a date that matches “Yesterday”
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # Example date; adjust as needed
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

# Cell K20: a date outside the “Yesterday” period
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # Example date; adjust as needed
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Optional label for the range
worksheet.cells.get("I20").put_value("Yesterday")
```

*यह क्यों महत्वपूर्ण है*: एक मेल खाने वाली और एक न मिलने वाली तिथि प्रदान करने से आप सत्यापित कर सकते हैं कि conditional formatting सही ढंग से काम कर रहा है। स्क्रिप्ट चलाते समय तिथियों को वर्तमान महीने के अनुसार समायोजित करें, या उन्हें डायनामिक वैल्यूज़ से बदलें।

## वर्कबुक सहेजें

अंत में हम फ़ाइल को डिस्क पर लिखते हैं। `SaveFormat.XLSX` कॉन्स्टेंट सुनिश्चित करता है कि आउटपुट एक आधुनिक Excel फ़ाइल है।

```python
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

*यह क्यों महत्वपूर्ण है*: वर्कबुक को स्थायी रूप से सहेजने से आप इसे Excel, LibreOffice, या किसी भी XLSX सपोर्ट करने वाले व्यूअर में खोल सकते हैं। प्रिंट किया गया पाथ यह पुष्टि करता है कि फ़ाइल कहाँ लिखी गई।

## पूर्ण स्क्रिप्ट

सभी भागों को मिलाकर, पूर्ण, चलाने योग्य स्क्रिप्ट इस प्रकार दिखती है:

```python
# -*- coding: utf-8 -*-
"""
Create an Excel workbook in Python, add a conditional formatting rule,
and highlight yesterday's cells.
"""

from aspose.cells import (
    Workbook, SaveFormat, FormatConditionType,
    BackgroundType, TimePeriodType
)
from aspose.pydrawing import Color as DrawingColor
from datetime import datetime

# Step 1: Create a new workbook and access the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Add a conditional formatting rule for the range I19:K20
condition_collection = worksheet.conditional_formattings.add("I19:K20")
condition_index = condition_collection.add_condition(FormatConditionType.TIME_PERIOD)
condition = condition_collection[condition_index]

# Step 3: Define the visual style for cells that meet the condition
condition.style.background_color = DrawingColor.pink
condition.style.pattern = BackgroundType.SOLID

# Step 4: Set the time‑period to “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Step 5: Populate sample dates for evaluation
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))   # yesterday relative to the example
cell_i19.style.number = 30
cell_i19.set_style(cell_i19.style)

cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))    # outside the period
cell_k20.style.number = 30
cell_k20.set_style(cell_k20.style)

# Step 6: Add a label for the formatted range
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodExample.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### अपेक्षित आउटपुट

जब आप `TimePeriodExample.xlsx` खोलते हैं:

* सेल **I19** में पिंक बैकग्राउंड दिखेगा क्योंकि उसका मान कल से मेल खाता है।
* सेल **K20** डिफ़ॉल्ट बैकग्राउंड रखेगा क्योंकि उसकी तिथि अवधि के बाहर है।
* स्पष्टता के लिए लेबल **“Yesterday”** सेल I20 में स्थित है।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | समायोजन |
|-----------|------------|
| **कल के बजाय आज को हाइलाइट करें** | `condition.time_period = TimePeriodType.TODAY` बदलें। |
| **नियम को बड़े क्षेत्र पर लागू करें** | `add("I19:K20")` में रेंज स्ट्रिंग को `"A1:Z100"` जैसी कुछ में अपडेट करें। |
| **विभिन्न फ़िल रंग उपयोग करें** | `DrawingColor.pink` को किसी अन्य `DrawingColor` (जैसे `DrawingColor.light_green`) से बदलें। |
| **डायनामिक तिथियों के साथ काम करें** | कल के लिए `datetime.now() - timedelta(days=1)` गणना करें और नियम लागू करने से पहले उस मान को सेल्स में लिखें। |

**Pro tip:** जब आप कई उपयोगकर्ताओं के लिए प्रोग्रामेटिकली वर्कबुक जनरेट करते हैं, तो conditional formatting परिभाषा को डेटा इन्सर्शन से अलग रखें। इस तरह आप कई शीट्स में कोड डुप्लिकेशन के बिना वही शैली पुन: उपयोग कर सकते हैं।

## प्रोग्रामेटिकली परिणाम सत्यापित करें (वैकल्पिक)

यदि आप Excel खोले बिना फॉर्मेटिंग की पुष्टि करना चाहते हैं, तो सहेजने के बाद किसी सेल की शैली को inspect कर सकते हैं:



## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Excel Automation: Aspose.Cells for .NET का उपयोग करके वर्कबुक बनाएं और ListBox जोड़ें](/cells/english/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)
- [Aspose.Cells for Java के साथ Excel वर्कबुक बनाएं और लेबल जोड़ें](/cells/english/java/advanced-excel-charts/data-labeling/)
- [Excel Automation: वर्कबुक बनाएं और ListBox जोड़ें Aspose Cells](/cells/german/net/automation-batch-processing/excel-automation-create-workbook-add-listbox-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}