---
title: कस्टम डेटा सत्यापन बनाना
linktitle: कस्टम डेटा सत्यापन बनाना
second_title: Aspose.Cells जावा एक्सेल प्रोसेसिंग एपीआई
description: Java के लिए Aspose.Cells का उपयोग करके कस्टम डेटा सत्यापन बनाना सीखें। स्रोत कोड के साथ चरण-दर-चरण मार्गदर्शिका।
weight: 10
url: /hi/java/data-validation-rules/creating-custom-data-validation/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# कस्टम डेटा सत्यापन बनाना


## परिचय

डेटा सत्यापन उपयोगकर्ताओं को Excel स्प्रेडशीट में गलत या अमान्य डेटा दर्ज करने से रोककर डेटा अखंडता बनाए रखने में मदद करता है। जबकि Excel अंतर्निहित डेटा सत्यापन विकल्प प्रदान करता है, ऐसे परिदृश्य हैं जहाँ आपको कस्टम सत्यापन नियम परिभाषित करने की आवश्यकता होती है। Aspose.Cells for Java आपको इसे कुशलतापूर्वक प्राप्त करने में सक्षम बनाता है।

## आवश्यक शर्तें

कोड में आगे बढ़ने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित पूर्वापेक्षाएँ हैं:

-  Aspose.Cells for Java: लाइब्रेरी को डाउनलोड करें और इंस्टॉल करें[यहाँ](https://releases.aspose.com/cells/java/).

## चरण 1: अपना जावा प्रोजेक्ट सेट अप करना

आरंभ करने के लिए, अपने पसंदीदा एकीकृत विकास वातावरण (IDE) में एक नया जावा प्रोजेक्ट बनाएँ। अपने प्रोजेक्ट के क्लासपाथ में Aspose.Cells for Java लाइब्रेरी जोड़ें।

## चरण 2: एक्सेल वर्कबुक बनाना

आइए, Java के लिए Aspose.Cells का उपयोग करके एक नई Excel कार्यपुस्तिका बनाकर शुरुआत करें।

```java
// नई Excel कार्यपुस्तिका बनाने के लिए जावा कोड
Workbook workbook = new Workbook();
```

## चरण 3: वर्कशीट जोड़ना

अब, कार्यपुस्तिका में एक वर्कशीट जोड़ें जहां हम अपना कस्टम डेटा सत्यापन लागू करेंगे।

```java
// वर्कशीट जोड़ने के लिए जावा कोड
Worksheet worksheet = workbook.getWorksheets().get(0);
```

## चरण 4: कस्टम सत्यापन मानदंड परिभाषित करना

इस चरण में, हम कस्टम सत्यापन मानदंड निर्धारित करेंगे जिसका हमारे डेटा को पालन करना होगा। मान लें कि हम किसी सेल में दर्ज की गई आयु को 18 से 60 के बीच सीमित करना चाहते हैं।

```java
// कस्टम सत्यापन मानदंड परिभाषित करने के लिए जावा कोड
Validation validation = worksheet.getValidations().add();
validation.setType(ValidationType.WHOLE);
validation.setOperator(OperatorType.BETWEEN);
validation.setFormula1("18");
validation.setFormula2("60");
validation.setShowError(true);
validation.setAlertStyle(ValidationAlertType.STOP);
validation.setErrorTitle("Invalid Age");
validation.setErrorMessage("Age must be between 18 and 60.");
```

## चरण 5: किसी रेंज पर डेटा सत्यापन लागू करना

अब जबकि हमने अपना कस्टम सत्यापन मानदंड परिभाषित कर लिया है, तो आइए इसे कक्षों की एक विशिष्ट श्रेणी पर लागू करें।

```java
// किसी श्रेणी में डेटा सत्यापन लागू करने के लिए जावा कोड
CellArea area = new CellArea();
area.startRow = 0;
area.startColumn = 0;
area.endRow = 9; // पहली दस पंक्तियों पर सत्यापन लागू करें
area.endColumn = 0;

validation.addArea(area);
```

## चरण 6: एक्सेल फ़ाइल को सेव करना

अंत में, कस्टम डेटा सत्यापन नियमों के साथ एक्सेल फ़ाइल को सेव करें।

```java
// एक्सेल फ़ाइल को सेव करने के लिए जावा कोड
workbook.save("CustomDataValidation.xlsx");
```

## निष्कर्ष

इस ट्यूटोरियल में, हमने जावा के लिए Aspose.Cells का उपयोग करके कस्टम डेटा सत्यापन नियम बनाने का तरीका खोजा है। इन चरणों का पालन करके, आप यह सुनिश्चित कर सकते हैं कि आपका एक्सेल डेटा विशिष्ट मानदंडों का पालन करता है, जिससे डेटा अखंडता और सटीकता बढ़ती है।

## अक्सर पूछे जाने वाले प्रश्न

### मैं Java के लिए Aspose.Cells कैसे डाउनलोड करूं?

 आप वेबसाइट से Java के लिए Aspose.Cells डाउनलोड कर सकते हैं[यहाँ](https://releases.aspose.com/cells/java/).

### क्या मैं एक ही वर्कशीट में एकाधिक श्रेणियों पर कस्टम डेटा सत्यापन लागू कर सकता हूँ?

हां, आप प्रत्येक वांछित श्रेणी के लिए चरण 5 को दोहराकर एक ही वर्कशीट में एकाधिक श्रेणियों पर कस्टम डेटा सत्यापन लागू कर सकते हैं।

### क्या Java के लिए Aspose.Cells द्वारा समर्थित अन्य प्रकार के डेटा सत्यापन हैं?

हां, Java के लिए Aspose.Cells विभिन्न प्रकार के डेटा सत्यापन का समर्थन करता है, जिसमें पूर्ण संख्या, दशमलव, दिनांक, समय, पाठ की लंबाई और बहुत कुछ शामिल है।

### डेटा सत्यापन विफल होने पर प्रदर्शित त्रुटि संदेश को मैं कैसे अनुकूलित कर सकता हूं?

 आप त्रुटि संदेश को संशोधित करके अनुकूलित कर सकते हैं`setErrorMessage` चरण 4 में विधि, जहाँ आप सत्यापन मानदंड परिभाषित करते हैं।

### क्या Aspose.Cells for Java विभिन्न प्रारूपों में Excel फ़ाइलों के साथ काम करता है?

हां, Java के लिए Aspose.Cells XLS, XLSX, XLSM, और अधिक सहित एक्सेल फ़ाइल स्वरूपों की एक विस्तृत श्रृंखला का समर्थन करता है।
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
