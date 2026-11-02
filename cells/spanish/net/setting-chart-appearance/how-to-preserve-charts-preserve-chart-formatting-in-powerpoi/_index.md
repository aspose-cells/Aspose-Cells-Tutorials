---
category: general
date: 2026-07-03
description: Cómo conservar los gráficos manteniendo el formato de los gráficos usando
  Aspose.Slides en C#. Sigue esta guía paso a paso.
draft: false
keywords:
- how to preserve charts
- preserve chart formatting
language: es
og_description: Cómo preservar gráficos y mantener el formato de los gráficos con
  Aspose.Slides en C#. Guía completa con código.
og_title: Cómo preservar gráficos – preservar el formato de los gráficos en PowerPoint
  (C#)
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  headline: how to preserve charts – preserve chart formatting in PowerPoint C#
  type: TechArticle
- description: how to preserve charts while keeping preserve chart formatting using
    Aspose.Slides in C#. Follow this step‑by‑step guide.
  name: how to preserve charts – preserve chart formatting in PowerPoint C#
  steps:
  - name: Open `EditableCharts.pptx` in PowerPoint.
    text: Open `EditableCharts.pptx` in PowerPoint.
  - name: Click any chart → “Edit Data”.
    text: Click any chart → “Edit Data”.
  - name: The Excel‑like data sheet should appear, letting you modify series values.
    text: The Excel‑like data sheet should appear, letting you modify series values.
  type: HowTo
- questions:
  - answer: Directly no—`ExportEditableObjects` only applies to the PPTX format. Convert
      first, then export.
    question: Does this work with PowerPoint 2003 (PPT) files?
  - answer: Absolutely. The same `ExportEditableObjects` flag keeps SmartArt, tables,
      and diagrams editable.
    question: Can I preserve other objects like SmartArt?
  - answer: 'The slide size is stored in the presentation metadata and isn’t affected
      by these options. No extra code needed. --- ## Next steps – keep the momentum
      Now that you’ve nailed **how to preserve charts**, try exploring: - **preserve
      chart formatting** for specific chart types (e.g., stacked bar vs. rad'
    question: What if I need to keep the original slide size?
  type: FAQPage
tags:
- Aspose.Slides
- C#
- PowerPoint
- chart automation
title: cómo preservar gráficos – preservar el formato de los gráficos en PowerPoint
  C#
url: /es/net/setting-chart-appearance/how-to-preserve-charts-preserve-chart-formatting-in-powerpoi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo preservar gráficos – conservar el formato de los gráficos en PowerPoint C#

¿Alguna vez te has preguntado **cómo preservar gráficos** cuando necesitas exportar o manipular un archivo PowerPoint de forma programática? Tal vez intentaste un guardado rápido y el gráfico se convirtió en una imagen estática, rompiendo la editabilidad que esperabas.

En este tutorial te mostraremos **cómo preservar gráficos** **y** mantener su **preserve chart formatting** intacto usando Aspose.Slides para .NET. Al final tendrás un fragmento de C# listo para ejecutar que produce un PPTX donde cada gráfico sigue siendo un objeto OOXML editable—no más imágenes aplanadas.

## Qué aprenderás

- Los pasos exactos para cargar una presentación, configurar las opciones de exportación y guardar **preservando el formato de los gráficos**.  
- Por qué la bandera `ExportEditableObjects` es importante y cómo evita que los gráficos se rastericen.  
- Trampas comunes (p. ej., formatos PPT antiguos, fuentes faltantes) y soluciones rápidas.  

No se requiere experiencia previa con Aspose; solo una configuración básica de C# y un archivo PowerPoint que quieras mantener amigable con los gráficos.

## Requisitos previos

- .NET 6.0 o posterior (el código también funciona con .NET Framework 4.7+).  
- Paquete NuGet Aspose.Slides para .NET (`Install-Package Aspose.Slides.NET`).  
- Un archivo de ejemplo `input.pptx` que contenga al menos un gráfico.  
- Visual Studio, Rider o cualquier editor que prefieras.

---

## Paso 1: Instalar Aspose.Slides y crear un nuevo proyecto de consola

Para comenzar, crea una aplicación de consola nueva e incluye la biblioteca:

```bash
dotnet new console -n PreserveChartsDemo
cd PreserveChartsDemo
dotnet add package Aspose.Slides.NET
```

> **Consejo profesional:** Si estás detrás de un proxy corporativo, agrega la bandera `--no-restore` y restaura más tarde con la configuración de tu proxy.

## Paso 2: Cargar la presentación de origen – el primer lugar para aplicar **cómo preservar gráficos**

Abre tu archivo PPTX usando la clase `Presentation`. Aquí es donde realmente comienza el viaje para **cómo preservar gráficos**.

```csharp
using Aspose.Slides;
using Aspose.Slides.Export;

namespace PreserveChartsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Load the source presentation
            // Replace the path with the location of your PPTX that contains charts.
            Presentation pres = new Presentation(@"YOUR_DIRECTORY\input.pptx");
```

Observa que aún no hemos tocado ningún objeto de gráfico—es intencional. Cargar el archivo tal cual garantiza que conservemos la estructura XML original, lo cual es crucial para **preserve chart formatting** más adelante.

## Paso 3: Configurar las opciones de exportación – el corazón de **cómo preservar gráficos**

Aspose.Slides ofrece la clase `PresentationExportOptions`. Establecer `ExportEditableObjects` a `true` indica al motor que mantenga gráficos, tablas y SmartArt como partes OOXML nativas en lugar de aplanarlas.

```csharp
            // Step 3: Configure export options to keep objects editable
            PresentationExportOptions exportOptions = new PresentationExportOptions
            {
                // This flag is the key to how to preserve charts.
                ExportEditableObjects = true
            };
```

¿Por qué funciona esto? Cuando `ExportEditableObjects` es `false` (valor predeterminado), la biblioteca rasteriza objetos complejos por compatibilidad, lo que destruye **preserve chart formatting**. Activarlo preserva el XML original del gráfico, permitiendo que los usuarios finales abran el PPTX y sigan editando los datos del gráfico.

## Paso 4: Guardar la presentación usando las opciones configuradas

Ahora escribimos el archivo de salida. La sobrecarga `Save` que acepta `SaveFormat` y `exportOptions` garantiza que el gráfico permanezca editable.

```csharp
            // Step 4: Save the presentation with the configured options
            pres.Save(@"YOUR_DIRECTORY\EditableCharts.pptx", SaveFormat.Pptx, exportOptions);

            // Optional: Inform the user
            Console.WriteLine("Presentation saved with editable charts at: YOUR_DIRECTORY\\EditableCharts.pptx");
        }
    }
}
```

Ejecutar este programa produce `EditableCharts.pptx`. Ábrelo en PowerPoint, haz clic derecho en un gráfico y verás la opción habitual “Edit Data”, prueba de que hemos dominado **cómo preservar gráficos** y **preserve chart formatting**.

## Paso 5: Verificar el resultado y solucionar problemas comunes

### Verificar

1. Abre `EditableCharts.pptx` en PowerPoint.  
2. Haz clic en cualquier gráfico → “Edit Data”.  
3. Debería aparecer la hoja de datos tipo Excel, permitiéndote modificar los valores de las series.

Si solo ves una imagen estática, verifica que:

- Estés usando una versión reciente de Aspose.Slides (las versiones antiguas tenían errores con `ExportEditableObjects`).  
- El PPTX de origen realmente contenga objetos de gráfico (no imágenes de gráficos).  
- Ningún tema personalizado o sustitución de fuentes esté provocando que el gráfico se renderice como imagen.

### Casos límite

- **Archivos PPT (binarios) antiguos:** Conviértelos a PPTX primero (`pres.Save("temp.pptx", SaveFormat.Pptx)`) antes de aplicar las opciones de exportación.  
- **Presentaciones grandes:** El uso de memoria puede incrementarse; considera el patrón `Dispose` de `Presentation` o las APIs de streaming para archivos masivos.  
- **Fuentes incrustadas:** Si el entorno de destino no tiene las fuentes originales, PowerPoint puede recurrir a un fallback y renderizar el gráfico como imagen. Incrusta las fuentes en el archivo de origen o envíalas con tu aplicación.

---

## Preguntas frecuentes (FAQ)

**P: ¿Esto funciona con archivos PowerPoint 2003 (PPT)?**  
R: Directamente no—`ExportEditableObjects` solo se aplica al formato PPTX. Convierte primero, luego exporta.

**P: ¿Puedo preservar otros objetos como SmartArt?**  
R: Absolutamente. La misma bandera `ExportEditableObjects` mantiene SmartArt, tablas y diagramas editables.

**P: ¿Qué pasa si necesito conservar el tamaño original de la diapositiva?**  
R: El tamaño de la diapositiva está almacenado en los metadatos de la presentación y no se ve afectado por estas opciones. No se necesita código adicional.

---

## Próximos pasos – mantén el impulso

Ahora que dominas **cómo preservar gráficos**, prueba explorar:

- **preserve chart formatting** para tipos de gráficos específicos (p. ej., barras apiladas vs. radar).  
- Uso de la API `Chart` para modificar datos programáticamente antes de guardar.  
- Exportar a otros formatos (PDF, HTML) manteniendo los gráficos editables en el PPTX de origen.  

Cada uno de estos se basa en el mismo principio: mantener intacto el OOXML subyacente.

---

## Conclusión

Hemos recorrido **cómo preservar gráficos** en un archivo PowerPoint usando Aspose.Slides para .NET, y hemos demostrado los pasos exactos de **preserve chart formatting** necesarios para que esos gráficos sigan siendo totalmente editables. El fragmento de código completo arriba está listo para integrarse en cualquier proyecto C#, y las explicaciones cubren el *por qué* detrás de cada línea—así que no solo copiarás y pegarás, sino que entenderás.

Pruébalo, ajusta las opciones de exportación y pronto estarás automatizando actualizaciones de presentaciones sin perder la capacidad de afinar los datos de los gráficos. ¡Feliz codificación!

## ¿Qué deberías aprender a continuación?

Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos y explicaciones paso a paso para ayudarte a dominar funciones adicionales de la API y explorar enfoques alternativos de implementación en tus propios proyectos.

- [How to Export Excel Charts to PDF Using Aspose.Cells for .NET&#58; A Step-by-Step Guide](/cells/english/net/workbook-operations/export-excel-charts-pdf-aspose-cells-net/)
- [How to Convert Excel Charts to SVG Using Aspose.Cells for .NET (Step-by-Step Guide)](/cells/english/net/charts-graphs/convert-excel-chart-to-svg-aspose-cells-net/)
- [How to Create Charts in Excel Using Aspose.Cells for .NET&#58; A Developer's Guide](/cells/english/net/charts-graphs/create-charts-excel-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}