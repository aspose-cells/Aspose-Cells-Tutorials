---
category: general
date: 2026-05-23
description: Incruste fuentes en HTML al exportar Excel a HTML usando Aspose.Cells.
  Guía paso a paso para convertir la hoja de cálculo a HTML con fuentes incrustadas.
draft: false
keywords:
- embed fonts in html
- export excel to html
- convert spreadsheet to html
- save workbook as html
- how to embed fonts html
language: es
og_description: Incrusta fuentes en HTML al exportar Excel a HTML. Aprende cómo convertir
  una hoja de cálculo a HTML con fuentes incrustadas en unos pocos pasos fáciles.
og_title: Incrustar fuentes en HTML – Exportar Excel a HTML con C#
schemas:
- author: Aspose
  dateModified: '2026-05-23'
  description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  headline: Embed fonts in HTML – Export Excel to HTML with C#
  type: TechArticle
- description: Embed fonts in HTML when you export Excel to HTML using Aspose.Cells.
    Step‑by‑step guide to convert spreadsheet to HTML with embedded fonts.
  name: Embed fonts in HTML – Export Excel to HTML with C#
  steps:
  - name: 1️⃣ **What if my workbook uses a custom font that isn’t installed on the
      server?**
    text: Aspose.Cells can only embed fonts that are available to the runtime. Install
      the `.ttf` or `.otf` file on the machine running the conversion, or copy it
      into the project directory and register it via `System.Drawing.Text.PrivateFontCollection`
      before invoking the save operation.
  - name: 2️⃣ **Will embedding increase the file size dramatically?**
    text: Yes, each embedded font is Base64‑encoded, which adds roughly 33 % overhead.
      If the workbook uses many large fonts, consider enabling `EmbedOnlyUsedFonts
      = true` to limit the payload to fonts actually referenced in the sheet.
  - name: 3️⃣ **Can I still export images separately?**
    text: Setting `ExportImagesAsBase64 = true` (as shown above) inlines images, making
      the HTML truly self‑contained. If you prefer external image files, set this
      property to `false` and specify `ExportImagesFolder` to control the output folder.
  - name: 4️⃣ **Is this approach compatible with older browsers?**
    text: Most modern browsers (Chrome, Edge, Firefox, Safari) support Base64‑encoded
      `@font-face`. Internet Explorer 11 also works, but you might need to ensure
      the MIME type is correct. For legacy support, consider providing a fallback
      font stack in your CSS.
  - name: 5️⃣ **How does this differ from a simple “export excel to html” without
      embedding?**
    text: A plain export writes the text using generic web fonts (`Arial`, `Helvetica`,
      etc.). The visual layout may shift, especially for corporate reports that rely
      on a brand‑specific typeface. Embedding removes that uncertainty.
  type: HowTo
tags:
- Aspose.Cells
- C#
- Excel automation
title: Incrustar fuentes en HTML – Exportar Excel a HTML con C#
url: /es/net/exporting-excel-to-html-with-advanced-options/embed-fonts-in-html-export-excel-to-html-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Insertar fuentes en HTML – Exportar Excel a HTML con C#

¿Alguna vez te has preguntado cómo **insertar fuentes en HTML** mientras exportas un libro de Excel? No eres el único. Cuando compartes una hoja de cálculo como página web, la falta de fuentes puede convertir un informe pulido en un desastre confuso, sobre todo si el visor no tiene la tipografía original instalada.  

En este tutorial recorreremos una solución completa, lista para ejecutar, que te muestra exactamente **cómo insertar fuentes en HTML** usando Aspose.Cells para .NET. Al final podrás **exportar Excel a HTML**, **convertir hoja de cálculo a HTML**, y **guardar el libro como HTML** con las fuentes incorporadas directamente en el archivo.

---

## Lo que aprenderás

- La razón por la que las fuentes incrustadas son importantes para exportaciones de Excel basadas en la web.  
- Cómo configurar `HtmlSaveOptions` para activar la opción `EmbedFonts`.  
- Un programa completo en C# que carga un libro, aplica la configuración y escribe un archivo HTML.  
- Consejos para manejar fuentes personalizadas, compatibilidad de versiones y solución de problemas comunes.  

No se requiere experiencia previa con Aspose.Cells, pero deberías tener una comprensión básica de C# y desarrollo .NET.

---

## Requisitos previos

| Requisito | Por qué es importante |
|-------------|----------------|
| **.NET 6.0 o posterior** | Entorno de ejecución moderno; los frameworks más antiguos pueden no incluir las últimas funciones de Aspose.Cells. |
| **Aspose.Cells para .NET** (paquete NuGet `Aspose.Cells`) | Proporciona la clase `HtmlSaveOptions` que necesitamos. |
| **Una fuente TrueType u OpenType** que desees incrustar (p. ej., `Arial.ttf`) | Sólo estos formatos de fuente pueden incrustarse en el archivo HTML. |
| **Un IDE** (Visual Studio, Rider, VS Code) | Facilita la ejecución y depuración del ejemplo. |

Si aún no has instalado el paquete NuGet, ejecuta:

```bash
dotnet add package Aspose.Cells
```

---

## Paso 1: Cargar el libro que deseas convertir

Primero, necesitamos una instancia de `Workbook`. Puedes cargar un archivo `.xlsx` existente, crear uno desde cero o incluso extraer datos de una base de datos. Aquí tienes un ejemplo mínimo que abre un archivo llamado `Sample.xlsx` desde la carpeta del proyecto:

```csharp
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Load the source Excel file
        var workbook = new Workbook("Sample.xlsx");
        // Continue with HTML conversion...
```

> **¿Por qué este paso?**  
> El objeto `Workbook` es el punto de entrada para todas las operaciones de Aspose.Cells. Sin él no puedes acceder a las hojas, estilos o datos que eventualmente se convertirán en HTML.

---

## Paso 2: Configurar las opciones de guardado HTML para **Insertar fuentes en HTML**

Ahora llega la línea mágica que responde a la pregunta “cómo insertar fuentes html”. Creamos una instancia de `HtmlSaveOptions` y establecemos `EmbedFonts` en `true`. Esto indica a la biblioteca que inserte los datos de la fuente como reglas CSS `@font-face` codificadas en Base64.

```csharp
        // Step 2: Set up HTML save options with embedded fonts
        var htmlOptions = new HtmlSaveOptions
        {
            // This flag ensures fonts are written directly into the HTML file
            EmbedFonts = true,

            // Optional: you can control whether to embed only used fonts
            // EmbedOnlyUsedFonts = true,

            // Optional: control the output folder for external resources
            ExportImagesAsBase64 = true
        };
```

> **¿Por qué habilitar `EmbedFonts`?**  
> Cuando el HTML resultante se abre en una máquina que no tiene la fuente original, el navegador recurre a una tipografía genérica. Incrustar garantiza la fidelidad visual en todas las plataformas.

---

## Paso 3: Guardar el libro como HTML

Con las opciones preparadas, llamamos a `Workbook.Save`, pasando el nombre de archivo deseado y el objeto `HtmlSaveOptions`. La biblioteca realiza el trabajo pesado: convierte celdas, fórmulas y estilos en marcado HTML, y luego inserta los datos de la fuente dentro de etiquetas `<style>`.

```csharp
        // Step 3: Export the workbook to HTML with embedded fonts
        workbook.Save("output.html", htmlOptions);

        // Inform the user
        Console.WriteLine("Workbook successfully saved as HTML with embedded fonts.");
    }
}
```

> **Lo que verás:**  
> Abre `output.html` en cualquier navegador moderno y notarás la misma tipografía exacta que el archivo Excel original, incluso si el visor no tiene la fuente instalada localmente.

---

## Ejemplo completo en funcionamiento

Juntando todo, aquí tienes el programa completo que puedes copiar y pegar en un proyecto de consola:

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the source workbook
        var workbook = new Workbook("Sample.xlsx");

        // 2️⃣ Configure HTML save options to embed fonts
        var htmlOptions = new HtmlSaveOptions
        {
            EmbedFonts = true,
            ExportImagesAsBase64 = true,
            // You can also set ExportActiveWorksheetOnly = true if you only need one sheet
        };

        // 3️⃣ Save the workbook as HTML
        workbook.Save("output.html", htmlOptions);

        Console.WriteLine("✅ Workbook saved as HTML with embedded fonts.");
    }
}
```

Ejecuta el programa (`dotnet run`), luego abre `output.html`. Deberías ver una réplica fiel de la hoja de cálculo original, con las fuentes exactas que utilizaste.

![Ejemplo de salida con fuentes incrustadas en HTML](embed-fonts-html.png "Captura de pantalla que muestra el archivo HTML con fuentes incrustadas")

*Texto alternativo de la imagen: insertar fuentes en html – captura de pantalla de la página HTML generada que conserva las fuentes originales de la hoja de cálculo.*

---

## Preguntas frecuentes y casos límite

### 1️⃣ **¿Qué pasa si mi libro usa una fuente personalizada que no está instalada en el servidor?**  
Aspose.Cells solo puede incrustar fuentes que estén disponibles para el tiempo de ejecución. Instala el archivo `.ttf` u `.otf` en la máquina que realiza la conversión, o cópialo al directorio del proyecto y regístralo mediante `System.Drawing.Text.PrivateFontCollection` antes de invocar la operación de guardado.

### 2️⃣ **¿Incrustar aumentará drásticamente el tamaño del archivo?**  
Sí, cada fuente incrustada se codifica en Base64, lo que añade aproximadamente un 33 % de sobrecarga. Si el libro usa muchas fuentes grandes, considera habilitar `EmbedOnlyUsedFonts = true` para limitar la carga solo a las fuentes realmente referenciadas en la hoja.

### 3️⃣ **¿Puedo seguir exportando imágenes por separado?**  
Establecer `ExportImagesAsBase64 = true` (como se muestra arriba) inserta las imágenes, haciendo que el HTML sea verdaderamente autocontenido. Si prefieres archivos de imagen externos, pon esta propiedad en `false` y especifica `ExportImagesFolder` para controlar la carpeta de salida.

### 4️⃣ **¿Este enfoque es compatible con navegadores antiguos?**  
La mayoría de los navegadores modernos (Chrome, Edge, Firefox, Safari) soportan `@font-face` codificado en Base64. Internet Explorer 11 también funciona, pero puede que necesites asegurarte de que el tipo MIME sea correcto. Para soporte legado, considera proporcionar una pila de fuentes de reserva en tu CSS.

### 5️⃣ **¿En qué se diferencia de una simple “exportar Excel a HTML” sin incrustar?**  
Una exportación simple escribe el texto usando fuentes web genéricas (`Arial`, `Helvetica`, etc.). El diseño visual puede variar, especialmente en informes corporativos que dependen de una tipografía de marca. Incrustar elimina esa incertidumbre.

---

## Consejos profesionales y buenas prácticas

- **Cachea el HTML** si generas el mismo informe repetidamente. El proceso de conversión, aunque rápido, sigue consumiendo ciclos de CPU.  
- **Valida la salida** con un validador HTML (p. ej., el validador de W3C) para detectar cualquier marcado erróneo que pueda romper clientes de correo.  
- **Combínalo con minificación de CSS** si planeas servir el HTML en la web. Los datos de la fuente ya están comprimidos, pero el CSS circundante puede recortarse.  
- **Vigila la licencia**: Aspose.Cells requiere una licencia válida para uso en producción; de lo contrario, aparecerá una marca de agua en la salida HTML.  
- **Prueba en varios dispositivos**, especialmente navegadores móviles, para asegurar que las fuentes incrustadas se rendericen correctamente en diferentes densidades de pantalla.

---

## Conclusión

Ahora dispones de una solución completa, lista para copiar y pegar, para **insertar fuentes en HTML** al **exportar Excel a HTML**, **convertir hoja de cálculo a HTML**, o simplemente **guardar el libro como HTML** con total fidelidad tipográfica. Al activar la bandera `EmbedFonts` en `HtmlSaveOptions`, eliminas el temido problema de “fuente faltante” y entregas una página web pulida y autocontenida a cualquier audiencia.

¿Listo para el siguiente desafío? Prueba a añadir **gráficos interactivos** a la exportación HTML, o experimenta con la **conversión a PDF** para ver cómo se comportan las fuentes incrustadas en otro formato. El mismo patrón de `HtmlSaveOptions` se aplica—solo cambia el tipo de salida.

¡Feliz codificación, y que tus hojas de cálculo siempre se vean exactamente como deseas—sin importar dónde se visualicen!

## Tutoriales relacionados

- [Convertir Excel a HTML en Java usando Aspose.Cells: Guía paso a paso](/cells/english/java/workbook-operations/convert-excel-html-aspose-cells-java/)
- [Exportar Excel a HTML usando Aspose.Cells Java: Guía paso a paso](/cells/english/java/workbook-operations/export-excel-html-aspose-cells-java/)
- [Convertir Excel a HTML con tooltips usando Aspose.Cells Java: Guía completa](/cells/english/java/workbook-operations/excel-to-html-conversion-with-tooltips-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}