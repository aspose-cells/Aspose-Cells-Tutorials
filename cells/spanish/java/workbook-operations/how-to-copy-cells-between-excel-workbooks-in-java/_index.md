---
category: general
date: 2026-11-16
description: Cómo copiar celdas entre libros de Excel en Java – cargar un libro, copiar
  un rango entre libros (incluyendo una tabla dinámica) y guardar el archivo del libro.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy cells
- copy range between workbooks
- copy pivot table workbook
- save workbook file
- load excel workbook java
language: es
lastmod: 2026-11-16
og_description: Cómo copiar celdas entre libros de Excel en Java. Aprende a cargar
  un libro de Excel, copiar un rango (incluyendo una tabla dinámica) entre libros
  y guardar el archivo del libro.
og_image_alt: Screenshot of Java code copying a cell range from one Excel workbook
  to another
og_title: Cómo copiar celdas entre libros de Excel en Java – guía completa
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  headline: How to copy cells between Excel workbooks in Java
  type: TechArticle
- description: How to copy cells between Excel workbooks in Java – load a workbook,
    copy range between workbooks (including a pivot table), and save the workbook
    file.
  name: How to copy cells between Excel workbooks in Java
  steps:
  - name: Load the source workbook
    text: '```java import com.aspose.cells.*;'
  - name: Define the range that includes the pivot table
    text: '```java // Define the cell range that you want to copy. // Adjust "A1:G20"
      to match the area that contains your data/pivot table. Range srcRange = srcWs.getCells().createRange("A1:G20");
      ```'
  - name: Create the destination workbook
    text: '```java // Create a new, empty workbook that will receive the copied range.
      Workbook destWb = new Workbook(); // defaults to a single empty sheet Worksheet
      destWs = destWb.getWorksheets().get(0); ```'
  - name: Copy the range to the destination workbook
    text: '```java // Copy the source range to cell A1 of the destination worksheet.
      destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1")); ```'
  - name: Save the destination workbook
    text: '```java // Save the new workbook to disk. destWb.save("YOUR_DIRECTORY/dest.xlsx");
      } } ```'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- Workbook manipulation
title: Cómo copiar celdas entre libros de Excel en Java
url: /es/java/workbook-operations/how-to-copy-cells-between-excel-workbooks-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo copiar celdas entre libros de Excel en Java

Si necesitas **copiar celdas** de un libro de Excel a otro usando Java, esta guía te muestra una forma fiable de hacerlo. Aprenderás cómo **load Excel workbook Java**, copiar un rango que puede contener una tabla dinámica, y finalmente **save workbook file** con los datos copiados.

Este tutorial cubre:

* Cargar un libro de origen y seleccionar una hoja de cálculo.  
* Definir el rango exacto que deseas mover (incluyendo una tabla dinámica).  
* Crear un libro de destino y copiar el rango.  
* Guardar el archivo de destino.  

El ejemplo usa la biblioteca Aspose.Cells for Java, que funciona con archivos Excel sin requerir Microsoft Office. El código se ejecuta en Java 8+ y cualquier IDE moderno (IntelliJ IDEA, Eclipse, VS Code, etc.).

---

## Requisitos previos

Antes de comenzar, asegúrate de tener:

| Requisito | Razón |
|-------------|--------|
| Java Development Kit (JDK) 8 o más reciente | Requerido para compilar y ejecutar el código. |
| Herramienta de construcción Maven o Gradle | Simplifica la adición de la dependencia Aspose.Cells. |
| Biblioteca Aspose.Cells for Java (última versión) | Proporciona las clases `Workbook`, `Worksheet` y `Range` usadas en el ejemplo. |
| Dos archivos Excel (`source.xlsx` y una carpeta vacía para `dest.xlsx`) | El archivo de origen debe contener los datos y, opcionalmente, una tabla dinámica que deseas copiar. |

Agrega la dependencia Aspose.Cells a tu `pom.xml` (Maven) o `build.gradle` (Gradle). Ejemplo para Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- use the latest version -->
</dependency>
```

---

## Cómo copiar celdas con Aspose.Cells

Los siguientes pasos te guían a través del proceso completo. Cada paso incluye el código Java, una explicación de **¿Por qué?** el paso es importante, y un consejo para evitar errores comunes.

### Paso 1: Cargar el libro de origen

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source Excel file (replace with your actual path)
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // Get the first worksheet (index 0)
        Worksheet srcWs = srcWb.getWorksheets().get(0);
```

**¿Por qué?**  
`Workbook` representa todo el archivo Excel. Cargarlo te brinda acceso a todas las hojas de cálculo, celdas y objetos como tablas dinámicas. Usar la primera hoja es común, pero puedes seleccionar cualquier hoja por nombre (`srcWb.getWorksheets().get("Sheet2")`).

**Consejo profesional:**  
Si el archivo de origen es grande, considera cargarlo en modo *memory‑efficient*: `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setMemorySetting(MemorySetting.MEMORY_PREFERENCE); }});`

### Paso 2: Definir el rango que incluye la tabla dinámica

```java
        // Define the cell range that you want to copy.
        // Adjust "A1:G20" to match the area that contains your data/pivot table.
        Range srcRange = srcWs.getCells().createRange("A1:G20");
```

**¿Por qué?**  
Un objeto `Range` abstrae un bloque rectangular de celdas. Al especificar `"A1:G20"` le indicas a Aspose.Cells exactamente qué celdas—incluyendo cualquier tabla dinámica incrustada—copiar. La biblioteca copia automáticamente los datos subyacentes, estilos y definiciones de tabla dinámica.

**Caso límite:**  
Si la tabla dinámica se extiende más allá del rango definido, amplía la dirección (p.ej., `"A1:Z100"`). También puedes usar `srcWs.getCells().getMaxDataColumn()` y `getMaxDataRow()` para calcular el área usada dinámicamente.

### Paso 3: Crear el libro de destino

```java
        // Create a new, empty workbook that will receive the copied range.
        Workbook destWb = new Workbook();               // defaults to a single empty sheet
        Worksheet destWs = destWb.getWorksheets().get(0);
```

**¿Por qué?**  
Un libro nuevo garantiza que no haya formatos no deseados o hojas ocultas que interfieran con el contenido copiado. El libro predeterminado ya contiene una hoja de cálculo, que usaremos como objetivo.

### Paso 4: Copiar el rango al libro de destino

```java
        // Copy the source range to cell A1 of the destination worksheet.
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));
```

**¿Por qué?**  
`copyRange` maneja todos los atributos de celda: valores, fórmulas, formato e incluso cachés de tabla dinámica. Al copiar a `"A1"` colocas el rango en la esquina superior izquierda de la hoja de destino, preservando el diseño original.

**Pregunta frecuente:** *¿La tabla dinámica seguirá funcionando?*  
Sí. Aspose.Cells copia la definición de la tabla dinámica y su caché, por lo que la tabla funciona exactamente como en el libro de origen.

### Paso 5: Guardar el libro de destino

```java
        // Save the new workbook to disk.
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**¿Por qué?**  
Llamar a `save` escribe el libro en memoria a un archivo físico `.xlsx`. También puedes guardar en otros formatos (`.xls`, `.csv`, `.pdf`) cambiando la extensión del archivo o usando `SaveOptions`.

**Consejo:**  
Si necesitas transmitir el archivo a una respuesta web, usa `destWb.save(OutputStream, SaveFormat.XLSX);` en lugar de una ruta de archivo.

---

## Copiar rango entre libros – código fuente completo

A continuación se muestra la clase Java completa, lista para ejecutar. Reemplaza `YOUR_DIRECTORY` con la carpeta real en tu máquina.

```java
import com.aspose.cells.*;

public class ExcelCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/source.xlsx");
        Worksheet srcWs = srcWb.getWorksheets().get(0);

        // Define the range that includes the data and pivot table
        Range srcRange = srcWs.getCells().createRange("A1:G20");

        // Create a new destination workbook
        Workbook destWb = new Workbook();
        Worksheet destWs = destWb.getWorksheets().get(0);

        // Copy the defined range to the destination workbook
        destWs.getCells().copyRange(srcRange, destWs.getCells().get("A1"));

        // Save the destination workbook
        destWb.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Resultado esperado:**  
`dest.xlsx` contiene una réplica exacta del rango `A1:G20` de `source.xlsx`. Si el rango de origen contenía una tabla dinámica, el archivo de destino muestra la misma tabla dinámica con su origen de datos correctamente vinculado a las celdas copiadas.

Puedes abrir `dest.xlsx` en Excel, LibreOffice o cualquier visor que soporte `.xlsx` para verificar que los valores, el formato y la funcionalidad de la tabla dinámica se conservan.

---

## Copiar libro de tabla dinámica – lo que debes saber

* **El caché de la tabla dinámica se copia automáticamente.** La biblioteca transfiere el caché subyacente, por lo que la tabla dinámica no necesita refrescarse manualmente.
* **Las fuentes de datos externas no se transfieren.** Si la tabla dinámica extrae datos de una base de datos externa, debes asegurarte de que el libro de destino pueda acceder a la misma fuente, o recrear el caché localmente.
* **Las tablas dinámicas grandes pueden aumentar el uso de memoria.** Para libros muy grandes, considera incrementar el heap de la JVM (`-Xmx2g`) para evitar `OutOfMemoryError`.

---

## Guardar archivo de libro en diferentes formatos

Aspose.Cells te permite guardar el resultado en muchos formatos sin cambios adicionales de código:

```java
// Save as XLS (Excel 97-2003)
destWb.save("dest.xls");

// Save as CSV (first worksheet only)
destWb.save("dest.csv");

// Save as PDF (visual representation)
destWb.save("dest.pdf");
```

Elige el formato que coincida con tu proceso posterior. La misma lógica `copyRange` funciona independientemente del formato final.

---

## Cargar Excel workbook Java – consejos adicionales

* **Cargando archivos encriptados:** Usa `LoadOptions` con una contraseña:  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setPassword("myPassword");
  Workbook wb = new Workbook("encrypted.xlsx", opt);
  ```
* **Leyendo solo hojas específicas:**  
  ```java
  LoadOptions opt = new LoadOptions(LoadFormat.XLSX);
  opt.setLoadDataOnly(true); // faster if you only need values
  Workbook wb = new Workbook("file.xlsx", opt);
  ```

Estas opciones pueden acelerar el paso **load excel workbook java**, especialmente para archivos grandes.

---

## Conclusión

Ahora sabes **cómo copiar celdas** entre libros de Excel en Java, cómo **copiar rango entre libros** que contiene una **tabla dinámica**, y cómo **guardar archivo de libro** en el formato que necesitas. Siguiendo los pasos anteriores, puedes integrar la manipulación de datos de Excel en cualquier aplicación Java—ya sea que estés construyendo un motor de informes, una canalización ETL o una utilidad simple de conversión de archivos.

**Próximos pasos** que podrías explorar:

* Usa **copy range between workbooks** para combinar varios informes en

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarte a dominar características adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Guardar nuevo libro en Java – Tutorial de copiar rango entre libros](/cells/english/java/workbook-operations/save-new-workbook-in-java-copy-range-between-workbooks-tutor/)
- [Cómo copiar tablas dinámicas entre libros de Excel en Java](/cells/english/java/excel-pivot-tables/how-to-copy-pivot-tables-between-excel-workbooks-in-java/)
- [Cómo copiar rango en Java – Copiar tabla dinámica con Aspose.Cells](/cells/english/java/excel-pivot-tables/how-to-copy-range-in-java-copy-pivot-table-with-aspose-cells/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}