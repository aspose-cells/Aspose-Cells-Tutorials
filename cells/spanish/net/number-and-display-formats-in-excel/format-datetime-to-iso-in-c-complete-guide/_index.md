---
category: general
date: 2026-03-22
description: Aprende cómo formatear la fecha y hora a ISO al extraer la fecha de Excel
  y mostrar la fecha ISO usando Aspose.Cells en C#.
draft: false
keywords:
- format datetime to iso
- extract date from excel
- display iso date
- Aspose.Cells date parsing
- Japanese era dates
language: es
og_description: Formatear fecha y hora a ISO hecho fácil. Esta guía muestra cómo extraer
  la fecha de Excel y mostrar la fecha ISO con Aspose.Cells.
og_title: formatear datetime a iso en C# – tutorial paso a paso
tags:
- C#
- Aspose.Cells
- DateTime
- Excel
- ISO 8601
title: Formatear datetime a ISO en C# – Guía completa
url: /es/net/number-and-display-formats-in-excel/format-datetime-to-iso-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# formatear datetime a iso en C# – Guía completa

¿Alguna vez necesitaste **formatear datetime a iso** pero la fuente está dentro de un libro de Excel? Tal vez la celda contiene una era japonesa como “令和3年5月1日” y estás rascándote la cabeza preguntándote cómo convertir eso en una cadena limpia `2021‑05‑01`. No estás solo. En este tutorial **extraeremos la fecha de excel**, analizaremos la era japonesa y luego **mostraremos la fecha iso** en la consola, todo con unas pocas líneas de C# y Aspose.Cells.

Recorreremos todo lo que necesitas: el paquete NuGet requerido, el código exacto que puedes copiar‑pegar, por qué cada línea es importante y algunos consejos para casos límite. Al final tendrás un fragmento reutilizable que formatea datetime a iso sin importar lo peculiar que sea el valor original de Excel.

## Lo que necesitarás

- .NET 6.0 o posterior (el código también compila en .NET Framework 4.6+)
- Visual Studio 2022 (o cualquier editor que prefieras)
- **Aspose.Cells for .NET** paquete NuGet – `Install-Package Aspose.Cells`
- Un archivo Excel (o un libro nuevo) que contiene una fecha en formato de era japonesa

Eso es todo. Sin bibliotecas extra, sin interop COM, solo un método único y bien documentado.

## Paso 1: Crear un libro y escribir una fecha de era japonesa  

Primero, necesitamos un libro con el que trabajar. Si ya tienes un archivo Excel, puedes cargarlo con `new Workbook("path")`. Para este ejemplo crearemos un nuevo libro en memoria y colocaremos una cadena de era japonesa en la celda **A1**.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // 1️⃣ Create a fresh workbook
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.Worksheets[0];

        // 2️⃣ Write a Japanese era date (Reiwa 3 = 2021) into A1
        sheet.Cells["A1"].PutValue("令和3年5月1日");
```

> **Por qué hacemos esto:** Aspose.Cells trata los valores de celda como cadenas por defecto. Al insertar el texto de era sin procesar simulamos un escenario del mundo real donde un cliente japonés ha introducido fechas en su calendario nativo.

## Paso 2: Habilitar el análisis de era japonesa y extraer la fecha  

Aspose.Cells puede traducir automáticamente cadenas de era japonesa a objetos .NET `DateTime`, siempre que se lo indiques. La bandera `DateTimeParseOptions.EnableJapaneseEra` realiza el trabajo pesado.

```csharp
        // 3️⃣ Retrieve the cell value while enabling Japanese era parsing
        CellValue parsed = sheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

> **Consejo profesional:** Si olvidas la opción `EnableJapaneseEra`, la biblioteca devolverá la cadena original y tu conversión posterior fallará. Siempre verifica `parsed.Type` si manejas contenido mixto.

## Paso 3: Convertir el DateTime analizado a ISO 8601  

Ahora que tenemos un `DateTime` correcto, convertirlo a una cadena con formato ISO es pan comido. El patrón `"yyyy-MM-dd"` cumple con la parte de fecha de ISO 8601, que es lo que la mayoría de las API esperan.

```csharp
        // 4️⃣ Convert to ISO 8601 (yyyy‑MM‑dd) and display it
        string isoDate = parsed.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

Ejecutar el programa imprime:

```
ISO date: 2021-05-01
```

Ese es el **mostrar fecha iso** que buscabas.

## Ejemplo completo y ejecutable  

A continuación está el bloque de código completo que puedes copiar directamente en un proyecto de consola. Sin dependencias ocultas, sin configuración extra.

```csharp
using System;
using Aspose.Cells;

class Program
{
    static void Main()
    {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.Worksheets[0];

        // Write a Japanese era date into cell A1
        worksheet.Cells["A1"].PutValue("令和3年5月1日");

        // Retrieve the cell value with Japanese era parsing enabled
        CellValue parsedValue = worksheet.Cells["A1"]
            .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);

        // Convert the DateTime to ISO 8601 format and output it
        string isoDate = parsedValue.DateTimeValue.ToString("yyyy-MM-dd");
        Console.WriteLine($"ISO date: {isoDate}");
    }
}
```

> **Salida esperada:** `ISO date: 2021-05-01`

## Desglose paso a paso (Por qué cada pieza es importante)

| Paso | Qué ocurre | Por qué es importante |
|------|------------|-----------------------|
| **Crear libro** | Inicializa un contenedor Excel en memoria. | Te brinda un entorno de pruebas sin tocar el sistema de archivos. |
| **PutValue** | Almacena la cadena cruda de era japonesa en **A1**. | Imita la entrada de datos real; asegura que el analizador vea el texto exacto. |
| **GetValue con `EnableJapaneseEra`** | Convierte la cadena de era a un .NET `DateTime`. | Gestiona la conversión del calendario automáticamente—no se necesitan tablas de búsqueda manuales. |
| `ToString("yyyy-MM-dd")` | Formatea el `DateTime` a ISO 8601. | Garantiza una cadena de fecha invariante a la cultura, ordenable y aceptada por APIs REST, bases de datos, etc. |
| **Console.WriteLine** | Muestra la fecha ISO final. | Confirma que todo el proceso funciona de extremo a extremo. |

## Manejo de variaciones comunes  

### 1. Diferentes ubicaciones de celda  

Si tu fecha está en **B2** o en un rango con nombre, simplemente reemplaza `"A1"` con la dirección adecuada:

```csharp
worksheet.Cells["B2"].PutValue("令和2年12月31日");
var value = worksheet.Cells["B2"]
    .GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
```

### 2. Múltiples fechas en una columna  

Cuando necesitas **extraer la fecha de excel** para muchas filas, recorre el rango usado:

```csharp
int lastRow = worksheet.Cells.MaxDataRow;
for (int i = 0; i <= lastRow; i++)
{
    var cell = worksheet.Cells[i, 0]; // column A
    var cv = cell.GetValue(CellValueType.DateTime, DateTimeParseOptions.EnableJapaneseEra);
    string iso = cv.DateTimeValue.ToString("yyyy-MM-dd");
    Console.WriteLine($"Row {i + 1}: {iso}");
}
```

### 3. Alternativa para fechas sin era  

Si una celda ya contiene una cadena de fecha estándar, el analizador aún funciona, pero podrías querer una red de seguridad:

```csharp
CellValue cv = cell.GetValue(CellValueType.DateTime,
    DateTimeParseOptions.EnableJapaneseEra | DateTimeParseOptions.TryParse);
```

La bandera `TryParse` evita excepciones y devuelve el valor original si la conversión falla.

### 4. Componente de tiempo  

Si también necesitas la parte de tiempo, usa `"yyyy-MM-ddTHH:mm:ss"`:

```csharp
string isoDateTime = parsedValue.DateTimeValue.ToString("yyyy-MM-ddTHH:mm:ss");
```

Eso produce una marca de tiempo ISO 8601 completa (`2021-05-01T00:00:00`).

## Ayuda visual  

![ejemplo de formatear datetime a iso](image.png "Un ejemplo de formatear datetime a iso en C#")

*Texto alternativo:* *ejemplo de formatear datetime a iso mostrando salida de consola*

## Preguntas frecuentes  

- **¿Puedo usar esto con archivos .xls?**  
  Sí. Aspose.Cells soporta `.xls`, `.xlsx`, `.csv` y muchos otros formatos listos para usar.

- **¿Qué pasa si el libro está protegido con contraseña?**  
  Cárgalo con `new Workbook("file.xlsx", new LoadOptions { Password = "secret" })`.

- **¿El formato ISO depende de la configuración regional?**  
  No. El patrón `"yyyy-MM-dd"` es invariable a la cultura, garantizando la misma cadena en cualquier máquina.

- **¿Funciona esto en .NET Core?**  
  Absolutamente—Aspose.Cells es compatible con .NET Standard 2.0.

## Conclusión  

Hemos cubierto cómo **formatear datetime a iso** mediante **extraer la fecha de excel**, analizando cadenas de era japonesa y finalmente **mostrando la fecha iso** en la consola. Los pasos clave—crear un libro, escribir o cargar el texto de era, habilitar el análisis de era japonesa y formatear con `ToString("yyyy-MM-dd")`—son todo lo que necesitas para la mayoría de los escenarios.

A continuación, podrías querer:

- Escribir las fechas ISO de nuevo en otra columna para procesamiento posterior.
- Exportar el libro transformado a CSV para importación masiva.
- Combinar esta lógica con una API web que acepte cargas de Excel y devuelva fechas ISO codificadas en JSON.

Siéntete libre de experimentar con diferentes formatos de fecha, zonas horarias o incluso calendarios personalizados. La flexibilidad de Aspose.Cells significa que rara vez encontrarás un obstáculo.

¡Feliz codificación, y que todas tus fechas sean perfectamente compatibles con ISO!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}