---
date: '2025-12-27'
description: Aspose.Cells for Java를 사용하여 Excel 데이터 소스를 프로그래밍 방식으로 변경하고, Excel 데이터
  연결을 수정하며, 워크플로를 자동화하는 방법을 배워보세요.
keywords:
- Excel data connections
- Aspose.Cells Java
- modify Excel data connections programmatically
title: Aspose.Cells for Java를 사용하여 Excel 데이터 소스를 변경하는 방법
url: /ko/java/advanced-features/master-excel-data-connections-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.Cells for Java를 사용하여 Excel 데이터 소스 변경하기

## 소개
프로그래밍 방식으로 **Excel 데이터 소스 변경** 및 Excel 파일 내 데이터 연결을 수정하는 데 어려움을 겪고 계신가요? 이 포괄적인 가이드는 강력한 **Aspose.Cells for Java** 라이브러리를 사용하여 보고 파이프라인을 자동화하려는 개발자를 위해 제작되었습니다. Excel 워크북을 로드하고, 외부 연결을 업데이트하며, 변경 사항을 저장하는 과정을 Java 코드로 안내해 드립니다.

### 배울게 될 내용
- Maven 또는 Gradle에서 Aspose.Cells for Java를 설정하는 방법.  
- **Load Excel workbook Java** – 기존 파일을 메모리로 읽어들이기.  
- **Modify Excel data connections** – 연결 이름, ODC 경로 및 SQL 명령을 업데이트하기.  
- **Save Excel workbook Java** – 업데이트된 워크북을 디스크에 저장하기.  

시작하기 전에 필요한 모든 준비가 갖춰졌는지 확인해 보겠습니다.

## 빠른 답변
- **주요 라이브러리는 무엇인가요?** Aspose.Cells for Java.  
- **워크북을 로드하는 메서드는?** `new Workbook(filePath)`.  
- **연결 문자열을 어떻게 업데이트하나요?** `DBConnection.setConnectionInfo(...)` 사용.  
- **ODC 파일 경로를 변경할 수 있나요?** 예, `ExternalConnection.setOdcFile(...)` 로 가능합니다.  
- **프로덕션에 라이선스가 필요합니까?** 상업용 라이선스를 사용하면 평가 제한이 해제됩니다.

## 전제 조건
시작하기 전에 다음 항목이 준비되어 있는지 확인하십시오:

### 필수 라이브러리
Aspose.Cells for Java 버전 25.3 이상은 이 튜토리얼에서 사용되는 API를 제공합니다.

### 환경 설정
- Java Development Kit (JDK) 설치  
- IntelliJ IDEA, Eclipse, NetBeans 등 IDE

### 지식 전제 조건
Java, Maven 또는 Gradle, 그리고 기본 SQL 개념에 익숙하면 원활히 따라올 수 있습니다.

## Aspose.Cells for Java 설정
Aspose.Cells 사용을 시작하려면 라이브러리를 프로젝트에 추가하십시오:

**Maven 설정**  
`pom.xml`에 다음 의존성을 추가하십시오:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle 설정**  
`build.gradle`에 다음 라인을 삽입하십시오:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### 라이선스 획득 단계
Aspose.Cells는 라이선스를 구매하기 전에 라이브러리를 평가할 수 있도록 무료 체험을 제공합니다:

- 무료 체험 페이지([free trial page](https://releases.aspose.com/cells/java/))를 방문하여 평가 패키지를 다운로드하십시오.  
- 전체 기능을 사용하려면 [구매 포털](https://purchase.aspose.com/buy)에서 라이선스를 구매하십시오.  
- 임시 접근이 필요하신가요? [임시 라이선스](https://purchase.aspose.com/temporary-license/)를 요청하십시오.

라이브러리를 참조하고 라이선스를 적용하면 코딩을 시작할 준비가 됩니다.

## 구현 가이드

### 기능 1: 파일에서 워크북 로드
**이 단계는 무엇을 하나요?** **load Excel workbook Java** 를 시연하여 데이터 연결을 작업할 수 있게 합니다.

#### 단계별 지침
**데이터 디렉터리 정의** – 프로그램에 소스 파일이 위치한 경로를 알려줍니다:

```java
String dataDir = "YOUR_DATA_DIRECTORY";
```
`DataConnection.xlsx` 파일이 해당 폴더에 존재하는지 확인하십시오.

**워크북 로드** – `Workbook` 객체를 인스턴스화합니다:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook(dataDir + "DataConnection.xlsx");
```
`Workbook` 인스턴스는 이제 메모리 내에서 Excel 파일을 나타냅니다.

### 기능 2: 워크북의 데이터 연결 수정
**왜 수정하나요?** 외부 연결을 업데이트하면 파일을 수동으로 열지 않고도 **Excel 데이터 소스 변경**이 가능합니다.

#### 단계별 지침
**데이터 연결 접근** – 첫 번째 연결을 가져옵니다(다중 연결이 필요하면 루프를 사용할 수 있습니다):

```java
import com.aspose.cells.DBConnection;
import com.aspose.cells.ExternalConnection;
import com.aspose.cells.OLEDBCommandType;

ExternalConnection conn = workbook.getDataConnections().get(0);
```
`getDataConnections()`는 모든 연결의 컬렉션을 반환하며, 이를 통해 **excel data connections**를 개별적으로 수정할 수 있습니다.

**연결 속성 수정** – 이름, ODC 파일, 명령 유형 및 SQL 문을 변경합니다:

```java
conn.setName("MyConnectionName");
conn.setOdcFile(dataDir + "MyDefaulConnection.odc");
```

데이터베이스 전용 설정을 위해 `DBConnection`으로 캐스팅합니다:

```java
DBConnection dbConn = (DBConnection) conn;
dbConn.setCommandType(OLEDBCommandType.SQL_STATEMENT);
dbConn.setCommand("SELECT * FROM AdminTable");

String connectionString = "Server=myServerAddress;Database=myDataBase;User ID=myUsername;Password=myPassword;Trusted_Connection=False";
dbConn.setConnectionInfo(connectionString);
```
여기서 SQL 쿼리와 연결 문자열과 같은 **excel external connection** 세부 정보를 업데이트합니다.

### 기능 3: 워크북을 파일에 저장
**다음은 무엇인가요?** 연결을 업데이트한 후, 변경 사항을 유지하려면 **save Excel workbook Java**가 필요합니다.

#### 단계별 지침
**출력 디렉터리 정의** – 수정된 파일이 기록될 위치:

```java
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

**워크북 저장** – 워크북을 디스크에 다시 씁니다:

```java
workbook.save(outDir + "MESQLDataConnection_out.xlsx");
```
`save()` 메서드는 **change excel data source** 작업을 최종 완료합니다.

## 실제 적용 사례
프로그램matically Excel 데이터 연결을 수정하면 다양한 가능성이 열립니다:

1. **자동 보고** – 데이터베이스에서 최신 데이터를 항상 가져오는 보고서를 생성합니다.  
2. **데이터 동기화** – 수동 새로 고침 없이 워크북을 실시간 시스템과 동기화합니다.  
3. **동적 대시보드** – 실시간 메트릭을 반영하는 대시보드를 구축합니다.

Aspose.Cells를 CRM, ERP 또는 BI 플랫폼과 통합하면 수동 작업을 크게 줄일 수 있습니다.

## 성능 고려 사항
대용량 워크북이나 방대한 결과 집합을 다룰 때:

- 메모리 급증을 방지하기 위해 데이터를 배치 처리하십시오.  
- 속도를 위해 SQL 쿼리를 최적화하십시오.  
- 리소스를 즉시 해제하십시오; 객체가 더 이상 필요 없으면 `workbook.dispose()`를 호출하십시오.

이러한 관행은 **changing Excel data source** 동안 애플리케이션이 응답성을 유지하도록 보장합니다.

## 결론
이제 **change Excel data source**를 위해 워크북을 로드하고, **modify excel data connections**를 수행한 뒤, **Aspose.Cells for Java**를 사용해 업데이트된 파일을 저장하는 방법을 배웠습니다. 이 기능을 통해 데이터 기반 워크플로를 자동화하고 Excel 파일을 외부 시스템과 동기화할 수 있습니다.

### 다음 단계
- `workbook.getDataConnections()`를 루프하여 다중 연결을 실험해 보세요.  
- 차트 생성, 셀 스타일링, 피벗 테이블 조작 등 다른 Aspose.Cells 기능을 탐색하십시오.

자동화를 강화할 준비가 되셨나요? 오늘 바로 이 코드를 구현하고 생산성 향상을 확인해 보세요!

## 자주 묻는 질문

**Q1: 워크북에서 다중 데이터 연결을 어떻게 처리하나요?**  
A1: 루프 내부에서 `workbook.getDataConnections().get(index)`를 사용하여 각 연결에 개별적으로 접근하십시오.

**Q2: Aspose.Cells Java를 사용해 Excel 파일의 다른 속성을 수정할 수 있나요?**  
A2: 물론입니다! Aspose.Cells는 셀 서식, 워크시트 관리, 차트 생성 등 다양한 기능을 지원합니다.

**Q3: SQL 명령이 실행되지 않으면 어떻게 해야 하나요?**  
A3: 연결 문자열을 확인하고, 데이터베이스 권한을 점검하며, 예외 세부 정보를 검토하여 원인을 파악하십시오.

**Q4: Aspose.Cells 문제에 대한 지원은 어디서 받을 수 있나요?**  
A4: [Aspose 포럼](https://forum.aspose.com/c/cells/9)에서 질문을 하거나 기존 솔루션을 찾아보세요.

**Q5: 무료 체험 버전에 제한이 있나요?**  
A5: 평가 버전은 워터마크가 추가되고 처리 용량에 제한이 있을 수 있습니다. 무제한 사용을 위해 라이선스를 구매하십시오.

## 리소스
- **문서:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **다운로드:** [Aspose.Cells for Java Releases](https://releases.aspose.com/cells/java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**마지막 업데이트:** 2025-12-27  
**테스트 환경:** Aspose.Cells Java 25.3  
**작성자:** Aspose