---
title: 사용자 정의 DB 숫자 패턴 서식을 사용하여 Excel로 데이터 가져오기
linktitle: 사용자 정의 DB 숫자 패턴 서식을 사용하여 Excel로 데이터 가져오기
second_title: Aspose.Cells .NET Excel 처리 API
description: 이 쉬운 튜토리얼에서는 Aspose.Cells for .NET을 사용하여 사용자 지정 DB Num 서식을 적용하여 Excel로 데이터를 가져오는 방법을 알아봅니다.
weight: 10
url: /ko/net/excel-data-import-export/import-data-to-worksheet-in-excel-with-specified-db-num-custom-pattern-formatting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 사용자 정의 DB 숫자 패턴 서식을 사용하여 Excel로 데이터 가져오기

## 소개

스프레드시트 조작과 관련하여 Excel로 데이터를 가져오고 올바르게 서식을 지정하는 것은 엄청난 작업처럼 느껴질 수 있습니다. 특히 DB Num 패턴과 같은 특정 문화 기반 서식을 사용하려는 경우 더욱 그렇습니다. Excel 서식 지정의 기술적 세부 사항에 얽매인 적이 있다면 올바른 위치에 있습니다! 이 가이드에서는 Aspose.Cells for .NET을 사용하여 간단한 단계로 나누어 데이터 가져오기를 간단할 뿐만 아니라 미적으로도 즐겁게 만들어 보겠습니다. 그러니 잠깐만 기다려 주세요. .NET 프로그래밍, 서식 지정 및 Excel 파일 내보내기의 세계로 쉽게 뛰어들 것입니다!

## 필수 조건

핵심을 파고들기 전에, 필요한 모든 것을 갖추었는지 확인해 보겠습니다. 성공을 위한 전제 조건의 간단한 체크리스트는 다음과 같습니다.

1. .NET Framework: 컴퓨터에 .NET Framework가 설치되어 있는지 확인하세요. Aspose.Cells는 다양한 .NET 버전과 원활하게 작동합니다.
2.  .NET용 Aspose.Cells: Aspose.Cells 라이브러리를 다운로드하여 설치해야 합니다. 다음에서 가져올 수 있습니다.[다운로드 링크](https://releases.aspose.com/cells/net/).
3. 통합 개발 환경(IDE): Visual Studio와 같은 IDE를 사용하여 C# 코드를 작성하고 실행할 수 있습니다.
4. C#에 대한 기본 지식: C#에 대한 기본적인 이해가 있으면 이 가이드에서 사용하는 코딩 관행을 따라가는 데 도움이 됩니다.

모든 것을 다 얻었나요? 좋아요! 필요한 패키지를 가져오는 것으로 넘어가죠.

## 패키지 가져오기

Aspose.Cells를 효과적으로 사용하려면 C# 파일의 시작 부분에서 필요한 네임스페이스를 가져와야 합니다. 단계별로 나누어 보겠습니다.

### C# 파일 만들기

 IDE를 열고(Visual Studio 권장) 새 C# 프로젝트를 만듭니다. 다음과 같이 관련 있는 이름을 지정합니다.`ExcelDataImport`.

### 참조 Aspose.Cells

프로젝트에 Aspose.Cells 라이브러리를 포함해야 합니다. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 버튼으로 클릭하고 '참조 추가'를 선택합니다. Aspose.Cells를 설치한 위치로 이동하여 선택합니다.

### 필요한 네임스페이스 가져오기

C# 파일의 맨 위에 다음 네임스페이스를 가져옵니다.

```csharp
using System;
using System.IO;
using Aspose.Cells;
using System.Drawing;
```

이 간단한 한 줄을 통해 Aspose.Cells가 제공하는 모든 기능을 사용할 수 있습니다. 

이제 모든 전제 조건을 충족하고 필요한 패키지를 가져왔으니 Excel로 데이터를 가져오고 사용자 지정 DB Num 패턴 서식을 적용하는 단계별 프로세스를 살펴보겠습니다. 명확성과 이해를 보장하기 위해 체계적으로 진행하겠습니다.

## 1단계: 데이터 디렉토리 설정

첫째, 출력이 저장될 문서 디렉토리 경로를 지정해야 합니다. 파일 구조에 따라 조정하세요.

```csharp
string dataDir = "Your Document Directory";
```

 이 예에서 다음을 대체합니다.`Your Document Directory` 실제 경로와 같이`C:\\Users\\YourName\\Documents\\`.

## 2단계: 워크북 만들기

다음으로, 기본적으로 Excel 파일인 새 통합 문서를 만듭니다.

```csharp
Workbook wb = new Workbook();
```

 여기서 우리는 새로운 것을 인스턴스화하고 있습니다`Workbook` 객체입니다. 이것은 당신의 빈 캔버스입니다!

## 3단계: 첫 번째 워크시트에 액세스

각 워크북에는 여러 워크시트가 들어 있습니다. 데이터 입력을 시작하려면 첫 번째 워크시트에 액세스해야 합니다.

```csharp
Worksheet ws = wb.Worksheets[0];
```

책의 첫 페이지를 펼치는 것처럼, 데이터를 추가하려면 첫 번째 워크시트에 접근하는 것입니다.

## 4단계: 셀에 데이터 입력

 이제 셀에 데이터를 채워 봅시다. 이 예에서는 값을 입력합니다.`123` 셀 A1에.

```csharp
Cell cell = ws.Cells["A1"];
cell.PutValue(123);
```

여기서는 Excel에 직접 말하고 있습니다. 즉, 데이터를 바로 A1 셀에 입력하는 것입니다! 

## 5단계: 셀 스타일 액세스

모든 셀에는 스타일이 있으며, 셀의 모양을 사용자 지정할 수 있습니다. 사용자 지정 형식을 적용하려면 먼저 셀의 스타일에 액세스해야 합니다.

```csharp
Style st = cell.GetStyle();
```

세포의 스타일을 잡으면, 당신만의 독특한 터치를 추가할 준비가 되는 셈입니다!

## 6단계: DBNum 사용자 지정 패턴 서식 지정

마법이 일어나는 곳은 바로 여기입니다. DBNum 포맷팅 스타일을 사용하여 사용자 지정 포맷 패턴을 지정할 수 있습니다.

```csharp
st.Custom = "[DBNum2][$-804]General";
```

 이 줄은 Excel에 숫자를 서식 지정하도록 지시합니다.`123`중국어에 해당하는 DBNum 패턴에 따라. 꽤 깔끔하죠?

## 7단계: 업데이트된 셀 스타일 설정

이제 사용자 정의 스타일을 정의했으니, 셀에 적용할 차례입니다.

```csharp
cell.SetStyle(st);
```

이것은 마치 당신의 휴대폰을 세련된 새로운 옷으로 차려입히는 것과 같습니다!

## 8단계: 열 너비 조정

모든 것이 보기 좋고 깔끔해 보이도록 합시다. 첫 번째 열의 너비를 조정하여 데이터에 더 잘 맞출 수 있습니다.

```csharp
ws.Cells.SetColumnWidth(0, 30);
```

여기서는 열 너비를 확장하여 데이터가 좁아 보이지 않도록 합니다. 데이터에 숨 쉴 공간을 주는 것처럼 생각하세요!

## 9단계: 통합 문서 저장

마지막으로, 이 걸작을 PDF 포맷으로 저장해 보겠습니다. 이게 대단원입니다!

```csharp
wb.Save(dataDir + "outputDBNumCustomFormatting.pdf", SaveFormat.Pdf);
```

축하합니다! 방금 DB Num 스타일로 포맷된 숫자를 보여주는 PDF 파일을 만들었습니다.

## 결론

이제 다 되었습니다! Excel로 데이터를 성공적으로 가져오고, 사용자 지정 DB Num 서식을 적용하고, PDF 형식으로 저장했습니다. Aspose.Cells for .NET을 사용하면 이 프로세스가 더 쉬워질 뿐만 아니라 훨씬 더 유연하고 강력해집니다. 더 이상 Excel의 기본 제공 서식 옵션으로 어려움을 겪지 않아도 됩니다. 이제 코드를 통해 직접 제어할 수 있습니다!

데이터 보고서를 준비하든 재무 제표를 작성하든 Aspose.Cells의 힘을 활용하면 스프레드시트 게임을 완전히 새로운 수준으로 끌어올릴 수 있습니다. 그럼, 무엇을 기다리고 계신가요? 자신감을 가지고 프로젝트에 뛰어들어 데이터를 빛나게 하세요!

## 자주 묻는 질문

### Aspose.Cells란 무엇인가요?  
Aspose.Cells는 개발자가 Excel 파일을 프로그래밍 방식으로 만들고, 조작하고, 변환할 수 있는 강력한 .NET용 라이브러리입니다.

### 다른 유형의 셀을 서식 지정할 수 있나요?  
네! 워크시트 내의 모든 셀에 다양한 스타일, 형식, 심지어 수식까지 적용할 수 있습니다.

### 무료 체험판이 있나요?  
 물론입니다! 무료 체험판을 확인해 보세요[여기](https://releases.aspose.com/).

### Excel 파일은 어떤 형식으로 저장할 수 있나요?  
Aspose.Cells는 XLSX, XLS, CSV, PDF 등 다양한 형식을 지원합니다.

### 더 많은 지원은 어디에서 받을 수 있나요?  
 도움이 필요하면 방문하세요[지원 포럼](https://forum.aspose.com/c/cells/9) 지역사회와 전문가에게 도움을 요청하세요.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
