---
"description": "Aspose.Cells에서 스마트 마커와 함께 익명 형식을 사용하여 .NET에서 동적인 Excel 보고서를 생성하는 방법을 알아보세요. 간단한 가이드를 따라 해 보세요."
"linktitle": "스마트 마커 Aspose.Cells를 사용하여 익명 유형 사용"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "스마트 마커 Aspose.Cells를 사용하여 익명 유형 사용"
"url": "/ko/net/smart-markers-dynamic-data/use-anonymous-types-smart-markers/"
"weight": 17
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# 스마트 마커 Aspose.Cells를 사용하여 익명 유형 사용

## 소개
.NET 애플리케이션에서 동적 Excel 보고서를 생성할 때 Aspose.Cells는 강력한 도구로 돋보입니다. 가장 큰 장점 중 하나는 스마트 마커와 익명 형식을 사용할 수 있다는 것입니다. 이 개념을 처음 접하더라도 걱정하지 마세요! 이 가이드에서는 필수 조건부터 실습 예제까지 필요한 모든 내용을 자세하고 흥미롭고 따라 하기 쉬운 방식으로 제공합니다.
## 필수 조건
코드를 살펴보기 전에, 이 튜토리얼의 예제를 원활하게 실행하는 데 필요한 모든 것이 있는지 확인해 보겠습니다.
### 1. .NET 환경
로컬 컴퓨터에 제대로 작동하는 .NET 환경이 설치되어 있는지 확인하세요. Visual Studio나 원하는 다른 IDE를 사용할 수 있습니다.
### 2. Aspose.Cells 라이브러리
Aspose.Cells 라이브러리가 필요합니다. 아직 다운로드하지 않으셨다면 쉽게 찾으실 수 있습니다. [여기](https://releases.aspose.com/cells/net/). 또한 무료 체험판을 통해 직접 체험해 볼 수도 있습니다. [이 링크](https://releases.aspose.com/).
### 3. C# 기본 지식
C# 프로그래밍에 대한 기본적인 이해가 있으면 튜토리얼을 더 쉽게 따라갈 수 있습니다. 클래스, 객체, 속성과 같은 용어에 익숙하다면 문제없습니다!
## 패키지 가져오기
프로젝트에서 Aspose.Cells 라이브러리를 사용하려면 관련 네임스페이스를 가져와야 합니다. C# 파일 맨 위에 다음 using 지시문을 추가하세요.
```csharp
using System.IO;
using Aspose.Cells;
using System.Collections.Generic;
```
이러한 네임스페이스를 사용하면 나중에 설명할 모든 필수 클래스와 메서드에 액세스할 수 있습니다.
이제 튜토리얼의 핵심을 살펴보겠습니다! 사용자 지정 클래스를 사용하여 스마트 마커가 포함된 Excel 파일을 만드는 방법을 알아보겠습니다. 걱정하지 마세요. 모든 과정을 단계별로 쉽게 설명해 드리겠습니다!
## 1단계: 사용자 정의 클래스 만들기
먼저, Excel 파일에 추가할 데이터를 나타내는 간단한 클래스가 필요합니다. 이 클래스는 개인 정보를 담을 것입니다.
```csharp
public class Person
{
    private string m_Name;
    private int m_Age;
    public string Name
    {
        get { return m_Name; }
        set { m_Name = value; }
    }
    public int Age
    {
        get { return m_Age; }
        set { m_Age = value; }
    }
    internal Person(string name, int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
}
```
여기서 우리는 다음과 같은 클래스를 정의합니다. `Person` 두 개의 속성이 있는, `Name` 그리고 `Age`생성자는 이러한 속성을 초기화합니다. 
## 2단계: 통합 문서 디자이너 설정
다음으로 인스턴스를 생성해 보겠습니다. `WorkbookDesigner` 이 클래스를 사용하면 스마트 마커로 Excel 파일을 디자인할 수 있습니다.
```csharp
// 문서 디렉토리의 경로입니다.
string dataDir = "Your Document Directory";
// 통합 문서 디자이너 개체를 인스턴스화합니다.
WorkbookDesigner report = new WorkbookDesigner();
```
바꾸다 `"Your Document Directory"` Excel 파일을 저장할 실제 파일 경로를 입력합니다. `WorkbookDesigner` 클래스는 템플릿을 정의하는 이 작업의 핵심입니다.
## 3단계: 셀에 마커 추가
이제 워크시트에 스마트 마커를 추가해야 합니다. 이 마커는 나중에 입력할 데이터의 자리 표시자 역할을 합니다.
```csharp
// 워크북의 첫 번째 워크시트를 가져옵니다.
Aspose.Cells.Worksheet sheet = report.Workbook.Worksheets[0];
// 셀에 일부 마커를 입력합니다.
sheet.Cells["A1"].PutValue("Name");
sheet.Cells["B1"].PutValue("Age");
sheet.Cells["A2"].PutValue("&=MyProduct.Name");
sheet.Cells["B2"].PutValue("&=MyProduct.Age");
```
첫 번째 워크시트를 지정하고 헤더 셀에 대한 값을 설정합니다. 스마트 마커에는 접두사가 붙습니다. `&=` 이는 나중에 삽입할 데이터를 위한 플레이스홀더임을 Aspose에 알려줍니다.
## 4단계: 사람 목록 만들기
이제 우리의 것을 사용하는 사람들의 목록을 만들어 보겠습니다. `Person` 스마트 마커를 채우는 데 사용할 클래스입니다.
```csharp
// 사용자 정의 클래스를 기반으로 목록 컬렉션을 인스턴스화합니다.
IList<Person> list = new List<Person>();
// 사용자 정의 클래스 객체를 사용하여 마커에 대한 값을 제공합니다.
list.Add(new Person("Simon", 30));
list.Add(new Person("Johnson", 33));
```
우리는 목록을 만들고 인스턴스를 추가합니다. `Person` 이 목록은 Excel 템플릿을 채울 때 데이터 소스로 사용됩니다.
## 5단계: 데이터 소스 및 프로세스 마커 설정
목록을 준비한 후에는 이를 데이터 소스로 설정해야 합니다. `WorkbookDesigner` 인스턴스를 생성한 다음 마커를 처리합니다.
```csharp
// 데이터 소스를 설정합니다.
report.SetDataSource("MyProduct", list);
// 마커를 처리합니다.
report.Process(false);
```
그만큼 `SetDataSource` 메서드는 이전에 정의한 목록을 마커에 연결합니다. `Process` 이 방법은 통합 문서의 스마트 마커를 개체의 실제 값으로 바꿉니다.
## 6단계: Excel 파일 저장
마지막으로, 수정된 통합 문서를 지정된 디렉토리에 저장합니다.
```csharp
// 엑셀 파일을 저장합니다.
report.Workbook.Save(dataDir + "Smart Marker Customobjects.xls");
```
이 줄은 통합 문서를 지정된 파일 경로에 저장합니다. Excel에서 이 파일을 열어 삽입된 데이터를 확인할 수 있습니다.
## 결론
자, 이제 완성했습니다! Aspose.Cells의 스마트 마커와 사용자 지정 클래스를 사용하여 Excel 파일을 성공적으로 만들었습니다. 이 방법은 데이터 관리를 더욱 역동적으로 만들 뿐만 아니라 코드를 깔끔하고 체계적으로 유지하는 데에도 도움이 됩니다.
따라서 분석, 정보 추적 또는 기타 데이터 관련 작업을 위한 보고서를 생성하는 경우 스마트 마커를 사용하면 Excel 보고서를 보다 관리하기 쉽고 유연하게 만들 수 있습니다!
## 자주 묻는 질문
### Aspose.Cells의 스마트 마커는 무엇인가요?
스마트 마커는 런타임 중에 동적으로 데이터를 삽입할 수 있는 Excel 문서의 특수한 자리 표시자입니다.
### 스마트 마커에 익명 유형을 사용할 수 있나요?
네! 스마트 마커는 예상되는 데이터 구조와 일치하는 한 익명 유형을 포함한 모든 객체 유형에 사용할 수 있습니다.
### Aspose.Cells는 무료로 사용할 수 있나요?
Aspose.Cells는 유료 제품이지만, 무료 체험판을 통해 기능을 체험해 볼 수 있습니다.
### Aspose.Cells는 어떤 파일 형식을 지원하나요?
XLS, XLSX, CSV 등 다양한 파일 형식을 지원합니다.
### Aspose.Cells에 대한 자세한 정보는 어디에서 찾을 수 있나요?
자세한 내용은 다음을 확인하세요. [선적 서류 비치](https://reference.aspose.com/cells/net/) 또는 방문하세요 [지원 포럼](https://forum.aspose.com/c/cells/9).


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}