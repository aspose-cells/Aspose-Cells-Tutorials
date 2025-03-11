---
title: Excel에서 워크시트에 목록 상자 추가
linktitle: Excel에서 워크시트에 목록 상자 추가
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 Excel 워크시트에 목록 상자를 추가하는 방법을 알아보세요. 간단한 단계별 가이드를 따르고 Excel 시트를 대화형으로 만들어보세요.
weight: 20
url: /ko/net/excel-shapes-controls/add-list-box-to-worksheet-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에서 워크시트에 목록 상자 추가

## 소개
목록 상자와 같은 대화형 요소를 Excel 워크시트에 추가하면 데이터 관리와 프레젠테이션을 크게 개선할 수 있습니다. 대화형 양식이나 사용자 지정 데이터 입력 도구를 만들 때 목록 상자로 사용자 입력을 제어하는 기능은 매우 중요합니다. Aspose.Cells for .NET은 Excel 파일에서 이러한 컨트롤을 추가하고 관리하는 효율적인 방법을 제공합니다. 이 가이드에서는 Aspose.Cells for .NET을 사용하여 워크시트에 목록 상자를 추가하는 과정을 안내합니다.
## 필수 조건
코딩에 들어가기 전에 다음 도구와 리소스가 있는지 확인하세요.
-  .NET 라이브러리용 Aspose.Cells: 여기에서 다운로드할 수 있습니다.[.NET용 Aspose.Cells 다운로드 페이지](https://releases.aspose.com/cells/net/).
- 개발 환경: Visual Studio와 같이 .NET 개발을 지원하는 모든 IDE.
- .NET Framework: 프로젝트가 지원되는 버전의 .NET Framework를 타겟으로 하고 있는지 확인하세요.
 또한 다음을 고려하십시오.[임시 면허](https://purchase.aspose.com/temporary-license/) 제한 없이 모든 기능을 탐색하고 싶다면.
## 패키지 가져오기
시작하기 전에 필요한 Aspose.Cells 네임스페이스를 가져왔는지 확인하세요. 방법은 다음과 같습니다.
```csharp
using System.IO;
using Aspose.Cells;
using Aspose.Cells.Drawing;
```
이 튜토리얼에서는 목록 상자를 추가하는 과정을 여러 개의 간단한 단계로 나눕니다. 모든 것이 예상대로 작동하는지 확인하기 위해 각 단계를 주의 깊게 따르세요.
## 1단계: 문서 디렉토리 설정
Excel 파일을 만들기 전에 저장할 위치가 필요합니다. 디렉토리를 설정하는 방법은 다음과 같습니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 아직 존재하지 않으면 디렉토리를 생성합니다.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
이 단계에서는 파일을 저장할 위치를 정의합니다. 코드는 디렉토리가 있는지 확인하고, 없으면 디렉토리를 만듭니다. 이렇게 하면 나중에 "파일을 찾을 수 없음" 오류가 발생하지 않습니다.
## 2단계: 새 통합 문서 만들기 및 첫 번째 워크시트 액세스
다음으로, 새 통합 문서를 만들고 목록 상자를 추가할 첫 번째 워크시트에 액세스하겠습니다.
```csharp
// 새로운 통합 문서를 만듭니다.
Workbook workbook = new Workbook();
// 첫 번째 워크시트를 받으세요.
Worksheet sheet = workbook.Worksheets[0];
```
통합 문서는 본질적으로 Excel 파일입니다. 여기서는 새 통합 문서를 만들고 첫 번째 워크시트에 액세스하는데, 여기에 목록 상자를 배치합니다. 컨트롤을 칠할 빈 캔버스를 만드는 것으로 생각하세요.
## 3단계: 목록 상자에 대한 데이터 입력
목록 상자를 추가하기 전에 목록 상자가 참조할 일부 데이터를 채워야 합니다.
```csharp
// 워크시트 셀 컬렉션을 가져옵니다.
Cells cells = sheet.Cells;
// 라벨에 대한 값을 입력하세요.
cells["B3"].PutValue("Choose Dept:");
// 라벨을 굵게 설정합니다.
cells["B3"].GetStyle().Font.IsBold = true;
// 목록 상자에 값을 입력합니다.
cells["A2"].PutValue("Sales");
cells["A3"].PutValue("Finance");
cells["A4"].PutValue("MIS");
cells["A5"].PutValue("R&D");
cells["A6"].PutValue("Marketing");
cells["A7"].PutValue("HRA");
```
여기서는 워크시트에 텍스트를 추가합니다. "부서 선택:" 라벨은 셀 B3에 배치되고 글꼴은 굵게 설정됩니다. 열 A에서 목록 상자의 입력 범위로 사용될 값을 삽입하여 다양한 부서를 나타냅니다. 이 입력 범위는 사용자가 목록 상자와 상호 작용할 때 선택하는 것입니다.
## 4단계: 워크시트에 목록 상자 추가
이제 데이터를 설정했으니 목록 상자 컨트롤 자체를 추가해 보겠습니다.
```csharp
// 새로운 목록 상자를 추가합니다.
Aspose.Cells.Drawing.ListBox listBox = sheet.Shapes.AddListBox(2, 0, 3, 0, 122, 100);
```
이 코드는 워크시트에 목록 상자를 추가합니다. 매개변수는 목록 상자의 위치와 크기를 정의합니다. 목록 상자는 너비 122, 높이 100으로 행 2, 열 0에 배치됩니다. 이는 워크시트에서 목록 상자가 나타날 위치를 결정하는 좌표와 크기입니다.
## 5단계: 목록 상자 속성 설정
다음으로, 목록 상자의 다양한 속성을 설정하여 목록 상자가 완벽하게 작동하도록 만들어 보겠습니다.
```csharp
// 배치 유형을 설정합니다.
listBox.Placement = PlacementType.FreeFloating;
// 연결된 셀을 설정합니다.
listBox.LinkedCell = "A1";
// 입력 범위를 설정합니다.
listBox.InputRange = "A2:A7";
// 선택 유형을 설정합니다.
listBox.SelectionType = SelectionType.Single;
// 목록 상자에 3차원 음영을 설정합니다.
listBox.Shadow = true;
```
- PlacementType.FreeFloating: 이 속성은 워크시트가 어떻게 수정되든 목록 상자가 해당 위치에 고정되도록 합니다.
- LinkedCell: 목록 상자에서 선택한 값이 표시될 셀(이 경우 A1)을 설정합니다.
- InputRange: 이 범위는 목록 상자에서 옵션 목록을 어디에서 찾아야 할지 알려줍니다(이전에 설정한 A2~A7).
- SelectionType.Single: 사용자가 목록 상자에서 하나의 항목만 선택하도록 제한합니다.
- 그림자: 그림자 효과는 목록 상자에 더 3차원적인 모양을 부여하여 시각적으로 매력적으로 만들어줍니다.
## 6단계: Excel 파일 저장
마지막으로 목록 상자를 포함한 통합 문서를 저장해 보겠습니다.
```csharp
// 통합 문서를 저장합니다.
workbook.Save(dataDir + "book1.out.xls");
```
이 코드 줄은 이전에 설정한 디렉토리에 통합 문서를 저장합니다. 파일 이름은 "book1.out.xls"이지만 프로젝트에 맞는 이름을 선택할 수 있습니다.
## 결론
이제 다 됐습니다! Aspose.Cells for .NET을 사용하여 Excel 워크시트에 목록 상자를 성공적으로 추가했습니다. 몇 줄의 코드만으로 완벽하게 작동하는 목록 상자를 만들어 워크시트를 더욱 상호 작용적이고 동적으로 만들었습니다. 이 튜토리얼은 Aspose.Cells for .NET의 다른 컨트롤과 기능을 탐색할 수 있는 견고한 기반을 제공합니다. 계속 실험해 보세요. 곧 라이브러리의 방대한 기능을 마스터하게 될 겁니다!
## 자주 묻는 질문
### 목록 상자에서 여러 선택을 허용할 수 있나요?  
 네, 변경할 수 있습니다.`SelectionType` 에게`SelectionType.Multi` 여러 선택을 허용합니다.
### 목록 상자의 모양을 변경할 수 있나요?  
물론입니다! Aspose.Cells를 사용하면 목록 상자의 모양, 크기, 글꼴, 심지어 색상까지 사용자 지정할 수 있습니다.
### 나중에 목록 상자를 제거해야 하는 경우에는 어떻게 해야 하나요?  
 목록 상자에 액세스하고 제거할 수 있습니다.`Shapes` 수집을 사용하여`sheet.Shapes.RemoveAt(index)`.
### 목록 상자를 다른 셀에 연결할 수 있나요?  
 네, 간단히 변경하세요`LinkedCell` 선택한 값을 표시하려는 다른 셀에 속성을 추가합니다.
### 목록 상자에 항목을 더 추가하려면 어떻게 해야 하나요?  
지정된 셀에 더 많은 값을 삽입하여 입력 범위를 업데이트하면 목록 상자가 자동으로 업데이트됩니다.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
