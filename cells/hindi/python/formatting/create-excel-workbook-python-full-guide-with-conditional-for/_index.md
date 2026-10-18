---
category: general
date: 2026-07-14
description: एक्सेल वर्कबुक बनाने के लिए पायथन कोड लिखें जो सेल की पृष्ठभूमि रंग सेट
  करता है, तिथि सीमा के आधार पर सेल को हाइलाइट करता है, और मिनटों में वर्कबुक को XLSX
  के रूप में सहेजता है।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook python
- set cell background color
- save workbook as xlsx
- highlight cells based on date range
- conditional formatting based on date
language: hi
lastmod: 2026-07-14
og_description: Python से तुरंत Excel वर्कबुक बनाएं। सेल की पृष्ठभूमि रंग सेट करना,
  तिथि सीमा के आधार पर सेल को हाइलाइट करना, और Aspose.Cells के साथ वर्कबुक को XLSX
  के रूप में सहेजना सीखें।
og_image_alt: Screenshot showing an Excel sheet created with Python highlighting yesterday's
  dates
og_title: Python से Excel वर्कबुक बनाएं – चरण‑दर‑चरण कंडीशनल फ़ॉर्मेटिंग
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Create Excel workbook Python code that sets cell background color,
    highlights cells based on date range, and saves workbook as XLSX in minutes.
  headline: Create Excel Workbook Python – Full Guide with Conditional Formatting
  type: TechArticle
tags:
- Python
- Aspose.Cells
- Excel Automation
- Conditional Formatting
title: Python के साथ Excel वर्कबुक बनाएं – कंडीशनल फ़ॉर्मेटिंग के साथ पूर्ण गाइड
url: /hi/python/formatting/create-excel-workbook-python-full-guide-with-conditional-for/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel Workbook Python बनाना – कंडीशनल फॉर्मेटिंग के साथ पूर्ण गाइड

क्या आपने कभी सोचा है कि **create excel workbook python** स्क्रिप्ट्स को बिना Excel मैन्युअली खोले भी परिष्कृत कैसे दिखाया जाए? आप अकेले नहीं हैं। कई डेटा‑ड्रिवन प्रोजेक्ट्स में हमें स्प्रेडशीट्स जेनरेट करने, सेल्स को रंग‑कोड करने, और यहाँ तक कि किसी विशेष रेंज में आने वाली तिथियों को फ़्लैग करने की जरूरत होती है—सभी शुद्ध Python कोड से।

इस ट्यूटोरियल में हम एक पूर्ण, तैयार‑चलाने योग्य उदाहरण के माध्यम से चलेंगे जो **creates an Excel workbook python** Aspose.Cells लाइब्रेरी का उपयोग करके, **sets cell background color**, **conditional formatting based on date** लागू करता है, और अंत में **saves workbook as xlsx**। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जिसे आप किसी भी ऑटोमेशन पाइपलाइन में डाल सकते हैं।

## आप क्या सीखेंगे

- वर्कबुक को इनिशियलाइज़ करने और पहली वर्कशीट को प्राप्त करने का तरीका।  
- एक हेल्पर फ़ंक्शन जो किसी भी सेल रेंज के लिए कंडीशनल‑फ़ॉर्मेटिंग कलेक्शन जोड़ता है।  
- **conditional formatting based on date** का उपयोग करके कल की एंट्रीज़ को हाइलाइट करना।  
- टाइडी लेआउट के लिए कॉलम की चौड़ाई समायोजित करना।  
- **save workbook as xlsx** के साथ परिणाम को स्थायी बनाना।  

कोई बाहरी Excel इंस्टॉलेशन आवश्यक नहीं है—Aspose.Cells सब कुछ मेमोरी में संभालता है।

## आवश्यकताएँ

- Python 3.8+ स्थापित हो।  
- `aspose-cells` पैकेज (`pip install aspose-cells`).  
- Python फ़ंक्शन्स और datetime ऑब्जेक्ट्स की बुनियादी जानकारी।  

यदि आपने पहले कभी Aspose.Cells का उपयोग नहीं किया है, तो इसे एक शक्तिशाली, शुद्ध‑Python API के रूप में सोचें जो Excel के ऑब्जेक्ट मॉडल की नकल करता है। यह सर्वर‑साइड जेनरेशन के लिए उपयुक्त है जहाँ Office सूट उपलब्ध नहीं है।

## चरण 1: वर्कबुक को इनिशियलाइज़ करें (Create Excel Workbook Python)

सबसे पहले: हमें **create excel workbook python** शैली में वर्कबुक बनानी है। यह चरण एक खाली वर्कबुक ऑब्जेक्ट बनाता है और हमें डिफ़ॉल्ट वर्कशीट की ओर इंगित करता है।

```python
# Step 1 – create a fresh workbook and get the first sheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, Color, SaveFormat
from datetime import datetime

workbook = Workbook()                     # <-- creates a new Excel file in memory
worksheet = workbook.worksheets[0]        # the default (first) sheet
```

> **क्यों यह महत्वपूर्ण है:** `Workbook` क्लास हर Excel ऑपरेशन का एंट्री पॉइंट है। इसे प्रोग्रामेटिकली बनाकर हम किसी भी मैनुअल फ़ाइल हैंडलिंग से बचते हैं।

## चरण 2: कंडीशनल‑फ़ॉर्मेटिंग कलेक्शन जोड़ने के लिए हेल्पर (Set Cell Background Color)

कंडीशनल फ़ॉर्मेटिंग एक *कलेक्शन* में रहती है जो रेंज से जुड़ी होती है। चलिए इस बायलरप्लेट को एक छोटे हेल्पर में लपेटते हैं जो पूरे रेंज के लिए **set cell background color** भी सेट करता है।

```python
def add_time_period_condition(cell_range: str, highlight_color: Color):
    """
    Adds a conditional‑formatting collection to `cell_range` and
    applies `highlight_color` as the base fill.
    """
    worksheet.conditional_formattings.add(cell_range)   # attach to the range
    cf = worksheet.conditional_formattings[-1]           # grab the newly added collection
    cf.style.background_color = highlight_color
    cf.style.pattern = BackgroundType.SOLID
    return cf
```

> **प्रो टिप:** हेल्पर का उपयोग करने से आपका मुख्य फ्लो साफ़ रहता है और कई रेंजों के लिए समान लॉजिक को पुन: उपयोग करना आसान हो जाता है।

## चरण 3: डेट पर आधारित कंडीशनल फ़ॉर्मेटिंग लागू करें (Highlight Cells Based on Date Range)

अब हम वास्तव में **highlight cells based on date range** करेंगे। उदाहरण “कल” पर केंद्रित है लेकिन आप `TimePeriodType.YESTERDAY` को `TODAY`, `LAST_WEEK` आदि से बदल सकते हैं।

```python
# Step 3 – create a TIME_PERIOD rule for I19:K20 (yesterday)
cf = add_time_period_condition("I19:K20", Color.medium_sea_green)

condition_index = cf.add_condition(FormatConditionType.TIME_PERIOD)
condition = cf[condition_index]

# Define the visual style for the matching cells
condition.style.background_color = Color.pink
condition.style.pattern = BackgroundType.SOLID

# The actual rule: any cell whose date is yesterday gets the pink fill
condition.time_period = TimePeriodType.YESTERDAY
```

> **क्या हो रहा है?**  
> 1. हम पहले पूरे रेंज को एक न्यूट्रल ग्रीन बैकग्राउंड देते हैं।  
> 2. फिर हम एक `TIME_PERIOD` कंडीशन जोड़ते हैं जो फ़िल को पिंक से **केवल** तब ओवरराइट करता है जब सेल की तिथि कल के बराबर हो।  
> 3. `TimePeriodType` एनीम डेट कैलकुलेशन को एब्स्ट्रैक्ट करता है, इसलिए आपको कस्टम लॉजिक लिखने की जरूरत नहीं है।

## चरण 4: सैंपल डेट्स भरें (ताकि नियम का मूल्यांकन हो सके)

नियम को क्रिया में देखने के लिए हम शीट में दो तिथियाँ डालेंगे। एक “कल” विंडो के भीतर आती है, दूसरी नहीं।

```python
# Populate I19 with a date that is yesterday (relative to the hard‑coded date)
date_cell = worksheet.cells.get("I19")
date_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008
date_style = date_cell.get_style()
date_style.number = 30                     # Excel’s built‑in date format
date_cell.set_style(date_style)

# Populate K20 with a date that is NOT yesterday
date_cell = worksheet.cells.get("K20")
date_cell.put_value(datetime(2008, 8, 3))    # 03‑Aug‑2008
date_style = date_cell.get_style()
date_style.number = 30
date_cell.set_style(date_style)

# Add a label for clarity
worksheet.cells.get("I20").put_value("Yesterday")
```

> **एज केस नोट:** यदि आपका वर्कबुक विभिन्न लोकेल्स में खोला जाएगा, तो एकसमान डिस्प्ले सुनिश्चित करने के लिए `date_style.custom = "dd‑mm‑yyyy"` का उपयोग करने पर विचार करें।

## चरण 5: लेआउट को टाइडी बनाएं (Auto‑Fit Columns)

एक भीड़भाड़ वाला स्प्रेडशीट अनप्रोफेशनल दिखता है। चलिए **adjust column width for a tidy output** करते हैं।

```python
# Auto‑fit column L (index 12) to show the full content without truncation
worksheet.auto_fit_column(12)
```

> **ऑटो‑फ़िट क्यों?** यह सुनिश्चित करता है कि कोई भी लंबा लेबल या तिथि पूरी तरह दिखे, जो विशेष रूप से तब महत्वपूर्ण है जब आप फ़ाइल को गैर‑तकनीकी स्टेकहोल्डर्स के साथ साझा करते हैं।

## चरण 6: वर्कबुक को सेव करें (Save Workbook As XLSX)

अंत में, हम **save workbook as xlsx** को अपनी पसंद के स्थान पर सेव करते हैं। `SaveFormat.XLSX` कॉन्स्टेंट Aspose.Cells को आधुनिक OpenXML फॉर्मेट लिखने के लिए बताता है।

```python
output_path = "YOUR_DIRECTORY/TimePeriodDemo.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to: {output_path}")
```

> **आपको जो परिणाम दिखना चाहिए:**  
> - सेल I19 और K20 में तिथियाँ हैं।  
> - I19 (कल) पिंक से हाइलाइट है, जबकि K20 हरा रहता है।  
> - कॉलम L स्वचालित रूप से “Yesterday” लेबल फिट करने के लिए विस्तारित हो जाता है।  

यदि आप `TimePeriodDemo.xlsx` को Excel में खोलते हैं, तो कंडीशनल फ़ॉर्मेटिंग पहले से ही लागू होगी—कोई अतिरिक्त कदम आवश्यक नहीं।

![हाइलाइटेड कल की तिथि दिखाती Excel शीट](https://example.com/images/excel-demo.png "हाइलाइटेड सेल्स के साथ जेनरेटेड Excel फ़ाइल का स्क्रीनशॉट")

*ऊपर की छवि अंतिम वर्कबुक को दर्शाती है; देखें कि कल की तिथि वाले सेल पर पिंक हाइलाइट है।*

## पुनरावलोकन: हमने क्या हासिल किया

- **Created an Excel workbook python** को Aspose.Cells का उपयोग करके शून्य से बनाया।  
- **Set cell background color** पूरे रेंज के लिए सेट किया ताकि शीट को विज़ुअल क्यू मिले।  
- **conditional formatting based on date** लागू किया ताकि कल की एंट्रीज़ को स्वचालित रूप से फ़्लैग किया जा सके।  
- **Saved workbook as xlsx**, वितरण या आगे की प्रोसेसिंग के लिए तैयार।  

इन सबको 60 लाइनों से कम Python कोड में किया गया, और कोड किसी भी प्लेटफ़ॉर्म पर काम करता है जो Aspose.Cells रनटाइम को सपोर्ट करता है।

## अगले कदम और संबंधित विषय

यदि आपको यह उपयोगी लगा, तो आप भी देख सकते हैं:

- **set cell background color** पूरे रो के लिए स्टेटस वैल्यूज़ (जैसे “Completed”, “Pending”) के आधार पर।  
- **highlight cells based on date range** का उपयोग करके रोलिंग विंडो बनाएं (पिछले 7 दिन, वर्तमान महीना)।  
- `SaveFormat.CSV` या `SaveFormat.PDF` के साथ **CSV** या **PDF** जैसे अन्य फ़ॉर्मेट्स में एक्सपोर्ट करना।  
- डेटा को विज़ुअलाइज़ करने के लिए प्रोग्रामेटिकली **charts** जोड़ना।  

डेट लॉजिक को बदलने, रंग पैलेट बदलने, या रेंज को पूरे कॉलम तक विस्तारित करने में संकोच न करें। पैटर्न वही रहता है: वर्कबुक बनाएं, कंडीशनल‑फ़ॉर्मेटिंग कलेक्शन अटैच करें, नियम परिभाषित करें, और सेव करें।

किसी विशेष उपयोग‑केस के बारे में प्रश्न हैं? नीचे टिप्पणी छोड़ें, और कोडिंग का आनंद लें!

## अब आपको क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ को एक्सप्लोर करने में मदद करेंगे।

- [Aspose.Cells .NET के साथ Excel ऑटोमेशन: वर्कबुक बनाएं और एक्सटर्नल लिंक सेट करें](/cells/english/net/automation-batch-processing/excel-automation-aspose-cells-net/)
- [Excel वर्कबुक बनाएं और सेव करें Aspose Cells Java](/cells/hongkong/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Excel वर्कबुक बनाएं और सेव करें Aspose Cells Dotnet](/cells/hongkong/net/workbook-operations/create-save-excel-workbook-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}