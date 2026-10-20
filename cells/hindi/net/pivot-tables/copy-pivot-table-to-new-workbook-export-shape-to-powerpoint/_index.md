---
category: general
date: 2026-10-20
description: Aspose.Cells का उपयोग करके पिवट टेबल को नई वर्कबुक में कॉपी करें और एक
  ही गाइड में संपादन योग्य शैप को PowerPoint में निर्यात करना सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- copy pivot table to new workbook
- copy rows between worksheets
- Aspose.Cells copy rows
- export shape to PowerPoint
- editable textbox in PowerPoint
language: hi
lastmod: 2026-10-20
og_description: Aspose.Cells का उपयोग करके पिवट टेबल को नई वर्कबुक में कॉपी करें और
  एक संपादन योग्य शैप को PowerPoint में निर्यात करें—आज ही चलाने योग्य चरण‑दर‑चरण
  कोड।
og_image_alt: Screenshot showing copy pivot table to new workbook using Aspose.Cells
og_title: पिवट तालिका को नई कार्यपुस्तिका में कॉपी करें, आकार को पावरपॉइंट में निर्यात
  करें
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  headline: Copy pivot table to new workbook, export shape to PowerPoint
  type: TechArticle
- description: Copy pivot table to new workbook using Aspose.Cells and learn how to
    export an editable shape to PowerPoint in a single guide.
  name: Copy pivot table to new workbook, export shape to PowerPoint
  steps:
  - name: – Load the source workbook and select the first worksheet
    text: '```csharp // Load the workbook that already contains the pivot table Workbook
      srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");'
  - name: – Define the cell area that includes the pivot table
    text: '```csharp // CellArea(startRow, startColumn, endRow, endColumn) // Here
      we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table CellArea
      sourceArea = new CellArea(0, 0, 20, 10); ```'
  - name: – Create the destination workbook and get its first worksheet
    text: '```csharp // Create an empty workbook that will receive the copied range
      Workbook destWorkbook = new Workbook();'
  - name: – Copy the rows from the source area to the destination sheet
    text: '```csharp // CopyRows(startRow, endRow, destinationCells, destinationStartRow)
      srcWorksheet.Cells.CopyRows( sourceArea.StartRow, sourceArea.EndRow, destWorksheet.Cells,
      0); // start at row 0 in the destination sheet ```'
  - name: – Save the new workbook
    text: '```csharp destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx"); ```'
  - name: – Create a new workbook and access its first worksheet
    text: '```csharp Workbook workbook = new Workbook(); // Empty workbook Worksheet
      worksheet = workbook.Worksheets[0]; // First (and only) sheet ```'
  - name: – Add a textbox shape to the worksheet
    text: '```csharp // AddTextBox(startRow, startColumn, width, height, text) int
      shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
      ```'
  - name: – Retrieve the shape and modify its text
    text: '```csharp Shape textShape = worksheet.Shapes[shapeIndex]; textShape.Text
      = "Change me in PowerPoint"; ```'
  - name: – Save the workbook as a PowerPoint presentation
    text: '```csharp workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
      ```'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Pivot Table
- PowerPoint Export
title: पिवट टेबल को नई वर्कबुक में कॉपी करें, आकार को पॉवरपॉइंट में निर्यात करें
url: /hi/net/pivot-tables/copy-pivot-table-to-new-workbook-export-shape-to-powerpoint/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# पिवट टेबल को नई वर्कबुक में कॉपी करें, आकार को PowerPoint में निर्यात करें

यदि आपको **copy pivot table to new workbook** को उसकी कार्यक्षमता बनाए रखते हुए कॉपी करना है, तो यह गाइड आपको Aspose.Cells के साथ इसे कैसे करना है दिखाता है। आप **export an editable shape to PowerPoint** का सबसे तेज़ तरीका भी देखेंगे, जिससे टेक्स्टबॉक्स रूपांतरण के बाद भी संपादन योग्य रहता है।

कई डेवलपर्स मानते हैं कि पिवट टेबल वाले रेंज को कॉपी करने से पिवट लॉजिक खो जाएगा, या PPTX के रूप में सहेजने पर आकार स्थिर छवियों में बदल जाते हैं। यह ट्यूटोरियल इन मिथकों को खारिज करता है और आपको एक विश्वसनीय, प्रोडक्शन‑रेडी समाधान देता है।

इन अगले सेक्शन्स में आप करेंगे:

* स्रोत वर्कबुक लोड करें और पिवट टेबल शामिल करने वाले रेंज को कॉपी करें।
* एक डेस्टिनेशन वर्कबुक बनाएं जिसमें वही पिवट टेबल हो।
* एक टेक्स्टबॉक्स आकार जोड़ें, उसका टेक्स्ट बदलें, और वर्कबुक को PowerPoint प्रेजेंटेशन के रूप में सहेजें जहाँ टेक्स्टबॉक्स संपादन योग्य बना रहे।
* समझें कि प्रत्येक API कॉल क्यों आवश्यक है और सामान्य pitfalls से कैसे बचें।

**आवश्यकताएँ**

* .NET 6.0 या बाद का (कोड .NET Framework 4.7+ के साथ भी काम करता है)।
* Aspose.Cells for .NET स्थापित (`Install-Package Aspose.Cells`)।
* C# और Visual Studio (या कोई भी IDE जो आप पसंद करते हैं) का बुनियादी ज्ञान।

---

## पिवट टेबल को नई वर्कबुक में कॉपी करें

यह चरण‑दर‑चरण सेक्शन दिखाता है कि पिवट टेबल वाले रेंज को कैसे कॉपी करें और नई फ़ाइल में पिवट परिभाषा को बनाए रखें।

### Step 1 – स्रोत वर्कबुक लोड करें और पहली वर्कशीट चुनें

```csharp
// Load the workbook that already contains the pivot table
Workbook srcWorkbook = new Workbook("YOUR_DIRECTORY/Source.xlsx");

// The first worksheet (index 0) holds the pivot table we want to copy
Worksheet srcWorksheet = srcWorkbook.Worksheets[0];
```

*क्यों?*  
`Workbook` Aspose.Cells में किसी भी Excel मैनिपुलेशन का एंट्री पॉइंट है। सही वर्कशीट चुनने से हम पिवट टेबल के सटीक स्थान पर काम कर पाते हैं।

### Step 2 – पिवट टेबल को शामिल करने वाले सेल एरिया को परिभाषित करें

```csharp
// CellArea(startRow, startColumn, endRow, endColumn)
// Here we copy rows 0‑20 and columns 0‑10, which covers the whole pivot table
CellArea sourceArea = new CellArea(0, 0, 20, 10);
```

*क्यों?*  
पिवट टेबल एक विशिष्ट सेल ब्लॉक के भीतर स्थित होती है। एक `CellArea` निर्दिष्ट करके जो पिवट को पूरी तरह घेरता है, Aspose.Cells को भी अंतर्निहित पिवट कैश को कॉपी करना पता चलता है।

### Step 3 – डेस्टिनेशन वर्कबुक बनाएं और उसकी पहली वर्कशीट प्राप्त करें

```csharp
// Create an empty workbook that will receive the copied range
Workbook destWorkbook = new Workbook();

// Destination worksheet (also index 0)
Worksheet destWorksheet = destWorkbook.Worksheets[0];
```

*क्यों?*  
एक नई वर्कबुक यह सुनिश्चित करती है कि कोई टकराव वाले नेम्ड रेंज या मौजूदा पिवट न हों, जिससे कॉपी ऑपरेशन साफ़ रहता है।

### Step 4 – स्रोत एरिया से पंक्तियों को डेस्टिनेशन शीट में कॉपी करें

```csharp
// CopyRows(startRow, endRow, destinationCells, destinationStartRow)
srcWorksheet.Cells.CopyRows(
    sourceArea.StartRow,
    sourceArea.EndRow,
    destWorksheet.Cells,
    0); // start at row 0 in the destination sheet
```

*क्यों?*  
`CopyRows` **Aspose.Cells copy rows** API का हिस्सा है। यह सेल वैल्यूज़ और छिपे हुए पिवट कैश दोनों को कॉपी करता है, इसलिए पिवट टेबल स्थानांतरण के बाद भी कार्यात्मक रहती है।

### Step 5 – नई वर्कबुक सहेजें

```csharp
destWorkbook.Save("YOUR_DIRECTORY/CopyWithPivot.xlsx");
```

*Result*  
Excel में `CopyWithPivot.xlsx` खोलें। पिवट टेबल बिल्कुल उसी तरह दिखती है जैसे स्रोत फ़ाइल में थी, और आप इसे सामान्य रूप से रिफ्रेश या संशोधित कर सकते हैं।

---

## संपादन योग्य आकार को PowerPoint में निर्यात करें

अब हम एक टेक्स्टबॉक्स आकार जोड़ेंगे, उसकी सामग्री बदलेंगे, और वर्कबुक को PPTX फ़ाइल के रूप में सहेजेंगे। PowerPoint में खोलने पर आकार पूरी तरह से संपादन योग्य रहता है।

### Step 1 – नई वर्कबुक बनाएं और उसकी पहली वर्कशीट तक पहुँचें

```csharp
Workbook workbook = new Workbook();          // Empty workbook
Worksheet worksheet = workbook.Worksheets[0]; // First (and only) sheet
```

### Step 2 – वर्कशीट में एक टेक्स्टबॉक्स आकार जोड़ें

```csharp
// AddTextBox(startRow, startColumn, width, height, text)
int shapeIndex = worksheet.Shapes.AddTextBox(10, 10, 200, 50, "Editable text");
```

*क्यों?*  
`AddTextBox` एक **editable textbox in PowerPoint**‑संगत आकार बनाता है। निर्देशांक पॉइंट्स में होते हैं; अपने लेआउट के अनुसार उन्हें समायोजित करें।

### Step 3 – आकार प्राप्त करें और उसका टेक्स्ट बदलें

```csharp
Shape textShape = worksheet.Shapes[shapeIndex];
textShape.Text = "Change me in PowerPoint";
```

*क्यों?*  
`Shape` ऑब्जेक्ट को सीधे एक्सेस करने से आप `Text`, `Font`, या `Fill` जैसी प्रॉपर्टीज़ बदल सकते हैं। यह चरण दर्शाता है कि प्रोग्रामेटिकली प्रारंभिक सामग्री कैसे सेट करें।

### Step 4 – वर्कबुक को PowerPoint प्रेजेंटेशन के रूप में सहेजें

```csharp
workbook.Save("YOUR_DIRECTORY/Presentation.pptx", SaveFormat.Pptx);
```

*Result*  
Microsoft PowerPoint में `Presentation.pptx` खोलें। टेक्स्टबॉक्स पहली स्लाइड पर दिखाई देता है, और आप इसे डबल‑क्लिक करके टेक्स्ट को किसी भी मूल PowerPoint आकार की तरह संपादित कर सकते हैं।

---

## अपेक्षित आउटपुट

| File | आप क्या देखेंगे |
|------|-----------------|
| `CopyWithPivot.xlsx` | मूल पिवट टेबल वाला एक वर्कशीट, पूरी तरह कार्यात्मक (रिफ्रेश काम करता है)। |
| `Presentation.pptx` | एकल स्लाइड जिसमें एक संपादन योग्य टेक्स्टबॉक्स है जिसमें लिखा है “Change me in PowerPoint”。 |

---

## सामान्य pitfalls और सर्वोत्तम‑प्रैक्टिस टिप्स

* **Pivot cache loss** – यदि आप केवल सेल वैल्यूज़ कॉपी करते हैं (उदाहरण के लिए `CopyRows` को `PasteOptions` फ़्लैग `PasteValues` के साथ उपयोग करते हुए), तो पिवट कैश छोड़ दिया जाता है और टेबल स्थिर हो जाता है। हमेशा दिखाए गए अनुसार डिफ़ॉल्ट `CopyRows` ओवरलोड का उपयोग करें।
* **Shape positioning** – `AddTextBox` पॉइंट यूनिट्स का उपयोग करता है, न कि Excel सेल इंडेक्स। स्लाइड पर गलत प्लेसमेंट से बचने के लिए एक सैंपल फ़ाइल पर निर्देशांक टेस्ट करें।
* **File format mismatch** – `SaveFormat.Pptx` के साथ वर्कबुक को PPTX के रूप में सहेजना सभी समर्थित आकारों को स्वचालित रूप से कन्वर्ट करता है। `Pdf` के रूप में सहेजने का प्रयास करने से आकार रास्टराइज़ हो जाता है, जिससे वह संपादन योग्य नहीं रहता।

---

## निष्कर्ष

अब आप जानते हैं कि Aspose.Cells for .NET का उपयोग करके **copy pivot table to new workbook** कैसे किया जाता है और **export an editable shape to PowerPoint** कैसे किया जाता है। पूर्ण, चलाने योग्य कोड उदाहरण प्रत्येक आवश्यक API कॉल को कवर करते हैं, बताते हैं कि प्रत्येक चरण क्यों महत्वपूर्ण है, और अपेक्षित परिणाम दिखाते हैं।

अगले, आप खोज सकते हैं:

* **Working with charts** – पिवट टेबल के साथ चार्ट कॉपी करें (`Aspose.Cells copy rows between worksheets`)।

## आपको आगे क्या सीखना चाहिए?

निम्नलिखित ट्यूटोरियल्स उन संबंधित विषयों को कवर करते हैं जो इस गाइड में दिखाए गए तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं जो आपको अतिरिक्त API फीचर्स में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक इम्प्लीमेंटेशन एप्रोच को खोजने में मदद करती हैं।

- [नया वर्कबुक बनाएं – पिवट टेबल के साथ वर्कशीट कॉपी करने का तरीका](/cells/english/net/excel-copy-worksheet/create-new-workbook-how-to-copy-a-worksheet-with-a-pivot-tab/)
- [पिवट टेबल कॉपी करें और Aspose.Cells के साथ Excel को PPTX में निर्यात करें](/cells/english/net/converting-excel-files-to-other-formats/copy-pivot-table-and-export-excel-to-pptx-with-aspose-cells/)
- [C# में नया वर्कबुक बनाएं – पिवट टेबल कॉपी करें](/cells/english/net/pivot-tables/create-new-workbook-in-c-copy-pivot-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}