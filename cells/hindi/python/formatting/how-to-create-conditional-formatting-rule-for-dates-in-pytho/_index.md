---
category: general
date: 2026-08-24
description: Aspose.Cells का उपयोग करके Python में शर्तीय स्वरूपण नियम बनाएं जो तिथियों
  को हाइलाइट करे, साथ ही कॉलम को ऑटो‑फ़िट और बैकग्राउंड रंग स्वरूपण लागू करे।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create conditional formatting rule
- auto fit column
- conditional formatting by date
- background color conditional format
- date based conditional format
language: hi
lastmod: 2026-08-24
og_description: Aspose.Cells के साथ Python में कंडीशनल फ़ॉर्मेटिंग नियम बनाएं। जानें
  कैसे कुछ ही कोड लाइनों में तिथियों को हाइलाइट करें, बैकग्राउंड रंग सेट करें, और
  कॉलम को ऑटो‑फ़िट करें।
og_image_alt: Screenshot of an Excel sheet where yesterday's date cells are highlighted
  in pink
og_title: Python में तिथियों के लिए कंडीशनल फ़ॉर्मेटिंग नियम बनाएं – चरण‑दर‑चरण गाइड
schemas:
- author: Aspose
  dateModified: '2026-08-24'
  description: Create conditional formatting rule in Python using Aspose.Cells to
    highlight dates, with auto‑fit column and background color formatting.
  headline: How to create conditional formatting rule for dates in Python
  type: TechArticle
tags:
- Aspose.Cells
- Python
- Excel automation
- Conditional formatting
title: Python में तिथियों के लिए शर्तीय स्वरूपण नियम कैसे बनाएं
url: /hi/python/formatting/how-to-create-conditional-formatting-rule-for-dates-in-pytho/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में तिथियों के लिए conditional formatting rule कैसे बनाएं

यदि आपको तिथियों पर प्रतिक्रिया देने वाला **create conditional formatting rule** बनाना है, तो यह गाइड आपको Aspose.Cells for Python के साथ इसे ठीक‑ठीक कैसे करना है दिखाता है। चाहे आप रिपोर्टिंग डैशबोर्ड बना रहे हों या स्वचालित स्प्रेडशीट, आप देखेंगे कि कैसे कल की तिथियों को हाइलाइट करें, कस्टम बैकग्राउंड रंग लागू करें, और **auto fit column** की चौड़ाई को समायोजित करें ताकि परिणाम परिष्कृत दिखे।

इस ट्यूटोरियल में हम **conditional formatting by date** को कवर करेंगे, एक **background color conditional format** का प्रदर्शन करेंगे, और अंत में वर्कबुक को XLSX फ़ाइल के रूप में सहेजेंगे। अंत तक आपके पास एक पुन: उपयोग योग्य हेल्पर होगा जिसे आप किसी भी **date based conditional format** के लिए अनुकूलित कर सकते हैं।

## आप क्या सीखेंगे

* Aspose.Cells का उपयोग करके एक workbook और worksheet सेट अप करें।
* एक हेल्पर फ़ंक्शन लिखें जो किसी भी सेल रेंज में **date based conditional format** जोड़ता है।
* सेल्स को नमूना तिथियों से भरें ताकि नियम का मूल्यांकन हो सके।
* सामग्री को पढ़ने योग्य बनाने के लिए **auto fit column** लागू करें।
* वर्कबुक को सहेजें और हाइलाइट किए गए सेल्स की पुष्टि करें।

एकमात्र पूर्वापेक्षा यह है कि आपके पास `aspose-cells` पैकेज स्थापित वाला कार्यशील Python वातावरण हो।

## पूर्वापेक्षाएँ

| आवश्यकता | विवरण |
|----------|-------|
| Python | 3.8+ |
| Aspose.Cells for Python via Java | `pip install aspose-cells` |
| Excel अवधारणाओं का मूल ज्ञान | worksheets, cells, formatting |
| वैकल्पिक: IDE (VS Code, PyCharm, आदि) | कोई भी एडिटर जो Python स्क्रिप्ट चला सके |

## चरण 1: एक workbook बनाएं और पहला worksheet प्राप्त करें

पहला कदम **create conditional formatting rule**‑तैयार ऑब्जेक्ट्स बनाना है: एक `Workbook` और उसका डिफ़ॉल्ट `Worksheet`। ये ऑब्जेक्ट्स सभी बाद के ऑपरेशनों के लिए प्रवेश बिंदु हैं।

```python
# Step 1 – initialize workbook and worksheet
from aspose.cells import Workbook, FormatConditionType, BackgroundType, TimePeriodType, SaveFormat
from aspose.pydrawing import Color
from datetime import datetime

# Create a new, empty workbook
workbook = Workbook()

# Grab the first worksheet (index 0)
worksheet = workbook.worksheets[0]
```

*Why this matters:* `Workbook` पूरे Excel फ़ाइल को रखता है, जबकि `Worksheet` वह जगह है जहाँ आप सेल्स, स्टाइल्स, और **conditional formatting by date** लागू करते हैं। इन ऑब्जेक्ट्स के बिना बाकी कोड के पास कार्य करने की कोई जगह नहीं रहती।

## चरण 2: TIME_PERIOD conditional format जोड़ने के लिए एक हेल्पर बनाएं

प्रत्येक रेंज के लिए वही बायलर‑प्लेट दोहराने के बजाय, हम लॉजिक को एक हेल्पर फ़ंक्शन में संलग्न करते हैं। यह फ़ंक्शन एक **background color conditional format** संलग्न करता है जो `TimePeriodType` (जैसे Yesterday, Today, LastWeek) के आधार पर सेल्स को रंगता है।

```python
def add_time_period_condition(cell_range: str, bg_color: Color, period: TimePeriodType):
    """
    Attach a TIME_PERIOD conditional format to `cell_range`.
    The rule highlights cells that fall within `period` using `bg_color`.

    Args:
        cell_range: A1‑style range string, e.g., "I19:K20".
        bg_color:   Desired background color for matching cells.
        period:     Aspose.Cells TimePeriodType enum value.
    Returns:
        The FormatConditionCollection for further customization if needed.
    """
    # 1️⃣ Attach a new ConditionalFormatting block to the specified range
    worksheet.conditional_formattings.add(cell_range)

    # 2️⃣ Grab the collection of conditions for that block
    conditions = worksheet.conditional_formattings[-1].format_conditions

    # 3️⃣ (Optional) Set a default background for the whole range
    conditions.back_color = bg_color

    # 4️⃣ Add a TIME_PERIOD condition and configure its appearance
    idx = conditions.add_condition(FormatConditionType.TIME_PERIOD)
    condition = conditions[idx]

    # Apply the visual style – pink background in this example
    condition.style.background_color = Color.pink
    condition.style.pattern = BackgroundType.SOLID

    # Define which period triggers the formatting
    condition.time_period = period

    return conditions
```

*Why we use a helper:* यह **date based conditional format** लॉजिक को अलग करता है, जिससे कोड पढ़ने, परीक्षण करने, और कई शीट्स या प्रोजेक्ट्स में पुन: उपयोग करने में आसान हो जाता है।

## चरण 3: एक विशिष्ट रेंज पर conditional formatting rule लागू करें

अब हम हेल्पर का उपयोग करके उन सेल्स को हाइलाइट करते हैं जिनमें “Yesterday” है। यह हमारे **create conditional formatting rule** ऑपरेशन का मूल है।

```python
# Step 3 – highlight cells I19:K20 that contain “Yesterday”
add_time_period_condition(
    cell_range="I19:K20",
    bg_color=Color.medium_sea_green,   # optional default background for the whole range
    period=TimePeriodType.YESTERDAY   # the date‑based trigger
)
```

जब वर्कबुक खोला जाता है, तो `I19:K20` में कोई भी सेल जिसकी तिथि कल की तिथि के बराबर है, गुलाबी भराव (pink fill) के साथ दिखेगा (हेल्पर में सेट किया गया स्टाइल)। `bg_color` आर्ग्यूमेंट दिखाता है कि आप इच्छानुसार conditional color के पीछे डिफ़ॉल्ट बैकग्राउंड कैसे लेयर कर सकते हैं।

## चरण 4: रेंज को नमूना तिथियों से भरें

एक conditional rule तभी दिखाई देता है जब worksheet में वह डेटा हो जो शर्त को पूरा करता हो। हम दो तिथियाँ डालेंगे: एक जो “Yesterday” से मेल खाती है और दूसरी जो अवधि के बाहर है।

```python
# Step 4 – insert sample dates for demonstration

# Cell I19 will match the YESTERDAY period
yesterday_cell = worksheet.cells.get("I19")
yesterday_cell.put_value(datetime(2008, 7, 30))   # 30‑Jul‑2008 is “yesterday” relative to 31‑Jul‑2008
yesterday_cell.get_style().number = 30          # 30 = built‑in date format
yesterday_cell.set_style(yesterday_cell.get_style())

# Cell K20 will NOT match the period (it’s a later date)
outside_cell = worksheet.cells.get("K20")
outside_cell.put_value(datetime(2008, 8, 3))     # 03‑Aug‑2008 is outside “Yesterday”
outside_cell.get_style().number = 30
outside_cell.set_style(outside_cell.get_style())

# Optional label for clarity – not part of the rule
worksheet.cells.get("I20").put_value("Yesterday")
```

*Why this matters:* `datetime` ऑब्जेक्ट्स का उपयोग करके हम सुनिश्चित करते हैं कि Excel इन मानों को वास्तविक तिथियों के रूप में मानता है, जो **conditional formatting by date** के सही काम करने के लिए आवश्यक है। संख्यात्मक फ़ॉर्मेट (`30`) यह सुनिश्चित करता है कि सेल्स पहचाने जाने योग्य तिथियों के रूप में दिखें।

## चरण 5: कॉलम को Auto‑fit करें और वर्कबुक सहेजें

डेटा और फ़ॉर्मेटिंग स्थापित होने के बाद, अंतिम चरण **auto fit column** की चौड़ाई को समायोजित करना है ताकि तिथियाँ पूरी तरह दिखाई दें। फिर हम फ़ाइल को डिस्क पर लिखते हैं।

```python
# Step 5 – adjust column width and save the file

# Auto‑fit column 12 (the column that contains our sample data)
worksheet.auto_fit_column(12)

# Save the workbook as an XLSX file
output_path = "YOUR_DIRECTORY/TimePeriodDemo.out.xlsx"
workbook.save(output_path, SaveFormat.XLSX)

print(f"Workbook saved to {output_path}")
```

`auto_fit_column` कॉल कॉलम 12 (जो Excel में कॉलम **L** के बराबर है) में सबसे लंबी सामग्री की जाँच करता है और उसके अनुसार चौड़ाई बढ़ाता है। यह छोटा कदम कटे हुए तिथियों को रोकता है और **background color conditional format** को स्पष्ट रूप से दिखाई देता है।

### अपेक्षित परिणाम

`TimePeriodDemo.out.xlsx` खोलने पर:

| I19 (तारीख) | I20 (लेबल) | K20 (तारीख) |
|-------------|------------|-------------|
| 30‑Jul‑2008 (हाइलाइटेड पिंक) | कल | 03‑Aug‑2008 (कोई हाइलाइट नहीं) |

* कल की तिथि वाला सेल गुलाबी बैकग्राउंड दिखाता है क्योंकि **create conditional formatting rule** ने `YESTERDAY` अवधि से मेल खाया।
* बाकी सभी सेल्स डिफ़ॉल्ट बैकग्राउंड रखते हैं (या आप द्वारा प्रदान किया गया वैकल्पिक `medium_sea_green`)।
* कॉलम L स्वतः विस्तारित हो जाता है, जिससे तिथियाँ पूरी तरह पढ़ी जा सकती हैं।

## सामान्य विविधताएँ और किनारे के मामले

| स्थिति | कोड को कैसे अनुकूलित करें |
|--------|---------------------------|
| **Highlight “Today” instead of “Yesterday”** | Replace `TimePeriodType.YESTERDAY` with `TimePeriodType.TODAY`. |
| **Use a different background color** | Change `condition.style.background_color = Color.pink` to any other `Color` (e.g., `Color.light_sky_blue`). |
| **Apply the rule to a non‑contiguous range** | Call `add_time_period_condition` multiple times with different `cell_range` strings (e.g., `"A1:A10", "C1:C10"`). |
| **Work with a pre‑existing workbook** | Load the file with `Workbook("myfile.xlsx")` instead of creating a new one. |
| **Multiple date‑based conditions on the same range** | After the first `add_time_period_condition` call, add another condition with `conditions.add_condition(FormatConditionType.TIME_PERIOD)` and set a different `time_period`. |

## निष्कर्ष

अब आप जानते हैं कि कैसे **create conditional formatting rule** बनाएं जो तिथियों पर प्रतिक्रिया देता है, एक **background color conditional format** लागू करें, और Aspose.Cells for Python का उपयोग करके **auto fit column** की चौड़ाई समायोजित करें। हेल्पर फ़ंक्शन लॉजिक को सारांशित करता है, जिससे आप किसी भी **conditional formatting by date** परिदृश्य—चाहे वह “Yesterday”, “LastWeek”, या कोई कस्टम रेंज हो—के लिए वही पैटर्न पुन: उपयोग कर सकते हैं।

अगले चरण में आप खोज सकते हैं:

* डेट रूल्स के साथ **icon sets** या **data bars** जोड़ना।
* डेटाबेस से तिथियों को खींचने वाले डायनामिक रिपोर्ट बनाना।
* एक ही शीट पर कई **date based conditional format** नियमों को मिलाना।

विभिन्न रंगों, अवधियों, और रेंजों के साथ प्रयोग करने में संकोच न करें ताकि आपके प्रोजेक्ट की आवश्यकताओं के अनुकूल हो सके। कोडिंग का आनंद लें!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन निकट संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करती हैं।

- [Aspose.Cells .NET का उपयोग करके Excel में Conditional Formatting में महारत: एक व्यापक गाइड](/cells/english/net/formatting/mastering-aspose-cells-net-conditional-formatting/)
- [Aspose.Cells for .NET का उपयोग करके Conditional Formatting रंगों को निकालने का तरीका](/cells/english/net/formatting/extract-conditional-formatting-colors-aspose-cells-net/)
- [Aspose.Cells for .NET और C# के साथ Excel में कस्टम फ़ॉन्ट्स के साथ Conditional Formatting में महारत](/cells/english/net/formatting/conditional-formatting-custom-fonts-aspose-csharp/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}