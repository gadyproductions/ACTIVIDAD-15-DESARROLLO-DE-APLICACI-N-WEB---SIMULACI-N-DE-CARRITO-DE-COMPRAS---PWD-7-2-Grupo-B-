# 📋🛒 ACTIVIDAD 15: DESARROLLO DE APLICACIÓN WEB - SIMULACIÓN DE CARRITO DE COMPRAS / SELECTOR REACTIVO
### Estándar Internacional: e-Commerce & State Management in Vanilla JS

---

## 🏛️ Datos Institucionales y Académicos
* **Institución Educativa:** E.E.S.T. N.º 1 *"Eduardo Ader"* - Vicente López
* **Materia:** Proyecto de Implementación de Sitios Web Dinámicos (PWD)
* **Curso y División:** 7° año 2° división - Grupo B (Miércoles de 17:35 a 21:45 hs)
* **Cuatrimestre:** 2° Cuatrimestre 2026
* **Profesor:** Mansilla Muñoz York Elías ([@docentedeclasesdeapoyo](https://github.com/docentedeclasesdeapoyo))
* **Alumno:** **Gadiel Siles**
* **Grupo de Proyecto Integrador:** **Grupo 4 - SIMC (Sistema Inteligente de Monitoreo y Control)**

---

## 🎯 1. Introducción y Contexto

Al utilizar aplicaciones web de comercio electrónico modernas (como Mercado Libre o PedidosYa), la aplicación necesita gestionar y "recordar" qué elementos o ítems va seleccionando el usuario en tiempo real sin requerir una recarga completa de la página cada vez que se produce una interacción. A esta memoria de datos volátil o temporal de la aplicación la denominamos **Estado (State)**.

Este proyecto implementa una arquitectura completa de **gestión reactiva de estado en Vanilla JavaScript**, cumpliendo con los estándares de reactividad, persistencia local y reducción matemática exigidos en la currícula.

---

## 🧠 2. Conceptos Fundamentales Implementados

### A. El Estado (State)
El estado es la estructura central de datos (un arreglo `carrito = []` de objetos) en la memoria del navegador que representa la selección viva del usuario:
```javascript
// Base de datos simulada de sensores y componentes
const productos = [
  { id: 1, nombre: "Sensor IoT de Flujo", precio: 4500 },
  { id: 2, nombre: "Módulo GPS Antirrobo", precio: 8200 },
  { id: 3, nombre: "Licencia Software Premium", precio: 12000 }
];

// Estado reactivo inicial (recuperado de memoria o vacío)
let carrito = JSON.parse(localStorage.getItem('pwd_carrito')) || [];
```

### B. Reactividad en Vanilla JS
Significa que cada vez que el estado muta (se agrega un ítem con `push()`, se quita con `splice()`, o se vacía con `[]`), se invoca de inmediato a la función `renderizarCarrito()` que se encarga de re-sincronizar el DOM:
```javascript
function agregarAlCarrito(id) {
  const producto = productos.find(p => p.id === id);
  carrito.push(producto);
  guardarYActualizar(); // Dispara persistencia y re-renderizado
}

function eliminarItem(index) {
  carrito.splice(index, 1);
  guardarYActualizar();
}
```

### C. Persistencia con `localStorage`
Permite almacenar los datos del carrito en el almacenamiento persistente del navegador bajo la clave `'pwd_carrito'`, garantizando que si el usuario recarga la página (<kbd>F5</kbd>) o cierra la pestaña, la selección no se pierda:
```javascript
function guardarYActualizar() {
  localStorage.setItem('pwd_carrito', JSON.stringify(carrito));
  renderizarCarrito();
}
```

### D. Cálculo Matemático con `.reduce()`
En lugar de recurrir a bucles imperativos manuales (`for` o `while`), el total acumulado se calcula de forma declarativa y funcional mediante `Array.prototype.reduce()`:
$$\text{Total} = \sum_{i=1}^n p_i$$

```javascript
// Recorre el arreglo 'carrito' y acumula la suma de los precios arrancando desde 0
const total = carrito.reduce((acumulado, producto) => acumulado + producto.precio, 0);
totalEl.textContent = total.toFixed(2);
```

---

## 🔗 3. Articulación con el Proyecto Integrador (Expo Técnica)
### **Grupo 4: SIMC (Sistema Inteligente de Monitoreo y Control)**
Conforme a lo especificado en la Sección 4 de la consigna:
> *"Grupo 3 (EVA) / Grupo 4 (SIMC): Usar la lista para acumular un historial de sensores y/o eventos seleccionados para generar un reporte agrupado."*

La aplicación incorpora una segunda pestaña dedicada que permite:
1. **Auditar eventos y anomalías de sensores en tiempo real:** Eventos críticos de sensores de flujo, módulos GPS de seguridad, sensores ambientales de calidad de aire MQ-135 y nodos de telemetría LoRaWAN.
2. **Selector Reactivo de Telemetría:** Acumular incidentes y métricas en memoria local.
3. **Métricas Agrupadas con `.reduce()`:**
   - Consumo acumulado de corriente ($\text{mA}$).
   - Ponderación de severidad media del sistema.
4. **Generación de Reporte Agrupado Oficial SIMC:** Modal formal e imprimible/exportable con carátula académica y resumen analítico.

---

## 🚀 4. Puesta en Marcha y Uso

### Ejecución Local
No requiere instalación de dependencias externas ni compiladores (Vanilla JS puro).

1. Clonar el repositorio:
   ```bash
   git clone https://github.com/gadyproductions/ACTIVIDAD-15-DESARROLLO-DE-APLICACI-N-WEB---SIMULACI-N-DE-CARRITO-DE-COMPRAS---PWD-7-2-Grupo-B-.git
   ```
2. Abrir el archivo `index.html` en cualquier navegador web moderno (Google Chrome, Mozilla Firefox, Microsoft Edge, etc.) haciendo doble clic sobre el archivo o utilizando la extensión *Live Server* de Visual Studio Code.

### Comprobación de Requerimientos del Docente
* **Catálogo interactivo:** Botones `+ Agregar` en cada tarjeta de producto.
* **Badge contador:** Refleja la cantidad total en `#contador-badge`.
* **Cálculo en vivo:** Elemento `#total-compra` actualizado con `.reduce()`.
* **Persistencia:** Al recargar la página (<kbd>F5</kbd>), el estado se mantiene íntegro gracias a `localStorage`.
* **Eliminación individual:** Botones `❌` por cada ítem de la lista.
* **Vaciado general:** Botón `Vaciar Lista` para resetear el estado y el almacenamiento.

---

## 📂 5. Estructura del Repositorio

```plaintext
├── index.html       # Solución unificada: Estructura HTML5, estilos CSS Glassmorphism y lógica JS reactiva
├── README.md        # Documentación técnica completa y justificación pedagógica
└── 📋🛒🗂️ ACTIVIDAD 15_...pdf # Documento de consigna pedagógica oficial 2026
```

---

> *"Programar no es hacer magia onda Rada; es simplemente guardar los datos en una lista y volver a dibujarla/recrearla en pantalla cada vez que algo cambia."* 🚀