---
title: Aspose.Cells를 사용하여 Excel에서 행과 열 그룹 해제
linktitle: Aspose.Cells를 사용하여 Excel에서 행과 열 그룹 해제
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 포괄적인 가이드를 통해 Aspose.Cells for .NET을 사용하여 Excel에서 행과 열을 그룹 해제하는 방법을 알아보세요. Excel 데이터 조작을 간소화하세요.
weight: 15
url: /ko/net/row-and-column-management/ungrouping-rows-and-columns/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells를 사용하여 Excel에서 행과 열 그룹 해제

## 소개
Excel 파일을 처리할 때 행과 열을 그룹 해제해야 하는 상황에 처할 수 있습니다. 스프레드시트를 정리하든 더 나은 프레젠테이션을 위해 데이터를 다시 포맷하든 Aspose.Cells for .NET은 프로세스를 단순화하는 환상적인 도구입니다. 이 튜토리얼에서는 Aspose.Cells를 사용하여 Excel에서 행과 열을 그룹 해제하는 단계를 안내합니다. 끝까지 읽으면 Excel 파일을 프로그래밍 방식으로 사용하는 방법을 확실히 이해하게 될 것입니다.
## 필수 조건
코드에 뛰어들기 전에 모든 것이 설정되어 있는지 확인해 보겠습니다. 필요한 것은 다음과 같습니다.
1.  Visual Studio: 컴퓨터에 Visual Studio의 작동 버전이 설치되어 있어야 합니다. 아직 설치되어 있지 않으면 다음에서 다운로드할 수 있습니다.[Visual Studio 사이트](https://visualstudio.microsoft.com/).
2. .NET용 Aspose.Cells: Aspose.Cells 라이브러리를 다운로드해야 합니다. 다음에서 가져올 수 있습니다.[Aspose 릴리스 페이지](https://releases.aspose.com/cells/net/) . 필요한 라이센스가 있는지 확인하십시오. 라이센스는 구매하거나 다음을 통해 얻을 수 있습니다.[임시 면허](https://purchase.aspose.com/temporary-license/).
3. C#에 대한 기본 지식: C# 프로그래밍에 대한 기본적인 이해가 있으면 더 쉽게 따라갈 수 있습니다.
모든 준비가 끝나면 이제 재밌는 부분인 코드로 넘어가보겠습니다!
## 패키지 가져오기
시작하려면 C# 프로젝트에서 필요한 패키지를 가져와야 합니다. 방법은 다음과 같습니다.
1. Visual Studio에서 프로젝트를 엽니다.
2. Aspose.Cells 라이브러리에 참조를 추가합니다. 프로젝트의 참조를 마우스 오른쪽 버튼으로 클릭하고 참조 추가를 선택하면 됩니다. Aspose.Cells DLL을 저장한 위치로 이동합니다.
3. C# 파일의 맨 위에 다음 using 지시문을 추가합니다.
```csharp
using System.IO;
using Aspose.Cells;
```
이제 모든 것이 설정되었으니 Excel 시트에서 행과 열의 그룹을 해제하는 단계를 살펴보겠습니다. 
## 1단계: 문서 디렉토리 정의
먼저, Excel 파일이 있는 디렉토리를 지정해야 합니다. 다음과 같이 설정할 수 있습니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
```
 바꾸다`"Your Document Directory"` Excel 파일이 저장된 컴퓨터의 실제 경로를 입력합니다. 
## 2단계: 파일 스트림 만들기
다음으로, Excel 파일을 열려면 파일 스트림을 만들어야 합니다. 이렇게 하면 됩니다.
```csharp
// 열려는 Excel 파일을 포함하는 파일 스트림 생성
FileStream fstream = new FileStream(dataDir + "book1.xls", FileMode.Open);
```
 여기서는 이름이 지정된 파일을 엽니다.`book1.xls`. 이 파일이 지정한 디렉토리에 있는지 확인하세요. 그렇지 않으면 파일을 찾을 수 없다는 오류가 발생합니다.
## 3단계: 통합 문서 개체 인스턴스화
이제 Excel 파일을 Workbook 객체에 로드해 보겠습니다. 이렇게 하면 통합 문서를 프로그래밍 방식으로 조작할 수 있습니다.
```csharp
// Workbook 개체 인스턴스화
// 파일 스트림을 통해 Excel 파일 열기
Workbook workbook = new Workbook(fstream);
```
이 코드 줄을 사용하면 Excel 파일을 메모리에 성공적으로 로드하여 작업할 준비가 됩니다.
## 4단계: 워크시트에 액세스
워크북을 만든 후 다음 단계는 행과 열을 그룹 해제할 특정 워크시트에 액세스하는 것입니다. 방법은 다음과 같습니다.
```csharp
// Excel 파일의 첫 번째 워크시트에 액세스하기
Worksheet worksheet = workbook.Worksheets[0];
```
이 경우, 우리는 첫 번째 워크시트에 접근하고 있습니다. 데이터가 다른 시트에 있는 경우, 그에 따라 인덱스를 변경할 수 있습니다.
## 5단계: 행 그룹 해제
이제 흥미로운 부분이 나옵니다! 첫 번째 여섯 행(행 0에서 행 5까지)을 그룹 해제해 보겠습니다. 다음 코드를 사용하세요.
```csharp
// 첫 번째 6개 행 그룹 해제(0~5)
worksheet.Cells.UngroupRows(0, 5);
```
이 방법은 지정된 행에 적용된 모든 그룹화를 제거합니다. 정말 쉽죠!
## 6단계: 열 그룹 해제
행과 마찬가지로 열도 그룹 해제할 수 있습니다. 처음 세 열(열 0에서 열 2까지)을 그룹 해제하는 방법은 다음과 같습니다.
```csharp
// 첫 번째 3개 열 그룹 해제(0~2)
worksheet.Cells.UngroupColumns(0, 2);
```
## 7단계: 수정된 Excel 파일 저장
 행과 열을 그룹 해제한 후 다음 단계는 변경 사항을 Excel 파일에 다시 저장하는 것입니다. 다음을 사용하여 이 작업을 수행할 수 있습니다.`Save` 방법:
```csharp
// 수정된 Excel 파일 저장하기
workbook.Save(dataDir + "output.xls");
```
 이 예에서 우리는 수정된 파일을 다음과 같이 저장합니다.`output.xls`파일 이름은 원하는 대로 변경할 수 있습니다.
## 8단계: 파일 스트림 닫기
마지막으로 리소스를 확보하려면 파일 스트림을 닫아야 합니다.
```csharp
// 모든 리소스를 해제하기 위해 파일 스트림을 닫습니다.
fstream.Close();
```
이는 애플리케이션이 필요 이상으로 오랫동안 파일 핸들을 보관하지 않도록 하는 좋은 방법입니다.
## 결론
이제 Aspose.Cells for .NET을 사용하여 Excel 파일에서 행과 열을 그룹 해제하는 방법을 성공적으로 배웠습니다. 몇 줄의 코드만 있으면 Excel 파일을 프로그래밍 방식으로 크게 변경할 수 있습니다. 보고서를 자동화하든 분석을 위해 데이터를 준비하든 이러한 기술을 마스터하면 많은 시간을 절약할 수 있습니다.
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 .NET 애플리케이션에서 Excel 파일을 작업하기 위한 강력한 라이브러리로, 스프레드시트를 쉽게 조작, 변환, 생성할 수 있습니다.
### 다른 라이브러리를 사용하여 Excel에서 행과 열의 그룹을 해제할 수 있나요?
네, .NET에서 Excel을 조작하는 데 사용할 수 있는 다른 라이브러리도 있지만 Aspose.Cells는 광범위한 기능과 사용 편의성을 제공합니다.
### 저장 후 변경 사항을 취소할 방법이 있나요?
Excel 파일을 저장하면 원본 파일의 백업이 없는 한 이전 상태를 복원할 수 없습니다.
### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?
 지원을 받으려면 다음을 방문하세요.[Aspose 지원 포럼](https://forum.aspose.com/c/cells/9)질문을 하고 해결책을 찾을 수 있는 곳입니다.
### 라이선스 없이 Aspose.Cells를 사용할 수 있나요?
예, 특정 제한 사항이 있는 Aspose.Cells를 무료로 사용할 수 있으며 시작할 수 있습니다.[임시 면허](https://purchase.aspose.com/temporary-license/) 모든 기능을 사용하려면.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
