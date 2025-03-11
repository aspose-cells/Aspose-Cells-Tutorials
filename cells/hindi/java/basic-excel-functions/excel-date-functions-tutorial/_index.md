---
title: एक्सेल दिनांक फ़ंक्शन ट्यूटोरियल
linktitle: एक्सेल दिनांक फ़ंक्शन ट्यूटोरियल
second_title: Aspose.Cells जावा एक्सेल प्रोसेसिंग एपीआई
description: जावा के लिए Aspose.Cells का उपयोग करके Excel दिनांक फ़ंक्शन सीखें। स्रोत कोड के साथ चरण-दर-चरण ट्यूटोरियल देखें।
weight: 19
url: /hi/java/basic-excel-functions/excel-date-functions-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# एक्सेल दिनांक फ़ंक्शन ट्यूटोरियल


## एक्सेल दिनांक फ़ंक्शन ट्यूटोरियल का परिचय

इस व्यापक ट्यूटोरियल में, हम एक्सेल डेट फ़ंक्शन और जावा के लिए Aspose.Cells की शक्ति का लाभ उठाने के तरीके के बारे में जानेंगे ताकि डेट-संबंधित डेटा के साथ काम किया जा सके। चाहे आप एक अनुभवी डेवलपर हों या Aspose.Cells के साथ अभी शुरुआत कर रहे हों, यह गाइड आपको एक्सेल में डेट फ़ंक्शन की क्षमता का दोहन करने में मदद करेगी। तो, चलिए शुरू करते हैं!

## एक्सेल में दिनांक फ़ंक्शन को समझना

एक्सेल में तारीख संबंधी कई फ़ंक्शन हैं जो जटिल तारीख संबंधी गणनाओं को सरल बनाते हैं। ये फ़ंक्शन तारीख अंकगणित, तारीखों के बीच अंतर खोजने और अन्य कार्यों के लिए अविश्वसनीय रूप से उपयोगी हैं। आइए कुछ सामान्य तारीख फ़ंक्शन देखें:

### दिनांक फ़ंक्शन

DATE फ़ंक्शन दिए गए वर्ष, महीने और दिन के मानों का उपयोग करके एक तिथि बनाता है। हम दिखाएंगे कि इसे Java के लिए Aspose.Cells के साथ कैसे उपयोग किया जाए।

### आज का समारोह

TODAY फ़ंक्शन वर्तमान दिनांक लौटाता है। Aspose.Cells का उपयोग करके प्रोग्रामेटिक रूप से इस जानकारी को प्राप्त करना सीखें।

### DATEDIF फ़ंक्शन

DATEDIF दो तिथियों के बीच अंतर की गणना करता है, परिणाम को विभिन्न इकाइयों (जैसे, दिन, महीने, वर्ष) में प्रदर्शित करता है। जानें कि Java के लिए Aspose.Cells के साथ इस फ़ंक्शन को कैसे लागू किया जाए।

### EOMONTH फ़ंक्शन

EOMONTH किसी दी गई तिथि के लिए महीने का अंतिम दिन लौटाता है। Aspose.Cells के साथ महीने के अंत की तिथि प्राप्त करने का तरीका जानें।

## Java के लिए Aspose.Cells के साथ कार्य करना

अब जबकि हमने Excel दिनांक फ़ंक्शन की मूल बातें कवर कर ली हैं, तो आइए इन फ़ंक्शन के साथ प्रोग्रामेटिक रूप से काम करने के लिए Java के लिए Aspose.Cells का उपयोग करना शुरू करें।

### Aspose.Cells की स्थापना

कोडिंग शुरू करने से पहले, हमें अपने प्रोजेक्ट में Java के लिए Aspose.Cells सेट अप करना होगा। आरंभ करने के लिए इन चरणों का पालन करें।

1. Aspose.Cells डाउनलोड और इंस्टॉल करें: पर जाएँ[जावा के लिए Aspose.Cells](https://releases.aspose.com/cells/java/) और नवीनतम संस्करण डाउनलोड करें.

2. अपने प्रोजेक्ट में Aspose.Cells शामिल करें: अपने जावा प्रोजेक्ट में Aspose.Cells लाइब्रेरी जोड़ें।

3. लाइसेंस कॉन्फ़िगरेशन: सुनिश्चित करें कि आपके पास Aspose.Cells का उपयोग करने के लिए वैध लाइसेंस है।

### Aspose.Cells के साथ DATE फ़ंक्शन का उपयोग करना

आइए, Java के लिए Aspose.Cells का उपयोग करके Excel में DATE फ़ंक्शन का उपयोग करने के व्यावहारिक उदाहरण से शुरुआत करें।

```java
// नई कार्यपुस्तिका बनाएँ
Workbook workbook = new Workbook();

// पहली वर्कशीट तक पहुँचें
Worksheet worksheet = workbook.getWorksheets().get(0);

// DATE फ़ंक्शन का उपयोग करके दिनांक सेट करें
worksheet.getCells().get("A1").putValue("=DATE(2023, 9, 7)");

// गणना की गई तिथि मान प्राप्त करें
String calculatedDate = worksheet.getCells().get("A1").getStringValue();

// परिणाम प्रिंट करें
System.out.println("Calculated Date: " + calculatedDate);
```

### TODAY फ़ंक्शन के साथ कार्य करना

अब, आइए जानें कि Java के लिए Aspose.Cells के साथ TODAY फ़ंक्शन का उपयोग करके वर्तमान दिनांक कैसे प्राप्त करें।

```java
// नई कार्यपुस्तिका बनाएँ
Workbook workbook = new Workbook();

// पहली वर्कशीट तक पहुँचें
Worksheet worksheet = workbook.getWorksheets().get(0);

// वर्तमान दिनांक प्राप्त करने के लिए TODAY फ़ंक्शन का उपयोग करें
worksheet.getCells().get("A1").setFormula("=TODAY()");

// वर्तमान दिनांक मान प्राप्त करें
String currentDate = worksheet.getCells().get("A1").getStringValue();

// परिणाम प्रिंट करें
System.out.println("Current Date: " + currentDate);
```

### DATEDIF के साथ तिथि अंतर की गणना करना

आप Excel में DATEDIF फ़ंक्शन के साथ आसानी से दिनांक अंतर की गणना कर सकते हैं। यहाँ बताया गया है कि Java के लिए Aspose.Cells का उपयोग करके इसे कैसे करें।

```java
// नई कार्यपुस्तिका बनाएँ
Workbook workbook = new Workbook();

// पहली वर्कशीट तक पहुँचें
Worksheet worksheet = workbook.getWorksheets().get(0);

// दो दिनांक मान सेट करें
worksheet.getCells().get("A1").putValue("2023-09-07");
worksheet.getCells().get("A2").putValue("2023-08-01");

// DATEDIF का उपयोग करके अंतर की गणना करें
worksheet.getCells().get("A3").setFormula("=DATEDIF(A1, A2, \"d\")");

//दिनों में अंतर जानें
int daysDifference = worksheet.getCells().get("A3").getIntValue();

// परिणाम प्रिंट करें
System.out.println("Days Difference: " + daysDifference);
```

### महीने का अंत ढूँढना

Java के लिए Aspose.Cells के साथ, आप EOMONTH फ़ंक्शन का उपयोग करके किसी दी गई तारीख के लिए महीने का अंत आसानी से पा सकते हैं।

```java
// नई कार्यपुस्तिका बनाएँ
Workbook workbook = new Workbook();

// पहली वर्कशीट तक पहुँचें
Worksheet worksheet = workbook.getWorksheets().get(0);

// दिनांक मान सेट करें
worksheet.getCells().get("A1").putValue("2023-09-07");

// EOMONTH का उपयोग करके महीने के अंत की गणना करें
worksheet.getCells().get("A2").setFormula("=EOMONTH(A1, 0)");

// महीने के अंत की तारीख प्राप्त करें
String endOfMonth = worksheet.getCells().get("A2").getStringValue();

// परिणाम प्रिंट करें
System.out.println("End of Month: " + endOfMonth);
```

## निष्कर्ष

इस ट्यूटोरियल में एक्सेल डेट फंक्शन का विस्तृत अवलोकन दिया गया है और जावा के लिए Aspose.Cells का उपयोग करके उनके साथ काम करने का तरीका बताया गया है। आपने सीखा है कि Aspose.Cells को कैसे सेट अप करें, DATE, TODAY, DATEDIF और EOMONTH फंक्शन का उपयोग कैसे करें और प्रोग्रामेटिक रूप से डेट कैलकुलेशन कैसे करें। इस ज्ञान के साथ, आप एक्सेल में अपने दिनांक-संबंधी कार्यों को सुव्यवस्थित कर सकते हैं और अपने जावा अनुप्रयोगों को बढ़ा सकते हैं।

## अक्सर पूछे जाने वाले प्रश्न

### मैं Java के लिए Aspose.Cells में दिनांकों को कैसे प्रारूपित करूं?

 Aspose.Cells में तिथियों को फ़ॉर्मेट करना सरल है। आप इसका उपयोग कर सकते हैं`Style` दिनांक स्वरूपों को परिभाषित करने और उन्हें कक्षों पर लागू करने के लिए क्लास। उदाहरण के लिए, दिनांकों को "dd-MM-yyyy" स्वरूप में प्रदर्शित करने के लिए:

```java
// दिनांक शैली बनाएँ
Style dateStyle = workbook.createStyle();
dateStyle.setCustom("dd-MM-yyyy");

// किसी सेल पर शैली लागू करें
worksheet.getCells().get("A1").setStyle(dateStyle);
```

### क्या मैं Aspose.Cells के साथ उन्नत दिनांक गणना कर सकता हूँ?

हां, आप Aspose.Cells के साथ उन्नत तिथि गणना कर सकते हैं। Excel दिनांक फ़ंक्शन और Aspose.Cells API को संयोजित करके, आप जटिल तिथि-संबंधी कार्यों को कुशलतापूर्वक संभाल सकते हैं।

### क्या Aspose.Cells बड़े पैमाने पर दिनांक प्रसंस्करण के लिए उपयुक्त है?

Aspose.Cells for Java छोटे पैमाने और बड़े पैमाने पर दिनांक प्रसंस्करण दोनों के लिए उपयुक्त है। यह उच्च प्रदर्शन और विश्वसनीयता प्रदान करता है, जो इसे विभिन्न अनुप्रयोगों में दिनांक-संबंधित डेटा को संभालने के लिए एक उत्कृष्ट विकल्प बनाता है।

### मैं Aspose.Cells for Java के लिए और अधिक संसाधन और दस्तावेज़ कहां पा सकता हूं?

 आप Aspose.Cells for Java के लिए व्यापक दस्तावेज़ और संसाधनों तक पहुँच सकते हैं[यहाँ](https://reference.aspose.com/cells/java/).

### मैं Java के लिए Aspose.Cells के साथ कैसे शुरुआत कर सकता हूं?

 Java के लिए Aspose.Cells के साथ आरंभ करने के लिए, लाइब्रेरी को यहां से डाउनलोड करें[यहाँ](https://releases.aspose.com/cells/java/) और स्थापना के लिए दस्तावेज़ देखें और
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
