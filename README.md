# Pasaporte IA

Souvenir digital que reúne lo que los cursantes escribieron en sus pasaportes durante las tres estaciones sobre inteligencia artificial: **Videos**, **Apps** y **Batalla de prompts**.

Es una sola página HTML, sin dependencias de servidor, pensada para recorrer como un pasaporte: se ganan sellos al visitar cada estación y al final se obtiene una visa personal que se puede descargar como imagen.

- **Página publicada:** https://claude.ai/artifact/4GJ6eP96uYfNjvRL4yCFe3
- **Archivo fuente:** `index.html` (todo incluido: estructura, estilos, datos y lógica)

---

## Contenido

| Página | Qué muestra |
|---|---|
| **Tapa** | Ruleta de temas, sellos tocables y datos generales (estaciones, respuestas, temas). |
| **El viaje** | Las tres preguntas del pasaporte y los casilleros de sellos ganados. |
| **Videos / Apps / Batalla de prompts** | Las respuestas de cada estación en tres columnas, una por pregunta, con filtro para resaltar un tema. |
| **Temas** | Gráfico de barras con la cantidad de respuestas por tema y el detalle de las frases de cada uno. |
| **Visa** | Seis reglas de uso responsable derivadas de las respuestas, nombre del viajero/a, sellos y descarga en JPG. |

Las tres preguntas del pasaporte:

1. Algo que no sabía.
2. Algo que me preocupa o me genera una pregunta.
3. Algo que debería tener en cuenta la próxima vez que use IA.

---

## Origen y tratamiento de los datos

**Fuente:** documento *Síntesis de pasaportes* (.docx), con una tabla por estación y una columna por pregunta.

**Criterios aplicados:**

- **Correcciones mínimas de tipeo** que impedían entender la frase ("pl{asticos", "aia", "isa", "prom", "ns supere", "errore"). Se respetó la forma de expresarse de los chicos.
- **Se descartó** "que es ntt", porque no se entiende.
- **Se descartaron 11 respuestas sin relación con la IA**, todas de la estación Apps, sobre contaminación del mar, plásticos y especies marinas. Se conservaron las que hablan de errores de la IA al reconocer basura o animales.
- Celdas vacías y filas sin contenido fueron omitidas.

**Resultado:** 104 respuestas válidas.

**Pendiente de decisión:** hay respuestas sobre IA que no es generativa (Uber, la aspiradora que saca fotos, el valor de las apps). Por ahora se conservan.

---

## Temas

Cada respuesta se clasificó **a mano** en uno o más de estos 8 temas. Por eso la suma de las barras supera el total de respuestas.

| Clave | Tema |
|---|---|
| `pedir` | Pedirle bien |
| `falso` | Lo falso que parece real |
| `agua` | El agua que gasta |
| `como` | ¿Cómo lo hace? |
| `errores` | La IA se equivoca |
| `personas` | Quién la crea y la entrena |
| `cuidado` | Usarla con cuidado |
| `privacidad` | Privacidad |

La clasificación es una lectura del equipo y conviene validarla con quienes estuvieron en las estaciones.

---

## Reglas de la visa

Las seis reglas son conclusiones generales. Cada una se apoya en uno o más temas, y la página **calcula** de cuántas respuestas sale cada regla a partir de los datos.

| # | Regla | Temas |
|---|---|---|
| 1 | Pedile con claridad y detalle | `pedir` |
| 2 | Antes de creer o compartir, revisá | `falso` |
| 3 | No le creas todo | `errores` |
| 4 | Usala cuando la necesites | `agua` |
| 5 | Preguntate quién está detrás | `personas`, `como` |
| 6 | Usala para bien | `cuidado`, `privacidad` |

---

## Interacción

- **Ruleta:** se gira con el botón *GIRÁ* o arrastrándola. Al frenar muestra una frase al azar del tema que salió, con acceso al detalle de ese tema.
- **Sellos de la tapa:** cada toque muestra una frase al azar de esa estación.
- **Sellos del pasaporte:** se ganan al visitar cada estación y aparecen en *El viaje* y en la visa.
- **Visa en imagen:** genera un JPG de 1080 × 1350 px con el nombre, las reglas, los sellos y la banda tipo pasaporte. Se descarga con el botón *Descargar JPG*. Si la descarga no está disponible, la imagen se puede guardar manteniéndola apretada o con clic derecho.
- **Sonido:** se puede apagar con el botón *Sonido* de la tapa.
- **Navegación:** pestañas superiores, botones Anterior / Siguiente y enlaces directos por página (`#tapa`, `#viajero`, `#videos`, `#apps`, `#prompts`, `#temas`, `#visa`).

Los sellos ganados, el nombre y la preferencia de sonido se guardan solo en el navegador de cada dispositivo. No se envía ni se almacena ningún dato en un servidor.

---

## Cómo actualizar el contenido

Todo está dentro del bloque `<script>` de `index.html`:

- **`STATIONS`:** respuestas por estación. Cada fila es `[no sabía, me preocupa, tendré en cuenta]`. Cada celda es `S("texto", "tema1", "tema2")`, o `null` si está vacía.
- **`THEMES`:** nombres de los temas.
- **`SHORT`:** etiquetas cortas de los temas en la ruleta.
- **`RULES`:** reglas de la visa (título, descripción y temas que la sostienen).

Los conteos de la tapa, de las estaciones, del gráfico de temas y de las reglas se recalculan solos al cambiar los datos.

---

## Aspectos técnicos

- Un único archivo HTML con CSS y JavaScript embebidos, sin frameworks.
- **Tipografías** (Google Fonts): Bricolage Grotesque (títulos), Atkinson Hyperlegible (texto, elegida por su legibilidad), Caveat (frases de los chicos) y Courier Prime (banda de la visa).
- **Imagen de la visa:** se dibuja con Canvas 2D, sin librerías externas.
- **Descarga:** usa la capacidad `downloads` del entorno de publicación. Abierto como archivo local, se usa el método alternativo de guardar la imagen manualmente.
- **Colores de las estaciones:** azul, naranja y violeta, validados para que se distingan con distintos tipos de daltonismo. Además, cada estación se identifica siempre por su nombre, no solo por el color.
- **Accesibilidad:** foco visible con teclado, etiquetas en los controles y respeto de la preferencia de movimiento reducido (la ruleta da el resultado sin animación).
- **Diseño adaptable:** funciona en celular y en pantalla grande.
