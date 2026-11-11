---
date: '2026-10-28'
description: Aprenda cómo pegar valores usando las opciones de copiar y pegar de Aspose.Cells
  en Java, con código paso a paso, configuración de dependencias Maven y consejos
  de licenciamiento.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Aprenda cómo pegar valores usando las opciones de copiar y pegar de
  Aspose.Cells en Java, con código paso a paso, configuración de dependencias Maven
  y consejos de licenciamiento.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Cómo pegar valores con las opciones de copiar y pegar de Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Cómo pegar valores con las opciones de copiar y pegar de Aspose.Cells
url: /es/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo pegar valores con las opciones de copiar y pegar de Aspose.Cells

Automatizar la generación de informes de Excel en Java significa que puedes crear, consolidar y formatear libros de trabajo sin abrir Excel manualmente. Con **Aspose.Cells** obtienes control total sobre fórmulas, filas ocultas y valores de celdas, de modo que tus informes se mantengan precisos y ligeros. En este tutorial aprenderás a usar **CopyOptions.ReferToDestinationSheet** para mantener las fórmulas correctas y **PasteOptions** para pegar solo los valores visibles que necesitas.

## Respuestas rápidas
- **¿Qué hace `CopyOptions.ReferToDestinationSheet`?** Reescribe las fórmulas para que apunten a la hoja de destino después de una operación de copia.  
- **¿Cómo puedo pegar solo celdas visibles?** Llama a `PasteOptions.setOnlyVisibleCells(true)` junto con `PasteType.VALUES`.  
- **¿Qué versión de la biblioteca se requiere?** Aspose.Cells 25.3 o posterior.  
- **¿Necesito una licencia para producción?** Sí – una licencia permanente o temporal elimina los límites de evaluación.  
- **¿Puedo usar Maven o Gradle?** Ambos son compatibles; consulta los fragmentos de dependencia a continuación.

## Qué significa “automatizar la generación de informes de Excel”
Automatizar la generación de informes de Excel significa crear y actualizar libros de trabajo de Excel de forma programática, lo que permite crear, combinar y formatear informes sin copiar‑pegar manualmente, reduciendo errores y ahorrando horas de trabajo repetitivo. Este enfoque es ideal para trabajos por lotes programados, paneles impulsados por datos y pipelines de consolidación financiera.

## ¿Por qué usar CopyOptions y PasteOptions para la generación de informes?
Estas dos clases te permiten mantener intactas las referencias de fórmulas al copiar datos **y** extraer solo las celdas visibles después de filtrar u ocultar filas. Usarlas juntas reduce la cantidad de datos transferidos hasta en un 80 % en escenarios típicos de tablas filtradas y garantiza que las fórmulas continúen calculándose correctamente en la hoja de destino.

## Requisitos previos
- Java 8 o superior.  
- Maven o Gradle para la gestión de dependencias.  
- Aspose.Cells 25.3+ (licencia de prueba, temporal o permanente).  

## Configuración de Aspose.Cells para Java

Agrega la biblioteca a tu proyecto con una de las siguientes opciones:

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Obtención de licencia
- **Free trial** – conjunto completo de funciones para evaluación.  
- **Temporary license** – elimina los límites de prueba mientras pruebas.  
- **Permanent license** – recomendado para cargas de trabajo de producción.

Inicializa Aspose.Cells en tu código Java:  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guía paso a paso

### 1. copyOptions con referToDestinationSheet

#### Visión general
`CopyOptions` es el objeto de configuración de Aspose.Cells que controla cómo se manejan las fórmulas y referencias de celdas durante una operación de copia. Configurar `CopyOptions.ReferToDestinationSheet` a `true` reescribe las referencias de fórmulas para que apunten a la nueva hoja después de la operación de copia.

#### Paso 1: inicializar el libro de trabajo y las hojas de cálculo  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Paso 2: configurar copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Paso 3: ejecutar la operación de copia  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Por qué es importante*: Las fórmulas que originalmente referenciaban `Sheet1` ahora referenciarán correctamente a `DestSheet`, manteniendo tus informes automatizados fiables.

**Consejo de solución**: Si las fórmulas aún referencian la hoja antigua, asegúrate de que `setReferToDestinationSheet(true)` se llame **antes** de la copia.

### 2. pasteOptions para valores‑solo de celdas visibles

#### Visión general
`PasteOptions` es el objeto de configuración de Aspose.Cells que define qué se pega. Usar `PasteType.VALUES` junto con `onlyVisibleCells=true` copia solo los valores mostrados, ignorando filas/columnas ocultas y el formato.

#### Paso 1: inicializar el libro de trabajo y las hojas de cálculo  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Paso 2: configurar pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Paso 3: ejecutar la operación de pegado  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Por qué es importante*: Ideal para extraer datos filtrados o generar informes limpios sin filas ocultas o ruido de formato.

**Consejo de solución**: Verifica que las filas/columnas estén realmente ocultas en Excel antes de copiar; de lo contrario, se incluirán.

## Aplicaciones prácticas
1. **Financial consolidation** – combina hojas mensuales en un libro maestro manteniendo todas las fórmulas precisas.  
2. **Filtered data export** – extrae solo las filas visibles de una tabla filtrada a una hoja de resumen.  
3. **Scheduled report generation** – automatiza la creación nocturna de informes de Excel con valores de celda precisos y referencias correctas.

## Consideraciones de rendimiento
- **Dispose of workbooks** when done (`wb.dispose();`) to free native resources.  
- **Batch operations** – agrupa múltiples llamadas de copiar/pegar para reducir la sobrecarga.  
- **Monitor memory** – los libros de trabajo grandes pueden requerir un heap aumentado (`-Xmx2g`).  
- Aspose.Cells soporta **más de 50 formatos de entrada y salida** y puede procesar libros de trabajo con **hasta 2 millones de filas** sin cargar todo el archivo en memoria, ofreciendo un rendimiento de alto rendimiento para cargas de trabajo empresariales.

## Preguntas frecuentes

**Q: ¿Para qué se utiliza `CopyOptions.ReferToDestinationSheet`?**  
A: Reescribe las referencias de fórmulas para que apunten a la hoja de destino después de una copia, asegurando que las fórmulas de los informes permanezcan correctas.

**Q: ¿Cómo pego solo celdas visibles?**  
A: Configura `PasteOptions.setOnlyVisibleCells(true)` y elige `PasteType.VALUES`.

**Q: ¿Puedo usar Aspose.Cells sin comprar una licencia?**  
A: Sí, hay una prueba gratuita o una licencia temporal disponible para evaluación, pero se requiere una licencia permanente para producción.

**Q: ¿Por qué algunas referencias siguen incorrectas después de copiar?**  
A: Verifica que `ReferToDestinationSheet` esté habilitado **antes** de la operación de copia y que las fórmulas de origen no contengan enlaces a libros de trabajo externos.

**Q: ¿Qué buenas prácticas de gestión de memoria debo seguir?**  
A: Libera los objetos `Workbook` cuando termines, procesa archivos grandes en fragmentos y monitorea el uso del heap de la JVM.

**Q: ¿Es posible combinar CopyOptions y PasteOptions en una sola operación?**  
A: Sí, puedes encadenarlos copiando primero con `CopyOptions` y luego aplicando `PasteOptions` en el rango objetivo.

## Recursos
- **Documentación**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Descarga**: [Aspose.Cells releases for Java](https://releases.aspose.com/cells/java/)  
- **Compra**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Prueba gratuita**: [Aspose.Cells free trial](https://releases.aspose.com/cells/java/)  
- **Licencia temporal**: [Apply for a temporary license](https://purchase.aspose.com/temporary-license/)  
- **Foro de soporte**: [Aspose support](https://forum.aspose.com/c/cells)

---

**Última actualización:** 2026-10-28  
**Probado con:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Tutoriales relacionados

- [Leer archivo Excel Java – Manipulación de celdas de libro de trabajo con Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Agregar datos a la celda en Excel usando Aspose.Cells para Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convertir índices de fila y columna de celdas Excel con Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}