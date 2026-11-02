---
category: general
date: 2026-10-04
description: Aspose.Cells का उपयोग करके Python में Excel वर्कबुक बनाएं। पूर्ण उदाहरण
  में Excel कंडीशनल फ़ॉर्मेटिंग Python, सेल बैकग्राउंड कलर Python, और फ़ॉर्मेट सेल्स
  डेट Python सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create Excel workbook python
- excel conditional formatting python
- cell background color python
- format cells date python
language: hi
lastmod: 2026-10-04
og_description: Aspose.Cells के साथ Python में Excel वर्कबुक बनाएं। यह ट्यूटोरियल
  Excel कंडीशनल फ़ॉर्मेटिंग Python, सेल बैकग्राउंड कलर Python, और फ़ॉर्मेट सेल्स डेट
  Python को चरण‑दर‑चरण दिखाता है।
og_image_alt: Screenshot of an Excel workbook created with Python showing highlighted
  yesterday dates
og_title: Python के साथ Excel वर्कबुक बनाएं – कंडीशनल फॉर्मेटिंग के साथ पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-10-04'
  description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  headline: Create Excel workbook python with conditional formatting and cell background
    color
  type: TechArticle
- description: Create Excel workbook python using Aspose.Cells. Learn excel conditional
    formatting python, cell background color python, and format cells date python
    in a full example.
  name: Create Excel workbook python with conditional formatting and cell background
    color
  steps:
  - name: '**create Excel workbook python** using the Aspose.Cells library.'
    text: '**create Excel workbook python** using the Aspose.Cells library.'
  - name: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
    text: Apply **excel conditional formatting python** that automatically highlights
      dates that fall on “Yesterday”.
  - name: Set the **cell background color python** to pink (or any color you prefer).
    text: Set the **cell background color python** to pink (or any color you prefer).
  - name: '**format cells date python** so the dates appear in the standard Excel
      date style.'
    text: '**format cells date python** so the dates appear in the standard Excel
      date style.'
  type: HowTo
tags:
- Aspose.Cells
- Python
- Excel automation
title: कंडीशनल फ़ॉर्मेटिंग और सेल बैकग्राउंड रंग के साथ पायथन में एक्सेल वर्कबुक बनाएं
url: /hi/python/formulas-and-functions/create-excel-workbook-python-with-conditional-formatting-and/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel workbook python बनाएं शर्तीय स्वरूपण और सेल बैकग्राउंड रंग के साथ

यदि आपको **create Excel workbook python** जल्दी से बनाना है, तो यह गाइड आपको ठीक‑ठीक दिखाता है। आप एक पूर्ण, चलाने योग्य उदाहरण देखेंगे जो **excel conditional formatting python** जोड़ता है, **cell background color python** बदलता है, और “Yesterday” हाइलाइट के लिए **format cells date python** करता है।  

कई रिपोर्टिंग परिदृश्यों में रंगीन सेल का दृश्य संकेत डेटा को तुरंत समझने योग्य बना देता है। यह ट्यूटोरियल आपको कोड की हर पंक्ति के माध्यम से ले जाता है, बताता है कि प्रत्येक चरण क्यों महत्वपूर्ण है, और आपको एक तैयार‑से‑चलाने वाली स्क्रिप्ट देता है जिसे आप अपने प्रोजेक्ट्स में अनुकूलित कर सकते हैं।

## आप क्या हासिल करेंगे

1. **create Excel workbook python** को Aspose.Cells लाइब्रेरी का उपयोग करके बनाना।  
2. **excel conditional formatting python** लागू करना जो स्वचालित रूप से “Yesterday” की तिथियों को हाइलाइट करता है।  
3. **cell background color python** को पिंक (या आपकी पसंद का कोई भी रंग) सेट करना।  
4. **format cells date python** ताकि तिथियां मानक Excel डेट स्टाइल में दिखें।  

Aspose.Cells के साथ कोई पूर्व अनुभव आवश्यक नहीं है—बस एक कार्यशील Python 3 वातावरण और pip एक्सेस होना चाहिए।

## पूर्वापेक्षाएँ

- Python 3.8 या उससे नया स्थापित हो।  
- `aspose-cells` और `aspose-pydrawing` पैकेज `pip install aspose-cells aspose-pydrawing` के माध्यम से स्थापित हों।  
- Python सिंटैक्स और Excel अवधारणाओं (workbooks, worksheets, cells) की बुनियादी समझ।  

> **Pro tip:** यदि आप स्क्रिप्ट को वर्चुअल एनवायरनमेंट में चलाते हैं, तो आप अन्य प्रोजेक्ट्स के साथ संस्करण टकराव से बचते हैं।

## चरण 1: प्रोजेक्ट सेट अप करें और आवश्यक क्लासेस इम्पोर्ट करें

पहला चरण जब आप **create Excel workbook python** करते हैं, वह है Aspose.Cells क्लासेस को इम्पोर्ट करना जो आपको चाहिए। ये क्लासेस आपको workbook निर्माण, शर्तीय स्वरूपण, और स्टाइलिंग तक सीधा पहुंच देती हैं।

```python
# Import Aspose.Cells core classes
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)

# Import Aspose.PyDrawing for color handling
from aspose.pydrawing import Color

# Standard library for date values
from datetime import datetime
```

*Why this matters:* केवल आवश्यक सिम्बॉल्स को इम्पोर्ट करने से नेमस्पेस साफ़ रहता है और स्क्रिप्ट पढ़ने में आसान बनती है। `Workbook` **create Excel workbook python** का एंट्री पॉइंट है, जबकि `FormatConditionType` और `TimePeriodType` **excel conditional formatting python** के लिए आवश्यक हैं।

## चरण 2: नया workbook बनाएं और पहली worksheet प्राप्त करें

अब हम वास्तव में **create Excel workbook python** करते हैं। `Workbook()` कंस्ट्रक्टर आपको एक खाली Excel फ़ाइल देता है जिसमें डिफ़ॉल्ट worksheet होता है।

```python
# Step 2: Initialize a new workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Explanation:* हर Excel फ़ाइल कम से कम एक worksheet से शुरू होती है। डिफ़ॉल्ट रूप से Aspose.Cells इसे “Sheet1” नाम देता है। आप बाद में अधिक शीट्स जोड़ सकते हैं, लेकिन इस डेमो के लिए एक ही शीट पर्याप्त है।

## चरण 3: शर्तीय स्वरूपण के लिए लक्ष्य रेंज निर्धारित करें

शर्तीय स्वरूपण एक आयताकार रेंज पर काम करता है। यहाँ हम रेंज `I19:K20` चुनते हैं, जो हमें तीन कॉलम और दो पंक्तियों का खेल मैदान देता है।

```python
# Define the range that will receive conditional formatting
target_range = "I19:K20"

# Retrieve (or create) the ConditionalFormatting collection for that range
conditional_formatting = worksheet.conditional_formattings.get(target_range)
```

*Why we do this:* `get` मेथड निर्दिष्ट रेंज से जुड़ा एक `ConditionalFormatting` ऑब्जेक्ट लौटाता है। यदि रेंज में अभी तक कोई स्वरूपण नहीं है, तो Aspose.Cells स्वचालित रूप से एक नया कलेक्शन बनाता है।

## चरण 4: TIME_PERIOD शर्त जोड़ें और बैकग्राउंड रंग सेट करें

यह **excel conditional formatting python** का मुख्य भाग है। हम एक `TIME_PERIOD` नियम जोड़ते हैं जो “Yesterday” की तिथियों वाले सेल्स को हाइलाइट करता है।

```python
# Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Access the newly created condition
condition = conditional_formatting[condition_index]

# Configure the condition to target “Yesterday”
condition.time_period = TimePeriodType.YESTERDAY

# Set the cell background color – this is the cell background color python part
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID
```

*Deep dive:*  
- `FormatConditionType.TIME_PERIOD` Excel को बताता है कि तिथियों का मूल्यांकन वर्तमान तिथि के सापेक्ष किया जाए।  
- `TimePeriodType.YESTERDAY` एक बिल्ट‑इन enum है जो हर दिन स्वचालित रूप से अपडेट होता है, इसलिए workbook हमेशा नवीनतम “Yesterday” को हाइलाइट करता रहता है।  
- `background_color` को `Color.pink` और पैटर्न को `SOLID` सेट करके हम **cell background color python** प्रभाव प्राप्त करते हैं, बिना अतिरिक्त VBA कोड के।

## चरण 5: रेंज को नमूना तिथियों से भरें और तिथि स्वरूपण लागू करें

शर्तीय स्वरूपण को क्रियाशील देखने के लिए हमें वास्तविक तिथि मान चाहिए। हमें **format cells date python** भी करना होगा ताकि Excel उन्हें साधारण संख्या की बजाय तिथि के रूप में समझे।

```python
# Helper function to set a cell's date style and value
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    # Excel’s built‑in date format code 30 = "m/d/yy"
    style.number = 30
    cell.set_style(style)
    cell.put_value(date_value)

# Populate I19 with a date that is “yesterday” relative to the sample data
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”

# Populate K20 with another arbitrary date
set_date("K20", datetime(2008, 8, 3))    # Not “yesterday”
```

*Explanation:*  
- `style.number = 30` पंक्ति **format cells date python** चरण है। कोड 30 शॉर्ट डेट फ़ॉर्मेट (`m/d/yy`) के अनुरूप है।  
- एक हेल्पर फ़ंक्शन का उपयोग करने से कोड DRY (Don’t Repeat Yourself) रहता है और बाद में अधिक तिथियां जोड़ना आसान हो जाता है।

## चरण 6: एक वर्णनात्मक लेबल जोड़ें

एक छोटा लेबल किसी भी व्यक्ति को workbook खोलते समय समझाता है कि सेल्स रंगीन क्यों हैं।

```python
# Place a label next to the formatted range
worksheet.cells.get("I20").put_value("Yesterday")
```

## चरण 7: workbook को डिस्क पर सहेजें

अंत में, हम `save` कॉल करके **create Excel workbook python** को डिस्क पर सहेजते हैं। `SaveFormat.XLSX` कॉन्स्टेंट सुनिश्चित करता है कि फ़ाइल आधुनिक Office Open XML फ़ॉर्मेट में हो।

```python
# Define the output path – replace YOUR_DIRECTORY with a real folder
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"

# Save the workbook
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

जब आप `TimePeriodDemo.xlsx` को Excel में खोलेंगे, तो आपको दिखेगा:

- सेल `I19` और `K20` में तिथियां होंगी।  
- वह सेल जो “Yesterday” से मेल खाता है (इस स्थिर उदाहरण में, `I19`) पिंक रंग में हाइलाइट होगा।  
- लेबल “Yesterday” `I20` में दिखाई देगा।  

> **Tip:** यदि आप स्क्रिप्ट को किसी अलग दिन चलाते हैं, तो शर्तीय स्वरूपण अभी भी उस सेल को हाइलाइट करेगा जिसकी तिथि वर्तमान सिस्टम तिथि से ठीक एक दिन पहले है—कोड में कोई बदलाव आवश्यक नहीं।

## पूर्ण स्क्रिप्ट – कॉपी करके चलाने के लिए तैयार

नीचे वह पूर्ण, स्व-निहित प्रोग्राम है जो ऊपर बताए गए सभी चरणों को सम्मिलित करता है। इसे `conditional_format_demo.py` नाम की फ़ाइल में कॉपी करें, `YOUR_DIRECTORY` को समायोजित करें, और `python conditional_format_demo.py` के साथ चलाएँ।

```python
from aspose.cells import (
    Workbook, FormatConditionType, BackgroundType,
    TimePeriodType, SaveFormat
)
from aspose.pydrawing import Color
from datetime import datetime

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Define the cell range that will receive the conditional format
target_range = "I19:K20"
conditional_formatting = worksheet.conditional_formattings.get(target_range)

# Step 3: Add a TIME_PERIOD condition to the range
condition_index = conditional_formatting.add_condition(FormatConditionType.TIME_PERIOD)

# Step 4: Configure the condition to highlight “Yesterday” dates
condition = conditional_formatting[condition_index]
condition.time_period = TimePeriodType.YESTERDAY
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# Helper to set date value and style
def set_date(cell_name: str, date_value: datetime):
    cell = worksheet.cells.get(cell_name)
    style = cell.get_style()
    style.number = 30          # Excel date format code 30 = short date
    cell.set_style(style)
    cell.put_value(date_value)

# Step 5: Populate the range with sample dates (excel conditional formatting python)
set_date("I19", datetime(2008, 7, 30))   # Example “yesterday”
set_date("K20", datetime(2008, 8, 3))    # Another sample date

# Step 6: Add a label describing the condition
worksheet.cells.get("I20").put_value("Yesterday")

# Step 7: Save the workbook
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)
print(f"Workbook saved to {output_path}")
```

### अपेक्षित आउटपुट

स्क्रिप्ट चलाने पर एक पुष्टि पंक्ति प्रिंट होती है:

```
Workbook saved to YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

जनरेट की गई फ़ाइल खोलने पर “Yesterday” नियम से मेल खाने वाले सेल पर पिंक बैकग्राउंड दिखेगा, जिससे यह पुष्टि होगी कि **excel conditional formatting python** और **cell background color python** एक साथ काम कर रहे हैं।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | कोड को कैसे अनुकूलित करें |
|-----------|-----------------------|
| **विभिन्न हाइलाइट रंग** | Change `Color.pink` to any other `Color` constant, e.g., `Color.light_green`. |
| **“Yesterday” के बजाय “Today” को हाइलाइट करें** | Set `condition.time_period = TimePeriodType.TODAY`. |
| **पूरे कॉलम पर स्वरूपण लागू करें** | Use a range like `"A:A"` and adjust the `target_range` variable accordingly. |
| **कस्टम डेट फ़ॉर्मेट उपयोग करें** | Replace `style.number = 30` with `style.custom = "dd-mmm-yyyy"` for a more readable format. |
| **एक ही रेंज पर कई शर्तें** |  |

## अब आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकटता से संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [Excel Workbook Python बनाएं – लैम्ब्डा के साथ पूर्ण गाइड](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)
- [ASP.NET में Aspose.Cells का उपयोग करके Excel Workbook को PDF के रूप में बनाएं और सहेजें](/cells/english/net/workbook-operations/create-save-excel-workbook-pdf-aspnet-aspose-cells/)
- [Aspose.Cells for .NET का उपयोग करके Excel Workbook को ODS के रूप में बनाएं और सहेजें](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}