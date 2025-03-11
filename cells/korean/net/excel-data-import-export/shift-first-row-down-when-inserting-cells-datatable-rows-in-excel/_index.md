---
title: Excel에 DataTable 행을 삽입할 때 첫 번째 행을 아래로 이동
linktitle: Excel에 DataTable 행을 삽입할 때 첫 번째 행을 아래로 이동
second_title: Aspose.Cells .NET Excel 처리 API
description: Aspose.Cells for .NET을 사용하여 첫 번째 행을 아래로 이동하지 않고 Excel에 DataTable 행을 삽입하는 방법을 알아보세요. 손쉬운 자동화를 위한 단계별 가이드.
weight: 11
url: /ko/net/excel-data-import-export/shift-first-row-down-when-inserting-cells-datatable-rows-in-excel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Excel에 DataTable 행을 삽입할 때 첫 번째 행을 아래로 이동

## 소개

Excel 스프레드시트에 새 데이터를 삽입할 때 수동으로 행을 이동하는 데 지치셨나요? 글쎄요, 운이 좋으시네요! 이 문서에서는 Aspose.Cells for .NET을 사용하여 이 프로세스를 자동화하는 방법을 자세히 알아보겠습니다. 이 튜토리얼을 마치면 Excel에서 데이터 테이블을 사용하는 방법뿐만 아니라 필요에 더 잘 맞게 가져오기 옵션을 사용자 지정하는 방법도 배우게 됩니다. 믿으세요. 이렇게 하면 많은 시간과 번거로움을 절약할 수 있습니다! 그러니 커피 한 잔을 들고 시작해 볼까요!

## 필수 조건

코딩에 들어가기 전에 모든 것이 설정되어 있는지 확인해 보겠습니다.

1. Visual Studio: Visual Studio가 설치되어 있는지 확인하세요(2017 이상이면 괜찮을 겁니다).
2.  .NET용 Aspose.Cells: Aspose.Cells 라이브러리가 필요합니다. 아직 하지 않았다면 다운로드할 수 있습니다.[여기](https://releases.aspose.com/cells/net/).
3. C# 및 Excel에 대한 기본 이해: C# 프로그래밍과 Excel의 작동 방식에 대한 기본적인 이해는 더욱 효과적으로 따라가는 데 도움이 될 것입니다.

 또한 샘플 Excel 파일을 준비해 두는 것이 좋습니다. 이 가이드에서는 샘플이라는 것을 사용합니다.`sampleImportTableOptionsShiftFirstRowDown.xlsx`. 이 파일을 만들거나 귀하의 필요에 맞는 템플릿을 찾을 수 있습니다.

## 패키지 가져오기

코딩에 들어가기 전에 필요한 패키지를 가져와야 합니다. C# 프로젝트에서 다음 네임스페이스를 포함합니다.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

이러한 패키지는 워크북, 워크시트, 표 작업에 필수적입니다.

## 1단계: 프로젝트 설정

### 새로운 C# 프로젝트 만들기

Visual Studio에서 새 C# 콘솔 애플리케이션을 만드는 것으로 시작합니다. 프로젝트에 "ExcelDataImport"와 같은 적절한 이름을 지정합니다.

### Aspose.Cells NuGet 패키지 추가

Aspose.Cells 패키지를 추가하려면 Solution Explorer에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 Manage NuGet Packages를 선택한 다음 "Aspose.Cells"를 검색합니다. 패키지를 설치하여 필요한 모든 기능에 액세스할 수 있는지 확인합니다.

## 2단계: 데이터 테이블 정의

 다음으로, 우리는 다음을 구현할 것입니다.`ICellsDataTable` 가져올 데이터를 제공하는 클래스를 만드는 인터페이스입니다. 다음은 이를 구조화하는 방법입니다.`CellsDataTable` 수업:

```csharp
class CellsDataTable : ICellsDataTable
{
    int m_index = -1;
    static String[] colsNames = new String[] { "Pet", "Fruit", "Country", "Color" };
    static String[] col0data = new String[] { "Dog", "Cat", "Duck" };
    static String[] col1data = new String[] { "Apple", "Pear", "Banana" };
    static String[] col2data = new String[] { "UK", "USA", "China" };
    static String[] col3data = new String[] { "Red", "Green", "Blue" };
    static String[][] colsData = new String[][] { col0data, col1data, col2data, col3data };
    
    // ... 다른 멤버를 구현합니다 ...
}
```

여기서는 열 이름과 각 열에 대한 데이터를 정의하여 가져온 테이블의 구조를 용이하게 해줍니다.

## 3단계: ICellsDataTable 인터페이스 멤버 구현

 내에서`CellsDataTable` 클래스의 멤버를 구현해야 합니다.`ICellsDataTable` 인터페이스. 필요한 구현은 다음과 같습니다.

```csharp
public object this[string columnName]
{
    get
    {
        throw new NotImplementedException();
    }
}

object ICellsDataTable.this[int columnIndex]
{
    get
    {
        return colsData[columnIndex][m_index];
    }
}

string[] ICellsDataTable.Columns
{
    get { return colsNames; }
}

int ICellsDataTable.Count
{
    get { return col0data.Length; }
}

void ICellsDataTable.BeforeFirst()
{
    m_index = -1;
}

bool ICellsDataTable.Next()
{
    m_index++;
    return (m_index < Count);
}
```

이 클래스의 일부는 데이터 검색, 행과 열의 수 정의, 현재 인덱스 상태 관리를 담당합니다.

## 4단계: Main 함수 작성

 이제 만들어 보겠습니다.`Run`전체 테이블 가져오기 프로세스를 조율하는 방법:

```csharp
public static void Run()
{
    string sourceDir = "Your Document Directory\\";
    string outputDir = "Your Document Directory\\";
    
    CellsDataTable cellsDataTable = new CellsDataTable();
    Workbook wb = new Workbook(sourceDir + "sampleImportTableOptionsShiftFirstRowDown.xlsx");
    Worksheet ws = wb.Worksheets[0];
```

## 5단계: 가져오기 옵션 설정

 가져오기 동작을 제어하려면 인스턴스를 생성해야 합니다.`ImportTableOptions` 그리고 그에 따라 속성을 설정합니다. 구체적으로, 우리는 다음과 같이 설정하고 싶습니다.`ShiftFirstRowDown` 에게`false`.

```csharp
    ImportTableOptions opts = new ImportTableOptions();
    opts.ShiftFirstRowDown = false; // 우리는 첫 번째 행을 아래로 이동하고 싶지 않습니다.
```

## 6단계: DataTable 가져오기

 이제 우리는 데이터를 가져올 수 있습니다`CellsDataTable` 워크시트에 넣으세요.

```csharp
    ws.Cells.ImportData(cellsDataTable, 2, 2, opts);
}
```

이 명령을 사용하면 지정된 행과 열에서 시작하여 데이터 표를 직접 삽입할 수 있습니다.

## 7단계: 통합 문서 저장

마지막으로 수정된 통합 문서를 파일로 저장합니다.

```csharp
    wb.Save(outputDir + "outputImportTableOptionsShiftFirstRowDown-False.xlsx");
}
```

## 결론

이제 다 봤습니다! Aspose.Cells for .NET을 사용하여 첫 번째 행을 이동하지 않고 DataTable 행을 Excel 시트에 삽입하는 방법을 알아보았습니다. 이 프로세스는 Excel 내에서 데이터 조작을 간소화할 뿐만 아니라 일반적으로 번거로운 작업을 자동화하여 애플리케이션의 성능을 향상시킵니다. 툴킷에 이러한 지식이 있으면 Excel 자동화 작업을 처리하는 데 더 잘 대비하여 시간과 노력을 절약할 수 있습니다.

## 자주 묻는 질문

### .NET용 Aspose.Cells란 무엇인가요?
.NET용 Aspose.Cells는 개발자가 .NET 애플리케이션에서 Excel 파일을 만들고, 조작하고, 변환할 수 있는 프로그래밍 라이브러리입니다.

### Aspose.Cells를 사용하려면 라이선스가 필요한가요?
네, 모든 기능을 사용하려면 유효한 라이선스가 필요합니다. 그러나 초기 테스트를 위해 무료 평가판을 사용할 수 있습니다.

### 웹 애플리케이션에서 Aspose.Cells를 사용할 수 있나요?
물론입니다! Aspose.Cells는 .NET으로 개발된 데스크톱, 웹 및 클라우드 기반 애플리케이션에 완벽합니다.

### Aspose.Cells로 어떤 유형의 Excel 파일을 만들 수 있나요?
XLSX, XLS, CSV 등 다양한 Excel 파일 형식을 만들 수 있습니다.

### Aspose.Cells에 대한 지원은 어디서 받을 수 있나요?
 질문을 하거나 도움을 찾을 수 있습니다.[Aspose 포럼](https://forum.aspose.com/c/cells/9).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
