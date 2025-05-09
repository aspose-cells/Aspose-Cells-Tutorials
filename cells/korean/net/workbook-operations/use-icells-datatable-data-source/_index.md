---
"description": "Aspose.Cells for .NET과 함께 ICellsDataTableDataSource를 사용하여 Excel 시트를 동적으로 채우는 방법을 알아보세요. 통합 문서에서 고객 데이터를 자동화하는 데 적합합니다."
"linktitle": "Workbook Designer에 ICellsDataTableDataSource 사용"
"second_title": "Aspose.Cells .NET Excel 처리 API"
"title": "Workbook Designer에 ICellsDataTableDataSource 사용"
"url": "/ko/net/workbook-operations/use-icells-datatable-data-source/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Workbook Designer에 ICellsDataTableDataSource 사용

## 소개
자동화된 데이터 통합 기능을 갖춘 고급 스프레드시트를 만드는 것은 특히 비즈니스 애플리케이션에서 획기적인 변화를 가져올 수 있습니다. 이 튜토리얼에서는 `ICellsDataTableDataSource` Aspose.Cells for .NET 통합 문서 디자이너를 위한 가이드입니다. 사용자 지정 데이터를 Excel 파일에 동적으로 로드하는 간단하고 사람이 읽을 수 있는 솔루션을 구축하는 방법을 안내해 드립니다. 고객 목록, 판매 데이터 등을 다루는 분이라면 이 가이드가 도움이 될 것입니다!
## 필수 조건
시작하려면 다음 사항이 있는지 확인하세요.
- .NET 라이브러리용 Aspose.Cells – 여기에서 다운로드할 수 있습니다. [여기](https://releases.aspose.com/cells/net/) 또는 무료 체험판을 받아보세요.
- .NET 개발 환경 – Visual Studio는 좋은 선택입니다.
- C#에 대한 기본적인 이해 – 클래스와 데이터 처리에 대한 지식이 있으면 따라가는 데 도움이 됩니다.
계속 진행하기 전에 개발 환경에 필요한 패키지가 설정되어 있는지 확인하세요.
## 패키지 가져오기
Aspose.Cells를 효과적으로 사용하려면 필수 패키지를 가져와야 합니다. 필요한 네임스페이스에 대한 간략한 참조는 다음과 같습니다.
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## 1단계: 고객 데이터 클래스 정의
시작하려면 간단한 것을 만드세요 `Customer` 클래스. 이 클래스는 다음과 같은 기본 고객 정보를 보관합니다. `FullName` 그리고 `Address`이를 데이터의 "형태"를 정의하는 방법으로 생각해 보세요.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## 2단계: 고객 목록 클래스 설정
다음으로, 다음을 정의합니다. `CustomerList` 확장되는 클래스 `ArrayList`. 이 사용자 지정 목록에는 인스턴스가 포함됩니다. `Customer` 각 항목에 대한 인덱싱된 액세스를 허용합니다.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
이 단계에서는 Aspose.Cells가 인식하고 처리할 수 있는 형식으로 데이터를 래핑합니다.
## 3단계: 고객 데이터 소스 클래스 만들기
여기서 흥미로운 일이 시작됩니다. 우리는 `CustomerDataSource` 클래스 구현 `ICellsDataTable` Aspose.Cells의 워크북 디자이너와 호환되는 데이터를 만들려면
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
이 관습 `CustomerDataSource` 클래스를 사용하면 Aspose.Cells가 각각을 해석할 수 있습니다. `Customer` Excel 파일에 행으로 객체를 추가합니다.
## 4단계: 고객 데이터 초기화
이제 목록에 고객을 추가해 보겠습니다. 여기에서 통합 문서에 기록할 데이터를 불러옵니다. 필요에 따라 항목을 더 추가해도 됩니다.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
이 예시에서는 작은 데이터 세트를 사용하고 있습니다. 하지만 데이터베이스나 다른 소스에서 데이터를 로드하여 목록을 쉽게 확장할 수 있습니다.
## 5단계: 통합 문서 로드
이제 필요한 스마트 마커가 포함된 기존 Excel 통합 문서를 열어 보겠습니다. 이 통합 문서를 템플릿으로 사용하고, Aspose.Cells가 스마트 마커를 고객 데이터로 동적으로 대체합니다.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
확인하십시오 `"SmartMarker1.xlsx"` 다음과 같은 플레이스홀더가 포함되어 있습니다. `&=Customer.FullName` 그리고 `&=Customer.Address` 데이터를 입력해야 하는 위치입니다.
## 6단계: 통합 문서 디자이너 설정
이제 통합 문서 디자이너를 구성하여 고객 데이터 소스를 통합 문서의 스마트 마커와 연결해 보겠습니다.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
그만큼 `SetDataSource` 방법은 우리의 것을 바인딩합니다 `CustomerDataSource` 통합 문서의 스마트 마커에. 각 마커에는 레이블이 지정되어 있습니다. `&=Customer` 이제 Excel의 데이터가 해당 고객 데이터로 대체됩니다.
## 7단계: 통합 문서 처리 및 저장
마지막으로 통합 문서를 처리하여 데이터를 채우고 결과를 저장해 보겠습니다.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
이 코드는 스마트 마커 처리를 트리거하고 모든 플레이스홀더를 데이터로 대체하고 결과를 다음과 같이 저장합니다. `dest.xlsx`.
## 결론
축하합니다! 성공적으로 구현되었습니다. `ICellsDataTableDataSource` Aspose.Cells for .NET을 사용하는 통합 문서 디자이너를 위한 자료입니다. 이 방식은 스프레드시트의 데이터 입력을 자동화하는 데 적합하며, 특히 고객 목록이나 제품 재고와 같은 동적 데이터를 처리할 때 유용합니다. 이러한 기술을 활용하면 Excel 기반 보고서를 손쉽게 작성할 수 있는 데이터 기반 애플리케이션을 구축하는 데 큰 도움이 될 것입니다!
## 자주 묻는 질문
### 무엇인가요 `ICellsDataTable` Aspose.Cells에 있나요?  
Aspose.Cells 스마트 마커와 사용자 정의 데이터 소스를 연결하여 동적으로 데이터를 채울 수 있는 인터페이스입니다.
### 통합 문서 템플릿에서 데이터를 사용자 지정하려면 어떻게 해야 하나요?  
스마트 마커라고 불리는 플레이스홀더, 예: `&=Customer.FullName`, 사용됩니다. 이러한 마커는 처리 과정에서 실제 데이터로 대체됩니다.
### Aspose.Cells for .NET은 무료인가요?  
Aspose.Cells는 무료 체험판을 제공하지만, 전체 기능을 이용하려면 유료 라이선스가 필요합니다. [무료 체험](https://releases.aspose.com/) 또는 [구입하다](https://purchase.aspose.com/buy) 옵션.
### 더 많은 고객 데이터를 동적으로 추가할 수 있나요?  
물론입니다! 간단히 입력하세요 `CustomerList` 프로그램을 실행하기 전에 추가 항목을 입력하세요.
### 막혔을 때 어디에서 도움을 받을 수 있나요?  
Aspose에는 [지원 포럼](https://forum.aspose.com/c/cells/9) 사용자가 커뮤니티와 Aspose 팀으로부터 질문을 하고 도움을 받을 수 있는 곳입니다.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}