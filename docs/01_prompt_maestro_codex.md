# Prompt maestro para Codex

## Tarea
Implementa Clubox como Single Page Application modular usando HTML, CSS, JavaScript y Bootstrap 5. Usa este archivo y el resto de archivos markdown como contexto de producto, arquitectura y criterios de aceptacion.

## Comportamiento esperado de Codex

Antes de modificar codigo:

1. Inspecciona la estructura actual del repositorio.
2. Si ya existe una convencion de carpetas, respetala.
3. Si no existe, crea la estructura propuesta en `02_arquitectura_spa.md`.
4. No borres codigo existente sin justificarlo en el diff.
5. Implementa por pasos pequenos y verificables.

## Stack base

- HTML5.
- CSS3 con variables CSS.
- JavaScript modular ES Modules.
- Bootstrap 5 por CDN o dependencia ya existente.
- localStorage como persistencia temporal.
- dataProvider desacoplado para futura conexion con Google Cloud.

## Reglas de UI

- No usar iconos, emojis ni librerias de iconos.
- No usar acentos en textos visibles.
- Todos los textos de interfaz deben ser ASCII.
- Usar Bootstrap para layout, formularios, tablas, nav-tabs, cards, modals y alerts.
- Usar alert-success para succed, alert-warning para warning y alert-danger para failed.
- Si se necesita mantener el nombre literal `succed`, mapearlo internamente a Bootstrap success.
- Si se necesita mantener el nombre literal `failed`, mapearlo internamente a Bootstrap danger.

## Reglas de codigo

- Variables y funciones en lowerCamelCase.
- Maximo dos palabras descriptivas por identificador.
- Sin acentos, sin ene con tilde, sin espacios.
- Evitar abreviaturas oscuras.
- Evitar nombres genericos como data, item, temp si no hay contexto claro.
- Separar responsabilidades: view, service, repository, validator, state.
- No mezclar HTML largo dentro de main.js.
- No acceder a localStorage directamente desde vistas. Usar repositories.

## Reglas de datos

- Todas las entidades deben tener `id`, `clubId`, `createdAt`, `updatedAt` y `estado` cuando aplique.
- Los importes se guardan como numeros con dos decimales.
- Fechas en ISO `YYYY-MM-DD` para formularios y filtros.
- No exponer datos sensibles en console.log.
- Documentos adjuntos se simularan con metadata hasta tener almacenamiento cloud.

## Entregable esperado

Codex debe dejar el proyecto con:

- `index.html` como entrada unica.
- `assets/css/styles.css` con branding y ajustes.
- `assets/js/main.js` como arranque.
- Modulos JS separados por dominio.
- Mock data inicial suficiente para navegar.
- README o nota tecnica con instrucciones de ejecucion local si no existe.

## Criterio de cierre

La SPA debe permitir navegar por:

- Dashboard.
- Formularios.
- Inscripciones.
- Gestion deportiva.
- Contabilidad.
- Cuotas y pagos como pantalla preparada.

Sin errores de consola en navegacion basica.
