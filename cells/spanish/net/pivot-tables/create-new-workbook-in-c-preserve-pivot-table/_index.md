---
category: general
date: 2026-02-15
description: Crear un nuevo libro de trabajo en C# y copiar una tabla dinámica sin
  perder su definición. Aprende cómo copiar filas, preservar la tabla dinámica y duplicar
  la tabla dinámica fácilmente.
draft: false
keywords:
- create new workbook
- copy pivot table
- preserve pivot table
- how to copy rows
- duplicate pivot table
language: es
og_description: Crear un nuevo libro de trabajo en C# y copiar una tabla dinámica
  preservando su definición. Guía paso a paso para desarrolladores.
og_title: Crear nuevo libro de trabajo en C# – Conservar tabla dinámica
tags:
- Aspose.Cells
- C#
- Excel automation
title: Crear nuevo libro de trabajo en C# – Conservar tabla dinámica
url: /es/net/pivot-tables/create-new-workbook-in-c-preserve-pivot-table/
---

see the same pivot table ready to slice and dice your data. No manual recreation required." translate.

- "## Conclusion" translate.

- Rest.

- Ensure shortcodes at end remain.

Let's craft final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Crear nuevo libro de trabajo en C# – Conservar tabla dinámica

¿Alguna vez necesitaste **crear nuevo libro de trabajo** en C# que contenga una copia exacta de una tabla dinámica de otro archivo? No eres el único. En muchos flujos de informes la tabla dinámica es el corazón del análisis, y perder su definición al mover los datos es una pesadilla.

¿La buena noticia? Con unas pocas líneas de código de Aspose.Cells puedes copiar filas—incluida la tabla dinámica—en un libro de trabajo nuevo y mantener todo intacto. A continuación verás **cómo copiar filas**, **conservar tabla dinámica** y hasta **duplicar tabla dinámica** entre archivos sin romper fórmulas ni caché.

## Qué cubre este tutorial

En esta guía repasaremos:

1. Cargar el libro de trabajo fuente que ya contiene una tabla dinámica.  
2. **Crear nuevo libro de trabajo** para el destino.  
3. Usar `CopyRows` para transferir el rango que contiene la tabla dinámica.  
4. Guardar el resultado asegurando que la tabla dinámica siga funcional.  

No se requiere documentación externa—solo el código, el porqué y algunos consejos prácticos que puedes pegar directamente en tu proyecto.

> **Consejo profesional:** Aspose.Cells funciona con .NET Core, .NET Framework e incluso Xamarin, así que el mismo fragmento se ejecuta donde lo necesites.

---

![Crear nuevo libro de trabajo con tabla dinámica copiada](/images/create-new-workbook-pivot.png "crear nuevo libro de trabajo con tabla dinámica copiada")

## Paso 1 – Crear nuevo libro de trabajo y cargar el archivo fuente

Lo primero que hacemos es **crear nuevo libro de trabajo**. Uno contiene los datos originales, el otro recibirá el rango copiado.

```csharp
using Aspose.Cells;

// Load the source workbook that already contains a pivot table
var sourceWorkbook = new Workbook(@"C:\Data\source.xlsx");

// Create an empty workbook that will become the destination
var destinationWorkbook = new Workbook();
```

*Por qué esto importa:*  
`Workbook` es el punto de entrada para cualquier manipulación de Excel en Aspose.Cells. Al instanciar un libro de trabajo nuevo garantizamos una pizarra limpia—sin estilos ocultos ni hojas de cálculo extra que puedan interferir después.

## Paso 2 – Cómo copiar filas incluyendo una tabla dinámica

Ahora llega el núcleo del problema: **cómo copiar filas** que encapsulan la tabla dinámica sin aplanarla. El método `CopyRows` hace exactamente eso.

```csharp
// Copy the first 20 rows (adjust as needed) from the source to the destination
// Parameters: startRow, totalRows, targetCells, targetStartRow
sourceWorkbook.Worksheets[0].Cells.CopyRows(
    startRow: 0,
    totalRows: 20,
    targetCells: destinationWorkbook.Worksheets[0].Cells,
    targetStartRow: 0);
```

Algunas cosas a tener en cuenta:

* `startRow` y `totalRows` definen el bloque que contiene la tabla dinámica.  
* El método copia **ambos**, datos sin procesar y la caché de la tabla dinámica, de modo que el libro de trabajo de destino sepa cómo reconstruir la tabla dinámica al vuelo.  
* Si tu tabla dinámica comienza más abajo en la hoja, solo cambia los índices—no necesitas una llamada API diferente.

> **Pregunta frecuente:** *¿Perderá la tabla dinámica copiada la referencia a sus datos de origen?*  
> No. Aspose.Cells incrusta la caché directamente en la hoja de cálculo, por lo que la tabla dinámica queda autosuficiente en el nuevo archivo.

## Paso 3 – Conservar tabla dinámica al guardar el destino

Después de copiar las filas, la tabla dinámica vive en el libro de trabajo de destino exactamente como estaba en el origen. Guardar el archivo es sencillo.

```csharp
// Save the destination workbook; the pivot table remains functional
destinationWorkbook.Save(@"C:\Data\destination.xlsx");
```

Al abrir `destination.xlsx` en Excel, verás la tabla dinámica lista para actualizarse. El comportamiento de **conservar tabla dinámica** es automático porque la caché viajó con las filas.

### Verificando el resultado

Abre el archivo y:

1. Haz clic en la tabla dinámica.  
2. Observa que aparece la lista de campos—esto indica que la caché está intacta.  
3. Intenta actualizar; los datos se refrescan sin errores.

Si encuentras un error *#REF!*, verifica que el rango copiado incluya las filas de caché ocultas (normalmente justo después de los datos visibles).

## Paso 4 – Duplicar tabla dinámica en varios libros de trabajo (Opcional)

A veces necesitas la misma tabla dinámica en varios informes. El patrón que acabamos de usar escala sin problemas—simplemente repite la copia para cada nuevo libro de trabajo.

```csharp
string[] targets = {
    @"C:\Reports\Q1.xlsx",
    @"C:\Reports\Q2.xlsx",
    @"C:\Reports\Q3.xlsx"
};

foreach (var path in targets)
{
    var wb = new Workbook(); // fresh workbook each loop
    sourceWorkbook.Worksheets[0].Cells.CopyRows(0, 20, wb.Worksheets[0].Cells, 0);
    wb.Save(path);
}
```

Este fragmento **duplica tabla dinámica** tres veces con un solo bucle. Ajusta la matriz `targets` para que coincida con tu calendario de informes.

### Casos límite a tener en cuenta

| Situación | Qué observar | Solución |
|-----------|--------------|----------|
| La tabla dinámica usa una fuente de datos externa | La caché puede referenciar una conexión que no existe en la nueva máquina | Incrusta la fuente de datos o recrea la conexión en el libro de trabajo de destino |
| Tabla dinámica muy grande ( > 100 k filas ) | `CopyRows` puede consumir mucha memoria | Usa `CopyRows` en fragmentos o considera `Copy` con `PasteOptions` para limitar el uso de memoria |
| La hoja tiene filas/columnas ocultas | Las filas de caché ocultas podrían omitirse si copias solo filas visibles | Siempre copia el rango exacto de filas que contiene la caché, no solo el área visible |

## Ejemplo completo funcionando

Juntándolo todo, aquí tienes un programa autónomo que puedes colocar en una aplicación de consola.

```csharp
using System;
using Aspose.Cells;

namespace PivotCopyDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load source workbook (contains the original pivot)
            var sourcePath = @"C:\Data\source.xlsx";
            var sourceWorkbook = new Workbook(sourcePath);

            // 2️⃣ Prepare destination workbook
            var destinationWorkbook = new Workbook();

            // 3️⃣ Copy rows that include the pivot (adjust range as needed)
            sourceWorkbook.Worksheets[0].Cells.CopyRows(
                startRow: 0,
                totalRows: 20,
                targetCells: destinationWorkbook.Worksheets[0].Cells,
                targetStartRow: 0);

            // 4️⃣ Save – the pivot table is preserved
            var destPath = @"C:\Data\destination.xlsx";
            destinationWorkbook.Save(destPath);

            Console.WriteLine("Pivot table successfully copied!");
        }
    }
}
```

Ejecuta el programa, abre `destination.xlsx` y verás la misma tabla dinámica lista para segmentar y analizar tus datos. No se requiere recreación manual.

---

## Conclusión

Acabamos de mostrar cómo **crear nuevo libro de trabajo** en C# y **copiar tabla dinámica** manteniendo todas sus configuraciones. Al usar `CopyRows` obtienes una forma fiable de **conservar tabla dinámica**, responder a la eterna pregunta de “**cómo copiar filas**” y hasta **duplicar tabla dinámica** en varios informes con código mínimo.

¿Próximos pasos? Prueba cambiar el rango copiado para incluir gráficos que referencien la misma tabla dinámica, o experimenta con `PasteOptions` para retener el formato exactamente. El mismo patrón funciona para otros objetos de Aspose.Cells como tablas y rangos con nombre, así que siéntete libre de ampliarlo.

¿Tienes un caso especial—tal vez una tabla dinámica que extrae datos de una base externa, o un libro de trabajo que vive en la nube? Deja un comentario abajo y lo abordaremos juntos. ¡Feliz codificación!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}