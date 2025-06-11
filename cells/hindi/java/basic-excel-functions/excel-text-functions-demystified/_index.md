---
"description": "Java के लिए Aspose.Cells के साथ Excel टेक्स्ट फ़ंक्शन के रहस्यों को अनलॉक करें। Excel में टेक्स्ट को आसानी से मैनिपुलेट करना, निकालना और बदलना सीखें।"
"linktitle": "एक्सेल टेक्स्ट फंक्शन्स का रहस्य उजागर"
"second_title": "Aspose.Cells जावा एक्सेल प्रोसेसिंग एपीआई"
"title": "एक्सेल टेक्स्ट फंक्शन्स का रहस्य उजागर"
"url": "/hi/java/basic-excel-functions/excel-text-functions-demystified/"
"weight": 18
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# एक्सेल टेक्स्ट फंक्शन्स का रहस्य उजागर


# जावा के लिए Aspose.Cells का उपयोग करके एक्सेल टेक्स्ट फ़ंक्शन का रहस्य उजागर

इस ट्यूटोरियल में, हम Aspose.Cells for Java API का उपयोग करके Excel में टेक्स्ट मैनिपुलेशन की दुनिया में गहराई से जाएंगे। चाहे आप एक अनुभवी Excel उपयोगकर्ता हों या अभी शुरुआत कर रहे हों, टेक्स्ट फ़ंक्शन को समझना आपके स्प्रेडशीट कौशल को काफी हद तक बढ़ा सकता है। हम विभिन्न टेक्स्ट फ़ंक्शन का पता लगाएंगे और उनके उपयोग को स्पष्ट करने के लिए व्यावहारिक उदाहरण प्रदान करेंगे।

## शुरू करना

शुरू करने से पहले, सुनिश्चित करें कि आपके पास Aspose.Cells for Java इंस्टॉल है। आप इसे डाउनलोड कर सकते हैं [यहाँ](https://releases.aspose.com/cells/java/)एक बार जब आप इसे सेट कर लें, तो चलिए एक्सेल टेक्स्ट फ़ंक्शन की आकर्षक दुनिया में गोता लगाते हैं।

## CONCATENATE - पाठ का संयोजन

The `CONCATENATE` फ़ंक्शन आपको अलग-अलग सेल से टेक्स्ट मर्ज करने की अनुमति देता है। आइए देखें कि जावा के लिए Aspose.Cells के साथ यह कैसे किया जाता है:

```java
// Aspose.Cells का उपयोग करके पाठ को संयोजित करने के लिए जावा कोड
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.getWorksheets().get(0);
Cell cell = worksheet.getCells().get("A1");

cell.putValue("Hello, ");
cell = worksheet.getCells().get("B1");
cell.putValue("World!");

// A1 और B1 को C1 में संयोजित करें
cell = worksheet.getCells().get("C1");
cell.setFormula("=CONCATENATE(A1,B1)");

workbook.calculateFormula();
```

अब, सेल C1 में "Hello, World!" लिखा होगा।

## बाएँ और दाएँ - पाठ निकालना

The `LEFT` और `RIGHT` फ़ंक्शन आपको टेक्स्ट स्ट्रिंग के बाएँ या दाएँ से निर्दिष्ट संख्या में वर्ण निकालने की अनुमति देते हैं। यहाँ बताया गया है कि आप उनका उपयोग कैसे कर सकते हैं:

```java
// Aspose.Cells का उपयोग करके पाठ निकालने के लिए जावा कोड
Cell cell = worksheet.getCells().get("A2");
cell.putValue("Excel Rocks!");

// पहले 5 अक्षर निकालें
cell = worksheet.getCells().get("B2");
cell.setFormula("=LEFT(A2, 5)");

// अंतिम 5 अक्षर निकालें
cell = worksheet.getCells().get("C2");
cell.setFormula("=RIGHT(A2, 5)");

workbook.calculateFormula();
```

सेल B2 में "एक्सेल" लिखा होगा, और सेल C2 में "रॉक्स!" लिखा होगा।

## LEN - अक्षर गिनना

The `LEN` फ़ंक्शन टेक्स्ट स्ट्रिंग में वर्णों की संख्या गिनता है। आइए देखें कि इसे Java के लिए Aspose.Cells के साथ कैसे उपयोग किया जाए:

```java
// Aspose.Cells का उपयोग करके वर्णों की गणना करने के लिए जावा कोड
Cell cell = worksheet.getCells().get("A3");
cell.putValue("Excel");

// वर्णों की गणना करें
cell = worksheet.getCells().get("B3");
cell.setFormula("=LEN(A3)");

workbook.calculateFormula();
```

सेल B3 में "5" होगा, क्योंकि "Excel" में 5 अक्षर होते हैं।

## ऊपरी और निचला - बदलता मामला

The `UPPER` और `LOWER` फ़ंक्शन आपको टेक्स्ट को अपरकेस या लोअरकेस में बदलने की अनुमति देते हैं। आप यह कैसे कर सकते हैं:

```java
// Aspose.Cells का उपयोग करके केस बदलने के लिए जावा कोड
Cell cell = worksheet.getCells().get("A4");
cell.putValue("java programming");

// अपरकेस में बदलें
cell = worksheet.getCells().get("B4");
cell.setFormula("=UPPER(A4)");

// लोअरकेस में बदलें
cell = worksheet.getCells().get("C4");
cell.setFormula("=LOWER(A4)");

workbook.calculateFormula();
```

सेल B4 में "जावा प्रोग्रामिंग" होगा, और सेल C4 में "जावा प्रोग्रामिंग" होगा।

## खोजें और बदलें - पाठ का पता लगाना और प्रतिस्थापित करना

The `FIND` फ़ंक्शन आपको एक स्ट्रिंग के भीतर एक विशिष्ट वर्ण या पाठ की स्थिति का पता लगाने की अनुमति देता है, जबकि `REPLACE` फ़ंक्शन आपको टेक्स्ट बदलने में मदद करता है। आइए उन्हें क्रियान्वित होते हुए देखें:

```java
// Aspose.Cells का उपयोग करके खोजने और बदलने के लिए जावा कोड
Cell cell = worksheet.getCells().get("A5");
cell.putValue("Search for me");

// "के लिए" की स्थिति का पता लगाएं
cell = worksheet.getCells().get("B5");
cell.setFormula("=FIND(\"for\", A5)");

// "के लिए" को "के साथ" से बदलें
cell = worksheet.getCells().get("C5");
cell.setFormula("=REPLACE(A5, B5, 3, \"with\")");

workbook.calculateFormula();
```

सेल B5 में "9" ('के लिए' की स्थिति) होगा, और सेल C5 में "मेरे साथ खोजें" होगा।

## निष्कर्ष

Excel में टेक्स्ट फ़ंक्शन टेक्स्ट डेटा में हेरफेर और विश्लेषण करने के लिए शक्तिशाली उपकरण हैं। Aspose.Cells for Java के साथ, आप इन फ़ंक्शन को अपने Java अनुप्रयोगों में आसानी से शामिल कर सकते हैं, टेक्स्ट-संबंधित कार्यों को स्वचालित कर सकते हैं और अपनी Excel क्षमताओं को बढ़ा सकते हैं। Aspose.Cells for Java के साथ अधिक टेक्स्ट फ़ंक्शन एक्सप्लोर करें और Excel की पूरी क्षमता को उजागर करें।

## पूछे जाने वाले प्रश्न

### मैं एकाधिक कक्षों से पाठ को कैसे संयोजित करूँ?

एकाधिक कक्षों से पाठ को संयोजित करने के लिए, का उपयोग करें `CONCATENATE` फ़ंक्शन.उदाहरण के लिए:
```java
Cell cell = worksheet.getCells().get("A1");
cell.setFormula("=CONCATENATE(A1, B1)");
```

### क्या मैं किसी टेक्स्ट स्ट्रिंग से पहला और अंतिम अक्षर निकाल सकता हूँ?

हां, आप इसका उपयोग कर सकते हैं `LEFT` और `RIGHT` टेक्स्ट स्ट्रिंग की शुरुआत या अंत से अक्षर निकालने के लिए फ़ंक्शन। उदाहरण के लिए:
```java
Cell cell = worksheet.getCells().get("A2");
cell.setFormula("=LEFT(A2, 5)");
```

### मैं किसी टेक्स्ट स्ट्रिंग में वर्णों की गणना कैसे कर सकता हूँ?

उपयोग `LEN` टेक्स्ट स्ट्रिंग में वर्णों की गणना करने के लिए फ़ंक्शन। उदाहरण के लिए:
```java
Cell cell = worksheet.getCells().get("A3");
cell.setFormula("=LEN(A3)");
```

### क्या टेक्स्ट का केस बदलना संभव है?

हां, आप इसका उपयोग करके टेक्स्ट को अपरकेस या लोअरकेस में बदल सकते हैं `UPPER` और `LOWER` कार्य.उदाहरण के लिए:
```java
Cell cell = worksheet.getCells().get("A4");
cell.setFormula("=UPPER(A4)");
```

### मैं किसी स्ट्रिंग में टेक्स्ट कैसे ढूंढूं और प्रतिस्थापित करूं?

किसी स्ट्रिंग में टेक्स्ट ढूंढने और बदलने के लिए, का उपयोग करें `FIND` और `REPLACE` कार्य.उदाहरण के लिए:
```java
Cell cell = worksheet.getCells().get("A5");
cell.setFormula("=FIND(\"for\", A5)");
```

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}