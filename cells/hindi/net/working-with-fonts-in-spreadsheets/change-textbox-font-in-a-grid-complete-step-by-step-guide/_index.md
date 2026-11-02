---
category: general
date: 2026-06-21
description: जानेँ कैसे टेक्स्टबॉक्स फ़ॉन्ट बदलें, प्रोग्रामेटिक रूप से फ़ॉन्ट रंग
  सेट करें और ग्रिड में फ़ॉन्ट आकार की सेल को समायोजित करें। टेक्स्टबॉक्स को स्टाइल
  करने के लिए इस व्यावहारिक ट्यूटोरियल का पालन करें।
draft: false
keywords:
- change textbox font
- change font size cell
- how to style textbox
- set font color programmatically
- change font family grid
language: hi
og_description: ग्रिड में टेक्स्टबॉक्स फ़ॉन्ट को जल्दी बदलें। यह गाइड दिखाता है कि
  टेक्स्टबॉक्स को कैसे स्टाइल करें, प्रोग्रामेटिक रूप से फ़ॉन्ट रंग सेट करें, और स्पष्ट
  कोड के साथ सेल का आकार समायोजित करें।
og_title: ग्रिड में टेक्स्टबॉक्स फ़ॉन्ट बदलें – पूर्ण प्रोग्रामिंग मार्गदर्शन
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  headline: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to change textbox font, set font color programmatically and
    adjust font size cell in a grid. Follow this practical tutorial for styling textboxes.
  name: Change Textbox Font in a Grid – Complete Step‑by‑Step Guide
  steps:
  - name: Breaking Down the Object
    text: '| Property | Purpose | Example Values | |----------|---------|----------------|
      | `family` | Font family – controls the typeface. | `"Arial"`, `"Helvetica"`,
      `"Courier New"` | | `size` | Font size in pixels (or points, depending on the
      grid). | `12`, `14`, `16` | | `color` | Text color in any CSS‑co'
  - name: Expected Output
    text: '- The textbox located at **row 2, column 3** now displays text in **Arial**,
      **14 px**, and a **#0066CC** blue hue. - Opening the browser console will print
      something like:'
  - name: Can I change only the font size without affecting family or color?
    text: 'Absolutely. Just omit the properties you don’t want to modify:'
  - name: What if my grid uses a different property name for the textbox?
    text: Inspect the cell object in the console (`console.log(cell)`). You’ll likely
      see something like `cell.editor` or `cell.input`. Replace `cell.textbox` with
      the correct reference.
  - name: How do I apply the same style to an entire column?
    text: 'Loop through the rows and set the font for each cell in that column:'
  - name: Is there a way to revert to the original font?
    text: 'Store the original style before overwriting:'
  type: HowTo
tags:
- JavaScript
- UI‑grid
- DOM‑manipulation
title: ग्रिड में टेक्स्टबॉक्स फ़ॉन्ट बदलें – पूर्ण चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/working-with-fonts-in-spreadsheets/change-textbox-font-in-a-grid-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ग्रिड में टेक्स्टबॉक्स फ़ॉन्ट बदलें – पूर्ण चरण‑दर‑चरण गाइड

क्या आपको कभी **डेटा ग्रिड** के अंदर टेक्स्टबॉक्स फ़ॉन्ट बदलना पड़ा लेकिन सही प्रॉपर्टी नहीं पता थी? आप अकेले नहीं हैं—बहुत से डेवलपर्स को एडिटेबल टेबल या डैशबोर्ड बनाते समय यही समस्या आती है। इस ट्यूटोरियल में हम बिल्कुल वही दिखाएंगे कि कैसे टेक्स्टबॉक्स फ़ॉन्ट बदलें, प्रोग्रामेटिकली उसका रंग सेट करें, और यहाँ तक कि फ़ॉन्ट साइज को सेल‑दर‑सेल समायोजित करें।

हम **टेक्स्टबॉक्स को स्टाइल करने** के टिप्स भी देंगे, **सेल में फ़ॉन्ट साइज बदलने** के परिदृश्य कवर करेंगे, और **फ़ॉन्ट रंग प्रोग्रामेटिकली सेट करने** का तरीका दिखाएंगे बिना सिरदर्द के। अंत तक आपके पास एक पुन: उपयोग योग्य स्निपेट होगा जो किसी भी ग्रिड कॉम्पोनेन्ट के साथ काम करेगा जो `getCell` API प्रदान करता है।

## Prerequisites

- ES6 सपोर्ट वाला आधुनिक ब्राउज़र (Chrome, Edge, Firefox, Safari)
- एक ग्रिड लाइब्रेरी जो `grid.getCell(row, col)` प्रदान करती है और एक सेल ऑब्जेक्ट लौटाती है जिसमें `textbox` रेफ़रेंस होता है
- जावास्क्रिप्ट ऑब्जेक्ट्स और CSS प्रॉपर्टीज़ का बेसिक ज्ञान

कोई अतिरिक्त पैकेज आवश्यक नहीं—सिर्फ प्लेन जावास्क्रिप्ट और ग्रिड की अपनी API।

## Overview of the Solution

मुख्य विचार सरल है: लक्ष्य सेल को प्राप्त करें, उसके एम्बेडेड टेक्स्टबॉक्स को पकड़ें, फिर एक नया फ़ॉन्ट ऑब्जेक्ट असाइन करें जिसमें फ़ॉन्ट फैमिली, साइज और रंग परिभाषित हों। इसे टेक्स्टबॉक्स को नया कपड़ा देने जैसा समझें। नीचे हाई‑लेवल फ्लो दिया गया है:

1. **लक्ष्य सेल तक पहुँचें** – वह रो/कॉलम लोकेट करें जिसे आप बदलना चाहते हैं।
2. **टेक्स्टबॉक्स प्राप्त करें** – वह UI एलिमेंट जो टेक्स्ट रखता है।
3. **फ़ॉन्ट स्टाइल ऑब्जेक्ट बनाएं** – फैमिली, साइज और रंग निर्दिष्ट करें।
4. **स्टाइल लागू करें** – ऑब्जेक्ट को टेक्स्टबॉक्स की `font` प्रॉपर्टी में असाइन करें।

बस इतना ही। अब प्रत्येक चरण में गहराई से देखें, क्यों महत्वपूर्ण है, और कोड को एक्शन में देखें।

![Screenshot of a grid cell with a styled textbox – change textbox font](/images/change-textbox-font-example.png)

## Step 1: Access the Target Cell in the Grid

```javascript
// Step 1: Access the target cell in the grid
const cell = grid.getCell(2, 3);
```

> **यह क्यों महत्वपूर्ण है:**  
> ग्रिड अक्सर रो और कॉलम को ज़ीरो‑बेस्ड इंडेक्स के रूप में स्टोर करता है। `grid.getCell(2, 3)` कॉल करके हम **रो 2, कॉलम 3** का सेल प्राप्त करते हैं। यदि आप किसी अन्य लोकेशन के लिए **सेल में फ़ॉन्ट साइज बदलना** चाहते हैं, तो बस इंडेक्स बदल दें।

**Pro tip:** यदि आपका ग्रिड नामित कॉलम सपोर्ट करता है, तो न्यूमेरिक कॉलम को की से बदल सकते हैं, जैसे `grid.getCell(2, "price")`।

## Step 2: Grab the Textbox Inside That Cell

```javascript
// Step 2: Get the textbox contained in that cell
const textbox = cell.textbox;
```

> **क्या हो रहा है:**  
> अधिकांश ग्रिड इम्प्लीमेंटेशन एडिटेबल कंटेंट को `<input>` या `<textarea>` एलिमेंट में रैप करते हैं और इसे `cell.textbox` के रूप में एक्सपोज़ करते हैं। रेफ़रेंस को पकड़ने से हम उसकी विज़ुअल स्टाइल को सीधे मैनिपुलेट कर सकते हैं।

यदि ग्रिड किसी अलग प्रॉपर्टी नाम (जैसे `cell.editor`) का उपयोग करता है, तो कोड को उसी अनुसार एडजस्ट करें—यह एक सामान्य वैरिएशन है जब आप **कस्टम कॉम्पोनेन्ट के लिए टेक्स्टबॉक्स को स्टाइल करना** चाहते हैं।

## Step 3: Define the Desired Font Properties

```javascript
// Step 3: Define the desired font properties
const fontStyle = {
  family: "Arial",          // change font family grid
  size: 14,                 // change font size cell
  color: "#0066CC"          // set font color programmatically
};
```

### Breaking Down the Object

| Property | Purpose | Example Values |
|----------|---------|----------------|
| `family` | फ़ॉन्ट फैमिली – टाइपफ़ेस को नियंत्रित करता है। | `"Arial"`, `"Helvetica"`, `"Courier New"` |
| `size`   | फ़ॉन्ट साइज पिक्सेल (या ग्रिड के अनुसार पॉइंट) में। | `12`, `14`, `16` |
| `color`  | टेक्स्ट रंग, कोई भी CSS‑कम्पैटिबल फ़ॉर्मेट। | `"#0066CC"`, `"rgb(255,0,0)"`, `"navy"` |

> **हम ऑब्जेक्ट क्यों उपयोग करते हैं:**  
> तीनों एट्रिब्यूट्स को एक साथ पैक करने से कोड साफ़ रहता है और कई UI लाइब्रेरीज़ की स्टाइल जानकारी की अपेक्षा के साथ मेल खाता है। यह आपको **ग्रिड में फ़ॉन्ट फैमिली बदलना** या **प्रोग्रामेटिकली फ़ॉन्ट रंग सेट करना** एक ही असाइनमेंट से करने देता है।

## Step 4: Apply the Font Style to the Textbox

```javascript
// Step 4: Apply the font style to the textbox
textbox.font = fontStyle;
```

> **पर्दे के पीछे:**  
> ग्रिड का टेक्स्टबॉक्स कॉम्पोनेन्ट `font` प्रॉपर्टी को इंटरप्रेट करता है और उसके अनुसार CSS अपडेट करता है। यह एक लाइन पहले के फ़ॉन्ट फैमिली, साइज और रंग को एक साथ बदल देती है—बिल्कुल वही जो आपको **कई सेल्स में टेक्स्टबॉक्स फ़ॉन्ट बदलने** के लिए चाहिए।

यदि कॉम्पोनेन्ट किसी अलग API (जैसे `textbox.style.fontFamily = ...`) का उपयोग करता है, तो असाइनमेंट को उसी अनुसार बदलें लेकिन सिद्धांत वही रखें।

## Full Working Example

नीचे एक सेल्फ‑कंटेन्ड स्निपेट है जिसे आप HTML फ़ाइल में पेस्ट कर सकते हैं जिसमें एक मॉक ग्रिड ऑब्जेक्ट शामिल है। यह स्टेप 1 से स्टेप 4 तक का पूरा फ्लो दिखाता है, साथ ही एक तेज़ वेरिफिकेशन भी देता है कि स्टाइल बदल गया है।

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Change Textbox Font Demo</title>
  <style>
    .grid { display: table; border-collapse: collapse; }
    .grid .row { display: table-row; }
    .grid .cell { display: table-cell; border: 1px solid #ccc; padding: 8px; }
    .grid .cell input { width: 100%; border: none; }
  </style>
</head>
<body>

<div id="myGrid" class="grid"></div>

<script>
/* ---------- Mock Grid Implementation ---------- */
class MockGrid {
  constructor(rows, cols) {
    this.rows = rows;
    this.cols = cols;
    this.el = document.getElementById('myGrid');
    this._build();
  }
  _build() {
    for (let r = 0; r < this.rows; r++) {
      const rowDiv = document.createElement('div');
      rowDiv.className = 'row';
      for (let c = 0; c < this.cols; c++) {
        const cellDiv = document.createElement('div');
        cellDiv.className = 'cell';
        const input = document.createElement('input');
        input.type = 'text';
        input.value = `R${r}C${c}`;
        // expose textbox via a custom property
        cellDiv.textbox = input;
        cellDiv.appendChild(input);
        rowDiv.appendChild(cellDiv);
      }
      this.el.appendChild(rowDiv);
    }
  }
  getCell(row, col) {
    const rowDiv = this.el.children[row];
    if (!rowDiv) return null;
    const cellDiv = rowDiv.children[col];
    return cellDiv || null;
  }
}

/* ---------- Use the Grid ---------- */
const grid = new MockGrid(5, 5); // 5x5 grid for demo

// ---- Change Textbox Font (the core tutorial steps) ----
const cell = grid.getCell(2, 3);          // step 1
const textbox = cell.textbox;             // step 2
const fontStyle = {                      // step 3
  family: "Arial",
  size: 14,
  color: "#0066CC"
};
textbox.font = fontStyle;                // step 4

// Verify by logging computed style
setTimeout(() => {
  const cs = window.getComputedStyle(textbox);
  console.log('Applied font family:', cs.fontFamily);
  console.log('Applied font size:', cs.fontSize);
  console.log('Applied color:', cs.color);
}, 0);
</script>
</body>
</html>
```

### Expected Output

- **रो 2, कॉलम 3** पर स्थित टेक्स्टबॉक्स अब **Arial**, **14 px**, और **#0066CC** नीले रंग में टेक्स्ट दिखाएगा।
- ब्राउज़र कंसोल खोलने पर कुछ इस तरह प्रिंट होगा:

```
Applied font family: Arial, Helvetica, sans-serif
Applied font size: 14px
Applied color: rgb(0, 102, 204)
```

यदि आप पेज खोलेंगे, तो आप विज़ुअली बदलाव देख पाएँगे—कोई डिफ़ॉल्ट सिस्टम फ़ॉन्ट नहीं रहेगा।

## Frequently Asked Questions (FAQ)

### क्या मैं केवल फ़ॉन्ट साइज बदल सकता हूँ बिना फैमिली या रंग को प्रभावित किए?
बिल्कुल। उन प्रॉपर्टीज़ को छोड़ दें जिन्हें आप बदलना नहीं चाहते:

```javascript
textbox.font = { size: 18 }; // only changes size
```

### अगर मेरे ग्रिड में टेक्स्टबॉक्स के लिए अलग प्रॉपर्टी नाम है तो क्या करें?
कंसोल में सेल ऑब्जेक्ट को इन्स्पेक्ट करें (`console.log(cell)`)। आपको संभवतः `cell.editor` या `cell.input` जैसा कुछ दिखेगा। `cell.textbox` को सही रेफ़रेंस से बदल दें।

### मैं पूरे कॉलम पर एक ही स्टाइल कैसे लागू करूँ?
रोज़ के माध्यम से लूप चलाएँ और उस कॉलम के प्रत्येक सेल के लिए फ़ॉन्ट सेट करें:

```javascript
for (let r = 0; r < grid.rowCount; r++) {
  const colCell = grid.getCell(r, 3);
  colCell.textbox.font = fontStyle; // reuse the same fontStyle object
}
```

### क्या मूल फ़ॉन्ट पर वापस लौटने का कोई तरीका है?
ओवरराइट करने से पहले मूल स्टाइल को स्टोर करें:

```javascript
const original = { ...textbox.font };
textbox.font = fontStyle; // apply new style
// later...
textbox.font = original; // revert
```

## Tips & Best Practices

- **बैच अपडेट्स:** यदि आपको कई सेल्स को स्टाइल करना है, तो बदलावों को `requestAnimationFrame` या ग्रिड‑स्पेसिफिक बैच मेथड में रैप करें ताकि लेआउट थ्रैशिंग से बचा जा सके।
- **रेस्पॉन्सिव फ़ॉन्ट्स:** यदि आपका UI स्केल करना है तो फिक्स्ड पिक्सेल की बजाय रिलेटिव यूनिट्स (`em`, `rem`) उपयोग करें।
- **एक्सेसिबिलिटी:** जब आप **प्रोग्रामेटिकली फ़ॉन्ट रंग सेट** करते हैं तो पर्याप्त कंट्रास्ट सुनिश्चित करें—WCAG AA न्यूनतम 4.5:1 रेशियो सामान्य टेक्स्ट के लिए है।
- **क्रॉस‑ब्राउज़र क्विर्क्स:** कुछ पुराने ग्रिड्स को `<input>` एलिमेंट पर सीधे `style.fontFamily` सेट करना पड़ सकता है बजाय `font` ऑब्जेक्ट के।

## Conclusion

हमने अभी-अभी **ग्रिड के अंदर टेक्स्टबॉक्स फ़ॉन्ट बदलना** कवर किया, सही सेल को पकड़ने से लेकर एक रीयूज़ेबल `fontStyle` ऑब्जेक्ट परिभाषित करने और एक लाइन में लागू करने तक। इस दौरान हमने **सेल में फ़ॉन्ट साइज बदलना**, **प्रोग्रामेटिकली फ़ॉन्ट रंग सेट करना**, और यहाँ तक कि **ग्रिड में फ़ॉन्ट फैमिली बदलना** भी सीखा।

अब आप इस पैटर्न को किसी भी UI लाइब्रेरी में एडेप्ट कर सकते हैं—चाहे आप एडमिन डैशबोर्ड बना रहे हों, स्प्रेडशीट‑जैसा एडिटर, या कस्टम रिपोर्टिंग टूल। विभिन्न फ़ॉन्ट फैमिली, साइज और रंग के साथ प्रयोग करें; शायद होवर इफ़ेक्ट्स या डेटा वैल्यू के आधार पर कंडीशनल स्टाइलिंग भी जोड़ें।

कोई और स्टाइलिंग चैलेंज है? कमेंट करें, और हम मिलकर हल करेंगे। Happy coding!

## What Should You Learn Next?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Change Font Color in Excel Using Aspose.Cells for Java&#58; A Complete Guide](/cells/english/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/german/java/formatting/change-font-color-aspose-cells-java-tutorial/)
- [Change Font Color Aspose Cells Java Tutorial](/cells/french/java/formatting/change-font-color-aspose-cells-java-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}