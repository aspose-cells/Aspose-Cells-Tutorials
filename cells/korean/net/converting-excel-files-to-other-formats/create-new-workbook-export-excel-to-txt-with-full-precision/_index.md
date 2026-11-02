---
category: general
date: 2026-03-18
description: 새 워크북을 만들고 숫자 정밀도를 유지하면서 Excel을 TXT로 내보냅니다. 워크시트를 TXT로 저장하는 방법과 워크시트를
  효율적으로 TXT로 변환하는 방법을 배워보세요.
draft: false
keywords:
- create new workbook
- export excel to txt
- save excel as txt
- save worksheet as txt
- convert worksheet to txt
language: ko
og_description: 새 워크북을 만들고 Excel을 정밀하게 TXT로 내보냅니다. 이 튜토리얼에서는 워크시트를 TXT로 저장하고 C#을 사용하여
  워크시트를 TXT로 변환하는 방법을 보여줍니다.
og_title: 새 워크북 만들기 – Excel을 TXT로 내보내는 가이드
tags:
- Aspose.Cells
- C#
- Excel automation
title: 새 워크북 만들기 – 전체 정밀도로 Excel을 TXT로 내보내기
url: /ko/net/converting-excel-files-to-other-formats/create-new-workbook-export-excel-to-txt-with-full-precision/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 새 워크북 만들기 – 전체 정밀도로 Excel을 TXT로 내보내기

C#에서 **새 워크북 만들기**만으로 데이터를 일반 텍스트 파일에 덤프해야 했던 적 있나요? 레거시 시스템에서 보고서를 추출하고, 다운스트림 도구가 `.txt` 피드만 받는 경우가 있을 수 있습니다. 좋은 소식은? 숫자 정밀도를 희생할 필요도 없고, CSV 문자열을 직접 만들 필요도 없습니다.

이 가이드에서는 **excel을 txt로 내보내기** 전체 과정을 단계별로 살펴보며, 워크북 초기화부터 **워크시트를 txt로 저장**할 때 뒤쪽의 0을 보존하는 방법까지 다룹니다. 끝까지 따라오면 .NET 프로젝트에 바로 넣을 수 있는 실행 가능한 코드 스니펫을 얻게 됩니다—추가 유틸리티는 필요 없습니다.

## 준비 사항

- **ASP.NET/.NET 6+** (코드는 .NET Framework 4.6+에서도 동작)  
- **Aspose.Cells for .NET** – `Workbook`, `Worksheet`, `TxtSaveOptions` 클래스를 제공하는 라이브러리. NuGet에서 `Install-Package Aspose.Cells` 로 설치하세요.  
- C# 기본 지식 ( `using` 문에 익숙하면 바로 시작 가능)  

이것만 있으면 됩니다—Excel 인터옵, COM 객체, 수동 문자열 연결은 전혀 필요 없습니다.  

---

## 1단계: 새 워크북 초기화 (Primary Keyword)

먼저 **새 워크북 만들기**를 해야 합니다. 워크북은 나중에 숫자, 텍스트, 수식을 붙여넣을 빈 캔버스와 같습니다.

```csharp
using System;
using Aspose.Cells;

namespace ExcelToTxtDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();                 // <‑‑ creates new workbook
            Worksheet worksheet = workbook.Worksheets[0];       // first sheet (index 0)
```

> **왜 중요한가:** 파일을 로드하지 않고 `Workbook`을 인스턴스화하면 깨끗한 상태가 됩니다. 이렇게 하면 기존 `.xlsx`가 없는 **워크시트를 txt로 변환** 상황에서도 프로그램matically 데이터를 추가할 수 있습니다.

---

## 2단계: 셀 채우기 – 뒤쪽 0 유지하기

숫자를 텍스트로 덤프할 때 흔히 발생하는 문제는 뒤쪽 0가 사라진다는 점(`123.45000` → `123.45`)입니다. 다운스트림 시스템이 고정 길이 필드를 요구한다면 이 손실은 치명적일 수 있습니다.

```csharp
            // Step 2: Write a numeric value that contains trailing zeros
            // PutValue respects the data type; we’ll later tell the saver to keep precision.
            worksheet.Cells[0, 0].PutValue(123.45000);
```

> **프로 팁:** `PutValue`는 데이터 유형을 자동으로 추론합니다. 숫자처럼 보이는 문자열이 필요하면 `PutValue("123.45000")` 를 사용하세요.

---

## 3단계: TXT 저장 옵션 설정 – 숫자 정밀도 보존

여기서 마법이 일어납니다. `PreserveNumericPrecision` 를 토글하면 Aspose.Cells가 입력한 정확한 값을, 의미 없는 뒤쪽 0까지 포함해 기록하도록 지시합니다.

```csharp
            // Step 3: Configure TXT save options to keep the original numeric precision
            TxtSaveOptions txtSaveOptions = new TxtSaveOptions(SaveFormat.Txt)
            {
                PreserveNumericPrecision = true   // retain all digits, even trailing zeros
            };
```

> **왜 활성화해야 할까?** **excel을 txt로 저장**할 때 기본 동작은 불필요한 소수점을 잘라냅니다. `PreserveNumericPrecision = true` 로 설정하면 출력이 셀에 표시된 값과 동일하게 보장되며, 이는 재무 보고서나 과학 데이터에 매우 중요합니다.

---

## 4단계: 워크시트를 TXT로 저장 – 최종 내보내기

이제 실제로 **워크시트를 txt로 저장**합니다. 쓰기 권한이 있는 경로라면 어디든 지정할 수 있으며, 예제에서는 `output`이라는 상대 폴더를 사용합니다.

```csharp
            // Step 4: Save the worksheet as a TXT file using the configured options
            string outputPath = "output/num-preserve.txt";
            worksheet.Save(outputPath, txtSaveOptions);

            Console.WriteLine($"File saved to {outputPath}");
        }
    }
}
```

> **예상 출력** (`num-preserve.txt`):

```
123.45000
```

뒤쪽 0가 그대로 유지된 것을 확인할 수 있습니다—요청한 대로 정확히 출력됩니다.

---

## 5단계: 결과 확인 – 간단한 검증

프로그램 실행 후 `num-preserve.txt`를 텍스트 편집기로 열어보세요. `123.45000` 한 줄만 보이면 정상입니다. `123.45`가 보인다면 `PreserveNumericPrecision`가 `true`로 설정됐는지, Aspose.Cells 최신 버전(v23.10+)을 사용했는지 다시 확인하세요.

---

## 흔히 발생하는 변형 및 예외 상황

### 여러 셀 또는 범위 내보내기

전체 범위에 대해 **excel을 txt로 내보내기**하려면 저장하기 전에 더 많은 셀을 채우면 됩니다:

```csharp
worksheet.Cells["A1"].PutValue(100);
worksheet.Cells["A2"].PutValue(200.500);
worksheet.Cells["A3"].PutValue(300.00);
```

Aspose는 기본적으로 각 셀을 새 줄에 기록합니다. `txtSaveOptions.Separator` 를 통해 구분자(탭, 콤마 등)를 변경할 수도 있습니다.

### 다른 인코딩으로 워크시트 변환

다운스트림 시스템이 UTF‑8 BOM 또는 ASCII를 요구할 때는 다음과 같이 인코딩을 조정합니다:

```csharp
txtSaveOptions.Encoding = System.Text.Encoding.UTF8;
```

### 대용량 워크북 처리

수십만 행의 거대한 시트를 다룰 때는 스트리밍 출력을 고려하세요:

```csharp
txtSaveOptions.EnableCache = true; // writes data in chunks to reduce memory footprint
```

---

## 프로 팁 & 주의사항

- `Save` 호출 전에 **출력 디렉터리를 반드시 생성**하세요. 그렇지 않으면 `DirectoryNotFoundException`이 발생합니다.  
- **지역화된 소수 구분자**에 유의하세요. 환경이 콤마(`1,23`)를 사용한다면 `txtSaveOptions.DecimalSeparator = '.'` 로 점을 강제 지정합니다.  
- **버전 호환성**: `PreserveNumericPrecision` 플래그는 Aspose.Cells 20.6부터 도입되었습니다. 이전 버전을 사용 중이라면 해당 플래그가 없으므로 셀을 텍스트 형식으로 포맷한 뒤 저장해야 합니다.

---

![Create new workbook example](excel-to-txt.png "Create new workbook")

*Image alt text: "Create new workbook and export Excel to TXT with numeric precision preserved"*

---

## 요약 – 다룬 내용

- Aspose.Cells를 이용한 **새 워크북 만들기**.  
- 뒤쪽 0가 포함된 숫자를 셀에 채우기.  
- `TxtSaveOptions.PreserveNumericPrecision = true` 로 **excel을 txt로 저장**하면서 정밀도 손실 방지.  
- 파일을 디스크에 기록하고, 출력이 원본 값과 일치하는지 검증하기.  

이것이 50줄 이하의 C# 코드로 구현한 **워크시트를 txt로 변환** 전체 흐름입니다.

---

## 다음 단계 및 연관 주제

완벽한 정밀도로 **excel을 txt로 내보내기**가 가능해졌다면 다음을 살펴볼 수 있습니다:

- 커스텀 구분자(`TxtSaveOptions.Separator`)를 사용한 **CSV 내보내기**.  
- TSV(`SaveFormat.TabDelimited`)와 같은 다른 텍스트 형식으로 **저장**.  
- `Directory.GetFiles` 를 활용한 폴더 내 다수 워크북 **배치 처리**.  
- 클라우드에서 온디맨드 변환을 위한 **Azure Functions와 통합**.

이 모든 작업은 동일한 `Workbook` → `Worksheet` → `TxtSaveOptions` 패턴을 기반하므로 익숙해지기 쉽습니다.

---

### 마무리 생각

이 튜토리얼을 따라했다면 **새 워크북 만들기**, 데이터를 채우기, 그리고 **워크시트를 txt로 저장**하면서 모든 소수점을 보존하는 방법을 정확히 알게 되었습니다. 작은 코드 조각이지만 레거시 파이프라인이 일반 텍스트 입력을 요구할 때 흔히 겪는 골칫거리를 해결합니다.

코드를 실행해 보고 옵션을 조정해 보세요. 데이터가 원하는 대로 흐를 것입니다. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}