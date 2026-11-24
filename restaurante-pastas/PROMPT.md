# Prompt: landing page "Solo Pastas – Oeste-Lincoln"

Crea una landing page profesional en un solo archivo `index.html` (HTML + CSS + JS puro, sin frameworks) para **"Solo Pastas – Oeste-Lincoln"**, restaurante italiano de pastas en Cochabamba, Bolivia. Todo el texto en español. Las imágenes van en una carpeta `img/`.

## Identidad visual
- Paleta del logo: amarillo **#F2E229** (dominante), rojo **#E1141E**, verde **#2E9E5B**, tinta **#1B1A17**, crema **#FFFBEA** para fondos claros.
- Para que el texto se lea bien (contraste AA): rojo de texto **#BE0F18**, rojo de botones **#CF111A**, fondo rojo de secciones **#C8101A**, verde oscuro **#1F7843** cuando lleva texto blanco.
- Usa la franja de la bandera italiana (verde / blanco / rojo) como motivo que se repite en toda la página.
- Tipografías (Google Fonts): **Alfa Slab One** para títulos, **Rubik** (400–700) para el texto.
- Botones tipo píldora con una sombra sólida abajo (efecto 3D): suben 2px al pasar el mouse y se hunden al hacer clic.
- Variables CSS en `:root`. Contenedor de 1200px con margen lateral `clamp(16px,4vw,40px)`.

## Imágenes (`img/`)
- `logo.png`: logo circular.
- `local.jpg`: foto de la fachada del local.
- `plato-principal.jpg`: fettuccine verde con filete.
- `lasagna.jpg`: lasagna gratinada.
- `pan-ajo.jpg`: pan con ajo.

## 1) Navbar fija (sticky)
- Izquierda: logo circular y el nombre "Solo Pastas" con el subtítulo "OESTE · LINCOLN".
- Links: Inicio, Menú, Cómo pedir, Visítanos. Botón rojo "Pedir ahora".
- Al bajar 40px se compacta: menos padding, logo más chico y sombra.
- Se oculta al bajar (pasados 160px) y reaparece al subir. Usa requestAnimationFrame.
- Barra de progreso de lectura abajo, con los colores de la bandera.
- El link activo cambia según la sección visible, con IntersectionObserver (rootMargin `-45% 0px -50% 0px`) y un subrayado rojo animado.
- Con menos de 860px pasa a menú hamburguesa:
  - El menú ocupa toda la pantalla, con fondo amarillo.
  - El botón tiene `aria-expanded` y su etiqueta cambia entre abrir y cerrar.
  - Se cierra con Escape o al tocar un link.
  - Bloquea el scroll de la página mientras está abierto.

## 2) Scroll reveal
- Clase `.reveal` con las variantes `.left`, `.right` y `.zoom`.
- IntersectionObserver con threshold 0.15. Cada elemento se anima una sola vez (`unobserve`).
- Retraso escalonado con la variable CSS `--d` (ejemplo: `style="--d:150ms"`).
- Solo se oculta cuando hay JS (`html.js .reveal`).
- Respeta `prefers-reduced-motion`: sin animación y todo visible.

## Secciones

### Hero (fondo amarillo)
- Patrón sutil de puntos.
- Badge: "OESTE · Parque Lincoln · Cochabamba".
- H1: "Aquí solo hacemos **pasta.**". La palabra "pasta." va en rojo, con un subrayado verde ondulado en SVG que se dibuja al cargar.
- Texto: "Spaghetti, fettuccine, raviolis y lasagnas al horno, con salsas de la casa y pasta a elección. Ven a comer frente al Parque Lincoln o pide en línea para llevar."
- Botones: "Pedir ahora" (rojo, con ícono de carrito) y "Ver el menú" (contorno).
- Datos destacados: "Bs 52 – Pasta desde", "4 pastas – Larga · Corta · Verde · Sin gluten", "4 sucursales – En Cochabamba".
- A la derecha, un **plato de spaghetti en SVG**:
  - Plato con degradado y la franja italiana en el borde.
  - Nido de fideos generado con JS: elipses con semilla fija, en 4 capas de color.
  - Salsa roja con brillo, 3 albóndigas, hojas de albahaca, parmesano y vapor animado.
  - El plato entra girando al cargar.
- Sello rojo giratorio con texto circular "Hecho al momento · Salsas de la casa" y "SP" al centro.
- Tarjeta flotante: "Pastas al horno desde Bs 57 – Lasagna gratinada".
- Borde inferior en onda.

### Cinta
Banda negra con bordes amarillos y un marquee con: "Pasta al dente", "Salsas de la casa", "Porciones generosas", "Directo de la olla", "Hecho en Cochabamba". Se pausa al pasar el mouse.

### Menú (fondo crema)
- Título "El menú de la casa".
- Texto: "Los principales vienen con pasta larga a elección…".
- Chips "Tu pasta": Spaghetti, Fettuccine, Tallarín, Sin gluten.
- **Pestañas por categoría**:
  - `role="tablist"`, se recorren con flechas, Home y End.
  - Cada una con su ícono SVG y un contador de platos.
  - La pestaña activa va en rojo.
  - Abre por defecto en "Principales".
- Layout de 2 columnas:
  - Izquierda: panel *sticky* con la foto de la categoría, con fundido al cambiar de pestaña y una etiqueta con el nombre de la categoría. Las categorías sin foto muestran un panel amarillo con el logo y una frase.
  - Derecha: grilla de **tarjetas** en 2 columnas. Cada tarjeta tiene:
    - nombre, descripción y precio "Bs XX" ("Consultar" si no tiene precio);
    - una etiqueta opcional (Vegetariana, Sin gluten, Picante, De la casa, Vino, Postre…);
    - un link "Pedir →".
  - Las tarjetas tienen una barra lateral de color que crece al pasar el mouse, entran escalonadas y suben 4px con el hover.
- Responsive: 1 columna con la foto arriba en menos de 1080px, tarjetas en 1 columna en menos de 640px.
- Nota final: precios en Bs, sujetos a cambio. Se puede pedir por WhatsApp o en Mercat.

**Datos del menú** (todos los precios en Bs):

**Pastas**
- Pasta larga (spaghetti, tallarín, fettuccine): 52
- Pasta verde (ravioles, fettuccine, tallarín): 52
- Pasta corta (gnocchi, ravioles): 62
- Pasta sin gluten (spaghetti, fussili): 67

**Principales** (todos con pasta larga a elección)
- Medallones de lomo: 87
- Filete de pollo crema de champiñones: 72
- Albóndigas (6 unidades): 72
- Langostinos salsa blanca: 87
- Langostinos salsa roja: 87
- Filete de pollo pomodoro: 67
- Filete de pollo tres quesos: 72
- Filete de pollo roquefort: 72
- Filete de pollo tres champiñones: 72
- Filete de res tres quesos: 72
- Filete de res roquefort: 72
- Filete de res tres champiñones: 72
- Pasta a la puttanesca: 67

**Al horno**
- Lasagna: 57
- Lasagna vegetariana: 67
- Lasagna con langostinos: 87
- Canelón al gratín: 67
- Canelón verde al gratín: 67
- Raviol al gratín: 67
- Raviol verde al gratín: 67
- Spaguetti al gratín: 57
- Gnocchi al gratín: 67

**Aperitivos**
- Bruschetta jamón y queso: 12
- Bruschetta queso y hongos: 17
- Bruschetta queso y choclo: 12
- Bruschetta tomate y orégano: 9
- Bruschetta a la pizza: 18
- Pan con ajo: 7
- Panzerotti tradicional: 12
- Panzerotti fungi: 15
- Panzerotti picante: 12
- Panzerotti langostinos: 30
- Combo panzerotti: 50
- Dip de pan con ajo: 30

**Postres y extras**
- Tiramisú: 20
- Cheesecake de temporada: 20
- Postre del día: 20
- Gelato (paleta): 10
- Salsa extra: 30
- Queso parmesano: 15
- Champiñones fritos: 20
- Langostinos extra: 40

**Bebidas y vinos**
- Jugos del Sol: 20
- Jugo del Sol personal: 12
- Agua: 12
- Gaseosas: Consultar
- Vino reserva 375 ml: 80
- Vino botella clásicos: Consultar
- Sweet: 135
- Cabernet Sauvignon: 145
- Tannat Campos de Solana: 145
- Trivarietal Campos de Solana: 200

### Cómo pedir (fondo rojo)
- Fondo #C8101A con patrón de mantel a cuadros sutil.
- Título "Cómo pedir en 3 pasos". Texto: "Sin apps ni registros…".
- 3 tarjetas, cada una con un número grande en amarillo (01, 02, 03) y un ícono en un cuadro blanco:
  1. **Elige tu plato**
  2. **Escríbenos**: por WhatsApp o en la tienda de Mercat.
  3. **Recógelo o recíbelo**
- Línea punteada amarilla que une los pasos (solo en escritorio).
- Botones: "Pedir por WhatsApp" (amarillo) y "Pedir en Mercat" (contorno blanco).

### Visítanos (fondo crema)
- Título "Visítanos frente al Parque Lincoln".
- Izquierda:
  - La foto del local, con zoom suave al pasar el mouse. Si la imagen no carga, se muestra un cartel a rayas con el nombre.
  - Debajo, un mapa de Google embebido con "Manchay Puito 1995, Cochabamba".
- Derecha, en una tarjeta blanca:
  - Dirección: **Manchay Puito 1995, Parque Lincoln, Cochabamba**.
  - Horario: "Todos los días · 11:30 – 22:00", con la nota "horario referencial, confírmalo por WhatsApp".
  - Chips de servicios: Comer en el local, Para llevar, Mesas afuera, Pedidos en línea.
  - Otras sucursales: Av. Humboldt 932 (11:30–22:00), Pasos Kanki 2160 casi esq. Ciclovía, Paseo de Comidas Aranjuez.
  - Botones: "Cómo llegar" (Google Maps) y "Pedir para llevar".

### Banda tipográfica
Fondo amarillo con "Solo Pastas." gigante (el punto en rojo) y el texto "Oeste · Lincoln · Cochabamba".

### Footer (fondo tinta)
- Franja de la bandera arriba.
- 4 columnas:
  - Logo y una frase corta, con los íconos de redes:
    - Facebook: https://www.facebook.com/share/1MVmiLkqtA/
    - Instagram: https://www.instagram.com/solopastascochabamba
    - TikTok: https://www.tiktok.com/@solopastas_cbba_bolivia
  - Navega
  - Pedidos: WhatsApp, Tienda en Mercat (https://www.mercat.bo/solo-pastas), Para llevar.
  - Sucursales.
- Línea final con "© {año automático} Solo Pastas · Oeste-Lincoln".

## Funcionalidad extra
- Objeto `CONFIG` al inicio del script con `whatsapp: '59176911505'` y un saludo.
- Todos los botones `.js-order` abren `wa.me` con el mensaje ya escrito. El botón "Pedir" de cada plato agrega "1 x {nombre del plato}".
- Si el número está vacío, los botones llevan a la sección "Cómo pedir".
- Barra fija inferior en el celular con "Ver menú" y "Pedir ahora". Se oculta en el hero y al final de la página.
- Accesibilidad:
  - Link "Saltar al contenido" y foco visible en rojo.
  - `alt` en las imágenes, `aria-label` en los íconos.
  - Botones y links de al menos 44px de alto.
  - Contraste AA.
- SEO: title, meta description, Open Graph, theme-color amarillo y el logo como favicon.
- Totalmente responsive: 1440, 1024, 768, 390 y 320px, sin scroll horizontal.
