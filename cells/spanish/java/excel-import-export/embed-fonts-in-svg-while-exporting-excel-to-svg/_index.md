---
category: general
date: 2026-08-14
description: Incrustar fuentes en SVG al exportar Excel a SVG usando Aspose.Cells.
  Aprende cómo establecer el área de impresión, configurar las opciones de impresión
  y usar la función WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: es
lastmod: 2026-08-14
og_description: Incruste fuentes en SVG al exportar Excel a SVG con Aspose.Cells.
  Esta guía le muestra cómo establecer el área de impresión, configurar las opciones
  de impresión y aplicar la función WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Incrustar fuentes en SVG al exportar Excel a SVG – paso a paso
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Incrustar fuentes en SVG al exportar Excel a SVG
url: /es/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Incrustar fuentes en SVG al exportar Excel a SVG

Si necesita **incrustar fuentes en SVG al exportar Excel a SVG**, este tutorial le muestra exactamente cómo hacerlo con Aspose.Cells for Java. También cubriremos cómo **establecer el área de impresión**, **establecer opciones de impresión** y **usar la función WRAPCOLS** para formatear datos sin perder el diseño.

Recorrerá un ejemplo completo y ejecutable que carga un libro de trabajo existente, aplica la fórmula `WRAPCOLS`, configura opciones de imagen específicas para SVG, define la región de impresión y, finalmente, guarda el archivo como SVG con fuentes incrustadas. No se requiere documentación externa; simplemente copie el código, ejecútelo y examine el SVG resultante.

## Incrustar fuentes en SVG – configurando ImageOrPrintOptions

Incrustar fuentes garantiza que el SVG se renderice exactamente como aparece en Excel, incluso en máquinas que no tienen instaladas las tipografías originales.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Por qué es importante*: Cuando `setEmbedFonts(true)` está habilitado, Aspose.Cells escribe los datos de la fuente directamente en la sección `<defs>` del SVG. El resultado es un archivo autónomo que se ve idéntico en todos los navegadores y plataformas.

## Exportar Excel a SVG – flujo de trabajo completo

Los siguientes pasos ilustran el proceso de extremo a extremo, desde cargar el libro de trabajo hasta guardar el archivo SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Salida esperada**: `output.svg` aparece en `YOUR_DIRECTORY`. Al abrirlo en un navegador se muestra la hoja de cálculo con todas las fuentes incrustadas, los datos envueltos en tres columnas (gracias a `WRAPCOLS`) y solo las celdas dentro de `A1:H30` renderizadas.

## Establecer el área de impresión para la hoja de cálculo

Definir un área de impresión limita el SVG exportado a un rango específico, lo que reduce el tamaño del archivo y enfoca al visor en los datos relevantes.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Consejo*: El rango sigue la notación A1 de Excel. Si necesita un rango dinámico, puede calcularlo programáticamente con `ws.getCells().getMaxDisplayRange()`.

## Establecer opciones de impresión para la salida SVG

Las opciones de impresión controlan cómo Aspose.Cells traduce la hoja de cálculo a una imagen. Además de incrustar fuentes, puede ajustar la resolución, el escalado y el diseño de página.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Por qué debe establecer opciones de impresión*: Sin opciones explícitas, Aspose.Cells usa valores predeterminados que pueden omitir la incrustación de fuentes o aplicar un factor de escalado no deseado, lo que genera SVG borrosos o con estilo incorrecto.

## Usar la función WRAPCOLS para envolver datos de columna

`WRAPCOLS` es una fórmula de Excel que distribuye un rango vertical en un número especificado de columnas. Es útil cuando desea mostrar una lista larga en una cuadrícula compacta.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Al guardar el libro de trabajo, Aspose.Cells evalúa la fórmula, produciendo un diseño de tres columnas dentro del área de impresión definida. Esta técnica funciona para cualquier rango de tamaño; simplemente ajuste el segundo argumento al número de columnas deseado.

## Ejemplo completo ejecutable

A continuación se muestra el programa Java completo que puede pegar en cualquier IDE. Asegúrese de tener la biblioteca Aspose.Cells for Java en su classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Pasos de verificación**

1. Ejecutar el programa.  
2. Abrir `output.svg` en un navegador web.  
3. Confirmar que el texto usa la misma tipografía que el archivo Excel original (las fuentes están incrustadas).  
4. Verificar que solo aparecen las celdas dentro de `A1:H30` y que los datos de `A2:A10` se muestran en tres columnas.

## Errores comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Faltan fuentes en el SVG | `setEmbedFonts(false)` o el archivo de fuente no es accesible | Asegúrese de `setEmbedFonts(true)` y de que la fuente esté instalada en la máquina que ejecuta el código |
| WRAPCOLS no se evalúa | Motor de cálculo deshabilitado | Llame a `workbook.calculateFormula()` antes de exportar, o permita que Aspose.Cells evalúe durante el guardado |
| El SVG exportado está en blanco | El área de impresión no incluye datos | Verifique nuevamente el rango pasado a `setPrintArea` |
| El archivo SVG es enorme | No se aplicó escalado, alta resolución de imagen | Ajuste `imgOptions.setResolution(96)` o similar para controlar DPI |

## Consejo profesional: reutilizar ImageOrPrintOptions para varias hojas de cálculo

Si su libro de trabajo contiene varias hojas que necesitan configuraciones SVG idénticas, cree una única instancia de `ImageOrPrintOptions` y asígnela al `PageSetup` de cada hoja. Esto reduce el consumo de memoria y garantiza una incrustación de fuentes coherente en todos los archivos exportados.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Próximos pasos

* **Exportar a otros formatos vectoriales** – Cambie `ImageFormat.SVG` a `ImageFormat.PDF` para PDFs de alta calidad.  
* **Procesamiento por lotes** – Recorra una carpeta de archivos `.xlsx` y genere SVGs automáticamente.  
* **Manejo de fuentes personalizadas** – Use `FontSettings` para cargar fuentes desde un directorio específico cuando las fuentes del sistema sean insuficientes.  

Al dominar **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options** y **use WRAPCOLS function**, puede automatizar la generación de SVG de alta fidelidad para informes, paneles y visualizaciones web directamente desde datos de Excel. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar características adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Cómo establecer un área de impresión en Excel usando Aspose.Cells para .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Establecer área de impresión Excel Aspose Cells .NET](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Establecer área de impresión Excel Aspose Cells .NET](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}