---
title: 범위 수식 로컬과 유사한 셀 수식 로컬 구현
linktitle: 범위 수식 로컬과 유사한 셀 수식 로컬 구현
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET에서 범위 수식 로컬 기능과 유사한 셀 수식을 구현하는 방법을 알아보세요. 기본 제공 Excel 함수 이름 등을 사용자 지정하는 방법을 알아보세요.
weight: 13
url: /ko/net/workbook-settings/implement-cell-formula-local-similar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 범위 수식 로컬과 유사한 셀 수식 로컬 구현

## 소개
Aspose.Cells for .NET은 Excel 파일을 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 강력하고 유연한 스프레드시트 조작 API입니다. Aspose.Cells에서 제공하는 많은 기능 중 하나는 기본 제공 Excel 함수의 동작을 사용자 정의하는 기능이며, 여기에는 고유한 로컬 함수 이름을 만드는 기능도 포함됩니다. 이 튜토리얼에서는 Aspose.Cells for .NET의 범위 수식 로컬 기능과 유사한 셀 수식을 구현하는 단계를 안내합니다.
## 필수 조건
시작하기 전에 다음 사항이 있는지 확인하세요.
1. Microsoft Visual Studio 2010 이상이 시스템에 설치되어 있어야 합니다.
2.  프로젝트에 설치된 Aspose.Cells for .NET 라이브러리의 최신 버전입니다. 라이브러리는 다음에서 다운로드할 수 있습니다.[.NET용 Aspose.Cells 다운로드 페이지](https://releases.aspose.com/cells/net/).
## 패키지 가져오기
시작하려면 C# 프로젝트에서 필요한 패키지를 가져와야 합니다. 코드 파일 맨 위에 다음 using 문을 추가합니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
## 1단계: 사용자 정의 글로벌화 설정 클래스 만들기
 첫 번째 단계는 사용자 정의를 만드는 것입니다`GlobalizationSettings`Excel 함수의 기본 동작을 재정의할 수 있는 클래스입니다. 이 예에서는 이름을 변경합니다.`SUM` 그리고`AVERAGE` 기능을`UserFormulaLocal_SUM` 그리고`UserFormulaLocal_AVERAGE`각각.
```csharp
class GS : GlobalizationSettings
{
    public override string GetLocalFunctionName(string standardName)
    {
        //필요에 맞게 SUM 함수 이름을 변경하세요.
        if (standardName == "SUM")
        {
            return "UserFormulaLocal_SUM";
        }
        //필요에 맞게 AVERAGE 함수 이름을 변경하세요.
        if (standardName == "AVERAGE")
        {
            return "UserFormulaLocal_AVERAGE";
        }
        return "";
    }
}
```
## 2단계: 새 통합 문서 만들기 및 사용자 지정 글로벌화 설정 지정
 다음으로 새 Workbook 인스턴스를 만들고 사용자 정의를 할당합니다.`GlobalizationSettings` Workbook의 구현 클래스`Settings.GlobalizationSettings` 재산.
```csharp
//워크북 만들기
Workbook wb = new Workbook();
//GlobalizationSettings 구현 클래스 할당
wb.Settings.GlobalizationSettings = new GS();
```
## 3단계: 첫 번째 워크시트 및 셀에 액세스
이제 통합 문서의 첫 번째 워크시트와 해당 워크시트 내의 특정 셀에 액세스해 보겠습니다.
```csharp
//첫 번째 워크시트에 접근하세요
Worksheet ws = wb.Worksheets[0];
//일부 셀에 접근
Cell cell = ws.Cells["C4"];
```
## 4단계: 수식 할당 및 수식 인쇄Local
 마지막으로 다음을 할당해 보겠습니다.`SUM` 그리고`AVERAGE` 셀에 수식을 입력하고 결과를 인쇄합니다.`FormulaLocal` 가치.
```csharp
//SUM 수식을 할당하고 해당 FormulaLocal을 인쇄합니다.
cell.Formula = "SUM(A1:A2)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
//AVERAGE 공식을 할당하고 해당 FormulaLocal을 인쇄합니다.
cell.Formula = "=AVERAGE(B1:B2, B5)";
Console.WriteLine("Formula Local: " + cell.FormulaLocal);
```
## 결론
이 튜토리얼에서는 Aspose.Cells for .NET의 범위 수식 로컬 기능과 유사한 셀 수식을 구현하는 방법을 알아보았습니다. 사용자 지정`GlobalizationSettings` 클래스에서 Excel 함수의 기본 동작을 재정의하고 필요에 맞게 로컬 함수 이름을 사용자 정의할 수 있습니다. 이는 특히 지역화된 또는 국제화된 Excel 문서로 작업할 때 유용할 수 있습니다.
## 자주 묻는 질문
###  의 목적은 무엇입니까?`GlobalizationSettings` class in Aspose.Cells?
 그만큼`GlobalizationSettings` Aspose.Cells의 클래스를 사용하면 로컬 함수 이름을 변경하는 기능을 포함하여 기본 제공 Excel 함수의 동작을 사용자 정의할 수 있습니다.
###  다른 함수의 동작을 재정의할 수 있나요?`SUM` and `AVERAGE`?
 예, 내장된 Excel 함수의 동작을 수정하여 재정의할 수 있습니다.`GetLocalFunctionName` 사용자 정의 방법`GlobalizationSettings` 수업.
### 함수 이름을 기본값으로 재설정하는 방법이 있나요?
 예, 사용자 정의를 제거하여 함수 이름을 재설정할 수 있습니다.`GlobalizationSettings` 클래스 또는 빈 문자열을 반환하여`GetLocalFunctionName` 방법.
### 이 기능을 사용하여 Aspose.Cells에서 사용자 정의 함수를 만들 수 있나요?
 아니,`GlobalizationSettings`클래스는 사용자 지정 함수를 만드는 것이 아니라 기본 제공 Excel 함수의 동작을 재정의하도록 설계되었습니다. 사용자 지정 함수를 만들어야 하는 경우 다음을 사용할 수 있습니다.`UserDefinedFunction` Aspose.Cells의 클래스.
### 이 기능은 .NET용 Aspose.Cells의 모든 버전에서 사용할 수 있나요?
 네,`GlobalizationSettings` 클래스와 함수 이름을 사용자 정의하는 기능은 모든 버전의 .NET용 Aspose.Cells에서 사용할 수 있습니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
