---
category: general
date: 2026-06-30
description: Python Excel ग्रिड में कस्टम कॉन्टेक्स्ट मेनू जोड़ें और अपडेटेड फ़ाइल
  को सेव करते समय Excel सेल में मान लिखें। राइट‑क्लिक मेनू बनाना और Python शैली में
  सेल वैल्यू अपडेट करना सीखें।
draft: false
keywords:
- add custom context menu
- write value to excel cell
- create right‑click menu
- update cell value python
- save updated excel file
language: hi
og_description: Python में कस्टम कॉन्टेक्स्ट मेनू जोड़ें ताकि मान को Excel सेल में
  लिखा जा सके और अपडेटेड Excel फ़ाइल को सहेजा जा सके। यह गाइड आपको GridJs के साथ राइट‑क्लिक
  मेनू बनाने की प्रक्रिया दिखाता है।
og_title: Python में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – चरण‑दर‑चरण ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Add custom context menu to a Python Excel grid and write value to excel
    cell while saving the updated file. Learn to create right‑click menu and update
    cell value python style.
  headline: Add Custom Context Menu in Python – Complete Guide
  type: TechArticle
tags:
- Python
- Excel Automation
- GridJs
- Context Menu
title: Python में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – पूर्ण गाइड
url: /hi/python/integration-and-interoperability/add-custom-context-menu-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python में कस्टम कॉन्टेक्स्ट मेनू जोड़ें – पूर्ण गाइड

क्या आपने कभी सोचा है कि Python से सर्व की जा रही स्प्रेडशीट ग्रिड में **कस्टम कॉन्टेक्स्ट मेनू** आइटम कैसे जोड़ें? शायद आपको एक तेज़ “Mark as Reviewed” बटन चाहिए जो उपयोगकर्ता जब किसी सेल पर राइट‑क्लिक करे तो पॉप अप हो, Excel सेल में एक मान लिखे, और फिर अपडेटेड वर्कबुक को सहेज दे—बिना वेब UI छोड़े।  

इस ट्यूटोरियल में हम ठीक वही बनाएँगे: GridJs द्वारा संचालित एक **कस्टम राइट‑क्लिक मेनू**, एक सर्वर‑साइड हैंडलर जो **Excel सेल में मान लिखता है**, और एक अंतिम चरण जो डिस्क पर **अपडेटेड Excel फ़ाइल को सहेजता है**। अंत तक आपके पास एक पुन: उपयोग योग्य पैटर्न होगा जिसे आप किसी भी Flask, FastAPI, या Django प्रोजेक्ट में डाल सकते हैं।

> **क्यों महत्वपूर्ण?**  
> कस्टम कॉन्टेक्स्ट मेनू जोड़ने से डेटा रिव्यू वर्कफ़्लो सरल हो जाता है, मैन्युअल कॉपी‑पेस्टिंग कम होती है, और एंड‑यूज़र्स को ग्रिड के भीतर ही एक नेटिव‑फ़ील अनुभव मिलता है। साथ ही, आप देखेंगे कि **Python‑स्टाइल में सेल वैल्यू अपडेट** कैसे करें, जो किसी भी Excel ऑटोमेशन टास्क के लिए एक मुख्य कौशल है।

## आवश्यकताएँ

- Python 3.9+ (कोड 3.10 पर भी काम करता है)  
- `openpyxl` Excel फ़ाइल हैंडलिंग के लिए  
- `gridjs` Python रैपर (या यदि आप फ्रंट‑एंड पसंद करते हैं तो JS लाइब्रेरी)  
- एक बेसिक वेब फ्रेमवर्क (Flask उदाहरण दिखाया गया)  
- आपके प्रोजेक्ट फ़ोल्डर में `sample.xlsx` नाम की वर्कबुक फ़ाइल  

यदि आप इनमें से कोई भी नहीं रखते हैं, तो चलाएँ:

```bash
pip install openpyxl flask gridjs
```

अब चलिए शुरू करते हैं।

---

## चरण 1 – कस्टम कॉन्टेक्स्ट मेनू जोड़ें: GridJs को इनिशियलाइज़ करें और वर्कशीट बाइंड करें

सबसे पहला काम यह है कि आप एक `GridJs` इंस्टेंस बनाएँ और उसे उस वर्कशीट की ओर इंगित करें जिसके साथ आप काम करने वाले हैं। यहीं पर हमारे कोड में **कस्टम कॉन्टेक्स्ट मेनू जोड़ें** वाक्यांश पहली बार आता है, और यह बाकी सबके लिए मंच तैयार करता है।

```python
# step_1_initialize.py
import openpyxl
from gridjs import GridJs

# Load the workbook – this could be any .xlsx file you own
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]                     # Grab the sheet you’ll display

# Create the GridJs object and bind it to the worksheet
grid = GridJs()
grid.set_worksheet(ws)                # <-- add custom context menu works on this sheet
```

**क्या हो रहा है?**  
`grid.set_worksheet(ws)` GridJs को बताता है कि वह `ws` से डेटा को अपने डेटा स्रोत के रूप में उपयोग करे। अब से, हम जो भी कॉन्टेक्स्ट‑मेन्यू संशोधन जोड़ेंगे, वह स्वचालित रूप से उसी वर्कशीट को टारगेट करेगा, जिससे UI और फ़ाइल सिंक में रहेंगी।

> **प्रो टिप:** अपनी वर्कबुक को केवल एक बार रीड/राइट मोड में खोलें। अनुरोध हैंडलर के भीतर इसे बार‑बार खोलने से Windows पर फ़ाइल‑लॉकिंग समस्याएँ हो सकती हैं।

---

## चरण 2 – Excel सेल में मान लिखें: मेनू आइटम के लिए एक्शन परिभाषित करें

अब जब ग्रिड तैयार है, हमें उपयोगकर्ता के हमारे कस्टम कमांड चुनने पर **excel सेल में मान लिखना** होगा। हम “Mark as Reviewed” नाम का एक मेनू एंट्री जोड़ेंगे और उसे `markReviewed` पहचानकर्ता देंगे। यह पहचानकर्ता वह है जो क्लाइंट‑साइड JavaScript सर्वर को वापस भेजेगा।

```python
# step_2_menu_item.py
# Append a custom item to the right‑click context menu
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",      # Text shown in the UI
    "action": "markReviewed",        # Identifier used on the client side
    "icon": "check_circle"           # Optional Material‑Icons name
})
```

**कस्टम पहचानकर्ता क्यों उपयोग करें?**  
पहचानकर्ता UI टेक्स्ट को सर्वर लॉजिक से अलग करता है, जिससे आप लेबल को बैकएंड कोड को छुए बिना बदल सकते हैं। यह **right‑click मेनू बनाना** ऑपरेशन को स्पष्ट और पुन: उपयोग योग्य भी बनाता है।

---

## चरण 3 – राइट‑क्लिक मेनू बनाएं: सर्वर‑साइड हैंडलर रजिस्टर करें

मेनू आइटम स्थापित होने के बाद, हमें GridJs को बताना होगा कि उपयोगकर्ता के क्लिक करने पर क्या करना है। यहीं पर हम **right‑click मेनू बनाते** हैं जो वास्तव में Python को एक अनुरोध भेजता है।

```python
# step_3_handler.py
def on_custom_command(request):
    """
    Server‑side handler for the 'markReviewed' custom command.
    It receives a JSON payload like {"cell": "C12"}.
    """
    # Extract the cell address from the incoming request
    cell_address = request["cell"]           # e.g., "C12"

    # Write the word "Reviewed" into that cell
    ws[cell_address] = "Reviewed"            # <-- write value to excel cell

    # Persist the change to disk (see next step)
    # We'll return a simple JSON response to the client
    return {"status": "ok"}
```

ध्यान देने योग्य कुछ बातें:

1. **`ws[cell_address] = "Reviewed"`** **cell value python अपडेट** को **अपडेट करने** का सबसे सीधा तरीका है। अंदरूनी रूप से, `openpyxl` A1‑स्टाइल एड्रेस को रो/कॉलम इंडेक्स में बदल देता है।  
2. हैंडलर एक छोटा JSON पेलोड लौटाता है। GridJs एक स्टेटस इंडिकेटर की अपेक्षा करता है; यदि आवश्यक हो तो आप इसे एरर मैसेज शामिल करने के लिए विस्तारित कर सकते हैं।

अब हम पहचानकर्ता को हैंडलर से बाइंड करते हैं:

```python
# step_3_register.py
grid.register_custom_command("markReviewed", on_custom_command)
```

**अगर सेल खाली या प्रोटेक्टेड हो तो क्या करें?**  
- खाली सेल ठीक हैं—`openpyxl` उन्हें तुरंत बना देगा।  
- प्रोटेक्टेड शीट्स के लिए, आपको पहले अनप्रोटेक्ट करना होगा (`ws.protection.sheet = False`) या `PermissionError` को पकड़ना होगा।

---

## चरण 4 – Python में सेल वैल्यू अपडेट करें: वर्कबुक को सहेजकर बदलाव को स्थायी बनाएं

मान लिखना केवल आधा काम है; आपको **अपडेटेड excel फ़ाइल सहेजनी** होगी ताकि बदलाव वर्तमान सत्र के बाद भी बना रहे। यहीं पर हम UI से डिस्क तक की राउंड‑ट्रिप पूरी करते हैं।

```python
# step_4_save.py
def on_custom_command(request):
    cell_address = request["cell"]
    ws[cell_address] = "Reviewed"

    # Save the workbook to a known location
    wb.save("output/sample-updated.xlsx")   # <-- save updated excel file
    return {"status": "ok"}
```

**एक अलग फ़ोल्डर क्यों?**  
`output/` डायरेक्टरी में सहेजने से मूल टेम्पलेट अपरिवर्तित रहता है, जो ऑडिट ट्रेल्स के लिए उपयोगी है। अपने डिप्लॉयमेंट वातावरण के अनुसार पाथ को समायोजित करें।

> **सावधान रहें:** यदि आप कई समकालिक उपयोगकर्ताओं को सर्व कर रहे हैं, तो `wb.save()` के आसपास एक थ्रेड‑सेफ़ लॉक (`threading.Lock`) उपयोग करने पर विचार करें ताकि रेस कंडीशन से बचा जा सके।

---

## चरण 5 – क्लाइंट कॉन्फ़िगरेशन JSON जेनरेट करें और सबको जोड़ें

अंत में, हमें वह JSON बनाना होगा जिसे फ्रंट‑एंड GridJs इंस्टेंस उपयोग करेगा। इस JSON में वर्कशीट डेटा **और** कस्टम मेनू परिभाषा दोनों होते हैं।

```python
# step_5_config.py
config_json = grid.get_client_config()
print(config_json)   # You can pipe this to your template engine
```

जब आप `config_json` को अपने HTML पेज में एम्बेड करेंगे, तो GridJs ग्रिड को “Mark as Reviewed” एंट्री के साथ राइट‑क्लिक योग्य हर सेल पर रेंडर करेगा।

### पूर्ण Flask उदाहरण

नीचे एक न्यूनतम Flask ऐप है जो सभी हिस्सों को जोड़ता है। इसे चलाएँ, `http://localhost:5000` खोलें और किसी भी सेल पर राइट‑क्लिक करके कस्टम मेनू को कार्य में देखें।

```python
# app.py
from flask import Flask, request, jsonify, render_template_string
import openpyxl
from gridjs import GridJs

app = Flask(__name__)

# Load workbook once at startup
wb = openpyxl.load_workbook("sample.xlsx")
ws = wb["Sheet1"]
grid = GridJs()
grid.set_worksheet(ws)

# ---- Add custom context menu item ----
grid.settings.context_menu.custom_items.append({
    "text": "Mark as Reviewed",
    "action": "markReviewed",
    "icon": "check_circle"
})

# ---- Server‑side handler ----
def on_custom_command(req):
    cell = req["cell"]
    ws[cell] = "Reviewed"
    wb.save("output/sample-updated.xlsx")
    return {"status": "ok"}

grid.register_custom_command("markReviewed", on_custom_command)

# ---- Routes ----
@app.route("/")
def index():
    config = grid.get_client_config()
    # Simple inline template; in production use a separate .html file
    html = f"""
    <!doctype html>
    <html>
      <head>
        <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
        <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
      </head>
      <body>
        <div id="wrapper"></div>
        <script>
          const config = {config};
          new gridjs.Grid(config).render(document.getElementById("wrapper"));
        </script>
      </body>
    </html>
    """
    return render_template_string(html)

@app.route("/custom-command", methods=["POST"])
def custom_command():
    payload = request.get_json()
    result = on_custom_command(payload)
    return jsonify(result)

if __name__ == "__main__":
    app.run(debug=True)
```

**अपेक्षित परिणाम:**  
- किसी भी सेल पर राइट‑क्लिक करें → “Mark as Reviewed” दिखाई देगा।  
- उस पर क्लिक करें → सेल की सामग्री “Reviewed” में बदल जाएगी।  
- वर्कबुक `output/sample-updated.xlsx` अब नया मान रखती है।

---

## सामान्य प्रश्न और किनारे के केस

| प्रश्न | उत्तर |
|----------|--------|
| *अगर मुझे कई कस्टम एक्शन चाहिए तो?* | सिर्फ `grid.settings.context_menu.custom_items` में और ऑब्जेक्ट जोड़ें और प्रत्येक को उसके अपने पहचानकर्ता के साथ रजिस्टर करें। |
| *क्या मैं हैंडलर को अतिरिक्त डेटा (जैसे, row ID) पास कर सकता हूँ?* | हाँ। क्लाइंट साइड पर JSON पेलोड में अतिरिक्त कुंजियाँ शामिल करें, फिर उन्हें `on_custom_command` में `request` से पढ़ें। |
| *क्या यह तरीका async फ्रेमवर्क्स के साथ संगत है?* | बिल्कुल—सिर्फ `on_custom_command` को async फ़ंक्शन बनाएं और यदि आप `aiofiles` या समान में स्विच करते हैं तो `await wb.save(...)` उपयोग करें। |
| *मैं मेनू आइकन को कैसे स्टाइल करूँ?* | कोई भी Material‑Icons नाम दें (`"icon": "edit"`)। फ्रंट‑एंड स्वचालित रूप से आइकन फ़ॉन्ट लोड करता है। |
| *बड़े वर्कबुक्स के बारे में क्या?* | सिर्फ आवश्यक शीट लोड करें, और मेमोरी उपयोग कम रखने के लिए `openpyxl.iter_rows()` से रो स्ट्रीम करने पर विचार करें। |

## आगे आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण करने में मदद करेंगे।

- [Preserve Single Quote Prefix of Cell Value or Range in Excel](/cells/english/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/german/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)
- [Preserve Single Quote Prefix Of Cell Value Or Range In Excel](/cells/french/net/excel-data-preservation-warning/preserve-single-quote-prefix-of-cell-value-or-range-in-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}