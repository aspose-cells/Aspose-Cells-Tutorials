---
category: general
date: 2026-11-16
description: Python का उपयोग करके Excel में कंडीशनल फ़ॉर्मेटिंग बनाएं। कंडीशनल फ़ॉर्मेटिंग
  रेंज जोड़ना, तिथियों को हाइलाइट करना, और प्रोग्रामेटिकली एक वर्कबुक बनाना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting
- create excel workbook python
- how to highlight dates
- add conditional formatting range
- add conditional formatting python
language: hi
lastmod: 2026-11-16
og_description: Python के साथ Excel में कंडीशनल फ़ॉर्मेटिंग बनाएं। यह ट्यूटोरियल दिखाता
  है कि कैसे कंडीशनल फ़ॉर्मेटिंग रेंज जोड़ें, तिथियों को हाइलाइट करें, और एक वर्कबुक
  जनरेट करें।
og_image_alt: Screenshot of Excel sheet with conditional formatting applied using
  Python
og_title: Python के साथ Excel में कंडीशनल फॉर्मेटिंग बनाएं – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Create conditional formatting in Excel using Python. Learn to add a
    conditional formatting range, highlight dates, and build a workbook programmatically.
  headline: How to create conditional formatting in Excel with Python
  type: TechArticle
tags:
- Excel
- Python
- Aspose.Cells
- Conditional Formatting
title: Python के साथ Excel में कंडीशनल फ़ॉर्मेटिंग कैसे बनाएं
url: /hi/python/formatting/how-to-create-conditional-formatting-in-excel-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python के साथ Excel में conditional formatting कैसे बनाएं

यदि आपको Python में काम करते हुए Excel फ़ाइल में **conditional formatting** बनाना है, तो यह गाइड आपको बिल्कुल बताता है कि इसे कैसे करें। आप **create excel workbook python**‑स्टाइल में वर्कबुक बनाना, फॉर्मेटिंग रेंज निर्धारित करना, और IDE छोड़े बिना तिथियों को हाइलाइट करना सीखेंगे।

Conditional formatting आपको विशिष्ट मानदंडों को पूरा करने वाली कोशिकाओं को दृश्य रूप से चिह्नित करने की सुविधा देता है—डैशबोर्ड, रिपोर्ट, या डेटा‑वैलिडेशन शीट्स के लिए एकदम उपयुक्त। इस ट्यूटोरियल के अंत तक आपके पास एक पूरी तरह कार्यशील वर्कबुक होगी जो “Yesterday” तिथि वाली कोशिकाओं को गुलाबी रंग में और बाकी रेंज को हरा रंग में दिखाएगी।

## आप क्या हासिल करेंगे

* शुरुआत से एक नया वर्कबुक बनाएं।  
* एक विशिष्ट सेल ब्लॉक के लिए conditional‑format संग्रह जोड़ें।  
* **TIME_PERIOD** नियम लागू करें जो तिथियों को हाइलाइट करता है (\"how to highlight dates\" परिदृश्य)।  
* फ़ाइल को XLSX वर्कबुक के रूप में सहेजें, जो आगे की प्रोसेसिंग के लिए तैयार हो।

**Prerequisites**  
* Python 3.8+  
* `aspose-cells` Python package (`pip install aspose-cells`)  
* Python के `datetime` मॉड्यूल की बुनियादी परिचितता  

---

## Python में conditional formatting कैसे बनाएं

पहला कदम वर्कबुक और वर्कशीट सेट करना है जो फॉर्मेटिंग नियमों को होस्ट करेगा।

```python
# Step 1: Import required classes and create a new workbook
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Instantiate a blank workbook and grab the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Optional: auto‑fit column 12 (L) to make the output readable
worksheet.auto_fit_column(12)
```

**Why this matters** – `Workbook` सभी Excel ऑपरेशन्स का एंट्री पॉइंट है। प्रोग्रामेटिक रूप से वर्कबुक बनाना मैन्युअल “File → New” चरण को बदल देता है, जिससे स्वचालित रिपोर्ट पाइपलाइन सक्षम होती है।

---

## conditional‑format संग्रह तैयार करना – conditional formatting रेंज जोड़ें

अब हम उस सेल ब्लॉक को परिभाषित करते हैं जो नियम प्राप्त करेगा। इस उदाहरण में रेंज **I19:K20** है।

```python
# Step 2: Create a conditional‑format collection for the target range
conds = worksheet.conditional_formattings.add("I19:K20")

# Apply a base style (green background) that will show when no rule matches
conds[0].style.background_color = Color.medium_sea_green
conds[0].style.pattern = BackgroundType.SOLID
```

**Explanation** – `conditional_formattings.add` पता स्ट्रिंग से जुड़ी नई संग्रह को रजिस्टर करता है। पहला कंडीशन (`conds[0]`) “default” शैली के रूप में काम करता है; बाद का नियम तब इसे ओवरराइड करेगा जब उसकी शर्तें पूरी होंगी।

---

## TIME_PERIOD कंडीशन जोड़ना – how to highlight dates

अब हम वह वास्तविक लॉजिक जोड़ते हैं जो “Yesterday” तिथियों की पहचान करता है और उन्हें गुलाबी रंग में रंगता है।

```python
# Step 3: Add a TIME_PERIOD condition that highlights cells dated “Yesterday”
idx = conds.add_condition(FormatConditionType.TIME_PERIOD)   # returns the new index
condition = conds[idx]

# Define the visual style for cells that satisfy the condition
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Set the rule to the built‑in YESTERDAY period
condition.time_period = TimePeriodType.YESTERDAY
```

**Why use TIME_PERIOD?** – Aspose.Cells `YESTERDAY`, `TODAY`, और `LAST_WEEK` जैसी बिल्ट‑इन एनेमरेशन प्रदान करता है। ये सेल की तिथि मान को वर्तमान सिस्टम तिथि के साथ तुलना करते हैं, जिससे कस्टम फ़ॉर्मूले की आवश्यकता नहीं रहती।

---

## नमूना डेटा भरना – नियम का प्रदर्शन

फ़ॉर्मेटिंग को क्रिया में देखने के लिए हम एक ऐसी तिथि डालते हैं जो नियम से मेल खाती है और एक ऐसी जो नहीं खाती।

```python
# Step 4: Populate sample dates so the rule can be seen

# Cell I19 gets a date that is “yesterday” relative to 2008‑07‑31
cell_i19 = worksheet.cells.get("I19")
cell_i19.put_value(datetime(2008, 7, 30))  # yesterday for the example
style = cell_i19.get_style()
style.number = 30                         # full date format (e.g., 7/30/2008)
cell_i19.set_style(style)

# Cell K20 gets a later date – it should stay green
cell_k20 = worksheet.cells.get("K20")
cell_k20.put_value(datetime(2008, 8, 3))   # a future date
style = cell_k20.get_style()
style.number = 30
cell_k20.set_style(style)

# Optional label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

**Edge case note** – `TIME_PERIOD` नियम केवल *वास्तविक* तिथियों पर काम करता है। यदि किसी सेल में टेक्स्ट हो (जैसे, “N/A”), तो नियम को नजरअंदाज़ किया जाता है, जिससे अप्रत्याशित रंग परिवर्तन नहीं होते।

---

## वर्कबुक सहेजना – add conditional formatting python

अंत में, वर्कबुक को डिस्क पर लिखें। फ़ाइल को किसी भी स्प्रेडशीट प्रोग्राम में खोलकर रंगों की पुष्टि की जा सकती है।

```python
# Step 5: Save the workbook
output_path = "TimePeriodExample.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

**Expected result**  

| I19 (green → pink) | J19 (green) | K19 (green) |
|--------------------|------------|------------|
| 7/30/2008 (yesterday) | – | – |
| **I20**: “Yesterday” label | – | – |
| I21‑K21 (green)    | – | – |

सेल **I19** का पृष्ठभूमि गुलाबी दिखता है क्योंकि उसकी तिथि “Yesterday” अवधि से मेल खाती है, जबकि **K20** हरा बना रहता है।

---

## सामान्य प्रश्न और व्यावहारिक टिप्स

* **Can I use a custom date range instead of a built‑in period?**  
  हाँ। `condition.time_period` को `condition.formula1 = "TODAY()-1"` से बदलें और `condition.type = FormatConditionType.FORMULA` सेट करें।

* **What if my workbook already contains data?**  
  `worksheet.cells.import_data` का उपयोग करके कंडीशनल फॉर्मेटिंग संग्रह जोड़ने से पहले डेटा को बल्क‑लोड करें।

* **Performance with large sheets?**  
  बहुत सारे कंडीशन जोड़ने से रेंडरिंग धीमी हो सकती है। समान नियम वाले सेल्स को एक ही रेंज (जैसे, “A1:C1000”) में समूहित करें ताकि कंडीशन की संख्या कम रहे।

* **Cross‑platform compatibility?**  
  जनरेट किया गया XLSX फ़ाइल Office Open XML मानक का पालन करता है, इसलिए यह Windows, macOS, और Linux स्प्रेडशीट एप्लिकेशन्स पर काम करता है।

---

## निष्कर्ष

अब आप जानते हैं कि Python का उपयोग करके Excel वर्कबुक में **conditional formatting** कैसे **create** करें। ट्यूटोरियल ने वर्कबुक बनाना, **add conditional formatting range** को परिभाषित करना, **how to highlight dates** नियम लागू करना, और फ़ाइल सहेजना—सभी **add conditional formatting python** दृष्टिकोण से Aspose.Cells द्वारा प्रदान किया गया, कवर किया।

अब आप कर सकते हैं:

* अन्य `TimePeriodType` मानों (जैसे, `TODAY`, `LAST_MONTH`) के साथ नियम सेट का विस्तार करें।  
* समान रेंज पर कई कंडीशन को मिलाकर अधिक समृद्ध दृश्य संकेत बनाएं।  
* इस वर्कफ़्लो को स्वचालित रिपोर्टिंग पाइपलाइन या वेब सेवाओं में एकीकृत करें।

कोडिंग का आनंद लें, और विभिन्न रंगों, रेंजों, और तिथि लॉजिक के साथ प्रयोग करने में संकोच न करें ताकि आपकी रिपोर्टिंग आवश्यकताओं के अनुसार हो सके!

## आगे आप क्या सीखें

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण-दर-चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में निपुण बनने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Create Excel workbook Python date conditional formatting](/cells/english/python/formatting/create-excel-workbook-python-date-conditional-formatting/)
- [How to apply time period conditional formatting in Excel using Python](/cells/english/python/formatting/how-to-apply-time-period-conditional-formatting-in-excel-usi/)
- [Create Excel Workbook Python – Full Guide to Styling & Conditional Formatting](/cells/english/python/formatting/create-excel-workbook-python-full-guide-to-styling-condition/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}