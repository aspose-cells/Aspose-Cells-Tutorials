---
category: general
date: 2026-06-21
description: Java에서 expand를 사용해 배열을 행으로 확장하고, Excel 수식 코드를 작성하며, Java 스타일로 Excel 파일을
  저장하는 방법을 한 번에 배워보세요—단일 튜토리얼에서 모두 다룹니다.
draft: false
keywords:
- how to use expand
- expand array to rows
- write excel formula code
- save excel file java
language: ko
og_description: Java에서 expand를 사용해 Excel 데이터를 조작하고, 배열을 행으로 확장하며, Excel 수식 코드를 작성하고,
  Java 방식으로 Excel 파일을 저장하는 방법.
og_title: Java에서 Expand 사용법 – 완전한 Excel 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-21'
  description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  headline: How to Use Expand in Java – Complete Excel Guide
  type: TechArticle
- description: Learn how to use expand in Java to expand array to rows, write Excel
    formula code, and save Excel file Java style—all in a single tutorial.
  name: How to Use Expand in Java – Complete Excel Guide
  steps:
  - name: Why This Works
    text: '- **`Workbook`**: Represents the entire Excel file. Creating a new one
      gives you a clean canvas; loading an existing file lets you augment a pre‑existing
      template. - **`Worksheet`**: Think of it as a single tab. We grab the first
      one because that’s where we’ll demonstrate the formula. - **`setFormul'
  - name: Real‑World Use Cases
    text: '| Scenario | How EXPAND Helps | |----------|------------------| | Generating
      a month‑long schedule from a short list of tasks | `=EXPAND(taskList,30)` |
      | Padding a matrix for a statistical model | `=EXPAND(matrix,10,10,0)` | | Creating
      placeholder rows for user input | `=EXPAND({""},20)` |'
  - name: Expected Output
    text: 'When you open `output.xlsx`:'
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
- Formulas
title: Java에서 Expand 사용 방법 – 완전한 Excel 가이드
url: /ko/java/spreadsheet-automation/how-to-use-expand-in-java-complete-excel-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 EXPAND 사용 방법 – 완전한 Excel 가이드

Excel을 Java로 자동화할 때 **EXPAND를 어떻게 사용하는지** 궁금했던 적 있나요? 당신만 그런 것이 아닙니다—개발자들은 끊임없이 배열을 행으로 확장하는 방법을 무한 루프 없이 묻습니다. 좋은 소식은 단일 수식으로 이를 할 수 있으며, 그 수식을 워크북에 삽입하는 Java 코드는 놀라울 정도로 짧습니다.

이 튜토리얼에서는 EXPAND를 정확히 어떻게 사용하는지, Java에서 Excel 수식 코드를 어떻게 작성하는지, 그리고 Java 방식으로 Excel 파일을 저장해 즉시 결과를 확인하는 방법을 실용적인 예제로 단계별로 안내합니다. 마지막까지 따라오면 기존 워크북을 로드하고, `EXPAND` 함수를 셀에 삽입한 뒤 파일을 디스크에 다시 쓰는 실행 가능한 프로그램을 얻게 됩니다.

## 필수 조건

시작하기 전에 다음이 설치되어 있는지 확인하세요:

- Java 17(또는 최신 JDK) 설치
- Maven 또는 Gradle을 사용하여 종속성 관리
- **Aspose.Cells for Java** 라이브러리 (Java에서 Excel을 조작하는 가장 쉬운 방법). Maven Central에서 가져올 수 있습니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- check for the latest -->
</dependency>
```

추가적인 Excel 설치는 필요하지 않습니다; 라이브러리가 파일 형식을 내부적으로 처리합니다. Gradle을 선호한다면 해당 의존성 블록을 교체하면 됩니다.

이제 기본 사항을 다졌으니, 실제로 손을 더럽혀 보겠습니다.

## Java에서 EXPAND 사용 방법

`EXPAND` 함수는 Excel 동적 배열 패밀리의 일부입니다. 소스 배열을 받아 지정된 크기로 확장하고, 기본값으로 빈 셀을 `#N/A` 로 채웁니다. 여기서는 간단한 1차원 배열 `{1,2,3}`을 제공하고 Excel에 **5행**으로 확장하도록 요청합니다.

```java
// Import statements
import com.aspose.cells.*;

public class ExpandDemo {
    public static void main(String[] args) {
        try {
            // 1️⃣ Load or create a workbook
            Workbook wb = new Workbook(); // creates a blank workbook
            // Optionally, load an existing file:
            // Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

            // 2️⃣ Get the first worksheet (index 0)
            Worksheet ws = wb.getWorksheets().get(0);

            // 3️⃣ Apply the EXPAND function in cell A1
            // This is where we **write excel formula code** from Java.
            ws.getCells().get("A1").setFormula("=EXPAND({1,2,3},5)");

            // 4️⃣ Save the workbook — **save excel file java** style.
            wb.save("YOUR_DIRECTORY/output.xlsx");
            System.out.println("Workbook saved successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

### 왜 이렇게 동작하는가

- **`Workbook`**: 전체 Excel 파일을 나타냅니다. 새 파일을 만들면 깨끗한 캔버스를 얻고, 기존 파일을 로드하면 미리 만든 템플릿을 확장할 수 있습니다.
- **`Worksheet`**: 하나의 탭이라고 생각하면 됩니다. 우리는 첫 번째 시트를 잡는데, 여기서 수식을 시연할 것이기 때문입니다.
- **`setFormula`**: 이 메서드는 유효한 Excel 수식을 문자열로 삽입합니다. 여기서는 `EXPAND` 함수를 넣어 Excel에 **배열을 행으로 확장**하도록 지시합니다(열도 필요하면 지정 가능).
- **`save`**: 변경 내용을 디스크에 영구 저장합니다. 이것이 **save excel file java** 단계이며, 저장 후 Excel이나 다른 뷰어에서 파일을 열 수 있게 합니다.

프로그램을 실행하고 `output.xlsx`를 열면 A열에 `1, 2, 3, #N/A, #N/A`가 채워진 것을 볼 수 있습니다. `EXPAND`의 두 번째 인수를 `3`으로 바꾸면 행이 세 개만 생성됩니다—동적 보고서에 딱 맞습니다.

## EXPAND 함수로 배열을 행으로 확장하기

수동으로 행을 반복해서 루프를 돌던 배경이 있다면, `EXPAND` 함수가 그 보일러플레이트를 대체할 수 있습니다. 구문을 간단히 정리하면 다음과 같습니다:

```
EXPAND(source, rows, columns, fill)
```

- **source** – 확장하려는 배열. 예시에서는 `{1,2,3}`.
- **rows** – 원하는 행 수. 여기서는 `5`를 사용했습니다.
- **columns** – 선택 사항; 기본값은 소스 배열의 열 수입니다.
- **fill** – 빈 셀에 넣을 값(`#N/A`가 기본).

### 실제 사용 사례

| 시나리오 | EXPAND가 도움이 되는 방법 |
|----------|--------------------------|
| 짧은 작업 목록으로 한 달 일정 생성 | `=EXPAND(taskList,30)` |
| 통계 모델을 위한 행렬 패딩 | `=EXPAND(matrix,10,10,0)` |
| 사용자 입력을 위한 자리표시자 행 만들기 | `=EXPAND({""},20)` |

Excel이 무거운 작업을 수행하도록 하면 Java 코드를 깔끔하게 유지하고 불필요한 루프를 피할 수 있습니다.

## Java에서 Excel 수식 코드를 작성하기

“수식 문자열을 동적으로 만들 수 있을까?” 라고 생각할 수 있습니다. 물론 가능합니다. 변수에 따라 `EXPAND` 호출을 구성하는 예시 코드는 다음과 같습니다:

```java
int[] numbers = {4, 5, 6};
int targetRows = 7;

// Convert int array to Excel‑style literal: {4,5,6}
StringBuilder sb = new StringBuilder("{");
for (int i = 0; i < numbers.length; i++) {
    sb.append(numbers[i]);
    if (i < numbers.length - 1) sb.append(",");
}
sb.append("}");

String formula = String.format("=EXPAND(%s,%d)", sb.toString(), targetRows);
ws.getCells().get("B2").setFormula(formula);
```

프로그램적으로 **write excel formula code**를 작성한 뒤 셀 `B2`에 삽입하는 방식을 확인하세요. 데이터베이스에서 데이터를 끌어와 동적 Excel 보고서를 만들 때처럼, 필요에 따라 수식을 즉석에서 생성할 때 확장성이 뛰어납니다.

## Java에서 Excel 파일 저장 – 변경 사항 영구 저장

워크북을 저장하는 것이 퍼즐의 마지막 조각입니다. Aspose.Cells는 몇 가지 옵션을 제공합니다:

- **`wb.save("path.xlsx")`** – 기본 XLSX 형식으로 저장.
- **`wb.save("path.xls", SaveFormat.EXCEL_97_TO_2003)`** – 레거시 호환성을 위해.
- **`wb.save(outputStream, SaveFormat.XLSX)`** – 파일을 스트리밍해야 할 때(예: 웹 애플리케이션).

다음은 `ByteArrayOutputStream`에 기록하여 REST 엔드포인트에서 바이트 배열을 반환할 수 있는 예시입니다:

```java
ByteArrayOutputStream baos = new ByteArrayOutputStream();
wb.save(baos, SaveFormat.XLSX);
byte[] excelBytes = baos.toByteArray();
// Now you can send `excelBytes` as a response payload.
```

이것이 많은 엔터프라이즈 서비스가 의존하는 **save excel file java** 패턴입니다.

## 일반적인 함정 및 전문가 팁

- **Formula Evaluation Timing** – Aspose.Cells는 `save` 시 자동으로 수식을 계산하지 **않습니다**. 계산된 값이 필요하면 저장 전에 `wb.calculateFormula()`를 호출하세요.
- **Dynamic Array Support** – `EXPAND` 함수는 Excel 365 / 2021 이상에서만 사용할 수 있습니다. 오래된 Excel 버전에서 파일을 열면 `#NAME?` 오류가 나타납니다. 레거시 클라이언트를 지원해야 한다면 수동 확장으로 대체를 고려하세요.
- **Locale Issues** – 워크북 로케일과 관계없이 영어 함수 이름(`EXPAND`)을 사용하세요; Aspose.Cells는 영어 구문을 따릅니다.
- **Large Arrays** – 수천 행으로 확장하면 파일 크기가 급증할 수 있습니다. 메모리 사용량을 주시하고 대용량 데이터셋은 스트리밍을 고려하세요.

## 전체 작업 예제

아래는 IDE에 복사·붙여넣기 할 수 있는 완전하고 독립적인 프로그램입니다. 모든 import, 오류 처리, 주석이 포함되어 있어 쉽게 따라 할 수 있습니다.

```java
import com.aspose.cells.*;

public class ExpandDemoFull {
    public static void main(String[] args) {
        // Adjust these paths as needed
        String inputPath = "YOUR_DIRECTORY/input.xlsx";
        String outputPath = "YOUR_DIRECTORY/output.xlsx";

        try {
            // Step 1: Load an existing workbook or create a new one
            Workbook wb;
            if (new java.io.File(inputPath).exists()) {
                wb = new Workbook(inputPath);
                System.out.println("Loaded existing workbook.");
            } else {
                wb = new Workbook(); // brand‑new workbook
                System.out.println("Created a new workbook.");
            }

            // Step 2: Access the first worksheet
            Worksheet ws = wb.getWorksheets().get(0);

            // Step 3: Build a dynamic EXPAND formula (expand array to rows)
            int[] sourceArray = {1, 2, 3};
            int rowsDesired = 5;

            // Convert Java array to Excel literal syntax
            StringBuilder literal = new StringBuilder("{");
            for (int i = 0; i < sourceArray.length; i++) {
                literal.append(sourceArray[i]);
                if (i < sourceArray.length - 1) literal.append(",");
            }
            literal.append("}");

            String formula = String.format("=EXPAND(%s,%d)", literal, rowsDesired);
            ws.getCells().get("A1").setFormula(formula);
            System.out.println("Inserted formula: " + formula);

            // Optional: force calculation so the file contains values, not just formulas
            wb.calculateFormula();

            // Step 4: Save the workbook – **save excel file java** style
            wb.save(outputPath);
            System.out.println("Workbook saved to " + outputPath);
        } catch (Exception ex) {
            System.err.println("Error occurred: " + ex.getMessage());
            ex.printStackTrace();
        }
    }
}
```

### 예상 출력

`output.xlsx`를 열면 다음과 같은 내용이 표시됩니다:

| A   |
|-----|
| 1   |
| 2   |
| 3   |
| #N/A |
| #N/A |

`rowsDesired`를 `3`으로 변경하면 세 번째 행까지만 표시됩니다. `#N/A` 자리표시자는 Excel이 “여기에 데이터가 없습니다”라고 알려주는 방식이며, `EXPAND`에 네 번째 인수를 전달해 예를 들어 `=EXPAND({1,` 와 같이 교체할 수 있습니다.

## 다음에 배울 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 리소스는 완전한 작업 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [Aspose.Cells for Java를 사용하여 Excel 워크북에 행 삽입하는 방법](/cells/english/java/worksheet-management/aspose-cells-java-insert-rows-excel-workbooks/)
- [Aspose.Cells for Java로 Excel에서 행 삭제하기 | 가이드 및 튜토리얼](/cells/english/java/worksheet-management/delete-row-excel-aspose-cells-java/)
- [Aspose.Cells Java를 사용하여 다양한 형식으로 Excel 파일 저장하기](/cells/english/java/workbook-operations/save-excel-files-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}