---
category: general
date: 2026-03-27
description: Cómo crear una tabla dinámica en C# usando Aspose.Cells – aprende a agregar
  datos, habilitar la actualización y guardar el libro de trabajo como xlsx en un
  solo tutorial.
draft: false
keywords:
- how to create pivot
- save workbook as xlsx
- how to enable refresh
- how to add data
- generate excel file c#
language: es
og_description: Cómo crear una tabla dinámica en C# con Aspose.Cells. Esta guía le
  muestra cómo agregar datos, habilitar la actualización y guardar el libro de trabajo
  como xlsx.
og_title: Cómo crear una tabla dinámica en C# – Tutorial completo de Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel automation
title: Cómo crear una tabla dinámica en C# – Guía completa con Aspose.Cells
url: /es/net/creating-and-configuring-pivot-tables/how-to-create-pivot-in-c-full-guide-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear una tabla dinámica en C# – Tutorial completo de Aspose.Cells

¿Alguna vez te has preguntado **cómo crear una tabla dinámica** en C# sin lidiar con COM interop? No eres el único. En muchas aplicaciones basadas en datos necesitamos una forma rápida de convertir cifras de ventas crudas en un resumen ordenado, y Aspose.Cells lo hace muy fácil.  

En este tutorial recorreremos cada paso: añadir datos, crear la tabla dinámica, activar la actualización automática y, finalmente, **guardar el libro como xlsx** para que tus usuarios lo abran en Excel al instante. Al final tendrás un archivo `PivotRefresh.xlsx` listo para usar y una comprensión sólida de por qué cada línea es importante.

## Requisitos previos

- .NET 6+ (o .NET Framework 4.7.2 y posteriores) – cualquier runtime reciente funciona.
- Aspose.Cells para .NET – puedes obtenerlo desde NuGet (`Install-Package Aspose.Cells`).
- Familiaridad básica con la sintaxis de C# – no se requiere un conocimiento profundo de Excel.

> **Consejo profesional:** Si trabajas en una máquina corporativa, asegúrate de que la licencia de Aspose esté aplicada; de lo contrario aparecerá una marca de agua en el archivo generado.

## Paso 1 – Cómo añadir datos a un nuevo libro

Antes de que exista una tabla dinámica, debe haber una tabla de origen. Crearemos un libro nuevo, nombraremos la primera hoja *SalesData* y añadiremos unas cuantas filas que imitan una descarga real de ventas.

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // 1️⃣ Create a new workbook and grab the default sheet
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        // 2️⃣ Write column headers
        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // 3️⃣ Insert a sample row – add more rows as your scenario demands
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);
```

**Por qué es importante:**  
- Usar `PutValue` establece automáticamente el tipo de celda, por lo que no tendrás que preocuparte por incompatibilidades entre cadenas y números más adelante.  
- Definir los encabezados en la fila 1 le da al motor de tabla dinámica algo a lo que referirse al mapear los campos.

## Paso 2 – Crear una hoja que alojará la tabla dinámica

Una tabla dinámica vive en su propia hoja, manteniendo los datos de origen limpios y el informe ordenado.

```csharp
        // 4️⃣ Add a dedicated sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");
```

> **¿Y si ya tienes una hoja?** Simplemente haz referencia a ella por índice (`workbook.Worksheets["MySheet"]`) en lugar de añadir una nueva.

## Paso 3 – Definir el rango de origen (Cómo añadir datos → Definir rango)

Aspose.Cells necesita un `CellArea` o una cadena de rango que incluya tanto los encabezados como los datos. Aquí asumimos un máximo de 100 filas; ajústalo según sea necesario.

```csharp
        // 5️⃣ Build the source range (A1:D100 covers headers + up to 99 data rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");
```

**Caso límite:** Si tu conjunto de datos es dinámico, puedes calcular la última fila usada con `salesDataSheet.Cells.MaxDataRow` y construir el rango en consecuencia.

## Paso 4 – Cómo crear la tabla dinámica – Insertar la tabla dinámica

Ahora la parte divertida: le decimos a Aspose.Cells que cree una tabla dinámica vinculada al rango que acabamos de definir.

```csharp
        // 6️⃣ Insert the pivot table at cell A3 of the pivot sheet
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];
```

Observa la referencia al estilo de fórmula (`=SalesData!A1:D100`). Esa es la misma sintaxis que escribirías en Excel, lo que hace que la API sea intuitiva.

## Paso 5 – Configurar campos de fila, columna y datos (Cómo añadir datos → Campos)

Colocaremos *Region* en filas, *Product* en columnas y sumaremos tanto *Units* como *Revenue*.

```csharp
        // 7️⃣ Set up row, column, and data fields
        pivotTable.RowFields.Add(0); // 0 = first column => Region
        pivotTable.ColumnFields.Add(1); // 1 = second column => Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);
```

**¿Por qué estos índices?**  
Aspose.Cells indexa las columnas comenzando en 0, por lo que `0` apunta a *Region*. El método `DataFields.Add` te permite renombrar el campo (p. ej., “Sum of Units”) y elegir un tipo de agregación – `Sum` es el más común para datos numéricos.

## Paso 6 – Cómo habilitar la actualización – Hacer que la tabla dinámica se actualice automáticamente al abrir

Si los datos de origen cambian después, probablemente quieras que la tabla dinámica refleje esos cambios automáticamente. Ahí es donde `RefreshDataOnOpen` brilla.

```csharp
        // 8️⃣ Turn on automatic refresh when the file is opened
        pivotTable.RefreshDataOnOpen = true;
```

> **Nota:** Esta bandera solo funciona cuando el libro se abre en Excel; no volverá a calcularse dentro de Aspose.Cells a menos que llames a `pivotTable.RefreshData()` manualmente.

## Paso 7 – Guardar el libro como XLSX (Cómo guardar el libro como XLSX)

Finalmente, persistimos el archivo en disco. El formato `.xlsx` es el tipo de archivo moderno basado en zip que funciona en todas partes.

```csharp
        // 9️⃣ Save the workbook – this also satisfies the “save workbook as xlsx” requirement
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Ejecutar el programa genera un archivo llamado **PivotRefresh.xlsx** en la carpeta de ejecución. Ábrelo en Excel y verás una tabla dinámica ordenada con filas *Región*, columnas *Product* y valores sumados de *Units* y *Revenue*. Como habilitamos la actualización, cualquier edición que realices en la hoja *SalesData* actualizará automáticamente la tabla dinámica la próxima vez que abras el libro.

### Salida esperada

| Región | Widget | Gadget | … |
|--------|--------|--------|---|
| Este   | 120    | 0      |   |
| Oeste  | 0      | 85     |   |
| **Total General** | **120** | **85** |   |

*(Los números variarán según las filas que añadas.)*

---

## Preguntas frecuentes y variaciones

### ¿Qué pasa si necesito varias tablas dinámicas?

Puedes repetir el **Paso 4** con un nombre y ubicación diferentes. Cada llamada a `PivotTables.Add` devuelve un nuevo índice que puedes usar para obtener el objeto de tabla.

### ¿Cómo cambio la agregación a *Average* en lugar de *Sum*?

Reemplaza `PivotTableDataAggregationType.Sum` por `PivotTableDataAggregationType.Average` en las llamadas a `DataFields.Add`.

### ¿Puedo dar estilo a la tabla dinámica (fuentes, colores)?

Sí. Después de crear la tabla, puedes acceder a su propiedad `Style` o aplicar formato de celda al rango que contiene la tabla dinámica. Por ejemplo:

```csharp
pivotTable.Style = workbook.Styles[workbook.Styles.Add()];
pivotTable.Style.Font.Color = System.Drawing.Color.DarkBlue;
```

### ¿Es posible añadir más filas después de guardar el libro?

Absolutamente. Carga el archivo con `new Workbook("PivotRefresh.xlsx")`, agrega filas a la hoja *SalesData* y llama a `pivotTable.RefreshData()` antes de volver a guardarlo.

---

## Ejemplo completo (listo para copiar y pegar)

```csharp
using Aspose.Cells;
using Aspose.Cells.Pivot;

class PivotRefreshTutorial
{
    static void Main()
    {
        // Step 1: Create workbook & add sample data
        var workbook = new Workbook();
        var salesDataSheet = workbook.Worksheets[0];
        salesDataSheet.Name = "SalesData";

        salesDataSheet.Cells["A1"].PutValue("Region");
        salesDataSheet.Cells["B1"].PutValue("Product");
        salesDataSheet.Cells["C1"].PutValue("Units");
        salesDataSheet.Cells["D1"].PutValue("Revenue");

        // Sample rows – extend as needed
        salesDataSheet.Cells["A2"].PutValue("East");
        salesDataSheet.Cells["B2"].PutValue("Widget");
        salesDataSheet.Cells["C2"].PutValue(120);
        salesDataSheet.Cells["D2"].PutValue(5400);

        salesDataSheet.Cells["A3"].PutValue("West");
        salesDataSheet.Cells["B3"].PutValue("Gadget");
        salesDataSheet.Cells["C3"].PutValue(85);
        salesDataSheet.Cells["D3"].PutValue(4250);

        // Step 2: Add sheet for the pivot
        var pivotSheet = workbook.Worksheets.Add("PivotReport");

        // Step 3: Define source range (covers up to 100 rows)
        var sourceRange = salesDataSheet.Cells.CreateRange("A1:D100");

        // Step 4: Insert pivot table
        int pivotIndex = pivotSheet.PivotTables.Add("=SalesData!A1:D100", "A3", "SalesPivot");
        var pivotTable = pivotSheet.PivotTables[pivotIndex];

        // Step 5: Configure fields
        pivotTable.RowFields.Add(0); // Region
        pivotTable.ColumnFields.Add(1); // Product
        pivotTable.DataFields.Add(2, "Sum of Units", PivotTableDataAggregationType.Sum);
        pivotTable.DataFields.Add(3, "Sum of Revenue", PivotTableDataAggregationType.Sum);

        // Step 6: Enable automatic refresh
        pivotTable.RefreshDataOnOpen = true;

        // Step 7: Save as .xlsx
        workbook.Save("PivotRefresh.xlsx");
    }
}
```

Guarda el archivo, ejecútalo y abre el **PivotRefresh.xlsx** generado – acabas de dominar **cómo crear una tabla dinámica** en C#.

---

## Conclusión

Hemos cubierto **cómo crear tablas dinámicas** programáticamente, cómo **añadir datos**, cómo **habilitar la actualización** y, finalmente, cómo **guardar el libro como xlsx** usando Aspose.Cells. El código

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}