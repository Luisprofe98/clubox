# Prompt de tarea para Codex

## Instruccion principal

Lee todos los archivos de `/docs/codex-context/` antes de modificar codigo.

Implementa la base navegable de Clubox como una Single Page Application con Bootstrap y JavaScript modular.

La primera entrega debe centrarse en:

- Landing publica.
- Login simulado.
- App privada.
- Menu lateral con desplegables.
- Router hash.
- Vistas placeholder de todos los modulos.

No implementes aun toda la logica interna de formularios, gestion deportiva, contabilidad o pagos. Primero deja lista la estructura navegable.

## Requisitos obligatorios

- Usar un unico `index.html`.
- Separar HTML, CSS y JS.
- Usar Bootstrap para estructura, formularios, botones, cards, tablas, alerts y menus.
- Usar JavaScript modular con `type="module"`.
- No usar frameworks frontend.
- No usar iconos.
- No usar acentos en textos de interfaz.
- Usar colores basados en el burdeo de Clubox, blanco y negro.
- Usar nombres de variables descriptivos.
- Cada nombre de variable debe tener maximo dos palabras.
- Usar camelCase.
- Preparar la arquitectura para conectar Google Cloud en una fase posterior.

## Rutas que deben funcionar

```text
#/                    Landing publica
#/login               Login
#/app/dashboard       Panel principal
#/app/formularios     Formularios creados
#/app/inscripciones   Inscripciones recibidas
#/app/jugadores       Jugadores
#/app/equipos         Equipos
#/app/tecnicos        Cuerpo tecnico
#/app/contabilidad    Registro de movimientos
#/app/resumen         Resumen economico
#/app/cuotas          Cuotas y pagos
#/app/pagos           Estado de pagos
```

## Archivos a crear

```text
index.html
assets/css/styles.css
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
assets/js/services/apiService.js
assets/js/services/storageService.js
assets/js/data/mockData.js
```

## Landing

La landing debe incluir:

- Hero de Clubox.
- Frase principal: Gestiona tu club deportivo desde un solo lugar.
- Texto breve sobre formularios, jugadores, equipos, cuotas y contabilidad.
- Boton principal: Acceder a Clubox.
- Boton secundario: Solicitar informacion.

El boton Acceder a Clubox debe navegar a `#/login`.

## Login

Crear formulario con:

- Email.
- Password.
- Boton Entrar.

Usar credenciales mock:

```text
admin@clubox.local
clubox123
```

Si el login es correcto, guardar sesion en `sessionStorage` y navegar a `#/app/dashboard`.

Si el login falla, mostrar alerta Bootstrap `alert-danger` con clase `failed`.

## App privada

Crear layout privado con:

- Header superior.
- Menu lateral izquierdo.
- Area principal `pageRoot`.
- Boton Cerrar sesion.

El menu lateral debe usar Bootstrap `accordion` o `collapse`.

## Menu lateral

Secciones:

```text
Inicio
  Dashboard

Formularios
  Formularios creados
  Inscripciones recibidas

Gestion deportiva
  Jugadores
  Equipos
  Cuerpo tecnico

Contabilidad
  Registro de movimientos
  Resumen economico

Cuotas y pagos
  Configuracion de cuotas
  Pagos
```

Cada opcion debe tener `data-route` y navegar con el router.

## Vistas placeholder

Cada vista debe renderizar:

- Titulo del modulo.
- Descripcion breve.
- Una card Bootstrap.
- Una tabla o bloque vacio preparado para datos.

Ejemplo:

```js
export function renderPlayers(pageRoot) {
  pageRoot.innerHTML = `
    <section class="container-fluid">
      <h1 class="h3 mb-3">Jugadores</h1>
      <div class="card">
        <div class="card-body">
          <p class="mb-0">Listado de jugadores del club.</p>
        </div>
      </div>
    </section>
  `;
}
```

## Estados visuales

Usar estas clases:

```text
succeed -> accion correcta
warning -> aviso
failed -> error
```

Aplicarlas junto a alerts de Bootstrap:

```html
<div class="alert alert-success succeed">Accion realizada</div>
<div class="alert alert-warning warning">Revisa los datos</div>
<div class="alert alert-danger failed">No se pudo completar</div>
```

## Entrega esperada

Al finalizar, la aplicacion debe permitir:

- Abrir la landing desde `#/`.
- Entrar al login desde la landing.
- Iniciar sesion con credenciales mock.
- Acceder al panel privado.
- Navegar desde el menu lateral a todos los modulos.
- Cerrar sesion.
- Bloquear rutas privadas si no hay sesion.

## Validacion manual

Probar estos casos:

1. Abrir `#/` y ver landing.
2. Pulsar Acceder a Clubox y ver login.
3. Entrar con credenciales incorrectas y ver error.
4. Entrar con credenciales correctas y ver dashboard.
5. Navegar a jugadores, equipos, contabilidad y resumen.
6. Cerrar sesion y volver a login.
7. Intentar abrir `#/app/dashboard` sin sesion y comprobar redireccion a login.
