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

Tomada de `lib/theme/colors.dart`, el sistema de diseño real de la app.

| Rol | Hex | Nombre en la app |
|---|---|---|
| Fondo profundo | `#081225` | `darkBackground` |
| Fondo secundario | `#0F1B38` | `darkSurface` |
| Tarjeta | `#13244A` | `darkCard` |
| **Marca / CTA** | `#1DB954` | `primary` |
| Verde claro | `#4ADE80` | `primaryLight` |
| Verde del símbolo | `#38EB6B` | del PNG del icono |
| Acento frío | `#19D3C5` | `accentTeal` |
| Texto | `#F8FAFC` / `#B7C2D9` | `darkText*` |

> **Corrección del 27-ago-2026.** La primera versión usó lavanda `#C9B6FF`,
> violeta `#7C6BFF` y dorado `#FFD700`: ninguno pertenece a la marca. Salieron de
> contar literales de color en el código —gradientes decorativos sueltos— en vez
> de leer el sistema de diseño. El resultado se veía correcto y era de otra marca.
> Lección: la identidad se lee del theme y de los assets, nunca de un `grep`.

**Tipografía**: **Fraunces** (display) + Inter (cuerpo). Se descartó Cormorant
Garamond: es una serif de lujo clásico y chocaba con una marca de verde vibrante
y símbolo minimalista. Fraunces mantiene el aire editorial —son libros— pero es
contemporánea.

**Firma visual**: *el libro que suena*. El logo de Zapienz ya es exactamente eso
—un libro abierto con ondas de audio verdes— y la saga lo pone en movimiento: el
libro se abre y se convierte en esas mismas ondas. El grano de papel cubre los
fondos. Ninguna otra marca puede usar este hero: son sus portadas, su símbolo y
su historia.

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
