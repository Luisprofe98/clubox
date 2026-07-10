# Flujo landing, login y aplicacion privada

## Objetivo

Implementar Clubox como una Single Page Application con Bootstrap y JavaScript modular.

La aplicacion debe separar claramente:

- Zona publica: landing y login.
- Zona privada: aplicacion de gestion del club.

La zona privada solo debe cargarse cuando exista una sesion activa.

## Flujo principal

```text
Landing publica
  -> Boton Acceder a Clubox
  -> Login
  -> Validacion de sesion
  -> App privada
  -> Menu lateral
  -> Carga dinamica de modulos
```

## Rutas principales

Usar rutas hash para simplificar el despliegue inicial.

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

## Regla de proteccion

Todas las rutas que empiecen por `/app` son privadas.

Si el usuario no tiene sesion activa, el router debe redirigir a:

```text
#/login
```

## Landing publica

La landing debe ser sencilla, clara y comercial.

Debe incluir:

- Nombre Clubox.
- Mensaje principal de gestion deportiva para clubes.
- Texto breve sobre centralizacion de formularios, jugadores, equipos, cuotas y contabilidad.
- Boton principal: Acceder a Clubox.
- Boton secundario opcional: Solicitar informacion.

No usar iconos.
No usar acentos en los textos de interfaz generados.
Usar Bootstrap para grid, botones, tarjetas y secciones.

## Login

El login debe ser una vista publica.

En esta primera version debe ser simulado con `sessionStorage`.

Credenciales mock recomendadas:

```text
Email: admin@clubox.local
Password: clubox123
```

Cuando el login sea correcto:

```js
sessionStorage.setItem("clubSession", "active");
```

Despues navegar a:

```text
#/app/dashboard
```

Cuando el login sea incorrecto, mostrar alerta Bootstrap con clase `failed`.

## App privada

La app privada debe cargar un layout fijo con:

- Menu lateral izquierdo.
- Cabecera superior simple.
- Area central de contenido.
- Boton para cerrar sesion.

El area central debe cargar la vista de cada modulo sin recargar la pagina completa.

## Cierre de sesion

Al cerrar sesion:

```js
sessionStorage.removeItem("clubSession");
```

Despues navegar a:

```text
#/login
```

## Menu lateral

El menu lateral debe estar construido con Bootstrap.

Debe usar `accordion` o `collapse`.

Secciones minimas:

### Inicio

- Dashboard

### Formularios

- Formularios creados
- Inscripciones recibidas

### Gestion deportiva

- Jugadores
- Equipos
- Cuerpo tecnico

### Contabilidad

- Registro de movimientos
- Resumen economico

### Cuotas y pagos

- Configuracion de cuotas
- Pagos

## Comportamiento de navegacion

Cada boton del menu debe tener un atributo `data-route`.

Ejemplo:

```html
<button class="btn btn-link w-100 text-start" data-route="/app/jugadores">
  Jugadores
</button>
```

El router debe capturar el click y cambiar el hash.

## Orden de implementacion para Codex

1. Crear el contenedor base en `index.html`.
2. Crear `app.js` para iniciar la SPA.
3. Crear `router.js` para controlar rutas.
4. Crear `auth.js` para sesion mock.
5. Crear `layout.js` para el layout privado.
6. Crear `landingView.js`.
7. Crear `loginView.js`.
8. Crear vistas placeholder para todos los modulos.
9. Conectar el menu lateral con el router.
10. Probar navegacion publica y privada.

## Resultado esperado

Al terminar esta fase debe existir una base navegable de Clubox donde:

- Al abrir la web se muestra la landing.
- El boton principal lleva al login.
- El login simulado permite entrar.
- La app privada muestra el menu lateral.
- Los modulos se cargan en el area principal.
- Las rutas privadas quedan protegidas.
- La estructura queda preparada para backend en Google Cloud.
