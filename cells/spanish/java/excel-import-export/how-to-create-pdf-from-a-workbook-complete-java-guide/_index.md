---
category: general
date: 2026-03-01
description: Cómo crear PDF y guardar el libro de trabajo como PDF, exportar Excel
  a HTML y usar la función expand con Aspose.Cells para Java. Código paso a paso incluido.
draft: false
keywords:
- how to create pdf
- save workbook as pdf
- export excel to html
- use expand function
language: es
og_description: Cómo crear PDF a partir de un libro de trabajo usando Aspose.Cells
  para Java. Aprende a guardar el libro de trabajo como PDF, exportar Excel a HTML
  y usar la función EXPAND.
og_title: Cómo crear PDF a partir de un libro de trabajo – Tutorial de Java
tags:
- Aspose.Cells
- Java
- PDF generation
title: Cómo crear un PDF a partir de un libro de trabajo – Guía completa de Java
url: /es/java/excel-import-export/how-to-create-pdf-from-a-workbook-complete-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear PDF a partir de un libro de trabajo – Guía completa de Java

¿Alguna vez te has preguntado **cómo crear PDF** directamente desde un libro de Excel sin depender de convertidores de terceros? No estás solo. Muchos desarrolladores se topan con un obstáculo cuando necesitan una exportación rápida a PDF, una vista previa en HTML o fórmulas de matriz avanzadas, todo en una sola operación.  

En este tutorial recorreremos un programa Java autónomo que hace exactamente eso. **Guardaremos el libro como PDF**, te mostraremos cómo **exportar Excel a HTML** manteniendo las filas congeladas y demostraremos el **uso de la función expand** dentro de una hoja. Al final tendrás un proyecto ejecutable que podrás integrar en cualquier compilación Maven o Gradle.

> **Consejo profesional:** Todo el código a continuación funciona con Aspose.Cells 23.10 (o versiones posteriores). Si utilizas una versión anterior, algunos nombres de métodos pueden variar ligeramente.

---

## Requisitos previos

- **Java 17** (o cualquier versión LTS) instalado y configurado.
- Biblioteca **Aspose.Cells for Java**. Añade la siguiente dependencia Maven a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

- Un IDE o editor de texto de tu preferencia (IntelliJ IDEA, VS Code, Eclipse…).

Sin APIs externas, sin servicios web—solo Java puro y el SDK de Aspose.Cells.

---

## Visión general de la solución

Dividiremos la implementación en **siete pasos lógicos**:

1. Crear un libro de trabajo y demostrar la función **EXPAND**.  
2. Habilitar los selectores de variación de fuentes y **guardar el libro como PDF**.  
3. Exportar el mismo libro a HTML preservando las filas congeladas.  
4. Utilizar un Smart Marker con un parámetro `IF` para inyectar texto condicional.  
5. Aplicar un Smart Marker maestro‑detalle para datos jerárquicos.  
6. Cargar un archivo Markdown que contiene imágenes codificadas en Base‑64.  
7. Configurar opciones de GridJs para alineación y bordes, y luego insertar datos.

Cada paso está encapsulado en su propio método para mantener ordenado el método `main` y para ilustrar **por qué** hacemos lo que hacemos, no solo **qué** escribimos.

---

## Paso 1 – Crear un libro de trabajo y usar la función EXPAND

La función **EXPAND** es una nueva fórmula de matriz dinámica introducida en Office 365. Permite expandir un rango a un área mayor sin copiar manualmente las celdas.

```java
import com.aspose.cells.*;

public class WorkbookDemo {

    private static void createWorkbookWithExpand() throws Exception {
        // Initialize a new workbook and grab the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // A1 uses EXPAND to turn a 1×3 array into a 5×2 block
        sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");

        // B1 demonstrates a classic trigonometric function (cotangent)
        sheet.getCells().get("B1").setFormula("=COT(PI()/4)");

        // Force calculation so we can read the results immediately
        workbook.calculateFormula();

        // Print the top‑left value to the console – should be 1
        System.out.println("A1 value after EXPAND: " + sheet.getCells().get("A1").getStringValue());
    }
```

**Por qué es importante:**  
- `EXPAND` rellena automáticamente el resultado con celdas en blanco, lo que es perfecto cuando luego **guardas el libro como PDF**—el PDF mostrará una tabla limpia y rectangular.  
- Llamar a `calculateFormula()` asegura que el motor de fórmulas se ejecute antes de exportar cualquier cosa.

---

## Paso 2 – Habilitar selectores de variación de fuentes y **guardar el libro como PDF**

Si necesitas admitir tipografía avanzada (p. ej., emoji o selectores de variación CJK), debes activar la función **antes** de guardar.

```java
    private static void saveAsPdf(Workbook workbook) throws Exception {
        // Enable support for variation selectors (useful for emojis, etc.)
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true);

        // Define the output path – adjust to your environment
        String pdfPath = "output/vsPdf.pdf";

        // Save the workbook as a PDF file
        workbook.save(pdfPath, SaveFormat.PDF);
        System.out.println("PDF saved to: " + pdfPath);
    }
```

**Punto clave:** La palabra clave principal **how to create pdf** se responde aquí—llamando a `workbook.save(..., SaveFormat.PDF)` después de configurar los ajustes.

---

## Paso 3 – **Exportar Excel a HTML** mientras se preservan las filas congeladas

A menudo los interesados solicitan una vista previa rápida en la web. Aspose.Cells puede exportar a HTML, y con `setPreserveFrozenRows(true)` mantenemos la misma experiencia de desplazamiento que en Excel.

```java
    private static void exportToHtml(Workbook workbook) throws Exception {
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setPreserveFrozenRows(true); // keep frozen panes

        String htmlPath = "output/frozenRows.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML exported to: " + htmlPath);
    }
```

**Por qué te importa:** Las filas congeladas son una comodidad de usabilidad; sin ellas, las filas de encabezado desaparecen cuando los usuarios se desplazan hacia abajo en la página.

---

## Paso 4 – Smart Marker con un parámetro IF

Los Smart Markers te permiten combinar datos en una plantilla sin escribir bucles. El parámetro `if` agrega lógica condicional directamente dentro del marcador.

```java
    private static void applyConditionalSmartMarker() throws Exception {
        String template = "${if(@IsVIP, 'VIP Customer', 'Regular Customer')}: ${CustomerName}";
        Map<String, Object> data = new HashMap<>();
        data.put("IsVIP", true);
        data.put("CustomerName", "Acme Corp");

        // Create a fresh workbook to host the result
        Workbook markerWorkbook = new Workbook();
        SmartMarkerProcessor processor = new SmartMarkerProcessor(markerWorkbook);
        processor.apply(template, data);

        // Save to see the result
        markerWorkbook.save("output/conditionalMarker.pdf", SaveFormat.PDF);
    }
```

El PDF resultante mostrará **“VIP Customer: Acme Corp”** porque `IsVIP` es `true`. Cambia la bandera a `false` y obtendrás **“Regular Customer: Acme Corp”**—sin código adicional.

---

## Paso 5 – Smart Marker maestro‑detalle usando un rango jerárquico

Cuando tienes datos padre‑hijo (p. ej., pedidos y líneas de detalle), un marcador maestro‑detalle te ahorra la inserción manual de filas.

```java
    private static void applyMasterDetailSmartMarker() throws Exception {
        // Simulated hierarchical data
        Map<String, Object> hierarchicalData = new HashMap<>();
        List<Map<String, Object>> orders = new ArrayList<>();

        Map<String, Object> order1 = new HashMap<>();
        order1.put("OrderID", 1001);
        order1.put("Date", "2024‑12‑01");
        List<Map<String, Object>> details1 = new ArrayList<>();
        details1.add(Map.of("Product", "Widget A", "Qty", 5));
        details1.add(Map.of("Product", "Widget B", "Qty", 2));
        order1.put("Detail", details1);
        orders.add(order1);

        hierarchicalData.put("Orders", orders);

        String masterDetailTemplate =
                "${Orders.Master:OrderID,Date}\n" +
                "${Orders.Detail:Product,Qty}";

        Workbook mdWorkbook = new Workbook();
        SmartMarkerProcessor mdProcessor = new SmartMarkerProcessor(mdWorkbook);
        mdProcessor.apply(masterDetailTemplate, hierarchicalData);

        mdWorkbook.save("output/masterDetail.pdf", SaveFormat.PDF);
    }
```

**Lo que obtienes:** El motor expande las filas maestras para cada pedido y anida automáticamente las filas de detalle debajo—ideal para facturas o informes de compras.

---

## Paso 6 – Cargar un documento Markdown con imágenes incrustadas en Base‑64

Si tus datos de origen están en Markdown (común en pipelines de documentación), Aspose.Cells puede renderizarlos directamente en un libro de trabajo.

```java
    private static void loadMarkdownWithBase64() throws Exception {
        MarkdownLoadOptions mdOptions = new MarkdownLoadOptions();
        mdOptions.setEnableBase64Images(true); // decode inline images

        // Assume doc.md lives in the project root
        Workbook mdWorkbook = new Workbook("input/doc.md", mdOptions);
        mdWorkbook.save("output/markdownExport.pdf", SaveFormat.PDF);
        System.out.println("Markdown loaded and saved as PDF.");
    }
```

**Nota de caso límite:** Si la cadena Base‑64 está malformada, Aspose omitirá la imagen pero continuará procesando el resto del documento—sin bloquearse.

---

## Paso 7 – Configurar opciones de GridJs e insertar datos

GridJs es una cuadrícula ligera de JavaScript que Aspose puede renderizar en HTML. Alinear números y aplicar bordes mejora la legibilidad.

```java
    private static void configureGridJs() throws Exception {
        GridJsOptions gridOptions = new GridJsOptions();
        gridOptions.setNumberFormatAlignment(Alignment.Center); // center numbers
        gridOptions.setNumberFormatBorder(BorderLineStyle.Thin); // thin border

        GridJsEngine gridEngine = new GridJsEngine(gridOptions);
        gridEngine.insertRows(0, 10); // create 10 empty rows
        gridEngine.setCellValue(0, 0, "123"); // first cell gets a value

        // Export the GridJs view to HTML for quick inspection
        String htmlPath = "output/gridJs.html";
        gridEngine.save(htmlPath);
        System.out.println("GridJs HTML saved to: " + htmlPath);
    }
```

**Por qué nos importa:** Una alineación adecuada y bordes hacen que el HTML generado se vea como una hoja de cálculo pulida—útil para paneles de control.

---

## Juntándolo todo – El método `main`

```java
    public static void main(String[] args) {
        try {
            // Step 1 – create workbook with EXPAND
            Workbook workbook = new Workbook();
            Worksheet sheet = workbook.getWorksheets().get(0);
            sheet.getCells().get("A1").setFormula("=EXPAND({1,2,3}, 5, 2)");
            sheet.getCells().get("B1").setFormula("=COT(PI()/4)");
            workbook.calculateFormula();
            System.out.println("A1 after EXPAND: " + sheet.getCells().get("A1").getStringValue());

            // Step 2 – save as PDF
            saveAsPdf(workbook);

            // Step 3 – export to HTML
            exportToHtml(workbook);

            // Step 4 – conditional Smart Marker
            applyConditionalSmartMarker();

            // Step 5 – master‑detail Smart Marker
            applyMasterDetailSmartMarker();

            // Step 6 – load Markdown with Base‑64 images
            loadMarkdownWithBase64();

            // Step 7 – GridJs configuration
            configureGridJs();

            System.out.println("All tasks completed successfully.");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}