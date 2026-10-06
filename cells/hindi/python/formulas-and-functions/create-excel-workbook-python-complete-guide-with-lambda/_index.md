---
category: general
date: 2026-06-08
description: एक्सेल वर्कबुक पायथन उदाहरण बनाएं जो दिखाता है कि एक्सेल में लैम्ब्डा
  कैसे उपयोग करें, BYROW के साथ पंक्तियों का योग करें, और कुछ चरणों में गणनाओं को
  स्वचालित करें।
draft: false
keywords:
- create excel workbook python
- how to use lambda
- how to sum rows
- use lambda excel
language: hi
og_description: Python से Excel वर्कबुक बनाएं और Excel में λ (लैम्ब्डा) का उपयोग करके
  BYROW फ़ॉर्मूले के साथ पंक्तियों को कुशलतापूर्वक जोड़ना सीखें।
og_title: Python से Excel वर्कबुक बनाएं – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Create Excel workbook Python example that shows how to use lambda in
    Excel, sum rows with BYROW, and automate calculations in a few steps.
  headline: Create Excel Workbook Python – Complete Guide with Lambda
  type: TechArticle
tags:
- python
- excel
- automation
title: Python के साथ Excel वर्कबुक बनाना – लैम्ब्डा के साथ पूर्ण मार्गदर्शिका
url: /hi/python/formulas-and-functions/create-excel-workbook-python-complete-guide-with-lambda/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Excel Workbook Python – लैम्ब्डा के साथ पूर्ण गाइड

क्या आपने कभी सोचा है कि कैसे **create Excel workbook Python** स्क्रिप्ट्स बनाएं जो उबाऊ नंबर‑क्रंचिंग को स्वचालित करें? आप अकेले नहीं हैं—बहुत से डेवलपर्स को तब समस्या आती है जब उन्हें शीट बनानी होती है, फ़ॉर्मूला डालना होता है, और परिणाम को कोड में वापस लाना होता है।  

इस ट्यूटोरियल में हम **how to use lambda** को Excel में दिखाएंगे, आधुनिक `BYROW` फ़ंक्शन के साथ **how to sum rows** समझाएंगे, और आपको एक साफ़, अंत‑से‑अंत उदाहरण देंगे जिसे आप आज ही कॉपी‑पेस्ट करके चला सकते हैं।

## आप क्या सीखेंगे

- Python से बिना Excel मैन्युअली खोले एक नया वर्कबुक सेट अप करें।  
- 3 × 3 संख्याओं की मैट्रिक्स के साथ एक रेंज भरें।  
- `BYROW` फ़ॉर्मूला डालें जो **use lambda excel** सिंटैक्स का उपयोग करके प्रत्येक पंक्ति का योग करता है।  
- शीट को पुनः गणना करें ताकि फ़ॉर्मूला मूल्यांकन हो, फिर परिणाम को Python में वापस पढ़ें।  

इस गाइड के अंत तक आपके पास एक स्व-निहित स्क्रिप्ट होगी जिसे आप इनवॉइस, स्कोर‑कार्ड, या किसी भी स्थिति में जहाँ आपको तुरंत **sum rows** करने की आवश्यकता हो, अनुकूलित कर सकते हैं।

### आवश्यकताएँ

- Python 3.8+ स्थापित हो।  
- `openpyxl` लाइब्रेरी (या `xlwings` यदि आप COM‑आधारित दृष्टिकोण पसंद करते हैं)। हम `openpyxl` का उपयोग करेंगे क्योंकि यह शुद्ध‑Python है और सभी प्लेटफ़ॉर्म पर काम करता है।  
- Microsoft Excel का नवीनतम संस्करण (365 या 2021) जो `BYROW` फ़ंक्शन और Lambda फ़ॉर्मूले को सपोर्ट करता हो।  

Install the library with:

```bash
pip install openpyxl
```

> **Pro tip:** यदि आप Windows पर अनुमति संबंधी समस्याओं का सामना करते हैं, तो `python -m pip install --user openpyxl` का उपयोग करें।

## Create Excel Workbook Python – वर्कबुक को इनिशियलाइज़ करें

पहली चीज़ जो हमें चाहिए वह एक बिल्कुल नया वर्कबुक ऑब्जेक्ट है जो पूरी तरह मेमोरी में रहता है। `openpyxl` के साथ यह एक लाइन में किया जा सकता है:

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and grab the first worksheet
wb = Workbook()
ws = wb.active   # .active is the first sheet by default
```

हम `wb.active` का उपयोग `Worksheets[0]` के इंडेक्सिंग के बजाय क्यों करते हैं? `openpyxl` सक्रिय शीट को सीधे एक्सपोज़ करता है, जो स्पष्ट है और अतिरिक्त लिस्ट लुकअप से बचाता है। यदि आपको कई शीट्स के साथ काम करना पड़े, तो आप हमेशा `wb.create_sheet(title="MySheet")` से उन्हें जोड़ सकते हैं।

## डेटा के साथ वर्कशीट भरें – एक सरल 3×3 मैट्रिक्स

अब हम शीट को एक छोटे मैट्रिक्स से भरते हैं। यह क्लासिक “प्रत्येक पंक्ति का योग” उदाहरण को दर्शाता है और कोड को संक्षिप्त रखता है।

```python
# Step 2: Define a 3×3 matrix of numbers
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

# Import the matrix into the worksheet starting at cell A1
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, value in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=value)
```

आप सोच सकते हैं कि हम `ws.append()` या `ws.values` के बजाय मैन्युअली लूप क्यों करते हैं। स्पष्ट लूप हमें शुरुआती सेल पर पूर्ण नियंत्रण देते हैं और बाद में ऑफ़सेट समायोजित करना आसान बनाते हैं—जब आप हेडर पंक्ति या कॉलम को खाली छोड़ना चाहते हैं तो यह उपयोगी है।

## Excel फ़ॉर्मूले में Lambda का उपयोग कैसे करें

Excel की **use lambda excel** सुविधा आपको सीधे सेल में अनाम फ़ंक्शन लिखने देती है। इसे Python के `lambda` की तरह समझें, लेकिन स्प्रेडशीट इंजन के भीतर रहता है। सिंटैक्स है:

```
=LAMBDA(parameter1, parameter2, …, calculation)
```

`BYROW` के साथ मिलाकर, आप उस lambda को रेंज की प्रत्येक पंक्ति पर लागू कर सकते हैं, जिससे परिणामों का एक कॉलम बनता है। यह हमारे **how to sum rows** ट्रिक का मूल है।

```python
# Step 3: Insert a BYROW formula that sums each row using a Lambda
ws["D1"] = "=BYROW(A1:C3, LAMBDA(r, SUM(r)))"
```

What’s happening under the hood?

- `A1:C3` स्रोत रेंज है (हमारा मैट्रिक्स)।  
- `LAMBDA(r, SUM(r))` एक अस्थायी फ़ंक्शन परिभाषित करता है जो एक पंक्ति (`r`) लेता है और उसका योग लौटाता है।  
- `BYROW` उस lambda को **प्रत्येक पंक्ति** के लिए चलाता है और परिणाम को कॉलम D में, `D1` से शुरू करके, स्पिल करता है।  

क्योंकि `BYROW` एक *डायनामिक एरे* फ़ंक्शन है, Excel स्वचालित रूप से `D1:D3` को तीन योगों से भर देता है।

> **Note:** `BYROW` और Lambda फ़ॉर्मूले केवल Excel 365/2021 और बाद के संस्करणों में उपलब्ध हैं। यदि आप पुराने संस्करण पर हैं, तो आपको पारम्परिक `SUM` फ़ॉर्मूले या VBA पर वापस जाना होगा।

## BYROW और Lambda के साथ Rows का योग कैसे करें

अब फ़ॉर्मूला शीट में मौजूद है, हमें Excel को इसे मूल्यांकन करने के लिए कहना होगा। `openpyxl` स्वयं फ़ॉर्मूले की गणना नहीं करता; यह केवल पढ़ता/लिखता है। गणना को ट्रिगर करने के लिए हम या तो:

1. वर्कबुक को सहेजें और Excel में खोलें (मैन्युअल)।  
2. `xlwings` COM इंजन का उपयोग करके पुनः गणना को मजबूर करें (Excel स्थापित होना आवश्यक)।  

शुद्ध‑Python समाधान के लिए हम केवल गणना चरण के लिए `xlwings` का उपयोग करेंगे—और कुछ नहीं।

```python
import xlwings as xw

# Step 4: Recalculate the workbook so the BYROW formula is evaluated
# Save the workbook to a temporary file first
temp_path = "temp_workbook.xlsx"
wb.save(temp_path)

# Open the file with xlwings, force a calculation, then close
app = xw.App(visible=False)
book = app.books.open(temp_path)
book.api.CalculateFull()          # Full recalculation
book.save()
book.close()
app.quit()
```

`wb.calculate()` क्यों नहीं बुलाते? `openpyxl` में मूल इंजन नहीं है, इसलिए हम Excel पर ही भरोसा करते हैं `xlwings` के माध्यम से। छोटे शीट्स के लिए ओवरहेड न्यूनतम है और हमें वही परिणाम मिलता है जो Excel दिखाता है।

## पुनः गणना और परिणाम प्राप्त करें – योग को Python में वापस लाएँ

अंत में, हम कॉलम D से स्पिल किए गए परिणाम पढ़ते हैं। `openpyxl` इसे सीधा बनाता है:

```python
# Step 5: Load the recalculated workbook and grab the results
wb = Workbook()  # re‑open the saved file
wb = xw.Book(temp_path).api  # alternative: use xlwings again to read values

# Using xlwings to fetch the range values as a Python list
results = xw.Range('D1:D3').value
print(results)   # Expected output: [6, 15, 24]
```

यदि आप `openpyxl` के भीतर रहना पसंद करते हैं, तो आप Excel पुनः गणना के बाद सेल्स को पढ़ सकते हैं:

```python
from openpyxl import load_workbook

wb = load_workbook(temp_path, data_only=True)  # data_only reads calculated values
ws = wb.active
results = [ws[f"D{row}"].value for row in range(1, 4)]
print(results)   # -> [6, 15, 24]
```

दोनों विधियां आपको वही सूची `[6, 15, 24]` देती हैं, जिससे पुष्टि होती है कि **how to sum rows** `BYROW` + Lambda के साथ जैसा बताया गया है, वैसा ही काम करता है।

## किनारे के केस और सामान्य समस्याएँ

| स्थिति | ध्यान देने योग्य बात | समाधान |
|-----------|-------------------|-----|
| Excel संस्करण 365 से पुराना | `BYROW` और `LAMBDA` `#NAME?` दिखाते हैं | क्लासिक `=SUM(A1:C1)` को मैन्युअली नीचे कॉपी करें, या Excel अपग्रेड करें। |
| बड़े मैट्रिक्स (10 k+ पंक्तियाँ) | पुनः गणना धीमी हो सकती है | `book.api.CalculateFullRebuild()` को केवल एक बार कॉल करें, या वर्कबुक को विभाजित करें। |
| बिना Excel के हेडलेस सर्वर पर चलाना | `xlwings` Excel लॉन्च नहीं कर सकता | गणनाओं के लिए `pandas` + `numpy` जैसी शुद्ध‑Python लाइब्रेरी पर स्विच करें, फिर परिणाम लिखें। |
| लोकेल समस्याएँ (कॉमा बनाम सेमीकोलन) | फ़ॉर्मूला अस्वीकृत हो सकता है | उन लोकेल्स के लिए `ws["D1"].value = "=BYROW(A1:C3; LAMBDA(r; SUM(r)))"` उपयोग करें। |

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```python
# ------------------------------------------------------------
# create_excel_workbook_python – full script
# ------------------------------------------------------------
import os
from openpyxl import Workbook, load_workbook
import xlwings as xw

# 1️⃣ Initialize workbook
wb = Workbook()
ws = wb.active

# 2️⃣ Populate with a 3×3 matrix
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
for r_idx, row in enumerate(matrix, start=1):
    for c_idx, val in enumerate(row, start=1):
        ws.cell(row=r_idx, column=c_idx, value=val)

# 3️⃣ Insert BYROW + Lambda formula


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Aspose.Cells Java के साथ Excel वर्कबुक बनाएं - पूर्ण गाइड](/cells/english/java/automation-batch-processing/excel-automation-aspose-cells-java-guide/)
- [Aspose.Cells के साथ Excel वर्कबुक बनाएं और रिपोर्ट्स को ऑटोमेट करें](/cells/english/java/automation-batch-processing/aspose-cells-java-two-three-color-scales/)
- [Aspose.Cells for .NET का उपयोग करके Excel वर्कबुक को ODS के रूप में बनाना और सहेजना](/cells/english/net/workbook-operations/create-save-excel-ods-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}