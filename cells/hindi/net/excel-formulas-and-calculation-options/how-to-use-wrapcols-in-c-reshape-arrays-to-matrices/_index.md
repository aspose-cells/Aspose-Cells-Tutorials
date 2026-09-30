---
category: general
date: 2026-05-23
description: C# में WRAPCOLS का उपयोग करके 1D एरे को 2D मैट्रिक्स में कैसे बदलें।
  रैप कॉलम्स फ़ंक्शन सीखें, फ़ॉर्मूला को सेल में लिखें, और 1D को आसानी से 2D में परिवर्तित
  करें।
draft: false
keywords:
- how to use wrapcols
- reshape array to matrix
- convert 1d to 2d
- write formula to cell
- wrap columns function
language: hi
og_description: C# में WRAPCOLS का उपयोग कैसे करें, यह आपको एकल सूत्र से 1D एरे को
  2D मैट्रिक्स में बदलने की सुविधा देता है। इस गाइड का पालन करके सूत्र को सेल में
  लिखें और wrap columns फ़ंक्शन में निपुण बनें।
og_title: C# में WRAPCOLS का उपयोग कैसे करें – एरेज़ को मैट्रिक्स में बदलें
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  headline: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  type: TechArticle
- description: How to use WRAPCOLS in C# to reshape a 1D array into a 2D matrix. Learn
    the wrap columns function, write formula to cell, and convert 1d to 2d easily.
  name: How to Use WRAPCOLS in C# – Reshape Arrays to Matrices
  steps:
  - name: Why this matters
    text: You could try to roll your own matrix logic, but the **wrap columns function**
      already handles edge cases like uneven division and empty inputs. Adding the
      Aspose.Cells NuGet package gives us a clean API to interact with Excel formulas
      directly from C#.
  - name: The core of “how to use WRAPCOLS”
    text: 'The **WRAPCOLS** function takes two arguments: an array (or range) and
      the number of columns you want per row. In our case we’ll reshape the literal
      array `{1,2,3,4,5,6}` into **2 rows × 3 columns**.'
  - name: Expected output
    text: '``` 1 2 3 4 5 6 ```'
  type: HowTo
tags:
- C#
- Aspose.Cells
- Excel Automation
title: C# में WRAPCOLS का उपयोग कैसे करें – एरेज़ को मैट्रिक्स में बदलना
url: /hi/net/excel-formulas-and-calculation-options/how-to-use-wrapcols-in-c-reshape-arrays-to-matrices/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# में WRAPCOLS का उपयोग कैसे करें – एरे को मैट्रिक्स में बदलें

क्या आप कभी सोचते रहे हैं **how to use WRAPCOLS** जब आपको संख्याओं की एक सपाट सूची को एक व्यवस्थित तालिका में बदलना हो? आप अकेले नहीं हैं—कई डेवलपर्स को तब रुकावट आती है जब वे 1‑डायमेंशनल सूची को 2‑डायमेंशनल ग्रिड में बदलने की कोशिश करते हैं बिना बहुत सारे लूपिंग कोड लिखे। अच्छी खबर? WRAPCOLS फ़ंक्शन (जिसे कभी‑कभी wrap columns function कहा जाता है) एक ही लाइन में भारी काम कर देता है, और आप इसे सीधे C# से Excel वर्कबुक में डाल सकते हैं।

इस ट्यूटोरियल में हम पूरी प्रक्रिया को चरण‑दर‑चरण देखेंगे: वर्कबुक बनाने से, **write formula to cell** तक, **reshape array to matrix** तक, और अंत में WRAPCOLS फ़ॉर्मूला का उपयोग करके **convert 1d to 2d** तक। अंत तक आपके पास एक पुन: उपयोगी स्निपेट होगा जो किसी भी संख्यात्मक एरे के साथ काम करता है, और आप समझेंगे कि wrap columns function अक्सर मैन्युअल एरे रीशेपिंग का एक साफ़ विकल्प क्यों होता है।

## आवश्यकताएँ

* .NET 6.0 या बाद का (कोड .NET Framework 4.6+ पर भी काम करता है)  
* **Aspose.Cells for .NET** लाइब्रेरी (फ्री ट्रायल या लाइसेंस्ड कॉपी) – यह वह घटक है जो नीचे उपयोग किए गए `Workbook`, `Worksheet`, और `Cell` ऑब्जेक्ट प्रदान करता है।  
* C# सिंटैक्स की बुनियादी समझ—उन्नत Excel ज्ञान की आवश्यकता नहीं।

ये सब हैं? बढ़िया—चलिए काम शुरू करते हैं।

![Resulting 2x3 matrix after using WRAPCOLS function in C# – how to use WRAPCOLS](https://example.com/images/wrapcols-result.png "How to use WRAPCOLS – resulting 2x3 matrix")

## चरण 1: प्रोजेक्ट सेट अप करें और Aspose.Cells जोड़ें

### क्यों यह महत्वपूर्ण है

आप अपना खुद का मैट्रिक्स लॉजिक बनाने की कोशिश कर सकते हैं, लेकिन **wrap columns function** पहले से ही असमान विभाजन और खाली इनपुट जैसी किनारी स्थितियों को संभालता है। Aspose.Cells NuGet पैकेज जोड़ने से हमें एक साफ़ API मिलती है जिससे हम C# से सीधे Excel फ़ॉर्मूले के साथ इंटरैक्ट कर सकते हैं।

```bash
dotnet add package Aspose.Cells
```

*Pro tip:* यदि आप Visual Studio का उपयोग कर रहे हैं, प्रोजेक्ट पर राइट‑क्लिक करें → **Manage NuGet Packages** → **Aspose.Cells** खोजें और नवीनतम स्थिर संस्करण स्थापित करें।

## चरण 2: नई वर्कबुक बनाएं (या मौजूदा लोड करें)

अब लाइब्रेरी स्थापित हो गई है, हम एक वर्कबुक ऑब्जेक्ट बना सकते हैं। यहीं पर **write formula to cell** चरण होगा।

```csharp
using Aspose.Cells;

class WrapColsDemo
{
    static void Main()
    {
        // Step 2: Initialize a fresh workbook
        Workbook workbook = new Workbook();          // creates an empty .xls/.xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0]; // grab the first sheet
```

यहाँ हमने एक नई वर्कबुक बनाई है; यदि आपको मैट्रिक्स को पहले से फ़ॉर्मेटेड टेम्प्लेट में एम्बेड करना है तो आप `new Workbook("path/to/file.xlsx")` से मौजूदा फ़ाइल भी लोड कर सकते हैं।

## चरण 3: WRAPCOLS फ़ॉर्मूला को एक सेल में डालें

### “how to use WRAPCOLS” का मूल भाग

**WRAPCOLS** फ़ंक्शन दो आर्ग्यूमेंट लेता है: एक एरे (या रेंज) और प्रति पंक्ति आप कितनी कॉलम चाहते हैं। हमारे मामले में हम लिटरल एरे `{1,2,3,4,5,6}` को **2 पंक्तियों × 3 कॉलम** में रीशेप करेंगे।

```csharp
        // Step 3: Write the WRAPCOLS formula into cell A1
        // The formula =WRAPCOLS({1,2,3,4,5,6},3) tells Excel to wrap every 3 items into a new row.
        worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6},3)";
```

ध्यान दें कि फ़ॉर्मूला वही है जो आप Excel में टाइप करेंगे। इसे `Cells[0,0]` (सेल **A1**) में रखकर हम **writing the formula to a cell** कर रहे हैं बिना किसी अतिरिक्त सेट‑अप के।

## चरण 4: फ़ॉर्मूला के मूल्यांकन के लिए गणना को मजबूर करें

Aspose.Cells स्वचालित रूप से फ़ॉर्मूले का मूल्यांकन नहीं करता जब तक आप इसे न बताएं। यह चरण सुनिश्चित करता है कि वर्कबुक में वास्तव में रीशेप्ड मैट्रिक्स मौजूद हो।

```csharp
        // Step 4: Recalculate the workbook so the WRAPCOLS formula runs
        workbook.CalculateFormula();
```

यदि आप इस लाइन को छोड़ देते हैं, तो सेल्स में गणना किए गए मानों के बजाय फ़ॉर्मूला टेक्स्ट दिखेगा।

## चरण 5: परिणाम को पढ़ें (वैकल्पिक, लेकिन सत्यापन के लिए उपयोगी)

आप यह पुष्टि करना चाह सकते हैं कि **reshape array to matrix** ऑपरेशन सफल रहा। यहाँ एक त्वरित लूप है जो परिणामी 2‑by‑3 ग्रिड को कंसोल पर प्रिंट करता है।

```csharp
        // Step 5: Output the matrix to the console for verification
        for (int row = 0; row < 2; row++)          // we expect 2 rows
        {
            for (int col = 0; col < 3; col++)      // and 3 columns per row
            {
                var value = worksheet.Cells[row, col].StringValue;
                Console.Write(value + "\t");
            }
            Console.WriteLine();
        }

        // Optional: Save the workbook to disk to see the Excel view
        workbook.Save("WrapColsResult.xlsx");
    }
}
```

### अपेक्षित आउटपुट

```
1   2   3
4   5   6
```

कंसोल वही लेआउट दिखाता है जो आप WRAPCOLS फ़ॉर्मूला चलाने के बाद Excel में देखेंगे। यही **convert 1d to 2d** परिवर्तन का कार्यान्वयन है।

## चरण 6: किनारी स्थितियों को संभालना – यदि एरे की लंबाई कॉलम की संख्या का गुणज नहीं है तो क्या?

यदि स्रोत एरे में, उदाहरण के लिए, 7 तत्व हैं और आप 3 कॉलम चाहते हैं, तो WRAPCOLS अंतिम पंक्ति को शेष तत्व(ओं) के साथ बनाएगा और बाकी सेल्स को खाली छोड़ देगा। यहाँ एक त्वरित बदलाव है दिखाने के लिए:

```csharp
worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4,5,6,7},3)";
workbook.CalculateFormula();
```

परिणाम:

```
1   2   3
4   5   6
7       
```

**wrap columns function** अंतिम पंक्ति को खाली सेल्स से सुगमता से पैड करता है, इसलिए आपको आकार में असंगति को संभालने के लिए अतिरिक्त कोड की आवश्यकता नहीं है।

## चरण 7: डायनेमिक डेटा के साथ WRAPCOLS का उपयोग

वास्तविक प्रोजेक्ट्स में आप शायद ही एरे को हार्ड‑कोड करेंगे। इसके बजाय आप C# कलेक्शन से स्ट्रिंग प्रतिनिधित्व बनाएंगे:

```csharp
int[] numbers = Enumerable.Range(1, 12).ToArray(); // 1..12
string arrayLiteral = "{" + string.Join(",", numbers) + "}";
int columns = 4; // desired columns per row

worksheet.Cells[0, 0].Formula = $"=WRAPCOLS({arrayLiteral},{columns})";
workbook.CalculateFormula();
```

अब आप किसी भी लंबाई के लिए **converted 1d to 2d** कर चुके हैं, और आपको वही साफ़ मैट्रिक्स आउटपुट मिलता है। फ़ॉर्मूला रन‑टाइम पर बनाया जाता है, लेकिन अंतर्निहित **wrap columns function** वही रहता है।

## सामान्य गलतियाँ और प्रो टिप्स

| गलती | क्यों होता है | समाधान |
|------|--------------|--------|
| `workbook.CalculateFormula()` भूलना | Aspose.Cells फ़ॉर्मूले को अनइवैल्यूएटेड छोड़ देता है | किसी भी फ़ॉर्मूले को सेट करने के बाद हमेशा इस मेथड को कॉल करें |
| गैर‑संख्यात्मक एरे लिटरल का उपयोग | WRAPCOLS को संख्याएँ या ऐसी स्ट्रिंग्स चाहिए जो क coerced हो सकें | लिटरल में केवल संख्याएँ (या कोटेड स्ट्रिंग्स) हों यह सुनिश्चित करें |
| अनजाने में मौजूदा डेटा को ओवरराइट करना | फ़ॉर्मूला को ऐसे सेल में रखना जो पहले से डेटा रखता है | नया सेल चुनें (जैसे A1) या पहले रेंज को साफ़ करें |
| सही वर्कशीट इंडेक्स का संदर्भ न देना | `Worksheets[0]` पहला शीट है, लेकिन आपने अन्य जोड़े हो सकते हैं | आवश्यकता होने पर `worksheet = workbook.Worksheets["SheetName"];` की जाँच करें |

## क्यों WRAPCOLS मैन्युअल लूप्स से बेहतर है

* **Readability** – फ़ॉर्मूले की एक लाइन कई `for` लूप्स को बदल देती है।  
* **Performance** – Excel का नेटिव इंजन एरे फ़ॉर्मूले के लिए अत्यधिक ऑप्टिमाइज़्ड है।  
* **Maintainability** – भविष्य के डेवलपर्स तुरंत इरादा देख सकते हैं: “इन मानों को कॉलम में रैप करें”。  
* **Portability** – वही फ़ॉर्मूला वर्कबुक को Google Sheets या LibreOffice में एक्सपोर्ट करने पर भी काम करता है—कोई C#‑विशिष्ट लॉजिक आवश्यक नहीं।

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)



## संबंधित ट्यूटोरियल

- [How to Use Aspose.Cells for .NET to Show Cell Ranges as Data Labels in Charts](/cells/english/net/charts-graphs/aspose-cells-net-chart-customization-cell-ranges-data-labels/)
- [How to Use Aspose.Cells for .NET to Group Rows and Columns in Excel](/cells/english/net/data-analysis/excel-grouping-aspose-cells-net/)
- [How to Use Excel IF Function](/cells/english/java/basic-excel-functions/how-to-use-excel-if-function/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}