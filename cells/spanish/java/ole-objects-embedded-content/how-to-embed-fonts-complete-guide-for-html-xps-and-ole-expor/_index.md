---
category: general
date: 2026-03-01
description: Aprende cómo incrustar fuentes en HTML y otros formatos. Tutorial paso
  a paso que cubre incrustar fuentes en HTML, convertir Excel a HTML, cómo exportar
  OLE y convertir Excel a XPS.
draft: false
keywords:
- how to embed fonts
- embed fonts in html
- convert excel to html
- how to export ole
- convert excel to xps
language: es
og_description: Cómo incrustar fuentes en exportaciones HTML, XPS y OLE. Aprende todo
  el flujo de trabajo, ve código Java ejecutable y domina la incrustación de fuentes
  en HTML para conversiones a Excel.
og_title: Cómo incrustar fuentes – Tutorial completo de Java
tags:
- Aspose.Cells
- Java
- Document Export
title: Cómo incrustar fuentes – Guía completa para HTML, XPS y exportación OLE
url: /es/java/ole-objects-embedded-content/how-to-embed-fonts-complete-guide-for-html-xps-and-ole-expor/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo incrustar fuentes – Guía completa para HTML, XPS y exportación OLE

¿Alguna vez te has preguntado **cómo incrustar fuentes** al convertir un libro de Excel en una página web o en un documento imprimible? No estás solo. Muchos desarrolladores se topan con un muro cuando la salida se ve bien en su máquina pero se rompe en otra porque faltan las fuentes requeridas.  

En este tutorial recorreremos un escenario del mundo real usando Aspose.Cells for Java: incrustaremos fuentes en HTML, preservaremos los selectores de variación de emoji al convertir a XPS, e incluso mantendremos un objeto OLE editable al exportar a PPTX. Al final tendrás una solución sólida, lista para copiar y pegar, que responde a “cómo incrustar fuentes” y también aborda **embed fonts in html**, **convert excel to html**, **how to export ole**, y **convert excel to xps**.

## Prerrequisitos

- Java 17 (o cualquier JDK reciente)  
- Aspose.Cells for Java 25.x o posterior  
- Un IDE de desarrollo (IntelliJ IDEA, Eclipse o VS Code)  
- Familiaridad básica con estructuras de datos de Excel  

No se requieren servicios externos; todo se ejecuta localmente.

## Visión general de la solución

1. **Crear un libro** y usar la función `WRAPCOLS` para transformar un rango vertical en un diseño de tres columnas.  
2. **Guardar el libro como XPS** activando los selectores de variación de fuentes para que los emoji permanezcan intactos.  
3. **Exportar a HTML** con fuentes incrustadas, garantizando que la página se vea igual en cualquier lugar.  
4. **Exportar un libro que contiene un objeto OLE a PPTX**, preservando su editabilidad.  
5. **Aplicar una plantilla Smart Marker** que demuestre la vinculación maestro‑detalle de datos.  

Cada paso está aislado en su propia sección H2, lo que facilita la lectura tanto para motores de búsqueda como para asistentes de IA.

![Ilustración de cómo incrustar fuentes](image.png "cómo incrustar fuentes")

*Texto alternativo de la imagen: diagrama de cómo incrustar fuentes que muestra el flujo de trabajo de Excel a HTML, XPS y PPTX.*

---

## Paso 1 – Crear un libro y usar WRAPCOLS (Por qué esto importa para embed fonts in html)

Antes de poder hablar de incrustar fuentes, necesitamos un libro que realmente contenga datos. La función `WRAPCOLS` es una manera práctica de dividir una sola columna en varias columnas, lo que a menudo hace que el HTML final sea más legible.

```java
import com.aspose.cells.*;

public class EmbedFontsDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Populate A2:A10 with sample data
        for (int i = 2; i <= 10; i++) {
            sheet.getCells().get("A" + i).putValue("Item " + (i - 1));
        }

        // Use WRAPCOLS to create a 3‑column block starting at A1
        Cell resultCell = sheet.getCells().get("A1");
        resultCell.setFormula("=WRAPCOLS(A2:A10,3)");
        workbook.calculateFormula();

        System.out.println("WRAPCOLS result: " + resultCell.getStringValue());
        // -----------------------------------------------------------------
        // The rest of the steps are demonstrated after this point.
        // -----------------------------------------------------------------
```

**¿Por qué este paso?**  
La llamada a `WRAPCOLS` genera un rango de varias columnas que luego aparece en HTML como una tabla. Cuando más adelante **embed fonts in html**, el estilo de la tabla dependerá de las fuentes que incrustemos, asegurando una renderización consistente en todos los navegadores.

---

## Paso 2 – Guardar el libro como XPS preservando los emoji (convert excel to xps)

Si necesitas un formato listo para imprimir, XPS es una opción sólida. Sin embargo, los documentos modernos a menudo contienen emoji o símbolos que usan selectores de variación. Activar `EnableFontVariationSelectors` asegura que esos caracteres sobrevivan a la conversión.

```java
        // --------------------------------------------------------------
        // Step 2: Save as XPS with font variation selectors enabled
        // --------------------------------------------------------------
        WorkbookSettings settings = workbook.getSettings();
        settings.setEnableFontVariationSelectors(true); // crucial for emoji

        String xpsPath = "output/withVariations.xps";
        workbook.save(xpsPath, SaveFormat.XPS);
        System.out.println("Workbook saved as XPS at: " + xpsPath);
```

**Qué obtienes:**  
Un archivo XPS que muestra cualquier emoji incrustado exactamente como en el libro de origen. Esto satisface el requisito de **convert excel to xps** y demuestra que el manejo de fuentes no se limita a HTML.

---

## Paso 3 – Exportar a HTML con fuentes incrustadas (how to embed fonts & embed fonts in html)

Ahora llegamos al núcleo del tutorial: **how to embed fonts** al convertir Excel a HTML. Aspose.Cells nos permite incrustar las fuentes directamente en el archivo HTML generado, eliminando la necesidad de archivos de fuentes externos.

```java
        // --------------------------------------------------------------
        // Step 3: Export to HTML with embedded fonts
        // --------------------------------------------------------------
        HtmlSaveOptions htmlOptions = new HtmlSaveOptions();
        htmlOptions.setEmbedFonts(true); // this is the key line for embed fonts in html
        htmlOptions.setExportImagesAsBase64(true); // optional, keeps all assets in one file

        String htmlPath = "output/embeddedFonts.html";
        workbook.save(htmlPath, htmlOptions);
        System.out.println("HTML with embedded fonts saved at: " + htmlPath);
```

**Cómo funciona:**  
`setEmbedFonts(true)` indica al renderizador que lea los archivos de fuentes usados en el libro y los incruste como reglas `@font-face` codificadas en Base64 dentro de la etiqueta `<style>`. El HTML resultante es autocontenido, por lo que puedes colocarlo en cualquier servidor y las fuentes se renderizarán correctamente—exactamente lo que los desarrolladores buscan cuando buscan **how to embed fonts**.

**Fragmento de salida esperado (dentro de `embeddedFonts.html`):**

```html
<style>
@font-face{font-family:"Arial";src:url(data:font/ttf;base64,AAEAAA... ) format('truetype');}
</style>
<table>
  <tr><td>Item 1</td><td>Item 4</td><td>Item 7</td></tr>
  <tr><td>Item 2</td><td>Item 5</td><td>Item 8</td></tr>
  <tr><td>Item 3</td><td>Item 6</td><td>Item 9</td></tr>
</table>
```

Observa la regla `@font-face`; esta es la respuesta concreta a **embed fonts in html**.

---

## Paso 4 – Exportar un libro que contiene un objeto OLE a PPTX (how to export ole)

Muchos informes empresariales incrustan documentos Word, PDFs u otras hojas de Excel como objetos OLE. Cuando exportas dicho libro a PowerPoint, a menudo pierdes la capacidad de editar ese objeto. Aspose.Cells preserva la editabilidad de forma predeterminada.

```java
        // --------------------------------------------------------------
        // Step 4: Export a workbook with an OLE object to PPTX
        // --------------------------------------------------------------
        // Load a workbook that already contains an OLE object.
        Workbook oleWorkbook = new Workbook("input/oleObject.xlsx");

        String pptxPath = "output/oleEditable.pptx";
        oleWorkbook.save(pptxPath, SaveFormat.PPTX);
        System.out.println("PPTX with editable OLE object saved at: " + pptxPath);
```

**Por qué importa:**  
Si buscas **how to export ole**, este fragmento muestra la llamada exacta a la API. La diapositiva de PowerPoint resultante contiene el objeto OLE como un componente activo, de doble clic para editar—sin procesamiento posterior adicional.

---

## Paso 5 – Aplicar una plantilla Smart Marker (master‑detail) y finalizar la demo

Los Smart Markers te permiten vincular una fuente de datos (Map, JSON, DataTable) directamente a una plantilla de Excel. Aquí tienes un ejemplo mínimo que imprime filas maestro‑detalle.

```java
        // --------------------------------------------------------------
        // Step 5: Apply Smart Marker template (master‑detail)
        // --------------------------------------------------------------
        String smartMarkerTemplate = "${Orders.Master:OrderID,Customer}\n${Orders.Detail:Product,Qty,Price}";
        // Simulated data source
        java.util.Map<String, Object> dataSource = new java.util.HashMap<>();
        java.util.List<java.util.Map<String, Object>> master = new java.util.ArrayList<>();
        java.util.Map<String, Object> masterRow = new java.util.HashMap<>();
        masterRow.put("OrderID", 1001);
        masterRow.put("Customer", "Acme Corp");
        master.add(masterRow);
        dataSource.put("Orders.Master", master);

        java.util.List<java.util.Map<String, Object>> detail = new java.util.ArrayList<>();
        java.util.Map<String, Object> detailRow = new java.util.HashMap<>();
        detailRow.put("Product", "Widget");
        detailRow.put("Qty", 5);
        detailRow.put("Price", 9.99);
        detail.add(detailRow);
        dataSource.put("Orders.Detail", detail);

        SmartMarkerProcessor processor = new SmartMarkerProcessor(new Workbook());
        processor.apply(smartMarkerTemplate, dataSource);
        processor.getWorkbook().save("output/smartMarkerResult.xlsx");
        System.out.println("Smart Marker workbook saved.");
    }
}
```

**Lo que ves:**  
Un nuevo libro (`smartMarkerResult.xlsx`) donde los marcadores de posición de la plantilla se sustituyen con los datos. Este paso no trata directamente de fuentes, pero completa el tutorial mostrando un flujo típico de generación de informes que a menudo precede a una exportación **embed fonts in html**.

---

## Problemas comunes y consejos profesionales (Asegurando una incrustación de fuentes exitosa)

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| Faltan fuentes en el archivo HTML | El libro de trabajo usa una fuente del sistema que no está instalada en el servidor. | Use `Workbook.getSettings().setDefaultFont("Arial")` antes de cargar los datos, o incruste manualmente los archivos de fuentes requeridos. |
| El HTML de salida es muy grande | Incrustar muchas fuentes grandes aumenta el tamaño del archivo. | Limite la incrustación solo a las fuentes que realmente usa: `htmlOptions.setFontEmbeddingMode(HtmlFontEmbeddingMode.EmbedSubset)`. |
| Los emojis desaparecen después de la conversión a XPS | Los selectores de variación se eliminan por defecto. | Active `settings.setEnableFontVariationSelectors(true)` como se muestra en el Paso 2. |
| El objeto OLE se convierte en una imagen estática en PPTX | El libro de trabajo fuente se guardó con `setSuppressOLEObjects(true)`. | Asegúrese de **no** suprimir objetos OLE al guardar en PPTX. |

---

## Verificando los resultados

1. Abra `embeddedFonts.html` en Chrome/Firefox. La tabla debería mostrarse usando la fuente incrustada (p.ej., Arial) incluso si esa fuente no está instalada en la máquina.  
2. Abra `withVariations.xps` en el Visor XPS de Windows. Emojis como 👍 deberían renderizarse correctamente.  
3. Abra `oleEditable.pptx` en PowerPoint. Haga doble clic en la forma OLE;

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}