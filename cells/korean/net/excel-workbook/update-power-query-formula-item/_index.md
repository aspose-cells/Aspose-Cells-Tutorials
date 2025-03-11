---
title: Power Query 수식 항목 업데이트
linktitle: Power Query 수식 항목 업데이트
second_title: .NET API 참조를 위한 Aspose.Cells
description: Aspose.Cells for .NET을 사용하여 Excel에서 Power Query 수식 항목을 쉽게 업데이트합니다. 데이터 조작 프로세스를 간소화하는 단계별 가이드입니다.
weight: 160
url: /ko/net/excel-workbook/update-power-query-formula-item/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Power Query 수식 항목 업데이트

## 소개

Excel을 사용해 본 적이 있다면, 특히 Power Queries를 사용하기 시작하면 얼마나 강력한지 알 것입니다. 이는 데이터를 손쉽게 변환, 정리 및 분석할 수 있는 비법입니다. Excel에서 Power Query 수식을 조작하는 한 가지 멋진 방법은 Aspose.Cells for .NET을 사용하는 것입니다. 오늘은 Power Query 수식 항목을 단계별로 업데이트하는 방법을 안내해 드리겠습니다. 그러니 코딩 모자를 쓰고 시작해 봅시다!

## 필수 조건

코드를 살펴보기 전에 설정해야 할 몇 가지 사항이 있습니다.

1. Visual Studio: .NET 코드를 작성하고 실행하려면 통합 개발 환경(IDE)이 필요합니다. Visual Studio가 최선의 선택입니다.
2.  Aspose.Cells 라이브러리: 프로젝트 내에서 Aspose.Cells 라이브러리를 사용할 수 있는지 확인하세요. 다음에서 다운로드할 수 있습니다.[대지](https://releases.aspose.com/cells/net/).
3. C#에 대한 기본 지식: 함께 살펴보겠지만 C#에 대한 기본적인 이해가 있으면 확실히 도움이 될 것입니다. 특히 다양한 클래스와 메서드를 살펴볼 때 더욱 그렇습니다.
4. 샘플 Excel 파일: 코드 조각에 언급된 Excel 파일이 필요합니다. 다음이 있는지 확인하세요.
   - `SamplePowerQueryFormula.xlsx`
   - `SamplePowerQueryFormulaSource.xlsx`

5. .NET Framework: 프로젝트가 호환되는 .NET Framework 버전을 대상으로 하는지 확인하세요.

이제 키트가 준비되었으니, 즐거운 단계인 코드 작성으로 넘어가겠습니다!

## 패키지 가져오기

우선, 필요한 네임스페이스를 가져와야 합니다. 방법은 다음과 같습니다.

```csharp
using Aspose.Cells.DigitalSignatures;
using Aspose.Cells.QueryTables;
using System;
using System.IO;
```

이러한 네임스페이스를 추가하면 Aspose.Cells 라이브러리의 클래스와 메서드를 사용하려고 한다는 것을 컴파일러에게 알리는 것입니다. 이 단계는 다음 코드의 기초를 마련하기 때문에 중요합니다.

제공하신 코드 조각을 분석해 보겠습니다. 이 튜토리얼은 각 부분을 안내하여 무슨 일이 일어나고 있는지 이해하도록 도와드립니다.

## 1단계: 작업 디렉토리 설정

이 단계에서는 소스 및 출력 파일의 위치를 정의합니다. 이렇게 하면 Aspose가 Excel 파일을 어디에서 찾아야 할지 알 수 있습니다.

```csharp
// 작업 디렉토리
string SourceDir = "Your Document Directory";
string outputDir = "Your Output Directory";
```

## 2단계: 통합 문서 로드

이제 Power Query가 있는 Excel 파일을 로드해 보겠습니다.

```csharp
Workbook workbook = new Workbook(SourceDir + "SamplePowerQueryFormula.xlsx");
```
 그만큼`Workbook` 클래스는 Excel 파일에 대한 진입점입니다. 소스 파일의 경로를 전달함으로써, 우리는 그것을 조작할 수 있는 인스턴스를 만들고 있습니다. 책을 여는 것과 같다고 상상할 수 있습니다. 즉, 내용을 읽거나(또는 편집)할 준비를 하는 것입니다.

## 3단계: 데이터 매시업에 액세스

다음으로, 통합 문서의 데이터 매시업에 저장된 Power Query 수식에 액세스하겠습니다.

```csharp
DataMashup mashupData = workbook.DataMashup;
```
 그만큼`DataMashup` 클래스에는 통합 문서와 관련된 모든 Power Query 수식이 들어 있습니다. 여기서 수리를 위해 도구 상자를 여는 것과 마찬가지로 무거운 작업을 할 것입니다.

## 4단계: Power Query 수식 반복

이제 Power Query 수식을 반복하여 업데이트하려는 특정 수식을 찾는 단계입니다.

```csharp
foreach (PowerQueryFormula formula in mashupData.PowerQueryFormulas)
{
    foreach (PowerQueryFormulaItem item in formula.PowerQueryFormulaItems)
    {
        if (item.Name == "Source")
        {
            item.Value = "Excel.Workbook(File.Contents(\"" + SourceDir + "SamplePowerQueryFormulaSource.xlsx\"), null, true)";
        }
    }
}
```

-  우리는 각각을 반복합니다`PowerQueryFormula` ~에`mashupData`.
- 그 루프 내에서 우리는 각각에 대해 깊이 파고듭니다.`PowerQueryFormulaItem`.
- 우리는 항목의 이름이 "소스"와 일치하는지 확인합니다. 일치하면 해당 값을 업데이트하여 새 소스 파일에 연결합니다.

이것은 매뉴얼에서 올바른 페이지를 찾아 필요한 업데이트를 하는 것과 같습니다. 간단하고 세심한 과정입니다.

## 5단계: 업데이트된 통합 문서 저장

업데이트를 한 후에는 변경 사항을 저장할 차례입니다.

```csharp
// 출력 통합 문서를 저장합니다.
workbook.Save(outputDir + "SamplePowerQueryFormula_out.xlsx");
Console.WriteLine("UpdatePowerQueryFormulaItem executed successfully.");
```
 그만큼`Save` 이 메서드는 업데이트된 통합 문서를 지정된 출력 디렉토리에 씁니다. 다른 사람들이 사용할 수 있도록 새로운 버전의 매뉴얼에 편집 내용을 봉인하는 것과 같습니다!

## 결론

축하합니다! Aspose.Cells for .NET을 사용하여 Power Query 수식 항목을 성공적으로 업데이트했습니다. 이 방법을 사용하면 Excel 파일에서 Power Query 수식 수정을 자동화하여 귀중한 시간과 노력을 절약할 수 있습니다.

## 자주 묻는 질문

### Aspose.Cells란 무엇인가요?
Aspose.Cells는 Microsoft Excel을 설치하지 않고도 .NET 애플리케이션에서 Excel 파일을 조작할 수 있는 강력한 라이브러리입니다.

### Aspose.Cells를 실행하려면 Microsoft Excel이 필요합니까?
아니요, Aspose.Cells를 사용하면 서버나 개발용 컴퓨터에 Excel이 없어도 프로그래밍 방식으로 Excel 파일을 만들고 편집할 수 있습니다.

### Aspose.Cells를 사용하여 어떤 유형의 Excel 파일을 작업할 수 있습니까?
Aspose.Cells를 사용하면 .xlsx, .xls, .xlsm 및 기타 여러 Excel 형식으로 작업할 수 있습니다.

### Aspose.Cells의 평가판이 있나요?
 네, 무료 평가판을 다운로드할 수 있습니다.[Aspose Cells 릴리스 페이지](https://releases.aspose.com/).

### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?
 다음을 통해 지원에 액세스할 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9), 커뮤니티와 Aspose 팀에 질문을 올리고 답변을 찾을 수 있습니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
