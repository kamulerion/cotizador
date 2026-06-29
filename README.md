# 🏗️ Cotizador de Construcción

> Aplicación web interactiva para generar cotizaciones/presupuestos de obras y remodelaciones.  
> **Sumativa 2 — Desarrollo Front End | INACAP Maipú 2026**

---

## 🔗 Demo en vivo

👉 **[Ver aplicación en GitHub Pages](https://kamulerion.github.io/cotizador/)**

---

## 📋 Descripción

Aplicación SPA (Single Page Application) desarrollada en **HTML, CSS y JavaScript vanilla** (sin frameworks ni librerías externas) que permite:

- Crear, editar, duplicar y eliminar **cotizaciones** organizadas por capítulos
- Gestionar un **catálogo de 100 materiales** de construcción chilenos (Sodimac, Construmart, Red MTS, Imperial, Prodalam)
- Calcular totales de **materiales, mano de obra y utilidad** en tiempo real
- Exportar cotizaciones a **PDF** (vía impresión) y **Excel (.xls)**
- **Búsqueda en tiempo real** con normalización de acentos
- Guardado automático en **localStorage** con sistema de backup/restore JSON
- Interfaz completamente **responsive** (desktop y móvil)

---

## 🎯 Conceptos evaluados aplicados

| Criterio | Implementación |
|---|---|
| **Formularios + validación JS** | Validación con regex en modal de materiales y cotizaciones; sanitización XSS |
| **Arreglos y objetos** | Estado global `state = { budgets[], materials[], settings{} }` con CRUD completo |
| **Manipulación del DOM** | Renderizado dinámico de listas, tablas, capítulos e ítems en tiempo real |
| **Funciones reutilizables** | `sanitizeHTML()`, `validateMaterialForm()`, `removeAccents()`, `formatCLP()`, etc. |
| **Seguridad (anti-XSS)** | Función `sanitizeHTML()` aplicada en todos los puntos de inserción de datos de usuario |
| **localStorage** | Persistencia completa + exportación/importación de backup en JSON |

---

## 🚀 Tecnologías

- **HTML5** semántico
- **CSS3** con variables custom (`--primary`, `--bg-card`, etc.) y diseño responsive
- **Vanilla JavaScript ES6+** — sin dependencias externas
- **localStorage** para persistencia de datos

---

## 📁 Estructura del proyecto

```
📦 cotizador/
├── index.html              # Aplicación completa (HTML + CSS + JS)
├── catalogo_materiales.json # Catálogo de materiales de referencia
├── USO_IA.md               # Documentación de uso de IA
└── README.md               # Este archivo
```

---

## 🤖 Uso de IA

Durante el desarrollo se utilizó **Google Gemini** como par de programación y **ChatGPT** para revisar patrones de validación.

### Prompts principales y mejoras aplicadas

**1. Sanitización XSS**
> *"Estoy usando innerHTML con datos del usuario. ¿Cómo prevengo XSS sin librerías externas?"*

➜ La IA sugirió la función `sanitizeHTML()` que usa el propio DOM para escapar caracteres peligrosos:
```js
// [IA] Función sugerida por IA para prevenir XSS
function sanitizeHTML(str) {
  const temp = document.createElement('div');
  temp.textContent = String(str || '');
  return temp.innerHTML;
}
```

**2. Validaciones con expresiones regulares**
> *"Necesito validar nombre de empresa (2-100 chars), URL de proveedor válida o vacía, número entero positivo y precio con hasta 2 decimales."*

➜ La IA generó las regex y recomendó encapsularlas en una función modular reutilizable `validateMaterialForm()`.

**3. Búsqueda sin tildes**
> *"¿Cómo hago búsqueda que ignore acentos? Que 'ceramica' encuentre 'cerámica'."*

➜ Técnica `normalize("NFD")` sugerida por IA e implementada en `removeAccents()`.

**4. Estructura de datos escalable**
> *"¿Cuál es la mejor estructura de objetos para un presupuesto con capítulos e ítems guardable en localStorage?"*

➜ Diseño del estado global centralizado con arreglos anidados.

📄 Ver documentación completa: [`USO_IA.md`](./USO_IA.md)

---

## ⚙️ Cómo ejecutar localmente

No requiere instalación ni servidor. Solo abre `index.html` en cualquier navegador moderno:

```bash
# Opción 1: doble clic sobre index.html
# Opción 2: desde terminal
start index.html        # Windows
open index.html         # macOS
xdg-open index.html     # Linux
```

---

**Asignatura:** Desarrollo Front End  
**Institución:** INACAP Maipú  
**Año:** 2026
