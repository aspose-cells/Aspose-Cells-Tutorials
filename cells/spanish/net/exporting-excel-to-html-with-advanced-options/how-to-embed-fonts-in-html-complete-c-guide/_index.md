---
category: general
date: 2026-01-14
description: Cómo incrustar fuentes en HTML y forzar el cálculo de fórmulas al convertir
  Excel a HTML. Aprende a establecer el área de impresión y exportar gráficos.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- force formula calculation
- convert excel to html
- how to set print area
language: es
og_description: Cómo incrustar fuentes en HTML, forzar el cálculo de fórmulas y convertir
  Excel a HTML con configuraciones de área de impresión, todo en C#.
og_title: Cómo incrustar fuentes en HTML – Guía completa de C#
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cómo incrustar fuentes en HTML – Guía completa de C#
url: /es/net/exporting-excel-to-html-with-advanced-options/how-to-embed-fonts-in-html-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo incrustar fuentes en HTML – Guía completa en C#

¿Alguna vez te has preguntado **cómo incrustar fuentes en HTML** al exportar un libro de Excel? No eres el único. Muchos desarrolladores se topan con que el HTML generado se ve bien en su máquina pero pierde la tipografía en otro dispositivo. ¿La buena noticia? Con Aspose.Cells para .NET puedes incrustar los archivos de fuente exactos directamente en la salida HTML—no más glifos faltantes.

En este tutorial recorreremos un ejemplo completo que no solo muestra **cómo incrustar fuentes en HTML**, sino que también demuestra **forzar el cálculo de fórmulas**, **convertir Excel a HTML**, y hasta **cómo establecer el área de impresión** antes de exportar un gráfico a un PPTX editable. Al final tendrás un programa C# único y ejecutable que puedes colocar en cualquier proyecto .NET.

---

## Lo que construirás

- Crear un libro nuevo, escribir un par de fórmulas de matriz y **forzar el cálculo de fórmulas** para que los resultados queden grabados en el archivo.
- Guardar el libro como HTML mientras **incrustas fuentes** y sus selectores de variación.
- Cargar un segundo libro que contiene un gráfico, definir un **área de impresión**, y exportar esa hoja a una presentación de PowerPoint editable.
- Todo esto usando solo unas cuantas líneas de código C# limpio y bien comentado.

Sin herramientas externas, sin copiar‑pegar manualmente archivos de fuentes—Aspose.Cells hace el trabajo pesado por ti.

---

## Requisitos previos

| Requisito | Razón |
|-------------|--------|
| .NET 6.0 o superior | Características modernas del lenguaje y mejor rendimiento |
| Aspose.Cells para .NET (paquete NuGet `Aspose.Cells`) | Proporciona `Workbook`, `HtmlSaveOptions`, `ImageOrPrintOptions`, etc. |
| Un par de archivos de fuentes TrueType/OpenType (p. ej., `Arial.ttf`) colocados en la carpeta del proyecto | Necesarios para la incrustación; Aspose los tomará automáticamente si están instalados en el SO host |
| Conocimientos básicos de C# | Para seguir el código y adaptarlo a tus propios escenarios |

---

## Paso 1 – Crear un libro y escribir fórmulas de matriz  

Primero iniciamos una nueva instancia de `Workbook` y colocamos dos fórmulas de matriz en las celdas **A1** y **A3**. Estas fórmulas (`WRAPCOLS` y `WRAPROWS`) generan una pequeña matriz de 2 columnas × 2 filas que más adelante veremos renderizada en la salida HTML.

```csharp
using Aspose.Cells;

namespace FontEmbeddingDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create a new workbook and get the first worksheet
            Workbook workbook = new Workbook();
            Worksheet worksheet = workbook.Worksheets[0];

            // Write WRAPCOLS formula – returns a 2‑column array
            worksheet.Cells[0, 0].Formula = "=WRAPCOLS({1,2,3,4},2)";

            // Write WRAPROWS formula – returns a 2‑row array
            worksheet.Cells[2, 0].Formula = "=WRAPROWS({1;2;3;4},2)";
```

> **Por qué es importante:** Al insertar fórmulas obtienes contenido dinámico que será evaluado cuando forzamos el cálculo más adelante. También muestra que la exportación a HTML puede manejar correctamente los resultados de matrices.

---

## Paso 2 – Forzar el cálculo de fórmulas  

Aspose.Cells evalúa las fórmulas de forma perezosa. Para garantizar que nuestro HTML contenga los valores calculados (en lugar de las fórmulas sin procesar), llamamos a `CalculateFormula()`.

```csharp
            // Step 2: Force calculation so the formulas are evaluated
            worksheet.CalculateFormula();
```

> **Consejo profesional:** Si omites este paso, el HTML mostrará el texto de la fórmula (`=WRAPCOLS...`) en lugar de los números, lo que anula el propósito de una exportación pulida.

---

## Paso 3 – Configurar opciones de guardado HTML para incrustar fuentes  

Ahora llega la estrella del espectáculo: la incrustación de fuentes. Establecer `EmbedFonts` a `true` indica a Aspose que incluya los datos de la fuente como flujos codificados en Base64 dentro del archivo HTML generado. Habilitar `EmbedFontVariationSelectors` asegura que también se conserven los selectores de variación OpenType (usados para tipografía avanzada).

```csharp
            // Step 3: Prepare HTML save options that embed fonts and their variation selectors
            HtmlSaveOptions htmlSaveOptions = new HtmlSaveOptions
            {
                EmbedFonts = true,
                EmbedFontVariationSelectors = true
            };
```

> **Cómo funciona:** Cuando se escribe el HTML, Aspose inyecta un bloque `<style>` con reglas `@font-face` que hacen referencia a los URIs de datos incrustados. Los navegadores renderizarán la misma fuente independientemente de las fuentes instaladas en el cliente.

---

## Paso 4 – Guardar el libro como HTML  

Persistimos el libro en un archivo `.xlsx` primero (por si necesitas la fuente) y luego lo exportamos a HTML usando las opciones que acabamos de definir.

```csharp
            // Step 4: Save the workbook as HTML using the configured options
            string outputDir = @"C:\Demo\Output\"; // adjust to your environment
            workbook.Save(Path.Combine(outputDir, "fontDemo.xlsx"));
            workbook.Save(Path.Combine(outputDir, "fontDemo.html"), htmlSaveOptions);
```

> **Resultado:** Abre `fontDemo.html` en cualquier navegador moderno y verás los valores de la matriz renderizados con la fuente incrustada, incluso si la fuente no está instalada en tu máquina.

---

## Paso 5 – Cargar un libro con un gráfico y establecer el área de impresión  

A continuación demostramos **cómo establecer el área de impresión** antes de exportar una hoja que contiene un gráfico. El área de impresión limita lo que se renderiza, lo cual es útil cuando solo deseas un rango específico en el PPTX final.

```csharp
            // Step 5: Load a workbook that contains a chart and configure PPTX export options
            Workbook chartWorkbook = new Workbook(Path.Combine(outputDir, "chartEditable.xlsx"));

            // Define the print area (e.g., A1:G20) – this is the SECONDARY keyword in action
            chartWorkbook.Worksheets[0].PageSetup.PrintArea = "A1:G20";
```

> **¿Por qué establecer un área de impresión?** Sin ella, Aspose exportaría toda la hoja, potencialmente incluyendo filas/columnas vacías y aumentando innecesariamente el tamaño del PPTX.

---

## Paso 6 – Exportar la hoja a un PPTX editable  

Finalmente exportamos la hoja a un archivo de PowerPoint editable. Al establecer `ExportChartAsEditable = true`, el gráfico se guarda como formas nativas de PowerPoint, permitiendo a los usuarios finales modificarlo directamente en PowerPoint.

```csharp
            // Step 6: Configure PPTX export options
            ImageOrPrintOptions pptSaveOptions = new ImageOrPrintOptions
            {
                SaveFormat = SaveFormat.Pptx,
                ExportChartAsEditable = true
            };

            // Step 7: Save as editable PPTX
            chartWorkbook.Save(Path.Combine(outputDir, "editableChart.pptx"), pptSaveOptions);
        }
    }
}
```

> **Qué obtienes:** `editableChart.pptx` contiene el gráfico de `chartEditable.xlsx` como objetos editables de PowerPoint, limitados al rango `A1:G20`.

---

## Resumen de la salida esperada  

| Archivo | Descripción |
|------|-------------|
| `fontDemo.xlsx` | Libro original con fórmulas de matriz calculadas. |
| `fontDemo.html` | Archivo HTML que **incrusta fuentes**, muestra los resultados de la matriz y funciona sin conexión. |
| `editableChart.pptx` | Presentación de PowerPoint con un gráfico editable, respetando el **área de impresión** que estableciste. |

Abre `fontDemo.html` en Chrome o Edge; notarás que el texto usa la fuente exacta que incrustaste (p. ej., Arial) aunque tu sistema no la tenga. El gráfico en `editableChart.pptx` puede abrirse con doble clic y editarse como cualquier gráfico nativo de PowerPoint.

---

## Preguntas frecuentes y casos límite  

### ¿Qué pasa si mi fuente no está instalada en el servidor?  
Aspose.Cells solo incrustará las fuentes que estén *disponibles* en tiempo de ejecución. Si falta un archivo de fuente concreto, el HTML recurrirá a la fuente predeterminada del navegador. Para garantizar la incrustación, copia los archivos `.ttf`/`.otf` necesarios a la carpeta de tu aplicación y haz referencia a ellos mediante `FontInfo` (escenario avanzado).

### ¿Puedo incrustar solo un subconjunto de caracteres para reducir el tamaño del archivo?  
Sí. Usa `HtmlSaveOptions.FontEmbeddingMode = FontEmbeddingMode.Subset`. Esto indica a Aspose que incluya solo los glifos realmente usados en el libro, reduciendo drásticamente la carga útil del HTML.

### ¿El **forzar cálculo de fórmulas** también funciona con funciones volátiles como `NOW()`?  
Absolutamente. `CalculateFormula()` evalúa todas las fórmulas, incluidas las volátiles, en el momento en que lo llamas. Si necesitas que el cálculo refleje una fecha/hora específica, configura `CalculationOptions` del libro antes de llamar.

### ¿Qué ocurre con libros grandes—la incrustación de fuentes inflará el HTML?  
Incrustar fuentes añade aproximadamente 100‑200 KB por fuente (dependiendo del tamaño). Para informes masivos, considera enlazar a fuentes alojadas en la web en lugar de incrustarlas, o usa el modo de subconjunto mencionado anteriormente.

---

## Consejos profesionales y buenas prácticas  

- **Guardados por lotes:** Si generas decenas de archivos HTML, reutiliza una única instancia de `HtmlSaveOptions` para evitar asignaciones innecesarias.  
- **Cachear áreas de impresión:** Al exportar muchas hojas, guarda el área de impresión deseada en un archivo de configuración para mantener tu código DRY.  
- **Validar la salida:** Después de guardar el HTML, ejecuta una rápida comprobación con un navegador sin cabeza (p. ej., Puppeteer) para asegurarte de que las fuentes se renderizan correctamente antes de entregarlas a los usuarios.  
- **Bloqueo de versión:** El código anterior está dirigido a Aspose.Cells 23.12+. Versiones más recientes pueden introducir opciones adicionales como `FontEmbeddingMode`. Revisa siempre las notas de la versión.

---

## Conclusión  

Hemos cubierto **cómo incrustar fuentes en HTML** usando Aspose.Cells, mostrado la importancia de **forzar el cálculo de fórmulas**, demostrado un flujo limpio de **convertir Excel a HTML**, y explicado **cómo establecer el área de impresión** antes de exportar un gráfico a un PPTX editable. El ejemplo completo y ejecutable vive en un solo archivo `Program.cs`, para que puedas copiar‑pegar, ajustar rutas y ejecutarlo hoy mismo.

¿Listo para el siguiente paso? Prueba cambiar la fuente incrustada por una tipografía personalizada de tu marca, o experimenta con el modo de incrustación `Subset` para mantener tu HTML ligero. El mismo patrón funciona para PDFs, imágenes e incluso exportaciones CSV—solo cambia la clase `SaveOptions`.

¿Tienes más preguntas sobre incrustar fuentes, manejo de fórmulas o trucos con áreas de impresión? Deja un comentario abajo o contáctame en los foros de la comunidad Aspose. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}