# Bitácora de desarrollo — Rueda Libre

## Estado del sitio

El proyecto ya cuenta con `index.html`, páginas HTML, hojas de estilo y
recursos en `img/` (incluidos `img/Logo.svg` e imágenes de bicicletas). Se
conserva la ubicación actual de las páginas para no romper sus enlaces
relativos. Se creó `paginas/` como parte de la estructura solicitada; por
ahora, las páginas existentes siguen en la raíz.

## 1. Petición del documento en Live Server

La URL de referencia para Live Server con su configuración predeterminada es:
`http://127.0.0.1:5500/index.html`

- **Protocolo:** HTTP
- **Host:** `127.0.0.1` (localhost)
- **Puerto:** `5500`
- **Ruta:** `/index.html`
- **Método:** `GET`
- **Estado esperado:** `200 OK` (el servidor encontró y entregó `index.html`).


## 2. Ruta inexistente

Prueba sugerida: `http://127.0.0.1:5500/promociones.html`

- **Estado esperado:** `404 Not Found`.
- **Significado:** el servidor está disponible, pero no encontró el archivo o
  la ruta solicitada. Confirma el código en la respuesta de Network de Live
  Server.

## 3. Tecnologías del sitio

- **HTML:** estructura y contenido. Por ejemplo, `index.html` organiza la
  navegación, la portada, los servicios y los pasos para alquilar;
  `Reserva.html` contiene el formulario de solicitud.
- **CSS:** presentación y adaptación a diferentes tamaños de pantalla. Por
  ejemplo, `style.css` define la barra de navegación, los colores y las
  tarjetas; usa Flexbox para la navegación y la portada, y Grid para las
  tarjetas de servicios.
- **JavaScript:** comportamiento e interacción. Por ejemplo, los botones de
  navegación usan `onclick` para llevar a `tarifas.html` o `Reserva.html`. El
  archivo `js.js` existe, pero actualmente está vacío y no está conectado a
  las páginas; no se atribuyen al JavaScript funciones que aún no se han
  implementado.

## 4. Decisiones de diseño y responsive

Flexbox se eligió para alinear elementos en una dimensión: logo y enlaces de
la navegación, y texto e imagen de la portada. En pantallas de hasta `768 px`
la portada pasa a una columna y la navegación muestra un botón de hamburguesa
de tres líneas; al activarlo, despliega los enlaces debajo del logo. En
escritorio se mantienen visibles los enlaces. El control también se puede
activar con teclado.

Grid se eligió para colecciones en dos dimensiones, como tarjetas de servicios,
pasos e información. Las columnas con `repeat(auto-fit, minmax(...))` se
ajustan al ancho disponible. En el formulario de `Reserva.html`, la cuadrícula
de dos campos pasa a una columna en pantallas de hasta `768 px`. La tabla de
tarifas puede desplazarse horizontalmente dentro de `.table-responsive`.

Estas reglas atienden el desbordamiento de la navegación, la portada, las
tarjetas, el formulario y la tabla en pantallas estrechas. Se registran como
decisiones visibles en el código actual, no como una comparación con Bootstrap.

## 5. Bootstrap

Bootstrap todavía no está implementado. El sitio usa HTML y CSS propios; esta
bitácora queda como referencia para comparar más adelante su estructura y
comportamiento responsive con una versión hecha con Bootstrap.

## 6. Control de versiones

El repositorio ya tenía commits anteriores a esta bitácora. El commit que
registra esta entrega debe describir la incorporación de la bitácora y la
estructura solicitada; por lo tanto, no es el primer commit histórico del
repositorio.

## 7. Rutas de navegación, enlaces y botones

Las rutas de páginas que siguen son relativas a la raíz del proyecto, donde
actualmente están `index.html`, `tarifas.html`, `Reserva.html` y
`Catalogo.html`. Con Live Server en el puerto predeterminado `5500`, sus URL
completas son:

| Página | URL local |
|---|---|
| `index.html` | `http://127.0.0.1:5500/index.html` |
| `tarifas.html` | `http://127.0.0.1:5500/tarifas.html` |
| `Reserva.html` | `http://127.0.0.1:5500/Reserva.html` |
| `Catalogo.html` | `http://127.0.0.1:5500/Catalogo.html` |

### Barra de navegación

Presente en las cuatro páginas:

- **Inicio** → `index.html`
- **Tarifas** → `tarifas.html`
- **Reserva** → `Reserva.html`
- **Catalogo** → `Catalogo.html`, excepto en `Catalogo.html`, donde el enlace
  activo tiene `href=""` y vuelve a cargar la ruta actual.

### Botones de la barra superior

- En `index.html`, **Tarifas** → `tarifas.html`.
- En `Reserva.html` y `Catalogo.html`, **Inicio** → `index.html`.
- En `tarifas.html`, **Reserva** → `Reserva.html`.

### Contenido de cada página

- **`index.html`:** en el pie de página, los enlaces Inicio, Tarifas, Reservas
  y Catalogo llevan respectivamente a `index.html`, `tarifas.html`,
  `Reserva.html` y `Catalogo.html`. Los enlaces de navegación llevan a los
  mismos destinos.
- **`tarifas.html`:** los dos botones **Reserva** llevan a `Reserva.html`. El
  botón **Ubicación** está dentro de un enlace externo a Google Maps para la
  dirección Cl. 16 #55-129, Guayabal, Medellín; abre una pestaña nueva.
  [Abrir ubicación en Google Maps](https://www.google.com/maps?client=opera-gx&oe=UTF-8&um=1&ie=UTF-8&fb=1&gl=co&sa=X&geocode=Ke9OEQ4_KUSOMYHAx0TdDGGZ&daddr=Cl.+16+%2355-129,+Guayabal,+Medellín,+Guayabal,+Medellín,+Antioquia).
  El pie de página enlaza a las cuatro páginas.
- **`Reserva.html`:** el botón **Inicio** lleva a `index.html`. El formulario
  tiene `action="#"` y `method="POST"`: al pulsar **Enviar Solicitud**, el
  navegador intenta enviar los datos mediante POST a la ruta actual (el
  fragmento `#` identifica la misma página). No se ha configurado un endpoint
  de servidor que procese la reserva. El pie de página enlaza a las cuatro
  páginas.
- **`Catalogo.html`:** el botón superior **Inicio** lleva a `index.html`. Hay
  seis botones **Reservar** en las tarjetas de bicicletas, pero no tienen
  enlace ni acción `onclick`; actualmente no llevan a ninguna ruta. Para que
  funcionen habría que asignarles un destino, por ejemplo `Reserva.html`. El
  pie de página enlaza a las cuatro páginas.

En total, los enlaces del pie de página repiten la navegación entre las cuatro
páginas. Los botones sin `href`, sin `onclick` y fuera de un formulario no
tienen un destino de navegación configurado.

## 8. Pruebas de validación del formulario de reserva

Pruebas realizadas en `Reserva.html` en Live Server
(`http://127.0.0.1:5500/Reserva.html`), comprobando la validación HTML5 del
navegador para cada campo. Se probaron entradas inválidas de forma individual;
el navegador las marcó como inválidas y mostró su aviso de validación. No se
envió una reserva al servidor: el formulario no tiene un servicio configurado
para procesarla. Los mensajes del navegador pueden variar según el idioma y el
navegador.

| Campo | Dato de prueba | Resultado esperado | Resultado obtenido |
|---|---|---|---|
| Nombre completo (obligatorio) | Vacío | Rechazado por campo obligatorio | Inválido; el navegador indica que se debe completar |
| Nombre completo (mínimo 3 caracteres) | `Al` | Rechazado por tener menos de 3 caracteres | Inválido; el navegador indica que se requieren al menos 3 |
| Documento (patrón de 6 a 10 dígitos) | `12345` | Rechazado por tener menos de 6 dígitos | Inválido; no coincide con el formato requerido |
| Correo | `correo-invalido` | Rechazado por no tener formato de correo | Inválido; el navegador indica que falta `@` |
| Celular (patrón 3 + 9 dígitos) | `1234567890` | Rechazado porque no empieza por 3 | Inválido; no coincide con el formato requerido |
| Fecha del alquiler (mínimo 2026-11-01) | `2026-10-31` | Rechazada por ser anterior a la fecha mínima | Inválida; el navegador exige 2026-11-01 o posterior |
| Fecha del alquiler (máximo 2026-12-31) | `2027-01-01` | Rechazada por superar la fecha máxima | Inválida; el navegador exige 2026-12-31 o anterior |
| Cantidad de bicicletas (mínimo 1) | `0` | Rechazada por estar bajo el mínimo | Inválida; el navegador exige un valor mayor o igual a 1 |
| Cantidad de bicicletas (máximo 6) | `7` | Rechazada por superar el máximo | Inválida; el navegador exige un valor menor o igual a 6 |
| Tipo de bicicleta (obligatorio) | Sin seleccionar opción | Rechazado por campo obligatorio | Inválido; el navegador pide seleccionar una opción |
| Plan de alquiler (obligatorio) | Sin seleccionar opción | Rechazado por campo obligatorio | Inválido; el navegador pide seleccionar una opción |
| Aceptación de políticas (obligatoria) | Casilla desmarcada | Rechazada por campo obligatorio | Inválida; el navegador pide marcar la casilla |

Las pruebas confirman que el navegador bloquea los valores inválidos mediante
las restricciones declaradas en `Reserva.html` (`required`, `minlength`,
`pattern`, `type="email"`, `min` y `max`). No se incluyó comentarios en esta
tabla: no se confirmó de forma fiable en esta sesión cómo se comporta
`maxlength` al escribir desde un teclado físico.

## 9. Mapa de uso de color y contraste

Clasificación calculada con la relación de contraste WCAG: texto normal
requiere al menos `4.5:1`; texto grande (desde `24 px` regular o
aproximadamente `19 px` en negrita) requiere al menos `3:1`. **No apta**
significa que no alcanza ninguno de esos dos umbrales. Para degradados se toma
el peor extremo, donde el contraste es menor.

| Combinación de texto y fondo | Contraste aprox. | Clasificación |
|---|---:|---|
| AliceBlue (#F0F8FF) sobre fondo oscuro (#0A0A0A) | 18.46:1 | Apta para texto normal |
| Gris claro (#CCCCCC) sobre fondo oscuro (#0A0A0A) | 12.33:1 | Apta para texto normal |
| Naranja (#FF9966) sobre fondo oscuro (#0A0A0A) | 9.43:1 | Apta para texto normal |
| Gris medio (#777777) sobre fondo oscuro (#0A0A0A) | 4.42:1 | Apta solo para texto grande |
| Blanco (#FFFFFF) sobre el degradado rojo-naranja de botones | 2.10:1 | No apta |
| AliceBlue (#F0F8FF) sobre el degradado rojo-naranja | 1.96:1 | No apta |
| Gris muy claro (#E2E8F0) sobre el naranja (#FF9966) | 1.70:1 | No apta |
| Naranja (#FF9966) sobre blanco (#FFFFFF) | 2.10:1 | No apta |
| Verde (#2ECC71) sobre fondo oscuro (#0A0A0A) | 9.42:1 | Apta para texto normal |
| Amarillo (#F1C40F) sobre fondo oscuro (#0A0A0A) | 11.92:1 | Apta para texto normal |
| Rojo (#E74C3C) sobre fondo oscuro (#0A0A0A) | 5.18:1 | Apta para texto normal |

### Mapa de uso de color propuesto

- **Texto principal:** AliceBlue (`#F0F8FF`) sobre fondos oscuros (`#0A0A0A` o
  `#121212`). Contraste alto y lectura apta para texto normal.
- **Texto secundario:** gris claro (`#CCCCCC`) sobre fondos oscuros. Evitar el
  gris `#777777` para texto pequeño; su contraste calculado es `4.42:1` y no
  alcanza el mínimo de `4.5:1` para texto normal.
- **Fondos:** negro suave (`#0A0A0A`) o `#121212` para el fondo general y las
  tarjetas. Los paneles translúcidos conservan el esquema oscuro.
- **Botones:** se puede conservar el degradado de marca (`#FF5E62` a
  `#FF9966`), pero usar texto oscuro (`#0A0A0A`), que alcanza al menos
  `6.63:1` frente al extremo rojo y `9.43:1` frente al naranja. El texto
  blanco actual sobre ese degradado no es apto ni siquiera para texto grande.
- **Enlaces:** AliceBlue (`#F0F8FF`) sobre el fondo oscuro para enlaces normales;
  destacar el estado hover con naranja solo si se mantiene un fondo oscuro. No
  usar texto naranja sobre fondo blanco o naranja claro.
- **Colores de estado:** verde, amarillo y rojo se reservan para avisos sobre
  el fondo oscuro; las tres combinaciones indicadas son aptas para texto
  normal.

Esta clasificación evalúa los colores de texto y fondo de la paleta actual;
las transparencias y superposiciones pueden alterar el contraste final según
el fondo que haya detrás. El mapa es una guía de uso y no implica que los
colores problemáticos existentes en todos los componentes ya hayan sido
corregidos en las hojas CSS.

## 10. DevTools: herencia, especificidad, estados y box model

### Herencia de propiedades

En DevTools, inspeccioné un párrafo dentro de una tarjeta `.paso-card` y
comparé los valores de **Computed** con los del `body`:

| Propiedad | Valor en `body` | Valor en el párrafo | Comprobación |
|---|---|---|---|
| `font-family` | `Arial, Helvetica, sans-serif` | `Arial, Helvetica, sans-serif` | Se hereda |
| `padding-top` | `100px` | `0px` | No se hereda; el reset universal `* { padding: 0; }` lo establece en cero |

### Clase que no aplicaba y cálculo de especificidad

En DevTools > Styles y Computed de `tarifas.html`, el elemento tenía las clases
`badge facil`, pero el estilo verde no aparecía: la regla escrita era
`.cover .badge.facil`, que requiere un ancestro con clase `cover`; ese ancestro
no existe en el HTML.

- `.cover .badge.facil`: especificidad `0-3-0` (tres selectores de clase).
- `.badge`: especificidad `0-1-0` (un selector de clase).
- La regla de mayor especificidad no se aplicaba porque no coincidía con la
  estructura HTML; la especificidad solo se compara entre reglas que sí
  coinciden. Corregí el selector a `.badge.facil` (`0-2-0`), que sí coincide y
  aplica el fondo, texto y borde de la etiqueta Fácil.

También comprobé un conflicto real al pasar el cursor sobre un enlace activo
del menú:

- `.nav-links li a:hover`: `0-2-2` (dos clases/pseudoclases y dos elementos).
- `nav.Navbar .active`: `0-2-1` (dos clases y un elemento).
- Ambas reglas coinciden con el enlace activo al pasar el cursor. La regla
  `:hover` tiene mayor especificidad por tener dos selectores de elemento,
  por lo que su color prevalece sobre la regla `.active`, aunque esta aparezca
  después.
- Añadí `.nav-links a.active:hover` (`0-3-1`), que prevalece sobre ambas para
  conservar el texto oscuro legible del enlace activo sobre su degradado.
  También eliminé una declaración `color` duplicada en la regla hover.

### Estados hover y focus

Añadí señales visuales para los controles interactivos:

- Los enlaces del menú resaltan con fondo y color al pasar el cursor; los
  enlaces del pie de página cambian a naranja y muestran subrayado en `:hover`.
- Los botones conservan el cambio de sombra y tamaño en `:hover`.
- Campos de texto, listas y áreas de texto resaltan el borde al pasar el
  cursor; al enfocarlos también cambian el borde y la sombra.
- Enlaces, botones, campos, listas, áreas de texto y casilla muestran un
  contorno claro de `3px` con separación de `3px` en `:focus-visible`.

Verifiqué el enlace activo del menú en hover, y recorrí con Tab enlaces,
botones y campos del formulario: los elementos enfocados mostraron el
contorno visible.

### Medición de box-sizing

Medí una tarjeta `.paso-card` en DevTools en el viewport de `1273px`. Para
comparar de forma controlada, fijé el ancho CSS a `275px` y cambié solo
`box-sizing`:

| `box-sizing` | Ancho total observado |
|---|---:|
| `border-box` | `275px` |
| `content-box` | `327px` |

Con `content-box`, se sumaron `50px` de padding horizontal (`25px` por lado) y
`2px` de borde al ancho de contenido. En el CSS del sitio ya existe
`box-sizing: border-box` en el reset universal, por lo que `border-box` es el
valor habitual de la tarjeta; el ancho se fijó temporalmente solo para hacer
una comparación equivalente.

## 11. Decisiones entre Flexbox y Grid

Las decisiones se basan en las dimensiones del contenido que se organiza:
Flexbox resuelve principalmente una dirección (fila o columna); Grid controla
filas y columnas como una cuadrícula. En el formulario completo, las secciones
se apilan con el flujo normal del documento, sin aplicar Flexbox ni Grid al
contenedor exterior.

| Caso | Técnica usada | Criterio de una o dos dimensiones |
|---|---|---|
| Portada (`.hero`) | Flexbox | Alinea en una fila el texto y la imagen; en móvil cambia a una columna, conservando una sola dirección de organización a la vez. |
| Galería de servicios/flota (`.servicios-grid`, `.pasos-grid`) | Grid | Distribuye varias tarjetas en filas y columnas; `auto-fit` y `minmax()` ajustan las columnas disponibles. |
| Reservas (contenedor exterior del formulario) | Flujo normal, sin Flexbox/Grid | Las secciones personales, alquiler y observaciones aparecen una debajo de otra; es una dimensión y el HTML ya proporciona ese orden. |
| Fila del formulario (`.form-grid-2`) | Grid | Presenta dos campos lado a lado y controla la distribución por filas y columnas; bajo `768px` pasa a una sola columna. |
| Encabezado (`.Navbar`) | Flexbox | Alinea logo, navegación y botón en una dirección; bajo `768px` los apila verticalmente. |
| Pie (`.Footer`) | Flexbox | Coloca en una fila los enlaces y el horario; organiza un eje, no una matriz de tarjetas. En móvil permanece en fila y puede quedar apretado. |

### Columnas observadas en la flota

Revisé `Catalogo.html` en el navegador con el viewport emulado a `1280px`,
`900px` y `500px`. El CSS tiene un breakpoint principal en `768px`; los tres
anchos son tamaños de prueba, no tres breakpoints.

| Ancho del viewport | Columnas calculadas en `.pasos-grid` | Qué se ve en la flota |
|---:|---:|---|
| `1280px` | 4 | Las cuatro tarjetas principales caben en una fila; las dos últimas bicicletas están en una subcuadrícula de 2 columnas. No se detectó desbordamiento horizontal del documento. |
| `900px` | 4 | Se mantienen cuatro columnas; la cuarta tarjeta sobresale aproximadamente `2px` del viewport. La subcuadrícula inferior conserva 2 columnas. |
| `500px` | 4 | El Grid sigue creando cuatro columnas, pero solo caben completas las dos primeras tarjetas; la tercera queda cortada y la cuarta queda fuera de pantalla. El documento llega a `776px` de ancho desplazable. La subcuadrícula de las dos bicicletas finales también se extiende fuera del viewport. |

Por tanto, el sitio no tiene tres breakpoints: tiene reglas móviles que se
activan en `768px` y las columnas de la flota cambian automáticamente según el
espacio. La observación de `500px` muestra un problema real; no afirmo que allí
no haya scroll horizontal.

### Comportamiento del encabezado y del pie al estrechar la ventana

- Entre `1280px` y `900px`, el encabezado permanece en una fila y mide
  aproximadamente `66px` de alto. A `500px`, se activa la regla de hasta
  `768px`: logo, enlaces y botón se apilan y el encabezado llega a unos
  `315px` de alto.
- El pie mantiene su distribución Flexbox en fila a los tres anchos. A `500px`
  sus dos grupos (enlaces y horario) quedan uno al lado del otro con poco
  espacio y aumenta su altura por el ajuste del contenido. No cambia a columna.
- En el sitio estrecho, el espacio superior de `180px` declarado para el
  contenido es menor que los aproximadamente `315px` del encabezado fijo; en
  algunas páginas el encabezado puede superponerse al comienzo del contenido.
  Queda registrado como pendiente responsive.

## 12. Problemas responsive y soluciones

### Ajustes que ya existen

1. **Portada demasiado ancha en móvil:** `.hero` permite `flex-wrap` y, hasta
   `768px`, cambia a columna para que texto e imagen no compitan por una fila
   estrecha.
2. **Menú superior apretado:** hasta `768px`, `.Navbar` y `.nav-links` apilan
   sus elementos. El contenido recibe `180px` de espacio superior para
   separarlo del encabezado fijo; en `500px` ese espacio aún puede ser menor
   que la altura real del menú, así que no resuelve por completo la
   superposición.
3. **Campos de reserva demasiado estrechos:** `.form-grid-2` cambia de dos
   columnas a una a `768px` o menos.
4. **Tabla de tarifas ancha:** `.table-responsive` contiene el ancho adicional
   mediante desplazamiento horizontal dentro de la tabla, en vez de ampliar
   toda la página.

### Pendientes observados

- **Flota a `500px`:** `.move-ulti` ocupa cuatro columnas del Grid exterior
  (`grid-column: span 4`) aunque el viewport sea angosto. Resultado observado:
  cuatro columnas calculadas y ancho desplazable de `776px`. Está pendiente
  ajustar el layout; no se modificó el CSS para respetar el alcance de esta
  entrega.
- **Encabezado fijo a `500px`:** sus `315px` de alto superan el espacio superior
  declarado de `180px`; puede cubrir parte del contenido. Requiere revisar ese
  espacio en una futura mejora responsive.
- **Pie a `500px`:** los dos grupos de `.Footer` siguen en una fila y quedan
  ajustados; una futura revisión podría apilarlos en móvil.

Comprobé que los cuatro enlaces del menú siguen presentes, que se muestran las
seis bicicletas con sus seis botones y que el formulario conserva sus campos
obligatorios y rangos de fecha/cantidad. No cambié archivos HTML ni CSS en esta
actualización; solo registré decisiones y resultados en la bitácora.

## 13. Cierre de los MiniRetos de la semana

### Lo construido

- **Estructura y primera petición:** sitio con página de inicio, páginas
  internas y recursos gráficos; documentación de URL local, método HTTP y
  respuesta esperada, pendiente de confirmar esos datos en Network para la
  sesión de Live Server utilizada.
- **Diseño y responsive:** navegación, portada y distribución de componentes
  con Flexbox; tarjetas y formularios con Grid; ajustes para pantallas
  estrechas.
- **Menú hamburguesa:** en pantallas de hasta `768 px` aparecen tres líneas
  junto al logo y, al activar el ícono, se despliegan los enlaces debajo. En
  escritorio se mantienen visibles los enlaces habituales; el control también
  se puede activar con teclado. Está implementado en las cuatro páginas.
- **Navegación y reserva:** enlaces entre inicio, tarifas, reserva y catálogo;
  formulario con restricciones nativas y tabla de pruebas de validación.
- **Estilos y accesibilidad:** mapa de colores y contraste, revisión de
  herencia y especificidad, arreglo del estilo de las etiquetas de nivel, y
  estados hover y focus visibles.
- **Comparación pendiente:** Bootstrap todavía no está implementado; el sitio
  actual sirve como referencia para una comparación posterior.

### Qué mejoraría

Conectaría el formulario a un servicio real y dirigiría cada botón **Reservar**
del catálogo a la página de reserva. También revisaría las etiquetas `alt`, el
idioma declarado en todas las páginas y los contrastes insuficientes del
degradado de los botones; probaría el sitio en más tamaños de pantalla y con
teclado/lector de pantalla. Finalmente, implementaría Bootstrap en una versión
de comparación sin perder esta referencia del diseño actual.


## 14. Migración del sitio a Bootstrap 5.3.8

### 14.1. Proceso de migración

Se realizó una adaptación del sitio web Rueda y Pedal utilizando Bootstrap 5.3.8 como framework de estilos. El objetivo fue reemplazar progresivamente la presentación basada en CSS propio por componentes y clases prediseñadas de Bootstrap, manteniendo la estructura general, el contenido y la identidad visual del proyecto.

El trabajo se desarrolló en una rama independiente llamada `bootstrap`, con el propósito de conservar la versión anterior en `main` y permitir trabajar en la nueva implementación sin modificar directamente la rama principal.

La migración se realizó sobre las cuatro páginas principales del proyecto:

- `index.html`: página de inicio.
- `tarifas.html`: información y tabla de tarifas.
- `Catalogo.html`: catálogo de bicicletas disponibles.
- `Reserva.html`: formulario para solicitar una reserva.

Se conservaron los nombres de los archivos y las rutas de las páginas para evitar modificar innecesariamente los enlaces internos del proyecto.

### 14.2. Incorporación de Bootstrap mediante CDN

Se incorporó Bootstrap 5.3.8 mediante su CDN, agregando la hoja de estilos dentro del elemento `<head>` de las páginas:

```html
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet">
```

También se agregó el paquete JavaScript Bundle antes del cierre de `</body>`:

```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/js/bootstrap.bundle.min.js"></script>
```

La hoja de estilos permite utilizar las clases de diseño y los componentes de Bootstrap. El paquete JavaScript habilita las interacciones de componentes como el menú desplegable de navegación y el carrusel de imágenes.

En las páginas migradas se utilizan las clases de Bootstrap para organizar la presentación, sin depender de las hojas CSS personalizadas anteriores. Los archivos originales se conservan en el repositorio como parte de la versión anterior del proyecto.

### 14.3. Adaptación de la barra de navegación

Se unificó la estructura de la barra de navegación en las cuatro páginas para mantener una presentación consistente.

Se utilizaron las siguientes clases:

- `navbar`: establece el componente de navegación.
- `navbar-expand-lg`: permite que el menú se expanda en pantallas grandes y se contraiga en pantallas pequeñas.
- `navbar-dark`: adapta los colores de los elementos para fondos oscuros.
- `bg-dark`: establece un fondo oscuro.
- `fixed-top`: mantiene la barra fija en la parte superior.
- `container`: organiza y centra el contenido.
- `navbar-brand`: identifica el nombre y el logotipo del sitio.
- `navbar-toggler`: crea el botón que permite desplegar el menú.
- `collapse navbar-collapse`: controla la expansión y contracción de los enlaces.
- `navbar-nav`: organiza los enlaces de navegación.
- `ms-auto`: desplaza los enlaces hacia el extremo derecho.
- `nav-link`: define la apariencia de los enlaces.

Se conservaron los destinos de navegación entre Inicio, Tarifas, Reserva y Catálogo. La clase `active` identifica la página que se está visitando.

### 14.4. Organización del contenido mediante Grid

Se utilizó el sistema de cuadrícula de Bootstrap para distribuir los elementos de las páginas.

Entre las clases empleadas se encuentran:

- `container`: establece un contenedor con ancho adaptable.
- `row`: crea una fila para organizar las columnas.
- `col-md-6`: ocupa la mitad del espacio disponible desde el breakpoint mediano.
- `col-lg-3`: ocupa una cuarta parte del espacio disponible desde el breakpoint grande.
- `g-4`: establece separación entre las columnas y filas.
- `mx-auto`: centra horizontalmente un elemento mediante márgenes automáticos.

Este sistema permite organizar los contenidos en columnas y modificar su distribución según el ancho de la pantalla.

### 14.5. Adaptación de las tarjetas del catálogo

En `Catalogo.html` se utilizaron tarjetas de Bootstrap para presentar las bicicletas disponibles.

Se emplearon clases como:

- `card`: define la estructura de cada tarjeta.
- `card-body`: organiza el contenido interior.
- `card-title`: identifica el título de la tarjeta.
- `card-text`: presenta la descripción.
- `img-fluid`: permite que las imágenes se adapten al ancho de su contenedor.
- `btn`: establece la estructura básica de un botón.
- `btn-warning`: aplica el estilo de color de Bootstrap.

Se conservaron las seis bicicletas del catálogo, sus imágenes, nombres, descripciones y precios:

1. Urbana Clásica.
2. Urbana Plegable.
3. Montaña Trail.
4. Gravel Aventura.
5. Eléctrica Urbana.
6. Infantil.

### 14.6. Adaptación de la tabla de tarifas

En `tarifas.html` se utilizaron las clases de tablas de Bootstrap para organizar la información de los precios.

Entre las clases disponibles se encuentran:

- `table`: aplica el formato base de una tabla.
- `table-dark`: adapta la tabla a una presentación oscura.
- `table-striped`: alterna el fondo de las filas.
- `table-hover`: permite destacar visualmente una fila al pasar el cursor.
- `table-responsive`: permite desplazar horizontalmente la tabla cuando su contenido no cabe en pantallas pequeñas.

La información de las tarifas se conserva dentro de la estructura de la tabla, sin necesidad de construir manualmente toda su presentación mediante reglas CSS.

### 14.7. Adaptación del formulario de reserva

En `Reserva.html` se reorganizaron los campos del formulario utilizando las clases de formularios de Bootstrap.

Se utilizaron:

- `form-label`: presenta las etiquetas de los campos.
- `form-control`: establece el estilo de los campos de texto, fecha, número y área de texto.
- `form-select`: aplica el estilo de Bootstrap a las listas desplegables.
- `form-check`: organiza la casilla de aceptación de políticas.
- `btn btn-warning`: aplica el estilo del botón de envío.
- `w-100`: permite que el botón ocupe todo el ancho disponible.

El formulario conserva sus secciones principales:

1. Datos personales.
2. Detalles del alquiler.
3. Observaciones.
4. Aceptación de las políticas de alquiler.

También se mantienen las restricciones HTML5 de los campos, como `required`, `minlength`, `pattern`, `min`, `max` y `type="email"`.

La incorporación de Bootstrap modifica la presentación del formulario, pero no crea por sí misma un sistema para almacenar o procesar las reservas. El formulario continúa necesitando un servicio de servidor para recibir y gestionar las solicitudes.

### 14.8. Incorporación del carrusel de imágenes

Se incorporó el componente Carousel de Bootstrap para mostrar varias imágenes dentro de una misma sección del sitio.

Su estructura utiliza los siguientes elementos:

- `carousel slide`: establece el componente y su transición.
- `carousel-inner`: contiene las diapositivas.
- `carousel-item`: representa cada imagen.
- `active`: identifica la primera diapositiva que se muestra.
- `carousel-control-prev`: permite regresar a la imagen anterior.
- `carousel-control-next`: permite avanzar a la siguiente imagen.
- `carousel-indicators`: permite identificar y seleccionar las diapositivas.

También se utilizaron clases como `rounded-4` para redondear las esquinas de la sección y `img-fluid` para adaptar las imágenes al espacio disponible.

Para modificar el tamaño de las imágenes se pueden utilizar las utilidades de ancho de Bootstrap, como `w-25`, `w-50`, `w-75` y `w-100`. Estas clases representan porcentajes del ancho del contenedor. Clases como `w-45` y `w-70` no pertenecen a las utilidades estándar de Bootstrap 5.3.8.

En este proyecto se utilizó específicamente la clase `w-25` para reducir el ancho de las imágenes del carrusel al 25% del contenedor. Se complementó con `mx-auto` para centrarlas horizontalmente.

### 14.9. Colores, espaciado y alineación

Se utilizaron diferentes clases de utilidad para establecer la apariencia general del sitio sin depender de reglas CSS individuales para cada elemento.

Algunas de las clases empleadas son:

| Clase | Función |
|---|---|
| `bg-black` | Establece un fondo negro. |
| `bg-dark` | Establece un fondo oscuro. |
| `text-light` | Aplica un color claro al texto. |
| `text-white` | Aplica el color blanco al texto. |
| `text-warning` | Aplica el color de advertencia de Bootstrap al texto. |
| `btn-warning` | Establece el estilo de advertencia en los botones. |
| `mt-5` | Agrega margen superior. |
| `mb-4` | Agrega margen inferior. |
| `p-4` | Agrega espacio interno. |
| `mx-auto` | Centra horizontalmente mediante márgenes automáticos. |
| `rounded-4` | Aplica bordes redondeados. |
| `shadow` | Agrega una sombra al elemento. |

Estas utilidades permiten modificar aspectos visuales directamente desde las clases de los elementos HTML.

### 14.10. Diseño responsive con Bootstrap

La adaptación a diferentes tamaños de pantalla se realizó utilizando el sistema responsive de Bootstrap.

Sus breakpoints permiten establecer diferentes distribuciones según el ancho del dispositivo. Por ejemplo:

- `col-md-6`: organiza dos columnas a partir del breakpoint mediano.
- `col-lg-3`: organiza cuatro columnas a partir del breakpoint grande.
- `navbar-expand-lg`: mantiene el menú expandido en pantallas grandes y utiliza el menú desplegable en pantallas más pequeñas.
- `img-fluid`: evita que las imágenes superen el ancho disponible de su contenedor.
- `container`: adapta el ancho del contenido según el tamaño de pantalla.

De esta manera, la distribución de los elementos puede cambiar sin tener que escribir manualmente una media query para cada componente.

### 14.11. Diferencias frente a la versión anterior

La versión original del sitio utilizaba principalmente hojas CSS propias para controlar la navegación, las tarjetas, los formularios, los colores y la distribución responsive.

En la nueva versión se utilizan componentes y utilidades de Bootstrap para resolver esas mismas necesidades.

| Aspecto | Versión anterior | Versión con Bootstrap |
|---|---|---|
| Navegación | Estructura y estilos CSS propios. | Componente Navbar de Bootstrap. |
| Distribución | Flexbox y Grid mediante CSS propio. | Sistema Grid de Bootstrap. |
| Tarjetas | Clases y estilos personalizados. | Componente Card. |
| Formularios | Estilos propios para los campos. | Clases de formularios de Bootstrap. |
| Botones | Estilos personalizados. | Clases como `btn` y `btn-warning`. |
| Carrusel | No estaba incorporado en la estructura original documentada. | Componente Carousel de Bootstrap. |
| Responsive | Media queries y reglas propias. | Breakpoints y clases responsive de Bootstrap. |

La principal diferencia es que la nueva implementación aprovecha componentes y utilidades prediseñados, reduciendo la cantidad de estilos que deben escribirse manualmente.

### 14.12. Verificaciones pendientes

Después de la migración es importante comprobar el funcionamiento de todos los elementos en el navegador.

Las verificaciones incluyen:

- Revisar que las cuatro páginas carguen correctamente.
- Comprobar que los enlaces de la barra de navegación dirijan a sus páginas correspondientes.
- Verificar que el botón hamburguesa despliegue y oculte el menú.
- Comprobar que las imágenes del catálogo y del carrusel carguen correctamente.
- Probar los controles para avanzar y retroceder en el carrusel.
- Revisar que la tabla de tarifas pueda visualizarse en pantallas pequeñas.
- Comprobar las validaciones del formulario de reserva.
- Revisar la distribución del contenido en diferentes tamaños de pantalla.
- Comprobar que los botones de reserva del catálogo tengan los destinos correspondientes.

Estas comprobaciones deben realizarse en el navegador. La inclusión de las clases de Bootstrap no garantiza por sí sola que todos los enlaces, formularios y botones tengan una funcionalidad completa.

### 14.13. Control de versiones de la migración

La adaptación a Bootstrap se realizó en la rama `bootstrap`, manteniendo separada la rama `main`.

Esta decisión permite conservar la versión anterior y comparar los cambios realizados durante la migración.

Antes de integrar los cambios en `main`, se debe revisar el contenido de ambas ramas, comprobar que las páginas funcionen correctamente y confirmar que no se hayan eliminado recursos necesarios.

La fusión (*merge*) se realizará cuando la nueva versión esté revisada y lista para integrarse al proyecto principal.

### 15. Ampliaciones y mejoras en la versión con Bootstrap

#### 15.1. Validación visual de formularios con Bootstrap
Se integró el sistema de validación de formularios de Bootstrap combinándolo con las restricciones nativas de HTML5 (`required`, `minlength`, `pattern`, `min`, `max`, `type="email"`). 

* **Clases de estado:** Bootstrap aplica de forma dinámica clases como `.is-invalid` (para marcar campos con errores o datos que no cumplen el patrón) y `.is-valid` (para entradas correctas).
* **Feedback visual:** El navegador y los estilos del framework despliegan bordes de advertencia y mensajes claros que guían al usuario para corregir la información antes de intentar el envío.

#### 15.2. Centralización de colores mediante variables CSS (`:root`)
Para mantener la identidad visual del proyecto sin depender exclusivamente de la paleta por defecto de Bootstrap, se definió un bloque de variables globales (`:root`) en la hoja de estilos personalizada.

* **Ventaja:** Permite gestionar de manera centralizada los colores corporativos (fondos oscuros, textos principales y tonos de acento). Modificando el valor en `:root`, este se actualiza de forma automática en todos los componentes que lo utilicen, asegurando consistencia cromática en las cuatro páginas.

#### 15.3. Botón flotante de WhatsApp transversal
Se incorporó un botón flotante de acceso directo a WhatsApp en la esquina inferior derecha de todas las páginas del sitio (`index.html`, `tarifas.html`, `Catalogo.html` y `Reserva.html`).

* **Comportamiento:** Cuenta con posicionamiento fijo (`position: fixed`), lo que garantiza que permanezca visible y accesible para el usuario en todo momento mientras realiza desplazamiento vertical (*scroll*).
* **Funcionalidad:** Enlaza directamente a una URL de WhatsApp (`https://wa.me/573001234567?text=Hola,%20quiero%20más%20información%20sobre%20el%20alquiler%20de%20bicicletas.`) con un mensaje de consulta preconfigurado, agilizando el canal de comunicación directa para la reserva o resolución de dudas de los clientes.