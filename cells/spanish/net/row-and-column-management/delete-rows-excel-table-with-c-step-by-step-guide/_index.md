---
category: general
date: 2026-02-28
description: Eliminar filas de una tabla de Excel en C# rápidamente. Aprende cómo
  agregar un rango con nombre en Excel, acceder a la hoja de cálculo por nombre y
  evitar errores de nombres duplicados.
draft: false
keywords:
- delete rows excel table
- add named range excel
- access worksheet by name
- how to add defined name
- named range on another sheet
language: es
og_description: Eliminar filas de una tabla de Excel usando C#. Este tutorial también
  muestra cómo agregar un rango con nombre en Excel y acceder a la hoja de cálculo
  por su nombre.
og_title: Delete Rows Excel Table with C# – Complete Guide
tags:
- C#
- Excel
- DevExpress Spreadsheet
title: Eliminar filas de una tabla de Excel con C# – Guía paso a paso
url: /es/net/row-and-column-management/delete-rows-excel-table-with-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Eliminar filas de una tabla de Excel con C# – Tutorial de programación completo

¿Alguna vez necesitaste **eliminar filas excel table** de un libro pero no estabas seguro de qué llamada API usar? No eres el único—la mayoría de los desarrolladores se topan con el mismo obstáculo cuando intentan reducir una tabla programáticamente por primera vez.  

En esta guía recorreremos un ejemplo completo y ejecutable que no solo elimina filas de una tabla de Excel, sino que también muestra **cómo agregar un nombre definido** (también llamado *named range*), cómo **acceder a la hoja de cálculo por nombre**, y por qué agregar un nombre duplicado en otra hoja lanza una `InvalidOperationException`.  

Al final del artículo podrás:

* Obtener una hoja de cálculo usando el nombre de su pestaña.  
* Eliminar de forma segura filas de datos de la primera tabla en esa hoja.  
* Crear un rango con nombre que apunte a una dirección específica.  
* Entender los problemas de nombres duplicados entre hojas.

No se requiere documentación externa—todo lo que necesitas está aquí.

---

## Lo que necesitarás

* **DevExpress Spreadsheet** (o cualquier biblioteca que exponga los objetos `Workbook`, `Worksheet`, `ListObject` y `Names`).  
* Un proyecto .NET que apunte a **.NET 6** o posterior (el código también compila con .NET Framework 4.8).  
* Familiaridad básica con C#—si puedes escribir un bucle `foreach`, estás listo.

> **Consejo profesional:** Si utilizas la edición Community gratuita de DevExpress, las API usadas a continuación son idénticas a la versión comercial.

---

## Paso 1 – Acceder a la hoja de cálculo por nombre

Lo primero que debes hacer es localizar la hoja que contiene la tabla que deseas modificar.  
La mayoría de los desarrolladores usan `Worksheets[0]` por costumbre, pero eso acopla tu código al orden de las hojas y se rompe tan pronto como alguien renombra una pestaña.

```csharp
using DevExpress.Spreadsheet;

// Assume 'workbook' is an already‑loaded Workbook instance
Worksheet worksheet = workbook.Worksheets["Sheet1"];   // <-- access worksheet by name
```

*Por qué es importante:* Al usar el **nombre** de la hoja en lugar de su índice evitas editar accidentalmente la hoja equivocada cuando el libro cambia.  

Si el nombre que proporcionas no existe, la biblioteca lanza una `KeyNotFoundException`, que puedes capturar para mostrar un mensaje de error amigable.

---

## Paso 2 – Eliminar filas de una tabla de Excel (de forma segura)

Ahora que tienes la hoja correcta, eliminemos las filas de datos de la primera tabla.  
Un error común es llamar a `DeleteRows(1, rowCount‑1)`. Desde **DevExpress 22.2** esa sobrecarga está **prohibida** y lanza una `InvalidOperationException`. La biblioteca espera que elimines filas **dentro del rango de datos de la tabla**, no la fila de encabezado.

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

> **¿Qué pasa si la tabla está vacía?** La condición `if` evita una llamada con `rowCount = 0`, lo que de otro modo generaría una excepción.

### Vista visual  

![delete rows excel table example](image.png "Captura de pantalla que muestra filas siendo eliminadas de una tabla de Excel")  

*Texto alternativo: ejemplo de eliminación de filas de tabla de Excel en código C#*

---

## Paso 3 – Cómo agregar un nombre definido (Crear un rango con nombre)

Después de limpiar la tabla, quizá quieras referirte a un rango específico más adelante—por ejemplo, para un gráfico o una lista de validación de datos. Ahí es donde **add named range excel** entra en juego.

```csharp
// Define a name that points to A1:C5 on Sheet1
workbook.Names.Add("MyTable", "Sheet1!$A$1:$C$5");

// Verify that the name exists
Name definedName = workbook.Names["MyTable"];
Console.WriteLine($"Defined name '{definedName.Name}' points to {definedName.RefersTo}");
```

El método `Names.Add` recibe dos parámetros: el identificador y la dirección en estilo A1.  
Como usamos **acceder a la hoja de cálculo por nombre** antes, la cadena de dirección puede referenciar de forma segura cualquier hoja sin preocuparse por cambios de índice.

---

## Paso 4 – Rango con nombre en otra hoja – Evitar errores de nombre duplicado

Podrías pensar que puedes reutilizar el mismo identificador en una hoja diferente, así:

```csharp
// Attempt to add the same name on Sheet2 – this will throw
workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

Desafortunadamente, el alcance de los nombres en Excel es **a nivel de libro**, no por hoja. La llamada anterior dispara una `InvalidOperationException` con el mensaje *“A name with the same identifier already exists.”*  

### Cómo solucionarlo

1. **Elige un nombre único** (`MyTable_Sheet2`).  
2. **Elimina el nombre existente** antes de volver a agregarlo (solo si realmente deseas reemplazarlo).  

```csharp
// Option A – use a unique name
workbook.Names.Add("MyTable_Sheet2", "Sheet2!$A$1:$C$5");

// Option B – replace the existing name (use with caution)
if (workbook.Names.Contains("MyTable"))
    workbook.Names.Remove("MyTable");

workbook.Names.Add("MyTable", "Sheet2!$A$1:$C$5");
```

---

## Ejemplo completo y ejecutable

Juntando todo, aquí tienes una aplicación de consola autónoma que puedes colocar en Visual Studio y ejecutar contra un archivo de ejemplo `sample.xlsx`.

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

**Resultado esperado**

* Todas las filas de datos de la primera tabla en **Sheet1** desaparecen, dejando solo la fila de encabezado.  
* El nombre **MyTable** ahora apunta a `Sheet1!$A$1:$C$5`.  
* Un segundo nombre **MyTable_Sheet2** referencia de forma segura un rango en **Sheet2** sin lanzar una excepción.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si el libro tiene varias tablas?* | Obtén el `ListObject` correcto por índice (`worksheet.ListObjects[1]`) o por nombre (`worksheet.ListObjects["MyTable"]`). |
| *¿Puedo eliminar filas de una tabla que abarca varias hojas?* | No—las tablas están confinadas a una sola hoja. Debes repetir la lógica de eliminación para cada hoja. |
| *¿Hay forma de eliminar solo un subconjunto de filas?* | Sí—usa `table.DeleteRows(startRow, count)` donde `startRow` es cero‑based dentro del área de datos de la tabla. |
| *¿Los rangos con nombre sobreviven después de guardar?* | Absolutamente. Una vez que llamas a `SaveDocument`, los nombres forman parte del XML del libro. |
| *¿Cómo listar todos los nombres definidos en el libro?* | Itera `foreach (var name in workbook.Names) Console.WriteLine(name.Name);`. |

---

## Conclusión

Hemos cubierto **eliminar filas excel table** usando C#, demostrado **add named range excel**, y mostrado la manera correcta de **acceder a la hoja de cálculo por nombre** evitando la temida excepción de nombre duplicado.  

La solución completa está en el fragmento de código anterior—cópialo, pégalo y ejecútalo contra tus propios archivos. Desde aquí puedes ampliar la lógica para manejar múltiples tablas, cálculos de rangos dinámicos, o incluso integrarlo con una interfaz de usuario.

**Próximos pasos** que podrías explorar:

* Usar **named range on another sheet** para impulsar series de gráficos.  
* Combinar la lógica de eliminación con **ExcelDataReader** para importar datos antes de limpiarlos.  
* Automatizar actualizaciones masivas en decenas de libros usando un simple bucle `foreach (var file in Directory.GetFiles(...))`.

¿Tienes más preguntas sobre la automatización de Excel en C#? Deja un comentario y sigamos la conversación. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}