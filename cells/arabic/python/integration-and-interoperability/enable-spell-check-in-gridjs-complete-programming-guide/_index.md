---
category: general
date: 2026-06-30
description: تفعيل التدقيق الإملائي في GridJs وتعلم كيفية تفعيل التدقيق النحوي، وضبط
  لغة التدقيق، واسترجاع إعدادات العميل في دليل واحد.
draft: false
keywords:
- enable spell check
- how to enable spell check
- how to enable syntax check
- how to set spell language
- retrieve client config
language: ar
og_description: فعّل التدقيق الإملائي في GridJs وتعرّف على كيفية تفعيل فحص الصياغة،
  وضبط لغة التدقيق، واسترجاع إعدادات العميل في دليل واحد.
og_title: تمكين التدقيق الإملائي في GridJs – دليل البرمجة الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Enable spell check in GridJs and learn how to enable syntax check,
    set spell language, and retrieve client config in a single walkthrough.
  headline: Enable Spell Check in GridJs – Complete Programming Guide
  type: TechArticle
- description: Enable spell check in GridJs and learn how to enable syntax check,
    set spell language, and retrieve client config in a single walkthrough.
  name: Enable Spell Check in GridJs – Complete Programming Guide
  steps:
  - name: '**Creating the `GridJs` instance** gives you a fresh context where all
      settings start from defaults.'
    text: '**Creating the `GridJs` instance** gives you a fresh context where all
      settings start from defaults.'
  - name: '**Binding the worksheet** (`set_worksheet`) tells GridJs which sheet the
      helpers should monitor. Without this, the helpers have nothing to act upon.'
    text: '**Binding the worksheet** (`set_worksheet`) tells GridJs which sheet the
      helpers should monitor. Without this, the helpers have nothing to act upon.'
  - name: '**Enabling syntax check** (`how to enable syntax check`) adds a lightweight
      parser that underlines malformed formulas, saving you from runtime errors later.'
    text: '**Enabling syntax check** (`how to enable syntax check`) adds a lightweight
      parser that underlines malformed formulas, saving you from runtime errors later.'
  - name: '**Turning on spell check** (`enable spell check`) highlights misspelled
      words in cell comments and plain‑text cells. Setting the language (`how to set
      spell language`) ensures the dictionary matches your locale—critical for non‑English
      sheets.'
    text: '**Turning on spell check** (`enable spell check`) highlights misspelled
      words in cell comments and plain‑text cells. Setting the language (`how to set
      spell language`) ensures the dictionary matches your locale—critical for non‑English
      sheets.'
  - name: '**Retrieving the client config** (`retrieve client config`) gives you a
      JSON snapshot of all active settings. You can store this JSON in a database,
      send it to a front‑end, or simply log it for debugging.'
    text: '**Retrieving the client config** (`retrieve client config`) gives you a
      JSON snapshot of all active settings. You can store this JSON in a database,
      send it to a front‑end, or simply log it for debugging.'
  type: HowTo
tags:
- GridJs
- Python
- Spreadsheet Automation
title: تمكين التدقيق الإملائي في GridJs – دليل برمجي كامل
url: /ar/python/integration-and-interoperability/enable-spell-check-in-gridjs-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تمكين التدقيق الإملائي في GridJs – دليل برمجة كامل

هل تساءلت يومًا **كيف يتم تمكين التدقيق الإملائي** لورقة عمل GridJs دون الغوص في وثائق لا نهائية؟ لست وحدك. في هذا الدرس سنستعرض الخطوات الدقيقة لتفعيل التدقيق الإملائي، وتمكين فحص الصياغة، وتعيين لغة التدقيق الإملائي، وأخيرًا سحب تكوين العميل بصيغة JSON لتتمكن من فحصه أو حفظ الإعدادات.

وبالطبع، سنغطي أيضًا **كيف يتم تمكين فحص الصياغة** لأن معظم المطورين يحتاجون إلى كلا المساعدين جنبًا إلى جنب. بنهاية هذا الدليل ستحصل على سكريبت جاهز للتنفيذ يمكنك إدراجه في أي مشروع يستخدم GridJs Python API.

## ما ستتعلمه

- تهيئة كائن `GridJs` وربطه بورقة عمل.  
- تشغيل **مساعد التدقيق الإملائي** (`enable spell check`).  
- تفعيل **مساعد فحص الصياغة** (`how to enable syntax check`).  
- تغيير لغة التدقيق الإملائي (`how to set spell language`).  
- استخراج تكوين العميل الكامل (`retrieve client config`).  

لا توجد مكتبات خارجية مطلوبة بخلاف GridJs، ويعمل الكود مع Python 3.9+.

---

## المتطلبات المسبقة

- Python 3.9 أو أحدث مثبت على جهازك.  
- رخصة GridJs صالحة أو تجربة مجانية تسمح لك بإنشاء كائن `gridjs.GridJs`.  
- إلمام أساسي بدوال وكائنات Python.  

إذا كان لديك بالفعل كائن ورقة عمل (`ws`) من جدول البيانات الخاص بك، فأنت جاهز للبدء. وإلا، أنشئ واحدًا باستخدام واجهة برمجة تطبيقات دفتر العمل في GridJs – هذا الجزء خارج نطاق هذا الدليل لكنه مغطى في الوثائق الرسمية.

---

## تمكين التدقيق الإملائي وفحص الصياغة في GridJs

فيما يلي **السكريبت الكامل القابل للتنفيذ** الذي يوضح كل ميزة ناقشناها. لا تتردد في نسخه ولصقه في ملف جديد يُسمى `gridjs_helpers.py` وتشغيله.

```python
# gridjs_helpers.py
import json
import gridjs  # Make sure the GridJs Python package is installed

def configure_gridjs(worksheet):
    """
    Sets up spell‑check and syntax‑check helpers for a given worksheet,
    then returns the client configuration as a formatted JSON string.
    """
    # Step 1: Create a GridJs instance
    grid = gridjs.GridJs()

    # Step 2: Associate the worksheet you want to work with
    grid.set_worksheet(worksheet)

    # Step 3: Enable the syntax‑check helper to underline formula errors
    grid.settings.syntax_check.enabled = True

    # Step 4: Enable the spell‑check helper and optionally set its language
    grid.settings.spell_check.enabled = True                # how to enable spell check
    grid.settings.spell_check.language = "en-US"            # how to set spell language

    # Step 5: Retrieve the client configuration JSON and display it
    config_json = grid.get_client_config()
    # Pretty‑print for readability
    formatted = json.dumps(config_json, indent=2)
    print("=== GridJs Client Configuration ===")
    print(formatted)

    # Return the raw dict in case the caller needs to process it
    return config_json

# ----------------------------------------------------------------------
# Example usage – replace this with your actual worksheet object
if __name__ == "__main__":
    # Mock worksheet for demonstration; in real code, fetch from your workbook
    ws = gridjs.Worksheet(name="DemoSheet")
    configure_gridjs(ws)
```

### لماذا كل خطوة مهمة

1. **إنشاء كائن `GridJs`** يمنحك سياقًا جديدًا حيث تبدأ جميع الإعدادات من القيم الافتراضية.  
2. **ربط ورقة العمل** (`set_worksheet`) يخبر GridJs أي ورقة يجب على المساعدين مراقبتها. بدون ذلك، لا يوجد ما يتعامل معه المساعدون.  
3. **تمكين فحص الصياغة** (`how to enable syntax check`) يضيف محللًا خفيفًا يضع خطًا تحت الصيغ غير الصحيحة، مما يوفر عليك أخطاء وقت التشغيل لاحقًا.  
4. **تشغيل التدقيق الإملائي** (`enable spell check`) يبرز الكلمات المكتوبة خطأً في تعليقات الخلايا والخلايا النصية العادية. ضبط اللغة (`how to set spell language`) يضمن توافق القاموس مع إعداداتك الإقليمية—وهو أمر حاسم للأوراق غير الإنجليزية.  
5. **استخراج تكوين العميل** (`retrieve client config`) يمنحك لقطة JSON لجميع الإعدادات النشطة. يمكنك تخزين هذا الـ JSON في قاعدة بيانات، إرساله إلى الواجهة الأمامية، أو ببساطة تسجيله للتصحيح.  

> **نصيحة احترافية:** إذا كنت تحتاج فقط إلى التدقيق الإملائي للغة معينة، عطل الرجوع الافتراضي للغة عن طريق ضبط `grid.settings.spell_check.fallback = False`. هذا يمنع المساعد من التحويل الصامت إلى الإنجليزية عندما لا يجد مطابقة.

---

## كيفية تمكين فحص الصياغة بشكل منفصل

أحيانًا قد تهتم فقط بالتحقق من صحة الصيغ. المقتطف أدناه يعزل هذه الحاجة:

```python
def enable_only_syntax_check(grid):
    """
    Turns on syntax checking while leaving spell‑check disabled.
    """
    grid.settings.syntax_check.enabled = True
    grid.settings.spell_check.enabled = False   # Explicitly turn off spell‑check
    return grid.get_client_config()
```

**متى تستخدمه؟** إذا كان جدول البيانات الخاص بك رقميًا بحتًا أو لديك بالفعل خط أنابيب تدقيق إملائي منفصل، فإن تعطيل مساعد التدقيق الإملائي يقلل من استهلاك المعالج.

---

## كيفية تعيين لغة التدقيق الإملائي ديناميكيًا

يمكنك السماح للمستخدمين النهائيين باختيار لغتهم المفضلة أثناء التشغيل. إليك مساعدًا صغيرًا يبدل اللغة بناءً على معلمة:

```python
def set_spell_language(grid, lang_code="en-US"):
    """
    Updates the spell‑check language. Accepts any IETF language tag
    supported by GridJs (e.g., 'fr-FR', 'es-ES', 'de-DE').
    """
    if not isinstance(lang_code, str):
        raise TypeError("Language code must be a string")
    grid.settings.spell_check.language = lang_code
    # Re‑fetch config to confirm the change
    return grid.get_client_config()
```

**حالة حدية:** إذا قدمت رمز لغة غير مدعوم، سيعود GridJs إلى الإعداد الافتراضي (`en-US`). لتجنب التحويل الصامت، يمكنك الاستعلام عن `grid.supported_languages` قبل تطبيق التغيير.

---

## استرجاع تكوين العميل بصيغة JSON – ما المتوقع

استدعاء `grid.get_client_config()` يُعيد قاموس Python يعكس الـ JSON المرسل إلى عميل الواجهة الأمامية. مخرجات نموذجية تبدو هكذا:

```json
{
  "worksheetId": "ws_12345",
  "settings": {
    "syntax_check": {
      "enabled": true
    },
    "spell_check": {
      "enabled": true,
      "language": "en-US",
      "fallback": true
    }
  },
  "version": "2.4.1"
}
```

يمكنك رؤية علامات `enabled`، اللغة المختارة، وحتى نسخة المكتبة. هذا هو بالضبط ما يشير إليه مصطلح **retrieve client config**، وهو مفيد للتصحيح أو حفظ تفضيلات المستخدم عبر الجلسات.

---

## الأخطاء الشائعة وكيفية تجنبها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| لا توجد خطوط تحت أخطاء الصيغ | `syntax_check.enabled` لا يزال `False` | تأكد من أنك استدعيت `grid.settings.syntax_check.enabled = True` قبل إدخال أي صيغة. |
| التدقيق الإملائي يبرز كل كلمة | اللغة غير مضبوطة أو تم تمكين الرجوع الافتراضي | اضبط `grid.settings.spell_check.language` على رمز صالح واختياريًا عطل الرجوع الافتراضي. |
| `grid.get_client_config()` يُعيد قاموسًا فارغًا | ورقة العمل غير مرفقة (`set_worksheet` مفقودة) | استدعِ `grid.set_worksheet(ws)` مع كائن ورقة عمل صالح أولاً. |
| إصدار JSON يثير `TypeError` | كائنات غير قابلة للتسلسل في التكوين | استخدم `json.dumps(..., default=str)` أو استبعد الكائنات المخصصة قبل الطباعة. |

---

## ملخص المثال الكامل القابل للتنفيذ

بجمع كل شيء معًا، إليك السكريبت النهائي الذي يمكنك تشغيله فورًا:

```python
import json
import gridjs

def main():
    # Create a demo worksheet – replace with your actual worksheet
    ws = gridjs.Worksheet(name="DemoSheet")

    # Initialize GridJs and configure helpers
    grid = gridjs.GridJs()
    grid.set_worksheet(ws)

    # Enable both helpers
    grid.settings.syntax_check.enabled = True          # how to enable syntax check
    grid.settings.spell_check.enabled = True           # enable spell check
    grid.settings.spell_check.language = "en-US"       # how to set spell language

    # Retrieve and display the client configuration
    config = grid.get_client_config()
    print("\n=== Client Config ===")
    print(json.dumps(config, indent=2))

if __name__ == "__main__":
    main()
```

Run it with:

```bash
python gridjs_helpers.py
```

يجب أن ترى الـ JSON منسقًا بشكل جميل يُطبع على وحدة التحكم، مؤكدًا أن كلا المساعدين نشطين وأن اللغة مضبوطة على `en-US`.

---

## الخطوات التالية والمواضيع ذات الصلة

- **حفظ تفضيلات المستخدم:** خزن الـ JSON من `retrieve client config` في قاعدة بيانات وأعد تحميله عند بدء الجلسة.  
- **قواميس مخصصة:** تعلم كيفية إضافة مصطلحات خاصة بالمجال إلى قاموس التدقيق الإملائي في GridJs (`grid.settings.spell_check.custom_words`).  
- **تشخيص الصيغ المتقدم:** اجمع بين فحص الصياغة وواجهة `formula_audit` في GridJs لتحليل أخطاء أعمق.  
- **التعريب:** استكشف `grid.settings.spell_check.language` مع إعدادات مثل `fr-FR` أو `ja-JP` لدعم الفرق متعددة اللغات.  

لا تتردد في التجربة—عطّل أحد المساعدين، غيّر اللغات، أو اربط التكوين بمكوّن واجهة المستخدم. مرونة GridJs تجعل الأمر سهلًا.

---

## الخلاصة

لقد غطينا **تمكين التدقيق الإملائي** في GridJs من البداية إلى النهاية، وعرضنا **كيفية تمكين فحص الصياغة**، وأظهرنا **كيفية تعيين لغة التدقيق الإملائي**، وأخيرًا شرحنا **استرجاع تكوين العميل** للفحص أو الحفظ. مع عينة الكود الكاملة أعلاه، يمكنك دمج هذه المساعدات في أي سير عمل GridJs مبني على Python خلال دقائق.

إذا واجهت أي مشاكل أو لديك أفكار لتوسيع الوظيفة، اترك تعليقًا أدناه. برمجة سعيدة، ولتظل جداول بياناتك خالية من الأخطاء! 

![Screenshot of GridJs settings panel with spell check enabled](https://example.com/images/enable-spell-check.png "Enable spell check in GridJs settings")

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة كود كاملة مع شرح خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية تعيين اللغة في ملفات Excel باستخدام Aspose.Cells .NET لدعم متعدد اللغات](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [كيفية فحص حماية كلمة مرور ورقة العمل في Excel باستخدام Aspose.Cells لـ .NET](/cells/english/net/security-protection/aspose-cells-dotnet-check-excel-worksheet-password-protection/)
- [كيفية فحص أقفال مشروع VBA في ملفات Excel باستخدام Aspose.Cells لـ .NET](/cells/english/net/security-protection/check-vba-project-locks-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}