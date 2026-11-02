---
category: general
date: 2026-08-11
description: Crear un nuevo libro de trabajo Aspose en Java, añadir una propiedad
  personalizada de Excel y luego guardar el libro como XLSB con un ejemplo completo
  paso a paso.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create new workbook aspose
- save workbook as xlsb
- add custom property excel
- Aspose.Cells Java
- custom properties Excel
- workbook serialization
language: es
lastmod: 2026-08-11
og_description: Crear un nuevo libro de trabajo Aspose en Java, añadir una propiedad
  personalizada de Excel y guardar el libro como XLSB con un ejemplo completo listo
  para ejecutar.
og_image_alt: Java code screenshot that creates a new workbook Aspose, adds a custom
  Excel property, and saves it as an XLSB file
og_title: Crear nuevo libro de trabajo Aspose – agregar propiedad personalizada Excel
schemas:
- author: Aspose
  dateModified: '2026-08-11'
  description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  headline: Create new workbook Aspose – add custom property Excel and save as XLSB
  type: TechArticle
- description: Create new workbook Aspose in Java, add a custom property Excel, then
    save workbook as XLSB with a full step‑by‑step example.
  name: Create new workbook Aspose – add custom property Excel and save as XLSB
  steps:
  - name: What if I need to store a string property?
    text: '```java worksheet.getCustomProperties().add("Owner", "Alice"); ```'
  - name: Can I add multiple custom properties at once?
    text: Yes. Call `add` repeatedly for each name/value pair. Aspose.Cells does not
      limit the number of custom properties, but keep the total size reasonable to
      avoid bloating the file.
  - name: How does the binary format affect performance?
    text: XLSB files load faster because they avoid XML parsing. This is especially
      noticeable for workbooks with many rows, formulas, or embedded images.
  - name: What if I need to work with an existing XLSX file?
    text: Replace the `new Workbook()` constructor with `new Workbook("ExistingFile.xlsx")`.
      The rest of the steps (adding properties, saving as XLSB) remain identical.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- XLSB
- Custom Properties
title: Crear nuevo libro de trabajo Aspose – agregar propiedad personalizada en Excel
  y guardar como XLSB
url: /es/java/spreadsheet-automation/create-new-workbook-aspose-add-custom-property-excel-and-sav/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo workbook Aspose – agregar propiedad personalizada Excel y guardar como XLSB

Si necesitas **crear nuevo workbook Aspose** en una aplicación Java, esta guía te muestra exactamente cómo hacerlo. Aprenderás a **agregar propiedad personalizada Excel**, a recuperar su valor y a **guardar el workbook como XLSB** sin perder metadatos.

El tutorial cubre todo, desde la configuración del proyecto hasta la verificación del archivo guardado. No se requiere documentación externa; solo sigue los pasos y ejecuta el código.

## Prerrequisitos

Antes de comenzar, asegúrate de tener:

- Java Development Kit (JDK) 8 o superior instalado.
- Maven o Gradle para gestionar dependencias (el ejemplo usa Maven).
- Una licencia activa de Aspose.Cells for Java (o usa el modo de evaluación gratuito para pruebas).

## Paso 1: Agregar Aspose.Cells a tu proyecto

Agrega el artefacto Maven de Aspose.Cells a tu `pom.xml`. Esta dependencia proporciona las clases necesarias para **crear nuevo workbook Aspose**.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

> **Consejo:** Si prefieres Gradle, reemplaza el fragmento Maven con la línea equivalente `implementation "com.aspose:aspose-cells:23.12"`.

## Paso 2: Crear un nuevo workbook Aspose

El primer paso funcional es instanciar un objeto `Workbook`. Este objeto representa un archivo Excel en memoria y es el punto de entrada para todas las operaciones posteriores.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {

    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();               // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0); // Default first sheet
```

Crear un nuevo workbook Aspose te brinda un libro limpio con una hoja de cálculo predeterminada, listo para personalizaciones.

## Paso 3: Agregar propiedad personalizada Excel

Las propiedades personalizadas te permiten almacenar metadatos arbitrarios dentro de un archivo Excel. Aquí **agregamos propiedad personalizada Excel** llamada `ProjectId` con un valor numérico.

```java
        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);
```

El método `add` acepta un nombre de propiedad y un valor de cualquier tipo compatible (cadena, número, fecha, etc.). Estos metadatos viajan con el archivo dondequiera que lo copies.

## Paso 4: Recuperar y mostrar la propiedad personalizada

Leer la propiedad verifica que se haya almacenado correctamente. También puedes usar el valor recuperado en tu lógica de negocio.

```java
        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);
```

El casting a `int` funciona porque almacenamos un valor numérico. Si almacenas una cadena, usa `(String)` en su lugar.

## Paso 5: Guardar el workbook como XLSB

Ahora **guardas el workbook como XLSB**. El formato XLSB almacena el libro en una representación binaria, lo que permite una apertura más rápida y un tamaño de archivo menor. Todas las propiedades personalizadas se conservan automáticamente.

```java
        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Reemplaza `"WithCustomProps.xlsb"` con una ruta absoluta si necesitas el archivo en un directorio específico. El enumerado `SaveFormat.XLSB` indica a Aspose.Cells que escriba en formato binario.

## Paso 6: Verificar la salida

Ejecuta el programa desde tu IDE o línea de comandos:

```bash
mvn compile exec:java -Dexec.mainClass=CustomPropertiesXlsb
```

Deberías ver:

```
ProjectId = 12345
```

Abre `WithCustomProps.xlsb` en Excel. Navega a **Archivo → Información → Propiedades → Propiedades avanzadas → Personalizadas**. La entrada `ProjectId` con el valor `12345` aparecerá listada, confirmando que el paso **add custom property excel** se completó correctamente y que la operación **save workbook as xlsb** retuvo los metadatos.

## Preguntas frecuentes y casos especiales

### ¿Qué pasa si necesito almacenar una propiedad de tipo cadena?

```java
worksheet.getCustomProperties().add("Owner", "Alice");
```

Recupérala con:

```java
String owner = (String) worksheet.getCustomProperties().get("Owner").getValue();
```

### ¿Puedo agregar varias propiedades personalizadas a la vez?

Sí. Llama a `add` repetidamente para cada par nombre/valor. Aspose.Cells no limita la cantidad de propiedades personalizadas, pero mantén el tamaño total razonable para evitar inflar el archivo.

### ¿Cómo afecta el formato binario al rendimiento?

Los archivos XLSB se cargan más rápido porque evitan el análisis XML. Esto es especialmente notable en libros con muchas filas, fórmulas o imágenes incrustadas.

### ¿Qué pasa si necesito trabajar con un archivo XLSX existente?

Reemplaza el constructor `new Workbook()` por `new Workbook("ExistingFile.xlsx")`. El resto de los pasos (agregar propiedades, guardar como XLSB) permanece idéntico.

## Código fuente completo

A continuación tienes el ejemplo completo, listo para ejecutar. Cópialo en un archivo llamado `CustomPropertiesXlsb.java` dentro de tu carpeta `src/main/java`.

```java
import com.aspose.cells.*;

public class CustomPropertiesXlsb {
    public static void main(String[] args) throws Exception {
        // Step 2: Create a new workbook Aspose
        Workbook workbook = new Workbook();                       // In‑memory workbook
        Worksheet worksheet = workbook.getWorksheets().get(0);    // Default first sheet

        // Step 3: Add a custom property named "ProjectId" with a numeric value
        worksheet.getCustomProperties().add("ProjectId", 12345);

        // Step 4: Retrieve the custom property value and display it
        int projectId = (int) worksheet.getCustomProperties()
                                      .get("ProjectId")
                                      .getValue();
        System.out.println("ProjectId = " + projectId);

        // Step 5: Save the workbook as an XLSB file (custom properties are preserved)
        workbook.save("WithCustomProps.xlsb", SaveFormat.XLSB);
    }
}
```

Ejecutar esta clase genera un archivo XLSB que contiene la propiedad personalizada y puede abrirse en cualquier versión moderna de Microsoft Excel.

## Conclusión

Ahora sabes cómo **crear nuevo workbook Aspose**, **agregar propiedad personalizada Excel** y **guardar el workbook como XLSB** usando Java. El ejemplo muestra todo el ciclo de vida: inicialización, inyección de metadatos, verificación y serialización binaria.

A continuación, explora temas relacionados como **establecer propiedades del documento**, **trabajar con fórmulas de Excel** o **convertir entre XLSX y XLSB**. Cada uno de estos se basa en la misma API de Aspose.Cells que acabas de usar, por lo que puedes ampliar la solución sin aprender nuevas bibliotecas.

Siéntete libre de experimentar con diferentes tipos de datos, múltiples hojas de cálculo o protección con contraseña—Aspose.Cells admite todos esos escenarios de forma nativa. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Create Save Excel Workbook Aspose Cells Java](/cells/english/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Excel Workbook and Add Labels with Aspose.Cells for Java](/cells/english/java/advanced-excel-charts/data-labeling/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}