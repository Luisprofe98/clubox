# Router y autenticacion mock

## Objetivo

Crear una capa de navegacion interna para Clubox sin usar frameworks.

La SPA debe usar JavaScript modular y rutas hash.

## Archivos necesarios

```text
assets/js/app.js
assets/js/router.js
assets/js/auth.js
assets/js/layout.js
assets/js/views/landingView.js
assets/js/views/loginView.js
assets/js/views/dashboardView.js
assets/js/views/formulariosView.js
assets/js/views/inscripcionesView.js
assets/js/views/jugadoresView.js
assets/js/views/equiposView.js
assets/js/views/tecnicosView.js
assets/js/views/contabilidadView.js
assets/js/views/resumenView.js
assets/js/views/cuotasView.js
assets/js/views/pagosView.js
```

## index.html

El HTML debe tener un unico punto de montaje:

```html
<div id="appRoot"></div>
```

Cargar Bootstrap desde CDN y cargar `app.js` como modulo.

```html
<script type="module" src="assets/js/app.js"></script>
```

## app.js

Responsabilidad:

- Arrancar la SPA.
- Inicializar el router.

Ejemplo base:

```js
import { initRouter } from "./router.js";

document.addEventListener("DOMContentLoaded", () => {
  initRouter();
});
```

## auth.js

Responsabilidad:

- Comprobar si hay sesion.
- Crear sesion mock.
- Cerrar sesion.

Usar nombres de variables de maximo dos palabras.

Ejemplo:

```js
const sessionKey = "clubSession";

export function isLogged() {
  return sessionStorage.getItem(sessionKey) === "active";
}

export function loginUser(emailData, passData) {
  const validEmail = emailData === "admin@clubox.local";
  const validPass = passData === "clubox123";

  if (!validEmail || !validPass) {
    return false;
  }

  sessionStorage.setItem(sessionKey, "active");
  return true;
}

export function logoutUser() {
  sessionStorage.removeItem(sessionKey);
}
```

## router.js

Responsabilidad:

- Leer la ruta actual.
- Proteger rutas privadas.
- Renderizar layout publico o privado.
- Cargar la vista correcta.

Rutas privadas:

```text
/app/dashboard
/app/formularios
/app/inscripciones
/app/jugadores
/app/equipos
/app/tecnicos
/app/contabilidad
/app/resumen
/app/cuotas
/app/pagos
```

Ejemplo de mapa de rutas:

```js
const routeMap = {
  "/": renderLanding,
  "/login": renderLogin,
  "/app/dashboard": renderDashboard,
  "/app/formularios": renderForms,
  "/app/inscripciones": renderInscriptions,
  "/app/jugadores": renderPlayers,
  "/app/equipos": renderTeams,
  "/app/tecnicos": renderStaff,
  "/app/contabilidad": renderAccounting,
  "/app/resumen": renderSummary,
  "/app/cuotas": renderFees,
  "/app/pagos": renderPayments
};
```

## Funcion goRoute

Crear una funcion unica para navegar.

```js
export function goRoute(routePath) {
  window.location.hash = routePath;
}
```

## Funcion getRoute

```js
function getRoute() {
  return window.location.hash.replace("#", "") || "/";
}
```

## Proteccion privada

```js
function isPrivate(routePath) {
  return routePath.startsWith("/app");
}
```

Si la ruta es privada y no hay sesion, enviar a login.

```js
if (isPrivate(routePath) && !isLogged()) {
  goRoute("/login");
  return;
}
```

## Renderizado

Las vistas publicas renderizan directamente sobre `appRoot`.

Las vistas privadas renderizan dentro del layout privado.

```js
if (isPrivate(routePath)) {
  renderLayout(appRoot, viewRender);
  return;
}

viewRender(appRoot);
```

## Clicks del menu

El router debe escuchar clicks sobre elementos con `data-route`.

```js
document.addEventListener("click", (eventData) => {
  const routeItem = eventData.target.closest("[data-route]");

  if (!routeItem) {
    return;
  }

  goRoute(routeItem.dataset.route);
});
```

## Reglas tecnicas

- No usar framework frontend.
- No usar iconos.
- No usar acentos en textos de interfaz.
- Mantener archivos separados.
- Cada vista debe exportar una funcion render.
- El router no debe contener HTML largo.
- El layout no debe contener logica de negocio.
- Las vistas no deben acceder directamente a `sessionStorage`, salvo login.

## Resultado esperado

Codex debe dejar funcionando:

- Rutas hash.
- Login mock.
- Cierre de sesion.
- Proteccion de rutas privadas.
- Carga de vistas publicas.
- Carga de vistas privadas dentro del layout de app.
