# Estandares de codigo para Clubox

## Nombres

Usar lowerCamelCase.
Maximo dos palabras por identificador.
Sin acentos ni caracteres especiales.

Correcto:

```js
const jugadorLista = [];
const equipoActivo = null;
const movFiltro = {};
function guardarMov() {}
function cargarEquipo() {}
function filtrarJugadores() {}
```

Incorrecto:

```js
const listaCompletaDeJugadores = [];
const movimientoEconomicoActual = {};
function renderAccountingSummary() {}
function obtenerTodosLosJugadoresActivos() {}
```

## Excepcion controlada
Los nombres de entidades pueden ser claros aunque sean largos si son modelos de dominio. Aun asi, evitar mas de dos palabras en variables locales.

## Separacion de capas

No hacer esto:

- View accede directamente a localStorage.
- View calcula toda la logica economica.
- main.js contiene todos los modulos.

Hacer esto:

- View captura eventos y muestra UI.
- Service valida y calcula.
- Repo persiste.
- Provider implementa origen de datos.

## Funciones asincronas
Todas las operaciones de repo y service que lean datos deben ser async, aunque ahora usen localStorage. Esto facilita migrar a Google Cloud.

Ejemplo:

```js
export async function listarMov() {
  return accountRepo.listarMov();
}
```

## Validacion
Cada modulo debe tener validator propio.

Ejemplos:

- formValidator.js.
- inscriptionValidator.js.
- accountValidator.js.

Las validaciones devuelven estructura simple:

```js
{
  valido: true,
  errorLista: []
}
```

## Money utils
Crear `moneyUtils.js` con:

- normalizarImporte.
- formatoEuros.
- sumarImporte.

Reglas:

- Guardar numero positivo.
- Mostrar dos decimales.
- Mostrar moneda como `EUR`.

## Date utils
Crear `dateUtils.js` con:

- fechaHoy.
- fechaIso.
- filtrarMes.
- filtrarTrimestre.
- obtenerAno.

## Alert utils
Crear `alertUtils.js` con:

- mostrarAviso.
- limpiarAviso.

Tipos:

- succed.
- warning.
- failed.

## Accesibilidad basica

- Labels asociados a inputs.
- Botones con texto claro.
- Contraste suficiente.
- Navegacion por teclado en modals.
- Tablas con thead.

## Seguridad basica

- No guardar claves de Google Cloud.
- No incluir credenciales en codigo.
- No hacer console.log de DNI, IBAN o documentos.
- Sanear textos antes de insertarlos como HTML.
- Preferir textContent cuando se escriben valores de usuario.

## Definition of done tecnico

- Sin errores de consola en navegacion basica.
- Sin acentos en UI.
- Sin iconos.
- Archivos separados.
- Modulos importables.
- Mock data visible.
- Capa cloudProvider creada como stub.
- README actualizado si procede.
