---
category: general
date: 2026-02-15
description: Cómo formatear moneda rápidamente usando Set Column Number Format y aplicar
  un formato numérico personalizado en C#. Aprende a obtener la columna por nombre
  y establecer la alineación de la columna en la cuadrícula.
draft: false
keywords:
- how to format currency
- set column number format
- apply custom numeric format
- retrieve column by name
- set grid column alignment
language: es
og_description: Cómo formatear moneda en una columna de cuadrícula usando C#. Este
  tutorial muestra cómo obtener la columna por nombre, establecer el formato numérico
  de la columna, aplicar un formato numérico personalizado y establecer la alineación
  de la columna de la cuadrícula.
og_title: Cómo formatear moneda en una columna de cuadrícula – Guía completa
tags:
- C#
- GridFormatting
- UI
title: Cómo formatear moneda en una columna de cuadrícula – Guía paso a paso
url: /es/net/number-and-display-formats-in-excel/how-to-format-currency-in-a-grid-column-step-by-step-guide/
---

translate to Spanish, maybe keep same style: "# cómo formatear moneda en una columna de Grid – Tutorial de programación completo". Keep "Grid" as is.

Then paragraph.

We'll translate.

Need to keep **bold** formatting.

Proceed.

Also need to translate blockquote > **TL;DR** – By the end you’ll have a ready‑to‑run snippet... etc.

Translate.

Then sections.

List items.

Tables.

Make sure to keep markdown syntax.

Let's craft.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cómo formatear moneda en una columna de Grid – Tutorial de programación completo

¿Alguna vez te has preguntado **cómo formatear moneda** en una columna de grid sin volverte loco? No eres el único. Cuando miras un número simple como `1234.5` y deseas que aparezca mágicamente como `$1,234.50`, la respuesta suele ser solo unas cuantas líneas de configuración.  

En esta guía **recuperaremos la columna por nombre**, **estableceremos el formato numérico de la columna** y **aplicaremos un formato numérico personalizado** que respeta el diseño contable típico. En el camino también **estableceremos la alineación de la columna del grid** y añadiremos un borde sutil para que la UI luzca pulida.

> **TL;DR** – Al final tendrás un fragmento listo‑para‑ejecutar que convierte decimales crudos en valores de moneda bellamente formateados dentro de cualquier control estilo `GridJs`.

---

## Qué necesitarás

- Un proyecto .NET (cualquier versión que soporte C# 8.0+ – Visual Studio 2022 funciona genial).  
- Un componente de grid que exponga una colección `Columns` (el ejemplo usa una clase ficticia `GridJs`, pero los conceptos se trasladan a grids de DevExpress, Telerik o Syncfusion).  
- Familiaridad básica con la sintaxis de C# – no se requieren trucos avanzados.

Si ya tienes eso, genial. Si no, simplemente crea una aplicación de consola; el grid puede ser simulado para la ilustración.

---

## Implementación paso a paso

A continuación, en cada paso verás un bloque de código compacto, una breve explicación de **por qué** la línea es importante y un consejo para evitar errores comunes.

### ## Paso 1 – Recuperar la columna “Amount” por nombre

```csharp
// Step 1: Retrieve the "Amount" column from the grid
var amountColumn = gridJs.Columns["Amount"];
if (amountColumn == null)
{
    throw new InvalidOperationException("Column 'Amount' does not exist. Verify the column name or check the grid's schema.");
}
```

**Por qué es importante:**  
La mayoría de las APIs de grids exponen las columnas mediante un indexador tipo diccionario. Obtener la columna por su nombre de encabezado (`"Amount"`) te permite manipular su apariencia sin tocar la fuente de datos subyacente.  

**Consejo profesional:** Siempre protege contra un retorno `null` – un error tipográfico en el nombre de la columna o un cambio dinámico del esquema pueden provocar una `NullReferenceException` en tiempo de ejecución.

---

### ## Paso 2 – Establecer el formato numérico de la columna usando una máscara de moneda personalizada

```csharp
// Step 2: Apply a custom numeric format for currency values
amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";
```

**Por qué es importante:**  
La cadena de formato sigue las convenciones de formato contable de Excel:

- `_(* #,##0.00_)` → Números positivos, alineados a la derecha con un espacio inicial para el símbolo de moneda.  
- `_(* (#,##0.00)` → Números negativos entre paréntesis.  
- `_(* \"-\"??_)` → Valores cero mostrados como un guión.  
- `_(@_)` → Los valores de texto permanecen sin cambios.

Usar **apply custom numeric format** te brinda control total sobre los separadores de miles, los decimales y la posición del símbolo de moneda.  

**Caso límite:** Si tu aplicación necesita respetar una localidad diferente (p. ej., Euro en lugar de USD), reemplaza el espacio inicial con el símbolo correspondiente o utiliza formato dependiente de `CultureInfo` en la fuente de datos.

---

### ## Paso 3 – Alinear el contenido de la columna a la derecha para mayor legibilidad

```csharp
// Step 3: Align the column contents to the right for better readability
amountColumn.Alignment = GridAlignment.Right;
```

**Por qué es importante:**  
Los valores monetarios son más fáciles de escanear cuando se alinean en el separador decimal. Configurar **set grid column alignment** a `Right` imita la forma en que las hojas de cálculo muestran datos financieros.  

**Truco:** Algunos grids ignoran la alineación en celdas que contienen plantillas personalizadas. Si notas que la alineación no surte efecto, verifica que la columna no esté usando un renderizador de celda personalizado.

---

### ## Paso 4 – Añadir un borde gris fino alrededor de las celdas de la columna

```csharp
// Step 4: Add a thin gray border around the column cells
amountColumn.Border = new GridBorder
{
    Color = Color.Gray,
    Style = BorderLineStyle.Thin
};
```

**Por qué es importante:**  
Un borde sutil separa la columna “Amount” de sus vecinas, especialmente cuando el grid tiene colores de fila alternados. Es una pista visual de que los datos representan una cifra financiera distinta.  

**Consejo:** Si necesitas una línea más gruesa para impresión, aumenta `BorderLineStyle` a `Medium` o cambia `Color` a `Color.Black`.

---

## Ejemplo completo funcionando

Aquí tienes el fragmento completo que puedes insertar en un proyecto WinForms o WPF que use un control estilo `GridJs`. El ejemplo también imprime los valores formateados en la consola para que puedas verificar la salida sin una UI.

```csharp
using System;
using System.Drawing;   // For Color
using GridLibrary;      // Hypothetical namespace for GridJs

namespace GridCurrencyDemo
{
    class Program
    {
        static void Main()
        {
            // Create a mock grid and add a sample column
            var gridJs = new GridJs();
            gridJs.Columns.Add(new GridColumn
            {
                Name = "Amount",
                Header = "Amount",
                DataType = typeof(decimal)
            });

            // Populate some sample data
            gridJs.Rows.Add(new { Amount = 1234.5m });
            gridJs.Rows.Add(new { Amount = -567.89m });
            gridJs.Rows.Add(new { Amount = 0m });

            // ---- Formatting steps ------------------------------------------------
            // 1️⃣ Retrieve the "Amount" column
            var amountColumn = gridJs.Columns["Amount"]
                ?? throw new InvalidOperationException("Column 'Amount' not found.");

            // 2️⃣ Apply custom numeric format for currency
            amountColumn.NumberFormat = "_(* #,##0.00_);_(* (#,##0.00);_(* \"-\"??_);_(@_)";

            // 3️⃣ Right‑align the values
            amountColumn.Alignment = GridAlignment.Right;

            // 4️⃣ Add a thin gray border
            amountColumn.Border = new GridBorder
            {
                Color = Color.Gray,
                Style = BorderLineStyle.Thin
            };
            // -----------------------------------------------------------------------

            // Render the grid (in a real UI you would call gridJs.Render() or similar)
            Console.WriteLine("Formatted Currency Grid:");
            foreach (var row in gridJs.Rows)
            {
                var rawValue = (decimal)row.Amount;
                // The grid library would automatically apply NumberFormat when displaying.
                // For console demo we mimic the formatting:
                string formatted = rawValue.ToString("#,##0.00", System.Globalization.CultureInfo.InvariantCulture);
                if (rawValue < 0)
                    formatted = $"({formatted.TrimStart('-')})";
                else if (rawValue == 0)
                    formatted = "-";

                Console.WriteLine($"| {formatted,15} |");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Salida esperada en la consola**

```
Formatted Currency Grid:
|        1,234.50 |
|       (567.89) |
|               - |
```

Observa cómo el número positivo está alineado a la derecha, el negativo aparece entre paréntesis y el cero muestra un guión – exactamente lo que dicta la cadena de formato personalizada.

---

## Preguntas frecuentes y casos límite

| Pregunta | Respuesta |
|----------|-----------|
| *¿Qué pasa si el grid usa una cultura diferente (p. ej., € en lugar de $)?* | Reemplaza el espacio inicial en la cadena de formato con el símbolo deseado o permite que la fuente de datos emita una cadena pre‑formateada usando `CultureInfo.CurrentCulture`. |
| *¿Puedo reutilizar el mismo formato para varias columnas?* | Por supuesto. Guarda la cadena de formato en una constante (`const string CurrencyMask = "...";`) y asígnala donde necesites moneda. |
| *¿Qué ocurre si la columna contiene un valor de tipo cadena?* | La cadena de formato solo afecta a tipos numéricos. Las cadenas pasan sin cambios, por eso existe la última parte de la máscara (`_(@_)`) – preserva contenido no numérico. |
| *¿Hay impacto en el rendimiento?* | Negligible. El formato se aplica en tiempo de renderizado, no durante la obtención de datos. A menos que estés renderizando miles de filas por cuadro, no notarás ralentización. |
| *¿Cómo hago el borde más grueso para informes impresos?* | Cambia `BorderLineStyle.Thin` por `BorderLineStyle.Medium` o `BorderLineStyle.Thick`. Algunas bibliotecas también permiten especificar un ancho en píxeles directamente. |

---

## Conclusión

Hemos recorrido **cómo formatear moneda** en una columna de grid de principio a fin: recuperar la columna por nombre, establecer el formato numérico, aplicar un formato numérico personalizado, alinear las celdas y añadir un borde elegante. El ejemplo completo funciona listo para usar y muestra el resultado visual exacto que puedes esperar.

Si estás listo para llevar esto más lejos, prueba:

- **Culturas dinámicas** – cambia la cadena de formato según la localidad del usuario.  
- **Condicional

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}