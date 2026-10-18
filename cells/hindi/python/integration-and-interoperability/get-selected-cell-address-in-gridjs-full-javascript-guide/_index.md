---
category: general
date: 2026-06-30
description: जानेँ कैसे JavaScript के साथ GridJs का उपयोग करके चयनित सेल का पता प्राप्त
  करें, ग्रिड सेल का मान अपडेट करें और इनपुट मान पढ़ें। चरण‑दर‑चरण कोड और टिप्स।
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: hi
og_description: चयनित सेल का पता प्राप्त करें, ग्रिड सेल मान अपडेट करें और जावास्क्रिप्ट
  से इनपुट मान पढ़ें। सुगम GridJs एकीकरण के लिए इस पूर्ण मार्गदर्शिका का पालन करें।
og_title: चयनित सेल का पता प्राप्त करें – पूर्ण GridJs जावास्क्रिप्ट ट्यूटोरियल
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: GridJs में चयनित सेल पता प्राप्त करें – पूर्ण जावास्क्रिप्ट गाइड
url: /hi/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# चयनित सेल पता प्राप्त करें – पूर्ण GridJs जावास्क्रिप्ट ट्यूटोरियल

क्या आपको कभी **चयनित सेल पता** GridJs टेबल से प्राप्त करने की ज़रूरत पड़ी, लेकिन कौन सा API कॉल इस्तेमाल करना है, नहीं पता चला? आप अकेले नहीं हैं। कई एडमिन पैनलों में, उपयोगकर्ता एक सेल पर क्लिक करते हैं, मोडल में मान संपादित करते हैं, और उम्मीद करते हैं कि ग्रिड तुरंत बदलाव को दर्शाए। यह ट्यूटोरियल आपको ठीक‑ठीक दिखाता है कि वह पता कैसे प्राप्त करें, इनपुट फ़ील्ड से नया मूल्य पढ़ें, और **पेज रीलोड किए बिना ग्रिड सेल वैल्यू अपडेट** करें।

हम **जावास्क्रिप्ट से इनपुट वैल्यू पढ़ना** सही तरीके से, एज केस को संभालना, और अपडेट समाप्त होने पर मोडल को बंद करना भी कवर करेंगे। अंत तक आपके पास एक स्व-समाहित स्निपेट होगा जिसे आप किसी भी GridJs‑प्रोजेक्ट में डाल सकते हैं।

## आप क्या बनाएँगे

- GridJs द्वारा संचालित एक साधारण HTML टेबल।
- एक एडिटिंग मोडल जो सेल पर क्लिक करने पर दिखाई देगा।
- जावास्क्रिप्ट जो **चयनित सेल पता प्राप्त करता है**, उपयोगकर्ता‑द्वारा टाइप किया गया मूल्य लेता है, **ग्रिड सेल वैल्यू अपडेट** करता है, और अंत में मोडल को छुपा देता है।

कोई बाहरी लाइब्रेरी नहीं चाहिए, केवल GridJs। कोड आधुनिक ब्राउज़रों (Chrome 102+, Edge, Firefox) में काम करता है। यदि आपके पेज पर पहले से GridJs इंस्टेंस है, तो आप सीधे संबंधित भाग कॉपी‑पेस्ट कर सकते हैं।

## पूर्वापेक्षाएँ

- जावास्क्रिप्ट और DOM का बुनियादी ज्ञान।
- GridJs लाइब्रेरी लोडेड (CDN या npm के माध्यम से)।
- एक पेज जो पहले से GridJs ग्रिड रेंडर करता है (हम एक न्यूनतम उदाहरण दिखाएंगे)।

यदि इनमें से कोई भी परिचित नहीं लग रहा, तो घबराएँ नहीं—हर कदम में एक त्वरित पुनरावलोकन शामिल है।

---

## चरण 1: HTML स्केलेटन सेट अप करें

पहले टेबल कंटेनर, छिपा हुआ मोडल, और प्राइस इनपुट को व्यवस्थित करें। मोडल को सरल CSS क्लासेज़ से टॉगल किया जाएगा।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **प्रो टिप:** `#editModal` एक न्यूनतम CSS ट्रिक उपयोग करता है—सिर्फ `active` क्लास जोड़ें ताकि यह दिखे। आप इसे Bootstrap, Tailwind, या किसी भी मौजूदा मोडल कंपोनेंट से बदल सकते हैं।

---

## चरण 2: GridJs को इनिशियलाइज़ करें और सेल क्लिक कैप्चर करें

अब हम सैंपल डेटा के साथ एक ग्रिड बनाएँगे और सेल चयन को सुनेंगे। जब उपयोगकर्ता किसी सेल पर क्लिक करेगा, हम **चयनित सेल पता प्राप्त करेंगे** और मोडल खोलेंगे।

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **क्यों काम करता है:** `GridJs.getSelectedCell()` एक स्ट्रिंग जैसे `"C2"` (कॉलम C, रो 2) लौटाता है। इसे `lastSelectedCell` में स्टोर करने से बाद में **ग्रिड सेल वैल्यू अपडेट** करते समय सटीक स्थान मिल जाता है।

---

## चरण 3: इनपुट फ़ील्ड से नया प्राइस पढ़ें

जब उपयोगकर्ता **Save** पर क्लिक करता है, हमें **जावास्क्रिप्ट से इनपुट वैल्यू पढ़ना** सुरक्षित रूप से करना होगा। यह चरण यह भी सुनिश्चित करता है कि दर्ज किया गया प्राइस एक सकारात्मक संख्या है।

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **नोट:** `parseFloat` का उपयोग करने से दशमलव (जैसे `1.99`) स्वीकार होते हैं। `isNaN` गार्ड अनजाने में खाली सबमिशन को रोकता है।

---

## चरण 4: चयनित सेल वैल्यू अपडेट करें

अब हम अंततः **ग्रिड सेल वैल्यू अपडेट** करेंगे, वह पता उपयोग करके जो हमने पहले कैप्चर किया था। GridJs का `updateCell` मेथड एक प्रॉमिस लौटाता है, इसलिए हम मोडल‑क्लोज़ एक्शन को चेन कर सकते हैं।

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **प्रॉमिस क्यों उपयोग करें?** GridJs को टेबल को पुनः‑रेंडर या बैकएंड के साथ सिंक करना पड़ सकता है। प्रॉमिस का इंतज़ार करने से हम सुनिश्चित करते हैं कि UI केवल तब छुपे जब ग्रिड नया वैल्यू दर्शा रहा हो।

---

## चरण 5: कैंसल और एज केस संभालें

एक मजबूत समाधान हमेशा उपयोगकर्ता को बाहर निकलने का विकल्प देता है। **Cancel** बटन बस मोडल को छुपा देता है और किसी भी स्टोर किए गए पते को साफ़ कर देता है।

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### अगर कोई सेल चयनित नहीं है तो क्या होगा?

यदि उपयोगकर्ता किसी सेल पर क्लिक किए बिना **Save** बटन ट्रिगर कर देता है (शायद प्रोग्रामेटिकली मोडल खोल दिया गया हो), तो `lastSelectedCell` `null` रहेगा। `updateSelectedCell` में शुरुआती‑रिटर्न रन‑टाइम एरर को रोकता है और एक उपयोगी चेतावनी लॉग करता है।

### बड़े ग्रिड्स से निपटना

पैजिनेशन वाले ग्रिड्स के लिए भी, `GridJs.getSelectedCell()` पूर्ण पता (जैसे `"B12"`) लौटाता है, केवल दृश्यमान रो नहीं। इसलिए अपडेट तब भी काम करता है जब संपादित रो किसी अन्य पेज पर हो। बस ध्यान रखें कि UI स्वचालित रूप से पेज नहीं बदलता—यदि आपको यह चाहिए, तो `grid.forceUpdate()` कॉल करें या मैन्युअली उचित पेज पर नेविगेट करें।

---

## पूर्ण कार्यशील उदाहरण

नीचे पूरा कोड दिया गया है जिसे आप एक ही HTML फ़ाइल में कॉपी‑पेस्ट कर सकते हैं। ब्राउज़र में खोलें, किसी भी सेल पर क्लिक करें, प्राइस बदलें, और देखें कि ग्रिड तुरंत अपडेट हो जाता है।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## आगे क्या सीखें?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकें और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन अप्रोचेज़ का अन्वेषण कर सकें।

- [पूरा Excel रेंज के लिए पता, सेल काउंट और ऑफसेट प्राप्त करें](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [पूरा Excel रेंज के लिए पता, सेल काउंट और ऑफसेट प्राप्त करें (जर्मन)](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [पूरा Excel रेंज के लिए पता, सेल काउंट और ऑफसेट प्राप्त करें (फ़्रेंच)](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}