# Layout privado y menu lateral Bootstrap

## Objetivo

Crear el layout privado de Clubox para navegar por los modulos de la aplicacion.

El layout debe estar disponible solo cuando el usuario haya iniciado sesion.

## Estructura visual

```text
+---------------------------------------------------------+
| Header privado                                          |
+----------------------+----------------------------------+
| Menu lateral         | Area principal                   |
|                      |                                  |
| Inicio               | Vista activa                     |
| Formularios          |                                  |
| Gestion deportiva    |                                  |
| Contabilidad         |                                  |
| Cuotas y pagos       |                                  |
+----------------------+----------------------------------+
```

## Archivo principal

Crear o actualizar:

```text
assets/js/layout.js
```

## Responsabilidad de layout.js

- Pintar estructura privada.
- Pintar menu lateral.
- Pintar cabecera superior.
- Crear contenedor para la vista activa.
- Ejecutar la vista activa dentro del contenedor.
- Gestionar boton de cierre de sesion.

No debe contener logica de cada modulo.

## Funcion principal

```js
export function renderLayout(appRoot, viewRender) {
  appRoot.innerHTML = getLayoutHtml();

  const pageRoot = document.getElementById("pageRoot");
  viewRender(pageRoot);

  bindLogout();
}
```

## Contenedor de vista

El area donde se cargan los modulos debe llamarse:

```html
<main id="pageRoot" class="club-content flex-grow-1 p-4"></main>
```

## Menu lateral

Usar Bootstrap `accordion`.

No usar iconos.

Cada enlace debe usar `data-route`.

Ejemplo:

```html
<button class="club-menu-link" data-route="/app/dashboard">
  Dashboard
</button>
```

## Secciones del menu

### Inicio

```text
Dashboard -> /app/dashboard
```

### Formularios

```text
Formularios creados -> /app/formularios
Inscripciones recibidas -> /app/inscripciones
```

### Gestion deportiva

```text
Jugadores -> /app/jugadores
Equipos -> /app/equipos
Cuerpo tecnico -> /app/tecnicos
```

### Contabilidad

```text
Registro de movimientos -> /app/contabilidad
Resumen economico -> /app/resumen
```

### Cuotas y pagos

```text
Configuracion de cuotas -> /app/cuotas
Pagos -> /app/pagos
```

## Header privado

Debe incluir:

- Nombre Clubox.
- Texto corto: Panel de gestion.
- Boton Cerrar sesion.

Ejemplo:

```html
<header class="club-header d-flex justify-content-between align-items-center px-4 py-3">
  <div>
    <strong>Clubox</strong>
    <span class="text-muted ms-2">Panel de gestion</span>
  </div>
  <button id="logoutBtn" class="btn btn-outline-light btn-sm">Cerrar sesion</button>
</header>
```

## Cierre de sesion

El boton `logoutBtn` debe llamar a `logoutUser()` y navegar a `/login`.

```js
function bindLogout() {
  const logoutBtn = document.getElementById("logoutBtn");

  if (!logoutBtn) {
    return;
  }

  logoutBtn.addEventListener("click", () => {
    logoutUser();
    goRoute("/login");
  });
}
```

## CSS requerido

Crear estilos propios en:

```text
assets/css/styles.css
```

Variables base:

```css
:root {
  --colorPrimary: #6f1d2f;
  --colorSecond: #8f2d46;
  --colorDark: #111111;
  --colorLight: #ffffff;
  --colorSoft: #f7f3f4;
  --colorLine: #e6d8dc;
  --colorOk: #198754;
  --colorWarn: #ffc107;
  --colorFail: #dc3545;
}
```

Clases recomendadas:

```css
.club-app {
  min-height: 100vh;
  background: var(--colorSoft);
}

.club-header {
  background: var(--colorPrimary);
  color: var(--colorLight);
}

.club-sidebar {
  width: 280px;
  min-height: calc(100vh - 64px);
  background: var(--colorLight);
  border-right: 1px solid var(--colorLine);
}

.club-content {
  background: var(--colorSoft);
}

.club-menu-link {
  width: 100%;
  border: 0;
  background: transparent;
  text-align: left;
  padding: 8px 12px;
  color: var(--colorDark);
}

.club-menu-link:hover {
  background: var(--colorSoft);
  color: var(--colorPrimary);
}
```

## Responsive

En escritorio, el menu lateral debe verse fijo a la izquierda.

En movil, el menu puede quedar encima del contenido o convertirse en menu colapsable.

La primera version puede priorizar escritorio, porque la app esta pensada para directivos y administradores del club.

## Resultado esperado

Codex debe entregar un layout privado con:

- Header superior.
- Sidebar con desplegables.
- Navegacion por modulos.
- Area dinamica de contenido.
- Boton de cerrar sesion.
- Estilos con branding burdeo, blanco y negro.
