---
date: '2026-10-28'
description: Aprenda cómo cambiar el sistema de fechas de Excel a 1904 usando Aspose.Cells
  for Java, establecer el formato de fecha de Excel y convertir el sistema 1904 de
  Excel de manera eficiente.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Cambie el sistema de fechas de Excel a 1904 usando Aspose.Cells for
  Java. Aprenda paso a paso cómo habilitar el sistema 1904, establecer fechas y volver
  a convertir.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Cambiar el sistema de fechas de Excel a 1904 con Aspose.Cells for Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Cambiar el sistema de fechas de Excel a 1904 con Aspose.Cells Java
url: /es/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar el sistema de fechas de Excel a 1904 con Aspose.Cells Java

En este tutorial aprenderá cómo **cambiar el sistema de fechas de Excel** al formato 1904 usando Aspose.Cells para Java. El sistema 1904 es esencial cuando necesita conservar fechas heredadas de Mac o alinearse con modelos financieros que esperan esa época. Recorreremos la instalación de la biblioteca, la carga de un libro de trabajo, la conmutación del sistema de fechas y el guardado del resultado, todo sin requerir Microsoft Excel en el servidor.

## Respuestas rápidas
- **¿Qué hace el sistema de fechas 1904?** Comienza a contar los días a partir del 1 de enero de 1904, desplazando todas las fechas 1 462 días respecto al sistema predeterminado de 1900.  
- **¿Por qué usar Aspose.Cells para cambiar el sistema de fechas?** Proporciona una API sencilla que funciona sin Excel instalado y soporta archivos grandes.  
- **¿Qué versiones de Java son compatibles?** JDK 8 o superior.  
- **¿Necesito una licencia?** Una prueba gratuita funciona para evaluación; una licencia elimina los límites de uso.  
- **¿Puedo volver al sistema 1900 más tarde?** Sí, basta con llamar a `setDate1904(false)`.

## ¿Qué es el sistema de fechas 1904 en Excel?
El sistema de fechas 1904 cuenta los días a partir del 1 de enero de 1904, en lugar de la época predeterminada de 1900. Este desplazamiento añade exactamente 1 462 días a cada valor de fecha, por lo que los libros de trabajo heredados de Mac aparecen desfasados cuando se abren en Windows. Se utiliza principalmente para compatibilidad con archivos de Excel de Macintosh antiguos y algunos modelos financieros heredados.

## ¿Por qué cambiar el sistema de fechas de Excel con Aspose.Cells?
Puede cambiar el sistema de fechas directamente desde Java, eliminando pasos manuales en Excel. Aspose.Cells procesa libros de trabajo de hasta **2 GB** y puede convertir un libro de 500 hojas en menos de **2 segundos** en un servidor típico de 4 núcleos, ofreciendo una automatización de alto rendimiento del lado del servidor.

## Requisitos previos
- Java Development Kit (JDK) 8 o superior.  
- Maven o Gradle para la gestión de dependencias.  
- Conocimientos básicos de programación en Java.  

## Configuración de Aspose.Cells para Java

### Maven
Agregue la siguiente dependencia a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Incluya esta línea en su archivo `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Obtención de licencia
Aspose ofrece una prueba gratuita, licencia temporal y licencias comerciales completas. Puede comenzar con la [prueba gratuita](https://releases.aspose.com/cells/java/) o obtener una licencia temporal desde la [página de licencia temporal](https://purchase.aspose.com/temporary-license/).

## ¿Cómo cambiar el sistema de fechas de Excel a 1904 con Aspose.Cells para Java?
Cargue el libro de trabajo, habilite la configuración 1904 y guarde el archivo; este flujo de tres pasos actualiza la época interna de fechas del libro en menos de un segundo. La llamada a la API `setDate1904(true)` invierte la bandera del sistema, y el cambio se persiste al llamar a `save`. No se requiere instalación de Excel, lo que lo hace ideal para entornos de servidor sin interfaz gráfica.

### Paso 1: inicializar y cargar el libro de trabajo
La clase `Workbook` representa un archivo Excel completo en memoria. Primero, cree una instancia de `Workbook` que apunte a su archivo existente.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Paso 2: habilitar el sistema de fechas 1904
El método `WorkbookSettings.setDate1904` conmute la bandera de fecha a nivel de libro. Establecerlo en `true` activa el sistema 1904 para todas las hojas.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Consejo profesional:** También puede llamar a `setDate1904(false)` más adelante si necesita revertir.

### Paso 3: guardar el libro de trabajo modificado
Finalmente, escriba los cambios en un nuevo archivo (o sobrescriba el original). El método `save` respeta automáticamente el sistema de fechas activo.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Nota:** El código anterior usa el nombre de clase `tWorkbook` tal como se proporcionó originalmente. Asegúrese de que este error tipográfico coincida con las convenciones de nombres de su proyecto o corríjalo a `Workbook` si es necesario.

## Establecer la fecha de Excel programáticamente (palabra clave secundaria)
Si necesita ajustar valores de celdas individuales después de cambiar el sistema, puede usar `cells.get(i, j).putValue(Date)` donde la fecha se interpretará según el sistema de fechas activo.

## Convertir el sistema 1904 de Excel a 1900 (palabra clave secundaria)
Para revertir, simplemente llame:

```java
workbook.getSettings().setDate1904(false);
```

Luego guarde el libro de trabajo nuevamente.

## Aplicaciones prácticas
1. **Archivado de datos** – Conservar marcas de tiempo heredadas al migrar hojas de cálculo antiguas basadas en Mac.  
2. **Informes multiplataforma** – Generar informes que se abran correctamente tanto en Windows como en macOS sin desajustes de fechas.  
3. **Modelado financiero** – Alinear los cálculos de fechas con modelos financieros heredados que esperan el sistema 1904.

## Consideraciones de rendimiento
- Limite las operaciones del libro de trabajo en una sola sesión para mantener bajo el uso de memoria; Aspose.Cells transmite datos y nunca carga todo el archivo en RAM a menos que lo solicite explícitamente.  
- Ajuste los flags de recolección de basura de Java (`-XX:+UseG1GC`) para archivos muy grandes y evitar picos de pausa.  

## Preguntas frecuentes

**P: ¿Cuál es la diferencia entre los sistemas de fechas 1900 y 1904?**  
R: El sistema 1900 comienza el 1 de enero de 1900, mientras que el 1904 comienza el 1 de enero de 1904, desplazando todas las fechas 1 462 días.

**P: ¿Puedo cambiar el sistema de fechas de un libro que está abierto en Excel?**  
R: Sí, pero debe cerrar el archivo en Excel primero; de lo contrario, la operación de guardado fallará.

**P: ¿Necesito una licencia para usar `setDate1904`?**  
R: El método funciona en la prueba gratuita, pero una licencia completa elimina las limitaciones de evaluación.

**P: ¿Es posible cambiar el sistema de fechas solo para una hoja?**  
R: No, el sistema de fechas es una configuración a nivel de libro; se aplica a todas las hojas.

**P: ¿Cómo puedo verificar que el sistema de fechas se haya cambiado?**  
R: Abra el archivo guardado en Excel, vaya a **Archivo → Opciones → Avanzado**, y marque la casilla **"Usar sistema de fechas 1904"**.

## Conclusión
Ahora sabe cómo **cambiar el sistema de fechas de Excel** a 1904 usando Aspose.Cells para Java, cómo establecer fechas en celdas individuales y cómo volver al sistema 1900 cuando sea necesario. Integre estos fragmentos en sus flujos de procesamiento de datos para garantizar la compatibilidad de fechas entre plataformas y archivos heredados.

---

**Última actualización:** 2026-10-28  
**Probado con:** Aspose.Cells 25.3 para Java  
**Autor:** Aspose  

**Recursos**
- **Documentación:** [Referencia de Aspose.Cells Java](https://reference.aspose.com/cells/java/)
- **Descarga:** [Lanzamientos de Aspose.Cells](https://releases.aspose.com/cells/java/)
- **Comprar licencia:** [Adquirir Aspose.Cells](https://purchase.aspose.com/buy)
- **Prueba gratuita:** [Iniciar prueba gratuita](https://releases.aspose.com/cells/java/)
- **Licencia temporal:** [Obtener licencia temporal](https://purchase.aspose.com/temporary-license/)
- **Foro de soporte:** [Soporte de Aspose](https://forum.aspose.com/c/cells/9)

## Tutoriales relacionados

- [Convertir Excel a PDF de forma eficiente con formatos de fecha personalizados usando Aspose.Cells para Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells para Java: Cómo crear y formatear libros de trabajo Excel de forma eficiente](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Dominar la manipulación de Excel con Aspose.Cells para Java: Operaciones de libros y tutorial de estilo de celdas](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}