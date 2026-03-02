---
category: general
date: 2026-03-01
description: 'Cómo crear un libro de trabajo en C# rápidamente: aprende a escribir
  valores en una celda, establecer el formato numérico de la celda y formatear el
  número de la celda con pasos simples.'
draft: false
keywords:
- how to create workbook
- write value to cell
- format cell number
- set cell number format
- how to write cell
language: es
og_description: ¿Cómo crear un libro de trabajo en C#? Esta guía te muestra cómo escribir
  un valor en una celda, establecer el formato numérico de la celda y formatear el
  número de la celda en solo unas pocas líneas de código.
og_title: Cómo crear un libro de trabajo en C# – Escribir valores y formatear números
tags:
- C#
- Aspose.Cells
- Excel Automation
title: Cómo crear un libro de trabajo en C# – Escribir valores y formatear números
url: /es/net/excel-workbook/how-to-create-workbook-in-c-write-value-format-number/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un libro de trabajo en C# – Escribir valor y formatear número

Crear un libro de trabajo en C# es una tarea común cuando necesitas generar archivos Excel al vuelo. En esta guía te mostraremos cómo escribir un valor en una celda y formatear el número de la celda para que la hoja final tenga un aspecto pulido.

Si alguna vez has mirado una hoja de cálculo en blanco y te has preguntado por qué los números aparecen con demasiados decimales, no estás solo. Cubriremos todo, desde la inicialización del objeto workbook hasta la configuración de un formato numérico personalizado, y añadiremos algunos consejos para casos límite que podrías encontrar más adelante.

## Lo que aprenderás

- **Inicializar** una nueva instancia de `Workbook`.  
- **Escribir valor en la celda** usando el método `PutValue`.  
- **Establecer el formato numérico de la celda** con un objeto `Style`, logrando una visualización limpia de dos dígitos.  
- Verificar el resultado leyendo la celda de nuevo o abriendo el archivo en Excel.  

No se requieren bibliotecas externas más allá de Aspose.Cells (o cualquier API similar) y el código funciona en .NET 6+ sin configuración adicional.

---

## Cómo crear un libro de trabajo – Inicializar el objeto

Lo primero: necesitas un objeto workbook que contenga tus hojas. Piensa en el `Workbook` como todo el archivo Excel, mientras que cada `Worksheet` es una sola pestaña.

```csharp
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

*Por qué es importante:* Crear el workbook asigna las estructuras internas que luego contendrán filas, columnas y formatos. Sin este objeto, no hay ningún lugar donde escribir un valor en una celda.

> **Consejo profesional:** Si planeas trabajar con un archivo existente, reemplaza `new Workbook()` por `new Workbook("template.xlsx")` para cargar una plantilla y conservar sus estilos.

## Escribir valor en la celda

Ahora que tenemos un workbook, vamos a colocar un número en la celda **A1** de la primera hoja.

```csharp
// Step 2: Access cell A1 in the first worksheet
Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

// Step 3: Insert a numeric value into the cell
cellA1.PutValue(123.456789);
```

*Por qué usamos `PutValue`*: Este método detecta automáticamente el tipo de datos, por lo que no tienes que convertir o castear manualmente. También respeta el estilo existente de la celda, lo cual es útil cuando después **estableces el formato numérico de la celda**.

### Verificación rápida

Si lees la celda de nuevo, verás el valor bruto:

```csharp
double raw = cellA1.DoubleValue; // raw == 123.456789
```

Ese es el número antes de que se aplique cualquier formato.

## Establecer el formato numérico de la celda

Mostrar un double crudo con muchos decimales no siempre es amigable para el usuario. Limitémoslo a dos dígitos significativos.

```csharp
// Step 4: Apply a style that formats the number with two significant digits
cellA1.SetStyle(new Style() { Number = 2 });
```

La propiedad `Number` corresponde a los IDs de formatos numéricos incorporados de Excel. `2` significa “Número con dos decimales”. Si necesitas un formato diferente —por ejemplo, moneda o una fecha— usarías otro ID o una cadena de formato personalizada.

### Alternativa: cadena de formato personalizada

```csharp
Style customStyle = workbook.CreateStyle();
customStyle.Custom = "#,##0.00"; // forces two decimals with thousand separator
cellA1.SetStyle(customStyle);
```

*¿Por qué elegir un estilo personalizado?* Te brinda control total, especialmente cuando los IDs incorporados no cubren tus configuraciones regionales.

## Verificar la salida (Opcional pero recomendado)

Después de aplicar el estilo, puedes guardar el workbook y abrirlo en Excel para confirmar la apariencia.

```csharp
// Save the workbook to a file
workbook.Save("FormattedWorkbook.xlsx");

// Or, for quick verification in code:
string displayed = cellA1.StringValue; // "123.46"
Console.WriteLine($"Displayed value: {displayed}");
```

Deberías ver **123.46** en la celda A1 —exactamente dos decimales, gracias al formato que establecimos.

---

### Ejemplo completo funcional

Juntándolo todo, aquí tienes un programa autónomo que puedes copiar y pegar en una aplicación de consola.

```csharp
using System;
using Aspose.Cells;   // Ensure you have the Aspose.Cells NuGet package

class Program
{
    static void Main()
    {
        // Initialize the workbook
        Workbook workbook = new Workbook();

        // Access the first worksheet and cell A1
        Cell cellA1 = workbook.Worksheets[0].Cells["A1"];

        // Write a numeric value
        cellA1.PutValue(123.456789);

        // Apply a two‑decimal number format
        cellA1.SetStyle(new Style() { Number = 2 });

        // Save to disk (optional)
        workbook.Save("FormattedWorkbook.xlsx");

        // Output the displayed text for verification
        Console.WriteLine($"Cell A1 shows: {cellA1.StringValue}");
    }
}
```

**Salida esperada al ejecutar el programa:**

```
Cell A1 shows: 123.46
```

Abre `FormattedWorkbook.xlsx` en Excel y verás el mismo valor formateado.

---

## Variaciones comunes y casos límite

### 1. Diferentes formatos numéricos

| Objetivo | ID de formato | Fragmento de código |
|----------|---------------|----------------------|
| Moneda (dos decimales) | 5 | `cellA1.SetStyle(new Style() { Number = 5 });` |
| Porcentaje (sin decimales) | 10 | `cellA1.SetStyle(new Style() { Number = 10 });` |
| Notación científica | 11 | `cellA1.SetStyle(new Style() { Number = 11 });` |

Si ninguno de los IDs incorporados se ajusta, recurre a una cadena personalizada como se mostró antes.

### 2. Separadores decimales específicos de la cultura

Algunas configuraciones regionales usan comas para los decimales. Puedes imponer un formato sensible a la cultura:

```csharp
Style cultureStyle = workbook.CreateStyle();
cultureStyle.Custom = "#,##0.00"; // works for most European locales
cellA1.SetStyle(cultureStyle);
```

### 3. Escribir texto en lugar de números

Cuando necesites **cómo escribir en la celda** con una cadena, simplemente pasa un string a `PutValue`:

```csharp
cellA1.PutValue("Total Revenue");
```

No se requiere formato numérico, pero aún puedes aplicar estilos de fuente.

### 4. Conjuntos de datos grandes

Si estás poblando miles de filas, la inserción por lotes (`Cells.ImportArray`) es más rápida que iterar con `PutValue`. El enfoque de formato sigue siendo el mismo; solo aplicas el estilo a un rango:

```csharp
Range range = workbook.Worksheets[0].Cells.CreateRange("B2:B1001");
range.ApplyStyle(new Style() { Number = 2 });
```

---

## Preguntas frecuentes

**P: ¿Esto funciona con .NET Core?**  
R: Absolutamente. Aspose.Cells soporta .NET Standard 2.0 y versiones posteriores, por lo que puedes dirigirte a .NET 5, .NET 6 o .NET 7 sin cambios.

**P: ¿Qué pasa si necesito más de dos decimales?**  
R: Cambia la propiedad `Number` al ID incorporado correspondiente (por ejemplo, `3` para tres decimales) o ajusta la cadena de formato personalizada (`"#,##0.000"`).

**P: ¿Puedo aplicar el formato a una columna completa de una sola vez?**  
R: Sí. Usa `Cells["A:A"]` para obtener toda la columna y luego `SetStyle`.

---

## Conclusión

Ahora sabes **cómo crear objetos workbook** en C#, **escribir valor en la celda**, y **establecer el formato numérico de la celda** para que los números aparezcan exactamente como deseas. Al dominar estos conceptos básicos estarás preparado para generar informes Excel profesionales, facturas o exportaciones de datos con un esfuerzo mínimo.

A continuación, podrías explorar **formatear número de celda** para fechas, porcentajes o formato condicional—cada uno se basa en los mismos principios que cubrimos. Sumérgete en la documentación de Aspose.Cells para opciones de estilo más avanzadas, o prueba combinar varias hojas en un solo workbook para informes más ricos.

¡Feliz codificación, y recuerda: una hoja de cálculo bien formateada es solo

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}