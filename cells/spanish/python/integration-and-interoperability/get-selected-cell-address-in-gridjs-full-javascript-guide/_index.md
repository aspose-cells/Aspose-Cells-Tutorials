---
category: general
date: 2026-06-30
description: Aprende cómo obtener la dirección de la celda seleccionada, actualizar
  el valor de una celda de la cuadrícula y leer el valor de entrada con JavaScript
  usando GridJs. Código paso a paso y consejos.
draft: false
keywords:
- get selected cell address
- update grid cell value
- read input value with javascript
language: es
og_description: Obtén la dirección de la celda seleccionada, actualiza el valor de
  la celda de la cuadrícula y lee el valor de entrada con JavaScript. Sigue esta guía
  completa para una integración fluida de GridJs.
og_title: Obtener la dirección de la celda seleccionada – Tutorial completo de GridJs
  JavaScript
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Learn how to get selected cell address, update grid cell value and
    read input value with JavaScript using GridJs. Step‑by‑step code and tips.
  headline: Get Selected Cell Address in GridJs – Full JavaScript Guide
  type: TechArticle
tags:
- GridJs
- JavaScript
- DOM manipulation
title: Obtener la dirección de la celda seleccionada en GridJs – Guía completa de
  JavaScript
url: /es/python/integration-and-interoperability/get-selected-cell-address-in-gridjs-full-javascript-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtener la dirección de la celda seleccionada – Tutorial completo de GridJs JavaScript

¿Alguna vez necesitaste **obtener la dirección de la celda seleccionada** de una tabla GridJs pero no sabías qué llamada a la API usar? No eres el único. En muchos paneles de administración, los usuarios hacen clic en una celda, editan un valor en un modal y esperan que la cuadrícula refleje el cambio al instante. Este tutorial te muestra exactamente cómo recuperar esa dirección, leer el nuevo precio de un campo de entrada y **actualizar el valor de la celda de la cuadrícula** sin recargar la página.

También cubriremos **leer el valor de entrada con JavaScript** de la manera correcta, manejaremos casos límite y cerraremos el modal una vez que la actualización termine. Al final tendrás un fragmento autónomo que puedes insertar en cualquier proyecto que use GridJs.

## Lo que vas a construir

- Una tabla HTML simple impulsada por GridJs.
- Un modal de edición que aparece al hacer clic en una celda.
- JavaScript que **obtiene la dirección de la celda seleccionada**, captura el precio escrito por el usuario, **actualiza el valor de la celda de la cuadrícula** y finalmente oculta el modal.

No se requieren bibliotecas externas más allá de GridJs, y el código funciona con navegadores modernos (Chrome 102+, Edge, Firefox). Si ya tienes una instancia de GridJs en la página, puedes copiar‑pegar directamente las partes relevantes.

## Requisitos previos

- Conocimientos básicos de JavaScript y del DOM.
- Biblioteca GridJs cargada (via CDN o npm).
- Una página que ya renderice una cuadrícula GridJs (mostraremos un ejemplo mínimo).

Si alguno de estos conceptos te resulta desconocido, no te alarmes: cada paso incluye un breve repaso.

---

## Paso 1: Configurar el esqueleto HTML

Primero, define el contenedor de la tabla, el modal oculto y la entrada de precio. El modal se mostrará mediante clases CSS simples.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GridJs Edit Example</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    /* Quick modal styling – feel free to replace with your UI framework */
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script src="script.js"></script>
</body>
</html>
```

> **Consejo profesional:** El `#editModal` usa un truco CSS mínimo—simplemente agrega la clase `active` para mostrarlo. Puedes sustituirlo por Bootstrap, Tailwind o cualquier componente modal que ya utilices.

---

## Paso 2: Inicializar GridJs y capturar clics en celdas

Ahora crearemos una cuadrícula con datos de ejemplo y escucharemos las selecciones de celdas. Cuando el usuario haga clic en una celda, **obtendremos la dirección de la celda seleccionada** y abriremos el modal.

```javascript
// script.js
const grid = new gridjs.Grid({
  columns: ['Item', 'Quantity', 'Price'],
  data: [
    ['Apple', 10, 0.5],
    ['Banana', 5, 0.3],
    ['Cherry', 20, 0.2]
  ],
  pagination: { limit: 5 },
  sort: true,
  // Enable cell selection – GridJs provides a helper for this
  style: {
    table: {
      'width': '100%'
    }
  }
}).render(document.getElementById('grid'));

// Helper to store the address of the last clicked cell
let lastSelectedCell = null;

// GridJs emits a 'cell' event when any cell is clicked
grid.on('cell', (event) => {
  // Step 2a: Get selected cell address
  const address = GridJs.getSelectedCell(); // <-- primary operation
  lastSelectedCell = address; // remember for later update

  // Show the modal
  document.getElementById('editModal').classList.add('active');

  // Optional: pre‑fill the input with the current cell value
  const currentValue = event.target.innerText;
  document.getElementById('price').value = currentValue;
});
```

> **Por qué funciona:** `GridJs.getSelectedCell()` devuelve una cadena como `"C2"` (columna C, fila 2). Guardarla en `lastSelectedCell` nos permite referirnos a la ubicación exacta cuando más tarde **actualicemos el valor de la celda de la cuadrícula**.

---

## Paso 3: Leer el nuevo precio del campo de entrada

Cuando el usuario haga clic en **Guardar**, necesitamos **leer el valor de entrada con JavaScript** de forma segura. Este paso también valida que el precio ingresado sea un número positivo.

```javascript
document.getElementById('saveBtn').addEventListener('click', () => {
  // Step 3a: Grab the raw string from the input
  const raw = document.getElementById('price').value;

  // Step 3b: Convert to a number and validate
  const newPrice = parseFloat(raw);
  if (isNaN(newPrice) || newPrice < 0) {
    alert('Please enter a valid positive number.');
    return;
  }

  // Proceed to update the cell
  updateSelectedCell(newPrice);
});
```

> **Nota:** Usar `parseFloat` asegura que aceptemos decimales (p. ej., `1.99`). La verificación `isNaN` evita envíos accidentales vacíos.

---

## Paso 4: Actualizar el valor de la celda seleccionada

Ahora finalmente **actualizamos el valor de la celda de la cuadrícula** usando la dirección que capturamos antes. El método `updateCell` de GridJs devuelve una promesa, por lo que podemos encadenar una acción de cierre del modal.

```javascript
function updateSelectedCell(value) {
  if (!lastSelectedCell) {
    console.warn('No cell selected – nothing to update.');
    return;
  }

  // Step 4a: Call GridJs.updateCell(address, newValue)
  GridJs.updateCell(lastSelectedCell, value)
    .then(() => {
      // Step 4b: Close the modal once the grid refreshes
      document.getElementById('editModal').classList.remove('active');
      // Reset stored address
      lastSelectedCell = null;
    })
    .catch(err => {
      console.error('Failed to update cell:', err);
      alert('Could not save the new price. Try again.');
    });
}
```

> **¿Por qué usar una promesa?** GridJs puede necesitar volver a renderizar la tabla o sincronizarse con un backend. Al esperar la promesa garantizamos que la UI solo se oculte después de que la cuadrícula refleje el nuevo valor.

---

## Paso 5: Manejar Cancelar y casos límite

Una solución robusta siempre brinda al usuario una salida. El botón **Cancelar** simplemente oculta el modal y borra cualquier dirección almacenada.

```javascript
document.getElementById('cancelBtn').addEventListener('click', () => {
  document.getElementById('editModal').classList.remove('active');
  lastSelectedCell = null;
});
```

### ¿Qué pasa si no se seleccionó ninguna celda?

Si un usuario de alguna manera activa el botón **Guardar** sin haber hecho clic en una celda primero (quizá abrió el modal programáticamente), `lastSelectedCell` será `null`. El retorno temprano en `updateSelectedCell` evita un error en tiempo de ejecución y registra una advertencia útil.

### Trabajando con cuadrículas grandes

Para cuadrículas con paginación, `GridJs.getSelectedCell()` sigue devolviendo la dirección absoluta (p. ej., `"B12"`), no solo la fila visible. Esto significa que la actualización funciona incluso si la fila editada está en otra página. Solo ten en cuenta que la UI no cambiará automáticamente de página después de una actualización; si lo necesitas, llama a `grid.forceUpdate()` o navega a la página correspondiente manualmente.

---

## Ejemplo completo y funcional

A continuación tienes el código completo que puedes copiar‑pegar en un solo archivo HTML. Ábrelo en un navegador, haz clic en cualquier celda, cambia el precio y observa cómo la cuadrícula se actualiza al instante.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Get Selected Cell Address – GridJs Demo</title>
  <link href="https://cdn.jsdelivr.net/npm/gridjs/dist/theme/mermaid.min.css" rel="stylesheet"/>
  <style>
    #editModal { display:none; position:fixed; top:20%; left:50%; transform:translateX(-50%);
                 background:#fff; padding:1rem; border:1px solid #ccc; box-shadow:0 4px 8px rgba(0,0,0,.1);}
    #editModal.active { display:block; }
  </style>
</head>
<body>

<div id="grid"></div>

<div id="editModal" aria-modal="true" role="dialog">
  <h3>Edit Price</h3>
  <input type="number" id="price" placeholder="Enter new price"/>
  <button id="saveBtn">Save</button>
  <button id="cancelBtn">Cancel</button>
</div>

<script src="https://cdn.jsdelivr.net/npm/gridjs/dist/gridjs.umd.js"></script>
<script>
  // Initialise the grid
  const grid = new gridjs.Grid({
    columns: ['Item', 'Quantity', 'Price'],
    data: [
      ['Apple', 10, 0.5],
      ['Banana', 5, 0.3],
      ['Cherry', 20, 0.2]
    ],
    pagination: { limit: 5 },
    sort: true
  }).render(document.getElementById('grid'));

  let lastSelectedCell = null;

  // Capture cell clicks – this is where we **get selected cell address**
  grid.on('cell', (event) => {
    const address = GridJs.getSelectedCell();   // primary keyword usage
    lastSelectedCell = address;
    document.getElementById('editModal').classList.add('active');
    document.getElementById('price').value = event.target.innerText;
  });

  // Save button – **read input value with JavaScript**
  document.getElementById('saveBtn').addEventListener('click', () => {
    const raw = document.getElementById('price').value;
    const newPrice = parseFloat(raw);
    if (isNaN(newPrice) || newPrice < 0) {
      alert('Please enter a valid positive number.');
      return;
    }
    updateSelectedCell(newPrice);
  });

  // Core update logic – **update grid cell value**
  function updateSelectedCell(value) {
    if (!lastSelectedCell) {
      console.warn('No cell selected – nothing to update.');
      return;
    }
    GridJs.updateCell(lastSelectedCell, value)
      .then(() => {
        document.getElementById('editModal').classList


## ¿Qué deberías aprender a continuación?


Los siguientes tutoriales cubren temas estrechamente relacionados que amplían las técnicas demostradas en esta guía. Cada recurso incluye ejemplos de código completos con explicaciones paso a paso para ayudarte a dominar funcionalidades adicionales de la API y explorar enfoques de implementación alternativos en tus propios proyectos.

- [Obtener dirección, recuento de celdas y desplazamiento para todo el rango de Excel](/cells/english/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Obtener dirección, recuento de celdas y desplazamiento para todo el rango de Excel](/cells/german/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)
- [Obtener dirección, recuento de celdas y desplazamiento para todo el rango de Excel](/cells/french/net/excel-range-address-calculation/get-address-cell-count-and-offset-for-entire-excel-range/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}