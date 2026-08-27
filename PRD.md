<!-- MOTION-CONTRACT
protagonista: pinned-saga
soporte: gallery-scroll-scale, blur-in-word, liquid-glass, grain, scramble
assets: assets/zapienz_mark.svg
-->

# PRD — Zapienz landing

## 1. Negocio y objetivo

App móvil de "Zaps": resúmenes de libros de no ficción en texto y audio, generados
con apoyo de IA. **305 Zaps publicados**, 10 categorías, ~20 min por Zap.
Monetiza con suscripción (RevenueCat) y créditos por libro.

- **Target**: hispanohablantes que quieren leer más y no tienen tiempo. Lectores
  de no ficción, profesionistas, estudiantes.
- **Objetivo**: descargas en App Store y Google Play.
- **KPI**: clics en los botones de tienda.
- **Brand DNA**: el arquetipo es *el sabio accesible* — sabe mucho y no te lo
  restriega. Tono: claro, cálido, sin humo motivacional.
- **Diferenciador real**: catálogo propio de 305 títulos en español, con audio.
- **Prueba real**: 5.0 de promedio en 18 valoraciones dentro de la app.

## 2. Concepto creativo

**La biblioteca se despliega.** La landing no dice que hay catálogo: lo enseña.
Al bajar, un panel se fija y las 305 portadas reales emergen y escalan según su
posición. El activo del negocio ES el espectáculo — y nadie más lo tiene.

## 3. Identidad visual

| Rol | Hex | Origen |
|---|---|---|
| Fondo profundo | `#0B1F3A` | del logo |
| Fondo secundario | `#313A59` | de la app |
| Primario claro | `#C9B6FF` | lavanda de la app |
| Acento | `#7C6BFF` | violeta de la app |
| Cálido / CTA | `#FFC86B` → `#FFD700` | dorado de la app + naranja del logo |
| Texto sobre oscuro | `#F6F7FB` | de la app |

**Tipografía**: Cormorant Garamond (display, literaria) + Inter (cuerpo).
Validadas contra la base de datos de pairings — nunca fuentes de sistema.

**Firma visual**: *el rayo sobre papel*. El grano de papel impreso (filtro SVG
`feTurbulence`) cubre los fondos, y el rayo del logo aparece como motivo — la
tensión exacta de la marca: la lentitud del libro contra la velocidad del Zap.
El dorado es canto de libro, no acento tecnológico: por eso esto no es
intercambiable con ninguna landing de IA.

## 4. Motion

- **Tipo de hero**: tipográfico con portadas reales flotando en profundidad.
- **Nivel de inmersión**: **3 — espacio navegable**. El scroll no decora: transforma
  el producto ante los ojos del visitante. Es la carta de presentación de GamaLabs
  como constructora de sitios, así que la vara es la página de producto de Apple.
- **Protagonista**: `pinned-saga` — una sola escena sticky de 720vh donde el objeto
  muta por capítulos ligados al progreso del scroll:
  1. un libro real del catálogo entra girando en perspectiva;
  2. **se abre** — la tapa rota 168° en Y y las hojas se despliegan;
  3. **se compacta** — el volumen colapsa en la tarjeta del Zap;
  4. **se vuelve voz** — la tarjeta se disuelve en 44 barras de onda que laten;
  5. **el teléfono sube desde abajo girando** (rotateY 200°→0) con el logo y la
     UI real de la app, y las ondas entran en su pantalla.
  Clave registrada en `verifica-motion.py` el 27-ago-2026: no existía ninguna para
  "objeto que muta por capítulos dentro de un pin".
- **Hilo de audio continuo**: canvas fijo tras toda la página con tres capas de onda
  que recorren el ancho; su amplitud sube al entrar en la saga y alcanza el pico en
  el capítulo de la voz. Es el hilo que cose el sitio entero.
- **Soporte**:
  - `gallery-scroll-scale` — las 305 portadas emergen en el panel de biblioteca
  - `blur-in-word` — titulares que enfocan palabra por palabra
  - `liquid-glass` — nav pill y tarjetas de precio
  - `grain` — textura de papel en todos los fondos
  - `scramble` — el contador de Zaps se decodifica al entrar en viewport
- **Fallbacks**: `prefers-reduced-motion` deja las portadas estáticas en grilla;
  sin JS el contenido completo sigue legible; efectos de cursor solo en desktop.

## 5. Secciones

1. **Hero** — "305 libros que no vas a leer. Nosotros ya los leímos." CTA a tiendas.
2. **El problema** — la pila de libros pendientes; el dato de 20 minutos.
3. **Cómo funciona** — leer o escuchar, tú eliges.
4. **La biblioteca** ← showstopper, portadas reales.
5. **Precios** — suscripción y créditos.
6. **Prueba social** — 5.0 ★ · 18 valoraciones (cifra real y visible).
7. **CTA final + footer** — con enlaces legales reales.

## 6. Assets

- 28 portadas reales desde el bucket público de Supabase (URLs directas).
- Logo y marca SVG del repo de la app.
- Sin generación de IA: todo el material visual es real del producto.

## 7. Técnico

- HTML/CSS/JS vanilla, cero dependencias salvo Google Fonts.
- Hosting: GitHub Pages con `CNAME` a `zapienz.gamalabs.mx`.
- Presupuesto: LCP < 2.5s, página < 5MB.
- Incluye `/privacidad`, `/terminos` y `/eliminar-cuenta` — cierra el hueco legal
  detectado en la auditoría del 27-ago-2026.

## 8. Criterios de aceptación

- Gate `verifica-motion.py --contrato` en exit 0.
- Prueba del logo tapado: el grano de papel + el rayo + las portadas reales hacen
  el hero imposible de reusar para otra marca.
- QA: consola limpia, mobile, reduced-motion, contraste AA, un solo `<h1>`.
