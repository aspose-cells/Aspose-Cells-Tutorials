---
category: general
date: 2026-06-30
description: पूर्ण जावास्क्रिप्ट उदाहरण के साथ आसानी से gridjs बनाने का तरीका, जिसमें
  gridjs कॉन्फ़िगरेशन, कंटेनर सेटअप और रेंडर प्रक्रिया शामिल है।
draft: false
keywords:
- how to create gridjs
- gridjs configuration
- gridjs render
- gridjs JavaScript
- gridjs container
language: hi
og_description: पूर्ण जावास्क्रिप्ट उदाहरण के साथ ग्रिडजएस को आसानी से कैसे बनाएं,
  जिसमें ग्रिडजएस कॉन्फ़िगरेशन, कंटेनर सेटअप और रेंडर प्रक्रिया शामिल है।
og_title: Gridjs कैसे बनाएं – पूर्ण जावास्क्रिप्ट ग्रिड गाइड
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  headline: How to Create Gridjs – Complete JavaScript Grid Guide
  type: TechArticle
- description: How to create gridjs easily with a full JavaScript example, covering
    gridjs configuration, container setup, and render process.
  name: How to Create Gridjs – Complete JavaScript Grid Guide
  steps:
  - name: Why this configuration matters
    text: '- **Columns** – define the header text and optional width. Without this,
      Gridjs would infer column names from the first data row, which is often less
      readable. - **Data** – an array of rows, each row being an array of cell values.
      You could also supply an async function that fetches data from an API'
  - name: Expected Output
    text: '``` +----+----------------+---------------------+--------+ | ID | Name
      | Email | Role | +----+----------------+---------------------+--------+ | 1
      | Alice Johnson | alice@example.com | Admin | | 2 | Bob Smith | bob@example.com
      | Editor | +----+----------------+---------------------+--------+ [←] [1]'
  - name: Loading Data Asynchronously
    text: 'If your data lives on a server, replace the static `data` array with a
      function that returns a Promise:'
  - name: Custom Cell Rendering
    text: 'Sometimes you need icons, buttons, or formatted dates inside cells. Use
      the `formatter` property on a column:'
  - name: Multiple Grids on One Page
    text: 'Just repeat steps 2‑5 with different container IDs:'
  type: HowTo
tags:
- gridjs
- JavaScript
- web‑development
title: Gridjs कैसे बनाएं – पूर्ण जावास्क्रिप्ट ग्रिड गाइड
url: /hi/python/integration-and-interoperability/how-to-create-gridjs-complete-javascript-grid-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gridjs कैसे बनाएं – पूर्ण जावास्क्रिप्ट ग्रिड गाइड

क्या आप कभी **how to create gridjs** और तुरंत अपनी पेज पर एक शानदार डेटा टेबल देखना चाहते हैं? आप अकेले नहीं हैं। कई डेवलपर्स पहली बार Gridjs को सेटअप करने की कोशिश में अटक जाते हैं, विशेष रूप से कॉन्फ़िगरेशन ऑब्जेक्ट और रेंडर कॉल के आसपास। अच्छी खबर? सही कदम जानने के बाद यह बहुत आसान है।

इस ट्यूटोरियल में हम एक वास्तविक‑दुनिया का उदाहरण देखेंगे जो **how to create gridjs** को शून्य से दिखाता है, कैसे एक उचित **gridjs configuration** तैयार करें, ग्रिड को एक **gridjs container** से बाइंड करें, और अंत में **gridjs render** को ट्रिगर करें। अंत तक आपके पास एक पूरी तरह से कार्यशील ग्रिड होगा जिसे आप किसी भी प्रोजेक्ट में डाल सकते हैं—कोई रहस्य नहीं, सिर्फ स्पष्ट कोड।

## आप क्या सीखेंगे

- Gridjs के लिए तैयार एक न्यूनतम HTML पेज सेट अप करें।
- एक **gridjs configuration** ऑब्जेक्ट लिखें जो कॉलम, डेटा और विकल्पों को परिभाषित करता है।
- Gridjs इंस्टेंस को एक **gridjs container** एलिमेंट से जोड़ें।
- **gridjs render** को कॉल करके टेबल दिखाएँ।
- सामान्य सेटिंग्स (पेजिनेशन, सॉर्टिंग, स्टाइलिंग) को समायोजित करें और सामान्य गलतियों से बचें।

कोई बाहरी बिल्ड टूल्स की आवश्यकता नहीं है; सब कुछ ब्राउज़र में एक ही स्क्रिप्ट टैग के साथ चलता है। चलिए शुरू करते हैं।

## Prerequisites

1. एक आधुनिक ब्राउज़र (Chrome, Edge, Firefox, Safari) – जो भी ES6 को सपोर्ट करता हो।  
2. HTML और JavaScript का बुनियादी ज्ञान – आपको किसी फ्रेमवर्क की जरूरत नहीं है।  
3. Gridjs लाइब्रेरी तक पहुंच – हम इसे CDN से लेंगे, इसलिए npm इंस्टॉल की जरूरत नहीं।

बस इतना ही। यदि आपके पास पहले से कोई पेज है जिसे आप सुधारना चाहते हैं, तो आप स्निपेट्स सीधे पेस्ट कर सकते हैं।

## Step 1: Add Gridjs Assets to Your Page

पहले, हमें Gridjs की CSS और JavaScript फ़ाइलें लोड करनी होंगी। CDN संस्करण हल्का है और त्वरित डेमो के लिए एकदम सही।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>How to Create Gridjs Example</title>
  <!-- Gridjs CSS -->
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet" />
</head>
<body>
  <!-- The grid will appear inside this div -->
  <div id="grid"></div>

  <!-- Gridjs JS -->
  <script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
```

> **Pro tip:** Mermaid थीम टेबल को बिना किसी अतिरिक्त CSS के एक साफ़, आधुनिक लुक देती है। यदि आप कोई अलग स्टाइल पसंद करते हैं तो `classic.min.css` से बदलने में संकोच न करें।

## Step 2: Define the **gridjs container**

**gridjs container** सिर्फ एक सामान्य `<div>` है जो रेंडर की गई टेबल को होस्ट करेगा। ऊपर के मार्कअप में हमने पहले ही `<div id="grid"></div>` बना दिया है। `id` एट्रिब्यूट महत्वपूर्ण है क्योंकि बाद में हम इसे Gridjs इंस्टेंस से बाइंड करेंगे।

यदि आपको एक ही पेज पर कई ग्रिड चाहिए, तो प्रत्येक कंटेनर को एक अनोखा ID (`grid1`, `grid2`, …) दें और बाइंडिंग लॉजिक को प्रत्येक के लिए दोहराएँ।

## Step 3: Craft a **gridjs configuration** Object

अब बात आती है **how to create gridjs** के दिल की – कॉन्फ़िगरेशन की। यह साधारण JavaScript ऑब्जेक्ट Gridjs को बताता है कि कौन से कॉलम दिखाने हैं, कौन सा डेटा भरना है, और कौन सी सुविधाएँ सक्षम करनी हैं।

```html
<script>
  // Step 3: Your gridjs configuration (replace with real data)
  const config = {
    columns: [
      { name: 'ID', width: '50px' },
      { name: 'Name' },
      { name: 'Email' },
      { name: 'Role' }
    ],
    data: [
      [1, 'Alice Johnson', 'alice@example.com', 'Admin'],
      [2, 'Bob Smith', 'bob@example.com', 'Editor'],
      [3, 'Carol White', 'carol@example.com', 'Viewer'],
      [4, 'David Brown', 'david@example.com', 'Admin']
    ],
    pagination: {
      limit: 2   // Show 2 rows per page
    },
    search: true,          // Enable client‑side search box
    sort: true,            // Allow column sorting
    language: {
      'search': {
        'placeholder': '🔍 Search…'
      },
      'pagination': {
        'previous': '←',
        'next': '→',
        'showing': 'Showing',
        'results': () => 'records'
      }
    }
  };
</script>
```

### Why this configuration matters

- **Columns** – हेडर टेक्स्ट और वैकल्पिक चौड़ाई को परिभाषित करता है। बिना इसे, Gridjs पहले डेटा रो से कॉलम नाम निकाल लेगा, जो अक्सर कम पढ़ने योग्य होता है।  
- **Data** – रो की एक एरे, जहाँ प्रत्येक रो सेल वैल्यू की एरे होती है। आप एक async फ़ंक्शन भी दे सकते हैं जो API से डेटा लाता है; लाइब्रेरी स्वचालित रूप से प्रॉमिस को संभालेगी।  
- **Pagination** – प्रति पेज रो की संख्या सीमित करता है, जिससे बड़ी टेबल UI को ओवरवेल्म नहीं करती।  
- **Search & Sort** – एक बूलियन से इंटरैक्टिव फीचर चालू करता है, जिससे आपको कस्टम हैंडलर लिखने की जरूरत नहीं पड़ती।  
- **Language** – UI स्ट्रिंग्स को कस्टमाइज़ करता है, स्थानीयकरण या ब्रांडिंग के लिए उपयुक्त।

बाद में आप स्थिर डेटा एरे को एक fetch कॉल से बदल सकते हैं; बाकी कदम बिल्कुल वही रहेंगे।

## Step 4: Instantiate Gridjs and Bind to the **gridjs container**

कॉन्फ़िगरेशन तैयार होने पर, हम एक नया `GridJs.Grid` (UMD बिल्ड में क्लास नाम `gridjs.Grid` है) बनाते हैं और इसे हमारे कंटेनर एलिमेंट की ओर इंगित करते हैं।

```html
<script>
  // Step 4: Create a Gridjs instance bound to the container
  const grid = new gridjs.Grid(document.getElementById('grid'), config);
</script>
```

ध्यान दें कि हमने `document.getElementById('grid')` का उपयोग किया है—यह वही **gridjs container** है जिसे हमने पहले परिभाषित किया था। यदि आपके पास कई कंटेनर हैं, तो इस लाइन को उचित ID के साथ दोहराएँ।

## Step 5: Trigger the **gridjs render** Call

पज़ल का अंतिम टुकड़ा **gridjs render** मेथड है। यह पहले पास की गई कॉन्फ़िगरेशन लेता है और कंटेनर में एक पूरी‑स्टाइल्ड `<table>` इन्जेक्ट करता है।

```html
<script>
  // Step 5: Render the grid inside the container
  grid.render();
</script>
</body>
</html>
```

बस इतना ही! जब आप पेज को ब्राउज़र में खोलेंगे, तो आपको चार रो वाली एक सर्चेबल, पेजिनेटेड टेबल दिखेगी। सर्च बॉक्स स्वचालित रूप से शीर्ष पर दिखाई देगा, और पेजिनेशन कंट्रोल्स नीचे स्थित होंगे।

### Expected Output

```
+----+----------------+---------------------+--------+
| ID | Name           | Email               | Role   |
+----+----------------+---------------------+--------+
| 1  | Alice Johnson  | alice@example.com   | Admin  |
| 2  | Bob Smith      | bob@example.com     | Editor |
+----+----------------+---------------------+--------+
[←] [1] [2] [→]   Search: 🔍 Search…
```

सर्च बॉक्स में टाइप करने या कॉलम हेडर पर क्लिक करके सॉर्ट करने पर UI अनुकूलित हो जाएगा।

## Common Variations & Edge Cases

### Loading Data Asynchronously

यदि आपका डेटा सर्वर पर रहता है, तो स्थिर `data` एरे को एक फ़ंक्शन से बदलें जो एक Promise रिटर्न करता है:

```js
const config = {
  columns: ['ID', 'Name', 'Email', 'Role'],
  data: () => fetch('/api/users')
                .then(res => res.json())
                .then(users => users.map(u => [u.id, u.name, u.email, u.role])),
  pagination: { limit: 10 },
  search: true,
  sort: true
};
```

Gridjs प्रॉमिस के रिजॉल्व होने तक एक लोडिंग स्पिनर दिखाएगा, फिर टेबल को स्वचालित रूप से रेंडर करेगा।

### Custom Cell Rendering

कभी‑कभी आपको सेल के अंदर आइकन, बटन, या फॉर्मेटेड डेट चाहिए होते हैं। ऐसे में कॉलम पर `formatter` प्रॉपर्टी का उपयोग करें:

```js
{
  name: 'Role',
  formatter: (cell) => {
    const color = cell === 'Admin' ? 'red' : 'gray';
    return gridjs.h('span', { style: { color } }, cell);
  }
}
```

`gridjs.h` हेल्पर वर्चुअल DOM एलिमेंट बनाता है बिना React को इम्पोर्ट किए।

### Multiple Grids on One Page

सिर्फ चरण 2‑5 को अलग‑अलग कंटेनर IDs के साथ दोहराएँ:

```html
<div id="usersGrid"></div>
<div id="ordersGrid"></div>

<script>
  const usersGrid = new gridjs.Grid(document.getElementById('usersGrid'), usersConfig);
  const ordersGrid = new gridjs.Grid(document.getElementById('ordersGrid'), ordersConfig);
  usersGrid.render();
  ordersGrid.render();
</script>
```

प्रत्येक ग्रिड स्वतंत्र रूप से काम करता है, इसलिए आप पेजिनेशन लिमिट, कॉलम सेट, और यहाँ तक कि थीम भी मिश्रित कर सकते हैं।

## Pro Tips & Pitfalls to Avoid

- **CSS को मत भूलें** – स्टाइलशीट के बिना टेबल साधारण HTML टेबल की तरह दिखेगा, सभी सुंदर स्टाइलिंग और पेजिनेशन कंट्रोल्स खो जाएंगे।  
- **डुप्लिकेट IDs से बचें** – प्रत्येक **gridjs container** का एक अनोखा ID होना चाहिए; नहीं तो Gridjs पहली इंस्टेंस को ओवरराइट कर देगा।  
- **डेटा की संरचना पर ध्यान दें** – कॉलम की संख्या प्रत्येक रो में सेल की संख्या से मेल खानी चाहिए; असंगत एरे साइलेंट लेआउट गड़बड़ी पैदा करेंगे।  
- **जटिल सेल्स के लिए `gridjs.h` का उपयोग करें** – रॉ HTML स्ट्रिंग्स इन्जेक्ट करने से वर्चुअल DOM डिफ़िंग एल्गोरिद्म टूट सकता है।  
- **वर्ज़न पर ध्यान दें** – ऊपर दिया गया CDN लिंक नवीनतम 5.x रिलीज़ (June 2026) की ओर इशारा करता है। यदि आप पुरानी वर्ज़न लॉक करते हैं, तो कुछ विकल्प (जैसे `language`) गायब हो सकते हैं।

## Full Working Example (Copy‑Paste)

नीचे पूरा HTML फ़ाइल दिया गया है जिसे आप `gridjs-demo.html` के रूप में सेव कर सीधे ब्राउज़र में खोल सकते हैं।



## What Should You Learn Next?

निम्नलिखित ट्यूटोरियल्स उन विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जिससे आप अतिरिक्त API फीचर्स में महारत हासिल कर सकते हैं और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को एक्सप्लोर कर सकते हैं।

- [Aspose.Cells for Java&#58; How to Create and Format Excel Workbooks Efficiently](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [How to Create and Export Excel to HTML Using Aspose.Cells Java | Workbook Operations Guide](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [How to Create and Merge Excel Workbooks Using Aspose.Cells for Java | Complete Guide](/cells/english/java/workbook-operations/create-merge-excel-workbooks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}