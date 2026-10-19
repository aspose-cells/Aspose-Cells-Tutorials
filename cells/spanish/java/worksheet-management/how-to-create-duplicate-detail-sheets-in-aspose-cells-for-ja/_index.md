---
category: general
date: 2026-08-17
description: Aprenda cómo crear hojas de detalle duplicadas con Aspose.Cells para
  Java y permitir nombres de hoja duplicados usando SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: es
lastmod: 2026-08-17
og_description: Crea hojas de detalle duplicadas en Aspose.Cells para Java y permite
  nombres de hoja duplicados. Sigue este tutorial completo para obtener resultados
  instantáneos.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: 'Crear hojas de detalle duplicadas en Aspose.Cells para Java: guía paso
  a paso'
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Cómo crear hojas de detalle duplicadas en Aspose.Cells para Java
url: /es/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear hojas de detalle duplicadas en Aspose.Cells para Java

Si necesita **crear hojas de detalle duplicadas** en un libro de Excel, Aspose.Cells para Java lo hace sencillo. Este tutorial muestra exactamente cómo permitir nombres de hoja duplicados al generar hojas de detalle con SmartMarkerProcessor, de modo que pueda producir un libro que contenga varias hojas que comparten el mismo nombre.

Verá un ejemplo completo y ejecutable, un desglose de cada opción de configuración y consejos para manejar casos límite comunes, como colisiones de nombres y conjuntos de datos grandes. No se requieren referencias externas—todo lo que necesita está incluido en el código a continuación.

## Requisitos previos

Antes de comenzar, asegúrese de tener:

* Java Development Kit (JDK) 8 o superior.
* Maven o Gradle para gestionar dependencias.
* Biblioteca Aspose.Cells para Java (versión 23.9 o posterior). Añada la siguiente dependencia Maven a su `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Un libro de plantilla maestro (`master_template.xlsx`) que contiene una región Smart Marker para los datos de detalle.

## Visión general de la solución

La solución sigue cuatro pasos lógicos:

1. Cargar el libro de plantilla maestro.
2. Configurar `SmartMarkerProcessor` para **permitir nombres de hoja duplicados**.
3. Procesar el libro para que se cree una nueva hoja de detalle para cada grupo de datos.
4. Guardar el libro resultante que ahora contiene hojas de detalle duplicadas.

Cada paso se explica en detalle a continuación, y el archivo fuente completo se proporciona al final de la guía.

## Paso 1: Cargar el libro de plantilla maestro

La primera operación crea una instancia de `Workbook` que representa el archivo de plantilla. La plantilla debe contener un marcador de posición Smart Marker (p. ej., `&=DetailData`) que indica al procesador dónde insertar los datos.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Por qué es importante:** Cargar la plantilla aísla el diseño y el formato de la lógica de generación de datos, lo que mantiene su código limpio y facilita reutilizar la misma plantilla para diferentes conjuntos de datos.

## Paso 2: Configurar SmartMarkerProcessor para permitir nombres de hoja duplicados

Por defecto, Aspose.Cells genera nombres de hoja únicos al crear hojas de detalle. Para **permitir nombres de hoja duplicados**, establezca la opción `DetailSheetNewName` a un valor constante. El procesador reutilizará este nombre para cada hoja generada.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Por qué es importante:** Establecer `DetailSheetNewName` indica al motor que reutilice el mismo nombre para cada hoja de detalle, lo que satisface directamente el requisito de **permitir nombres de hoja duplicados**. Este enfoque es útil cuando las herramientas posteriores identifican las hojas por su posición en lugar de por su nombre.

## Paso 3: Procesar el libro para generar las hojas de detalle

Después de la configuración, invoque `process` en el libro. El procesador lee la región Smart Marker, crea una nueva hoja para cada grupo de datos y la rellena con las filas correspondientes.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Por qué es importante:** La llamada a `process` realiza el trabajo pesado—analiza los Smart Markers, clona la hoja de plantilla e inserta los datos. Como la opción `DetailSheetNewName` ya está establecida, cada hoja nueva recibe el mismo nombre, lo que produce nombres de hoja duplicados en el archivo final.

## Paso 4: Guardar el libro resultante

Finalmente, escriba el libro modificado en un nuevo archivo. El archivo de salida contendrá tantas pestañas “DetailSheet” como grupos de datos haya.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Por qué es importante:** Guardar el archivo finaliza los cambios realizados por el procesador. El libro resultante puede abrirse en Microsoft Excel, LibreOffice o cualquier otra aplicación de hoja de cálculo que admita el formato XLSX.

## Código fuente completo

Juntando todas las piezas, aquí está el programa completo que puede copiar, pegar y ejecutar:

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Resultado esperado

Cuando abra `duplicate_detail.xlsx`, verá varias pestañas nombradas **DetailSheet**. Cada pestaña contiene el conjunto de datos que correspondía a un grupo específico de Smart Marker en la plantilla. El diseño, formato y fórmulas de la plantilla maestra se conservan en cada hoja duplicada.

## Manejo de problemas comunes

| Problema | Explicación | Solución |
|----------|-------------|----------|
| Excel muestra una advertencia sobre nombres de hoja duplicados | Excel permite nombres duplicados pero puede mostrar una advertencia al abrir el archivo. | La advertencia es inofensiva; el libro funciona correctamente. Si prefiere suprimir la advertencia, renombre las hojas después del procesamiento usando `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Los conjuntos de datos grandes causan alto uso de memoria | Cada hoja duplicada crea una copia completa de la plantilla, lo que puede consumir RAM. | Active el modo de transmisión con `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` antes de cargar la plantilla. |
| Región Smart Marker no encontrada | El procesador no puede localizar `&=DetailData` en la plantilla. | Verifique que la sintaxis del marcador de posición coincida con la fuente de datos y que la hoja de plantilla no esté oculta. |

## Consejo profesional: personalizar el esquema de nombres duplicados

Si necesita un patrón de nombres predecible mientras sigue permitiendo duplicados, combine un nombre base con un índice:

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

El marcador `{0}` se reemplaza por el índice de la hoja, produciendo nombres como `DetailSheet_1`, `DetailSheet_2`, etc. Esto sigue cumpliendo el requisito de **permitir nombres de hoja duplicados** porque el nombre base permanece constante.

## Próximos pasos

Ahora que puede **crear hojas de detalle duplicadas**, podría explorar los siguientes temas:

* **Rellenar hojas de detalle con imágenes** – use objetos `Picture` para incrustar logotipos o gráficos.
* **Aplicar formato condicional** – añada reglas `FormatCondition` para resaltar filas según valores.
* **Exportar a PDF** – llame a `workbook.save("output.pdf", SaveFormat.PDF);` para generar una versión PDF de las hojas duplicadas.

Cada una de estas extensiones se basa en el mismo flujo de trabajo Smart Marker demostrado aquí, permitiéndole automatizar tareas complejas de generación de informes en Excel con confianza.

---

*Ha aprendido cómo crear hojas de detalle duplicadas en Aspose.Cells para Java y cómo permitir nombres de hoja duplicados usando SmartMarkerProcessor. Aplique el código, adapte la plantilla e integre la técnica en sus flujos de trabajo de generación de informes.*

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Crear y acceder a hojas de Excel, agregar marcadores PDF usando Aspose.Cells para Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Crear acceso a hojas de Excel, agregar marcadores PDF Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Crear acceso a hojas de Excel, agregar marcadores PDF Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}