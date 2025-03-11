---
title: Excel에서 추가 기능에서 함수 등록 및 호출
linktitle: Excel에서 추가 기능에서 함수 등록 및 호출
second_title: Aspose.Cells .NET Excel 처리 API
description: 간단한 단계별 튜토리얼을 통해 Aspose.Cells for .NET을 사용하여 Excel의 추가 기능에서 함수를 등록하고 호출하는 방법을 알아보세요.
weight: 20
url: /ko/net/excel-formulas-and-calculation-options/registering-and-calling-function-from-add-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 추가 기능에서 함수 등록 및 호출

## 소개
추가 기능에서 함수를 호출하여 Excel 경험을 향상시키고 싶으신가요? 그렇다면 올바른 곳에 오셨습니다! Excel 추가 기능은 스프레드시트의 요정 대모와 같습니다. 마법처럼 기능을 확장하여 손끝에서 여러 가지 새로운 도구를 사용할 수 있습니다. 그리고 Aspose.Cells for .NET을 사용하면 이러한 추가 기능 함수를 등록하고 사용하는 것이 그 어느 때보다 쉬워졌습니다. 
이 가이드에서는 Aspose.Cells for .NET을 사용하여 Excel 추가 기능에서 함수를 등록하고 호출하는 과정을 안내해 드리겠습니다. 모든 것을 단계별로 나누어 설명해 드리니, 금세 프로처럼 느껴질 겁니다!
## 필수 조건
코딩 마법에 들어가기 전에 먼저 준비해야 할 사항부터 살펴보겠습니다.
1. Visual Studio: 컴퓨터에 Visual Studio가 설치되어 있는지 확인하세요. 여기서 코드를 작성하고 실행합니다.
2.  Aspose.Cells 라이브러리: Aspose.Cells 라이브러리가 설치되어 있어야 합니다. 여기에서 가져올 수 있습니다.[다운로드 페이지](https://releases.aspose.com/cells/net/).
3. C#에 대한 기본 지식: C#에 대한 약간의 이해가 있으면 많은 도움이 됩니다. 원활하게 따라갈 수 있을 것입니다.
4.  Excel 추가 기능: 추가 기능 파일(예:`.xlam`)에 등록하여 사용하고 싶은 기능이 포함되어 있습니다.
5.  샘플 Excel 추가 기능: 이 튜토리얼에서는 다음과 같은 Excel 추가 기능을 사용합니다.`TESTUDF.xlam`. 그러니 꼭 이걸 준비해 두세요!
이제 준비가 되었으니, 소매를 걷어붙이고 코딩을 시작해볼까요!
## 패키지 가져오기
시작하려면 C# 파일 맨 위에 몇 가지 필수 네임스페이스를 가져와야 합니다. 포함해야 할 내용은 다음과 같습니다.
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
```
이러한 네임스페이스를 사용하면 이 튜토리얼에서 사용할 클래스와 메서드에 액세스할 수 있습니다.
이것을 관리 가능한 단계로 나누어 보겠습니다. 이 가이드를 마칠 때쯤이면 추가 기능 함수를 등록하고 Excel 통합 문서에서 사용하는 방법을 확실히 이해하게 될 것입니다.
## 1단계: 소스 및 출력 디렉토리 설정
추가 기능을 등록하려면 먼저 추가 기능과 출력 파일을 저장할 위치를 정의해야 합니다.
```csharp
// 소스 디렉토리
string sourceDir = "Your Document Directory";
// 출력 디렉토리
string outputDir = "Your Document Directory";
```
 바꾸다`"Your Document Directory"` 실제 경로와 함께`.xlam` 파일과 출력 파일이 저장됩니다. 이는 쇼가 시작되기 전에 무대를 설정하는 것과 같습니다.
## 2단계: 빈 통합 문서 만들기
다음으로, 추가 기능 함수를 사용해 볼 수 있는 빈 통합 문서를 만들어야 합니다.
```csharp
// 빈 통합 문서 만들기
Workbook workbook = new Workbook();
```
이 코드 줄은 우리의 놀이터 역할을 할 새로운 워크북을 만듭니다. 창의적인 획을 그릴 준비가 된 새로운 캔버스라고 생각하세요.
## 3단계: 추가 기능 기능 등록
이제 문제의 핵심으로 들어가보죠! 애드인 함수를 등록할 시간입니다. 방법은 다음과 같습니다.
```csharp
// 함수 이름과 함께 매크로 활성화 추가 기능을 등록합니다.
int id = workbook.Worksheets.RegisterAddInFunction(sourceDir + @"TESTUDF.xlam", "TEST_UDF", false);
```
 이 줄은 추가 기능 함수를 등록합니다.`TEST_UDF` 에서 발견됨`TESTUDF.xlam` 추가 기능 파일입니다.`false`매개변수는 추가 기능이 '격리된' 모드로 로드되지 않았음을 의미합니다. 
## 4단계: 추가 기능 등록(있는 경우)
동일한 추가 기능 파일에 여러 개의 기능이 등록되어 있다면, 해당 기능도 등록할 수 있습니다!
```csharp
// 파일에 더 많은 기능을 등록합니다(있는 경우)
workbook.Worksheets.RegisterAddInFunction(id, "TEST_UDF1");
```
여기서, 같은 애드인에서 더 많은 기능을 추가하는 것이 얼마나 쉬운지 볼 수 있습니다. 빌딩 블록처럼 계속 쌓아 올리세요!
## 5단계: 워크시트에 액세스
계속해서 함수를 사용할 워크시트에 접근해 보겠습니다. 
```csharp
// 첫 번째 워크시트에 접근하세요
Worksheet worksheet = workbook.Worksheets[0];
```
우리는 공식을 배치하기 위해 워크북의 첫 번째 워크시트에 접근하고 있습니다. 마치 재미가 일어나는 방으로 가는 문을 여는 것과 같습니다.
## 6단계: 특정 셀에 액세스
다음으로, 수식에 사용할 셀을 선택해야 합니다. 
```csharp
// 첫 번째 셀에 접근
var cell = worksheet.Cells["A1"];
```
여기서 우리는 셀 A1을 가리키고 있습니다. 여기에 마법 공식을 놓을 것입니다. 보물 지도에 표적을 고정하는 것으로 생각할 수 있습니다!
## 7단계: 수식 설정
이제 웅장한 공개의 시간입니다! 등록된 함수를 호출하는 공식을 설정해 보겠습니다.
```csharp
// 추가 기능에 있는 수식 이름을 설정합니다.
cell.Formula = "=TEST_UDF()";
```
이 줄을 통해 우리는 Excel에 셀 A1에서 함수를 사용하라고 말하고 있습니다. 마치 Excel에 명령을 내리고 "이봐, 이걸 해!"라고 말하는 것과 같습니다.
## 8단계: 통합 문서 저장
마지막으로, 우리의 걸작을 구할 시간입니다.
```csharp
// XLSX 형식으로 출력하여 통합 문서를 저장합니다.
workbook.Save(outputDir + @"test_udf.xlsx", Aspose.Cells.SaveFormat.Xlsx);
```
여기서 우리는 워크북을 XLSX 파일로 저장합니다. 이 마지막 단계는 그림을 액자에 넣고 전시할 준비를 하는 것과 같습니다!
## 9단계: 실행 확인
마지막으로 콘솔에 성공 메시지를 출력하여 마무리하겠습니다.
```csharp
Console.WriteLine("RegisterAndCallFuncFromAddIn executed successfully.");
```
이 선은 우리의 승리 깃발 역할을 합니다. 모든 것이 순조롭게 진행되었다는 것을 확인하는 좋은 작은 터치입니다.
## 결론 
이제 다 됐습니다! Aspose.Cells for .NET을 사용하여 Excel 추가 기능에서 함수를 등록하고 호출하는 방법을 배웠을 뿐만 아니라, 관련된 각 단계에 대한 더 깊은 이해도 얻었습니다. 이제 삶이 조금 더 쉬워졌죠? 그러니 직접 시도해 보는 건 어떨까요? Excel 추가 기능을 살펴보고 스프레드시트에 새로운 수준의 상호 작용과 기능을 추가하세요.
## 자주 묻는 질문
### Excel 추가 기능이란 무엇인가요?  
Excel 추가 기능은 사용자가 Excel의 기능을 확장할 수 있도록 사용자 정의 기능, 함수 또는 명령을 추가하는 프로그램입니다.
### Aspose.Cells를 로컬에 설치하지 않고도 사용할 수 있나요?  
아니요, .NET 애플리케이션에서 Aspose.Cells 라이브러리를 사용하려면 먼저 설치해야 합니다.
### Aspose.Cells에 대한 임시 라이센스를 받으려면 어떻게 해야 하나요?  
 당신은 그들을 방문 할 수 있습니다[임시 라이센스 페이지](https://purchase.aspose.com/temporary-license/) 자세한 내용은.
### 하나의 추가 기능에서 여러 함수를 호출할 수 있나요?  
 네! 동일한 추가 기능 파일에서 여러 기능을 등록할 수 있습니다.`RegisterAddInFunction` 방법.
### Aspose.Cells에 대한 추가 문서는 어디에서 찾을 수 있나요?  
 사이트에서 포괄적인 문서를 탐색할 수 있습니다.[여기](https://reference.aspose.com/cells/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
