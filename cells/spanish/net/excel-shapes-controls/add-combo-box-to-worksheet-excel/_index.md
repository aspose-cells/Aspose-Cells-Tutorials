---
"description": "Aprenda a agregar un cuadro combinado a una hoja de cálculo de Excel mediante programación con Aspose.Cells para .NET. Esta guía paso a paso le explica cada detalle."
"linktitle": "Agregar cuadro combinado a una hoja de cálculo en Excel"
"second_title": "API de procesamiento de Excel Aspose.Cells .NET"
"title": "Agregar cuadro combinado a una hoja de cálculo en Excel"
"url": "/es/net/excel-shapes-controls/add-combo-box-to-worksheet-excel/"
"weight": 21
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Agregar cuadro combinado a una hoja de cálculo en Excel

## Introducción
Crear hojas de cálculo interactivas de Excel puede mejorar considerablemente la experiencia del usuario, especialmente al añadir elementos de formulario como cuadros combinados. Estos cuadros permiten seleccionar opciones de una lista predefinida, lo que facilita y agiliza la introducción de datos. Con Aspose.Cells para .NET, puede crear cuadros combinados en hojas de Excel mediante programación sin usar Excel directamente. Esta potente biblioteca permite a los desarrolladores manipular archivos de Excel de diversas maneras, incluyendo la posibilidad de automatizar los controles de formulario.
En este tutorial, le guiaremos por el proceso de agregar un cuadro combinado a una hoja de cálculo de Excel con Aspose.Cells para .NET. Si desea crear hojas de cálculo dinámicas e intuitivas, esta guía le ayudará a empezar.
## Prerrequisitos
Antes de sumergirnos en el código, asegurémonos de que tienes todo lo que necesitas:
- Aspose.Cells para .NET: Descargue e instale la biblioteca Aspose.Cells para .NET desde [página de descarga](https://releases.aspose.com/cells/net/).
- .NET Framework: Asegúrate de tener .NET Framework instalado en tu equipo. Cualquier versión compatible con Aspose.Cells funcionará.
- Entorno de desarrollo: utilice un IDE como Visual Studio para administrar su proyecto y escribir código.
- Licencia de Aspose: Puede trabajar sin licencia en el modo de evaluación, pero para obtener la versión completa, deberá solicitar una. Obtenga una [licencia temporal](https://purchase.aspose.com/temporary-license/) Si es necesario.
## Importar paquetes
Para empezar, necesitas importar los espacios de nombres necesarios a tu proyecto. Esto es lo que necesitas:
```csharp
using System.IO;
using Aspose.Cells;
```
Estos son esenciales para interactuar con archivos de Excel y manipular elementos de formulario como cuadros combinados en el libro.
Dividamos el proceso de agregar un cuadro combinado en varios pasos simples para facilitar su comprensión.
## Paso 1: Configurar el directorio de documentos
El primer paso es crear un directorio donde se guardarán tus archivos de Excel. Puedes crear una carpeta nueva si aún no existe.
```csharp
// La ruta al directorio de documentos.
string dataDir = "Your Document Directory";
// Crear directorio si aún no está presente.
bool IsExists = System.IO.Directory.Exists(dataDir);
if (!IsExists)
    System.IO.Directory.CreateDirectory(dataDir);
```
- dataDir: especifica la ubicación donde se guardará el archivo de salida.
- System.IO.Directory.Exists: comprueba si el directorio ya existe.
- System.IO.Directory.CreateDirectory: crea el directorio si falta.
## Paso 2: Crear un nuevo libro de trabajo
Ahora, crea un nuevo libro de Excel donde agregarás el cuadro combinado.

```csharp
// Crear un nuevo libro de trabajo.
Workbook workbook = new Workbook();
```

- Libro de trabajo libro de trabajo: inicializa una nueva instancia de la clase Libro de trabajo, que representa un archivo de Excel.
## Paso 3: Obtenga la hoja de trabajo y las celdas
A continuación, acceda a la primera hoja de cálculo del libro y recupere la colección de celdas donde ingresará los datos.

```csharp
// Obtenga la primera hoja de trabajo.
Worksheet sheet = workbook.Worksheets[0];
// Obtenga la colección de celdas de la hoja de trabajo.
Cells cells = sheet.Cells;
```

- Hoja de trabajo hoja: obtiene la primera hoja de trabajo del libro.
- Células células: obtiene la colección de celdas de la hoja de cálculo.
## Paso 4: Valores de entrada para el cuadro combinado
Ahora, necesitamos introducir algunos valores en las celdas. Estos valores servirán como opciones para el cuadro combinado.

```csharp
// Introduzca un valor.
cells["B3"].PutValue("Employee:");
// Ponlo en negrita.
cells["B3"].GetStyle().Font.IsBold = true;
// Ingrese algunos valores que indiquen el rango de entrada para el cuadro combinado.
cells["A2"].PutValue("Emp001");
cells["A3"].PutValue("Emp002");
cells["A4"].PutValue("Emp003");
cells["A5"].PutValue("Emp004");
cells["A6"].PutValue("Emp005");
cells["A7"].PutValue("Emp006");
```

- cells["B3"].PutValue: coloca la etiqueta "Empleado" en la celda B3.
- Font.IsBold = true: establece el texto en negrita para que se destaque.
- Rango de entrada: Introduce varios ID de empleados en las celdas A2 a A7. Estos aparecerán en el cuadro combinado desplegable.
## Paso 5: Agregar el cuadro combinado a la hoja de trabajo
El siguiente paso es agregar el cuadro combinado a la hoja de cálculo. Este cuadro combinado permitirá a los usuarios seleccionar uno de los ID de empleado ingresados anteriormente.

```csharp
// Agregar un nuevo cuadro combinado.
Aspose.Cells.Drawing.ComboBox comboBox = sheet.Shapes.AddComboBox(2, 0, 2, 0, 22, 100);
```

- AddComboBox: Agrega un nuevo cuadro combinado a la hoja de cálculo. Los números (2, 0, 2, 0, 22, 100) representan la posición y las dimensiones del cuadro combinado.
## Paso 6: Vincular el cuadro combinado a una celda y establecer el rango de entrada
Para que el cuadro combinado funcione, debemos vincularlo a una celda específica y definir el rango de celdas del que extraerá sus opciones.

```csharp
// Establecer la celda vinculada.
comboBox.LinkedCell = "A1";
// Establecer el rango de entrada.
comboBox.InputRange = "A2:A7";
```

- LinkedCell: Vincula la selección del cuadro combinado a la celda A1. El valor seleccionado del cuadro combinado aparecerá en esta celda.
- InputRange: define el rango de celdas (A2:A7) que contiene los valores que completarán las opciones del cuadro combinado.
## Paso 7: Personaliza la apariencia del cuadro combinado
Puede personalizar aún más el cuadro combinado especificando la cantidad de líneas desplegables y habilitando el sombreado 3D para una mejor estética.

```csharp
// Establezca el número de líneas de lista que se muestran en la parte de lista del cuadro combinado.
comboBox.DropDownLines = 5;
// Establezca el cuadro combinado con sombreado 3D.
comboBox.Shadow = true;
```

- DropDownLines: controla cuántas opciones serán visibles en el cuadro combinado desplegable a la vez.
- Sombra: agrega un efecto de sombreado 3D al cuadro combinado.
## Paso 8: Autoajustar columnas y guardar el libro
Por último, ajustemos automáticamente las columnas para lograr un diseño limpio y guardemos el libro de trabajo.

```csharp
// Autoajustar columnas
sheet.AutoFitColumns();
// Guarda el archivo.
workbook.Save(dataDir + "book1.out.xls");
```

- AutoFitColumns: ajusta automáticamente el ancho de las columnas para adaptarse al contenido.
- Guardar: guarda el libro como un archivo Excel en el directorio especificado.

## Conclusión
Añadir un cuadro combinado a tus hojas de cálculo de Excel con Aspose.Cells para .NET es un proceso sencillo que mejora considerablemente la flexibilidad de entrada de datos. Al crear controles de formulario mediante programación, puedes crear hojas de cálculo interactivas fácilmente. Este tutorial te mostró cómo añadir un cuadro combinado, vincularlo a una celda y configurar su rango de entrada, todo ello con Aspose.Cells.
Aspose.Cells ofrece una amplia gama de funciones para la manipulación de archivos de Excel, lo que lo convierte en la opción ideal para desarrolladores que buscan automatizar tareas de hojas de cálculo. Pruébelo con un [prueba gratuita](https://releases.aspose.com/).
## Preguntas frecuentes
### ¿Puedo usar Aspose.Cells sin Excel instalado?
Sí, Aspose.Cells funciona independientemente de Excel y no requiere que Excel esté instalado.
### ¿Cómo aplico una licencia en Aspose.Cells?
Puede solicitar una licencia obteniéndola en [aquí](https://purchase.aspose.com/buy) y llamando `License.SetLicense()` en su código.
### ¿Qué formatos admite Aspose.Cells para guardar archivos?
Aspose.Cells admite guardar archivos en múltiples formatos como XLSX, XLS, CSV, PDF y más.
### ¿Existe un límite en la cantidad de cuadros combinados que puedo agregar?
No, no hay un límite estricto; puedes agregar tantos cuadros combinados como requiera tu proyecto.
### ¿Cómo puedo obtener soporte para Aspose.Cells?
Puede obtener ayuda de la [Foro de Aspose](https://forum.aspose.com/c/cells/9).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}