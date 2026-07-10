# Arquitectura SPA modular

## Objetivo
Crear una Single Page Application mantenible, modular y preparada para backend futuro en Google Cloud.

## Estructura recomendada

```text
/
  index.html
  README.md
  assets/
    css/
      styles.css
    js/
      main.js
      router.js
      config/
        appConfig.js
        appTheme.js
      state/
        appStore.js
      data/
        dataProvider.js
        localProvider.js
        cloudProvider.js
        mockData.js
      utils/
        dateUtils.js
        moneyUtils.js
        domUtils.js
        alertUtils.js
      modules/
        dashboard/
          dashboardView.js
        forms/
          formModel.js
          formRepo.js
          formService.js
          formView.js
          formValidator.js
        inscriptions/
          inscriptionModel.js
          inscriptionRepo.js
          inscriptionService.js
          inscriptionView.js
          inscriptionValidator.js
        sports/
          playerModel.js
          teamModel.js
          staffModel.js
          sportsRepo.js
          sportsService.js
          playerView.js
          teamView.js
          staffView.js
        accounting/
          movModel.js
          budgetModel.js
          accountRepo.js
          accountService.js
          movView.js
          summaryView.js
          accountValidator.js
        fees/
          feeModel.js
          feeRepo.js
          feeService.js
          feeView.js
```

## Router interno

Implementa hash routing simple:

```text
#dashboard
#forms
#inscriptions
#sports
#accounting
#fees
```

El router debe:

- Pintar la vista activa dentro de `#appRoot`.
- Actualizar navegacion activa.
- Mantener el estado de filtros por modulo si es razonable.
- No recargar pagina.

## Responsabilidades por capa

### View
Renderiza HTML, captura eventos, invoca servicios.

### Service
Aplica reglas de negocio, validaciones, calculos y operaciones compuestas.

### Repo
Lee y escribe datos usando dataProvider.

### Data provider
Implementa persistencia. Para MVP usar localStorage. Para Google Cloud dejar `cloudProvider.js` como adaptador pendiente.

### Utils
Funciones pequenas, puras y reutilizables.

## Arranque de aplicacion

`main.js` debe:

1. Cargar configuracion.
2. Inicializar dataProvider.
3. Cargar mock data si no existe data local.
4. Inicializar router.
5. Pintar vista inicial.

## Regla para HTML

`index.html` debe contener solo estructura base:

- Header.
- Navegacion principal.
- Contenedor `#appRoot`.
- Modal raiz opcional.
- Scripts.

Las vistas de cada modulo se generan desde archivos JS dedicados.

## Reglas de CSS

Todo el estilo custom debe estar en `assets/css/styles.css`.
Bootstrap resuelve la estructura. CSS custom solo debe cubrir:

- Branding.
- Espaciados concretos.
- Estados visuales de Clubox.
- Tablas responsivas.
- Ajustes de mobile.

## Persistencia temporal

Usar claves localStorage:

```text
clubox.forms
clubox.inscriptions
clubox.players
clubox.teams
clubox.staff
clubox.moves
clubox.budget
clubox.fees
```

No guardar blobs reales de documentos. Guardar solo metadata de documento.

## Preparacion Google Cloud

`cloudProvider.js` debe exponer las mismas funciones que `localProvider.js`:

```js
export async function getList(tipoClave) {}
export async function getItem(tipoClave, itemId) {}
export async function saveItem(tipoClave, itemDato) {}
export async function deleteItem(tipoClave, itemId) {}
```

No incluir credenciales reales ni claves de servicio.
