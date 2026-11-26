---
category: general
date: 2026-11-25
description: Ejemplo de código Java para crear un libro de Excel usando marcadores
  inteligentes de Aspose.Cells para vincular matrices JSON como valores únicos.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- Aspose.Cells smart marker
- Java JSON to Excel
- setSmartMarkerData
- Excel export Java
language: es
lastmod: 2026-11-25
og_description: Crea un libro de Excel en Java con Aspose.Cells para exportar fácilmente
  matrices JSON como celdas individuales. Sigue la guía paso a paso.
og_image_alt: Screenshot of an Excel workbook created in Java using Aspose.Cells smart
  markers
og_title: Crear libro de Excel en Java – Guía de marcadores inteligentes de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-11-25'
  description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  headline: How to create Excel workbook Java with Aspose.Cells markers
  type: TechArticle
- description: Create Excel workbook Java code example using Aspose.Cells smart markers
    to bind JSON arrays as single values.
  name: How to create Excel workbook Java with Aspose.Cells markers
  steps:
  - name: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
    text: '**Creates a fresh workbook** – `new Workbook()` gives you an in‑memory
      Excel file with a default sheet.'
  - name: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
    text: '**Places a smart marker in cell A1** – `{{jsonArray:ArrayAsSingle}}` tells
      Aspose.Cells to replace the marker with the *entire* array, joined by commas.'
  - name: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
    text: '**Builds a `Map` data source** – The key `"jsonArray"` matches the marker
      name; the value is a `String[]`.'
  - name: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
    text: '**Calls `setSmartMarkerData`** – This binds the map to the marker and performs
      the replacement.'
  - name: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
    text: '**Saves the file** – `workbook.save(...)` writes `JsonSingleValue.xlsx`
      to disk.'
  - name: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
    text: Open `JsonSingleValue.xlsx` in Microsoft Excel, LibreOffice Calc, or Google
      Sheets.
  - name: Confirm that cell **A1** reads `One, Two, Three`.
    text: Confirm that cell **A1** reads `One, Two, Three`.
  - name: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
    text: Check that no extra rows or columns were added – the smart marker performed
      an in‑place replacement.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo crear un libro de trabajo de Excel en Java con marcadores de Aspose.Cells
url: /es/java/templates-reporting/how-to-create-excel-workbook-java-with-aspose-cells-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un libro de Excel Java con marcadores de Aspose.Cells

Si necesitas **crear Excel workbook Java** código que escriba una matriz JSON en una sola celda, este tutorial te muestra exactamente cómo. Usando los marcadores inteligentes de Aspose.Cells puedes tratar una matriz completa como un solo valor, evitando bucles manuales y escrituras celda por celda.

Aprenderás a configurar un libro de trabajo, definir un marcador inteligente, enlazar una fuente de datos `Map` que contiene una matriz al estilo JSON y, finalmente, guardar el archivo. El ejemplo funciona con Java 17+, Maven y la biblioteca de prueba gratuita de Aspose.Cells for Java.

---

![Screenshot of an Excel workbook created in Java using Aspose.Cells smart markers](excel-workbook-java.png){: .center-image alt="Captura de pantalla de un libro de Excel creado en Java usando marcadores inteligentes de Aspose.Cells"}

## Requisitos previos

| Requisito | Por qué es importante |
|-------------|----------------|
| Java 17 o posterior | Las últimas características del lenguaje y actualizaciones de seguridad |
| Maven 3.6+ | Simplifica la gestión de dependencias |
| Aspose.Cells for Java (v23.12 o más reciente) | Proporciona las APIs `Workbook`, `Worksheet` y smart‑marker usadas en el ejemplo |
| Conocimientos básicos de colecciones de Java | Crearás un `Map<String, Object>` que actúa como la fuente de datos |

Agrega la dependencia de Aspose.Cells a tu `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Crear Excel workbook Java – ejemplo completo

El siguiente programa es una solución **completa, ejecutable**. Cópialo en un archivo llamado `ExcelSmartMarkerDemo.java`, compílalo y ejecútalo.

```java
package com.example.excel;

import com.aspose.cells.*;
import java.util.HashMap;
import java.util.Map;

/**
 * Demonstrates how to create Excel workbook Java using Aspose.Cells smart markers.
 * The smart marker "{{jsonArray:ArrayAsSingle}}" treats the whole array as a single cell value.
 */
public class ExcelSmartMarkerDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();                       // empty workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // first (default) sheet

        // Step 2: Define a smart marker that treats a JSON array as a single value
        // The "ArrayAsSingle" option concatenates the array elements with commas.
        String smartMarker = "{{jsonArray:ArrayAsSingle}}";
        worksheet.getCells().get("A1").putValue(smartMarker);

        // Step 3: Prepare the data source – a simple string array
        Map<String, Object> dataSource = new HashMap<>();
        dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });

        // Step 4: Bind the data to the smart marker and save the workbook
        worksheet.getCells().get("A1").setSmartMarkerData(dataSource);
        workbook.save("JsonSingleValue.xlsx");   // workbook saved to project root
        System.out.println("Workbook created successfully.");
    }
}
```

### Qué hace el código

1. **Crea un nuevo libro de trabajo** – `new Workbook()` te proporciona un archivo Excel en memoria con una hoja predeterminada.  
2. **Coloca un marcador inteligente en la celda A1** – `{{jsonArray:ArrayAsSingle}}` indica a Aspose.Cells que reemplace el marcador con la *entera* matriz, unida por comas.  
3. **Construye una fuente de datos `Map`** – La clave `"jsonArray"` coincide con el nombre del marcador; el valor es un `String[]`.  
4. **Llama a `setSmartMarkerData`** – Esto enlaza el mapa al marcador y realiza la sustitución.  
5. **Guarda el archivo** – `workbook.save(...)` escribe `JsonSingleValue.xlsx` en disco.

Al abrir el archivo Excel generado, la celda **A1** contiene:

```
One, Two, Three
```

La matriz se muestra como una cadena única, separada por comas, gracias a la opción `ArrayAsSingle`.

---

## Usando marcadores inteligentes de Aspose.Cells para enlazar datos JSON

Los marcadores inteligentes de Aspose.Cells son una forma potente de mapear objetos complejos (incluidas estructuras tipo JSON) directamente a las hojas de cálculo. La sintaxis `{{fieldName:Option}}` funciona como un motor de plantillas:

* **fieldName** – la clave en tu fuente de datos (`Map`, POJO, o `DataTable`).  
* **Option** – controla cómo se manejan las colecciones. `ArrayAsSingle` trata toda la colección como un solo valor; otras opciones como `Array` expandirían la matriz en filas.

**¿Por qué usar un marcador inteligente en lugar de un bucle?**  
Un bucle requiere cálculos manuales de direcciones de celda, indexación propensa a errores y código adicional para el estilo. Los marcadores inteligentes te permiten escribir marcadores declarativos, mantener tu código Java breve y dejar que la biblioteca gestione los detalles de diseño.

---

## Configurando la fuente de datos Map de Java

El `Map<String, Object>` es el contenedor de datos más sencillo para Aspose.Cells:

```java
Map<String, Object> dataSource = new HashMap<>();
dataSource.put("jsonArray", new String[] { "One", "Two", "Three" });
```

*La clave (`jsonArray`) debe coincidir exactamente con el nombre del marcador.*  
También puedes usar un `List<String>`, un POJO personalizado o incluso un `Map` anidado para estructuras JSON más complejas. Aspose.Cells recorrerá el grafo de objetos automáticamente.

**Consejo:** Si necesitas formatear la cadena concatenada de forma diferente (p. ej., usando punto y coma), preprocesa la matriz en Java antes de asignarla al mapa:

```java
String joined = String.join(";", new String[] {"One","Two","Three"});
dataSource.put("jsonArray", new String[] { joined });
```

---

## Guardando el libro de trabajo y verificando la salida

```java
workbook.save("JsonSingleValue.xlsx");
```

El método `save` admite muchos formatos (`.xlsx`, `.xls`, `.csv`, `.pdf`). Para este tutorial mantenemos el formato predeterminado Excel Open XML.

**Pasos de verificación**

1. Abre `JsonSingleValue.xlsx` en Microsoft Excel, LibreOffice Calc o Google Sheets.  
2. Confirma que la celda **A1** muestra `One, Two, Three`.  
3. Verifica que no se hayan añadido filas o columnas extra – el marcador inteligente realizó una sustitución in‑place.

Si la celda muestra el texto del marcador sin procesar (`{{jsonArray:ArrayAsSingle}}`), verifica que:

* El nombre del marcador coincida exactamente con la clave del mapa (distinción de mayúsculas y minúsculas).  
* `setSmartMarkerData` se llame **después** de colocar el marcador.  
* La versión de Aspose.Cells admita la opción `ArrayAsSingle` (disponible desde v20.3).

---

## Variaciones comunes y casos límite

| Escenario | Ajuste |
|----------|------------|
| **Delimitador diferente** | Usa `ArrayAsSingle` junto con una unión personalizada en Java (ver consejo anterior). |
| **Múltiples matrices en una hoja** | Coloca marcadores adicionales como `{{anotherArray:ArrayAsSingle}}` en otras celdas y agrega entradas correspondientes al mapa. |
| **Objetos JSON anidados** | Proporciona un `Map<String, Object>` anidado; referencia los campos con notación de punto (`{{parent.child}}`). |
| **Conjuntos de datos grandes** | Para miles de filas, prefiere la opción `Array` para que Aspose.Cells expanda filas automáticamente, lo que |

---

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Cómo crear y exportar Excel a HTML usando Aspose.Cells Java \| Guía de operaciones de libro de trabajo](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Exportar libro de Excel como imagen usando Aspose.Cells para Java: Guía paso a paso](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Cómo crear y guardar un libro de Excel como SVG usando Aspose.Cells para Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}