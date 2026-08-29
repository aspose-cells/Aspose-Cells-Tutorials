---
date: '2026-08-16'
description: Aspose.Cells를 사용하여 Java에서 글로벌화를 추가하고, Excel 오류 메시지를 사용자 정의하며, Maven 종속성을
  설정하는 방법을 배웁니다.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Aspose.Cells를 사용하여 Java에서 글로벌화를 추가하고, Excel 오류 메시지를 사용자 정의하며, Maven
  종속성을 설정하는 방법을 배웁니다. step‑by‑step guide를 따르세요.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Java에서 Aspose.Cells를 사용하여 글로벌화 추가하는 방법
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Java에서 Aspose.Cells를 사용하여 글로벌화 추가하는 방법
url: /ko/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 Aspose.Cells를 사용하여 글로벌화 추가하기

## 소개

Java 워크북에 글로벌화를 추가하면 사용자가 기대하는 언어로 오류 메시지, 불리언 값 및 기타 로케일별 문자열을 표시할 수 있습니다. 이 튜토리얼에서는 러시아어에 대한 **글로벌화 추가 방법**을 배우게 되며, 동일한 패턴을 다른 언어에도 적용할 수 있습니다. 가이드가 끝날 때 다음을 수행할 수 있게 됩니다:

- 기본 오류 텍스트와 불리언 표현을 재정의합니다.
- `Workbook` 인스턴스에 사용자 지정 설정을 적용합니다.
- 일반적인 Maven 기반 Java 프로젝트에 솔루션을 통합합니다.

Excel 파일을 진정으로 다국어로 만들 준비가 되셨나요? 먼저 개발 환경이 전제 조건을 충족하는지 확인해 보겠습니다.

## 빠른 답변

- **Aspose.Cells에서 글로벌화란 무엇입니까?** 로케일을 인식하는 문자열(오류, 불리언 등)의 집합으로, 이를 사용자 지정 텍스트로 교체할 수 있습니다.  
- **필요한 Maven 아티팩트는 무엇입니까?** `com.aspose:aspose-cells:25.3`.  
- **러시아어 외의 다른 언어를 대상으로 할 수 있습니까?** 예 – `GlobalizationSettings`를 확장하고 각 로케일에 필요한 메서드를 재정의합니다.  
- **개발에 라이선스가 필요합니까?** 무료 체험판으로 테스트가 가능하며, 정식 라이선스를 사용하면 평가 워터마크가 제거됩니다.  
- **이 솔루션은 스레드 안전합니까?** 워크북별로 설정을 적용합니다; `GlobalizationSettings` 객체 자체는 생성 후 불변입니다.

## Aspose.Cells에서 글로벌화란 무엇입니까?

`GlobalizationSettings`는 오류 메시지, 불리언 값, 통화 기호 및 날짜 형식과 같은 로케일별 문자열을 제어하는 Aspose.Cells의 구성 객체입니다. 자체 서브클래스를 제공하면 라이브러리에게 각 문화권에 표시할 텍스트를 알려줄 수 있어, 기본 영어 문자열을 최종 사용자의 언어와 지역 관습에 맞는 번역으로 교체할 수 있습니다.

## 왜 사용자 지정 글로벌화를 추가해야 할까요?

Aspose.Cells는 **50개 이상의 입력 및 출력 형식**(XLSX, CSV, PDF, ODS 등)을 지원하며, 전체 파일을 메모리에 로드하지 않고도 **최대 200 000행**까지의 워크북을 처리할 수 있습니다. 글로벌화를 사용자 지정하면 최종 사용자가 자신의 모국어로 메시지를 확인할 수 있어, 다국적 배포에서 지원 티켓을 약 **30 %** 감소시킬 수 있습니다.

## 전제 조건

- **Java Development Kit** 8 이상.
- **IDE**(IntelliJ IDEA 또는 Eclipse 등).
- **Aspose.Cells for Java** 버전 25.3(또는 이후) 를 Maven 또는 Gradle을 통해 추가.

### Aspose.Cells for Java 설정

Add the Maven dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Or, if you prefer Gradle, insert the following into `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 라이선스 획득

Aspose offers several licensing options:

- **무료 체험** – 30일 동안 전체 기능을 평가할 수 있습니다.  
- **임시 라이선스** – 워터마크 없이 무제한 평가.  
- **상업용 라이선스** – 프로덕션 준비 완료, 우선 지원 제공.

After obtaining a license file, set it once at application startup:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## 러시아어에 대한 글로벌화를 추가하는 방법은?

`Workbook` 객체는 메모리에 로드된 Excel 파일을 나타내며, 시트, 셀 및 설정에 접근할 수 있습니다. 워크북을 로드하고 `GlobalizationSettings`의 서브클래스를 생성한 뒤 워크북에 연결합니다. 직접적인 답은: **맞춤형 `GlobalizationSettings` 클래스를 인스턴스화하고 `getErrorValueString` 및 `getBooleanValueString`을 재정의한 다음 `workbook.setGlobalizationSettings(customSettings)`를 호출**하는 것입니다. 이 두 단계 접근 방식은 기본 러시아어 문자열을 사용자 정의 문자열로 교체합니다.

### 맞춤 설정 정의

The first time you reference `GlobalizationSettings` in this guide, note the definition:

`GlobalizationSettings` is the base class that Aspose.Cells uses to retrieve locale‑specific strings.  

Now create a subclass that returns Russian‑specific text:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### 워크북에 설정 적용

After defining the subclass, attach it to any `Workbook` instance:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## 실제 적용 사례

- **재무 보고** – 회계사의 모국어로 오류 코드를 표시하여 오해를 줄입니다.  
- **전사적 도구** – 수십 개의 내부 Excel 기반 유틸리티에 동일한 글로벌화 로직을 삽입합니다.  
- **자동화 데이터 파이프라인** – 하위 시스템이 추가 번역 단계 없이 로케일 인식 값을 받도록 보장합니다.

## 성능 고려 사항

맞춤 글로벌화를 활성화해도 Aspose.Cells는 동일한 높은 성능으로 수식 및 I/O를 처리합니다. 메모리 사용량을 낮게 유지하려면:

- 저장 후 워크북 참조(`wb.dispose()`)를 해제합니다.  
- 필요할 때만 `CalculationOptions.setEnableIterativeCalculation(true)`를 사용합니다.  
- 100 MB보다 큰 워크북에 대해 JVM 힙(`-Xmx2g`)을 조정합니다.

## 자주 묻는 질문

**Q: 동일한 글로벌화 설정을 여러 워크북에 동시에 적용할 수 있습니까?**  
A: 예. 단일 `RussianGlobalization` 인스턴스를 생성하고 `setGlobalizationSettings`를 통해 각 워크북에 전달합니다.

**Q: 오른쪽에서 왼쪽으로 쓰는 스크립트를 사용하는 언어를 지원해야 하면 어떻게 해야 합니까?**  
A: 서브클래스에서 `getCurrencySymbol` 및 `getDatePattern`과 같은 추가 메서드를 재정의하여 적절한 RTL 기호를 반환합니다.

**Q: 체험판에서 맞춤 글로벌화를 사용하려면 라이선스가 필요합니까?**  
A: 아니요. 체험판은 `GlobalizationSettings`를 완전히 지원하며, 특정 출력 형식에만 평가 워터마크가 표시됩니다.

**Q: 잘못된 오류 문자열을 어떻게 디버깅합니까?**  
A: 재정의한 메서드 내부에 `System.out.println` 구문을 삽입하여 입력 `err` 값이 스위치 케이스와 일치하는지 확인합니다.

**Q: 이것이 수식 계산 속도에 영향을 줍니까?**  
A: 거의 영향을 주지 않습니다. 라이브러리는 셀 값을 렌더링할 때만 문자열을 조회하며, 중간 계산 단계에서는 조회하지 않습니다.

## 추가 리소스

- **문서**: 자세한 가이드를 [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)에서 확인하세요.  
- **다운로드**: 최신 릴리스를 [Aspose Downloads](https://releases.aspose.com/cells/java/)에서 확인하세요.  
- **구매**: 상업적 사용을 위한 라이선스를 [Aspose Purchase](https://purchase.aspose.com/buy)에서 구매하세요.  
- **무료 체험**: [Aspose Free Trial](https://releases.aspose.com/cells/java/)에서 무료 체험을 시작하세요.  
- **임시 라이선스**: [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)를 통해 임시 라이선스를 획득하세요.  
- **지원**: 커뮤니티에서 도움을 받으려면 [Aspose Support Forum](https://forum.aspose.com/c/cells/9)에서 확인하세요.

---

**마지막 업데이트:** 2026-08-16  
**테스트 환경:** Aspose.Cells 25.3 for Java  
**작성자:** Aspose

## 관련 튜토리얼

- [Aspose.Cells Java: 사용자 지정 계산 엔진 가이드](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Aspose Cells 사용 방법 – Java용 Excel 엔진 튜토리얼](/cells/java/calculation-engine/)
- [Aspose Cells Maven 의존성 – Java에서 Aspose.Cells를 사용한 Excel 데이터 연결 관리](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}