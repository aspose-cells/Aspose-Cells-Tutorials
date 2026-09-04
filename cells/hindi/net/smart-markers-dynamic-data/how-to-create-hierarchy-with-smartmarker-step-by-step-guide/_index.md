---
category: general
date: 2026-02-14
description: SmartMarker टेम्प्लेट्स में पदानुक्रम बनाना आपके सोचने से भी आसान है
  – पदानुक्रमित डेटा बनाना और कर्मचारियों को प्रभावी ढंग से सूचीबद्ध करना सीखें।
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: hi
og_description: SmartMarker टेम्प्लेट्स में पदानुक्रम बनाना सरल है। इस गाइड का पालन
  करके पदानुक्रमित डेटा बनाएं और नेस्टेड रेंज के साथ कर्मचारियों की सूची बनाएं।
og_title: SmartMarker के साथ पदानुक्रम कैसे बनाएं – पूर्ण गाइड
tags:
- SmartMarker
- C#
- templating
title: स्मार्टमार्कर के साथ पदानुक्रम कैसे बनाएं – चरण‑दर‑चरण मार्गदर्शिका
url: /hi/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarker के साथ पदानुक्रम कैसे बनाएं – पूर्ण गाइड

क्या आपने कभी **पदानुक्रम कैसे बनाएं** इस बारे में सोचा है, बिना सिर दर्द हुए? आप अकेले नहीं हैं। कई रिपोर्टिंग परिदृश्यों में आपको पैरेंट‑चाइल्ड संबंध चाहिए—जैसे विभाग और उनमें काम करने वाले लोग। अच्छी बात यह है कि SmartMarker सही चरणों को जानने पर इसे बहुत आसान बना देता है।

इस ट्यूटोरियल में हम पूरी प्रक्रिया को चरण‑दर‑चरण देखेंगे: C# में **पदानुक्रमिक डेटा** बनाना, नेस्टेड रेंज सक्षम करना, और अंत में एक टेम्प्लेट रेंडर करना जो प्रत्येक विभाग के **कर्मचारियों की सूची** दिखाता है। अंत तक आपके पास एक तैयार‑से‑चलाने वाला नमूना होगा जिसे आप किसी भी .NET प्रोजेक्ट में डाल सकते हैं।

---

## आपको क्या चाहिए

- .NET 6+ (कोई भी हालिया संस्करण चलेगा)
- **SmartMarker** लाइब्रेरी का रेफ़रेंस (`ws.SmartMarkerProcessor` नेमस्पेस)
- बेसिक C# ज्ञान – कुछ खास नहीं, बस कुछ ऑब्जेक्ट्स और एक‑दो लैम्ब्डा
- आपका पसंदीदा IDE या एडिटर (Visual Studio, Rider, VS Code… आप चुनें)

यदि आपके पास ये सब है, तो चलिए शुरू करते हैं।

---

## SmartMarker के साथ पदानुक्रम कैसे बनाएं – अवलोकन

मुख्य विचार यह है कि आप एक **नेस्टेड ऑब्जेक्ट ग्राफ** बनाएं जो अंतिम दस्तावेज़ में दिखने वाली संरचना को प्रतिबिंबित करे। हमारे मामले में ग्राफ़ इस प्रकार दिखता है:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker फिर `Departments` पर इटरिटेट करेगा और, क्योंकि हम **नेस्टेड रेंज प्रोसेसिंग** को चालू करेंगे, यह प्रत्येक विभाग के `Employees` कलेक्शन को भी स्वचालित रूप से लूप करेगा।

---

## चरण 1: पदानुक्रमिक डेटा मॉडल बनाएं

सबसे पहले हम एक अनाम ऑब्जेक्ट बनाते हैं जिसमें विभागों की एक एरे होती है, प्रत्येक विभाग में अपनी कर्मचारी सूची होती है। अनाम प्रकार का उपयोग उदाहरण को हल्का रखता है—बाद में आप इसे वास्तविक POCO क्लासेज़ से बदल सकते हैं।

```csharp
// Step 1: Create hierarchical data that SmartMarker will iterate over
var departmentData = new
{
    Departments = new[]
    {
        new { Name = "HR", Employees = new[] { "John", "Amy" } },
        new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
    }
};
```

> **यह क्यों महत्वपूर्ण है:** `Departments` एरे शीर्ष‑स्तर का कलेक्शन है। प्रत्येक तत्व में एक `Employees` एरे होता है, जिससे हमें दूसरा स्तर का पदानुक्रम मिलता है जिसे हम बाद में `#Departments.Employees#` से एक्सेस करेंगे।

---

## चरण 2: नेस्टेड रेंज प्रोसेसिंग सक्षम करें

SmartMarker अंदरूनी कलेक्शन्स में नहीं जाएगा जब तक आप उसे नहीं बताते। `SmartMarkerOptions` ऑब्जेक्ट इस स्विच को रखता है।

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **प्रो टिप:** यदि आप यह फ़्लैग भूल जाते हैं, तो अंदरूनी `#Employees#` रेंज कुछ भी रिटर्न नहीं करेगी, और आप सोचते रह जाएंगे कि टेम्प्लेट खाली क्यों है।

---

## चरण 3: अपने डेटा के साथ प्रोसेसर चलाएँ

अब हम डेटा और विकल्पों को प्रोसेसर को देते हैं। `ws` वेरिएबल आपके **WebService** (या वह ऑब्जेक्ट जो SmartMarker इंजन को होस्ट करता है) को दर्शाता है।

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

इस चरण पर SmartMarker टेम्प्लेट को पार्स करता है, प्रत्येक विभाग के नाम के लिए `#Departments.Name#` को प्रतिस्थापित करता है, और चूँकि नेस्टेड रेंजेस सक्षम हैं, प्रत्येक विभाग के `Employees` कलेक्शन को इटरिटेट करता है।

---

## चरण 4: टेम्प्लेट मार्कर्स बनाएं

नीचे एक न्यूनतम टेम्प्लेट है जो बाहरी और आंतरिक दोनों लूप को दर्शाता है। इसे SmartMarker टेम्प्लेट एडिटर में पेस्ट करें (या एक `.txt` फ़ाइल में जिसे आप प्रोसेसर को पास करते हैं)।

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

रेंडर होने पर आपको यह दिखेगा:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **आप क्या देख रहे हैं:** बाहरी `#Departments.Name#` विभाग का शीर्षक प्रिंट करता है। आंतरिक `#Departments.Employees#` ब्लॉक प्रत्येक कर्मचारी पर लूप करता है, और ब्लॉक के भीतर `#Departments.Employees#` वास्तविक नाम आउटपुट करता है।

---

## अपेक्षित आउटपुट और सत्यापन

पूरा उदाहरण (डेटा + विकल्प + टेम्प्लेट) चलाने पर ऊपर दिखाए गए सूची के समान आउटपुट मिलना चाहिए। जल्दी से सत्यापित करने के लिए, आप परिणाम को कंसोल में डंप कर सकते हैं:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

यदि आप दो विभाग शीर्षक और उनके बाद कर्मचारियों की बुलेट लिस्ट देखते हैं, तो आपने सफलतापूर्वक **पदानुक्रम बनाया** और **कर्मचारियों की सूची बनायी** है।

---

## सामान्य समस्याएँ और किनारे के मामले

| समस्या | क्यों होता है | समाधान |
|-------|----------------|-----|
| कर्मचारियों का कोई आउटपुट नहीं | `EnableNestedRange` को `false` रखा गया | `EnableNestedRange = true` सेट करें |
| दोहराए गए कर्मचारी नाम | एक ही एरे कई विभागों में पुन: उपयोग किया गया | एरे को क्लोन करें या अलग-अलग कलेक्शन उपयोग करें |
| बहुत बड़े पदानुक्रम मेमोरी पर दबाव डालते हैं | SmartMarker पूरे ऑब्जेक्ट ग्राफ को मेमोरी में लोड करता है | डेटा को स्ट्रीम करें या बड़े कलेक्शन को पेजिनेट करें |
| टेम्प्लेट सिंटैक्स त्रुटियाँ | बंद करने वाले `#/…#` टैग मिस हो गए | SmartMarker वैलिडेटर का उपयोग करें या छोटे टेम्प्लेट से जल्दी टेस्ट करें |

---

## आगे बढ़ें – वास्तविक‑दुनिया के वैरिएशन

1. **डायनामिक डेटा स्रोत** – डेटाबेस से विभागों को खींचें और LINQ का उपयोग करके उन्हें अनाम संरचना में मैप करें।  
2. **कंडीशनल फॉर्मेटिंग** – प्रत्येक कर्मचारी में `IsManager` फ़्लैग जोड़ें और SmartMarker के कंडीशनल टैग (`#if …#`) का उपयोग करके मैनेजर्स को हाइलाइट करें।  
3. **एक से अधिक नेस्टेड लेवल** – यदि आपको विभागों के भीतर टीमें चाहिए, तो बस एक और कलेक्शन (`Teams`) जोड़ें और `EnableNestedRange` को चालू रखें।

---

## पूर्ण कार्यशील उदाहरण (कॉपी‑पेस्ट तैयार)

```csharp
using System;
using SmartMarker; // hypothetical namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Build hierarchical data
        var departmentData = new
        {
            Departments = new[]
            {
                new { Name = "HR", Employees = new[] { "John", "Amy" } },
                new { Name = "IT", Employees = new[] { "Bob", "Eve" } }
            }
        };

        // 2️⃣ Enable nested ranges
        var smartMarkerOptions = new SmartMarkerOptions
        {
            EnableNestedRange = true
        };

        // 3️⃣ Start processing
        var ws = new WebService(); // assume this is your entry point
        ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);

        // 4️⃣ Retrieve and display the result
        string output = ws.SmartMarkerProcessor.GetProcessedResult(); // placeholder method
        Console.WriteLine(output);
    }
}
```

**टेम्प्लेट (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

प्रोग्राम चलाने पर पदानुक्रम ठीक उसी तरह प्रिंट होगा जैसा ऊपर दिखाया गया था।

---

## निष्कर्ष

हमने **SmartMarker में पदानुक्रम कैसे बनाएं** को कवर किया, C# में **पदानुक्रमिक डेटा** तैयार करने से लेकर नेस्टेड रेंजेस को चालू करने और अंत में एक टेम्प्लेट रेंडर करने तक जो प्रत्येक विभाग के **कर्मचारियों की सूची** बनाता है। यह पैटर्न स्केलेबल है—बस अधिक नेस्टेड कलेक्शन या कंडीशनल लॉजिक जोड़ें और आपके पास एक शक्तिशाली रिपोर्टिंग इंजन आपके हाथ में होगा।

अगली चुनौती के लिए तैयार हैं? अनाम टाइप्स को स्ट्रॉन्गली‑टाइप्ड POCO क्लासेज़ से बदलें, या इस फ्लो को एक ASP.NET Core एंडपॉइंट में इंटीग्रेट करें जो PDF या Word दस्तावेज़ लौटाता है। संभावनाएँ असीमित हैं, और अब आपके पास एक ठोस आधार है।

![How to create hierarchy diagram](image.png){alt="विभाग‑कर्मचारी संबंध दिखाने वाला पदानुक्रम आरेख"}

*हैप्पी कोडिंग! यदि आपको कोई समस्या आती है, तो नीचे टिप्पणी करें—मैं मदद करने के लिए तैयार हूँ।*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}