---
title: Excel에서 모양을 앞이나 뒤로 보내기
linktitle: Excel에서 모양을 앞이나 뒤로 보내기
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel에서 모양을 앞이나 뒤로 보내는 방법을 알아보세요. 이 가이드는 팁이 포함된 단계별 튜토리얼을 제공합니다.
weight: 16
url: /ko/net/excel-shape-text-modifications/send-shape-front-back-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 모양을 앞이나 뒤로 보내기

## 소개
Excel 파일을 작업할 때 스프레드시트의 시각적 요소를 더 많이 제어해야 할 수도 있습니다. 이미지와 그래픽과 같은 도형은 데이터의 표현을 향상시킬 수 있습니다. 하지만 이러한 도형이 겹치거나 재정렬해야 하는 경우 어떻게 될까요? 바로 여기서 Aspose.Cells for .NET이 빛을 발합니다. 이 자습서에서는 Excel 워크시트에서 도형을 조작하는 단계를 안내합니다. 특히 도형을 다른 도형의 앞이나 뒤로 보내는 방법을 설명합니다. Excel 게임을 강화할 준비가 되었다면 바로 시작해 보겠습니다!
## 필수 조건
시작하기 전에 몇 가지 준비가 필요합니다.
1.  Aspose.Cells 라이브러리 설치: .NET에 대한 Aspose.Cells 라이브러리가 설치되어 있는지 확인하십시오. 찾을 수 있습니다.[여기](https://releases.aspose.com/cells/net/).
2. 개발 환경: Visual Studio 등 .NET 지원이 포함된 개발 환경이 설정되어 있는지 확인하세요.
3. C#에 대한 기본 지식: C# 프로그래밍에 익숙하면 코드 조각을 더 잘 이해하는 데 도움이 됩니다.
좋아요, 필수 조건 목록의 모든 상자를 체크하셨나요? 좋아요! 이제 재밌는 부분인 코드 작성으로 넘어가보죠!
## 패키지 가져오기
실제 코딩에 들어가기 전에 필요한 패키지를 임포트해 보겠습니다. C# 파일의 맨 위에 다음 using 지시문을 추가하기만 하면 됩니다.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
using System;
```
이러한 네임스페이스는 Excel 파일과 도형을 조작하는 데 사용하는 클래스와 메서드를 포함하고 있으므로 매우 중요합니다.
## 1단계: 파일 경로 정의
이 첫 번째 단계에서는 소스 및 출력 디렉토리를 설정해야 합니다. 여기가 Excel 파일이 있는 위치이며 수정된 파일을 저장할 위치입니다.
```csharp
//소스 디렉토리
string sourceDir = "Your Document Directory";
//출력 디렉토리
string outputDir = "Your Document Directory";
```
 바꾸다`"Your Document Directory"` Excel 파일이 저장된 실제 경로를 사용합니다.
## 2단계: 통합 문서 로드
이제 디렉토리가 설정되었으니, 조작하려는 도형이 포함된 통합 문서(Excel 파일)를 로드해 보겠습니다.
```csharp
//소스 Excel 파일 로드
Workbook wb = new Workbook(sourceDir + "sampleToFrontOrBack.xlsx");
```
 이 코드 줄은 새로운 것을 초기화합니다.`Workbook` 객체, 지정된 Excel 파일을 메모리에 로드하여 작업할 수 있도록 합니다.
## 3단계: 워크시트에 액세스 
다음으로, 우리는 모양이 있는 특정 워크시트에 액세스해야 합니다. 이 예에서는 첫 번째 워크시트를 사용하겠습니다.
```csharp
//첫 번째 워크시트에 접근하세요
Worksheet ws = wb.Worksheets[0];
```
 참조함으로써`Worksheets[0]`, 우리는 워크북의 첫 번째 시트를 타겟으로 삼고 있습니다. 모양이 다른 시트에 있는 경우 인덱스를 적절히 조정합니다.
## 4단계: 모양에 액세스
워크시트에 대한 액세스가 준비되었으니, 관심 있는 모양을 잡아보겠습니다. 이 예에서는 첫 번째와 네 번째 모양에 액세스하겠습니다.
```csharp
//첫 번째와 네 번째 모양에 접근하세요
Shape sh1 = ws.Shapes[0];
Shape sh4 = ws.Shapes[3];
```
이러한 선은 인덱스를 기반으로 워크시트에서 특정 모양을 가져옵니다.
## 5단계: 모양의 Z 순서 위치 인쇄
모양을 옮기기 전에 현재 Z-Order 위치를 인쇄해 보겠습니다. 이렇게 하면 변경하기 전에 위치를 추적하는 데 도움이 됩니다.
```csharp
//모양의 Z-Order 위치를 인쇄합니다
Console.WriteLine("Z-Order Shape 1: " + sh1.ZOrderPosition);
```
 전화로`ZOrderPosition`, 우리는 각 모양이 그림 순서에서 어떤 위치에 있는지 볼 수 있습니다.
## 6단계: 첫 번째 모양을 앞으로 보내기
이제 행동할 시간입니다! 첫 번째 모양을 Z-Order의 앞으로 보내보겠습니다.
```csharp
//이 모양을 앞으로 보내기
sh1.ToFrontOrBack(2);
```
 지나가면서`2` 에게`ToFrontOrBack`, Aspose.Cells에게 이 모양을 앞으로 가져오라고 지시합니다. 
## 7단계: 두 번째 모양의 Z 순서 위치 인쇄
두 번째 모양을 뒤로 보내기 전에, 모양이 어디에 위치해 있는지 확인해 보겠습니다.
```csharp
//모양의 Z-Order 위치를 인쇄합니다
Console.WriteLine("Z-Order Shape 4: " + sh4.ZOrderPosition);
```
이를 통해 어떤 변경을 하기 전에 네 번째 모양의 위치에 대한 통찰력을 얻을 수 있습니다.
## 8단계: 네 번째 모양을 뒤로 보내기
마지막으로, 네 번째 모양을 Z-Order 스택의 맨 뒤로 보냅니다.
```csharp
//이 모양을 뒤로 보내기
sh4.ToFrontOrBack(-2);
```
 사용 중`-2` 매개변수는 모양을 스택의 뒤쪽으로 보내 다른 모양이나 텍스트를 가리지 않도록 합니다.
## 9단계: 통합 문서 저장 
마지막 단계는 새로 배치된 모양으로 통합 문서를 저장하는 것입니다.
```csharp
//출력 Excel 파일을 저장합니다.
wb.Save(outputDir + "outputToFrontOrBack.xlsx");
```
이 명령은 수정된 통합 문서를 지정된 출력 디렉토리에 저장합니다.
## 10단계: 확인 메시지
마지막으로, 우리의 작업이 성공적으로 완료되었음을 알려주는 간단한 확인을 제공해 보겠습니다.
```csharp
Console.WriteLine("SendShapeFrontOrBackInWorksheet executed successfully.\r\n");
```
이것으로 튜토리얼의 코드를 마칩니다!
## 결론
Aspose.Cells for .NET을 사용하여 Excel에서 모양을 조작하는 것은 간단할 뿐만 아니라 강력합니다. 이 가이드를 따르면 이제 모양을 앞이나 뒤로 쉽게 보낼 수 있어 Excel 프레젠테이션을 더 잘 제어할 수 있습니다. 이러한 도구를 사용하면 스프레드시트의 시각적 매력을 향상시킬 준비가 되었습니다.
## 자주 묻는 질문
### Aspose.Cells에 어떤 프로그래밍 언어가 필요한가요?  
Aspose.Cells를 사용하려면 C#이나 .NET을 지원하는 언어를 사용해야 합니다.
### Aspose.Cells를 무료로 사용할 수 있나요?  
 네, Aspose.Cells의 무료 체험판으로 시작할 수 있습니다.[여기](https://releases.aspose.com/).
### Excel에서 어떤 종류의 모양을 조작할 수 있나요?  
사각형, 원, 선, 이미지 등 다양한 모양을 조작할 수 있습니다.
### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?  
 지원이나 질문이 있으시면 커뮤니티 포럼을 방문하세요.[여기](https://forum.aspose.com/c/cells/9).
### Aspose.Cells에 사용할 수 있는 임시 라이센스가 있나요?  
 네, 임시 면허를 요청할 수 있습니다.[여기](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
