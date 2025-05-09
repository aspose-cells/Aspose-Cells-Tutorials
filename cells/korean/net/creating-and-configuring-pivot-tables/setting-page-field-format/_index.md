---
"description": "Aspose.Cells for .NET을 사용하여 피벗 테이블의 페이지 필드 서식을 프로그래밍 방식으로 설정하는 방법을 알아보세요. 원활한 데이터 관리를 위한 단계별 튜토리얼을 따라해 보세요."
"linktitle": ".NET에서 프로그래밍 방식으로 페이지 필드 형식 설정"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": ".NET에서 프로그래밍 방식으로 페이지 필드 형식 설정"
"url": "/ko/net/creating-and-configuring-pivot-tables/setting-page-field-format/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 프로그래밍 방식으로 페이지 필드 형식 설정

## 소개
코드를 통해 Excel 파일을 만들고 조작하는 것은 특히 대규모 데이터 세트를 분석해야 할 때 매우 유용합니다. .NET용 Aspose.Cells는 여러분이 활용할 수 있는 훌륭한 도구 중 하나로, Excel 파일과 프로그래밍 방식으로 상호 작용하고 복잡한 보고 구조를 만들 수 있도록 해줍니다. 이 튜토리얼에서는 이 강력한 라이브러리를 사용하여 피벗 테이블에서 페이지 필드 서식을 설정하는 방법을 자세히 살펴보겠습니다. 숙련된 개발자든 초보자든 이 가이드를 마치면 .NET에서 피벗 테이블과 다양한 설정을 사용하는 방법을 완벽하게 이해하게 될 것입니다.
## 필수 조건
코딩에 본격적으로 들어가기 전에 모든 것이 제대로 설정되어 있는지 확인해 보겠습니다. 필요한 것은 다음과 같습니다.
- Visual Studio: .NET 코드를 작성하고 실행할 수 있는 작업 환경입니다.
- Aspose.Cells: 라이브러리를 다운로드할 수 있습니다 [여기](https://releases.aspose.com/cells/net/).
- C#에 대한 기본 지식: C# 프로그래밍에 대한 지식은 코드 조각을 더 잘 이해하는 데 도움이 됩니다.
- Excel 파일: Excel 파일을 준비하세요(예: `Book1.xls`) 피벗 테이블 생성에 적합한 데이터가 포함되어 있습니다. 
아직 Aspose.Cells의 무료 평가판을 받아보지 않으셨다면 지금 바로 받아보세요. [여기](https://releases.aspose.com/).
## 패키지 가져오기
시작하려면 프로젝트에 적합한 패키지를 가져와야 합니다. 먼저 C# 프로젝트에 Aspose.Cells 라이브러리 참조를 추가합니다. 방법은 다음과 같습니다.
```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
using Aspose.Cells.Pivot;
```
이렇게 하면 Aspose.Cells를 사용하여 Excel 파일을 조작하는 데 필요한 모든 클래스와 메서드가 가져옵니다.
## 1단계: 작업 공간 설정
먼저 Excel 파일을 저장할 작업 디렉터리를 정의하세요. 예를 들어, 다음과 같이 변수를 선언할 수 있습니다.
```csharp
string dataDir = "Your Document Directory";
```
## 통합 문서 로드
다음으로, Excel 템플릿을 로드해야 합니다. 이는 운영의 맥락을 확립하기 때문에 필수적인 단계입니다.
```csharp
Workbook workbook = new Workbook(dataDir + "Book1.xls");
```
이 줄은 지정된 디렉토리에서 기존 통합 문서를 로드합니다.
## 2단계: 워크시트에 액세스
통합 문서가 로드되면 피벗 테이블 또는 분석하려는 데이터가 포함된 워크시트에 액세스할 차례입니다. 방법은 다음과 같습니다.
```csharp
Worksheet worksheet = workbook.Worksheets[0];
```
이렇게 하면 로드된 통합 문서의 첫 번째 워크시트가 표시됩니다. 여러 시트로 작업하는 경우 색인을 쉽게 수정할 수 있습니다.
## 3단계: 피벗 테이블 액세스
계속해서 선택한 워크시트에서 피벗 테이블에 액세스해 보겠습니다. 단일 피벗 테이블을 사용하는 경우 해당 인덱스를 다음과 같이 설정할 수 있습니다. `0`:
```csharp
int pivotindex = 0;
// 피벗 테이블 액세스
PivotTable pivotTable = worksheet.PivotTables[pivotindex];
```
이 코드 조각은 워크시트에서 첫 번째 피벗 테이블을 선택합니다. 
## 4단계: 피벗 테이블 구성
이제 흥미로운 부분입니다! 피벗 테이블에 행의 총합계를 표시하도록 설정해 보겠습니다.
```csharp
pivotTable.RowGrand = true;
```
이 줄은 보고서에 총계가 표시되도록 보장하며, 이는 데이터 분석을 위한 유용한 요약이 될 수 있습니다.
## 5단계: 행 필드 액세스 및 구성
다음으로 피벗 테이블의 행 필드에 액세스해야 합니다.
```csharp
Aspose.Cells.Pivot.PivotFieldCollection pivotFields = pivotTable.RowFields;
```
이 컬렉션을 사용하면 필요에 따라 필드를 조작할 수 있습니다.
## 첫 번째 행 필드 구성
특정 소계 유형을 설정하고 싶으신가요? 컬렉션의 첫 번째 필드에 접근하여 설정해 보겠습니다.
```csharp
Aspose.Cells.Pivot.PivotField pivotField = pivotFields[0];
// 소계 설정.
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Sum, true);
pivotField.SetSubtotals(Aspose.Cells.Pivot.PivotFieldSubtotalType.Count, true);
```
활성화함으로써 `Sum` 그리고 `Count` 소계를 사용하면 보고서에서 데이터를 빠르게 요약할 수 있습니다.
## 6단계: 자동 정렬 옵션 설정
다음으로, 스마트 정렬 기능을 사용해 보겠습니다. 이렇게 하면 피벗 테이블에서 데이터가 의미 있는 순서로 정렬됩니다.
```csharp
// 자동 정렬 옵션 설정.
pivotField.IsAutoSort = true;
pivotField.IsAscendSort = true;
pivotField.AutoSortField = -5; // 미리 정의된 정렬 필드를 사용합니다.
```
이 코드 조각은 자동 정렬을 활성화하고 오름차순을 지정합니다. 
## 7단계: 자동 표시 옵션 설정
데이터를 더욱 세부적으로 필터링하시겠습니까? 자동 표시 옵션은 정의된 조건에서 특정 데이터 포인트를 표시하는 데 유용합니다.
```csharp
// 자동표시 옵션 설정.
pivotField.IsAutoShow = true;
pivotField.IsAscendShow = false;
pivotField.AutoShowField = 0; // 자동으로 표시할 필드를 지정하세요.
```
이렇게 하면 피벗 테이블에 관련 데이터만 표시되어 명확성과 집중도가 향상됩니다.
## 8단계: 작업 저장
이 모든 구성을 완료한 후에는 작업 내용을 잃어버리고 싶지 않을 겁니다! 수정된 통합 문서를 다음과 같이 저장하세요.
```csharp
workbook.Save(dataDir + "output.xls");
```
이제 문서 디렉토리에서 새로 생성된 Excel 파일을 찾을 수 있습니다.
## 결론
자, 여기까지입니다! Aspose.Cells for .NET을 사용하여 피벗 테이블에서 페이지 필드 서식을 프로그래밍 방식으로 설정하는 포괄적이고 실용적인 방법을 살펴보았습니다. 제공된 간단한 단계를 따라 하면 보고 요구 사항에 맞게 Excel 데이터를 수정하는 데 자신감을 가질 수 있을 것입니다. C#의 강력한 기능과 Aspose.Cells를 결합하면 놀라운 결과를 얻을 수 있습니다.
## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 개발자가 Excel 파일을 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 .NET 라이브러리입니다.
### Aspose.Cells를 어떻게 설치하나요?
에서 직접 다운로드할 수 있습니다. [Aspose 웹사이트](https://releases.aspose.com/cells/net/).
### Excel을 설치하지 않고도 Aspose.Cells를 사용할 수 있나요?
네, Aspose.Cells는 Microsoft Excel을 설치할 필요가 없는 독립 실행형 라이브러리입니다.
### 자세한 지원은 어디에서 찾을 수 있나요?
자세한 지원 및 포럼은 다음에서 확인하실 수 있습니다. [Aspose 지원](https://forum.aspose.com/c/cells/9).
### 임시면허를 받으려면 어떻게 해야 하나요?
임시면허를 취득할 수 있습니다. [여기](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}