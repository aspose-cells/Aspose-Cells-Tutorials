---
category: general
date: 2026-10-26
description: C# में WRAPCOLS का उपयोग करके एक रेंज को कॉलम में विभाजित करना, पंक्तियों
  के लिए WRAPROWS लागू करना, और प्रोग्रामेटिक रूप से वर्कबुक को XLSX के रूप में सहेजना
  सीखें।
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use wrapcols
- split range into rows
- excel wrapcols example
- save workbook as xlsx
- create excel workbook programmatically
language: hi
lastmod: 2026-10-26
og_description: C# में WRAPCOLS का उपयोग करके डेटा को कॉलम में विभाजित करना, पंक्तियों
  के लिए WRAPROWS का उपयोग करना, और वर्कबुक को XLSX के रूप में सहेजना। पूरी चरण‑दर‑चरण
  गाइड का पालन करें।
og_image_alt: Screenshot illustrating how to use WRAPCOLS to split a range into columns
  in Excel
og_title: C# में WRAPCOLS का उपयोग कैसे करें – रेंज को विभाजित करें और XLSX के रूप
  में सहेजें
schemas:
- author: Aspose
  dateModified: '2026-10-26'
  description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  headline: How to use WRAPCOLS in C# and save workbook as XLSX
  type: TechArticle
- description: Learn how to use WRAPCOLS in C# to split a range into columns, apply
    WRAPROWS for rows, and save workbook as XLSX programmatically.
  name: How to use WRAPCOLS in C# and save workbook as XLSX
  steps:
  - name: What the saved file looks like
    text: 'When you open `wrapcols_wraprows_output.xlsx` in Excel you’ll see:'
  - name: Changing the number of columns or rows
    text: '* **More columns:** Increase the second argument of `WRAPCOLS`. Example:
      `=WRAPCOLS(A1:A10,5)` creates five columns, leaving empty cells where data runs
      out. * **Dynamic column count:** Use a cell reference instead of a hard‑coded
      number. `=WRAPCOLS(A1:A10, G1)` where `G1` holds the desired column c'
  - name: Handling empty or non‑numeric cells
    text: WRAPCOLS and WRAPROWS ignore empty cells by default, but they preserve the
      order of non‑empty values. If you need to preserve blanks, wrap the source range
      with `IFERROR` or `TEXT` functions before applying WRAPCOLS.
  - name: Saving to other formats
    text: 'While this tutorial focuses on **save workbook as xlsx**, Aspose.Cells
      supports many formats (`.xls`, `.csv`, `.pdf`, etc.):'
  - name: What’s next?
    text: '* Explore **conditional formatting** to highlight the spilled data. * Combine
      **WRAPCOLS** with **SORT** or **FILTER** for dynamic dashboards. * Use Aspose.Cells’
      **charting API** to visualize the rearranged data directly from code.'
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: C# में WRAPCOLS का उपयोग कैसे करें और वर्कबुक को XLSX के रूप में सहेजें
url: /hi/net/row-and-column-management/how-to-use-wrapcols-in-c-and-save-workbook-as-xlsx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में WRAPCOLS का उपयोग कैसे करें और वर्कबुक को XLSX के रूप में सहेजें

यदि आपको **WRAPCOLS का उपयोग कैसे करें** Excel फ़ाइल में डेटा को पुनः व्यवस्थित करने की आवश्यकता है, तो यह गाइड आपको एक पूर्ण, चलाने योग्य समाधान दिखाता है। आप एक **excel wrapcols example** देखेंगे, WRAPROWS के साथ **range को rows में विभाजित करना** सीखेंगे, और **save workbook as XLSX** के साथ समाप्त करेंगे—सभी **programmatically** किया गया।

Excel के साथ C# से काम करना अक्सर वर्कबुक बनाना, फ़ॉर्मूले लागू करना और फ़ाइल को स्थायी रूप से सहेजना शामिल करता है। नीचे दिया गया कोड Aspose.Cells लाइब्रेरी का उपयोग करता है, जो आपको Microsoft Office स्थापित किए बिना Excel फ़ाइलों को संभालने की सुविधा देता है। इस ट्यूटोरियल के अंत तक आप **create excel workbook programmatically** कर पाएँगे, डेटा को क्षैतिज और लंबवत दोनों रूप में विभाजित कर पाएँगे, और एक साफ़ `.xlsx` फ़ाइल तैयार कर पाएँगे जो आगे की प्रोसेसिंग के लिए तैयार है।

## आवश्यकताएँ

* .NET 6.0 या बाद का संस्करण (कोड .NET Framework 4.7+ के साथ भी काम करता है)
* **Aspose.Cells** NuGet पैकेज का रेफ़रेंस  
  ```bash
  dotnet add package Aspose.Cells
  ```
* C# और Excel फ़ॉर्मूले की बुनियादी समझ

## चरण 1: WRAPCOLS का उपयोग करके रेंज को कॉलम में विभाजित करना

**WRAPCOLS** फ़ंक्शन एक‑आयामी रेंज लेता है और उसके मानों को निर्दिष्ट कॉलम संख्या में फैलाता है। इस उदाहरण में हम `A1:A10` में मौजूद मानों से शुरू करते हैं और WRAPCOLS को तीन कॉलम बनाने के लिए कहते हैं।

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook – this is the “create excel workbook programmatically” step
        Workbook workbook = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet ws = workbook.Worksheets[0];

        // Populate source data for demonstration
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 0].PutValue($"Item {i + 1}");
        }

        // Apply WRAPCOLS: split A1:A10 into 3 columns starting at C1
        // The formula is entered in cell C1 (row 0, column 2)
        ws.Cells[0, 2].Formula = "=WRAPCOLS(A1:A10,3)";

        // -------------------------------------------------
        // Why this works:
        // -------------------------------------------------
        // * WRAPCOLS reads the source range (A1:A10) vertically.
        // * The second argument (3) tells Excel to create three columns.
        // * The function returns a 2‑dimensional array that Excel spills into the
        //   surrounding cells automatically.
        // -------------------------------------------------
```

> **परिणाम:** सेल `C1:E4` अब मूल दस आइटम को तीन कॉलम में व्यवस्थित दिखाते हैं (अंतिम कॉलम में शेष आइटम रखे गए हैं)।

![Excel में WRAPCOLS का उपयोग करके रेंज को कॉलम में कैसे विभाजित किया जाए, यह दर्शाता स्क्रीनशॉट](image-url.png)

## चरण 2: WRAPROWS के साथ रेंज को पंक्तियों में विभाजित करना

जबकि **WRAPCOLS** क्षैतिज रूप से काम करता है, **WRAPROWS** इसके विपरीत करता है: यह रेंज को निर्दिष्ट पंक्तियों की संख्या में फैलाता है। यहाँ हम `B1:B10` से मान लेकर उन्हें `F1` से शुरू होने वाली दो पंक्तियों में व्यवस्थित करते हैं।

```csharp
        // Populate a second source column for WRAPROWS
        for (int i = 0; i < 10; i++)
        {
            ws.Cells[i, 1].PutValue($"Value {i + 1}");
        }

        // Apply WRAPROWS: split B1:B10 into 2 rows starting at F1
        ws.Cells[0, 5].Formula = "=WRAPROWS(B1:B10,2)";

        // -------------------------------------------------
        // Why WRAPROWS is useful:
        // -------------------------------------------------
        // * It converts a vertical list into a matrix with the specified row count.
        // * Handy when you need to prepare data for pivot tables, charts, or
        //   reporting layouts that expect a horizontal orientation.
        // -------------------------------------------------
```

> **परिणाम:** सूत्र `F1:K2` कोशिकाओं को दस मानों से भरता है जो दो पंक्तियों में वितरित होते हैं।

## चरण 3: वर्कबुक को XLSX के रूप में सहेजें

फ़ॉर्मूले लागू करने के बाद, अंतिम चरण फ़ाइल को स्थायी रूप से सहेजना है। **save workbook as xlsx** ऑपरेशन इन‑मेमोरी वर्कबुक को आधुनिक OpenXML फ़ॉर्मेट में डिस्क पर लिखता है।

```csharp
        // Save the workbook – this completes the “save workbook as xlsx” step
        string outputPath = Path.Combine(
            Environment.GetFolderPath(Environment.SpecialFolder.Desktop),
            "wrapcols_wraprows_output.xlsx");

        workbook.Save(outputPath, SaveFormat.Xlsx);

        Console.WriteLine($"Workbook saved to: {outputPath}");
    }
}
```

### सहेजी गई फ़ाइल कैसी दिखती है

| C | D | E |
|---|---|---|
| आइटम 1 | आइटम 4 | आइटम 7 |
| आइटम 2 | आइटम 5 | आइटम 8 |
| आइटम 3 | आइटम 6 | आइटम 9 |
|        |        | आइटम 10 |

और

| F | G | H | I | J | K |
|---|---|---|---|---|---|
| मान 1 | मान 3 | मान 5 | मान 7 | मान 9 | |
| मान 2 | मान 4 | मान 6 | मान 8 | मान 10 | |

फ़ॉर्मूले कोशिकाओं में बने रहते हैं, इसलिए स्रोत रेंज में बाद में किए गए कोई भी परिवर्तन स्वचालित रूप से परिलक्षित होते हैं।

## चरण 4: सामान्य विविधताएँ और किनारे के मामले

### कॉलम या पंक्तियों की संख्या बदलना

* **More columns:** `WRAPCOLS` के दूसरे तर्क को बढ़ाएँ।  
  उदाहरण: `=WRAPCOLS(A1:A10,5)` पाँच कॉलम बनाता है, जहाँ डेटा समाप्त हो जाता है वहाँ खाली कोशिकाएँ छोड़ देता है।
* **Dynamic column count:** हार्ड‑कोडेड संख्या के बजाय एक सेल रेफ़रेंस उपयोग करें।  
  `=WRAPCOLS(A1:A10, G1)` जहाँ `G1` वांछित कॉलम संख्या रखता है।

### खाली या गैर‑संख्यात्मक कोशिकाओं को संभालना

WRAPCOLS और WRAPROWS डिफ़ॉल्ट रूप से खाली कोशिकाओं को नजरअंदाज़ करते हैं, लेकिन गैर‑खाली मानों का क्रम बनाए रखते हैं। यदि आपको खाली स्थान भी संरक्षित रखने हैं, तो WRAPCOLS लागू करने से पहले स्रोत रेंज को `IFERROR` या `TEXT` फ़ंक्शन से घेरें।

### अन्य फ़ॉर्मैट में सहेजना

जबकि यह ट्यूटोरियल **save workbook as xlsx** पर केंद्रित है, Aspose.Cells कई फ़ॉर्मैट (`.xls`, `.csv`, `.pdf`, आदि) को सपोर्ट करता है:

```csharp
workbook.Save("output.pdf", SaveFormat.Pdf);   // Export to PDF
workbook.Save("output.csv", SaveFormat.Csv);   // Export to CSV
```

## प्रो टिप्स और संभावित समस्याएँ

* **Pro tip:** यदि आप सहेजने के तुरंत बाद फ़ॉर्मूले का मूल्यांकन करना चाहते हैं तो `Workbook.Settings.CalcEngineEnabled = true` सेट करें।
* **Watch out for:** बड़े स्रोत रेंज बहुत बड़े स्पिल एरिया उत्पन्न कर सकते हैं, जिससे प्रदर्शन पर असर पड़ सकता है। रेंज आकार को सीमित रखें या ऑपरेशन को कई वर्कशीट में विभाजित करें।
* **Thread safety:** Aspose.Cells ऑब्जेक्ट **थ्रेड‑सेफ़ नहीं** हैं। यदि आप फ़ाइलों को समानांतर में प्रोसेस कर रहे हैं तो प्रत्येक थ्रेड के लिए एक अलग `Workbook` इंस्टेंस बनाएँ।

## निष्कर्ष

अब आप जानते हैं **WRAPCOLS का उपयोग कैसे करें** एक लंबवत रेंज को कई कॉलम में विभाजित करने के लिए, **WRAPROWS के साथ range को rows में विभाजित करना**, और इन परिवर्तन के बाद **save workbook as XLSX** कैसे करें। ऊपर बताए गए चरणों का पालन करके आप **create excel workbook programmatically** कर सकते हैं, शक्तिशाली स्पिल फ़ॉर्मूले लागू कर सकते हैं, और बिना मैन्युअल हस्तक्षेप के तैयार‑से‑शेयर Excel फ़ाइलें बना सकते हैं।

### आगे क्या?

* **conditional formatting** का उपयोग करके स्पिल्ड डेटा को हाइलाइट करें।
* **WRAPCOLS** को **SORT** या **FILTER** के साथ मिलाकर डायनेमिक डैशबोर्ड बनाएँ।
* कोड से सीधे पुनर्व्यवस्थित डेटा को विज़ुअलाइज़ करने के लिए Aspose.Cells की **charting API** का उपयोग करें।

कोडिंग का आनंद लें, और अपने Excel वर्कफ़्लो को स्वचालित करने का मज़ा उठाएँ!

## अगला आप क्या सीखें?

निम्नलिखित ट्यूटोरियल्स निकटतम संबंधित विषयों को कवर करते हैं जो इस गाइड में प्रदर्शित तकनीकों पर आधारित हैं। प्रत्येक संसाधन में पूर्ण कार्यशील कोड उदाहरण और चरण‑दर‑चरण व्याख्याएँ शामिल हैं, जो आपको अतिरिक्त API सुविधाओं में महारत हासिल करने और अपने प्रोजेक्ट्स में वैकल्पिक कार्यान्वयन दृष्टिकोणों का अन्वेषण करने में मदद करेंगे।

- [C# में WRAPCOLS का उपयोग कैसे करें – Excel WRAPROWS और फ़ॉर्मूला पुनर्गणना के साथ पूर्ण गाइड](/cells/english/net/row-and-column-management/how-to-use-wrapcols-in-c-full-guide-with-excel-wraprows-reca/)
- [C# में WRAPCOLS का उपयोग – Excel में एरे को मैट्रिक्स में बदलना](/cells/english/net/formulas-functions/how-to-use-wrapcols-in-c-reshape-an-array-to-a-matrix-in-exc/)
- [WRAPCOLS का उपयोग – C# Excel ऑटोमेशन के लिए पूर्ण गाइड](/cells/english/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-complete-guide-for-c-excel-automation/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}