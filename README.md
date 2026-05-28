# Character Counter

Interfaz web estática inspirada en el diseño de referencia entregado. Replica fielmente el layout, colores, tipografía y componentes del mockup original.

---

## 1. Objetivo del proyecto

Desarrollar una interfaz de análisis de texto que incluya:
- Header con logo e ícono de configuración
- Título hero bold italic centrado
- Textarea estilizada para ingreso de texto
- Controles: checkboxes y reading time
- 3 tarjetas de métricas con colores y patrones decorativos
- Sección "Letter Density" con barras de progreso CSS puras
- Sin JavaScript — valores hardcodeados

---

## 2. Tecnologías utilizadas

| Tecnología | Propósito |
|---|---|
| HTML5 semántico | Estructura del documento |
| CSS3 con custom properties | Estilos, layout, variables |
| CSS Grid | Cards de métricas (3 columnas) y filas de Letter Density |
| Flexbox | Header, controles, listas |
| Google Fonts — DM Sans | Tipografía principal italic bold |

---

## 3. Cómo está organizado el HTML

```
index.html
├── <header>              → Logo + botón settings (SVG inline)
└── <main>
    ├── <section.hero>    → H1 bold italic
    ├── <section.editor>  → <textarea> + controles
    │   └── .editor__controls
    │       ├── checkboxes personalizados
    │       └── reading time (texto alineado derecha)
    ├── <section.metrics> → 3 <article> (cards de estadísticas)
    └── <section.density> → título + filas de letra/barra/stats
```

**Decisiones semánticas:**
- Se usa `<article>` para cada tarjeta de métrica (contenido independiente)
- El textarea es `<textarea>`, no `<div>` ni `<p>` como exige la consigna
- Los controles usan `<label>` correctamente asociados a sus inputs
- SVGs de íconos son inline para control total del estilo

---

## 4. Cómo se resolvió el CSS

### Variables CSS (`:root`)
Toda la paleta, espaciados, radios y sombras como custom properties. Facilita consistencia y futuros cambios de tema.

### Textura de fondo
Se replica la textura de puntos del diseño de referencia con:
```css
background-image: radial-gradient(circle, rgba(255,255,255,0.04) 1px, transparent 1px);
background-size: 28px 28px;
```

### Cards de métricas
- `display: grid` con `repeat(3, 1fr)` para las 3 columnas
- Fondo sólido de color (violeta / naranja / coral)
- Patrón decorativo en esquina superior derecha: doble `linear-gradient` formando cuadrícula, `opacity: 0.25`
- `position: relative` + `overflow: hidden` para contener el patrón

### Barras de progreso (Letter Density)
Técnica investigada e implementada: dos `<div>` anidados:
- `.density__bar-track` — carril con fondo oscuro, `border-radius: 999px`
- `.density__bar-fill` — relleno con `width` inline como porcentaje, color `#A855F7`

No se usan SVG, `<meter>`, `<progress>` ni librerías externas. CSS puro.

### Layout de filas de Letter Density
```css
grid-template-columns: 18px 1fr auto;
```
Columna fija para la letra, columna flexible para la barra, columna automática para los números.

### Checkboxes personalizados
El input nativo se oculta con `opacity: 0`. El `<span.checkbox-custom>` actúa como visual.
Al marcar el input, el selector `input:checked + .checkbox-custom` activa fondo violeta y un checkmark con `::after`.

---

## 5. Dificultades encontradas

1. **Replicar la textura de fondo** del mockup — se resolvió con `radial-gradient` repetido como patrón puntual.

2. **Patrón geométrico en las cards** — se logró con `background-image` de doble `linear-gradient` formando grilla, con baja opacidad sobre el color de la card.

3. **Alineación de filas de Letter Density** — lograr que letra, barra y estadísticas queden perfectamente en línea en distintos tamaños requirió ajustar el grid de 3 columnas y el `min-width` del stats.

4. **Tipografía italic bold del título** — el diseño de referencia usa una fuente condensada bold italic. Se eligió **DM Sans** italic 700 que lo replica bien.

---

## 6. Capturas del resultado final

> *(Agregar screenshots una vez finalizado y subido a GitHub Pages o similar)*

---

## Cómo correr el proyecto

```bash
# Sin instalación — abrir directamente:
open index.html

# O con Live Server en VS Code:
# Click derecho en index.html → "Open with Live Server"
```

---

## Estructura de carpetas

```
text-analyzer/
├── index.html
├── styles/
│   └── main.css
├── assets/
│   └── images/
└── README.md
```

---

## Commits sugeridos (mínimo 10)

```
feat: estructura HTML inicial con header y hero
feat: agregar textarea y section editor
feat: agregar section de cards de métricas
feat: agregar section Letter Density con barras
style: variables CSS y paleta de colores
style: estilar header con logo y botón settings
style: estilar hero con tipografía bold italic
style: estilar textarea y controles
style: estilar cards con colores, patrones y hover
style: implementar barras de progreso CSS puras
style: textura de fondo con radial-gradient
style: responsive mobile y tablet
docs: agregar README completo
```
