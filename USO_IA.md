# USO_IA.md — Documentación de Apoyo con Inteligencia Artificial

**Asignatura:** Desarrollo Front End  
**Evaluación:** Sumativa 2  
**Institución:** INACAP Maipú  

---

## Herramienta utilizada

**Google Gemini / Antigravity** fue la herramienta de IA principal utilizada como par de programación durante el desarrollo. También se consultó **ChatGPT** para revisar patrones de validación con expresiones regulares.

---

## Prompts utilizados y mejoras incorporadas

### 1. Arquitectura del estado y estructura de datos

**Prompt:**
> "Tengo que hacer una app de cotizaciones en JavaScript vanilla. ¿Cuál es la mejor estructura de objetos para representar un presupuesto con capítulos e ítems? Necesito que se pueda guardar en localStorage."

**Mejora aplicada:**  
La IA sugirió un estado global centralizado `state = { budgets: [], materials: [], settings: {} }` donde cada presupuesto es un objeto con capítulos anidados y cada capítulo tiene un arreglo de ítems. Esto permite serialización directa con `JSON.stringify()` para localStorage.

```js
// Estructura sugerida por IA e implementada:
const state = {
  budgets: [],     // Array de objetos cotización
  materials: [],   // Array de objetos material del catálogo
  settings: {}     // Configuración del usuario
};
```

---

### 2. Validaciones con expresiones regulares

**Prompt:**
> "Necesito validar campos de un formulario en JavaScript con expresiones regulares. Necesito validar: (1) un nombre de empresa con entre 2 y 100 caracteres, (2) una URL de proveedor válida o vacía, (3) un número de cotización entero positivo, (4) un precio positivo con hasta 2 decimales."

**Regex generadas con apoyo de IA e implementadas:**

```js
const REGEX_NOMBRE = /^.{2,100}$/;
const REGEX_URL    = /^(https?:\/\/.+)?$/;
const REGEX_NUMERO = /^\d+$/;
const REGEX_PRECIO = /^\d+(\.\d{1,2})?$/;
```

La IA además recomendó no bloquear el guardado automático con estas validaciones, sino usarlas al hacer submit del modal para no interrumpir la experiencia del usuario.

---

### 3. Prevención de XSS con función de sanitización

**Prompt:**
> "Estoy usando innerHTML con datos ingresados por el usuario en mi app JavaScript. El profesor dijo que es una vulnerabilidad XSS. ¿Cómo sanitizo los datos sin librerías externas?"

**Mejora aplicada:**

La IA explicó que innerHTML con datos no escapados permite inyección de código HTML/JS malicioso. Sugirió esta función utilitaria:

```js
// Función de escape XSS sugerida por IA e implementada en el proyecto:
function sanitizeHTML(str) {
  const temp = document.createElement('div');
  temp.textContent = String(str || '');
  return temp.innerHTML;
}
```

Esta función convierte `<`, `>`, `"`, `&` en sus entidades HTML seguras, eliminando el riesgo de XSS.

---

### 4. Búsqueda sin tildes (normalización Unicode)

**Prompt:**
> "¿Cómo puedo hacer una búsqueda en JavaScript que ignore tildes? Por ejemplo, que 'ceramica' encuentre 'cerámica'."

**Mejora aplicada:**

```js
function removeAccents(str) {
  if (!str) return '';
  return str.normalize("NFD").replace(/[\u0300-\u036f]/g, "");
}
```

La IA explicó que `normalize("NFD")` descompone las letras acentuadas en su carácter base + el acento separado, y el regex elimina los caracteres de acento (U+0300–U+036F).

---

### 5. Exportación a Excel sin librerías externas

**Prompt:**
> "Quiero exportar una tabla a Excel desde JavaScript puro sin librerías como SheetJS. ¿Es posible?"

**Mejora aplicada:** La IA sugirió generar un documento HTML con namespace de Excel (`xmlns:o="urn:schemas-microsoft-com:office:excel"`) y descargarlo como `.xls` usando `Blob` y `URL.createObjectURL`. Implementado en `exportToExcel()`.

---

### 6. Sistema de pan & zoom táctil para vista previa

**Prompt:**
> "¿Cómo implemento pan y zoom con rueda del mouse en un div en JavaScript puro? También necesito que funcione con gestos táctiles (pinch to zoom)."

**Mejora aplicada:** La IA proporcionó la lógica base para los eventos `mousedown`, `wheel`, `touchstart`, `touchmove` con cálculo del punto focal del zoom centrado en el cursor.

---

## Secciones del código asistidas por IA

Ver comentarios `// [IA]` en el código fuente de `index.html`. Incluyen:

- `sanitizeHTML()` — función de escape XSS
- `validateMaterialForm()` — validación con regex del formulario de materiales
- `validateBudgetBeforePreview()` — validación antes de previsualizar
- `removeAccents()` — normalización Unicode para búsqueda
- `exportToExcel()` — técnica de exportación HTML-Excel con Blob
- Pan & zoom táctil — eventos touch y cálculo de escala focal

---

## Reflexión

El uso de IA fue como **par de programación**: se planteaban problemas específicos y se evaluaban las sugerencias antes de implementarlas. Ningún fragmento fue copiado sin comprenderlo. Las decisiones de arquitectura, diseño visual y flujo de la app fueron tomadas por el equipo.

La IA fue especialmente útil para:
- **Seguridad:** identificar y resolver el problema de XSS con innerHTML
- **Validaciones:** generar expresiones regulares para diferentes tipos de datos
- **APIs nativas:** técnicas como `normalize("NFD")`, `Blob`, `URL.createObjectURL`

---

*Sumativa 2 — INACAP Maipú 2026*
