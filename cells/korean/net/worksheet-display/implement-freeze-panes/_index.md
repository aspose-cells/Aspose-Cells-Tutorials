---
title: 워크시트에서 동결 창 구현
linktitle: 워크시트에서 동결 창 구현
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 자세한 단계별 가이드를 통해 Aspose.Cells for .NET을 사용하여 Excel에서 동결 창을 구현하는 방법을 알아보세요. 워크시트의 유용성을 효율적으로 향상하세요.
weight: 15
url: /ko/net/worksheet-display/implement-freeze-panes/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 워크시트에서 동결 창 구현

## 소개
방대한 데이터 세트가 있는 Excel 워크시트가 있다고 상상해보세요. 아래로 스크롤하거나 위로 스크롤할 때마다 중요한 헤더를 추적하지 못합니다. 스크롤하는 동안 헤더가 제자리에 그대로 유지된다면 편리하지 않겠습니까? 바로 여기서 고정 패널이 등장하여 탐색을 원활하고 효율적으로 만듭니다. Aspose.Cells for .NET은 이 프로세스를 간소화하여 고정 패널을 원활하게 구현할 수 있는 기능을 제공합니다. 이 가이드에서는 프로세스를 단계별로 나누어 안내하여 고정된 헤더를 즉시 설정할 수 있도록 합니다.
## 필수 조건
시작하기 전에 몇 가지를 준비하세요.
-  .NET용 Aspose.Cells 라이브러리: 이 라이브러리는 여기에서 다운로드해야 합니다.[Aspose의 릴리스 페이지](https://releases.aspose.com/cells/net/).
- .NET Framework 설치: 개발 환경에 .NET이 설치되어 있는지 확인하세요.
- C#에 대한 기본 지식: C#에 대한 지식이 있으면 따라가는 데 도움이 됩니다.
- Excel 파일: 동결 창을 적용할 Excel 파일을 준비합니다(예: "book1.xls").
Aspose.Cells에 대한 자세한 내용은 다음에서 확인할 수 있습니다.[문서 페이지](https://reference.aspose.com/cells/net/).

## 패키지 가져오기
필요한 패키지를 가져오는 것으로 시작해 보겠습니다. C# 프로젝트를 열고 다음을 가져오세요.
```csharp
using System.IO;
using Aspose.Cells;
```
패키지가 설정되었으니, 단계별 가이드로 넘어가겠습니다.
Aspose.Cells for .NET을 사용하여 동결 패널을 설정하는 각 단계를 살펴보겠습니다. 각 단계를 주의 깊게 따르면 워크시트에 동결 패널이 손쉽게 적용됩니다.
## 1단계: 문서 디렉토리 경로 정의
 Excel 파일을 열기 전에 문서 경로를 지정해야 합니다.`dataDir` 파일의 디렉토리 경로를 보관하는 변수입니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
```
 바꾸다`"Your Document Directory"` Excel 파일이 저장된 실제 경로와 함께. 이렇게 하면 프로그램이 파일을 찾는 데 도움이 됩니다.
## 2단계: FileStream을 사용하여 Excel 파일 열기
다음으로, Aspose.Cells가 마법을 부릴 수 있도록 Excel 파일을 로드해야 합니다. 이를 위해 파일 스트림을 만들고 해당 스트림을 사용하여 Excel 파일을 엽니다.
```csharp
// 열려는 Excel 파일을 포함하는 파일 스트림 생성
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
파일 스트림을 사용하면 명시적으로 변경 사항을 저장할 때까지 원본 파일을 변경하지 않고도 Aspose.Cells에서 액세스할 수 있는 파일을 열 수 있습니다.
## 3단계: 통합 문서 개체 인스턴스화
 파일 스트림이 제자리에 있으면 이제 다음을 생성할 시간입니다.`Workbook` 개체. 이 개체는 전체 Excel 통합 문서를 나타내므로 필수적이며 파일 내에서 개별 시트, 셀 및 설정으로 작업할 수 있습니다.
```csharp
// Workbook 개체 인스턴스화
// 파일 스트림을 통해 Excel 파일 열기
Workbook workbook = new Workbook(fstream);
```
 생각해 보세요`Workbook` 모든 시트를 함께 보관하는 바인더로. 바인더를 열면 그 안의 모든 페이지(워크시트)에 접근할 수 있습니다.
## 4단계: 첫 번째 워크시트에 액세스
이제 통합 문서가 로드되었으므로 동결 창을 적용할 워크시트를 선택할 수 있습니다. 이 예에서는 첫 번째 시트로 작업합니다. Aspose.Cells를 사용하면 인덱싱을 통해 시트를 쉽게 선택할 수 있습니다.
```csharp
// Excel 파일의 첫 번째 워크시트에 액세스하기
Worksheet worksheet = workbook.Worksheets[0];
```
 다른 시트에서 작업해야 하는 경우 인덱스를 조정하기만 하면 됩니다.`workbook.Worksheets[0]`.
## 5단계: 동결 창 설정 적용
 마법이 일어나는 곳은 바로 여기입니다! 동결 창을 설정하려면 다음을 사용하세요.`FreezePanes`고정을 시작할 행과 열을 지정하고, 고정할 행과 열의 개수도 지정하는 방법입니다.
```csharp
// 동결 창 설정 적용
worksheet.FreezePanes(3, 2, 3, 2);
```
매개변수를 분석해 보겠습니다.
- 첫 번째 행(3): 행 3에서 동결을 시작합니다.
- 첫 번째 열(2): 열 2에서 동결을 시작합니다.
- 행 개수(3): 3개 행을 고정합니다.
- 열 개수(2): 2개의 열을 고정합니다.
특정 요구 사항에 따라 이러한 값을 조정합니다. 동결점은 지정된 행과 열의 교차점이 됩니다.
## 6단계: 수정된 Excel 파일 저장
 동결 패널을 적용한 후에는 변경 사항을 저장할 차례입니다. 수정된 통합 문서 파일을 저장하면 동결 설정이 유지됩니다. 다음을 사용하여 업데이트된 파일을 저장할 수 있습니다.`Save` 방법.
```csharp
// 수정된 Excel 파일 저장하기
workbook.Save(dataDir + "output.xls");
```
원본 파일도 보존하려면 다른 이름으로 저장해야 합니다.
## 7단계: 파일 스트림 닫기
마지막으로 파일 스트림을 닫는 것을 기억하세요. 이렇게 하면 시스템 리소스가 해제되고 파일에 대한 모든 열린 연결이 완료됩니다.
```csharp
// 모든 리소스를 해제하기 위해 파일 스트림을 닫습니다.
fstream.Close();
```
스트림을 닫는 것은 작업을 마친 후 파일을 다시 선반에 올려놓는 것으로 생각하세요. 좋은 청소 습관입니다.

## 결론
축하합니다! Aspose.Cells for .NET을 사용하여 Excel 워크시트에 동결 창을 성공적으로 적용했습니다. 이 기술은 대용량 데이터 세트를 관리하고 데이터를 스크롤하는 동안 헤더나 특정 행과 열이 계속 표시되도록 하는 데 매우 유용합니다. 이 단계별 가이드를 따르면 자신 있게 동결 창을 구현하고 스프레드시트의 유용성을 향상시킬 수 있습니다.
## 자주 묻는 질문
### 통합 문서에서 여러 개의 시트를 고정할 수 있나요?
 네, 간단히 반복하세요`FreezePanes` 각 시트에 적용하려는 방법을 선택하세요.
### 시트의 범위를 초과하는 행과 열 값을 사용하면 어떻게 되나요?
Aspose.Cells는 예외를 발생시키므로 값이 워크시트의 범위 내에 있는지 확인하세요.
### 동결 창 설정을 적용한 후에 조정할 수 있나요?
 물론입니다! 그냥 전화하세요`FreezePanes`설정을 업데이트하기 위해 새로운 매개변수를 사용하여 다시 메서드를 실행합니다.
### 동결 창은 모든 버전의 Excel 파일에서 작동합니까?
네, 동결 창은 Aspose.Cells에서 지원하는 대부분의 Excel 형식(예: XLS, XLSX)에서 보존됩니다.
### 유리창의 녹은 부분을 해동할 수 있나요?
 동결 유리창을 제거하려면 전화하기만 하면 됩니다.`UnfreezePanes()` 워크시트에.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
