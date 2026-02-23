---
date: '2026-02-22'
description: Aprende cómo automatizar la generación de informes de Excel con Aspose.Cells
  en Java utilizando CopyOptions y PasteOptions para mantener las fórmulas precisas
  y pegar solo los valores visibles.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatizar la generación de informes en Excel – Dominando CopyOptions y PasteOptions
  en Java con Aspose.Cells
url: /es/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatizar informes de Excel con Aspose.Cells: CopyOptions y PasteOptions en Java

¿Busca **automatizar la generación de informes de Excel** usando Java? Con Aspose.Cells puede copiar, pegar y ajustar fórmulas de forma programática para que sus informes permanezcan precisos y solo se transfieran los datos que necesita. En este tutorial revisaremos dos características esenciales—**CopyOptions.ReferToDestinationSheet** y **PasteOptions**—que le permiten conservar las referencias de fórmulas y pegar valores solo de las celdas visibles.

## Respuestas rápidas
- **¿Qué hace `CopyOptions.ReferToDestinationSheet`?** Ajusta las fórmulas para que apunten a la hoja de destino al copiar datos.  
- **¿Cómo puedo pegar solo las celdas visibles?** Establezca `PasteOptions.setOnlyVisibleCells(true)` con `PasteType.VALUES`.  
- **¿Qué versión de la biblioteca se requiere?** Aspose.Cells 25.3 o posterior.  
- **¿Necesito una licencia para producción?** Sí, una licencia permanente o temporal elimina los límites de evaluación.  
- **¿Puedo usar Maven o Gradle?** Ambos son compatibles; vea los fragmentos de dependencias a continuación.

## ¿Qué es “automatizar la generación de informes de Excel”?
Automatizar la generación de informes de Excel significa crear, consolidar y formatear libros de Excel de forma programática, eliminando pasos manuales de copiar‑pegar y reduciendo errores. Aspose.Cells ofrece una API completa que permite a los desarrolladores Java manipular hojas de cálculo a gran escala.

## ¿Por qué usar CopyOptions y PasteOptions para los informes?
- **Mantener la integridad de las fórmulas** al mover datos entre hojas.  
- **Excluir filas/columnas ocultas** para mantener los informes limpios y enfocados.  
- **Mejorar el rendimiento** copiando solo los datos necesarios en lugar de rangos completos.

## Requisitos previos
- Java 8 o superior.  
- Maven o Gradle para la gestión de dependencias.  
- Aspose.Cells 25.3+ (licencia de prueba, temporal o permanente).  

## Configuración de Aspose.Cells para Java

Agregue la biblioteca a su proyecto con una de las siguientes opciones:

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

### Obtención de la licencia
- **Prueba gratuita** – Conjunto completo de funcionalidades para evaluación.  
- **Licencia temporal** – Elimina las limitaciones de prueba mientras prueba.  
- **Licencia permanente** – Recomendada para cargas de trabajo en producción.

Inicialice Aspose.Cells en su código Java:

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guía paso a paso

### 1. CopyOptions con ReferToDestinationSheet

#### Visión general
Establecer `CopyOptions.ReferToDestinationSheet` en `true` reescribe las referencias de fórmulas para que apunten a la nueva hoja después de la operación de copia.

#### Paso 1: Inicializar Workbook y Worksheets
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Paso 2: Configurar CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Paso 3: Ejecutar la operación de copia
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Por qué es importante*: Las fórmulas que originalmente hacían referencia a `Sheet1` ahora harán referencia correctamente a `DestSheet`, manteniendo sus informes automatizados fiables.

**Consejo de solución de problemas**: Si las fórmulas aún hacen referencia a la hoja anterior, asegúrese de que `setReferToDestinationSheet(true)` se llame **antes** de la copia.

### 2. PasteOptions para valores‑únicamente de celdas visibles

#### Visión general
`PasteOptions` le permite definir qué se pega. Usar `PasteType.VALUES` junto con `onlyVisibleCells=true` copia solo los valores mostrados, ignorando filas/columnas ocultas y el formato.

#### Paso 1: Inicializar Workbook y Worksheets
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Paso 2: Configurar PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Paso 3: Ejecutar la operación de pegado
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Por qué es importante*: Ideal para extraer datos filtrados o generar informes limpios sin filas ocultas o ruido de formato.

**Consejo de solución de problemas**: Verifique que las filas/columnas estén realmente ocultas en Excel antes de copiar; de lo contrario, se incluirán.

## Aplicaciones prácticas
1. **Consolidación financiera** – Fusionar hojas mensuales en un libro maestro manteniendo todas las fórmulas precisas.  
2. **Exportación de datos filtrados** – Extraer solo las filas visibles de una tabla filtrada a una hoja de resumen.  
3. **Generación programada de informes** – Automatizar la creación nocturna de informes de Excel con valores de celda precisos y referencias correctas.

## Consideraciones de rendimiento
- **Liberar los Workbooks** cuando termine (`wb.dispose();`) para liberar recursos nativos.  
- **Operaciones por lotes** – Agrupar múltiples llamadas de copiar/pegar para reducir la sobrecarga.  
- **Monitorear la memoria** – Los libros grandes pueden requerir un heap mayor (`-Xmx2g`).

## Preguntas frecuentes

**Q1: ¿Para qué se usa `CopyOptions.ReferToDestinationSheet`?**  
R: Reescribe las referencias de fórmulas para que apunten a la hoja de destino después de una copia, asegurando que las fórmulas de los informes permanezcan correctas.

**Q2: ¿Cómo pego solo las celdas visibles?**  
R: Establezca `PasteOptions.setOnlyVisibleCells(true)` y elija `PasteType.VALUES`.

**Q3: ¿Puedo usar Aspose.Cells sin comprar una licencia?**  
R: Sí, hay una prueba gratuita o licencia temporal disponible para evaluación, pero se requiere una licencia permanente para producción.

**Q4: ¿Por qué algunas referencias siguen incorrectas después de copiar?**  
R: Verifique que `ReferToDestinationSheet` esté habilitado **antes** de la operación de copia y que las fórmulas de origen no contengan enlaces a libros externos.

**Q5: ¿Qué buenas prácticas de gestión de memoria debo seguir?**  
R: Libere los objetos `Workbook` cuando termine, procese archivos grandes por partes y monitoree el uso del heap de la JVM.

**Q6: ¿Es posible combinar CopyOptions y PasteOptions en una sola operación?**  
R: Sí, puede encadenarlos copiando primero con `CopyOptions` y luego aplicando `PasteOptions` en el rango de destino.

## Recursos
- **Documentación**: [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Descarga**: [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Compra**: [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Prueba gratuita**: [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Licencia temporal**: [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Foro de soporte**: [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Última actualización:** 2026-02-22  
**Probado con:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose