---
title: Excel에서 순환 참조를 프로그래밍 방식으로 감지
linktitle: Excel에서 순환 참조를 프로그래밍 방식으로 감지
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 순환 참조를 쉽게 감지하세요. 단계별 가이드를 따라 스프레드시트에서 정확한 계산을 보장하세요.
weight: 13
url: /ko/net/excel-formulas-and-calculation-options/detecting-circular-reference/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 순환 참조를 프로그래밍 방식으로 감지

## 소개
Excel 파일을 작업할 때 마주칠 수 있는 가장 짜증나는 문제 중 하나는 순환 참조입니다. 이는 수식이 직접 또는 간접적으로 자체 셀을 다시 참조할 때 발생하여 Excel의 계산 엔진을 혼란스럽게 할 수 있는 루프를 생성합니다. 하지만 걱정하지 마세요! Aspose.Cells for .NET을 사용하면 이러한 성가신 순환 참조를 프로그래밍 방식으로 감지하여 스프레드시트가 기능적이고 정확하게 유지되도록 할 수 있습니다. 이 가이드에서는 이 과정을 단계별로 안내하여 파이처럼 간단하게 만들어 드립니다.
## 필수 조건
순환 참조 감지의 세부 사항을 살펴보기 전에 시작하는 데 필요한 모든 것이 있는지 확인해 보겠습니다.
1. Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요. 이것이 개발 환경이 됩니다.
2. .NET Framework: 호환되는 .NET Framework 버전(최소 .NET Framework 4.0)을 사용하고 있는지 확인하세요.
3.  Aspose.Cells 라이브러리: Aspose.Cells 라이브러리가 필요합니다. 다음에서 다운로드할 수 있습니다.[Aspose 웹사이트](https://releases.aspose.com/cells/net/).
4. C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 도움이 됩니다. 이 언어로 코드를 작성하게 되기 때문입니다.
5. Excel 파일: 테스트를 위해 순환 참조가 포함된 Excel 파일을 준비하세요. 간단한 파일을 만들거나 샘플을 다운로드할 수 있습니다.
이제 전제 조건을 갖추었으니, 즐거운 부분으로 넘어가보죠!
## 패키지 가져오기
코딩을 시작하기 전에 필요한 패키지를 가져와야 합니다. 방법은 다음과 같습니다.
### 새 프로젝트 만들기
- Visual Studio를 열고 새로운 C# 콘솔 애플리케이션 프로젝트를 만듭니다.
### Aspose.Cells 참조 추가
- 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭합니다.
- "NuGet 패키지 관리"를 선택하세요.
- “Aspose.Cells”를 검색하여 최신 버전을 설치하세요.
### 필요한 네임스페이스 가져오기
 당신의 맨 위에`Program.cs` 파일에서 필요한 네임스페이스를 가져옵니다.
```csharp
using System;
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```

이제 모든 것이 설정되었으니 Excel 파일에서 순환 참조를 감지하는 코드를 살펴보겠습니다.
## 1단계: 입력 디렉토리 정의
먼저, Excel 파일이 있는 디렉토리를 지정해야 합니다. 여기가 Excel 파일을 로드할 곳입니다.
```csharp
// 입력 디렉토리
string sourceDir = "Your Document Directory";
```
 바꾸다`"Your Document Directory"` Excel 파일의 실제 경로를 포함합니다.
## 2단계: LoadOptions로 통합 문서 로드
다음으로 Excel 통합 문서를 로드합니다. 여기서 마법이 시작됩니다!
```csharp
LoadOptions loadOptions = new LoadOptions();
var objWB = new Aspose.Cells.Workbook(sourceDir + "Circular Formulas.xls", loadOptions);
```
 여기서 우리는 새로운 인스턴스를 생성하고 있습니다`LoadOptions` 지정된 경로에서 통합 문서를 로드합니다. Excel 파일 이름이 일치하는지 확인하세요!
## 3단계: 반복 설정 활성화
순환 참조를 허용하려면 통합 문서에서 반복 설정을 활성화해야 합니다.
```csharp
objWB.Settings.Iteration = true;
```
이렇게 하면 Aspose.Cells에서 계산 중에 순환 참조를 허용하게 됩니다.
## 4단계: 계산 옵션 및 원형 모니터 만들기
이제 계산 옵션과 사용자 정의 원형 모니터를 만들어 보겠습니다.
```csharp
CalculationOptions copts = new CalculationOptions();
CircularMonitor cm = new CircularMonitor();
copts.CalculationMonitor = cm;
```
 여기서 우리는 인스턴스를 생성하고 있습니다`CalculationOptions` 그리고 관습`CircularMonitor`이 모니터는 계산 중에 발견된 순환 참조를 추적하는 데 도움이 됩니다.
## 5단계: 공식 계산
이제 통합 문서에 있는 수식을 계산할 시간입니다.
```csharp
objWB.CalculateFormula(copts);
```
이 줄은 계산을 실행하고 순환 참조를 확인합니다.
## 6단계: 순환 참조 계산
계산 후에는 얼마나 많은 순환 참조가 발견되었는지 셀 수 있습니다.
```csharp
long lngCircularRef = cm.circulars.Count;
Console.WriteLine("Circular References found - " + lngCircularRef);
```
이는 Excel 파일에서 감지된 순환 참조의 개수를 출력합니다.
## 7단계: 결과 표시
마지막으로 결과를 표시하고 메서드가 성공적으로 실행되었는지 확인해 보겠습니다.
```csharp
Console.WriteLine("DetectCircularReference executed successfully.\r\n");
```
## 8단계: CircularMonitor 클래스 구현
 프로세스를 완료하려면 다음을 구현해야 합니다.`CircularMonitor` 클래스. 이 클래스는 다음에서 상속됩니다.`AbstractCalculationMonitor` 순환 참조 감지를 처리합니다.
```csharp
public class CircularMonitor : AbstractCalculationMonitor
{
    public ArrayList circulars = new ArrayList();
    public ArrayList Circulars { get { return circulars; } }
    public override bool OnCircular(IEnumerator circularCellsData)
    {
        CalculationCell cc = null;
        ArrayList cur = new ArrayList();
        while (circularCellsData.MoveNext())
        {
            cc = (CalculationCell)circularCellsData.Current;
            cur.Add(cc.Worksheet.Name + "!" + CellsHelper.CellIndexToName(cc.CellRow, cc.CellColumn));
        }
        circulars.Add(cur);
        return true;
    }
}
```
이 클래스는 워크시트 이름과 셀 인덱스를 포함하여 발견된 각 순환 참조의 세부 정보를 캡처합니다.
## 결론
Aspose.Cells for .NET을 사용하여 Excel에서 순환 참조를 감지하는 것은 관리 가능한 단계로 나누면 간단한 프로세스입니다. 이 가이드를 따르면 스프레드시트에서 순환 참조를 쉽게 식별하고 처리하여 계산이 정확하고 신뢰할 수 있도록 할 수 있습니다. 노련한 개발자이든 방금 시작한 개발자이든 Aspose.Cells는 Excel 조작 기능을 향상시키는 강력한 도구를 제공합니다. 
## 자주 묻는 질문
### Excel에서 순환 참조란 무엇입니까?
순환 참조는 수식이 자체 셀을 다시 참조할 때 발생하며, 이로 인해 계산이 무한 루프로 진행됩니다.
### 프로그래밍적으로 순환 참조를 어떻게 감지할 수 있나요?
.NET에서 Aspose.Cells 라이브러리를 사용하면 사용자 정의 계산 모니터를 구현하여 프로그래밍 방식으로 순환 참조를 감지할 수 있습니다.
### Aspose.Cells를 사용하기 위한 전제 조건은 무엇입니까?
Visual Studio, .NET Framework 및 Aspose.Cells 라이브러리가 설치되어 있어야 합니다.
### Aspose.Cells를 무료로 사용할 수 있나요?
네, Aspose.Cells는 기능을 탐색해 볼 수 있는 무료 평가판을 제공합니다.
### Aspose.Cells에 대한 자세한 정보는 어디에서 볼 수 있나요?
 방문할 수 있습니다[Aspose.Cells 설명서](https://reference.aspose.com/cells/net/) 자세한 정보와 예를 확인하세요.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
