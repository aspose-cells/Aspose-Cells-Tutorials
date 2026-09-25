---
category: general
date: 2026-03-29
description: SmartMarker를 사용해 JSON에서 변수를 대체하는 방법 – if 표현식 사용법을 배우고, 조건 로직을 적용하며, 값을
  곱하고, 손쉽게 JSON을 생성하세요.
draft: false
keywords:
- how to substitute variables
- use if expression
- how to apply conditional
- how to multiply values
- how to generate json
language: ko
og_description: SmartMarker를 사용하여 JSON에서 변수를 대체하는 방법. if 표현식을 사용하고, 조건 로직을 적용하며, 값을
  곱하고, 몇 분 안에 JSON을 생성하는 방법을 알아보세요.
og_title: SmartMarker를 사용하여 JSON에서 변수 교체하는 방법 – 단계별 가이드
tags:
- C#
- SmartMarker
- JSON templating
title: SmartMarker로 JSON 변수 교체하는 방법 – 완전 가이드
url: /ko/net/smart-markers-dynamic-data/how-to-substitute-variables-in-json-with-smartmarker-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSON에서 SmartMarker를 사용하여 변수 대체하는 방법 – 완전 가이드

JSON 페이로드 안에서 **변수 대체 방법**을 직접 파서를 작성하지 않고도 할 수 있는지 궁금하셨나요? 당신만 그런 것이 아닙니다. 청구서, 가격 엔진, 동적 설정 파일과 같은 다양한 통합 시나리오에서는 런타임 값을 주입하고, 간단한 조건문을 적용하며, 때로는 빠른 곱셈까지 해야 합니다. 이 튜토리얼에서는 SmartMarker 라이브러리를 사용해 **변수 대체 방법**을 정확히 보여드리며, JSON을 깔끔하고 읽기 쉽게 유지하는 방법을 알려드립니다.

실제 예제를 통해 **if 표현식 사용**, **조건 적용 방법**, **값 곱셈 방법**, 그리고 **JSON 생성 방법**을 단계별로 살펴보겠습니다. 마지막에는 .NET 프로젝트 어디에든 바로 넣어 사용할 수 있는 C# 스니펫을 제공합니다.

## 배울 내용

- 재사용 가능한 변수를 저장하기 위해 `SmartMarkerOptions` 설정하기.  
- 조건 로직을 포함하는 `if` 표현식이 들어간 JSON 템플릿 작성하기.  
- 템플릿 안에서 변수를 사용해 값을 곱하기.  
- `SmartMarkerProcessor`로 템플릿을 처리하고 최종 JSON 문자열 얻기.  
- 변수 누락이나 잘못된 표현식 같은 흔한 문제점 해결하기.

외부 서비스 없이, 무거운 의존성 없이—그냥 순수 C#과 SmartMarker NuGet 패키지만 있으면 됩니다.

---

## 변수 대체 – 단계별 개요

아래는 워크플로우의 고수준 그림입니다. 원시 JSON 템플릿이 왼쪽에 들어가고, SmartMarker 엔진이 마법을 부린 뒤, 완전히 렌더링된 JSON이 오른쪽에서 나옵니다.

![JSON에서 변수 대체 과정을 보여주는 다이어그램](https://example.com/images/smartmarker-flow.png "JSON에서 변수 대체 방법")

*이미지 대체 텍스트: JSON에서 변수 대체 과정을 보여주는 다이어그램.*

---

## Step 1: Install and Import SmartMarker

시작하기 전에 프로젝트에 SmartMarker 패키지가 참조되어 있는지 확인하세요. .NET CLI를 사용한다면 다음을 실행합니다:

```bash
dotnet add package SmartMarker
```

그런 다음 C# 파일 상단에 필요한 `using` 지시문을 추가합니다:

```csharp
using SmartMarker;
using SmartMarker.Models;
using System;
```

> **Pro tip:** 최신 버전(2026년 3월 기준)은 2.4.1입니다. .NET 6 이상을 지원하지만 .NET Framework 4.7에서도 정상적으로 동작합니다.

---

## Step 2: Create SmartMarker Options and Define Variables

이제 템플릿 전반에서 재사용할 변수를 보관할 `SmartMarkerOptions` 인스턴스를 생성합니다. 여기서 **변수 대체 방법**에 대한 답을 찾을 수 있습니다—변수는 SmartMarker가 나중에 교체할 자리표시자 역할을 합니다.

```csharp
// Step 2: Create SmartMarker options to hold variables used in the template
var smartMarkerOptions = new SmartMarkerOptions();

// Define a variable (Rate) that we’ll reference later in the JSON expression
smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission rate
```

왜 `Variables`에 비율을 저장하고 하드코딩하지 않을까요? 데이터베이스, 설정 파일, 사용자 입력 등에서 해당 값을 가져올 수 있기 때문입니다. 옵션에 보관하면 템플릿을 재사용하고 테스트하기 쉬워집니다.

---

## Step 3: Write the JSON Template with an `if` Expression

여기서 **if 표현식 사용** 키워드가 빛을 발합니다. SmartMarker를 사용하면 JSON 문자열 안에 직접 조건 로직을 삽입할 수 있습니다. 구문은 속성 이름처럼 보이지만 SmartMarker는 이를 지시문으로 처리합니다.

```csharp
// Step 3: Prepare the JSON data with a conditional field that uses the variable
string jsonTemplate = @"{
    ""Amount"": 1000,
    ""if(Amount>500)"": ""${Amount * Rate}""
}";
```

`if(Amount>500)` 키를 주목하세요. SmartMarker는 `Amount>500` 표현식을 평가하고, 참이면 해당 값(`${Amount * Rate}`)을 출력에 삽입합니다. `${...}` 구문은 *변수 대체* 엔진이며, 여기서는 **값 곱셈 방법**(`Amount * Rate`)을 수행한 뒤 결과를 삽입합니다.

---

## Step 4: Process the Template and Retrieve the Final JSON

옵션과 템플릿이 준비되면 모두 프로세서에 전달합니다. `ProcessJson` 메서드는 템플릿을 파싱하고, 조건을 적용하며, 곱셈을 수행한 뒤 깔끔한 JSON 문자열을 반환합니다.

```csharp
// Step 4: Process the JSON with SmartMarker, applying the variable substitution
string resultJson = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(resultJson);
```

스니펫을 실행하면 다음이 출력됩니다:

```json
{
  "Amount": 1000,
  "Result": "80"
}
```

**무슨 일이 일어났나요?**  
- `Amount`가 1000이므로 `Amount>500` 조건을 만족합니다.  
- SmartMarker는 `${Amount * Rate}`를 평가하여 `1000 * 0.08 = 80`을 얻습니다.  
- 원래의 조건 키(`if(Amount>500)`)는 깔끔한 속성 이름(`Result`)으로 교체됩니다. 기본적으로 SmartMarker는 `"Result"`를 사용하지만, 나중에 커스터마이징할 수 있습니다(자세한 내용은 아래).

`Amount`를 `400`으로 바꾸면 출력은 다음과 같이 됩니다:

```json
{
  "Amount": 400
}
```

조건 블록이 사라지는데, 이는 표현식이 `false`로 평가되었기 때문입니다. 이것이 JSON에서 **조건 적용 방법**의 핵심입니다.

---

## Step 5: Customizing the Output Property Name (Optional)

때때로 일반적인 `"Result"` 키 대신 다른 이름을 사용하고 싶을 수 있습니다. `RenameIfExpression` 옵션을 사용하면 커스텀 이름을 지정할 수 있습니다:

```csharp
smartMarkerOptions.RenameIfExpression = "Discount";
string customResult = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);
Console.WriteLine(customResult);
```

출력:

```json
{
  "Amount": 1000,
  "Discount": "80"
}
```

이제 조건값이 더 의미 있는 속성 이름 아래에 저장됩니다—특정 필드를 기대하는 다운스트림 서비스에 이상적입니다.

---

## Common Pitfalls and How to Avoid Them

| 문제 | 발생 원인 | 해결 방법 |
|------|-----------|-----------|
| 변수 없음 | `smartMarkerOptions.Variables`에 변수가 정의되지 않음 | 철자를 다시 확인하고, 처리 전에 변수가 추가되었는지 확인 |
| 잘못된 `if` 구문 | 괄호 누락 또는 연산자 오류(`>`, `<`, `==`) | 정확한 `if(<expression>)` 패턴을 따르세요; SmartMarker는 단순 숫자 비교만 지원 |
| JSON 형식 오류 | 조건 블록 뒤에 쉼표가 남아 있음 | SmartMarker가 자동으로 제거하도록 두고, 원본 템플릿을 문법적으로 올바르게 유지 |
| 예상치 못한 숫자 형식 | 결과가 숫자 대신 문자열 `"80"`으로 표시 | 나중에 형변환하거나 `${(Amount * Rate):N0}`와 같이 숫자 포맷을 사용 |

---

## Full Working Example (Copy‑Paste Ready)

아래는 컴파일하고 실행할 수 있는 전체 프로그램입니다. 동적 변수, 조건, 산술을 이용해 **JSON 생성 방법**을 30줄 이하로 보여줍니다.

```csharp
using System;
using SmartMarker;
using SmartMarker.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Create SmartMarker options and define a reusable variable
        var smartMarkerOptions = new SmartMarkerOptions();
        smartMarkerOptions.Variables["Rate"] = 0.08; // 8% commission
        smartMarkerOptions.RenameIfExpression = "Discount"; // optional custom name

        // 2️⃣ JSON template with an if expression and multiplication
        string jsonTemplate = @"{
            ""Amount"": 1000,
            ""if(Amount>500)"": ""${Amount * Rate}""
        }";

        // 3️⃣ Process the template
        string output = ws.SmartMarkerProcessor.ProcessJson(jsonTemplate, smartMarkerOptions);

        // 4️⃣ Show the result
        Console.WriteLine("Generated JSON:");
        Console.WriteLine(output);
    }
}
```

**예상 콘솔 출력**

```
Generated JSON:
{
  "Amount": 1000,
  "Discount": "80"
}
```

`Amount` 값을 바꿔 조건 분기를 테스트하거나, `Rate`를 조정해 다양한 할인 계산을 확인해 보세요.

---

## Extending the Pattern – More “How to” Scenarios

- **변수 대체 방법**을 설정 파일에서 가져오기: `appsettings.json`에서 `Dictionary<string, object>`를 로드하고 `smartMarkerOptions.Variables`에 전달합니다.  
- **if 표현식 사용**을 여러 조건에 적용하기: `"if(Amount>500 && CustomerType=='VIP')"`처럼 체인하면 됩니다—SmartMarker는 논리 AND/OR을 지원합니다.  
- **조건 적용 방법** 포맷팅: 표현식 안에 `${Amount:0.00}`를 사용해 소수점 자릿수를 제어합니다.  
- **값 곱셈 방법**을 복잡한 수식으로 확장하기: `${(Amount - Discount) * TaxRate}`와 같이 사용할 수 있습니다.  
- **JSON 생성 방법**을 중첩 객체에 적용하기: 조건 블록을 다른 JSON 객체 안에 넣으면 SmartMarker가 계층 구조를 그대로 유지합니다.

---

## Conclusion

우리는 SmartMarker를 사용해 JSON에서 **변수 대체 방법**을 다루고, **if 표현식 사용**을 통해 조건 포함을 구현했으며, **조건 적용 방법**과 **값 곱셈 방법**을 템플릿 안에서 수행하고, 최종적으로 **JSON 생성 방법**을 보여주었습니다. 이 접근 방식은 가볍고 외부 템플릿 엔진이 필요 없으며, 어떤 C# 코드베이스에도 깔끔히 들어맞습니다.

한 번 직접 해보세요—변수를 조정하고, 조건을 추가하고, 전체 로직을 헬퍼 클래스로 감싸서 솔루션 전반에 재사용해 보세요. 동적 JSON을 빠르게 만들어야 할 때 SmartMarker는 견고하고 프로덕션에 적합한 선택입니다.

**다음 단계**

- `foreach`와 같은 루프 및 사용자 정의 함수와 같은 SmartMarker 고급 기능을 더 깊이 탐색합니다.  
- 이 기법을 ASP.NET Core 엔드포인트와 결합해 동적 JSON API를 제공합니다.  
- Handlebars.NET 등 다른 템플릿 라이브러리를 비교해 보고, 더 풍부한 구문이 필요할 경우 검토합니다.

궁금한 점이나 해결하고 싶은 특정 사용 사례가 있나요? 아래에 댓글을 남겨 주세요. 함께 문제를 해결해 봅시다. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}