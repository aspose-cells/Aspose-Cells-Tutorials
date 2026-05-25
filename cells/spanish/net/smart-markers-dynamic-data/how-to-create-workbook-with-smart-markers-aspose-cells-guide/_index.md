---
category: general
date: 2026-02-23
description: Cómo crear un libro de trabajo usando Aspose.Cells y agregar marcadores
  con una matriz JSON. Aprende cómo agregar marcadores, usar una matriz JSON y marcadores
  inteligentes de Aspose.Cells en minutos.
draft: false
keywords:
- how to create workbook
- how to add markers
- use json array
- smart markers aspose.cells
language: es
og_description: Cómo crear un libro de trabajo usando Aspose.Cells, agregar marcadores
  y usar una matriz JSON. Esta guía paso a paso te muestra todo lo que necesitas.
og_title: Cómo crear un libro de trabajo con marcadores inteligentes – Aspose.Cells
tags:
- Aspose.Cells
- C#
- Excel Automation
title: Cómo crear un libro de trabajo con marcadores inteligentes – Guía de Aspose.Cells
url: /es/net/smart-markers-dynamic-data/how-to-create-workbook-with-smart-markers-aspose-cells-guide/
---

.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cómo crear un libro de trabajo con marcadores inteligentes – Guía de Aspose.Cells

¿Alguna vez te has preguntado **cómo crear un libro de trabajo** que rellene automáticamente los datos desde una fuente JSON? No eres el único: los desarrolladores preguntan constantemente cómo agregar marcadores que extraigan valores de arreglos, especialmente al trabajar con Aspose.Cells. ¿La buena noticia? Es bastante sencillo una vez que comprendes el concepto de marcador inteligente. En este tutorial recorreremos la creación de un libro de trabajo, la adición de marcadores, el uso de un arreglo JSON y la configuración de marcadores inteligentes en Aspose.Cells para que puedas generar archivos Excel al vuelo.

Cubrirémos todo lo que necesitas saber: inicializar el libro de trabajo, construir una `MarkerCollection`, alimentar un arreglo JSON, activar la bandera “ArrayAsSingle” y, finalmente, aplicar los marcadores. Al final tendrás un programa C# completamente funcional que produce un archivo Excel con los valores **A**, **B** y **C** poblados automáticamente. Sin servicios externos, solo pura magia de Aspose.Cells.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.6+)
- Paquete NuGet Aspose.Cells for .NET (`Install-Package Aspose.Cells`)
- Conocimientos básicos de sintaxis C# (si eres nuevo, los fragmentos están muy comentados)
- Visual Studio o cualquier IDE que prefieras

Si ya cuentas con esto, genial—¡vamos al grano!

## Paso 1: Cómo crear un libro de trabajo (Inicializar el archivo Excel)

Lo primero que necesitas es un objeto de libro de trabajo vacío. Piensa en él como un lienzo en blanco que Aspose.Cells pintará más adelante con datos.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();               // creates an empty .xlsx in memory
        Worksheet worksheet = workbook.Worksheets[0];    // reference to the default sheet
```

> **Por qué es importante:** `Workbook` es el punto de entrada para cualquier operación de Excel. Sin él no puedes adjuntar marcadores inteligentes ni guardar el archivo. Crear el libro de trabajo primero también garantiza que tengas un entorno limpio para los pasos posteriores.

## Paso 2: Cómo agregar marcadores – Inicializar una colección de marcadores

Los marcadores inteligentes viven dentro de una `MarkerCollection`. Esta colección es donde defines los marcadores (los marcadores de posición) y los datos que los reemplazarán.

```csharp
        // Step 2: Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();
```

> **Consejo profesional:** Puedes reutilizar la misma `MarkerCollection` para varias hojas de cálculo, pero mantener una por hoja facilita la depuración.

## Paso 3: Usar un arreglo JSON – Agregar un marcador con datos JSON

Ahora realmente agregamos un marcador. El marcador de posición `{SmartMarker}` será reemplazado por el arreglo JSON que suministremos. El JSON debe ser una cadena que represente un arreglo, por ejemplo, `["A","B","C"]`.

```csharp
        // Step 3: Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");
```

> **Explicación:** El método `Add` recibe dos argumentos: el texto del marcador y la fuente de datos. Aquí la fuente de datos es un arreglo JSON, que Aspose.Cells puede analizar automáticamente. Este es el núcleo de **usar arreglo json** con marcadores inteligentes.

## Paso 4: Configurar el marcador – Tratar el arreglo como un solo valor

Por defecto, Aspose.Cells expande un arreglo JSON en filas separadas. Si deseas que todo el arreglo se trate como un único valor de celda (útil para listas desplegables o cadenas concatenadas), activa la bandera `ArrayAsSingle`.

```csharp
        // Step 4: Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;
```

> **Cuándo usarlo:** Si necesitas que el arreglo aparezca en una sola celda (p. ej., `"A,B,C"`), habilita esta bandera. De lo contrario, Aspose.Cells escribirá cada elemento en su propia fila.

## Paso 5: Adjuntar marcadores a la hoja y aplicarlos

Finalmente, enlaza la colección de marcadores a la hoja de cálculo y dile a Aspose.Cells que reemplace los marcadores de posición con los datos reales.

```csharp
        // Step 5: Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Optional: write the placeholder into a cell so you can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook to disk
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

> **Resultado:** Después de ejecutar el programa, `SmartMarkerResult.xlsx` contiene el valor **A** (o todo el arreglo si `ArrayAsSingle` es true) en la celda `A1`. Abre el archivo para verificar.

### Salida esperada

| A |
|---|
| A |   *(si `ArrayAsSingle` es false, el primer elemento llena la celda)*

Si estableces `ArrayAsSingle = true`, la celda `A1` contendrá la cadena `["A","B","C"]`.

## Paso 6: Cómo agregar marcadores – Escenarios avanzados (Opcional)

Quizás te preguntes, *¿qué pasa si necesito más de un marcador?* La respuesta es simple: solo llama a `Add` nuevamente.

```csharp
        smartMarkerCollection.Add("{SecondMarker}", "[{\"Name\":\"John\"},{\"Name\":\"Jane\"}]");
        // You can also control each marker individually:
        smartMarkerCollection["SecondMarker"] = false; // expand into rows
```

> **Por qué funciona:** Cada marcador opera de forma independiente, por lo que puedes mezclar “arreglo como único” y “expandir en filas” dentro de la misma hoja. Esta flexibilidad es una característica distintiva de **marcadores inteligentes aspose.cells**.

## Problemas comunes y cómo evitarlos

| Problema | Por qué ocurre | Solución |
|----------|----------------|----------|
| El marcador no se reemplaza | Texto del marcador ausente o con error tipográfico | Asegúrate de que la celda contenga exactamente la cadena del marcador (`{SmartMarker}`) |
| JSON no se analiza | Sintaxis JSON inválida (faltan comillas) | Usa un validador JSON o escapa doblemente las comillas en las cadenas C# |
| El arreglo se expande inesperadamente | `ArrayAsSingle` dejado en `false` por defecto | Establece `["ArrayAsSingle"] = true` para el marcador específico |
| Libro de trabajo guardado vacío | No se llamó a `Apply()` antes de `Save()` | Siempre llama a `worksheet.SmartMarkers.Apply()` antes de guardar |

## Ejemplo completo (Listo para copiar y pegar)

A continuación tienes el programa completo que puedes colocar en una aplicación de consola. No se requieren archivos adicionales.

```csharp
using System;
using Aspose.Cells;

class SmartMarkerDemo
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Initialise a collection for smart markers
        MarkerCollection smartMarkerCollection = new MarkerCollection();

        // Add a smart marker and provide replacement data (JSON array)
        smartMarkerCollection.Add("{SmartMarker}", "[\"A\",\"B\",\"C\"]");

        // Configure the marker to treat the array as a single value
        smartMarkerCollection["ArrayAsSingle"] = true;

        // Attach the marker collection to the worksheet and apply it
        worksheet.SmartMarkers.Add(smartMarkerCollection);
        worksheet.SmartMarkers.Apply();

        // Place the marker in a cell so we can see the replacement
        worksheet.Cells["A1"].PutValue("{SmartMarker}");

        // Save the workbook
        workbook.Save("SmartMarkerResult.xlsx");
        Console.WriteLine("Workbook created successfully!");
    }
}
```

Ejecuta el programa, abre `SmartMarkerResult.xlsx` y verás el arreglo JSON (o su primer elemento) colocado ordenadamente en la celda **A1**.

## Próximos pasos: Extender la solución

Ahora que sabes **cómo crear un libro de trabajo**, **cómo agregar marcadores** y **usar arreglo json** con Aspose.Cells, considera estas ideas de seguimiento:

1. **Múltiples hojas** – Recorre una lista de hojas y adjunta diferentes colecciones de marcadores a cada una.
2. **JSON dinámico** – Obtén JSON de una API web (`HttpClient`) y pásalo directamente a `smartMarkerCollection.Add`.
3. **Estilizar la salida** – Después de aplicar los marcadores, formatea celdas (fuentes, colores) para que el informe luzca pulido.
4. **Formatos de exportación** – Guarda el libro como PDF, CSV o HTML cambiando `workbook.Save("file.pdf")`.

Cada uno de estos temas involucra naturalmente **marcadores inteligentes aspose.cells**, así que estarás ampliando los mismos conceptos centrales que acabas de aprender.

## Conclusión

Hemos recorrido **cómo crear un libro de trabajo** desde cero, **cómo agregar marcadores** y cómo **usar arreglo json** con los marcadores inteligentes de Aspose.Cells. El ejemplo completo y ejecutable muestra todo el flujo de trabajo, desde la inicialización del `Workbook` hasta el guardado del archivo final. Al alternar la bandera `ArrayAsSingle` obtienes un control granular sobre cómo aparecen los datos JSON en Excel, lo que hace que la solución sea adaptable a una amplia gama de escenarios de generación de informes.

Prueba el código, modifica el JSON y experimenta con marcadores adicionales. Cuando domines estos bloques de construcción, generar informes Excel sofisticados será pan comido. ¿Tienes preguntas o quieres compartir un caso de uso interesante? Deja un comentario abajo—¡feliz codificación!

![Diagrama que muestra cómo crear un libro de trabajo con marcadores inteligentes en Aspose.Cells](https://example.com/images/create-workbook-smart-markers.png "cómo crear un libro de trabajo con marcadores inteligentes de Aspose.Cells")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}