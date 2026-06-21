---
category: general
date: 2026-06-21
description: Python का उपयोग करके Excel में गुणा तालिका बनाएं। लैंब्डा का उपयोग कैसे
  करें, makearray का उपयोग कैसे करें, Excel एरे को प्रदर्शित करना और Python में Excel
  मान पढ़ना सीखें, एक चरण‑दर‑चरण ट्यूटोरियल में।
draft: false
keywords:
- create multiplication table
- how to use lambda
- how to use makearray
- display excel array
- read excel values python
language: hi
og_description: Python का उपयोग करके Excel में गुणा तालिका बनाएं। यह ट्यूटोरियल दिखाता
  है कि लैम्ब्डा, मेकऐरे का उपयोग कैसे करें, Excel ऐरे को कैसे प्रदर्शित करें और Python
  में Excel मानों को कुशलतापूर्वक कैसे पढ़ें।
og_title: Python के साथ Excel में गुणन तालिका बनाएं – पूर्ण गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Create multiplication table in Excel using Python. Learn how to use
    lambda, how to use makearray, display excel array and read excel values python
    in a step‑by‑step tutorial.
  headline: Create multiplication table in Excel with Python – Full Guide
  type: TechArticle
tags:
- python
- excel
- openpyxl
title: Python के साथ Excel में गुणन तालिका बनाएं – पूर्ण गाइड
url: /hi/python/import-and-export/create-multiplication-table-in-excel-with-python-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel में Python के साथ गुणन तालिका बनाएं – पूर्ण गाइड

क्या आपने कभी सोचा है कि Excel में **create multiplication table** को बिना प्रत्येक सेल को मैन्युअल रूप से टाइप किए कैसे बनाया जाए? आप अकेले नहीं हैं। कई रिपोर्टिंग परिदृश्यों में आपको उत्पादों की तेज़ 5×5 (या बड़ी) ग्रिड चाहिए होती है, और इसे हाथ से बनाना समय की बर्बादी है।  

इस ट्यूटोरियल में हम एक साफ़, Python‑ड्रिवेन तरीका दिखाएंगे जिससे आप वह तालिका जनरेट कर सकते हैं, उसे `MAKEARRAY` फ़ॉर्मूला के साथ एम्बेड कर सकते हैं, और फिर परिणाम को अपने स्क्रिप्ट में वापस खींच सकते हैं। इस दौरान हम **how to use lambda** का उत्तर देंगे, **how to use makearray** दिखाएंगे, और **display excel array** के साथ-साथ **read excel values python** को भी प्रदर्शित करेंगे—सब एक ही सुसंगत उदाहरण में।

अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जो किसी भी वर्कबुक के साथ काम करता है, और आप समझेंगे कि यह तरीका क्यों तेज़ और भविष्य‑सुरक्षित दोनों है।

## आपको क्या चाहिए

- Python 3.8+ (नवीनतम स्थिर रिलीज़ ठीक है)
- `openpyxl` लाइब्रेरी (या कोई भी Excel‑सजग लाइब्रेरी जो फ़ॉर्मूले सपोर्ट करती हो)
- Python में lambda अभिव्यक्तियों की बुनियादी समझ
- कोई विशेष Excel ऐड‑इन नहीं; मूल `MAKEARRAY` फ़ंक्शन (Excel 365 में उपलब्ध) भारी काम करता है

यदि आपके पास इनमें से कोई भी नहीं है, तो बस `pip install openpyxl` चलाएँ और आप तैयार हैं।

## गुणन तालिका बनाना – अवलोकन

मुख्य विचार सरल है: हम एक नई वर्कबुक बनाते हैं, एक `MAKEARRAY` फ़ॉर्मूला लिखते हैं जो 5 × 5 गुणन मैट्रिक्स बनाता है, Excel को इसे गणना करने के लिए मजबूर करते हैं, और अंत में परिणामी मानों को Python में वापस पढ़ते हैं।

```python
from openpyxl import Workbook

# Step 1: Create a new workbook and get the first worksheet
workbook = Workbook()
worksheet = workbook.worksheets[0]

# Step 2: Insert a MAKEARRAY formula that builds a 5×5 multiplication table
# The formula uses a LAMBDA that returns r*c for each row (r) and column (c)
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"

# Step 3: Calculate all formulas so the array is materialized in the sheet
workbook.calculate_formula()

# Step 4: Read and display the top‑left 5×5 block of values
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

स्क्रिप्ट चलाने पर प्रिंट होता है:

```
[1, 2, 3, 4, 5]
[2, 4, 6, 8, 10]
[3, 6, 9, 12, 15]
[4, 8, 12, 16, 20]
[5, 10, 15, 20, 25]
```

यह Excel में पूरी तरह कार्यशील **create multiplication table** है, जो पूरी तरह Python से जनरेट किया गया है।

### Python लूप की बजाय `MAKEARRAY` क्यों उपयोग करें?

- **Performance**: Excel मूल रूप से गणना संभालता है, जो बड़े मैट्रिक्स के लिए तेज़ है।
- **Live updating**: यदि आप बाद में फ़ॉर्मूला में आयाम बदलते हैं, तो शीट स्वतः‑पुनः गणना करती है।
- **Readability**: फ़ॉर्मूला सीधे इरादा (“make an array”) व्यक्त करता है, जिससे आपका Python कोड साफ़ रहता है।

## Excel फ़ॉर्मूले के लिए Python में lambda कैसे उपयोग करें

`MAKEARRAY` कॉल का `LAMBDA` भाग एक Excel‑साइड अनाम फ़ंक्शन है, Python lambda नहीं। फिर भी, अवधारणा समान है: आप एक छोटा, इनलाइन लॉजिक परिभाषित करते हैं जो `r` (पंक्ति सूचक) और `c` (स्तंभ सूचक) लेता है और `r*c` लौटाता है।  

यदि आप Excel दुनिया में **how to use lambda** में नए हैं, तो इसे एक मिनी‑फ़ंक्शन के रूप में सोचें जो केवल फ़ॉर्मूला के भीतर रहता है। कहीं अलग फ़ंक्शन घोषित करने की आवश्यकता नहीं है। Python में हम बस स्ट्रिंग को एम्बेड करते हैं:

```python
worksheet["A1"] = "=MAKEARRAY(5,5, LAMBDA(r,c, r*c))"
```

यह पंक्ति Excel को बताती है: *“5‑by‑5 ब्लॉक में प्रत्येक सेल के लिए, पंक्ति × स्तंभ की गणना करें।”*  

क्योंकि lambda को Excel द्वारा मूल्यांकित किया जाता है, आपको यहाँ Python के अपने lambda सिंटैक्स की चिंता नहीं करनी है—सिर्फ Excel सिंटैक्स की।

## एरे जनरेट करने के लिए makearray कैसे उपयोग करें

`MAKEARRAY` Excel फ़ंक्शन लाइब्रेरी में एक अपेक्षाकृत नया जोड़ है (Microsoft 365 में 2022 से उपलब्ध)। यह `INDEX` + `ROW`/`COLUMN` जैसी पुरानी ट्रिक्स को बदलता है। इसका सिग्नेचर है:

```
MAKEARRAY(rows, columns, lambda)
```

- **rows** – आप जितनी पंक्तियाँ चाहते हैं।
- **columns** – आप जितने कॉलम चाहते हैं।
- **lambda** – एक Excel LAMBDA जो `(row, column)` प्राप्त करता है और एक मान लौटाता है।

हमारे उदाहरण में हमने क्लासिक गुणन तालिका के लिए `5,5` पास किया, लेकिन आप आसानी से इन संख्याओं को बदल सकते हैं:

```python
worksheet["A1"] = "=MAKEARRAY(10,10, LAMBDA(r,c, r*c))"
```

यह आपको बिना किसी Python लूप को छुए 10 × 10 तालिका देगा। यह **how to use makearray** को किसी भी प्रकार के निर्धारक ग्रिड के लिए दर्शाता है, चाहे वह लुकअप टेबल हो, हीटमैप, या वित्तीय शेड्यूल।

## Excel एरे दिखाना – डेटा को Python में वापस खींचना

एक बार Excel ने फ़ॉर्मूला की गणना कर ली, तो परिणामी मान शीट में किसी भी मैन्युअल रूप से दर्ज किए गए सेल की तरह मौजूद होते हैं। **display excel array** करने के लिए, हम रेंज पर इटररेट करते हैं और प्रत्येक पंक्ति प्रिंट करते हैं:

```python
for row_index in range(1, 6):
    row_values = [worksheet.cell(row=row_index, column=col_index).value
                  for col_index in range(1, 6)]
    print(row_values)
```

कुछ टिप्स:

- `worksheet.cell(row, column).value` का उपयोग करें बजाय डिक्शनरी‑स्टाइल इंडेक्सिंग के, यदि आपको बड़े रेंज को संभालना है; यह थोड़ा तेज़ है।
- यदि आप एक सुंदर तालिका चाहते हैं, तो आउटपुट को फ़ॉर्मेट करने के लिए `tabulate` या `pandas.DataFrame` पर विचार करें।

नीचे परिणामस्वरूप शीट का एक स्क्रीनशॉट है (छवि का alt टेक्स्ट SEO के लिए मुख्य कीवर्ड शामिल करता है):

![Python का उपयोग करके Excel में create multiplication table दिखाते हुए स्क्रीनशॉट](/images/multiplication-table-excel.png)

## Python से Excel मान पढ़ना – आगे की प्रोसेसिंग के लिए मैट्रिक्स निकालना

अक्सर **display excel array** के बाद अगला कदम उन संख्याओं को डेटा‑विश्लेषण पाइपलाइन में फीड करना होता है। यहीं पर **read excel values python** चमकता है। वही लूप जो हमने प्रिंट करने के लिए इस्तेमाल किया था, उसे सूची‑की‑सूची, NumPy एरे, या Pandas DataFrame बनाने के लिए पुनः उपयोग किया जा सकता है:

```python
import pandas as pd

# Build a list of rows
data = []
for row_index in range(1, 6):
    row = [worksheet.cell(row=row_index, column=col_index).value
           for col_index in range(1, 6)]
    data.append(row)

# Convert to DataFrame for easy manipulation
df = pd.DataFrame(data, columns=[f"Col{c}" for c in range(1, 6)],
                  index=[f"Row{r}" for r in range(1, 6)])

print(df)
```

आउटपुट:

```
      Col1  Col2  Col3  Col4  Col5
Row1     1     2     3     4     5
Row2     2     4     6     8    10
Row3     3     6     9    12    15
Row4     4     8    12    16    20
Row5     5    10    15    20    25
```

अब आपके पास एक पूरी तरह टाइप किया गया DataFrame है जिसे आप प्लॉट कर सकते हैं, CSV में एक्सपोर्ट कर सकते हैं, या मशीन‑लर्निंग मॉडल में फीड कर सकते हैं। यह वर्कफ़्लो के **read excel values python** भाग को पूरा करता है।

## किनारे के मामलों और व्यावहारिक टिप्स

- **Formula recalculation**: यदि आप प्रारंभिक `calculate_formula()` कॉल के बाद वर्कबुक को संशोधित करते हैं, तो आपको इसे फिर से चलाना होगा; अन्यथा कैश्ड एरे पुराना रहेगा।
- **Non‑365 Excel**: पुराने Excel संस्करण `MAKEARRAY` को सपोर्ट नहीं करते। ऐसे में Python‑जनित तालिका पर वापस जाएँ और प्रत्येक सेल को अलग‑अलग लिखें।
- **Large tables**: ~100 × 100 से बड़े मैट्रिक्स के लिए, डेटा को स्ट्रीम करने पर विचार करें ताकि पूरी शीट को मेमोरी में लोड करने से बचा जा सके।
- **Error handling**: गणना और पढ़ने के चरणों को `try/except` ब्लॉक्स में रैप करें ताकि `InvalidFileException` या `FormulaError` को पकड़ा जा सके।

## निष्कर्ष

हमने अभी आपको दिखाया है कि Python का उपयोग करके Excel में **create multiplication table** कैसे बनाते हैं, **how to use lambda** और **how to use makearray** की शक्ति को उपयोग में लाते हुए। आपने देखा कि **display excel array** कैसे किया जाता है, उन मानों को **read excel values python** से वापस पढ़ा जाता है, और परिणाम को डाउनस्ट्रीम विश्लेषण के लिए Pandas DataFrame में कैसे बदला जाता है।  

और आगे बढ़ना चाहते हैं? गुणन लॉजिक को कुछ अधिक जटिल से बदलें—शायद एक दूरी मैट्रिक्स, एक प्रायिकता तालिका, या एक डायनेमिक प्राइसिंग ग्रिड। वही पैटर्न लागू होता है: एक पंक्ति `MAKEARRAY` की, एक तेज़ `calculate_formula()`, और डेटा निकालने के लिए कुछ Python लूप।  

यदि आपको यह गाइड उपयोगी लगा, तो इसे GitHub पर स्टार दें, टीम के साथ साझा करें, या अपने स्वयं के उपयोग‑केस के साथ एक टिप्पणी छोड़ें। कोडिंग का आनंद लें, और एक ही फ़ॉर्मूला से Excel तालिकाएँ जनरेट करने की सरलता का आनंद उठाएँ!

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट-संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API फीचर्स में निपुण होने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [How to Create and Configure Excel Workbooks with Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/getting-started/create-configure-excel-workbook-aspose-cells-net/)
- [Aspose.Cells .NET Tutorial: How to Create and Modify Excel Workbooks Easily](/cells/english/net/workbook-operations/aspose-cells-net-create-modify-excel-workbooks/)
- [How to Create and Style Named Ranges in Excel Using Aspose.Cells .NET | Step‑By‑Step Guide](/cells/english/net/range-management/create-style-named-ranges-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}