---
category: general
date: 2026-03-18
description: Aprende cómo aplicar colores alternados a las filas en una hoja de cálculo
  usando C#. Incluye establecer el color de fondo de la fila, agregar un fondo amarillo
  claro y colorear las filas de forma alterna.
draft: false
keywords:
- apply alternating row colors
- set row background color
- add light yellow background
- set alternating row shading
- color rows alternately
language: es
og_description: Aplica colores alternados en filas en C# para mejorar la legibilidad.
  Esta guía muestra cómo establecer el color de fondo de la fila, agregar un fondo
  amarillo claro y colorear las filas de forma alterna.
og_title: Aplicar colores alternados a las filas en C# – Tutorial completo
tags:
- C#
- DataTable
- Spreadsheet styling
- UI design
title: Aplicar colores alternados a filas en C# – Guía paso a paso
url: /es/net/excel-colors-and-background-settings/apply-alternating-row-colors-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar colores de fila alternados en C# – Tutorial completo

¿Alguna vez necesitaste **aplicar colores de fila alternados** a una hoja de cálculo basada en datos pero no sabías por dónde empezar? No eres el único — la mayoría de los desarrolladores se topan con ese problema la primera vez que intentan que las tablas se vean un poco más amigables. ¿La buena noticia? En solo unas pocas líneas de C# puedes **establecer el color de fondo de la fila**, añadir un **fondo amarillo claro**, y obtener una cuadrícula pulida que mejora instantáneamente la legibilidad.

En este tutorial recorreremos todo el proceso, desde cargar un `DataTable` en memoria hasta dar estilo a cada fila con una sutil franja amarillo‑blanca. Al final podrás **colorear filas alternadamente** con confianza, y también verás algunas variaciones útiles para cuando necesites diferentes tonos o un tema dinámico.

## Lo que necesitarás

Antes de sumergirnos, asegúrate de tener lo siguiente a mano:

- Un proyecto .NET que apunte a .NET 6 o posterior (el código también funciona en .NET Framework 4.7+).  
- Una biblioteca de hojas de cálculo que admita objetos de estilo – el ejemplo usa una API genérica `Workbook`/`Worksheet` que refleja bibliotecas como **Aspose.Cells**, **GemBox.Spreadsheet**, o **ClosedXML**.  
- Una fuente `DataTable` – puede provenir de una consulta a base de datos, importación CSV, o cualquier colección en memoria.  

No se requieren paquetes NuGet adicionales más allá de la propia biblioteca de hojas de cálculo. Si usas Aspose.Cells, el espacio de nombres es `Aspose.Cells`; para ClosedXML es `ClosedXML.Excel`. Cambia las llamadas a `CreateStyle` e `ImportDataTable` según corresponda.

## Paso 1: Recuperar los datos fuente como DataTable

Lo primero—obtener los datos que deseas mostrar. En aplicaciones reales esto suele significar consultar una base de datos, pero para mayor claridad crearemos un método auxiliar llamado `GetData()` que devuelve un `DataTable` poblado.

```csharp
// Step 1: Retrieve the source data as a DataTable
DataTable dataTable = GetData();   // Replace with your actual data retrieval logic
```

> **Por qué es importante:** El `DataTable` define las filas y columnas que luego recibirán el sombreado alternado. Si la tabla está vacía, no hay nada que estilizar, así que siempre verifica que `Rows.Count` > 0 antes de continuar.

### Consejo profesional
Si estás obteniendo datos de Entity Framework, puedes usar `DataTable.Load(reader)` después de ejecutar un `SqlCommand`. Eso mantiene el código ordenado y evita definiciones manuales de columnas.

## Paso 2: Reservar una matriz para contener un estilo por cada fila

A continuación, necesitamos un contenedor que coincida con el número de filas. La mayoría de las APIs de hojas de cálculo permiten pasar una matriz de estilos al método de importación, así que crearemos un `Style[]` con el tamaño exacto del recuento de filas.

```csharp
// Step 2: Allocate an array to hold a style for each row
Style[] rowStyles = new Style[dataTable.Rows.Count];
```

> **Explicación:** Al pre‑asignar la matriz, evitamos crear un nuevo objeto de estilo en cada iteración, lo que puede ser una mejora de rendimiento cuando se manejan miles de filas.

## Paso 3: Aplicar colores de fila alternados (Amarillo claro / Blanco)

Ahora llega el corazón del asunto: **aplicar colores de fila alternados**. Recorreremos cada fila, crearemos una nueva instancia de estilo a partir del libro de trabajo y estableceremos su fondo según el índice de fila. Las filas pares obtienen un relleno amarillo claro, las impares permanecen blancas.

```csharp
// Step 3: Create alternating background colors (light yellow / white) for the rows
for (int rowIndex = 0; rowIndex < dataTable.Rows.Count; rowIndex++)
{
    // Create a new style instance from the workbook
    rowStyles[rowIndex] = wb.CreateStyle();

    // Apply a light yellow background to even rows, white to odd rows
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow   // add light yellow background
        : Color.White;        // set row background color to white

    rowStyles[rowIndex].Pattern = BackgroundType.Solid; // set alternating row shading
}
```

### Por qué funciona
- **`rowIndex % 2 == 0`** verifica si la fila es par.  
- **`Color.LightYellow`** brinda un tono suave y no intrusivo que es perfecto para tablas de datos.  
- **`BackgroundType.Solid`** asegura que el relleno cubra toda la celda, logrando el efecto de **establecer el color de fondo de la fila**.  

Puedes sustituir `Color.LightYellow` por cualquier otro tono (p. ej., `Color.LightCyan`) si prefieres un aspecto diferente. La misma lógica también te permite **colorear filas alternadamente** basándote en otros criterios, como banderas de estado.

## Paso 4: Importar el DataTable en la hoja de cálculo con los estilos preparados

Finalmente, volcamos todo en la hoja de cálculo. La mayoría de las bibliotecas exponen una sobrecarga de `ImportDataTable` que acepta una matriz de estilos. El valor `true` indica a la API que escriba los encabezados de columna, y las coordenadas `0, 0` inician en la celda superior‑izquierda.

```csharp
// Step 4: Import the DataTable into the worksheet, applying the prepared row styles
ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);
```

> **Resultado:** La hoja de cálculo ahora muestra tus datos con un patrón limpio de **sombreado de filas alternado**—amarillo claro en filas pares, blanco en filas impares. Los usuarios pueden escanear la cuadrícula sin que sus ojos salten de un lado a otro.

### Salida esperada
Si abres la hoja de cálculo resultante, verás algo como esto:

| ID | Nombre   | Cantidad |
|----|----------|----------|
| **1** | Apple      | 50       |
| **2** | Banana     | 30       |
| **3** | Cherry     | 20       |
| **4** | Date       | 15       |

Las filas 1, 3, 5… tienen un **fondo amarillo claro**, mientras que las filas 2, 4, 6… permanecen **blancas**. La fila de encabezado (fila 0) hereda el estilo predeterminado a menos que la personalices por separado.

## Variaciones opcionales y casos límite

### 1. Usar una paleta de colores diferente
Si el amarillo claro choca con tu identidad visual, simplemente reemplaza `Color.LightYellow` por otro `System.Drawing.Color`. Para un tema azul‑gris podrías usar:

```csharp
rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
    ? Color.FromArgb(220, 235, 247) // soft blue
    : Color.White;
```

### 2. Sombreado dinámico basado en datos
A veces deseas resaltar filas que cumplen una condición (p. ej., inventario bajo). Combina la comprobación de módulo con una prueba personalizada:

```csharp
int quantity = Convert.ToInt32(dataTable.Rows[rowIndex]["Quantity"]);
if (quantity < 20)
{
    rowStyles[rowIndex].ForegroundColor = Color.Salmon; // urgent low‑stock color
}
else
{
    rowStyles[rowIndex].ForegroundColor = (rowIndex % 2 == 0)
        ? Color.LightYellow
        : Color.White;
}
```

### 3. Aplicar estilos solo a columnas específicas
Si solo necesitas el **establecer el color de fondo de la fila** en ciertas columnas, crea un estilo separado para cada columna y asígnalo después de la importación usando la API de rangos de celdas de la hoja de cálculo.

```csharp
// Example for column B only
var colBStyle = wb.CreateStyle();
colBStyle.ForegroundColor = Color.LightYellow;
colBStyle.Pattern = BackgroundType.Solid;

// Apply after import
ws.Cells[$"B2:B{dataTable.Rows.Count + 1}"].SetStyle(colBStyle);
```

### 4. Consejo de rendimiento para tablas grandes
Al trabajar con > 10,000 filas, considera reutilizar un único objeto de estilo para cada color en lugar de crear uno nuevo por fila. La matriz entonces contiene referencias a los dos estilos compartidos, reduciendo drásticamente el uso de memoria.

```csharp
Style yellowStyle = wb.CreateStyle();
yellowStyle.ForegroundColor = Color.LightYellow;
yellowStyle.Pattern = BackgroundType.Solid;

Style whiteStyle = wb.CreateStyle();
whiteStyle.ForegroundColor = Color.White;
whiteStyle.Pattern = BackgroundType.Solid;

for (int i = 0; i < dataTable.Rows.Count; i++)
    rowStyles[i] = (i % 2 == 0) ? yellowStyle : whiteStyle;
```

## Ejemplo completo funcional

A continuación tienes un programa autónomo que puedes pegar en una aplicación de consola. Usa una API ficticia `Workbook`/`Worksheet`; sustituye los tipos por los de la biblioteca que hayas elegido.

```csharp
using System;
using System.Data;
using System.Drawing;          // For Color
using YourSpreadsheetLib;     // Replace with actual namespace

class Program
{
    static void Main()
    {
        // Initialize workbook & worksheet
        Workbook wb = new Workbook();
        Worksheet ws = wb.Worksheets[0];

        // Step 1: Retrieve data
        DataTable dataTable = GetData();

        // Step 2: Allocate style array
        Style[] rowStyles = new Style[dataTable.Rows.Count];

        // Step 3: Apply alternating row colors
        for (int i = 0; i < dataTable.Rows.Count; i++)
        {
            rowStyles[i] = wb.CreateStyle();
            rowStyles[i].ForegroundColor = (i % 2 == 0)
                ? Color.LightYellow   // add light yellow background
                : Color.White;        // set row background color
            rowStyles[i].Pattern = BackgroundType.Solid; // set alternating row shading
        }

        // Step 4: Import with styles
        ws.Cells.ImportDataTable(dataTable, true, 0, 0, rowStyles);

        // Save to file
        wb.Save("AlternatingRows.xlsx");
        Console.WriteLine("Workbook saved with alternating row colors.");
    }

    // Sample data generator
    static DataTable GetData()
    {
        var dt = new DataTable();
        dt.Columns.Add("ID", typeof(int));
        dt.Columns.Add("Product", typeof(string));
        dt.Columns.Add("Quantity", typeof(int));

        dt.Rows.Add(1, "Apple", 50);
        dt.Rows.Add(2, "Banana", 30);
        dt.Rows.Add(3, "Cherry", 20);
        dt.Rows.Add(4, "Date", 15);
        dt.Rows.Add(5, "Elderberry", 5);
        return dt;
    }
}
```

**Salida:** Un archivo llamado `AlternatingRows.xlsx` donde cada fila alterna entre un relleno amarillo claro y blanco, facilitando la lectura de la tabla.

## Preguntas frecuentes

**P: ¿Este enfoque funciona con formato condicional al estilo de Excel?**  
R: Sí. Si tu biblioteca admite reglas condicionales, puedes traducir la misma lógica a una regla que verifique `MOD(ROW(),2)=0`. El método basado en código mostrado aquí es más portátil entre bibliotecas que no disponen de formato condicional incorporado.

**P: ¿Qué pasa si necesito **colorear filas alternadamente** en una tabla PDF en lugar de una hoja de Excel?**  
R: La mayoría de los generadores de tablas PDF (p. ej., iTextSharp, PdfSharp) permiten establecer un `BackgroundColor` por fila. La misma cálculo de módulo se aplica—

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}