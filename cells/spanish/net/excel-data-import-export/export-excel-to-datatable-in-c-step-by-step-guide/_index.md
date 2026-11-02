---
category: general
date: 2026-03-25
description: Aprende a exportar Excel a DataTable en C# rápidamente. Este tutorial
  cubre la exportación de Excel con nombres de columna y la exportación de datos de
  Excel como cadena para un manejo de datos fiable.
draft: false
keywords:
- export excel to datatable
- how to export excel to datatable
- export excel with column names
- export excel data as string
language: es
og_description: Exporta Excel a DataTable en C# con nombres de columna y conversión
  a cadena. Sigue este tutorial conciso para obtener una solución lista para ejecutar.
og_title: Exportar Excel a DataTable en C# – Guía completa
tags:
- C#
- Aspose.Cells
- DataTable
- Excel
title: Exportar Excel a DataTable en C# – Guía paso a paso
url: /es/net/excel-data-import-export/export-excel-to-datatable-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exportar Excel a DataTable en C# – Guía paso a paso

¿Alguna vez necesitaste **exportar Excel a DataTable** pero no estabas seguro de qué opciones activar? No estás solo—muchos desarrolladores se encuentran con el mismo obstáculo la primera vez que intentan extraer datos de una hoja de cálculo a un `DataTable`.  

¿La buena noticia? En solo unas pocas líneas de código puedes **exportar Excel con nombres de columna** e incluso **exportar datos de Excel como cadena** para evitar dolores de cabeza por incompatibilidades de tipos. A continuación encontrarás un ejemplo completo y ejecutable más el “por qué” de cada configuración, para que puedas adaptarlo a cualquier proyecto sin conjeturas.

## Qué cubre este tutorial

* Cómo crear un libro de trabajo en memoria (sin necesidad de un archivo físico).  
* Poblar algunas filas de ejemplo para que puedas ver el resultado al instante.  
* Configurar `ExportTableOptions` para que cada celda se trate como una cadena.  
* Exportar un rango rectangular a un `DataTable` conservando la primera fila como encabezados de columna.  
* Verificar la salida e imprimir la primera fila en la consola.  

No se requieren enlaces a documentación externa—todo lo que necesitas está aquí. Si ya tienes un archivo Excel en disco, simplemente reemplaza la línea de creación del libro de trabajo con `new Workbook("path/to/file.xlsx")` y listo.

---

## Paso 1: Configura el proyecto y agrega el paquete NuGet Aspose.Cells

Antes de escribir cualquier código, asegúrate de que tu proyecto haga referencia a **Aspose.Cells for .NET** (la biblioteca que impulsa la clase `Workbook`). Puedes agregarlo mediante el Administrador de paquetes NuGet:

```bash
dotnet add package Aspose.Cells
```

> **Consejo profesional:** Usa la última versión estable (a partir de marzo 2026, es 22.12) para obtener las correcciones de errores y mejoras de rendimiento más recientes.

---

## Paso 2: Crea un Workbook y llénalo con datos de ejemplo

Comenzaremos con un `Workbook` recién creado y escribiremos un par de filas para que puedas ver la exportación en acción. Este paso también demuestra **cómo exportar excel a datatable** cuando los datos de origen viven solo en memoria.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook and grab the first worksheet
        Workbook workbook = new Workbook();                 // in‑memory workbook
        Worksheet worksheet = workbook.Worksheets[0];

        // 2️⃣ Populate a few cells – this mimics a real Excel file
        worksheet.Cells["A1"].PutValue("Name");   // column header
        worksheet.Cells["B1"].PutValue("Age");    // column header
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);
```

*Por qué es importante:* Al insertar la fila de encabezado primero (`A1` & `B1`), luego podemos indicarle al exportador que trate la primera fila como nombres de columna—exactamente lo que significa **exportar excel con nombres de columna**.

---

## Paso 3: Indica a Aspose.Cells que trate cada celda como una cadena

Cuando exportas celdas numéricas o de fecha, Aspose intenta inferir el tipo .NET. Eso puede causar errores sutiles si tu código posterior espera cadenas. La bandera `ExportTableOptions.ExportAsString` fuerza una conversión uniforme a cadena.

```csharp
        // 3️⃣ Configure export options – all values will be strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true       // <-- ensures Export Excel Data As String
        };
```

*¿Por qué usar esto?* Imagina una columna que a veces contiene números y a veces texto (p. ej., “00123” vs. “ABC”). Al exportar todo como cadena evitas perder ceros a la izquierda o provocar excepciones de conversión de tipo.

---

## Paso 4: Exporta el rango deseado a un DataTable

Ahora realmente **exportamos excel a datatable**. El método `ExportDataTable` recibe la fila/columna de inicio, el número de filas/columnas, una bandera para la extracción de nombres de columna y las opciones que acabamos de crear.

```csharp
        // 4️⃣ Export rows 0‑9 and columns 0‑4 (adjust as needed)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,   // <-- uses the first row as headers
            exportOptions: exportOptions);
```

*¿Qué está sucediendo bajo el capó?*  
- `startRow: 0` apunta a la primera fila de Excel (la fila de encabezado).  
- `exportColumnNames: true` indica a Aspose que eleve “Name” y “Age” a la colección de columnas del `DataTable`.  
- `totalRows`/`totalColumns` pueden ser mayores que los datos reales; las celdas excedentes se convierten en cadenas vacías debido a `ExportAsString`.

---

## Paso 5: Verifica el resultado – Imprime la primera fila

Una rápida volcada en la consola demuestra que la conversión se realizó con éxito y que los nombres de columna están intactos.

```csharp
        // 5️⃣ Show the first data row (if any)
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

**Salida esperada**

```
First row: Alice, 30
```

Si cambias los datos de ejemplo, la consola reflejará esos cambios automáticamente—no se necesita código adicional.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| **¿Puedo exportar una hoja que ya existe en disco?** | Sí—reemplaza `new Workbook()` con `new Workbook("myFile.xlsx")`. El resto de los pasos permanece idéntico. |
| **¿Qué pasa si mi archivo Excel tiene celdas combinadas?** | Las celdas combinadas se desenvuelven; el valor de la celda superior‑izquierda se usa para todo el rango combinado. |
| **¿Debo preocuparme por formatos de número específicos de cultura?** | No cuando `ExportAsString = true`; todo llega como la cadena cruda mostrada en Excel. |
| **¿Cuántas filas puedo exportar de una vez?** | Aspose.Cells puede manejar millones de filas, pero el consumo de memoria crece con el tamaño del `DataTable`. Considera paginar si alcanzas límites. |
| **¿Qué pasa con las columnas ocultas?** | Las columnas ocultas se exportan a menos que establezcas `ExportHiddenColumns = false` en `ExportTableOptions`. |

---

## Bonus: Exportar a CSV en lugar de un DataTable

A veces puedes preferir un archivo plano. Las mismas `ExportTableOptions` pueden reutilizarse con `ExportDataTableToCSV`:

```csharp
        string csvPath = "output.csv";
        worksheet.Cells.ExportDataTableToCSV(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            csvPath,
            exportColumnNames: true,
            exportOptions);
        Console.WriteLine($"CSV written to {csvPath}");
```

Esa única línea te brinda un CSV listo para importar mientras sigue **exportando datos de excel como cadena**.

---

## Ejemplo completo y funcional (listo para copiar y pegar)

Ejecuta el programa (`dotnet run`) y verás el resultado del **export excel to datatable** impreso en la consola. Cambia los datos de ejemplo, modifica `totalRows`/`totalColumns`, o apunta el workbook a un archivo real—todo escala.

```csharp
using System;
using System.Data;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create workbook and worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Populate sample data (header + two rows)
        worksheet.Cells["A1"].PutValue("Name");
        worksheet.Cells["B1"].PutValue("Age");
        worksheet.Cells["A2"].PutValue("Alice");
        worksheet.Cells["B2"].PutValue(30);
        worksheet.Cells["A3"].PutValue("Bob");
        worksheet.Cells["B3"].PutValue(25);

        // Export everything as strings
        ExportTableOptions exportOptions = new ExportTableOptions
        {
            ExportAsString = true
        };

        // Export range to DataTable (first row = column names)
        DataTable table = worksheet.Cells.ExportDataTable(
            startRow: 0,
            startColumn: 0,
            totalRows: 10,
            totalColumns: 5,
            exportColumnNames: true,
            exportOptions: exportOptions);

        // Display first row
        if (table.Rows.Count > 0)
        {
            Console.WriteLine($"First row: {table.Rows[0]["Name"]}, {table.Rows[0]["Age"]}");
        }
        else
        {
            Console.WriteLine("The exported DataTable is empty.");
        }
    }
}
```

---

## Conclusión

Ahora tienes una **solución completa y autónoma para exportar Excel a DataTable** en C#. Configurando `ExportTableOptions.ExportAsString` garantizas que **exportes datos de excel como cadena**, y al establecer `exportColumnNames: true` obtienes los encabezados de columna familiares que esperas al **exportar excel con nombres de columna**.  

A partir de aquí puedes:

* Alimentar el `DataTable` a Entity Framework o Dapper para inserciones masivas.  
* Pasarlo a un motor de informes como **FastReport** o **RDLC**.  
* Convertirlo a JSON para una respuesta de API (`JsonConvert.SerializeObject(table)`).

Siéntete libre de experimentar—quizás probar exportar una hoja más grande, o combinar esto con **cómo exportar excel a datatable** desde un recurso compartido en red. El patrón sigue siendo el mismo, y el código está listo para producción.

---

![Diagrama del flujo de conversión de Excel → DataTable – export excel to datatable](https://example.com/placeholder.png "diagrama de export excel to datatable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}