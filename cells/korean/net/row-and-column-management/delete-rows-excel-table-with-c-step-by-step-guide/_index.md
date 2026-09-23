---
category: general
date: 2026-02-28
description: C#에서 엑셀 테이블 행을 빠르게 삭제합니다. 이름이 지정된 범위를 추가하는 방법, 이름으로 워크시트에 접근하는 방법, 그리고
  중복 이름 오류를 방지하는 방법을 배워보세요.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: ko
og_description: C#를 사용하여 Excel 테이블의 행을 삭제합니다. 이 튜토리얼에서는 이름이 지정된 범위를 추가하고 이름으로 워크시트에
  접근하는 방법도 보여줍니다.
og_title: C#로 Excel 테이블 행 삭제 – 완전 가이드
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: C#로 Excel 테이블 행 삭제 – 단계별 가이드
url: /ko/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#로 Excel 테이블 행 삭제 – 완전 프로그래밍 튜토리얼

워크북에서 **delete rows excel table**을 해야 하는데 어떤 API 호출을 사용해야 할지 몰라 고민한 적 있나요? 여러분만 그런 것이 아닙니다—대부분의 개발자는 처음으로 프로그래밍으로 테이블을 정리하려 할 때 같은 벽에 부딪힙니다.  

이 가이드에서는 Excel 테이블에서 행을 제거할 뿐만 아니라 **add defined name**(즉 *named range*)을 추가하는 방법, **access worksheet by name**을 수행하는 방법, 그리고 다른 시트에 중복된 이름을 추가하면 `InvalidOperationException`이 발생하는 이유까지 전체 실행 가능한 예제로 단계별로 살펴보겠습니다.  

이 글을 다 읽고 나면 다음을 할 수 있게 됩니다:

* 탭 이름으로 워크시트를 가져오기.  
* 해당 시트의 첫 번째 테이블에서 데이터 행을 안전하게 삭제하기.  
* 특정 주소를 가리키는 이름 범위를 만들기.  
* 시트 간 중복 이름이 초래하는 함정을 이해하기.

외부 문서는 필요 없습니다—여기에 모든 것이 준비되어 있습니다.

---

## 준비물

* **DevExpress Spreadsheet**(또는 `Workbook`, `Worksheet`, `ListObject`, `Names` 객체를 제공하는 라이브러리).  
* **.NET 6** 이상을 타깃으로 하는 .NET 프로젝트(코드는 .NET Framework 4.8에서도 컴파일됩니다).  
* C#에 대한 기본 지식—`foreach` 루프만 작성할 수 있으면 충분합니다.

> **Pro tip:** DevExpress 무료 Community Edition을 사용하더라도 아래 API는 상용 버전과 동일합니다.

---

## Step 1 – Access Worksheet by Name

먼저 수정하려는 테이블이 들어 있는 시트를 찾아야 합니다.  
대부분의 개발자는 습관적으로 `Worksheets[0]`을 사용하지만, 이렇게 하면 시트 순서에 코드가 묶여 버리고 탭 이름이 바뀌면 바로 깨집니다.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*왜 중요한가:* 시트 **이름**을 사용하면 워크북 구조가 바뀌어도 잘못된 시트를 편집할 위험을 피할 수 있습니다.  

제공한 이름이 존재하지 않으면 라이브러리는 `KeyNotFoundException`을 발생시키며, 이를 잡아 친절한 오류 메시지를 표시할 수 있습니다.

---

## Step 2 – Delete Rows Excel Table (The Safe Way)

올바른 워크시트를 확보했으니, 이제 첫 번째 테이블의 데이터 행을 삭제해 보겠습니다.  
흔히 하는 실수는 `DeleteRows(1, rowCount‑1)`을 호출하는 것입니다. **DevExpress 22.2**부터 이 오버로드는 **사용 금지**이며 `InvalidOperationException`을 발생시킵니다. 라이브러리는 헤더 행이 아닌 **테이블 데이터 영역** 내에서만 행을 삭제하도록 요구합니다.

```csharp
// Grab the first table (ListObject) on the sheet
var table = worksheet.ListObjects[0];

// Calculate how many data rows we actually have (excluding the header)
int dataRowCount = table.DataRange.RowCount;

// Delete only the data rows – keep the header intact
if (dataRowCount > 0)
{
    // DeleteRows(startRow, rowCount) – startRow is zero‑based within the table
    table.DeleteRows(0, dataRowCount);
}
```

> **테이블이 비어 있으면 어떻게 될까?** `if` 가드가 `rowCount = 0`인 경우 호출을 방지하므로 예외가 발생하지 않습니다.

### Visual Overview  

![delete rows excel table example](image.png "Excel 테이블에서 행이 제거되는 스크린샷")  

*Alt text: C# 코드에서 delete rows excel table 예시*

---

## Step 3 – How to Add Defined Name (Create a Named Range)

테이블을 정리한 뒤에 차트나 데이터 검증 목록 등에서 나중에 특정 범위를 참조하고 싶을 수 있습니다. 바로 **add named range excel**이 필요한 상황입니다.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

`Names.Add` 메서드는 두 개의 매개변수를 받습니다: 식별자와 A1‑스타일 주소.  
앞서 **access worksheet by name**을 사용했기 때문에 주소 문자열이 시트 인덱스 변화에 구애받지 않고 안전하게 어느 시트든 가리킬 수 있습니다.

---

## Step 4 – Named Range on Another Sheet – Avoid Duplicate Name Errors

다른 시트에서도 같은 식별자를 재사용할 수 있을 것이라고 생각할 수 있습니다. 예:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

하지만 Excel의 이름 범위 범위는 **워크북 전체**에 적용되며 시트별이 아닙니다. 위 코드는 *“A name with the same identifier already exists.”* 라는 메시지와 함께 `InvalidOperationException`을 발생시킵니다.  

### 해결 방법

1. **고유한 이름**을 선택합니다(`MyTable_Sheet2`).  
2. **기존 이름을 삭제**한 뒤 다시 추가합니다(교체가 필요할 때만).

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Full, Runnable Example

모든 내용을 하나로 합치면, 아래와 같은 독립 실행형 콘솔 앱이 됩니다. Visual Studio에 붙여넣고 `sample.xlsx` 파일을 대상으로 실행해 보세요.

```csharp
using System;
using DevExpress.Spreadsheet;

class Program
{
    static void Main()
    {
        // Load an existing workbook (replace with your file path)
        Workbook workbook = new Workbook();
        workbook.LoadDocument("sample.xlsx");

        // -------------------------------------------------
        // Step 1 – Access the worksheet by its tab name
        // -------------------------------------------------
        Worksheet worksheet = workbook.Worksheets["Sheet1"]; // primary sheet

        // -------------------------------------------------
        // Step 2 – Delete rows excel table (safe method)
        // -------------------------------------------------
        var table = worksheet.ListObjects[0];
        int dataRows = table.DataRange.RowCount;
        if (dataRows > 0)
            table.DeleteRows(0, dataRows); // removes only data rows

        // -------------------------------------------------
        // Step 3 – Add a defined name (named range) on Sheet1
        // -------------------------------------------------
        workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

        // -------------------------------------------------
        // Step 4 – Demonstrate duplicate‑name handling
        // -------------------------------------------------
        try
        {
            workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
        }
        catch (InvalidOperationException ex)
        {
            Console.WriteLine("Duplicate name error: " + ex.Message);
            // Use a unique identifier instead
            workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");
        }

        // Save the modified workbook
        workbook.SaveDocument("sample_modified.xlsx");
        Console.WriteLine("Workbook updated successfully.");
    }
}
```

**예상 결과**

* **Sheet1**의 첫 번째 테이블에서 모든 데이터 행이 사라지고 헤더 행만 남습니다.  
* 이름 **MyTable**은 이제 `Sheet1!$A$1:$C$5`를 가리킵니다.  
* 두 번째 이름 **MyTable_Sheet2**는 **Sheet2**의 범위를 안전하게 참조하며 예외가 발생하지 않습니다.

---

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *워크북에 테이블이 여러 개 있으면 어떻게 하나요?* | 인덱스(`worksheet.ListObjects[1]`) 또는 이름(`worksheet.ListObjects["MyTable"]`)으로 올바른 `ListObject`를 가져옵니다. |
| *여러 워크시트에 걸친 테이블에서 행을 삭제할 수 있나요?* | 아니요—테이블은 단일 시트에만 존재합니다. 각 시트마다 삭제 로직을 반복해야 합니다. |
| *행의 일부만 삭제하고 싶다면?* | `table.DeleteRows(startRow, count)`를 사용하면 됩니다. 여기서 `startRow`는 테이블 데이터 영역 내에서 0부터 시작합니다. |
| *저장 후에도 이름 범위가 유지되나요?* | 네. `SaveDocument`를 호출하면 이름이 워크북 XML에 포함됩니다. |
| *워크북에 정의된 모든 이름을 나열하려면?* | `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`와 같이 순회하면 됩니다. |

---

## Conclusion

C#으로 **delete rows excel table**을 수행하고, **add named range excel**을 구현하며, **access worksheet by name**을 올바르게 사용하고 중복 이름 예외를 피하는 방법을 모두 살펴보았습니다.  

위 코드 스니펫이 완전한 솔루션이니 복사·붙여넣기만 하면 바로 자신의 파일에 적용할 수 있습니다. 여기서 로직을 확장해 여러 테이블을 다루거나 동적 범위 계산을 추가하거나 UI와 연동하는 등 다양한 활용이 가능합니다.

**다음 단계**로 고려해 볼 내용:

* **named range on another sheet**를 활용해 차트 시리즈를 구동하기.  
* 삭제 로직을 **ExcelDataReader**와 결합해 데이터를 가져온 뒤 정리하기.  
* `foreach (var file in Directory.GetFiles(...))` 루프를 사용해 수십 개의 워크북을 일괄 업데이트 자동화하기.

C#에서 Excel 자동화에 대해 더 궁금한 점이 있나요? 댓글로 알려 주세요. 계속해서 이야기를 나눠요. 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}