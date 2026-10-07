---
category: general
date: 2026-10-07
description: Python में Excel वर्कबुक बनाएं, सेल की पृष्ठभूमि रंग सेट करें, कॉलम को
  ऑटो‑फ़िट करें, और संक्षिप्त कोड उदाहरण के साथ Excel में तिथियों को भरें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- auto fit excel columns
- populate dates in excel
- how to create excel
language: hi
lastmod: 2026-10-07
og_description: Python में Excel वर्कबुक बनाएं, फिर सेल की पृष्ठभूमि रंग सेट करें,
  कॉलम को ऑटो‑फ़िट करें, और Excel में तिथियां भरें। TimePeriodDemo.xlsx फ़ाइल बनाने
  के लिए इस चरण‑दर‑चरण गाइड का पालन करें।
og_image_alt: Screenshot of a Python‑generated Excel workbook with pink highlighted
  cells
og_title: Python में Excel वर्कबुक बनाएं – पृष्ठभूमि सेट करें और ऑटो‑फ़िट करें
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  headline: Create Excel workbook in Python and set cell background
  type: TechArticle
- description: Create Excel workbook in Python, set cell background color, auto‑fit
    columns, and populate dates in Excel with a concise code example.
  name: Create Excel workbook in Python and set cell background
  steps:
  - name: Import required namespaces and define a helper function
    text: '```python # Step 1: Import Aspose.Cells classes and supporting modules
      from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType,
      SaveFormat from aspose.pydrawing import Color from datetime import datetime
      import os ```'
  - name: Create the workbook and get the first worksheet
    text: '```python def create_workbook(): # Step 2: Instantiate a new workbook (empty
      Excel file) book = Workbook() # Aspose.Cells creates a default worksheet; we
      retrieve it for further work sheet = book.worksheets[0] return book, sheet ```'
  - name: Set cell background color with a conditional format
    text: '```python def add_yesterday_rule(sheet): # Define a conditional format
      for the range I19:K20 (Yesterday) conds = sheet.get_range("I19:K20").format_conditions
      idx = conds.add_condition(FormatConditionType.TIME_PERIOD) cond = conds[idx]'
  - name: Populate dates in Excel
    text: '```python def populate_sample_dates(sheet): # Insert a date that falls
      on yesterday relative to the demo data cell = sheet.cells.get("I19") cell.put_value(datetime(2008,
      7, 30)) # sample date cell.style.number = 30 # Excel’s date format ID cell.set_style(cell.style)'
  - name: Auto‑fit Excel columns for better visibility
    text: '```python def auto_fit_columns(sheet): # Auto‑fit column L (index 12) so
      the content is fully visible sheet.auto_fit_column(12) # <-- auto fit excel
      columns ```'
  - name: Save the workbook
    text: '```python def save_workbook(book, filename="TimePeriodDemo.xlsx"): out_path
      = os.path.join("YOUR_DIRECTORY", filename) os.makedirs(os.path.dirname(out_path),
      exist_ok=True) book.save(out_path, SaveFormat.XLSX) print(f"Workbook saved to:
      {out_path}") ```'
  - name: Full script – putting it all together
    text: '```python def main(): # Create workbook and obtain the first worksheet
      book, sheet = create_workbook()'
  type: HowTo
tags:
- Excel
- Python
- Aspose.Cells
title: Python में Excel वर्कबुक बनाएं और सेल पृष्ठभूमि सेट करें
url: /hi/python/import-and-export/create-excel-workbook-in-python-and-set-cell-background/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में Excel वर्कबुक बनाएं और सेल बैकग्राउंड सेट करें

Python में Excel वर्कबुक बनाएं और कुछ ही लाइनों के कोड से कंडीशनल फ़ॉर्मेटिंग लागू करें। यह ट्यूटोरियल आपको प्रोग्रामेटिकली **excel कैसे बनाएं** फ़ाइलें, सेल बैकग्राउंड रंग सेट करने, Excel कॉलम को ऑटो‑फ़िट करने, और Aspose.Cells लाइब्रेरी का उपयोग करके Excel में तिथियों को पॉप्युलेट करने का तरीका दिखाता है।

आप सीखेंगे कि कैसे:
* एक वर्कबुक इनिशियलाइज़ करें और पहला वर्कशीट प्राप्त करें।  
* एक कंडीशनल फ़ॉर्मेट परिभाषित करें जो “Yesterday” तिथियों को हाइलाइट करे।  
* विशिष्ट सेल्स में सैंपल तिथियां डालें।  
* कॉलम्स को ऑटो‑फ़िट करें ताकि डेटा स्पष्ट रूप से दिखे।  
* वर्कबुक को चुने हुए फ़ोल्डर में सेव करें।  

एकमात्र पूर्वापेक्षा यह है कि आपके पास एक कार्यशील Python 3 वातावरण हो, जिसमें `aspose-cells` और `aspose-pydrawing` पैकेज स्थापित हों:

```bash
pip install aspose-cells aspose-pydrawing
```

---

## Python में Excel वर्कबुक बनाएं – चरण दर चरण

निम्नलिखित सेक्शन प्रक्रिया को प्रबंधनीय चरणों में विभाजित करते हैं। प्रत्येक चरण में आवश्यक कोड, यह समझाने के लिए **क्यों** यह महत्वपूर्ण है, और सामान्य गलतियों से बचने के लिए एक टिप शामिल है।

### चरण 1: आवश्यक नेमस्पेस इम्पोर्ट करें और एक हेल्पर फ़ंक्शन परिभाषित करें

```python
# Step 1: Import Aspose.Cells classes and supporting modules
from aspose.cells import Workbook, FormatConditionType, TimePeriodType, BackgroundType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime
import os
```

*यह क्यों महत्वपूर्ण है*: सही क्लासेज़ को इम्पोर्ट करने से आपको वर्कबुक निर्माण, कंडीशनल फ़ॉर्मेटिंग, और कलर हैंडलिंग तक पहुंच मिलती है।  
**Pro tip**: इम्पोर्ट्स को फ़ाइल के शीर्ष पर रखें; इससे स्क्रिप्ट पढ़ने में आसान होती है और सर्कुलर‑इम्पोर्ट त्रुटियों से बचाव होता है।

### चरण 2: वर्कबुक बनाएं और पहला वर्कशीट प्राप्त करें

```python
def create_workbook():
    # Step 2: Instantiate a new workbook (empty Excel file)
    book = Workbook()
    # Aspose.Cells creates a default worksheet; we retrieve it for further work
    sheet = book.worksheets[0]
    return book, sheet
```

`Workbook()` कंस्ट्रक्टर मेमोरी में एक खाली Excel वर्कबुक बनाता है।  
**Why**: एक नई वर्कबुक से शुरू करने से पिछले रन से बची हुई फ़ॉर्मेटिंग नहीं रहती।

### चरण 3: कंडीशनल फ़ॉर्मेट के साथ सेल बैकग्राउंड रंग सेट करें

```python
def add_yesterday_rule(sheet):
    # Define a conditional format for the range I19:K20 (Yesterday)
    conds = sheet.get_range("I19:K20").format_conditions
    idx = conds.add_condition(FormatConditionType.TIME_PERIOD)
    cond = conds[idx]

    # Apply visual style – this is where we set the cell background color
    cond.style.background_color = Color.pink          # <-- set cell background color
    cond.style.pattern = BackgroundType.SOLID
    cond.time_period = TimePeriodType.YESTERDAY
```

*Why*: **time period** कंडीशन का उपयोग करने से वह सेल जो कल की तिथि रखता है, स्वचालित रूप से हाइलाइट हो जाता है, जिससे मैन्युअल डेट चेक हट जाता है।  
**Tip**: `Color.pink` सिर्फ एक उदाहरण है; आप कोई भी `Color` ऑब्जेक्ट (`Color.yellow`, `Color.light_green`, आदि) उपयोग कर सकते हैं।

### चरण 4: Excel में तिथियां पॉप्युलेट करें

```python
def populate_sample_dates(sheet):
    # Insert a date that falls on yesterday relative to the demo data
    cell = sheet.cells.get("I19")
    cell.put_value(datetime(2008, 7, 30))   # sample date
    cell.style.number = 30                 # Excel’s date format ID
    cell.set_style(cell.style)

    # Insert another date outside the “Yesterday” range
    cell = sheet.cells.get("K20")
    cell.put_value(datetime(2008, 8, 3))
    cell.style.number = 30
    cell.set_style(cell.style)

    # Add a label for the rule
    sheet.cells.get("I20").put_value("Yesterday")
```

यहां हम **Excel में तिथियां पॉप्युलेट** करते हैं सेल `I19` और `K20` में। पहली तिथि कंडीशनल फ़ॉर्मेटिंग को ट्रिगर करेगी, जबकि दूसरी नहीं करेगी।  
**Why this matters**: मिलते और न मिलते मानों दोनों को दिखाने से आप यह सत्यापित कर सकते हैं कि नियम अपेक्षित रूप से काम कर रहा है।

### चरण 5: बेहतर दृश्यता के लिए Excel कॉलम्स को ऑटो‑फ़िट करें

```python
def auto_fit_columns(sheet):
    # Auto‑fit column L (index 12) so the content is fully visible
    sheet.auto_fit_column(12)   # <-- auto fit excel columns
```

`auto_fit_column` कॉलम की चौड़ाई को सबसे लंबे सेल वैल्यू के आधार पर समायोजित करता है।  
**Tip**: सभी डेटा लिखने के बाद इसे कॉल करें; अन्यथा चौड़ाई अधूरे कंटेंट के आधार पर गणना हो सकती है।

### चरण 6: वर्कबुक को सेव करें

```python
def save_workbook(book, filename="TimePeriodDemo.xlsx"):
    out_path = os.path.join("YOUR_DIRECTORY", filename)
    os.makedirs(os.path.dirname(out_path), exist_ok=True)
    book.save(out_path, SaveFormat.XLSX)
    print(f"Workbook saved to: {out_path}")
```

फ़ाइल को सेव करने से इन‑मेमोरी वर्कबुक डिस्क पर आधुनिक XLSX फ़ॉर्मेट में लिखी जाती है।  

### पूर्ण स्क्रिप्ट – सब कुछ एक साथ

```python
def main():
    # Create workbook and obtain the first worksheet
    book, sheet = create_workbook()

    # Apply conditional formatting (set cell background color)
    add_yesterday_rule(sheet)

    # Populate the demo dates (populate dates in excel)
    populate_sample_dates(sheet)

    # Auto‑fit the relevant column (auto fit excel columns)
    auto_fit_columns(sheet)

    # Persist the file
    save_workbook(book)

if __name__ == "__main__":
    main()
```

**अपेक्षित आउटपुट**

```
Workbook saved to: YOUR_DIRECTORY/TimePeriodDemo.xlsx
```

जनरेट की गई फ़ाइल को Excel में खोलें – सेल `I19:K20` “Yesterday” तिथि के लिए पिंक बैकग्राउंड दिखाएगा, और कॉलम L इतना चौड़ा होगा कि लेबल बिना कटे दिखे।

---

## यह तरीका सबसे अच्छा क्यों काम करता है

* **Single‑pass workflow** – सभी ऑपरेशन्स एक ही `Workbook` इंस्टेंस पर होते हैं, जिससे अनावश्यक I/O से बचा जा सकता है।  
* **Conditional formatting** – `FormatConditionType.TIME_PERIOD` का उपयोग करने से Excel डेट लॉजिक संभालता है, जो कस्टम Python डेट चेक लिखने से अधिक भरोसेमंद है।  
* **Explicit styling** – `background_color` और `pattern` सेट करने से विभिन्न Excel संस्करणों में विज़ुअल परिणाम सुनिश्चित होता है।  
* **Auto‑fit डेटा के बाद**  

## अब आप आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Excel वर्कबुक Python बनाएं – पूर्ण गाइड](/cells/english/python/import-and-export/create-excel-workbook-python-full-guide/)
- [Excel वर्कबुक Python बनाएं – पूर्ण चरण‑दर‑चरण गाइड](/cells/english/python/import-and-export/create-excel-workbook-python-complete-step-by-step-guide/)
- [Excel वर्कबुक Python बनाएं – लैम्ब्डा के साथ पूर्ण गाइड](/cells/english/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}