---
category: general
date: 2026-07-14
description: Guarda Excel como HTML rápidamente y aprende cómo convertir Excel a HTML
  con formato completo. Exporta Excel con formato usando Aspose.Cells en minutos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- save excel as html
- convert excel to html
- export excel with formatting
- Aspose.Cells HTML export
- Grid.js number formatting
language: es
lastmod: 2026-07-14
og_description: Guarda Excel como HTML al instante. Esta guía muestra cómo convertir
  Excel a HTML preservando los estilos y habilitando el formato de números de Grid.js.
og_image_alt: Screenshot of a spreadsheet saved as HTML using Aspose.Cells – save
  excel as html example
og_title: Guardar Excel como HTML – Exportación paso a paso con formato completo
schemas:
- author: Aspose
  dateModified: '2026-07-14'
  description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  headline: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  type: TechArticle
- description: Save Excel as HTML quickly and learn how to convert Excel to HTML with
    full formatting. Export Excel with formatting using Aspose.Cells in minutes.
  name: Save Excel as HTML – Complete Guide to Export Excel with Formatting
  steps:
  - name: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
    text: '**Styling intact?** Compare cell background colors and borders to the original
      Excel view.'
  - name: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
    text: '**Number formats preserved?** Look for the `data-format` attribute on `<td>`
      elements.'
  - name: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
    text: '**Images displayed?** If you exported images as Base64, they should appear
      inline.'
  - name: '**Browser console clean?** No JavaScript errors related to Grid.js.'
    text: '**Browser console clean?** No JavaScript errors related to Grid.js.'
  type: HowTo
tags:
- Excel
- HTML
- Aspose.Cells
title: Guardar Excel como HTML – Guía completa para exportar Excel con formato
url: /es/net/exporting-excel-to-html-with-advanced-options/save-excel-as-html-complete-guide-to-export-excel-with-forma/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Guardar Excel como HTML – Guía completa para exportar Excel con formato

¿Alguna vez te has preguntado cómo **guardar Excel como HTML** sin perder los colores, bordes o formatos de número? No eres el único. En muchos escenarios de informes necesitas una vista lista para la web de un libro de trabajo, y la forma más rápida es exportar el archivo directamente a HTML.  

En este tutorial recorreremos paso a paso cómo **convertir Excel a HTML** usando Aspose.Cells, habilitar el formato numérico de Grid.js y asegurarnos de que el resultado se vea idéntico a la hoja de cálculo original. Al final tendrás un archivo HTML listo para usar que podrás servir desde cualquier servidor web.

## Lo que aprenderás

- Requisitos previos e instalación del paquete  
- Cargar un libro de trabajo existente (o crear uno sobre la marcha)  
- Configurar `HtmlSaveOptions` para una fidelidad visual perfecta  
- Habilitar `GridJsOptions.EnableNumberFormat` para mantener el estilo numérico intacto  
- Guardar el archivo y verificar el resultado  

Si alguna vez intentaste **exportar Excel con formato** usando una exportación genérica a CSV, sabes lo frustrante que es cuando los números se convierten en texto plano. Esta guía evita esa trampa.

---

## Requisitos previos – Configura tu entorno de desarrollo

Antes de sumergirnos en el código, asegúrate de contar con:

| Requisito | Por qué es importante |
|-----------|-----------------------|
| .NET 6.0 o posterior (el tutorial usa .NET 6) | APIs modernas y mejor rendimiento |
| Visual Studio 2022 (o VS Code con la extensión C#) | Edición y depuración cómodas |
| Paquete NuGet Aspose.Cells para .NET | La biblioteca que impulsa `HtmlSaveOptions` y `GridJsOptions` |
| Un archivo Excel de muestra (`sample.xlsx`) o un libro que generes en código | La fuente que convertirás |

Instala Aspose.Cells con el siguiente comando en la Consola del Administrador de paquetes:

```powershell
Install-Package Aspose.Cells
```

> **Consejo profesional:** Si trabajas en una canalización CI, agrega la misma línea `dotnet add package` a tu script de compilación para que la dependencia esté siempre presente.

---

## Paso 1: Cargar o crear un libro de trabajo

Puedes cargar un archivo existente o crear uno programáticamente. Aquí tienes un ejemplo mínimo que crea un libro con algunas celdas con estilo para que puedas ver cómo el formato sobrevive a la exportación.

```csharp
using Aspose.Cells;
using System.Drawing;

// Create a new workbook
Workbook wb = new Workbook();
Worksheet sheet = wb.Worksheets[0];
sheet.Name = "Report";

// Populate some data
sheet.Cells["A1"].PutValue("Product");
sheet.Cells["B1"].PutValue("Price");
sheet.Cells["A2"].PutValue("Widget");
sheet.Cells["B2"].PutValue(19.99);
sheet.Cells["A3"].PutValue("Gadget");
sheet.Cells["B3"].PutValue(42.5);

// Apply basic styling
Style headerStyle = wb.CreateStyle();
headerStyle.Font.IsBold = true;
headerStyle.ForegroundColor = Color.LightGray;
headerStyle.Pattern = BackgroundType.Solid;
sheet.Cells["A1:B1"].SetStyle(headerStyle);

// Format the price column as currency
Style priceStyle = wb.CreateStyle();
priceStyle.Number = 164; // Built‑in currency format
sheet.Cells["B2:B3"].SetStyle(priceStyle);
```

> **Por qué es importante:** Al establecer explícitamente los formatos numéricos, más adelante verás que `GridJsOptions.EnableNumberFormat` mantiene esos formatos vivos en la salida HTML.

---

## Paso 2: Configurar opciones de guardado HTML

Ahora creamos una instancia de `HtmlSaveOptions`. Este objeto indica a Aspose.Cells exactamente cómo deseas que se renderice el HTML.

```csharp
// Step 2: Create HTML save options
HtmlSaveOptions htmlOptions = new HtmlSaveOptions
{
    // Export the entire workbook as a single HTML page
    ExportActiveWorksheetOnly = false,

    // Keep the original cell styles (fonts, colors, borders)
    ExportGridLines = true,
    ExportColumnHeaders = true,
    ExportRowHeaders = true
};
```

### Habilitando el formato numérico de Grid.js

Si planeas incrustar el HTML en una página que usa **Grid.js** para tablas interactivas, querrás que los números mantengan su formato (por ejemplo, símbolos de moneda, separadores de miles). La siguiente línea hace precisamente eso:

```csharp
// Step 3: Enable number formatting for Grid.js tables
htmlOptions.GridJsOptions = new GridJsOptions { EnableNumberFormat = true };
```

> **¿Qué ocurre tras bambalinas?** `EnableNumberFormat` inyecta un pequeño fragmento de JavaScript que indica a Grid.js interpretar el atributo `data-format` de la celda, preservando el formato al estilo Excel en el navegador.

---

## Paso 3: Guardar el libro de trabajo como archivo HTML

Con el libro listo y las opciones afinadas, la última línea escribe el archivo HTML en disco.

```csharp
// Step 4: Save the workbook as an HTML file with the configured options
string outputPath = @"C:\Temp\gridjs.html";
wb.Save(outputPath, htmlOptions);
Console.WriteLine($"Workbook successfully saved as HTML to: {outputPath}");
```

Ejecutar el programa genera un archivo `gridjs.html` que se ve así (vista simplificada):

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Report</title>
    <link rel="stylesheet" href="gridjs.css" />
    <script src="gridjs.js"></script>
</head>
<body>
    <table class="gridjs-table">
        <thead>
            <tr><th>Product</th><th>Price</th></tr>
        </thead>
        <tbody>
            <tr><td>Widget</td><td data-format="$#,##0.00">19.99</td></tr>
            <tr><td>Gadget</td><td data-format="$#,##0.00">42.5</td></tr>
        </tbody>
    </table>
</body>
</html>
```

Abre el archivo en cualquier navegador y verás una tabla bien estilizada, con el fondo gris claro del encabezado y el formato de moneda. Si insertas la página en un sitio que ya carga Grid.js, los números se renderizarán automáticamente con las comas y símbolos correctos.

---

## Problemas comunes al **convertir Excel a HTML**

| Problema | Por qué ocurre | Cómo evitarlo |
|----------|----------------|---------------|
| **Fórmulas perdidas** | HTML es estático; las fórmulas se convierten en valores simples. | Si necesitas cálculos en tiempo real, mantén el libro en el servidor y usa bibliotecas JavaScript como SheetJS. |
| **Imágenes ausentes** | Las imágenes se guardan como recursos separados. | Configura `HtmlSaveOptions.ExportImagesAsBase64 = true` para incrustarlas directamente. |
| **Archivos enormes** | Libros grandes generan HTML + JS masivo. | Usa `ExportOnlyVisibleSheets` o divide en varias páginas mediante `HtmlSaveOptions.OnePagePerSheet`. |
| **Configuración regional de números incorrecta** | Excel guarda los números en cultura invariante, los navegadores pueden aplicar la configuración local. | Establece explícitamente `htmlOptions.Encoding = Encoding.UTF8` y usa `GridJsOptions.EnableNumberFormat`. |

---

## Avanzado: Exportar varias hojas con instancias individuales de Grid.js

Si tu libro contiene varias hojas y deseas que cada una se convierta en su propia tabla Grid.js, puedes iterar sobre las hojas de cálculo y guardarlas por separado:

```csharp
for (int i = 0; i < wb.Worksheets.Count; i++)
{
    Worksheet ws = wb.Worksheets[i];
    HtmlSaveOptions opt = new HtmlSaveOptions
    {
        ExportActiveWorksheetOnly = true,
        GridJsOptions = new GridJsOptions { EnableNumberFormat = true }
    };
    string sheetPath = $@"C:\Temp\{ws.Name}.html";
    wb.Save(sheetPath, opt);
    Console.WriteLine($"Saved {ws.Name} to {sheetPath}");
}
```

Cada archivo contendrá su propio elemento `<table class="gridjs-table">`, listo para manipulación independiente.

---

## Verificando la salida – Lista de verificación rápida

1. **¿Estilos intactos?** Compara los colores de fondo y bordes de las celdas con la vista original de Excel.  
2. **¿Formatos numéricos preservados?** Busca el atributo `data-format` en los elementos `<td>`.  
3. **¿Imágenes mostradas?** Si exportaste imágenes como Base64, deberían aparecer en línea.  
4. **¿Consola del navegador limpia?** Sin errores JavaScript relacionados con Grid.js.  

Si alguna de estas comprobaciones falla, revisa la propiedad correspondiente de `HtmlSaveOptions`; la mayoría de los problemas provienen de una bandera omitida.

---

## Conclusión

Ahora dispones de un método sólido y listo para producción para **guardar Excel como HTML** manteniendo cada estilo, borde y representación numérica intactos. Al configurar `HtmlSaveOptions` y activar `GridJsOptions.EnableNumberFormat`, has convertido una hoja de cálculo estática en una tabla web‑amigable que funciona sin problemas con Grid.js.

En resumen, este tutorial te muestra cómo **convertir Excel a HTML** y **exportar Excel con formato** usando Aspose.Cells. Siéntete libre de experimentar: prueba diferentes temas, incrusta gráficos o incluso sirve el HTML a través de un endpoint ASP.NET para conversiones bajo demanda.

---

## ¿Qué sigue?

- **Explora otros formatos de exportación**: PDF, PNG o CSV mediante `Workbook.Save`.  
- **Integra con ASP.NET Core**: Devuelve la cadena HTML directamente desde una acción de controlador.  
- **Combina con SheetJS**: Carga el HTML generado de nuevo en un libro JavaScript para edición del lado del cliente.  

Si encuentras algún obstáculo, deja un comentario abajo o consulta la documentación de Aspose.Cells para opciones de configuración más avanzadas. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo exportar Excel a HTML con líneas de cuadrícula usando Aspose.Cells para .NET](/cells/english/net/workbook-operations/export-excel-to-html-grid-lines-aspose-cells-net/)
- [Exportar Excel a HTML preservando estilos de borde usando Aspose.Cells para Java](/cells/english/java/workbook-operations/aspose-cells-java-export-excel-html-border-styles/)
- [Convertir HTML a Excel usando Aspose.Cells .NET: Guía completa](/cells/english/net/workbook-operations/convert-html-to-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}