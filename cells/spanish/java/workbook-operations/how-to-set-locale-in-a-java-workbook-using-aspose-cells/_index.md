---
category: general
date: 2026-11-22
description: Aprende cómo establecer la configuración regional en un libro de trabajo
  Java, cambiar el idioma del libro de trabajo y configurar el calendario en japonés
  con ejemplos de código claros.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: es
lastmod: 2026-11-22
og_description: Cómo establecer la configuración regional en un libro de trabajo Java
  rápidamente. Sigue este tutorial para cambiar el idioma del libro, establecer la
  configuración regional a japonés y configurar el calendario japonés.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Cómo establecer la configuración regional en un libro de Java – guía paso
  a paso
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: Cómo establecer la configuración regional en un libro de trabajo Java usando
  Aspose.Cells
url: /es/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo establecer la configuración regional en un libro de Java usando Aspose.Cells

Establecer la configuración regional en un libro de Java es un requisito común cuando necesita adaptar su hoja de cálculo a diferentes regiones. En esta guía aprenderá cómo establecer la configuración regional, cambiar el idioma del libro y establecer el calendario a japonés usando la API de Aspose.Cells.

Internacionalizar un libro va más allá de traducir texto; también influye en los formatos de número, el análisis de fechas y el sistema de calendario predeterminado. Al final de este tutorial podrá:

* Configurar la configuración regional del libro a japonés (Japón) – **set locale to japanese**.  
* Cambiar el idioma del libro para que las fórmulas y cadenas de la interfaz respeten la cultura objetivo – **change workbook language**.  
* Cambiar el calendario al calendario imperial japonés – **how to set calendar**.  

Los pasos funcionan con cualquier versión reciente de Aspose.Cells para Java (v23.9 o posterior) y solo requieren un entorno de desarrollo Java estándar.

## Requisitos previos

| Requisito | Razón |
|-------------|--------|
| Java 8 o superior | La biblioteca está dirigida a Java 8+. |
| Aspose.Cells for Java (v23.9+) | Proporciona `Workbook`, `WorkbookSettings` y utilidades de configuración regional. |
| IDE (IntelliJ IDEA, Eclipse, or VS Code) | Para compilar y ejecutar el ejemplo. |
| Conocimientos básicos de Java | Necesario para comprender los fragmentos de código. |

Agregue la dependencia de Aspose.Cells Maven a su `pom.xml` (o descargue el JAR manualmente):

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Cómo establecer la configuración regional y el calendario en un libro

El primer paso es crear una instancia de workbook y obtener su objeto de configuración. El objeto de configuración expone las API de configuración regional y calendario.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Por qué cada línea es importante

* **`new Workbook()`** – Instancia un workbook vacío que puede manipular antes de guardarlo.  
* **`getSettings()`** – Devuelve un objeto `WorkbookSettings`; todas las opciones regionales se encuentran aquí.  
* **`setCalendar(...)`** – Reemplaza el calendario gregoriano predeterminado con el calendario imperial japonés, afectando cómo se renderizan y analizan las fechas.  
* **`setLocale(new Locale("ja","JP"))`** – Cambia el idioma y las convenciones regionales (p.ej., meses, separadores decimales). Este es el núcleo de **how to set locale** para el workbook.  

Ejecutar el programa crea `LocaleDemo.xlsx`. Ábralo en Excel o LibreOffice y verá nombres de meses en japonés, símbolos de moneda Yen japonés y fechas formateadas según el calendario japonés.

## Cambiar el idioma del libro (establecer configuración regional a japonés)

Si su objetivo principal es **cambiar el idioma del libro**, puede centrarse solo en la llamada `setLocale`. El siguiente fragmento aísla ese paso:

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**¿Qué cambia?**  
* Las cadenas de formato de celda cambian a japonés (p.ej., `#,##0.00` se convierte en `#,##0.00` con un símbolo de yen).  
* Los nombres de funciones incorporadas (como `SUM`) permanecen en inglés porque la configuración regional de funciones de Excel es independiente, pero las cadenas de fecha y los mensajes de error siguen las convenciones japonesas.  

**¿Cuándo usar esto?**  
* Cuando necesita una hoja de cálculo que muestre números y fechas para una audiencia japonesa pero el calendario subyacente puede permanecer gregoriano.  
* Para informes que se exportan a PDF o se imprimen, asegurando que el idioma visual coincida con el mercado objetivo.

## Cómo establecer el calendario al calendario japonés

A veces el requisito de **how to set calendar** es independiente de la configuración regional. Para sistemas heredados que almacenan fechas en la era imperial japonesa, debe establecer explícitamente el calendario mientras opcionalmente mantiene la configuración regional predeterminada.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Puntos clave:**

* `Calendar.getInstance(Locale.JAPAN)` devuelve un `java.util.Calendar` configurado para la era japonesa.  
* El workbook ahora renderizará fechas usando símbolos de era (R para Reiwa, H para Heisei, etc.).  
* Esta configuración **no** afecta el formato de número ni el idioma de la interfaz; combínela con `setLocale` si necesita ambos.

## Ejemplo completo de extremo a extremo

A continuación se muestra un programa completo y ejecutable que demuestra **how to set locale**, **change workbook language** y **set the calendar** en un flujo cohesivo. También agrega una celda de ejemplo para ilustrar el efecto.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Salida esperada:**  
Al abrir `FullJapaneseLocale.xlsx` se muestra la primera celda con una fecha como `R3/04/01` (Reiwa 3) y la segunda celda formateada como `¥1,234,567.89`. Esto confirma que **how to set locale**, **change workbook language** y **how to set calendar** funcionan juntos.

## Errores comunes y cómo evitarlos

| Error | Por qué ocurre | Solución |
|---------|----------------|-----|
| Usar `Locale.CHINA` en lugar de `new Locale("ja","JP")` | `Locale.CHINA` establece el idioma chino, no japonés. | Siempre instancie `Locale` con `"ja", "JP"` para japonés. |
| Olvidar llamar a `settings.setCalendar(...)` después de `setLocale` | El calendario predeterminado es gregoriano, por lo que las fechas aparecen en la era incorrecta. | Llame a `setCalendar` **después** de establecer la configuración regional, o establezca ambos juntos como se muestra. |
| Guardar el workbook antes de aplicar la configuración | Las configuraciones se aplican al objeto en memoria; guardar temprano escribe la configuración regional predeterminada. | Aplique todos los cambios de configuración regional/calendario **antes** de llamar a `workbook.save()`. |
| Usar una versión desactualizada de Aspose.Cells | Las versiones anteriores carecen de sobrecargas `setCalendar`. | Actualice a v23.9+ o revise las notas de la versión para soporte de configuración regional. |

## Probando su configuración

1. Ejecute la clase **FullLocaleExample**.  
2. Abra el `FullJapaneseLocale.xlsx` generado en Excel.  
3. Verifique que:  
   * La columna de fechas muestra símbolos de era japoneses (`R`, `H`, etc.).  
   * La columna de números usa el símbolo Yen y separadores de coma.  
   * Cualquier mensaje de error incorporado (p.ej., `#DIV/0!`) aparezca en japonés si el workbook contiene errores.  

Si alguna de estas verificaciones falla, verifique nuevamente que el objeto `WorkbookSettings` que modificó sea la misma instancia utilizada al guardar.

## Próximos pasos

* **Localizar fórmulas** – Aunque la configuración regional controla el formato, también puede traducir nombres de funciones personalizadas usando `FormulaParser`.  
* **Aplicar configuración regional a libros existentes** – Cargue un libro con `new Workbook

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que se basan en las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y funcionales con explicaciones paso a paso para ayudarle a dominar funciones adicionales de la API y explorar enfoques de implementación alternativos en sus propios proyectos.

- [Formato de fecha de Aspose Cells: Cómo establecer un formato de fecha personalizado en Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [Cómo establecer el idioma en archivos de Excel usando Aspose.Cells .NET para soporte multilingüe](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [Cómo establecer el formato numérico de celda y convertir fechas japonesas en C# usando Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}