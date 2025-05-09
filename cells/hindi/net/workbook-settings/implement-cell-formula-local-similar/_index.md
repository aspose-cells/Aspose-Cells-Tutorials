---
"description": "जानें कि Aspose.Cells for .NET में श्रेणी सूत्र स्थानीय कार्यक्षमता के समान सेल सूत्र को कैसे लागू किया जाए। अंतर्निहित Excel फ़ंक्शन नामों और अधिक को कस्टमाइज़ करना सीखें।"
"linktitle": "सेल फॉर्मूला लोकल को रेंज फॉर्मूला लोकल के समान लागू करें"
"second_title": "Aspose.Cells .NET एक्सेल प्रोसेसिंग API"
"title": "सेल फॉर्मूला लोकल को रेंज फॉर्मूला लोकल के समान लागू करें"
"url": "/hi/net/workbook-settings/implement-cell-formula-local-similar/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# सेल फॉर्मूला लोकल को रेंज फॉर्मूला लोकल के समान लागू करें

## परिचय
Aspose.Cells for .NET एक शक्तिशाली और लचीला स्प्रेडशीट मैनिपुलेशन API है जो आपको प्रोग्रामेटिक रूप से Excel फ़ाइलें बनाने, उनमें हेरफेर करने और उन्हें परिवर्तित करने की अनुमति देता है। Aspose.Cells द्वारा प्रदान की जाने वाली कई विशेषताओं में से एक अंतर्निहित Excel फ़ंक्शन के व्यवहार को अनुकूलित करने की क्षमता है, जिसमें आपके स्वयं के स्थानीय फ़ंक्शन नाम बनाने की क्षमता भी शामिल है। इस ट्यूटोरियल में, हम आपको Aspose.Cells for .NET में श्रेणी फ़ॉर्मूला स्थानीय कार्यक्षमता के समान सेल फ़ॉर्मूला को लागू करने के चरणों के माध्यम से चलेंगे।
## आवश्यक शर्तें
आरंभ करने से पहले, सुनिश्चित करें कि आपके पास निम्नलिखित हैं:
1. आपके सिस्टम पर Microsoft Visual Studio 2010 या बाद का संस्करण स्थापित होना चाहिए।
2. आपके प्रोजेक्ट में Aspose.Cells for .NET लाइब्रेरी का नवीनतम संस्करण स्थापित है। आप लाइब्रेरी को यहाँ से डाउनलोड कर सकते हैं [Aspose.Cells for .NET डाउनलोड पृष्ठ](https://releases.aspose.com/cells/net/).
## पैकेज आयात करें
आरंभ करने के लिए, आपको अपने C# प्रोजेक्ट में आवश्यक पैकेज आयात करने होंगे। अपनी कोड फ़ाइल के शीर्ष पर निम्नलिखित using कथन जोड़ें:
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## चरण 1: कस्टम ग्लोबलाइज़ेशन सेटिंग क्लास बनाएँ
पहला कदम एक कस्टम बनाना है `GlobalizationSettings` क्लास जो आपको एक्सेल फ़ंक्शन के डिफ़ॉल्ट व्यवहार को ओवरराइड करने की अनुमति देगा। इस उदाहरण में, हम के नाम बदलेंगे `SUM` और `AVERAGE` कार्यों के लिए `UserFormulaLocal_SUM` और `UserFormulaLocal_AVERAGE`, क्रमश।
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //अपनी आवश्यकतानुसार SUM फ़ंक्शन का नाम बदलें।
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //अपनी आवश्यकतानुसार AVERAGE फ़ंक्शन का नाम बदलें।
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## चरण 2: एक नई कार्यपुस्तिका बनाएं और कस्टम ग्लोबलाइज़ेशन सेटिंग्स असाइन करें
इसके बाद, एक नई कार्यपुस्तिका इंस्टेंस बनाएं और कस्टम असाइन करें `GlobalizationSettings` कार्यान्वयन वर्ग को कार्यपुस्तिका में जोड़ें `Settings.GlobalizationSettings` संपत्ति।
```csharp
//कार्यपुस्तिका बनाएं
Workbook wb = new Workbook();
//GlobalizationSettings कार्यान्वयन वर्ग असाइन करें
wb.Settings.GlobalizationSettings = new GS();
```
## चरण 3: पहली वर्कशीट और एक सेल तक पहुँचें
अब, आइए कार्यपुस्तिका में पहली वर्कशीट और उस वर्कशीट के भीतर एक विशिष्ट सेल तक पहुँचें।
```csharp
//पहली वर्कशीट तक पहुंचें
Worksheet ws = wb.Worksheets[0];
//कुछ सेल तक पहुंचें
Cell cell = ws.Cells["C4"];
```
## चरण 4: सूत्र निर्दिष्ट करें और सूत्र मुद्रित करेंस्थानीय
अंत में, आइए असाइन करें `SUM` और `AVERAGE` सेल में सूत्र डालें और परिणामी परिणाम प्रिंट करें `FormulaLocal` मूल्य.
```csharp
//SUM फ़ॉर्मूला असाइन करें और उसका फ़ॉर्मूला प्रिंट करेंLocal
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//औसत सूत्र निर्दिष्ट करें और उसका FormulaLocal प्रिंट करें
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## निष्कर्ष
इस ट्यूटोरियल में, आपने सीखा है कि सेल फ़ॉर्मूला को कैसे लागू किया जाए जो कि Aspose.Cells for .NET में रेंज फ़ॉर्मूला लोकल कार्यक्षमता के समान है। कस्टम बनाकर `GlobalizationSettings` क्लास में, आप एक्सेल फ़ंक्शन के डिफ़ॉल्ट व्यवहार को ओवरराइड कर सकते हैं और अपनी ज़रूरतों के हिसाब से स्थानीय फ़ंक्शन नामों को कस्टमाइज़ कर सकते हैं। स्थानीयकृत या अंतर्राष्ट्रीयकृत एक्सेल दस्तावेज़ों के साथ काम करते समय यह विशेष रूप से उपयोगी हो सकता है।
## अक्सर पूछे जाने वाले प्रश्न
### इसका उद्देश्य क्या है? `GlobalizationSettings` Aspose.Cells में क्लास?
The `GlobalizationSettings` Aspose.Cells में क्लास आपको अंतर्निहित Excel फ़ंक्शन के व्यवहार को अनुकूलित करने की अनुमति देता है, जिसमें स्थानीय फ़ंक्शन नाम बदलने की क्षमता भी शामिल है।
### क्या मैं के अलावा अन्य कार्यों के व्यवहार को ओवरराइड कर सकता हूँ `SUM` और `AVERAGE`?
हां, आप किसी भी अंतर्निहित एक्सेल फ़ंक्शन के व्यवहार को संशोधित करके ओवरराइड कर सकते हैं `GetLocalFunctionName` अपने कस्टम में विधि `GlobalizationSettings` कक्षा।
### क्या फ़ंक्शन नामों को उनके डिफ़ॉल्ट मानों पर रीसेट करने का कोई तरीका है?
हां, आप कस्टम को हटाकर फ़ंक्शन नामों को रीसेट कर सकते हैं `GlobalizationSettings` क्लास से या खाली स्ट्रिंग लौटाकर `GetLocalFunctionName` तरीका।
### क्या मैं इस सुविधा का उपयोग Aspose.Cells में कस्टम फ़ंक्शन बनाने के लिए कर सकता हूँ?
नहीं, `GlobalizationSettings` क्लास को बिल्ट-इन एक्सेल फ़ंक्शन के व्यवहार को ओवरराइड करने के लिए डिज़ाइन किया गया है, न कि कस्टम फ़ंक्शन बनाने के लिए। यदि आपको कस्टम फ़ंक्शन बनाने की आवश्यकता है, तो आप इसका उपयोग कर सकते हैं `UserDefinedFunction` Aspose.Cells में वर्ग.
### क्या यह सुविधा .NET के लिए Aspose.Cells के सभी संस्करणों में उपलब्ध है?
हां `GlobalizationSettings` क्लास और फ़ंक्शन नामों को अनुकूलित करने की क्षमता .NET के लिए Aspose.Cells के सभी संस्करणों में उपलब्ध है।


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}