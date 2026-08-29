---
category: general
date: 2026-06-30
description: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें और सीखें कि Excel वर्कबुक कैसे
  लोड करें, सेल वैल्यू अपडेट करें, स्पेल‑चेकिंग सक्षम करें, और कस्टम कमांड रजिस्टर
  करें।
draft: false
keywords:
- add custom context menu
- update cell value
- enable spell checking
- load excel workbook
- register custom command
language: hi
og_description: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें, जबकि Excel वर्कबुक लोड करना
  सीखें, सेल वैल्यू अपडेट करें, स्पेल‑चेकिंग सक्षम करें, और कस्टम कमांड रजिस्टर करें।
og_title: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – चरण‑दर‑चरण पाइथन ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu in GridJs and learn how to load Excel workbook,
    update cell value, enable spell checking, and register custom command.
  headline: Add Custom Context Menu to GridJs – Complete Python Guide
  type: TechArticle
tags:
- GridJs
- Python
- Excel Automation
title: GridJs में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – पूर्ण पायथन गाइड
url: /hi/python/integration-and-interoperability/add-custom-context-menu-to-gridjs-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ग्रिडजेएस में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – पूर्ण पायथन गाइड

क्या आपने कभी सोचा है कि Excel वर्कबुक द्वारा समर्थित GridJs तालिका में **कस्टम कॉन्टेक्स्ट मेनू** आइटम कैसे जोड़ें? आप अकेले नहीं हैं। कई डेटा‑भारी एप्लिकेशनों में आपको राइट‑क्लिक मेनू की जरूरत होती है जिससे उपयोगकर्ता पंक्तियों को फ़्लैग कर सकें, आइटम को Reviewed के रूप में चिह्नित कर सकें, या सर्वर‑साइड कार्रवाई शुरू कर सकें—बिना ग्रिड छोड़े।  

इस ट्यूटोरियल में हम Excel वर्कबुक लोड करने, कस्टम कॉन्टेक्स्ट‑मेन्‍यू एंट्री जोड़ने, सेल वैल्यू अपडेट करने, स्पेल‑चेकिंग सक्षम करने, और एक कस्टम कमांड रजिस्टर करने की प्रक्रिया को देखेंगे जो बदलावों को फ़ाइल में वापस सहेजता है। अंत तक आपके पास एक पूरी तरह कार्यात्मक GridJs इंस्टेंस होगा जो उपयोगकर्ताओं को नेटिव महसूस होगा और स्रोत स्प्रेडशीट में सीधे लिखेगा।

## Prerequisites

- Python 3.9+ (कोड टाइप हिंट्स का उपयोग करता है लेकिन किसी भी हालिया संस्करण पर चलता है)  
- `cells` लाइब्रेरी (या कोई भी Excel‑हैंडलिंग रैपर जो `Workbook` और `Worksheet` ऑब्जेक्ट प्रदान करता है)  
- `gridjs` पायथन बाइंडिंग (ऑब्जेक्ट मॉडल जावास्क्रिप्ट API को प्रतिबिंबित करता है)  
- लैम्ब्डा और JSON संरचनाओं की बुनियादी समझ  

यदि आपके पास ये हैं, तो चलिए शुरू करते हैं।

## Step 1: Load Excel Workbook and Select a Worksheet

पहला काम **excel workbook लोड** करना है ताकि GridJs के पास दिखाने के लिए डेटा हो। `cells.Workbook` क्लास फ़ाइल‑IO को एब्स्ट्रैक्ट करती है और आपको पंक्तियों, कॉलमों और व्यक्तिगत सेल्स तक सीधे पहुँच देती है।

```python
# Step 1: Load the workbook and select the first worksheet
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]          # Grab the first sheet – change index if needed
```

> **Why this matters:** वर्कबुक को पहले से लोड करने का मतलब है कि ग्रिड मांग पर डेटा खींच सकता है, और बाद में किए गए किसी भी एडिट (जैसे **update cell value**) उसी फ़ाइल में सहेजे जाएंगे।

## Step 2: Create GridJs Instance and Bind It to the Worksheet

अब हम एक `gridjs.GridJs` ऑब्जेक्ट बनाते हैं और उसे बताते हैं कि कौन सा वर्कशीट रेंडर करना है। इसे इस तरह समझें कि GridJs को एक लाइव डेटा स्रोत दिया गया है जिसे वह पेज रेंडर करने या लेज़ी‑लोडेड चंक की आवश्यकता पर क्वेरी कर सकता है।

```python
# Step 2: Create a GridJs instance and bind it to the worksheet
grid = gridjs.GridJs()
grid.set_worksheet(ws)
```

> **Pro tip:** यदि आप कई शीट्स के साथ काम करते हैं, तो बाद में बस `grid.set_worksheet(other_ws)` कॉल करें—ग्रिड को फिर से बनाने की ज़रूरत नहीं।

## Step 3: Enable Spell Checking (and Other Nice‑to‑Haves)

अधिकांश बिज़नेस ऐप्स उपयोगकर्ताओं को फ्री‑फ़ॉर्म नोट्स टाइप करने देते हैं। **spell checking** सक्षम करने से टाइपो कम होते हैं और डेटा क्वालिटी सुधरती है। GridJs इसके लिए एक सरल फ़्लैग प्रदान करता है।

```python
# Step 3: Turn on spell checking (and keep other helpers enabled)
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True          # optional but handy
grid.settings.formula_explanation.enabled = True   # if you support formulas
```

> **Why enable spell checking?** यह क्लाइंट‑साइड चलता है, अतिरिक्त सर्वर कॉल्स के बिना तुरंत फीडबैक देता है—बड़े‑पैमाने के शीट्स के लिए परफ़ेक्ट।

## Step 4: Add a Custom Context‑Menu Item

यह ट्यूटोरियल का मुख्य भाग है: **add custom context menu** एंट्रीज़। हम “Mark as Reviewed” विकल्प बनाएँगे जो क्लिक होने पर अगले चरण में परिभाषित सर्वर‑साइड कमांड चलाएगा।

```python
# Step 4: Add a custom context‑menu item
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",   # What the user sees
    "action": "markReviewed"      # Identifier used in the command registration
})
```

> **Image illustration**  
> ![कस्टम कॉन्टेक्स्ट मेनू स्क्रीनशॉट जिसमें राइट‑क्लिक विकल्प दिखाए गए हैं](/images/add-custom-context-menu.png "कस्टम कॉन्टेक्स्ट मेनू उदाहरण")

ऊपर का alt टेक्स्ट मुख्य कीवर्ड शामिल करता है, जिससे SEO आवश्यकताएँ पूरी होती हैं।

## Step 5: Register Custom Command to Update the Cell Value

जब उपयोगकर्ता “Mark as Reviewed” चुनता है, तो हमें **register custom command** की आवश्यकता होती है जो अंतर्निहित Excel सेल को अपडेट करे और फ़ाइल को सहेजे। `grid.register_custom_command` मेथड एक पायथन कॉलेबल को उस एक्शन आइडेंटिफ़ायर से बाइंड करता है जिसे हमने पहले सेट किया था।

```python
# Step 5: Register the server‑side command that updates a cell value
def mark_reviewed_handler(req):
    """
    req is a dict containing at least:
        - 'cell': Excel address like "B5"
    This function writes "Reviewed" into the target cell and saves the workbook.
    """
    # Update the cell value
    ws.get_range(req["cell"]).put_value("Reviewed")
    
    # Persist changes back to disk
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    
    # Return a simple JSON response the client can interpret
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)
```

> **Why this works:** हैंडलर क्लाइंट से सेल रेफ़रेंस प्राप्त करता है, `Worksheet` API का उपयोग करके **update cell value** करता है, और फिर पूरी वर्कबुक को डिस्क पर वापस लिखता है। रिस्पॉन्स फ्रंट‑एंड को बताता है कि ऑपरेशन सफल रहा।

### Edge‑Case Handling

- **Missing cell reference:** यदि `req` में `"cell"` नहीं है, तो स्पष्ट त्रुटि उठाएँ ताकि UI टॉस्ट दिखा सके।  
- **Concurrent edits:** उच्च‑ट्रैफ़िक परिदृश्यों के लिए, वर्कबुक को लॉक करने या संस्करण‑स्टैम्प उपयोग करने पर विचार करें ताकि रेस कंडीशन से बचा जा सके।

## Step 6: Enable Lazy Loading for Big Sheets

यदि आप हजारों पंक्तियों के साथ काम कर रहे हैं, तो लेज़ी लोडिंग UI को तेज़ रखती है। पेज साइज को एक उचित चंक पर सेट करें—500 पंक्तियाँ अधिकांश ब्राउज़रों के लिए अच्छी रहती हैं।

```python
# Step 6: Activate lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500
```

> **What if you have 10 000 rows?** ग्रिड डेटा को पेज‑बाय‑पेज अनुरोध करेगा, जिससे क्लाइंट और सर्वर दोनों पर मेमोरी दबाव कम हो जाता है।

## Step 7: (Optional) Add a Custom Modal for Row Editing

कभी‑कभी आपको इनलाइन एडिटर से अधिक रिच UI चाहिए होती है। GridJs आपको एक मोडल विंडो पॉप‑अप करने देता है जिसे आप कहीं भी होस्ट कर सकते हैं—शायद एक React कंपोनेंट या एक साधारण HTML फ़ॉर्म।

```python
# Step 7: Configure a custom modal window for row editing
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"   # Serve this URL from your Flask/Django app
```

> **Why use a modal?** यह जटिल वैलिडेशन लॉजिक को अलग करता है और लेआउट पर पूर्ण नियंत्रण देता है, जबकि अभी भी ग्रिड से ट्रिगर किया जाता है।

## Step 8: Retrieve the Client‑Side Configuration JSON

अंत में, आपको कॉन्फ़िगरेशन को ब्राउज़र तक पहुँचाना होगा। `get_client_config` मेथड सब कुछ एक JSON ब्लॉब में सीरियलाइज़ करता है जिसे फ्रंट‑एंड GridJs लाइब्रेरी उपभोग कर सकती है।

```python
# Step 8: Get the JSON configuration for the front‑end
client_config = grid.get_client_config()

# Example: you might embed this in a template
print(client_config)   # For debugging – remove in production
```

आउटपुट लगभग इस तरह दिखता है (संक्षिप्तता के लिए ट्रिम किया गया):

```json
{
  "worksheet": "example.xlsx",
  "settings": {
    "spell_check": {"enabled": true},
    "context_menu": {
      "custom_items": [
        {"text": "Mark as Reviewed", "action": "markReviewed"}
      ]
    },
    "lazy_load": {"enabled": true, "page_size": 500},
    "custom_modal": {
      "enabled": true,
      "title": "Edit Row Details",
      "url": "/row-editor.html"
    }
  }
}
```

### Expected Result

- किसी भी सेल पर राइट‑क्लिक करने से **Mark as Reviewed** वाला मेनू खुलता है।  
- इसे चुनने पर सर्वर को अनुरोध भेजा जाता है, जो सेल वैल्यू को “Reviewed” में **अपडेट** करता है और `example‑updated.xlsx` को सहेजता है।  
- स्पेल‑चेकिंग उपयोगकर्ता के टाइप करने पर गलत शब्दों को हाइलाइट करती है।  

यह सब बिना पूरे पेज को रीफ़्रेश किए होता है, लेज़ी लोडिंग और हल्के JSON पेलोड की वजह से।

## Common Questions & Pro Tips

| प्रश्न | उत्तर |
|----------|--------|
| *यदि वर्कबुक केवल‑पढ़ने योग्य है तो क्या करें?* | फ़ाइल अनुमतियों को लिखने योग्य बनाएं, या यदि लाइब्रेरी समर्थन करती है तो `mode="rw"` के साथ वर्कबुक खोलें। |
| *क्या मैं एक से अधिक कस्टम मेनू आइटम जोड़ सकता हूँ?* | बिल्कुल—सिर्फ अतिरिक्त डिक्ट को `grid.settings.context_menu.custom_items` में जोड़ें। |
| *सेल अपडेट के बाद क्या मुझे ग्रिड को रीफ़्रेश करना चाहिए?* | यदि आप `{status:"ok"}` लौटाते हैं तो GridJs स्वचालित रूप से प्रभावित पंक्ति को रीफ़्रेश करता है; अन्यथा क्लाइंट से `grid.refresh()` कॉल करें। |
| *स्पेल‑चेकिंग को भाषा‑विशिष्ट कैसे बनाऊँ?* | `grid.settings.spell_check.language = "en-US"` सेट करें (या कोई भी समर्थित लोकेल)। |
| *क्या लेज़ी लोडिंग सर्वर‑साइड फ़िल्टरिंग के साथ संगत है?* | हां—`grid.settings.filter.enabled = True` को संयोजित करें और अपने कस्टम कमांड में फ़िल्टर लॉजिक लागू करें। |

## Full Working Example (All Steps Combined)

नीचे एक सिंगल स्क्रिप्ट है जिसे आप Flask रूट में ड्रॉप कर सकते हैं या स्टैंडअलोन प्रोसेस के रूप में चला सकते हैं। `YOUR_DIRECTORY` को अपने सर्वर पर वास्तविक पाथ से बदलें।

```python
import cells
import gridjs
from flask import Flask, request, jsonify, render_template_string

app = Flask(__name__)

# ---------- Initialization ----------
wb = cells.Workbook("YOUR_DIRECTORY/example.xlsx")
ws = wb.worksheets[0]

grid = gridjs.GridJs()
grid.set_worksheet(ws)

# Enable helpers
grid.settings.spell_check.enabled = True
grid.settings.syntax_check.enabled = True
grid.settings.formula_explanation.enabled = True

# Lazy loading
grid.settings.lazy_load.enabled = True
grid.settings.lazy_load.page_size = 500

# Custom context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed"
})

# Custom command implementation
def mark_reviewed_handler(req):
    cell_addr = req.get("cell")
    if not cell_addr:
        return {"status": "error", "message": "Cell address missing"}
    ws.get_range(cell_addr).put_value("Reviewed")
    wb.save("YOUR_DIRECTORY/example-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", mark_reviewed_handler)

# Optional modal
grid.settings.custom_modal.enabled = True
grid.settings.custom_modal.title = "Edit Row Details"
grid.settings.custom_modal.url = "/row-editor.html"

client_config = grid.get_client_config()

# ---------- Flask Routes ----------
@app.route("/")
def index():
    # Simple page that injects the config into a <script> tag
    html = f"""
    <!doctype html>
    <html>
    <head>
        <title>GridJs Demo</title>
        <script src="https://unpkg.com/gridjs/dist/gridjs.umd.js"></script>
    </head>
    <body>
        <div id="grid"></div>
        <script>
            const config = {client_config};
            new gridjs.Grid(config).render(document.getElementById("grid"));
        </script>
    </body>
    </html>
    """
    return render_template_string(html)

@app.route("/command/<name>", methods=["POST"])
def command(name):


## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोच को एक्सप्लोर कर सकें।

- [Aspose.Cells Java का उपयोग करके Excel वर्कबुक में कस्टम कंटेंट टाइप प्रॉपर्टीज़ जोड़ें](/cells/english/java/tables-structured-references/aspose-cells-java-custom-content-types/)
- [वर्कबुक में ID के साथ कस्टम XML पार्ट्स जोड़ें](/cells/english/net/workbook-operations/add-custom-xml-parts-with-id/)
- [Aspose Cells Java कस्टम लोड फ़िल्टर Excel एक्सपोर्ट](/cells/hindi/java/import-export/aspose-cells-java-custom-load-filters-excel-export/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}