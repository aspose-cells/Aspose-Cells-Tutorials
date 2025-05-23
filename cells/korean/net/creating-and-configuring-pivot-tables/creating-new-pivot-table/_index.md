---
"description": "Aspose.Cells를 사용하여 .NET에서 프로그래밍 방식으로 피벗 테이블을 만드는 방법을 단계별 가이드를 통해 알아보세요. 데이터를 효율적으로 분석할 수 있습니다."
"linktitle": ".NET에서 프로그래밍 방식으로 새 피벗 테이블 만들기"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": ".NET에서 프로그래밍 방식으로 새 피벗 테이블 만들기"
"url": "/ko/net/creating-and-configuring-pivot-tables/creating-new-pivot-table/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# .NET에서 프로그래밍 방식으로 새 피벗 테이블 만들기

## 소개
피벗 테이블을 만드는 것은, 특히 프로그래밍 방식으로 작업할 때, 어려운 작업처럼 느껴질 수 있습니다. 하지만 걱정하지 마세요! Aspose.Cells for .NET을 사용하면 피벗 테이블을 만드는 것이 간단할 뿐만 아니라 데이터 분석에도 매우 효과적입니다. 이 튜토리얼에서는 .NET 애플리케이션에서 새 피벗 테이블을 만드는 방법을 단계별로 안내합니다. 판매, 스포츠 또는 기타 비즈니스 지표에 대한 데이터를 추가하든, 이 가이드를 통해 피벗 테이블을 빠르게 구축하고 실행할 수 있습니다.

## 필수 조건
시작하기 전에, 모든 준비가 완료되었는지 확인하세요. 준비해야 할 사항은 다음과 같습니다.

1. .NET Framework 설치: 컴퓨터에 .NET Framework가 설치되어 있는지 확인하세요. Aspose.Cells는 다양한 버전을 지원하지만 최신 버전을 사용하는 것이 가장 좋습니다.
2. Aspose.Cells 라이브러리: Aspose.Cells 라이브러리가 필요합니다. [여기서 다운로드하세요](https://releases.aspose.com/cells/net/) 또는 얻을 [임시 면허](https://purchase.aspose.com/temporary-license/) 평가를 위해.
3. IDE 설정: Visual Studio와 같이 C# 호환 IDE를 준비하여 새 프로젝트를 시작하세요.
4. C#에 대한 기본 지식: C# 프로그래밍에 대한 지식이 있으면 너무 어려워지지 않고 따라갈 수 있습니다.

다 준비되셨나요? 좋습니다! 이제 필요한 패키지를 가져오는 단계로 넘어가 보겠습니다.

## 패키지 가져오기
먼저, 필요한 네임스페이스를 C# 프로젝트로 가져와야 합니다. C# 파일을 열고 다음 using 지시문을 추가합니다.

```csharp
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

이러한 네임스페이스를 통해 이 튜토리얼 전체에서 사용할 통합 문서, 워크시트 및 피벗 테이블 기능에 액세스할 수 있습니다.

## 1단계: 통합 문서 개체 만들기
통합 문서를 만드는 것이 여정의 시작입니다. 새 통합 문서를 인스턴스화하고 첫 번째 워크시트에 액세스하는 것부터 시작해 보겠습니다.

```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// Workbook 개체 인스턴스화
Workbook workbook = new Workbook();

// 새로 추가된 워크시트의 참조 얻기
Worksheet sheet = workbook.Worksheets[0];
```

이 단계에서는 다음을 생성합니다. `Workbook` Excel 파일을 나타내는 인스턴스를 만들고 피벗 테이블의 놀이터가 될 첫 번째 워크시트를 가져옵니다.

## 2단계: 셀에 데이터 삽입
다음으로, 워크시트에 샘플 데이터를 채워 보겠습니다. 피벗 테이블에 요약할 내용을 추가하기 위해 다양한 스포츠, 분기, 매출 수치에 대한 행을 입력하겠습니다.

```csharp
Cells cells = sheet.Cells;

// 셀에 값 설정
Cell cell = cells["A1"];
cell.PutValue("Sport");
cell = cells["B1"];
cell.PutValue("Quarter");
cell = cells["C1"];
cell.PutValue("Sales");

// 데이터셀 채우기 = cells["A2"];
cell.PutValue("Golf");
// ... 더 많은 데이터 항목
```

여기서는 열 머리글을 정의하고 각 머리글 아래에 값을 삽입합니다. 이 데이터는 피벗 테이블의 소스 역할을 하므로 체계적으로 정리해야 합니다! 이 단계를 따라 하면 포괄적인 데이터세트를 만들 수 있습니다.

## 3단계: 피벗 테이블 추가
데이터가 준비되었으니 이제 피벗 테이블을 만들 차례입니다. 워크시트의 피벗 테이블 모음을 사용하여 새 피벗 테이블을 추가합니다.

```csharp
Aspose.Cells.Pivot.PivotTableCollection pivotTables = sheet.PivotTables;

// 워크시트에 피벗 테이블 추가
int index = pivotTables.Add("=A1:C8", "E3", "PivotTable2");
```

이 스니펫에서는 데이터 범위(이 경우 A1~C8 셀)를 참조하는 피벗 테이블을 워크시트에 추가합니다. E3 셀부터 피벗 테이블을 배치하고 이름을 "PivotTable2"로 지정합니다. 꽤 간단하죠?

## 4단계: 피벗 테이블 사용자 지정
이제 피벗 테이블이 완성되었으니, 의미 있는 요약을 표시하도록 테이블을 맞춤설정해 보겠습니다. 피벗 테이블의 행, 열, 데이터 영역에 표시되는 내용을 제어할 수 있습니다.

```csharp
// 새로 추가된 피벗 테이블 인스턴스에 액세스하기
Aspose.Cells.Pivot.PivotTable pivotTable = pivotTables[index];

// 행의 총계를 표시하지 않습니다.
pivotTable.RowGrand = false;

// 첫 번째 필드를 행 영역으로 끌어다 놓습니다.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Row, 0);

// 두 번째 필드를 열 영역으로 끌어다 놓습니다.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Column, 1);

// 세 번째 필드를 데이터 영역으로 끌어다 놓습니다.
pivotTable.AddFieldToArea(Aspose.Cells.Pivot.PivotFieldType.Data, 2);
```

이 단계에서는 피벗 테이블에서 행의 총합계를 숨기도록 설정한 다음, 행, 열 및 데이터 영역에 어떤 필드를 포함할지 지정합니다. 스포츠 종목명은 행을 채우고, 분기는 열을 채우며, 매출 수치는 요약 정보를 제공합니다.

## 5단계: 통합 문서 저장
마지막으로, 우리는 새로 만든 통합 문서를 저장하여 노력의 결실을 보고 싶습니다.

```csharp
// Excel 파일 저장
workbook.Save(dataDir + "pivotTable_test_out.xls");
```

적절한 경로만 제공하면 피벗 테이블 출력이 Excel 파일로 저장되므로 열어서 검토할 수 있습니다.

## 결론
Aspose.Cells for .NET을 사용하여 프로그래밍 방식으로 피벗 테이블을 만들면, 특히 대용량 데이터 세트를 다룰 때 시간을 크게 절약할 수 있습니다. 프로젝트 설정, 필요한 패키지 가져오기, 데이터 채우기, 그리고 사용자 지정 가능한 피벗 테이블을 처음부터 만드는 방법을 배웠습니다. 다음에 숫자 때문에 어려움을 겪을 때 이 튜토리얼을 기억하고 Aspose.Cells에 맡겨 보세요.

## 자주 묻는 질문
### Aspose.Cells란 무엇인가요?
Aspose.Cells는 Excel 스프레드시트를 프로그래밍 방식으로 만들고 관리하기 위한 강력한 .NET 라이브러리입니다.

### Aspose.Cells 무료 체험판이 있나요?
네, 무료 체험판을 받으실 수 있습니다. [여기](https://releases.aspose.com/).

### 피벗 테이블의 모양을 사용자 지정할 수 있나요?
물론입니다! 피벗 테이블의 서식, 레이아웃, 스타일까지 필요에 맞게 사용자 지정할 수 있습니다.

### Aspose.Cells에 대한 더 많은 예제와 문서는 어디에서 찾을 수 있나요?
확인할 수 있습니다 [선적 서류 비치](https://reference.aspose.com/cells/net/) 포괄적인 가이드와 예시를 확인하세요.

### Aspose.Cells에 대한 지원은 어떻게 받을 수 있나요?
다음을 통해 지원을 받을 수 있습니다. [Aspose 포럼](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}