---
category: general
date: 2026-06-05
description: Aplica estilos de celda al usar la importación de Aspose.Cells. Aprende
  cómo importar DataTable con formato, dar estilo a las filas y mantener las hojas
  de cálculo ordenadas.
draft: false
keywords:
- apply cell styles
- aspose cells import
- import with formatting
- how to import datatable
- import datatable worksheet
language: es
og_description: Aplica estilos de celda al importar una DataTable en una hoja de cálculo
  de Aspose.Cells. Guía paso a paso con código completo y consejos.
og_title: Aplicar estilos de celda con Aspose.Cells – Importar DataTable
schemas:
- author: Aspose
  dateModified: '2026-06-05'
  description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  headline: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  type: TechArticle
- description: Apply cell styles while using Aspose.Cells import. Learn how to import
    DataTable with formatting, style rows, and keep worksheets tidy.
  name: Apply Cell Styles with Aspose.Cells – Import DataTable with Formatting
  steps:
  - name: How It Works
    text: 1. **Headers** – Because we passed `true`, Aspose writes “Name” and “Score”
      into the first row. 2. **Data Rows** – Each subsequent row receives the corresponding
      style from `importStyles`. 3. **Performance** – The method streams the data
      directly into the worksheet, which is faster than looping cell
  - name: What if My DataTable Has More Columns Than Styles?
    text: Aspose will apply the last style in the array to any extra columns. To avoid
      unexpected colors, always match the array length to the column count, or pass
      `null` for columns you don’t want styled.
  - name: Can I Apply Different Styles to Specific Rows?
    text: 'Absolutely. After the import, you can loop through rows and assign new
      `Style` objects based on conditions (e.g., highlight scores > 90 in green).
      Here’s a quick snippet:'
  - name: Does This Work with Large DataSets?
    text: Yes. `ImportDataTable` streams data efficiently, and applying a static style
      array adds negligible overhead. For millions of rows, consider using `ImportDataTable`
      in chunks or leveraging `Cells.ImportDataTable` with a `DataReader` for even
      better memory usage.
  - name: How Do I Preserve Existing Formatting in the Worksheet?
    text: If the target range already has formatting you want to keep, set the `ImportDataTable`
      overload’s `importOptions` parameter (`ImportTableOptions`) and tweak `ImportDataTableOptions.PreserveCellFormatting`.
      The default behavior overwrites styles with the ones you supply.
  type: HowTo
tags:
- Aspose.Cells
- C#
- DataTable
title: Aplicar estilos de celda con Aspose.Cells – Importar DataTable con formato
url: /es/net/excel-formatting-and-styling/apply-cell-styles-with-aspose-cells-import-datatable-with-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aplicar estilos de celda con Aspose.Cells – Importar DataTable con formato

¿Alguna vez te has preguntado cómo **aplicar estilos de celda** al extraer un `DataTable` a una hoja de Excel? No eres el único. En muchos escenarios de generación de informes necesitas que los datos se vean bien desde el principio, sin formateo manual posterior. La buena noticia es que Aspose.Cells facilita **importar con formato**, de modo que tus filas pueden ser rojas o azules, negritas o cualquier estilo que desees.

En este tutorial recorreremos un ejemplo completo y ejecutable que muestra **cómo importar un datatable** a una hoja de cálculo **con estilos de celda** aplicados. Al final tendrás una aplicación de consola C# lista para ejecutar que crea un libro, estiliza las dos primeras columnas y guarda el archivo, todo usando la API `aspose cells import`.

## Lo que aprenderás

- Configurar Aspose.Cells en un proyecto .NET  
- Construir un `DataTable` de ejemplo que imite datos del mundo real  
- Definir objetos `Style` para fuentes rojas y azules  
- Usar `Worksheet.Cells.ImportDataTable` para **importar datatable a la hoja** mientras se aplican los estilos  
- Verificar el resultado y guardar el libro  

Sin herramientas externas, solo C# puro y Aspose.Cells. ¡Comencemos!

---

## Requisitos previos

Antes de sumergirnos en el código, asegúrate de contar con lo siguiente:

| Requisito | Por qué es importante |
|-------------|----------------|
| .NET 6.0 o posterior | Aspose.Cells 23.x apunta a .NET Standard 2.0+, por lo que .NET 6 te brinda las últimas características del runtime. |
| Aspose.Cells para .NET (NuGet) | La biblioteca proporciona los métodos `Workbook`, `Worksheet`, `Style` y `ImportDataTable` que necesitamos. |
| Conocimientos básicos de C# | Entenderás clases, arreglos y sentencias `using`. |
| Un IDE (Visual Studio, VS Code, Rider) | Cualquier editor sirve, pero necesitarás restaurar los paquetes NuGet. |

Puedes instalar el paquete desde la línea de comandos:

```bash
dotnet add package Aspose.Cells
```

---

## Paso 1: Crear un nuevo Workbook y acceder a la primera hoja

Lo primero—creemos un `Workbook` y obtengamos la primera hoja. Piensa en el libro como un cuaderno en blanco; la primera hoja es la página donde escribiremos.

```csharp
using Aspose.Cells;
using System;
using System.Data;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Create a new workbook (equivalent to a new Excel file)
        Workbook wb = new Workbook();

        // Access the first worksheet (index 0)
        Worksheet worksheet = wb.Worksheets[0];
```

> **Consejo:** Si alguna vez necesitas varias hojas, simplemente añádelas con `wb.Worksheets.Add()` y haz referencia a ellas por nombre o índice.

---

## Paso 2: Preparar un DataTable de muestra (Cómo importar DataTable)

Ahora necesitamos algo que importar. En proyectos reales llamarías a una base de datos, pero para mayor claridad construiremos un `DataTable` en memoria.

```csharp
        // Build a sample DataTable with two columns: Name and Score
        DataTable dataTable = new DataTable("Results");
        dataTable.Columns.Add("Name", typeof(string));
        dataTable.Columns.Add("Score", typeof(int));

        // Populate rows – imagine these came from a query
        dataTable.Rows.Add("Alice", 85);
        dataTable.Rows.Add("Bob", 92);
        dataTable.Rows.Add("Charlie", 78);
        dataTable.Rows.Add("Diana", 91);
```

> **Por qué importa:** Tener un `DataTable` nos permite probar el flujo **aspose cells import** sin dependencias externas.

---

## Paso 3: Definir los estilos a aplicar a las celdas importadas

Aquí es donde ocurre la magia. Crearemos dos objetos `Style`: uno con fuente roja y otro con fuente azul. Estos se aplicarán por columna durante la importación.

```csharp
        // Define an array of styles – one per column
        Style[] importStyles = new Style[2];

        // Style for the first column (Name) – red text
        Style redStyle = wb.CreateStyle();
        redStyle.Font.Color = Color.Red;
        importStyles[0] = redStyle;

        // Style for the second column (Score) – blue text
        Style blueStyle = wb.CreateStyle();
        blueStyle.Font.Color = Color.Blue;
        importStyles[1] = blueStyle;
```

> **Cuidado:** La longitud de `importStyles` debe coincidir con el número de columnas que estás importando; de lo contrario Aspose lanzará una `ArgumentException`.

---

## Paso 4: Importar el DataTable a la hoja **con formato**

Ahora juntamos todo. La sobrecarga de `ImportDataTable` que usamos acepta el arreglo `Style[]`, permitiéndonos **aplicar estilos de celda** mientras los datos se insertan en la hoja.

```csharp
        // Import the DataTable starting at cell A1 (row 0, column 0)
        // The 'true' flag tells Aspose to generate column headers automatically
        worksheet.Cells.ImportDataTable(dataTable, true, 0, 0, importStyles);
```

### Cómo funciona

1. **Encabezados** – Como pasamos `true`, Aspose escribe “Name” y “Score” en la primera fila.  
2. **Filas de datos** – Cada fila subsiguiente recibe el estilo correspondiente del arreglo `importStyles`.  
3. **Rendimiento** – El método transmite los datos directamente a la hoja, lo que es más rápido que iterar celda por celda.

---

## Paso 5: Verificar el resultado y guardar el Workbook

Echemos un vistazo a las primeras celdas para asegurarnos de que los estilos se aplicaron, y luego escribamos el archivo en disco.

```csharp
        // Optional: Quick sanity check – print the first row's values
        Console.WriteLine("Header Row:");
        Console.WriteLine($"{worksheet.Cells[0, 0].StringValue} | {worksheet.Cells[0, 1].StringValue}");

        // Save the workbook to an Excel file
        string outputPath = "StyledImport.xlsx";
        wb.Save(outputPath);
        Console.WriteLine($"Workbook saved to {outputPath}");
    }
}
```

Al abrir **StyledImport.xlsx**, verás:

- La columna “Name” con texto **rojo**.  
- La columna “Score” con texto **azul**.  
- Los encabezados de columna con el estilo predeterminado (puedes estilarlos también, pero eso es otro tutorial).

![Ejemplo de aplicación de estilos de celda](https://example.com/images/apply-cell-styles.png "Aplicación de estilos de celda en Aspose.Cells")

> **Nota:** La imagen anterior muestra la apariencia final. El atributo `alt` contiene la palabra clave principal, cumpliendo con los requisitos SEO.

---

## Preguntas frecuentes y casos límite

### ¿Qué pasa si mi DataTable tiene más columnas que estilos?

Aspose aplicará el último estilo del arreglo a cualquier columna extra. Para evitar colores inesperados, siempre haz que la longitud del arreglo coincida con el número de columnas, o pasa `null` para las columnas que no deseas estilizar.

### ¿Puedo aplicar estilos diferentes a filas específicas?

Claro. Después de la importación, puedes recorrer las filas y asignar nuevos objetos `Style` según condiciones (por ejemplo, resaltar puntuaciones > 90 en verde). Aquí tienes un fragmento rápido:

```csharp
for (int i = 1; i <= dataTable.Rows.Count; i++) // start at 1 to skip header
{
    int score = worksheet.Cells[i, 1].IntValue;
    if (score > 90)
    {
        Style highScore = wb.CreateStyle();
        highScore.Font.Color = Color.Green;
        worksheet.Cells[i, 1].SetStyle(highScore);
    }
}
```

### ¿Esto funciona con conjuntos de datos grandes?

Sí. `ImportDataTable` transmite los datos de forma eficiente, y aplicar un arreglo estático de estilos añade una sobrecarga mínima. Para millones de filas, considera usar `ImportDataTable` en bloques o aprovechar `Cells.ImportDataTable` con un `DataReader` para un uso de memoria aún mejor.

### ¿Cómo preservo el formato existente en la hoja?

Si el rango de destino ya tiene formato que deseas conservar, configura el parámetro `importOptions` de la sobrecarga `ImportDataTable` (`ImportTableOptions`) y ajusta `ImportDataTableOptions.PreserveCellFormatting`. El comportamiento predeterminado sobrescribe los estilos con los que suministres.

---

## Resumen: Lo que logramos

- **Aplicamos estilos de celda** durante una operación **aspose cells import**.  
- Demostramos **importar con formato** pasando un arreglo `Style[]`.  
- Mostramos **cómo importar datatable** a una hoja y guardar el resultado.  
- Cubrimos casos límite como conteos de estilo no coincidentes y estilizado condicional de filas.

Todo esto se realizó en una única aplicación de consola autocontenida, sin scripts externos ni manipulación manual de Excel. Ahora tienes una base sólida para cualquier función de informes o exportación de datos que requiera una salida de Excel pulida.

---

## Próximos pasos

¿Listo para subir de nivel? Aquí tienes algunas ideas que amplían lo que acabas de aprender:

- **Estilizar la fila de encabezado** (por ejemplo, negrita, color de fondo).  
- **Aplicar formato condicional** usando `Worksheet.Cells[i, j].ConditionalFormattingCollection`.  
- **Exportar a otros formatos** como CSV o PDF con `wb.Save("file.pdf", SaveFormat.Pdf)`.  
- **Combinar varios DataTables** en un solo libro, cada uno en su propia hoja, usando el mismo enfoque de estilizado.

Si encuentras algún obstáculo, deja un comentario o consulta la documentación oficial de Aspose sobre `ImportDataTable`. ¡Feliz codificación y disfruta de esos archivos Excel bellamente estilizados!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [How to Import DataTable into Excel Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/import-export/import-datatable-excel-aspose-cells-net/)
- [How to Set Font Styles in Excel Using Aspose.Cells for .NET (Step‑By‑Step Guide)](/cells/english/net/formatting/aspose-cells-dotnet-set-font-styles-excel/)
- [How to Apply Text Shadow in Excel Using Aspose.Cells .NET: A Step‑By‑Step Guide](/cells/english/net/formatting/apply-text-shadow-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}