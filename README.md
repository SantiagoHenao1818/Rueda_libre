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

> **Pendiente de confirmar:** esta URL y el estado son los valores habituales
> de Live Server, pero deben confirmarse en DevTools > Network. Si Live Server
> muestra otra URL o puerto, reemplaza estos datos por los de la petición real
> después de recargar `index.html` y seleccionar la solicitud de tipo
> `document`.

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
la portada pasa a una columna y la navegación apila sus elementos; `flex-wrap`
permite que la portada se acomode si falta espacio.

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