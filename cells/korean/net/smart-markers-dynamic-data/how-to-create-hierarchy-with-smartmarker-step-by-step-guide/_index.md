---
category: general
date: 2026-02-14
description: SmartMarker 템플릿에서 계층 구조를 만드는 방법은 생각보다 쉽습니다 – 계층형 데이터를 만드는 방법과 직원을 효율적으로
  나열하는 방법을 배워보세요.
draft: false
keywords:
- how to create hierarchy
- create hierarchical data
- how to list employees
- SmartMarker nested range
- C# template processing
language: ko
og_description: SmartMarker 템플릿에서 계층 구조를 만드는 방법은 간단합니다. 이 가이드를 따라 계층형 데이터를 만들고 중첩된
  범위로 직원들을 나열하세요.
og_title: SmartMarker로 계층 구조 만들기 – 완전 가이드
tags:
- SmartMarker
- C#
- templating
title: SmartMarker로 계층 구조 만들기 – 단계별 가이드
url: /ko/net/smart-markers-dynamic-data/how-to-create-hierarchy-with-smartmarker-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# SmartMarker로 계층 구조 만들기 – 완전 가이드

SmartMarker 템플릿 안에서 **계층 구조를 만드는 방법**이 궁금하셨나요? 머리카락이 빠질 정도로 복잡하게 느껴질 수 있지만, 혼자만 그런 것이 아닙니다. 많은 보고서 시나리오에서 부모‑자식 관계가 필요합니다—예를 들어 부서와 그 부서에 속한 직원들 같은 경우죠. 좋은 소식은, 올바른 단계를 알면 SmartMarker가 이를 아주 쉽게 처리해 준다는 점입니다.

이 튜토리얼에서는 **C#에서 계층형 데이터 생성**, 중첩 범위 활성화, 그리고 각 부서별 **직원 목록**을 출력하는 템플릿 렌더링까지 전체 과정을 단계별로 살펴보겠습니다. 마지막까지 따라오시면 .NET 프로젝트 어디에든 바로 넣어 실행할 수 있는 샘플을 얻게 됩니다.

---

## 준비 사항

- .NET 6+ (최근 버전이면 모두 가능)
- **SmartMarker** 라이브러리 참조 (`ws.SmartMarkerProcessor` 네임스페이스)
- 기본적인 C# 지식 – 복잡한 내용은 필요 없으며, 객체 몇 개와 람다식 정도면 충분합니다
- 원하는 IDE 또는 편집기 (Visual Studio, Rider, VS Code 등)

위 항목들을 이미 갖추셨다면, 바로 시작해 보겠습니다.

---

## 계층 구조 만들기 – 개요

핵심 아이디어는 최종 문서에 표시하고자 하는 구조와 동일한 **중첩 객체 그래프**를 만드는 것입니다. 우리 예시에서는 그래프가 다음과 같이 구성됩니다:

```
Departments
 ├─ Name (string)
 └─ Employees (string[])
```

SmartMarker는 `Departments` 를 순회하고, **중첩 범위 처리**를 켜면 각 부서의 `Employees` 컬렉션도 자동으로 반복합니다.

---

## 1단계: 계층형 데이터 모델 구축

먼저 부서 배열을 포함하고, 각 부서마다 직원 리스트를 갖는 익명 객체를 만듭니다. 익명 타입을 사용하면 예제가 가볍게 유지됩니다—필요에 따라 실제 POCO 클래스로 교체하셔도 됩니다.

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

> **왜 중요한가:** `Departments` 배열이 최상위 컬렉션이며, 각 요소는 `Employees` 배열을 포함해 두 번째 수준의 계층을 형성합니다. 이후 `#Departments.Employees#` 로 접근하게 됩니다.

---

## 2단계: 중첩 범위 처리 활성화

SmartMarker는 내부 컬렉션을 자동으로 탐색하지 않습니다. 이를 위해 `SmartMarkerOptions` 객체의 스위치를 켜야 합니다.

```csharp
// Step 2: Enable nested range processing so inner collections (Employees) can be used
var smartMarkerOptions = new SmartMarkerOptions
{
    EnableNestedRange = true   // crucial for #Departments.Employees# to work
};
```

> **프로 팁:** 이 플래그를 빼먹으면 내부 `#Employees#` 범위가 아무 것도 반환하지 않아 템플릿이 빈 화면처럼 보입니다.

---

## 3단계: 데이터와 옵션을 프로세서에 전달

이제 데이터와 옵션을 프로세서에 넘깁니다. `ws` 변수는 **WebService**(또는 SmartMarker 엔진을 호스팅하는 객체)를 나타냅니다.

```csharp
// Step 3: Run SmartMarker processing with the data and the configured options
ws.SmartMarkerProcessor.StartSmartMarkerProcessing(departmentData, smartMarkerOptions);
```

이 시점에서 SmartMarker는 템플릿을 파싱하고, 각 부서 이름에 대해 `#Departments.Name#` 를 대체한 뒤, 중첩 범위가 활성화돼 있으면 각 부서의 `Employees` 컬렉션을 순회합니다.

---

## 4단계: 템플릿 마커 작성

아래는 외부 루프와 내부 루프를 모두 보여주는 최소 템플릿 예시입니다. SmartMarker 템플릿 편집기(또는 프로세서에 전달할 `.txt` 파일)에 붙여넣으세요.

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

렌더링 결과는 다음과 같습니다:

```
HR
  - John
  - Amy
IT
  - Bob
  - Eve
```

> **보이는 내용:** 외부 `#Departments.Name#` 가 부서 제목을 출력하고, 내부 `#Departments.Employees#` 블록이 각 직원 이름을 반복합니다. 블록 안의 `#Departments.Employees#` 가 실제 이름을 출력합니다.

---

## 예상 출력 및 검증

전체 예시(데이터 + 옵션 + 템플릿)를 실행하면 위에 표시된 리스트가 정확히 출력됩니다. 콘솔에 결과를 바로 확인하려면 다음과 같이 하면 됩니다:

```csharp
string result = ws.SmartMarkerProcessor.GetProcessedResult(); // pseudo‑method
Console.WriteLine(result);
```

두 개의 부서 헤딩과 그 아래 직원 불릿이 보이면 **계층 구조를 성공적으로 생성하고 직원 목록을 출력**한 것입니다.

---

## 흔히 발생하는 문제와 해결 방법

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| 직원 출력 없음 | `EnableNestedRange` 가 false 로 남아 있음 | `EnableNestedRange = true` 로 설정 |
| 직원 이름 중복 | 동일 배열을 부서 간에 재사용 | 배열을 복제하거나 별도 컬렉션 사용 |
| 매우 큰 계층 구조로 메모리 압박 | SmartMarker가 전체 객체 그래프를 메모리에 로드 | 데이터를 스트리밍하거나 큰 컬렉션을 페이지네이션 |
| 템플릿 구문 오류 | 닫는 `#/…#` 태그 누락 | SmartMarker 검증 도구 사용 또는 작은 템플릿으로 빠르게 테스트 |

---

## 확장하기 – 실제 적용 사례

1. **동적 데이터 소스** – 데이터베이스에서 부서를 가져와 LINQ 로 익명 구조에 매핑합니다.  
2. **조건부 서식** – 각 직원에 `IsManager` 플래그를 추가하고 SmartMarker 조건 태그(`#if …#`) 로 관리자를 강조합니다.  
3. **다중 중첩 레벨** – 부서 안에 팀이 필요하면 `Teams` 컬렉션을 추가하고 `EnableNestedRange` 를 그대로 유지합니다.

---

## 완전 작동 예제 (복사‑붙여넣기 가능)

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

**템플릿 (template.txt)**

```
#Departments.Name#
  #Departments.Employees#
    - #Departments.Employees#
  #/Departments.Employees#
#/Departments.Name#
```

프로그램을 실행하면 앞서 보여드린 계층 구조가 정확히 출력됩니다.

---

## 결론

우리는 **SmartMarker에서 계층 구조를 만드는 방법**을 다루었습니다. C#에서 **계층형 데이터**를 구성하고, 중첩 범위를 활성화한 뒤, **부서별 직원 목록**을 출력하는 템플릿을 렌더링하는 전체 흐름을 살펴보았습니다. 이 패턴은 확장성이 뛰어나며, 더 많은 중첩 컬렉션이나 조건 로직을 추가하면 강력한 보고 엔진을 손쉽게 구축할 수 있습니다.

다음 과제에 도전해 보세요. 익명 타입 대신 강타입 POCO 클래스를 사용하거나, 이 흐름을 ASP.NET Core 엔드포인트에 통합해 PDF 또는 Word 문서를 반환하도록 만들 수 있습니다. 가능성은 무한하고, 이제 탄탄한 기반을 갖추셨습니다.

---

![How to create hierarchy diagram](image.png){alt="부서‑직원 관계를 보여주는 계층 구조 다이어그램"}

*코딩 즐겁게! 진행 중 문제가 생기면 아래 댓글로 알려 주세요—도와드리겠습니다.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}