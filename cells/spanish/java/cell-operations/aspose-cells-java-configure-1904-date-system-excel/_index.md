---
date: '2026-02-22'
description: Aprende cómo cambiar el sistema de fechas de Excel a 1904 usando Aspose.Cells
  para Java, establecer el formato de fecha de Excel y convertir el sistema 1904 de
  Excel de manera eficiente.
keywords:
- 1904 date system Excel
- Aspose.Cells Java configuration
- Excel workbook manipulation
title: Cambiar el sistema de fechas de Excel a 1904 con Aspose.Cells Java
url: /es/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cambiar el sistema de fechas de Excel a 1904 con Aspose.Cells Java

Gestionar datos históricos en Excel puede ser un desafío porque Excel admite dos sistemas de fechas diferentes. **En este tutorial aprenderás cómo cambiar el sistema de fechas de Excel al formato 1904 usando Aspose.Cells para Java**, lo que hace que el manejo de fechas heredadas sea sencillo. Repasaremos la inicialización de un libro, la activación del sistema de fechas 1904 y la persistencia del cambio.

## Respuestas rápidas
- **¿Qué hace el sistema de fechas 1904?** Comienza a contar los días a partir del 1 de enero de 1904, desplazando todas las fechas 1462 días respecto al sistema predeterminado de 1900.  
- **¿Por qué usar Aspose.Cells para cambiar el sistema de fechas?** Proporciona una API simple que funciona sin necesidad de tener Excel instalado y admite archivos grandes.  
- **¿Qué versiones de Java son compatibles?** JDK 8 o superior.  
- **¿Necesito una licencia?** Una prueba gratuita sirve para evaluación; una licencia elimina los límites de uso.  
- **¿Puedo volver al sistema 1900 más tarde?** Sí, solo establece `setDate1904(false)`.

## ¿Qué es el sistema de fechas 1904 en Excel?
El sistema de fechas 1904 se utilizó originalmente en las primeras versiones de Excel para Macintosh. Cuenta los días a partir del 1 de enero de 1904, lo que resulta útil para la compatibilidad con hojas de cálculo antiguas y algunos modelos financieros.

## ¿Por qué cambiar el sistema de fechas de Excel con Aspose.Cells?
- **Compatibilidad multiplataforma** – funciona en Windows, Linux y macOS.  
- **No se requiere instalación de Excel** – ideal para procesamiento del lado del servidor.  
- **Alto rendimiento** – maneja libros grandes con un consumo mínimo de memoria.  

## Requisitos previos
- Java Development Kit (JDK) 8 o superior.  
- Maven o Gradle para la gestión de dependencias.  
- Conocimientos básicos de programación en Java.  

## Configuración de Aspose.Cells para Java

### Maven
Agrega la siguiente dependencia a tu archivo `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Incluye esta línea en tu archivo `build.gradle`:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Adquisición de licencia
Aspose ofrece una prueba gratuita, licencia temporal y licencias comerciales completas. Puedes comenzar con la [prueba gratuita](https://releases.aspose.com/cells/java/) o obtener una licencia temporal desde la [página de licencia temporal](https://purchase.aspose.com/temporary-license/).

## Cambiar el sistema de fechas de Excel usando Aspose.Cells Java

A continuación se muestra la guía paso a paso que realmente **cambia el sistema de fechas de Excel**. Cada paso incluye una breve explicación seguida del código exacto que necesitas.

### Paso 1: Inicializar y cargar el libro
Primero, crea una instancia de `Workbook` que apunte a tu archivo Excel existente.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Paso 2: Habilitar el sistema de fechas 1904
Utiliza la configuración del libro para cambiar el sistema de fechas.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Consejo:** También puedes llamar a `setDate1904(false)` más adelante si necesitas revertir el cambio.

### Paso 3: Guardar el libro modificado
Finalmente, escribe los cambios en un nuevo archivo (o sobrescribe el original).

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

> **Nota:** El código anterior usa el nombre de clase `tWorkbook` tal como se proporcionó originalmente. Asegúrate de que este error tipográfico coincida con las convenciones de nombres de tu proyecto o corrígelo a `Workbook` si es necesario.

## Establecer la fecha de Excel programáticamente (palabra clave secundaria)
Si necesitas ajustar valores de celdas individuales después de cambiar el sistema, puedes usar `Cells.get(i, j).putValue(Date)` donde la fecha se interpretará según el sistema de fechas activo.

## Convertir el sistema 1904 de Excel de nuevo a 1900 (palabra clave secundaria)
Para revertir, simplemente llama:

```java
workbook.getSettings().setDate1904(false);
```

Luego guarda el libro nuevamente.

## Aplicaciones prácticas
1. **Archivado de datos** – Conserva marcas de tiempo heredadas al migrar hojas de cálculo antiguas de Mac.  
2. **Informes multiplataforma** – Genera informes que pueden abrirse tanto en Windows como en macOS sin desajustes de fechas.  
3. **Modelado financiero** – Alinea los cálculos de fechas con modelos financieros heredados que esperan el sistema 1904.

## Consideraciones de rendimiento
- Limita las operaciones del libro en una sola sesión para mantener bajo el uso de memoria.  
- Utiliza la afinación de la recolección de basura de Java para archivos muy grandes.  

## Preguntas frecuentes

**P: ¿Cuál es la diferencia entre los sistemas de fechas 1900 y 1904?**  
R: El sistema 1900 comienza el 1 de enero de 1900, mientras que el sistema 1904 comienza el 1 de enero de 1904, desplazando todas las fechas 1462 días.

**P: ¿Puedo cambiar el sistema de fechas de un libro que está abierto en Excel?**  
R: Sí, pero debes cerrar el archivo en Excel primero; de lo contrario, la operación de guardado fallará.

**P: ¿Necesito una licencia para usar `setDate1904`?**  
R: El método funciona en la prueba gratuita, pero una licencia completa elimina las limitaciones de evaluación.

**P: ¿Es posible cambiar el sistema de fechas solo para una hoja de cálculo?**  
R: No, el sistema de fechas es una configuración a nivel de libro; se aplica a todas las hojas.

**P: ¿Cómo puedo verificar que el sistema de fechas se haya cambiado?**  
R: Abre el archivo guardado en Excel, ve a **Archivo → Opciones → Avanzado**, y marca la casilla **"Usar sistema de fechas 1904"**.

## Conclusión
Ahora sabes cómo **cambiar el sistema de fechas de Excel** a 1904 usando Aspose.Cells para Java, cómo establecer formatos de fecha en Excel y cómo volver atrás si es necesario. Incorpora estos fragmentos en tus flujos de procesamiento de datos para garantizar la compatibilidad de fechas entre plataformas.

---

**Última actualización:** 2026-02-22  
**Probado con:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose  

**Recursos**
- **Documentación:** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Descarga:** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Comprar licencia:** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Prueba gratuita:** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Licencia temporal:** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Foro de soporte:** [Aspose Support](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}