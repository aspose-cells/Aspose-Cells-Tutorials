---
date: '2026-08-16'
description: Aprenda cómo agregar globalización en Java usando Aspose.Cells, personalice
  los mensajes de error de Excel y configure la dependencia de Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Aprenda cómo agregar globalización en Java usando Aspose.Cells, personalice
  los mensajes de error de Excel y configure la dependencia de Maven. Siga la guía
  paso a paso.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Cómo agregar globalización en Java con Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Cómo agregar globalización en Java con Aspose.Cells
url: /es/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Cómo agregar globalización en Java con Aspose.Cells

## Introducción

Agregar globalización a su libro de trabajo Java le permite presentar mensajes de error, valores booleanos y otras cadenas específicas de la configuración regional en el idioma que sus usuarios esperan. En este tutorial aprenderá **cómo agregar globalización** para ruso, pero el mismo patrón funciona para cualquier idioma. Al final de la guía podrá:

- Anular el texto de error predeterminado y las representaciones booleanas.
- Aplicar su configuración personalizada a cualquier instancia de `Workbook`.
- Integrar la solución en un proyecto Java típico basado en Maven.

¿Listo para que sus archivos Excel sean realmente multilingües? Primero verifiquemos que su entorno de desarrollo cumpla con los requisitos previos.

## Respuestas rápidas
- **¿Qué es la globalización en Aspose.Cells?** Es un conjunto de cadenas conscientes de la configuración regional (errores, booleanos, etc.) que puede reemplazar con texto personalizado.  
- **¿Qué artefacto Maven se requiere?** `com.aspose:aspose-cells:25.3`.  
- **¿Puedo dirigirme a idiomas distintos del ruso?** Sí – extienda `GlobalizationSettings` y anule los métodos necesarios para cada configuración regional.  
- **¿Necesito una licencia para el desarrollo?** Una prueba gratuita funciona para pruebas; una licencia permanente elimina las marcas de agua de evaluación.  
- **¿La solución es segura para subprocesos?** Aplique la configuración por libro de trabajo; el objeto `GlobalizationSettings` es inmutable después de su creación.

## Qué es la globalización en Aspose.Cells?

`GlobalizationSettings` es el objeto de configuración de Aspose.Cells que controla cadenas específicas de la configuración regional, como mensajes de error, valores booleanos, símbolos de moneda y patrones de fecha. Al proporcionar su propia subclase indica a la biblioteca qué texto mostrar para cada cultura, lo que le permite reemplazar las cadenas predeterminadas en inglés por traducciones que coincidan con el idioma y las convenciones regionales del usuario final.

## Por qué agregar globalización personalizada?

Aspose.Cells admite **más de 50 formatos de entrada y salida** – incluidos XLSX, CSV, PDF y ODS – y puede procesar libros de trabajo con **hasta 200 000 filas** sin cargar todo el archivo en memoria. Personalizar la globalización garantiza que los usuarios finales vean los mensajes en su idioma nativo, reduciendo los tickets de soporte en un estimado **30 %** para implementaciones multinacionales.

## Requisitos previos

- **Java Development Kit** 8 o superior.
- **IDE** como IntelliJ IDEA o Eclipse.
- **Aspose.Cells for Java** versión 25.3 (o posterior) agregado mediante Maven o Gradle.

### Configuración de Aspose.Cells para Java

Agregue la dependencia Maven a su `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

O, si prefiere Gradle, inserte lo siguiente en `build.gradle`:

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Obtención de licencia

Aspose ofrece varias opciones de licencia:

- **Prueba gratuita** – evaluación con todas las funciones durante 30 días.  
- **Licencia temporal** – evaluación ilimitada sin marcas de agua.  
- **Licencia comercial** – lista para producción, con soporte prioritario.

Después de obtener un archivo de licencia, configúrelo una sola vez al iniciar la aplicación:

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Cómo agregar globalización para ruso?

Un objeto `Workbook` representa un archivo Excel cargado en memoria, proporcionando acceso a sus hojas, celdas y configuraciones. Cargue su libro de trabajo, cree una subclase de `GlobalizationSettings` y asígnela al libro. La respuesta directa es: **instanciar una clase personalizada `GlobalizationSettings`, anular `getErrorValueString` y `getBooleanValueString`, y luego llamar a `workbook.setGlobalizationSettings(customSettings)`**. Este enfoque de dos pasos reemplaza las cadenas rusas predeterminadas por las suyas.

### Definiendo la configuración personalizada

La primera vez que mencione `GlobalizationSettings` en esta guía, observe la definición:

`GlobalizationSettings` es la clase base que Aspose.Cells usa para obtener cadenas específicas de la configuración regional.  

Ahora cree una subclase que devuelva texto específico para ruso:

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Aplicando la configuración a un libro de trabajo

Después de definir la subclase, asígnela a cualquier instancia de `Workbook`:

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Aplicaciones prácticas

- **Informes financieros** – muestre códigos de error en el idioma nativo del contable, reduciendo malentendidos.  
- **Herramientas empresariales** – incorpore la misma lógica de globalización en decenas de utilidades internas basadas en Excel.  
- **Canales de datos automatizados** – garantice que los sistemas downstream reciban valores conscientes de la configuración regional sin pasos de traducción adicionales.

## Consideraciones de rendimiento

Al habilitar la globalización personalizada, Aspose.Cells sigue procesando fórmulas y E/S con el mismo alto rendimiento. Para mantener bajo el uso de memoria:

- Libere referencias al libro de trabajo (`wb.dispose()`) después de guardar.  
- Use `CalculationOptions.setEnableIterativeCalculation(true)` solo cuando sea necesario.  
- Ajuste el heap de la JVM (`-Xmx2g`) para libros de trabajo mayores a 100 MB.

## Preguntas frecuentes

**P: ¿Puedo aplicar la misma configuración de globalización a varios libros de trabajo a la vez?**  
R: Sí. Cree una única instancia `RussianGlobalization` y pásela a cada libro mediante `setGlobalizationSettings`.

**P: ¿Qué pasa si necesito admitir un idioma que usa escritura de derecha a izquierda?**  
R: Anule métodos adicionales como `getCurrencySymbol` y `getDatePattern` en su subclase para devolver los símbolos RTL apropiados.

**P: ¿Se requiere una licencia para la versión de prueba al usar globalización personalizada?**  
R: No. La versión de prueba soporta completamente `GlobalizationSettings`; solo aparecen marcas de agua de evaluación en ciertos formatos de salida.

**P: ¿Cómo depuro cadenas de error incorrectas?**  
R: Inserte sentencias `System.out.println` dentro de sus métodos anulados para verificar que el valor de entrada `err` coincida con sus casos `switch`.

**P: ¿Esto afecta la velocidad de cálculo de fórmulas?**  
R: De manera insignificante. La biblioteca busca la cadena solo al renderizar valores de celda, no durante los pasos intermedios de cálculo.

## Recursos adicionales

- **Documentación**: Explore guías detalladas en [Aspose.Cells Documentation](https://reference.aspose.com/cells/java/)  
- **Descarga**: Acceda a las últimas versiones en [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Compra**: Adquiera una licencia para uso comercial en [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Prueba gratuita**: Comience con una prueba gratuita desde [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Licencia temporal**: Obtenga una licencia temporal a través de [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Soporte**: Obtenga ayuda de la comunidad en [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Última actualización:** 2026-08-16  
**Probado con:** Aspose.Cells 25.3 for Java  
**Autor:** Aspose

## Tutoriales relacionados

- [Aspose.Cells Java: Guía del motor de cálculo personalizado](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Cómo usar Aspose Cells – Tutoriales del motor Excel para Java](/cells/java/calculation-engine/)
- [Dependencia Maven de Aspose Cells – Gestionar conexiones de datos Excel con Aspose.Cells en Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}