# jaenstyles

Repositorio de estilos y scripts personalizados para el proyecto **Diputación Provincial de Jaén**. Cada carpeta representa una landing y cada archivo `.html` dentro contiene los estilos/scripts de una sección concreta de esa landing.

## Estructura

```
jaenstyles/
├── theme.css               # Estilos globales compartidos configurador en theme settings
├── comoponentstyles.html   # Boilerplate base para nuevos bloques de sección
└── nombrelanding/
    └── nombrebloque.html   # Estilos de sección
└── nombrecontenido/
    └── contenido.html     # Estilos de ficha de contenido
```

**Convención:**
- Una carpeta por landing (ej: `home/`, `destinos/`, `contacto/`)
- Un `.html` por sección dentro de esa landing (ej: `sliderhome.html`, `herocontacto.html`)

---

## Boilerplate

`comoponentstyles.html` es la plantilla de partida para cualquier bloque nuevo. Copiarlo y renombrarlo según la sección.

```html
<div id="edition-block">

<style>
  /* START IDS: */
  /* Sustituir los siguientes IDs por clases o atributos de datos para evitar problemas de especificidad y mantener el CSS limpio y mantenible. */

  /* .page-node-XXXX - Nombre de la landing */
  /* id-del-bloque-generado - Nombre de la sección */

  /* STOP IDS: */

  :root {
  }

  /* START Section*/
  /* STOP SECTION */

</style>
</div>
```

El `<div id="edition-block">` sirve como contenedor identificador. En `theme.css` existe la regla:

```css
body:not(.user-logged-in) .block:has(#edition-block) {
  display: none;
}
```

Esto oculta el bloque a usuarios no autenticados, de forma que el HTML del bloque nunca sea visible en el front para visitantes normales.

---

## Sección de IDs

Entre `/* START IDS: */` y `/* STOP IDS: */` se listan los IDs que se usan como selectores CSS en ese archivo. Son IDs generados dinámicamente por el CMS (Drupal) y pueden cambiar si se regenera o reimporta un bloque.

**Cuando un ID cambia:**
1. Localizar el ID nuevo en el inspector del navegador o en la administración del CMS.
2. Actualizar el comentario en la sección de IDs.
3. Reemplazar todas las ocurrencias del ID antiguo en el CSS del archivo.

Ejemplo:

```css
/* START IDS: */
/* .page-node-1295 - Home */
/* segittur_static_portrait_ai_f41212c3-15e9-47b0-899c-6751b4dd81c4 - Home slider */
/* STOP IDS: */
```

---

## Variables globales `:root`

Cada archivo puede declarar variables CSS en `:root`. Las variables compartidas por todas las landings van en `theme.css`. Si una variable solo aplica a una sección concreta, declararla en el `:root` del propio archivo `.html`.

Variables globales actuales (definidas en `theme.css`):

```css
:root {
  --white: #fff;
  --black: #000;
}
```

---

## theme.css

Contiene los estilos base que afectan a todas las landings: header, comportamiento de scroll, primera sección, etc. No incluir aquí estilos específicos de una sección concreta; para eso usar el `.html` correspondiente dentro de la carpeta de la landing.

---

## Bloques con `contenido-x`

Cuando un archivo `.html` de bloque tiene como selector principal una clase del tipo `contenido-x` (por ejemplo `.contenido-destino`, `.contenido-noticia`), significa que el CSS de ese archivo corresponde a la **ficha** de ese tipo de contenido (la página de detalle), pero aplicado únicamente dentro de los bloques donde aparece ese contenido. Es decir, los estilos van acotados a ese contexto de bloque y no afectan al resto de la página.
