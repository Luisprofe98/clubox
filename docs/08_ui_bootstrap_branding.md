# UI, Bootstrap y branding Clubox

## Objetivo visual
Crear una interfaz profesional, simple y fiable, orientada a directivos de clubes deportivos.

## Paleta
Usar colores CSS globales:

```css
:root {
  --clubox-primary: #6e1028;
  --clubox-secondary: #9c1b3d;
  --clubox-dark: #111111;
  --clubox-light: #ffffff;
  --clubox-muted: #f5f2f3;
  --clubox-border: #e6dde0;
  --clubox-success: #198754;
  --clubox-warning: #ffc107;
  --clubox-failed: #dc3545;
}
```

## Bootstrap
Usar Bootstrap para:

- Container.
- Row y col.
- Navbar.
- Nav tabs.
- Cards.
- Tables.
- Forms.
- Modals.
- Alerts.
- Badges.
- Buttons.

## Alertas
Crear helper `alertUtils.js`.

Tipos del producto:

```js
const avisoMapa = {
  succed: "alert-success",
  warning: "alert-warning",
  failed: "alert-danger"
};
```

Nota: se mantiene `succed` por requisito de producto aunque Bootstrap use `success`.

## Componentes visuales

### Header
Debe incluir:

- Nombre Clubox.
- Navegacion principal.
- Club activo si existe.

### Dashboard
Mostrar cards de acceso rapido:

- Formularios.
- Inscripciones.
- Gestion deportiva.
- Contabilidad.
- Cuotas.

No usar iconos. Usar solo texto y numeros.

### Tablas

- Usar `table table-hover align-middle`.
- En mobile envolver con `table-responsive`.
- Acciones como botones de texto: `Ver`, `Editar`, `Eliminar`.

### Botones

- Principal: fondo burdeo.
- Secundario: borde burdeo.
- Acciones peligrosas: Bootstrap danger.
- Boton alta: `+ Nuevo ...`.

### Estados

- activo: badge success.
- inactivo: badge secondary.
- recibida: badge warning.
- aprobada: badge success.
- rechazada: badge danger.

## CSS base sugerido

```css
body {
  background: var(--clubox-muted);
  color: var(--clubox-dark);
}

.app-shell {
  min-height: 100vh;
}

.btn-clubox {
  background: var(--clubox-primary);
  border-color: var(--clubox-primary);
  color: var(--clubox-light);
}

.btn-clubox:hover {
  background: var(--clubox-secondary);
  border-color: var(--clubox-secondary);
  color: var(--clubox-light);
}

.card-clubox {
  border: 1px solid var(--clubox-border);
  border-radius: 1rem;
}

.text-income {
  color: var(--clubox-success);
}

.text-expense {
  color: var(--clubox-failed);
}
```

## Textos sin acentos

Ejemplos correctos:

- Gestion deportiva.
- Inscripcion recibida.
- Cuerpo tecnico.
- Ano nacimiento.
- Direccion.
- Telefono.
- Resumen economico.
- Exportacion pendiente.

Ejemplos incorrectos:

- Gestion deportiva con acento.
- Inscripcion con acento.
- Ano nacimiento.
- Direccion con acento.

## Prohibiciones

- No usar emojis.
- No usar Font Awesome.
- No usar Bootstrap Icons.
- No usar imagenes como iconos.
- No usar acentos en UI.
- No incluir logo si no existe archivo en repo.
